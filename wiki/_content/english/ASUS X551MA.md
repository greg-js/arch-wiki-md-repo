## Contents

*   [1 Model](#Model)
*   [2 Hardware](#Hardware)
    *   [2.1 lspci](#lspci)
    *   [2.2 lsusb](#lsusb)
*   [3 Settings](#Settings)
    *   [3.1 Video](#Video)
    *   [3.2 LAN](#LAN)
    *   [3.3 Wi-fi](#Wi-fi)
    *   [3.4 Audio](#Audio)
    *   [3.5 Touchpad](#Touchpad)
    *   [3.6 Brightness](#Brightness)
    *   [3.7 Webcam](#Webcam)
    *   [3.8 Bluetooth](#Bluetooth)
    *   [3.9 Card Reader](#Card_Reader)
*   [4 Dual boot with Windows](#Dual_boot_with_Windows)

## Model

X551MA-SX056D

## Hardware

*   CPU: Intel(R) Pentium(R) CPU N3520 @ 2.16GHz (quad core)
*   RAM: DDR3 1333MHz 4096 MB
*   SCREEN: 15.6"
*   VIDEO: Intel GMA HD 1366x768
*   HDD: 500 GB TOSHIBA MQ01ABF050 5400R SATA
*   Wi-fi: BCM943142HM 802.11b/g/n (+ Bluetooth 4.0)
*   Network: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 06)
*   DVD-RW
*   1xUSB 2.0, 1xUSB 3.0, 1xHDMI, 1xD-sub, 1xEthernet, Cardreader, Camera

### lspci

```
00:00.0 Host bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0c)
00:13.0 SATA controller: Intel Corporation Atom Processor E3800 Series SATA AHCI Controller (rev 0c)
00:1a.0 Encryption controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine (rev 0c)
00:1b.0 Audio device: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller (rev 0c)
00:1c.0 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 1 (rev 0c)
00:1c.1 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 2 (rev 0c)
00:1c.3 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 4 (rev 0c)
00:1d.0 USB controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB EHCI (rev 0c)
00:1f.0 ISA bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit (rev 0c)
00:1f.3 SMBus: Intel Corporation Atom Processor E3800 Series SMBus Controller (rev 0c)
02:00.0 Network controller: Broadcom Corporation BCM43142 802.11b/g/n (rev 01)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5286 PCI Express Card Reader (rev 01)
03:00.2 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 06)

```

### lsusb

```
Bus 001 Device 005: ID 04f2:b404 Chicony Electronics Co., Ltd 
Bus 001 Device 002: ID 8087:07e6 Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Settings

### Video

For Intel GMA HD install: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)

### LAN

Works out of the box

### Wi-fi

Install from AUR: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) or (better) [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)

### Audio

Works out of the box. KDE: Install [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix)

### Touchpad

Works out of the box

### Brightness

fn + F5 / fn + F6 - control brightness. Kernel parameter: `acpi_osi= acpi_backlight=native` For example for the systemd-boot EFI boot manager:

```
# cat /boot/loader/entries/arch.conf 
title   Arch Linux
linux   /vmlinuz-linux
initrd  /initramfs-linux.img
options root=PARTUUID=dfe3c3a3-ea61-4440-ba0a-2b29267298cb rw acpi_osi= acpi_backlight=native

```

KDE: install [powerdevil](https://www.archlinux.org/packages/?name=powerdevil)

### Webcam

Works out of the box. Tested at online webcam tester in Chromium.

### Bluetooth

Bluetooth 4.0 is in combo wireless chip BCM43142.

Install: [bluez](https://www.archlinux.org/packages/?name=bluez) and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)

```
$ dmesg|grep -i bluetooth
[   21.959501] Bluetooth: Core ver 2.21
[   21.959527] Bluetooth: HCI device and connection manager initialized
[   21.959533] Bluetooth: HCI socket layer initialized
[   21.959536] Bluetooth: L2CAP socket layer initialized
[   21.959554] Bluetooth: SCO socket layer initialized
[   22.020034] Bluetooth: hci0: BCM: chip id 70
[   22.036791] Bluetooth: hci0: thinkbali
[   22.036795] Bluetooth: hci0: BCM (001.001.011) build 0172
[   22.102001] bluetooth hci0: Direct firmware load for brcm/BCM.hcd failed with error -2
[   22.102007] Bluetooth: hci0: BCM: Patch brcm/BCM.hcd not found
[   25.435436] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[   25.435438] Bluetooth: BNEP filters: protocol multicast
[   25.435444] Bluetooth: BNEP socket layer initialized

```

In spite of `hci0: BCM: Patch brcm/BCM.hcd not found` the bluetooth module works:

```
# hciconfig -a
hci0:   Type: Primary  Bus: USB
       BD Address: A4:DB:30:BB:2F:C1  ACL MTU: 1021:8  SCO MTU: 64:1
       DOWN 
       RX bytes:872 acl:0 sco:0 events:35 errors:0
       TX bytes:383 acl:0 sco:0 commands:35 errors:0
       Features: 0xff 0xfe 0xcf 0xfe 0xdb 0xff 0x7b 0x87
       Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
       Link policy: RSWITCH HOLD SNIFF 
       Link mode: SLAVE ACCEPT 

```

```
# hciconfig hci0 up
# hciconfig -a
hci0:   Type: Primary  Bus: USB
       BD Address: A4:DB:30:BB:2F:C1  ACL MTU: 1021:8  SCO MTU: 64:1
       UP RUNNING PSCAN ISCAN 
       RX bytes:1488 acl:0 sco:0 events:72 errors:0
       TX bytes:1091 acl:0 sco:0 commands:72 errors:0
       Features: 0xff 0xfe 0xcf 0xfe 0xdb 0xff 0x7b 0x87
       Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
       Link policy: RSWITCH HOLD SNIFF 
       Link mode: SLAVE ACCEPT 
       Name: 'thinkbali'
       Class: 0x00010c
       Service Classes: Unspecified
       Device Class: Computer, Laptop
       HCI Version: 4.0 (0x6)  Revision: 0xac
       LMP Version: 4.0 (0x6)  Subversion: 0x210b
       Manufacturer: Broadcom Corporation (15)

```

Sometimes it is needed to run:

```
# rfkill unblock bluetooth

```

[blueman](https://www.archlinux.org/packages/?name=blueman) works correctly.

Here [https://forum.libreelec.tv/post-12512.html](https://forum.libreelec.tv/post-12512.html) I've found a firmware for BCM43142 - BCM.hcd.

```
# unzip BCM.zip
# cp BCM.hcd /lib/firmware/brcm/

```

After restart:

```
$ dmesg|grep -i bluetooth
[   21.606725] Bluetooth: Core ver 2.21
[   21.606750] Bluetooth: HCI device and connection manager initialized
[   21.606758] Bluetooth: HCI socket layer initialized
[   21.606762] Bluetooth: L2CAP socket layer initialized
[   21.606771] Bluetooth: SCO socket layer initialized
[   21.663192] Bluetooth: hci0: BCM: chip id 70
[   21.679212] Bluetooth: hci0: thinkbali
[   21.679218] Bluetooth: hci0: BCM (001.001.011) build 0172
[   22.414606] Bluetooth: hci0: BCM (001.001.011) build 0172
[   22.430520] Bluetooth: hci0: Broadcom Bluetooth Device (43142)
[   25.208811] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[   25.208814] Bluetooth: BNEP filters: protocol multicast
[   25.208822] Bluetooth: BNEP socket layer initialized

```

But I felt no any difference without or with firmware.

### Card Reader

Works out of the box. Tested with SD card 512 Mb.

## Dual boot with Windows

To boot Windows 7 it is needed to switch on `CSM` at BIOS. Otherwise Windows boot hangs at logo. Set the BIOS setting `OS Selection` in the `Advanced` menu to `Windows 7`.