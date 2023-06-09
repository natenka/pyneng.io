# break, continue, pass

Python має кілька операторів, які дозволяють змінювати поведінку циклів за замовчуванням.

## Оператор break

Оператор break дозволяє достроково перервати цикл:

* break перериває поточний цикл і продовжує виконання наступних виразів
* якщо використовується кілька вкладених циклів, break перериває внутрішній цикл і продовжує виконувати вирази, що йдуть за блоком
* break може використовуватися в циклах for та while

Приклад із циклом for:

```python
In [1]: for num in range(10):
   ...:     if num < 7:
   ...:         print(num)
   ...:     else:
   ...:         break
   ...:     
0
1
2
3
4
5
6
```

Приклад із циклом while:

```python
In [2]: i = 0

In [3]: while i < 10:
   ...:     if i == 5:
   ...:         break
   ...:     else:
   ...:         print(i)
   ...:         i += 1
   ...:         
0
1
2
3
4
```

Використання break у прикладі із запитом пароля (файл
check_password_with_while_break.py):

```python
username = input("Введіть ім'я користувача: ")
password = input("Введіть пароль: ")

while True:
    if len(password) < 8:
        print("Пароль надто короткий\n")
    elif username in password:
        print("Пароль містить ім'я користувача\n")
    else:
        print("Пароль для користувача {} встановлено".format(username))
        # завершує цикл while
        break
    password = input("Введіть пароль ще раз: ")
```

Тепер можна не повторювати рядок
``password = input("Введіть пароль ще раз: ")``
у кожному відгалуженні, достатньо перенести його в кінець циклу.


І як тільки буде введено правильний пароль, break виведе програму з циклу while.

## Оператор continue

Оператор continue повертає керування на початок циклу. Тобто, continue дозволяє
"перестрибнути" вирази, що залишилися в циклі і перейти до наступної ітерації.

Приклад із циклом for:

```python
for num in range(5):
    if num == 3:
        continue
    else:
        print(num)
```

Результат
```
0
1
2
4
```

Приклад із циклом while:

```python
i = 0

while i < 6:
    i += 1
    if i == 3:
        print("Пропускаємо 3")
        continue
        print("Це ніхто не побачить")
    else:
        print("Поточне значення: ", i)
```

Вивід
```
Поточне значення:  1
Поточне значення:  2
Пропускаємо 3
Поточне значення:  4
Поточне значення:  5
Поточне значення:  6
```

Використання continue у прикладі із запитом пароля (файл
check_password_with_while_continue.py):

```python
username = input("Введіть ім'я користувача: ")
password = input("Введіть пароль: ")

password_correct = False

while not password_correct:
    if len(password) < 8:
        print("Пароль надто короткий\n")
    elif username in password:
        print("Пароль містить ім'я користувача\n")
    else:
        print("Пароль для користувача {} встановлено'.format(username))
        password_correct = True
        continue
    password = input("Введіть пароль ще раз: ")
```

Тут вихід із циклу виконуються за допомогою перевірки змінної-прапорця password_correct.
Коли було введено правильний пароль, прапор виставляється рівним True, і з
допомогою continue виконується перехід початку циклу, перескочивши останній
рядок із запитом пароля.

Результат виконання буде таким:

```
$ python check_password_with_while_continue.py
Введіть ім'я користувача: nata
Введіть пароль: nata12
Пароль надто короткий

Введіть пароль ще раз: natalksdjflsdjf
Пароль містить ім'я користувача

Введіть пароль ще раз: asdfsujljhdflaskjdfh
Пароль для користувача nata встановлено
```


## Оператор pass

Оператор pass нічого не робить. Фактично це така заглушка для блоків коду.

Наприклад, pass може допомогти ситуації, коли потрібно прописати структуру
скрипта. Його можна ставити у циклах, функціях, класах. І це не впливатиме на
виконання коду.

Приклад використання pass:

```python
for num in range(5):
    if num < 3:
        pass
    else:
        print(num)
```

Результат
```
3
4
```
