# for/else, while/else

У циклах for і while опціонально можна використовувати блок else.

## for/else

У циклі for:

* блок else виконується у разі, якщо цикл завершив ітерацію списку
* else не виконується, якщо в циклі було виконано break

Приклад циклу for з else (блок else виконується після завершення циклу for):

```python
In [1]: for num in range(5):
   ....:     print(num)
   ....: else:
   ....:     print("Числа закінчилися")
   ....:
0
1
2
3
4
Числа закінчилися
```

Приклад циклу for з else і break в циклі (через break блок else не виконується):

```python
In [2]: for num in range(5):
   ....:     if num == 3:
   ....:         break
   ....:     else:
   ....:         print(num)
   ....: else:
   ....:     print("Числа закінчилися")
   ....:
0
1
2
```

Приклад циклу for з else та continue у циклі (continue не впливає на блок else):

```python
In [3]: for num in range(5):
   ....:     if num == 3:
   ....:         continue
   ....:     else:
   ....:         print(num)
   ....: else:
   ....:     print("Числа закінчилися")
   ....:
0
1
2
4
Числа закінчилися
```

## while/else

У циклі while:

* блок else виконується в тому випадку, якщо умова в while хибно
* else не виконується, якщо в циклі було виконано break

Приклад циклу while з else (блок else виконується після завершення циклу while):

```python
In [4]: i = 0
In [5]: while i < 5:
  ....:     print(i)
  ....:     i += 1
  ....: else:
  ....:     print("Кінець")
  ....:
0
1
2
3
4
Кінець
```

Приклад циклу while з else та break у циклі (через break блок else не виконується):

```python
In [6]: i = 0

In [7]: while i < 5:
  ....:     if i == 3:
  ....:         break
  ....:     else:
  ....:         print(i)
  ....:         i += 1
  ....: else:
  ....:     print("Кінець")
  ....:
0
1
2
```
