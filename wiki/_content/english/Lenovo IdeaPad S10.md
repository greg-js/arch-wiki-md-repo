## Contents

*   [1 System Specification](#System_Specification)
*   [2 Wireless](#Wireless)
*   [3 Sound](#Sound)
*   [4 SD Card Reader](#SD_Card_Reader)

## System Specification

*   CPU: Intel Atom N270 (1.6 GHz) - works with i686 only
*   Memory: 512 MB internal - can be expanded to max of 2GB
*   WiFi: Broadcom BCM4312
*   Hard-Drive: 80GB standard with larger sizes available
*   Optical Drive: None
*   Integrated Graphics: Intel 945GME
*   Sound: Intel HDA (ICH7)
*   Screen: 10" LCD (1024x600)
*   SD Card Reader
*   Express Card 34 Slot
*   Webcam: Lenovo Easycam

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 3 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.1 IDE interface: Intel Corporation 82801G (ICH7 Family) IDE Controller (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
00:1f.3 SMBus: Intel Corporation 82801G (ICH7 Family) SMBus Controller (rev 02)
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM5906M Fast Ethernet PCI Express (rev 02)
05:00.0 Network controller: Broadcom Corporation BCM4312 802.11b/g (rev 01)

```

## Wireless

The Broadcom BCM4312 card requires the [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) module which is available in the [AUR](/index.php/AUR "AUR"). See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for details.

## Sound

Works out of the box but the internal microphone is not turned on by default. To make the internal microphone work, turn the capture channel on (using the spacebar in alsamixer if you are using that), unmute the internal microphone channel and turn it up.

## SD Card Reader

Works out of the box but you cannot boot from it.