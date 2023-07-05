---
# draft: true 
date: 2023-07-04
categories:
  - python
tags:
  - basics
---

# Відмінності між `a == b` та `a is b`

`==` перевіряє значення, а `is` перевіряє, що обидві змінні посилаються на той
самий об'єкт. Для перевірки того, що значення однієї змінної
дорівнює якомусь іншому значенню, треба використовувати `==`.

<!-- more -->

Із рекомендацій PEP 8: порівняння з `None`, завжди слід робити з `is` або `is not`, ніколи не з
операторами рівності `==`, `!=`:

```python
data is None
data is not None
```

!!! quote "[PEP 8](https://peps.python.org/pep-0008/#programming-recommendations)"

	Comparisons to singletons like `None` should always be done with `is` or `is not`, never the equality operators.

	Also, beware of writing `if x` when you really mean `if x is not None` – e.g.
    when testing whether a variable or argument that defaults to None was set to
    some other value. The other value might have a type (such as a container) that
    could be false in a boolean context!

В інших випадках краще використовувати `==`:

```python
len(data) == 4
len(data) != 4
```


Приклад використання `is` (sw2 посилається на той самий список, що і sw1):

```python
In [1]: sw1 = [10, 20, 30]

In [2]: sw2 = sw1

In [3]: sw1 is sw2
Out[3]: True

In [4]: sw1 == sw2
Out[4]: True
```

Змінні sw1 та sw2 посилаються на різні об'єкти з однаковими елементами:
```python
In [6]: sw1 = [10, 20, 30]

In [7]: sw2 = [10, 20, 30]

In [8]: sw1 is sw2
Out[8]: False

In [9]: sw1 == sw2
Out[9]: True
```


## True/False

!!! quote "[PEP 8](https://peps.python.org/pep-0008/#programming-recommendations)"

	Don't compare boolean values to True or False using `==`:

	```python
	# Correct:
    if greeting:
	```

	```python
	# Wrong:
	if greeting == True:
	```

	Worse:
	```python
	# Wrong:
	if greeting is True:
	```

Відповідно до рекомендацій PEP8, щоб перевірити, що якийсь об'єкт дорівнює True
або False, краще використовувати такі вирази:
```python
if value: # для True
    print("істинне значення")

if not value: # для False
    print("хибне значення")
```

## Приклади використання `is` поза темами курсу

Навчальний приклад [функції для скасування задач, яка має скасувати всі задачі, окрім себе](https://github.com/pyneng/advpyneng-course-examples/blob/main/examples/19_inside_asyncio/example_19_0x_task_cancel.py#L31)

```python
async def cancel_all_tasks():
    tasks = [
        task for task in asyncio.all_tasks()
        if task is not asyncio.current_task()
    ]
    [task.cancel() for task in tasks]
    await asyncio.gather(*tasks, return_exceptions=True)
```


