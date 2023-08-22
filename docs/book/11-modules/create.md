# Приклад імпорту

Приклад створення своїх модулів та імпорту функції з одного модуля до іншого.

Файл examples_01_sum_numbers.py:

```python
def sum_numbers(num1, num2):
    return num1 + num2


print("Start")
res1 = sum_numbers(100, 200)
print(f"{res1=}")
print("Stop")
```


Якщо запустити скрипт examples_01_sum_numbers.py вивід буде таким:

```
$ python examples_01_sum_numbers.py
Start
res1=300
Stop
```

Другий скрипт імпортує функцію sum_numbers та використовує її:

```python
from examples_01_sum_numbers import sum_numbers


numbers = [1, 2, 3]
for num in numbers:
    print(sum_numbers(100, num))
```

Результат виконання скрипту:

```
$ python examples_02_import_sum_numbers.py
Start
res1=300
res2=30
Stop
101
102
103
```

Зверніть увагу, що виведено не лише інформацію зі скрипту
examples_01_sum_numbers.py, але й інформацію зі скрипту
examples_02_import_sum_numbers.py. Так відбувається через те, що будь-який
різновид import виконує весь скрипт. Тобто навіть коли імпорт виглядає як `from
examples_01_sum_numbers import sum_numbers`, виконується весь скрипт
examples_01_sum_numbers.py, а не тільки функція sum_numbers. У результаті
будуть виводитися всі повідомлення скрипту, що імпортується.

У цьому випадку функція не виконує довгих обчислень, тому цей вивід впливає
лише на зручність використання. Однак у ситуації, коли замість sum_numbers буде
якась функція, що підключається до обладнання або щось подібне, що довго
виконується, це вже вплине на код, який імпортує функцію.


В Python можна вказати, що деякі рядки не повинні виконуватися при імпорті. Про це
у наступному підрозділі.
