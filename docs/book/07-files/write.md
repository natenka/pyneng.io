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
In [1]: f = open('new_data.txt', "w")

```

Перетворюємо список команд в один рядок за допомогою [join](/reference/string/methods/join/):

```python
In [2]: lines_as_string = ''.join(lines)

In [3]: lines_as_string
Out[3]: 'line1\nline2\nline3\n'
```

Запис рядка у файл:

```python
In [4]: f.write(lines_as_string)
Out[4]: 18
```

Після завершення роботи з файлом його необхідно закрити:
```python
In [5]: f.close()

In [6]: cat new_data.txt # (1)
line1
line2
line3
```

1. Оскільки ipython підтримує команду cat, можна переглянути вміст файлу `cat new_data.txt`


## writelines


Метод writelines очікує як аргумент ітерований об'єкт з рядками.
Запис списку рядків lines у файл:

```python
In [1]: lines = ["line1\n", "line2\n", "line3\n"] # (1)

In [3]: f = open('new_data.txt', "w")

In [5]: f.writelines(lines)

In [6]: f.close()

In [7]: cat new_data.txt
line1
line2
line3
```

1. Метод writelines не додає символ нового рядка, тому кожен рядок має бути з потрібним символом нового рядка.

## режим `a`

Якщо відкрити файл у режимі `a`, файл буде відкритий для доповнення запису. Дані додаються в кінці файлу:

```python
In [1]: lines = ["line1\n", "line2\n", "line3\n"]

In [2]: f = open('new_data.txt', "a")

In [4]: f.writelines(["line4\n", "line5\n"])

In [5]: f.close()

In [6]: cat new_data.txt
line1
line2
line3
line4
line5
```

## режим `x`

Якщо у режимі `x` відкрити існуючий файл, виникне виняток FileExistsError:

```python
In [1]: f = open('new_data.txt', "x")
---------------------------------------------------------------------------
FileExistsError                           Traceback (most recent call last)
Cell In[1], line 1
----> 1 f = open('new_data.txt', "x")
...

FileExistsError: [Errno 17] File exists: 'new_data.txt'
```

З новим файлом такої проблеми не буде і дані додаються як в режимі `w`:
```python
In [8]: f = open('new_data_x.txt', "x")

In [9]: lines = ["line1\n", "line2\n", "line3\n"]

In [10]: f.writelines(lines)

In [11]: f.close()
```

