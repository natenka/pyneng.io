# add

Метод add додає елемент в множину.

## Синтаксис

```python
set.add(elem)
```

### Параметри

#### elem

Додайте елемент elem до набору.

### Значення, що повертається

None

### Виняток

Якщо elem не хешований об'єкт, виникає виняток [TypeError](/reference/exceptions/#typeerror)

```python
In [1]: vlans = {1, 2, 3, 10, 100, 11}

In [3]: vlans.add([])
------------------------------------------------------------------------
TypeError                              Traceback (most recent call last)
Cell In[3], line 1
----> 1 vlans.add([])

TypeError: unhashable type: 'list'
```

## Приклади використання

```python
In [4]: vlans = {1, 2, 3, 10, 100, 11}

In [5]: vlans.add(200)

In [6]: vlans
Out[6]: {1, 2, 3, 10, 11, 100, 200}

In [7]: vlans.add(200)

In [8]: vlans
Out[8]: {1, 2, 3, 10, 11, 100, 200}
```

