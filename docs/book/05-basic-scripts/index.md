# 5. Створення базових скриптів

Якщо говорити загалом, то скрипт – це звичайний файл. У цьому файлі
зберігається послідовність команд, які потрібно виконати.

Почнемо із базового скрипту. Виведемо на стандартний потік виведення кілька
рядків.

Для цього потрібно створити файл access_template.py з таким вмістом:

```python
access_template = ['switchport mode access',
                   'switchport access vlan {}',
                   'switchport nonegotiate',
                   'spanning-tree portfast',
                   'spanning-tree bpduguard enable']

print('\n'.join(access_template).format(5))
```

Спочатку елементи списку об'єднуються в рядок, розділений символом ``\n``, а в
рядок підставляється номер VLAN, використовуючи форматування рядків.

Після цього потрібно зберегти файл і перейти до командного рядка.

Так виглядає виконання скрипту:

```python
$ python access_template.py
switchport mode access
switchport access vlan 5
switchport nonegotiate
spanning-tree portfast
spanning-tree bpduguard enable
```

Ставити розширення ``.py`` у файлу не обов'язково, але це бажано робити.

У книзі всі скрипти, які створюватимуться, використовують розширення ``.py``. Можна
сказати, що це гарний тон - створювати скрипти Python з таким розширенням.
