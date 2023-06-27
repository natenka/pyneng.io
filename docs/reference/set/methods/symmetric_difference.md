
# symmetric_difference

Повертає нову множину із елементами які є в одній множині чи іншій, але не в обох.

![set](https://pyneng.io/assets/images/set_operations_symmetric_difference.png)

## Синтаксис

Повертає нову множину із елементами або в set, або в other, але не в обох.

```python
set.symmetric_difference(other)
```

### Параметри

#### other

Набор даних.

### Значення, що повертається

Множина.

### Виняток

Якщо якийсь елемент набору даних не хешований, виникає виняток [TypeError](/reference/exceptions/#typeerror)

```python
sw1 = {1, 2, 3, 10, 20}
sw3 = [10, 100, [1, 2, 3]]

In [6]: sw1.symmetric_difference(sw3)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[6], line 1
----> 1 sw1.symmetric_difference(sw3)

TypeError: unhashable type: 'list'
```

Оператор `^`:

```python
sw1 = {1, 2, 3, 10, 20}
sw3 = [10, 100, 200, 300]

In [8]: sw1 ^ sw3
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[8], line 1
----> 1 sw1 ^ sw3

TypeError: unsupported operand type(s) for ^: 'set' and 'list'
```

## Приклади використання

Метод symmetric_difference

```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 40, 100, 10, 20}
sw3 = [10, 30]

In [10]: sw1.symmetric_difference(sw2)
Out[10]: {1, 2, 3, 30, 40, 100}

In [11]: sw1.symmetric_difference(sw3)
Out[11]: {1, 2, 3, 20, 30}
```

Оператор `^`:
```python
sw1 = {1, 2, 3, 10, 20}
sw2 = {30, 40, 100, 10, 20}
sw3 = [10, 30]

In [12]: sw1 ^ sw2
Out[12]: {1, 2, 3, 30, 40, 100}

In [13]: sw1 ^ sw2 ^ set(sw3)
Out[13]: {1, 2, 3, 10, 40, 100}
```

