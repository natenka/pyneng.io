# isinstance

## Синтаксис

```python
isinstance(object, classinfo)
```

### Параметри

#### object

Будь-який об'єкт Python.

#### classinfo

Тип або кортеж типів.

### Значення, що повертається

True/False

### Виняток

Якщо classinfo не є типом або кортежем типів, виникає виняток
[TypeError](/reference/exceptions/#typeerror).

## Приклади використання

```python
In [1]: numbers = [1, 2, 3]

In [2]: isinstance(numbers, list)
Out[2]: True

In [3]: isinstance(numbers, tuple)
Out[3]: False

In [4]: isinstance(numbers, (list, tuple))
Out[4]: True
```

Використання класів із collections.abc:

```python
In [19]: from collections.abc import Iterable

In [22]: isinstance(numbers, Iterable)
Out[22]: True
```

### Приклади з винятком

Приклад невірного використання isinstance, в classinfo переданий не тип:
```python
In [5]: isinstance(numbers, "test")
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[5], line 1
----> 1 isinstance(numbers, "test")

TypeError: isinstance() arg 2 must be a type, a tuple of types, or a union
```

В цьому випадку перевірка відпрацює через те що перший тип пройшов перевірку:
```python
In [8]: numbers = [1, 2, 3]

In [9]: isinstance(numbers, (list, "test"))
Out[9]: True
```


## Дивись також

#### [type](/reference/functions/type/)
