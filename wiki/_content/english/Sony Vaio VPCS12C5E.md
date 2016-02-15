This page is about setting up Arch Linux on the Sony Vaio VPCS12C5E laptop. It is advisable to read [Laptop](/index.php/Laptop "Laptop") beforehand to get an idea about the topic in general.

## Contents

*   [1 Overview](#Overview)
*   [2 Dedicated graphics](#Dedicated_graphics)
*   [3 WWAN](#WWAN)
*   [4 See also](#See_also)

## Overview

It seems that you need at least kernel 2.36 when you have a dedicated graphics card built into your laptop. With kernels lower than that trying to boot the machine will result in a black screen, as kernel mode setting won't work. However it is possible to boot without KMS, appending "nomodeset" to the boot parameters.

At least the wlan adapter seems to work out of the box, as well as the webcam. Nothing else tested so far.

## Dedicated graphics

When you've got a model providing a dedicated graphic card, you probably will need to blacklist the "intel_ips" module. You can do this by creating a file "intel_ips_blacklist.conf" within "/etc/modprobe.d/":

```
# echo "blacklist intel_ips" > /etc/modprobe.d/intel_ips_blacklist.conf

```

Afterwards you'll have to recreate your initramfs, so that this module won't be loaded in the initramfs neither, by issuing the following command:

```
# mkinitcpio -p linux

```

There seems to be some bug that prevents you from switching back to any consoles after starting the X server once with the current version of the nvidia package (290.10-1). The only known workaround so far is to use [Uvesafb](/index.php/Uvesafb "Uvesafb"). Alternatively you could use [Nouveau](/index.php/Nouveau "Nouveau") instead of the Nvidia binaries.

## WWAN

To get the optional UMTS modem get working you can refer to [Gobi Broadband Modems](/index.php/Gobi_Broadband_Modems "Gobi Broadband Modems"). You probably want to install [gobi-loader](https://aur.archlinux.org/packages/gobi-loader/). In order to get the appropriate firmware you can either use the package [gobi-firmware](https://aur.archlinux.org/packages/gobi-firmware/) or get it off from a Windows installation. Further information can be found at the [ThinkWiki](http://www.thinkwiki.org/wiki/Qualcomm_Gobi_2000) as they seem to use the same hardware for some of their devices. The device ID for Sony seems to be "05c6:9224" before the firmware is loaded and "05c6:9225" when the firmware is actually loaded.

## See also

So far there have been some people ran into several issues with this model (and some similiar), take a lookg at the following links:

*   [http://lowl.net/en/linux-on-vaio-vpc-z.html](http://lowl.net/en/linux-on-vaio-vpc-z.html)
*   [http://ubuntuforums.org/showthread.php?t==1578004](http://ubuntuforums.org/showthread.php?t==1578004)
*   [http://code.google.com/p/vaio-f11-linux/](http://code.google.com/p/vaio-f11-linux/)