# union

Повертає нову множину із елементами з кожної з множин.

![set](https://pyneng.io/assets/images/set_operations_union.png)

## Синтаксис

Повертає нову множину із елементами, спільними для множини та всіх наборів даних others.

```python
set.union(*others)
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

In [25]: sw1.union(sw3)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[25], line 1
----> 1 sw1.union(sw3)

TypeError: unhashable type: 'list'
```

Оператор `|`:

```python
sw1 = {1, 2, 3, 10, 20}
sw3 = [10, 100, 200, 300]

In [18]: sw1 | sw3
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[18], line 1
----> 1 sw1 | sw3

TypeError: unsupported operand type(s) for |: 'set' and 'list'
```

## Приклади використання

Метод union

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 40, 100, 10, 20}
sw3 = [10, 30]

In [6]: sw1.union(sw2)
Out[6]: {1, 2, 3, 10, 20, 30, 40, 100}

In [7]: sw1.union(sw2, sw3)
Out[7]: {1, 2, 3, 10, 20, 30, 40, 100}
```


### Оператор `|`

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 40, 100, 10, 20}
sw3 = [10, 30]

In [9]: sw1 | sw2
Out[9]: {1, 2, 3, 10, 20, 30, 40, 100}

In [10]: sw1 | sw2 | set(sw3)
Out[10]: {1, 2, 3, 10, 20, 30, 40, 100}
```

