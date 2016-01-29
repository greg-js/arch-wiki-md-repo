# Lenovo Ideapad Y560

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Lenovo Ideapad Y560#](https://wiki.archlinux.org/index.php/Talk:Lenovo_Ideapad_Y560))

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
*   [4 Sound](#Sound)
*   [5 Touchpad](#Touchpad)

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

## Sound

[ALSA](/index.php/ALSA "ALSA") works fine with the sound card, using the snd_hda_intel module.

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_Y560&oldid=412545](https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_Y560&oldid=412545)"