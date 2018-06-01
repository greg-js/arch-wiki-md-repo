Related articles

*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

Prerequisite for modifying the key mapping is knowing how a key press results in a symbol:

1.  The keyboard sends a [scancode](https://en.wikipedia.org/wiki/Scancode "wikipedia:Scancode") to the computer.
2.  The Linux kernel converts the scancode to a [keycode](#Keycodes), see [#Mapping scancodes to keycodes](#Mapping_scancodes_to_keycodes).
3.  The [keyboard layout](https://en.wikipedia.org/wiki/Keyboard_layout "wikipedia:Keyboard layout") maps the keycode to a symbol or **keysym**, depending on what [modifier keys](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key") are pressed:
    *   For the Linux console, [KBD](http://kbd-project.org/) is used, see [Console keyboard configuration](/index.php/Console_keyboard_configuration "Console keyboard configuration").
    *   For [Xorg](/index.php/Xorg "Xorg") and [Wayland](/index.php/Wayland "Wayland"), the [X Keyboard Extension](/index.php/X_Keyboard_Extension "X Keyboard Extension") is used, see [Xorg keyboard configuration](/index.php/Xorg_keyboard_configuration "Xorg keyboard configuration").

Most of your keys should already have a *keycode*, or at least a *scancode*. Keys without a *scancode* are not recognized by the kernel; these can include additional keys from 'gaming' keyboards, etc.

In Xorg, some *keysyms* (e.g. `XF86AudioPlay`, `XF86AudioRaiseVolume` etc.) can be mapped to actions (i.e. launching an external application). See [Xorg keyboard configuration#Keybinding](/index.php/Xorg_keyboard_configuration#Keybinding "Xorg keyboard configuration") for details.

In Linux console, some *keysyms* (e.g. `F1` to `F246`) can be mapped to certain actions (e.g. switch to other console or print some sequence of characters). See [Console keyboard configuration#Creating a custom keymap](/index.php/Console_keyboard_configuration#Creating_a_custom_keymap "Console keyboard configuration") for details.

**Tip:** [systemd](/index.php/Systemd "Systemd")'s [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) can be used to define the keyboard layout for both Xorg and the virtual console.

## Contents

*   [1 Identifying scancodes](#Identifying_scancodes)
    *   [1.1 Using showkey](#Using_showkey)
    *   [1.2 Using evtest](#Using_evtest)
    *   [1.3 Using dmesg](#Using_dmesg)
*   [2 Keycodes](#Keycodes)
*   [3 Mapping scancodes to keycodes](#Mapping_scancodes_to_keycodes)
    *   [3.1 Using setkeycodes](#Using_setkeycodes)

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

## Keycodes

The Linux keycodes are defined in `/usr/include/linux/input-event-codes.h` (see the `KEY_` variables).

**Note:** The Xorg keycodes are 8 larger than the Linux keycodes.[[2]](https://cgit.freedesktop.org/xorg/driver/xf86-input-evdev/tree/src/evdev.c)

To identify keycodes in the console, see [Console keyboard configuration#Identifying keycodes](/index.php/Console_keyboard_configuration#Identifying_keycodes "Console keyboard configuration").

To identify keycodes in [Xorg](/index.php/Xorg "Xorg"), see [Xorg keyboard configuration#Identifying keycodes](/index.php/Xorg_keyboard_configuration#Identifying_keycodes "Xorg keyboard configuration").

## Mapping scancodes to keycodes

Mapping *scancodes* to *keycodes* is universal and not specific to Linux console or Xorg, which means that changes to this mapping will be effective in both.

There are two ways of mapping *scancodes* to *keycodes*:

*   [Using udev's hwdb](/index.php/Scancode_mapping_with_hwdb "Scancode mapping with hwdb")
*   [#Using setkeycodes](#Using_setkeycodes)

The preferred method is to use *udev* because it uses hardware information (which is a quite reliable source) to choose the keyboard model in a database. It means that if your keyboard model has been found in the database, your keys are recognized *out of the box*.

### Using setkeycodes

[setkeycodes(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setkeycodes.8) is a tool to load *scancodes*-to-*keycodes* mapping table into Linux kernel. Its usage is:

```
# setkeycodes *scancode* *keycode* ...

```

It is possible to specify multiple pairs at once. *Scancodes* are given in hexadecimal, *keycodes* in decimal.

**Note:** Apparently *setkeycodes* does not work with USB keyboards (Linux 3.14.44-1-lts):
```
# setkeycodes 45 30     # bind NumLock (0x45) to KEY_A (30) on AT keyboard
(successful)
# setkeycodes 70053 30  # bind NumLock (0x70053) to KEY_A (30) on USB keyboard
KDSETKEYCODE: Invalid argument
failed to set scancode 620d3 to keycode 31

```