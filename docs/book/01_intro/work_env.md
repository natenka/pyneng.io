# Підготовка робочого оточення

Для виконання завдань книги можна використати кілька варіантів:

* налаштувати свою ОС
* підготувати віртуалку
* використовувати якийсь хмарний сервіс


## Підготовка віртуальної машини/хоста самостійно

Список модулів, які потрібно встановити:

```
pip install pytest pytest-clarity pyyaml tabulate jinja2 textfsm pexpect netmiko graphviz
```

Також необхідно встановити graphviz прийнятим способом в ОС (приклад для debian):

```
apt-get install graphviz
```

### Хмарні сервіси

Ще один варіант – використовувати один із наступних сервісів:

* [repl.it](https://repl.it/) – цей сервіс надає онлайн інтерпретатор Python, а також графічний редактор. [Приклад використання](https://repl.it/KSIp/3/)
* [PythonAnywhere](https://www.pythonanywhere.com/) - виділяє окрему віртуалку,
  але у безкоштовному варіанті ви можете працювати тільки з командного рядка,
  тобто немає графічного текстового редактора


### Мережеве обладнання

До 18 розділу книги потрібно підготувати віртуальне або реальне мережеве обладнання.

Всі приклади та завдання, в яких зустрічається мережеве обладнання,
використовують однакову кількість пристроїв: три маршрутизатори з такими
базовими налаштуваннями:

* користувач: cisco
* пароль: cisco
* пароль на режим enable: cisco
* SSH версії 2 (обов'язково саме версія 2), Telnet
* IP-адреси маршрутизаторів: 192.168.139.1, 192.168.139.2, 192.168.139.3
* IP-адреси повинні бути доступні з віртуалки, на якій ви виконуєте завдання
  і можуть бути призначені на фізичних/логічних/loopback інтерфейсах

Топологія може бути довільною. Приклад топології:


![gns3_network](https://pyneng.io/assets/images/gns3_network.png)


Базова конфігурація:

```
hostname R1
!
no ip domain lookup
ip domain name pyneng
!
crypto key generate rsa modulus 1024
ip ssh version 2
!
username cisco password cisco
enable secret cisco
!
line vty 0 4
 logging synchronous
 login local
 transport input telnet ssh
```


На якомусь інтерфейсі треба налаштувати IP-адресу

```
interface ...
 ip address 192.168.139.1 255.255.255.0
```


Аліаси (за бажанням)

```
!
alias configure sh do sh
alias exec ospf sh run | s ^router ospf
alias exec bri show ip int bri | exc unass
alias exec id show int desc
alias exec top sh proc cpu sorted | excl 0.00%__0.00%__0.00%
alias exec c conf t
alias exec diff sh archive config differences nvram:startup-config system:running-config
alias exec desc sh int desc | ex down
alias exec bgp sh run | s ^router bgp
```


За бажання можна налаштувати [EEM applet](http://xgu.ru/wiki/Embedded_Event_Manager)
для відображення команд, які вводить користувач:

```
!
event manager applet COMM_ACC
 event cli pattern ".*" sync no skip no occurs 1
 action 1 syslog msg "User $_cli_username entered $_cli_msg on device $_cli_host "
!
```

