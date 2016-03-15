[Point-to-Point Tunneling Protocol](https://en.wikipedia.org/wiki/ru:PPTP "wikipedia:ru:PPTP") (PPTP) — метод реализации виртуальной частной сети. PPTP использует канал контроля над туннелями TCP и GRE для инкапсуляции PPP-пакетов.

Далее будет показано, как создать сервер PPTP в Arch.

**Важно:** Протокол PPTP по своей сути небезопасен. Подробности смотрите на странице [http://poptop.sourceforge.net/dox/protocol-security.phtml](http://poptop.sourceforge.net/dox/protocol-security.phtml).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Настройка межсетевого экрана iptables](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BC.D0.B5.D0.B6.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_iptables)
    *   [2.2 Настройка межсетевого экрана UFW](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BC.D0.B5.D0.B6.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_UFW)
*   [3 Запуск сервера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Ошибка 619 на стороне клиента](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_619_.D0.BD.D0.B0_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.B5_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
    *   [4.2 pptpd[xxxxx]: Long config file line ignored](#pptpd.5Bxxxxx.5D:_Long_config_file_line_ignored)
    *   [4.3 ppp0: ppp: compressor dropped pkt](#ppp0:_ppp:_compressor_dropped_pkt)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [pptpd](https://www.archlinux.org/packages/?name=pptpd) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Настройка

**Совет:** Примеры файлов настроек доступны в каталоге `/usr/share/doc/pptpd`

Настройка производится в файле `/etc/pptpd.conf`. Пример:

 `/etc/pptpd.conf` 
```
# Обратитесь к man pptpd.conf для получения подробной информации о настройке

# Файл опций, который будет передан в pppd вместо стандартного /etc/ppp/options
# В данном примере: /etc/ppp/options.pptpd
option /etc/ppp/options.pptpd

# IP-адрес сервера в локальной сети (замените своим)
# В данном примере: 192.168.1.2
localip 192.168.1.2

# Диапазон адресов для клиентов PPTP-сервера (замените по своему усмотрению)
# В данном примере клиенты будут получать IP-адреса в диапазоне 192.168.1.234-238 и 192.168.1.245
remoteip 192.168.1.234-238,192.168.1.245

```

После чего создайте файл опций `/etc/ppp/options.pptpd`. Пример:

 `/etc/ppp/options.pptpd` 
```
# Обратитесь к man pppd чтобы увидеть полный список доступных опций и их описание.

name pptpd         # Название локальной системы для целей авторизации
refuse-pap         # Отказывать авторизацию пирам, использующим PAP
refuse-chap        # Отказывать авторизацию пирам, использующим CHAP
refuse-mschap      # Отказывать авторизацию пирам, использующим MS-CHAP
require-mschap-v2  # Требовать авторизацию с использованием MS-CHAPv2
require-mppe-128   # Требовать использование MPPE с 128-битным шифрованием
proxyarp           # Добавлять запись в системную таблицу ARP
lock               # Обеспечить блокирование для монопольного доступа к последовательному устройству
nobsdcomp          # Отключить сжатие BSD-Compress
novj               # Отключить сжатие Вана Якобсона для заголовков
novjccomp          # Отключить сжатие идентификатора соединения
nolog              # Отличить логирование в файл
ms-dns 8.8.8.8     # Указываем первичный адрес DNS-сервера для клиентов Microsoft Windows
ms-dns 8.8.4.4     # Указываем вторичный адрес DNS-сервера для клиентов Microsoft Windows

```

**Примечание:** Убедитесь, что в конце файла `/etc/ppp/options.pptpd` присутствует пустая строка, так как раннее замечались проблемы при запуске сервера из-за её отсутствия.

Далее вам необходимо создать пользователей для авторизации в файле `/etc/ppp/chap-secrets`:

 `/etc/ppp/chap-secrets` 
```
# <Имя> <Название сервера> <Пароль> <IP-адреса>
user2    pptpd    123    *

```

Теперь вы сможете авторизоваться, используя имя "user2" и пароль "123" под любым IP-адресом.

Далее необходимо включить форвардинг пакетов (это можно сделать несколькими способами, больше информации доступно на странице [Sysctl#Configuration](/index.php/Sysctl#Configuration "Sysctl")):

 `/etc/sysctl.d/99-sysctl.conf`  `net.ipv4.ip_forward=1` 

Теперь примените все изменения, сделанные в конфигурационных файлах sysctl:

```
# sysctl --system

```

### Настройка межсетевого экрана iptables

Ниже представлен пример конфигурации *iptables* для настройки межсетевого экрана.

```
# Пропускать все пакеты с интерфейсов ppp*, например ppp0
iptables -A INPUT -i ppp+ -j ACCEPT
iptables -A OUTPUT -o ppp+ -j ACCEPT

# Пропускать входящие соединения на порт 1723 (PPTP)
iptables -A INPUT -p tcp --dport 1723 -j ACCEPT

# Пропускать все пакеты GRE
iptables -A INPUT -p 47 -j ACCEPT
iptables -A OUTPUT -p 47 -j ACCEPT

# Включить форвардинг IP
iptables -F FORWARD
iptables -A FORWARD -j ACCEPT

# Включить NAT для интерфейсов eth0 и ppp*
iptables -A POSTROUTING -t nat -o eth0 -j MASQUERADE
iptables -A POSTROUTING -t nat -o ppp+ -j MASQUERADE

```

После чего сохраните новые правила iptables в файл командой:

```
# iptables-save > /etc/iptables/iptables.rules

```

Больше информации доступно на странице [Iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)").

### Настройка межсетевого экрана UFW

Настройте UFW так, чтобы предоставить доступ клиентам PPTP.

Вам необходимо изменить правило переадресации по умолчанию в файле `/etc/default/ufw`:

 `/etc/default/ufw`  `DEFAULT_FORWARD_POLICY="ACCEPT"` 

Теперь отредактируйте файл `/etc/ufw/before.rules`, добавив следующий код после заголовка и перед строкой *filter:

 `/etc/ufw/before.rules` 
```
# Правила для таблицы NAT
*nat
:POSTROUTING ACCEPT [0:0]

# Пропускать пакеты от клиентов на интерфейс eth0
-A POSTROUTING -s 172.16.36.0/24 -o eth0 -j MASQUERADE

# Коммит, чтобы изменения вступили в силу
COMMIT

```

Открываем PPTP порт 1723:

```
ufw allow 1723

```

Перезапустите ufw:

```
ufw disable
ufw enable

```

## Запуск сервера

Для запуска сервера PPTP, [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `pptpd.service`.

## Решение проблем

Информация о решении проблем со службами доступна на странице [Systemd (Русский)#Решение проблем](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC "Systemd (Русский)").

### Ошибка 619 на стороне клиента

Найдите и удалите (или закомментируйте) опцию `logwtmp` в файле `/etc/pptpd.conf`. С включенной опцией используется *wtmp* для записи лога подключений и отключений клиента.

### pptpd[xxxxx]: Long config file line ignored

Добавьте пустую строку в конец файла `/etc/pptpd.conf`.[[1]](http://sourceforge.net/p/poptop/bugs/35/)

### ppp0: ppp: compressor dropped pkt

Если при подключении клиента выводится это сообщение, добавьте скрипт `/etc/ppp/ip-up.d/mppefixmtu.sh` со следующим содержимым:

```
#!/bin/sh
CURRENT_MTU="`ip link show $1 | grep -Po '(?<=mtu )([0-9]+)'`"
FIXED_MTU="`expr $CURRENT_MTU + 4`"
ip link set $1 mtu $FIXED_MTU

```

После чего не забудьте сделать его исполняемым:

```
# chmod 755 /etc/ppp/ip-up.d/mppefixmtu.sh

```

Смотрите также отчет об ошибке: [http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=330973](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=330973).