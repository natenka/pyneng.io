# Передача аргументів скрипту (argv)

Найчастіше скрипт вирішує якесь загальне завдання. Наприклад, скрипт обробляє
файл конфігурації. І щоб обробити інший файл конфігурації, треба вказувати його
якимось чином у коді. Звичайно, у такому разі не хочеться щоразу руками у скрипті
правити назву файлу.

Набагато краще передавати ім'я файлу як аргумент скрипту і потім
використовувати вже вказаний файл.

Модуль sys дає змогу працювати з аргументами скрипта за допомогою argv.

Приклад access_template_argv.py:

```python
from sys import argv

interface = argv[1]
vlan = argv[2]

access_template = ['switchport mode access',
                   'switchport access vlan {}',
                   'switchport nonegotiate',
                   'spanning-tree portfast',
                   'spanning-tree bpduguard enable']

print('interface {}'.format(interface))
print('\n'.join(access_template).format(vlan))
```

Перевірка роботи скрипту:

```
$ python access_template_argv.py Gi0/7 4
interface Gi0/7
switchport mode access
switchport access vlan 4
switchport nonegotiate
spanning-tree portfast
spanning-tree bpduguard enable
```


Аргументи, які були передані скрипту, підставляються як значення до шаблону.


![argv](https://pyneng.io/assets/images/05_sys_argv_example.png)

Тут треба пояснити кілька моментів:

* argv – це список
* всі аргументи знаходяться у списку у вигляді рядків
* argv містить не лише аргументи, які передали скрипту, але й назву самого скрипту

У цьому випадку у списку argv знаходяться такі елементи:

```
['access_template_argv.py', 'Gi0/7', '4']
```

Спочатку йде ім'я самого скрипта, потім аргументи в тому ж порядку в якому вони передавалися.
