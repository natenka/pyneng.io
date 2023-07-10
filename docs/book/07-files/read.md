# Читання файлів

У Python є кілька методів читання файлу:

* `read` - зчитує вміст файлу в рядок
* `readline` - зчитує один рядок
* `readlines` - зчитує рядки файлу та створює список із рядків


## read

Метод read – зчитує весь файл в один рядок.

Приклад використання методу read:

```python
In [1]: f = open('r1.txt')

In [2]: f.read()
Out[2]: '!\nservice timestamps debug datetime msec localtime show-timezone year\nservice timestamps log datetime msec localtime show-timezone year\nservice password-encryption\nservice sequence-numbers\n!\nno ip domain lookup\n!\nip ssh version 2\n!\n'

In [3]: f.read()
Out[3]: ''
```

При повторному читанні файлу в 3 рядку відображається порожній рядок. Так
відбувається через те, що при виклик методу read, зчитується весь файл. І після
того, як файл було зчитано, курсор залишається в кінці файлу. Керувати
положенням курсору можна за допомогою методу seek.


## readline

Файл можна читати рядок за рядком за допомогою методу `readline`:

```python
In [4]: f = open('r1.txt')

In [5]: f.readline()
Out[5]: '!\n'

In [6]: f.readline()
Out[6]: 'service timestamps debug datetime msec localtime show-timezone year\n'
```

Но чаще всего проще пройтись по объекту file в цикле, не используя
методы ``read...``:

```python
In [7]: f = open('r1.txt')

In [8]: for line in f:
   ...:     print(line.rstrip())
   ...:
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

``readlines``
^^^^^^^^^^^^^^^

Еще один полезный метод - ``readlines``. Он считывает строки файла в
список:

```python
In [9]: f = open('r1.txt')

In [10]: f.readlines()
Out[10]:
['!\n',
 'service timestamps debug datetime msec localtime show-timezone year\n',
 'service timestamps log datetime msec localtime show-timezone year\n',
 'service password-encryption\n',
 'service sequence-numbers\n',
 '!\n',
 'no ip domain lookup\n',
 '!\n',
 'ip ssh version 2\n',
 '!\n']
```

Если нужно получить строки файла, но без перевода строки в конце, можно
воспользоваться методом ``split`` и как разделитель, указать символ
``\n``:

```python
In [11]: f = open('r1.txt')

In [12]: f.read().split('\n')
Out[12]:
['!',
 'service timestamps debug datetime msec localtime show-timezone year',
 'service timestamps log datetime msec localtime show-timezone year',
 'service password-encryption',
 'service sequence-numbers',
 '!',
 'no ip domain lookup',
 '!',
 'ip ssh version 2',
 '!',
 '']
```

Обратите внимание, что последний элемент списка - пустая строка.

Если перед выполнением ``split``, воспользоваться методом
``rstrip``, список будет без пустой строки в конце:

```python

In [13]: f = open('r1.txt')

In [14]: f.read().rstrip().split('\n')
Out[14]:
['!',
 'service timestamps debug datetime msec localtime show-timezone year',
 'service timestamps log datetime msec localtime show-timezone year',
 'service password-encryption',
 'service sequence-numbers',
 '!',
 'no ip domain lookup',
 '!',
 'ip ssh version 2',
 '!']
```

``seek``
^^^^^^^^^^

До сих пор, файл каждый раз приходилось открывать заново, чтобы снова
его считать. Так происходит из-за того, что после методов чтения, курсор
находится в конце файла. И повторное чтение возвращает пустую строку.

Чтобы ещё раз считать информацию из файла, нужно воспользоваться методом
``seek``, который перемещает курсор в необходимое положение.

Пример открытия файла и считывания содержимого:

```python
In [15]: f = open('r1.txt')

In [16]: print(f.read())
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

Если вызывать ещё раз метод ``read``, возвращается пустая строка:

```python
In [17]: print(f.read())
```

Но с помощью метода ``seek`` можно перейти в начало файла (0 означает
начало файла):

```python
In [18]: f.seek(0)
```

После того как с помощью ``seek`` курсор был переведен в начало
файла, можно опять считывать содержимое:

```python
In [19]: print(f.read())
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
