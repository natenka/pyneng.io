# Основи Git

Git – це розподілена система контролю версій (Version Control System, VCS), яка
широко використовується та випущена під ліцензією GNU GPL v2. Вона може:

* відстежувати зміни у файлах
* зберігати кілька версій одного файла
* скасовувати внесені зміни
* реєструвати, хто та коли зробив зміни


Файл в Git може бути в такому стані:

* змінений (modified) - зміни у файлі ще не збережені у локальній базі даних
* індексований (staged) - файл позначений на додавання в наступний коміт
* збережений у коміті (committed) - файл збережено у локальній базі даних

Три основні частини проекту Git:

* робоча директорія - копія версії проекту
* індекс (staging area) - що буде збережено у наступному коміті
* директорія Git (.git) - тут система зберігає метадані та базу даних об’єктів вашого проекту

``` mermaid
sequenceDiagram
  participant WD as Робочий каталог
  participant SA as Індекс
  participant G as Каталог .git
  G->>WD: git checkout
  WD->>SA: git add
  SA->>G: git commit
```

## Установка Git

```
$ sudo apt-get install git
```

## Первинне налаштування Git

Для початку роботи з Git, необхідно вказати ім'я та e-mail користувача, які
будуть використовуватись для синхронізації локального репозиторію з
репозиторієм на GitHub:

```
$ git config --global user.name "username"
$ git config --global user.email "username.user@example.com"
```

Подивитися налаштування Git можна таким чином:

```
$ git config --list
```

## Ініціалізація репозиторію

Створення та перехід до каталогу first_repo


```
mkdir first_repo
cd first_repo
```

Ініціалізація репозиторію виконується за допомогою команди git init:

```
[~/tools/first_repo]
$ git init
Initialized empty Git repository in /home/vagrant/tools/first_repo/.git/
```

Після виконання цієї команди у поточному каталозі створюється папка .git, в
якій містяться службові файли, необхідні для Git.
