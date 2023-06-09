# Додаткові можливості

## git diff

Команда git diff дозволяє переглянути різницю між різними станами. Наприклад,
на даний момент в репозиторії внесені зміни до файлу README і .gitignore.

Команда git status показує, що обидва файли змінені


![git](https://pyneng.io/assets/images/git_status_5.png)

Команда git diff показує, які зміни було внесено з моменту останнього комміту

![git](https://pyneng.io/assets/images/git_diff.png)

Якщо додати зміни, внесені до файлів, в staging командою ``git add`` і ще раз
виконати команду ``git diff``, вона нічого не покаже

![git](https://pyneng.io/assets/images/git_add_git_diff.png)

Щоб показати відмінності між staging та останнім коммітом, треба додати параметр ``--staged``

![git](https://pyneng.io/assets/images/git_diff_staged.png)

Закомітити зміни

![git](https://pyneng.io/assets/images/git_commit_2.png)

## git log

Команда git log показує, коли було виконано останні зміни

![git](https://pyneng.io/assets/images/git_log.png)

За замовчуванням команда показує всі комміти, починаючи з найближчого часу. За
допомогою додаткових параметрів можна не тільки переглянути інформацію про
коміти, але й те, які зміни були внесені.

Опція ``-p`` дозволяє відобразити відмінності, внесені кожним коммітом.

![git](https://pyneng.io/assets/images/git_log_p.png)

Коротший варіант можна вивести з опцією ``--stat``

![git](https://pyneng.io/assets/images/git_log_stat.png)


