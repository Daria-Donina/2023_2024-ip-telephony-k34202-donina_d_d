University: [ITMO University](https://itmo.ru/ru/) <br/>
Faculty: [FICT](https://fict.itmo.ru) <br/>
Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)<br/>
Year: 2023/2024<br/>
Group: K34202<br/>
Author: Donina Daria Dmitrievna<br/>
Lab: Lab2<br/>
Date of create: 17.03.2024<br/>
Date of finished: 19.03.2024<br/>

# Цель работы
Изучить построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.

# Ход работы
### Часть 1

Создана схема следующего вида:

<img width="622" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/02ee8fec-5333-4320-b512-eb83893f69d6">

Имя маршрутизатора изменено:
```
hostname CMERouter
```
Отключен синтаксис ввода слов от DNS серверов:
```
no ip domain-lookup
```
Задан пароль для защиты маршрутизатора как в удаленном режиме, так и в режиме консоли:
```
line console 0
password 1234
login
line vty 0 4
password 1234
login
```

На маршрутизаторе Cisco 2811 (CMERouter) настроен интерфейс fa0/0:

```
int fa0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
```

Настроен DHCP сервер для передачи голоса и данных:

```
ip dhcp pool voip
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
option 150 ip 192.168.1.1
```

Настроены услуги телефонии:

```
telephony-service 
max-dn 10
max-ephones 10
ip source-address 192.168.1.1 port 3100
auto assign 1 to 19

```

Настроен коммутатор для работы с IP-телефонами:

```
int range fa 0/1 - fa 0/3
switchport mode access
switchport voice vlan 1
int fa0/24
switchport mode access
switchport voice vlan 1
```

Включены физически IP-телефоны, настроены их номера:

```
ephone-dn 1
number 001
ephone-dn 2
number 002
ephone-dn 3
number 003
```

Проверены звонки. 
C 003 на 001:

<img width="1275" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/54fd54aa-a134-4d1a-91c9-95126b6ce014">

При активном звонке и попытке позвонить с 002 на 001, выводится сообщение, что линия занята:

<img width="681" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/732fba24-aa31-4e35-b0cb-6ba1ff3bc649">

Звонок с 002 на 003:

<img width="1279" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/71121632-ae79-448b-9962-04c281fa72e9">

### Часть 2

Создать VLAN порты на коммутаторе для взаимо- действия коммутатора с маршрутизатором и подключить IP телефоны.
Задайте маршрут по умолчанию командой ip default-gateway.
Настройте порт как канал типа trunk.
Настроить DHCP сервера для передачи голоса и данных на маршрутизаторе Cisco 2811.
Настроить услуги телефонии Cisco CallManager Express на маршрутизаторе.
Настроить IP-телефоны и соединить с коммутатором.
Подключить конечные узлы устройств.
Проверить звонки между телефонами и проверить остальные сервисы (перевод звонков, конференц-связь, перехват звонка).

# Вывод

В ходе данной лабораторной работы было изучено построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.
