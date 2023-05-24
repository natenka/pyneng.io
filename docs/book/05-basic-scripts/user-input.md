# Введення інформації користувачем

Іноді потрібно отримати інформацію від користувача, наприклад, запросити пароль.

Для отримання інформації від користувача використовується функція ``input``:

```python
In [1]: print(input('Routing protocol: '))
Routing protocol: OSPF
OSPF
```

В цьому разі інформація відразу виводиться користувачеві, але крім цього
інформація, яку ввів користувач, може бути збережена в якусь змінну і може
використовуватися далі в скрипті.

```python
In [2]: protocol = input('Routing protocol: ')
Routing protocol: OSPF

In [3]: print(protocol)
OSPF
```

У дужках зазвичай пишеться якийсь запит, який уточнює яку інформацію потрібно ввести.

Запит інформації зі скрипту (файл access_template_input.py):

```python
interface = input('Enter interface type and number: ')
vlan = input('Enter VLAN number: ')

access_template = ['switchport mode access',
                   'switchport access vlan {}',
                   'switchport nonegotiate',
                   'spanning-tree portfast',
                   'spanning-tree bpduguard enable']

print('\n' + '-' * 30)
print('interface {}'.format(interface))
print('\n'.join(access_template).format(vlan))
```


У перших двох рядках запитується інформація користувача.

Рядок ``print('\n' + '-' * 30)`` використовується для того, щоб візуально
відокремити запит інформації від виводу.

Виконання скрипту:

```
$ python access_template_input.py
Enter interface type and number: Gi0/3
Enter VLAN number: 55

------------------------------
interface Gi0/3
switchport mode access
switchport access vlan 55
switchport nonegotiate
spanning-tree portfast
spanning-tree bpduguard enable
```

