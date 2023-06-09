# open

Функція open відкриває файл і повертає відповідний файловий об'єкт. Якщо файл неможливо
відкрити, виникає виняток OSError.

## Синтаксис

```python
open(
    file,
    mode='r',
    buffering=-1,
    encoding=None,
    errors=None,
    newline=None,
    closefd=True,
    opener=None,
)
```

### Параметри

#### file

#### mode

| Символ | Значення |
|--------|-----------|
| `"r"` | відкритий для читання (за замовчуванням) |
| `"w"` | відкрити для запису, спочатку видаливши вміст файлу |
| `"x"` | відкрити для ексклюзивного створення, якщо файл уже існує, виникає виняток FileExistsError |
| `"а"` | відкрити для запису, додаючи в кінець файлу, якщо він існує |
| `"b"` | двійковий режим |
| `"t"` | текстовий режим (за замовчуванням) |
| `"+"` | відкритий для оновлення (читання та запис) |

Python розрізняє двійковий і текстовий ввід-вивід.  Файли, відкриті в
двійковому режимі (із буквою `b` в аргументі mode), повертають вміст як об'єкти
байти (bytes) без будь-якого декодування. У текстовому режимі (за
замовчуванням, або коли `t` включено в аргумент режиму), вміст файлу
повертається як рядок, відповідно байти були спочатку декодовані з
використанням кодування.


```
| Режим відкриття            | r | r+ | w | w+ | a | a+ | x | x+ |
|----------------------------|---|----|---|----|---|----|---|----|
| читання                    | + | +  |   | +  |   | +  |   | +  |
| запис                      |   | +  | + | +  | + | +  | + | +  |
| створення нового файлу     |   |    | + | +  | + | +  | + | +  |
| відкриття існуючого файлу  |   |    | + | +  | + | +  |   |    |
| вміст файлу видаляється    |   |    | + | +  |   |    |   |    |
| позиція на початку         | + | +  | + | +  |   |    | + | +  |
| позиція в кінці            |   |    |   |    | + | +  |   |    |
| запис після seek           |   | +  | + | +  |   |    | + | +  |
```

??? info "Пояснення до таблиці"

    [Джерело таблиці](https://stackoverflow.com/a/30931305)

    * читання - дозволено читання з файлу
    * запис - запис у файл дозволений
    * створення - файл створюється, якщо він ще не існує
    * вміст файлу видаляється - під час відкриття файл стає порожнім (увесь вміст файлу стирається)
    * позиція на початку - після відкриття файлу початкова позиція встановлюється на початок файлу
    * позиція в кінці - після відкриття файлу початкова позиція встановлюється в кінець файлу

#### encoding

У текстовому режимі, якщо кодування не вказано, кодування, що використовується,
залежить від платформи: викликається `locale.getencoding()`, щоб отримати поточне
кодування.

#### errors

errors — необов'язковий рядок, який визначає, як мають оброблятися помилки
кодування та декодування у текстовому режимі.

Доступні різноманітні [стандартні обробники помилок](https://docs.python.org/3/library/codecs.html#error-handlers).
Стандартні назви включають:

* `'strict'` викликає виняток ValueError, якщо є помилка кодування. Стандартне значення `None` має той самий ефект.
* `'ignore'` ігнорує помилки. Ігнорування помилок кодування може призвести до втрати даних!
* `'replace'` вставляє маркер заміни (наприклад, `?`), там де є неправильні дані.
* `'surrogateescape'` детальніше в документації [open](https://docs.python.org/3/library/functions.html#open).
* `'backslashreplace'` замінює некоректні дані escape-послідовностями Python зі зворотною косою рискою.

Підтримується лише під час запису у файл. Символи, які не підтримуються кодуванням:

* `'xmlcharrefreplace'` замінюються відповідним посиланням на символ XML `&#nnn`
* `'namereplace'`  замінюються escape-послідовностями `\N{...}`

#### newline

#### buffering

У документації [open](https://docs.python.org/3/library/functions.html#open).

#### closefd

У документації [open](https://docs.python.org/3/library/functions.html#open).

#### opener

У документації [open](https://docs.python.org/3/library/functions.html#open).

### Значення, що повертається


### Виняток

Якщо ... виникає виняток ...

[Ієрархія винятків](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)

```
OSError
   ├── BlockingIOError
   ├── ChildProcessError
   ├── ConnectionError
   │    ├── BrokenPipeError
   │    ├── ConnectionAbortedError
   │    ├── ConnectionRefusedError
   │    └── ConnectionResetError
   ├── FileExistsError
   ├── FileNotFoundError
   ├── InterruptedError
   ├── IsADirectoryError
   ├── NotADirectoryError
   ├── PermissionError
   ├── ProcessLookupError
   └── TimeoutError
```

## Приклади використання



## Дивись також

* [open](https://docs.python.org/3/library/functions.html#open)
* [file object](https://docs.python.org/3/glossary.html#term-file-object)
* [Reading and Writing Files](https://docs.python.org/3/tutorial/inputoutput.html#tut-files)

