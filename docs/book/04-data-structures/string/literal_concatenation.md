# Об'єднання літералів рядків 

У Python є дуже зручна функціональність - об'єднання літералів рядків.
Вона дозволяє розбивати рядки на частини при написанні коду і навіть переносити
ці частини на різні рядки коду.  Це потрібно як для розділення довгого тексту
на частини через рекомендації щодо максимальної довжини рядка в Python, так і
для зручності сприйняття.

> Літерал – це вираз, що створює об’єкт. Для рядка це коли ми пишемо якісь
> символи у лапках - створюємо рядок руками.

Приклад об'єднання літералів рядків:

```python
In [1]: s = 'Test' 'String'

In [2]: s
Out[2]: 'TestString'
```


Можна переносити складові рядки на різні рядки, але тільки якщо вони в дужках:

```python
In [5]: s = ('Test'
   ...: 'String')

In [6]: s
Out[6]: 'TestString'
```

Цим дуже зручно користуватися в регулярних виразах:

```python
regex = ('(\S+) +(\S+) +'
         '\w+ +\w+ +'
         '(up|down|administratively down) +'
         '(\w+)')
```

Регулярний вираз можна розбивати на частини, так його простіше зрозуміти. Плюс
можна додавати пояснювальні коментарі у рядках.

```python
regex = ('(\S+) +(\S+) +' # interface and IP
         '\w+ +\w+ +'
         '(up|down|administratively down) +' # Status
         '(\w+)') # Protocol
```

Також цим прийомом зручно користуватися, коли треба написати довге повідомлення:

```python
message = (
    'При виконанні команди "{}" виникла така помилка "{}".\n'
    'Виключити цю команду зі списку? [y/n]'
)

In [8]: message
Out[8]: 'При виконанні команди "{}" виникла така помилка "{}".\nВиключити цю команду зі списку? [y/n]'
```
