# Функція enumerate

Функція enumerate очікує як аргумент ітерований об'єкт і повертає ітератор, у
якому кожен елемент є кортежем із двох елементів: числа та елементу ітерованого об'єкту.


Синтаксис:

```python
enumerate(iterable, start=0)
```

Приклад:

```python
In [5]: list1 = ['str1', 'str2', 'str3']

In [6]: for position, string in enumerate(list1):
   ...:     print(position, string)
   ...:
0 str1
1 str2
2 str3
```

Enumerate вміє генерувати числа не тільки з нуля, але і з будь-якого значення,
яке йому вказали в параметрі start:

```python
In [7]: list1 = ['str1', 'str2', 'str3']

In [8]: for position, string in enumerate(list1, 100):
   ...:     print(position, string)
   ...:
100 str1
101 str2
102 str3
```

Важливою особливістю enumerate є те, що його можна використовувати з
ітераторами і разом з перебором елементів enumerate, будуть перебиратися і
елементи іншого ітератора.
