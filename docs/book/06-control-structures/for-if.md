# Комбінування for і if

Приклад поєднання for і if.

```python
access_template = ['switchport mode access',
                   'switchport access vlan',
                   'spanning-tree portfast',
                   'spanning-tree bpduguard enable']

access = {'0/12': 10, '0/14': 11, '0/16': 17, '0/17': 150}

for intf, vlan in access.items():
    print('interface FastEthernet {}'.format(intf))
    for command in access_template:
        if command.endswith('access vlan'):
            print(' {} {}'.format(command, vlan))
        else:
            print(' {}'.format(command))
```

Коментарі до коду:

* Перший цикл for виконує ітерацію по ключам і значенням у словнику access
* Поточний ключ у цій точці циклу зберігається у змінній intf
* Поточне значення на цьому етапі циклу зберігається у змінній vlan
* Відображається print рядок `interface FastEthernet` з доданим до нього номером інтерфейсу
* Другий цикл for повторює команди зі списку access_template
* Оскільки потрібно додати номер VLAN до команди switchport access vlan:

  * всередині другого циклу for перевіряються команди
  * якщо команда закінчується на access vlan, виводиться команда, і до неї додається номер VLAN
  * у всіх інших випадках команда просто відображається print

Результат виконання скрипта:

```
$ python generate_access_port_config.py
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
interface FastEthernet0/17
 switchport mode access
 switchport access vlan 150
 spanning-tree portfast
 spanning-tree bpduguard enable
```
