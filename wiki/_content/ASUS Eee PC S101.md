# ASUS Eee PC S101

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:ASUS Eee PC S101#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_S101))

For now, this is just some notes on the Asus EeePC S101.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 boot loader setup of Kernel](#boot_loader_setup_of_Kernel)
*   [2 Wireless](#Wireless)
*   [3 Xorg](#Xorg)
*   [4 Touchpad](#Touchpad)
*   [5 ACPI](#ACPI)
    *   [5.1 Touchpad toggle - Silver Button](#Touchpad_toggle_-_Silver_Button)
    *   [5.2 Sleep Fn+F1](#Sleep_Fn.2BF1)
    *   [5.3 Wifi Fn+F2](#Wifi_Fn.2BF2)
    *   [5.4 Brightness Fn+F5/F6](#Brightness_Fn.2BF5.2FF6)
    *   [5.5 Camera Fn+F7](#Camera_Fn.2BF7)
*   [6 extend battery life](#extend_battery_life)
    *   [6.1 Notes](#Notes)
*   [7 Hardware](#Hardware)
    *   [7.1 lspci](#lspci)
    *   [7.2 lsusb](#lsusb)

# Installation

*   Download from [https://www.archlinux.org/download/](https://www.archlinux.org/download/), (ex. archlinux-2010.05-netinstall-i686.iso because EEE PC is 32 bit machine.
*   Refer [Install from a USB flash drive](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive") to write iso file into USB stick.(ex. UNetBootin under windows)
*   Disable **boost boot** in BIOS Setup to allow USB stick bootable at boot time.
*   Follow [Installation guide](/index.php/Installation_guide "Installation guide") to install till reboot.
*   Follow [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") to install your hardware driver and desktop.
*   remember to add **hal** in DAEMONS line of /etc/rc.conf , it will automatic detect all hardware.

```
/etc/rc.d/hal start  # detect and install all hardware

```

## boot loader setup of Kernel

I just use standard kernel. eeepc_wmi module will be loaded. Note: add acpi_osi=Linux line in kernel boot loader, to let eeepc_laptop module loading. Otherwise Fn+F2 won't workable.

# Wireless

The card is a Atheros Communications Inc. AR928X Wireless Network Adapter (module: ath9k) It is automatic detected by **hal**.

# Xorg

About the Video(Intel 945GME), It is automatic detected by **hal**.

# Touchpad

It is automatic detected by **hal**.

*   install **xf86-input-synaptics**

# ACPI

big_gie created a acpi package to support the acpi events: [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/)<sup><small>AUR</small></sup>. This package was inspired by many others.

## Touchpad toggle - Silver Button

edit /etc/conf.d/acpi-eeepc-generic.conf

```
COMMANDS_BUTTON_BLANK=("/etc/acpi/eeepc/acpi-eeepc-generic-toggle-touchpad.sh")

```

## Sleep Fn+F1

Fn+F1 or closing lid should put the eee pc to sleep. It calls "acpi-eeepc-generic-suspend2ram.sh".

## Wifi Fn+F2

Pressing Fn+F2 will call "acpi-eeepc-generic-wifi-toggle.sh" which will toggle the wireless card. Be sure to load "rfkill" module for this to work. edit /etc/conf.d/acpi-eeepc-generic.conf

```
WIFI_DRIVERS=("ath9k")

```

## Brightness Fn+F5/F6

BIOS v1504 has controlled it.

## Camera Fn+F7

edit /etc/conf.d/acpi-eeepc-generic.conf:

```
COMMANDS_SCREEN_OFF=(/etc/acpi/eeepc/acpi-eeepc-generic-toggle-webcam.sh)

```

To use the camera, install mplayer or luvcview.

```
luvcview -f yuv
mplayer -vf screenshot -fps 30 tv://  # press 's' to capture

```

# extend battery life

*   install **cpufreq**
*   edit /etc/rc.conf

```
MODULES=(... acpi-cpufreq cpufreq_ondemand cpufreq_powersave)
DAEMONS=(... cpufreq)

```

*   edit /etc/conf.d/cpufreq

```
governor="ondemand"
min_freq="800MHz"
max_freq="1.5GHz"

```

ref: [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")

## Notes

# Hardware

## lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev  03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation N10/ICH 7 Family High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 3 (rev 02)
00:1d.0 USB Controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation N10/ICH 7 Family USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
00:1f.3 SMBus: Intel Corporation N10/ICH 7 Family SMBus Controller (rev 02)
01:00.0 Network controller: Atheros Communications Inc. AR928X Wireless Network Adapter (PCI-Express) (rev 01)
02:00.0 Ethernet controller: Atheros Communications AR8121/AR8113/AR8114 Gigabit or Fast Ethernet (rev b0)

```

## lsusb

```
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 002: ID 058f:6366 Alcor Micro Corp. Multi Flash Reader
Bus 001 Device 003: ID 04f2:b036 Chicony Electronics Co., Ltd Asus Integrated 0.3M UVC Webcam

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_S101&oldid=408676](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_S101&oldid=408676)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")