# Нюанси виконання завдань на Windows

Модуль pexpect не працює на Windows і оскільки він не потрібен для виконання
завдань, це впливає лише на те, що не вдасться повторити приклади з лекції.

Решта модулів працюють, але з деякими є нюанси.

### graphviz

Для малювання схеми у завданнях в 11 та 17 розділі буде потрібен graphviz.
І потрібно буде встановити модуль Python:
```
pip install graphviz
```

І додаток [graphviz](https://graphviz.gitlab.io/_pages/Download/Download_windows.html)

Після установки треба додати [graphviz до PATH](https://bobswift.atlassian.net/wiki/spaces/GVIZ/pages/131924165/Graphviz+installation)

### csv

При роботі з csv на Windows завжди потрібно вказувати `newline=""` під час відкриття файлу:

```
    with open(output, "w", newline="") as dest:
        writer = csv.writer(dest)
```


