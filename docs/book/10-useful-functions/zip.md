# Функція zip

Функція zip:

* як аргументи функції передаються послідовності
* zip повертає ітератор з кортежами, в якому n-ий кортеж складається з n-их елементів послідовностей, які були передані як аргументи
* якщо як аргументи були передані послідовності різної довжини, то всі вони будуть скорочені до довжини найкоротшої послідовності

Синтаксис

```python
zip(*iterables, strict=False)
```

Приклад використання zip:

```python
In [1]: a = [1, 2, 3]

In [2]: b = [100, 200, 300]

In [3]: list(zip(a, b))
Out[3]: [(1, 100), (2, 200), (3, 300)]
```

Використання zip зі списками різної довжини:

```python
list1 = [1, 2, 3, 4, 5]
list2 = [10, 20, 30, 40, 50]
list3 = [100, 200, 300]

In [5]: list(zip(list1, list2, list3))
Out[5]: [(1, 10, 100), (2, 20, 200), (3, 30, 300)]
```

Виклик zip зі  списками різної довжини та `strict=True`:
```python
In [6]: list(zip(list1, list2, list3, strict=True))
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
Cell In[6], line 1
----> 1 list(zip(list1, list2, list3, strict=True))

ValueError: zip() argument 3 is shorter than arguments 1-2
```

## Використання zip для створення словника

Приклад використання zip для створення словника:

```python
d_keys = ['hostname', 'location', 'vendor', 'model', 'ios', 'ip']
d_values = ['london_r1', '21 New Globe Walk', 'Cisco', '4451', '15.4', '10.255.0.1']

In [2]: r1 = dict(zip(d_keys, d_values))

In [3]: r1
Out[3]:
{'hostname': 'london_r1',
 'location': '21 New Globe Walk',
 'vendor': 'Cisco',
 'model': '4451',
 'ios': '15.4',
 'ip': '10.255.0.1'}
```

