# Як створити свій ітерований об'єкт

### Приклад створення з методом `__getitem__`

```python
from ipaddress import ip_network


class Network:
    def __init__(self, network, mask):
        self.network = network
        self.mask = mask
        net = ip_network(f"{self.network}/{self.mask}")
        self.hosts = [str(ip) for ip in net.hosts()]

    def __str__(self):
        return f"{self.network}/{self.mask}"

    def __repr__(self):
        return f"{self.__class__.__name__}('{self.network}', {self.mask})"

    def __len__(self):
        return len(self.hosts) + 2

    def __getitem__(self, index):
        return self.hosts[index]


if __name__ == "__main__":
    net1 = Network("10.1.1.0", 29)
    for ip in net1:
        print(ip)
```

### Приклад створення з методом `__iter__`

```python
from ipaddress import ip_network


class Network:
    def __init__(self, network, mask):
        self.network = network
        self.mask = mask
        net = ip_network(f"{self.network}/{self.mask}")
        self.hosts = [str(ip) for ip in net.hosts()]

    def __str__(self):
        return f"{self.network}/{self.mask}"

    def __repr__(self):
        return f"{self.__class__.__name__}('{self.network}', {self.mask})"

    def __len__(self):
        return len(self.hosts) + 2

    def __getitem__(self, index):
        return self.hosts[index]

    def __iter__(self):
        return iter(self.hosts)


if __name__ == "__main__":
    net1 = Network("10.1.1.0", 29)
    for ip in net1:
        print(ip)
```

