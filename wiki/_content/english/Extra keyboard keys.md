Related articles

*   [Xorg keyboard configuration](/index.php/Xorg_keyboard_configuration "Xorg keyboard configuration")
*   [Console keyboard configuration](/index.php/Console_keyboard_configuration "Console keyboard configuration")
*   [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes")
*   [Xmodmap](/index.php/Xmodmap "Xmodmap")

Many keyboards include some *special keys* (also called *hotkeys* or *multimedia keys*), which are supposed to execute an application or print special characters (not included in the standard national keymaps). [udev](/index.php/Udev "Udev") contains a large database of mappings specific to individual keyboards, so common keyboards usually work out of the box. If you have very recent or uncommon piece of hardware, you may need to adjust the mapping manually.

Prerequisite for modifying the key mapping is knowing how a key press results in a symbol:

1.  The keyboard sends a [scancode](https://en.wikipedia.org/wiki/Scancode "wikipedia:Scancode") to the computer.
2.  The Linux kernel maps the scancode to a **keycode**, see [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes").
3.  The keyboard layout maps the keycode to a symbol or **keysym**, depending on what [modifier keys](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key") are pressed, see [Console keyboard configuration](/index.php/Console_keyboard_configuration "Console keyboard configuration") or [XKB](/index.php/XKB "XKB")/[xmodmap](/index.php/Xmodmap "Xmodmap").

Most of your keys should already have a *keycode*, or at least a *scancode*. Keys without a *scancode* are not recognized by the kernel; these can include additional keys from 'gaming' keyboards, etc.

In Xorg, some *keysyms* (e.g. `XF86AudioPlay`, `XF86AudioRaiseVolume` etc.) can be mapped to actions (i.e. launching an external application). See [Xorg keyboard configuration#Mapping keysyms to actions](/index.php/Xorg_keyboard_configuration#Mapping_keysyms_to_actions "Xorg keyboard configuration") for details.

In Linux console, some *keysyms* (e.g. `F1` to `F246`) can be mapped to certain actions (e.g. switch to other console or print some sequence of characters). See [Console keyboard configuration#Creating a custom keymap](/index.php/Console_keyboard_configuration#Creating_a_custom_keymap "Console keyboard configuration") for details.

## Contents

*   [1 Identifying scancodes](#Identifying_scancodes)
    *   [1.1 Using showkey](#Using_showkey)
    *   [1.2 Using evtest](#Using_evtest)
    *   [1.3 Using dmesg](#Using_dmesg)
*   [2 Mapping scancodes to keycodes](#Mapping_scancodes_to_keycodes)
*   [3 Mapping keycodes to keysyms](#Mapping_keycodes_to_keysyms)
    *   [3.1 In Xorg](#In_Xorg)
*   [4 Laptops](#Laptops)
    *   [4.1 Apple MacBooks](#Apple_MacBooks)
    *   [4.2 Asus M series](#Asus_M_series)
    *   [4.3 Asus N56VJ (or possibly others)](#Asus_N56VJ_.28or_possibly_others.29)
    *   [4.4 Lenovo T460p (or possibly others)](#Lenovo_T460p_.28or_possibly_others.29)
*   [5 Gaming Keyboards](#Gaming_Keyboards)
    *   [5.1 Cooler Master CM Storm QuickFire TK](#Cooler_Master_CM_Storm_QuickFire_TK)
    *   [5.2 Corsair K series keyboards](#Corsair_K_series_keyboards)
    *   [5.3 Logitech G series G710 and 710+](#Logitech_G_series_G710_and_710.2B)
*   [6 See also](#See_also)

## Identifying scancodes

### Using showkey

The traditional way to get a *scancode* is to use the *showkey* utility. *showkey* waits for a key to be pressed, or exits if no keys are pressed within 10 seconds. For *showkey* to work you need to be in a [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"), not in a graphical environment or logged in via a network connection. Run the following command:

```
# showkey --scancodes

```

and try to push keyboard keys; you should see *scancodes* being printed to the output.

### Using evtest

For USB keyboards, it is apparently necessary to use *evtest* from the [evtest](https://www.archlinux.org/packages/?name=evtest) package instead of *showkey*:[[1]](https://ask.fedoraproject.org/en/question/46201/how-to-map-scancodes-to-keycodes/)

```
# evtest /dev/input/event12
...
Event: time 1434666536.001123, type 4 (EV_MSC), code 4 (MSC_SCAN), value 70053
Event: time 1434666536.001123, type 1 (EV_KEY), code 69 (KEY_NUMLOCK), value 0
Event: time 1434666536.001123, -------------- EV_SYN ------------

```

Use the "value" field of `MSC_SCAN`. This example shows that NumLock has scancode 70053 and keycode 69.

### Using dmesg

**Note:** This method does not provide *scancodes* for all keys, it only identifies the unknown keys.

You can get the *scancode* of a key by pressing the desired key and looking the output of `dmesg` command. For example, if you get:

```
Unknown key pressed (translated set 2, code 0xa0 on isa0060/serio0

```

then the *scancode* you need is `0xa0`.

## Mapping scancodes to keycodes

See the main article: [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes").

## Mapping keycodes to keysyms

### In Xorg

See the main article: [xmodmap](/index.php/Xmodmap "Xmodmap").

## Laptops

### Apple MacBooks

All the required information is available on the [Apple Keyboard](/index.php/Apple_Keyboard "Apple Keyboard") dedicated article.

### Asus M series

In order to have control over the light sensor and the multimedia keys on your Asus machine, you should use the following command:

```
# echo 1 > /sys/devices/platform/asus_laptop/ls_switch

```

To have it run on boot create a [Systemd tmpfile](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/devices/platform/asus_laptop/ls_switch - - - - 1

```

**Note:** This may work also for other Asus notebook models.

### Asus N56VJ (or possibly others)

If most of your special keys do not work, try loading the asus-nb-wmi kernel module with

```
# modprobe asus-nb-wmi

```

then check xev again. If you combine this with the acpi_osi="!Windows 2012" boot option, you may get weird results in xev, so try not using it. If this did fix things, make sure to make the module load at boot with methods described in [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

### Lenovo T460p (or possibly others)

Out of the box, the backlight keys (on F5, F6) might not be available, even via the `/dev/input` interface. To fix this, follow [Backlight#Kernel command-line options](/index.php/Backlight#Kernel_command-line_options "Backlight").

## Gaming Keyboards

Gaming keyboards have some special features which may cause them to "misbehave" in Linux.

### Cooler Master CM Storm QuickFire TK

This keyboard has two features that could cause confusion in Linux: N-Key Rollover and the Win-Lock Key.

N-Key Rollover can [cause problems with the Function keys](https://bbs.archlinux.org/viewtopic.php?id=170877). To disable N-key rollover, hold down the FN lock key (next to right-ctrl) until it lights up, then hold Escape and press 6 to switch to 6-key rollover. Hold down the FN lock key to disable the Fn lock.

The Win-Lock Key completely disables the Super (Windows) keys. Simply press the FN lock key and F12 together to toggle Win-Lock on and off.

### Corsair K series keyboards

There is a winlock button on these keyboards that can disable the use of the Super (Windows) keys. This button is located at the top right of the keyboard next to the num and capslock buttons. CKB can be used to disable this functionality entirely preventing further locking. However, in a default state, simply pressing the button would enable the Super (Windows) keys again.

### Logitech G series G710 and 710+

This keyboard has a row of 6 programmable G keys. In order to use them as intended by Logitech, you need to install [sidewinderd](https://aur.archlinux.org/packages/sidewinderd/) and [start](/index.php/Start "Start") `sidewinderd.service`.

## See also

*   [Enabling Keyboard Multimedia Keys](http://wiki.linuxquestions.org/wiki/Configuring_keyboards#Enabling_Keyboard_Multimedia_Keys) - guide on LinuxQuestions wiki
*   [Multimedia Keys](http://www.gentoo-wiki.info/HOWTO_Use_Multimedia_Keys) on [Gentoo Wiki Archives](http://www.gentoo-wiki.info/)