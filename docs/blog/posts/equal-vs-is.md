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
