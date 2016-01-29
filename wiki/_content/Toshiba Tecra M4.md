# Toshiba Tecra M4

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section should provide only information specific to the hardware. Content from the general wiki articles should not be [duplicated](/index.php/Category:Laptops "Category:Laptops"); crosslink it instead.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Toshiba Tecra M4#](https://wiki.archlinux.org/index.php/Talk:Toshiba_Tecra_M4))

The Tecra M4 is a convertible-PC produced by Toshiba.

Mine includes 512MByte of RAM, 60Gbyte SATA-HDD, NVidia 6200 graphics card and a serial Wacom tablet.

This will be a short introduction on how to make everything work perfectly.

This tutorial is a bit work in progress so stay tuned ;)

## Contents

*   [1 Installation](#Installation)
*   [2 Wireless drivers](#Wireless_drivers)
*   [3 Installing Wacom Tablet](#Installing_Wacom_Tablet)
*   [4 Optimizing battery lifetime](#Optimizing_battery_lifetime)
    *   [4.1 CPUFreq](#CPUFreq)
    *   [4.2 PHC](#PHC)
*   [5 Mapping screen-key to something that makes sense](#Mapping_screen-key_to_something_that_makes_sense)
*   [6 Script for changing orientation](#Script_for_changing_orientation)
*   [7 What does not work](#What_does_not_work)

# Installation

Just boot the ArchLinux Installation disc and install the basics

# Wireless drivers

This PC contains an intel wireless card, that is supported by the ipw2200 driver. See [Wireless network configuration#ipw2100 and ipw2200](/index.php/Wireless_network_configuration#ipw2100_and_ipw2200 "Wireless network configuration").

# Installing Wacom Tablet

See [Wacom Tablet](/index.php/Wacom_Tablet "Wacom Tablet").

# Optimizing battery lifetime

## CPUFreq

Just install [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")

## PHC

Optionally use [PHC](/index.php/PHC "PHC") to undervolt the processor.

# Mapping screen-key to something that makes sense

by default, the buttons on the screen return the combinations Super_L + [1-7] I prefer this tiny joystick to use as page up and page down - so I tried xmodmap

```
$ nano -w .Xmodmap

```

change the line of keycode 134 to

```
keycode 134 = Mode_switch NoSymbol Mode_switch NoSymbol Super_R

```

and the following lines:

```
keycode  10 = 1 exclam Prior Prior onesuperior exclamdown
keycode  11 = 2 quotedbl Next Next twosuperior oneeighth
keycode  12 = 3 section Prior Prior threesuperior sterling
keycode  13 = 4 dollar Next Next onequarter currency

```

that produces: tablet is landscape and orientation "normal" - joystick up -> page up, down -> page down tablet is portrait and orientation "left" - joystick up -> page up, down -> page down

# Script for changing orientation

```
# nano -w /usr/bin/rotate

```

```
#!/bin/bash

#### rotate.sh - A script for tablet PCs to rotate the display.

## This software is licensed under the CC-GNU GPL.
## [http://creativecommons.org/licenses/GPL/2.0/](http://creativecommons.org/licenses/GPL/2.0/)

## [https://wiki.archlinux.org/index.php/Tablet_PC](https://wiki.archlinux.org/index.php/Tablet_PC)
## REQUIRES: linuxwacom ([http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Main_Page](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Main_Page))

#### Function(s)
function set_normal {
 xrandr -o normal
 xsetwacom set "stylus" Rotate NONE
 xsetwacom set "cursor" Rotate NONE
 xsetwacom set "eraser" Rotate NONE
 orientation="normal"
}

function set_left {
 xrandr -o left
 xsetwacom set "stylus" Rotate CCW
 xsetwacom set "cursor" Rotate CCW
 xsetwacom set "eraser" Rotate CCW
 orientation="left"
}

#### Variable(s)
orientation="$(xrandr --query --verbose | grep '(normal left inverted right) 0mm x 0mm' | awk '{print $5}')"

#### Main
if [ "$orientation" = "normal" ]; then
	set_left
elif [ "$orientation" = "right" ]; then
	set_normal
elif [ "$orientation" = "inverted" ]; then
	set_normal
elif [ "$orientation" = "left" ]; then
	set_normal
fi

#### EOF

```

```
# chmod 0755 /usr/bin/rotate

```

I customized the given script a bit, because turning right and inverted made no sense for me. This script can now be used with gnome-keybinding-properties

# What does not work

*   Mapping joystick to page_up/down AND using the rotate button in gnome-keybinding-properties at the same time
*   sound does work, if you reload the snd_intel8x0 module after boot - do not know, why

Retrieved from "[https://wiki.archlinux.org/index.php?title=Toshiba_Tecra_M4&oldid=400569](https://wiki.archlinux.org/index.php?title=Toshiba_Tecra_M4&oldid=400569)"