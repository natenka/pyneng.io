# Ітерований об'єкт

Ітерований об'єкт (iterable) - це об'єкт, який здатний повертати елементи по
одному. Крім того, це об'єкт, з якого можна отримати ітератор.

Приклади ітерованих об'єктів:

* список, рядок, кортеж
* словники
* файли

Будь-який об'єкт елементи який ви можете перебирати в циклі for - ітерований об'єкт.

Для Python це будь-який об'єкт, який має метод `__iter__` або метод `__getitem__`.


## [Як створити новий ітерований об'єкт за допомогою класів](/reference/protocols/iterable_custom/)
