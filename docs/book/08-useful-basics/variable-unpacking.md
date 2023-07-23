# Розпакування змінних

Розпакування змінної — це спеціальний синтаксис, який дозволяє призначати елементи ітерованого об'єкта змінним.

Досить часто цей функціонал називають розпакуванням кортежів (tuple unpacking), але розпакування
працює з будь-яким ітерованим об'єктом, а не лише з кортежами.

Приклад розпакування змінних:

```python
interface = ['FastEthernet0/1', '10.1.1.1', 'up', 'up']

intf, ip, status, protocol = interface

In [3]: intf
Out[3]: 'FastEthernet0/1'

In [4]: ip
Out[4]: '10.1.1.1'
```

Такий варіант набагато зручніше використовувати, ніж використання індексів:

```python
In [5]: intf, ip, status, protocol = interface[0], interface[1], interface[2], interface[3]
```

При розпаковуванні змінних кожен елемент списку потрапляє у відповідну змінну.
Важливо враховувати, що змінних зліва має бути рівно стільки, скільки елементів
у списку.

Якщо змінних більше або менше, виникне виняток:

```python
In [6]: intf, ip, status = interface
------------------------------------------------------------
ValueError                 Traceback (most recent call last)
<ipython-input-11-a304c4372b1a> in <module>()
----> 1 intf, ip, status = interface

ValueError: too many values to unpack (expected 3)

In [7]: intf, ip, status, protocol, other = interface
------------------------------------------------------------
ValueError                 Traceback (most recent call last)
<ipython-input-12-ac93e78b978c> in <module>()
----> 1 intf, ip, status, protocol, other = interface

ValueError: not enough values to unpack (expected 5, got 4)
```

## Заміна непотрібних елементів `_`

Часто з усіх елементів ітерованого об'єкту потрібні лише деякі. У цьому випадку
синтаксис розпакування вимагає від вас вказати рівно стільки змінних, скільки є
елементів у ітерованому об'єкті.

Якщо, наприклад, з рядка line треба отримати лише VLAN, MAC та інтерфейс, треба
все одно вказати змінну для типу запису:

```python
line = '100    01bb.c580.7000    DYNAMIC     Gi0/1'

vlan, mac, item_type, intf = line.split()

In [10]: vlan
Out[10]: '100'

In [11]: intf
Out[11]: 'Gi0/1'
```

Якщо тип запису не потрібний надалі, можна замінити змінну `item_type` нижнім підкресленням:

```python
vlan, mac, _, intf = line.split()
```

Таким чином, явно вказується, що цей елемент не потрібен.

Підкреслення можна використовувати кілька разів:

```python
In [13]: dhcp = '00:09:BB:3D:D6:58   10.1.10.2        86250       dhcp-snooping   10    FastEthernet0/1'

In [14]: mac, ip, _, _, vlan, intf = dhcp.split()

In [15]: mac
Out[15]: '00:09:BB:3D:D6:58'

In [16]: vlan
Out[16]: '10'
```

## Використання `*`

Розпакування змінних підтримує спеціальний синтаксис, який дозволяє
розпаковувати кілька елементів на один.  Якщо поставити `*` перед іменем
змінної, до неї запишуться всі елементи, крім присвоєних явно.

Наприклад, так можна отримати перший елемент змінну `first`, а інші в `rest`:

```python
In [18]: vlans = [10, 11, 13, 30]

In [19]: first, *rest = vlans

In [20]: first
Out[20]: 10

In [21]: rest
Out[21]: [11, 13, 30]
```

При цьому змінна із зірочкою завжди буде списком:

```python
In [22]: vlans = (10, 11, 13, 30)

In [22]: first, *rest = vlans

In [23]: first
Out[23]: 10

In [24]: rest
Out[24]: [11, 13, 30]
```

Якщо елемент лише один, розпакування все одно відпрацює:

```python
In [25]: first, *rest = vlans

In [26]: first
Out[26]: 55

In [27]: rest
Out[27]: []
```

У виразі розпакування може бути лише одна змінна із зірочкою.

```python
In [4]: vlans = (10, 11, 13, 30)

In [5]: first, *rest, *others = vlans
  Cell In[5], line 1
    first, *rest, *others = vlans
    ^
SyntaxError: multiple starred expressions in assignment
```

Змінна із зірочкою може бути не тільки в кінці виразу:

```python
In [30]: vlans = (10, 11, 13, 30)

In [31]: *rest, last = vlans

In [32]: rest
Out[32]: [10, 11, 13]

In [33]: last
Out[33]: 30
```

