# Приклади роботи з файлами

У цьому підрозділі розглядається робота з файлами та поєднуються теми: файли,
цикли та умови.

При обробці виводу команд чи конфігурації часто потрібно буде записати
підсумкові дані у словник. Не завжди очевидно, як обробляти виводу команд і
як загалом підходити до розбору виводу на частини. У цьому підрозділі
розглядаються кілька прикладів, із зростаючим рівнем складності.

## Розбір виводу стовпцями

У цьому прикладі розбиратиметься вивід команди sh ip int br. З виводу
команди нам треба отримати відповідність ім'я інтерфейсу – IP-адресу. Тобто
ім'я інтерфейсу – це ключ словника, а IP-адреса – значення. При цьому,
відповідність треба робити тільки для тих інтерфейсів, у яких призначено
IP-адресу.

Приклад виводу команди sh ip int br (файл sh_ip_int_br.txt):

```
R1#show ip interface brief
Interface                  IP-Address      OK? Method Status           Protocol
FastEthernet0/0            15.0.15.1       YES manual up               up
FastEthernet0/1            10.0.12.1       YES manual up               up
FastEthernet0/2            10.0.13.1       YES manual up               up
FastEthernet0/3            unassigned      YES unset  up               down
Loopback0                  10.1.1.1        YES manual up               up
Loopback100                100.0.0.1       YES manual up               up
```

Файл working_with_dict_example_1.py:

```python
result = {}

with open('sh_ip_int_br.txt') as f:
    for line in f:
        line_list = line.split()
        if line_list and line_list[1][0].isdigit():
            interface = line_list[0]
            address = line_list[1]
            result[interface] = address

print(result)
```

Команда sh ip int br відображає вивід стовпцями. Всі потрібні поля знаходяться
в одному рядку. Скрипт обробляє вивід рядок за рядком і кожен рядок розбиває
методом [split](/reference/string/methods/split/).

Отриманий список містить стовпці виводу. Так як з усього виводу потрібні тільки
інтерфейси, на яких налаштована IP-адреса, виконується перевірка першого
символу другого стовпця: якщо перший символ число, значить на інтерфейсі
призначена адреса і цей рядок треба обробляти.

Оскільки для кожного рядка є пара ключа та значення, вони присвоюються у
словник: `result[interface] = address`.

Результатом виконання скрипта буде такий словник (тут він розбитий на пари
ключ-значення для зручності, у реальному виводу скрипта словник
відображатиметься в один рядок):

```python
{'FastEthernet0/0': '15.0.15.1',
 'FastEthernet0/1': '10.0.12.1',
 'FastEthernet0/2': '10.0.13.1',
 'Loopback0': '10.1.1.1',
 'Loopback100': '100.0.0.1'}
```

## Отримання ключа та значення з різних рядків виводу

Дуже часто вивід команд виглядає таким чином, що ключ та значення
знаходяться у різних рядках.

Наприклад, з виводу команди sh ip interface треба отримати ім'я інтерфейсу та
MTU (файл sh_ip_interface.txt):

```
Ethernet0/0 is up, line protocol is up
  Internet address is 192.168.100.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  ...
Ethernet0/1 is up, line protocol is up
  Internet address is 192.168.200.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  ...
Ethernet0/2 is up, line protocol is up
  Internet address is 19.1.1.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  ...
```

Ім'я інтерфейсу знаходиться у рядку `Ethernet0/0 is up, line protocol is up`,
а MTU у рядку  `MTU is 1500 bytes`.

Наприклад, спробуємо запам'ятовувати щоразу інтерфейс у змінну interface і виводити його значення print,
але тільки коли зустрічається рядок зі значенням MTU:

```python
with open('sh_ip_interface.txt') as f:
    for line in f:
        if 'line protocol' in line:
            interface = line.split()[0]
        elif 'MTU is' in line:
            mtu = line.split()[-2]
            print('{:15}{}'.format(interface, mtu))
```

Вивід
```
Ethernet0/0    1500
Ethernet0/1    1500
Ethernet0/2    1500
Ethernet0/3    1500
Loopback0      1514
```

Вивід організований таким чином, що спочатку йде рядок з інтерфейсом, а потім
через кілька рядків - рядок з MTU. Якщо запам'ятовувати ім'я інтерфейсу кожного
разу, коли воно зустрічається, то на момент, коли зустрінеться рядок з MTU,
останній записаний інтерфейс - це той, до якого належить MTU.

Тепер, якщо необхідно створити словник з відповідністю інтерфейсу - MTU,
достатньо записати значення на момент, коли був знайдений MTU.

```python
result = {}

with open('sh_ip_interface.txt') as f:
    for line in f:
        if 'line protocol' in line:
            interface = line.split()[0]
        elif 'MTU is' in line:
            mtu = line.split()[-2]
            result[interface] = mtu

print(result)
```

Результатом виконання скрипта буде такий словник (тут він розбитий на пари
ключ-значення для зручності, у реальному результаті скрипта словник
відображатиметься в один рядок):

