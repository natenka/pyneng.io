# Підготовка редактора

## Відступи

У python прийнято використовувати як відступ 4 пробіли. Треба перевірити, що
ваш редактор по натисканню Tab ставитиме 4 пробіли:

* Гуглим "notepad++ indent size" (замінюємо notepad++ на свій редактор).
  Шукаємо як правильно налаштовувати відступ у вашому редакторі
* Налаштовуємо відступ на 4 пробіли


## Віртуальні оточення

Деякі редактори/IDE створюють віртуальне оточення. Деякі не створюють, але їм
треба якось підказати, що треба використовувати віртуальне оточення, яке ви
створили.

Деякі редактори/IDE дуже явно створюють віртуальні оточення, тобто при старті
проекту запитують вас, який Python використовувати. У цьому випадку, ви можете
вибрати відразу створювати новий вірт. оточення або використовувати існуюче.


## Редактор створює віртуальне оточення

### Як визначити, що редактор створив своє віртуальне оточення

Потрібно відкрити редактор і в будь-який новий файл вставити такий код

```python
import sys
from pprint import pprint


pprint(sys.path)
```

Запускаємо код і дивимося на каталоги, якщо там присутнє слово venv, швидше за
все редактор створив віртуальне оточення:

```
 'C:\\Users\\nata\\PycharmProjects\\pythonProject\\venv',
 'C:\\Users\\nata\\PycharmProjects\\pythonProject\\venv\\lib\\site-packages']
```

### Робота в терміналі

Якщо вам треба/зручніше працювати в терміналі окремому від IDE/редактора, треба
знати, в яке віртуальне оточення перейти, щоб робота була в тому ж оточенні, в
якому працює редактор.

Вище вже перевірили шляхи. Якщо там віртуальне оточення, яке ви створили, ви
знаєте, як у нього перейти. Якщо це віртуальне оточення редактора, можна
перейти так:


Windows:

```
C:\Users\nata\PycharmProjects\pythonProject\venv\Scripts\activate.bat',
```

Linux/Mac OS (шлях залежить від того, що показав редактор у sys.path)

```
source ~/project/venv/bin/activate
```


## Ви створили віртуальне оточення і треба, щоб редактор його використовував

* Гуглим "notepad++ python venv" (замінюємо notepad++ на свій редактор)
* Шукаємо як правильно налаштовувати використання вашого віртуального оточення в редакторі
