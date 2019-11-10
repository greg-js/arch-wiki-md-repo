Ссылки по теме

*   [GNUnet](/index.php/GNUnet "GNUnet")
*   [I2P (Русский)](/index.php/I2P_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I2P (Русский)")
*   [Freenet](/index.php/Freenet "Freenet")

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
*   [10 Pacman](#Pacman)
*   [11 Java](#Java)
*   [12 Запуск сервера Tor](#Запуск_сервера_Tor)
    *   [12.1 Настройка](#Настройка_2)
*   [13 TorDNS](#TorDNS)
*   [14 Torsocks](#Torsocks)
*   [15 "Торификация"](#"Торификация")
*   [16 Советы и рекомендации](#Советы_и_рекомендации)
*   [17 Решение проблем](#Решение_проблем)
    *   [17.1 Проблема с пользовательским значением](#Проблема_с_пользовательским_значением)
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

## Pacman

## Java

Чтобы заставить приложение Java проксировать все соединения через Tor, задайте следующую опцию командной строки:

```
export JAVA_OPTIONS="$JAVA_OPTIONS -DsocksProxyHost=localhost -DsocksProxyPort=9050"

```

## Запуск сервера Tor

### Настройка

Вы должны иметь скорость доступа в интернет не менее 20кб/с:

```
Nickname <tornickname>
ORPort 9001
BandwidthRate 20 KB            # Замедлить трафик до 20кб/с
BandwidthBurst 50 KB           # Но позволить всплески до 50кб/с

```

Allow irc ports 6660-6667 to exit from node:

```
ExitPolicy accept *:6660-6667,reject *:* # Разрешить IRC порты, но не более

```

Run Tor as an exit node:

```
ExitPolicy accept *:119        # Принимать nntp тажке как и политики выходных нод по умолчанию

```

Run Tor as middleman ( a relay):

```
ExitPolicy reject *:*

```

## TorDNS

Tor версий 0.2.x имеет встроенный механизм перенаправления DNS-запросов. Чтобы включить его, добавьте следующую строку в конфигурационный файл:

 `/etc/tor/torrc` 
```
 DNSPort 9053
 AutomapHostsOnResolve 1
 AutomapHostsSuffixes .exit,.onion

```

И перезапустите Tor, чтобы он подхватил новые настройки:

```
systemctl restart tor

```

Это позволит Tor принимать запросы (например слушать 9053 порт в этом примере) как обычному DNS-серверу, и разрешать домены по сети Tor. Недостатком является то, что становится возможным разрешать только A-записи; MX и NS запросы будут проигнорированы. См. [документацию для Debian](https://techstdout.boum.org/TorDns/).

DNS запросы могут быть осуществлены средствами коммандного интерпретатора, используя `tor-resolve`. For example:

```
$ tor-resolve archlinux.org
66.211.214.131

```

## Torsocks

## "Торификация"

"Торификация" (torify) позволяет использовать приложение через сеть Tor без каких либо дополнительных настроек в самом приложении. Выдержка из man page:

```
 torify - это простая оболочка, вызывающая tsocks с конфигурационным файлом

 tsocks представляет собой оболочку между библиотекой tsocks и приложением, которое вы хотите соксифицировать

```

Пример использования:

```
$ torify elinks checkip.dyndns.org
$ torify wget -qO- https://check.torproject.org/ | grep -i congratulations

```

Учтите, что torify не будет выполнять поиск DNS через Tordns. Для этого придётся использовать его в сочетании с `tor-resolve` (описано выше). В этом случае процедура для первого из приведенных примеров будет выглядеть следующим образом:

```
$ tor-resolve checkip.dyndns.org
208.78.69.70
$ torify elinks 208.78.69.70

```

## Советы и рекомендации

## Решение проблем

### Проблема с пользовательским значением

Если демон tor не запускается, выполните следующую комманду от root:

```
# tor

```

Если вы получили следующую ошибку:

```
May 23 00:27:24.624 [warn] Error setting groups to gid 43: "Operation not permitted".
May 23 00:27:24.624 [warn] If you set the "User" option, you must start Tor as root.
May 23 00:27:24.624 [warn] Failed to parse/validate config: Problem with User value. See logs for details.
May 23 00:27:24.624 [err] Reading config failed--see warnings above.

```

Она означает проблемы с пользовательскими значениями. Приступим к решению проблемы.

Узнайте права доступа к папке `/var/lib/tor`:

```
# ls -l /var/lib/

```

Если права `/var/lib/tor` такие же как указанные ниже, то это значит, что директория является собственностью пользователя *tor* группы *tor*.

```
drwx------ 2 tor    tor    4096 May 12 21:03 tor

```

Измените владельца и группу:

```
# chown -R root:root /var/lib/tor

```

Теперь права доступы должны быть такими:

```
drwx------ 2 root   root   4096 May 12 21:03 tor

```

Теперь откройте `/etc/tor/torrc` и найдите следующие строки:

```
## Uncomment this to start the process in the background... or use
## --runasdaemon 1 on the command line.
RunAsDaemon 1
User tor
Group tor

```

Закомментируйте строки *User tor* и *Group tor*:

```
## Uncomment this to start the process in the background... or use
## --runasdaemon 1 on the command line.
RunAsDaemon 1
#User tor
#Group tor

```

Сохраните и перезапустите демон **tor**. Теперь всё должно работать.

```
# systemctl restart tor

```

## Смотрите также

*   [Запуск клиента Tor на Linux/BSD/Unix](https://www.torproject.org/docs/tor-doc-unix.html.en)
*   [Список статей о Tor для Unix](https://trac.torproject.org/projects/tor/wiki#Unixish)
*   [Программы с интеграцией Tor](https://trac.torproject.org/projects/tor/wiki/doc/SupportPrograms)
*   [Как включить Tor *Hidden Service*](https://www.torproject.org/docs/tor-hidden-service.html.en)
*   [Pluggable Transports для обфускации трафика Tor](https://trac.torproject.org/projects/tor/wiki/doc/PluggableTransports)