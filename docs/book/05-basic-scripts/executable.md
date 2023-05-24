# Виконуваний файл

Для того, щоб файл був виконуваним, і не потрібно було щоразу писати python
перед викликом файлу, потрібно:

* зробити файл виконуваним (для Linux)
* **у першому рядку файлу** має бути рядок ``#!/usr/bin/env python`` або
  ``#!/usr/bin/env python3``, залежно від того, яка версія Python
  використовується за умовчанням

Приклад файлу access_template_exec.py:

```python

#!/usr/bin/env python3

access_template = ['switchport mode access',
                   'switchport access vlan {}',
                   'switchport nonegotiate',
                   'spanning-tree portfast',
                   'spanning-tree bpduguard enable']

print('\n'.join(access_template).format(5))
```

Після цього:

```
chmod +x access_template_exec.py
```

Тепер можна викликати файл у такий спосіб:

```
$ ./access_template_exec.py
```

