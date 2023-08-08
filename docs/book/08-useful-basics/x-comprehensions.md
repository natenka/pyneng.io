# Спискові, словникові, множинні вирази

Python підтримує спеціальні вирази, які дозволяють компактно створювати списки,
словники та множини.

Англійською ці вирази називаються, відповідно:

-  List comprehensions (спискові вирази)
-  Dict comprehensions (словникові вирази)
-  Set comprehensions (множинні вирази)

Ці вирази не тільки дозволяють компактніше створювати відповідні об'єкти, але й
створюють їх швидше. І хоча спочатку вони вимагають певної звички використання
та розуміння, вони часто використовуються.

## Синтаксис

Синтаксис спискового виразу (синтаксис словникових та множинних виразів
відрізняється тільки дужками):

```python
[expression for item1 in iterable1 if condition1
            for item2 in iterable2 if condition2
            ...
            for itemN in iterableN if conditionN]
```

В найпростішому варіанті (один цикл без умови)

```python
[expression for item in iterable]
```

Цикл з умовою:

```python
[expression for item in iterable if condition]
```

## Спискові вирази (list comprehensions)

Приклад спискового виразу:

```python
vlans = [int(vl) for vl in items]
```

Списковий вираз дозволяє записати код:

```python
items = ["10", "20", "30", "1", "11", "100"]

vlans = []
for vl in items:
    vlans.append(int(vl))
```

Таким списковим виразом:

```python
items = ["10", "20", "30", "1", "11", "100"]
vlans = [int(vl) for vl in items]
```

Результат буде однаковим, список vlans:

```python
[10, 20, 30, 1, 11, 100]
```

Відповідність між звичайним циклом та списковим виразом:

![list_comp](https://pyneng.io/assets/images/08_list_comp.png)

У спискових виразах можна використовувати умови if. Таким чином можна додавати
до списку лише деякі елементи з ітерованого об'єкту.

Наприклад, такий цикл відбирає ті елементи, які є числами, конвертує їх та
додає до списку only_digits:

```python
items = ['10', '20', 'a', '30', 'b', '40']

only_digits = []

for item in items:
    if item.isdigit():
        only_digits.append(int(item))
```

Аналогічний варіант як списковий вираз:

```python
items = ['10', '20', 'a', '30', 'b', '40']
only_digits = [int(item) for item in items if item.isdigit()]
```

Результат буде однаковим, список only_digits:
```python
[10, 20, 30, 40]
```

Відповідність між циклом з умовою та списковим виразом з умовою:

![list_comp_if](https://pyneng.io/assets/images/08_list_comp_if.png)



За допомогою генератора списку також зручно отримувати елементи із вкладених
словників:

```python
london_co = {
    'r1' : {
    'hostname': 'london_r1',
    'location': '21 New Globe Walk',
    'vendor': 'Cisco',
    'model': '4451',
    'ios': '15.4',
    'ip': '10.255.0.1'
    },
    'r2' : {
    'hostname': 'london_r2',
    'location': '21 New Globe Walk',
    'vendor': 'Cisco',
    'model': '4451',
    'ios': '15.4',
    'ip': '10.255.0.2'
    },
    'sw1' : {
    'hostname': 'london_sw1',
    'location': '21 New Globe Walk',
    'vendor': 'Cisco',
    'model': '3850',
    'ios': '3.6.XE',
    'ip': '10.255.0.101'
    }
}

In [14]: [london_co[device]['ios'] for device in london_co]
Out[14]: ['15.4', '15.4', '3.6.XE']

In [15]: [london_co[device]['ip'] for device in london_co]
Out[15]: ['10.255.0.1', '10.255.0.2', '10.255.0.101']
```

У списковому виразі можна використовувати кілька for.
Наприклад, у списку vlans є кілька вкладених списків з VLAN'ами:

```python
vlans = [[10, 21, 35], [101, 115, 150], [111, 40, 50]]
```

З цього списку потрібно сформувати один плоский список із номерами VLAN. Перший
варіант із циклами for:

```python
result = []

for vlan_list in vlans:
    for vlan in vlan_list:
        result.append(vlan)
```

Аналогічний варіант із списковим виразом:

```python
result = [vlan for vlan_list in vlans for vlan in vlan_list]
```

Результат:

```python
[10, 21, 35, 101, 115, 150, 111, 40, 50]
```

Відповідність між двома вкладеними циклами та списковим виразом з двома циклами:

![list_comp_for_for](https://pyneng.io/assets/images/08_list_comp_for_for.png)


## Словникові вирази (dict comprehensions)


Словникові вирази подібні до спискових виразів, але вони використовуються
для створення словників.

Наприклад, такий код:

```python
d = {}

for num in range(1, 6):
    d[num] = num**2
```

Можна замінити словниковим виразом:

```python
d = {num: num**2 for num in range(1, 6)}
```

Результат:

```python
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

Ще один приклад, у якому треба перетворити існуючий словник та перевести всі
ключі в нижній регістр. Варіант без словникового виразу:

```python
r1 = {'IOS': '15.4',
      'IP': '10.255.0.1',
      'hostname': 'london_r1',
      'location': '21 New Globe Walk',
      'model': '4451',
      'Vendor': 'Cisco'}

lower_r1 = {}

for key, value in r1.items():
    lower_r1[key.lower()] = value
```

Аналогічний варіант зі словниковим виразом:

```python
r1 = {'IOS': '15.4',
      'IP': '10.255.0.1',
      'hostname': 'london_r1',
      'location': '21 New Globe Walk',
      'model': '4451',
      'Vendor': 'Cisco'}

lower_r1 = {key.lower(): value for key, value in r1.items()}
```

Результат:
```python
{'ios': '15.4',
 'ip': '10.255.0.1',
 'hostname': 'london_r1',
 'location': '21 New Globe Walk',
 'model': '4451',
 'vendor': 'Cisco'}
```

Як і списовий вираз, словникові вирази можна робити вкладеними. Спробуємо
аналогічним чином перетворити ключі у вкладених словниках:

```python
london_co = {
    "r1": {
        "hostname": "london_r1",
        "IOS": "15.4",
        "IP": "10.255.0.1",
    },
    "r2": {
        "hostname": "london_r2",
        "IOS": "15.4",
        "IP": "10.255.0.2",
    },
    "sw1": {
        "hostname": "london_sw1",
        "IOS": "3.6.XE",
        "IP": "10.255.0.101",
    },
}

lower_london_co = {}

for device, params in london_co.items():
    lower_london_co[device] = {}
    for key, value in params.items():
        lower_london_co[device][key.lower()] = value
```

Аналогічний варіант зі словниковим виразом:

```python
result = {device: {key.lower(): value for key, value in params.items()}
          for device, params in london_co.items()}
```

Результат:

```python
{
    "r1": {
        "hostname": "london_r1",
        "ios": "15.4",
        "ip": "10.255.0.1",
    },
    "r2": {
        "hostname": "london_r2",
        "ios": "15.4",
        "ip": "10.255.0.2",
    },
    "sw1": {
        "hostname": "london_sw1",
        "ios": "3.6.XE",
        "ip": "10.255.0.101",
    },
}
```

## Множинні вирази (set comprehensions)

Множинні вирази загалом аналогічні списковим виразам.

Наприклад, отримати множину з унікальними числами можна так:

```python
vlans = [10, '30', 30, 10, '56']

unique_vlans = {int(vlan) for vlan in vlans}
```

Варіант без використання множинного виразу:

```python
vlans = [10, '30', 30, 10, '56']

unique_vlans = set()

for vlan in vlans:
    unique_vlans.add(int(vlan))
```

Результат список unique_vlans:
```python
{10, 30, 56}
```
