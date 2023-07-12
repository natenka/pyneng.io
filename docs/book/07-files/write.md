# Запис файлів

При записі дуже важливо визначитися з режимом відкриття файлу, щоб випадково
не видалити вміст файлу:

* `w` - відкрити файл для запису. Якщо файл існує, то його вміст видаляється
* `a` - відкрити файл для доповнення запису. Дані додаються в кінці файлу
* `x` - відкрити файл для запису. Якщо файл існує, запис не виконується

Всі режими створюють файл, якщо він не існує.

Для запису в файл використовуються такі методи:

* write - записати один рядок у файл
* writelines - дозволяє передавати список рядків як аргумент

## write

Метод write очікує рядок для запису.

Наприклад, візьмемо список рядків:

```python
lines = ["line1\n", "line2\n", "line3\n"]
```

Відкриття файлу new_data.txt в режимі запису:

```python
In [18]: f = open('new_data.txt', "w")

```

Перетворюємо список команд в один рядок за допомогою [join](/reference/string/methods/join/):

```python
In [21]: lines_as_string = ''.join(lines)

In [22]: lines_as_string
Out[22]: 'line1\nline2\nline3\n'
```

Запис рядка у файл:

```python
In [23]: f.write(lines_as_string)
Out[23]: 18
```

Після завершення роботи з файлом його необхідно закрити:
```python
In [25]: f.close()

In [26]: cat new_data.txt # (1)
line1
line2
line3
```

1. Оскільки ipython підтримує команду cat, можна переглянути вміст файлу `cat new_data.txt`


## writelines

Метод ``writelines`` ожидает список строк, как аргумент.

Запись списка строк cfg_lines в файл:

```python

In [1]: cfg_lines = ['!',
   ...:  'service timestamps debug datetime msec localtime show-timezone year',
   ...:  'service timestamps log datetime msec localtime show-timezone year',
   ...:  'service password-encryption',
   ...:  'service sequence-numbers',
   ...:  '!',
   ...:  'no ip domain lookup',
   ...:  '!',
   ...:  'ip ssh version 2',
   ...:  '!']

In [9]: f = open('r2.txt', 'w')

In [10]: f.writelines(cfg_lines)

In [11]: f.close()

In [12]: cat r2.txt
!service timestamps debug datetime msec localtime show-timezone yearservice timestamps log datetime msec localtime show-timezone yearservice password-encryptionservice sequence-numbers!no ip domain lookup!ip ssh version 2!
```

В результате все строки из списка записались в одну строку файла, так
как в конце строк не было символа ``\n``.

Добавить перевод строки можно по-разному.
Например, можно просто обработать список в цикле:

```python

In [13]: cfg_lines2 = []

In [14]: for line in cfg_lines:
   ....:     cfg_lines2.append(line + '\n')
   ....:

In [15]: cfg_lines2
Out[15]:
['!\n',
 'service timestamps debug datetime msec localtime show-timezone year\n',
 'service timestamps log datetime msec localtime show-timezone year\n',
 'service password-encryption\n',
 'service sequence-numbers\n',
 '!\n',
 'no ip domain lookup\n',
 '!\n',
 'ip ssh version 2\n',
```

Если итоговый список записать заново в файл, то в нём уже
будут переводы строк:

```python

In [18]: f = open('r2.txt', 'w')

In [19]: f.writelines(cfg_lines2)

In [20]: f.close()

In [21]: cat r2.txt
!
service timestamps debug datetime msec localtime show-timezone year
service timestamps log datetime msec localtime show-timezone year
service password-encryption
service sequence-numbers
!
no ip domain lookup
!
ip ssh version 2
!
```
