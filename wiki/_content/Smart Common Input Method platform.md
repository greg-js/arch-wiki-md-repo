# Smart Common Input Method platform

Related articles

*   [IBus](/index.php/IBus "IBus")
*   [Fcitx](/index.php/Fcitx "Fcitx")
*   [UIM](/index.php/UIM "UIM")

[SCIM](https://en.wikipedia.org/wiki/Smart_Common_Input_Method "wikipedia:Smart Common Input Method") is an input method framework developed by Su Zhe (or James Su) around 2001, similar to [IBus](/index.php/IBus "IBus") or [UIM](/index.php/UIM "UIM").

Its stated goals are to:

*   Act as an unified front-end for current available input method libraries. Currently bindings to [UIM](/index.php/UIM "UIM") and [m17n](http://www.m17n.org/m17n-lib-en/) library are available.
*   Act as a language engine of [IIIMF](https://en.wikipedia.org/wiki/Internet/Intranet_Input_Method_Framework "wikipedia:Internet/Intranet Input Method Framework") input method framework.
*   Provide as many native [IMEngines](http://www.scim-im.org/projects/imengines) as possible.
*   Support as many input method protocols/interfaces as possible.
*   Support as many operating systems as possible.

Nowadays, SCIM is also:

*   Highly modularized.
*   Very flexible in its architecture, it can be used as a dynamically loaded library as well as a C/S input method environment.
*   Simple from a programming interface perspective.
*   Fully i18n enabled with support for UCS-4/UTF-8 encoding.
*   Easy to configure through its unified configuration framework.

## Contents

*   [1 Installing SCIM](#Installing_SCIM)
    *   [1.1 Installing Input Method Engines](#Installing_Input_Method_Engines)
*   [2 Configure SCIM](#Configure_SCIM)
    *   [2.1 A simple scenario](#A_simple_scenario)
    *   [2.2 Note for GTK+](#Note_for_GTK.2B)
        *   [2.2.1 Note for GNOME, Xfce, LXDE](#Note_for_GNOME.2C_Xfce.2C_LXDE)
        *   [2.2.2 Note for KDE3](#Note_for_KDE3)
    *   [2.3 Locale-related files](#Locale-related_files)
        *   [2.3.1 Further troubleshooting with locales](#Further_troubleshooting_with_locales)
    *   [2.4 Executing SCIM](#Executing_SCIM)
        *   [2.4.1 Note for GNOME](#Note_for_GNOME)
        *   [2.4.2 Note for KDE](#Note_for_KDE)
*   [3 Bugs](#Bugs)
    *   [3.1 LWJGL (Lightweight Java Game Library) losing keyboard focus](#LWJGL_.28Lightweight_Java_Game_Library.29_losing_keyboard_focus)
    *   [3.2 Chrome/Chromium doesn't take input](#Chrome.2FChromium_doesn.27t_take_input)
*   [4 Links](#Links)

## Installing SCIM

SCIM can be [installed](/index.php/Pacman "Pacman") with the package [scim](https://www.archlinux.org/packages/?name=scim), available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Installing Input Method Engines

Currently the SCIM project has a wide range of input methods (some may need other libraries), covering more than 30 languages, including (Simplified/Traditional) Chinese, Japanese, Korean and many European languages. These are some of the examples (more can be found [here](http://www.scim-im.org/projects/imengines)):

*   **Chinese Smart PinYin**: [scim-pinyin](https://www.archlinux.org/packages/?name=scim-pinyin).
*   **Chinese WuBi or other tables based**: [scim-tables](https://www.archlinux.org/packages/?name=scim-tables).
*   **Japanese**: [scim-anthy](https://www.archlinux.org/packages/?name=scim-anthy).
*   **Korean**: [scim-hangul](https://www.archlinux.org/packages/?name=scim-hangul)

## Configure SCIM

Configuring SCIM correctly requires the following three steps:

1.  Exporting some environment variables that specify the used input method.
2.  Modifying locale related files.
3.  Finally, starting SCIM.

### A simple scenario

If you just need SCIM to work urgently in any Desktop Environment or Window Manager, put these lines into `/etc/xprofile` or `~/.xprofile` and then reboot:

 `~/.xprofile` 

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="scim"
export QT_IM_MODULE="scim"
scim -d

```

These lines can be added to other files that are run at startup, such as: `/etc/profile`, `~/.profile`, `~/.xinitrc` or `~/.config/openbox/autostart` (when using [Openbox](/index.php/Openbox "Openbox")).

**Note:** The first environment variable conflicts with some (unusual) options like `XMODIFIERS=urxvt`.

This is a very basic example for configuring XIM (X Input Method) to work with SCIM. XIM is not recommended because it has quite some limitations.

### Note for GTK+

If you use [GNOME](/index.php/GNOME "GNOME"), edit `/etc/gtk-2.0/gtk.immodules` by adding follow content at the end:

 `/etc/gtk-2.0/gtk.immodules` 

```
"/usr/lib/gtk-2.0/immodules/im-scim.so"
"scim" "SCIM Input Method" "scim" "/usr/share/locale" "ja:ko:zh"

```

If your `LC_CTYPE` or `LANG` is _en_US.UTF-8_, change `ja:ko:zh` to `en:ja:ko:zh`.

After making those changes, be sure to reboot. You can find out what input method modules are available on your system by executing `gtk-query-immodules-2.0`.

If SCIM does not work with GTK+ applications after these changes, check that the GTK_IM_MODULE_FILE environment variable is set to `/etc/gtk-2.0/gtk.immodules`.

You can use another file (in this example `~/.immodules`) that contains the necessary information about input methods modules by adding these lines in the file you selected in the [section above](#A_simple_scenario).

```
gtk-query-immodules-2.0 > ~/.immodules
export GTK_IM_MODULE_FILE=~/.immodules

```

#### Note for GNOME, Xfce, LXDE

If you are using GNOME, Xfce or LXDE and Qt applications do not pick up the `export QT_IM_MODULE="scim"` variable, you can use scim-bridge. To use _scim-bridge_ instead, export the following:

```
export QT_IM_MODULE="scim-bridge"

```

#### Note for KDE3

For KDE3 you should `export QT_IM_MODULE="xim"` instead of _scim_ and also install [qtimm](http://www.scim-im.org/projects/scim_qtimm)] for Qt3.

### Locale-related files

If your keyboard locale is not `en_US.UTF-8` (or `en_US.utf8`), you have to modify the first line of `~/.scim/global` (or `/etc/scim/global` to apply these settings to all users) according to the following example:

```
/SupportedUnicodeLocales = en_US.UTF-8,de_CH.UTF-8

```

and replace your `de_CH.UTF-8` with your locale.

**Note:** Your locale has to be active (i.e. you have to uncomment it in `/etc/locale-gen` and then execute `locale-gen` as root) _and_ has to be supported by SCIM (most *.UTF-8 locales are).

If you do not know which locales you have active at the moment, you can check it:

```
locale -a

```

(alternatively you can look at `/etc/locale.gen`).

#### Further troubleshooting with locales

If after you have install SCIM and the necessary input tables, SCIM still does not work, then you need to set the `LC_CTYPE` environmental variable in `/etc/profile` to the locale you plan to use. Simply create an entry for LC_CTYPE such as:

```
LC_CTYPE="zh_CN.UTF-8"              # if you want to type simplified chinese

```

Finally you need to generate the locale using the `locale-gen` command.

### Executing SCIM

SCIM can be run by just executing the `scim` command, although it is common to start SCIM as a daemon:

```
scim -d

```

You can put the above command in a script file and execute it automatically. Usual places are `~/.xinitrc` (after environment variables and before DE/WM), `/etc/profile` (after environment variables) or `~/.config/openbox/autostart` (after environment variables and possibly after some sleep command).

#### Note for GNOME

In case you use GNOME as your desktop environment, the command above does not seem to work as expected. Instead, you have to execute the following:

```
 scim -f x11 -c simple -d

```

If you want SCIM to start automatically at startup, go to System > Preferences > Session and create a new command with the line above.

**Note:** If you use the line `scim -f socket -c socket -d` instead, the configuration of your SCIM will be unmodifiable.

#### Note for KDE

In case you use KDE as a desktop environment, the command above does not seem to work as expected. Instead, you have to execute the following:

```
 scim -f socket -c socket -d

```

## Bugs

### LWJGL (Lightweight Java Game Library) losing keyboard focus

See [these](http://www.scim-im.org/forums#nabble-td2499750) [two](http://ubuntuforums.org/showthread.php?t=1641861) forum posts for a solution.

### Chrome/Chromium doesn't take input

Edit the .xinitrc or .xsession file.

 `~/.xprofile` 

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="xim"
export QT_IM_MODULE="scim"
scim -d

```

This is a rather sloppy workaround. Also, even with this workaround, Korean users may find scim unusable with Chrome/Chromium, as the preedit string disappears when the space bar or other modifier keys are pressed at the end of a word.

## Links

*   [See the official news page for more details](https://www.archlinux.org/news/166/).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Smart_Common_Input_Method_platform&oldid=401115](https://wiki.archlinux.org/index.php?title=Smart_Common_Input_Method_platform&oldid=401115)"