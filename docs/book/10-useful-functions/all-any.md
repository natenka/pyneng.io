# Функції all та any

## Функція all

Функція all повертає True, якщо всі елементи істинні (або об'єкт порожній).

```python
In [1]: all([False, True, True])
Out[1]: False

In [2]: all([True, True, True])
Out[2]: True

In [3]: all([])
Out[3]: True
```

Наприклад, за допомогою all можна перевірити, чи всі октети в IP-адресі є числами:

```python
In [4]: ip = '10.0.1.1'

In [5]: all(i.isdigit() for i in ip.split('.'))
Out[5]: True

In [6]: all(i.isdigit() for i in '10.1.1.a'.split('.'))
Out[6]: False
```

## Функція any

Функція any повертає True, якщо хоча б один елемент істинний.

```python
In [7]: any([False, True, True])
Out[7]: True

In [8]: any([False, False, False])
Out[8]: False

In [9]: any([])
Out[9]: False

In [10]: any(i.isdigit() for i in '10.1.1.a'.split('.'))
Out[10]: True
```

## Приклад використання any

Наприклад, за допомогою any можна замінити функцію ignore_command:

```python
def ignore_command(command):
    ignore = ['duplex', 'alias', 'Current configuration']

    for word in ignore:
        if word in command:
            return True
    return False
```

На такий варіант:

```python
def ignore_command(command):
    ignore = ['duplex', 'alias', 'Current configuration']

    return any([word in command for word in ignore])
```
