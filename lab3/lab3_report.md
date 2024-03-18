University: [ITMO University](https://itmo.ru/ru/) <br/>
Faculty: [FICT](https://fict.itmo.ru) <br/>
Course: [IP-telephony](https://github.com/itmo-ict-faculty/ip-telephony)<br/>
Year: 2023/2024<br/>
Group: K34202<br/>
Author: Donina Daria Dmitrievna<br/>
Lab: Lab3<br/>
Date of create: 18.03.2024<br/>
Date of finished: 19.03.2024<br/>

# Цель работы
Изучить программный комплекс Asterisk. Настроить Asterisk для локальных звонков.

# Ход работы

Установим Asterisk на Ubutu:
```
sudo apt-get install asterisk
```
Настроим SIP-каналы. В файл /etc/asterisk/sip.conf добавим информация о телефонах 1000 и 1001:
```
[1000]
type=friend
host=dynamic
secret=1000
context=ext_1000

[1001]
type=friend
host=dynamic
secret=1001
context=ext_1001
```
Также настроим конфигурацию в файле /etc/asterisk/extensions.conf:
```
[ext_1000]
exten => _XXXX,1,Dial(SIP/${EXTEN})

[ext_1001]
exten => _XXXX,1,Dial(SIP/${EXTEN})
```

Перезапустим asterisk, чтобы применить изменения:
```
sudo service asterisk restart
```

Установим soft-телефон Zoiper5 с официального сайта, войдем под номером 1000, который указан в конфигурации. Hostname указываем localhost.

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/3b17ce12-9391-4eda-a09a-7e8b4a518233)

Доступен протокол SIP UDP:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/4a3828fc-7511-45de-8a4a-6ea70feda432)

Для второго канала установим и настроим аккаунт MicroSIP:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/d050ae3f-e129-4c83-83f4-d0d52da8a3eb)

С помощью команд
```
sudo asterisk -r
sip show peers
```
Увидим созданные и настроенные SIP-каналы:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/0f93c55b-835f-4b60-8f03-2c63c4aedce2)

Совершен звонок с 1001 на 1000, соединение было установлено:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/91d42c1d-5ffc-4aae-9b96-f23f5594a6e4)

Звонок с 1000 на 1001 также установлен:

![image](https://github.com/Daria-Donina/2023_2024-ip-telephony-k34202-donina_d_d/assets/43678323/8689d402-195b-45b9-8bb3-277e4fd19a8e)

# Вывод

В ходе данной лабораторной работы был изучен и настроен для локальных звонков программный комплекс Asterisk.
