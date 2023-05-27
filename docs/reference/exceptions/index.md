# Винятки

## Вбудовані винятки

Тут розглядаються кілька винятків які будуть часто генеруватися, в тому числі
через помилки в коді.  Опис винятків спрощений, за повною інформацією та описом
звертайтесь до [документації](https://docs.python.org/3/library/exceptions.html).

### TypeError

Цей виняток генерується, коли операція або функція застосована до об'єкта невідповідного типу.

Наприклад, функція len не працює з типом int:

```python
In [1]: len(100)
--------------------------------------------------------------------------
TypeError                                Traceback (most recent call last)
Cell In[1], line 1
----> 1 len(100)

TypeError: object of type 'int' has no len()
```

Також функція len очікує тільки один аргумент, а тут передані два:

```python
In [2]: len("hello", "test")
--------------------------------------------------------------------------
TypeError                                Traceback (most recent call last)
Cell In[2], line 1
----> 1 len("hello", "test")

TypeError: len() takes exactly one argument (2 given)
```

Приклад для операцій:

```python
In [1]: 100 + "test"
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[1], line 1
----> 1 100 + "test"

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

### ValueError

Генерується, коли операція або функція отримує аргумент, який має правильний
тип, але невідповідне значення.


Наприклад, функція int може виконувати конвертацію із рядка в число:
```python
In [3]: int("100")
Out[3]: 100
```

Але якщо передати int рядок, який вона не може конвертувати в десяткове число
(за замовчуванням), згенерується виняток ValueError:
```python
In [4]: int("ff")
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Cell In[4], line 1
----> 1 int("ff")

ValueError: invalid literal for int() with base 10: 'ff'
```

Із вказанням додаткового параметру, можна вказати, що конвертація буде із
шістнадцяткового формату:
```python
In [5]: int("ff", 16)
Out[5]: 255
```

### AttributeError

Генерується, коли код звертається до атрибута, якого немає в об'єкті.

Часто AttributeError генерується, коли очікується, що вираз повертає
об'єкт, а він повертає, наприклад, None.

Метод append повертає None, оскільки він змінює сам список vlans, а не створює
новий. Але якщо випадково подумати, що він повертає новий список і записати
його у змінну result.

```python
In [3]: vlans = [1, 2, 3]

In [4]: result = vlans.append(100)
```

Наступна операція зі змінною в якій має бути список, сгенерує виняток
AttributeError (через те що в result насправді None):
```python
In [5]: result.append(200)
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
Cell In[5], line 1
----> 1 result.append(200)

AttributeError: 'NoneType' object has no attribute 'append'

In [6]: print(result)
None
```


### TabError

Генерується, коли в коді для відступу використовуються і табуляція, і пробіл
(мова саме про символи).

```python
TabError: inconsistent use of tabs and spaces in indentation
```

Виправити ситуацію можна заміною символу табуляції 4 пробілами.


### IndentationError

Генерується у випадку виникнення синтаксичних помилок, пов’язаних із
неправильним відступом.

Код і відповідна помилка при виконанні:

```python
for i in range(10):
    print(i)
  print(i)

IndentationError: unindent does not match any outer indentation level
```

Код і відповідна помилка при виконанні:

```python
for i in range(10):
print(i)
    print(i)

IndentationError: expected an indented block after 'for' statement on line 2
```

### SyntaxError

Генерується у випадку виникнення синтаксичних помилок.

```python
    for i in range(10)
                      ^
SyntaxError: expected ':'
```

