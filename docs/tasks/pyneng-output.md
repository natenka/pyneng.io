---
title: "Вывод pyneng"
permalink: /docs/pyneng-output/
excerpt: "Вывод pyneng"
---

## Warning

В конце вывода теста часто написано "1 warning". Это можно игнорировать, предупреждения в основном связаны с работой
каких-то модулей и скрыты чтобы не отвлекать от заданий.


## Тесты прошли успешно

![passed](https://pyneng.io/assets/images/ptest_output_5.png)

## Тесты не прошли

Когда какие-то тесты не прошли, в выводе показываются отличия между тем как должен выглядеть вывод и какой
вывод был получен.
Проверка правильности вывода в тесте проверяется с помощью выражения `assert ...`. Два самых распространенных варианта (98% тестов):

```python
assert correct_return_value == return_value
assert correct_output in return_output
```

### assert x == y

В большинстве заданий проверяется равенство двух значений:

```python
assert correct_return_value == return_value
```

В этом случае, тест выводит Left как правильный ответ зеленого цвета, а Right как вывод задания красного цвета.
В этом задании надо было вывести строку с GigabitEthernet, а была выведена FastEthernet:

![passed](https://pyneng.io/assets/images/pyneng_output_1.png)

Другие примеры вывода, с разными отличиями, но тут во всех случаях left (зеленое) это правильный результат,
а rigth (красное) то что было получено при запуске задания:

Тут отличие в том, что надо вывести MAC-адрес с точками, а выведен с двоеточиями:

![passed](https://pyneng.io/assets/images/pyneng_output_3.png)

В задании надо получить список с вланами, где каждый влан отдельный элемент списка, а получен список с одной строкой, в которой написаны все вланы:

![passed](https://pyneng.io/assets/images/pyneng_output_2.png)

Отличие с правильным результатом в том, что в правильном выводе не должно быть квадратных скобок `[]`:

![passed](https://pyneng.io/assets/images/pyneng_output_4.png)


### assert x in y

Выражение `assert x in y` проверяет находится ли нужный вывод в полученном результате задания.
Например, в тесте это может выглядеть так:

```python
assert correct_stdout in out.strip()
```

В этом случае Left (зеленый) это правильный вывод, right вывод задания:

![passed](https://pyneng.io/assets/images/ptest_output_1.png)


### Неправильный тип данных

Кроме отличий в результате, может также отличаться тип данных. Например, по заданию надо получить список,
а получена строка. В этом случае проще всего читать сообщение ошибки (выделено):

![passed](https://pyneng.io/assets/images/pyneng_output_5.png)

В тесте проверка типа данных выглядит так

```python
assert (
    type(task_4_3.result) == list
), f"По заданию в переменной result должен быть список, а в ней {type(task_4_3.result).__name__}"
```

И для проверки типов left это то что получено в задании, а right то что должно быть. При этом,
так как в этом случае генерируется понятное сообщение, проще читать его.