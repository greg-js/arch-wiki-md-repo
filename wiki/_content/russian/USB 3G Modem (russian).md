Сегодня многие операторы сотовой связи во всём мире предлагают своим абонентам небольшие USB модемы для доступа к Интернету по технологиям UMTS, GSM или EDGE. В этой статье описывается, как подключить и произвести первичную настройку такого модема в Arch Linux.

## Contents

*   [1 Идентификация модема](#.D0.98.D0.B4.D0.B5.D0.BD.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.86.D0.B8.D1.8F_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
*   [2 Переключение режима модема](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
*   [3 Права на доступ к модему](#.D0.9F.D1.80.D0.B0.D0.B2.D0.B0_.D0.BD.D0.B0_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BA_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D1.83)
*   [4 Дополнительные возможности](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Информация о настройках провайдеров](#.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0.D1.85_.D0.BF.D1.80.D0.BE.D0.B2.D0.B0.D0.B9.D0.B4.D0.B5.D1.80.D0.BE.D0.B2)
    *   [4.2 Некоторые команды AT](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B_AT)
    *   [4.3 USSD](#USSD)
        *   [4.3.1 Huawei](#Huawei)
        *   [4.3.2 Ручной способ](#.D0.A0.D1.83.D1.87.D0.BD.D0.BE.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1)
    *   [4.4 Понятные имена в /dev](#.D0.9F.D0.BE.D0.BD.D1.8F.D1.82.D0.BD.D1.8B.D0.B5_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B0_.D0.B2_.2Fdev)
    *   [4.5 Отправка SMS](#.D0.9E.D1.82.D0.BF.D1.80.D0.B0.D0.B2.D0.BA.D0.B0_SMS)
*   [5 Что дальше?](#.D0.A7.D1.82.D0.BE_.D0.B4.D0.B0.D0.BB.D1.8C.D1.88.D0.B5.3F)
*   [6 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Идентификация модема

**Tip:** Если вы являетесь обладателем модема ZTE MF626 или MF 636, обратите внимание на [эту статью](/index.php/ZTE_MF626_/_MF636 "ZTE MF626 / MF636").

Если вам нужно, установите [usbutils](https://www.archlinux.org/packages/?name=usbutils)

```
pacman -S usbutils

```

А потом посмотрите результат работы `lsusb`:

```
lsusb

```

```
[root@home elf]# lsusb
**Bus 002 Device 003: ID 12d1:1446 Huawei Technologies Co., Ltd. E1220 USB Modem**
Bus 002 Device 002: ID 046e:5540 Behavior Tech. Computer Corp.
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 003: ID 058f:6362 Alcor Micro Corp. Hi-Speed 21-in-1 Flash Card Reader/Writer (Internal/External)
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

Первая строчка - это USB 3G модем Huawei. Вам нужно найти свой модем и запомнить номер производителя и номер изделия: это соответственно, два числа после `ID`. У моего модема номер производителя получился **12d1**, а номер изделия - **1446**.

## Переключение режима модема

Как правило, USB модем может работать в двух режимах: виртуального диска и собственно модема. К тому же, некоторые модели модемов имеют встроенный ридер карт памяти.

**Примечание:** Первый режим нужен для установки драйвера и сервисной программы модема на компьютер. Затем, сервисная программа, при подключении к Интернету, переводит модем во второй режим. Однако, если версия такой программы Linux вас по каким-либо причинам не устраивает, необходимо помнить, что переключение модема в "режим модема" придётся настраивать вручную.

Для переключения модема в нужный режим можно воспользоваться утилитой `/lib/udev/modem-modeswitch`, поставляемой вместе с **udev**. Кстати, в udev 157 `modem-modeswitch` была переименована в `mobile-action-modeswitch` и используется только для переключения Mobile Action Cables.

**Примечание:**

Вы также можете воспользоваться утилитой [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch) для переключения режимов модема.

```
pacman -S usb_modeswitch

```

Примечательно то, что usb_modeswtich при установке создаёт правила udev для ряда моделей устройств. Подробнее вы можете почитать на официальном [сайте](http://www.draisberghof.de/usb_modeswitch) программы, или же загляните в сами правила, `/lib/udev/rules.d/40-usb_modeswitch.rules`.

Правила udev находятся в `/etc/udev/rules.d`. Например, для автоматического переключения Huawei E1220 в режим модема, нужно создать файл `/etc/udev/rules.d/40-huawei-e1220.rules` с правилом:

```
SUBSYSTEM=="usb", SYSFS{idProduct}=="**1446**", SYSFS{idVendor}=="**12d1**", RUN+="/lib/udev/modem-modeswitch --vendor **0x12d1** --product **0x1446** --type option-zerocd"

```

Обратите внимание на `1446` и `12d1` в строке правила - это номер изделия и номер производителя. Вам нужно заменить эти значения на свои, которые вы определили с помощью команды `lsusb` ранее.

Для проверки извлеките и заново подключите модем. Если вы выполните команду `lsusb`, то может оказаться, что номер продукта или даже имя устройства могут поменяться (например, с `1446` на `1002`).

Если переключение модема прошло успешно, в `/dev` появится новое устройство с именем вида `ttyUSBn`, где *n* - число.

**Примечание:** Если у вас не появилось устройства с именем `ttyUSBn`, обратите внимание на устройства `ttyACMn`. Некоторые устройства "прописываются" под такими именами.

## Права на доступ к модему

Для использования модема через Network Manager необходимо, чтобы пользователь входил в группы network и networkmanager. Группа networkmanager по умолчанию в Arch Linux не создается. Её нужно добавить вручную.

## Дополнительные возможности

### Информация о настройках провайдеров

Для возможности выбора предустановленных настроек доступа для вашего провайдера установите пакет mobile-broadband-provider-info.

### Некоторые команды AT

**Tip:** Для работы с командами AT в Windows можно использовать HyperTerminal, а в Linux - minicom

**Важно:** Возможно, для вашего модема, команды задания режима будут другими.

1.  `AT^U2DIAG=0` - установить режим "модем"
2.  `AT^U2DIAG=1` - установить режим "модем + CD-ROM"
3.  `AT^U2DIAG=255` - установить режим "модем + CD-ROM + Card Reader"
4.  `AT^U2DIAG=256` - установить режим "модем + Card Reader"
5.  `AT+CPIN=<PIN-код>` - отправить PIN-код
6.  `AT+CUSD=1,<закодированный-в-PDU-код-USSD>,15` - отправить запрос USSD, результат (наверное) можно получить в `/dev/ttyUSB2`

### USSD

#### Huawei

Если вы являетесь обладателем модема Huawei, возможно, вас заинтересует пакет [huawei-ussd](https://aur.archlinux.org/packages/huawei-ussd/). Он позволит Вам отправлять запросы USSD с помощью модема (и, конечно же, получать ответы от оператора). Также можете взглянуть на аналогичную утилиту [ussd.php](https://github.com/gnomeby/ussd).

#### Ручной способ

**Примечание:** При отправке запросов USSD используется кодировка PDU

Чтобы закодировать запрос USSD в PDU, используйте команду:

```
perl -e '@a=split(//,unpack("b*","*Запрос USSD*")); for ($i=7; $i < $#a; $i+=8) { $a[$i]="" } print uc(unpack("H*", pack("b*", join("", @a))))."
"'

```

Чтобы раскодировать ответ на USSD-запрос, выполните:

```
perl -e 'print pack("H*", "*Полученный ответ на запрос USSD*");'

```

Некоторые операторы отправляют ответ в PDU. Чтобы извлечь текст ответа из такого сообщения, используйте команду:

```
perl -e '@a=split(//,unpack("b*", pack("H*","*Ответ в USSD*"))); for ($i=6; $i < $#a; $i+=7) {$a[$i].="0" } print pack("b*", join("", @a)).""'

```

### Понятные имена в /dev

Возможно, вам будет приятнее работать не с `ttyUSB0`, `ttyUSB1` и т.д., а с более понятными `ttyUSB_utps_modem`, `ttyUSB_utps_diag` и `ttyUSB_utps_pcui`. Для этого достаточно записать следующие правила **udev**:

**Важно:** Приведенные правила справедливы для модемов Huawei. Вам следует заменить **idVendor** и **idProduct** на свои:

	`SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v**idVendor**p**idProduct***" …`

```
SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1001*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="00", ATTRS{bInterfaceProtocol}=="ff", NAME="ttyUSB_utps_modem"
SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1001*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="01", ATTRS{bInterfaceProtocol}=="ff", NAME="ttyUSB_utps_diag"
SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1001*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="02", ATTRS{bInterfaceProtocol}=="ff", NAME="ttyUSB_utps_pcui"

```

```
SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1003*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="00", ATTRS{bInterfaceProtocol}=="ff", NAME="ttyUSB_utps_modem"
SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1003*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="01", ATTRS{bInterfaceProtocol}=="ff", NAME="ttyUSB_utps_pcui

```

### Отправка SMS

Для этого вы можете использовать [gammu](https://www.archlinux.org/packages/?name=gammu).

Подредактируйте `~/.gammurc`:

```
[gammu]
port=/dev/ttyUSB0
connection=at
name=huawei e1550
model=

```

Команда:

```
gammu sendsms TEXT *<номер телефона: +7..........>* -text *<текст сообщения>*

```

## Что дальше?

После того, как ваш 3G модем подключён, настроен - а значит доступен в `/dev`, его может использовать любая программа-звонилка. Выбор того или иного средства для подключения к Интернету зависит от ваших предпочтений: вы можете воспользоваться [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)"), [wvdial](/index.php/Wvdial_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wvdial (Русский)"), [gnome-ppp](https://www.archlinux.org/packages/?name=gnome-ppp) или любым другим.

Возможно, вас заинтересует способ подключения к Интернету с помощью **pppd**, он подробно описан в [этой статье](/index.php/3G_and_GPRS_modems_with_pppd_alone_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "3G and GPRS modems with pppd alone (Русский)").

## Ссылки

*   [3G and GPRS modems with pppd alone (Русский)](/index.php/3G_and_GPRS_modems_with_pppd_alone_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "3G and GPRS modems with pppd alone (Русский)")
*   [Wvdial (Русский)](/index.php/Wvdial_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wvdial (Русский)")