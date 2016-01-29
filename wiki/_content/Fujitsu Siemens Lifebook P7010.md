# Fujitsu Siemens Lifebook P7010

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Fujitsu Siemens Lifebook P7010#](https://wiki.archlinux.org/index.php/Talk:Fujitsu_Siemens_Lifebook_P7010))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Fujitsu Siemens Lifebook P7010#](https://wiki.archlinux.org/index.php/Talk:Fujitsu_Siemens_Lifebook_P7010))

## Contents

*   [1 Overview](#Overview)
    *   [1.1 What works/What does not](#What_works.2FWhat_does_not)
*   [2 Video](#Video)
*   [3 Audio](#Audio)
*   [4 Wireless Network](#Wireless_Network)
*   [5 Card Readers](#Card_Readers)
    *   [5.1 PCMCIA](#PCMCIA)
    *   [5.2 Secure Digital](#Secure_Digital)
*   [6 Important Config files](#Important_Config_files)
*   [7 External Links](#External_Links)

## Overview

### What works/What does not

Pretty much everything works on this laptop except the TV-out and the SD-card reader. The screen needs a little tweaking to get working. The preferred resolution (1280x768) is not part of the VBIOS, and consequently the VBIOS needs to be patched with Alain Poirier's software 855resolution (to be found in the AUR).

## Video

**Note:** relevant modules:

*   intel-agp
*   i915

In order to get the video working fine at 1280x768 you need to patch the VBIOS with Alain Poirier's 855resolution for which there is a [PKGBUILD](https://aur.archlinux.org/packages.php?do_Details=1&ID=1672&O=0&L=&C=&K=&SB=&PP=&do_MyPackages=&do_Orphans=) in the AUR. This application allows you to replace any of the modes in the VBIOS with something else. After you have compiled the package and installed it, run the following command.

```
855resolution 5c 1280 768

```

This will replace mode 5c with 1280 768\. You can list the modes with

```
855resolution -l

```

which should return something like this:

```
855resolution version 0.4, by Alain Poirier

Chipset: 855GM (id=0x35808086)
VBIOS type: 2
VBIOS Version: 3181 

Mode 30 : 640x480, 8 bits/pixel
Mode 32 : 800x600, 8 bits/pixel
Mode 34 : 1024x768, 8 bits/pixel
Mode 38 : 1280x1024, 8 bits/pixel
Mode 3a : 1600x1200, 8 bits/pixel
Mode 3c : 1280x768, 8 bits/pixel
Mode 41 : 640x480, 16 bits/pixel
Mode 43 : 800x600, 16 bits/pixel
Mode 45 : 1024x768, 16 bits/pixel
Mode 49 : 1280x1024, 16 bits/pixel
Mode 4b : 1600x1200, 16 bits/pixel
Mode 4d : 1280x768, 16 bits/pixel
Mode 50 : 640x480, 32 bits/pixel
Mode 52 : 800x600, 32 bits/pixel
Mode 54 : 1024x768, 32 bits/pixel
Mode 58 : 1280x1024, 32 bits/pixel
Mode 5a : 1600x1200, 32 bits/pixel
Mode 5c : 1280x768, 32 bits/pixel

```

Before everything is set, you will also need to add the proper modelines in xorg.conf. This is done in the monitor section

```
Section "Monitor"
        Identifier      "InternalMonitor"
        Option  "DPMS"
        HorizSync    28.0 - 96.0
        VertRefresh  50.0 - 75.0
        Modeline "1280x768" 80.14 1280 1344 1480 1680 768 769 772 795
        Modeline "1024x768" 65.00 1024 1047 1183 1343 768 770 776 805
EndSection

```

## Audio

**Note:** relevant modules:

*   snd-intel8x0

The audio is really not a big deal, at least not if you use ALSA (which is the only sound system I have ever used under Linux). The only weirdness is that the Master channel has no effect on the sound, you have to play around with the Headphone and PCM channels in order to set the sound.

## Wireless Network

[Install](/index.php/Install "Install") [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw).

## Card Readers

### PCMCIA

**Note:** relevant modules:

*   yenta_socket

### Secure Digital

There is now a driver in alpha test stage on Sourceforge [http://sourceforge.net/projects/sdricohcs/](http://sourceforge.net/projects/sdricohcs/) it supports only the SD Card driver so far and must be compiled from source. Arch packages found here [https://aur.archlinux.org/packages.php?do_Details=1&ID=9884](https://aur.archlinux.org/packages.php?do_Details=1&ID=9884).

## Important Config files

## External Links

*   This report is listed at the [TuxMobil: Linux Laptop and Notebook Installation Guides Survey: Fujitsu-Siemens - FSC](http://tuxmobil.org/fujitsu.html).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fujitsu_Siemens_Lifebook_P7010&oldid=353569](https://wiki.archlinux.org/index.php?title=Fujitsu_Siemens_Lifebook_P7010&oldid=353569)"