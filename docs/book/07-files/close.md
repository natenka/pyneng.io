# Закриття файлів

У реальному житті для закриття файлів найчастіше використовується конструкція
with. Її набагато зручніше і безпечніше використовувати, ніж закривати файл
явно. Але, оскільки в житті можна зустріти і метод close, у цьому розділі
сприймається як його використовувати.

Після завершення роботи з файлом його потрібно закрити. У деяких випадках
Python може самостійно закрити файл. Але краще не розраховувати і закривати
файл явно.

## close

Метод close зустрічався у розділі запис файлів.  Там він був потрібний для
того, щоб вміст файлу був записаний на диск.

Для цього в Python є окремий метод flush. Але так як у прикладі із записом
файлів, не потрібно було виконувати жодних операцій, файл можна було закрити.

Відкриємо файл r1.txt:

```python
In [1]: f = open('r1.txt', 'r')
```

Тепер ми можемо прочитати файл:

```python

In [2]: print(f.read())
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

Об'єкт file має спеціальний атрибут closed, який дозволяє перевірити, закритий
файл чи ні. Якщо файл відкритий, він повертає False:

```python

In [3]: f.closed
Out[3]: False
```

Тепер закриваємо файл і знову перевіряємо closed:

```python

In [4]: f.close()

In [5]: f.closed
Out[5]: True
```

Якщо спробувати прочитати файл, виникне виняток:

```python
In [6]: print(f.read())
------------------------------------------------------------------
ValueError                       Traceback (most recent call last)
<ipython-input-53-2c962247edc5> in <module>()
----> 1 print(f.read())

ValueError: I/O operation on closed file
```
