# Вкладені for

Цикли for можуть бути вкладені один в одного.
У цьому прикладі список команд містить команди, які потрібно виконати для
кожного з інтерфейсів у списку interfaces:

```python
commands = [
    'switchport mode access',
    'spanning-tree portfast',
    'spanning-tree bpduguard enable',
]
interfaces = ['0/1', '0/3', '0/4', '0/7', '0/9', '0/10', '0/11']

In [9]: for intf in interfaces:
   ...:     print(f'interface FastEthernet {intf}')
   ...:     for command in commands:
   ...:         print(f' {command}')
   ...:
interface FastEthernet 0/1
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
interface FastEthernet 0/3
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
interface FastEthernet 0/4
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
...
```
