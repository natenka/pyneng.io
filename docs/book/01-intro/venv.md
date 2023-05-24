# Віртуальні оточення

Віртуальні оточення:

* дозволяють ізолювати різноманітні проекти один від одного
* пакети, які потрібні різним проектам, перебувають у різних місцях – якщо, наприклад, у
  одному проекті потрібен пакет версії 1.0, а іншому проекті потрібен той самий
  пакет, але версії 3.1, вони не заважатимуть один одному
* пакети, встановлені у віртуальних оточеннях, не перебивають глобальні пакети


## Вбудований модуль venv

Починаючи з версії 3.5, у Python рекомендується використовувати модуль venv для
створення віртуальних оточень:

```
$ python3.11 -m venv ~/.venv/pyneng
```

Замість python3.11 можна використовувати python або python3, залежно від того,
як встановлено Python 3.11. Ця команда створює вказаний каталог і всі необхідні
каталоги всередині нього, якщо вони створені.

Команда створює таку структуру каталогів:

```
$ ls -ls ~/.venv/pyneng
total 16
4 drwxr-xr-x 2 nata nata 4096 Aug 21 14:50 bin
4 drwxr-xr-x 2 nata nata 4096 Aug 21 14:50 include
4 drwxr-xr-x 3 nata nata 4096 Aug 21 14:50 lib
4 -rw-r--r-- 1 nata nata   75 Aug 21 14:50 pyvenv.cfg
```

Для переходу у віртуальне оточення треба виконати команду:

```
$ source ~/.venv/pyneng/bin/activate
```

Для виходу з віртуального оточення використовується команда deactivate:

```
$ deactivate
```

Докладніше про модуль venv у [документації](https://docs.python.org/3/library/venv.html#module-venv).

### Встановлення пакетів у віртуальному оточенні

Наприклад, встановимо у віртуальному оточенні пакет simplejson.

```
(pyneng)$ pip install simplejson
...
Successfully installed simplejson
Cleaning up...
```

Якщо перейти в інтерпретатор Python і імпортувати simplejson, він доступний і ніяких помилок немає:

```
(pyneng)$ python
>>> import simplejson
>>> simplejson
<module 'simplejson' from '/home/nata/.venv/pyneng/lib/python3.11/site-packages/simplejson/__init__.py'>
>>>
```

Але якщо вийти з віртуального оточення і спробувати зробити те саме, то такого модуля немає:

```
(pyneng)$ deactivate 

$ python
>>> import simplejson
Traceback (most recent call last):
  File "<stdin>", line 1, in](module>
ModuleNotFoundError: No module named 'simplejson'
>>> 
```

