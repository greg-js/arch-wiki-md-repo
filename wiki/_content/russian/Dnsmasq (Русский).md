**Состояние перевода:** На этой странице представлен перевод статьи [dnsmasq](/index.php/Dnsmasq "Dnsmasq"). Дата последней синхронизации: 19 июля 2015‎‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Dnsmasq&diff=0&oldid=383170).

**dnsmasq** это DHCP и DNS сервера в одной программе. Она может быть использована для создания подключения к интернету с возможностью автоматической выдачи IP адреса и одновременным кэшированием соответствия доменов их IP адресам (DNS-кэширование). Это кэширование дает отличный прирост скорости работы с интернетом, т.к. не нужно постоянно обращаться за IP адресом к DNS-серверу - он держит эти параметры у себя в кэше. Dnsmasq легковесное приложение, разработанное для персонального использования, или как DHCP сервер для сети, в которой не более 50 компьютеров. Оно также отлично подойдет для развертывания [PXE](/index.php/PXE "PXE") сервера.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка кэша DNS](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D1.8D.D1.88.D0.B0_DNS)
    *   [2.1 Файл адресов DNS](#.D0.A4.D0.B0.D0.B9.D0.BB_.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.BE.D0.B2_DNS)
        *   [2.1.1 resolv.conf](#resolv.conf)
            *   [2.1.1.1 Больше трех серверов DNS](#.D0.91.D0.BE.D0.BB.D1.8C.D1.88.D0.B5_.D1.82.D1.80.D0.B5.D1.85_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.BE.D0.B2_DNS)
    *   [2.2 dhcpcd](#dhcpcd)
    *   [2.3 dhclient](#dhclient)
    *   [2.4 NetworkManager](#NetworkManager)
        *   [2.4.1 IPv6](#IPv6)
        *   [2.4.2 Другие методы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4.D1.8B)
*   [3 Установка сервера DHCP](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0_DHCP)
*   [4 Запуск в качестве службы](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
*   [5 Тестирование](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [5.1 Кэширования DNS](#.D0.9A.D1.8D.D1.88.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_DNS)
    *   [5.2 DHCP сервер](#DHCP_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
*   [6 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [6.1 Предотвращение перенаправления OpenDNS запросов Google](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.82.D0.B2.D1.80.D0.B0.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BD.D0.B0.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_OpenDNS_.D0.B7.D0.B0.D0.BF.D1.80.D0.BE.D1.81.D0.BE.D0.B2_Google)
    *   [6.2 Просмотр хостов-арендаторов](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D1.85.D0.BE.D1.81.D1.82.D0.BE.D0.B2-.D0.B0.D1.80.D0.B5.D0.BD.D0.B4.D0.B0.D1.82.D0.BE.D1.80.D0.BE.D0.B2)
    *   [6.3 Добавление пользовательского домена](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B4.D0.BE.D0.BC.D0.B5.D0.BD.D0.B0)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq)

## Настройка кэша DNS

Когда вы запускаете Dnsmasq как DHCP сервер, он также начинает прослушивать локальный интерфейс (localhost) на запросы DNS. Для запуска функции кэширования DNS отредактируйте `/etc/dnsmasq.conf`, добавив в него:

```
listen-address=127.0.0.1

```

Чтобы другие компьютеры локальной сети могли использовать этот сервер, можно позволить слушать локальный IP адрес:

```
listen-address=192.168.1.1    # Пример IP

```

В этом случае рекомендуется использовать статический IP адрес для локальной сети.

### Файл адресов DNS

После конфигурирования dnsmasq DHCP клиенту нужно будет дописать локальный адрес в вершину списка известных DNS адресов `/etc/resolv.conf`. Это обеспечит отправку всех запросов на dnsmasq прежде попыток разрешить их на внешнем DNS. После конфигурирования DHCP клиента сетевые демоны должны быть перезапущены чтобы изменения вступили в силу.

#### resolv.conf

Одним из вариантов может быть использование конфигурации `resolv.conf`. Для этого просто укажите localhost первой строчкой в `/etc/resolv.conf`:

 `/etc/resolv.conf` 

```
nameserver 127.0.0.1
# другие сервера DNS
...

```

Теперь все запросы DNS будут перенаправляться на обработку к dnsmasq. Внешние сервера будут использоваться только тогда, когда dnsmasq не удастся выполнить запрос. [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) может переписать стандартный `/etc/resolv.conf`. Если используется DHCP, то хорошей практикой будет защита `/etc/resolv.conf`. Для этого добавьте `nohook resolv.conf` в конфигурационный файл dhcpcd:

 `/etc/dhcpcd.conf` 

```
...
nohook resolv.conf
```

Кроме того, можно защитить resolv.conf, запретив любую его модификацию:

```
# chattr +i /etc/resolv.conf

```

##### Больше трех серверов DNS

В Linux имеется ограничение способности самостоятельной обрабатки DNS запросов, при котором можно использовать не более трех серверов DNS в `resolv.conf`. В качестве обходного пути можно указать только localhost в `resolv.conf`, а затем создать отдельный `resolv-file` для используемых внешних серверов DNS. Сначала создайте новый resolv файл для dnsmasq:

 `/etc/resolv.dnsmasq.conf` 

```
# например, DNS сервера от Google
nameserver 8.8.8.8
nameserver 8.8.4.4

```

Затем отредактируйте `/etc/dnsmasq.conf` для использования нового resolv файла:

 `/etc/dnsmasq.conf` 

```
...
resolv-file=/etc/resolv.dnsmasq.conf
...

```

### dhcpcd

[dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") может сам добавлять или удалять DNS сервера в `/etc/resolv.conf` создавая или изменяя `/etc/resolv.conf.head` и `/etc/resolv.conf.tail` файлы соответственно:

```
echo "nameserver 127.0.0.1" > /etc/resolv.conf.head

```

### dhclient

Для [dhclient](https://www.archlinux.org/packages/?name=dhclient) добавьте или раскомментируйте в `/etc/dhcp/dhclient.conf`:

```
prepend domain-name-servers 127.0.0.1;

```

### NetworkManager

[NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)") можно сконфигурировать так, чтобы он запускал _dnsmasq_. Добавьте опцию `dns=dnsmasq` в секцию `[main]` файла `NetworkManager.conf`, затем [выключите](/index.php/%D0%92%D1%8B%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Выключите") `dnsmasq.service`:

 `/etc/NetworkManager/NetworkManager.conf` 

```
[main]
plugins=keyfile
dns=dnsmasq

```

Собственные настройки _dnsmasq_ желательно хранить в `/etc/NetworkManager/dnsmasq.d/`. Например, чтобы изменить размер кэша DNS (который хранится в RAM):

 `/etc/NetworkManager/dnsmasq.d/cache`  `cache-size=1000` 

Когда _dnsmasq_ запускается `NetworkManager`, настройки в этом каталоге приоритетней стандартного файла конфигурации.

**Совет:** This method can allow you to enable custom DNS settings on particular domains. For instance: `server=/example1.com/exemple2.com/xx.xxx.xxx.x` change the first DNS address to `xx.xxx.xxx.xx` while browsing only the following websites `example1.com, example2.com`. This method is preferred to a global DNS configuration when using particular DNS nameservers which lack of speed, stability, privacy and security.

#### IPv6

Enabling `dnsmasq` in NetworkManager may break IPv6-only DNS lookups (i.e. `dig -6 [hostname]`) which would otherwise work. In order to resolve this, creating the following file will configure _dnsmasq_ to also listen to the IPv6 loopback:

 `/etc/NetworkManager/dnsmasq.d/ipv6_listen.conf`  `listen-address=::1` 

In addition, `dnsmasq` also does not prioritize upstream IPv6 DNS. Unfortunately NetworkManager does not do this ([Ubuntu Bug](https://bugs.launchpad.net/ubuntu/+source/network-manager/+bug/936712)). A workaround would be to disable IPv4 DNS in the NetworkManager config, assuming one exists

#### Другие методы

Другим вариантом является использование NetworkManager, настроенного вручную. Доступ к настройкам зависит от используемого фронтэнда; как правило, вызываемые по нажатию правой кнопки мыши апплета, редактирование (или создание) профиля, затем выбрав 'DHCP Автоматический' (указать адрес). Адреса DNS серверов должны быть введены так:

```
`127.0.0.1, DNS-server-one, ...`.

```

## Установка сервера DHCP

По умолчанию функционал DHCP сервера деактивирован. Чтобы его задействовать, измените (`/etc/dnsmasq.conf`). Наиболее важные параметры:

```
# Only listen to router LAN NIC, also opens up tcp/udp port 53 to localhost
# and udp port 67 to world:
interface=<LAN-NIC>

# dnsmasq will open tcp/udp port 53 and udp port 67 to world to help with
# dynamic interfaces (assigning dynamic ips). Dnsmasq will discard world
# requests to them, but the paranoid might like to close them and let the 
# kernel handle them:
bind-interfaces

# Задать динамический диапазон IP-адресов доступных для локальной сети ПК

dhcp-range=192.168.111.50,192.168.111.100,12h

# Если требуется выделить статический IP-адрес на основании NIC MAC-адреса компьютера локальной сети:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50

```

If you choose not to bind interfaces the domain port will need to be allowed in `/etc/hosts.allow`:

```
domain ALL : ALLOW

```

## Запуск в качестве службы

Для старта dnsmasq включите и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу

`# systemctl enable dnsmasq.service`

`# systemctl start dnsmasq.service`

Чтобы убедиться, что dnsmasq корректно запустился, проверьте системный журнал:

 `$ journalctl -u dnsmasq` 

Сеть также следует перезапустить, чтобы клиенты DHCP могли получить новый `/etc/resolv.conf`.

## Тестирование

### Кэширования DNS

Чтобы протестировать скорость ответа на запрос ресурса, к которому ещё не обращались через Dnsmasq (_dig_- утилита из пакета [bind-tools](https://www.archlinux.org/packages/?name=bind-tools)):

```
dig archlinux.org | grep "Query time"

```

При повторном запуске команды будет использоваться кэшированный DNS IP , что значительно ускорит обработку запроса, если Dnsmasq настроен правильно:

 `$ dig archlinux.org | grep "Query time"` 

```
;; Query time: 18 msec

```

 `$ dig archlinux.org | grep "Query time"` 

```
;; Query time: 2 msec

```

### DHCP сервер

Проверить можно на клиенте, находящимся в том же сегменте сети, в котором развернут сервер Dnsmasq.

## Советы и рекомендации

### Предотвращение перенаправления OpenDNS запросов Google

Чтобы предотвратить перенаправление OpenDNS запросов Google через Ваш сервер, добавте в `/etc/dnsmasq.conf`:

```
server=/www.google.com/<ISP DNS IP> //IP адрес сервера DNS провайдера

```

### Просмотр хостов-арендаторов

 `$ cat /var/lib/misc/dnsmasq.leases` 

### Добавление пользовательского домена

Можно добавить пользовательский домен к узлам в вашей (локальной) сети:

```
local=/home.lan/
domain=home.lan

```

что позволит пинговать хост/устройство (например указанное в вашем файле hosts ) как `hostname.home.lan`.

Раскомментируйте `expand-hosts` для авто-дополнения имен хостов, в которых не указан домен:

```
expand-hosts

```

Если эту функцию не использовать,то придется добавлять доменное имя к записям в /etc/hosts.