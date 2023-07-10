---
# draft: true 
date: 2023-07-10
categories:
  - python
tags:
  - basics
---

# Як зрозуміти підказки для функцій та методів

!!! warning

	Цей допис йде як доповнення до [відео про підказки для функцій та методів](https://www.youtube.com/watch?v=R-4cS-vMEWg).
    Тут немає детальних пояснень, тільки вивід підказок.

Розбираємося з тим, що показує у підказках ipython та редактори/IDE.

Залежно від того, як було створено метод або функцію, ipython/editor/IDE може
відображати різні типи підказок.  Крім того, підказки можуть відрізнятися між
ipython і редактором.

!!! note

    Цей пост призначений для тих, хто ще не навчився створювати власні функції.
    Після вивчення теми "09: Функції" більшість або всі описані тут варіанти будуть зрозумілі.


Приклад створення функції та відображення підказки для неї:

```python
def sum_numbers(num1, num2):
    """
    Функція обчислює суму двох чисел
    """
    return num1 + num2


In [3]: sum_numbers(100, 42)
Out[3]: 142

In [4]: sum_numbers?
Signature: sum_numbers(num1, num2) # (1)
Docstring: Функція обчислює суму двох чисел # (2)
File:      ~/repos/.../<ipython-input-2> # (3)
Type:      function # (4)
```

1. Опис функції, як правило, дорівнює рядку, за допомогою якого була створена функція.
2. Рядок документації функції. Опис роботи функції, як правило, створений людиною.
3. Де була створена функція (в якому файлі).
4. Тип об'єкту: function для функцій, method для методів, builtin_function_or_method для деяких вбудованих функцій

<!-- more -->

Приклад підказки для різних функцій, для порівняння рядків Signature/File/Type
(docstring функцій скорочено до одного рядка для спрощення порівняння):

=== "ipaddress.ip_address"

     Функція із модуля стандартної бібліотеки:

    ```python
    In [2]: ip_address? # (1)
    Signature: ip_address(address)
    Docstring: Take an IP string/int and return an object of the correct type.
    File:      /usr/local/lib/python3.11/ipaddress.py
    Type:      function
    ```

    1. Імпорт `from ipaddress import ip_address`

=== "len"

    Вбудована функція:

    ```python
    In [3]: len?
    Signature: len(obj, /)
    Docstring: Return the number of items in a container.
    Type:      builtin_function_or_method
    ```

=== "netutils.ip.cidr_to_netmask"

    Функція із стороннього модуля netutils:

    ```python
    In [4]: cidr_to_netmask? # (1)
    Signature: cidr_to_netmask(cidr: int) -> str
    Docstring: Creates a decimal format of a CIDR value.
    File:      ~/venv/pyneng311/lib/python3.11/site-packages/netutils/ip.py
    Type:      function
    ```

    1. Інсталяція `pip install netutils`, імпорт функції `from netutils.ip import cidr_to_netmask`

## Термінологія

![terms](https://pyneng.io/assets/images/09_function_basics_signature.png)

Типи аргументів функції:

![args](https://pyneng.io/assets/images/09_function_args_signature.png)


## Базові підказки для функцій та методів

### Функція round

У функції round є один обов'язковий параметр number, та один необов'язковий параметр ndigits.
Параметр ndigits необов’язковий, оскільки він має значення за замовчуванням.

=== "Підказка"

	```python
	In [16]: round?
	Signature: round(number, ndigits=None)
	Docstring:
	Round a number to a given precision in decimal digits.

	The return value is an integer if ndigits is omitted or None.  Otherwise
	the return value has the same type as the number.  ndigits may be negative.
	Type:      builtin_function_or_method
	```

=== "Приклад роботи"

	```python
	In [17]: 10/3
	Out[17]: 3.3333333333333335

	In [18]: round(10/3, ndigits=3)
	Out[18]: 3.333

	In [20]: round(3.7)
	Out[20]: 4
	```

### Метод str.lower

Найпростіший варіант опису - метод без параметрів:

```python
In [6]: s.lower?
Signature: s.lower()
Docstring: Return a copy of the string converted to lowercase.
Type:      builtin_function_or_method
```


### Метод str.split

!!! abstract "[Детальніше про метод split в довіднику](/reference/string/methods/split/)"

У методу split обидва параметри необов'язкові, оскільки вони мають значення за
замовчуванням.


=== "Підказка"

	```python
	In [7]: s.split?
	Signature: s.split(sep=None, maxsplit=-1)
	Docstring:
	Return a list of the substrings in the string, using sep as the separator string.

	  sep
		The separator used to split the string.

		When set to None (the default value), will split on any whitespace
		character (including \\n \\r \\t \\f and spaces) and will discard
		empty strings from the result.
	  maxsplit
		Maximum number of splits (starting from the left).
		-1 (the default value) means no limit.

	Note, str.split() is mainly useful for data that has been intentionally
	delimited.  With natural text that includes punctuation, consider using
	the regular expression module.
	Type:      builtin_function_or_method
	```

=== "Приклад роботи"

	```python
	In [2]: line = "FastEthernet0/0       15.0.15.1    YES manual up         up"

	In [3]: line.split()
	Out[3]: ['FastEthernet0/0', '15.0.15.1', 'YES', 'manual', 'up', 'up']

	In [4]: line.split(maxsplit=2)
	Out[4]: ['FastEthernet0/0', '15.0.15.1', 'YES manual up         up']

	In [5]: ip = "10.1.1.1"

	In [6]: ip.split(".")
	Out[6]: ['10', '1', '1', '1']

	In [7]: ip.split(".", 2)
	Out[7]: ['10', '1', '1.1']

	In [9]: ip.split(sep=".", maxsplit=1)
	Out[9]: ['10', '1.1.1']
	```

## Використання `/` та `*` - лише позиційні або іменовані аргументи

### `/` - лише позиційні

Аргументи, вказані перед `/`, можна передавати лише як позиційні під час виклику функції.

Приклади функцій, у яких аргументи можна передавати лише як позиційні:

```python
In [1]: len?
Signature: len(obj, /)
Docstring: Return the number of items in a container.
Type:      builtin_function_or_method

In [4]: input?
Signature: input(prompt=None, /)
Docstring:
Read a string from standard input.  The trailing newline is stripped.

The prompt string, if given, is printed to standard output without a
trailing newline before reading input.

If the user hits EOF (*nix: Ctrl-D, Windows: Ctrl-Z+Return), raise EOFError.
On *nix systems, readline is used if available.
Type:      builtin_function_or_method
```

#### Метод str.replace

```python
In [2]: s = "test"

In [3]: s.replace?
Signature: s.replace(old, new, count=-1, /)
Docstring:
Return a copy with all occurrences of substring old replaced by new.

  count
    Maximum number of occurrences to replace.
    -1 (the default value) means replace all occurrences.

If the optional argument count is given, only the first count occurrences are
replaced.
Type:      builtin_function_or_method
```

#### Метод list.insert

```python
In [4]: vlans = [1, 2, 3]

In [5]: vlans.insert?
Signature: vlans.insert(index, object, /)
Docstring: Insert object before index.
Type:      builtin_function_or_method
```


#### Метод dict.get

```python
In [3]: d1 = {"key": "value"}

In [5]: d1.get?
Signature: d1.get(key, default=None, /)
Docstring: Return the value for key if key is in the dictionary, else default.
Type:      builtin_function_or_method
```


### `*` - лише іменовані

Аргументи, вказані після `*`, можна передавати лише як іменовані (ключові) під час виклику функції.

#### Метод list.sort

```python
In [6]: vlans.sort?
Signature: vlans.sort(*, key=None, reverse=False)
Docstring:
Sort the list in ascending order and return None.

The sort is in-place (i.e. the list itself is modified) and stable (i.e. the
order of two equal elements is maintained).

If a key function is given, apply it once to each list item and sort them,
ascending or descending, according to their function values.

The reverse flag can be set to sort in descending order.
Type:      builtin_function_or_method
```
### Використання `/` та `*` одночасно

```python
In [8]: sorted?
Signature: sorted(iterable, /, *, key=None, reverse=False)
Docstring:
Return a new list containing all items from the iterable in ascending order.

A custom key function can be supplied to customize the sort order, and the
reverse flag can be set to request the result in descending order.
Type:      builtin_function_or_method
```

## Використання `*args` - довільна кількість позиційних аргументів

Функція print:

```python
In [19]: print?
Signature: print(*args, sep=' ', end='\n', file=None, flush=False)
Docstring:
Prints the values to a stream, or to sys.stdout by default.

sep
  string inserted between values, default a space.
end
  string appended after the last value, default a newline.
file
  a file-like object (stream); defaults to the current sys.stdout.
flush
  whether to forcibly flush the stream.
Type:      builtin_function_or_method
```


## Для деяких вбудованих методів, не відображається рядок signature в ipython

```python
In [4]: s.find?
Docstring:
S.find(sub[, start[, end]]) -> int

Return the lowest index in S where substring sub is found,
such that sub is contained within S[start:end].  Optional
arguments start and end are interpreted as in slice notation.

Return -1 on failure.
Type:      builtin_function_or_method

In [5]: s.count?
Docstring:
S.count(sub[, start[, end]]) -> int

Return the number of non-overlapping occurrences of substring sub in
string S[start:end].  Optional arguments start and end are
interpreted as in slice notation.
Type:      builtin_function_or_method
```


## Анотація типів

Функція із стороннього модуля netutils (1):
{ .annotate }

1. Інсталяція `pip install netutils`.

=== "netutils"

    ```python
	In [2]: from netutils.ip import cidr_to_netmask

    In [4]: cidr_to_netmask? # (1)
    Signature: cidr_to_netmask(cidr: int) -> str
    Docstring: Creates a decimal format of a CIDR value.
    File:      ~/venv/pyneng311/lib/python3.11/site-packages/netutils/ip.py
    Type:      function
    ```

=== "Приклад роботи"

	```python
	In [1]: from netutils.ip import cidr_to_netmask

	In [2]: cidr_to_netmask(24)
	Out[2]: '255.255.255.0'

	In [3]: cidr_to_netmask(22)
	Out[3]: '255.255.252.0'

	In [5]: cidr_to_netmask(32)
	Out[5]: '255.255.255.255'
	```

### rich.inspect

```python
In [5]: inspect?
Signature:
inspect(
    obj: Any,
    *,
    console: Optional[ForwardRef('Console')] = None,
    title: Optional[str] = None,
    help: bool = False,
    methods: bool = False,
    docs: bool = True,
    private: bool = False,
    dunder: bool = False,
    sort: bool = True,
    all: bool = False,
    value: bool = True,
) -> None
Docstring:
Inspect any Python object.

* inspect(<OBJECT>) to see summarized info.
* inspect(<OBJECT>, methods=True) to see methods.
* inspect(<OBJECT>, help=True) to see full (non-abbreviated) help.
* inspect(<OBJECT>, private=True) to see private attributes (single underscore).
* inspect(<OBJECT>, dunder=True) to see attributes beginning with double underscore.
* inspect(<OBJECT>, all=True) to see all attributes.

Args:
    obj (Any): An object to inspect.
    title (str, optional): Title to display over inspect result, or None use type. Defaults to None.
    help (bool, optional): Show full help text rather than just first paragraph. Defaults to False.
    methods (bool, optional): Enable inspection of callables. Defaults to False.
    docs (bool, optional): Also render doc strings. Defaults to True.
    private (bool, optional): Show private attributes (beginning with underscore). Defaults to False.
    dunder (bool, optional): Show attributes starting with double underscore. Defaults to False.
    sort (bool, optional): Sort attributes alphabetically. Defaults to True.
    all (bool, optional): Show all attributes. Defaults to False.
    value (bool, optional): Pretty print value. Defaults to True.
File:      ~/venv/pyneng311/lib/python3.11/site-packages/rich/__init__.py
Type:      function
```

