[Fcitx](https://fcitx-im.org/wiki/Fcitx) (Flexible Input Method Framework) is a lightweight [input method framework](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") aimed at providing environment independent language support for Linux. It supports a lot of different languages and also provides many useful non-CJK features.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
        *   [1.1.1 Chinese](#Chinese)
        *   [1.1.2 Japanese](#Japanese)
        *   [1.1.3 Other languages](#Other_languages)
    *   [1.2 Input method module](#Input_method_module)
    *   [1.3 Others](#Others)
*   [2 Usage](#Usage)
    *   [2.1 Desktop Environment](#Desktop_Environment)
    *   [2.2 Non desktop environment](#Non_desktop_environment)
    *   [2.3 Xim](#Xim)
*   [3 Configuration](#Configuration)
    *   [3.1 Configuration tools](#Configuration_tools)
    *   [3.2 Change default UI](#Change_default_UI)
        *   [3.2.1 Gnome-Shell](#Gnome-Shell)
        *   [3.2.2 KDE](#KDE)
        *   [3.2.3 kimpanel UI](#kimpanel_UI)
        *   [3.2.4 Extend pinyin dictionary](#Extend_pinyin_dictionary)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Clipboard Access](#Clipboard_Access)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Diagnose the problem](#Diagnose_the_problem)
    *   [5.2 Emacs](#Emacs)
    *   [5.3 Input method module](#Input_method_module_2)
    *   [5.4 Ctrl+Space fail to work in GTK programs](#Ctrl.2BSpace_fail_to_work_in_GTK_programs)
    *   [5.5 Buildin Chinese Pinyin Default NOT ACTIVE](#Buildin_Chinese_Pinyin_Default_NOT_ACTIVE)
    *   [5.6 fcitx and KDE](#fcitx_and_KDE)
    *   [5.7 Input method switched to English unintentionally](#Input_method_switched_to_English_unintentionally)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") package [fcitx](https://www.archlinux.org/packages/?name=fcitx) from [official repositories](/index.php/Official_repositories "Official repositories").

### Input method engines

Fcitx provides built-in input methods for Chinese [Pinyin](https://en.wikipedia.org/wiki/Pinyin "wikipedia:Pinyin") and table-based input (for example [Wubi](https://en.wikipedia.org/wiki/Wubi "wikipedia:Wubi")).

Depending on the language you wish to type, other input method engines are available:

#### Chinese

*   [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin), based on [sunpinyin](https://www.archlinux.org/packages/?name=sunpinyin). It strikes a good balance between speed and accuracy.
*   [fcitx-libpinyin](https://www.archlinux.org/packages/?name=fcitx-libpinyin), based on [libpinyin](https://www.archlinux.org/packages/?name=libpinyin). It has a better algorithm than [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin), but still has bugs and lacks a good dictionary.
*   [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime), based on schemas from the [Rime IME](/index.php/Rime_IME "Rime IME") project.
*   [fcitx-googlepinyin](https://www.archlinux.org/packages/?name=fcitx-googlepinyin), the Google pinyin IME for Android.
*   [fcitx-sogoupinyin](https://aur.archlinux.org/packages/fcitx-sogoupinyin/), Sogou input method for linux—Supports, Jianpin, fuzzy sound, cloud input, English input, mixed skin.[Official website](http://pinyin.sogou.com/linux/)
*   [fcitx-cloudpinyin](https://www.archlinux.org/packages/?name=fcitx-cloudpinyin) uses internet sources to provide input candidates. The selected cloud result will be added to local dictionary.
*   [fcitx-chewing](https://www.archlinux.org/packages/?name=fcitx-chewing) is a popular Zhuyin input engine for Traditional Chinese based on [libchewing](https://www.archlinux.org/packages/?name=libchewing).
*   [fcitx-table-extra](https://www.archlinux.org/packages/?name=fcitx-table-extra) adds [Cangjie](https://en.wikipedia.org/wiki/Cangjie_input_method "wikipedia:Cangjie input method"), [Zhengma](https://en.wikipedia.org/wiki/Zhengma_method "wikipedia:Zhengma method"), [Boshiamy](https://en.wikipedia.org/wiki/Boshiamy_method "wikipedia:Boshiamy method") support.

#### Japanese

*   [fcitx-anthy](https://www.archlinux.org/packages/?name=fcitx-anthy), a popular Japanese input engine. However, it is not actively developed anymore.
*   [fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc), based on [Mozc](/index.php/Mozc "Mozc"), the Open Source Edition of Google Japanese Input.
*   [fcitx-kkc](https://www.archlinux.org/packages/?name=fcitx-kkc), a new Japanese Kana Kanji input engine, based on [libkkc](https://www.archlinux.org/packages/?name=libkkc).

#### Other languages

*   [fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul), for typing Korean hangul, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul).
*   [fcitx-unikey](https://www.archlinux.org/packages/?name=fcitx-unikey), for typing Vietnamese characters.
*   [fcitx-sayura](https://www.archlinux.org/packages/?name=fcitx-sayura), for typing Sinhalese.
*   [fcitx-m17n](https://www.archlinux.org/packages/?name=fcitx-m17n), for other languages provided by [M17n](http://www.nongnu.org/m17n/).

### Input method module

To obtain a better experience in Gtk+ and Qt programs, install the [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt4](https://www.archlinux.org/packages/?name=fcitx-qt4) and [fcitx-qt5](https://www.archlinux.org/packages/?name=fcitx-qt5) input method modules as your need, or the [fcitx-im](https://www.archlinux.org/groups/x86_64/fcitx-im/) group to install all of them.

Applications below do not use Gtk+/Qt input module:

*   Applications use Tk, motif or xlib
*   Emacs, Opera, OpenOffice, LibreOffice, Skype, Wine, Java, Xterm, urxvt, WPS

### Others

*   [fcitx-ui-light](https://www.archlinux.org/packages/?name=fcitx-ui-light), light UI for fcitx.
*   [fcitx-fbterm](https://www.archlinux.org/packages/?name=fcitx-fbterm), for Fbterm support.
*   [fcitx-table-extra](https://www.archlinux.org/packages/?name=fcitx-table-extra), extra table.
*   [fcitx-table-other](https://www.archlinux.org/packages/?name=fcitx-table-other), tables for Latex, Emoji and others.
*   [kcm-fcitx](https://www.archlinux.org/packages/?name=kcm-fcitx), KDE configuration module for fcitx.

Others packages (including git version) are also available in the [AUR](/index.php/AUR "AUR"). All components of fcitx will requires fcitx to restart after install.

## Usage

**Note:** You need to have [east Asian fonts](/index.php/Fonts_FAQ#Chinese.2C_Japanese.2C_Korean.2C_Vietnamese "Fonts FAQ") installed if you want to enter Chinese, Japanese, Korean or Vietnamese characters.

### Desktop Environment

If you are using any XDG compatible desktop environment such as [KDE](/index.php/KDE "KDE"), [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE"), after you relogin, the autostart should work out of box. If not, open your favorite terminal, type:

```
$ fcitx

```

To see if fcitx is working correctly, open an application such as leafpad and press CTRL+Space (the default shortcut for switching input method) to invoke FCITX and input some words.

If Fcitx failed to start with your desktop automatically or if you want to change the parameters to start fcitx, please use tools provided by your desktop environment to configure xdg auto start or edit the `fcitx-autostart.desktop` file in your `~/.config/autostart/` directory (copy it from `/etc/xdg/autostart/` if it doesn't exist yet).

If your desktop environment does not support xdg auto start, please add the following command to your startup script (after the environment variables are set up properly).

```
$ fcitx

```

When other input methods with xim support is also running, Fcitx may fail to start due to xim error. Please make sure no other input method is running before you start Fcitx.

### Non desktop environment

Add the following lines to your desktop start up script files to register the input method modules and support xim programs.

*   Use `.xprofile` if you are using KDM, GDM, LightDM or SDDM.
*   Use `.xinitrc` if you are using startx or Slim.

```
 export GTK_IM_MODULE=fcitx
 export QT_IM_MODULE=fcitx
 export XMODIFIERS=@im=fcitx

```

*   Re-login to make these environment changes effective.

**Note:** Avoid `.bashrc` for this, see [DotFiles](http://mywiki.wooledge.org/DotFiles)

**Note:** If all Qt apps have problem with fcitx, run qtconfig (qtconfig-qt4), and go to the third tab, make sure fcitx is in the "Default Input Method" combo-box.

### Xim

Optionally, you can use xim in your GTK+ and/or Qt programs without installing the above modules in which case you need to change the corresponding lines above as following:

```
 export GTK_IM_MODULE=xim
 export QT_IM_MODULE=xim

```

**Warning:** Using xim can sometimes cause problems including not being able to input, no cursor following, word selection window issue, application freeze on input method restart. For these xim related problems, Fcitx cannot provide any fix or support. This is the same with any other input method framework, so please use the GTK+ and Qt input method modules instead of xim whenever possible

**Note:** Gtk2 uses `/usr/lib/gtk-2.0/2.10.0/immodules.cache` as immodule cache file since 2.24.20\. If you have set `GTM_IM_MODULE_FILE` environment variable or do not use install script of official packages to update the cache, please change/clear the environment variable and use `/usr/bin/gtk-query-immodules-2.0 --update-cache` to update immodule cache.

## Configuration

### Configuration tools

Fcitx provides GUI configure tools. You can install either [kcm-fcitx](https://www.archlinux.org/packages/?name=kcm-fcitx)(KDE), [fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool) (based on gtk3). Run fcitx-config-gtk3 after [fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool) is installed. Unset *Only Show Current Language* if you want to enable a input method of a different language.

Note that Fcitx does not supports manual configuration while its GUI is active.

In order to enable spell checking, press ctrl + alt + h when fcitx is on a input method provides by fcitx-keyboard. Then that's it, you can type long word, to see whether it works.

### Change default UI

Fcitx support kimpanel protocal to provide bettter desktop intergation.

#### Gnome-Shell

You can install kimpanel from extensions.gnome.org or [gnome-shell-extension-kimpanel-git](https://aur.archlinux.org/packages/gnome-shell-extension-kimpanel-git/) package in [AUR](/index.php/AUR "AUR"), which provides a similar user experience as ibus-gjs.

#### KDE

[kdeplasma-addons-applets-kimpanel](https://www.archlinux.org/packages/?name=kdeplasma-addons-applets-kimpanel) - a plasmoids providing native feeling under kde. Simply add kimpanel to plasma and fcitx will automatically switch to it without extra configuration.

#### kimpanel UI

[kimtoy](https://www.archlinux.org/packages/?name=kimtoy) could use skin from Sogou and fcitx.

#### Extend pinyin dictionary

Pinyin dictionary is located at `~/.config/fcitx/pinyin`. File `pybase.mb` is for single characters and file `pyphrase.mb` defines pinyin phrases. To extend them, put your file into `/usr/share/fcitx/pinyin` and restart fcitx.

## Tips and tricks

### Clipboard Access

You can use fcitx to input text in you clipboard (as well as a short clipboard history and primary selection). The default trigger key is Control-;. You can change the trigger key as well as other options in the Clipboard addon configure page.

NOTE: This is NOT a clipboard manager, it doesn't hold the selection or change its content as what a clipboard manager is supposed to do. It can only be used to input from the clipboard.

**Warning:** Some clients do not support multi-line input, so you may see the multi-line clipboard content pasted as a single line using fcitx-clipboard. This is either a bug or feature of the program being used and it is not something fcitx is able to help with.

## Troubleshooting

### Diagnose the problem

If you have problems using fcitx, eg. Ctrl+Space fail to work in all applications, then the first thing you should try is to diagnose using `fcitx-diagnose`. The output of `fcitx-diagnose` should contain the clue to most common problems. Providing the output of it will also help when you consult other people(eg. in IRC or forums).

### Emacs

If your `LC_CTYPE` is English, you may not be able to use input method in emacs due to an old emacs' bug. You can set your `LC_CTYPE` to something else such as `zh_CN.UTF-8` before emacs starts to get rid of this problem.

Note that the corresponding locale should be enabled on your your system. Uncomment the corresponding line, for example, `zh_CN.UTF-8`, in `/etc/locale.gen` and run `locale-gen`.

If you are using [emacs daemon/client mode](/index.php/Emacs#As_a_daemon "Emacs"), `LC_CTYPE` should be set when starting the daemon. For example, by running emacs daemon with `LC_CTYPE=zh_CN.UTF-8 emacs --daemon`

The default fontset will use `-*-*-*-r-normal--14-*-*-*-*-*-*-*' as basefont(in src/xfns.c), if you do not have one matched(like terminus、or 75dpi things, you can look the output of `xlsfonts'), XIM can not be activated.

### Input method module

**Warning:** You may still be able to use input method in most programs without the input method module, however, you may have unsolvable weird problems if you do so.

**Warning:** for firefox above version 13, the popup menu may fail to work due to xim, please make sure that fcitx-gtk2 along with a latest version fcitx are installed.

### Ctrl+Space fail to work in GTK programs

This problem sometimes happens especially when locale is set as English. Please make sure your GTK_IM_MODULE is set correctly.

See also [FAQ](http://fcitx-im.org/wiki/FAQ#When_use_Ctrl_.2B_Space.2C_Fcitx_cannot_be_triggered_on)

If you have set the *_IM_MODULE environment variables to fcitx but cannot activate fcitx, please check if you have installed the corresponding input method modules.

Some programs can only use xim, if you are using these programs, please make sure your XMODIFIERS is set properly and be aware of the problems you may have. These programs includes: all programs that are not using gtk or qt (e.g. programs that use tk, motif, or xlib directly), emacs, opera, openoffice, libreoffice, skype

If you cannot enable fcitx in gnome-terminal under gnome and the above way doesn't work, try:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'fcitx'>}"

```

### Buildin Chinese Pinyin Default NOT ACTIVE

If your locale is `en_US.UTF-8`, fcitx did NOT enable the buildin Chinese Pinyin input method by default. There is only `fcitx-keyboard-us` input method enabled. You can get a notice by `fcitx-diagnose` command like this:

```
   ## Input Methods:
       1\.  Found 1 enabled input methods:
               fcitx-keyboard-us
       2\.  Default input methods:
           **You only have one input method enabled, please add a keyboard input method as the first one and your main input method as the second one.**

```

Then you should add `Pinyin` or `Shuangpin` input method to actived input methods by the GUI configure tool.

### fcitx and KDE

For some reasons, [KDE](/index.php/KDE "KDE") doesn't handle keyboard layouts properly. For example, if you switch from US (English) to LT (Lithuanian), all numbers on the keyboard should produce Lithuanian letters, but they still produce numbers as the output. This can be fixed by these steps:

1.  Install required packages mentioned [here](#KDE).
2.  Turn off `fcitx` if it's running in the background.
3.  Disable stuff related to KDE:
    1.  At *System settings --> Input devices --> Layouts (tab)* make sure that "Configure layouts" is unchecked.
    2.  At *System settings --> Input devices --> Advanced (tab)* make sure that "Configure keyboard options" is unchecked.
4.  Open terminal and type `fcitx` to start it. You can close terminal - `fcitx` will still be running in the background.
5.  Set up your needed layouts (Right click on the system tray icon, then "Configure").
6.  Right click on the system tray icon, then "Exit"

At this point you should have working layouts, native KDE layouts switch icon should appear and you can switch them by mouse scroll or click on it.

### Input method switched to English unintentionally

For instance, in XMind, when the user presses Enter to create a node, input method is always switched to English, and have to be switched back to Chinese manually.

To fix this issue, open the fcitx GUI configuration tool (provided by [fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool)), switch to tab "Global Config", in dropdown menu "Share State Among Window", select "PerProgram" or "All".

## See also

*   [Fcitx GitHub](https://github.com/fcitx/fcitx/)
*   [Fcitx Wiki](http://fcitx-im.org/)