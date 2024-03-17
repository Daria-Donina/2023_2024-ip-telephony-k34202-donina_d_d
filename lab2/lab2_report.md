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

Схема сети:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/eaec5c20-d084-4b58-9765-7d8f2479ca37)

На коммутаторе созданы VLAN порты:
```
vlan 10
name data
vlan 20
name voice
vlan 30
name router
```
Интерфейсы, ведущие к телефонам переведены в режим access и подключены к VLANам для телефонов и компьютеров:

```
interface range fa0/2-4
switchport mode access
switchport access vlan 10
switchport voice vlan 20
```

Интерфейс, ведущий к роутеру был переведен в режим trunk:
```
int fa 0/1
switchport trunk native vlan 30
switchport trunk allowed vlan 10,20,30
switchport trunk encapsulation dot1q 
switchport mode trunk 
```

Задан маршрут по умолчанию:
```
ip default-gateway 192.168.30.1
```
Настроен DHCP сервер для передачи голоса и данных на маршрутизаторе:
```
ip dhcp pool data
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1

ip dhcp pool voice
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
option 150 ip 192.168.20.1
```
На маршрутизаторе настроен vlan (сабинтерфейсы):
```
int fa0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
no shutdown

int fa0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
no shutdown

int fa 0/0
no shutdown
```
Настроены услуги телефонии на маршрутизаторе:
```
telephony-service 
max-dn 3
max-ephones 3
ip source-address 192.168.20.1 port 3100
auto assign 1 to 3
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
На компьютерах получен IP-адрес с помощью DHCP:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/b808c7ee-63be-492b-9933-9344f610373c)

На телефонах так же:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/f6709d60-5248-4da1-9ce0-3eda23da4e0b)

Проверим пинг другого ПК и IP-телефона:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/bdb0b2cb-e490-414e-8118-42e9fd8be629)

Проверим звонок:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/ad009866-e8a3-45e8-829e-46a544684a78)

# Вывод

В ходе данной лабораторной работы было изучено построение сети IP-телефонии с помощью маршрутизатора Cisco 2811, коммутатора Cisco catalyst 3560 и IP телефонов Cisco 7960.
