Related articles

*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

Prerequisite for modifying the key mapping is knowing how a key press results in a symbol:

1.  The keyboard sends a [scancode](https://en.wikipedia.org/wiki/Scancode "wikipedia:Scancode") to the computer.
2.  The Linux kernel maps the scancode to a **keycode**, see [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes").
3.  The [keyboard layout](https://en.wikipedia.org/wiki/Keyboard_layout "wikipedia:Keyboard layout") maps the keycode to a symbol or **keysym**, depending on what [modifier keys](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key") are pressed.
    *   For the [Linux console](/index.php/Linux_console "Linux console"), see [Linux console/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration").
    *   For [Xorg](/index.php/Xorg "Xorg") and [Wayland](/index.php/Wayland "Wayland"), see [Xorg/Keyboard configuration](/index.php/Xorg/Keyboard_configuration "Xorg/Keyboard configuration").

Most of your keys should already have a *keycode*, or at least a *scancode*. Keys without a *scancode* are not recognized by the kernel; these can include additional keys from "gaming" keyboards, etc.

In Xorg, some *keysyms* (e.g. `XF86AudioPlay`, `XF86AudioRaiseVolume` etc.) can be mapped to actions (i.e. launching an external application). See [Xorg keyboard configuration#Keybinding](/index.php/Xorg_keyboard_configuration#Keybinding "Xorg keyboard configuration") for details.

In Linux console, some *keysyms* (e.g. `F1` to `F246`) can be mapped to certain actions (e.g. switch to other console or print some sequence of characters). See [Console keyboard configuration#Creating a custom keymap](/index.php/Console_keyboard_configuration#Creating_a_custom_keymap "Console keyboard configuration") for details.

## Contents

*   [1 Identifying scancodes](#Identifying_scancodes)
    *   [1.1 Using showkey](#Using_showkey)
    *   [1.2 Using evtest](#Using_evtest)
    *   [1.3 Using dmesg](#Using_dmesg)
*   [2 Identifying keycodes](#Identifying_keycodes)
    *   [2.1 Identifying keycodes in console](#Identifying_keycodes_in_console)
    *   [2.2 Identifying keycodes in Xorg](#Identifying_keycodes_in_Xorg)

## Identifying scancodes

### Using showkey

The traditional way to get a *scancode* is to use the [showkey(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/showkey.1) utility. *showkey* waits for a key to be pressed, or exits if no keys are pressed within 10 seconds. For *showkey* to work you need to be in a [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"), not in a graphical environment or logged in via a network connection. Run the following command:

```
# showkey --scancodes

```

and try to push keyboard keys; you should see *scancodes* being printed to the output.

### Using evtest

For USB keyboards, it is apparently necessary to use [evtest(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/evtest.1) from the [evtest](https://www.archlinux.org/packages/?name=evtest) package instead of *showkey* [[1]](https://ask.fedoraproject.org/en/question/46201/how-to-map-scancodes-to-keycodes/):

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

The Linux keycodes are defined in `/usr/include/linux/input-event-codes.h` (see the `KEY_` variables).

### Identifying keycodes in console

The *keycodes* for [virtual console](/index.php/Virtual_console "Virtual console") are reported by the [showkey(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/showkey.1) utility. *showkey* waits for a key to be pressed and if none is during 10 seconds it quits. To execute *showkey* you need to be in a virtual console, not in a graphical environment. Run the following command:

```
# showkey --keycodes

```

and try to push keyboard keys; you should see *keycodes* being printed to the output.

### Identifying keycodes in Xorg

**Note:** The Xorg *keycodes* are 8 larger than the Linux *keycodes*.[[2]](https://cgit.freedesktop.org/xorg/driver/xf86-input-evdev/tree/src/evdev.c)

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