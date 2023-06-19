# Методи рядків

## Об'єднання рядків в один

#### [join](/reference/string/methods/join/)

Метод join повертає рядок, який є об'єднанням рядків у послідовності рядків,
переданої як аргумент. Між елементами в об'єднанні рядків проставляється роздільник.

## Поділ рядка на частини

#### [split](/reference/string/methods/split/)

Розділяє рядок на частини за вказаним роздільником. Повертає список рядків.

#### [rsplit](/reference/string/methods/rsplit/)

Розділяє рядок на частини за вказаним роздільником. Повертає список рядків.
Працює як split за замовчуванням, єдина відмінність у поведінці полягає в тому,
що розділ починається праворуч під час використання maxsplit.

#### splitlines

Розділяє рядок на частини за символом нового рядку. Повертає список рядків.

#### partition

Partition the string into three parts using the given separator.

#### rpartition

Partition the string into three parts using the given separator.


## Видалення символів whitespace

#### strip

Return a copy of the string with leading and trailing whitespace removed.

#### rstrip

Return a copy of the string with trailing whitespace removed.

#### lstrip

Return a copy of the string with leading whitespace removed.

## Перевірка початку/кінця рядка

#### startswith

Return True if S starts with the specified prefix, False otherwise.

#### endswith

Return True if S ends with the specified prefix, False otherwise.

## Перетворення регістрів

#### lower

Return a copy of the string converted to lowercase.

#### capitalize

Return a capitalized version of the string.

#### swapcase

Convert uppercase characters to lowercase and lowercase characters to uppercase.

#### title

Return a version of the string where each word is titlecased.

#### upper

Return a copy of the string converted to uppercase.

#### casefold

Return a version of the string suitable for caseless comparisons.


## Вирівнювання тексту

### center

Return a centered string of length width.

#### ljust

Return a left-justified string of length width.

#### rjust

Return a right-justified string of length width.


## Пошук, підрахунок елементів

#### count

S.count(sub[, start[, end]]) -> int

#### find

S.find(sub[, start[, end]]) -> int

#### index

S.index(sub[, start[, end]]) -> int

#### rfind

S.rfind(sub[, start[, end]]) -> int

#### rindex

S.rindex(sub[, start[, end]]) -> int

## Заміна

#### replace

S.replace(old, new)

#### translate

Replace each character in the string using the given translation table.

#### removeprefix

Return a str with the given prefix string removed if present.

#### removesuffix

Return a str with the given suffix string removed if present.

## Інші методи

#### expandtabs

Return a copy where all tab characters are expanded using spaces.

#### zfill

Pad a numeric string with zeros on the left, to fill a field of the given width.

#### format

`S.format(*args, **kwargs) -> str`

#### format_map

S.format_map(mapping) -> str

#### maketrans

Return a translation table usable for str.translate().

#### encode

Encode the string using the codec registered for encoding.


## Перевірка того, що знаходиться у рядку

#### isalnum

Return True if the string is an alpha-numeric string, False otherwise.

#### isalpha

Return True if the string is an alphabetic string, False otherwise.

#### isascii

Return True if all characters in the string are ASCII, False otherwise.

#### isdecimal

Return True if the string is a decimal string, False otherwise.

#### isdigit

Return True if the string is a digit string, False otherwise.

#### isidentifier

Return True if the string is a valid Python identifier, False otherwise.

#### islower

Return True if the string is a lowercase string, False otherwise.

#### isnumeric

Return True if the string is a numeric string, False otherwise.

#### isprintable

Return True if the string is printable, False otherwise.

#### isspace

Return True if the string is a whitespace string, False otherwise.

#### istitle

Return True if the string is a title-cased string, False otherwise.

#### isupper

Return True if the string is an uppercase string, False otherwise.


