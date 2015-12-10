# HP Envy 14

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

<td>xf86-video-radeon</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>atl1c</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>iwlagn</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

<td>uvcvideo</td>

</tr>

<tr>

<td>USB 3.0</td>

<td style="color:orange">**Partially Working**</td>

<td>xhci-hcd</td>

</tr>

<tr>

<td>USB 2.0</td>

<td style="color:green">**Working**</td>

<td>ehci-hcd</td>

</tr>

<tr>

<td>eSATA</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Function Keys</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Suspend to RAM</td>

<td style="color:green">**Working**</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Video](#Video)
        *   [2.2.1 Intel](#Intel)
        *   [2.2.2 AMD](#AMD)
            *   [2.2.2.1 Switching](#Switching)
    *   [2.3 Audio](#Audio)
        *   [2.3.1 HDMI](#HDMI)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Suspend to RAM](#Suspend_to_RAM)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Function Keys](#Function_Keys)

# Hardware

_CPU_ Intel Core i7 i7-2630QM (2 GHz Quad-core, 6 MB Cache, hyperthreading, Turbo Boost (2.9 GHz))

_Mainboard_ Intel HM65

_RAM_ 8 GB (2x4GB)

_Display_ 14.5" HD LED (1366x768)

_Graphics adapter_ AMD Radeon HD 6630M, 1GB memory

_Soundcard_ Intel HD Audio

_Network_ Atheros Communications AR8151 v2.0 Gigabit Ethernet, Intel Corporation Centrino Advanced-N 6230 Wireless

_Hard disk_ 750 GB 7200rpm SATA

_Webcam_ Quanta Computer, Inc.

_Touchpad_ Synaptics ClickPad

# Configuration

This article is based on HP Envy 14 2090eo (LS782EA) model. Wireless chip might be different on other regions.

## CPU

Works out of the box. See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for more information on power saving. Both cpufrequtils and cpupower work. Latter is recommended for additional features.

## Video

This laptop has two graphics chips, one on the CPU and the other AMD Radeon 6630M with dedicated 1 GB RAM.

**Note:** that the screen goes black after booting because the backlight is disabled by default. Increase back light using shift-fn-f3 key combination. After installing add command `w /sys/class/backlight/acpi_video0/brightness - - - - 1` to `/etc/tmpfiles.d/local.conf` for turning the back light on automatically.

### Intel

After enabling using vga_swictheroo works perfectly. No Xorg configuration needed.

### AMD

Radeon card is used by default. No Xorg configuration needed.

#### Switching

WIP, see [Tackling the Switchable graphics](http://linuxenvy.blogspot.com/2011/01/tackling-switchable-graphics.html).

## Audio

Works out of the box.

### HDMI

Works out of the box. (Tested only with AMD graphics)

## Touchpad

Works out of the box.

## Suspend to RAM

Works out of the box.

## Webcam

Works out of the box.

## Function Keys

Works out of the box, including keyboard back light activation (shift-fn-f5).

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Envy_14&oldid=384051](https://wiki.archlinux.org/index.php?title=HP_Envy_14&oldid=384051)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")