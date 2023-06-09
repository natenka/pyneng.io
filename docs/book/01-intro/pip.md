# Система керування пакетами pip

Для встановлення пакетів Python використовуватиметься pip. Це система керування
пакетами, яка використовується для встановлення пакетів із Python Package Index
(PyPI). Швидше за все, якщо у вас вже встановлено Python, то встановлено pip.

Перевірка версії pip:

```
$ pip --version
pip 23.1.2 from /home/nata/.venv/pyneng/lib/python3.11/site-packages/pip (python 3.11)
```

Якщо команда видала помилку, то pip не встановлений. Установка pip описана у
[документації](https://pip.pypa.io/en/stable/installing/)

## Встановлення модулів

Для встановлення модулів використовується команда pip install:

```
$ pip install tabulate
```

Видалення пакета виконується таким чином:

```
$ pip uninstall tabulate
```

Крім того, іноді необхідно оновити пакет:

```
$ pip install --upgrade tabulate
```

або так:
```
$ pip install -U tabulate
```

## pip або pip3

Залежно від того, як встановлений та налаштований Python у системі, може
знадобитися використовувати pip3 замість pip. Щоб перевірити, який варіант
використовується, виконайте команду ``pip --version``.

Варіант, коли pip відповідає Python 2.7:

```
$ pip --version
pip 9.0.1 from /usr/local/lib/python2.7/dist-packages (python 2.7)
```

На сучасних версіях ОС, найімовірніше, системний Python буде версії 3.x. Наприклад, для Debian bullseye:

```
$ pip --version
pip 20.3.4 from /usr/lib/python3/dist-packages/pip (python 3.9)
```

Варіант, коли pip3 відповідає Python 3.9:

```
$ pip3 --version
pip 20.3.4 from /usr/lib/python3/dist-packages/pip (python 3.9)
```

Якщо в системі використовується pip3, то щоразу, коли в книзі встановлюється
модуль Python, потрібно буде замінити pip на pip3.

Також можна використати альтернативний варіант виклику pip:

```
$ python3.11 -m pip install tabulate
```

Таким чином, завжди зрозуміло для якої версії Python встановлюється пакет.


