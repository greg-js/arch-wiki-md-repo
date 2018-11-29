Related articles

*   [Xorg/Keyboard configuration](/index.php/Xorg/Keyboard_configuration "Xorg/Keyboard configuration")
*   [Keyboard input](/index.php/Keyboard_input "Keyboard input")
*   [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console")

Keyboard mappings (keymaps) for [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"), console fonts and console maps are provided by the [kbd](https://www.archlinux.org/packages/?name=kbd) package (a dependency of [systemd](/index.php/Systemd "Systemd")), which also provides many low-level tools for managing virtual console. In addition, *systemd* also provides the *localectl* tool, which can control both the system [locale](/index.php/Locale "Locale") and keyboard layout settings for both the virtual console and Xorg.

## Contents

*   [1 Viewing keyboard settings](#Viewing_keyboard_settings)
*   [2 Keymaps](#Keymaps)
    *   [2.1 Listing keymaps](#Listing_keymaps)
    *   [2.2 Loadkeys](#Loadkeys)
    *   [2.3 Persistent configuration](#Persistent_configuration)
    *   [2.4 Creating a custom keymap](#Creating_a_custom_keymap)
        *   [2.4.1 Adding directives](#Adding_directives)
        *   [2.4.2 Other examples](#Other_examples)
        *   [2.4.3 Saving changes](#Saving_changes)
*   [3 Adjusting typematic delay and rate](#Adjusting_typematic_delay_and_rate)
    *   [3.1 Systemd service](#Systemd_service)

## Viewing keyboard settings

Use `localectl status` to view the current keyboard configurations.

## Keymaps

The keymap files are stored in the `/usr/share/kbd/keymaps/` directory tree. Usually one keymap file corresponds to one keyboard layout (the `include` statement can be used to share common parts and a keymap file can contain multiple layouts with some key combination used for switching). For more details see [keymaps(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/keymaps.5).

### Listing keymaps

The naming conventions of console keymaps are somewhat arbitrary, but usually they are based on:

*   [Language codes](https://en.wikipedia.org/wiki/ISO_639-1 "wikipedia:ISO 639-1"): where the language code is the same as its country code (e.g. `de` for German, or `fr` for French).
*   [Country codes](https://en.wikipedia.org/wiki/Country_code "wikipedia:Country code"): where variations of the same language are used in different countries (e.g.`uk` for United Kingdom English, or `us` for United States English); a list of country codes can also be found in [wikipedia:ISO 3166-1#Officially assigned code elements](https://en.wikipedia.org/wiki/ISO_3166-1#Officially_assigned_code_elements "wikipedia:ISO 3166-1").
*   [Keyboard layouts](https://en.wikipedia.org/wiki/Keyboard_layout "wikipedia:Keyboard layout"): where the layout is not related to a particular country or language (e.g. `dvorak` for the [Dvorak keyboard layout](https://en.wikipedia.org/wiki/Dvorak_Simplified_Keyboard "wikipedia:Dvorak Simplified Keyboard")).

For a list of all the available keymaps, use the command:

```
$ localectl list-keymaps

```

To search for a keymap, use the following command, replacing `*search_term*` with the code for your language, country, or layout:

```
$ localectl list-keymaps | grep -i *search_term*

```

Alternatively, using find:

```
$ find /usr/share/kbd/keymaps/ -type f

```

### Loadkeys

It is possible to set a keymap just for current session. This is useful for testing different keymaps, solving problems etc.

The *loadkeys* tool is used for this purpose, it is used internally by [systemd](/index.php/Systemd "Systemd") when loading the keymap configured in `/etc/vconsole.conf`. It can be used very simply for this purpose:

```
# loadkeys *keymap*

```

See [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) details.

### Persistent configuration

A persistent keymap can be set in `/etc/vconsole.conf`, which is read by [systemd](/index.php/Systemd "Systemd") on start-up. The `KEYMAP` variable is used for specifying the keymap. If the variable is empty or not set, the `us` keymap is used as default value. See [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) for all options. For example:

 `/etc/vconsole.conf` 
```
KEYMAP=uk
...

```

For convenience, *localectl* may be used to set console keymap. It will change the `KEYMAP` variable in `/etc/vconsole.conf` and also set the keymap for current session:

```
$ localectl set-keymap --no-convert *keymap*

```

The `--no-convert` option can be used to prevent `localectl` from automatically changing the [Xorg keymap](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") to the nearest match. See [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) for more information.

If required, the keymap from `/etc/vconsole.conf` can be loaded during early userspace by the `keymap` [mkinitcpio hook](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio").

### Creating a custom keymap

When using the console, you can use hotkeys to print a specific character. Moreover we can also print a sequence of characters and some escape sequences. Thus, if we print the sequence of characters constituting a command and afterwards an escape character for a new line, that command will be executed.

One method of doing this is editing the keymap file. However, since it will be rewritten anytime the package it belongs to is updated, editing this file is discouraged. It is better to integrate the existing keymap with a personal keymap. The `loadkeys` utility can do this.

First, create a keymap file. This keymap file can be anywhere, but one method is to mimic the directory hierarchy in `/usr/local`:

```
# mkdir -p /usr/local/share/kbd/keymaps
# vim /usr/local/share/kbd/keymaps/personal.map

```

As a side note, it is worth noting that such a personal keymap is useful also to redefine the behaviour of keys already treated by the default keymap: when loaded with `loadkeys`, the directives in the default keymap will be replaced when they conflict with the new directives and conserved otherwise. This way, only changes to the keymap must be specified in the personal keymap.

**Tip:** You can also edit an existing keymap located in the `/usr/share/kbd/keymaps/` directory tree. Keymaps have an *.map.gz* extension, for example `us.map.gz` is an American keymap. Just copy the keymap to `/usr/local/share/kbd/keymaps/personal.map.gz` and *gunzip* it.

#### Adding directives

Two kinds of directives are required in this personal keymap. First of all, the [keycode](/index.php/Extra_keyboard_keys "Extra keyboard keys") directives, which matches the format seen in the default keymaps. These directives associate a keycode with a keysym. Keysyms represent keyboard actions. The actions available include outputting character codes or character sequences, switching consoles or keymaps, booting the machine, and many other actions. The full currently active keymap can be obtained with

```
# dumpkeys -l

```

Most keysyms are intuitive. For example, to set key 112 to output an 'e', the directive will be:

```
keycode 112  = e

```

To set key 112 to output a euro symbol, the directive will be:

```
keycode 112 = euro

```

Some keysym are not immediately connected to a keyboard actions. In particular, the keysyms prefixed by a capital F and one to three digits (F1-F246) constituting a number greater than 30 are always free. This is useful directing a hotkey to output a sequence of characters and other actions:

```
keycode 112 = F70

```

Then, F70 can be bound to output a specific string:

```
string F70 = "Hello"

```

When key 112 is pressed, it will output the contents of F70\. In order to execute a printed command in a terminal, a newline escape character must be appended to the end of the command string. For example, to enter a system into hibernation, the following keymap is added:

```
string F70 = "sudo /usr/sbin/hibernate
"

```

#### Other examples

*   To make the Right Alt key same as Left Alt key (for Emacs), use the following line in your keymap. It will include the file `/usr/share/kbd/keymaps/i386/include/linux-with-two-alt-keys.inc`, check it for details.

```
include "linux-with-two-alt-keys"

```

*   To swap CapsLock with Escape (for Vim), remap the respective keycodes:

```
keycode 1 = Caps_Lock
keycode 58 = Escape

```

*   To make CapsLock another Control key, remap the respective keycode:

```
keycode 58 = Control

```

*   To swap CapsLock with Left Control key, remap the respective keycodes:

```
keycode 29 = Caps_Lock
keycode 58 = Control

```

#### Saving changes

In order to make use of the personal keymap, it must be loaded with *loadkeys*:

```
$ loadkeys /usr/local/share/kbd/keymaps/personal.map

```

However this keymap is only active for the current session. In order to load the keymap at boot, specify the full path to the file in the `KEYMAP` variable in [/etc/vconsole.conf](#Persistent_configuration). The file does not have to be gzipped as the official keymaps provided by [kbd](https://www.archlinux.org/packages/?name=kbd).

## Adjusting typematic delay and rate

The *typematic delay* indicates the amount of time (typically in milliseconds) a key needs to be pressed and held in order for the repeating process to begin. After the repeating process has been triggered, the character will be repeated with a certain frequency (usually given in Hz) specified by the *typematic rate*. These values can be changed using the *kbdrate* command. Note that these settings are configured separately for the virtual console and [for Xorg](/index.php/Keyboard_configuration_in_Xorg#Adjusting_typematic_delay_and_rate "Keyboard configuration in Xorg").

```
# kbdrate [-d *delay*] [-r *rate*]

```

For example to set a typematic delay to 200ms and a typematic rate to 30Hz, use the following command:

```
# kbdrate -d 200 -r 30

```

Issuing the command without specifying the delay and rate will reset the typematic values to their respective defaults; a delay of 250ms and a rate of 11Hz:

```
# kbdrate

```

### Systemd service

A systemd service can be used to set the keyboard rate. For example

 `/etc/systemd/system/kbdrate.service` 
```

[Unit]
Description=Keyboard repeat rate in tty.

[Service]
Type=oneshot
RemainAfterExit=yes
StandardInput=tty
StandardOutput=tty
ExecStart=/usr/bin/kbdrate -s -d 450 -r 60

[Install]
WantedBy=multi-user.target

```

Then [start/enable](/index.php/Start/enable "Start/enable") the `kbdrate.service` systemd service.