# Домашнее задание по сетям #
https://github.com/erlong15/otus-linux/tree/network
(ветка network)
Vagrantfile с начальным построением сети
- inetRouter
- centralRouter
- centralServer

# Планируемая архитектура
построить следующую архитектуру
Сеть office1
- 192.168.2.0/26 - dev
- 192.168.2.64/26 - test servers
- 192.168.2.128/26 - managers
- 192.168.2.192/26 - office hardware

Сеть office2
- 192.168.10.0/25 - dev
- 192.168.10.128/26 - test servers
- 192.168.10.192/26 - office hardware

Сеть central
- 192.168.0.0/28 - directors
- 192.168.0.32/28 - office hardware
- 192.168.0.64/26 - wifi

```
Office1 ---\
-----> Central --IRouter --> internet
Office2----/
```
Итого должны получится следующие сервера
- inetRouter
- centralRouter
- office1Router
- office2Router
- centralServer
- office1Server
- office2Server

# Теоретическая часть
- Найти свободные подсети
- Посчитать сколько узлов в каждой подсети, включая свободные
- Указать broadcast адрес для каждой подсети
- проверить нет ли ошибок при разбиении

# Практическая часть
- Соединить офисы в сеть согласно схеме и настроить роутинг
- Все сервера и роутеры должны ходить в инет черз inetRouter
- Все сервера должны видеть друг друга
- у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи
- при нехватке сетевых интервейсов добавить по несколько адресов на интерфейс
- --
**Теоретическая часть**
* найти свободные подсети:
***
Сеть в Office1
- 192.168.2.0/26 - dev 
-- 62 hosts; 
-- broadcast 192.168.2.63;
- 192.168.2.64/26 - test servers
-- 62 hosts;
-- broadcast 192.168.2.127;
- 192.168.2.128/26 - managers
-- 62 hosts;
-- broadcast 192.168.2.191;
- 192.168.2.192/26 - office hardware
-- 62 hosts;
-- broadcast 192.168.2.255
***
Сеть в office2
- 192.168.10.0/25 - dev
-- 126 hosts;
-- broadcast 192.168.10.127
- 192.168.10.128/26 - test servers
-- 62 hosts;
-- broadcast 192.168.10.191;
- 192.168.10.192/26 - office hardware
-- 62 hosts;
-- broadcast 192.168.10.255;
***
-- в Central в первой подсети 14 может быть хостов, во второй тоже, в третьей 62. Бродкасты: -15, -47, -127.
Сеть central
- 192.168.0.0/28 - directors
-- 14 hosts
-- broadcast 192.168.0.15;
- 192.168.0.32/28 - office hardware
-- 14 hosts;
-- broadcast 192.168.47;
- 192.168.0.64/26 - wifi
-- 62 hosts;
-- broadcast 192.168.0.127;
=> свободная сеть 192.168.0.128/25 
-- 126 hosts
-- broadcast 192.168.0.255


 ![Рисунок сети](https://github.com/paulDashkevich/netlab/blob/master/netw1.png)
