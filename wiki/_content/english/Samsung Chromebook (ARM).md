Related articles

*   [Chromebook](/index.php/Chromebook "Chromebook")

The Samsung Chromebook (model XE303C12) is a laptop intended work in the cloud. It provides a powerful Cortex-A15 Dual Core Exynos 5 processor at 1.7 GHz with Mali-T604 GPU, 2 GiB of DDR3, 16 GiB of internal flash storage, WiFi a/b/g/n, SD and USB ports, HDMI connector and a 11.6" display. It is visually like the MacBook Air 11\. With stock firmware it runs a heavily modified Gentoo-Linux, which means that nearly all the source code is [available](https://chromium.googlesource.com/chromiumos) from Google. **It is possible to install ArchLinux ARM (ALARM) on this device**.

More information at dedicated pages by [Google](http://www.google.com/intl/en/chrome/devices/samsung-chromebook.html#ss-cb) and [Samsung](http://www.samsung.com/us/computer/chrome-os-devices/XE303C12-A01US).

## Contents

*   [1 Article Preface](#Article_Preface)
*   [2 Installing Arch Linux ARM](#Installing_Arch_Linux_ARM)
*   [3 Stop Here If You're Not 100% Sure](#Stop_Here_If_You.27re_Not_100.25_Sure)
*   [4 Booting from SD](#Booting_from_SD)
*   [5 Related Links](#Related_Links)

## Article Preface

This article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before.

**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org](http://archlinuxarm.org) not through posts to the official Arch Linux Forum. Any posts related to ARM specific issues will be promptly closed per the [Arch Linux Distrubution Support ONLY](/index.php/Forum_etiquette#Arch_Linux_distribution_support_.2Aonly.2A "Forum etiquette") policy.

## Installing Arch Linux ARM

See the instructions at the [archlinuxarm site](https://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook). This is a fully supported platform at Arch Linux ARM (wholly separate entity)

You can install to:

*   SD Card
*   USB 2.0 Flash stick
*   eMMC (after installing one of the prior)

To install to SD or USB, follow the instructions linked above. To install to eMMC, install to one of the prior medias, then install to /dev/mmcblk0, a simple edit from the install instructions from SD. You must boot onto a different media prior to this however.

## Stop Here If You're Not 100% Sure

**Installation to the eMMC can be removed via the USB Restore method that is a part of all Chromebook devices, when installing with official method.**

**Flashing of non-verified uboot is *not required* for eMMC install.**

## Booting from SD

If you ever screw things up by burning a wrong bootloader, there is a recovery mechanism. The SoC built-in bootloader (known as BL0 and BL1) can be configured to boot from SPI, USB, SD and probably other options. This is known because of the Arndale development board (and previous Exynos models behave the same as well).

This is configured at the factory to boot from SPI, but this is done with a bunch of resistors located at the bottom of the PCB (link to image). User (name) experimented and got the working configuration (link to image).

**Warning:** If you are unsure about how to short-circuit pads, you should definitely go away and experiment a bit with other electronics. A wrong short-circuit may permanently damage your board.

By short-circuiting the pads as per the diagram linked, your SoC will boot from SD. You have to (confirm this and complete the information) load a U-Boot with BL2 incorporated.

## Related Links

*   [http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook)
*   [http://archlinuxarm.org/forum/viewtopic.php?t=4016](http://archlinuxarm.org/forum/viewtopic.php?t=4016)