# Корисні методи для роботи з рядками

При автоматизації дуже часто треба буде працювати з рядками, так як
конфігураційний файл, виведення команд і команди, що відправляються - це рядки.
Знання різних методів (дій), які можна застосовувати до рядків, допомагає
ефективно працювати з ними.

Рядки незмінний тип даних, тому всі методи, які перетворюють рядок повертають
новий рядок, а вихідний рядок залишається незмінним.

## Методи upper, lower, swapcase, capitalize

Методи ``upper``, ``lower``, ``swapcase``, ``capitalize`` виконують
перетворення регістра рядка:

```python
In [25]: string1 = 'FastEthernet'

In [26]: string1.upper()
Out[26]: 'FASTETHERNET'

In [27]: string1.lower()
Out[27]: 'fastethernet'

In [28]: string1.swapcase()
Out[28]: 'fASTeTHERNET'

In [29]: string2 = 'tunnel 0'

In [30]: string2.capitalize()
Out[30]: 'Tunnel 0'
```

Методи не перетворюють вихідний рядок, а повертають новий із виконаним
перетворенням. Це означає, що треба не забути записати його в якусь змінну
(можна в ту саму).

```python
In [31]: string1 = string1.upper()

In [32]: print(string1)
FASTETHERNET
```


## Метод join

Метод ``join`` збирає список рядків в один рядок із роздільником, який вказаний перед join:

```python
In [16]: vlans = ['10', '20', '30']

In [17]: ','.join(vlans)
Out[17]: '10,20,30'
```


> Метод join може збирати в рядок будь-який набір рядків, а не тільки список рядків.

## Метод count

Метод ``count`` використовується для підрахунку того, скільки разів символ або
підрядок зустрічаються у рядку:

```python
In [33]: string1 = 'Hello, hello, hello, hello'

In [34]: string1.count('hello')
Out[34]: 3

In [35]: string1.count('ello')
Out[35]: 4

In [36]: string1.count('l')
Out[36]: 8
```

## Метод find

Методу ``find`` можна передати підрядок або символ, і він покаже, на якій
позиції знаходиться перший символ підрядка (перший збіг):

```python
In [37]: string1 = 'interface FastEthernet0/1'

In [38]: string1.find('Fast')
Out[38]: 10

In [39]: string1[string1.find('Fast')::]
Out[39]: 'FastEthernet0/1'
```

Якщо збіг не виявлено, метод find повертає ``-1``.

## Методи startswith, endswith

Перевірка на те, чи починається чи закінчується рядок на певні символи (методи
``startswith``, ``endswith``):

```python
In [40]: string1 = 'FastEthernet0/1'

In [41]: string1.startswith('Fast')
Out[41]: True

In [42]: string1.startswith('fast')
Out[42]: False

In [43]: string1.endswith('0/1')
Out[43]: True

In [44]: string1.endswith('0/2')
Out[44]: False
```

Методам ``startswith`` і ``endswith`` можна передавати кілька значень
(обов'язково як кортеж):

```python
In [1]: "test".startswith(("r", "t"))
Out[1]: True

In [2]: "test".startswith(("r", "a"))
Out[2]: False

In [3]: "rtest".startswith(("r", "a"))
Out[3]: True

In [4]: "rtest".endswith(("r", "a"))
Out[4]: False

In [5]: "rtest".endswith(("r", "t"))
Out[5]: True
```


## Метод replace

Заміна послідовності символів у рядку на іншу послідовність (метод
``replace``):

```python
In [5]: string1 = 'FastEthernet0/1'

In [6]: string1.replace('Fast', 'Gigabit')
Out[6]: 'GigabitEthernet0/1'

In [7]: line = "aabb.cc10.a1a0"

In [8]: line.replace("a", "A")
Out[8]: 'AAbb.cc10.A1A0'
```


## Метод strip

У рядку часто будуть спеціальні символи: символ нового рядка, пробіли, таби.
Метод strip дозволяє видалити ці символи на початку та в кінці рядка.

```python
In [47]: string1 = '\n\tinterface FastEthernet0/1\n'

In [48]: print(string1)

    interface FastEthernet0/1


In [49]: string1
Out[49]: '\n\tinterface FastEthernet0/1\n'

In [50]: string1.strip()
Out[50]: 'interface FastEthernet0/1'
```


За замовчуванням метод strip забирає пробілові символи. Цей набір символів
містить: ``\t\n\r\f\v``.

Методу strip можна передати як аргумент будь-які символи. Тоді на початку та в
кінці рядка будуть видалені всі символи, які були вказані у рядку:

```python
In [51]: ad_metric = '[110/1045]'

In [52]: ad_metric.strip('[]')
Out[52]: '110/1045'
```

Метод strip прибирає вказані символи на початку і в кінці рядка. Якщо
необхідно прибрати символи лише ліворуч або праворуч, можна використовувати,
відповідно, методи lstrip і rstrip.

## Метод split

!!! abstract "[Метод split в довіднику](/reference/string/methods/split/)"

Метод split розбиває рядок на частини, використовуючи як роздільник якийсь
символ (або символи) та повертає список рядків:

```python
In [53]: string1 = 'switchport trunk allowed vlan 10,20,30,100'

In [54]: commands = string1.split()

In [55]: print(commands)
['switchport', 'trunk', 'allowed', 'vlan', '10,20,30,100']
```

У прикладі вище ``string1.split`` розбиває рядок за пробілом і повертає список рядків.
Список записаний у змінну commands.

За замовчуванням як роздільник використовуються пробільні символи (пробіли, таби,
символ нового рядка), але в дужках можна вказати будь-який роздільник:

```python
In [56]: vlans = commands[-1].split(',')

In [57]: print(vlans)
['10', '20', '30', '100']
```

У списку commands останній елемент - це рядок з вланами, тому використовується
індекс ``-1``. Потім рядок розбивається на частини за допомогою split
``commands[-1].split(',')``. Оскільки, як роздільник зазначена кома, отримано такий
список ``['10', '20', '30', '100']``.

Приклад поділу адреси на октети:

```python
In [10]: ip = "192.168.100.1"

In [11]: ip.split(".")
Out[11]: ['192', '168', '100', '1']
```

Корисна особливість методу split з роздільником за замовчуванням - рядок не
лише поділяється до списку рядків за пробіловими символами, але пробілові
символи також видаляються на початку та наприкінці рядка:

```python
In [58]: string1 = '  switchport trunk allowed vlan 10,20,30,100-200\n\n'

In [59]: string1.split()
Out[59]: ['switchport', 'trunk', 'allowed', 'vlan', '10,20,30,100-200']
```

У методу split є ще одна хороша особливість: за замовчуванням метод розбиває
рядок не за одним пробіловим символом, а за будь-якою кількістю. Це буде,
наприклад, дуже корисним при обробці команд show:

```python
In [60]: sh_ip_int_br = "FastEthernet0/0       15.0.15.1    YES manual up         up"

In [61]: sh_ip_int_br.split()
Out[61]: ['FastEthernet0/0', '15.0.15.1', 'YES', 'manual', 'up', 'up']
```

А ось так виглядає поділ того ж рядка, коли один пробіл використовується як
роздільник:

```python
In [62]: sh_ip_int_br.split(' ')
Out[62]:
['FastEthernet0/0', '', '', '', '', '', '', '', '', '', '', '', '15.0.15.1', '', '', '', '', '', '', 'YES', 'manual', 'up', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', 'up']
```

