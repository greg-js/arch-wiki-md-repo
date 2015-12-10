# Acer Aspire One D250

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

There are a lot of netbooks under the Aspire One banner. Here's a third-party website that lists them (at least up through 2009): [Aspire One Cheatsheet](http://netbookscoop.com/buyers-guide/aspire-one-cheatsheets/)

*   Booted with acpi=off to keep from hanging on acpi module loading
*   Had to drop to other console, wipe partition table with fdisk before cfdisk would work

See the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") for more information.

## Contents

*   [1 Wifi](#Wifi)
*   [2 Xorg](#Xorg)
*   [3 Hardware](#Hardware)
    *   [3.1 Fn Keycodes](#Fn_Keycodes)

## Wifi

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

## Xorg

See [Xorg](/index.php/Xorg "Xorg") and [Intel graphics](/index.php/Intel_graphics "Intel graphics").

## Hardware

Here's lspci:

```
 00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
 00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
 00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
 00:1b.0 Audio device: Intel Corporation N10/ICH 7 Family High Definition Audio Controller (rev 02)
 00:1c.0 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 1 (rev 02)
 00:1c.1 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 2 (rev 02)
 00:1c.2 PCI bridge: Intel Corporation N10/ICH 7 Family PCI Express Port 3 (rev 02)
 00:1d.0 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #1 (rev 02)
 00:1d.1 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #2 (rev 02)
 00:1d.2 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #3 (rev 02)
 00:1d.3 USB controller: Intel Corporation N10/ICH 7 Family USB UHCI Controller #4 (rev 02)
 00:1d.7 USB controller: Intel Corporation N10/ICH 7 Family USB2 EHCI Controller (rev 02)
 00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
 00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
 00:1f.1 IDE interface: Intel Corporation 82801G (ICH7 Family) IDE Controller (rev 02)
 00:1f.2 SATA controller: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA AHCI Controller (rev 02)
 00:1f.3 SMBus: Intel Corporation N10/ICH 7 Family SMBus Controller (rev 02)
 01:00.0 Ethernet controller: Atheros Communications Inc. AR242x / AR542x Wireless Network Adapter (PCI-Express) (rev 01)
 03:00.0 Ethernet controller: Atheros Communications AR8132 Fast Ethernet (rev c0)

```

### Fn Keycodes

The Aspire One US keyboard when operating under WinXP has a number of special keys which are accessed by holding down the Function/Fn key and the relevant key. Some of these operate under Arch as well, but most do not.

<table class="wikitable"><caption>**Fn+ Data**</caption>

<tbody>

<tr>

<th>Fn+</th>

<th>Action in WinXP</th>

<th>Console Keycode/Effect</th>

<th>X Keycode/Effect</th>

</tr>

<tr>

<td>Left Arrow</td>

<td>LCD Brighten</td>

<td>112; works OOB but also types "?" character</td>

<td>No symbol; works OOB</td>

</tr>

<tr>

<td>Down Arrow</td>

<td>Volume Down</td>

<td>114</td>

<td>XF86AudioLowerVolume</td>

</tr>

<tr>

<td>Right Arrow</td>

<td>LCD Dim</td>

<td>118; works OOB but also types "?" character</td>

<td>plusminus; works OOB but also types +/- symbol</td>

</tr>

<tr>

<td>Pg Up</td>

<td>Home</td>

<td>102</td>

<td>Home</td>

</tr>

<tr>

<td>Up Arrow</td>

<td>Volume Up</td>

<td>115</td>

<td>XF86AudioRaiseVolume</td>

</tr>

<tr>

<td>Pg Dn</td>

<td>End</td>

<td>107</td>

<td>End</td>

</tr>

<tr>

<td>m</td>

<td>Keypad 0</td>

<td>82; works with NumLk on</td>

<td>with Fn gives KP_Insert; works with NumLk on</td>

</tr>

<tr>

<td>.</td>

<td>Keypad .</td>

<td>83; works with NumLk on</td>

<td>with Fn gives KP_Delete; works with NumLk on</td>

</tr>

<tr>

<td>/</td>

<td>Keypad +</td>

<td>78; works with NumLk on</td>

<td>works</td>

</tr>

<tr>

<td>j</td>

<td>Keypad 1</td>

<td>79; works with NumLk on</td>

<td>with Fn gives KP_End; works with NumLk on</td>

</tr>

<tr>

<td>k</td>

<td>Keypad 2</td>

<td>80; works with NumLk on</td>

<td>with Fn gives KP_Down; works with NumLk on</td>

</tr>

<tr>

<td>l</td>

<td>Keypad 3</td>

<td>81; works with NumLk on</td>

<td>with Fn gives KP_Next; works with NumLk on</td>

</tr>

<tr>

<td> ;</td>

<td>Keypad -</td>

<td>74; works with NumLk on</td>

<td>with Fn gives KP_; works with NumLk on</td>

</tr>

<tr>

<td>u</td>

<td>Keypad 4</td>

<td>75; works with NumLk on</td>

<td>with Fn gives KP_Left; works with NumLk on</td>

</tr>

<tr>

<td>l</td>

<td>Keypad 5</td>

<td>76; works with NumLk on</td>

<td>with Fn gives KP_Begin; works with NumLk on</td>

</tr>

<tr>

<td>o</td>

<td>Keypad 6</td>

<td>77; works with NumLk on</td>

<td>with Fn gives KP_Right; works with NumLk on</td>

</tr>

<tr>

<td>p</td>

<td>Keypad *</td>

<td>55; works with NumLk on</td>

<td>works</td>

</tr>

<tr>

<td>7</td>

<td>Keypad 7</td>

<td>71;</td>

</tr>

<tr>

<td>8</td>

<td>Keypad 8</td>

<td>72;</td>

</tr>

<tr>

<td>9</td>

<td>Keypad 9</td>

<td>73;</td>

</tr>

<tr>

<td>0</td>

<td>Keypad /</td>

<td>98;</td>

</tr>

<tr>

<td>F1</td>

<td>Launch Fn key help</td>

<td>None</td>

</tr>

<tr>

<td>F2</td>

<td>Launch System Properties</td>

<td>None</td>

</tr>

<tr>

<td>F3</td>

<td>Launch Power Options</td>

<td>None</td>

</tr>

<tr>

<td>F4</td>

<td>Sleep Mode</td>

<td>None</td>

</tr>

<tr>

<td>F5</td>

<td>Toggle to external display</td>

<td>225</td>

</tr>

<tr>

<td>F6</td>

<td>Turn off LCD backlight</td>

<td>Works OOB</td>

</tr>

<tr>

<td>F7</td>

<td>Turn touchpad off/on</td>

<td>Works OOB</td>

</tr>

<tr>

<td>F8</td>

<td>Mute/unmute</td>

<td>None</td>

</tr>

<tr>

<td>F11</td>

<td>NumLk</td>

<td>None; works (including LED)</td>

</tr>

<tr>

<td>F12</td>

<td>Scr Lk</td>

<td>None</td>

</tr>

</tbody>

</table>

As you can see, some of the stuff "Just Works" and some of the stuff (Fn+F1, F2, F3) will never work, since it doesn't produce a keycode of any sort. I used Compiz keybindings deal with the things in the middle and to compensate for the things that won't ever work.

<table class="wikitable"><caption>**Keybindings**</caption>

<tbody>

<tr>

<th>Keys</th>

<th>Action in WinXP</th>

<th>Bound Action</th>

<th>Commandline</th>

</tr>

<tr>

<td>Alt+F1</td>

<td>Launch Fn key help</td>

<td>Launch Xorg man page browser</td>

<td>export MANPATH=/usr/share/man; xman -notopbox</td>

</tr>

<tr>

<td>Alt+F2</td>

<td>Launch System Properties</td>

<td>Launch GTK hardware browser</td>

<td>/usr/bin/gksu /usr/sbin/lshw-gtk</td>

</tr>

<tr>

<td>F3</td>

<td>Launch Power Options</td>

<td>Launch GTK power properties browser</td>

<td>/usr/bin/gnome-power-statistics</td>

</tr>

<tr>

<td>F4</td>

<td>Sleep Mode</td>

<td>Suspend to RAM</td>

<td>/usr/bin/dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Suspend</td>

</tr>

<tr>

<td>F5</td>

<td>Toggle to external display</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_One_D250&oldid=377630](https://wiki.archlinux.org/index.php?title=Acer_Aspire_One_D250&oldid=377630)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")