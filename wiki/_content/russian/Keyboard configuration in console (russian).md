**Состояние перевода:** На этой странице представлен перевод статьи [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console"). Дата последней синхронизации: 23 января 2017‎‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Keyboard_configuration_in_console&diff=0&oldid=466395).

**Примечание:** В этой статье описана лишь базовая настройка без модификации раскладок, назначения действий для дополнительных клавиш и т.п. Информацию по этим темам можно найти в статье [Дополнительные клавиши](/index.php/%D0%94%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D1%88%D0%B8 "Дополнительные клавиши")

Keyboard mappings (keymaps) for [virtual console](https://en.wikipedia.org/wiki/ru:%D0%92%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C and keyboard layout settings for both the virtual console and Xorg.

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

A persistent keymap can be set in `/etc/vconsole.conf`, which is read by [systemd](/index.php/Systemd "Systemd") on start-up. The `KEYMAP` variable is used for specifying the keymap. If the variable is empty or not set, the `us` keymap is used as default value. See `man 5 vconsole.conf` for all options. For example:

 `/etc/vconsole.conf` 
```
KEYMAP=uk
...

```

For convenience, *localectl* may be used to set console keymap. It will change the `KEYMAP` variable in `/etc/vconsole.conf` and also set the keymap for current session:

```
$ localectl set-keymap --no-convert *keymap*

```

The `--no-convert` option can be used to prevent `localectl` from automatically changing the [Xorg keymap](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") to the nearest match. See `man localectl` for more information.

### Temporary configuration

It is possible to set a keymap just for current session. This is useful for testing different keymaps, solving problems etc.

The *loadkeys* tool is used for this purpose, it is used internally by [systemd](/index.php/Systemd "Systemd") when loading the keymap configured in `/etc/vconsole.conf`. It can be used very simply for this purpose:

```
# loadkeys *keymap*

```

See `man 1 loadkeys` details.

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