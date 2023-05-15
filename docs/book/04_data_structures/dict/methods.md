# Корисні методи для роботи зі словниками

## ``clear``

Метод clear дозволяє очистити словник - видалити всі елементи:

```python
In [1]: london = {'name': 'London1', 'location': 'London Str'}

In [2]: london.clear()

In [3]: london
Out[3]: {}
```

## ``copy``

Метод ``copy`` створює копію словника:

```python
In [10]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [11]: london2 = london.copy()

In [12]: id(london)
Out[12]: 25524512

In [13]: id(london2)
Out[13]: 25563296

In [14]: london['vendor'] = 'Juniper'

In [15]: london2['vendor']
Out[15]: 'Cisco'
```

## ``get``

Якщо при зверненні до словника вказується ключ, якого немає у словнику, виникає
помилка:

```python
In [16]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [17]: london['ios']
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-17-b4fae8480b21> in <module>()
----> 1 london['ios']

KeyError: 'ios'
```

Метод ``get`` замість помилки повертає ``None``.

```python
In [18]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [19]: print(london.get('ios'))
None
```

Метод get також дозволяє вказувати інше значення замість ``None``:

```python
In [20]: print(london.get('ios', 'Ooops'))
Ooops
```


## ``keys, values, items``

Методи ``keys``, ``values``, ``items``:

```python
In [24]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [25]: london.keys()
Out[25]: dict_keys(['name', 'location', 'vendor'])

In [26]: london.values()
Out[26]: dict_values(['London1', 'London Str', 'Cisco'])

In [27]: london.items()
Out[27]: dict_items([('name', 'London1'), ('location', 'London Str'), ('vendor', 'Cisco')])
```

Всі три методи повертають спеціальні об'єкти view, які відображають ключі,
значення та пари ключ-значення словника відповідно.

Дуже важлива особливість view полягає в тому, що вони змінюються разом із
зміною словника. І фактично вони лише дають спосіб подивитися на відповідні
об'єкти, але не створюють їхньої копії.

На прикладі методу keys:

```python
In [28]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [29]: keys = london.keys()

In [30]: print(keys)
dict_keys(['name', 'location', 'vendor'])
```

Зараз змінна keys відповідає view, в якому три ключі: name, location і vendor.
Якщо додати до словника ще одну пару ключ-значення, об'єкт keys також зміниться:

```python
In [31]: london['ip'] = '10.1.1.1'

In [32]: keys
Out[32]: dict_keys(['name', 'location', 'vendor', 'ip'])
```

Якщо потрібно отримати звичайний список ключів, який не змінюватиметься зі
змінами словника, достатньо конвертувати view в список:

```python

In [33]: list_keys = list(london.keys())

In [34]: list_keys
Out[34]: ['name', 'location', 'vendor', 'ip']
```

## ``del``

Видалити ключ і значення:

```python
In [35]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [36]: del london['name']

In [37]: london
Out[37]: {'location': 'London Str', 'vendor': 'Cisco'}
```

## ``update``

Метод update дозволяє додавати до словника вміст іншого словника:

```python
In [38]: r1 = {'name': 'London1', 'location': 'London Str'}

In [39]: r1.update({'vendor': 'Cisco', 'ios':'15.2'})

In [40]: r1
Out[40]: {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco', 'ios': '15.2'}
```

Аналогічним чином можна оновити значення:

```python
In [41]: r1.update({'name': 'london-r1', 'ios': '15.4'})

In [42]: r1
Out[42]:
{'name': 'london-r1',
 'location': 'London Str',
 'vendor': 'Cisco',
 'ios': '15.4'}
```

## ``setdefault``

Метод ``setdefault`` шукає ключ, а якщо його немає, замість помилки створює
ключ зі значенням ``None``.

```python
In [21]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [22]: ios = london.setdefault('ios')

In [23]: print(ios)
None

In [24]: london
Out[24]: {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco', 'ios': None}
```

Якщо ключ є, setdefault повертає відповідне значення:

```python
In [25]: london.setdefault('name')
Out[25]: 'London1'
```

Другий аргумент дозволяє вказати, яке значення має відповідати ключу:

```python
In [26]: model = london.setdefault('model', 'Cisco3580')

In [27]: print(model)
Cisco3580

In [28]: london
Out[28]:
{'name': 'London1',
 'location': 'London Str',
 'vendor': 'Cisco',
 'ios': None,
 'model': 'Cisco3580'}
```


Метод setdefault в такому вигляді:

```python
value = london.setdefault(key, "somevalue")
```

замінює таку конструкцію:

```python
if key in london:
    value = london[key]
else:
    london[key] = "somevalue"
    value = london[key]
```
