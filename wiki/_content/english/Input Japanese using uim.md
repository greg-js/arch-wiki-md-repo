Related articles

*   [Localization](/index.php/Localization "Localization")
*   [Localization/Japanese](/index.php/Localization/Japanese "Localization/Japanese")

This page explains how to get the Japanese input to work using [uim](http://code.google.com/p/uim/).

If you use SCIM, see [Smart Common Input Method platform](/index.php/Smart_Common_Input_Method_platform "Smart Common Input Method platform").

If you use IBus, see [IBus](/index.php/IBus "IBus").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Japanese fonts](#Japanese_fonts)
        *   [1.1.1 Sans-serif](#Sans-serif)
        *   [1.1.2 Serif and Sans-serif](#Serif_and_Sans-serif)
    *   [1.2 uim](#uim)
        *   [1.2.1 Using pacman](#Using_pacman)
        *   [1.2.2 Compiling uim from source using PKGBUILD](#Compiling_uim_from_source_using_PKGBUILD)
    *   [1.3 Input method](#Input_method)
        *   [1.3.1 Anthy](#Anthy)
            *   [1.3.1.1 Extra dictionary](#Extra_dictionary)
        *   [1.3.2 Modified Anthy (anthy-ut)](#Modified_Anthy_(anthy-ut))
            *   [1.3.2.1 Compiling modified Anthy using PKGBUILD](#Compiling_modified_Anthy_using_PKGBUILD)
        *   [1.3.3 Anthy Kaomoji](#Anthy_Kaomoji)
        *   [1.3.4 Mozc](#Mozc)
            *   [1.3.4.1 Mozc (Vanilla)](#Mozc_(Vanilla))
            *   [1.3.4.2 mozc-ut](#mozc-ut)
            *   [1.3.4.3 Registering Mozc](#Registering_Mozc)
        *   [1.3.5 Google CGI API for Japanese input](#Google_CGI_API_for_Japanese_input)
*   [2 Settings](#Settings)
    *   [2.1 Environment variables](#Environment_variables)
    *   [2.2 Toolbar utilities](#Toolbar_utilities)
        *   [2.2.1 uim-toolbar-gtk/qt](#uim-toolbar-gtk/qt)
        *   [2.2.2 uim-toolbar-gtk-systray](#uim-toolbar-gtk-systray)
        *   [2.2.3 Panel applet](#Panel_applet)
    *   [2.3 Using systemd](#Using_systemd)
    *   [2.4 uim preferences](#uim_preferences)
    *   [2.5 Input Japanese on Emacs](#Input_Japanese_on_Emacs)
        *   [2.5.1 LEIM or minor-mode](#LEIM_or_minor-mode)
            *   [2.5.1.1 Settings for the minor-mode](#Settings_for_the_minor-mode)
            *   [2.5.1.2 Settings for the LEIM](#Settings_for_the_LEIM)
        *   [2.5.2 Preferred character encoding](#Preferred_character_encoding)
        *   [2.5.3 Enable inline candidates displaying mode by default](#Enable_inline_candidates_displaying_mode_by_default)
        *   [2.5.4 Set Hiragana input mode by default](#Set_Hiragana_input_mode_by_default)
        *   [2.5.5 Ignoring C-SPC on uim.el](#Ignoring_C-SPC_on_uim.el)
        *   [2.5.6 Disabling XIM on Emacs](#Disabling_XIM_on_Emacs)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Set the GTK_IM_MODULE variable, but uim still does not work with GTK 2 applications](#Set_the_GTK_IM_MODULE_variable,_but_uim_still_does_not_work_with_GTK_2_applications)
    *   [3.2 Cannot input Japanese on Opera](#Cannot_input_Japanese_on_Opera)
    *   [3.3 Cannot type a consonant in Zenkaku mode](#Cannot_type_a_consonant_in_Zenkaku_mode)
    *   [3.4 uim-toolbar-gtk-systray: tray icon is crushed](#uim-toolbar-gtk-systray:_tray_icon_is_crushed)
    *   [3.5 I use darker theme, I cannot read the uim mode icons](#I_use_darker_theme,_I_cannot_read_the_uim_mode_icons)
*   [4 See also](#See_also)

## Installation

You need the following packages to input Japanese.

*   Japanese fonts
*   Japanese input method (Kana to Kanji conversion engine)
*   Input method framework: uim

### Japanese fonts

*see also [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") for configuration or more detail.*

Recommended Japanese fonts are as follows.

#### Sans-serif

*   [adobe-source-han-sans](https://github.com/adobe-fonts/source-han-sans) || [adobe-source-han-sans-jp-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-jp-fonts) or [adobe-source-han-sans-otc-fonts](https://www.archlinux.org/packages/?name=adobe-source-han-sans-otc-fonts)

	Open-source OTF fonts developed by Adobe.

#### Serif and Sans-serif

*   [IPA fonts](http://ossipedia.ipa.go.jp/ipafont/) || [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont)

	An open source OTF font set including sans-serif (Gothic) and serif (Mincho) glyphs provided by Information-technology Promotion Agency, Japan (IPA).

If you want to show [2channel Shift JIS art](https://en.wikipedia.org/wiki/2channel_Shift_JIS_art "wikipedia:2channel Shift JIS art") properly, use one of the following fonts:

*   ipamona font (AUR: [ttf-ipa-mona](https://aur.archlinux.org/packages/ttf-ipa-mona/))
*   Monapo font (AUR: [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/))

### uim

#### Using pacman

[Install](/index.php/Install "Install") [uim](https://www.archlinux.org/packages/?name=uim) from the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** uim versions before 1.8.0 do not support Qt5\. To use uim in Qt5 applications, install the development version ([uim-git](https://aur.archlinux.org/packages/uim-git/)), or the Debian fork ([uim-debian](https://aur.archlinux.org/packages/uim-debian/)).

#### Compiling uim from source using PKGBUILD

If you want to build uim with your configuration, you can compile from source, using [ABS](/index.php/ABS "ABS") for instance. See [official wiki](http://code.google.com/p/uim/wiki/InstallUim) for all configure options.

In Arch official repositories, uim is built with the following custom configuration (as of 1.8.6):

*   `--with-anthy-utf8` - Enable Anthy(UTF-8) support
*   `--with-qt4-immodule` - Build Qt4 immodule
*   `--with-qt4` - Build uim-tools for Qt4

If you want KDE4 plasma widget, install [automoc4](https://aur.archlinux.org/packages/automoc4/) for making dependency, and add `--enable-kde4-applet` option to PKGBUILD file.

### Input method

#### Anthy

Anthy is one of the most popular Japanese input methods in the open source world. However, it has not been maintained for a long time. [Debian succeeds it](http://wiki.debian.org/Teams/DebianAnthy) from May 2010.

Install [anthy](https://www.archlinux.org/packages/?name=anthy) from the official repositories.

##### Extra dictionary

Anthy's default dictionary does not include several characters which are not specified on EUC-JP (JIS X 0208) such as "①", "♥", etc. [alt-cannadic](http://en.sourceforge.jp/projects/alt-cannadic/) provides extra dictionaries including those characters.

Get [alt-cannadic dictionary](http://en.sourceforge.jp/projects/alt-cannadic/releases/?package_id=6129) and put them under your `~/.anthy/imported_words_default.d`.

```
$ tar jxvf alt-cannadic-091230.tar.bz2
$ mkdir ~/.anthy/imported_words_default.d (if not exist)
$ cp alt-cannadic-091230/extra/*.t ~/.anthy/imported_words_default.d/

```

Please see [official wiki](http://sourceforge.jp/projects/alt-cannadic/wiki/%E4%BD%BF%E3%81%84%E6%96%B9_Anthy-UTF-8) for more detail (Japanese).

**Warning:** If you will be using this extra dictionary, choose **Anthy (UTF-8)** for default input method on uim.

#### Modified Anthy (anthy-ut)

[Modified Anthy](http://www.geocities.jp/ep3797/anthy_dict_01.html) is a set of patches and huge extended dictionaries which aims to improve the Kana to Kanji conversion quality of original Anthy.

Modified Anthy consists two different upstreams:

*   Patched source of Anthy by [G-HAL](http://www.fenix.ne.jp/~G-HAL/soft/nosettle/#anthy)
*   Huge extended dictionalies by [UTSUMI](http://www.geocities.jp/ep3797/anthy_dict_01.html)

**Warning:**

*   Modified Anthy applies to only Anthy (UTF-8). So you have to choose **Anthy (UTF-8)** for default input method on uim.
*   Modified Anthy does not have compatibility of the dictionaries and learning data with original Anthy.

##### Compiling modified Anthy using PKGBUILD

Modified Anthy is available on AUR named [anthy-ut](https://aur.archlinux.org/packages/anthy-ut/).

If you already use original Anthy, you have to convert the existing learning data format.

```
$ rm ~/.anthy/last-record1_*.bin
$ anthy-agent --update-base-record
$ rm ~/.anthy/last-record1_*.bin
$ anthy-agent --update-base-record

```

(Though this step repeats the same commands twice, it is not mistypes.)

#### Anthy Kaomoji

[Anthy Kaomoji](http://sourceforge.jp/projects/anthy/) is a modified version of Anthy that converts Hiragana text to Kana Kanji mixed text and has emoticon (顔文字) and 2ch dictionaries. It can be found in the AUR ([anthy-kaomoji](https://aur.archlinux.org/packages/anthy-kaomoji/)).

#### Mozc

*See [Mozc](/index.php/Mozc "Mozc").*

[Mozc](http://code.google.com/p/mozc/) is a Japanese Input Method Editor (IME) designed for multi-platform such as Chromium OS, Windows, Mac and Linux which originates from [Google Japanese Input](http://www.google.com/intl/ja/ime/).

Though [Mozc](https://aur.archlinux.org/packages/Mozc/) adapts to only ibus input method framework, [macuim](http://code.google.com/p/macuim/) provides uim-mozc plugin.

##### Mozc (Vanilla)

[uim-mozc](https://aur.archlinux.org/packages/uim-mozc/) is available on AUR.

**Note:** This does not support the kill_line feature of uim-mozc.

You can install this from the unofficial [pnsft-pur](/index.php/Unofficial_user_repositories#pnsft-pur "Unofficial user repositories") user repository.

You can choose to install all packages in the `mozc-im` group by specifying the group name as follows:

```
# pacman -S mozc-im

```

Or, specify the individual package names directly. For example:

```
# pacman -S uim-mozc

```

##### mozc-ut

[mozc-ut2](https://aur.archlinux.org/packages/mozc-ut2/) can be built uim-mozc.

**Note:** mozc-ut can work with [uim-mozc](https://aur.archlinux.org/packages/uim-mozc/).

To build uim-mozc, edit PKGBUILD like follow, i,e. uncomment `_uim_mozc=` line:

```
## If you will not be using ibus, comment out below.
_ibus_mozc="yes"
## If you will be using uim, uncomment below.
_uim_mozc="yes"
## If applying patch for uim-mozc fails, try to uncomment below.
#_kill_kill_line="yes"
## This will disable the 'kill-line' function of uim-mozc.

```

**Tip:** If you will never be using ibus-mozc, comment out the `_ibus_mozc=` line.

##### Registering Mozc

**Warning:** You **must** run the following command whenever you upgrade or (re-)install uim.
# uim-module-manager --register mozc

#### Google CGI API for Japanese input

[Google CGI API for Japanese Input](http://www.google.co.jp/ime/cgiapi.html) (Google-CGIAPI-Jp) is CGI service to provide Japanese conversion on the Internet by Google. It can be used on [web browser](http://www.google.com/transliterate). Its conversion engine seems to be equivalent to Google Japanese Input, so conversion quality is probably better than Mozc.

**Note:** This service sends/receives preedits and candidates as plain text (as of 2012-09).

You can use it via uim. Choose "Google-CGIAPI-Jp" on uim-im-switcher-gtk/gtk3/qt4 or uim-pref-gtk/gtk3/qt4.

## Settings

### Environment variables

Add the following to ~/.[xprofile](/index.php/Xprofile "Xprofile"), ~/.[xinitrc](/index.php/Xinitrc "Xinitrc") or ~/.xsession:

```
export GTK_IM_MODULE='uim'
export QT_IM_MODULE='uim'
uim-xim &
export XMODIFIERS='@im=uim'

```

**Note:** The variables should be exported before starting your desktop environment, i.e. before "exec startxfce4" or similar. [See below](#Using_systemd) if you're using systemd to manage your X session.

### Toolbar utilities

If you want to use UimToolbar utilities which shows and controls uim mode, add **one** of the followings, too.

#### uim-toolbar-gtk/qt

Using toolbar appears as a window.

For GTK 2:

```
uim-toolbar-gtk &

```

For GTK 3:

```
uim-toolbar-gtk3 &

```

For Qt4:

```
uim-toolbar-qt4 &

```

#### uim-toolbar-gtk-systray

Using toolbar for system tray.

For GTK 2:

```
uim-toolbar-gtk-systray &

```

For GTK 3:

```
uim-toolbar-gtk3-systray &

```

#### Panel applet

Or, if you use GNOME, KDE or Xfce, you can use uim-toolbar panel applet (Xfce requires xfce4-xfapplet-plugin to use uim-applet-gnome).

### Using systemd

If you are [using systemd to manage your X session](/index.php/Systemd/User#Xorg_and_systemd "Systemd/User"), you'll need to set the environment variables in your systemd session rather than an init script.

 `~/.config/systemd/user/uim-env.service` 
```
[Unit]
Description=uim environment initialization
Before=xorg.target

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl --user set-environment XMODIFIERS=@im=uim
ExecStart=/usr/bin/systemctl --user set-environment GTK_IM_MODULE=uim
ExecStart=/usr/bin/systemctl --user set-environment QT_IM_MODULE=uim

```
 `~/.config/systemd/user/uim.service` 
```
[Unit]
Description=uim daemon
Wants=uim-env.service
After=xorg.target

[Service]
ExecStart=/usr/bin/uim-xim
Restart=on-abort

[Install]
WantedBy=xorg.target

```
 `~/.config/systemd/user/uim-toolbar.service` 
```
[Unit]
Description=uim toolbar
PartOf=uim.service

[Service]
ExecStart=/usr/bin/uim-toolbar-of-your-choice
Restart=on-abort

[Install]
WantedBy=uim.service

```

Lastly, you'll need to enable the services:

```
 $ systemctl --user enable uim.service uim-toolbar.service

```

### uim preferences

Configure uim preferences by running :

```
$ uim-pref-gtk (Or, uim-pref-gtk3/uim-pref-qt4)

```

which brings forth a GUI.

Choose your preferring input method as 'Default input method'.

**Note:** Mozc will be not listed in 'Default input method' at first time so you will need to add it into 'Enabled input methods' to use.

You can run `uim-xim` or restart X to test your settings.

Provided everything went well you should be able to input Japanese in X.

### Input Japanese on Emacs

uim provides uim.el the bridge software between Emacs and uim. Here is a sample to use uim on Emacs with utf-8 encoding.

Please see [Official wiki](http://code.google.com/p/uim/wiki/UimEl) for more detail.

#### LEIM or minor-mode

You can call uim.el from Emacs in two ways; directly or with the LEIM (Library of Emacs Input Method) framework. Though settings of them are different, basic functions are same. If you want to switch between uim.el and other Emacs IMs frequently, you should use LEIM framework.

##### Settings for the minor-mode

If you will be using on minor-mode, write the following settings into your `.emacs.d/init.el` or some other file for Emacs customizing.

```
;; read uim.el
(require 'uim)
;; uncomment next and comment out previous to load uim.el on-demand
;; (autoload 'uim-mode "uim" nil t)

;; key-binding for activate uim (ex. C-\)
(global-set-key "\C-\\" 'uim-mode)

```

##### Settings for the LEIM

If you will be using via LEIM, write the following settings into your `.emacs.d/init.el` or some other file for Emacs customizing and choose default input method.

```
;; read uim.el with LEIM initializing
(require 'uim-leim)

;; set default IM. Uncomment the one of the followings.
;(setq default-input-method "japanese-anthy-utf8-uim")        ; Anthy (UTF-8)
;(setq default-input-method "japanese-google-cgiapi-jp-uim")  ; Google-CGIAPI-Jp
;(setq default-input-method "japanese-mozc-uim")              ; Mozc

```

#### Preferred character encoding

uim.el uses euc-jp character encoding by default. To set UTF-8 as preferred encodings, add the followings into your `.emacs.d/init.el` or some other file for Emacs customizing.

```
;; Set UTF-8 as preferred character encoding (default is euc-jp).
(setq uim-lang-code-alist
      (cons '("Japanese" "Japanese" utf-8 "UTF-8")
           (delete (assoc "Japanese" uim-lang-code-alist) 
                   uim-lang-code-alist)))

```

#### Enable inline candidates displaying mode by default

The inline candidates displaying mode displays conversion candidates just below (or above) preedit text vertically instead of echo area. If you want to enable inline candidates displaying mode by default, write as follows.

```
;; set inline candidates displaying mode as default
(setq uim-candidate-display-inline t)

```

#### Set Hiragana input mode by default

To set Hiragana input mode at activting uim, add the settings like follows:

```
;; Set Hiragana input mode at activating uim.
(setq uim-default-im-prop '("action_anthy_utf8_hiragana"
                            "action_google-cgiapi-jp_hiragana"
                            "action_mozc_hiragana"))

```

#### Ignoring C-SPC on uim.el

When you are assigning activation/deactivation of input method to C-SPC, C-SPC is stolen to switch input mode by uim.el while it is activated. To prevent the stealing and use for set-mark-command, add the followings into your `.emacs.d/init.el` or some other file for Emacs customizing.

```
(add-hook 'uim-load-hook
          '(lambda ()
             (define-key uim-mode-map [67108896] nil)
             (define-key uim-mode-map [0] nil)))

```

#### Disabling XIM on Emacs

When you are using input method on your desktop and assigning activation/deactivation of input method to C-SPC, you will be not able to use C-SPC/C-@ as set-mark-command on Emacs. To avoid this problem, add the following into your `~/.Xresources` or `~/.Xdefaults`. xim will be disabled on Emacs.

```
Emacs*UseXIM: false

```

## Troubleshooting

### Set the GTK_IM_MODULE variable, but uim still does not work with GTK 2 applications

In case you already set the GTK_IM_MODULE environmental variable, but uim still does not work with GTK 2 applications, you need to specify the location of gtk.immodules, which is created by and can be generated with `gtk-query-immodules-2.0`.

The default location is `/etc/gtk-2.0/gtk.immodules` for GTK 2.

You can do this with either the GTK_IM_MODULE_FILE variable (*not recommended*, it causes GTK 3 applications to see incompatible modules) or the im_module_file setting (*recommended*).

Add the following to `/etc/gtk-2.0/gtkrc` or `~/.gtkrc-2.0`:

```
 im_module_file "/etc/gtk-2.0/gtk.immodules"

```

### Cannot input Japanese on Opera

If you use Opera and cannot input Japanese with uim, try to edit environment variable as follows: Make sure to add the following to the beginning of /usr/bin/opera.

```
export XMODIFIERS='@im=uim'
export QT_IM_MODULE='xim'

```

### Cannot type a consonant in Zenkaku mode

If you cannot type a consonant in Zenkaku mode, add the following to your config file.

```
   e.g.  vi ~/.uim.d/customs/custom-google-cgiapi-jp.scm

   (define ja-rk-rule-hoge
   (map
   (lambda (c)
   (list (cons (list c) ()) (list c c c)))
   '("b" "c" "d" "f" "g" "h" "j" "k" "l" "m"
   "p" "q" "r" "s" "t" "v" "w" "x" "y" "z"
   "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M"
   "N" "O" "P" "Q" "R" "S" "T" "U" "V" "W" "X" "Y" "Z")))
   (if (symbol-bound? 'ja-rk-rule-hoge)
   (set! ja-rk-rule (append ja-rk-rule-hoge ja-rk-rule)))

```

### uim-toolbar-gtk-systray: tray icon is crushed

Though some of DE, WM or panel application may provide only one icon space per application on system-tray/notification-area, uim-toolbar-gtk-systray displays some icons on it by default so those icons are crushed. Choose just one of them to solve it. The steps to display only 'Input mode' icon for example as follows:

1.  Run `uim-pref-gtk`.
2.  Click 'Toolbar' on 'Group' list.
3.  Take the all checkmarks off.
4.  Click 'Anthy', 'Anthy (UTF-8)' or 'Mozc' which you are using on 'Group' list.
5.  Click Edit button in 'Toolbar' box > 'Enable toolbar buttons' line.
6.  Enable only 'Input mode' and click 'Close' button.
7.  Click 'OK' button to close uim-pref-gtk.

The tray icon will be displayed "あ" (Hiragana mode) or "ー" (Direct mode).

### I use darker theme, I cannot read the uim mode icons

You can choose icons for darker background (uim 1.6.0 or later).

1.  Run uim-perf-gtk
2.  Click 'Toolbar' on 'Group' list.
3.  Check 'Use icon for dark background'.

## See also

	uim

	[uim official document](https://github.com/uim/uim/wiki/OfficialUserDocument)

	[uim on wikibooks](http://en.wikibooks.org/wiki/Uim)

	Fonts

	[Japanese fonts showcase](http://www.geocities.jp/ep3797/japanese_fonts.html)

	[modified Japanese fonts](http://www.geocities.jp/ep3797/modified_fonts_01.html)