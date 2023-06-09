# Робота зі своїм репозиторієм завдань

У цьому розділі описується, як створити свій репозиторій із копією файлів завдань.


## Створення репозиторію на GitHub

Для створення свого репозиторію на основі шаблону потрібно:

-  залогінитися на [GitHub](https://github.com/)
-  відкрити [репозиторій із завданнями](https://github.com/natenka/pynenguk-tasks)
-  натиснути «Use this template» та створити новий репозиторій на основі цього шаблону
-  у вікні треба ввести назву репозиторію
-  після цього готовий новий репозиторій із копією всіх файлів із вихідного репозиторію із завданнями

## Клонування репозиторію з GitHub

Для локальної роботи з репозиторієм його необхідно клонувати.
Для цього використовується команда git clone:

```
$ git clone ssh://git@github.com/natenka/my_pyneng_tasks.git
Cloning into 'my_pyneng_tasks'...
remote: Counting objects: 241, done.
remote: Compressing objects: 100% (191/191), done.
remote: Total 241 (delta 43), reused 239 (delta 41), pack-reused 0
Receiving objects: 100% (241/241), 119.60 KiB | 0 bytes/s, done.
Resolving deltas: 100% (43/43), done.
Checking connectivity... done.
```

Порівняно з наведеною в цьому лістингу командою вам потрібно змінити:

-  ім'я користувача natenka на ім'я користувача на GitHub
-  ім'я репозиторію my_pyneng_tasks на ім'я свого репозиторію на GitHub

У результаті, в поточному каталозі, в якому було виконано команду git clone,
з'явиться каталог з ім'ям репозиторію, в моєму випадку - "my_pyneng_tasks". У
цьому каталозі тепер міститься вміст репозиторію на GitHub.


## Робота з репозиторієм

Попередня команда не просто скопіювала репозиторій, щоб використовувати його
локально, але й налаштувала відповідним чином Git:

-  створено каталог .git
-  завантажено всі дані репозиторію
-  завантажено всі зміни, які були в репозиторії
-  репозиторій на GitHub налаштований як remote для локального репозиторію

Тепер готовий повноцінний локальний репозиторій Git, у якому ви можете
працювати. Зазвичай послідовність роботи буде такою:

-  перед початком роботи, синхронізація локального вмісту з GitHub командою git pull
-  зміна файлів репозиторію
-  додавання змінених файлів до staging командою git add
-  фіксація змін через коміт командою git commit
-  передача локальних змін у репозиторії на GitHub командою git push

При роботі із завданнями на роботі та вдома, треба звернути особливу увагу на перший та останній крок:

-  перший крок – оновлення локального репозиторію
-  останній крок – завантаження змін на GitHub


## Синхронізація локального репозиторію з віддаленим

Усі команди виконуються всередині каталогу репозиторію (у прикладі вище - my_pyneng_tasks).

Якщо вміст локального репозиторію однаковий з віддаленим, вивід буде таким:

```
$ git pull
Already up-to-date.
```

Якщо були зміни, виведення буде приблизно таким:

```
$ git pull
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 5 (delta 4), reused 5 (delta 4), pack-reused 0
Unpacking objects: 100% (5/5), done.
From ssh://github.com/natenka/my_pyneng_tasks
   89c04b6..fc4c721  master     -> origin/master
Updating 89c04b6..fc4c721
Fast-forward
 exercises/03_data_structures/task_3_3.py | 2 ++
 1 file changed, 2 insertions(+)
```

## Додавання нових файлів або змін до існуючих

Якщо потрібно додати конкретний файл (у даному випадку – README.md), потрібно
дати команду ``git add README.md``. Додавання всіх файлів поточної директорії
здійснюється командою ``git add .``.


## Коміт

Під час виконання комміту обов'язково треба вказати повідомлення. Краще, якщо
повідомлення буде зі змістом, а не просто «update» чи подібне. Коміт робиться
командою, подібною до ``git commit -m "Зроблені завдання 4.1-4.3"``.

## Push на GitHub

Для завантаження всіх локальних змін на GitHub використовується команда git
push:

```
$ git push origin master
Counting objects: 5, done.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 426 bytes | 0 bytes/s, done.
Total 5 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 4 local objects.
To ssh://git@github.com/natenka/my_pyneng_tasks.git
   fc4c721..edcf417  master -> master
```

Перед виконанням git push можна виконати команду ``git log -p origin/master..``
- вона покаже, які зміни ви збираєтеся додавати до свого репозиторію на GitHub.
