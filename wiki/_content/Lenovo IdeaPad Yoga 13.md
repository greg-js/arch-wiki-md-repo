# Lenovo IdeaPad Yoga 13

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo IdeaPad Yoga 13#](https://wiki.archlinux.org/index.php/Talk:Lenovo_IdeaPad_Yoga_13))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** not defined rules how to fill such articles (Discuss in [Talk:Lenovo IdeaPad Yoga 13#](https://wiki.archlinux.org/index.php/Talk:Lenovo_IdeaPad_Yoga_13))

Models covered: Lenovo IdeaPad Yoga 13

Sub-models options :

<table class="wikitable sortable collapsible" style="text-align: left;">

<tbody>

<tr>

<th>Diffefenses</th>

<th>Value</th>

</tr>

<tr>

<td>CPU</td>

<td>Intel i3, i5, i7</td>

</tr>

<tr>

<td>RAM</td>

<td>4GB, 8GB</td>

</tr>

<tr>

<td>SSD</td>

<td>128 GB, 256 GB</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Overall Status](#Overall_Status)
*   [2 Display](#Display)
    *   [2.1 Backlight](#Backlight)
    *   [2.2 Touch Screen](#Touch_Screen)
*   [3 Keyboard](#Keyboard)
*   [4 Configaration](#Configaration)
    *   [4.1 Wireless Fidelity](#Wireless_Fidelity)
    *   [4.2 Bluetooth](#Bluetooth)
*   [5 Hardware](#Hardware)
    *   [5.1 PCI devices](#PCI_devices)
*   [6 See also](#See_also)

## Overall Status

<table class="wikitable sortable">

<tbody>

<tr>

<th>Feature</th>

<th>Status</th>

</tr>

<tr>

<td>Boot Standard Kernel</td>

<td>OK</td>

</tr>

<tr>

<td>Detect SSD</td>

<td>OK</td>

</tr>

<tr>

<td>CPU Frequency Scaling</td>

<td>not tested</td>

</tr>

<tr>

<td>Hibernation</td>

<td>not tested</td>

</tr>

<tr>

<td>Sleep / Suspend</td>

<td>OK</td>

</tr>

<tr>

<td>Switch to External Screen</td>

<td>OK</td>

</tr>

<tr>

<td>Wireless/Bluetooth</td>

<td>with troubles</td>

</tr>

<tr>

<td>Wireless/Wifi</td>

<td>with troubles</td>

</tr>

<tr>

<td>Keyboard's Hotkeys</td>

<td>not all</td>

</tr>

<tr>

<td>Touch screen</td>

<td>works, but multitouch is a problem</td>

</tr>

<tr>

<td>Card reader</td>

<td>not tested</td>

</tr>

</tbody>

</table>

## Display

Works out of the box. Intel HD 4000

### Backlight

Control of brightness only works after suspend. After wake up, you can control brightness via f11 (less bright) and f12 (more bright). However, it is not brightnes problem, but keyboard buttons' problem. To control brightness while loaded from scratch, you can do the following command:

```
# cat 4882 > /sys/class/backlight/intel_backlight/brightness

```

This will change brightness value to 4882\. It is maximum brightness level. You can choose some other value, of course.

### Touch Screen

One touch works out of the box. But it works like a mouse.

## Keyboard

In addition to keyboard, there are some extra lenovo keys: vol+, vol-, recovery button, button for locking screen rotation, windows button under screen.

Not all media buttons work out of the box: mute on f1 works vol- on f2 works vol+ on f3 works close on f4 works renew on f5 works disable touchpad on f6 do not works disable network on f7 do not work choose application on f8 does not work disable display on f9 works change output video sink on f10 do not work brightness- on f11 works brightness+ on f12 works

## Configaration

### Wireless Fidelity

Internal Wi-Fi driver (r8723au) is working with a huge troubles with current kernel (3.17.6-1-ARCH). So to get wifi work, [blacklist](/index.php/Blacklisting#Blacklisting "Blacklisting") r8723 module. Then you should install [dkms-8723au-git](https://aur.archlinux.org/packages/dkms-8723au-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dkms-8723au-git)]</sup> package and insert 8723au module.

### Bluetooth

???

## Hardware

### PCI devices

 `lspci` 

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:04.0 Signal processing controller: Intel Corporation 3rd Gen Core Processor Thermal Subsystem (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation QS77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
00:1f.6 Signal processing controller: Intel Corporation 7 Series/C210 Series Chipset Family Thermal Management Controller (rev 04)

```

## See also

*   [https://wiki.debian.org/InstallingDebianOn/Lenovo/IdeaPad_Yoga_13_(Wheezy)](https://wiki.debian.org/InstallingDebianOn/Lenovo/IdeaPad_Yoga_13_(Wheezy))
*   [Lenovo IdeaPad Yoga 13](https://en.wikipedia.org/wiki/Lenovo_IdeaPad_Yoga_13 "wikipedia:Lenovo IdeaPad Yoga 13")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_IdeaPad_Yoga_13&oldid=392334](https://wiki.archlinux.org/index.php?title=Lenovo_IdeaPad_Yoga_13&oldid=392334)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")