Таким чином можна вказати, що потрібен перший, другий та останній елемент:

```python
In [34]: cdp = 'SW1     Eth 0/0    140   S I   WS-C3750-  Eth 0/1'

In [35]: name, l_intf, *other, r_intf = cdp.split()

In [36]: name
Out[36]: 'SW1'

In [37]: l_intf
Out[37]: 'Eth'

In [38]: r_intf
Out[38]: '0/1'
```

## Приклади розпакування

### Розпакування ітерованих об'єктів

Ці приклади показують, що ви можете розпакувати не лише списки, кортежі та
рядки, але й будь-який інший ітерований об'єкт.

Розпакування range:

```python
In [39]: first, *rest = range(1, 6)

In [40]: first
Out[40]: 1

In [41]: rest
Out[41]: [2, 3, 4, 5]
```

Розпакування zip:

```python
In [42]: a = [1, 2, 3, 4, 5]

In [43]: b = [100, 200, 300, 400, 500]

In [44]: zip(a, b)
Out[44]: <zip at 0xb4df4fac>

In [45]: list(zip(a, b))
Out[45]: [(1, 100), (2, 200), (3, 300), (4, 400), (5, 500)]

In [46]: first, *rest, last = zip(a, b)

In [47]: first
Out[47]: (1, 100)

In [48]: rest
Out[48]: [(2, 200), (3, 300), (4, 400)]

In [49]: last
Out[49]: (5, 500)
```

### Приклад розпакування в циклі for

Приклад циклу, який проходить через ключі:

```python
access_template = ['switchport mode access',
                   'switchport access vlan',
                   'spanning-tree portfast',
                   'spanning-tree bpduguard enable']

access = {'0/12': 10, '0/14': 11, '0/16': 17}

for intf in access:
    print(f'interface FastEthernet {intf}')
    for command in access_template:
        if command.endswith('access vlan'):
            print(' {} {}'.format(command, access[intf]))
        else:
            print(' {}'.format(command))

interface FastEthernet0/12
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
interface FastEthernet0/14
 switchport mode access
 switchport access vlan 11
 spanning-tree portfast
 spanning-tree bpduguard enable
interface FastEthernet0/16
 switchport mode access
 switchport access vlan 17
 spanning-tree portfast
 spanning-tree bpduguard enable
```

Натомість можна проходити по парах ключ-значення і відразу ж розпаковувати їх у
різні змінні:

```python
for intf, vlan in access.items():
    print(f'interface FastEthernet {intf}')
    for command in access_template:
        if command.endswith('access vlan'):
            print(' {} {}'.format(command, vlan))
        else:
            print(' {}'.format(command))
```

Приклад розпакування елементів списку в циклі:

```python
In [54]: table
Out[54]:
[['100', 'a1b2.ac10.7000', 'DYNAMIC', 'Gi0/1'],
 ['200', 'a0d4.cb20.7000', 'DYNAMIC', 'Gi0/2'],
 ['300', 'acb4.cd30.7000', 'DYNAMIC', 'Gi0/3'],
 ['100', 'a2bb.ec40.7000', 'DYNAMIC', 'Gi0/4'],
 ['500', 'aa4b.c550.7000', 'DYNAMIC', 'Gi0/5'],
 ['200', 'a1bb.1c60.7000', 'DYNAMIC', 'Gi0/6'],
 ['300', 'aa0b.cc70.7000', 'DYNAMIC', 'Gi0/7']]


In [55]: for line in table:
    ...:     vlan, mac, _, intf = line
    ...:     print(vlan, mac, intf)
    ...:
100 a1b2.ac10.7000 Gi0/1
200 a0d4.cb20.7000 Gi0/2
300 acb4.cd30.7000 Gi0/3
100 a2bb.ec40.7000 Gi0/4
500 aa4b.c550.7000 Gi0/5
200 a1bb.1c60.7000 Gi0/6
300 aa0b.cc70.7000 Gi0/7
```

Але ще краще зробити так:

```python
In [56]: for vlan, mac, _, intf in table:
    ...:     print(vlan, mac, intf)
    ...:
100 a1b2.ac10.7000 Gi0/1
200 a0d4.cb20.7000 Gi0/2
300 acb4.cd30.7000 Gi0/3
100 a2bb.ec40.7000 Gi0/4
500 aa4b.c550.7000 Gi0/5
200 a1bb.1c60.7000 Gi0/6
m00 aa0b.cc70.7000 Gi0/7
```
