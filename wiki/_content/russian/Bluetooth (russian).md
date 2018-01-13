Ссылки по теме

*   [Bluez4](/index.php/Bluez4 "Bluez4")
*   [Bluetooth мышь](/index.php/Bluetooth_%D0%BC%D1%8B%D1%88%D1%8C "Bluetooth мышь")
*   [Bluetooth наушники](/index.php/Bluetooth_%D0%BD%D0%B0%D1%83%D1%88%D0%BD%D0%B8%D0%BA%D0%B8 "Bluetooth наушники")
*   [Blueman](/index.php/Blueman "Blueman")

**Состояние перевода:** На этой странице представлен перевод статьи [Bluetooth](/index.php/Bluetooth "Bluetooth"). Дата последней синхронизации: 2015-09-30\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Bluetooth&diff=0&oldid=391967).

[Bluetooth](http://www.bluetooth.org/) является стандартом для беспроводных соединений малой дальности сотовых телефонов, компьютеров и других электронных устройств. В Linux канонической реализацией стека протоколов Bluetooth является [BlueZ](http://www.bluez.org/).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка при помощи интерфейса командной строки](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B0_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8)
    *   [2.1 Bluetoothctl](#Bluetoothctl)
*   [3 Настройка при помощи графических фронтендов](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D1.85_.D1.84.D1.80.D0.BE.D0.BD.D1.82.D0.B5.D0.BD.D0.B4.D0.BE.D0.B2)
    *   [3.1 GNOME Bluetooth](#GNOME_Bluetooth)
    *   [3.2 BlueDevil](#BlueDevil)
    *   [3.3 Blueberry](#Blueberry)
    *   [3.4 Blueman](#Blueman)
*   [4 Использование Obex для отсылки и получения файлов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Obex_.D0.B4.D0.BB.D1.8F_.D0.BE.D1.82.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.D0.B8_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
    *   [4.1 ObexFS](#ObexFS)
    *   [4.2 Передача по ObexFTP](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D0.BF.D0.BE_ObexFTP)
    *   [4.3 Obex Object Push](#Obex_Object_Push)
*   [5 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 bluetoothctl](#bluetoothctl_2)
    *   [6.2 gnome-bluetooth](#gnome-bluetooth)
    *   [6.3 Bluetooth USB донгл](#Bluetooth_USB_.D0.B4.D0.BE.D0.BD.D0.B3.D0.BB)
    *   [6.4 Logitech Bluetooth USB донгл](#Logitech_Bluetooth_USB_.D0.B4.D0.BE.D0.BD.D0.B3.D0.BB)
    *   [6.5 hcitool scan: Устройство не найдено](#hcitool_scan:_.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.BD.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD.D0.BE)
    *   [6.6 rfkill unblock: не происходит разблокировка](#rfkill_unblock:_.D0.BD.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.B8.D1.82_.D1.80.D0.B0.D0.B7.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [6.7 Мой компьютер невидим](#.D0.9C.D0.BE.D0.B9_.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80_.D0.BD.D0.B5.D0.B2.D0.B8.D0.B4.D0.B8.D0.BC)
    *   [6.8 Не происходит сопряжение с клавиатурой Logitech](#.D0.9D.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.B8.D1.82_.D1.81.D0.BE.D0.BF.D1.80.D1.8F.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.BE.D0.B9_Logitech)
    *   [6.9 Профили HSP/HFP](#.D0.9F.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B8_HSP.2FHFP)
    *   [6.10 Проблемы с Thinkpad Bluetooth Laser Mouse](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_Thinkpad_Bluetooth_Laser_Mouse)
    *   [6.11 Lite-On Broadcom устройства](#Lite-On_Broadcom_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [bluez](https://www.archlinux.org/packages/?name=bluez) и [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). Пакет [bluez](https://www.archlinux.org/packages/?name=bluez) предоставляет стек Bluetooth протокола, а пакет [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) предоставляет утилиту `bluetoothctl`.

Загрузите универсальный драйвер bluetooth, если это еще не сделано:

```
# modprobe btusb

```

Теперь [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `bluetooth.service` systemd юнит. Вы можете [включить сервис](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") в автозагрузку.

**Примечание:**

*   По умолчанию демон bluetooth разрешит использовать устройства bnep0 только пользователям, входящим в группу `lp`. Удостоверьтесь, что учетная запись обычного пользователя добавлена в нее, если вы намереваетесь подключаться по bluetooth. Вы можете изменить группу, требуемую для этого, в файле `/etc/dbus-1/system.d/bluetooth.conf`.
*   Некоторые адаптеры Bluetooth встроены в платы Wi-Fi (например, [Intel Centrino](http://www.intel.ru/content/www/ru/ru/wireless-products/centrino-advanced-n-6235.html)). В этих случаях необходимо, чтобы сперва была включена плата Wi-Fi (обычно при помощи клавиш(и) на ноутбуке), после чего ядро сможет увидеть адаптер Bluetooth.
*   Некоторые адаптеры Bluetooth (например, Broadcom) конфликтуют с сетевыми адаптерами. В этом случае вам необходимо удостовериться, что устройство Bluetooth подключается до начала загрузки сетевых служб.

## Настройка при помощи интерфейса командной строки

### Bluetoothctl

Сопряжение с устройством в оболочке (shell) является одним из самых простых и надежных вариантов. То, что необходимо делать, зависит от используемых устройств и их входной функциональности. Последующие инструкции описывают сопряжение с устройством при помощи `/usr/bin/bluetoothctl` лишь в общих чертах.

Запустите интерактивную команду `bluetoothctl`. После этого можно ввести `help` для получения списка доступных команд.

*   Включите питание контроллера, введя `power on`. По умолчанию оно отключено.
*   Введите `devices`, чтобы увидеть MAC-адрес устройства для сопряжения.
*   Войдите в режим обнаружения устройств при помощи команды `scan on`, если нужного вам устройства нет в списке.
*   Включите агент при помощи `agent on`.
*   Введите `pair *MAC-адрес*`, чтобы осуществить сопряжение (работает автодополнение по tab).
*   При использовании устройства без PIN, возможно, потребуется подтверждение, прежде чем оно сможет успешно переподключиться. Для этого введите `trust *MAC-адрес*`.
*   Наконец, используйте `connect *MAC-адрес*` для установки соединения.

Ваша сессия будет выглядеть примерно так:

```
# bluetoothctl 
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent KeyboardOnly 
Agent registered
[bluetooth]# default-agent 
Default agent request successful
[bluetooth]# scan on
Discovery started
[CHG] Controller 00:10:20:30:40:50 Discovering: yes
[NEW] Device 00:12:34:56:78:90 myLino
[CHG] Device 00:12:34:56:78:90 LegacyPairing: yes
[bluetooth]# pair 00:12:34:56:78:90
Attempting to pair with 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
[CHG] Device 00:12:34:56:78:90 Connected: no
[CHG] Device 00:12:34:56:78:90 Connected: yes
Request PIN code
[agent] Enter PIN code: 1234
[CHG] Device 00:12:34:56:78:90 Paired: yes
Pairing successful
[CHG] Device 00:12:34:56:78:90 Connected: no

```

Чтобы устройство было активно после перезагрузки, необходимо правило udev:

 `/etc/udev/rules.d/10-local.rules` 
```
# Set bluetooth power up
ACTION=="add", KERNEL=="hci0", RUN+="/usr/bin/hciconfig hci0 up"
```

После цикла ухода/возвращения из спящего режима устройство можно включать автоматически, используя подобный сервис *systemd*:

 `/etc/systemd/system/bluetooth-auto-power@.service` 
```
[Unit]
Description=Bluetooth auto power on
After=bluetooth.service sys-subsystem-bluetooth-devices-%i.device suspend.target

[Service]
Type=oneshot
#We could also do a 200 char long call to bluez via dbus. Except this does not work since bluez does not react to dbus at this point of the resume sequence and I do not know how I get this service to run at a time it does. So we just ignore bluez and force %i up using hciconfig. Welcome to the 21st century.
#ExecStart=/usr/bin/dbus-send --system --type=method_call --dest=org.bluez /org/bluez/%I org.freedesktop.DBus.Properties.Set string:org.bluez.Adapter1 string:Powered variant:boolean:true
ExecStart=/usr/bin/hciconfig %i up

[Install]
WantedBy=suspend.target

```

## Настройка при помощи графических фронтендов

Следующие пакеты предоставляют графический интерфейс для изменения настроек Bluetooth.

### GNOME Bluetooth

[GNOME Bluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) — это Bluetooth утилита в [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"). Пакет [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) предоставляет бэкенд, [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) — апплет для отображения состояния, а [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) — GUI-фронтенд настройки, к которому можно получить доступ, набрав Bluetooth на экране обзора или при помощи команды `gnome-control-center bluetooth`. Также вы можете запустить команду `bluetooth-sendto`, чтобы напрямую послать файл на удаленное устройство.

Чтобы получать файлы, вы должны установить пакет [gnome-user-share](https://www.archlinux.org/packages/?name=gnome-user-share). Затем вы можете перейти в *Settings -> Sharing*, чтобы авторизовать принимаемые файлы со спаренных устройств по Bluetooth.

**Совет:** Если вы используете Thunar и хотите добавить пункт Bluetooth в подменю *Отправить на* в меню свойств файлов, смотрите инструкции [здесь](http://docs.xfce.org/xfce/thunar/send-to) (команда, которую необходимо добавить — `bluetooth-sendto %F`).

### BlueDevil

[BlueDevil](https://projects.kde.org/projects/kde/workspace/bluedevil) — это Bluetooth утилита в [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"). Он может быть [установлен](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD "Установлен") с пакетом [bluedevil](https://www.archlinux.org/packages/?name=bluedevil) (KDE Plasma 5) или [bluedevil4](https://www.archlinux.org/packages/?name=bluedevil4) (KDE4).

Если иконка Bluetooth не отображается в Dolphin и в системном трее, добавьте её вручную. Вы можете настроить Bluedevil, чтобы он искал устройства Bluetooth при нажатии на иконку. Также вы можете настроить BlueDevil через Параметры Системы KDE.

### Blueberry

*Blueberry* — это альтернативный фронтэнд для GNOME Bluetooth, который работает во всех окружениях рабочего стола. Его можно установить с пакетом [blueberry](https://www.archlinux.org/packages/?name=blueberry). Он предоставляет утилиту настройки (*blueberry*) и апплет системного трея (*blueberry-tray*).

### Blueman

Смотрите статью [Blueman](/index.php/Blueman "Blueman").

## Использование Obex для отсылки и получения файлов

### ObexFS

Другим вариантом, по сравнению с использованием пакетов KDE или Gnome Bluetooth, является Obexfs, который позволяет вам примонтировать ваш телефон и использовать его как часть файловой системы.

**Примечание:** Для использования ObexFS необходимо устройство, которое поддерживает сервис Obex FTP

Установите пакет [obexfs](https://aur.archlinux.org/packages/obexfs/) и примонтируйте поддерживаемые телефоны, выполнив:

```
$ obexfs -b *MAC-адрес_устройства* /точка_монтирования

```

Когда вы закончите, используйте следующую команду для отмонтирования устройства:

```
$ fusermount -u /точка_монтирования

```

Чтобы узнать об остальных опциях монтирования, загляните на [http://dev.zuckschwerdt.org/openobex/wiki/ObexFs](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs)

**Примечание:** Убедитесь, что устройство bluetooth, которое вы монтируете, **не** настроено так, чтобы монтироваться в режиме *только для чтения*. Это должно настраиваться в настройках на самом устройстве. Если оно примонтировано в режиме *только для чтения*, вы можете столкнуться с ошибкой прав доступа при попытке передачи файлов на устройство

### Передача по ObexFTP

Если ваше устройство поддерживает сервис Obex FTP, но вы не желаете монтировать его, вы можете осуществлять передачу файлов на и с устройства, используя команду obexftp.

Чтобы послать файл на устройство, выполните команду:

```
$ obexftp -b *MAC-адрес_устройства* -p /путь/к/файлу

```

Чтобы получить файл с устройства, выполните команду:

```
$ obexftp -b *MAC-адрес_устройства* -g имя_файла

```

**Примечание:** Убедитесь, что файл, который вы хотите получить, находится в *папке обмена* устройства. Если файл находится в её подпапке, пропишите в команде правильный путь.

### Obex Object Push

Если ваше устройство не поддерживает сервис Obex FTP, проверьте, поддерживает ли оно Obex Object Push.

```
# sdptool browse *XX:XX:XX:XX:XX:XX*

```

Просмотрите вывод: ищите Obex Object Push, запомните канал этого сервиса. Если он поддерживается, можно использовать пакет [ussp-push](https://aur.archlinux.org/packages/ussp-push/) для отсылки файлов на устройство:

```
# ussp-push *XX:XX:XX:XX:XX:XX*@*КАНАЛ* *файл* *желаемое_имя_файла_на_телефоне*

```

## Примеры

Все примеры были перемещены в статью [bluez4](/index.php/Bluez4 "Bluez4"). Их необходимо проверить и исправить для использования с bluez5.

## Решение проблем

### bluetoothctl

Если bluetoothctl не может найти ни один контроллер, возможно заблокировано bluetooth устройство. Попробуйте разблокировать его с помощью rfkill:

```
# rfkill unblock bluetooth

```

### gnome-bluetooth

Если вы видите это при попытке включить получение файлов в настройках bluetooth:

```
 Bluetooth OBEX start failed: Invalid path
 Bluetooth FTP start failed: Invalid path

```

Установите пакет [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) и выполните:

```
 $ xdg-user-dirs-update

```

Вы можете отредактировать пути, используя команду:

```
 $ vi ~/.config/user-dirs.dirs

```

### Bluetooth USB донгл

Если вы пользуетесь USB донглом, вы должны проверить, что ваш Bluetooth донгл распознан системой. Это можно сделать с помощью команды `journalctl -f`, после того как вы воткнёте USB донгл (или заглянув в `/var/log/messages.log`). Должно появиться что-то вроде следующего (ищите hci):

```
 Feb 20 15:00:24 hostname kernel: [ 2661.349823] usb 4-1: new full-speed USB device number 3 using uhci_hcd
 Feb 20 15:00:24 hostname bluetoothd[4568]: HCI dev 0 registered
 Feb 20 15:00:24 hostname bluetoothd[4568]: Listening for HCI events on hci0
 Feb 20 15:00:25 hostname bluetoothd[4568]: HCI dev 0 up
 Feb 20 15:00:25 hostname bluetoothd[4568]: Adapter /org/bluez/4568/hci0 has been enabled

```

Если вы получили только первые две строки, значит донгл распознан, но вам необходимо его активировать (поднять). Пример:

 `hciconfig -a hci0` 
```
hci0:	Type: USB
	BD Address: 00:00:00:00:00:00 ACL MTU: 0:0 SCO MTU: 0:0
	DOWN 
	RX bytes:0 acl:0 sco:0 events:0 errors:0
        TX bytes:0 acl:0 sco:0 commands:0 errors:

```

```
# hciconfig hci0 up

```
 `hciconfig -a hci0` 
```
hci0:	Type: USB
	BD Address: 00:02:72:C4:7C:06 ACL MTU: 377:10 SCO MTU: 64:8
	UP RUNNING 
	RX bytes:348 acl:0 sco:0 events:11 errors:0
        TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

Если появляется ошибка вроде этой:

```
Operation not possible due to RF-kill

```

это ошибка может возникать либо из-за утилиты `rfkill`, в таком случаевы можете решить проблему командой:

```
# rfkill unblock all

```

либо это может быть из-за того, что используется аппаратный выключатель на компьютере. Аппаратный выключатель bluetooth (по крайней мере, иногда) также контролирует доступ к bluetooth USB донглам. Передвиньте/нажмите этот переключатель и попробуйте поднять устройство ещё раз.

Чтобы убедиться, что устройство было определено, вы можете использовать `hcitool`, являющуюся частью `bluez-utils`. Вы можете получить список доступных устройств, их идентификаторов и MAC-адресов, используя:

 `$ hcitool dev` 
```
 Devices:
         hci0	00:1B:DC:0F:DB:40
```

Более детальная информация об устройстве может быть получена с помощью `hciconfig`.

 `$ hciconfig -a hci0` 
```
 hci0:   Type: USB
         BD Address: 00:1B:DC:0F:DB:40 ACL MTU: 310:10 SCO MTU: 64:8
         UP RUNNING PSCAN ISCAN 
         RX bytes:1226 acl:0 sco:0 events:27 errors:0
         TX bytes:351 acl:0 sco:0 commands:26 errors:0
         Features: 0xff 0xff 0x8f 0xfe 0x9b 0xf9 0x00 0x80
         Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
         Link policy: RSWITCH HOLD SNIFF PARK 
         Link mode: SLAVE ACCEPT 
         Name: 'BlueZ (0)'
         Class: 0x000100
         Service Classes: Unspecified
         Device Class: Computer, Uncategorized
         HCI Ver: 2.0 (0x3) HCI Rev: 0xc5c LMP Ver: 2.0 (0x3) LMP Subver: 0xc5c
         Manufacturer: Cambridge Silicon Radio (10)
```

### Logitech Bluetooth USB донгл

Существуют Logitech донглы (например, Logitech MX5000), которые могут работать в двух режимах: встроенный и HCI. Во встроенном режиме донгл эмулирует устройство USB так, что ваш компьютер думает, что вы используете обычную USB мышь/клавиатуру.

Если вы нажмёте маленькую красную кнопку на USB BT мини-приёмнике, включится другой режим. Удерживайте красную кнопку на BT донгле и вставьте его в компьютер, и через 3-5 секунд удерживания кнопки в системном трее появится иконка Bluetooth ([Обсуждение](http://ubuntuforums.org/showthread.php?t=1332197)).

В качестве альтернативы, вы можете установить пакет [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci). Когда вы подключите ваш Logitech донгл, он автоматически переключится.

### hcitool scan: Устройство не найдено

*   На некоторых ноутбуках Dell (например, Studio 15) вы должны переключить режим Bluetooth с HID на HCI. Установите пакет [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci), после чего [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") будет делать это автоматически. В качестве альтернативы вы можете выполнить эту команду для переключения на HCI вручную:

```
# /usr/lib/udev/hid2hci

```

*   Если устройство не появится, а на вашей машине есть операционная система Windows, попробуйте загрузить её и включить адаптер bluetooth в windows.

*   Иногда также помогает эта простая команда:

```
# hciconfig hci0 up

```

### rfkill unblock: не происходит разблокировка

Если ваше устройство по-прежнему программно блокируется и у вас запущен connman, попробуйте это:

```
$ connmanctl enable bluetooth

```

### Мой компьютер невидим

Не можете найти ваш компьютер с вашего телефона? Включите PSCAN и ISCAN:

```
# enable PSCAN and ISCAN
$ hciconfig hci0 piscan 
# check it worked

```
 `$ hciconfig` 
```
 hci0:   Type: USB
         BD Address: 00:12:34:56:78:9A ACL MTU: 192:8 SCO MTU: 64:8
         **UP RUNNING PSCAN ISCAN**
         RX bytes:20425 acl:115 sco:0 events:526 errors:0
         TX bytes:5543 acl:84 sco:0 commands:340 errors:0
```

**Примечание:** Проверьте DiscoverableTimeout и PairableTimeout в `/etc/bluetooth/main.conf`

Попробуйте изменить класс устройства в /etc/bluetooth/main.conf, как здесь:

```
# Default device class. Only the major and minor device class bits are
# considered.
#Class = 0x000100 (from default config)
Class = 0x100100

```

Это было единственное решение, сделавшее мой компьютер видимым для телефона.

### Не происходит сопряжение с клавиатурой Logitech

Если вам не выдается ключ доступа при попытке сопряжения клавиатуры Logitech, наберите следующую команду:

```
# hciconfig hci0 sspmode 0

```

Если после сопряжения клавиатура по-прежнему не подключается, проверьте вывод `hcidump -at`. Если в нем содержатся повторяющиеся подключения-отключения, как в следующем сообщении:

```
   status 0x00 handle 11 reason 0x13
   Reason: Remote User Terminated Connection

```

значит, на данный момент единственным решением является установка [старого стека Bluetooth](/index.php/Bluez4 "Bluez4").

### Профили HSP/HFP

В bluez5 убрали поддержку профилей HSP/HFP (гарнитура телефонии для [TeamSpeak](/index.php/TeamSpeak "TeamSpeak"), [Skype](/index.php/Skype_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Skype (Русский)") и т.д.). Вам нужно установить [PulseAudio](/index.php/PulseAudio "PulseAudio") (>= версии 6) или другое приложение, которое реализует HSP/HFP самостоятельно.

### Проблемы с Thinkpad Bluetooth Laser Mouse

Если вы чувствуете, что ваша Thinkpad Bluetooth Laser Mouse быстро подключается, а затем (через несколько миллисекунд) снова отключается каждые несколько секунд (когда вы двигаете мышь или нажимаете кнопку), попробуйте спарить её с пин кодом `0000`, вместо того, чтобы спаривать её без пин кода.

### Lite-On Broadcom устройства

Некоторые из этих устройств необходимо прошивать при загрузке. Прошивка не предоставляется, но может быть сконвертирована из *.hex* файла для Microsoft Windows в *.hcd* с помощью [hex2hcd](https://github.com/jessesung/hex2hcd).

Чтобы получить нужный *.hex* файл, попробуйте поискать устройство по коду vendor:product (производитель:продукт), который отобразила командой *lsusb*, например:

```
   ...
   Bus 002 Device 004: ID **04ca:2006** Lite-On Technology Corp. Broadcom BCM43142A0 Bluetooth Device
   ...

```

В качестве альтернативы, вы можете загрузиться в Windows (можете использовать виртуальную машину) и узнать название прошивки из утилиты Диспетчер Устройств.

Когда вы получите *.hcd* файл, скопируйте его в `/lib/firmware/brcm/BCM.hcd` - *dmesg* знает, что по этому пути лежит прошивка и в вашем случае он может меняться, поэтому проверьте вывод команды *dmesg*, чтобы убедиться в этом. Затем прошейте файл *.hcd* с помощью утилиты *brcm_patchram_plus*, предоставляемой пакетом [brcm_patchram_plus-git](https://aur.archlinux.org/packages/brcm_patchram_plus-git/). Загрузите модуль btusb:

```
# modprobe btusb

```

Убедитесь, что устройство распознано в качестве bluetooth устройства. Замените *04ca 2006* на ваши значения vendor и product:

```
# echo '04ca 2006' > /sys/bus/usb/drivers/btusb/new_id

```

Включите устройство:

```
# hciconfig hci0 up

```

Прошейте прошивку:

```
# brcm_patchram_plus_usb --patchram fw-04ca_2006.hcd hci0

```

Теперь устройство должно быть доступно. Смотрите [BBS#162688](https://bbs.archlinux.org/viewtopic.php?id=162688) для информации о том, как сделать эти изменения постоянными.