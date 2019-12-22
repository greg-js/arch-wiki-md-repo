Ссылки по теме

*   [Network Debugging](/index.php/Network_Debugging "Network Debugging")
*   [Межсетевой экран](/index.php/%D0%9C%D0%B5%D0%B6%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D1%8D%D0%BA%D1%80%D0%B0%D0%BD "Межсетевой экран")
*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Раздача интернета](/index.php/%D0%A0%D0%B0%D0%B7%D0%B4%D0%B0%D1%87%D0%B0_%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B5%D1%82%D0%B0 "Раздача интернета")
*   [Router](/index.php/Router "Router")

**Состояние перевода:** На этой странице представлен перевод статьи [Network configuration](/index.php/Network_configuration "Network configuration"). Дата последней синхронизации: 21 декабря 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Network_configuration&diff=0&oldid=591458).

В этой статье описана настройка подключения к сети на [3-м уровне сетевой модели OSI](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D1%8B_%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE_%D1%83%D1%80%D0%BE%D0%B2%D0%BD%D1%8F и [/Wireless (Русский)](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Wireless_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)/Wireless (Русский)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Проверка подключения](#Проверка_подключения)
    *   [1.1 Ping](#Ping)
*   [2 Управление сетевым подключением](#Управление_сетевым_подключением)
    *   [2.1 net-tools](#net-tools)
    *   [2.2 iproute2](#iproute2)
    *   [2.3 Сетевые интерфейсы](#Сетевые_интерфейсы)
        *   [2.3.1 Обнаружение сетевых интерфейсов](#Обнаружение_сетевых_интерфейсов)
        *   [2.3.2 Включение и отключение сетевых интерфейсов](#Включение_и_отключение_сетевых_интерфейсов)
    *   [2.4 Статический IP-адрес](#Статический_IP-адрес)
    *   [2.5 IP-адреса](#IP-адреса)
    *   [2.6 Таблицы маршрутизации](#Таблицы_маршрутизации)
    *   [2.7 DHCP](#DHCP)
    *   [2.8 Сетевые менеджеры](#Сетевые_менеджеры)
*   [3 Установка имени хоста](#Установка_имени_хоста)
    *   [3.1 Разрешение имени хоста](#Разрешение_имени_хоста)
    *   [3.2 Разрешение имён хостов локальной сети](#Разрешение_имён_хостов_локальной_сети)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 Смена имени интерфейса](#Смена_имени_интерфейса)
    *   [4.2 Традиционные названия интерфейсов](#Традиционные_названия_интерфейсов)
    *   [4.3 Установка MTU и длины очереди](#Установка_MTU_и_длины_очереди)
    *   [4.4 Объединение сетевых интерфейсов (bonding) или LAG](#Объединение_сетевых_интерфейсов_(bonding)_или_LAG)
    *   [4.5 Создание псевдонимов IP-адресов](#Создание_псевдонимов_IP-адресов)
        *   [4.5.1 Пример](#Пример)
    *   [4.6 "Неразборчивый" режим](#"Неразборчивый"_режим)
    *   [4.7 Получение информации о сокетах](#Получение_информации_о_сокетах)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Проблема масштабирования TCP window](#Проблема_масштабирования_TCP_window)
        *   [5.1.1 Диагностика](#Диагностика)
        *   [5.1.2 Способы решения проблемы](#Способы_решения_проблемы)
            *   [5.1.2.1 Плохой](#Плохой)
            *   [5.1.2.2 Хороший](#Хороший)
            *   [5.1.2.3 Лучший](#Лучший)
        *   [5.1.3 Дополнительная информация](#Дополнительная_информация)
*   [6 Смотрите также](#Смотрите_также)

## Проверка подключения

При появлении проблем с подключением последовательно выполните описанные ниже шаги и убедитесь, что:

1.  [Сетевой интерфейс](#Сетевые_интерфейсы) обнаружен и включён. В противном случае, проверьте драйвер устройства – см. [/Ethernet (Русский)#Драйвер устройства](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Ethernet_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Драйвер_устройства "Network configuration (Русский)/Ethernet (Русский)") или [/Wireless (Русский)#Драйвер устройства](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Wireless_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Драйвер_устройства "Network configuration (Русский)/Wireless (Русский)").
2.  Вы подключены к сети: воткнут сетевой кабель или есть [подключение к беспроводной сети](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Wireless_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)/Wireless (Русский)").
3.  Сетевому интерфейсу присвоен [IP-адрес](#IP-адреса).
4.  [Таблица маршрутизации](#Таблицы_маршрутизации) настроена правильно.
5.  Возможно выполнить [ping](#Ping) локального IP-адреса (например, [шлюза по умолчанию](https://en.wikipedia.org/wiki/ru:%D0%A8%D0%BB%D1%8E%D0%B7_%D0%BF%D0%BE_%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E "wikipedia:ru:Шлюз по умолчанию")).
6.  Возможно выполнить [ping](#Ping) публичного IP-адреса (например, `8.8.8.8` — DNS-сервер Google и удобный адрес для проверки подключения).
7.  Работает [распознавание доменных имен](/index.php/Domain_name_resolution "Domain name resolution") (например, `archlinux.org`).

### Ping

Чтобы установить, есть ли связь с удалённым хостом, используется утилита [ping](https://en.wikipedia.org/wiki/ru:ping "wikipedia:ru:ping"). Утилита посылает хосту ICMP-пакеты и записывает полученные ответы:

 `$ ping www.example.com` 
```
PING www.example.com (93.184.216.34): 56(84) data bytes
64 bytes from 93.184.216.34: icmp_seq=0 ttl=56 time=11.632 ms
64 bytes from 93.184.216.34: icmp_seq=1 ttl=56 time=11.726 ms
64 bytes from 93.184.216.34: icmp_seq=2 ttl=56 time=10.683 ms
...
```

Для каждого полученного ответа будет выведена соответствующая информация, как показано выше. См. справочную страницу [ping(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) для получения более подробной информации. Также обратите внимание, что удалённый хост может игнорировать ICMP-запросы. [[1]](https://unix.stackexchange.com/questions/412446/how-to-disable-ping-response-icmp-echo-in-linux-all-the-time)

Кроме того, если вы не получаете ответов, это может быть связано со шлюзом по умолчанию или интернет-провайдером. Можно воспользоваться утилитой [traceroute](/index.php/Traceroute "Traceroute") для диагностики маршрута к хосту.

**Примечание:** Если вы получили сообщение об ошибке `ping: icmp open socket: Operation not permitted` во время выполнения *ping*, попробуйте переустановить пакет [iputils](https://www.archlinux.org/packages/?name=iputils).

## Управление сетевым подключением

Чтобы настроить сетевое подключение, последовательно выполните следующие действия:

1.  Убедитесь, что [сетевой интерфейс](#Сетевые_интерфейсы) обнаружен и включен;
2.  Подключитесь к сети. Вставьте Ethernet-кабель или [подключитесь к беспроводной сети](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Wireless_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network configuration (Русский)/Wireless (Русский)").
3.  Настройте сетевое подключение:
    *   [статический IP-адрес](#Статический_IP-адрес);
    *   динамический IP-адрес: используйте [DHCP](#DHCP)

**Примечание:** Установочный образ Arch Linux автоматически запускает [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") (`dhcpcd@*interface*.service`) для [подключения по проводной сети](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) во время загрузки.

### net-tools

Набор утилит [net-tools](https://www.archlinux.org/packages/?name=net-tools) считается устаревшим, рекомендуется использовать вместо него пакет [iproute2](https://www.archlinux.org/packages/?name=iproute2). [[2]](https://www.archlinux.org/news/deprecation-of-net-tools/)

| Устаревшая команда | Замена |
| arp | ip neigh |
| [ifconfig](https://en.wikipedia.org/wiki/ru:ifconfig "wikipedia:ru:ifconfig") | ip address, ip link |
| netstat | [ss](#Получение_информации_о_сокетах) |
| route | ip route |

Более подробную информацию о замене устаревших команд можно найти в [этом сообщении](https://dougvitale.wordpress.com/2011/12/21/deprecated-linux-networking-commands-and-their-replacements/).

### iproute2

[iproute2](https://en.wikipedia.org/wiki/ru:iproute2 "wikipedia:ru:iproute2") — зависимость [мета-пакета](/index.php/%D0%9C%D0%B5%D1%82%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%B0 "Мета-пакета") [base](https://www.archlinux.org/packages/?name=base), включающий интерфейс командной строки для управления [сетевыми интерфейсами](#Сетевые_интерфейсы), [IP-адресами](#IP-адреса) и [таблицей маршрутизации](#Таблицы_маршрутизации). Не забудьте, что настройки, сделанные посредством `ip`, не сохранятся после перезагрузки. Для применения постоянных настроек можно использовать [сетевой менеджер](#Сетевые_менеджеры) или автоматизировать *ip*-команды посредством скриптов или [файлов юнитов systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Написание_файлов_юнитов "Systemd (Русский)"). Также обратите внимание, что `ip` команды часто имеют сокращённую форму, но в этой статье для большей ясности они указаны полностью.

### Сетевые интерфейсы

По умолчанию, [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") дает имена сетевым интерфейсам в соответствии со [схемой именования](https://www.freedesktop.org/software/systemd/man/systemd.net-naming-scheme.html), в которой тип устройства обозначается двухбуквенным префиксом: `en` (проводной/[Ethernet](https://en.wikipedia.org/wiki/ru:Ethernet "wikipedia:ru:Ethernet")), `wl` (беспроводной/[WLAN](https://en.wikipedia.org/wiki/ru:%D0%91%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%B0%D1%8F_%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D1%81%D0%B5%D1%82%D1%8C "wikipedia:ru:Беспроводная локальная сеть")) или `ww` ([WWAN](https://en.wikipedia.org/wiki/ru:WWAN "wikipedia:ru:WWAN")).

**Совет:** Для смены имени интерфейса изучите разделы [#Смена имени интерфейса](#Смена_имени_интерфейса) и [#Традиционные названия интерфейсов](#Традиционные_названия_интерфейсов).

#### Обнаружение сетевых интерфейсов

Имена как проводных, так и беспроводных интерфейсов можно найти посредством команд `ls /sys/class/net` и `ip link`. Имейте в виду, что префиксом `lo` обозначается [петлевое устройство](https://en.wikipedia.org/wiki/loop_device "wikipedia:loop device"), которое не используется для создания сетевого подключения.

Имена беспроводных устройств также можно получить посредством `iw dev`. См. также [/Wireless (Русский)#Определение имени интерфейса](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Wireless_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Определение_имени_интерфейса "Network configuration (Русский)/Wireless (Русский)").

Если сетевой интерфейс не обнаружен, убедитесь, что драйвер устройства ([проводного](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Ethernet_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Драйвер_устройства "Network configuration (Русский)/Ethernet (Русский)") или [беспроводного](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Wireless_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Драйвер_устройства "Network configuration (Русский)/Wireless (Русский)")) был успешно загружен во время запуска системы.

#### Включение и отключение сетевых интерфейсов

Включение и выключение интерфейса производится командой `ip link set *интерфейс* up|down` (подробнее см. [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8)).

Для проверки текущего состояния интерфейса (например, `enp2s0`) выполните:

 `$ ip link show dev enp2s0` 
```
2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
...

```

На состояние интерфейса указывает слово `UP` в `<BROADCAST,MULTICAST,UP,LOWER_UP>`, а не в `state UP`.

**Примечание:** Если выключить интерфейс, через который проходит маршрут по умолчанию, то маршрут будет удалён. Последующее включение интерфейса не восстановит автоматически исходный маршрут. Чтобы восстановить маршрут вручную воспользуйтесь информацией из раздела [#Таблицы маршрутизации](#Таблицы_маршрутизации).

### Статический IP-адрес

Настройка статического IP-адреса производится либо посредством [сетевого менеджера](#Сетевые_менеджеры), либо с помощью демона [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)").

Чтобы настроить статический IP-адрес вручную, добавьте IP-адрес как описано в разделе [#IP-адреса](#IP-адреса), настройте [таблицу маршрутизации](#Таблицы_маршрутизации) и [DNS-сервер](/index.php/Domain_name_resolution "Domain name resolution").

### IP-адреса

Для управления [IP-адресами](https://en.wikipedia.org/wiki/ru:IP-%D0%B0%D0%B4%D1%80%D0%B5%D1%81 "wikipedia:ru:IP-адрес") используется команда [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8).

Показать существующие IP-адреса:

```
$ ip address show

```

Добавить IP-адрес к сетевому интерфейсу:

```
# ip address add *адрес/длина_префикса* broadcast + dev *интерфейс*

```

	Обратите внимание:

*   адрес указан в [CIDR-нотации](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing") вместе с [маской подсети](https://en.wikipedia.org/wiki/ru:%D0%9F%D0%BE%D0%B4%D1%81%D0%B5%D1%82%D1%8C "wikipedia:ru:Подсеть");
*   спецсимвол `+` говорит утилите `ip` вычислить [широковещательный адрес](https://en.wikipedia.org/wiki/ru:%D0%A8%D0%B8%D1%80%D0%BE%D0%BA%D0%BE%D0%B2%D0%B5%D1%89%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9_%D0%B0%D0%B4%D1%80%D0%B5%D1%81 "wikipedia:ru:Широковещательный адрес") на основе IP-адреса и маски подсети.

**Примечание:** Убедитесь, что добавленные вручную IP-адреса не конфликтуют с адресами, добавленными DHCP.

Удалить IP-адрес устройства:

```
$ ip address del *адрес/длина_префикса* broadcast + dev *интерфейс*

```

Удалить все адреса определенного интерфейса (можно добавить критерий, на соответствие которому будет проверяться каждый адрес перед удалением):

```
$ ip address flush dev *интерфейс*

```

**Совет:** IP-адрес можно вычислить с помощью [ipcalc](http://jodies.de/ipcalc) ([ipcalc](https://www.archlinux.org/packages/?name=ipcalc)).

### Таблицы маршрутизации

С помощью [таблицы маршрутизации](https://en.wikipedia.org/wiki/ru:%D0%A2%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0_%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8 "wikipedia:ru:Таблица маршрутизации") определяется возможность достижения удалённого хоста, напрямую или посредством какого-либо шлюза (маршрутизатора). Если подходящего маршрута нет, то используется адрес [шлюза по умолчанию](https://en.wikipedia.org/wiki/ru:%D0%A8%D0%BB%D1%8E%D0%B7_%D0%BF%D0%BE_%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E "wikipedia:ru:Шлюз по умолчанию").

Настройка таблицы маршрутизации производится посредством команды [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8).

В приведённых ниже примерах значение *ПРЕФИКС* либо указывается в [CIDR-нотации](https://en.wikipedia.org/wiki/ru:%D0%91%D0%B5%D1%81%D0%BA%D0%BB%D0%B0%D1%81%D1%81%D0%BE%D0%B2%D0%B0%D1%8F_%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0%D1%86%D0%B8%D1%8F "wikipedia:ru:Бесклассовая адресация"), либо принимает значение `default` для шлюза по умолчанию.

Показать маршруты IPv4:

```
$ ip route show

```

Показать маршруты IPv6:

```
$ ip -6 route show

```

Добавить маршрут:

```
# ip route add *ПРЕФИКС* via *адрес* dev *интерфейс*

```

Удалить маршрут:

```
# ip route del *ПРЕФИКС* via *адрес* dev *интерфейс*

```

### DHCP

Сервер [DHCP](https://en.wikipedia.org/wiki/ru:DHCP "wikipedia:ru:DHCP") предоставляет клиенту динамический IP-адрес, маску подсети, IP-адрес шлюза по умолчанию и опционально — сервер имён DNS.

**Примечание:** Запускать несколько DHCP-клиентов одновременно запрещено.

Для использования DHCP нужен DHCP-сервер в вашей сети и DHCP-клиент на локальной машине:

| Клиент | Пакет | [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") | Примечания | [Юниты systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Использование_юнитов "Systemd (Русский)") |
| [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) | Да | DHCP, DHCPv6, ZeroConf, статический IP | `dhcpcd.service`, `dhcpcd@*интерфейс*.service` |
| [ISC dhclient](https://www.isc.org/downloads/dhcp/) | [dhclient](https://www.archlinux.org/packages/?name=dhclient) | Да | DHCP, DHCPv6, BOOTP, статический IP | `dhclient@*интерфейс*.service` |

Обратите внимание, что вместо непосредственно DHCP-клиента вы также можете воспользоваться [сетевым менеджером](#Сетевые_менеджеры).

**Совет:** Проверить, запущен ли DHCP-сервер, можно с помощью [dhcping](https://www.archlinux.org/packages/?name=dhcping).

### Сетевые менеджеры

Сетевой менеджер позволяет создавать т.н. "сетевые профили", содержащие настройки сетевого подключения, что облегчает переключение между сетями.

**Примечание:** Выбор приложений довольно широк, но нужно помнить, что все варианты взаимоисключают друг друга. Запускать два сетевых демона одновременно запрещено.

| Сетевой менеджер | Графический интерфейс | [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") [[3]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | Утилиты командной строки | Поддержка [PPP](https://en.wikipedia.org/wiki/ru:PPP_(%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB) "wikipedia:ru:PPP (сетевой протокол)")
(например, 3G-модем) | [DHCP-клиент](#DHCP) | [Юниты](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Написание_файлов_юнитов "Systemd (Русский)") systemd |
| [ConnMan](/index.php/ConnMan "ConnMan") | 8 неофиц. | Нет | [connmanctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connmanctl.1) | Да (с [ofono](https://aur.archlinux.org/packages/ofono/)) | встроенный | `connman.service` |
| [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)") | 2 неофиц. | Да | [netctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1), wifi-menu | Да | [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") или [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `netctl-ifplugd@*интерфейс*.service`, `netctl-auto@*интерфейс*.service` |
| [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)") | Да | Нет | [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1), [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1) | Да | встроенный, [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") или [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `NetworkManager.service` |
| [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") | Нет | Да ([base](https://www.archlinux.org/packages/?name=base)) | [networkctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/networkctl.1) | Нет [[4]](https://github.com/systemd/systemd/issues/481) | встроенный | `systemd-networkd.service`, `systemd-resolved.service` |
| [Wicd](/index.php/Wicd "Wicd") | Да | Нет | [wicd-cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-cli.8), [wicd-curses(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-curses.8) | Нет | [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | `wicd.service` |

Для беспроводных подключений доступно приложение с графическим интерфейсом [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar"), которое управляет WiFi-сетями посредством [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools). Для проводных подключений не работает.

Полный список сетевых менеджеров можно найти в статье [List of applications (Русский)#Управление подключениями](/index.php/List_of_applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Управление_подключениями "List of applications (Русский)").

## Установка имени хоста

[Имя хоста](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") — уникальное имя-идентификатор машины в сети. Имя хоста содержится в файле `/etc/hostname`, описание которого и правила распознавания имён можно найти в справочных страницах [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) и [hostname(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7) соответственно. В файле также может храниться доменное имя системы, если оно существует. Чтобы задать имя компьютера, добавьте в файл `/etc/hostname` одну строку:

 `/etc/hostname` 
```
*имя-хоста*

```

**Совет:** В [RFC 1178](https://tools.ietf.org/html/rfc1178) находятся рекомендации по выбору имени компьютера.

В качестве альтернативы для задания имени компьютера можно воспользоваться утилитой [hostnamectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostnamectl.1):

```
# hostnamectl set-hostname *имя-хоста*

```

Утилита [hostname(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.1) из пакета [inetutils](https://www.archlinux.org/packages/?name=inetutils) позволяет задать имя хоста временно, до первой перезагрузки:

```
# hostname *имя-хоста*

```

На странице справочного руководства [machine-info(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/machine-info.5) можно найти информацию о том, как задать "красивое" имя машины и другие метаданные.

### Разрешение имени хоста

Модуль `nss-myhostname` входящей в состав [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") службы [Name Service Switch](/index.php/Name_Service_Switch "Name Service Switch") (NSS) позволяет выполнять разрешение имени локального хоста без обращения к файлу `/etc/hosts`. Этот модуль включён по умолчанию. Однако следует иметь в виду, что некоторые программы всё же полагаются на файл `/etc/hosts`. [[5]](https://lists.debian.org/debian-devel/2013/07/msg00809.html), [[6]](https://bugzilla.mozilla.org/show_bug.cgi?id=87717#c55)

Чтобы настроить файл `/etc/hosts`, добавьте в него следующие строки:

```
127.0.0.1        localhost
::1              localhost
127.0.1.1        *имя-хоста*.localdomain        *имя-хоста*

```

**Примечание:** Порядок соответствующих IP-адресам имён компьютера и псевдонимов имеет значение. Сразу после IP-адреса следует "каноническое" имя хоста, к которому при неоходимости может присоединиться название родительского домена, отделенное от имени точкой (как, например, `.localdomain` выше). Все последующие значения на той же строке считаются псевдонимами. Подробности можно найти на странице документации [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5).

В результате система будет использовать оба варианта — и NSS, и файл `/etc/hosts`:

 `$ getent hosts` 
```
127.0.0.1       localhost
127.0.0.1       localhost
127.0.1.1       *имя-хоста*.localdomain *имя-хоста*

```

**Примечание:** Если хосту присвоен статический IP-адрес, то этот адрес следует указать вместо `127.0.1.1`.

### Разрешение имён хостов локальной сети

Чтобы машина была доступна по локальной сети посредством имени хоста, следует выбрать один из вариантов:

*   отредактировать файл `/etc/hosts` на каждом устройстве вашей локальной сети, см. [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5);
*   выбрать [DNS-сервер](/index.php/Domain_name_resolution#DNS_servers "Domain name resolution") для разрешения вашего имени хоста и настроить все машины в локальной сети использовать его (например, посредством [#DHCP](#DHCP));
*   использовать сервис [Zeroconf](https://en.wikipedia.org/wiki/ru:Zeroconf "wikipedia:ru:Zeroconf"), осуществляющий автоматическое создание IP-сети без необходимости выполнения ручных настроек. Можно выбрать одну из двух реализаций:
    *   [NetBIOS](https://en.wikipedia.org/wiki/ru:NetBIOS "wikipedia:ru:NetBIOS"). Разработан компанией Microsoft, входит в состав [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)"). Всё, что необходимо — запустить `nmb.service`. Машины с операционными системами Windows, macOS, или Linux и работающим `nmb` смогут найти ваш компьютер в сети;
    *   [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS"). Возможны два варианта использования: [Avahi](/index.php/Avahi#Hostname_resolution "Avahi") и [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"). Компьютеры с macOS или Linux, на которых запущен Avahi или systemd-resolved, смогут обнаружить ваш хост. Windows не имеет встроенного mDNS клиента или демона.

## Советы и рекомендации

### Смена имени интерфейса

Вы можете изменить имя устройства, установив его вручную при помощи правила udev. Например:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"

```

Кое-что на заметку:

*   Чтобы увидеть MAC-адрес каждой платы, используйте команду `cat /sys/class/net/*имя_устройства*/address`
*   Убедитесь, что в ваших правилах udev используются шестнадцатиричные значения со строчным написанием. Буквы не должны быть прописными

Если сетевая плата имеет динамический MAC-адрес, вы можете использовать `DEVPATH`, например:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"
SUBSYSTEM=="net", DEVPATH=="/devices/pci*/*1c.0/*/net/*", NAME="en"

```

Чтобы получить `DEVPATH` всех подключённых устройств, посмотрите куда указывают символические ссылки в `/sys/class/net/`. Например:

 `file /sys/class/net/*` 
```
/sys/class/net/enp0s20f0u4u1: symbolic link to ../../devices/pci0000:00/0000:00:14.0/usb2/2-4/2-4.1/2-4.1:1.0/net/enp0s20f0u4u1
/sys/class/net/enp0s31f6:     symbolic link to ../../devices/pci0000:00/0000:00:1f.6/net/enp0s31f6
/sys/class/net/lo:            symbolic link to ../../devices/virtual/net/lo
/sys/class/net/wlp4s0:        symbolic link to ../../devices/pci0000:00/0000:00:1c.6/0000:04:00.0/net/wlp4s0

```

Паттерн пути устройства (DEVPATH) должен подходить для обоих названий устройств, и нового, и старого, поскольку правило udev может срабатывать в процессе загрузки более одного раза. Например, для второго правила в примере выше назначается название устройства `en`, и если указать путь `"/devices/pci*/*1c.0/*/net/enp*"`, то паттерн не подойдет. Если после этого системное правило по умолчанию сработает во второй раз, то название изменится обратно на, к примеру, `enp1s0`.

Если вы используете USB-интерфейс (например, подключаясь через Android-смартфон) с динамическим MAC-адресом и хотите иметь возможность использовать разные USB-порты, вы можете создать правило на основе данных о производителе и ID устройства:

 `/etc/udev/rules.d/10-network.rules`  `SUBSYSTEM=="net", ACTION=="add", ATTRS{idVendor}=="12ab", ATTRS{idProduct}=="3cd4", NAME="net2"` 

Если необходимо [проверить](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Проверка_правил_перед_загрузкой "Udev (Русский)") созданное правило, его можно запустить непосредственно из пространства пользователя, например командой `udevadm --debug test /sys/class/net/*`. Не забудьте предварительно отключить интерфейс, который собираетесь переименовать (например, выполнив `ip link set enp1s0 down`).

**Примечание:** При выборе статических имен **вы должны избегать использования формата "eth*X*" и "wlan*X*"**, поскольку это может привести к "гонке" между ядром и udev во время загрузки системы. Вместо этого лучше взять имена интерфейсов, которые не используются по умолчанию в ядре, например: `net0`, `net1`, `wifi0`, `wifi1`. Для получения дополнительной информации, пожалуйста, смотрите документацию по [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames)

### Традиционные названия интерфейсов

Если вы предпочитаете восстановить традиционные названия интерфейсов вроде `eth0`, использование [предсказуемых имён интерфейсов](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) может быть отключено с помощью создания маски для правила udev.

```
# ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

```

Другой способ — добавить `net.ifnames=0` в [параметры ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)").

### Установка MTU и длины очереди

Вы можете изменить [MTU](https://en.wikipedia.org/wiki/ru:Maximum_transmission_unit "wikipedia:ru:Maximum transmission unit") и длину очереди для устройства, определив их вручную в правиле udev. Например:

 `/etc/udev/rules.d/10-network.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1500", ATTR{tx_queue_len}="2000"` 
**Примечание:**

*   `mtu`: Для PPPoE величина MTU не должна превышать 1492\. Также значение MTU можно задать посредством [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5).
*   `tx_queue_len`: Малые значения — для медленных устройств с высокой задержкой ([ADSL](https://en.wikipedia.org/wiki/ru:ADSL "wikipedia:ru:ADSL"), [ISDN](https://en.wikipedia.org/wiki/ru:ISDN "wikipedia:ru:ISDN")). Большие значения рекомендованы для высокоскоростных подключений к серверам, где требуется передача значительных объёмов данных.

### Объединение сетевых интерфейсов (bonding) или LAG

Бондинг — объединение нескольких сетевых интерфейсов в одно логическое устройство. Подробную информацию можно найти в соответствующем [разделе](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Объединение_сетевых_интерфейсов_(бондинг) "Netctl (Русский)") о бондинге в netctl, а также в статье [Wireless bonding](/index.php/Wireless_bonding "Wireless bonding").

### Создание псевдонимов IP-адресов

Псевдонимы (aliases) необходимы для назначения нескольких IP-адресов одному сетевому интерфейсу. Благодаря этому один узел сети может иметь несколько подключений, каждое из которых используется в своих целях. Типичное использование этой возможности — виртуальный хостинг Web- и FTP-серверов или реорганизация серверов без необходимости обновления каких-либо других машин (это особенно полезно для серверов имен (nameservers)).

#### Пример

Чтобы вручную назначить псевдоним для определенного сетевого интерфейса (например, `enp2s0`) используйте входящую в состав пакета [iproute2](https://www.archlinux.org/packages/?name=iproute2) утилиту *ip*:

```
# ip addr add 192.168.2.101/24 dev enp2s0 label enp2s0:1

```

Для удаления псевдонима выполните

```
# ip addr del 192.168.2.101/24 dev enp2s0:1

```

По умолчанию для исходящих из определённой подсети пакетов используется основной псевдоним устройства. Если же отправитель находится в подсети вторичного псевдонима, то IP-адрес отправителя в заголовке пакета будет соответствующим. В случае наличия более чем одного сетевого интерфейса маршруты по умолчанию можно уточнить командой `ip route`.

### "Неразборчивый" режим

Включение ["неразборчивого" режима](https://en.wikipedia.org/wiki/ru:Promiscuous_mode "wikipedia:ru:Promiscuous mode") заставит (беспроводную) сетевую плату перенаправлять весь трафик, который она получает, в операционную систему для дальнейшей обработки. Это противоположность "нормальному режиму", при котором сетевая плата будет терять пакеты, не предназначенные для приема. Чаще всего эта возможность используется для продвинутого решения сетевых проблем и [анализа пакетов](https://en.wikipedia.org/wiki/ru:%D0%90%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80_%D1%82%D1%80%D0%B0%D1%84%D0%B8%D0%BA%D0%B0 "wikipedia:ru:Анализатор трафика").

 `/etc/systemd/system/promiscuous@.service` 
```
[Unit]
Description=Set %i interface in promiscuous mode
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i promisc on
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Если вы хотите включить "неразборчивый" режим для интерфейса `eth0`, выполните:

```
# systemctl enable promiscuous@eth0.service

```

### Получение информации о сокетах

Входящая в состав пакета [iproute2](https://www.archlinux.org/packages/?name=iproute2) утилита *ss* используется для вывода информации о сокетах. Обладает схожим функционалом со считающейся [устаревшей](https://www.archlinux.org/news/deprecation-of-net-tools/) утилитой *netcat*.

Примеры использования:

Показать все TCP-сокеты с названиями сервисов:

```
$ ss -at

```

Показать все TCP-сокеты с номерами портов:

```
$ ss -atn

```

Показать все UDP-сокеты:

```
$ ss -au

```

За подробной информацией обращайтесь к справочной странице [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8).

## Решение проблем

### Проблема масштабирования TCP window

Пакеты TCP содержат в своих заголовках значение "window", обозначающее, как много данных другие узлы могут посылать в ответ. Это значение может содержать только 16 бит информации, следовательно, размер window должен быть не более 64Kб. Пакеты TCP на некоторое время кэшируются (они должны быть перераспределены), а, поскольку память ограничена, один узел может легко перевалить за это значение.

В далеком 1992 году становилось доступно все больше и больше памяти, и для улучшения ситуации был написан [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html): Window Scaling. Значение "window", содержащееся во всех пакетах, будет изменено при помощи коэффициента масштабирования (Scale Factor), определяемого один раз в самом начале подключения. Этот 8-битный коэффициент масштабирования позволяет Window быть в 32 раза больше, чем изначальные 64Kб.

Похоже, некоторые нестандартные маршрутизаторы и межсетевые экраны в интернете переписывают этот коэффициент в значение 0, что вызывает недопонимание между узлами. В ядре Linux версии 2.6.17 была представлена новая схема подсчета, генерирующая максимальные коэффициенты масштабирования и виртуально делающая последующие подсчеты нестандартных маршрутизаторов и межсетевых экранов более видимыми.

В итоге соединение в лучшем случае очень медленное или часто рвется.

#### Диагностика

Прежде всего, необходимо разъяснить: это странная проблема. В некоторых случаях вы не сможете по-полной использовать соединения TCP (HTTP, FTP и т.д.), в других вы сможете обращаться к некоторым узлам (лишь нескольким).

Если у вас появилась такая проблема, вывод `dmesg` будет нормальным, логи - чистыми, а `ip addr` сообщит о нормальном состоянии... Все будет выглядеть нормально.

Если вы не можете просматривать никакие веб-сайты, но можете отправлять запросы ping на некоторые узлы, высока вероятность, что у вас именно эта проблема: ping использует ICMP и не затрагивается проблемами TCP.

Вы можете попробовать использовать [Wireshark](/index.php/Wireshark "Wireshark"). В итоге вы можете получить успешные соединения UDP и ICMP, но неудачные соединения TCP (только для неизвестных узлов).

#### Способы решения проблемы

##### Плохой

Плохой способ заключается в изменении значения `tcp_rmem`, на котором основывается подсчет коэффициента масштабирования. Несмотря на то, что это должно помочь для большинства узлов, это не гарантирует успеха, особенно для очень удаленных из них.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

##### Хороший

Просто отключите масштабирование Window. Поскольку оно - лишь приятная функция TCP, это может быть некомфортно, особенно, если вы не можете исправить проблему с нестандартным маршрутизатором. Есть несколько способов отключения этого масштабирования, и, кажется, наиболее "пуленепробиваемый" из них (который будет работать с большинством ядер) - добавление следующей строки в файл `/etc/sysctl.d/99-disable_window_scaling.conf` (смотрите также статью [sysctl](/index.php/Sysctl "Sysctl")):

```
net.ipv4.tcp_window_scaling = 0

```

##### Лучший

Проблема вызвана нестандартными маршрутизаторами/межсетевыми экранами, поэтому замените их. Некоторые пользователи отмечали, что нестандартным маршрутизатором был их собственный маршрутизатор DSL.

#### Дополнительная информация

Этот раздел основывается на статьях LWN [Масштабирование window TCP и нестандартные маршрутизаторы](http://lwn.net/Articles/92727/) и Kernel Trap [Масштабирование Window в интернете](http://kerneltrap.org/node/6723).

На странице LKML есть также несколько ссылок по теме.

## Смотрите также

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/index.html)
*   [Debian Reference: Network setup](https://www.debian.org/doc/manuals/debian-reference/ch05.en.html)
*   [RHEL7: Networking Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/)
*   [Linux Home Networking](http://www.linuxhomenetworking.com/wiki/)
*   [Monitoring and tuning the Linux Networking Stack: Receiving data](https://blog.packagecloud.io/eng/2016/06/22/monitoring-tuning-linux-networking-stack-receiving-data/)
*   [Monitoring and tuning the Linux Networking Stack: Sending data](https://blog.packagecloud.io/eng/2017/02/06/monitoring-tuning-linux-networking-stack-sending-data/)
*   [Tracing a packet journey using tracepoints, perf and eBPF](http://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/)