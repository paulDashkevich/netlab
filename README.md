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
- 192.168.1.0/25 - dev
- 192.168.1.128/26 - test servers
- 192.168.1.192/26 - office hardware

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
-- в Office1 26 маска означает 4 подсети и 64 хоста за минусом адреса бродкаста и самой подсети - итого 62 адреса в каждой подсети. Свободной здесь будет первая подсеть с адресами для хостов 1-62. Бродкастовые адреса 192.168.2.63, -127, -191, -255.
-- в office2 /25 Разрешает 2 подсети и 1 первая подсеть содержит 126 адресов для хостов, бродкаст - -127; вторая подсеть поделена на 2 подсети по 62 адреса на хост, где бродкастовые адреса: -191, -255.
-- в Central в первой подсети 14 может быть хостов, во второй тоже, в третьей 62. Бродкасты: -15, -47, -127.