```python
{'Ethernet0/0': '1500',
 'Ethernet0/1': '1500',
 'Ethernet0/2': '1500',
 'Ethernet0/3': '1500',
 'Loopback0': '1514'}
```

Цей трюк часто буде корисним, оскільки часто вивід команд організований подібним
чином.

## Вкладений словник

Якщо потрібно отримати кілька параметрів з виводу команди, дуже зручно
використовувати словник із вкладеним словником.

Наприклад, з виводу `sh ip interface` потрібно отримати два параметри
IP-адресу та MTU:

```
Ethernet0/0 is up, line protocol is up
  Internet address is 192.168.100.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  ...
Ethernet0/1 is up, line protocol is up
  Internet address is 192.168.200.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  ...
Ethernet0/2 is up, line protocol is up
  Internet address is 19.1.1.1/24
  Broadcast address is 255.255.255.255
  Address determined by non-volatile memory
  MTU is 1500 bytes
  Helper address is not set
  ...
```

На першому етапі кожне значення зберігається в змінній, а потім виводяться всі
три значення. Значення відображаються, коли зустрічається рядок MTU, оскільки
він зустрічається у виводі останнім:

```python
with open('sh_ip_interface.txt') as f:
    for line in f:
        if 'line protocol' in line:
            interface = line.split()[0]
        elif 'Internet address' in line:
            ip_address = line.split()[-1]
        elif 'MTU' in line:
            mtu = line.split()[-2]
            print('{:15}{:17}{}'.format(interface, ip_address, mtu))

Ethernet0/0    192.168.100.1/24 1500
Ethernet0/1    192.168.200.1/24 1500
Ethernet0/2    19.1.1.1/24      1500
Ethernet0/3    192.168.230.1/24 1500
Loopback0      4.4.4.4/32       1514
```

Тут ми використовуємо ту саму техніку, що й у попередньому прикладі, але
додаємо ще одне вкладення словника:

```python
from pprint import pprint


result = {}

with open('sh_ip_interface.txt') as f:
    for line in f:
        if 'line protocol' in line:
            interface = line.split()[0]
            result[interface] = {}
        elif 'Internet address' in line:
            ip_address = line.split()[-1]
            result[interface]['ip'] = ip_address
        elif 'MTU' in line:
            mtu = line.split()[-2]
            result[interface]['mtu'] = mtu

pprint(result)
```

Щоразу, коли зустрічається інтерфейс, у словнику результатів створюється ключ
із назвою інтерфейсу і значення порожній словник. Це потрібно для
того, щоб у момент виявлення IP-адреси або MTU, параметр можна було записати до
вкладеного словника відповідного інтерфейсу.

Результатом виконання скрипта буде наступний словник:

```python
{'Ethernet0/0': {'ip': '192.168.100.1/24', 'mtu': '1500'},
 'Ethernet0/1': {'ip': '192.168.200.1/24', 'mtu': '1500'},
 'Ethernet0/2': {'ip': '19.1.1.1/24', 'mtu': '1500'},
 'Ethernet0/3': {'ip': '192.168.230.1/24', 'mtu': '1500'},
 'Loopback0': {'ip': '4.4.4.4/32', 'mtu': '1514'}}
```

## Вивід із порожніми значеннями

Іноді, у виводі команди траплятимуться секції з порожніми значеннями. Наприклад, у
випадку з `sh ip interface` можуть траплятися інтерфейси, які виглядають
так:

```
Ethernet0/1 is up, line protocol is up
  Internet protocol processing disabled
Ethernet0/2 is administratively down, line protocol is down
  Internet protocol processing disabled
Ethernet0/3 is administratively down, line protocol is down
  Internet protocol processing disabled
```

Відповідно, тут немає MTU та IP-адреси.

І якщо виконати попередній скрипт для файлу з такими інтерфейсами, результат
буде таким (вивід для файлу sh_ip_interface2.txt):

```python
{'Ethernet0/0': {'ip': '192.168.100.2/24', 'mtu': '1500'},
 'Ethernet0/1': {},
 'Ethernet0/2': {},
 'Ethernet0/3': {},
 'Loopback0': {'ip': '2.2.2.2/32', 'mtu': '1514'}}
```

Якщо необхідно додавати інтерфейси до словника лише, коли на інтерфейсі
призначено IP-адресу, треба перенести створення ключа з ім'ям інтерфейсу на
момент, коли зустрічається рядок з IP-адресою:

```python
result = {}

with open('sh_ip_interface2.txt') as f:
    for line in f:
        if 'line protocol' in line:
            interface = line.split()[0]
        elif 'Internet address' in line:
            ip_address = line.split()[-1]
            result[interface] = {}
            result[interface]['ip'] = ip_address
        elif 'MTU' in line:
            mtu = line.split()[-2]
            result[interface]['mtu'] = mtu

print(result)
```

У цьому випадку результатом буде такий словник:

```python
{'Ethernet0/0': {'ip': '192.168.100.2/24', 'mtu': '1500'},
 'Loopback0': {'ip': '2.2.2.2/32', 'mtu': '1514'}}
```
