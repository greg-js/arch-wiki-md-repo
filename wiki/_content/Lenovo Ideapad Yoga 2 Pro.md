# Lenovo Ideapad Yoga 2 Pro

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Missing templates, poorly organized (Discuss in [Talk:Lenovo Ideapad Yoga 2 Pro#](https://wiki.archlinux.org/index.php/Talk:Lenovo_Ideapad_Yoga_2_Pro))

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Graphics</td>

<td style="color:green">**Working**</td>

<td>xf86-video-intel</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working***</td>

<td>iwlwifi</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchscreen</td>

<td style="color:green">**Working**</td>

<td>usbtouchscreen</td>

</tr>

<tr>

<td>Accelerometer</td>

<td style="color:red">**Not Working**</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="color:green">**Working**</td>

<td>xf86-input-synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:blue">**Unknown**</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="color:green">**Working**</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Installation](#Installation)
*   [2 The ideapad_laptop module](#The_ideapad_laptop_module)
*   [3 Keyboard and other hardware keys](#Keyboard_and_other_hardware_keys)
    *   [3.1 Keyboard special keys](#Keyboard_special_keys)
    *   [3.2 Hardware keys on right side](#Hardware_keys_on_right_side)
*   [4 Touchscreen](#Touchscreen)
    *   [4.1 Multitouch gestures](#Multitouch_gestures)
    *   [4.2 Touchscreen button](#Touchscreen_button)
    *   [4.3 Touchscreen stops working after suspension](#Touchscreen_stops_working_after_suspension)
*   [5 ACPI](#ACPI)
    *   [5.1 Touchpad](#Touchpad)
    *   [5.2 Backlight](#Backlight)
    *   [5.3 Battery](#Battery)
*   [6 Graphics](#Graphics)
*   [7 Rotation/Conversion](#Rotation.2FConversion)
*   [8 See also](#See_also)

## Installation

Installing Arch on the HiDPI screen may be difficult as the text will be hard to read. To make the font more readable, before you hit install, [disable mode settings](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting"). Hit Tab in the arch linux boot menu and append the option `nomodeset` along with `nomodeset` kernel parameter. For Intel graphics card you need to add `i915.modeset=0` and for Nvidia graphics card you need to add `nouveau.modeset=0`. For Nvidia Optimus dual-graphics system, you need to add all the three kernel parameters (i.e. `"nomodeset i915.modeset=0 nouveau.modeset=0"`).

Be aware, adding nomodeset prevents the kernel from identifying the monitor. As a result brightness adjustment and xrandr won't work. This line should probably be removed after installation.

## The ideapad_laptop module

Several problems come up if the ideapad_laptop module is in use. Namely, it blocks the network card and generates a massive stream of warning from the USB subsystem such as:

```
Dec  5 08:40:44 localhost kernel: [  290.632613] xhci_hcd 0000:00:14.0: ep 0x81 - asked for 15360 bytes, 15117 bytes untransferred
Dec  5 08:40:44 localhost kernel: [  290.735110] xhci_hcd 0000:00:14.0: ep 0x81 - asked for 15360 bytes, 15117 bytes untransferred
Dec  5 08:40:44 localhost kernel: [  290.837534] xhci_hcd 0000:00:14.0: ep 0x81 - asked for 15360 bytes, 15117 bytes untransferred
Dec  5 08:40:44 localhost kernel: [  290.940070] xhci_hcd 0000:00:14.0: ep 0x81 - asked for 15360 bytes, 15117 bytes untransferred
Dec  5 08:40:44 localhost kernel: [  291.042570] xhci_hcd 0000:00:14.0: ep 0x81 - asked for 15360 bytes, 15117 bytes untransferred

```

You can silence these in the short run by running:

```
# dmesg -D

```

And you can unblock the wireless card by running:

```
# rfkill unblock wlan

```

However, in the long term, you will probably want to blacklist the `ideapad_laptop` driver so that neither of these occur in the first place. I am yet to find a disadvantage to doing so.

## Keyboard and other hardware keys

To access boot menu or BIOS settings, you must use the alternate power button, next to the standard one.

No keypad available at all.

### Keyboard special keys

**Note:** A working keymap means that there is some output in `xev` when the key combination is pressed OR that the functionality is built in and "just works". It does not means that the keymap is linked to the functionality. For that it is often necessary to add a keyboard shortcut [by the method of your choice](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg") or to use a desktop shell with built-in shortcut support for the keycode in question. For some of the keys the function operates on a BIOS level and no shortcut is needed.

**Note:** BIOS has a setting to flip the behavior of the FN key.

<table class="wikitable">

<tbody>

<tr>

<th>Keys</th>

<th>Function</th>

<th>X sees</th>

</tr>

<tr>

<td>`Fn+F1`</td>

<td>Audio mute/unmute</td>

<td>XF86AudioMute</td>

</tr>

<tr>

<td>`Fn+F2`</td>

<td>Audio volume down</td>

<td>XF86AudioLowerVolume</td>

</tr>

<tr>

<td>`Fn+F3`</td>

<td>Audio volume up</td>

<td>XF86AudioRaiseVolume</td>

</tr>

<tr>

<td>`Fn+F4`</td>

<td>Close application</td>

<td>`Alt_L+F4`</td>

</tr>

<tr>

<td>`Fn+F5`</td>

<td>Refresh page</td>

<td>`F5`</td>

</tr>

<tr>

<td>`Fn+F6`</td>

<td>Disable Touchpad</td>

<td> ?</td>

</tr>

<tr>

<td>`Fn+F7`</td>

<td>Airplane mode</td>

<td> ?</td>

</tr>

<tr>

<td>`Fn+F8`</td>

<td>Unknown</td>

<td>`Alt_L+Tab`</td>

</tr>

<tr>

<td>`Fn+F9`</td>

<td>Turn off LCD</td>

<td> ?</td>

</tr>

<tr>

<td>`Fn+F10`</td>

<td>Toggle display</td>

<td>`Super+p`</td>

</tr>

<tr>

<td>`Fn+F11`</td>

<td>Dim LCD backlight</td>

<td>XF86MonBrightnessDown</td>

</tr>

<tr>

<td>`Fn+F12`</td>

<td>Brighten LCD backlight</td>

<td>XF86MonBrightnessUp</td>

</tr>

</tbody>

</table>

### Hardware keys on right side

From hinge to front:

```
XF86AudioRaiseVolume
XF86AudioLowerVolume
Super_L+o

```

## Touchscreen

Touchscreen USB device seems to come and go if the `usbtouchscreen` module is not loaded.

### Multitouch gestures

You need to install [Touchegg](https://aur.archlinux.org/packages/Touchegg/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") in order to enable multitouch gestures. Optionally, you can install [touchegg-gce-git](https://aur.archlinux.org/packages/touchegg-gce-git/)<sup><small>AUR</small></sup> as a graphical front-end. See more details in the [dedicated wiki page](/index.php/Touchegg "Touchegg").

**Tip:** If you use [Gnome Shell](/index.php/Gnome_Shell "Gnome Shell") you should start `touchegg` before it, in order to avoid conflicts.

### Touchscreen button

The touchscreen button with a Windows logo is mapped as `Super`. However, `key_down` and `key_up` are generated simultaneously on touch release. The haptic feedback (vibration) when touching this button is currently not controllable via software.

### Touchscreen stops working after suspension

Sometimes touchscreen stops working after resuming from suspension mode. You should be able to fix the problem reloading the `usbhid` and `usbtouchscreen` kernel modules:

```
# modprobe -r usbhid usbtouchscreen

```

## ACPI

I modified `/etc/acpi/default.sh` to allow for some debugging and additional features (see below):

```
#!/bin/sh
set $*
group=${1%%/*}
device=$2
id=$3
value=$4
log_unhandled() {
       logger "ACPI event unhandled: $*"
}
case "$group" in
       button)
               case "$action" in
                       power)
                               /etc/acpi/actions/powerbtn.sh
                               ;;
                       lid)
                               /etc/acpi/actions/lid.sh
                               ;;
                       *)      log_unhandled $* ;;
               esac
               ;;
       ac_adapter)
               case "$value" in
                       *)      log_unhandled $* ;;
               esac
               ;;
       *)      echo $* > /dev/tty5
               log_unhandled $* ;;
esac

```

### Touchpad

The touchpad sends random input from time to time, especially when lid is closed. If you like your computer to keep running when the lid is closed, you may want to disable the touchpad with ACPI events:

/etc/acpi/actions/lid.sh

```
#!/bin/bash
export DISPLAY=:0
if grep closed /proc/acpi/button/lid/LID0/state
then
       synclient TouchpadOff=1 2>/dev/tty5 && echo "lid closed, disabling touchpad" >/dev/tty5
else
       synclient TouchpadOff=0 2>/dev/tty5 && echo "lid open, eênabling touchpad" >/dev/tty5
fi

```

Of course, the echo statement is optional and for debug purposes.

### Backlight

With newer kernels (I am currently using `3.17.6-1-ARCH`) backlight works out-of-the-box.

"old" (ref needed) kernels require boot argument

```
acpi_backlight=vendor

```

Screen backlight brightness can be manually set with

```
# echo $VAL > /sys/class/backlight/intel_backlight/brightness

```

with $VAL between 0 and 937

It's possible that you will get a permission denied error, in which case you can run

```
 # chmod a+rw /sys/class/backlight/intel_backlight/brightness

```

which makes the brightness editable by any user.

### Battery

Battery info can be accessed with

```
ls /sys/class/power_supply/BAT1/*

```

Unfortunately, the values obtained there have no units (older Lenovo products had rates in mA, battery voltage, etc.)

## Graphics

Steam crashes trying to run games complaining about missing i965 module. It seems some applications treat it as accelerated, and some do not.

Resolution seems to be not so well supported by some desktop environments/window managers. Gnome-based DEs like Cinnamon and Mate, as well as XFCE and fvwm seem to work fine.

Users may wish to boost font-sizes, as the HiDPI screen can be hard to read in some settings.

If you have trouble detecting a display with the micro hdmi port, consider filing the plastic on the male hdmi plug back a bit (not on the laptop). See [here](https://forums.lenovo.com/t5/Lenovo-Edge-Yoga-Flex-Laptops/Yoga-2-Pro-micro-HDMi-issue-SOLVED/td-p/1297269). The ruber case can prevent the plug from inserting fully.

## Rotation/Conversion

You can easily rotate screen with xrandr, however it does not rotate touchscreen/touchpad input which makes it fairly awkward to use. There is a [project](https://github.com/wolneykien/xrandr-align) attempting to address this. Keyboard hardware-disables in tablet mode, but touchpad is still active which needs to be addressed. No ACPI or keycode signals appear to be emitted for the various screen rotation states.

## See also

*   The LinLap site has some good information - see [[1]](http://www.linlap.com/lenovo_ideapad_yoga_2_pro);
*   a good Review of Arch Linux on a HiDPI Lenovo Yoga 2 Pro by KeithCU with useful comments [[2]](http://keithcu.com/wordpress/?p=3270);
*   an installation guide written by Ubuntu users: [[3]](http://askubuntu.com/questions/367963/ubuntu-on-lenovo-yoga-2-pro).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_Yoga_2_Pro&oldid=414415](https://wiki.archlinux.org/index.php?title=Lenovo_Ideapad_Yoga_2_Pro&oldid=414415)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")