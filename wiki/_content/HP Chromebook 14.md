# HP Chromebook 14

This is a work in progress with information about the HP Chromebook 14 (FALCO)

The HP Chromebook 14 (and newer chromebooks in general) features a "legacy boot" mode that makes it easy to boot Linux and other operating systems. The legacy boot mode is provided by the [SeaBIOS](http://www.coreboot.org/SeaBIOS) payload of coreboot. SeaBIOS behaves like a traditional BIOS that boots into the GPT of a disk, and from there into your standard bootloaders like Syslinux and GRUB.

## Contents

*   [1 Installation](#Installation)
*   [2 Post Installation Configuration](#Post_Installation_Configuration)
    *   [2.1 Touchpad Configuration](#Touchpad_Configuration)
    *   [2.2 Keyboard Keymapping Fix](#Keyboard_Keymapping_Fix)
    *   [2.3 Adding hotkeys back](#Adding_hotkeys_back)
*   [3 Locating the Write-Protect Screw](#Locating_the_Write-Protect_Screw)
*   [4 See also](#See_also)

## Installation

Go to the [Chromebook](/index.php/Chromebook "Chromebook") page, read the [Introduction](/index.php/Chromebook#Introduction "Chromebook") and continue by following the [Installation](/index.php/Chromebook#Installation "Chromebook") guide.

## Post Installation Configuration

For information on general Chromebook post installation configuration (hotkeys, power key handling ...) see [Post installation configuration](/index.php/Chromebook#Post_installation_configuration "Chromebook") on the [Chromebook](/index.php/Chromebook "Chromebook") page.

### Touchpad Configuration

Add the Xorg touchpad configuration below for better usability (higher sensitivity).

 `/etc/X11/xorg.conf.d/50-cros-touchpad.conf` 

```
Section "InputClass" 
    Identifier      "touchpad peppy cyapa" 
    Driver          "synaptics"
    MatchIsTouchpad "on" 
    MatchDevicePath "/dev/input/event*" 
    MatchProduct    "cyapa" 
    Option          "FingerLow" "10" 
    Option          "FingerHigh" "10" 
EndSection
```

Reboot for the touchpad to become operational.

### Keyboard Keymapping Fix

We will create a custom hwdb config file to bypass the default mapping in `/usr/lib/udev/hwdb.d/60-keyboard.hwdb` of the keys between escape and power so they will work as F1-F10 and the search button as Super_L/Mod4.

Add the following to the new hwdb config file, save and exit.

 `/etc/udev/hwdb.d/90-chromebook-keyboard-fix.hwdb` 

```
# Chromebook 14 fix
evdev:atkbd:dmi:bvn*:bvr*:bd*:svnHewlett-Packard*:pnFalco:pvr*
 KEYBOARD_KEY_3b=f1
 KEYBOARD_KEY_3c=f2
 KEYBOARD_KEY_3d=f3
 KEYBOARD_KEY_3e=f4
 KEYBOARD_KEY_3f=f5
 KEYBOARD_KEY_40=f6
 KEYBOARD_KEY_41=f7
 KEYBOARD_KEY_42=f8
 KEYBOARD_KEY_43=f9
 KEYBOARD_KEY_44=f10
 KEYBOARD_KEY_db=leftmeta

```

Rebuild `hwdb.bin` by running

```
# udevadm hwdb --update

```

Reboot to load the updated hwdb database.

After each upgrade of [Systemd](/index.php/Systemd "Systemd"), its installation script will rebuild the database automatically so we don't need to take care of it.

See [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes#Using_udev "Map scancodes to keycodes") for more details.

### Adding hotkeys back

Once you've applied the above fix you can set the function and arrow keys to act similar to how they are in ChromeOS using a modifer key. The example below uses Mod4 (Search on the chromebook's keyboard). This can be changed to Control or Alt if you prefer.

First make sure you have all the needed packages: [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys), [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight), [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [xvkbd](https://www.archlinux.org/packages/?name=xvkbd), [xdotool](https://www.archlinux.org/packages/?name=xdotool).

Create `.xbindkeysrc` in your home folder:

 `~/.xbindkeysrc` 

```
#Delete
"xvkbd -xsendevent -text '\[Delete]'"
   Mod4 + BackSpace

#End
"xvkbd -xsendevent -text '\[End]'"
   Mod4 + Right

#Home
"xvkbd -xsendevent -text '\[Home]'"
   Mod4 + Left

#Page Down
"xvkbd -xsendevent -text '\[Page_Down]'"
   Mod4 + Down

#Page Up
"xvkbd -xsendevent -text '\[Page_Up]'"
   Mod4 + Up

#Volume Controls 
#Mute
"amixer sset Master toggle"
   Mod4 + F8 

#Volume Down
"amixer sset Master 2%-"
   Mod4 + F9 

#Volume Up
"amixer sset Master 2%+"
   Mod4 + F10

#Backlight
#Dim
"xbacklight -dec 10"
   Mod4 + F6 

#Brighten
"xbacklight -inc 10"
   Mod4 + F7 

#Back,Fwd,Reload as Multimedia Prev,Next,Play
#Play/Pause
"xdotool key XF86AudioPlay"
   Mod4 + F3

#Prev Track
"xdotool key XF86AudioPrev"
   Mod4 + F1 

#Next Track
"xdotool key XF86AudioNext"
   Mod4 + F2

```

To activate it when you login add

```
xbindkeys

```

to your .xinitrc, or whatever your DE uses for startup.

## Locating the Write-Protect Screw

**Warning:** There are 4 hidden screws under rubber stubs (not the rubber feet) at the bottom.

*   Remove the visible screws and another 4 hidden screws under rubber stubs (not the rubber feet) at the bottom.
*   Flip the laptop right side up and use a thin blunt object to pry the keyboard surface from the bottom half.
*   The bios screw is located to the left of the fan, it can be recognized by the fact that the copper circle it sits on is split in half "( )" vs "O". The screw connects the two halves, making the bios unwriteable.
*   Once this screw is removed, it's advisable to unplug the battery and plug it back in to ensure that the removal is recognized.

See disassembly pictures [[1]](http://imgur.com/a/aGSQC), [[2]](http://imgur.com/a/hFq7S) and [the location of the write-protect screw](http://i290.photobucket.com/albums/ll257/bond304/IMG_5313_zpsacbb2723.jpg).

## See also

*   [A HOWTO for replacing SSD](http://chromebook-falco.blogspot.com.es/2013/11/here-are-mechanics-of-ngff-ssd-removal.html)
*   [A log of how to replace ChromeOS with ArchLinux](https://github.com/somenxavier/falco/wiki/Events-log)
*   [Disassembly for replacing the screen](https://www.youtube.com/watch?v=efbM9dkDvSU)
*   [Disassembly instructions (official)](http://h10032.www1.hp.com/ctg/Manual/c03936089.pdf)

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Chromebook_14&oldid=399168](https://wiki.archlinux.org/index.php?title=HP_Chromebook_14&oldid=399168)"