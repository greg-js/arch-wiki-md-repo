# HP Envy 17

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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

<td>AMD</td>

<td style="color:green">**Working**</td>

<td>ati-dri</td>

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

</tbody>

</table>

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Audio](#Audio)
    *   [2.3 SD Card Reader](#SD_Card_Reader)

# Hardware

<table>

<tbody>

<tr>

<td>**CPU**</td>

<td>Intel Core i7-2670QM (2.2GHz Quad-core)</td>

</tr>

<tr>

<td>**RAM**</td>

<td>8 GB (2x4GB)</td>

</tr>

<tr>

<td>**Display**</td>

<td>17.3" LCD</td>

</tr>

<tr>

<td>**Integrated Graphics**</td>

<td>Intel HD 3000</td>

</tr>

<tr>

<td>**Discrete Graphics**</td>

<td>AMD Radeon HD 7690 (1 GB)</td>

</tr>

<tr>

<td>**Sound**</td>

<td>Intel HD Audio</td>

</tr>

<tr>

<td>**Ethernet**</td>

<td>Atheros AR8151 v2.0 Gigabit Ethernet</td>

</tr>

<tr>

<td>**Wireless**</td>

<td>Intel Centrino Advanced-N 6235</td>

</tr>

<tr>

<td>**Hard Disk**</td>

<td>750 GB 7200rpm SATA</td>

</tr>

<tr>

<td>**Touchpad**</td>

<td>Synaptics ClickPad</td>

</tr>

</tbody>

</table>

# Configuration

This is based on the 2012 HP Envy 17.

## Video

Works by following [http://www.reddit.com/r/linux/comments/1nu4pc/muxless_graphics_cards_on_linux/](http://www.reddit.com/r/linux/comments/1nu4pc/muxless_graphics_cards_on_linux/). I strongly recommend switching to linux-mainline ([AUR](https://aur.archlinux.org/packages/linux-mainline/)) to take advantage of power-management built into 3.12.

## Audio

`hdajackretask` in the package `extra/alsa-tools` can be used to remap the unconnected 0x10 pin to the subwoofer (Internal Speaker LFE).

## SD Card Reader

**As of 3.8 a third party module is not needed, device is accessible @ /dev/mmcX**

The module **for pre 3.8** `rts5229` is in the [AUR](https://aur.archlinux.org/packages/rts5229/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Envy_17&oldid=384278](https://wiki.archlinux.org/index.php?title=HP_Envy_17&oldid=384278)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")