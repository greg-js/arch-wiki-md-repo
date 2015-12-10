# Lenovo ThinkPad T440s

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article covers the installation and configuration of Arch Linux on a Lenovo T440s laptop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 UEFI vs BIOS](#UEFI_vs_BIOS)
    *   [1.2 Driver Selection](#Driver_Selection)
    *   [1.3 Tp_smapi](#Tp_smapi)
*   [2 Tweaks](#Tweaks)
    *   [2.1 Screen resolution](#Screen_resolution)
    *   [2.2 Backlight](#Backlight)
    *   [2.3 Touchpad](#Touchpad)

## Installation

### UEFI vs BIOS

The T440s has SecureBoot and UEFI enabled by default. Unless you know you want to use UEFI, it's simpler to get Arch installed if booting is switched to BIOS-only. In the BIOS/EFI menu, set booting to "Legacy only" (which uses BIOS emulation instead of EFI).

### Driver Selection

<table class="wikitable">

<tbody>

<tr>

<th>Device</th>

<th>Driver Package</th>

<th>Free Software?</th>

</tr>

<tr>

<td>Video</td>

<td>[Intel graphics](/index.php/Intel_graphics "Intel graphics")</td>

<td>Yes</td>

</tr>

<tr>

<td>ClickPad</td>

<td>[libinput](/index.php/Libinput "Libinput")</td>

<td>Yes</td>

</tr>

<tr>

<td>Wireless/Bluetooth</td>

<td>iwlwifi*</td>

<td>Yes</td>

</tr>

<tr>

<td>Finger Print Reader</td>

<td>[Fprint](/index.php/Fprint "Fprint") since V 0.6.0</td>

<td>yes</td>

</tr>

</tbody>

</table>

Note*: Depending on what you picked when ordering the laptop, you might have a stock ThinkPad wireless card. Check [this page](http://www.thinkwiki.org/wiki/Drivers) for more information.

### Tp_smapi

See [tp_smapi](/index.php/Tp_smapi "Tp smapi") and a configuration for [ThinkPad T420](/index.php/Lenovo_ThinkPad_T420#Tp_smapi "Lenovo ThinkPad T420").

## Tweaks

### Screen resolution

In order to use the real dpi value create the file (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<default monitor>"
    DisplaySize            309 173    # In millimeters
EndSection

```

Otherwise the defalut resolution is set to 96dpi.

### Backlight

Controlling the backlight can be a little tricky- on my T440s, KDE's default brightness controls would only do 0%, 50%, and 100% brightness. GNOME 3 worked out of the box, but it would never save the last-used brightness value on reboot. A workaround for both of these issues is to use [[1]](https://www.archlinux.org/packages/extra/x86_64/xorg-xbacklight/). An example script for setting the backlight on boot is:

 `~/.config/autostart/backlight-hack.desktop` 

```
[Desktop Entry]
Comment=backlight
Exec=xbacklight -set 40
GenericName=backlight hack
Name=Backlight hack
Terminal=false
TerminalOptions=
Type=Application

```

If you just want to set the current brightness level, run:

```
xbacklight -set <value>

```

### Touchpad

*   [Good configuration for touchpad](http://rscircus.org/post/72978821261/t440s-clickpad-fix-which-feels-good)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T440s&oldid=410922](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T440s&oldid=410922)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")