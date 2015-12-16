# Lenovo ThinkPad Edge E420s

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad Edge E420s#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_Edge_E420s))

This article covers the Arch Linux support for the Lenovo ThinkPad Edge E420s laptop.

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 lspci](#lspci)
*   [2 Configuration](#Configuration)
    *   [2.1 Clickpad](#Clickpad)
    *   [2.2 Video](#Video)
    *   [2.3 Ethernet](#Ethernet)
    *   [2.4 Wireless](#Wireless)
        *   [2.4.1 Intel Centrino Wireless-N 1000](#Intel_Centrino_Wireless-N_1000)
    *   [2.5 Sound](#Sound)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Power](#Power)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Delay with Space Bar](#Delay_with_Space_Bar)
    *   [3.2 Trackpoint is NOT detected or is detected after X minutes](#Trackpoint_is_NOT_detected_or_is_detected_after_X_minutes)

## Hardware

Using **kernel 2.6.38.3**

<table class="wikitable">

<tbody>

<tr>

<th>Device</th>

<th>Works</th>

</tr>

<tr>

<td>Video</td>

<td>Yes</td>

</tr>

<tr>

<td>Ethernet</td>

<td>Yes</td>

</tr>

<tr>

<td>Wireless (Intel Centrino Wireless-N 1000)</td>

<td>Yes</td>

</tr>

<tr>

<td>Bluetooth</td>

<td>Not Tested</td>

</tr>

<tr>

<td>Audio</td>

<td>Yes</td>

</tr>

<tr>

<td>Camera</td>

<td>Yes</td>

</tr>

<tr>

<td>Finger Print Reader</td>

<td>Not Tested</td>

</tr>

<tr>

<td>Card Reader</td>

<td>Not Tested</td>

</tr>

</tbody>

</table>

### lspci

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 6 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 1 (rev b4)
00:1c.1 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 2 (rev b4)
00:1c.2 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 3 (rev b4)
00:1c.3 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 4 (rev b4)
00:1d.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM65 Express Chipset Family LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 6 Series Chipset Family 6 port SATA AHCI Controller (rev 04)
00:1f.3 SMBus: Intel Corporation 6 Series Chipset Family SMBus Controller (rev 04)
07:00.0 Network controller: Intel Corporation Centrino Wireless-N 1000
0c:00.0 System peripheral: JMicron Technology Corp. SD/MMC Host Controller (rev 30)
0c:00.2 SD Host controller: JMicron Technology Corp. Standard SD Host Controller (rev 30)
11:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 06)

```

## Configuration

### Clickpad

The clickpad works with the xf86-input-synaptic driver from extra, but the left/right click buttons at the bottom of the clickpad do not work.

Install [xf86-input-synaptics-clickpad](https://aur.archlinux.org/packages.php?ID=38120) from the [AUR](/index.php/AUR "AUR").

### Video

See [Intel graphics](/index.php/Intel_graphics "Intel graphics") and [xrandr](/index.php/Xrandr "Xrandr").

### Ethernet

See [Network configuration#Realtek RTL8111/8168B](/index.php/Network_configuration#Realtek_RTL8111.2F8168B "Network configuration").

### Wireless

#### Intel Centrino Wireless-N 1000

Works out of the box. Module: **iwlagn**

### Sound

Works out of the box. Module: **snd-hda-intel**

### Webcam

Works out of the box. Tested using Skype

### Power

Suspend and Hibernation both work using [pm-utils](/index.php/Pm-utils "Pm-utils") Note: Hibernation did not work on 2.6.38.2 (works with 2.6.38.3)

## Troubleshooting

### Delay with Space Bar

**Solution:** Update BIOS (at least 1.08)

### Trackpoint is NOT detected or is detected after X minutes

This appears to be a kernel bug. See: [https://bugzilla.kernel.org/show_bug.cgi?id=33292](https://bugzilla.kernel.org/show_bug.cgi?id=33292)

A workaround is passing proto=bare to the psmouse module. However this disable scrolling with the clickpad and the two finger middle click.

```
modprobe psmouse proto=bare

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Edge_E420s&oldid=412550](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Edge_E420s&oldid=412550)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")