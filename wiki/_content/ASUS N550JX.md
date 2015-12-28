# ASUS N550JX

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Module**</td>

</tr>

<tr>

<td>Intel</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>xf86-video-intel</td>

</tr>

<tr>

<td>Nvidia</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>nvidia</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>r8169</td>

</tr>

<tr>

<td>Wireless</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>iwlwifi</td>

</tr>

<tr>

<td>Audio</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>xf86-input-synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>uvcvideo</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>rtsx_usb</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>bluetooth</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Audio](#Audio)
    *   [2.3 Keyboard](#Keyboard)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 nouveau problems](#nouveau_problems)

# Hardware

This article covers hardware specific configuration for [ASUS N550JX](https://www.asus.com/Notebooks/N550JX/specifications/) laptop.

# Configuration

## Video

Laptop comes with two GPU's (main [INTEL](/index.php/Intel_graphics "Intel graphics") and dedicated [NVIDIA](/index.php/NVIDIA "NVIDIA")):

```
$ lspci | grep "VGA|3D"

```

```
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 950M] (rev ff)
```

NVIDIA Optimus technology can be implemented and controlled using [Bumblebee](/index.php/Bumblebee "Bumblebee") software.

## Audio

Built-in speakers and headphones work out of the box with **snd_hda_intel** driver. External sub-woofer works after this patch is applied:

 `/etc/modprobe.d/snd-hda-intel-n550jx.conf`  `options snd-hda-intel patch=n550jx-lfe-fix,n550jx-lfe-fix`  `/lib/firmware/n550jx-lfe-fix` 

```
[codec]
0x10ec0668 0x104313df 0

[pincfg]
0x1a 0x00106111
```

At the time of writing this article kernel [bug](https://bugzilla.kernel.org/show_bug.cgi?id=110001) is filled for this patch to be included in ALSA future releases.

## Keyboard

In order to make all keyboard function keys (FN+F{1..12}) generate correct signals - add [kernel parameter](/index.php/Kernel_parameters "Kernel parameters") 'acpi_osi=' (without quotation marks) to your bootloader.

# Troubleshooting

## nouveau problems

Installation media sometimes produces a lot of error messages during boot. This is a bug in the _nouveau_ driver. Just ignore hitting Enter few times. Later you can disable _nouveau_ module:

 `/etc/modprobe.d/blacklist-nouveau.conf`  `blacklist nouveau` 

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_N550JX&oldid=413587](https://wiki.archlinux.org/index.php?title=ASUS_N550JX&oldid=413587)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")