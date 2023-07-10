# Читання файлів

У Python є кілька методів читання файлу:

* `read` - зчитує вміст файлу в рядок
* `readline` - зчитує один рядок
* `readlines` - зчитує рядки файлу та створює список із рядків


## Робота із файлом в циклі for

Найпоширеніший варіант роботи з файлом – пройтися по об'єкту file у циклі:

=== "Приклад роботи із файлом в циклі for"

    ```python
    In [1]: from pprint import pprint

    In [2]: f = open('data.txt')

    In [3]: for line in f:
       ...:     pprint(line)
       ...:
    'line1\n'
    'line2\n'
    'line3\n'
    'line4\n'
    'line5\n'
    'line6\n'
    'line7\n'
    ```

=== "Файл data.txt"

    ```
    line1
    line2
    line3
    line4
    line5
    line6
    line7
    ```

## read

Метод read – зчитує весь файл в один рядок.

=== "read"

    Приклад використання методу read:

    ```python
    In [4]: f = open('data.txt')

    In [5]: f.read()
    Out[5]: 'line1\nline2\nline3\nline4\nline5\nline6\nline7\n'

    In [6]: f.read()
    Out[6]: ''
    ```

=== "Файл data.txt"

    ```
    line1
    line2
    line3
    line4
    line5
    line6
    line7
    ```


При повторному читанні файлу в 3 рядку відображається порожній рядок. Так
відбувається через те, що при виклик методу read, зчитується весь файл. І після
того, як файл було зчитано, курсор залишається в кінці файлу. Керувати
положенням курсору можна за допомогою методу seek.


## readline

=== "readline"

    Файл можна читати рядок за рядком за допомогою методу `readline`:

    ```python
    In [8]: f = open('data.txt')

    In [9]: f.readline()
    Out[9]: 'line1\n'

    In [10]: f.readline()
    Out[10]: 'line2\n'
    ```

=== "Файл data.txt"

    ```
    line1
    line2
    line3
    line4
    line5
    line6
    line7
    ```

## readlines

=== "readlines"

    Ще один корисний метод - readlines. Він зчитує рядки файлу до списку:

    ```python
    In [6]: f = open('data.txt')

    In [7]: f.readlines()
    Out[7]: ['line1\n', 'line2\n', 'line3\n', 'line4\n', 'line5\n', 'line6\n', 'line7\n']
    ```

=== "Файл data.txt"

    ```
    line1
    line2
    line3
    line4
    line5
    line6
    line7
    ```

Якщо потрібно отримати рядки файлу, але без перекладу рядка в кінці, можна
скористатися методом split і як роздільник вказати символ `\n`:

```python
In [11]: f = open('data.txt')

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

Зауважте, що останній елемент списку - порожній рядок.
Якщо перед виконанням split, скористатися методом rstrip, список буде без
порожнього рядка наприкінці:

```python

In [13]: f = open('data.txt')

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

## seek

Досі файл щоразу доводилося відкривати заново, щоб прочитати його знову.  Так
відбувається через те, що після методів читання курсор знаходиться в кінці
файлу. І повторне читання повертає порожній рядок.

Щоб знову прочитати інформацію з файлу, потрібно скористатися методом seek,
який переміщує курсор у потрібне положення.

Приклад відкриття файлу та читання вмісту:

```python
In [15]: f = open('data.txt')

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

Якщо викликати ще раз метод read, повертається порожній рядок:

```python
In [17]: print(f.read())
```

За допомогою методу seek можна перейти на початок файлу (0 означає початок файлу):

```python
In [18]: f.seek(0)
```

Після того, як за допомогою seek курсор був переведений на початок файлу, можна
знову зчитувати вміст:

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
