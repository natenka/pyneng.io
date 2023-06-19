# join

Метод join повертає рядок, який є об'єднанням рядків у послідовності рядків,
переданої як аргумент. Між елементами в об'єднанні рядків проставляється роздільник.

## Синтаксис

```python
str.join(iterable)
```

### Параметри

#### iterable

[Ітерований об'єкт](/reference/protocols/iterable/) з рядками.

### Значення, що повертається

Рядок.

### Виняток

Якщо iterable містить будь-які значення, окрім рядків, виникає виняток
[TypeError](/reference/exceptions/#typeerror)

## Приклади використання

Роздільник у змінній:

```python
In [1]: octets = ['10', '1', '1', '1']

In [2]: sep = "."

In [3]: sep.join(octets)
Out[3]: '10.1.1.1'
```

Роздільник як літерал:

```python
In [1]: octets = ['10', '1', '1', '1']

In [4]: ".".join(octets)
Out[4]: '10.1.1.1'
```

Об'єднання рядків без роздільника:

```python
In [1]: mac_parts = ["AAAA", "BBBB", "CCCC"]

In [2]: "".join(mac_parts)
Out[2]: 'AAAABBBBCCCC'
```

Якщо iterable містить будь-які значення, окрім рядків, виникає виняток
[TypeError](/reference/exceptions/#typeerror):

```python
In [3]: numbers = [1, 2, 3]

In [4]: "_".join(numbers)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[4], line 1
----> 1 "_".join(numbers)

TypeError: sequence item 0: expected str instance, int found

In [5]: numbers = ["1", 2, 3]

In [6]: "_".join(numbers)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[6], line 1
----> 1 "_".join(numbers)

TypeError: sequence item 1: expected str instance, int found
```

Join працює з будь-яким [ітерованим об'єктом](/reference/protocols/iterable/):

```python
In [1]: ".".join(('10', '1', '1', '1'))
Out[1]: '10.1.1.1'

In [2]: "_".join("test")
Out[2]: 't_e_s_t'

In [3]: numbers = ["1", 2, 3]

In [4]: "_".join(map(str, numbers))
Out[4]: '1_2_3'
```

## Дивись також

#### [split](/reference/string/methods/split/)

