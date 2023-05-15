# Словник (Dictionary)

Словники - це змінюваний упорядкований тип даних:

* дані у словнику - це пари ключ: значение
* доступ до значень здійснюється за ключом
* дані у словнику впорядковані за порядком додавання елементів
* словники можна змінювати, тобто елементи словника можна змінювати, додавати, видаляти
* ключ має бути об'єктом незмінного типу: число, рядок, кортеж
* значення може бути даними будь-якого типу


> В інших мовах програмування тип даних подібний до словника може називатися
> асоціативний масив, хеш або хеш-таблиця.

Приклад словника:

```python
london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}
```

Можна записувати і так:

```python
london = {
    'id': 1,
    'name': 'London',
    'it_vlan': 320,
    'user_vlan': 1010,
    'mngmt_vlan': 99,
    'to_name': None,
    'to_id': None,
    'port': 'G1/0/11'
}
```


Для того, щоб отримати значення зі словника, треба звернутися по ключу:

```python
In [1]: london = {'name': 'London1', 'location': 'London Str'}

In [2]: london['name']
Out[2]: 'London1'

In [3]: london['location']
Out[3]: 'London Str'
```

Додати нову пару ключ-значення:

```python
In [4]: london['vendor'] = 'Cisco'

In [5]: print(london)
{'vendor': 'Cisco', 'name': 'London1', 'location': 'London Str'}
```

У словнику як значення можна використовувати словник:

```python
london_co = {
    'r1': {
        'hostname': 'london_r1',
        'location': '21 New Globe Walk',
        'vendor': 'Cisco',
        'model': '4451',
        'ios': '15.4',
        'ip': '10.255.0.1'
    },
    'r2': {
        'hostname': 'london_r2',
        'location': '21 New Globe Walk',
        'vendor': 'Cisco',
        'model': '4451',
        'ios': '15.4',
        'ip': '10.255.0.2'
    },
    'sw1': {
        'hostname': 'london_sw1',
        'location': '21 New Globe Walk',
        'vendor': 'Cisco',
        'model': '3850',
        'ios': '3.6.XE',
        'ip': '10.255.0.101'
    }
}
```

Отримати значення із вкладеного словника можна так:

```python
In [7]: london_co['r1']['ios']
Out[7]: '15.4'

In [8]: london_co['r1']['model']
Out[8]: '4451'

In [9]: london_co['sw1']['ip']
Out[9]: '10.255.0.101'
```

Функция sorted сортирует ключи словаря по возрастанию и возвращает
новый список с отсортированными ключами:

```python
In [1]: london = {'name': 'London1', 'location': 'London Str', 'vendor': 'Cisco'}

In [2]: sorted(london)
Out[2]: ['location', 'name', 'vendor']
```

