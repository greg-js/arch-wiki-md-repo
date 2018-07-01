Related articles

*   [Xorg keyboard configuration](/index.php/Xorg_keyboard_configuration "Xorg keyboard configuration")
*   [Console keyboard configuration](/index.php/Console_keyboard_configuration "Console keyboard configuration")
*   [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes")
*   [Xmodmap](/index.php/Xmodmap "Xmodmap")

Many keyboards include some *special keys* (also called *hotkeys* or *multimedia keys*), which are supposed to execute an application or print special characters (not included in the standard national keymaps). [udev](/index.php/Udev "Udev") contains a large database of mappings specific to individual keyboards, so common keyboards usually work out of the box. If you have very recent or uncommon piece of hardware, you may need to adjust the mapping manually.

Prerequisite for modifying the key mapping is knowing how a key press results in a symbol:

1.  The keyboard sends a [scancode](https://en.wikipedia.org/wiki/Scancode "wikipedia:Scancode") to the computer.
2.  The Linux kernel maps the scancode to a **keycode**, see [#Mapping scancodes to keycodes](#Mapping_scancodes_to_keycodes).
3.  The keyboard layout maps the keycode to a symbol or **keysym**, depending on what [modifier keys](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key") are pressed, see [#Mapping keycodes to keysyms](#Mapping_keycodes_to_keysyms).

Most of your keys should already have a *keycode*, or at least a *scancode*. Keys without a *scancode* are not recognized by the kernel; these can include additional keys from "gaming" keyboards, etc.

In Xorg, some *keysyms* (e.g. `XF86AudioPlay`, `XF86AudioRaiseVolume` etc.) can be mapped to actions (i.e. launching an external application). See [Xorg keyboard configuration#Keybinding](/index.php/Xorg_keyboard_configuration#Keybinding "Xorg keyboard configuration") for details.

In Linux console, some *keysyms* (e.g. `F1` to `F246`) can be mapped to certain actions (e.g. switch to other console or print some sequence of characters). See [Console keyboard configuration#Creating a custom keymap](/index.php/Console_keyboard_configuration#Creating_a_custom_keymap "Console keyboard configuration") for details.

## Contents

*   [1 Identifying scancodes](#Identifying_scancodes)
    *   [1.1 Using showkey](#Using_showkey)
    *   [1.2 Using evtest](#Using_evtest)
    *   [1.3 Using dmesg](#Using_dmesg)
*   [2 Identifying keycodes](#Identifying_keycodes)
    *   [2.1 In console](#In_console)
    *   [2.2 In Xorg](#In_Xorg)
*   [3 Mapping scancodes to keycodes](#Mapping_scancodes_to_keycodes)
*   [4 Mapping keycodes to keysyms](#Mapping_keycodes_to_keysyms)
    *   [4.1 In console](#In_console_2)
    *   [4.2 In Xorg](#In_Xorg_2)
*   [5 Laptops](#Laptops)
    *   [5.1 Apple MacBooks](#Apple_MacBooks)
    *   [5.2 Asus M series](#Asus_M_series)
    *   [5.3 Asus N56VJ (or possibly others)](#Asus_N56VJ_.28or_possibly_others.29)
    *   [5.4 Lenovo T460p (or possibly others)](#Lenovo_T460p_.28or_possibly_others.29)
*   [6 Gaming Keyboards](#Gaming_Keyboards)
    *   [6.1 Cooler Master CM Storm QuickFire TK](#Cooler_Master_CM_Storm_QuickFire_TK)
    *   [6.2 Corsair K series keyboards](#Corsair_K_series_keyboards)
    *   [6.3 Logitech G series G710 and 710+](#Logitech_G_series_G710_and_710.2B)
*   [7 See also](#See_also)

## Identifying scancodes

### Using showkey

The traditional way to get a *scancode* is to use the *showkey* utility. *showkey* waits for a key to be pressed, or exits if no keys are pressed within 10 seconds. For *showkey* to work you need to be in a [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"), not in a graphical environment or logged in via a network connection. Run the following command:

```
# showkey --scancodes

```

and try to push keyboard keys; you should see *scancodes* being printed to the output.

### Using evtest

For USB keyboards, it is apparently necessary to use *evtest* from the [evtest](https://www.archlinux.org/packages/?name=evtest) package instead of *showkey* [[1]](https://ask.fedoraproject.org/en/question/46201/how-to-map-scancodes-to-keycodes/):

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

## Identifying keycodes

**Note:** The Xorg *keycodes* are larger than the Linux *keycodes* by 8\. [[2]](https://cgit.freedesktop.org/xorg/driver/xf86-input-evdev/tree/src/evdev.c)

### In console

The *keycodes* for [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") are reported by the *showkey* utility. *showkey* waits for a key to be pressed and if none is during 10 seconds it quits. To execute *showkey* you need to be in a virtual console, not in a graphical environment. Run the following command:

```
# showkey --keycodes

```

and try to push keyboard keys; you should see *keycodes* being printed to the output.

### In Xorg

The *keycodes* used by [Xorg](/index.php/Xorg "Xorg") are reported by a utility called [xev(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xev.1), which is provided by the [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) package. Of course to execute *xev*, you need to be in a graphical environment, not in the console.

With the following command you can start *xev* and show only the relevant parts:

```
 $ xev | awk -F'[ )]+' '/^KeyPress/ { a[NR+2] } NR in a { printf "%-3s %s
", $5, $8 }'

```

Here is an example output:

```
38  a
55  v
54  c
50  Shift_L
133 Super_L
135 Menu

```

[Xbindkeys](/index.php/Xbindkeys#Identifying_keycodes "Xbindkeys") is another wrapper to *xev* that reports *keycodes*.

If you press a key and nothing appears in the terminal, it means that either the key does not have a *scancode*, the *scancode* is not mapped to a *keycode*, or some other process is capturing the keypress. If you suspect that a process listening to X server is capturing the keypress, you can try running *xev* from a clean X session:

```
$ xinit /usr/bin/xterm -- :1

```

## Mapping scancodes to keycodes

See the main article: [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes").

## Mapping keycodes to keysyms

### In console

See [Keyboard configuration in console#Creating a custom keymap](/index.php/Keyboard_configuration_in_console#Creating_a_custom_keymap "Keyboard configuration in console").

### In Xorg

See [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension") and [xmodmap](/index.php/Xmodmap "Xmodmap").

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