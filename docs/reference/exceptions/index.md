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

```python
In [4]: int("ff")
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Cell In[4], line 1
----> 1 int("ff")

ValueError: invalid literal for int() with base 10: 'ff'

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


## Ієрархія винятків

```
BaseException
 ├── BaseExceptionGroup
 ├── GeneratorExit
 ├── KeyboardInterrupt
 ├── SystemExit
 └── Exception
      ├── ArithmeticError
      │    ├── FloatingPointError
      │    ├── OverflowError
      │    └── ZeroDivisionError
      ├── AssertionError
      ├── AttributeError
      ├── BufferError
      ├── EOFError
      ├── ExceptionGroup [BaseExceptionGroup]
      ├── ImportError
      │    └── ModuleNotFoundError
      ├── LookupError
      │    ├── IndexError
      │    └── KeyError
      ├── MemoryError
      ├── NameError
      │    └── UnboundLocalError
      ├── OSError
      │    ├── BlockingIOError
      │    ├── ChildProcessError
      │    ├── ConnectionError
      │    │    ├── BrokenPipeError
      │    │    ├── ConnectionAbortedError
      │    │    ├── ConnectionRefusedError
      │    │    └── ConnectionResetError
      │    ├── FileExistsError
      │    ├── FileNotFoundError
      │    ├── InterruptedError
      │    ├── IsADirectoryError
      │    ├── NotADirectoryError
      │    ├── PermissionError
      │    ├── ProcessLookupError
      │    └── TimeoutError
      ├── ReferenceError
      ├── RuntimeError
      │    ├── NotImplementedError
      │    └── RecursionError
      ├── StopAsyncIteration
      ├── StopIteration
      ├── SyntaxError
      │    └── IndentationError
      │         └── TabError
      ├── SystemError
      ├── TypeError
      ├── ValueError
      │    └── UnicodeError
      │         ├── UnicodeDecodeError
      │         ├── UnicodeEncodeError
      │         └── UnicodeTranslateError
      └── Warning
           ├── BytesWarning
           ├── DeprecationWarning
           ├── EncodingWarning
           ├── FutureWarning
           ├── ImportWarning
           ├── PendingDeprecationWarning
           ├── ResourceWarning
           ├── RuntimeWarning
           ├── SyntaxWarning
           ├── UnicodeWarning
           └── UserWarning
```
