# Читання файлів

У Python є кілька методів читання файлу:

* `read` - зчитує вміст файлу в рядок
* `readline` - зчитує один рядок
* `readlines` - зчитує рядки файлу та створює список із рядків


## Робота із файлом в циклі for

Найпоширеніший варіант роботи з файлом – використання об'єкту file у циклі for:

=== "Приклад роботи із файлом в циклі for"

    В цьому випадку файл читається рядок за рядком, отримуючи новий рядок на
    кожній ітерації циклу for:

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
    In [1]: f = open('data.txt')

    In [2]: f.read()
    Out[2]: 'line1\nline2\nline3\nline4\nline5\nline6\nline7\n'

    In [3]: f.read() # (1)
    Out[3]: ''
    ```

    1. При повторному читанні файлу в 3 рядку відображається порожній рядок. Так
       відбувається через те, що після першого виклику методу read, зчитується весь файл. І після
       того, як файл було зчитано, курсор залишається в кінці файлу. Керувати
       положенням курсору можна за допомогою методу [seek](/book/07-files/read/#seek).


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



## readline

Файл можна читати рядок за рядком за допомогою методу `readline`.

=== "readline"

    Кожен виклик методу readline, читає наступний рядок файлу. Коли рядки
    закінчуються, readline повертає порожній рядок:

    ```python
	In [1]: f = open('data.txt')

	In [2]: f.readline()
	Out[2]: 'line1\n'

	In [3]: f.readline()
	Out[3]: 'line2\n'

	In [4]: f.readline()
	Out[4]: 'line3\n'

	In [5]: f.readline()
	Out[5]: ''

	In [6]: f.readline()
	Out[6]: ''
    ```

=== "Файл data.txt"

    ```
    line1
    line2
    line3
    ```

## readlines

=== "readlines"

	Метод readlines зчитує рядки файлу до списку:

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
In [2]: f = open('data.txt')

In [3]: f.read().split('\n')
Out[3]: ['line1', 'line2', 'line3', 'line4', 'line5', 'line6', 'line7', '']
```

Зауважте, що останній елемент списку - порожній рядок.  Якщо перед виконанням
split, скористатися методом rstrip, список буде без порожнього рядка
наприкінці:

```python
In [5]: f = open('data.txt')

In [6]: f.read().strip().split('\n')
Out[6]: ['line1', 'line2', 'line3', 'line4', 'line5', 'line6', 'line7']
```

Або скористатися методом рядків splitlines:

```python
In [11]: f = open('data.txt')

In [12]: f.read().splitlines()
Out[12]: ['line1', 'line2', 'line3', 'line4', 'line5', 'line6', 'line7']
```

## seek

Досі файл щоразу доводилося відкривати заново, щоб прочитати його знову.  Так
відбувається через те, що після методів читання курсор знаходиться в кінці
файлу. І повторне читання повертає порожній рядок.

Щоб знову прочитати інформацію з файлу, потрібно скористатися методом seek,
який переміщує курсор у потрібне положення.

Приклад відкриття файлу та читання вмісту:

```python
In [13]: f = open('data.txt')

In [14]: f.read()
Out[14]: 'line1\nline2\nline3\nline4\nline5\nline6\nline7\n'
```

Якщо викликати ще раз метод read, повертається порожній рядок:

```python
In [15]: f.read()
Out[15]: ''
```

За допомогою методу seek можна перейти на початок файлу (0 означає початок файлу):

```python
In [16]: f.seek(0)
Out[16]: 0
```

Після того, як за допомогою seek курсор був переведений на початок файлу, можна
знову зчитувати вміст:

```python
In [17]: f.read()
Out[17]: 'line1\nline2\nline3\nline4\nline5\nline6\nline7\n'
```
