# list

list - конвертує об'єкт в список.

## Синтаксис

```python
In [1]: list?
Init signature: list(iterable=(), /)
Docstring:     
Built-in mutable sequence.

If no argument is given, the constructor creates a new empty list.
The argument must be an iterable if specified.
Type:           type
```

## Приклади

Створення порожнього списку (в Python для цього частіше
використовується вираз `items = []`):

```python
items = list()
```

Створення списку символів з рядку:

```python
In [2]: list('router')
Out[2]: ['r', 'o', 'u', 't', 'e', 'r']
```

List працює тільки з [ітерованими об'єктами](/reference/protocols/iterable).
Якщо ви передасте list не ітерований об’єкт, буде згенеровано [виняток TypeError](/reference/exceptions/):

```python
In [3]: list(100)
--------------------------------------------------------------------------
TypeError                                Traceback (most recent call last)
Cell In[3], line 1
----> 1 list(100)

TypeError: 'int' object is not iterable
```
