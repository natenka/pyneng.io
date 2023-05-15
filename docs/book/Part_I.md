# Основи Python

Перша частина книги присвячена основам Python. У ній розглядаються:

* типи даних Python
* як створювати базові скрипти
* контроль перебігу програми
* робота із файлами

```python
import re
from pprint import pprint


def parse_cdp(filename):
    regex = (r'Device ID: (?P<device>\S+)'
             r'|IP address: (?P<ip>\S+)'
             r'|Platform: (?P<platform>\S+ \S+),'
             r'|Cisco IOS Software, (?P<ios>.+), RELEASE')

    result = {}

    with open(filename) as f:
        match_iter = re.finditer(regex, f.read())
        for match in match_iter:
            if match.lastgroup == 'device':
                device = match.group(match.lastgroup)
                result[device] = {}
            elif device:
                result[device][match.lastgroup] = match.group(match.lastgroup)

    return result

pprint(parse_cdp('sh_cdp_neighbors_sw1.txt'))
```
