# input

## Синтаксис

```python
input(prompt=None, /)
```

### Параметри

#### prompt

Запит, який потрібно показати користувачеві. Зазвичай це рядок.

!!! note

    Насправді як аргумент можна передати будь-який об'єкт, input перетворює
    його на рядок і відображає його.

### Значення, що повертається

Рядок.

## Приклади використання

input завжди повертає рядок:

```python
In [5]: input("Enter IP: ")
Enter IP: 10.1.1.1
Out[5]: '10.1.1.1'

In [6]: input("Enter mask: ")
Enter mask: 24
Out[6]: '24'
```

Input також можна використовувати, щоб призупинити виконання коду:
```python
input("Press Enter to Continue")
```

## Дивись також

Корисні сторонні модулі, які дозволяють робити більш зручний input із
підтвердженням, переліком дозволених значень, тощо.

* [rich.prompt](https://rich.readthedocs.io/en/latest/prompt.html)
* [click.prompt](https://click.palletsprojects.com/en/8.1.x/prompts/)

