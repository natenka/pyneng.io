# Підготовка віртуальної машини/хоста Linux

Якщо ви бажаєте самостійно підготувати віртуальну машину або працювати без
віртуалки, вам потрібно буде встановити Python 3.8-3.11.  За замовчуванням,
краще встановити Python 3.11, оскільки у 3.10-3.11 покращилося відображення
помилок.  Якщо щось піде не так під час встановлення Python 3.11, можна
спробувати версію менше.

> [Встановлення Python на різних ОС](https://realpython.com/installing-python/)


## Встановлення Python

У цій інструкції Python 3.11 встановлюється на Debian, не перебиваючи версію Python за замовчуванням.

Якщо інсталяція виконується на чистій ОС, краще встановити ці пакети:
```
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev
sudo apt-get install libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev
```

Установка Python 3.11
```
wget https://www.python.org/ftp/python/3.11.2/Python-3.11.2.tgz
tar xvf Python-3.11.2.tgz
cd Python-3.11.2
./configure --enable-optimizations --enable-loadable-sqlite-extensions
sudo make altinstall
```

Після цього можна створювати віртуальне оточення.

## Створення віртуального оточення

Віртуальні оточення:

* дозволяють ізолювати різноманітні проекти один від одного
* пакети, які потрібні різним проектам, перебувають у різних місцях – якщо,
  наприклад, у одному проекті потрібен пакет версії 1.0, а іншому проекті
  потрібен той самий пакет, але версії 3.1, вони не заважатимуть один одному
* пакети, встановлені у віртуальних оточеннях, не перебивають глобальні пакети

Створення нового віртуального оточення, в якому Python 3.11 використовується за замовчуванням:
```
$ python3.11 -m venv ~/.venv/pyneng-course-3.11
```

Для переходу у віртуальне оточення треба виконати команду (Linux/Mac):
```
$ source ~/.venv/pyneng-course-3.11/bin/activate
```

Для виходу з віртуального оточення використовується команда deactivate:
```
deactivate
```

### Список модулів

Список модулів, які потрібно встановити (ця команда оновить модулі, якщо вони вже встановлені):

```
pip install -U pytest pytest-clarity ipython pyyaml tabulate jinja2 textfsm graphviz
```

Також треба встановити graphviz:

```
apt-get install graphviz
```

