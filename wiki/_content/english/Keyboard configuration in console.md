Related articles

*   [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")
*   [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts")

**Note:** This article covers only basic configuration without modifying layouts, mapping extra keys etc. See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") for these advanced topics.

Keyboard mappings (keymaps) for [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"), console fonts and console maps are provided by the [kbd](https://www.archlinux.org/packages/?name=kbd) package (a dependency of [systemd](/index.php/Systemd "Systemd")), which also provides many low-level tools for managing virtual console. In addition, *systemd* also provides the *localectl* tool, which can control both the system [locale](/index.php/Locale "Locale") and keyboard layout settings for both the virtual console and Xorg.

## Contents

*   [1 Viewing keyboard settings](#Viewing_keyboard_settings)
*   [2 Setting keyboard layout](#Setting_keyboard_layout)
    *   [2.1 Keymap codes](#Keymap_codes)
    *   [2.2 Persistent configuration](#Persistent_configuration)
    *   [2.3 Temporary configuration](#Temporary_configuration)
*   [3 Adjusting typematic delay and rate](#Adjusting_typematic_delay_and_rate)
    *   [3.1 Systemd service](#Systemd_service)

## Viewing keyboard settings

Use `localectl status` to view the current keyboard configurations.

## Setting keyboard layout

### Keymap codes

Usually one keymap file corresponds to one keyboard layout (the `include` statement can be used to share common parts and a keymap file can contain multiple layouts with some key combination used for switching). The keymap files are stored in the `/usr/share/kbd/keymaps/` directory tree.

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

### Persistent configuration

A persistent keymap can be set in `/etc/vconsole.conf`, which is read by [systemd](/index.php/Systemd "Systemd") on start-up. The `KEYMAP` variable is used for specifying the keymap. If the variable is empty or not set, the `us` keymap is used as default value. See [vconsole.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) for all options. For example:

 `/etc/vconsole.conf` 
```
KEYMAP=uk
...

```

For convenience, *localectl* may be used to set console keymap. It will change the `KEYMAP` variable in `/etc/vconsole.conf` and also set the keymap for current session:

```
$ localectl set-keymap --no-convert *keymap*

```

The `--no-convert` option can be used to prevent `localectl` from automatically changing the [Xorg keymap](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") to the nearest match. See [localectl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) for more information.

### Temporary configuration

It is possible to set a keymap just for current session. This is useful for testing different keymaps, solving problems etc.

The *loadkeys* tool is used for this purpose, it is used internally by [systemd](/index.php/Systemd "Systemd") when loading the keymap configured in `/etc/vconsole.conf`. It can be used very simply for this purpose:

```
# loadkeys *keymap*

```

See [loadkeys(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) details.

## Adjusting typematic delay and rate

The *typematic delay* indicates the amount of time (typically in miliseconds) a key needs to be pressed and held in order for the repeating process to begin. After the repeating process has been triggered, the character will be repeated with a certain frequency (usually given in Hz) specified by the *typematic rate*. These values can be changed using the *kbdrate* command. Note that these settings are configured seperately for the virtual console and [for Xorg](/index.php/Keyboard_configuration_in_Xorg#Adjusting_typematic_delay_and_rate "Keyboard configuration in Xorg").

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