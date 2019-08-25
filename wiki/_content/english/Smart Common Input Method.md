[SCIM](https://en.wikipedia.org/wiki/Smart_Common_Input_Method "wikipedia:Smart Common Input Method") is an [input method](/index.php/Input_method "Input method") framework developed by Su Zhe (or James Su) around 2001, similar to [IBus](/index.php/IBus "IBus") or [Uim](/index.php/Uim "Uim").

Its stated goals are to:

*   Act as an unified front-end for current available input method libraries. Currently bindings to [uim](/index.php/Uim "Uim") and [m17n](http://www.m17n.org/m17n-lib-en/) library are available.
*   Act as a language engine of [IIIMF](https://en.wikipedia.org/wiki/Internet/Intranet_Input_Method_Framework "wikipedia:Internet/Intranet Input Method Framework") input method framework.
*   Provide as many native [IMEngines](https://web.archive.org/web/20130318035826/http://www.scim-im.org/projects/imengines) as possible.
*   Support as many input method protocols/interfaces as possible.
*   Support as many operating systems as possible.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
*   [2 Configuration](#Configuration)
    *   [2.1 A simple scenario](#A_simple_scenario)
    *   [2.2 Note for GTK](#Note_for_GTK)
        *   [2.2.1 Note for GNOME, Xfce, LXDE](#Note_for_GNOME,_Xfce,_LXDE)
        *   [2.2.2 Note for KDE3](#Note_for_KDE3)
    *   [2.3 Locale-related files](#Locale-related_files)
        *   [2.3.1 Further troubleshooting with locales](#Further_troubleshooting_with_locales)
    *   [2.4 Executing SCIM](#Executing_SCIM)
        *   [2.4.1 Note for GNOME](#Note_for_GNOME)
        *   [2.4.2 Note for KDE](#Note_for_KDE)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 LWJGL (Lightweight Java Game Library) losing keyboard focus](#LWJGL_(Lightweight_Java_Game_Library)_losing_keyboard_focus)
    *   [3.2 Chrome/Chromium doesn't take input](#Chrome/Chromium_doesn't_take_input)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [scim](https://www.archlinux.org/packages/?name=scim) package.

### Input method engines

Currently the SCIM project has a wide range of input methods (some may need other libraries), covering more than 30 languages, including (Simplified/Traditional) Chinese, Japanese, Korean and many European languages. These are some of the examples (more can be found [here](https://web.archive.org/web/20130318035826/http://www.scim-im.org/projects/imengines)):

*   [scim-chewing](https://www.archlinux.org/packages/?name=scim-chewing) - Chinese
*   [scim-pinyin](https://aur.archlinux.org/packages/scim-pinyin/) - Chinese Smart PinYin .
*   [scim-tables](https://aur.archlinux.org/packages/scim-tables/) - Chinese WuBi or other tables based
*   [scim-anthy](https://aur.archlinux.org/packages/scim-anthy/) - Japanese
*   [scim-hangul](https://aur.archlinux.org/packages/scim-hangul/) - Korean

[uim](/index.php/Uim "Uim") can be used as an engine for SCIM by using [scim-uim](https://aur.archlinux.org/packages/scim-uim/).

## Configuration

Configuring SCIM correctly requires the following three steps:

1.  Exporting some environment variables that specify the used input method.
2.  Modifying locale related files.
3.  Finally, starting SCIM.

### A simple scenario

If you just need SCIM to work urgently in any [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager"), put these lines into your [xprofile](/index.php/Xprofile "Xprofile") and then reboot:

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

### Note for GTK

If you use [GNOME](/index.php/GNOME "GNOME"), edit `/etc/gtk-2.0/gtk.immodules` by adding follow content at the end:

 `/etc/gtk-2.0/gtk.immodules` 
```
"/usr/lib/gtk-2.0/immodules/im-scim.so"
"scim" "SCIM Input Method" "scim" "/usr/share/locale" "ja:ko:zh"

```

If your `LC_CTYPE` or `LANG` is *en_US.UTF-8*, change `ja:ko:zh` to `en:ja:ko:zh`.

After making those changes, be sure to reboot. You can find out what input method modules are available on your system by executing `gtk-query-immodules-2.0`.

If SCIM does not work with GTK applications after these changes, check that the GTK_IM_MODULE_FILE environment variable is set to `/etc/gtk-2.0/gtk.immodules`.

You can use another file (in this example `~/.immodules`) that contains the necessary information about input methods modules by adding these lines in the file you selected in the [section above](#A_simple_scenario).

```
gtk-query-immodules-2.0 > ~/.immodules
export GTK_IM_MODULE_FILE=~/.immodules

```

#### Note for GNOME, Xfce, LXDE

If you are using GNOME, Xfce or LXDE and Qt applications do not pick up the `export QT_IM_MODULE="scim"` variable, you can use scim-bridge. To use *scim-bridge* instead, export the following:

```
export QT_IM_MODULE="scim-bridge"

```

#### Note for KDE3

For KDE3 you should `export QT_IM_MODULE="xim"` instead of *scim* and also install [qtimm](https://web.archive.org/web/20130715195838/http://www.scim-im.org/projects/scim_qtimm) for Qt3.

### Locale-related files

If your keyboard locale is not `en_US.UTF-8` (or `en_US.utf8`), you have to modify the first line of `~/.scim/global` (or `/etc/scim/global` to apply these settings to all users) according to the following example:

```
/SupportedUnicodeLocales = en_US.UTF-8,de_CH.UTF-8

```

and replace your `de_CH.UTF-8` with your locale.

**Note:** Your locale has to be active (i.e. you have to uncomment it in `/etc/locale-gen` and then execute `locale-gen` as root) *and* has to be supported by SCIM (most *.UTF-8 locales are).

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

## Troubleshooting

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

## See also

*   [GitHub repository](https://github.com/scim-im/scim)
*   [Arch Linux news page from 2005](https://www.archlinux.org/news/166/)