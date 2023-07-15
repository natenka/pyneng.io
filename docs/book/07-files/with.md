# Блок with

У Python існує більш зручний спосіб роботи з файлами, ніж ті, які
використовувалися досі - конструкція with.  Конструкція with називається
менеджер контексту.


```python
In [1]: with open('r1.txt', 'r') as f:
  ....:     for line in f:
  ....:         print(line)
  ....:
!
service timestamps debug datetime msec localtime show-timezone year
service timestamps log datetime msec localtime show-timezone year
service password-encryption
service sequence-numbers
!
no ip domain lookup
!
ip ssh version 2
!
```

З конструкцією with можна використовувати не тільки цикл for, а й всі
методи, що розглядалися до цього:


```python
In [4]: with open('r1.txt', 'r') as f:
  ....:     print(f.read())
  ....:
!
service timestamps debug datetime msec localtime show-timezone year
service timestamps log datetime msec localtime show-timezone year
service password-encryption
service sequence-numbers
!
no ip domain lookup
!
ip ssh version 2
!
```

## Відкриття двох файлів

Іноді потрібно працювати одночасно із двома файлами. Наприклад, треба записати
деякі рядки з одного файлу, до іншого.

У такому випадку, у блоці with можна відкривати два файли таким чином:

```python
with open('r1.txt') as src, open('result.txt', 'w') as dest:
    for line in src:
        if line.startswith('service'):
            dest.write(line)


In [6]: cat result.txt
service timestamps debug datetime msec localtime show-timezone year
service timestamps log datetime msec localtime show-timezone year
service password-encryption
service sequence-numbers
```

Це рівнозначно таким двом блокам with:

```python
with open('r1.txt') as src:
    with open('result.txt', 'w') as dest:
        for line in src:
            if line.startswith('service'):
                dest.write(line)
```
