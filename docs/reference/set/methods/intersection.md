# intersection

Повертає нову множину із елементами, спільними для множини.

## Синтаксис

Повертає нову множину із елементами, спільними для множини та всіх наборів даних others.

```python
set.intersection(*others)
```

### Параметри

#### others

Набори даних.

### Значення, що повертається

Множина.

### Виняток

Якщо якийсь елемент набору даних не хешований, виникає виняток [TypeError](/reference/exceptions/#typeerror)

```python
In [23]: sw1 = {1, 2, 3, 10, 20}

In [24]: sw3 = [10, 100, [1, 2, 3]]

In [25]: sw1.intersection(sw3)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[25], line 1
----> 1 sw1.intersection(sw3)

TypeError: unhashable type: 'list'
```

Оператор `&`:

```python
In [20]: sw1 = {1, 2, 3, 10, 20}

In [21]: sw3 = [10, 100, 200, 300]

In [22]: sw1 & sw3
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[22], line 1
----> 1 sw1 & sw3

TypeError: unsupported operand type(s) for &: 'set' and 'list'
```

## Приклади використання

```python
In [13]: sw1 = {1, 2, 3, 10, 20}

In [14]: sw2 = {30, 40, 100, 10, 20}

In [15]: sw3 = [10, 30]

In [16]: sw1.intersection(sw2)
Out[16]: {10, 20}

In [17]: sw1 & sw2
Out[17]: {10, 20}

In [18]: sw1.intersection(sw2, sw3)
Out[18]: {10}

In [19]: sw1 & sw2 & set(sw3)
Out[19]: {10}
```
