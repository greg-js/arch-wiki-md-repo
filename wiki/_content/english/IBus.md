[IBus](https://en.wikipedia.org/wiki/Intelligent_Input_Bus "wikipedia:Intelligent Input Bus") (*Intelligent Input Bus*) is an [input method](/index.php/Input_method "Input method") framework, a system for entering non-Latin characters.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
        *   [1.1.1 Chinese](#Chinese)
        *   [1.1.2 Japanese](#Japanese)
        *   [1.1.3 Others](#Others)
    *   [1.2 Initial setup](#Initial_setup)
    *   [1.3 GNOME](#GNOME)
*   [2 Configuration](#Configuration)
    *   [2.1 IBus](#IBus)
    *   [2.2 Ibus-rime](#Ibus-rime)
    *   [2.3 Entering Special Characters—The Compose Input Method](#Entering_Special_Characters.E2.80.94The_Compose_Input_Method)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Pinyin usage](#Pinyin_usage)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Plasma 5](#Plasma_5)
    *   [4.2 Kimpanel](#Kimpanel)
    *   [4.3 rxvt-unicode](#rxvt-unicode)
    *   [4.4 GTK+ applications](#GTK.2B_applications)
    *   [4.5 Chinese input](#Chinese_input)
    *   [4.6 LibreOffice](#LibreOffice)
    *   [4.7 Non US keyboards](#Non_US_keyboards)
*   [5 ibus-m17n](#ibus-m17n)
    *   [5.1 English international AltGr](#English_international_AltGr)
    *   [5.2 Trouble with Japanese](#Trouble_with_Japanese)
*   [6 See also](#See_also)

## Installation

Install the [ibus](https://www.archlinux.org/packages/?name=ibus) package.

Additionally, to smooth the typing experience of IBus for Qt applications, please install the [ibus-qt](https://www.archlinux.org/packages/?name=ibus-qt) library with provides IM modules to replace XIM protocol.

### Input method engines

You will need at least one input method, corresponding to the language you wish to type. Available input methods include:

#### Chinese

*   ~~[ibus-pinyin](https://www.archlinux.org/packages/?name=ibus-pinyin) - Intelligent Chinese Phonetic IME for Hanyu pinyin and Zhuyin (Bopomofo) users. Designed by IBus main author and has many advance features such as English spell checking.~~ Package currently not maintained and partly broken with latest ibus base. Use [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) instead.
*   [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) - Powerful and smart input method for a wide range of Chinese input methods, based on the [Rime IME](/index.php/Rime_IME "Rime IME") project.
*   [ibus-chewing](https://www.archlinux.org/packages/?name=ibus-chewing) - Intelligent Chinese Phonetic IME for Zhuyin (Bopomofo) users, based on [libchewing](https://www.archlinux.org/packages/?name=libchewing).
*   [ibus-cangjie](https://aur.archlinux.org/packages/ibus-cangjie/) - Chinese IME for Cangjie3, Cangjie3, and Quick based on [libcangjie](https://aur.archlinux.org/packages/libcangjie/) and [python-pycangjie](https://aur.archlinux.org/packages/python-pycangjie/).

#### Japanese

*   [ibus-anthy](https://www.archlinux.org/packages/?name=ibus-anthy) - Japanese IME, based on [anthy](https://www.archlinux.org/packages/?name=anthy).
*   [ibus-mozc](https://aur.archlinux.org/packages/ibus-mozc/) - Japanese IME, based on [Mozc](/index.php/Mozc "Mozc").
*   [ibus-kkc](https://www.archlinux.org/packages/?name=ibus-kkc) - Japanese IME, based on [libkkc](https://www.archlinux.org/packages/?name=libkkc).

#### Others

*   [ibus-hangul](https://www.archlinux.org/packages/?name=ibus-hangul) - Korean IME, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul).
*   [ibus-unikey](https://www.archlinux.org/packages/?name=ibus-unikey) - IME for typing Vietnamese characters.
*   [ibus-table](https://www.archlinux.org/packages/?name=ibus-table) - IME that accommodates table-based IMs.
*   [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) - M17n IME which allows input of many languages using the input methods from [m17n-db](https://www.archlinux.org/packages/?name=m17n-db).
*   [ibus-kmfl](https://aur.archlinux.org/packages/ibus-kmfl/) - Linux port of [Keyman](https://keyman.com/) input method for Windows which supports over 1,000 languages, such as complex scripts, languages of minorities, and IPA symbols. Only part of them is available in KMFL as it can work with uncompiled layout description only (*.kmn files).

To see all available input methods:

```
$ pacman -Ss '^ibus-*'

```

Others packages are also available in the [AUR](/index.php/AUR "AUR").

### Initial setup

Now, run `$ ibus-setup` (as the user who will use IBus). It will start the daemon and give you this message:

```
IBus has been started! If you cannot use IBus, please add below lines in `~/.bashrc`, and relogin your desktop.
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus

```

**Note:**

*   Although IBus uses a daemon, it is not the sort of daemon managed by *systemd*: it runs as an ordinary user and will be started for you when you login.
*   If, however, IBus is **not** autostarted upon login, then move the “export …” lines above to either
    *   `~/.xprofile` instead and append this line to the same file: `ibus-daemon -drx`, **or**
    *   `~/.xinitrc` and append this line to the same file: `ibus-daemon -drx`.

	Which works best, depends on your [Window manager](/index.php/Window_manager "Window manager"), see also [xprofile](/index.php/Xprofile "Xprofile") and [xinitrc](/index.php/Xinitrc "Xinitrc").

*   You can also try adding `ibus-daemon -drx` after the `export ...` lines in `~/.bashrc`.

You will then see a configuration screen; you can access this screen whenever IBus is running by right-clicking the icon in the system tray and choosing *Preferences*. See [Configuration](#Configuration).

If IBus does not work in Qt/KDE applications, ensure that the *ibus-qt* library is installed and define IBus as the default IME in the Qt configuration editor:

```
$ qtconfig-qt4

```

In *Interface > Default Input Method*, select *ibus* instead of *xim*.

### GNOME

[GNOME](/index.php/GNOME "GNOME") integrates with IBus[[1]](https://help.gnome.org/misc/release-notes/3.6/i18n-ibus.html.en), so you should only need to install the package specific to your language. To enable input in your language, add it to the *Input Sources* section of the *Region & Language* settings. After you add your input sources (at least 2), GNOME will show the input switcher icon in the tray. If you do not find your appropriate input source when trying to add your input sources, most likely you have not done locale-gen for that locale. The default keyboard shortcut to switch to the next input method in GNOME is `Super+space`; disregard the *next input method* shortcut set in *ibus-setup*.

## Configuration

### IBus

**Note:** You need to have [east Asian fonts](/index.php/Fonts_FAQ#Chinese.2C_Japanese.2C_Korean.2C_Vietnamese "Fonts FAQ") installed if you want to enter Chinese, Japanese, Korean or Vietnamese characters.

The default *General* settings should be fine, but go to *Input Methods* and select your input method(s) in the drop down box, then press *Add*. You can use multiple input methods if you wish. Once IBus is set up, you can press `Super+space` to use it (multiple times to cycle through available input methods). IBus will remember which input method you are using in each window, so you will have to reactivate it for each new window. You can override this behavior by right clicking the system tray icon, selecting *Preferences*, and going to the *Advanced* tab.

**Note:** By default, IBus overrides your [Xmodmap](/index.php/Xmodmap "Xmodmap") setting. You can disable this feature by enabling "Use system keyboard layout" option in Preference -> Advanced.

### Ibus-rime

If you have decided to use the great *ibus-rime* IME, check out [Rime IME](/index.php/Rime_IME "Rime IME") for some help to configure it.

### Entering Special Characters—The Compose Input Method

To type special characters, XKB supports compose key sequences. To fulfil this function, IBus supports an input method that is permanently in Compose mode. Instead of hitting a compose key, then typing out the compose sequence, the user switches to the Compose input method (by default using super-space (a.k.a. win-space)), types the compose sequence, then switches back to the previous method. In Archlinux, the Compose input method is not installed by default. To use it, install [ibus-table-others](https://aur.archlinux.org/packages/ibus-table-others/) from the AUR, restart IBus, then look for it in the list of input methods under 'other' at the bottom.

## Tips and tricks

### Pinyin usage

When using *ibus-pinyin*,

*   First type the pinyin (sans tones) for the characters you wish to enter.
*   Press `Up` and `Down` repeatedly to select a character (going on to the next page if necessary).
*   Press `Space` to use a character.
*   You can also use `PageUp` or `PageDown` to scroll pages, and use the number keys 1-5 to select the character you need.
*   You can enter multiple characters that form a word or phrase at a time (such as "zhongwen" to enter "中文"). ibus-pinyin will remember which characters you type most frequently and over time make suggestions that are more tuned to your typing profile.

## Troubleshooting

### Plasma 5

Some applications may not accept non-"direct input" text (e.g. Japanese and Chinese) from Mozc using IBus. In order to resolve this problem add

```
export QT_IM_MODULE=ibus

```

to `~/.xprofile` and restart your X user session.

### Kimpanel

IBus main interface is currently only available in GTK+, but Kimpanel provides a native Qt/KDE input interface. Kimpanel is bundled with Plasma 5, but IBus needs to be launched as following to be able to communicate with the panel

```
$ ibus-daemon --panel=/usr/lib/kimpanel-ibus-panel

```

To get a menu entry for launching ibus this way, save the following file to `~/.local/share/applications/ibus-kimpanel.desktop`:

```
[Desktop Entry]
Encoding=UTF-8
Name=IBus (KIMPanel)
GenericName=Input Method Framework
Comment=Start IBus Input Method Framework
Exec=ibus-daemon --panel=/usr/lib/kimpanel-ibus-panel
Icon=ibus
Terminal=false
Type=Application
Categories=System;Utility;
X-GNOME-Autostart-Phase=Applications
X-GNOME-AutoRestart=false
X-GNOME-Autostart-Notify=true
X-KDE-autostart-after=panel

```

Then you can either let KDE autostart ibus, or set it as the input method application in Kimpanel, and manually click on the kimpanel icon to start it. In either case, choose Utility/Ibus (Kimpanel) in the Choose Application dialog.

Finally, add the input panel widget to show the panel.

### rxvt-unicode

If anyone has any issues with IBus and *rxvt-unicode*, the following steps should solve it.

Add the following to your `~/.Xresources` (possibly not required, first try without):

```
URxvt.inputMethod: ibus
URxvt.preeditType: OverTheSpot

```

And start IBus with:

```
$ ibus-daemon --xim

```

If you start *ibus-daemon* automatically (e.g. in `~/.xinitrc` or `~/.xsession`) but used to use `ibus-daemon &` without the `--xim` option, make sure to kill the existing process before testing the new command.

### GTK+ applications

Some users have had problems using Input Methods with GTK applications, because it seems that the gtk.immodules file cannot be found. Adding:

```
export GTK_IM_MODULE_FILE=/etc/gtk-2.0/gtk.immodules

```

for GTK+ 2, or:

```
export GTK_IM_MODULE_FILE=/usr/lib/gtk-3.0/3.0.0/immodules.cache

```

for GTK+ 3, in addition to the three lines above in your `$HOME/.bashrc` seems to fix the problem.

**Note:** If you set it to GTK+ 2, then you cannot use GTK+ 3 applications like *gedit*, if you set it to GTK+ 3, then you cannot use GTK+ 2 applications like Xfce.

### Chinese input

If you encounter problems when using Chinese input, check your locale setting. For example in Hong Kong, export LANG=zh_HK.utf8.

**Note:** There are large revisions after IBus 1.4, you might not be able to input Chinese words with *ibus-pinyin* or *ibus-sunpinyin*, which are written in C. So the solution is to install [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin).

To start ibus with GNOME, add this in `~/.profile` and restart the GNOME.

```
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
ibus-daemon -d -x

```

Chinese users can refer to this [page](http://forum.ubuntu.org.cn/viewtopic.php?f=155&t=346639) for detailed solution concerning this bug.

### LibreOffice

If IBus does load but does not see LibreOffice as an input window, add this line to `~/.bashrc`:

```
export XMODIFIERS=@im=ibus

```

And then, you need to start ibus with `--xim -d`, for example, add this line to `~/.xinitrc`:

```
ibus-daemon --xim -d

```

But the horrible thing is that you need to start LibreOffice in terminal.

If you are using KDE and the above does not work, install [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) and add this line to `~/.xprofile` if you do not mind running LibreOffice in GTK+ 2 mode:

```
export OOO_FORCE_DESKTOP="gnome"

```

That will make IBus work with LibreOffice, and you can start LibreOffice from anywhere, not just the terminal.

### Non US keyboards

If [Ibus does not let you write in a given language](https://code.google.com/p/ibus/issues/detail?id=155), let's say Chinese, with a different keyboard layout other than US, then you need to tell it which one to use.

Each input method specifies its desired input layout in an XML configuration file in `/usr/share/ibus/component/<method_name>.xml`. Setting the `<layout>` tag to the desired value will make the ibus use that layout. With the special value `default`, ibus will use whatever is the default layout configured on the system.

You need to change `/usr/share/ibus/component/<method_name>.xml` and change the `<layout>` tag to the expected keyboard layout.

## ibus-m17n

In the specific case of `ibus-m17n`, a helper, `/usr/lib/ibus/ibus-engine-m17n`, generates the necessary XML at runtime. With version [1.3.4-4 of the package](https://www.archlinux.org/packages/community/x86_64/ibus-m17n/), this unfortunately uses `us` as the `layout` without a possibility of override. Fortunately, this was changed to `default` [a few commits later in Git](https://github.com/ibus/ibus-m17n/commit/2b915cb54122e2010db1182f4f1007b9f7cda5aa), but no new release was made since then. To remediate the issue, a [Git-master version of the package is available from AUR](https://aur.archlinux.org/packages/ibus-m17n-git/), which works nicely.

### English international AltGr

If you want to use AltGr as compose key for the english keyboard, choose `English international AltGr` in the ibus-setup instead of 'English'.

### Trouble with Japanese

If you have trouble with Japanese input try to generate the locales with uncommenting `ja_JP.UTF-8 UTF-8` in the `/etc/locale.gen` file and then run `locale-gen`.

## See also

*   [GitHub repository](https://github.com/ibus/ibus)