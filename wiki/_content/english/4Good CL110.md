This article serves as a temporal indexing directory for the issues of running Arch Linux on 4GOOD CL110 Cloudbook until there's time to improve, and possibly rewrite it.

## Contents

*   [1 Hardware](#Hardware)
*   [2 Installing](#Installing)
*   [3 CPU](#CPU)
    *   [3.1 cpufreq](#cpufreq)
*   [4 Init](#Init)
*   [5 UEFI](#UEFI)
*   [6 Multimedia](#Multimedia)
    *   [6.1 Audio](#Audio)
    *   [6.2 Video](#Video)
    *   [6.3 Webcam](#Webcam)
*   [7 Networking](#Networking)
    *   [7.1 Wireless](#Wireless)
*   [8 Input](#Input)
    *   [8.1 Touchpad](#Touchpad)
*   [9 See also](#See_also)

## Hardware

*   CPU: Intel Atom Z3735F, 4 cores, up to 1.83 GHz
*   RAM: 2048 Mb, DDR3L-RS 1333 Mhz, integrated
*   eMMC: 32GB
*   GPU: Intel HD Graphics Gen7 4EU, Valleyview, 620 MHz, up to 1268 MB(drawn from the mainboard RAM)
*   LCD: 1366x768, 11.6" widescreen
*   WLAN: Realtek RTL8723BS , 802.11 b/g/n SDIO
*   CAM: 0.3 Mpix
*   BAT: LI-ON 10000 mAh, 5-7 hours. Uses 3.5 DC-jack.
*   Bluetooth 4.0, microSD card reader(64GB), 2x USB 2.0, miniHDMI
*   Touchpad:

## Installing

## CPU

### cpufreq

## Init

Section coming soon... In short - switch over from systemd to OpenRC Use [this website](http://systemd-free.org/) as a guide.

A flawless [migration guide](http://systemd-free.org/migrate.php) It's actually pretty flawed, so this article *should* address some of the out-of-date issues

## UEFI

This model has a 32bit UEFI [32bit UEFI boot image instructions](https://git.archlinux.org/archiso.git/tree/docs/README.transfer#n105)

## Multimedia

### Audio

Audio is supported through ALSA with virtually no configuration. Following the [ALSA](/index.php/ALSA "ALSA") article should cover all that is needed.

### Video

The on-board graphics uses the Intel driver. [Install](/index.php/Install "Install") [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

Aside from that, there are no out-of-the-ordinary configuration steps. Consult [Xorg](/index.php/Xorg "Xorg") and [Intel](/index.php/Intel "Intel") for more information.

### Webcam

The webcam should be supported through the `uvcvideo` module by default, if not:

```
# modprobe uvcvideo

```

## Networking

### Wireless

See [#See also](#See_also)

## Input

### Touchpad

## See also

*   [On system hangs](https://bbs.archlinux.org/viewtopic.php?pid=1681385) - in case you are experiencing system freezes
*   [Similar hardware setup, r8723bs wireless](https://bbs.archlinux.org/viewtopic.php?id=203180)
*   [A github page dedicated to the driver](https://github.com/hadess/rtl8723bs)
*   [Generic r8723bs issues thread on Ubuntu forums](https://ubuntuforums.org/archive/index.php/t-2249936.html)
*   [Generic building guide for r8723bs driver](https://github.com/hadess/rtl8723bs/wiki/RTL8723BS-module-building-instruction-for-Debian-GNU-Linux)