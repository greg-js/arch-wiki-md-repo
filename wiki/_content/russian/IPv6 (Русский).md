По умолчанию в Arch Linux включена поддержка IPv6\. Если вы ищете информацию о туннелировании IPv6 через брокера, смотрите [IPv6 tunnel broker setup](/index.php/IPv6_tunnel_broker_setup "IPv6 tunnel broker setup").

## Contents

*   [1 Privacy Extensions](#Privacy_Extensions)
    *   [1.1 dhcpcd](#dhcpcd)
    *   [1.2 NetworkManager](#NetworkManager)
*   [2 Сетевое обнаружение](#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B5_.D0.BE.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
*   [3 Статический адрес](#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B0.D0.B4.D1.80.D0.B5.D1.81)
*   [4 IPv6 и Comcast](#IPv6_.D0.B8_Comcast)
*   [5 Отключение IPv6](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_IPv6)
    *   [5.1 Отключение функциональности](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.2 Другие программы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
        *   [5.2.1 dhcpcd](#dhcpcd_2)
        *   [5.2.2 NetworkManager](#NetworkManager_2)
        *   [5.2.3 ntpd](#ntpd)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Privacy Extensions

В этом разделе описано, как включить Privacy Extensions для stateless-автонастройки адресов IPv6 в соответствии с [RFC 4941](https://tools.ietf.org/html/rfc4941).

Добавьте следующие строки в `/etc/sysctl.d/40-ipv6.conf`:

```
# Enable IPv6 Privacy Extensions
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
net.ipv6.conf.*nic0*.use_tempaddr = 2
...
net.ipv6.conf.*nicN*.use_tempaddr = 2

```

Где `nic0`...`nicN` — имена ваших сетевых интерфейсов (параметры `all.use_tempaddr` и `default.use_tempaddr` не будут применены к сетевым интерфейсам, которые уже определены в системе на момент выполнения файла настроек [sysctl](/index.php/Sysctl "Sysctl")).

После перезагрузки Privacy Extensions будут включены, а сетевым интерфейсам будут присваиваться дополнительные временные адреса IPv6.

### dhcpcd

С версии [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") 6.4.0 добавлена опция `slaac private`, которая включает функцию присвоения стабильных частных адресов вместо адресов, основанных на MAC-адресе интерфейса, реализуя [RFC 7217](https://tools.ietf.org/html/rfc7217) ([коммит](http://roy.marples.name/projects/dhcpcd/info/8aa9dab00dc72c453aeccbde885ecce27a3d81ff)). Дополнительная настройка не требуется, если, конечно, вы не хотите изменять адрес IPv6 при каждом новом подключении к сети.

### NetworkManager

NetworkManager не учитывает настройки, размещенные в `/etc/sysctl.d/40-ipv6.conf`. Вы можете убедиться в этом, выполнив `$ ip -6 addr show *имя_интерфейса*` после перезагрузки: вы увидите, что кроме обычного адреса временный адрес `scope global **temporary**` не отображается.

Как это исправить смотрите на странице [NetworkManager#Enable IPv6 Privacy Extensions](/index.php/NetworkManager#Enable_IPv6_Privacy_Extensions "NetworkManager").

**Обратите внимание:** Может показаться, что временный адрес IPv6, созданный при включении Privacy Extensions, никогда не обновляется (он не переходит в статус `deprecated` после истечения времени жизни `valid_lft`). На самом деле это не совсем так: через больший промежуток времени адрес рано или поздно изменится.

## Сетевое обнаружение

Пинг по мультивещательному адресу `ff02::1` заставит все хосты в локальной сети ответить. При этом должен быть указан конкретный сетевой интерфейс:

```
$ ping6 ff02::1%eth0

```

Аналогично, если сделать пинг по адресу `ff02::2`, то вам ответят только маршрутизаторы, которые присутствуют в локальной сети.

Если вы добавите опцию `-I *your-global-ipv6*` в пинг-запрос, локальные хосты ответят с использованием локальных же адресов. При этом вы можете не указывать сетевой интерфейс:

```
$ ping6 -I 2001:4f8:fff6::21 ff02::1

```

## Статический адрес

Иногда использование статического адреса может быть применено в качестве одной из мер обеспечения безопасности. Например, если ваш локальный маршрутизатор использует сетевое обнаружение или radvd ([RFC 2461](http://www.apps.ietf.org/rfc/rfc2461.html)), вашему интерфейсу будет автоматически присвоен адрес, который содержит часть MAC-адреса сетевого интерфейса (используя stateless-автонастройку IPv6). Это может быть не слишком хорошо для безопасности, так как позволяет без труда отслеживать систему даже если часть IPv6-адреса сменилась.

Чтобы присвоить статический IP-адрес при помощи [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)"), используйте шаблон профиля `/etc/netctl/examples/ethernet-static`. Следующие строки особенно важны:

```
# For IPv6 static address configuration
IP6=static
Address6=('1234:5678:9abc:def::1/64' '1234:3456::123/96')
Routes6=('abcd::1234')
Gateway6='1234:0:123::abcd'

```

## IPv6 и Comcast

`dhcpcd -4` и `dhcpcd -6` работают с Motorola SURFBoard 6141 и Realtek RTL8168d/8111d, но не одновременно для каждого интерфейса. Запуск с ключом `-6` не станет работать, если клиент уже был запущен с опцией `-4`, даже после сброса сетевого интерфейса. И, когда это произойдет, интерфейсу будет присвоен адрес с маской /128\. Используйте следующие команды:

```
dhclient -4 enp3s0
dhclient -P -v enp3s0

```

Опция `-P` получает аренду только префикса IPv6\. С опцией `-v` содержимое `/var/lib/dhclient/dhclient6.leases` будет выведено в стандартный поток вывода:

```
Bound to *:546
Listening on Socket/enp3s0
Sending on   Socket/enp3s0
PRC: Confirming active lease (INIT-REBOOT).
XMT: Forming Rebind, 0 ms elapsed.
XMT:  X-- IA_PD a1:b2:cd:e2
XMT:  | X-- Requested renew  +3600
XMT:  | X-- Requested rebind +5400
XMT:  | | X-- IAPREFIX 1234:5:6700:890::/64

```

IAPREFIX является необходимым значением. Подставьте `1` перед слэшем, чтобы адрес стал корректным:

```
ip -6 addr add 1234:5:6700:890::1/64 dev enp3s0

```

## Отключение IPv6

**Обратите внимание:** Сборка ядра Linux в Arch поддерживает IPv6 напрямую, поэтому вы не можете отключить модуль, просто добавив его в черный список.

### Отключение функциональности

Добавление опции `ipv6.disable=1` в параметрах ядра отключает весь стек IPv6, что в большинстве случаев помогает добиться желаемого результата. Смотрите [параметры ядра](/index.php/Kernel_parameters "Kernel parameters") для получения дополнительной информации.

Добавив вместо этого `ipv6.disable_ipv6=1`, вы оставите стек IPv6 работающим, но при этом адреса IPv6 просто не будут присваиваться сетевым интерфейсам.

Также вы можете отключить присвоение адреса IPv6 конкретным сетевым интерфейсам, добавив следующие строки в файл настроек [sysctl](/index.php/Sysctl "Sysctl") `/etc/sysctl.d/40-ipv6.conf`:

```
# Disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.*nic0*.disable_ipv6 = 1
...
net.ipv6.conf.*nicN*.disable_ipv6 = 1

```

Вы должны явно перечислить здесь все сетевые интерфейсы, для которых требуется отключить IPv6, так как опция `all.disable_ipv6` не будет применена к сетевым интерфейсам, которые уже включены на момент выполнения инструкций из файла настроек.

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

Например, *dhcpcd* будет продолжать пытаться запрашивать настройки сети у маршрутизаторов IPv6 (т. н. *Router solicitation*). Чтобы отключить это, добавьте следующие строки в `/etc/dhcpcd.conf`, как указано в [man-странице](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Man page (Русский)") `dhcpcd.conf (5)`:

```
noipv6rs
noipv6

```

#### NetworkManager

Чтобы отключить IPv6 в NetworkManager, вызовите контекстное меню значка статуса сети и перейдите в *Edit Connections > Wired > Network name > Edit > IPv6 Settings > Method*, затем выберите *Method* как *Ignore/Disabled*.

#### ntpd

Следуя совету из раздела [Systemd#Drop-in snippets](/index.php/Systemd#Drop-in_snippets "Systemd"), измените способ запуска `ntpd.service`:

```
# systemctl edit ntpd.service

```

Это создаст drop-in сниппет, который будет запускаться вместо стандартного `ntpd.service`. Флаг `-4` отключает использование IPv6 демоном ntp. Поместите следующее в drop-in сниппет:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -4 -g -u ntp:ntp

```

Здесь сначала очищается значение `ExecStart`, а затем устанавливается новая команда.

## Смотрите также

*   [IPv6](https://www.kernel.org/doc/Documentation/networking/ipv6.txt) — документация на kernel.org
*   [IPv6 temporary addresses](http://www.ipsidixit.net/2012/08/09/ipv6-temporary-addresses-and-privacy-extensions/) — временные адреса и расширения приватности
*   [IPv6 prefixes](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/x513.html) — о типах префиксов
*   [net.ipv6 options](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/proc-sys-net-ipv6..html) — настройка параметров ядра