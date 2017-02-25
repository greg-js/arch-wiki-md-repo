**Состояние перевода:** На этой странице представлен перевод статьи [Template:TranslationStatus](/index.php/Template:TranslationStatus "Template:TranslationStatus"). Дата последней синхронизации: 25 февраля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Template:TranslationStatus&diff=0&oldid=469030).

В этой статье описываются несколько способов подмены адреса Media Access Control (MAC).

## Contents

*   [1 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
    *   [1.1 Способ 1: iproute2](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_1:_iproute2)
    *   [1.2 Способ 2: macchanger](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_2:_macchanger)
*   [2 Автоматически](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8)
    *   [2.1 Способ 1: systemd-networkd](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_1:_systemd-networkd)
    *   [2.2 Способ 2: systemd-udevd](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_2:_systemd-udevd)
    *   [2.3 Способ 3: юнит systemd](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_3:_.D1.8E.D0.BD.D0.B8.D1.82_systemd)
        *   [2.3.1 Создание юнита](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.B0)
            *   [2.3.1.1 iproute2](#iproute2)
            *   [2.3.1.2 macchanger](#macchanger)
        *   [2.3.2 Включение службы](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B)
    *   [2.4 Способ 4: использование netctl](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_4:_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_netctl)
    *   [2.5 Способ 5: NetworkManager](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_5:_NetworkManager)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Не удается подключиться к сети DHCPv4](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C.D1.81.D1.8F_.D0.BA_.D1.81.D0.B5.D1.82.D0.B8_DHCPv4)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Вручную

Существует два способа подмены MAC-адреса: используя [iproute2](https://www.archlinux.org/packages/?name=iproute2) (установленный по умолчанию), и с помощью [macchanger](https://www.archlinux.org/packages/?name=macchanger) (доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)")). Оба способа изложены ниже.

### Способ 1: iproute2

Сперва проверьте ваш текущий MAC-адрес при помощи команды:

```
# ip link show *интерфейс*

```

где `*интерфейс*` — имя вашего [сетевого интерфейса](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B "Network configuration (Русский)").

Необходимая нам в данный момент информация расположена в строке, начинающейся со слов "link/ether", за которыми следует 6-битный номер. Скорее всего, у вас это будет выглядеть примерно так:

```
link/ether 00:1d:98:5a:d1:3a

```

Первый шаг для подмены MAC-адреса — отключить интерфейс. Это можно сделать, выполнив команду:

```
# ip link set dev *интерфейс* down

```

Теперь мы переходим собственно к подмене нашего MAC-адреса. Подойдет любое шестнадцатеричное число, однако, некоторые сети могут отказывать в присвоении IP-адресов клиентам, чьи MAC-адреса не соответствуют тем, что устанавливают поставщики оборудования. Поэтому, если вы не контролируете сеть(и), к которой вы подключаетесь, желательно использовать реальный префикс MAC (первые три байта), а для для оставшихся трех использовать случайное значение. Для дополнительной информации пожалуйста прочтите [Wikipedia:ru:Уникальный идентификатор организации](https://en.wikipedia.org/wiki/ru:%D0%A3%D0%BD%D0%B8%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9_%D0%B8%D0%B4%D0%B5%D0%BD%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82%D0%BE%D1%80_%D0%BE%D1%80%D0%B3%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B8 "wikipedia:ru:Уникальный идентификатор организации")

Чтобы сменить MAC, необходимо выполнить команду:

```
# ip link set dev *интерфейс* address *XX:XX:XX:XX:XX:XX*

```

где вместо `*XX:XX:XX:XX:XX:XX*` необходимо указать любое 6-байтное значение.

Последний шаг — включить интерфейс обратно. Это можно сделать, выполнив команду:

```
# ip link set dev *интерфейс* up

```

Если вы хотите проверить, произошла ли подмена MAC-адреса, просто еще раз запустите `ip link show *интерфейс*` и проверьте значение "link/ether". Если подмена сработала, "link/ether" будет иметь то значение, которое вы ему присвоили.

### Способ 2: macchanger

В этом способе используется пакет [macchanger](https://www.archlinux.org/packages/?name=macchanger) (GNU MAC Changer). Он предоставляет множество функций, таких как смена адреса для соответствия конкретному поставщику и присвоение полностью случайного адреса.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [macchanger](https://www.archlinux.org/packages/?name=macchanger) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Подмена осуществляется для конкретного интерфейса: в каждой из следующих команд заменяйте `*интерфейс*` на имя вашего [сетевого интерфейса](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D1.8B.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B "Network configuration (Русский)").

Вы можете сгенерировать полностью случайный адрес:

```
# macchanger -r *интерфейс*

```

А чтобы изменить только байты, которые являются уникальными для конкретного устройства (благодаря чему при проверке MAC-адрес будет по-прежнему считаться принадлежащим тому же производителю), необходимо выполнить:

```
# macchanger -e *интерфейс*

```

Для установки конкретного MAC-адреса выполните:

```
# macchanger --mac=*XX:XX:XX:XX:XX:XX* *интерфейс*

```

где `*XX:XX:XX:XX:XX:XX*` — MAC, который вы хотите присвоить.

Наконец, для восстановления исходного значения MAC-адреса:

```
# macchanger -p *интерфейс*

```

**Примечание:** Пока будет происходить смена МАС-адреса, вы не сможете использовать устройство вне зависимости от способа подключения и того, включен ли сетевой интерфейс.

## Автоматически

### Способ 1: systemd-networkd

[systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") поддерживает подмену MAC-адреса при помощи [файлов link](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_link "Systemd-networkd (Русский)") (смотрите `man systemd.link` для получения дополнительной информации).

Для подмены статическим адресом:

 `/etc/systemd/network/00-default.link` 
```
[Match]
MACAddress=*оригинальный MAC*

[Link]
MACAddress=*новый MAC*
NamePolicy=kernel database onboard slot path
```

Для случайной генерации MAC-адреса при каждой загрузке, установите `MACAddressPolicy=random` вместо `MACAddress=*новый MAC*`.

### Способ 2: systemd-udevd

[Udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") позволяет подменять MAC-адреса в [файлах правил](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B2.D0.BE.D0.B8.D1.85_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB "Udev (Русский)"). Атрибут `address` дает возможность udev находить правильное устройство по MAС-адресу производителя, а затем выполняется команда *ip* для смены адреса:

 `/etc/udev/rules.d/75-mac-spoof.rules`  `ACTION=="add", SUBSYSTEM=="net", ATTR{address}=="XX:XX:XX:XX:XX:XX", RUN+="/usr/bin/ip link set dev %k address YY:YY:YY:YY:YY:YY"` 

где `XX:XX:XX:XX:XX:XX` — оригинальный MAC-адрес, `YY:YY:YY:YY:YY:YY` — новый.

### Способ 3: юнит systemd

#### Создание юнита

Ниже вы найдете пару примеров юнитов [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") для изменения MAC-адреса при загрузе системы: первый устанавливает указанный MAC, используя утилиту *ip*, а второй использует *macchanger* для присвоения случайного адреса. Зависимость `network-pre.target` используется для того, чтобы смена MAC происходила перед тем, как запустятся сетевые программы вроде [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)"), [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)"), [systemd-networkd](/index.php/Systemd-networkd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd-networkd (Русский)") или [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)").

##### iproute2

Юнит [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), устанавливающий указанный MAC-адрес:

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=MAC Address Change %I
Wants=network-pre.target
Before=network-pre.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i address 36:aa:88:c8:75:3a
ExecStart=/usr/bin/ip link set dev %i up

[Install]
WantedBy=multi-user.target

```

##### macchanger

Юнит [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), устанавливающий случайный адрес (префикс производителя остается тем же). Удостоверьтесь, что у вас [установлен](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [macchanger](https://www.archlinux.org/packages/?name=macchanger)):

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=macchanger on %I
Wants=network-pre.target
Before=network-pre.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
ExecStart=/usr/bin/macchanger -e %I
Type=oneshot

[Install]
WantedBy=multi-user.target

```

Если вы хотите, чтобы адрес измнялся целиком, включая префикс производителя (первые три байта), используйте опцию `-r` вместо `-e` (смотрите также [#Способ 2: macchanger](#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_2:_macchanger)).

#### Включение службы

[Включите](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") службу, добавив требуемое имя интерфейса (например, `eth0`) к:

```
# systemctl enable macspoof@eth0.service

```

Перезагрузитесь либо перезапустите необходимые службы в правильном порядке.If you are in control of your network, verify that the spoofed MAC has been picked up by your router by examining the static, or DHCP address tables within the router.

### Способ 4: использование netctl

Вы можете использовать [netctl хуки](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.85.D1.83.D0.BA.D0.BE.D0.B2 "Netctl (Русский)") для запуска команд, каждый раз когда профиль netctl (пере)запускается для нужного вам интерфейса. Замените `*interface*` на необходимый:

 `/etc/netctl/interfaces/*interface*` 
```
#!/usr/bin/env sh
/usr/bin/macchanger -r *interface*
```

Сделайте скрипт исполняемым:

```
chmod +x /etc/netctl/interfaces/*interface*

```

Источник: [akendo.eu](https://blog.akendo.eu/archlinuxrandom-mac-address-for-new-wireless-connections/)

### Способ 5: NetworkManager

Смотрите [NetworkManager (Русский)#Настройка подмены MAC-адреса на случайный](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D0.BE.D0.B4.D0.BC.D0.B5.D0.BD.D1.8B_MAC-.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.B0_.D0.BD.D0.B0_.D1.81.D0.BB.D1.83.D1.87.D0.B0.D0.B9.D0.BD.D1.8B.D0.B9 "NetworkManager (Русский)").

## Решение проблем

### Не удается подключиться к сети DHCPv4

Если вы не можете подключиться к сети DHCPv4 и используете dhcpcd, который по умолчанию используется NetworkManager, необходимо [изменить настройки dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.B4.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D1.80_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0 "Dhcpcd (Русский)"), чтобы арендовать адрес.

## Смотрите также

*   [Страница Macchanger на GitHub](https://github.com/alobbs/macchanger)
*   [Статья на debianadmin.com](http://www.debianadmin.com/change-your-network-card-mac-media-access-control-address.html) с большим количеством опций для *macchanger*