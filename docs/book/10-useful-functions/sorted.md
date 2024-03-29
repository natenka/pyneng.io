# Функція sorted

Функція sorted повертає новий відсортований список елементів ітерованого
об'єкта, який було передано як аргумент. Функція також підтримує додаткові
параметри, які дозволяють контролювати сортування.

Синтаксис функції:

```python
sorted(iterable, /, *, key=None, reverse=False)
```

Перший аспект, на який важливо звернути увагу – sorted завжди повертає список,
незалежно від типу даних, переданого як аргумент.

Наприклад, для таких даних:

```python
list_of_words = ['one', 'two', 'list', '', 'dict']
tuple_of_words = ('one', 'two', 'list', '', 'dict')
set_of_words = {'one', 'two', 'list', '', 'dict'}
```

Результатом буде однаковий список:
```python
In [4]: sorted(list_of_words)
Out[4]: ['', 'dict', 'list', 'one', 'two']

In [5]: sorted(tuple_of_words)
Out[5]: ['', 'dict', 'list', 'one', 'two']

In [6]: sorted(set_of_words)
Out[6]: ['', 'dict', 'list', 'one', 'two']
```

Сортування рядка:

```python
In [7]: string_to_sort = 'long string'

In [8]: sorted(string_to_sort)
Out[8]: [' ', 'g', 'g', 'i', 'l', 'n', 'n', 'o', 'r', 's', 't']
```

Якщо передати sorted словник, функція поверне відсортований список ключів:

```python
dict_for_sort = {
    'id': 1,
    'name': 'London',
    'IT_VLAN': 320,
    'User_VLAN': 1010,
    'Mngmt_VLAN': 99,
    'to_name': None,
    'to_id': None,
    'port': 'G1/0/11'
}

In [10]: sorted(dict_for_sort)
Out[10]:
['IT_VLAN',
 'Mngmt_VLAN',
 'User_VLAN',
 'id',
 'name',
 'port',
 'to_id',
 'to_name']
```

## reverse

Параметр reverse дозволяє керувати порядком сортування. За замовчуванням
сортування буде за зростанням елементів.

Вказавши параметр reverse, можна змінити порядок:

```python
In [11]: list_of_words = ['one', 'two', 'list', '', 'dict']

In [12]: sorted(list_of_words)
Out[12]: ['', 'dict', 'list', 'one', 'two']

In [13]: sorted(list_of_words, reverse=True)
Out[13]: ['two', 'one', 'list', 'dict', '']
```

## key

ітерованого об'єкта

За допомогою параметра key можна вказувати, як саме сортувати елементи.
Параметр key очікує функцію яка приймає один аргумент. Функція використовується
для отримання ключа порівняння з кожного елемента ітерованого об'єкта. Значення
за замовчуванням — None (порівнюються безпосередньо елементи).

Наприклад, таким чином можна відсортувати список рядків за довжиною рядка:

```python
In [14]: list_of_words = ['one', 'two', 'list', '', 'dict']

In [15]: sorted(list_of_words, key=len)
Out[15]: ['', 'one', 'two', 'list', 'dict']
```

Якщо потрібно відсортувати список рядків, але ігнорувати регістр рядків, можна
створити функцію, яка переводить рядок у нижній регістр і використати її в key:

```python
def to_lower(string):
    return string.lower()

words = ['id', 'name', 'IT_VLAN', 'User_VLAN', 'Mngmt_VLAN', 'to_name', 'port']

In [6]: sorted(words, key=to_lower)
Out[6]: ['id', 'IT_VLAN', 'Mngmt_VLAN', 'name', 'port', 'to_name', 'User_VLAN']
```

Такий самий результат можна отримати з використанням методу lower:

```python
In [7]: sorted(words, key=str.lower)
Out[7]: ['id', 'IT_VLAN', 'Mngmt_VLAN', 'name', 'port', 'to_name', 'User_VLAN']
```

За допомогою параметра key можна сортувати об'єкти не за першим елементом, а за
будь-яким іншим. Але для цього треба створити додаткову функцію або
використовувати функцію lambda або спеціальні функції з модуля operator.

Наприклад, щоб відсортувати список кортежів із двох елементів за другим
елементом, можна використовувати такий прийом:

```python
from operator import itemgetter

list_of_tuples = [
    ('IT_VLAN', 320),
    ('Mngmt_VLAN', 99),
    ('User_VLAN', 1010),
    ('DB_VLAN', 11)
]

In [2]: sorted(list_of_tuples, key=itemgetter(1))
Out[2]: [('DB_VLAN', 11), ('Mngmt_VLAN', 99), ('IT_VLAN', 320), ('User_VLAN', 1010)]
```


## Приклад сортування різних об'єктів

Сортування виконується за першим елементом, наприклад, за першим символом у
списку рядків, якщо він збігається, за другим і так далі. Сортування
виконується за кодом Unicode символу.

Приклад сортування списку рядків:

```python
In [6]: data = ["test1", "test2", "text1", "text2"]

In [7]: sorted(data)
Out[7]: ['test1', 'test2', 'text1', 'text2']
```

Деякі дані будуть сортуватися "неправильно", наприклад, список IP-адрес:

```python
In [11]: ip_list = ["10.1.1.1", "10.1.10.1", "10.1.2.1", "10.1.11.1"]

In [12]: sorted(ip_list)
Out[12]: ['10.1.1.1', '10.1.10.1', '10.1.11.1', '10.1.2.1']
```

Таке сортування називається лексикографічним. Щоб у цьому випадку
сортування було нормальним, треба або використовувати окремий модуль з
натуральним сортуванням (модуль natsort) або сортувати, наприклад, за
двійковим/десятковим значенням адреси.

Приклад сортування IP-адрес за двійковим значенням. Спочатку створюємо функцію,
яка перетворює IP-адреси на двійковий формат:

```python
def bin_ip(ip):
    octets = [int(octet) for octet in ip.split(".")]
    return "{:08b}{:08b}{:08b}{:08b}".format(*octets)


In [16]: bin_ip("10.1.1.1")
Out[16]: '00001010000000010000000100000001'

In [17]: bin_ip("160.1.1.1")
Out[17]: '10100000000000010000000100000001'
```

Сортування за допомогою функції bin_ip:

```python
In [18]: ip_list = ["10.1.1.1", "10.1.10.1", "10.1.2.1", "10.1.11.1"]

In [19]: sorted(ip_list, key=bin_ip)
Out[19]: ['10.1.1.1', '10.1.2.1', '10.1.10.1', '10.1.11.1']
```


!!! note

    Також далі розглядатиметься модуль ipaddress, який дозволить створювати
    спеціальні об'єкти, які відповідають IP-адресі і вони вже сортуються
    правильно за десятковим значенням.

