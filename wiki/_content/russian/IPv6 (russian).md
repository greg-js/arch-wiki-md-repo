Ссылки по теме

*   [IPv6 tunnel broker setup](/index.php/IPv6_tunnel_broker_setup "IPv6 tunnel broker setup")

**Состояние перевода:** На этой странице представлен перевод статьи [IPv6](/index.php/IPv6 "IPv6"). Дата последней синхронизации: 28 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=IPv6&diff=0&oldid=587192).

В Arch Linux протокол IPv6 включён по умолчанию.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Обнаружение соседей](#Обнаружение_соседей)
*   [2 Автоконфигурация узла (SLAAC)](#Автоконфигурация_узла_(SLAAC))
    *   [2.1 Клиент](#Клиент)
    *   [2.2 Шлюз](#Шлюз)
*   [3 Privacy Extensions](#Privacy_Extensions)
    *   [3.1 dhcpcd](#dhcpcd)
    *   [3.2 NetworkManager](#NetworkManager)
    *   [3.3 systemd-networkd](#systemd-networkd)
    *   [3.4 connman](#connman)
*   [4 Постоянный приватный адрес](#Постоянный_приватный_адрес)
    *   [4.1 NetworkManager](#NetworkManager_2)
*   [5 Статический адрес](#Статический_адрес)
*   [6 IPv6 и PPPoE](#IPv6_и_PPPoE)
*   [7 Делегирование префикса (DHCPv6-PD)](#Делегирование_префикса_(DHCPv6-PD))
    *   [7.1 dibbler](#dibbler)
    *   [7.2 dhcpcd](#dhcpcd_2)
    *   [7.3 WIDE-DHCPv6](#WIDE-DHCPv6)
    *   [7.4 systemd-networkd](#systemd-networkd_2)
    *   [7.5 Другие клиенты](#Другие_клиенты)
*   [8 Отключение IPv6](#Отключение_IPv6)
    *   [8.1 Отключение функциональности](#Отключение_функциональности)
    *   [8.2 Другие программы](#Другие_программы)
        *   [8.2.1 dhcpcd](#dhcpcd_3)
        *   [8.2.2 NetworkManager](#NetworkManager_3)
        *   [8.2.3 ntpd](#ntpd)
    *   [8.3 systemd-networkd](#systemd-networkd_3)
*   [9 Использование IPv4 вместо IPv6](#Использование_IPv4_вместо_IPv6)
*   [10 Смотрите также](#Смотрите_также)

## Обнаружение соседей

Пинг по адресу многоадресной рассылки `ff02::1` заставит все хосты в локальной сети ответить. При этом нужно указать сетевой интерфейс:

```
$ ping ff02::1%eth0

```

После этого список "соседей" по локальной сети можно вывести командой

```
$ ip -6 neigh

```

Аналогично, если сделать пинг по адресу `ff02::2`, то ответят только маршрутизаторы локальной сети.

Если добавить опцию `-I *ваш-глобальный-ipv6*` в пинг-запрос, хосты локальной сети ответят с использованием глобальных адресов. В этом случае сетевой интерфейс можно не указывать:

```
$ ping -I 2001:4f8:fff6::21 ff02::1

```

## Автоконфигурация узла (SLAAC)

Простейший способ получения IPv6-адреса в уже настроенной сети — автоконфигурация узла (SLAAC, Stateless address autoconfiguration). При этом адрес автоматически вычисляется на основании объявленного маршрутизатором префикса сети. Никакие дальнейшие настройки или использование специализированного ПО вроде DHCP-клиента не требуются.

### Клиент

Если вы используете [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)"), то нужно только добавить одну строку в файл настроек вашей проводной или беспроводной сети.

```
IP6=stateless

```

Если вы используете [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)"), то он автоматически включит использование IPv6-адресов, если таковые объявлены в сети.

Нужно также заметить, что для нормальной работы автоконфигурации должны быть разрешены пакеты ICMP для IPv6\. Поэтому необходимо добавить разрешения для пакетов `ipv6-icmp` в настройки межсетевого экрана. Если вы используете [брандмауэр](/index.php/Simple_stateful_firewall_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Simple stateful firewall (Русский)") на основе [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)"), то добавьте следующее правило:

```
-A INPUT -p ipv6-icmp -j ACCEPT

```

Если вы используете другой интерфейс межсетевого экрана (ufw, shorewall и т.д.), то инструкции по разрешению пакетов `ipv6-icmp` нужно искать в документации.

Если вы выбрали сетевой менеджер, который не поддерживает разрешение DNS с бесконтекстным (stateless) IPv6 (например, netctl), то для этох целей можно воспользоваться демоном [rdnssd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rdnssd.8) из пакета [ndisc6](https://www.archlinux.org/packages/?name=ndisc6).

### Шлюз

Чтобы соответствующим образом работать с адресами IPv6 клиентских устройств вашей сети, нужно настроить демон объявлений (advertisement daemon). Для этой задачи используется входящий в [официальные репозитории](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории") пакет [radvd](https://www.archlinux.org/packages/?name=radvd). Настройка *radvd* довольно проста. Добавьте следующие строки в файл `/etc/radvd.conf`, заменив `LAN` на название вашего сетевого интерфейса:

```
interface LAN {
  AdvSendAdvert on;
  MinRtrAdvInterval 3;
  MaxRtrAdvInterval 10;
  prefix ::/64 {
    AdvOnLink on;
    AdvAutonomous on;
    AdvRouterAddr on;
  };
};

```

Такая настройка скажет клиентам выбрать адреса из объявленного блока `/64`. Обратите внимание, что эта настройка объявляет *все доступные префиксы*, привязанные к сетевому интерфейсу. Если вы хотите указать конкретные префиксы, то замените `::/64` на необходимый, например, `2001:DB8::/64`. Блок настроек `prefix` нужно повторить для каждого указанного префикса.

Чтобы объявить DNS-сервера клиентам вашей локальной сети, можно использовать предлагаемую протоколом обнаружения соседей [функциональность RDNSS](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB_%D0%BE%D0%B1%D0%BD%D0%B0%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_%D1%81%D0%BE%D1%81%D0%B5%D0%B4%D0%B5%D0%B9#.D0.A2.D0.B5.D1.85.D0.BD.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D0.B5.D1.82.D0.B0.D0.BB.D0.B8 "wikipedia:ru:Протокол обнаружения соседей"). Например, добавьте следующие строки к файлу `/etc/radvd.conf`, чтобы объявить DNSv6-сервер Google:

```
RDNSS 2001:4860:4860::8888 2001:4860:4860::8844 {
};

```

Шлюз должен также разрешать трафик `ipv6-icmp` во всех основных цепочках межсетевого экрана. Для [брэндмауэра](/index.php/Simple_stateful_firewall_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Simple stateful firewall (Русский)")/[iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") добавьте правила:

```
-A INPUT -p ipv6-icmp -j ACCEPT
-A OUTPUT -p ipv6-icmp -j ACCEPT
-A FORWARD -p ipv6-icmp -j ACCEPT

```

Для других интерфейсов межсетевого экрана выполните аналогичные настройки и в конце не забудьте [включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C "Включить") `radvd.service`.

## Privacy Extensions

Когда устройство-клиент получает адрес посредством SLAAC, его IPv6-адрес вычисляется на основании префикса сети и MAC-адреса сетевого интерфейса. Это может иметь определённые последствия с точки зрения безопасности, поскольку MAC-адрес компьютера теперь можно узнать по IPv6-адресу. Для решения этой проблемы был разработан стандарт *IPv6 Privacy Extensions* ([RFC 4941](https://tools.ietf.org/html/rfc4941)). В соответствии с ним ядро видоизменяет исходный адрес, генерируя вместо него временный. Такой подход используется, когда необходимо скрыть настоящий адрес при подключении к удалённому серверу.

Чтобы включить Privacy Extensions, добавьте в файл `/etc/sysctl.d/40-ipv6.conf` следующие строки:

```
# Enable IPv6 Privacy Extensions
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
net.ipv6.conf.*nic0*.use_tempaddr = 2
...
net.ipv6.conf.*nicN*.use_tempaddr = 2

```

Здесь `nic0`...`nicN` — названия сетевых интерфейсов. В статье [Настройка сети#Обнаружение сетевых интерфейсов](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#Обнаружение_сетевых_интерфейсов "Настройка сети") описано, как узнать имена сетевых интерфейсов на вашей машине. Параметры `all.use_tempaddr` и `default.use_tempaddr` не будут применены к сетевым интерфейсам, которые уже определены в системе на момент выполнения файла настроек [sysctl](/index.php/Sysctl "Sysctl").

После перезагрузки Privacy Extensions будут включены.

### dhcpcd

Начиная с версии 6.4.0 в [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") добавлена опция `slaac private`, которая включает функцию присвоения стабильных приватных адресов вместо адресов, основанных на MAC-адресе интерфейса, в соответствии [RFC 7217](https://tools.ietf.org/html/rfc7217). Дополнительная настройка не требуется, если, конечно, вы не хотите изменять адрес IPv6 при каждом новом подключении к сети. Если назначить опцию `slaac hwaddr`, то адреса будут назначаться исходя из MAC-адреса интерфейса.

### NetworkManager

NetworkManager не учитывает указанные в файле `/etc/sysctl.d/40-ipv6.conf` настройки. Убедиться в этом можно выполнив `$ ip -6 addr show *имя_интерфейса*` после перезагрузки: отобразится только обычный адрес, не временный.

Чтобы включить IPv6 Privacy Extensions по умолчанию, добавьте следующие строки в файл `/etc/NetworkManager/NetworkManager.conf`:

```
*[connection]*
ipv6.ip6-privacy=2

```

Чтобы включить IPv6 Privacy Extensions для отдельных соединений под управлением NetworkManager, отредактируйте соответствующий нужному соединения файл в каталоге `/etc/NetworkManager/system-connections/`, добавив к разделу `[ipv6]` пару ключ-значение `ip6-privacy=2`:

```
[ipv6]
method=auto
ip6-privacy=2

```

**Примечание:** Может показаться, что временный адрес IPv6, созданный при включении Privacy Extensions, никогда не обновляется (он не переходит в статус `deprecated` после истечения времени жизни `valid_lft`). На самом деле это не совсем так: через больший промежуток времени адрес всё же изменится.

### systemd-networkd

Systemd-networkd тоже не учитывает настройки `net.ipv6.conf.xxx.use_tempaddr` в файле `/etc/sysctl.d/40-ipv6.conf`, если оцпия `IPv6PrivacyExtensions` в файле `.network` не установлена в значение `kernel`.

Тем не менее, учитываются некоторые другие опции:

```
net.ipv6.conf.xxx.temp_prefered_lft
net.ipv6.conf.xxx.temp_valid_lft

```

**Примечание:** `temp_prefered_lft` — корректное имя переменной, хотя допущена грамматическая ошибка (правильно preferred).

См. также [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") и [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).

### connman

Добавьте следующую строку в секцию global файла `/var/lib/connman/settings`:

```
[global]
IPv6.privacy=preferred

```

## Постоянный приватный адрес

Другой полезной возможностью являются описанные в [RFC 7217](https://tools.ietf.org/html/rfc7217) постоянные приватные IP-адреса (stable private addresses). Эта технология позволяет назначать интерфейсам постоянные адреса, для вычисления которых вместо MAC-адреса устройства используется специально сгенерированный ключ.

Чтобы заставить ядро сгенерировать ключ (например, для интерфейса `wlan0`), нужно назначить [параметр ядра](/index.php/%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80_%D1%8F%D0%B4%D1%80%D0%B0 "Параметр ядра"):

```
sysctl net.ipv6.conf.wlan0.addr_gen_mode=3

```

Выключив/включив интерфейс и выполнив `ip addr show dev wlan0` вы увидите пункт `stable-privacy` рядом с каждым адресом IPv6\. Ядро должно было создать 128-битный ключ для генерирования адресов этого интерфейса. Чтобы увидеть сам ключ, выполните команду `sysctl net.ipv6.conf.wlan0.stable_secret`. Чтобы ключ сохранялся после перезагрузок и был постоянным, нужно добавить в файл `/etc/sysctl.d/40-ipv6.conf` следующие строки:

```
# Enable IPv6 stable privacy mode
net.ipv6.conf.wlan0.stable_secret = *<ключ>*
net.ipv6.conf.wlan0.addr_gen_mode = 2

```

### NetworkManager

Описанные выше настройки не работают для [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)"), но он использует постоянные приватные адреса по умолчанию.

## Статический адрес

Иногда использование статического адреса может быть применено в качестве одной из мер обеспечения безопасности. Например, если ваш локальный маршрутизатор использует обнаружение соседей (Neighbor Discovery) или radvd ([RFC 2461](https://www.ietf.org/rfc/rfc2461.txt)), вашему интерфейсу будет автоматически присвоен адрес, который содержит часть MAC-адреса сетевого интерфейса (используя SLAAC). Это может быть не слишком хорошо для безопасности, так как позволяет без труда отслеживать систему даже если часть IPv6-адреса сменилась.

Чтобы присвоить статический IP-адрес при помощи [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)"), используйте шаблон профиля `/etc/netctl/examples/ethernet-static`. Следующие строки особенно важны:

```
# For IPv6 static address configuration
IP6=static
Address6=('1234:5678:9abc:def::1/64' '1234:3456::123/96')
Routes6=('abcd::1234')
Gateway6='1234:0:123::abcd'

```

**Примечание:** Если вы подключены к сети только посредстмов IPv6, то необходимо определить соответствующий DNS-сервер. Например:
```
DNS=('6666:6666::1' '6666:6666::2')

```
Если ваш провайдер не предоставляет DNS для IPv6 и вы не хотите настраивать свой сервер, то можно выбрать его по рекомендациям в статье [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution").

## IPv6 и PPPoE

Стандартный инструмент для [PPPoE](https://en.wikipedia.org/wiki/ru:PPPoE "wikipedia:ru:PPPoE"), `pppd`, позволяет использовать IPv6 в PPPoE, если это поддерживается вашим провайдером и модемом. Добавьте одну строку в файл `/etc/ppp/options`:

```
+ipv6

```

Если вы используете [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)") для PPPoE, тогда вместо этого добавьте следующую строку в файл настроек netctl:

```
PPPoEIP6=yes

```

## Делегирование префикса (DHCPv6-PD)

**Примечание:** В этом разделе рассматривается настройка пользовательского шлюза, а не клиентских машин. Для стандартных маршрутизаторов, доступных на рынке, рекомендуется предварительно изучить документацию по включению функции делегирования префикса.

Делегирование префикса (prefix delegation) — широко распространённая технология развёртывания IPv6, используемая многими интернет-провайдерами. Представляет собой метод назначения сетевого префикса пользователю (например, локальной сети). Маршрутизатор может быть настроен на привязку разных сетевых префиксов к различным подсетям. Провайдер выдаёт префикс с помощью DHCPv6 (обычно это префикс `/56` или `/64`), а dhcp-клиент присваивает префиксы локальным сетям. В случае простого шлюза с двумя интерфейсами клиент обычно получает адрес через WAN-интерфейс (или псевдоинтерфейс вроде ppp) и на его основании присваивает IPv6-префикс интерфейсу локальной сети.

### dibbler

[Dibbler](http://klub.com.pl/dhcpv6/) — портируемый клиент и сервер DHCPv6, который может использоваться для делегирования префикса. [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") его с пакетом [dibbler](https://aur.archlinux.org/packages/dibbler/).

Если вы используете `dibbler`, отредактируйте файл `/etc/dibbler/client.conf`:

```
log-mode short
log-level 7
# use the interface connected to your WAN
iface "WAN" {
  ia
  pd
}

```

**Совет:** См. также dibbler-client(8).

### dhcpcd

[dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") помимо поддержки dhcp для IPv4 также предлагает полноценную реализацию протокола DHCPv6 (включая DHCPv6-PD). Если вы используете `dhcpcd`, отредактируйте файл `/etc/dhcpcd.conf`. Скорее всего, вы уже используете dhcpcd для IPv4, поэтому просто обновите существующую конфигурацию.

```
duid
noipv6rs
waitip 6
# Uncomment this line if you are running dhcpcd for IPv6 only.
#ipv6only

# use the interface connected to WAN
interface WAN
ipv6rs
iaid 1
# use the interface connected to your LAN
ia_pd 1 LAN
#ia_pd 1/::/64 LAN/0/64

```

Эта конфигурация запросит префикс у WAN-интерфейса (`WAN`) и делегирует его внутреннему интерфейсу (`LAN`). Если вдруг с диапазоном `/64` возникнут проблемы, то нужно использовать вторую инструкцию `ia_pd`, которая в примере выше закомментирована. Кроме того, приведённая конфигурация также отключит вызовы маршрутизатора (router solicitation) для всех интерфейсов, кроме WAN.

**Совет:** См. также [dhcpcd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.8) и [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5).

### WIDE-DHCPv6

[WIDE-DHCPv6](http://wide-dhcpv6.sourceforge.net/) — свободная реализация протокола DHCP для IPv6 (DHCPv6), первоначально разработанная проектом KAME. [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") его с пакетом [wide-dhcpv6](https://aur.archlinux.org/packages/wide-dhcpv6/).

Если вы используете `wide-dhcpv6`, отредактируйте файл `/etc/wide-dhcpv6/dhcp6c.conf`, заменив `WAN` и `LAN` названиями соответвующих интерфейсов:

```
# use the interface connected to your WAN
interface WAN {
  send ia-pd 0;
};

id-assoc pd 0 {
  # use the interface connected to your LAN
  prefix-interface LAN {
    sla-id 1;
    sla-len 8;
  };
};

```

**Примечание:** Параметр `sla-len` нужно назначить таким образом, чтобы выполнялась формула `(WAN-prefix) + (sla-len) = 64`. В нашем случае для сети с префиксом `/56` формула примет вид 56+8=64\. Для префикса `/64` `sla-len` будет равен `0`.

Клиент wide-dhcpv6 можно [запустить](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C "Запустить")/[включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C "Включить") с помощью файла юнита systemd `dhcp6c@*interface*.service`, где `*interface*` — название интерфейса в файле настроек, т.е. например для интерфейса "WAN" используйте `dhcp6c@WAN.service`.

**Совет:** См. также dhcp6c(8) и dhcp6c.conf(5).

### systemd-networkd

 `/etc/systemd/network/lan.network` 
```
[Network]
Address=192.168.1.1
IPv6PrefixDelegation=dhcpv6
```
 `/etc/systemd/network/wan.network` 
```
[Network]
DHCP=yes
IPForward=yes
IPv6Token=::1
IPv6AcceptRouterAdvertisements=2
IPv6AcceptRA=yes
IPv6DuplicateAddressDetection=1
IPv6PrivacyExtensions=kernel
```

### Другие клиенты

[dhclient](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#DHCP "Network configuration (Русский)") также может запрашивать сетевой префикс, но для присваивания этого префикса или его части нужно использовать специальный скрипт. Пример программы: [https://github.com/jaymzh/v6-gw-scripts/blob/master/dhclient-ipv6](https://github.com/jaymzh/v6-gw-scripts/blob/master/dhclient-ipv6).

## Отключение IPv6

**Примечание:** Поддержка IPv6 встроена в ядро Arch Linux, поэтому отключить модуль просто добавив его в чёрный список не получится.

### Отключение функциональности

**Важно:** Отключение стека IPv6 может нарушить работу некоторых программ, которые ожидают, что он включён. [FS#46297](https://bugs.archlinux.org/task/46297)

Добавление опции `ipv6.disable=1` в параметрах ядра отключает весь стек IPv6, что в большинстве случаев помогает добиться желаемого результата. Смотрите статью [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") для получения дополнительной информации.

Добавив вместо этого `ipv6.disable_ipv6=1`, вы оставите стек IPv6 работающим, но адреса IPv6 не будут присваиваться сетевым интерфейсам.

Также вы можете отключить присвоение адреса IPv6 конкретным сетевым интерфейсам, добавив следующие строки в файл настроек [sysctl](/index.php/Sysctl "Sysctl") `/etc/sysctl.d/40-ipv6.conf`:

```
# Disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.*nic0*.disable_ipv6 = 1
...
net.ipv6.conf.*nicN*.disable_ipv6 = 1

```

Необходимо перечислить здесь все сетевые интерфейсы, для которых требуется отключение IPv6, так как опция `all.disable_ipv6` не будет применена к сетевым интерфейсам, которые уже включены на момент выполнения инструкций из файла настроек.

Обратите также внимание, что при отключении IPv6 таким образом, вы должны закомментировать все хосты IPv6 в вашем файле `/etc/hosts`:

```
#<ip-address> <hostname.domain.org> <hostname>
127.0.0.1 localhost.localdomain localhost
#::1 localhost.localdomain localhost

```

В противном случае могут появляться ошибки подключения, если при определении адреса произошло разрешение на адрес IPv6, который недоступен.

### Другие программы

Отключение IPv6 в ядре не предотвращает другие программы от попытки использования версии IPv6\. В большинстве случаев это не приводит к проблемам, однако, если они все-таки появляются, вам остается лишь искать в man-страницах или на просторах сети способ отключить эту функциональность.

#### dhcpcd

Например, *dhcpcd* будет продолжать пытаться запрашивать настройки сети у маршрутизаторов IPv6 (т.н. *Router solicitation*). Чтобы отключить это, добавьте следующие строки в файл `/etc/dhcpcd.conf`:

```
noipv6rs
noipv6

```

#### NetworkManager

Чтобы отключить IPv6 в NetworkManager, вызовите контекстное меню значка статуса сети и перейдите в *Edit Connections > Wired > Network name > Edit > IPv6 Settings > Method*, затем выберите *Method* как *Ignore/Disabled*.

#### ntpd

Чтобы определить, как systemd должен запускать службу ntpd, необходимо [внести изменения](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Drop-in_файлы "Systemd (Русский)") в файл `ntpd.service`.

Это создаст drop-in сниппет, который будет запускаться вместо стандартного `ntpd.service`. Флаг `-4` отключает использование IPv6 демоном ntp. Поместите следующее в drop-in сниппет:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -4 -g -u ntp:ntp

```

Здесь сначала очищается значение `ExecStart`, а затем устанавливается новая команда.

### systemd-networkd

networkd позволяет отключить IPv6 для отдельного интерфейса. Когда в разделе `[Network]` сетевого юнита указан параметр `LinkLocalAddressing=ipv4` или `LinkLocalAddressing=no`, networkd не будет настраивать IPv6 на соответствующих сетевых интерфейсах.

Следует однако отметить, что даже при использовании указанных выше опций networkd всё еще будет ожидать получения "объявлений маршрутизатора" (router advertisements, RA), если IPv6 не был отключён глобально для всей системы. Если трафик IPv6 не будет доходить до интерфейса (например, из-за настроек sysctl или ip6tables), то интерфейс останется в состоянии настройки и потенциально может стать причиной превышения времени ожидания (timeout) для служб, требующих полной настройки сети. Чтобы этого избежать, добавьте опцию `IPv6AcceptRA=no` в раздел `[Network]`.

## Использование IPv4 вместо IPv6

Раскомментируйте следующую строку в файле `/etc/gai.conf`:

```
#
#    For sites which prefer IPv4 connections change the last line to
#
precedence ::ffff:0:0/96  100

```

## Смотрите также

*   [IPv6](https://www.kernel.org/doc/Documentation/networking/ipv6.txt) — документация на kernel.org
*   [IPv6 temporary addresses](http://www.ipsidixit.net/2012/08/09/ipv6-temporary-addresses-and-privacy-extensions/) — временные адреса и расширения приватности
*   [IPv6 prefixes](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/x513.html) — о типах префиксов
*   [net.ipv6 options](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/proc-sys-net-ipv6..html) — настройка параметров ядра