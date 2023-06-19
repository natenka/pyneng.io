# type

## Синтаксис

```python
class type(object)
```

!!! note "[Це не повний синтаксис type, за повним варіантом звертайтесь до документації](https://docs.python.org/3/library/functions.html#type)"

### Параметри

#### object

Будь-який об'єкт Python.

### Значення, що повертається

Тип.

## Приклади використання

```python
In [30]: numbers = [1, 2, 3]

In [31]: type(numbers)
Out[31]: list

In [32]: type(numbers) == list
Out[32]: True
```

З type можна перевіряти тільки конкретний тип, успадкування не працює:

```python
In [33]: from collections.abc import Iterable

In [34]: type(numbers) == Iterable
Out[34]: False
```

## Дивись також

#### [isinstance](/reference/functions/isinstance/)
