# Імпорт модуля

У Python є кілька способів імпорту модуля:

* ``import module``
* ``import module as sn``
* ``from module import object``
* ``from module import *``

## import module

Варіант `import module`:

```python
In [1]: dir()
Out[1]: 
['In',
 'Out',
 ...
 'exit',
 'get_ipython',
 'quit']

In [2]: import os

In [3]: dir()
Out[3]: 
['In',
 'Out',
 ...
 'exit',
 'get_ipython',
 'os',
 'quit']
```

Після імпорту модуль os з'явився у виводі dir. Це означає, що він тепер у
поточному іменному просторі.

Щоб викликати якусь функцію або метод із модуля os, треба вказати `os.` а потім
ім'я об'єкта:

```python
In [4]: os.getlogin()
Out[4]: 'nata'
```

Перевага цього варіанта імпорту в тому, що об'єкти модуля не потрапляють до
іменного простору поточної програми. Тобто якщо створити функцію з ім'ям
`getlogin`, вона не буде конфліктувати з аналогічною функцією модуля os.

!!! note

    Якщо в імені файлу міститься точка, стандартний спосіб імпортування не
    працюватиме. Для таких випадків використовується 
    [інший спосіб](http://stackoverflow.com/questions/1828127/how-to-reference-python-package-when-filename-contains-a-period/1828249#1828249).

## import module as

Конструкція `import module as` дозволяє імпортувати модуль під іншим ім'ям (як
правило, коротшим):

```python
In [1]: import subprocess as sp

In [2]: sp.check_output('ping -c 2 -n  8.8.8.8', shell=True)
Out[2]: 'PING 8.8.8.8 (8.8.8.8): 56 data bytes\n64 bytes from 8.8.8.8: icmp_seq=0 ttl=48 time=49.880 ms\n64 bytes from 8.8.8.8: icmp_seq=1 ttl=48 time=46.875 ms\n\n--- 8.8.8.8 ping statistics ---\n2 packets transmitted, 2 packets received, 0.0% packet loss\nround-trip min/avg/max/stddev = 46.875/48.377/49.880/1.503 ms\n'
```


## from module import object

Варіант `from module import object` зручно використовувати, коли з усього
модуля потрібні лише одна-дві функції:

```python
In [1]: from os import getlogin, getcwd
```

Тепер ці функції доступні у поточному іменному просторі:

```python
In [2]: dir()
Out[2]: 
['In',
 'Out',
 ...
 'exit',
 'get_ipython',
 'getcwd',
 'getlogin',
 'quit']
```

Їх можна викликати без імені модуля:

```python
In [3]: getlogin()
Out[3]: 'nata'

In [4]: getcwd()
Out[4]: '/home/vagrant/repos/examples/'
```

## from module import *

Варіант `from module import *` імпортує всі імена модуля в поточний іменний простір:
Це імпортує всі імена, крім тих, що починаються з підкреслення `_`. У більшості
випадків програмісти Python не використовують цю можливість, оскільки вона
вводить невідомий набір імен в інтерпретатор, можливо, приховуючи деякі речі,
які ви вже визначили.

```python
In [1]: from os import *

In [2]: dir()
Out[2]: 
['EX_CANTCREAT',
 'EX_CONFIG',
 ...
 'wait',
 'wait3',
 'wait4',
 'waitpid',
 'walk',
 'write']
```

У модулі os дуже багато об'єктів, тому список скорочено.

Такий варіант імпорту краще не використовувати. При такому імпорті кодом
незрозуміло, що якусь функцію взято, наприклад, з модуля os.
Це істотно ускладнює розуміння коду.
