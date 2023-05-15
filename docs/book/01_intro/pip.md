# Система керування пакетами pip

Для встановлення пакетів Python використовуватиметься pip. Це система керування
пакетами, яка використовується для встановлення пакетів із Python Package Index
(PyPI). Швидше за все, якщо у вас вже встановлено Python, то встановлено pip.

Перевірка версії pip:

```
$ pip --version
pip 19.1.1 from /home/vagrant/venv/pyneng-py3-7/lib/python3.7/site-packages/pip (python 3.7)
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

## pip або pip3

Залежно від того, як встановлений та налаштований Python у системі, може
знадобитися використовувати pip3 замість pip. Щоб перевірити, який варіант
використовується, виконайте команду [[pip --version[[.

Варіант, коли pip відповідає Python 2.7:

```
$ pip --version
pip 9.0.1 from /usr/local/lib/python2.7/dist-packages (python 2.7)
```

Варіант, коли pip3 відповідає Python 3.7:

```
$ pip3 --version
pip 19.1.1 from /home/vagrant/venv/pyneng-py3-7/lib/python3.7/site-packages/pip (python 3.7)
```

Якщо в системі використовується pip3, то щоразу, коли в книзі встановлюється
модуль Python, потрібно буде замінити pip на pip3.

Також можна використати альтернативний варіант виклику pip:

```
$ python3.7 -m pip install tabulate
```

Таким чином, завжди зрозуміло для якої версії Python встановлюється пакет.




