Related articles

*   [Install from a USB flash drive](/index.php/Install_from_a_USB_flash_drive "Install from a USB flash drive")
*   [Laptop](/index.php/Laptop "Laptop")

## Contents

*   [1 Installation](#Installation)
*   [2 Xorg](#Xorg)
*   [3 Touchpad](#Touchpad)
*   [4 Camera](#Camera)
*   [5 Wireless](#Wireless)
*   [6 Hot keys](#Hot_keys)
*   [7 Hardware](#Hardware)
    *   [7.1 lspci](#lspci)
    *   [7.2 lsusb](#lsusb)

## Installation

To boot from a USB stick, disable **boot booster** in BIOS Setup.

## Xorg

[Install](/index.php/Install "Install") the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package.

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

## Camera

Supported by stock kernel, see [Webcam Software](/index.php/Webcam_setup#Webcam_configuration "Webcam setup")

## Wireless

*   AR9281/PCIe Full MiniCard 91, Single band 1x2 configuration

## Hot keys

| Hotkey | Action | Notes |
| Fn+F1 | Sleep |
| Fn+F2 | Wifi | *Atheros Communications Inc. AR928X Wireless Network Adapter* (uses the [ath9k](/index.php/Wireless_network_configuration#ath9k "Wireless network configuration") module) |
| Fn+F5/F6 | Brightness | BIOS v1504 has controlled it. |
| Fn+F10/F11/F21 | Volume Mute/Lower/Raise | Setup required, see [Acpid](/index.php/Acpid "Acpid") |

## Hardware

### lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev  03)00:00.0 Host bridge: Intel Corporation Mobile 945GSE Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GSE Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation NM10/ICH7 Family High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation NM10/ICH7 Family PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation NM10/ICH7 Family PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation NM10/ICH7 Family PCI Express Port 3 (rev 02)
00:1d.0 USB controller: Intel Corporation NM10/ICH7 Family USB UHCI Controller #1 (rev 02)
00:1d.1 USB controller: Intel Corporation NM10/ICH7 Family USB UHCI Controller #2 (rev 02)
00:1d.2 USB controller: Intel Corporation NM10/ICH7 Family USB UHCI Controller #3 (rev 02)
00:1d.3 USB controller: Intel Corporation NM10/ICH7 Family USB UHCI Controller #4 (rev 02)
00:1d.7 USB controller: Intel Corporation NM10/ICH7 Family USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7-M Family) SATA Controller [IDE mode] (rev 02)
00:1f.3 SMBus: Intel Corporation NM10/ICH7 Family SMBus Controller (rev 02)
01:00.0 Network controller: Qualcomm Atheros AR928X Wireless Network Adapter (PCI-Express) (rev 01)
02:00.0 Ethernet controller: Qualcomm Atheros AR8121/AR8113/AR8114 Gigabit or Fast Ethernet (rev b0)

```

### lsusb

```
Bus 001 Device 004: ID 04f2:b036 Chicony Electronics Co., Ltd Asus Integrated 0.3M UVC Webcam
Bus 001 Device 002: ID 058f:6366 Alcor Micro Corp. Multi Flash Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

```