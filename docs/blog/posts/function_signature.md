---
draft: true 
date: 2023-07-01
categories:
  - python
tags:
  - basics
---

# Підказки для функцій та методів

Розбираємося з тим, що показує у підказках ipython та редактори/IDE.

Залежно від того, як було створено метод або функцію, ipython/editor/IDE може
відображати різні типи підказок.  Крім того, підказки можуть відрізнятися між
ipython і редактором.

```python
def sum_numbers(num1, num2):
    """
    Функція обчислює суму двох чисел
    """
    return num1 + num2


In [3]: sum_numbers(100, 42)
Out[3]: 142

In [4]: sum_numbers?
Signature: sum_numbers(num1, num2)
Docstring: Функція обчислює суму двох чисел
File:      ~/repos/.../<ipython-input-2>
Type:      function
```

<!-- more -->

simple function
```python
In [16]: round?
Signature: round(number, ndigits=None)
Docstring:
Round a number to a given precision in decimal digits.

The return value is an integer if ndigits is omitted or None.  Otherwise
the return value has the same type as the number.  ndigits may be negative.
Type:      builtin_function_or_method
```

simple methods
```python
In [6]: s.lower?
Signature: s.lower()
Docstring: Return a copy of the string converted to lowercase.
Type:      builtin_function_or_method

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

## positional/keyword only


functions
```python
In [17]: len?
Signature: len(obj, /)
Docstring: Return the number of items in a container.
Type:      builtin_function_or_method

In [18]: sorted?
Signature: sorted(iterable, /, *, key=None, reverse=False)
Docstring:
Return a new list containing all items from the iterable in ascending order.

A custom key function can be supplied to customize the sort order, and the
reverse flag can be set to request the result in descending order.
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

Methods
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

list
```python
In [4]: vlans = [1, 2, 3]

In [5]: vlans.insert?
Signature: vlans.insert(index, object, /)
Docstring: Insert object before index.
Type:      builtin_function_or_method

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



dict
```python
In [3]: d1 = {"key": "value"}

In [5]: d1.get?
Signature: d1.get(key, default=None, /)
Docstring: Return the value for key if key is in the dictionary, else default.
Type:      builtin_function_or_method

```

## var length pos/keyword args

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


## no signature, docstring only

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


bad docstring

```python
In [5]: s1.difference?
Docstring:
Return the difference of two or more sets as a new set.

(i.e. all elements that are in this set but not the others.)
Type:      builtin_function_or_method

In [6]: s1.intersection?
Docstring:
Return the intersection of two sets as a new set.

(i.e. all elements that are in both sets.)
Type:      builtin_function_or_method

```

## Type annotations

### simple

```python
In [2]: from netutils.ip import cidr_to_netmask

In [3]: cidr_to_netmask?
Signature: cidr_to_netmask(cidr: int) -> str
Docstring:
Creates a decimal format of a CIDR value.

**IPv4** only.  For IPv6, please use `cidr_to_netmaskv6`.

Args:
    cidr: A CIDR value.

Returns:
    Decimal format representation of CIDR value.

Examples:
    >>> from netutils.ip import cidr_to_netmask
    >>> cidr_to_netmask(24)
    '255.255.255.0'
    >>> cidr_to_netmask(17)
    '255.255.128.0'
File:      ~/venv/pyneng311/lib/python3.11/site-packages/netutils/ip.py
Type:      function
```

```python
In [1]: from netutils.ip import cidr_to_netmask

In [2]: cidr_to_netmask(24)
Out[2]: '255.255.255.0'

In [3]: cidr_to_netmask(22)
Out[3]: '255.255.252.0'

In [5]: cidr_to_netmask(32)
Out[5]: '255.255.255.255'

```

### complex

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
