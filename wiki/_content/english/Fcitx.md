Related articles

*   [IBus](/index.php/IBus "IBus")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")

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
    *   [3.2 Input methods configuration](#Input_methods_configuration)
    *   [3.3 Change default UI](#Change_default_UI)
    *   [3.4 Extend pinyin dictionary](#Extend_pinyin_dictionary)
    *   [3.5 Skins](#Skins)
    *   [3.6 Cloud Pinyin configuration](#Cloud_Pinyin_configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Clipboard Access](#Clipboard_Access)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Diagnose the problem](#Diagnose_the_problem)
    *   [5.2 Emacs](#Emacs)
        *   [5.2.1 Emacs Daemon](#Emacs_Daemon)
    *   [5.3 Firefox popup menu not work](#Firefox_popup_menu_not_work)
    *   [5.4 Ctrl+Space fail to work in GTK programs](#Ctrl.2BSpace_fail_to_work_in_GTK_programs)
    *   [5.5 Buildin Chinese Pinyin Default NOT ACTIVE](#Buildin_Chinese_Pinyin_Default_NOT_ACTIVE)
    *   [5.6 fcitx and KDE](#fcitx_and_KDE)
    *   [5.7 Input method switched to English unintentionally](#Input_method_switched_to_English_unintentionally)
    *   [5.8 xmodmap settings being overwritten](#xmodmap_settings_being_overwritten)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [fcitx](https://www.archlinux.org/packages/?name=fcitx) package.

### Input method engines

Fcitx provides built-in input methods for Chinese [Pinyin](https://en.wikipedia.org/wiki/Pinyin "wikipedia:Pinyin") and table-based input (for example [Wubi](https://en.wikipedia.org/wiki/Wubi "wikipedia:Wubi")).

Depending on the language you wish to type, other input method engines are available:

#### Chinese

*   [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin), based on [sunpinyin](https://www.archlinux.org/packages/?name=sunpinyin). It strikes a good balance between speed and accuracy.
*   [fcitx-libpinyin](https://www.archlinux.org/packages/?name=fcitx-libpinyin), based on [libpinyin](https://www.archlinux.org/packages/?name=libpinyin). It has a better algorithm than [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin).
*   [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime), based on schemas from the [Rime IME](/index.php/Rime_IME "Rime IME") project.
*   [fcitx-googlepinyin](https://www.archlinux.org/packages/?name=fcitx-googlepinyin), the Google pinyin IME for Android.
*   [fcitx-sogoupinyin](https://aur.archlinux.org/packages/fcitx-sogoupinyin/), Sogou input method for linux—Supports, Jianpin, fuzzy sound, cloud input, English input, mixed skin.[Official website](http://pinyin.sogou.com/linux/)
*   [fcitx-cloudpinyin](https://www.archlinux.org/packages/?name=fcitx-cloudpinyin) uses internet sources to provide input candidates. The selected cloud result will be added to local dictionary. It support all fcitx pinyin input method except [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime).
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

To obtain a better experience in Gtk+ and Qt programs, install the [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt4](https://www.archlinux.org/packages/?name=fcitx-qt4) and [fcitx-qt5](https://www.archlinux.org/packages/?name=fcitx-qt5) input method modules as your need, or the [fcitx-im](https://www.archlinux.org/groups/x86_64/fcitx-im/) group to install all of them. Without those modules, the input method may work on most applications but you may experience input method hang up, preview window screen location error or no preview error.

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

If you are using any XDG compatible desktop environment such as [KDE](/index.php/KDE "KDE"), [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE"), after you relogin, the autostart should work out of box. If not, open your favorite terminal, type `fcitx`. To see if fcitx is working correctly, open an application such as leafpad and press CTRL+Space (the default shortcut for switching input method) to invoke FCITX and input some words.

If Fcitx failed to start with your desktop automatically or if you want to change the parameters to start fcitx, please use tools provided by your desktop environment to configure xdg auto start or edit the `fcitx-autostart.desktop` file in your `~/.config/autostart/` directory (copy it from `/etc/xdg/autostart/` if it doesn't exist yet).

If your desktop environment does not support xdg auto start, please add `fcitx` to your startup script (after the environment variables are set up properly).

When other input methods with xim support is also running, Fcitx may fail to start due to xim error. Please make sure no other input method is running before you start Fcitx.

### Non desktop environment

Add the following lines to your desktop start up script files to register the input method modules and support xim programs.

*   Use `.xprofile` if you are using GDM, LightDM or SDDM with Xorg.
*   Use `/etc/environment` for Wayland, it will not read environment variables stored in `~/.xprofile`
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

Stop fcitx manually before changing configuration, or the change may be lost.

In order to enable spell checking, press ctrl + alt + h when fcitx is on a input method provides by fcitx-keyboard. Then that's it, you can type long word, to see whether it works.

### Input methods configuration

You can add/remove input methods in GUI tools. Set first item to Keyborad layout (e.g. Keyboard - English) if you want to enable/disable other input methods quickly.

### Change default UI

Fcitx support kimpanel protocol to provide bettter desktop intergation.

*   Gnome-Shell: You can install kimpanel from extensions.gnome.org or [gnome-shell-extension-kimpanel-git](https://aur.archlinux.org/packages/gnome-shell-extension-kimpanel-git/), which provides a similar user experience as ibus-gjs.
*   KDE: [kimtoy](https://www.archlinux.org/packages/?name=kimtoy) could use skin from Sogou and fcitx.

### Extend pinyin dictionary

Pinyin dictionary is located at `~/.config/fcitx/pinyin`. File `pybase.mb` is for single characters and file `pyphrase.mb` defines pinyin phrases. To extend them, put your file into `/usr/share/fcitx/pinyin` and restart fcitx.

### Skins

You can download skins and extract them to one of the following directories, you can create the directory if it doesn't exist:

```
/usr/share/fcitx/skin   #Global settings
~/.config/fcitx/skin    #User settings

```

### Cloud Pinyin configuration

After install [fcitx-cloudpinyin](https://www.archlinux.org/packages/?name=fcitx-cloudpinyin) input method, restart fcitx. If you could not find it in configuration GUI, enable advanced setting. The cloud query result will be added to current input method dictionary automatically.

If your network could not access Google, change Cloud Pinyin source to Baidu.

The query result from cloud will list as secondary candicate by default and it is configuable. If the result already exit, only one item is shown.

**Note:** Set query result as first candicate is not recommend because the dictionary order will be changed if query return empty result。

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

The default fontset will use `-*-*-*-r-normal--14-*-*-*-*-*-*-*' as basefont(in src/xfns.c), if you do not have one matched(like terminus、or 75dpi things, you can look the output of `xlsfonts'), XIM can not be activated.

#### Emacs Daemon

If you are using [emacs daemon/client mode](/index.php/Emacs#As_a_daemon "Emacs"), `LC_CTYPE` should be set when starting the daemon. For example, by running emacs daemon with `LC_CTYPE=zh_CN.UTF-8 emacs --daemon`.

If starting emacs daemon from systemd, set Environment in the unit file like this:

```
Environment="LC_CTYPE=zh_CN.UTF-8" "XMODIFIERS=@im=fcitx"

```

(XMODIFIERS may need to be set explicitly here as systemd doesn't load .xprofile. Check the `initial-environment` variable in emacs to verify both variables are set correctly.)

### Firefox popup menu not work

For firefox above version 13, the popup menu may fail to work due to xim, please make sure that fcitx-gtk2 along with a latest version fcitx are installed.

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

### xmodmap settings being overwritten

Fcitx controls keyboard layout, so your xmodmap settings will be overwritten. Since 4.2.7, Fcitx will try to load ~/.Xmodmap if it exists.

For more details on how you can save your xmodmap changes see [FAQ](http://fcitx-im.org/wiki/FAQ#xmodmap_settings_being_overwritten)

## See also

*   [Fcitx GitHub](https://github.com/fcitx/fcitx/)
*   [Fcitx Wiki](http://fcitx-im.org/)