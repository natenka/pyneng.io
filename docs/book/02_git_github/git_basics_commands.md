# Робота з Git

Для керування Git використовуються різні команди, зміст яких пояснюється далі.

## git status

При роботі з Git важливо розуміти поточний статус репозиторію. Для цього у Git
є команда git status


.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_status_0.png

Git повідомляє, що ми знаходимося в гілці master (ця гілка створюється сама і
використовується за замовчуванням), і що йому нема чого додавати в коміт. Крім
цього, Git пропонує створити або скопіювати файли і після цього скористатися
командою git add, щоб Git почав стежити за ними.

Створення файлу README та додавання до нього рядка "test"

```
$ vi README
$ echo "test" >> README
```

Після цього запрошення виглядає таким чином

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/bash_prompt.png

У запрошенні показано, що є два файли, за якими Git ще не стежить

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_status_1.png

Два файли вийшло через те, що в даному випадку для Vim налаштовані undo-файли.
Це спеціальні файли, завдяки яким можна скасовувати зміни не тільки в поточній
сесії роботи з файлом, а й у минулі. Зауважте, що Git повідомляє, що є файли,
за якими він не стежить і підказує, якою командою це зробити.


## Файл .gitignore

Undo-файл .README.un~ – службовий файл, який не потрібно додавати до
репозиторію. Git має можливість вказати, які файли або каталоги потрібно
ігнорувати. Для цього потрібно створити відповідні шаблони у файлі .gitignore у
каталозі репозиторію.

Для того, щоб Git ігнорував undo-файли Vim, можна додати, наприклад, такий
рядок до файлу .gitignore

```
    *.un~
```

Це означає, що Git повинен ігнорувати всі файли, які закінчуються на .un ~.

Після цього, git status показує

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_status_2.png

Зверніть увагу, що тепер у виводі немає файлу .README.un~. Як тільки до
репозиторій було додано файл .gitignore, файли, які вказані в ньому, стали
ігноруватися.

## git add

Для того щоб Git почав стежити за файлами, використовується команда git add.

Можна вказати що слід стежити за конкретним файлом

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_add_readme.png

Або за всіма файлами

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_add_all.png

git status:

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_status_3.png

Тепер файли знаходяться у секції під назвою "Changes to be committed".

## git commit

Після того, як всі потрібні файли були додані в staging, можна змінити зміни.
Staging - це сукупність файлів, які будуть додані до наступного коміту. Команда
git commit має лише один обов'язковий параметр – опція "-m". Він дає змогу
вказати повідомлення для цього комміту.

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_commit_1.png

Після цього git status відображає

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_status_4.png

Фраза nothing to commit, working directory clean означає, що немає змін, які
потрібно додати до Git або закоммітити.
