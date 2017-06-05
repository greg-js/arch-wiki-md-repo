**Примечание:** Данная статья актуальна как для Lenovo thinkPad Edge E530, так и для E430.

## Contents

*   [1 Железо](#.D0.96.D0.B5.D0.BB.D0.B5.D0.B7.D0.BE)
    *   [1.1 Видео](#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE)
    *   [1.2 Ethernet](#Ethernet)
    *   [1.3 Wireless](#Wireless)
    *   [1.4 Сканер отпечатков пальцев](#.D0.A1.D0.BA.D0.B0.D0.BD.D0.B5.D1.80_.D0.BE.D1.82.D0.BF.D0.B5.D1.87.D0.B0.D1.82.D0.BA.D0.BE.D0.B2_.D0.BF.D0.B0.D0.BB.D1.8C.D1.86.D0.B5.D0.B2)
    *   [1.5 Картридер](#.D0.9A.D0.B0.D1.80.D1.82.D1.80.D0.B8.D0.B4.D0.B5.D1.80)
*   [2 Трэкпоинт](#.D0.A2.D1.80.D1.8D.D0.BA.D0.BF.D0.BE.D0.B8.D0.BD.D1.82)
*   [3 Fan-control](#Fan-control)
*   [4 tp_smapi](#tp_smapi)
*   [5 Информация об устройствах](#.D0.98.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F_.D0.BE.D0.B1_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0.D1.85)
    *   [5.1 Вывод lspci](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_lspci)
    *   [5.2 Вывод lsusb](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_lsusb)

## Железо

| Устройство | Работоспособность |
| Видео (Intel HD4000/Nvidia GTX 630) | Да |
| Ethernet (Realtek RTL8111/8168B) | Да |
| Wireless (Broadcom BCM4313 802.11b/g/n) | Да |
| Bluetooth | Да |
| Аудио (Intel HD Audio) | Да |
| Камера | Да |
| Сканер отпечатков пальцев | Да ([Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui")) |
| Картридер (Realtek RTS5229) | Да |

### Видео

При наличии дополнительной видеокарты **Nvidia GTX 630**, следует установить пакет [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Далее следовать инструкциям соответствующей страницы [вики](/index.php/Bumblebee "Bumblebee").

### Ethernet

Хотя, **Realtek RTL8111/8168B** работает корректно со стандартным модулем **r8169**, в некоторых случаях рекомендуется установить модуль [r8168](https://www.archlinux.org/packages/?name=r8168), доступный в [официальном репозитории](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

```
# pacman -S r8168

```

После установки потребуется выгрузить модуль **r8169** и загрузить установленный. Также, модуль [r8168](https://www.archlinux.org/packages/?name=r8168) конфликтует с модулем **r8169**, поэтому также следует добавить последний в **blacklist**:

```
# rmmod r8169
# modprobe r8168
# echo "blacklist r8169" > /etc/modprobe.d/r8169_blacklist.conf

```

### Wireless

Сетевая карта **Broadcom BCM4313** работает с модулем **brcmsmac** "из коробки". Однако, при работе с этим модулем устройство находится в режиме энергосбережения, что приводит к плохому приему сигнала и малому радиусу видимости сетей. Рекомендуется установить проприетарный драйвер для карточки из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"):

```
# yaourt -S broadcom-wl

```

Затем загрузить установленный модуль:

```
# modprobe wl

```

Добавлять модули **b43** и **brcmsmac** в **blacklist** нет необходимости, так как пакет [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) уже содержит нужный файл. Следует также заметить, что данная сетевая карта с модулем **b43** **не работает**.

### Сканер отпечатков пальцев

Работает корректно с [fingerprint-gui](https://aur.archlinux.org/packages/fingerprint-gui/). Следует установить соответствующий пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"):

```
# yaourt -S fingerprint-gui

```

Далее следовать инструкциям соответствующей страницы [вики](/index.php/Fingerprint-gui "Fingerprint-gui"). Адрес устройства можно посмотреть, выполнив команду:

```
# lsusb | grep Upek
Bus 001 Device 004: ID 147e:1002 Upek

```

### Картридер

**Примечание:** При использовании ядра версии >3.8 драйвер работает "из коробки". Устройства будут определяться, как **/dev/mmcX**.

Картридер **не работает** "из коробки". Для корректной работы следует установить пакет [rts5229](https://aur.archlinux.org/packages/rts5229/) и выполнить команду `modprobe rts5229`.

## Трэкпоинт

Трэкпоинт работает "из коробки", однако отсутствует возможность прокрутки. Для того, чтобы ее включить в X при зажатии средней клавиши тачпада, необходимо создать файл:

 `/etc/X11/xorg.conf.d/20-thinkpad.conf` 
```
Section "InputClass"
	Identifier	"Trackpoint Wheel Emulation"
	MatchProduct	"TPPS/2 IBM TrackPoint"
	MatchDevicePath	"/dev/input/event*"
	Option		"EmulateWheel"		"true"
	Option		"EmulateWheelButton"	"2"
	Option		"Emulate3Buttons"	"false"
	Option		"XAxisMapping"		"6 7"
	Option		"YAxisMapping"		"4 5"
EndSection

```

## Fan-control

**Важно:** [Сообщается](https://bbs.archlinux.org/viewtopic.php?id=151028), что Thinkfan в настоящий момент на данной модели не работает.

Для работы с кулером необходимо добавить опцию к модулю **thinkpad_acpi**:

 `/etc/modprobe.d/modprobe.conf`  `options thinkpad_acpi fan_control=1` 

и отредактировать файл настроек:

 `/etc/thinkfan.conf`  `sensor /sys/devices/platform/coretemp.0/temp1_input` 

Управление кулером осуществляется записью в соответствующие файлы:

```
# echo engage > /proc/acpi/ibm/fan
# echo level auto > /proc/acpi/ibm/fan
# echo level 1 > /proc/etc/ibm/fan

```

Доступные параметры можно посмотреть, вызвав:

```
# cat /proc/acpi/ibm/fan

```

## tp_smapi

Стандартный модуль [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) в настоящее время не поддерживает настройку батареи на данной модели. Для настройки режима зарядки следует установить из [пользовательского репозитория](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") пакет [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat):

```
# yaourt -S tpacpi-bat

```

Затем отредактировать (по желанию) файл настроек:

 `/usr/lib/systemd/system/tpacpi-bat.service` 
```
[Unit]
Description=sets battery thresholds
[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/tpacpi-bat -s ST 0 35
ExecStart=/usr/bin/tpacpi-bat -s SP 0 85
[Install]
WantedBy=multi-user.target
```

где для параметра **ST** выставить желаемое значение заряда батареи, при котором она начнет заряжаться (35%), а для параметра **SP** - при котором перестанет (85%). Затем, при необходимости изменения настроек выполнить:

```
# systemctl start tpacpi-bat.service

```

Включать сервис при каждой загрузке нет необходимости. Для подробностей обратитесь к соответствующей странице [вики](/index.php/Tp_smapi "Tp smapi").

## Информация об устройствах

### Вывод lspci

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200/2nd Generation Core Processor Family PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 VGA compatible controller: NVIDIA Corporation Device 1058 (rev a1)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5229 PCI Express Card Reader (rev 01)
03:00.0 Network controller: Broadcom Corporation BCM4313 802.11b/g/n Wireless LAN Controller (rev 01)
0c:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 07)

```

### Вывод lsusb

```
Bus 003 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 004 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 003: ID 0a5c:21f4 Broadcom Corp. 
Bus 003 Device 004: ID 147e:1002 Upek 
Bus 004 Device 003: ID 05ca:1823 Ricoh Co., Ltd

```