# type

З одним аргументом повертає тип об'єкта. Значення, що повертається, є 
типом та, як правило, тим самим об'єктом, який повертає object.__class__.

Для перевірки типу об'єкта рекомендується використовувати вбудовану функцію
[isinstance](/reference/functions/isinstance/), оскільки вона враховує підкласи.


## Синтаксис

```python
type(object)
```

!!! note "[Це не повний синтаксис type, за повним варіантом звертайтесь до документації](https://docs.python.org/3/library/functions.html#type)"

### Параметри

#### object

Будь-який об'єкт Python.

### Значення, що повертається

Тип.

## Приклади використання

```python
In [30]: numbers = [1, 2, 3]

In [31]: type(numbers)
Out[31]: list

In [32]: type(numbers) == list
Out[32]: True
```

З type можна перевіряти тільки конкретний тип, успадкування не працює:

```python
In [33]: from collections.abc import Iterable

In [34]: type(numbers) == Iterable
Out[34]: False
```

### Приклад використання всередині класу

Тут type використовується для додавання імені класу до str/repr без введення
його вручну:

```python
from datetime import datetime


class Task:
    def __init__(self, title, description=None, due=None):
        self.title = title
        self.description = description
        if due is None:
            self.due = datetime.now().date()
        else:
            self.due = datetime.strptime(due, "%d/%m/%Y").date()

    def __str__(self):
        return f"{type(self).__name__}('{self.title}')"

    def __repr__(self):
        return f"<{type(self).__name__} title='{self.title}' due={self.due}>"


if __name__ == "__main__":
    t1 = Task("task1", due="15/09/2023")
    t2 = Task("task2")
```

```python
In [2]: str(t1)
Out[2]: "Task('task1')"

In [3]: repr(t1)
Out[3]: "<Task title='task1' due=2023-09-15>"
```

У цьому випадку при успадкуванні класу ім'я буде ім'ям дочірнього класу:

```python
class ScheduledTask(Task):
    pass


In [6]: t3 = ScheduledTask("task1", due="15/09/2023")

In [7]: str(t3)
Out[7]: "ScheduledTask('task1')"

In [8]: repr(t3)
Out[8]: "<ScheduledTask title='task1' due=2023-09-15>"
```

## Дивись також

#### [isinstance](/reference/functions/isinstance/)
