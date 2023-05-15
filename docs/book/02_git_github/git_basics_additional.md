# Додаткові можливості

## git diff

Команда git diff дозволяє переглянути різницю між різними станами. Наприклад,
на даний момент в репозиторії внесені зміни до файлу README і .gitignore.

Команда git status показує, що обидва файли змінені


.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_status_5.png

Команда git diff показує, які зміни було внесено з моменту останнього комміту

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_diff.png

Якщо додати зміни, внесені до файлів, в staging командою ``git add`` і ще раз
виконати команду ``git diff``, вона нічого не покаже

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_add_git_diff.png

Щоб показати відмінності між staging та останнім коммітом, треба додати параметр ``--staged``

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_diff_staged.png

Закомітити зміни

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_commit_2.png

## git log

Команда git log показує, коли було виконано останні зміни

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_log.png

За замовчуванням команда показує всі комміти, починаючи з найближчого часу. За
допомогою додаткових параметрів можна не тільки переглянути інформацію про
коміти, але й те, які зміни були внесені.

Опція ``-p`` дозволяє відобразити відмінності, внесені кожним коммітом.

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_log_p.png

Коротший варіант можна вивести з опцією ``--stat``

.. figure:: https://raw.githubusercontent.com/natenka/PyNEng/master/images/git/git_log_stat.png


