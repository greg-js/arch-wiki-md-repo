There are a lot of netbooks under the Aspire One banner. Here's a third-party website that lists them (at least up through 2009): [Aspire One Cheatsheet](http://netbookscoop.com/buyers-guide/aspire-one-cheatsheets/)

*   Booted with acpi=off to keep from hanging on acpi module loading
*   Had to drop to other console, wipe partition table with fdisk before cfdisk would work

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

<caption>**Fn+ Data**</caption>
| Fn+ | Action in WinXP | Console Keycode/Effect | X Keycode/Effect |
| Left Arrow | LCD Brighten | 112; works OOB but also types "?" character | No symbol; works OOB |
| Down Arrow | Volume Down | 114 | XF86AudioLowerVolume |
| Right Arrow | LCD Dim | 118; works OOB but also types "?" character | plusminus; works OOB but also types +/- symbol |
| Pg Up | Home | 102 | Home |
| Up Arrow | Volume Up | 115 | XF86AudioRaiseVolume |
| Pg Dn | End | 107 | End |
| m | Keypad 0 | 82; works with NumLk on | with Fn gives KP_Insert; works with NumLk on |
| . | Keypad . | 83; works with NumLk on | with Fn gives KP_Delete; works with NumLk on |
| / | Keypad + | 78; works with NumLk on | works |
| j | Keypad 1 | 79; works with NumLk on | with Fn gives KP_End; works with NumLk on |
| k | Keypad 2 | 80; works with NumLk on | with Fn gives KP_Down; works with NumLk on |
| l | Keypad 3 | 81; works with NumLk on | with Fn gives KP_Next; works with NumLk on |
|  ; | Keypad - | 74; works with NumLk on | with Fn gives KP_; works with NumLk on |
| u | Keypad 4 | 75; works with NumLk on | with Fn gives KP_Left; works with NumLk on |
| l | Keypad 5 | 76; works with NumLk on | with Fn gives KP_Begin; works with NumLk on |
| o | Keypad 6 | 77; works with NumLk on | with Fn gives KP_Right; works with NumLk on |
| p | Keypad * | 55; works with NumLk on | works |
| 7 | Keypad 7 | 71; |
| 8 | Keypad 8 | 72; |
| 9 | Keypad 9 | 73; |
| 0 | Keypad / | 98; |
| F1 | Launch Fn key help | None |
| F2 | Launch System Properties | None |
| F3 | Launch Power Options | None |
| F4 | Sleep Mode | None |
| F5 | Toggle to external display | 225 |
| F6 | Turn off LCD backlight | Works OOB |
| F7 | Turn touchpad off/on | Works OOB |
| F8 | Mute/unmute | None |
| F11 | NumLk | None; works (including LED) |
| F12 | Scr Lk | None |

As you can see, some of the stuff "Just Works" and some of the stuff (Fn+F1, F2, F3) will never work, since it doesn't produce a keycode of any sort. I used Compiz keybindings deal with the things in the middle and to compensate for the things that won't ever work.

<caption>**Keybindings**</caption>
| Keys | Action in WinXP | Bound Action | Commandline |
| Alt+F1 | Launch Fn key help | Launch Xorg man page browser | export MANPATH=/usr/share/man; xman -notopbox |
| Alt+F2 | Launch System Properties | Launch GTK hardware browser | /usr/bin/gksu /usr/sbin/lshw-gtk |
| F3 | Launch Power Options | Launch GTK power properties browser | /usr/bin/gnome-power-statistics |
| F4 | Sleep Mode | Suspend to RAM | /usr/bin/dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Suspend |
| F5 | Toggle to external display |