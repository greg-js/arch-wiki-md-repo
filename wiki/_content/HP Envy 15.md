# HP Envy 15

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Laptop/HP](/index.php/Laptop/HP "Laptop/HP").**

**Notes:** Abysmal style, mostly trivial notes (Discuss in [Talk:HP Envy 15#](https://wiki.archlinux.org/index.php/Talk:HP_Envy_15))

<table style="float:right; border: 1px solid #000;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel</td>

<td style="color:green">**Working**</td>

<td>xf86-video-intel</td>

</tr>

<tr>

<td>nVdia</td>

<td style="color:green">**Working**</td>

<td>nvidia</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>r8169</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>iwlwifi _or_ rt2800pci</td>

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

<td>uvcvideo</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="color:green">**Working**</td>

<td>rtbth</td>

</tr>

<tr>

<td>Fingerprint Reader</td>

<td style="color:green">**Working**</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video -- _j013sg and j082sf_](#Video_--_j013sg_and_j082sf)
    *   [2.2 Audio -- _j013sg and j082sf_](#Audio_--_j013sg_and_j082sf)
    *   [2.3 WIFI Button -- _j082sf_](#WIFI_Button_--_j082sf)
    *   [2.4 Fingerprint Reader -- _j082sf_](#Fingerprint_Reader_--_j082sf)
    *   [2.5 Wifi -- _j013sg and j082sf_](#Wifi_--_j013sg_and_j082sf)
    *   [2.6 Bluetooth -- _j082sf_](#Bluetooth_--_j082sf)

# Hardware

<table>

<tbody>

<tr>

<td>**CPU**</td>

<td>Intel Core i7-4702MQ (2.2GHz Quad-core + HT)</td>

</tr>

<tr>

<td>**RAM**</td>

<td>16 GB (2x8GB)</td>

</tr>

<tr>

<td>**Display**</td>

<td>15.6" LCD</td>

</tr>

<tr>

<td>**Integrated Graphics**</td>

<td>Intel HD 4600</td>

</tr>

<tr>

<td>**Discrete Graphics**</td>

<td>NVIDIA GeForce GT 750M (2G)</td>

</tr>

<tr>

<td>**Sound**</td>

<td>Intel HD Audio</td>

</tr>

<tr>

<td>**Ethernet**</td>

<td>Realtek RTL8168/8111g Gigabit Ethernet</td>

</tr>

<tr>

<td>**Wireless**</td>

<td>**j013sg :** Intel Centrino Wireless-N 2230</td>

</tr>

<tr>

<td>**j082sf :** Ralink RT3290 (bluetooth + wifi)</td>

</tr>

<tr>

<td>**Bluetooth**</td>

<td>**j013sg :** None</td>

</tr>

<tr>

<td>**j082sf :** Ralink RT3290 (bluetooth + wifi)</td>

</tr>

<tr>

<td>**Hard Disk**</td>

<td>1 TB 5400rpm SATA</td>

</tr>

<tr>

<td>**Touchpad**</td>

<td>Synaptics ClickPad</td>

</tr>

</tbody>

</table>

[[Schematic diagram](https://framapic.org/HHmPmSh9DV1r/S04qJm6r)]

# Configuration

This is based on the HP Envy 15 j013sg (E8N68EA) and HP Envy j082sf

## Video -- _j013sg and j082sf_

xf86-video-modesetting and bumblebee setups work. nouveau untested Works by folllowing [https://wiki.archlinux.org/index.php/Optimus](https://wiki.archlinux.org/index.php/Optimus)

## Audio -- _j013sg and j082sf_

`hdajackretask` in the package `extra/alsa-tools` can be used to remap the unconnected 0x0f pin to Internal Speaker, and the 0x10 pin to the subwoofer (Internal Speaker LFE).

## WIFI Button -- _j082sf_

The `hp-wireless` module landed in kernel version 3.14\. This button will not work with [rt3290sta-dkms](https://aur.archlinux.org/packages/rt3290sta-dkms/) AUR package.

## Fingerprint Reader -- _j082sf_

Works fine with this package : [https://github.com/payden/libfprint](https://github.com/payden/libfprint)

## Wifi -- _j013sg and j082sf_

Works out of the box for both of them. If you have issues with j082sf, you can use [rt3290sta-dkms](https://aur.archlinux.org/packages/rt3290sta-dkms/) AUR package

## Bluetooth -- _j082sf_

Works fine with [rtbth-dkms](https://aur.archlinux.org/packages/rtbth-dkms/) AUR package.

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Envy_15&oldid=380737](https://wiki.archlinux.org/index.php?title=HP_Envy_15&oldid=380737)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")