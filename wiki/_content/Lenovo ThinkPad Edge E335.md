# Lenovo ThinkPad Edge E335

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad Edge E335#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_Edge_E335))

This article covers the Arch Linux support for the Lenovo ThinkPad Edge E335s laptop.

## Installation

This laptop has no optical drives, so an alternate installation method is required. For instance, Arch Linux can be installed from an [USB drive](/index.php/USB_flash_installation_media "USB flash installation media").

## Hardware support

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

<td>Wireless (Broadcom BCM43228)</td>

<td>Yes (tested with _w_ driver)</td>

</tr>

<tr>

<td>Audio</td>

<td>Yes (using [PulseAudio](/index.php/PulseAudio "PulseAudio"))</td>

</tr>

<tr>

<td>Camera</td>

<td>Yes</td>

</tr>

<tr>

<td>Card Reader</td>

<td>Yes</td>

</tr>

<tr>

<td>USB 2.0</td>

<td>Yes</td>

</tr>

<tr>

<td>USB 3.0</td>

<td>Yes</td>

</tr>

</tbody>

</table>

### lspci

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 14h Processor Root Complex
00:01.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Wrestler [Radeon HD 7340]
00:01.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Wrestler HDMI Audio
00:04.0 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 14h Processor Root Port
00:05.0 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 14h Processor Root Port
00:07.0 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 14h Processor Root Port
00:10.0 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB XHCI Controller (rev 03)
00:11.0 SATA controller: Advanced Micro Devices, Inc. [AMD] FCH SATA Controller [AHCI mode]
00:12.0 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB OHCI Controller (rev 11)
00:12.2 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB EHCI Controller (rev 11)
00:13.0 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB OHCI Controller (rev 11)
00:13.2 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB EHCI Controller (rev 11)
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 14)
00:14.2 Audio device: Advanced Micro Devices, Inc. [AMD] FCH Azalia Controller (rev 01)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 11)
00:14.4 PCI bridge: Advanced Micro Devices, Inc. [AMD] FCH PCI Bridge (rev 40)
00:14.5 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB OHCI Controller (rev 11)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 0 (rev 43)
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 1
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 2
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 3
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 4
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 6
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 5
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 12h/14h Processor Function 7
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 07)
02:00.0 Network controller: Broadcom Corporation BCM43228 802.11a/b/g/n
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5209 PCI Express Card Reader (rev 01)

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Edge_E335&oldid=412549](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Edge_E335&oldid=412549)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")