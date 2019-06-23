<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Определение устройства](#Определение_устройства)
    *   [1.1 pwc](#pwc)
    *   [1.2 qc-usb](#qc-usb)
    *   [1.3 qc-usb-messenger](#qc-usb-messenger)
    *   [1.4 zr364xx](#zr364xx)
    *   [1.5 sn9c102](#sn9c102)
    *   [1.6 spca5xx](#spca5xx)
    *   [1.7 stv680](#stv680)
    *   [1.8 linux-uvc](#linux-uvc)
    *   [1.9 ov51x-jpeg](#ov51x-jpeg)
    *   [1.10 r5u870 (Ricoh)](#r5u870_(Ricoh))
    *   [1.11 stk11xx (Syntek)](#stk11xx_(Syntek))

# Определение устройства

Определите название вашей камеры и найдите драйвер. Если вы заставили её работать, то добавьте название и драйвер, который она использует в список!

## pwc

*   Creative Labs Webcam Pro Ex
*   Logitech QuickCam Notebook Pro (только модели серии "Pro")
*   Logitech Quickcam Pro 4000
*   Philips ToUCams (не поддерживаются на данный момент, но используют pwc driver если я правильно помню)

## [qc-usb](/index.php?title=Retrieving_Qc-usb_drivers_HOWTO&action=edit&redlink=1 "Retrieving Qc-usb drivers HOWTO (page does not exist)")

*   Dexxa Webcam
*   Labtec Webcam (old model)
*   LegoCam
*   Logitech Quickcam Express (old model)
*   Logitech QuickCam Notebook (not the "Pro" models)
*   Logitech Quickcam Web

## qc-usb-messenger

*   Logitech Quickcam Messenger
*   Logitech Quickcam Communicate

Сейчас поддерживаются в репозитории community.

**NOTE:** Если qc-usb-messenger не заработал, то используйте gspca module, из пакета gspcav1 . **NOTE:** Сейчас этот драйвер существует как модуль к ядру 2.6.27

## zr364xx

Этот драйвер может быть использован для многих камер:

*   Aiptek PocketDV 3300
*   Creative PC-CAM 880
*   Konica Revio 2
*   Genius Digital Camera
*   Maxell Maxcam PRO DV3

Тут приведен полный список поддерживаемых устройст [here](http://royale.zerezo.com/zr364xx/). Вы можете найти PKGBUILD для этого драйвера здесь [AUR](https://aur.archlinux.org/).

## sn9c102

*   Trust Spacecam series
*   Maxell Smartcam (for notebooks): 352x288 max. resolution @ 3fps

## spca5xx

Полный список поддерживаемых устройств [здесь](http://mxhaard.free.fr/spca5xx.html).

*   Logitech QuickCam IM
*   Logitech QuickCam for Notebooks Deluxe
*   Labtec Webcam Pro
*   Trust Mini Webcam WB-1200p

Ядра >= 2.6.11 сейчас могут использовать gspca модуль, установленный из пакета gspcav1 .

## stv680

Множество дешевых камер, не имеющих названия, пришедших из азии в большенстве случаев используют чипсет stv680 ( Pencam, SpyC@m and LegoCam).

*   Aiptek PenCam series
*   Digitaldream series
*   Dolphin Peripherals series
*   Lego LegoCam
*   Trust SpyC@m series
*   Welback Coolcam

Более подробный список устройств, работающих на чипе stv680 доступен [здесь](http://webcam-osx.sourceforge.net/cameras/index.php?orderBy=controller).

## linux-uvc

*   Logitech Quickcam Pro 5000
*   Logitech Quickcam Pro 9000
*   Logitech Quickcam Orbit MP
*   Logitech, Inc. Webcam C270 (ID 046d:0825)
*   Microdia Pavilion Webcam (on MSI PR200)

Полный список устройств с поддержкой UVC [здесь](http://linux-uvc.berlios.de/).

Пакет **linux-uvc-svn-all** доступен в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

Note: Этот драйвер не поддерживает V4L1 .

## ov51x-jpeg

*   Sony EyeToy
*   Chicony DC-2120
*   Chicony DC-2120 pro
*   Trust Spacecam 320
*   Hercules Webcam Deluxe
*   Hercules Webcam Classic
*   Creative Live! Cam Notebook Pro VF0400
*   Creative Live! Cam Vista IM
*   Creative Live! Cam Vista IM VF0420
*   Creative Vista Webcam VF0330
*   ASUS webcam Model?
*   Philips PCVC820K/00
*   NGS showtime plus
*   HP VGA Webcam with Integrated Microphone

Модуль ядра можно найти в AUR . Смотрите [здесь](http://www.rastageeks.org/ov51x-jpeg/index.php/Main_Page)

Для работы "Creative Live! Cam Vista IM" добавьте в /etc/modprobe.d/modprobe.conf строку:

```
options ov51x-jpeg forceblock=1

```

## r5u870 (Ricoh)

*   HP Pavilion Webcam
*   HP Webcam 1000
*   Sony VAIO VGP-VCCx

The Ricoh webcam встроены в большинство ноутбуков Sony. Существует [драйвер](https://aur.archlinux.org/packages.php?ID=15227) от произвоидителя (Сперва установите) и [драйвер](https://aur.archlinux.org/packages.php?ID=15226) в AUR.

## stk11xx (Syntek)

*   Встроенные камеры в большинство ноутбуков фирмы Asus
*   Asus A8J, F3S, F5R, VX2S, V1S, A6T

Просто установите [этот](https://aur.archlinux.org/packages.php?do_Details=1&ID=12669) AUR пакет. Он содержит нужный модуль ядра.