# Fujitsu-Siemens Amilo Se 1520

This info may be helpful in addition to the Arch Linux Installation guide.

## Contents

*   [1 SOUND](#SOUND)
*   [2 TOUCHPAD](#TOUCHPAD)
*   [3 WIRELESS LAN](#WIRELESS_LAN)
*   [4 ACPI](#ACPI)
*   [5 HOTKEYS, SPECIAL BUTTONS](#HOTKEYS.2C_SPECIAL_BUTTONS)
*   [6 See also](#See_also)

## SOUND

Works poorly in Linux. Alsa is able to determine driver, but SPDIF doesn't work and external microphone too. Luckily internal microphone (above LCD) works good, though you can't change its' volume or disable it in **alsamixer**.

## TOUCHPAD

Install the synaptics driver with

```
    pacman -S synaptics

```

In xorg.conf

```
Section "ServerLayout"
	Identifier     "Layout0"
	Screen         0 "Screen_local" 0 0
	InputDevice    "Keyboard0" "CoreKeyboard"
	InputDevice    "TouchPad" "CorePointer"
	InputDevice    "ExtMouse" "SendCoreEvents"
EndSection

Section "InputDevice"
	Identifier  "TouchPad"
	Driver      "synaptics"
	Option	    "Protocol" "Auto"
	Option	    "Emulate3Buttons"
	Option	    "Device" "/dev/input/mouse0"
	Option	    "VertEdgeScroll" "true"
	Option	    "HorizEdgeScroll" "true"
	Option	    "SHMConfig" "true"
EndSection

Section "InputDevice"
	Identifier  "ExtMouse"
	Driver      "mouse"
	Option	    "Protocol" "Auto"
	Option	    "Device" "/dev/input/mice"
EndSection

```

If you just change **Driver** to **synaptics**, external mouse will not work at all. This way you will have external mouse working and horizontal scrool on touch pad.

Also, I would recommend you to add following in ~/.xinitrc:

```
syndaemon -i 0.5 -d

```

It will disable touch pad, while you typing.

## WIRELESS LAN

Fortunately, we have Linux native driver **ipw3945**, just install it and use **wifi-radar**

## ACPI

You will need to install **powersave** and add "powersaved" into _/etc/rc.conf_.

## HOTKEYS, SPECIAL BUTTONS

Alt+Function key commands work ok, but the special buttons on the left side of the keyboard do not work out of the box.

## See also

*   This report is listed at the [TuxMobil: Linux Laptop and Notebook Installation Guides Survey: Fujitsu-Siemens - FSC](http://tuxmobil.org/fujitsu.html).
*   See my personal page [about](http://wiki.mobbing-gegner.de/AmiloSi1520), feel free a help

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fujitsu-Siemens_Amilo_Se_1520&oldid=345613](https://wiki.archlinux.org/index.php?title=Fujitsu-Siemens_Amilo_Se_1520&oldid=345613)"