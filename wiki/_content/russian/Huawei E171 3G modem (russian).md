Ссылки по теме

*   [wvdial](/index.php/Wvdial "Wvdial")
*   [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection")
*   [3G and GPRS modems with pppd](/index.php/3G_and_GPRS_modems_with_pppd "3G and GPRS modems with pppd")

Это не статья, скорее небольшая заметка по использованию модема Huawei E171 без NetworkManager. Подключение осуществляется с помощью утилиты gnome-ppp, вместо которой можно использовать консольную утилиту wvdial.

## Contents

*   [1 Определение и переключение в режим модема](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
*   [2 Установка пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
*   [3 Подключение модема](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D0.B5.D0.BC.D0.B0)
*   [4 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Определение и переключение в режим модема

При подключении данное устройство определяется как CDROM, по-этому требуется его перед использованием переключить в режим модема. Подключаем модем и смотрим его заводские маркеры:

```
#lsusb
Bus 002 Device 009: ID 12d1:1446 Huawei Technologies Co., BLA-BLA-BLA

```

**Tip:** 12d1:1446 — Это как раз нужные нам значения.

## Установка пакетов

Для работы с модемом потребуются следующие пакеты:

```
local/usb_modeswitch 1.2.5-2
    Activating switchable USB devices on Linux.
local/gnome-ppp 0.3.23-8
    A GNOME 2 WvDial frontend
sudo pacman -Sy gnome-ppp usb_modeswitch

```

**Примечание:** В пакет usb_modeswitch входят наборы пресетов для переключения девайса в режим модема, они находятся в папке

/usr/share/usb_modeswitch/[МАРКЕР из lsusb]

Для включения модема вводим команду:

```
usb_modeswitch  -v 0x12d1 -p 0x1446 -c /usr/share/usb_modeswitch/12d1\:1446

```

И снова проверяем вывод lsusb:

```
#lsusb
Bus 002 Device 009: ID 12d1:1436 Huawei Technologies Co., BLA-BLA-BLA

```

Как видно из примера, значения изменились, что свидетельствует об успешном переключении устройства. Также должно было появиться устройство вида:

```
/dev/ttyUSB[0-9+]

```

## Подключение модема

Теперь можно запустить gnome-ppp, указать настройки и подключиться к сети. Настройки для Beeline

```
Логин  beeline
Пароль beeline
Номер  *99#

```

## Ссылки

*   [Оригинал](http://wilful.su/blog/linux/481.html)