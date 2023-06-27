# intersection

Повертає нову множину із елементами, спільними для множини.

![set](https://pyneng.io/assets/images/set_operations_intersection.png)

## Синтаксис

Повертає нову множину із елементами, спільними для множини та всіх наборів даних others.

```python
set.intersection(*others)
```

### Параметри

#### others

[Ітеровані об'єкти](/reference/protocols/iterable/).

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

Метод intersection

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 40, 100, 10, 20}
sw3 = [10, 30]

In [6]: sw1.intersection(sw2)
Out[6]: {10, 20}

In [8]: sw1.intersection(sw2, sw3)
Out[8]: {10}
```

### Оператор `&`

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 40, 100, 10, 20}
sw3 = [10, 30]

In [7]: sw1 & sw2
Out[7]: {10, 20}

In [9]: sw1 & sw2 & set(sw3)
Out[9]: {10}
```
