# Інтерпретатор Python. IPython

Інтерпретатор дозволяє отримати моментальний відгук на виконані дії. Можна
сказати, що інтерпретатор працює як CLI (Command Line Interface) мережевих
пристроїв: кожна команда виконуватиметься відразу після натискання Enter. Однак
є виняток - складніші об'єкти (наприклад цикли або функції) виконуються тільки
після дворазового натискання Enter.

У попередньому розділі для перевірки установки Python викликався стандартний
інтерпретатор. Крім нього, є й удосконалений інтерпретатор [IPython](http://ipython.readthedocs.io/en/stable/index.html).
IPython дозволяє
набагато більше, ніж стандартний інтерпретатор, який викликається за командою
python. Декілька прикладів (можливості IPython набагато ширші):

-  автодоповнення команд по Tab або підказка, якщо варіантів команд декілька
-  більш структурований та зрозумілий вивід команд
-  автоматичні відступи у циклах та інших об'єктах
-  можна пересуватися з історії виконання команд, або ж подивитися її «чарівною» командою історії

Встановити IPython можна за допомогою pip (установка буде проводитися у
віртуальному оточенні, якщо воно налаштоване):

```
pip install ipython
```

Після цього, перейти в IPython можна так:

```
$ ipython
Python 3.7.3 (default, May 13 2019, 15:44:23)
Type 'copyright', 'credits' or 'license' for more information
IPython 7.5.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]:
```

Для виходу використається команда quit. Далі описується, як
використовуватиметься IPython.

Для знайомства з інтерпретатором можна спробувати використати його як
калькулятор:

```python
In [1]: 1 + 2
Out[1]: 3

In [2]: 22*45
Out[2]: 990

In [3]: 2**3
Out[3]: 8
```

В IPython введення та вивід позначені:

-  In - вхідні дані користувача
-  Out - результат, який повертає команда (якщо він є)
-  числа після In або Out - це порядкові номери виконаних команд у поточній сесії IPython

Приклад виведення рядка функцією print():

```python
In [4]: print('Hello!')
Hello!
```

Коли в інтерпретаторі створюється, наприклад, цикл, то всередині циклу
запрошення змінюється на крапки. Для виконання циклу та виходу з цього
підрежиму необхідно двічі натиснути Enter:

```python
In [5]: for i in range(5):
   ...:     print(i)
   ...:
0
1
2
3
4
```

## help

В IPython є можливість переглянути довідку по довільному об'єкту, функції або
методу за допомогою help():

```python
In [1]: help(str)
Help on class str in module builtins:

class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
...

In [2]: help(str.strip)
Help on method_descriptor:

strip(...)
    S.strip([chars]) -> str

    Return a copy of the string S with leading and trailing
    whitespace removed.
    If chars is given and not None, remove characters in chars instead.
```

Другий варіант:

```python
In [3]: ?str
Init signature: str(self, /, *args, **kwargs)
Docstring:
str(object='') -> str
str(bytes_or_buffer[, encoding[, errors]]) -> str

Create a new string object from the given object. If encoding or
errors is specified, then the object must expose a data buffer
that will be decoded using the given encoding and error handler.
Otherwise, returns the result of object.__str__() (if defined)
or repr(object).
encoding defaults to sys.getdefaultencoding().
errors defaults to 'strict'.
Type:           type

In [4]: ?str.strip
Docstring:
S.strip([chars]) -> str

Return a copy of the string S with leading and trailing
whitespace removed.
If chars is given and not None, remove characters in chars instead.
Type:      method_descriptor
```

### print

Функція ``print`` дозволяє вивести інформацію стандартний потік виведення
(поточний екран терміналу).  Якщо необхідно вивести рядок, то його потрібно
обов'язково взяти в лапки (подвійні чи одинарні). Якщо ж потрібно вивести,
наприклад, результат обчислення чи просто число, то лапки не потрібні:

```python
In [6]: print('Hello!')
Hello!

In [7]: print(5*5)
25
```

Якщо потрібно вивести поспіль кілька значень через пропуск, то потрібно
перерахувати їх через кому:

```python
In [8]: print(1*5, 2*5, 3*5, 4*5)
5 10 15 20

In [9]: print('one', 'two', 'three')
one two three
```

За замовчуванням наприкінці кожного виразу, переданого в print, буде
переведено рядок. Якщо необхідно, щоб після виведення кожного виразу не було б
перекладу рядка, треба як останній вираз у print вказати додатковий аргумент
end.

.. seealso``` Дополнительные параметры функции print :ref:`print`

## dir


Функція dir може використовуватися для того, щоб переглянути атрибути та методи
об'єкта:

* атрибути - змінні, прив'язані до об'єкта
* методи - функції, прив'язані до об'єкта

Наприклад, для числа вивід буде таким (зверніть увагу на різні методи, які
дозволяють робити арифметичні операції):

```python
In [10]: dir(5)
Out[10]:
['__abs__',
 '__add__',
 '__and__',
 ...
 'bit_length',
 'conjugate',
 'denominator',
 'imag',
 'numerator',
 'real']
```

Аналогічно для рядка:

```python
In [11]: dir('hello')
Out[11]:
['__add__',
 '__class__',
 '__contains__',
 ...
 'startswith',
 'strip',
 'swapcase',
 'title',
 'translate',
 'upper',
 'zfill']
```

Якщо виконати dir без передачі значення, то вона показує існуючі методи,
атрибути та змінні, визначені в поточній сесії інтерпретатора:

```python
In [12]: dir()
Out[12]:
[ '__builtin__',
 '__builtins__',
 '__doc__',
 '__name__',
 '_dh',
 ...
 '_oh',
 '_sh',
 'exit',
 'get_ipython',
 'i',
 'quit']
```

Наприклад, після створення змінної a та test:

```python
In [13]: a = 'hello'

In [14]: test = "test"

In [15]: dir()
Out[15]:
 ...
 'a',
 'exit',
 'get_ipython',
 'i',
 'quit',
 'test']
```
