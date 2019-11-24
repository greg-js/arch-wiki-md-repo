Ссылки по теме

*   [GNUnet](/index.php/GNUnet "GNUnet")
*   [I2P (Русский)](/index.php/I2P_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I2P (Русский)")
*   [Freenet](/index.php/Freenet "Freenet")

**Состояние перевода:** На этой странице представлен перевод статьи [Tor](/index.php/Tor "Tor"). Дата последней синхронизации: 17 ноября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Tor&diff=0&oldid=589195).

[Tor](https://www.torproject.org) — открытая реализация анонимной сети, основанная на [луковой маршрутизации](https://en.wikipedia.org/wiki/ru:%D0%9B%D1%83%D0%BA%D0%BE%D0%B2%D0%B0%D1%8F_%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F "wikipedia:ru:Луковая маршрутизация") 2-го поколения. Tor позволяет защититься от атак с использованием [анализа трафика](https://en.wikipedia.org/wiki/ru:HTTPS#.D0.90.D1.82.D0.B0.D0.BA.D0.B8_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_.D0.B0.D0.BD.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0_.D1.82.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.B0 "wikipedia:ru:HTTPS"), что даёт пользователю возможность сохранить [анонимность](https://en.wikipedia.org/wiki/ru:%D0%90%D0%BD%D0%BE%D0%BD%D0%B8%D0%BC%D0%BD%D0%BE%D1%81%D1%82%D1%8C#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82_.D0.B8_.D0.90.D0.BD.D0.BE.D0.BD.D0.B8.D0.BC.D0.BD.D0.BE.D1.81.D1.82.D1.8C "wikipedia:ru:Анонимность") в Интернете.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Введение](#Введение)
*   [2 Установка](#Установка)
*   [3 Настройка](#Настройка)
    *   [3.1 Настройка Tor Relay](#Настройка_Tor_Relay)
    *   [3.2 Tor ControlPort](#Tor_ControlPort)
        *   [3.2.1 Cookie-файл Tor Control](#Cookie-файл_Tor_Control)
        *   [3.2.2 Пароль Tor Control](#Пароль_Tor_Control)
        *   [3.2.3 Tor ControlSocket](#Tor_ControlSocket)
        *   [3.2.4 Проверка Tor Control](#Проверка_Tor_Control)
*   [4 Запуск Tor в Chroot](#Запуск_Tor_в_Chroot)
*   [5 Запуск Tor в контейнере systemd-nspawn](#Запуск_Tor_в_контейнере_systemd-nspawn)
    *   [5.1 Установка и настройка хоста](#Установка_и_настройка_хоста)
        *   [5.1.1 Виртуальный сетевой интерфейс](#Виртуальный_сетевой_интерфейс)
        *   [5.1.2 Запуск и включение systemd-nspawn](#Запуск_и_включение_systemd-nspawn)
    *   [5.2 Настройка контейнера](#Настройка_контейнера)
        *   [5.2.1 Запуск и включение systemd-networkd](#Запуск_и_включение_systemd-networkd)
    *   [5.3 Настройка Tor](#Настройка_Tor)
*   [6 Использование](#Использование)
*   [7 Веб-сёрфинг](#Веб-сёрфинг)
    *   [7.1 Firefox](#Firefox)
    *   [7.2 Chromium](#Chromium)
        *   [7.2.1 Отладка](#Отладка)
        *   [7.2.2 Расширения](#Расширения)
    *   [7.3 Luakit](#Luakit)
*   [8 Tor и HTTP прокси](#Tor_и_HTTP_прокси)
    *   [8.1 Firefox](#Firefox_2)
    *   [8.2 Polipo](#Polipo)
    *   [8.3 Privoxy](#Privoxy)
*   [9 Обмен мгновенными сообщениями](#Обмен_мгновенными_сообщениями)
    *   [9.1 Pidgin](#Pidgin)
    *   [9.2 Irssi](#Irssi)
*   [10 Pacman](#Pacman)
*   [11 Java](#Java)
*   [12 Запуск сервера Tor](#Запуск_сервера_Tor)
    *   [12.1 Мост](#Мост)
    *   [12.2 Передающий узел](#Передающий_узел)
    *   [12.3 Выходной узел](#Выходной_узел)
        *   [12.3.1 Пример настройки выходного узла](#Пример_настройки_выходного_узла)
            *   [12.3.1.1 Tor](#Tor)
                *   [12.3.1.1.1 Количество соединений](#Количество_соединений)
                *   [12.3.1.1.2 Привилегированные порты](#Привилегированные_порты)
                *   [12.3.1.1.3 Конфигурация](#Конфигурация)
            *   [12.3.1.2 nyx](#nyx)
            *   [12.3.1.3 iptables](#iptables)
            *   [12.3.1.4 Haveged](#Haveged)
            *   [12.3.1.5 pdnsd](#pdnsd)
                *   [12.3.1.5.1 Uncensored DNS](#Uncensored_DNS)
*   [13 TorDNS](#TorDNS)
    *   [13.1 Перенаправление DNS-запросов через TorDNS](#Перенаправление_DNS-запросов_через_TorDNS)
*   [14 Torsocks](#Torsocks)
*   [15 "Торификация"](#"Торификация")
*   [16 Советы и рекомендации](#Советы_и_рекомендации)
    *   [16.1 Возможности ядра](#Возможности_ядра)
*   [17 Решение проблем](#Решение_проблем)
    *   [17.1 Проблема с параметром User](#Проблема_с_параметром_User)
    *   [17.2 Проблемы с прокси tor-browser](#Проблемы_с_прокси_tor-browser)
*   [18 Смотрите также](#Смотрите_также)

## Введение

Для использования возможностей сети Tor пользователь должен запустить на своей машине "луковый" прокси-сервер (onion proxy), который займётся созданием виртуальных каналов через узлы сети. Полная секретность передачи информации между маршрутизаторами достигается за счёт многослойной криптографии — отсюда "луковые" аналогии. Кроме того, луковый прокси-сервер поддерживает [SOCKS](https://en.wikipedia.org/wiki/ru:SOCKS "wikipedia:ru:SOCKS")-интерфейс. Использующие SOCKS приложения могут работать через Tor, который выполняет [мультиплексирование](https://en.wikipedia.org/wiki/ru:%D0%9C%D1%83%D0%BB%D1%8C%D1%82%D0%B8%D0%BF%D0%BB%D0%B5%D0%BA%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5 "wikipedia:ru:Мультиплексирование") трафика на входе в виртуальный канал.

**Важно:** Сам по себе Tor не обеспечивает полную анонимность. Вопросы анонимности и безопасности подробно освещены [в FAQ](https://2019.www.torproject.org/docs/faq.html.en#anonsec) на сайте проекта.

Как описано выше, луковый прокси-сервер обрабатывает сетевой трафик с целью обеспечить анонимность пользователя. Трафик шифруется на входе в сеть, совершает несколько переходов между узлами Tor, после чего попадает на выходной узел сети, где дешифруется и отправляется целевому адресату. За анонимность приходится платить низкой скоростью обмена данными по сравнению с обычным соединением, поскольку выполняется большое количество перенаправлений трафика. Кроме того, хотя Tor предлагает защиту от анализа трафика, невозможно избежать подтверждения трафика на границах сети Tor (т.е. в точках входа и выхода из сети).

Подробную информацию о сети Tor можно найти в статье [Википедии](https://en.wikipedia.org/wiki/ru:Tor "wikipedia:ru:Tor").

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [tor](https://www.archlinux.org/packages/?name=tor).

Как правило, доступ к сети Tor осуществляется через Tor Browser, который можно установить в систему с пакетом [tor-browser](https://aur.archlinux.org/packages/tor-browser/) или использовать [исполняемый файл](https://www.torproject.org/projects/torbrowser.html.en) с сайта проекта.

Пакет [nyx](https://www.archlinux.org/packages/?name=nyx) (прежде носивший название *arm* — Anonymizing Relay Monitor) содержит консольный системный монитор, с помощью которого можно отслеживать использование пропускной способности, детали действующих соединений и т.п.

## Настройка

По умолчанию Tor использует файл конфигурации `/etc/tor/torrc`. Перечень доступных опций можно найти на странице руководства [tor(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tor.1) или в [документации](https://www.torproject.org/docs/tor-manual.html.en) проекта Tor. Базовый конфигурационный файл без дополнительных настроек вполне подойдет для большинства пользователей.

Имеется неколько потенциальных конфликтов настроек в файлах `torrc` и `tor.service`.

*   Если в разделе `[Service]` файла `tor.service` задано значение `Type=simple`, то в файле `torrc` нужно указать `RunAsDaemon=0` (значение по умолчаниию).
*   В файле `torrc` не должно быть задано значение `User`, кроме случая, когда в разделе `[Service]` файла `tor.service` задано значение `User=root`.

### Настройка Tor Relay

Максимальное количество дескрипторов файлов, одновременно открытых Tor, задаётся параметром `LimitNOFILE` в файле `tor.service`. Для быстрых ретрансляторов имеет смысл увеличить это значение.

Если на вашей системе не запущен веб-сервер и вы не задавали значение `AccountingMax` (определяет максимальный объём передаваемых данных), рассмотрите возможность установки параметра `ORPort` в значение `443` и/или `DirPort` в значение `80`. Многие пользователи Tor находятся за жёсткими межсетевыми экранами, которые разрешают им только веб-сёрфинг, и такая настройка позволит им использовать ваш ретранслятор. Если порты 80 и 443 уже заняты, то можно воспользоваться портами 22, 110 и 143\. Однако поскольку эти порты относятся к числу системных, то в этом случае Tor будет нужно запускать от пользователя root, задав параметры `User=root` и `User tor` в файлах `tor.service` и `torrc` соответственно.

Также будет полезно прочитать статью о [жизненном цикле](https://blog.torproject.org/blog/lifecycle-of-a-new-relay) ретрансляторов в документации Tor.

### Tor ControlPort

Как правило, особой необходимости открывать *ControlPort* не возникает, но некоторым программам это может потребоваться для получения низкоуровневого доступа к узлу.

Через открытый ControlPort внешние приложения смогут отслеживать состояние вашего узла, корректировать настройки, а также получать информацию о состоянии сети Tor и виртуальных каналов.

Добавьте следующую строку в файл `torrc`:

```
ControlPort 9051

```

Разумеется, доступ к ControlPort должен предоставляться только доверенным пользователям. Ограничение доступа осуществляется либо с помощью cookie-файла, либо паролем, либо обоими способами одновременно.

#### Cookie-файл Tor Control

Добавьте к файлу `torrc` следующие строки:

```
CookieAuthentication 1
CookieAuthFile /var/lib/tor/control_auth_cookie
CookieAuthFileGroupReadable 1
DataDirectoryGroupReadable 1

```

Доступ к ControlPort будет ограничен набором файловых разрешений cookie-файла и каталога data. Доступ к cookie-файлу Tor Control получат все пользователи группы `tor`.

Добавьте пользователя в группу `tor`:

```
# usermod -a -G tor *пользователь*

```

Перезагрузите настройки группы:

```
$ newgrp tor

```

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") Tor:

```
# systemctl restart tor

```

Теперь *пользователь* имеет доступ к файлу сookie. Команда

```
$ stat -c%a /var/lib/tor /var/lib/tor/control_auth_cookie

```

должна вывести значения `750` и `640`.

#### Пароль Tor Control

Преобразуйте пароль из представления в виде открытого текста в хэш:

```
# set +o history                          # отключить историю команд bash
# tor --hash-password *пароль*
# set -o history                          # включить историю команд bash

```

Добавьте этот хэш к файлу `torrc`:

```
HashedControlPassword *хэш*

```

Команда `set +o history` отключает сохранение истории в файл `$HISTFILE`, чтобы при выполнении команды `tor --hash-password` в нём не сохранилось значение пароля открытым текстом.

#### Tor ControlSocket

Tor ControlSocket имеет примерно то же назначение, что и [#Tor ControlPort](#Tor_ControlPort), с той лишь разницей, что прослушивается не TCP-сокет, а [сокет домена](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%BE%D0%BA%D0%B5%D1%82_%D0%B4%D0%BE%D0%BC%D0%B5%D0%BD%D0%B0_Unix "wikipedia:ru:Сокет домена Unix") Unix.

Если какой-то программе нужен доступ к Tor ControlSocket, добавьте следующие строки к файлу `torrc`:

```
ControlSocket /var/lib/tor/control_socket
ControlSocketsGroupWritable 1
DataDirectoryGroupReadable 1
CacheDirectoryGroupReadable 1             # обходное решение для бага #26913

```

Добавьте запускающего программу пользователя в группу `tor`:

```
# usermod -a -G tor *пользователь*

```

Перезагрузите настройки группы:

```
$ newgrp tor

```

Затем [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") Tor

```
# systemctl restart tor

```

и перезапустите программу.

Чтобы проверить состояние контрольного сокета, выполните

```
# stat -c%a /var/lib/tor /var/lib/tor/control_socket

```

Команда должна вывести значения `750` и `660`.

#### Проверка Tor Control

Чтобы проверить настройки ControlPort, используйте входящую в пакет [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) утилиту *nc*:

```
$ echo -e 'PROTOCOLINFO\r
' | nc 127.0.0.1 9051

```

Также запустите [socat](https://www.archlinux.org/packages/?name=socat):

```
$ echo -e 'PROTOCOLINFO\r
' | sudo -u *пользователь* socat - UNIX-CLIENT:/var/lib/tor/control_socket

```

Обе команды должны вывести

```
250-PROTOCOLINFO 1
250-AUTH METHODS=COOKIE,SAFECOOKIE,HASHEDPASSWORD COOKIEFILE="/var/lib/tor/control_auth_cookie"
250-VERSION Tor="0.3.4.8"
250 OK
514 Authentication required.

```

Дополнительную информацию можно найти в описании [протокола Tor Control](https://gitweb.torproject.org/torspec.git/tree/control-spec.txt).

## Запуск Tor в Chroot

**Важно:** Подключение по telnet на локальный ControlPort окажется невозможным, если Tor был запущен в chroot.

По соображениям безопасности желательно запускать Tor в [chroot](/index.php/Chroot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chroot (Русский)"). Следующий скрипт создаст подходящее окружение chroot в каталоге `/opt/torchroot`:

 `~/torchroot-setup.sh` 
```
#!/bin/bash
export TORCHROOT=/opt/torchroot

mkdir -p $TORCHROOT
mkdir -p $TORCHROOT/etc/tor
mkdir -p $TORCHROOT/dev
mkdir -p $TORCHROOT/usr/bin
mkdir -p $TORCHROOT/usr/lib
mkdir -p $TORCHROOT/usr/share/tor
mkdir -p $TORCHROOT/var/lib

ln -s /usr/lib  $TORCHROOT/lib
cp /etc/hosts           $TORCHROOT/etc/
cp /etc/host.conf       $TORCHROOT/etc/
cp /etc/localtime       $TORCHROOT/etc/
cp /etc/nsswitch.conf   $TORCHROOT/etc/
cp /etc/resolv.conf     $TORCHROOT/etc/
cp /etc/tor/torrc       $TORCHROOT/etc/tor/

cp /usr/bin/tor         $TORCHROOT/usr/bin/
cp /usr/share/tor/geoip* $TORCHROOT/usr/share/tor/
cp /lib/libnss* /lib/libnsl* /lib/ld-linux-*.so* /lib/libresolv* /lib/libgcc_s.so* $TORCHROOT/usr/lib/
cp $(ldd /usr/bin/tor | awk '{print $3}'|grep --color=never "^/") $TORCHROOT/usr/lib/
cp -r /var/lib/tor      $TORCHROOT/var/lib/
chown -R tor:tor $TORCHROOT/var/lib/tor

sh -c "grep --color=never ^tor /etc/passwd > $TORCHROOT/etc/passwd"
sh -c "grep --color=never ^tor /etc/group > $TORCHROOT/etc/group"

mknod -m 644 $TORCHROOT/dev/random c 1 8
mknod -m 644 $TORCHROOT/dev/urandom c 1 9
mknod -m 666 $TORCHROOT/dev/null c 1 3

if [[ "$(uname -m)" == "x86_64" ]]; then
  cp /usr/lib/ld-linux-x86-64.so* $TORCHROOT/usr/lib/.
  ln -sr /usr/lib64 $TORCHROOT/lib64
  ln -s $TORCHROOT/usr/lib ${TORCHROOT}/usr/lib64
fi

```

Выполнив скрипт от пользователя root, вы можете запустить Tor в окружении chroot командой:

```
# chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor

```

Или же, если вы используете systemd, то можете создать [drop-in файл](/index.php/Drop-in_%D1%84%D0%B0%D0%B9%D0%BB "Drop-in файл") для службы `tor.service`:

 `/etc/systemd/system/tor.service.d/chroot.conf` 
```
[Service]
User=root
ExecStart=
ExecStart=/usr/bin/sh -c "chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor -f /etc/tor/torrc"
KillSignal=SIGINT

```

## Запуск Tor в контейнере systemd-nspawn

В этом примере мы создадим контейнер systemd-nspawn с виртуальным сетевым macvlan-интерфейсом. Контейнер будет называться `tor-exit`.

В статьях [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") и [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") можно найти полную информацию о работе и настройке соответствующих программ.

### Установка и настройка хоста

Контейнер будет размещаться в каталоге `/srv/container`:

```
# mkdir -p /srv/container/tor-exit

```

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), чтобы получить доступ к утилите *pacstrap*.

С помощью *pacstrap* установите в каталог контейнера пакеты [base](https://www.archlinux.org/packages/?name=base), [tor](https://www.archlinux.org/packages/?name=tor) и [nyx](https://www.archlinux.org/packages/?name=nyx) (подробнее см. статью об [установке в контейнер](/index.php/Systemd-nspawn#Create_and_boot_a_minimal_Arch_Linux_distribution_in_a_container "Systemd-nspawn") минимального дистрибутива Arch Linux):

```
# pacstrap -сi /srv/container/tor-exit base tor nyx

```

Если зарегистрировать контейнер на хосте, то в дальнейшем с ним можно будет взаимодействовать извне с помощью команды `machinectl`. Для этого необходимо создать символическую ссылку на контейнер в каталоге `/var/lib/container/`. Создайте каталог, если он отсутствует:

```
# mkdir -p /var/lib/container

```

и поместите в него символическую ссылку на контейнер:

```
# ln -s /srv/container/tor-exit /var/lib/container/tor-exit

```

#### Виртуальный сетевой интерфейс

Создайте Dropin-каталог для службы контейнера:

```
# mkdir /etc/systemd/system/systemd-nspawn@tor-exit.service.d

```

и поместите в него [drop-in файл](/index.php/Drop-in_%D1%84%D0%B0%D0%B9%D0%BB "Drop-in файл") следующего содержания:

 `/etc/systemd/system/systemd-nspawn@tor-exit.service.d/tor-exit.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/systemd-nspawn --quiet --keep-unit --boot --link-journal=guest --network-macvlan=*интерфейс* --private-network --directory=/var/lib/container/%i
LimitNOFILE=32768

```

Опция `--network-macvlan=*интерфейс* --private-network` создаст для контейнера macvlan-интерфейс с названием `mv-*интерфейс*`, который не будет видим с хоста. Подробную информацию об опциях можно найти на странице справочного руководства [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1).

Строка `LimitNOFILE=32768` позволит открывать [больше файловых дескрипторов](#Увеличение_максимума_открытых_файловых_дескрипторов) одновременно.

Также необходимо сохранить сетевые настройки [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") в файле `/srv/container/tor-exit/etc/systemd/network/mv-*интерфейс*.network`.

#### Запуск и включение systemd-nspawn

[Запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `systemd-nspawn@tor-exit.service`.

### Настройка контейнера

Чтобы войти в контейнер, выполните (подробнее см. статью [Systemd-nspawn#machinectl](/index.php/Systemd-nspawn#machinectl "Systemd-nspawn")):

```
# machinectl login tor-exit

```

Если при попытке войти в контейнер как root появляется ошибка "[Login incorrect](/index.php/Systemd-nspawn#Root_login_fails "Systemd-nspawn")", выполните

```
# mv /srv/container/tor-exit/etc/securetty /srv/container/tor-exit/etc/securetty.bak

```

#### Запуск и включение systemd-networkd

[Запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `systemd-networkd.service`. Команда `networkctl` отобразит список сетевых интерфейсов контейнера, если `systemd-networkd` настроен корректно.

### Настройка Tor

Смотри раздел [#Запуск сервера Tor](#Запуск_сервера_Tor).

**Совет:** Файлы контейнера удобнее редактировать с хоста, вашим любимым редактором.

## Использование

[Запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `tor.service`. В качестве альтернативы можно запустить Tor командой `sudo -u tor /usr/bin/tor`.

Для использования программы через Tor настройте её на использование `127.0.0.1` или localhost в качестве SOCKS5H-прокси на порте 9050 (для Tor со стандартными настройками). Чтобы проверить работу Tor, посетите страницу [Tor](https://check.torproject.org/) или [Xenobite.eu](https://torcheck.xenobite.eu/).

## Веб-сёрфинг

В настоящее время The Tor Project поддерживает веб-сёрфинг исключительно через Tor Browser, который представляет собой пропатченую версию браузера Firefox ESR (extended support release). В [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") можно найти [различные версии](https://aur.archlinux.org/packages/?K=tor-browser) пакетов с Tor Browser. Также можно просматривать веб-страницы через Tor с помощью обычного [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)"), [Chromium](/index.php/Chromium "Chromium") и других браузеров.

**Важно:** The Tor Project настоятельно рекомендует использовать только Tor Browser, если вы хотите сохранить анонимность. [[1]](https://www.torproject.org/docs/faq.html.en#TBBOtherBrowser)

**Совет:** Чтобы подтвердить подпись исходного пакета Tor Browser Bundle при сборке, нужно импортировать [ключи Tor Project](https://www.torproject.org/docs/signing-keys.html.en), как описано в статье [GnuPG#Use a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG").

### Firefox

*Preferences > General > Network Settings > Settings...* , выберите пункт *Manual proxy configuration*, после чего укажите:

*   SOCKS Host — `localhost`;
*   Port — `9050`;
*   SOCKS v5 — для использования пятой версии протокола SOCKS;
*   Proxy DNS when using SOCKS v5 — чтобы перенаправить все DNS-запросы в сеть Tor.

### Chromium

Запустите Chromium:

```
$ chromium --proxy-server="socks5://*мой-прокси*:8080" --host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE *мой-прокси*"

```

Флаг `--proxy-server="socks5://*мой-прокси*:8080"` означает, что все `http://` и `https://` запросы будут посылаться через прокси-сервер `"*мой-прокси*:8080"` посредством протокола SOCKS пятой версии. Разрешение имён для этих запросов будет выполняться прокси-сервером, а не браузером локально.

**Важно:** Проксирование `ftp://` через SOCKS-прокси на данный момент не реализовано. [[2]](https://www.chromium.org/developers/design-documents/network-stack/socks-proxy)

Флаг `--proxy-server` влияет только на загрузку URL-страниц. Однако в Chromium есть и другие компоненты, которые могут попытаться выполнить DNS-разрешение напрямую. Наиболее важный их этих компонентов — *DNS-prefetcher*. Если DNS-prefetcher не отключён, то браузер будет посылать DNS-запросы напрямую, минуя SOCKS5-сервер. Prefetcher и другие компоненты можно отключить, но такой подход неудобен и ненадёжен, поскольку придётся отслеживать каждый элемент Chromium, который может захотеть посылать DNS-запросы самостоятельно.

Для комплексного решения этой проблемы используется флаг `--host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE *мой-прокси*"`, который представляет собой ловушку для посылаемых через обычную сеть DNS-запросов. Каждое выполяемое локально разрешение DNS теперь будет привязано к (нерабочему) адресу `~NOTFOUND` (можно представить его как адрес `0.0.0.0`). Указание `"EXCLUDE"` создаёт исключение для прокси-сервера `"*мой-прокси*"`, потому что без этого Chromium не сможет выполнять разрешение адреса самого прокси-сервера SOCKS и все запросы будут завершаться неудачей с ответом `PROXY_CONNECTION_FAILED`.

Также, чтобы предотвратить [утечки WebRTC](https://ipleak.net/#webrtcleak), можно установить расширение браузера [WebRTC Network Limiter](https://chrome.google.com/webstore/detail/webrtc-network-limiter/npeicpdbkakmehahjeeohfdhnlpdklia).

#### Отладка

В случае возникновения каких-либо проблем в первую очередь нужно проверить настройки прокси, введя адрес `chrome://net-internals/#proxy`.

Затем нужно изучить вкладку настроек DNS, чтобы убедиться, что Chromium не выполняет локальное разрешение DNS: `chrome://net-internals/#dns`.

#### Расширения

Как и для Firefox, вы можете установить удобный переключатель прокси вроде [Proxy SwitchySharp](https://chrome.google.com/webstore/detail/dpplabbmogkhghncfbfdeeokoefdjegm).

После установки перейдите на его панель настроек. Под вкладкой *Proxy Profiles* добавьте новый профиль *Tor*, уберите отметку с опции *Use the same proxy server for all protocols*, затем добавьте *localhost* в качестве хоста SOCKS, порт *9050*, и выберите *SOCKS v5*.

При желании можно включить опцию быстрого переключения на вкладке настроек *General*. Тогда переключаться между нормальной навигацией и сетью Tor можно будет одним кликом на иконке Proxy SwitchySharp.

### Luakit

**Важно:** Стороннему наблюдателю будет несложно вас опознать по редкой стороке `user-agent` в заголовке HTTP-запроса; также могут возникнуть проблемы с воспроизведением Flash, работой JavaScript и т.д.

Выполните:

```
$ torsocks luakit

```

## Tor и HTTP прокси

Tor может использовать HTTP-прокси вроде [Polipo](/index.php/Polipo "Polipo") или [Privoxy](/index.php/Privoxy "Privoxy"), однако разработчики Tor рекомендуют воспользоваться библиотекой SOCKS5, если ваш браузер её поддерживает.

### Firefox

Расширение браузера [FoxyProxy](https://addons.mozilla.org/en-us/firefox/addon/foxyproxy-standard/) позволяет назначить прокси-сервер как для всех HTTP-запросов в целом, так и для обращения по отдельным веб-адресам. После установки расширения перезапустите браузер и вручную настройте использование прокси по адресу `localhost:8118`, где должен работать [Polipo](/index.php/Polipo "Polipo") или [Privoxy](/index.php/Privoxy "Privoxy"). Эти настройки находятся в меню *Add > Standard proxy type*. Выберите метку прокси-сервера (например, `Tor`) и введите хост и порт в поля *HTTP Proxy* и *SSL Proxy*. Для проверки правильности работы Tor посетите страницу [Tor Check](https://check.torproject.org/).

### Polipo

Командой The Tor Project был создан стандартный [файл настроек](https://gitweb.torproject.org/torbrowser.git/plain/build-scripts/config/polipo.conf?id=1ffcd9dafb9dd76c3a29dd686e05a71a95599fb5) Polipo, чтобы избежать возможных проблем и обеспечить анонимность пользователей.

Обратите внимание, что если вы можете использовать SOCKS5-прокси, который Tor запускает автоматически на порте `9050`, то нет необходимости использовать Polipo. Если вы хотите использовать Chromium в связке с Tor, то Polipo тоже не требуется (см. [#Chromium](#Chromium)).

### Privoxy

Privoxy можно использовать для обмена сообщениями ([Jabber](/index.php/Jabber "Jabber"), [IRC](/index.php/IRC "IRC")) и других приложений. Приложения, которые поддерживают HTTP-прокси, можно подключить к Privoxy (например, на адрес `127.0.0.1:8118`). Чтобы использовать SOCKS-прокси, направьте ваше приложение в Tor (адрес `127.0.0.1:9050`). Следует иметь в виду, что приложение может самостоятельно выполнять DNS-разрешение, что приведет к утечке информации. В этом случае можно попробовать использовать SOCKS4A (например, с Privoxy).

## Обмен мгновенными сообщениями

Для использования мессенджера через Tor не нужен HTTP-прокси вроде [Polipo](/index.php/Polipo "Polipo")/[Privoxy](/index.php/Privoxy "Privoxy"). Мы используем напрямую демон Tor, по умолчанию прослушивающий порт 9050.

### Pidgin

[Pidgin](/index.php/Pidgin "Pidgin") можно настроить на работу через Tor глобально или для отдельных аккаунтов. Для глобальных настроек используйте пункт меню *Tools -> Preferences -> Proxy*. Чтобы настроить использование Tor для одного аккаунта, перейдите в *Accounts > Manage Accounts*, выберите нужный аккаунт, нажмите *Modify*, после чего на вкладке *Proxy* укажите следующие параметры:

```
Proxy type SOCKS5
Host 127.0.0.1
Port 9150

```

Заметьте, что [в 2013 году](https://trac.torproject.org/projects/tor/ticket/8135) значение Port для Tor Browser Bundle изменилось с 9050 на 9150\. Если вы получили ошибку *Connection refused*, попробуйте изменить номер порта на прежний.

### Irssi

Freenode рекомендует подключаться напрямую к `.onion`. Для этого также потребуется charybdis и механизм ircd-seven's SASL для идентификации сервером имён (nickserv) в процессе соединения; подробности можно найти в статье [Irssi#Authenticating with SASL](/index.php/Irssi#Authenticating_with_SASL "Irssi"). Запустите irssi:

```
$ torsocks irssi

```

Задайте ваши индентификационные данные для сервиса [nickserv](https://en.wikipedia.org/wiki/ru:IRC-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D1%8B "wikipedia:ru:IRC-сервисы"), которые будут считываться при создании соединения. Поддерживаются механизмы аутентификации ECDSA-NIST256P-CHALLENGE (см. [ecdsatool](https://github.com/atheme/ecdsatool/blob/master/cap_sasl.pl)) и PLAIN. DH-BLOWFISH больше [не поддерживается](https://freenode.net/sasl/sasl-irssi.shtml).

```
/sasl set *сеть* *имя-пользователя* *пароль* *механизм*

```

Отключите CTCP и DCC и задайте фальшивое имя хоста, чтобы чтобы скрыть настоящее [[3]](https://encrypteverything.ca/IRC_Anonymity_Guide):

```
/ignore * CTCPS
/ignore * DCC
/set hostname *фальшивый_хост*

```

Подключитесь к Freenode:

```
/connect -network *сеть* freenodeok2gncmy.onion

```

Дополнительную информацию можно найти в статьях [Accessing freenode Via Tor](https://freenode.net/kb/answer/chat#accessing-freenode-via-tor), [SASL README](http://freenode.net/sasl/README.txt) или [IRC/SILC Wiki article](https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO/IrcSilc).

## Pacman

Через сеть Tor можно выполнять загрузочные операции [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") — синхронизировать базы данных репозиториев, скачивать пакеты и открытые ключи.

Преимущества:

*   Если кто-то отслеживает Интернет-соединение вашей машины, то он не увидит выполняемые обновления. Соответственно, нельзя будет определить, какие пакеты установлены, какие из них устарели и как часто выполяется обновление. Но следует учитывать, что атакующий всё ещё может опознать используемое программное обеспечение и узнать его версию другими способами. Например, проанализировав исходящие пакеты вашего HTTP-сервера и просканировав его порт можно будет определить, что а) это работающий HTTP-сервер и б) его версию.
*   Если зеркало для скачивания находится не в onion-домене, то скомпроментированный выходной узел может обнаружить попытку обновления и решить атаковать вашу машину. Однако при этом атакующий скорее всего не будет знать, какую именно машину он атакует.
*   Атакующий может попытаться убедить вашу машину, что доступных обновлений нет, чтобы не позволить применить обновления безопасности. При обновлении через Tor сделать это будет крайне непросто, поскольку в анонимной сети почти невозможно определить конкретно вашу машину.

Недостатки:

*   Более длительное время обновления из-за высокого значения задержки и низкой пропускной способности сети Tor. Это может быть значительным недостатком с точки зрения безопасности, если обновление нужно выполнить как можно быстрее, особенно на машинах, непосредственно подключённых к сети Интернет. Например, если уязвимость серьёзная и её легко обнаружить и использовать, то злоумышленники часто стараются атаковать как можно больше уязвимых систем максимально быстро, чтобы успеть до применения обновлений безопасности.

Надёжность обновлений через Tor:

*   Не нужно использовать DNS.
*   Вы зависите от состояния сети Tor и особенно выходных узлов (например, они могут блокировать обновления).
*   Вы зависите от правильной работы демона Tor. Например, если на диске закончилось свободное место, то демон Tor может отказать работать. "Reserved blocks gid:" в ext4, квоты на использование дискового пространства и некоторые другие меры помогут решить эту проблему.
*   Если вы находитесь в стране, где Tor блокируется, или в которой почти или совсем нет пользователей Tor, то вам придётся использовать мост (Tor bridge).

Замечание по поводу gpg:

Pacman считает надёжными только те ключи, которые подписаны либо лично вами (делается командой `pacman-key --lsign-key`), либо тремя из пяти мастер-ключей Arch. Если вредоносная выходная нода попробует заменить пакет на другой, подписаный её ключом, pacman не позволит пользователю установить такой пакет.

**Важно:** Для других дистрибутивов на основе Arch, а также неофициальных репозиториев и AUR это утверждение может оказаться неверным.
 `/etc/pacman.conf` 
```
...
XferCommand = /usr/bin/curl --socks5-hostname localhost:9050 --continue-at - --fail --output %o %u
...

```

**Примечание:** Во время обработки сигнатур баз данных вы иногда можете получать ошибку 404\. Это зависит от [настроек pacman](/index.php/Pacman/Package_signing#Configuring_pacman "Pacman/Package signing") и как правило безвредно.

## Java

Чтобы заставить приложение Java [проксировать](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html) все соединения через Tor, задайте следующую опцию командной строки:

```
export JAVA_OPTIONS="$JAVA_OPTIONS -DsocksProxyHost=localhost -DsocksProxyPort=9050"

```

## Запуск сервера Tor

Сеть Tor существует благодаря пользователям, которые создают и обслуживают узлы сети, предлагая свою пропускную способность, и запускают onion-сервисы. Есть несколько способов внести свой вклад в работу сети.

### Мост

Мост (bridge) — передающий узел сети, адрес которого не содержится в открытом каталоге узлов Tor. По этой причине мост останется доступным для желающих подключиться к Tor, даже если правительство или интернет-провайдер блокирует все публичные передатчики.

Согласно [документации](https://2019.www.torproject.org/docs/bridges#RunningABridge), для работы моста в [файле настроек](https://2019.www.torproject.org/docs/faq.html.en#torrc) `torrc` должно быть только четыре следующие строки:

```
SocksPort 0
ORPort 443
BridgeRelay 1
Exitpolicy reject *:*

```

### Передающий узел

В режиме передатчика (relay) ваша машина будет работать в качестве входного (guard relay) или промежуточного (middle relay) узла сети. В отличие от моста, адрес передающей машины будет опубликован в каталоге узлов Tor. Задача передающего узла заключается в пересылке пакетов к другим передатчикам или выходным узлам, но не в сеть Интернет.

Файл настроек передающего узла с пропускной способностью не менее 20 Кбит/с должен выглядеть так:

```
Nickname *название-узла-Tor*
ORPort 9001                    # Этот TCP-порт должен быть открыт или проброшен в вашем сетевом экране
BandwidthRate 20 KB            # Ограничить скорость передачи величиной 20 Kбит/с
BandwidthBurst 50 KB           # Но разрешить пиковые значения до 50 Kбит/с

```

Укажите также следующую строку, чтобы запретить пересылку пакетов с вашего узла в обычную сеть:

```
ExitPolicy reject *:*

```

### Выходной узел

Чтобы запрос из сети Tor попал в обычную сеть Интернет, необходим т.н. "выходной узел сети" (exit relay). Здесь важно понимать, что кто бы ни посылал запрос, для получателя всё будет выглядеть так, будто отправителем является именно выходной узел. Поэтому запуск выходной ноды считается наиболее небезопасным с точки зрения законности. Если вы размышляете над запуском выходного узла, то стоит изучить [советы и рекомендации](https://blog.torproject.org/tips-running-exit-node) от создателей проекта, чтобы избежать возможных проблем в будущем.

В файле `torrc` можно настроить перечень разрешённых на выходном узле сервисов. Например, разрешить весь трафик:

```
ExitPolicy accept *:*

```

Разрешить только соединения через IRC-порты 6660-6667 и запретить всё остальное:

```
ExitPolicy accept *:6660-6667,reject *:*

```

По умолчанию Tor настроен блокировать определённые порты. В файле `torrc` можно внести корректировки в этот список:

```
ExitPolicy accept *:119

```

#### Пример настройки выходного узла

Ниже даны рекомендации по настройке быстрого (более 100 Мбит/с) выходного узла Tor, защищённого сетевым экраном [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)"), а также генератора случайных чисел [Haveged](/index.php/Haveged_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Haveged (Русский)") для увеличения энтропии системы, DNS-кэша [pdnsd](/index.php/Pdnsd "Pdnsd") и службы мониторинга **nyx**. Настоятельно рекомендуется *предварительно* изучить статью [о настройке выходного узла](https://community.torproject.org/relay/setup/exit/).

**Примечание:** В разделе [#Запуск Tor в контейнере systemd-nspawn](#Запуск_Tor_в_контейнере_systemd-nspawn) описана установка Tor в контейнер `systemd-nspawn`. [Haveged](/index.php/Haveged_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Haveged (Русский)") должен быть установлен на хосте контейнера.

##### Tor

###### Количество соединений

По умолчанию, Tor может обрабатывать до 8192 соединений одновременно. Можно увеличить это значение до 32768 [[4]](https://www.torproject.org/docs/faq.html.en#PackagedTor):

 `/etc/systemd/system/tor.service.d/increase-file-limits.conf` 
```
[Service]
LimitNOFILE=32768

```

Также нужно скорректировать системный параметр `nofile`:

 `/etc/security/limits.conf` 
```
...
tor     soft    nofile    32768
tor     hard    nofile    32768
@tor    soft    nofile    32768
@tor    hard    nofile    32768

```

Узнать текущее значение `nofile` можно командой `# sudo -u tor 'ulimit -Hn'` (или разбив её на две: `# sudo -u tor bash` и `# ulimit -Hn`).

###### Привилегированные порты

Чтобы разрешить Tor использовать привилегированные порты, службу `tor.service` нужно запускать от root. Не забудьте также добавить параметр `User tor` в файле `/etc/tor/torrc`, чтобы понизить привилегии после запуска.

 `/etc/systemd/system/tor.service.d/start-as-root.conf` 
```
[Service]
User=root

```

###### Конфигурация

Образец файла настроек выходного узла Tor:

 `/etc/tor/torrc` 
```
SocksPort 0                                       ## Обычный передатчик без использования локального прокси-сервера SOCKS

Log notice stdout                                 ## Стандартное поведение Tor

ControlPort 9051                                  ## Для соединения nyx
CookieAuthentication 1                            ## Для соединения nyx
DisableDebuggerAttachment 0                       ## Для соединения nyx

ORPort 443                                        ## Служба tor.service должна быть запущена от root

Address $IP                                       ## IP-адрес или FQDN
Nickname $NICKNAME                                ## Название узла

RelayBandwidthRate 500 Mbits                      ## bytes/KBytes/MBytes/GBytes/KBits/MBits/GBits
RelayBandwidthBurst 1000 MBits                    ## bytes/KBytes/MBytes/GBytes/KBits/MBits/GBits

ContactInfo $E-MAIL - $BTC-ADDRESS                ## Контактная информация

DirPort 80                                        ## Служба tor.service должна быть запущена от root
DirPortFrontPage /etc/tor/tor-exit-notice.html    ## Демонстрация веб-страницы на порте 80

MyFamily $($KEYID),$($KEYID)...                   ## Не забудьте знак $ перед keyid ;)

ExitPolicy reject XXX.XXX.XXX.XXX/XX:*            ## Заблокировать отдельный домен или IP-адрес в дополнение к стандартной политике

User tor                                          ## Изменяет пользователя на tor, если служба была запущена от root

### Производительность ###
AvoidDiskWrites 1                                 ## Уменьшение износа SSD
DisableAllSwap 1                                  ## Служба tor.service должна быть запущена от root
HardwareAccel 1                                   ## Использование аппаратной поддержки OpenSSL
NumCPUs 2                                         ## Запуск в двух потоках

```

Информацию об использованных здесь опциях можно найти в [руководстве Tor](https://www.torproject.org/docs/tor-manual.html.en).

Tor по умолчанию запускает SOCKS-прокси на порте 9050 — даже если вы не не говорили ему этого делать. Укажите параметр `SocksPort 0`, если планируете использовать Tor только в качестве передатчика без запуска работающих через прокси-сервер локальных приложений.

`Log notice stdout` перенаправляет логи в поток стандартного вывода stdout, что тоже является настройкой Tor по умолчанию.

`ControlPort 9051`, `CookieAuthentication 1` и `DisableDebuggerAttachment 0` позволит использовать [nyx](https://www.archlinux.org/packages/?name=nyx) для мониторинга.

`ORPort 443` и `DirPort 80` говорит Tor прослушивать порты 443 и 80, а `DirPortFrontPage` выводит [страницу приветствия](https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html) при установлении соединения на порте 80.

`ExitPolicy reject XXX.XXX.XXX.XXX/XX:*` позволяет заблокировать соединения с определённого адреса или домена; можно использовать для блокировки соседних с выходным узлом хостов, чтобы злоумышленник не смог воспользоваться ими для обхода правил сетевого экрана.

`AvoidDiskWrites 1` уменьшает количество записей на диск и износ SSD. `DisableAllSwap 1` заблокирует все текущие и будущие страницы памяти, чтобы её нельзя было выгрузить.

Если команда `grep aes /proc/cpuinfo` возвращает какой-то результат, то ваш CPU поддерживает AES-инструкции. Если соответствующий модуль был загружен (`lsmod | grep aes`), то параметр `HardwareAccel 1` включит встроенное аппаратное ускорение шифрования [[5]](http://www.torservers.net/wiki/setup/server#aes-ni_crypto_acceleration).

`ORPort 443`, `DirPort 80` и `DisableAllSwap 1` требуют запуска службы Tor от root, как описано в разделе [#Привилегированные порты](#Привилегированные_порты).

##### nyx

Если в файле `/etc/tor/torrc` указаны параметры `ControlPort 9051` и `CookieAuthentication 1`, то можно запустить [nyx](https://www.archlinux.org/packages/?name=nyx) командой `sudo -u tor nyx`.

Чтобы просматривать список соединений Tor с помощью [nyx](https://www.archlinux.org/packages/?name=nyx), нужно также указать параметр `DisableDebuggerAttachment 0`.

Чтобы запустить `nyx` от другого пользователя (не `tor`), изучите раздел [#Cookie-файл Tor Control](#Cookie-файл_Tor_Control).

##### iptables

Установите и изучите работу с [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)"). Вместо использования [экрана с контекстной фильтрацией](/index.php/Simple_stateful_firewall_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Simple stateful firewall (Русский)"), которому на выходном узле пришлось бы отслеживать тысячи соединений, мы настроим межсетевой экран без отслеживания контекста.

 `/etc/iptables/iptables.rules` 
```
*raw
-A PREROUTING -j NOTRACK
-A OUTPUT -j NOTRACK
COMMIT

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -p tcp ! --syn -j ACCEPT
-A INPUT -p udp -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -p tcp --dport 443 -j ACCEPT
-A INPUT -p tcp --dport 80 -j ACCEPT
-A INPUT -i lo -j ACCEPT
COMMIT

```

`-A PREROUTING -j NOTRACK` и `-A OUTPUT -j NOTRACK` отключит отслеживание соединений в таблице `raw`.

`:INPUT DROP [0:0]` — цель (target) цепочки `INPUT` по умолчанию; отбрасывает входящий трафик, который не был отдельно разрешён опцией `ACCEPT`.

`:FORWARD DROP [0:0]` — цель цепочки `FORWARD` по умолчанию; используется для обычных маршрутизаторов, но не подходит для "луковых".

`:OUTPUT ACCEPT [0:0]` — цель цепочки `OUTPUT` по умолчанию; разрешает все исходящие соединения.

`-A INPUT -p tcp ! --syn -j ACCEPT` разрешает уже установленные по перечисленным ниже правилам входящие TCP соединения, а также TCP соединения от выходного узла.

`-A INPUT -p udp -j ACCEPT` разрешает все входящие UDP соединения, т.к. мы не используем отслеживание соединений (connection tracking).

`-A INPUT -p icmp -j ACCEPT` разрешает [ICMP](https://en.wikipedia.org/wiki/ru:ICMP "wikipedia:ru:ICMP")-пакеты.

`-A INPUT -p tcp --dport 443 -j ACCEPT` разрешает входящие соединения на `ORPort`.

`-A INPUT -p tcp --dport 80 -j ACCEPT` разрешает входящие соединения на `DirPort`.

`-A INPUT -i lo -j ACCEPT` разрешает входящие соединения на петлевой интерфейс.

##### Haveged

В статье [Haveged](/index.php/Haveged_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Haveged (Русский)") описано, как определить, генерирует ли ваша система достаточно энтропии для управления большим количеством OpenSSL соединений; документация и советы: [[6]](http://www.issihosts.com/haveged/), [[7]](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged).

##### pdnsd

**Важно:** Предполагается, что у вас доверенный (не цензурируемый) DNS-сервер.

Вы можете использовать [pdnsd](/index.php/Pdnsd "Pdnsd") для локального кэширования DNS-запросов, тогда выходной узел сможет быстрее выполнять разрешение и посылать меньшее количество запросов внешнему DNS-серверу.

 `/etc/pdnsd.conf` 
```
...
perm_cache=102400                       ## (Значение по умолчанию)*100 = 1 Мбайт * 100 = 100 Мбайт
...
server {
    label= "resolvconf";
    file = "/etc/pdnsd-resolv.conf";    ## Чтобы не использовать файл /etc/resolv.conf
    timeout=4;                          ## Период ожидания ответа сервера; может быть значительно меньше, чем глобальное время ожидания
    uptest=query;                       ## Проверять доступность сервера, посылая пустые DNS-запросы
    query_test_name=".";                ## Используется, если удалённый сервер игнорирует пустые запросы
    interval=10m;                       ## Выполнять тестирование каждые 10 минут
    purge_cache=off;                    ## Игнорировать парамет TTL
    edns_query=yes;                     ## Использовать EDNS для исходящих запросов, чтобы разрешить UDP-сообщения длиннее 512 байт; может вызвать проблемы на некоторых устаревших системах
    preset=off;                         ## Перед проверкой состояния сервера предполагать, что он выключен
 }
...

```

Такая настройка позволит кэшировать локально до 100 Мбайт DNS-запросов.

###### Uncensored DNS

Если ваш обычный DNS-сервер каким-то образом цензурируется или работает нестабильно, в статье [Alternative DNS services](/index.php/Alternative_DNS_services "Alternative DNS services") описаны альтернативные сервера; добавьте нужное в отдельный server-разделе файла `/etc/pdnsd.conf` (см. [Pdnsd#DNS servers](/index.php/Pdnsd#DNS_servers "Pdnsd")).

## TorDNS

Начиная с версий 0.2.x в Tor появился механизм перенаправления DNS-запросов. Чтобы его включить, добавьте строки ниже в файл настроек и [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") демон Tor:

 `/etc/tor/torrc` 
```
DNSPort 9053
AutomapHostsOnResolve 1
AutomapHostsSuffixes .exit,.onion

```

Теперь Tor будет принимать запросы на порт 9053 как обычный DNS-сервер и выполнять разрешение доменов через сеть Tor. К сожалению, через Tor выполняется разрешение только A-записей; MX и NS запросы будут проигнорированы. Дополнительную информацию можно найти в [документации TorDNS](https://techstdout.boum.org/TorDns/) для Debian.

Кроме того, появилась возможность посылать DNS-запросы посредством командного интерпретатора, командой `tor-resolve`. Например:

```
$ tor-resolve archlinux.org
66.211.214.131

```

### Перенаправление DNS-запросов через TorDNS

Вашу систему можно настроить посылать *все* запросы через TorDNS вне зависимости от того, используется ли Tor для соединения с конечной целью. Для этого настройте систему использовать адрес `127.0.0.1` в качестве DNS-сервера и отредактируйте строку `DNSPort` в файле `/etc/tor/torrc`:

```
DNSPort 53

```

Альтернативное решение — использовать локальный кэширующий DNS-сервер, вроде [dnsmasq](/index.php/Dnsmasq "Dnsmasq") или [pdnsd](/index.php/Pdnsd "Pdnsd"). Кэш DNS позволит несколько компенсировать низкую скорость TorDNS по сравнению с обычными DNS-серверами. Далее приведены инструкции по настройке *dnsmasq*.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) и укажите Tor прослушивать DNS запросы на порте 9053.

Задайте следующую конфигурацию dnsmasq:

 `/etc/dnsmasq.conf` 
```
no-resolv
port=53
server=127.0.0.1#9053
listen-address=127.0.0.1

```

Теперь dnsmasq будет ожидать локальных запросов и использовать TorDNS в качестве посредника. Отредактируйте файл `/etc/resolv.conf`, чтобы система опрашивала только сервер dnsmasq:

 `/etc/resolv.conf` 
```
nameserver 127.0.0.1

```

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") демон dnsmasq.

Наконец, если вы используете [dhcpcd](/index.php/Dhcpcd "Dhcpcd"), укажите ему не изменять настройки в файле `resolv.conf`:

 `/etc/dhcpcd.conf` 
```
nohook resolv.conf

```

Если строка `nohook` уже есть, то добавьте **resolv.conf** через запятую.

## Torsocks

[torsocks](https://www.archlinux.org/packages/?name=torsocks) позволяет заставить приложение работать через сеть Tor без необходимости корректировать настройки самого приложения. Выдержка из руководства:

*torsocks — обёртка между библиотекой torsocks и приложением с целью сделать каждое Интернет-соединение проходящим через сеть Tor.*

Примеры использования:

```
$ torsocks elinks checkip.dyndns.org
$ torsocks wget -qO- [https://check.torproject.org/](https://check.torproject.org/) | grep -i congratulations

```

## "Торификация"

В некоторых случаях более безопасно (и часто проще) выполнить сквозную "торифицикацию" всей системы вместо настройки отдельных приложений на использование SOCKS-порта Tor и отслеживания утечек DNS. Для полной торификации сетевой экран [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") настраивают на пересылку всех исходящих пакетов (помимо собственно трафика Tor) на *TransPort*. В этом случае приложения не нужно настраивать для работы через Tor, хотя работа через *SocksPort* всё ещё возможна. Торификация также работает и для DNS (*DNSPort*), но при этом нужно учитывать, что Tor поддерживает только протокол TCP, и, за исключением DNS-запросов, UDP-пакеты через Tor посылаться не могут. Следовательно, они должны блокироваться для предотвращения утечек.

Торификация через iptables даёт сравнительно надёжную защиту, но она не является полноценной заменой приложениям виртуализированной торификации вроде Whonix или TorVM [[8]](https://www.whonix.org/wiki/Comparison_with_Others). Торификация также не позволяет скрыть отпечаток браузера (fingerprint), поэтому рекомендуется использовать её вместе с Tor Browser (в AUR можно выбрать [подходящую версию](https://aur.archlinux.org/packages/?K=tor-browser)) или же воспользоваться "амнезийным" решением вроде [Tails](http://tails.boum.org/). Приложения всё ещё могут узнать имя хоста, MAC-адрес, серийный номер, временную зону вашего компьютера и другие данные, а с root-привилегиями смогут даже отключить сетевой экран целиком. Другими словами, полная торификация через iptables защищает от случайных соединений и DNS-утечек неправильно настроенного программного обеспечения, но не от вредоносных программ или ПО с серьёзными уязвимостями.

Ниже приведён файл настроек для утилит `iptables-restore` и `ip6tables-restore` (используются [службами](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") `iptables.service` и `ip6tables.service` соответственно).

**Примечание:** Правила в таблице nat принудительно перенаправляют исходящие соединения на TransPort или DNSPort, и блокируют всё, что торифицировать не удаётся.

*   Флагами `--ipv6` и `--ipv4` задаются правила для конкретных версий протокола [IP](https://en.wikipedia.org/wiki/ru:IP "wikipedia:ru:IP"). Таким образом, утилиты `iptables-restore` и `ip6tables-restore` могут использовать один и тот же файл настроек.
*   В случае явного указания флага `--ipv6` или `--ipv4`, утилита `ip*tables-restore` будет игнорировать правило, если оно установлено для другой версии протокола.
*   `ip6tables` не поддерживает флаг `--reject-with`.

Убедитесь, что в файле `torrc` есть следующие строки:

```
SocksPort 9050
DNSPort 5353
TransPort 9040

```

Подробнее смотрите руководство [iptables(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8).

**Примечание:** Если вы получили ошибку `iptables-restore: unable to initialize table 'nat'`, то нужно загрузить некоторые модули ядра:
```
# modprobe ip_tables iptable_nat ip_conntrack iptable-filter ipt_state

```

 `/etc/iptables/iptables.rules` 
```
*nat
:PREROUTING ACCEPT [6:2126]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [17:6239]
:POSTROUTING ACCEPT [6:408]

-A PREROUTING ! -i lo -p udp -m udp --dport 53 -j REDIRECT --to-ports 5353
-A PREROUTING ! -i lo -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j REDIRECT --to-ports 9040
-A OUTPUT -o lo -j RETURN
--ipv4 -A OUTPUT -d 192.168.0.0/16 -j RETURN
-A OUTPUT -m owner --uid-owner "tor" -j RETURN
-A OUTPUT -p udp -m udp --dport 53 -j REDIRECT --to-ports 5353
-A OUTPUT -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j REDIRECT --to-ports 9040
COMMIT

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT DROP [0:0]

-A INPUT -i lo -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
--ipv4 -A INPUT -p tcp -j REJECT --reject-with tcp-reset
--ipv4 -A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
--ipv4 -A INPUT -j REJECT --reject-with icmp-proto-unreachable
--ipv6 -A INPUT -j REJECT
--ipv4 -A OUTPUT -d 127.0.0.0/8 -j ACCEPT
--ipv4 -A OUTPUT -d 192.168.0.0/16 -j ACCEPT
--ipv6 -A OUTPUT -d ::1/8 -j ACCEPT
-A OUTPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -m owner --uid-owner "tor" -j ACCEPT
--ipv4 -A OUTPUT -j REJECT --reject-with icmp-port-unreachable
--ipv6 -A OUTPUT -j REJECT
COMMIT

```

Данный файл также подходит для утилиты `ip6tables-restore`. Создайте символическую ссылку на него:

```
# ln -s /etc/iptables/iptables.rules /etc/iptables/ip6tables.rules

```

Убедитесь, что Tor работает, и [запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службы `iptables` и `ip6tables`.

При необходимости можно [добавить указания](/index.php/%D0%9E%D1%82%D1%80%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5 "Отредактируйте") `Requires=iptables.service` и `Requires=ip6tables.service` к любому юниту systemd, чтобы выбранный процесс запускался строго после включения межсетевого экрана.

## Советы и рекомендации

### Возможности ядра

Если необходимо запустить Tor от обычного пользователя, и в то же время использовать порты меньше 1024, то можно воспользоваться функциональностью ядра для выдачи процессу `/usr/bin/tor` разрешения выполнять привязку привилегированных портов:

```
# setcap CAP_NET_BIND_SERVICE=+eip /usr/bin/tor

```

**Примечание:** После обновления пакета Tor эти разрешения сбросятся. Создайте [хук](/index.php/Pacman#Hooks "Pacman") для автоматической выдачи разрешений после обновлений.

Если вы используете службу systemd, то выдать Tor соответствующие разрешения можно также через настройки системного демона. Это удобно тем, что разрешения не нужно возобновлять после каждого обновления Tor:

 `/etc/systemd/system/tor.service.d/netcap.conf` 
```
[Service]
CapabilityBoundingSet=
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
AmbientCapabilities=
AmbientCapabilities=CAP_NET_BIND_SERVICE

```

Подробности можно найти на странице [superuser.com](https://superuser.com/questions/710253/allow-non-root-process-to-bind-to-port-80-and-443).

## Решение проблем

### Проблема с параметром User

Если не удалось запустить демон Tor, выполните следующую команду от root (или воспользуйтесь утилитой [sudo](/index.php/Sudo "Sudo")):

```
# tor

```

Ошибка

```
May 23 00:27:24.624 [warn] Error setting groups to gid 43: "Operation not permitted".
May 23 00:27:24.624 [warn] If you set the "User" option, you must start Tor as root.
May 23 00:27:24.624 [warn] Failed to parse/validate config: Problem with User value. See logs for details.
May 23 00:27:24.624 [err] Reading config failed--see warnings above.

```

означает проблемы с параметром User. Скорее всего, один или несколько файлов/каталогов в каталоге `/var/lib/tor` не принадлежат пользователю `tor`. Это можно определить с помощью команды *find*:

```
find /var/lib/tor/ ! -user tor

```

Для всех выведенных файлов и каталогов нужно поменять параметр владельца. Можно сделать это индивидуально для каждого файла

```
# chown tor:tor /var/lib/tor/*файл*

```

или отредактировать все сразу командой

```
# chown -R -v tor:tor /var/lib/tor

```

Теперь Tor должен запуститься без проблем.

Если запустить службу всё же не удаётся, запустите её от root. Измените имя пользователя в файле `/etc/tor/torrc`:

```
User tor

```

Затем отредактируйте файл службы systemd `/usr/lib/systemd/system/tor.service`:

```
[Service]
User=root
Group=root
Type=simple

```

В дальнейшем процесс будет запускаться от пользователя `tor`, поэтому измените UID и GID файлов на `tor` и добавьте разрешение на запись:

```
# chown -R tor:tor /var/lib/tor/
# chmod -R 700 /var/lib/tor

```

Сохраните изменения:

```
# systemctl --system daemon-reload

```

Наконец, [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `tor.service`.

### Проблемы с прокси tor-browser

[tor-browser](https://aur.archlinux.org/packages/tor-browser/) обычно нормально работает без дополнительных настроек. Если установленный/настроенный прокси выдаёт ошибку `proxy server is refusing connections` при любой попытке установить соединение, попробуйте сбросить настройки, переместив или удалив каталог `~/.tor-browser`.

## Смотрите также

*   [Запуск клиента Tor на Linux/BSD/Unix](https://www.torproject.org/docs/tor-doc-unix.html.en)
*   [Список статей о Tor для Unix](https://trac.torproject.org/projects/tor/wiki#Unixish)
*   [Программы с интеграцией Tor](https://trac.torproject.org/projects/tor/wiki/doc/SupportPrograms)
*   [Как включить Tor *Hidden Service*](https://www.torproject.org/docs/tor-hidden-service.html.en)
*   [Pluggable Transports для обфускации трафика Tor](https://trac.torproject.org/projects/tor/wiki/doc/PluggableTransports)