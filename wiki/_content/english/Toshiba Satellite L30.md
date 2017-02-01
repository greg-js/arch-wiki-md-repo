This document applies in particular to Arch Linux on a Toshiba Satellite L30/L35 PSL33U series. This document may help you solving some issues of this laptop.

## Contents

*   [1 Specification](#Specification)
*   [2 GPU](#GPU)
*   [3 Wi-Fi](#Wi-Fi)
*   [4 Ethernet](#Ethernet)
*   [5 Modem](#Modem)
*   [6 PCMCIE](#PCMCIE)
*   [7 Touchpad](#Touchpad)
*   [8 HDD](#HDD)
*   [9 CD/DVD](#CD.2FDVD)
*   [10 Audio issues](#Audio_issues)
*   [11 Hybernate/Suspent](#Hybernate.2FSuspent)
*   [12 Desktop Environment](#Desktop_Environment)
*   [13 HTPC use](#HTPC_use)

## Specification

Originally this is Intel Celeron M440 single core processor, 1024MB of RAM, ATI X200m 128MB video card, 80GB HDD, Atheros AR2413/AR2414 Wireless Network Adapter 54mb b/g, two USB ports, one PCMCIA card port type II, Synaptics touchpad, 100Mb Ethernet Lan, V.92 modem, DVD drive.

Processor can be upgraded up to Intel Core 2 Duo T2450 2.0GHz for x86 system, or even Intel Core 2 Duo T7200 2.0GHz for x64 system. Processor upgrade gives you much performance improvements. T7200 processor works @ 1600MHz due to 533MHz system clock.

Officialy L30 can handle up to 2GB of RAM, but it works with 3GB of RAM too(2+1). DO NOT WORKS with 2+2GB or RAM.

Details from "lspci" in my case(not stock):

`
```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD/ATI] RC410 Host Bridge (rev 01)
00:01.0 PCI bridge: Advanced Micro Devices, Inc. [AMD/ATI] RC4xx/RS4xx PCI Bridge [int gfx]
00:12.0 IDE interface: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 Serial ATA Controller (rev 80)
00:13.0 USB controller: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 USB Host Controller (rev 80)
00:13.1 USB controller: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 USB Host Controller (rev 80)
00:13.2 USB controller: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 USB2 Host Controller (rev 80)
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 SMBus Controller (rev 82)
00:14.1 IDE interface: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 IDE Controller (rev 80)
00:14.2 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 High Definition Audio Controller (rev 01)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 PCI-ISA Bridge (rev 80)
00:14.4 PCI bridge: Advanced Micro Devices, Inc. [AMD/ATI] IXP SB4x0 PCI-PCI Bridge (rev 80)
01:05.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] RC410M [Mobility Radeon Xpress 200M]
09:01.0 CardBus bridge: ENE Technology Inc CB1410 Cardbus Controller (rev 01)
09:02.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8100/8101L/8139 PCI Fast Ethernet Adapter (rev 10)
09:04.0 Ethernet controller: Qualcomm Atheros AR2413/AR2414 Wireless Network Adapter [AR5005G(S) 802.11bg] (rev 01)
0a:00.0 USB controller: NEC Corporation OHCI USB Controller (rev 43)
0a:00.1 USB controller: NEC Corporation OHCI USB Controller (rev 43)
0a:00.2 USB controller: NEC Corporation uPD72010x USB 2.0 Controller (rev 04)

```
`

## GPU

AMD/ATI Mobility Radeon Xpress 200M 128MB works well with xf86-video-ati driver. Recomended to install mesa-vdpau and opencl-mesa for better video performance. Can play 720p and some 1080p with mpv player or kodi, but only after processor upgrade.

## Wi-Fi

Atheros AR2413/AR2414 Wireless Network Adapter 802.11bg has issues, can cause random system freezes, web browsing problems. Can be fixed by adding conf file to `/etc/modprobe.d` directory, for example `/etc/modprobe.d/ath5k.conf`:

`
```
options ath5k nohwcrypt=1

```
`

Unfortunately this fix works not so good. Best solution change wi-fi card. For example to this: `Network controller: Qualcomm Atheros AR922X Wireless Network Adapter (rev 01)` It is 300Mbit N wifi card, but with this card some hardware modifications is needed to work second USB port, because Atheros AR9223 is much bigger then AR2413/2414\. Vertical 4 pin usb socket must be replaced with 4 pin horizontal socket on motherboard.

## Ethernet

Works out of the box perfectly.

## Modem

Not tested

## PCMCIE

Works. Best solution to add 2 more USB ports to your laptop. PCMCIA card with NEC Corporation uPD72010x USB 2.0 chip.

## Touchpad

Synaptics touchpad works well.

## HDD

SATA HDD, can be replaced with SSD. First-generation SATA interface, now known as SATA 1.5 Gbit/s, communicate at a rate of 1.5 Gbit/s, so SSD speed limited.

## CD/DVD

CD/DVD drive can/MUST be raplaces with optibay to support second HDD.

## Audio issues

Internal speakers may be muted after using headphones/expernal speakers. To fix this problem comment `#load-module module-switch-on-port-available` in `/etc/pulse/default.pa`

## Hybernate/Suspent

Do not work properly. Don't know fix yet.

## Desktop Environment

Please choose one of with for better performance: - Openbox - LXDE - MATE

Gnome, KDE and others are too heavy for comfortable experience.

## HTPC use

Can be used as HTPC with Kodi standalone session.