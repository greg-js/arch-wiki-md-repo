# HP Envy 15t-j000 Quad Edition

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** Power Management, Video Card, NVIDIA optimus, Mouse, mSATA SSD cache, more on installing, fingerprint reader, camera, sound, what works/dosen't work summary,wireless, dual boot, hard drive (Discuss in [Talk:HP Envy 15t-j000 Quad Edition#](https://wiki.archlinux.org/index.php/Talk:HP_Envy_15t-j000_Quad_Edition))

The HP Envy 15t-j000 Quad Edition is a laptop released in 2013.

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel</td>

<td style="color:green">**Working**</td>

<td>xf86-video-intel (on some versions use NVIDIA with bumblebee)</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>atl1c</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>iwlwifi</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="color:green">**Working**</td>

<td>synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:green">**Working**</td>

<td>rts5229</td>

</tr>

<tr>

<td>Fingerprint Reader</td>

<td style="color:red">**Not Working**</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Installing Arch](#Installing_Arch)
*   [2 Backlight Issue](#Backlight_Issue)
*   [3 Battery and Power Management](#Battery_and_Power_Management)
*   [4 Mouse and Trackpad](#Mouse_and_Trackpad)
*   [5 Graphics, Video Card, and NVIDIA Optimus](#Graphics.2C_Video_Card.2C_and_NVIDIA_Optimus)
*   [6 Fingerprint Reader](#Fingerprint_Reader)
*   [7 Wireless Networking](#Wireless_Networking)
*   [8 Sound](#Sound)
*   [9 mSATA SSD Cache](#mSATA_SSD_Cache)
*   [10 Dual Boot](#Dual_Boot)

## Installing Arch

This laptop has secure boot enabled by default. In order to install Arch this should be disabled. UFEI should be set to legacy mode.

## Backlight Issue

On some kernels the laptop backlight will not turn on, leaving a black screen on boot. This can be solved with the following kernel parameter.

```
 acpi_backlight=vendor

```

The following kernel parameter will also work, but will disable 3d acceleration.

```
 nomodeset

```

## Battery and Power Management

The rated battery life for this laptop is 9hrs and with configuration [5.5 hrs is usually possible](http://answers.yahoo.com/question/index?qid=20130630193950AAXQF6h).

Install [acpi](https://www.archlinux.org/packages/?name=acpi).

Install [thermald](https://aur.archlinux.org/packages/thermald/)<sup><small>AUR</small></sup>

```
# systemctl enable thermald.service
# systemctl start thermald.service

```

Install [tlp](https://www.archlinux.org/packages/?name=tlp)

Configure it as per [https://wiki.archlinux.org/index.php/TLP](https://wiki.archlinux.org/index.php/TLP)

Install [iw](https://www.archlinux.org/packages/?name=iw)

Install [smartmontools](https://www.archlinux.org/packages/?name=smartmontools)

Install [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode)

```
# su -c 'echo "microcode" >> /etc/modules-load.d/microcode.conf'

```

Install [cpupower](https://www.archlinux.org/packages/?name=cpupower)

```
# systemctl start cpupower
# systemctl enable cpupower

```

## Mouse and Trackpad

The trackpad for this laptop supports a virtual scroll wheel. To enable it edit /etc/X11/xorg.conf.d/10-evdev.conf

and make sure the following is commented out

```
Section "InputClass"
       Identifier "evdev touchpad catchall"
       MatchIsTouchpad "on"
       MatchDevicePath "/dev/input/event*"
       Driver "evdev"
EndSection

```

## Graphics, Video Card, and NVIDIA Optimus

If you have the version of this laptop with an NVIDIA card then you have an optimus based chipset.

## Fingerprint Reader

This laptop comes with a fingerprint reader but there is no Linux driver for it.

## Wireless Networking

Recent kernels contain a driver for this laptop's wireless adapter.

## Sound

Sound works out of the box. [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) may be useful in configuring audio.

## mSATA SSD Cache

This laptop has a mSATA bay that can include a cache hard drive. This mSATA can be used as a primary hard drive with some configuration.

## Dual Boot

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Envy_15t-j000_Quad_Edition&oldid=368727](https://wiki.archlinux.org/index.php?title=HP_Envy_15t-j000_Quad_Edition&oldid=368727)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")