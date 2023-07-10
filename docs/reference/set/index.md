# Множина (Set)

Множина — це змінюваний невпорядкований набір унікальних хешованих об'єктів.

Множини використовуються для тестування членства, видалення дублікатів із
послідовності та обчислення математичних операцій, таких як перетин,
об'єднання, різниця та симетрична різниця.

## Створення множин

[Літерал](/reference/syntax/#literals)

```python
set1 = {1, 2, 10, 20}
```

Порожня множина:

```python
set2 = set()
```

Створення множини із рядка:

```python
In [5]: set('long long long long string')
Out[5]: {' ', 'g', 'i', 'l', 'n', 'o', 'r', 's', 't'}
```

Створення множини зі списку:

```python
In [6]: set([10, 20, 30, 10, 10, 30])
Out[6]: {10, 20, 30}
```
