# Поширені проблеми/нюанси роботи з функціями

## Список/словарь в который собираются данные в функции, создан за пределами функции

Очень часто в решении заданий встречается такой нюанс: функция должна собрать какие-то данные в список/словарь
и список создан вне функции. Тогда вроде как функция работает правильно,
но при этом тест не проходит. Это происходит потому что в таком варианте функция
работает неправильно и каждый вызов добавляет элементы в тот же список:

```python
result = []

def func(items):
    for i in items:
        result.append(i*100)
    return result


In [3]: func([1, 2, 3])
Out[3]: [100, 200, 300]

In [4]: func([7, 8])
Out[4]: [100, 200, 300, 700, 800]
```

Исправить это можно переносом строки создания списка в функцию:

```python
def func(items):
    result = []
    for i in items:
        result.append(i*100)
    return result


In [21]: func([1, 2, 3])
Out[21]: [100, 200, 300]

In [22]: func([7, 8])
Out[22]: [700, 800]
```

Всё, что относится к функции лучше всегда писать внутри функции.
Тест тут не проходит потому что внутри файла задания функция вызывается первый
раз - всё правильно, а потом тест вызывает её второй раз и там вдруг в два раза больше данных чем нужно.

## Значения по умолчанию в параметрах создаются во время создания функции

Пример функции, которая должна выводить текущую дату и время при каждом вызове:

```python
from datetime import datetime
import time

def print_current_datetime(ptime=datetime.now()):
    print(f">>> {ptime}")


for i in range(3):
    print("Имитируем долгое выполнение...")
    time.sleep(1)
    print_current_datetime()

Имитируем долгое выполнение...
>>> 2021-02-23 09:01:49.845425
Имитируем долгое выполнение...
>>> 2021-02-23 09:01:49.845425
Имитируем долгое выполнение...
>>> 2021-02-23 09:01:49.845425
```

Так как ``datetime.now()`` указано в значении по умолчанию,
это значение создается во время создания функции и в итоге при каждом вызове
время одно и то же. Для корректного вывода, надо вызывать ``datetime.now()``
в теле функции:

```python
def print_current_datetime():
    print(f">>> {datetime.now()}")
```


Второй пример где этот нюанс может привести к неожиданным результатам,
если о нем не знать - изменяемые типы данных в значении по умолчанию.

Например, использование списка в значении по умолчанию:

```python
def add_item(item, data=[]):
    data.append(item)
    return data
```

В этом случае список data создается один раз - при создании функции и
при вызове функции, данные добавляются в один и тот же список.
В итоге все повторные вызовы будут добавлять элементы:

```python
In [16]: add_item(1)
Out[16]: [1]

In [17]: add_item(2)
Out[17]: [1, 2]

In [18]: add_item(4)
Out[18]: [1, 2, 4]
```

Если нужно сделать так, чтобы параметр data был необязательным и по умолчанию
создавался пустой список, надо сделать так:

```python
def add_item(item, data=None):
    if data is None:
        data = []
    data.append(item)
    return data


In [23]: add_item(1)
Out[23]: [1]

In [24]: add_item(2)
Out[24]: [2]
```

## Ошибка UnboundLocalError: local variable referenced before assignment

Ошибка может возникнуть в таких случаях:

* обращение к переменной в функции идет до ее создания - это может быть
случайность (ошибка) или следствие того, что какое-то условие не выполнилось
* обращение внутри функции к глобальной переменной, но при этом внутри функции
создана такая же переменная позже

Первый случай - обратились к переменной до ее создания:

```python
def f():
    print(b)
    b = 55

In [6]: f()
---------------------------------------------------------------------------
UnboundLocalError                         Traceback (most recent call last)
Input In [6], in <cell line: 1>()
----> 1 f()

Input In [5], in f()
      1 def f():
----> 2     print(b)
      3     b = 55

UnboundLocalError: local variable 'b' referenced before assignment
```

Переменная создается в условии, а условие не выполнилось:

```python
def f():
    if 5 > 8:
        b = 55
    print(b)

In [8]: f()
---------------------------------------------------------------------------
UnboundLocalError                         Traceback (most recent call last)
Input In [8], in <cell line: 1>()
----> 1 f()

Input In [7], in f()
      2 if 5 > 8:
      3     b = 55
----> 4 print(b)

UnboundLocalError: local variable 'b' referenced before assignment
```

Имя глобальной и локальной переменной одинаковое и внутри функции сначала идет
попытка обращения к глобальной, потом создание локальной:

```python
a = 10

def f():
    print(a)
    a = 55
    print(a)


In [4]: f()
---------------------------------------------------------------------------
UnboundLocalError                         Traceback (most recent call last)
Input In [4], in <cell line: 1>()
----> 1 f()

Input In [3], in f()
      1 def f():
----> 2     print(a)
      3     a = 55
      4     print(a)

UnboundLocalError: local variable 'a' referenced before assignment
```


Python должен определить область видимости переменной. И в случае функций, Python
считает, что переменная локальная, если она создана внутри функции.
На момент когда мы доходим до вызова функции, Python уже решил, что ``a`` это
локальная переменная и именно из-за этого первая строка ``print(a)`` дает ошибку.
