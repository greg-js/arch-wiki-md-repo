# Lenovo Ideapad Y560

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The Lenovo Ideapad Y560 is a multimedia laptop available with several different option packages. This wiki will focus on support for as many variations as possible. At the time of writing, the Ideapad Y560 is available with the following options:

**CPU:** Intel® Core™ i3-370M Processor ( 2.40GHz 1066MHz 3MB )

Intel® Core™ i5-460M Processor ( 2.53GHz 1066MHz 3MB )

Intel® Core™ i7-720QM Processor ( 1.60GHz 1333MHz 6MB )

Intel® Core™ i7-740QM Processor ( 1.73GHz 1333MHz 6MB )

**Screen:** 15.6” (1366×768) Widescreen

**Memory:** Up to 8GB ram

**Graphics:** ATI Mobility Radeon HD 5730

## Contents

*   [1 Initial Installation](#Initial_Installation)
*   [2 Graphics](#Graphics)
*   [3 Networking](#Networking)
    *   [3.1 Wireless](#Wireless)
    *   [3.2 Ethernet](#Ethernet)
*   [4 The Linux-Ideapad Kernel](#The_Linux-Ideapad_Kernel)
*   [5 Sound](#Sound)
*   [6 Touchpad](#Touchpad)

## Initial Installation

Lenovo's default partitioning scheme thankfully included an extended partition. Using a utility such as gparted, it is recommended to shrink your windows partitions to at least half the size of the drive and increase the extended partition to fill in the gap, then installing Arch within new logical partitions inside. Installing the bootloader to /dev/sda will allow it to boot into all of the operating systems, though you will need to chainload windows (chainloader +1 boot option, see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") for an example).

## Graphics

The Lenovo Ideapad Y560's ATi 5730 graphics card works very well with both the open-source Radeon driver and the proprietary Catalyst driver, though there are minor performance differences to note:

[Catalyst](/index.php/Catalyst "Catalyst"): Decent 2D performance, stock settings appear to work fine. 3D acceleration performance is highest with this driver, though 2D accelerated performance is not quite as good as the open-source driver. Noticeable performance reduction in fullscreen video performance (both applications such as VLC and web-based videos such as flash videos from sites like [YouTube](http://www.youtube.com/).

[Radeon](/index.php/Radeon "Radeon"): Superb 2D and 2D accelerated performance, as well as decent 3D performance (though not as good as Catalyst). Fullscreen video is fine, and image-rendering programs/GPU-intensive applications tend to work well (with exception of 3D games, though this is under active development and so may have changed since the writing of this article).

Both drivers support overclocking, though the benefit of doing so on the Ideapad is negligible compared to the potential damage that can be done to the system, as the card will idle at about ~50-60C and can easily overheat due to the poor cooling system designed by Lenovo. [note: Admiralspark]

## Networking

### Wireless

As of Kernel 3.2.x, wireless works out-of-the-box with the iwlwifi driver.

### Ethernet

There is a bug in the kernel which causes the tg3 module to load before broadcom, rendering the Intel Ethernet adapter useless. To fix, you will need to change the following lines in your /etc/rc.conf:

```
MODULES=(broadcom tg3)

```

Now the ethernet interface, eth0, should load without issue.

## The Linux-Ideapad Kernel

The [linux-ideapad](https://aur.archlinux.org/packages/linux-ideapad/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-ideapad)]</sup> kernel is optimized for the Lenovo Y5xx laptops, though it should work on any laptop that uses the same chipset as the Ideapad. Includes all changes from the parent package by graysky [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup>, as well as:

*   Optimized for Intel Core2/i3/i5/i7 processors
*   BFQ I/O enabled by default
*   tun/tap driver for VPN use
*   1000MHz timer (reduced latency)
*   Low-latency preemptible kernel options
*   Networking filesystems: CIFS, <s>NFS client/server</s> **As of version 3.6.8-1, CFS is re-enabled**
*   Filesystem support added for NTFS, EXT4, EXT3, EXT2, VFAT, iso9660, as well as USB mass storage devices
*   FUSE module for network filesystems
*   iwlwifi driver
*   broadcom/tg3
*   Ideapad rfkill switch support
*   Ideapad switchable graphics (non-i7 models that included the intel integrated graphics card with the ATi/nVidia)
*   other small tweaks for performance, constantly being updated. Suggestions should be left on the [linux-ideapad](https://aur.archlinux.org/packages/linux-ideapad/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-ideapad)]</sup> page.
*   Many unused drivers switched on by default are disabled, reducing the final kernel size significantly

## Sound

[ALSA](/index.php/ALSA "ALSA") works fine with the sound card, using the snd_hda_intel module.

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_Y560&oldid=392335](https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_Y560&oldid=392335)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")