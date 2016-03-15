*systemd-timesyncd* это служба, которая была добавлена для синхронизации системных часов по сети. Эта служба по сути реализует упрощенный клиент SNTP. В отличие сложных реализаций NTP, *systemd-timesyncd* представляет только клиентскую часть, ориентируясь на запрос времени из одного удаленного сервера и синхронизации локальных часов с ним. Подробнее смотрите [список рассылки systemd](http://lists.freedesktop.org/archives/systemd-devel/2014-May/019537.html) (англ.)

## Установка

Служба *systemd-timesyncd* доступна с [systemd](https://www.archlinux.org/packages/?name=systemd) >= 213\. Для ее [активации и запуска](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D1.8B_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_systemctl "Systemd (Русский)") выполните:

```
# timedatectl set-ntp true 

```

Чтобы узнать текущее состояние службы, выполните `timedatectl status`:

 `$ timedatectl status` 
```
      Local time: Sat 2015-11-14 22:20:38 MSK
  Universal time: Sat 2015-11-14 19:20:38 UTC
        RTC time: Sat 2015-11-14 19:20:38
       Time zone: Europe/Minsk (MSK, +0300)
 Network time on: yes
NTP synchronized: yes
 RTC in local TZ: no

```

**Совет:** До systemd 216 *systemd-timesyncd* требуется запущенный [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") (без дополнительной настройки) для уведомлений о статусе сетевых событий (up/down). Хоть он теперь получает события из [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") и [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)"), но все еще может потребоваться как зависимость от конфигурации сети или используемого инструмента управления сетью.

## Настройка

При запуске *systemd-timesyncd* будет читать файл конфигурации `/etc/systemd/timesyncd.conf`, который для [systemd](/index.php/Systemd "Systemd") 217 выглядит так:

 `/etc/systemd/timesyncd.conf` 
```
[Time]
#NTP=
#FallbackNTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
```

Чтобы добавить [сервера времени](/index.php/Network_Time_Protocol_daemon#Connection_to_NTP_servers "Network Time Protocol daemon") или изменить предложенные, необходимо раскомментировать соответствующую строку со списком их имен хостов или IP, разделяемых пробелами. Например, вы можете использовать любые серверы, предоставляемые [NTP pool project](http://www.pool.ntp.org/) или использовать [стандартные для Arch](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ntp&id=1b485f87c9e1384eaf069d031e415515e8ead92d) (также предусмотренные NTP pool project):

 `/etc/systemd/timesyncd.conf` 
```
[Time]
NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
FallbackNTP=0.pool.ntp.org 1.pool.ntp.org 0.fr.pool.ntp.org
```

Также NTP сервера могут быть предусмотрены в [systemd-networkd](/index.php/Systemd-networkd#.5BNetwork.5D_section "Systemd-networkd") конфигурации с опцией `NTP=` или динамически через DHCP сервер (с *systemd* 216).

Используемый сервер NTP будет определяться по следующим правилам:

*   Приоритетно - с любого интерфейса NTP серверов, полученных из конфигурации `systemd-networkd.service(8)` или через DHCP.
*   Сервера NTP, указанные в `/etc/systemd-timesyncd.conf` будут добавлены в список интерфейса после получения ответа от серверов в процессе соединения с ними.
*   Если после выполнения действий выше информация о серверах NTP не будет получена, то будет использоваться имя хоста и IP адреса, указанные в `FallbackNTP=`.

**Важно:** При каждой синхронизации служба перезаписывает файл /var/lib/systemd/clock, путь к которому на данный момент захардкоден и не может быть изменен. В связи с этим могут возникнуть проблемы, если корневой раздел работает в режиме "только для чтения" или при попытки минимизации операций записи.

## Смотрите также

*   [Форум: systemd-timesyncd не синхронизирует время](https://bbs.archlinux.org/viewtopic.php?id=182600)(англ.)
*   [Форум: Использование systemd-timesync вместо NTP](https://bbs.archlinux.org/viewtopic.php?id=182172)(англ.)