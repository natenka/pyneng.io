# Модуль subprocess


Модуль subprocess дозволяє створювати нові процеси. При цьому він може
підключатися до [стандартних потоків введення/виведення](https://uk.wikipedia.org/wiki/%D0%A1%D1%82%D0%B0%D0%BD%D0%B4%D0%B0%D1%80%D1%82%D0%BD%D1%96_%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%B8) 
та отримувати код повернення.

За допомогою subprocess можна, наприклад, виконувати будь-які команди Linux зі
скрипту. І залежно від ситуації отримувати виведення чи лише перевіряти, що
команда виконалася без помилок.


!!! note

    Цей модуль призначений для заміни кількох старих модулів і функцій:

    * `os.system`
    * `os.spawn*`


Рекомендований варіант роботи з модулем, це використання функції run для всіх
випадків використання, які вона може обробляти.  Для більш складних випадків
можна використовувати Popen (функція run всередині також використовує Popen).

## Функція ``subprocess.run``

Функція ``subprocess.run`` – основний спосіб роботи з модулем subprocess.

Синтаксис функції run:

```python
In [5]: subprocess.run?
Signature:
subprocess.run(
    *popenargs,
    input=None,
    capture_output=False,
    timeout=None,
    check=False,
    **kwargs,
)
```

Функція `subprocess.run` виконує команду описану аргументами popenargs, чекає,
поки команда завершиться і повертає екземпляр класу CompletedProcess.

У сигнатурі функції subprocess.run зазначена тільки частина параметрів для
налаштування роботи функції. Всі інші параметри заховані в `**kwargs` - тут
можна вказувати будь-які параметри [Popen](https://docs.python.org/3/library/subprocess.html#subprocess.Popen).

В документації в описі функції зазначено більше параметрів, але для повного переліку все ж треба звернутися до опису Popen:

```python
subprocess.run(args, *, stdin=None, input=None, stdout=None, stderr=None, capture_output=False, shell=False, cwd=None, timeout=None, check=False, encoding=None, errors=None, text=None, env=None, universal_newlines=None, **other_popen_kwargs)
```

Найпростіший варіант використання функції – запуск її таким чином:

```python
In [1]: import subprocess

In [2]: result = subprocess.run('ls')
ipython_as_mngmt_console.md  README.md         version_control.md
module_search.md             useful_functions
naming_conventions           useful_modules
```

У змінній результат тепер міститься спеціальний об'єкт CompletedProcess. З
цього об'єкта можна отримати інформацію про виконання процесу, наприклад, про
[код повернення](https://en.wikipedia.org/wiki/Exit_status) (це код, який
вказує статус завершення роботи, в найпростішому випадку, вдалий чи ні):

```python
In [3]: result
Out[3]: CompletedProcess(args='ls', returncode=0)

In [4]: result.returncode
Out[4]: 0
```

Код 0 означає, що програма виконалася успішно.

!!! warning

	Всі команди які передаються subprocess виконуються на Debian. Якщо ви
    використовуєте іншу ОС, потрібно змінити команди на відповідні для ОС.

Якщо потрібно викликати команду з аргументами, її потрібно передавати таким
чином (як список або будь-який інший ітерований об'єкт):

```python
In [15]: subprocess.run(['ls', '-l'])
total 32
-rw-r--r-- 1 vagrant vagrant   66 Jun 26  2023 basics_01_subprocess_ping.py
-rw-r--r-- 1 vagrant vagrant  359 Jun 26  2023 basics_02_subprocess_ping_func.py
-rw-r--r-- 1 vagrant vagrant  693 Jun 26  2023 basics_03_subprocess_popen_ping_func.py
-rw-r--r-- 1 vagrant vagrant  758 Jun 26  2023 basics_04_subprocess_popen_ping_func_zip.py
-rw-r--r-- 1 vagrant vagrant  688 Jun 26  2023 basics_05_subprocess_popen_ping_func_zip.py
-rw-r--r-- 1 vagrant vagrant  384 Jun 26  2023 basics_06_rich_progress_ping_func.py
-rw-r--r-- 1 vagrant vagrant  487 Jun 26  2023 basics_07_rich_colors_ping_func.py
drwxr-xr-x 2 vagrant vagrant 4096 Jun 26  2023 ipaddress
Out[15]: CompletedProcess(args=['ls', '-l'], returncode=0)
```

При спробі виконати команду з використанням wildcard-виразів, наприклад, якщо
використати `*`, виникне помилка:

```python
In [20]: subprocess.run(['ls', '-ls', '*rich*py'])
ls: cannot access '*rich*py': No such file or directory
Out[20]: CompletedProcess(args=['ls', '-ls', '*rich*py'], returncode=2)
```

Для того щоб викликати команди, в яких використовуються wildcard-вирази,
потрібно додавати аргумент shell і викликати команду таким чином (всю команду
пишемо в середині одного рядка):

```python
In [22]: subprocess.run('ls -ls *rich*py', shell=True)
4 -rw-r--r-- 1 vagrant vagrant 384 Jun 26  2023 basics_06_rich_progress_ping_func.py
4 -rw-r--r-- 1 vagrant vagrant 487 Jun 26  2023 basics_07_rich_colors_ping_func.py
Out[22]: CompletedProcess(args='ls -ls *rich*py', returncode=0)
```

Ще одна особливість функції run - вона очікує на завершення виконання команди.
Якщо спробувати, наприклад, запустити команду ping, цей аспект буде більш помітний:

```python
In [26]: subprocess.run(['ping', '-c', '3', '-n', '8.8.8.8'])
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=23.5 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=24.6 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=29.8 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2012ms
rtt min/avg/max/mdev = 23.467/25.974/29.836/2.770 ms
Out[26]: CompletedProcess(args=['ping', '-c', '3', '-n', '8.8.8.8'], returncode=0)
```

## Отримання результату виконання команди

За замовчуванням функція run виводить результат виконання команди на стандартний
потік виведення.

```python
In [5]: subprocess.run('ls')
basics_01_subprocess_ping.py                 basics_05_subprocess_popen_ping_func_zip.py
basics_02_subprocess_ping_func.py            basics_06_rich_progress_ping_func.py
basics_03_subprocess_popen_ping_func.py      basics_07_rich_colors_ping_func.py
basics_04_subprocess_popen_ping_func_zip.py  ipaddress
Out[5]: CompletedProcess(args='ls', returncode=0)


In [7]: result = subprocess.run('ls')
basics_01_subprocess_ping.py                 basics_05_subprocess_popen_ping_func_zip.py
basics_02_subprocess_ping_func.py            basics_06_rich_progress_ping_func.py
basics_03_subprocess_popen_ping_func.py      basics_07_rich_colors_ping_func.py
basics_04_subprocess_popen_ping_func_zip.py  ipaddress
```

Якщо результат виконання команди треба зберегти для подальшої обробки, можна
використовувати параметр `capture_output`:

```python
In [8]: result = subprocess.run('ls', capture_output=True)
```

Тепер можна отримати результат виконання команди таким чином:

```python
In [9]: result.stdout
Out[9]: b'basics_01_subprocess_ping.py\nbasics_02_subprocess_ping_func.py\nbasics_03_subprocess_popen_ping_func.py\nbasics_04_subprocess_popen_ping_func_zip.py\nbasics_05_subprocess_popen_ping_func_zip.py\nbasics_06_rich_progress_ping_func.py\nbasics_07_rich_colors_ping_func.py\nipaddress\n'
```

Зверніть увагу на літеру `b` перед рядком. Вона означає, що модуль повернув
вивід у вигляді байтового рядка. Для переведення байтового рядка у звичайний
рядок є два варіанти:

* використовувати метод decode для отриманого байтового рядка
* вказати аргумент encoding

Варіант із decode:


```python
In [11]: result.stdout.decode("utf-8")
Out[11]: 'basics_01_subprocess_ping.py\nbasics_02_subprocess_ping_func.py\nbasics_03_subprocess_popen_ping_func.py\nbasics_04_subprocess_popen_ping_func_zip.py\nbasics_05_subprocess_popen_ping_func_zip.py\nbasics_06_rich_progress_ping_func.py\nbasics_07_rich_colors_ping_func.py\nipaddress\n'
```

Варіант із encoding:

```python
In [12]: result = subprocess.run('ls', capture_output=True, encoding="utf-8")

In [13]: result.stdout
Out[13]: 'basics_01_subprocess_ping.py\nbasics_02_subprocess_ping_func.py\nbasics_03_subprocess_popen_ping_func.py\nbasics_04_subprocess_popen_ping_func_zip.py\nbasics_05_subprocess_popen_ping_func_zip.py\nbasics_06_rich_progress_ping_func.py\nbasics_07_rich_colors_ping_func.py\nipaddress\n'
```

## Отключение вывода


Иногда достаточно получения кода возврата и нужно отключить вывод
результата выполнения на стандартный поток вывода, и при этом сам
результат не нужен.
Это можно сделать, передав функции run аргумент stdout со значением
subprocess.DEVNULL:

```python

In [14]: result = subprocess.run(['ls', '-ls'], stdout=subprocess.DEVNULL)

In [15]: print(result.stdout)
None

In [16]: print(result.returncode)
0
```

Работа со стандартным потоком ошибок


Если команда была выполнена с ошибкой или не отработала корректно, вывод
команды попадет на стандартный поток ошибок.

Получить этот вывод можно так же, как и стандартный поток вывода:

```python

In [17]: result = subprocess.run(['ping', '-c', '3', '-n', 'a'], stderr=subprocess.PIPE, encoding='utf-8')
```

Теперь в result.stdout пустая строка, а в result.stderr находится
стандартный поток вывода:

```python

In [18]: print(result.stdout)
None

In [19]: print(result.stderr)
ping: unknown host a


In [20]: print(result.returncode)
2
```

Примеры использования модуля


Пример использования модуля subprocess (файл subprocess_run_basic.py):

```python

import subprocess

reply = subprocess.run(['ping', '-c', '3', '-n', '8.8.8.8'])

if reply.returncode == 0:
    print('Alive')
else:
    print('Unreachable')
```

Результат выполнения будет таким:

```

$ python subprocess_run_basic.py
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=43 time=54.0 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=43 time=54.4 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=43 time=53.9 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2005ms
rtt min/avg/max/mdev = 53.962/54.145/54.461/0.293 ms
Alive
```

То есть, результат выполнения команды выводится на стандартный поток
вывода.

Функція ping_ip проверяет доступность IP-адреса и возвращает True и
stdout, если адрес доступен, или False и stderr, если адрес недоступен
(файл subprocess_ping_function.py):

```python

import subprocess


def ping_ip(ip_address):
    """
    Ping IP address and return tuple:
    On success:
        * True
        * command output (stdout)
    On failure:
        * False
        * error output (stderr)
    """
    reply = subprocess.run(['ping', '-c', '3', '-n', ip_address],
                           stdout=subprocess.PIPE,
                           stderr=subprocess.PIPE,
                           encoding='utf-8')
    if reply.returncode == 0:
        return True, reply.stdout
    else:
        return False, reply.stderr

print(ping_ip('8.8.8.8'))
print(ping_ip('a'))
```

Результат выполнения будет таким:

```
$ python subprocess_ping_function.py
(True, 'PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.\n64 bytes from 8.8.8.8: icmp_seq=1 ttl=43 time=63.8 ms\n64 bytes from 8.8.8.8: icmp_seq=2 ttl=43 time=55.6 ms\n64 bytes from 8.8.8.8: icmp_seq=3 ttl=43 time=55.9 ms\n\n--- 8.8.8.8 ping statistics ---\n3 packets transmitted, 3 received, 0% packet loss, time 2003ms\nrtt min/avg/max/mdev = 55.643/58.492/63.852/3.802 ms\n')
(False, 'ping: unknown host a\n')
```
