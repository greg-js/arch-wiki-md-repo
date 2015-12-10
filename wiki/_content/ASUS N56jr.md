# ASUS N56jr

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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

<td>xf86-video-intel</td>

</tr>

<tr>

<td>Nvidia</td>

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

<td>ath9k</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="color:green">**Working**</td>

<td>xf86-input-synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

<td>evdev?</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:blue">**Unknown**</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="color:blue">**Unknown**</td>

</tr>

</tbody>

</table>

Related articles

*   [ASUS N56vj](/index.php/ASUS_N56vj "ASUS N56vj")

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Audio](#Audio)
    *   [2.4 Multitouch](#Multitouch)

# Hardware

<table class="wikitable">

<tbody>

<tr>

<td>**CPU**</td>

<td>Intel(R) Core(TM) i7-4700HQ CPU @ 2.40GHz</td>

</tr>

<tr>

<td>**RAM**</td>

<td>12 GB (1x4GB,1x8GB)</td>

</tr>

<tr>

<td>**Display**</td>

<td>15.6" LCD</td>

</tr>

<tr>

<td>**Integrated Graphics**</td>

<td>Intel HD 4000</td>

</tr>

<tr>

<td>**Discrete Graphics**</td>

<td>NVIDIA GeForce GTX 760M</td>

</tr>

<tr>

<td>**Sound**</td>

<td>Intel HD Audio</td>

</tr>

<tr>

<td>**Ethernet**</td>

<td>RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller</td>

</tr>

<tr>

<td>**Wireless**</td>

<td>AR9485 Wireless Network Adapter</td>

</tr>

<tr>

<td>**Hard Disk**</td>

<td>1 TB 5400rpm SATA</td>

</tr>

<tr>

<td>**Touchpad**</td>

<td>ETPS/2 Elantech Touchpad</td>

</tr>

</tbody>

</table>

# Configuration

## Video

nouveau runs into some problems ([https://bbs.archlinux.org/viewtopic.php?id=178207](https://bbs.archlinux.org/viewtopic.php?id=178207)). There may be a way to patch it, but not without building a custom kernel and applying the patches mentioned in the bug report. After a full day of trying (module won't build against current kernel, patch won't apply to linux-mainline, ...), I've given up and switched to:

nvidia works fine using [bumblebee](/index.php/Bumblebee "Bumblebee").

## Wireless

**Edit:** I switched to the linux-ck kernel and no longer see this bug. I didn't see any obvious patches for it, but maybe there's something there. Either way, everything works flawlessly now...

Ugh. Why can't everyone just use Intel wireless cards?

The card (using `ath9k`) successfully scans for networks, successfully connects, successfully negotiates an IP address, and successfully disconnects immediately afterwards. Maybe the fifth or sixth time I power down the card and power it up again, it will hold the connection. After connecting once successfully, I haven't seen any problems reconnecting to a given network. This seems like a dhcp problem.

## Audio

Using `hdajackretask` to set the unconnected 0x16 pin to anything sets the external speaker as the rear right channel (`Internal (LFE)` is the closest approximation to what it should be).

## Multitouch

Gesture support is provided via [xf86-input-synaptics-mtpatch](https://aur.archlinux.org/packages/xf86-input-synaptics-mtpatch/) and [touchegg-svn](https://aur.archlinux.org/packages/touchegg-svn/) in the [AUR](/index.php/AUR "AUR"). I personally prefer GNOME Shell, which has some issues with how it handles touchpad input. Essentially, any event that is mapped to a gnome shell gesture and a touchegg gesture will be executed in both ways. For example, if you have natural scrolling mapped to two-finger drag via GNOME and non-inverted scrolling mapped to two-finger drag via touchegg, the page will scroll down then up when you two-finger drag up resulting in no net change in position.

The command `touchegg` will have to be executed every time the GUI loads (maybe add it to gnome-session or the equivalent for your WM?).

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_N56jr&oldid=328989](https://wiki.archlinux.org/index.php?title=ASUS_N56jr&oldid=328989)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")