**ppp** (*Paul's PPP Package*) — пакет с открытым исходным кодом, который реализует [протокол соединения точка-точка](https://en.wikipedia.org/wiki/ru:PPP_(%D1%81%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB) (PPP) для систем Linux и Solaris. Пакет предоставляет демон *pppd*, который может быть использован вместе с [xl2tpd](https://www.archlinux.org/packages/?name=xl2tpd), [pptpd](https://www.archlinux.org/packages/?name=pptpd) и [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)").

Протоколы [3G](https://en.wikipedia.org/wiki/ru:3G "wikipedia:ru:3G"), [L2TP](https://en.wikipedia.org/wiki/ru:L2TP "wikipedia:ru:L2TP") и [PPPoE](https://en.wikipedia.org/wiki/ru:PPPoE "wikipedia:ru:PPPoE") работают на основе PPP, поэтому они также могут контролироваться ppp.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 PPPoE](#PPPoE)
    *   [2.2 Запуск pppd при старте системы](#Запуск_pppd_при_старте_системы)
*   [3 Дополнительно](#Дополнительно)
    *   [3.1 Автодозвон](#Автодозвон)
    *   [3.2 Автоматический разрыв соединения](#Автоматический_разрыв_соединения)
        *   [3.2.1 Используя cron](#Используя_cron)
        *   [3.2.2 Используя таймер systemd](#Используя_таймер_systemd)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Маршрут по умолчанию](#Маршрут_по_умолчанию)
    *   [4.2 Маскарадинг работает, но некоторые сайты не открываются](#Маскарадинг_работает,_но_некоторые_сайты_не_открываются)
    *   [4.3 Не удается загрузить модуль ядра ppp_generic](#Не_удается_загрузить_модуль_ядра_ppp_generic)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [ppp](https://www.archlinux.org/packages/?name=ppp), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Убедитесь, что ядро вашей системы скомпилировано с поддержкой PPPoE (верно для стандартной сборки):

 `$ zgrep CONFIG_PPPOE /proc/config.gz`  `CONFIG_PPPOE=m` 

## Настройка

### PPPoE

Создайте файл настроек соединения:

 `/etc/ppp/peers/*имя_соединения*` 
```
plugin rp-pppoe.so
# rp_pppoe_ac 'имя концентратора доступа'
# rp_pppoe_service 'имя службы PPPoE'

# сетевой интерфейс
eth0
# ваш логин
name "*имя_пользователя*"
usepeerdns
persist
# раскомментируйте, если вам нужен автодозвон "по требованию"
#demand
#idle 180
defaultroute
hide-password
noauth
```

Если задана опция `usepeerdns`, при соединении *pppd* создаст файл `/etc/ppp/resolv.conf` с полученными адресами DNS-серверов. По умолчанию скрипт `/etc/ppp/ip-up.d/00_dns` перемещает этот файл в `/etc/resolv.conf`, чтобы система могла использовать эти DNS-серверы. Если это поведение является нежелательным (например, установлен локальный кэширующий DNS), отредактируйте `/etc/ppp/ip-up.d/00_dns.sh` под ваши нужды.

Добавьте запись с паролем соединения в `/etc/ppp/pap-secrets` или `/etc/ppp/chap-secrets`, в зависимости от типа аутентификации, используемого вашим провайдером. Если вы не уверены, можно добавить запись в оба файла, *pppd* выберет нужный самостоятельно. Запись выглядит следующим образом:

```
*имя_пользователя* * *пароль*

```

Имя пользователя должно совпадать с именем, указанным в опции `name`. Оно также используется для аутентификации, если не переопределено другим значением с помощью опции `user`.

Теперь вы можете попробовать установить соединение командой:

```
# pppd call *имя_соединения*

```

или

```
# pon *имя_соединения*

```

где *имя_соединения* — имя файла настроек, созданного в `/etc/ppp/peers`.

Чтобы убедиться, что соединение PPPoE установлено, проверьте вывод *pppd* в системном логе:

```
# journalctl -b --no-pager | grep pppd

```

При успешном соединении вы увидите что-то наподобие следующих строк:

```
Jul 09 22:42:33 localhost pppd[239]: Plugin rp-pppoe.so loaded.
Jul 09 22:42:33 localhost pppd[239]: RP-PPPoE plugin version 3.8p compiled against pppd 2.4.6
Jul 09 22:42:33 localhost network[184]: RP-PPPoE plugin version 3.8p compiled against pppd 2.4.6
Jul 09 22:42:33 localhost pppd[239]: pppd 2.4.6 started by root, uid 0
Jul 09 22:42:39 localhost pppd[239]: PPP session is 292
Jul 09 22:42:39 localhost pppd[239]: Connected to a0:f3:e4:4f:e3:b0 via interface enp4s0
Jul 09 22:42:39 localhost pppd[239]: Using interface ppp0
Jul 09 22:42:39 localhost pppd[239]: Connect: ppp0 <--> enp4s0
Jul 09 22:42:39 localhost pppd[239]: CHAP authentication succeeded: CHAP authentication success
Jul 09 22:42:39 localhost pppd[239]: CHAP authentication succeeded
Jul 09 22:42:39 localhost pppd[239]: peer from calling number A0:F3:E4:4F:E3:B0 authorized
Jul 09 22:42:39 localhost pppd[239]: Cannot determine ethernet address for proxy ARP
Jul 09 22:42:39 localhost pppd[239]: local  IP address 10.6.2.137
Jul 09 22:42:39 localhost pppd[239]: remote IP address 10.6.1.1
Jul 09 22:42:39 localhost pppd[239]: primary   DNS address 10.6.1.1
Jul 09 22:42:39 localhost pppd[239]: secondary DNS address 210.21.196.6

```

Файл настроек `/etc/ppp/peers/provider` используется по умолчанию, если при вызове *pppd* не было указано имя файла. Вместо явного указания имени файла настроек программе *pppd* вы также можете просто добавить символическую ссылку на свой файл:

```
# ln -s /etc/ppp/peers/*имя_соединения* /etc/ppp/peers/provider

```

Теперь можно устанавливать соединение одной командой

```
# pon

```

Чтобы разорвать соединение, выполните

```
# poff *имя_соединения*

```

### Запуск pppd при старте системы

Выполните следующие шаги:

*   Настройте модуль `ppp_generic` для загрузки во время запуска. Инструкции можно найти на странице [Модули ядра#Автоматическое управление модулями](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Автоматическое_управление_модулями "Модули ядра").
*   [Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу systemd:

```
# systemctl enable ppp@*имя_соединения*.service

```

## Дополнительно

### Автодозвон

Если *pppd* запущен, вы можете выполнить сброс соединения, отправив процессу сигнал `SIGHUP`:

```
# export PPPD_PID=$(pidof pppd)
# kill -s HUP $PPPD_PID

```

После разрыва соединение будет вновь установлено.

**Примечание:** Убедитесь, что опция `persist` включена в ваш файл конфигурации `/etc/ppp/peers/provider`. Также вы можете добавить параметр `holdoff 0` для переподключения без тайм-аута.

### Автоматический разрыв соединения

**Примечание:** Если вы не оставляете ваш компьютер работать круглосуточно, то можете смело пропустить этот шаг

Если у вас безлимитное соединение и вы поддерживаете его непрерывно, некоторые провайдеры могут сбрасывать его каждые 24 часа. Это гарантирует, что ваш динамический IP-адрес будет меняться каждые сутки. Чтобы иметь возможность подключиться извне, вы можете использовать какой-нибудь динамический DNS-сервис вместе с [inadyn](https://aur.archlinux.org/packages/inadyn/), тогда по доменному имени всегда можно будет вычислить текущий IP. Но чтобы избежать нежелательных разрывов, вы можете сами (настроив задачу для [cron](/index.php/Cron "Cron") либо создав таймер [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Таймеры "Systemd (Русский)")) выполнять сброс каждые сутки в такое время, когда никто не пользуется соединением — например, в 4 утра.

#### Используя cron

Выполните следующие шаги от имени суперпользователя.

Создайте файл скрипта (например, `pppd_redial.sh`) со следующим содержимым:

```
#!/bin/bash

message="Restarting the PPP connection @:" $(date)
pppd_id=$(pidof pppd)

kill -s HUP $pppd_id
echo $message

```

Сохраните файл и дайте ему права на выполнение.

Теперь создайте задачу для [cron](/index.php/Cron "Cron"), используя команду `crontab -e`. Если появляется ошибка, убедитесь, что установлена [переменная окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `EDITOR`. По команде откроется редактор — добавьте в него строку, указав правильный путь до вашего скрипта перезапуска соединения:

```
0 4 * * * /bin/bash /root/pppd_redial.sh

```

Сохраните файл и убедитесь, что служба `cronie` работает. Если это не так, [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `cronie`.

Теперь ваше соединение будет перезапускаться каждый день в 4 утра.

#### Используя таймер systemd

Также вы можете настроить таймер [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") для выполнения ежедневного перезапуска соединения. Просто создайте файлы *.service* и *.timer* с одинаковыми именами:

 `ppp-redial.timer` 
```
[Unit]
Description=Reconnect PPP connections daily

[Timer]
OnCalendar=*-*-* 05:00:00

[Install]
WantedBy=multi-user.target

```
 `ppp-redial.service` 
```
[Unit]
Description=Reconnect PPP connections

[Service]
Type=simple
ExecStart=/usr/bin/poff -r

```

Теперь просто [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") таймер, и systemd будет выполнять сброс соединения каждый день в указанное время.

## Решение проблем

### Маршрут по умолчанию

При запуске *pppd* пытается добавить свой системный маршрут по умолчанию (*default route*). Если перед запуском уже был установлен такой маршрут, *pppd* не станет его обновлять, и новые соединения во внешнюю сеть направляться не будут. При этом в `/var/log/errors.log` вы увидите что-то наподобие:

```
pppd[nnnn]: not replacing existing default route via *xxx.xxx.xxx.xxx*

```

Если это поведение нежелательно, и `xxx.xxx.xxx.xxx` — совсем не то, что вам нужно, вы можете создать простой скрипт в `/etc/ppp/ip-pre-up` с таким содержимым:

 `/etc/ppp/ip-pre-up/10-route-del-default.sh` 
```
#!/bin/sh
/usr/bin/route del default

```

Не забудьте дать скрипту права на запуск.

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") службу `pppd`.

### Маскарадинг работает, но некоторые сайты не открываются

Проблема выражается в том, что соединение есть, но часть сайтов и сервисов не работают, если вы используете ваш компьютер в роли маршрутизатора для других компьютеров. Дело в том, что размер MTU (*Maximum Transmission Unit* — максимальное количество байт данных в одном пакете) в PPPoE равен 1492 байтам, что меньше, чем используют большинство сайтов (1500). Ваш маршрутизатор отправляет серверу специальный пакет ICMP 3:4 (сообщение о том, что нужно переразбиение данных), запрашивая меньший MTU, но сетевые экраны многих сайтов блокируют это сообщение.

Проблема решается добавлением правила с PMTU clamping в [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)"):

```
# iptables -I FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu

```

Однако, по некоторой причине, это правило может не попадать в вывод *iptables-save*. Если у вас тот случай, когда *iptables-restore* не восстанавливает правило после перезапуска, попробуйте следующее решение.

Создайте файл службы [systemd](/index.php/Systemd "Systemd"):

 `pmtu-clamping.service` 
```
[Unit]
Description=PMTU clamping for pppoe
Requires=iptables.service
After=iptables.service

[Service]
Type=oneshot
ExecStart=/usr/bin/iptables -I FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu

[Install]
WantedBy=multi-user.target

```

И включите эту службу.

### Не удается загрузить модуль ядра ppp_generic

Проблема выражается в том, что при запуске процесс *pppd* не может найти соответствующий модуль:

```
Couldn't open the /dev/ppp device: No such device or address
Please load the ppp_generic kernel module.

```

Решается исправлением `/etc/modprobe.d/modules.conf`: замените в файле строку

```
alias char-major-108 ppp

```

на

```
alias char-major-108 ppp_generic

```

или добавьте ее, если первой строки в файле не было.

После перезагрузки проблема должна решиться.