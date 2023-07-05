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
самий об'єкт. Відповідно для перевірки того, що значення однієї змінної
дорівнює якомусь іншому значенню, треба використовувати `==`.

`is` може використовуватися при перевірці, що значення дорівнює None:

```python
data is None
data is not None
```

В інших випадках краще використовувати `==`:

```python
len(data) == 4
len(data) != 4
```

<!-- more -->

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

!!! quote "PEP8"

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
