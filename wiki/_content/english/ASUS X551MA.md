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

Install from AUR: [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)

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

Doesn't work out of the box

### Bluetooth

Not tested yet

### Card Reader

Works out of the box. Tested with SD card 512 Mb

## Dual boot with Windows

To boot Windows 7 it is needed to switch on CSM at BIOS. Otherwise Windows boot hangs at logo.