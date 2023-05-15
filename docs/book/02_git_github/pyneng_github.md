# Робота з репозиторієм прикладів

Усі приклади з лекцій [курсу](https://pynenguk.natenka.io/course/) викладено в окремому `репозиторії](https://github.com/natenka/pynenguk-examples).

## Копіювання репозиторію з GitHub

Приклади оновлюються, тому зручніше буде клонувати цей репозиторій на свою
машину та періодично оновлювати його.

Для копіювання репозиторію з GitHub виконайте команду git clone:

```
$ git clone https://github.com/natenka/pynenguk-examples
Cloning into 'pynenguk-examples'...
remote: Counting objects: 1263, done.
remote: Compressing objects: 100% (504/504), done.
remote: Total 1263 (delta 735), reused 1263 (delta 735), pack-reused 0
Receiving objects: 100% (1263/1263), 267.10 KiB | 444.00 KiB/s, done.
Resolving deltas: 100% (735/735), done.
Checking connectivity... done.
```

## Оновлення локальної копії репозиторію

При необхідності оновити локальний репозиторій, щоб синхронізувати його з
версією на GitHub, потрібно виконати git pull, перебуваючи всередині створеного
каталогу pynenguk-examples.

Якщо оновлень не було, вивід буде таким:

```
$ git pull
Already up-to-date.
```

Якщо оновлення були, результат буде приблизно таким:

```
$ git pull
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 2), reused 3 (delta 2), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/natenka/pynenguk-examples
   49e9f1b..1eb82ad  master     -> origin/master
Updating 49e9f1b..1eb82ad
Fast-forward
 README.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Зверніть увагу на інформацію про те, що змінився лише файл README.md.

## Перегляд змін

Якщо ви хочете подивитися, які зміни були внесені, можна скористатися командою
git log:

```
$ git log -p -1
commit 98e393c27e7aae4b41878d9d979c7587bfeb24b4
Author: Наталія Самойленко](test@gmail.com>
Date:   Fri Aug 18 17:32:07 2017 +0300

    Update task_x_x.py

diff --git a/exercises/task_x_x.py b/exercises/task_x_x.py
index c4307fa..137a221 100644
--- a/exercises/task_x_x.py
+++ b/exercises/task_x_x.py
@@ -13,11 +13,12 @@
 * застосувати ACL до інтерфейсу

 ACL має бути таким
+
 ip access-list extended INET-to-LAN
  permit tcp 10.0.1.0 0.0.0.255 any eq www
  permit tcp 10.0.1.0 0.0.0.255 any eq 22
  permit icmp any any
-
+
```

Перевірте роботу Playbook на маршрутизаторі R1.

В этой команде флаг ``-p`` указывает, что надо отобразить вывод утилиты
Linux diff для внесённых изменений, а не только сообщение коммита. В
свою очередь, ``-1`` указывает, что надо показать только один самый свежий
коммит.

У цій команді опція ``-p`` вказує, що треба відобразити вихід утиліти Linux
diff для внесених змін, а не лише повідомлення комміту. У свою чергу, ``-1``
вказує, що треба показати лише один найсвіжіший коміт.


## Перегляд змін, які будуть синхронізовані


Попередній варіант git log спирається на кількість коммітів, але це не завжди
зручно. До виконання команди git pull можна переглянути, які зміни були
виконані з моменту останньої синхронізації.

Для цього використовується наступна команда:

```
$ git log -p ..origin/master
commit 4c1821030d20b3682b67caf362fd777d098d9126
Author: Наталія Самойленко](test@gmail.com>
Date:   Mon May 29 07:53:45 2017 +0300

Update README.md

diff --git a/tools/README.md b/tools/README.md
index 2b6f380..4f8d4af 100644
--- a/tools/README.md
+++ b/tools/README.md
@@ -1 +1,4 @@
+
```

У цьому випадку зміни були лише в одному файлі. Ця команда буде дуже корисною
для того, щоб подивитися, які зміни були внесені до формулювання завдань та
яких саме завдань. Так буде легше орієнтуватися і розуміти, чи це стосується
завдань, які ви вже зробили, і якщо стосується, то чи треба їх змінювати.

> "..origin/master" у команді git log -p ..origin/master означає показати всі
> комміти, які є в origin/master (в даному випадку, це GitHub), але яких
> немає в локальній копії репозиторію

Якщо зміни були в тих завданнях, які ви ще не робили, цей вивід підкаже, які
файли потрібно скопіювати з репозиторію курсу у ваш особистий репозиторій (а
може бути весь розділ, якщо ви ще не робили завдання з цього розділу).
