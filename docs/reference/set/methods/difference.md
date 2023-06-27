# difference

Повертає нову множину із елементами, яких немає в іншій множині.

![set](https://pyneng.io/assets/images/set_operations_difference.png)

## Синтаксис

Повертає нову множину із елементами, яких немає в others.

```python
set.difference(*others)
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

In [25]: sw1.difference(sw3)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[25], line 1
----> 1 sw1.difference(sw3)

TypeError: unhashable type: 'list'
```

Оператор `-`:

```python
In [20]: sw1 = {1, 2, 3, 10, 20}

In [21]: sw3 = [10, 100, 200, 300]

In [28]: sw1 - sw3
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[28], line 1
----> 1 sw1 - sw3

TypeError: unsupported operand type(s) for -: 'set' and 'list'
```

## Приклади використання

Метод difference

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 10, 20}
sw3 = [1, 30]

In [5]: sw1.difference(sw2)
Out[5]: {1, 2, 3}

In [6]: sw2.difference(sw1)
Out[6]: {30}

In [7]: sw1.difference(sw2, sw3)
Out[8]: {2, 3}
```

### Оператор `-`

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 10, 20}
sw3 = [1, 30]

In [3]: sw1 - sw2
Out[3]: {1, 2, 3}

In [4]: sw2 - sw1
Out[4]: {30}

In [5]: sw1 - sw2 - set(sw3)
Out[5]: {2, 3}
```


