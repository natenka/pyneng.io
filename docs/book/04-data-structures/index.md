# 4. Типи даних у Python

!!! tip "[Цей розділ в форматі відео](https://pyneng.io/course/topics/04-data-types/)"

У Python є кілька базових типів даних:

* Numbers (числа)
* Strings (рядки)
* Lists (списки)
* Dictionaries (словники)
* Tuples (кортежі)
* Sets (множини)
* Boolean (логічний тип даних)

Ці типи даних можна класифікувати за кількома ознаками:

* змінювані (списки, словники та множини)
* незмінні (числа, рядки та кортежі)
* упорядковані (списки, кортежі, рядки та словники)
* невпорядковані (множини)

``` mermaid
flowchart TD
  A[змінювані] --> B[список];
  A --> C[словник];
  A --> D[множина];
  F[незмінні] --> R[число];
  F --> S[рядок];
  F --> T[кортеж];
```


``` mermaid
flowchart TD
  A[упорядковані] --> B[список];
  A --> T[кортеж];
  A --> S[рядок];
  A --> C[словник];
  F[невпорядковані] --> D[множина];
```
