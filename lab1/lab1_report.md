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

Собрать схему соединения, указанную на рисунке
Изменить имя маршрутизатора на CMERouter.
Настроить интерфейс fa0/0 на маршрутизаторе Cisco 2811 (CMERouter).
Настроить DHCP сервера для передачи голоса и данных на маршрутизаторе - Cisco 2811.
Настроить услуги телефонии Cisco CallManager Express на маршрутизаторе 2811.
Настроить маршрутизацию сети.
Создать VLAN порты на коммутаторе для взаимодействия коммутатора с маршрутизатором и подключить IP телефоны.
Настроить IP-телефоны, присвоить им номера и соединить с коммутатором.
Проверить звонки между телефонами и проверить остальные сервисы (перевод звонков, конференц-связь, перехват звонка).
