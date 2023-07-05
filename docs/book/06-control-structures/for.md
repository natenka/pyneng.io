# for

Дуже часто ту саму дію необхідно виконати для набору даних одного типу.
Наприклад, перетворити всі рядки в списку на верхній регістр. Для виконання цих
дій Python використовує цикл for.

Цикл for перебирає елементи вказаної послідовності один за одним і виконує дії,
вказані в блоці for для кожного елемента.

Приклади послідовностей елементів, по яким цикл for може виконувати ітерацію:

* рядок
* список
* словник
* range
* будь-який ітерований об'єкт

Приклад перетворення рядків у списку на верхній регістр:

```python
In [10]: words = ['list', 'dict', 'tuple']

In [11]: upper_words = []

In [12]: for word in words:
    ...:     upper_words.append(word.upper())
    ...:

In [13]: upper_words
Out[13]: ['LIST', 'DICT', 'TUPLE']
```

Вираз `for word in words:` означає "для кожного слова в списку слів words виконати
дії в блоці for". У цьому випадку word - це ім'я змінної, яка посилається на
різні значення на кожній ітерації циклу.


!!! note

    [Проект pythontutor](http://www.pythontutor.com/) може дуже допомогти в
    розумінні циклів.  Візуалізація коду дозволяє побачити, що відбувається на
    кожному етапі виконання коду, що особливо корисно з циклами. Ви можете
    завантажити свій код на сайт pythontutor, але для прикладу перейдіть за цим
    посиланням, щоб переглянути
    [приклад вище](http://www.pythontutor.com/visualize.html#code=words%20%3D%20%5B'list',%20'dict',%20'tuple'%5D%0Aupper_words%20%3D%20%5B%5D%0A%0Afor%20word%20in%20words%3A%0A%20%20%20%20upper_words.append%28word.upper%28%29%29%0A&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false).

Цикл for може працювати з будь-якою послідовністю елементів.

Під час роботи з рядками цикл for виконує ітерацію по символах рядка,
наприклад:

```python
In [1]: for letter in 'Test string':
   ...:     print(letter)
   ...:
T
e
s
t

s
t
r
i
n
g
```

Цикл використовує змінну з іменем letter. Хоча ім'я може бути будь-яким,
найкраще, коли ім'я говорить вам, через які об'єкти виконуються ітерації.

Іноді потрібно використовувати послідовність чисел у циклі. У цьому випадку
можна використовувати функцію range.
Приклад циклу з функцією range:

```python
In [2]: for i in range(10):
   ...:     print(f'interface FastEthernet0/{i}')
   ...:
interface FastEthernet0/0
interface FastEthernet0/1
interface FastEthernet0/2
interface FastEthernet0/3
interface FastEthernet0/4
interface FastEthernet0/5
interface FastEthernet0/6
interface FastEthernet0/7
interface FastEthernet0/8
interface FastEthernet0/9
```

Функція range генерує числа в діапазоні від нуля до вказаного числа (у цьому
прикладі до 10), не враховуючи його.

У цьому прикладі перебирається список VLAN, тому змінну можна назвати vlan:

```python
In [3]: vlans = [10, 20, 30, 40, 100]
In [4]: for vlan in vlans:
   ...:     print(f'vlan {vlan}')
   ...:     print(f' name VLAN_{vlan}')
   ...:     
vlan 10
 name VLAN_10
vlan 20
 name VLAN_20
vlan 30
 name VLAN_30
vlan 40
 name VLAN_40
vlan 100
 name VLAN_100
```

Коли цикл for проходить через словник, він виконує ітерацію за ключами:

```python
r1 = {
     'ios': '15.4',
     'ip': '10.255.0.1',
     'hostname': 'london_r1',
     'location': '21 New Globe Walk',
     'model': '4451',
     'vendor': 'Cisco',
}


In [35]: for k in r1:
    ...:     print(k)
    ...:
ios
ip
hostname
location
model
vendor
```

Якщо потрібно вивести пари ключ-значення в циклі, можна зробити так:

```python
In [36]: for key in r1:
    ...:     print(key + ' => ' + r1[key])
    ...:
ios => 15.4
ip => 10.255.0.1
hostname => london_r1
location => 21 New Globe Walk
model => 4451
vendor => Cisco
```

Або скористатися методом items, який дозволяє отримати пару ключ-значення:

```python
In [37]: for key, value in r1.items():
    ...:     print(key + ' => ' + value)
    ...:
ios => 15.4
ip => 10.255.0.1
hostname => london_r1
location => 21 New Globe Walk
model => 4451
vendor => Cisco
```

