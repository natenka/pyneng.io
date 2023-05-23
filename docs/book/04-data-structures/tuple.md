# Кортеж (Tuple)


Кортеж в Python це:

* послідовність елементів в дужках, які розділені між собою комою
* незмінний упорядкований тип даних

Грубо кажучи, кортеж – це список, який не можна змінити. Тобто в кортежі є лише
права на читання. Це може бути захистом від випадкових змін.

Створити порожній кортеж:

```python
In [1]: tuple1 = tuple()

In [2]: print(tuple1)
()
```

Кортеж з одного елемента (зверніть увагу на кому):

```python
In [3]: tuple2 = ('password',)
```

Кортеж зі списку:

```python
In [4]: list_keys = ['hostname', 'location', 'vendor', 'model', 'ios', 'ip']

In [5]: tuple_keys = tuple(list_keys)

In [6]: tuple_keys
Out[6]: ('hostname', 'location', 'vendor', 'model', 'ios', 'ip')
```

До елементів у кортежі можна звертатись, як і до елементів списку, за
порядковим номером:

```python
In [7]: tuple_keys[0]
Out[7]: 'hostname'
```

Оскільки кортеж незмінний, привласнити нове значення не можна:

```python
In [8]: tuple_keys[1] = 'test'
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-9-1c7162cdefa3> in <module>()
----> 1 tuple_keys[1] = 'test'

TypeError: 'tuple' object does not support item assignment
```

Функція sorted сортує елементи кортежу за зростанням та повертає новий список
із відсортованими елементами:

```python
In [2]: tuple_keys = ('hostname', 'location', 'vendor', 'model', 'ios', 'ip')

In [3]: sorted(tuple_keys)
Out[3]: ['hostname', 'ios', 'ip', 'location', 'model', 'vendor']
```

