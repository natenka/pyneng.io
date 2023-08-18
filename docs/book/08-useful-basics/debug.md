# Налагодження коду

Налагодження коду це складний процес, який навіть із досвідом залишається
складним. Спростити його можна, вивчивши доступні інструменти для налагодження.

Глобально, можна сказати, є два варіанти налагодження:

* додаємо print у якомусь вигляді
* використовуємо налагоджувач (debugger)

Обидва варіанти можна використовувати і звичайно при використанні налагоджувача
набагато більше можливостей, але при цьому треба витратити час на вивчення
самого налагоджувача.

Також хочеться виділити окремо налагодження для вивчення Python. Тобто коли ви
використовуєте якийсь налагоджувач та/або print не тому, що код не працює, а тому
що ви намагаєтеся зрозуміти, що відбувається в коді в той чи інший момент.

Для вивчення Python підходять:

* [сайт pythontutor](https://pythontutor.com/)
* налагоджувач у редакторах для початківців: [Thonny](https://thonny.org/), [Mu](https://codewith.mu/) 
* print, pprint
* якщо досвід у програмуванні вже є, також підійдуть налагоджувачі в IDE

!!! tip "[Цей розділ в форматі відео](https://pyneng.io/course/topics/debug)"


## Налагоджувач

Налагоджувач (debugger) — це окремий модуль, програмне забезпечення або частина
редактора/IDE, що дозволяє налагоджувати код.

Приклади налагоджувачів і редакторів із налагоджувачами:

* [сайт pythontutor](https://pythontutor.com/)
* [pdb](https://docs.python.org/3/library/pdb.html) - модуль стандартної бібліотеки Python (є багато варіантів pdbr, ipdb, pdbpp)
* [Thonny](https://thonny.org/)
* [Mu](https://codewith.mu/)
* [PyCharm](https://www.jetbrains.com/pycharm/)
* [VS Code](https://code.visualstudio.com/)

### Налагодження за допомогою print та різновидів

Налагодження за допомогою print зазвичай полягає в тому, що в незрозумілих
місцях коду або перед рядком з помилкою, додається print в якомусь вигляді.

### print vs pprint vs ``print(f"{value=}")``

Звичайний print з виведенням значень змінних не завжди найкращий вибір, тому
що, наприклад, print однаково виводить рядок `"100"` та число `100`.

```python
In [1]: print("100")
100

In [2]: print(100)
100
```

Тут може бути зручніше pprint, який виводить рядки з лапками, а числа без:

```python
In [3]: from pprint import pprint

In [5]: pprint("100")
'100'

In [6]: pprint(100)
100
```

Також pprint зручний для виведення складніших рядків, оскільки він показує
спеціальні символи:

```python
In [7]: line = "\nline1\t\nline2\r\n"

In [8]: print(line)

line1
line2


In [9]: pprint(line)
'\nline1\t\nline2\r\n'
```

Можна вивести такий самий рядок з print, якщо використовувати repr разом із print:

```python
In [11]: print(repr(line))
'\n\nline1\t\nline2\r\n'
```

Мінус pprint в тому, що він може виводити лише одне значення, тобто не можна
зробити як з print, виведення кількох змінних. Плюс у тому, що pprint
також вміє виводить складніші структури даних із зрозумілим форматуванням, а
також дає можливість вказувати "глибину" даних, яку треба показувати.

Також, починаючи з версії 3.8, у Python з'явився спеціальний різновид виведення
у f-рядках, саме для налагодження - `f"{var=}"`:

```python
In [13]: line = "\nline1\t\nline2"

In [14]: item = "100"

In [15]: print(f"{line=} {item=}")
line='\nline1\t\nline2' item='100'

In [16]: for i in range(5):
    ...:     print(f"{i=}")
    ...:
i=0
i=1
i=2
i=3
i=4
```

Цей варіант з одного боку дозволяє відображати скільки завгодно значень плюс
автоматично додає ім'я змінної до виводу, з іншого, виводить як і pprint,
рядки зі спеціальними символами і лапками.


## locals

Функція locals показує всі локальні змінні. Якщо в коді немає функцій, то це
будуть усі глобальні змінні, якщо ви виводите всередині функції, то лише змінні
цієї функції.

Приклад коду:

```python
from pprint import pprint

item = "100"
line = "\nline1\n\tline2"

pprint(locals())
```

Що виводить locals:

```python
{'__annotations__': {},
 '__builtins__': <module 'builtins' (built-in)>,
 '__cached__': None,
 '__doc__': None,
 '__file__': '/home/user/repos/tasks/exercises/15_module_re/code.py',
 '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0xb73f30d0>,
 '__name__': '__main__',
 '__package__': None,
 '__spec__': None,
 'item': '100',
 'line': '\nline1\n\tline2',
 'pprint': <function pprint at 0xb7253808>}
```

Приклад коду з функцією:

```python
from pprint import pprint

def num_sum(x, y):
    result = x + y
    pprint(locals())
    return result
```

Виведення locals під час виклику функції:

```python
In [4]: num_sum(10, 5)
{'result': 15, 'x': 10, 'y': 5}
Out[4]: 15
```


## rich.inspect

Rich це сторонній модуль, в якому є багато можливостей для виведення інформації
терміналі: красиві таблиці, виведення кольорових рядків, progress bar та інші можливості.
Одна із зручних можливостей rich - функція inspect. Вона виводить інформацію
про зазначений об'єкт, його методи та атрибути.

Встановлення rich:

```
pip install rich
```

Приклад використання rich.inspect зі списком:

```python
In [10]: from rich import inspect

In [11]: items = [10, 20, 30, 40]

In [12]: inspect(items)
╭───────────────────────](class 'list'> ───────────────────────╮
│ Built-in mutable sequence.                                   │
│                                                              │
│ ╭──────────────────────────────────────────────────────────╮ │
│ │ [10, 20, 30, 40]                                         │ │
│ ╰──────────────────────────────────────────────────────────╯ │
│                                                              │
│ 36 attribute(s) not shown. Run inspect(inspect) for options. │
╰──────────────────────────────────────────────────────────────╯

In [13]: inspect(items, methods=True)
╭────────────────────────────────────](class 'list'> ────────────────────────────────────╮
│ Built-in mutable sequence.                                                             │
│                                                                                        │
│ ╭────────────────────────────────────────────────────────────────────────────────────╮ │
│ │ [10, 20, 30, 40]                                                                   │ │
│ ╰────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                        │
│  append = def append(object, /): Append object to the end of the list.                 │
│   clear = def clear(): Remove all items from list.                                     │
│    copy = def copy(): Return a shallow copy of the list.                               │
│   count = def count(value, /): Return number of occurrences of value.                  │
│  extend = def extend(iterable, /): Extend list by appending elements from the          │
│           iterable.                                                                    │
│   index = def index(value, start=0, stop=2147483647, /): Return first index of value.  │
│  insert = def insert(index, object, /): Insert object before index.                    │
│     pop = def pop(index=-1, /): Remove and return item at index (default last).        │
│  remove = def remove(value, /): Remove first occurrence of value.                      │
│ reverse = def reverse(): Reverse *IN PLACE*.                                           │
│    sort = def sort(*, key=None, reverse=False): Sort the list in ascending order and   │
│           return None.                                                                 │
╰────────────────────────────────────────────────────────────────────────────────────────╯
```

Приклад використання rich.inspect із файлом:

```python
In [19]: f = open("code.py")

In [20]: inspect(f)
╭────────────────────](class '_io.TextIOWrapper'> ─────────────────────╮
│ Character and line based layer over a BufferedIOBase object, buffer. │
│                                                                      │
│ ╭──────────────────────────────────────────────────────────────────╮ │
│ │](_io.TextIOWrapper name='code.py' mode='r' encoding='UTF-8'>     │ │
│ ╰──────────────────────────────────────────────────────────────────╯ │
│                                                                      │
│         buffer =](_io.BufferedReader name='code.py'>                 │
│         closed = False                                               │
│       encoding = 'UTF-8'                                             │
│         errors = 'strict'                                            │
│ line_buffering = False                                               │
│           mode = 'r'                                                 │
│           name = 'code.py'                                           │
│       newlines = None                                                │
│  write_through = False                                               │
╰──────────────────────────────────────────────────────────────────────╯

In [21]: inspect(f, methods=True)
╭─────────────────────────────](class '_io.TextIOWrapper'> ──────────────────────────────╮
│ Character and line based layer over a BufferedIOBase object, buffer.                   │
│                                                                                        │
│ ╭────────────────────────────────────────────────────────────────────────────────────╮ │
│ │](_io.TextIOWrapper name='code.py' mode='r' encoding='UTF-8'>                       │ │
│ ╰────────────────────────────────────────────────────────────────────────────────────╯ │
│                                                                                        │
│         buffer =](_io.BufferedReader name='code.py'>                                   │
│         closed = False                                                                 │
│       encoding = 'UTF-8'                                                               │
│         errors = 'strict'                                                              │
│ line_buffering = False                                                                 │
│           mode = 'r'                                                                   │
│           name = 'code.py'                                                             │
│       newlines = None                                                                  │
│  write_through = False                                                                 │
│          close = def close(): Flush and close the IO object.                           │
│         detach = def detach(): Separate the underlying buffer from the TextIOBase and  │
│                  return it.                                                            │
│         fileno = def fileno(): Returns underlying file descriptor if one exists.       │
│          flush = def flush(): Flush write buffers, if applicable.                      │
│         isatty = def isatty(): Return whether this is an 'interactive' stream.         │
│           read = def read(size=-1, /): Read at most n characters from stream.          │
│       readable = def readable(): Return whether object was opened for reading.         │
│       readline = def readline(size=-1, /): Read until newline or EOF.                  │
│      readlines = def readlines(hint=-1, /): Return a list of lines from the stream.    │
│    reconfigure = def reconfigure(*, encoding=None, errors=None, newline=None,          │
│                  line_buffering=None, write_through=None): Reconfigure the text stream │
│                  with new parameters.                                                  │
│           seek = def seek(cookie, whence=0, /): Change stream position.                │
│       seekable = def seekable(): Return whether object supports random access.         │
│           tell = def tell(): Return current stream position.                           │
│       truncate = def truncate(pos=None, /): Truncate file to size bytes.               │
│       writable = def writable(): Return whether object was opened for writing.         │
│          write = def write(text, /):                                                   │
│                  Write string to stream.                                               │
│                  Returns the number of characters written (which is always equal to    │
│                  the length of the string).                                            │
│     writelines = def writelines(lines, /): Write a list of lines to stream.            │
╰────────────────────────────────────────────────────────────────────────────────────────╯
```

## rich.traceback

Ще одна корисна можливість rich - красивий traceback.

Код із помилкою:

```python
vlans = ["1", "2", "3", "test", "4", "5", "switchport allowed vlans add"]

vlans_list = []
for vl in vlans:
    new_vl = int(vl)
    vlans_list.append(new_vl)

print(vlans_list)
```


Стандартний traceback для коду:

```
$ python basics_debug_05_rich_traceback.py
Traceback (most recent call last):
  File "/examples/basics_debug_05_rich_traceback.py", line 11, in](module>
    new_vl = int(vl)
ValueError: invalid literal for int() with base 10: 'test'
```

З використанням rich (частина виведення locals скорочена):

```python
$ python basics_debug_05_rich_traceback.py
╭──────────────────── Traceback (most recent call last) ────────────────────╮
│ /examples/basics_debug_05_rich_traceback.py:11 in](module>                │
│                                                                           │
│    7                                                                      │
│    8                                                                      │
│    9 vlans_list = []                                                      │
│   10 for vl in vlans:                                                     │
│ ❱ 11 │   new_vl = int(vl)                                                 │
│   12 │   vlans_list.append(new_vl)                                        │
│   13                                                                      │
│   14 print(vlans_list)                                                    │
│   15                                                                      │
│                                                                           │
│ ╭─────────────────────────────── locals ────────────────────────────────╮ │
│ │          new_vl = 3                                                   │ │
│ │              vl = 'test'                                              │ │
│ │           vlans = [                                                   │ │
│ │                   │   '1',                                            │ │
│ │                   │   '2',                                            │ │
│ │                   │   '3',                                            │ │
│ │                   │   'test',                                         │ │
│ │                   │   '4',                                            │ │
│ │                   │   '5',                                            │ │
│ │                   │   'switchport allowed vlans add'                  │ │
│ │                   ]                                                   │ │
│ │      vlans_list = [1, 2, 3]                                           │ │
│ ╰───────────────────────────────────────────────────────────────────────╯ │
╰───────────────────────────────────────────────────────────────────────────╯
ValueError: invalid literal for int() with base 10: 'test'
```

Отримати такий вивід можна, додавши у файл з кодом такі рядки:

```python
from rich.traceback import install
install(show_locals=True, extra_lines=5)
```

Повний код

```python
from rich.traceback import install
install(show_locals=True, extra_lines=5)

vlans = ["1", "2", "3", "test", "4", "5", "switchport allowed vlans add"]

vlans_list = []
for vl in vlans:
    new_vl = int(vl)
    vlans_list.append(new_vl)

print(vlans_list)
```

І, якщо такий traceback сподобається, можна зробити так, щоб він
використовувався за замовчуванням. Для цього потрібно створити файл
`sitecustomize.py` у каталозі `site-packages` з таким вмістом:

```python
from rich.traceback import install
install(show_locals=True, extra_lines=5)
```

Як зрозуміти який каталог site-packages використовувати:

```
$ python -m site
sys.path = [
    '/home/user/repos/examples/',
    '/usr/local/lib/python310.zip',
    '/usr/local/lib/python3.10',
    '/usr/local/lib/python3.10/lib-dynload',
    '/home/user/venv/pyneng-py3-10-0/lib/python3.10/site-packages',
]
USER_BASE: '/home/user/.local' (exists)
USER_SITE: '/home/user/.local/lib/python3.10/site-packages' (doesn't exist)
```

Повний шлях до site-packages показаний у sys.path, в даному випадку це шлях:

```
'/home/user/venv/pyneng-py3-10-0/lib/python3.10/site-packages',
```

## Вбудований налагоджувач pdb

Тут описані тільки команди pdb і варто сприймати цю секцію як довідник по командах.
Як саме виглядає робота з налагоджувачем [показано у відео](https://pyneng.io/course/topics/debug/).

Як запустити pdb

```
python -m pdb script.py
```


Для виходу із pdb використовується команда `q`.

У будь-який момент можна перезапустити скрипт, без втрати breakpoint, за
допомогою команди `run`.

### Базові команди

* n (next) – виконати все до наступного рядка. Ця команда не входить до функцій, які викликаються в рядку
* s (step) – виконати поточний рядок, зупинитися якомога раніше. Ця команда входить у функції, що викликаються у рядку
* c (continue) – виконати все до breakpoint. Також корисна, коли скрипт відпрацьовує з винятком, дозволяє дійти до рядка, де виник виняток

### Контекст у коді, змінні

* `l` (list) - показує наступний рядок, який виконуватиметься і 5 рядків до і після нього. При додаванні діапазону показує зазначені рядки, наприклад, `list 1, 20` покаже код з 1 по 20 рядок
* `ll` (longlist) - показує весь метод чи функцію у якому ми знаходимося
* `a` (args) – показує аргументи функції (або методу) та їх значення. Працює лише всередині функції
* `p` – показує значення змінної, працює як print. Синтаксис `p data`, де data ім'я змінної
* `pp` – показує значення змінної, працює як pprint. Синтаксис `pp data`, де data ім'я змінної


### Виконання Python команд у pdb

Будь-яку команду можна виконати вказавши ! перед нею:

```
!vara = 55
!result.append(vara)
```

Таким чином, можна пробувати виконати якісь дії в поточному контексті програми,
змінити значення змінних.

Також можна перейти в інтерпретатор python із поточного контексту. Для цього
використовується команда interact:

```
(Pdb) interact
*interactive*
>>> print(cfg)
](_io.TextIOWrapper name='sh_cdp_n_sw1.txt' mode='r' encoding='UTF-8'>
>>> cfg.closed
False
>>>
>>> data = ['1','2','3']
>>> print(','.join(data))
1,2,3
>>>
now exiting InteractiveConsole...
(Pdb)
```

Для виходу з інтерпретатора використовується команда `Ctrl-d`.


### Додаткові команди з пересування

* until - виконати все до вказаного рядка. Синтаксис `until 15`, де 15 номер рядка
* return - виконується всередині функції та виконує все до return
* u (up) – перейти на один рівень вище в стеку викликів. Наприклад, якщо ми по ланцюжку переходили в один виклик функції, потім в інше, щоб повернутися назад треба використовувати up
* d (down) – перейти на один рівень нижче в стеку викликів


### Breakpoints

* b (break) - команда для встановлення breakpoint

Якщо команда вказується з аргументом, наприклад `break 12` або `break check_ip`,
встановлюється breakpoint. Без аргументів команда показує всі встановлені
breakpoint.

Видалення breakpoint під номером 1:

```
clear 1
```

Видалити всі breakpoint можна clear без аргументів.

#### Базові варіанти встановлення breakpoint

Встановити breakpoint у рядку 12:

```
break 12
```

Встановити breakpoint у першому рядку функції check_ip:

```
break check_ip
```

#### Breakpoint з умовою

Зробити breakpoint у рядку 12, якщо значення змінної num буде більше 10:

```
break 12, num > 10
```

#### Прив'язка команд до breakpoint

Створюємо breakpoint (він перший, тому його номер буде 1):

```
break 12
```

Додаємо команди, які будуть виконуватися щоразу, коли потрапляємо на breakpoint
(var1, var2, result_dict повинні бути замінені на ваші змінні)

```
commands 1
 pp var1
 pp var2
 pp result_dict
end
```

## ipdb

Модуль [ipdb](https://github.com/gotcha/ipdb) це один з різновидів pdb, який
додає підсвічування синтаксису, виклик ipython замість вбудованого
інтерпретатора, автопродовження команд.


Встановлення ipdb:

```
pip install ipdb
```

Як запустити ipdb

```
python -m ipdb script.py
```

В іншому, команди ті ж, що в pdb, тільки по команді interact відкриється
ipython, а не вбудований python інтепретатор.
