# Змінні

Змінні в Python не вимагають оголошення типу змінної (оскільки Python – мова з
динамічною типізацією) і є посиланнями на область пам'яті. Правила іменування
змінних:

-  ім'я змінної може складатися лише з літер, цифр та знака підкреслення
-  ім'я не може починатися із цифри
-  ім'я не може містити спеціальних символів @, $, %

Приклад створення змінних у Python:

```python
In [1]: a = 3

In [2]: b = 'Hello'

In [3]: c, d = 9, 'Test'

In [4]: print(a,b,c,d)
3 Hello 9 Test
```

Зверніть увагу, що в Python не потрібно вказувати, що a це число, а b це рядок.

## Імена змінних

Імена змінних не повинні перетинатися з назвами операторів та модулів або інших
зарезервованих слів. У Python є рекомендації щодо іменування функцій, класів та
змінних:

-  імена змінних зазвичай пишуться або повністю великими або маленькими літерами (наприклад DB_NAME, db_name)
-  імена функцій задаються маленькими літерами, з підкреслення між словами (наприклад, get_names)
-  імена класів задаються словами з великими літерами без пробілів, це звані CamelCase (наприклад, CiscoSwitch)