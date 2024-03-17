University: [ITMO University](https://itmo.ru/ru/) <br/>
Faculty: [FICT](https://fict.itmo.ru) <br/>
Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)<br/>
Year: 2023/2024<br/>
Group: K34202<br/>
Author: Donina Daria Dmitrievna<br/>
Lab: Lab1<br/>
Date of create: 17.03.2024<br/>
Date of finished: 19.03.2024<br/>

# Цель работы
Изучить рабочую среду Cisco Packet Tracer, ознакомиться с интерфейсами основных устройств, 
типами кабелей, научиться собирать топологию. Изучить построение сети IP-телефонии с помощью маршрутизатора, 
коммутатора и IP телефонов Cisco 7960 в среде Packet tracer.

# Ход работы
### Часть 1
Создадим и настроим сеть из хостов и коммутаторов. Схема получившейся сети:

<img width="696" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/7777c71a-8f27-4cee-b3e8-fd779b13b893">

Настроим хостам статические IP-адреса в сети 192.168.10.0/24:

<img width="691" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/c50a6d33-c3ef-4187-8d84-0e3cd6640ec4">

Коммутаторам настроим IP-адреса из той же сети:

<img width="475" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/7b8987bf-98e6-4701-9302-6f1403331b23">

Сеть настроена. Проверим связность узлов. Пинг с PC0 на PC6:

<img width="685" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/3804ecdf-8901-4e01-af9b-746a6762f2aa">

### Часть 2

Собрана новая схема с роутером, коммутатором и двумя IP-телефонами.
Схема сети:

<img width="516" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/3041c2a3-3a29-4a6f-bd85-6260666db361">


Изменено имя роутера:

```
hostname CMERouter
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
```

Включены физически IP-телефоны, настроены их номера:

```
ephone-dn 1
number 001
ephone-dn 2
number 002
```

Проверен звонок. Удалось успешно дозвониться с одного телефона на другой:

<img width="1275" alt="image" src="https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/c4fb01f2-4aed-4c51-9a49-40837c065e88">

# Вывод

В ходе данной лабораторной работы была изучена рабочая среда Cisco Packet Tracer, удалось ознакомиться с интерфейсами основных устройств, 
типами кабелей, научиться собирать топологию. Было изучено построение сети IP-телефонии с помощью маршрутизатора, 
коммутатора и IP телефонов Cisco 7960 в среде Packet tracer.
