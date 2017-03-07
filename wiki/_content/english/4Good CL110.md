This article serves as a temporal indexing directory for the issues of running Arch Linux on 4GOOD CL110 Cloudbook until there's time to improve, and possibly rewrite it. As much as it would be desirable to keep this article wikified - I am afraid that it will have to stay informal for the time being.

## Contents

*   [1 Hardware](#Hardware)
*   [2 Installing](#Installing)
*   [3 UEFI](#UEFI)
    *   [3.1 Init-related hard-freezes](#Init-related_hard-freezes)
*   [4 CPU](#CPU)
    *   [4.1 CPU-related hard-freezes](#CPU-related_hard-freezes)
    *   [4.2 cpufreq](#cpufreq)
*   [5 Multimedia](#Multimedia)
    *   [5.1 Audio](#Audio)
    *   [5.2 Video](#Video)
    *   [5.3 Webcam](#Webcam)
*   [6 Networking](#Networking)
    *   [6.1 Wireless](#Wireless)
*   [7 Input](#Input)
    *   [7.1 Touchpad](#Touchpad)
*   [8 See also](#See_also)

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

## UEFI

This model has a 32bit UEFI [32bit UEFI boot image instructions](https://git.archlinux.org/archiso.git/tree/docs/README.transfer#n105) After that the process is pretty straightforward and the installation is no different to that of a normal Arch system.

### Init-related hard-freezes

The deal with init system is ugly. System experiences a hard(unrecoverable freeze) soon after being booted(5-20 seconds), probably due to some delayed service startup. The problem lies in the systemd, and as of 2017/01/10 it was still there. Section coming soon... In short - switch over from systemd to OpenRC Use [this website](http://systemd-free.org/) as a guide.

A flawless [migration guide](http://systemd-free.org/migrate.php) It's actually pretty flawed, so this article *should* address some of the out-of-date issues An up-to-date [scipt](https://github.com/MiCoArcher/openrc-migrator/blob/master/openrc-migrator.sh) designed to aid in migration. Read it first, and only then run it!

## CPU

There are multiple CPU-related issues, which if left unaddress may turn one's computing into a hell-like experience.

### CPU-related hard-freezes

A single major CPU issue are the [hard freezes](https://forum.manjaro.org/t/intel-bay-trail-freezes-the-linux-kernel/1931), common to many bay-trail devices . A simple solution to the problem is to add "max_cstate=1" option to the [kernel parameters](https://wiki.archlinux.org/index.php/Kernel_parameters).

### cpufreq

Coming soon...

## Multimedia

### Audio

Audio driver is not in the mainline yet, and I had no way of testing whether it is even going to work. It's a rather unpopular laptop, and I don't see how this is going to change. However, you are welcome to contribute to this article if you know of any regular bay-trail audio drivers. I suggest using a USB soundcard.

### Video

The on-board graphics uses the Intel driver. [Install](/index.php/Install "Install") [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Xorg will only start with the following syntax:

```
startx -- <other flags>

```

Such as

```
startx -- -keeptty

```

Aside from that, there are no out-of-the-ordinary configuration steps. Consult [Xorg](/index.php/Xorg "Xorg") and [Intel](/index.php/Intel "Intel") for more information.

### Webcam

The webcam is not supported and there is not even a driver for it.

## Networking

### Wireless

Wireless is provided by r8723bs SDIO driver. Rather unstable, but it is still usable. See [#See also](#See_also)

## Input

### Touchpad

A nightmare. It's a mono-pad, that has no buttons on it, but that's not the main issue. The big thing about the touchpad is that it is generating random characters when you tap at it's edges. Another issue - it's not a Synaptic, so it doesn't benefit from any of the synaptic-related settings. The driver comes from the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package.

## See also

*   [On system hangs](https://bbs.archlinux.org/viewtopic.php?pid=1681385) - in case you are experiencing system freezes
*   [Similar hardware setup, r8723bs wireless](https://bbs.archlinux.org/viewtopic.php?id=203180)
*   [A github page dedicated to the driver](https://github.com/hadess/rtl8723bs)
*   [Generic r8723bs issues thread on Ubuntu forums](https://ubuntuforums.org/archive/index.php/t-2249936.html)
*   [Generic building guide for r8723bs driver](https://github.com/hadess/rtl8723bs/wiki/RTL8723BS-module-building-instruction-for-Debian-GNU-Linux)