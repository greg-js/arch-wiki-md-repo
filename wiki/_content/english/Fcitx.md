[Fcitx](https://en.wikipedia.org/wiki/Fcitx "wikipedia:Fcitx") is a lightweight [input method](/index.php/Input_method "Input method") framework aimed at providing environment independent language support for Linux. It supports a lot of different languages and also provides many useful non-CJK features.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
        *   [1.1.1 Chinese](#Chinese)
        *   [1.1.2 Japanese](#Japanese)
        *   [1.1.3 Other languages](#Other_languages)
    *   [1.2 Input method module](#Input_method_module)
    *   [1.3 Others](#Others)
*   [2 Usage](#Usage)
    *   [2.1 Desktop Environment Autostart](#Desktop_Environment_Autostart)
    *   [2.2 Set environment variables for IM modules](#Set_environment_variables_for_IM_modules)
    *   [2.3 XIM](#XIM)
*   [3 Configuration](#Configuration)
    *   [3.1 GUI configuration tools](#GUI_configuration_tools)
    *   [3.2 Input methods configuration](#Input_methods_configuration)
    *   [3.3 Change default UI](#Change_default_UI)
    *   [3.4 Extend pinyin dictionary](#Extend_pinyin_dictionary)
    *   [3.5 Skins](#Skins)
    *   [3.6 Cloud Pinyin configuration](#Cloud_Pinyin_configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Clipboard Access](#Clipboard_Access)
    *   [4.2 fcitx-remote](#fcitx-remote)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Disable or change *Extra key for trigger input method* [sic]](#Disable_or_change_Extra_key_for_trigger_input_method_[sic])
    *   [5.2 Diagnose the problem](#Diagnose_the_problem)
    *   [5.3 Emacs](#Emacs)
        *   [5.3.1 Emacs Daemon](#Emacs_Daemon)
    *   [5.4 Firefox popup menu not work](#Firefox_popup_menu_not_work)
    *   [5.5 Ctrl+Space fail to work in GTK programs](#Ctrl+Space_fail_to_work_in_GTK_programs)
    *   [5.6 Buildin Chinese Pinyin Default NOT ACTIVE](#Buildin_Chinese_Pinyin_Default_NOT_ACTIVE)
    *   [5.7 fcitx and KDE](#fcitx_and_KDE)
    *   [5.8 Input method switched to English unintentionally](#Input_method_switched_to_English_unintentionally)
    *   [5.9 xmodmap settings being overwritten](#xmodmap_settings_being_overwritten)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [fcitx](https://www.archlinux.org/packages/?name=fcitx) package.

### Input method engines

Fcitx provides built-in input methods for Chinese [Pinyin](https://en.wikipedia.org/wiki/Pinyin "wikipedia:Pinyin") and table-based input (for example [Wubi](https://en.wikipedia.org/wiki/Wubi_method "wikipedia:Wubi method")).

Depending on the language you wish to type, other input method engines are available:

#### Chinese

*   [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin), based on [sunpinyin](https://www.archlinux.org/packages/?name=sunpinyin). It strikes a good balance between speed and accuracy.
*   [fcitx-libpinyin](https://www.archlinux.org/packages/?name=fcitx-libpinyin), based on [libpinyin](https://www.archlinux.org/packages/?name=libpinyin). It has a better algorithm than [fcitx-sunpinyin](https://www.archlinux.org/packages/?name=fcitx-sunpinyin).
*   [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime), based on schemas from the [Rime IME](/index.php/Rime_IME "Rime IME") project.
*   [fcitx-googlepinyin](https://www.archlinux.org/packages/?name=fcitx-googlepinyin), the Google pinyin IME for Android.
*   [fcitx-sogoupinyin](https://aur.archlinux.org/packages/fcitx-sogoupinyin/), [Sogou input method](http://pinyin.sogou.com/linux/) supporting Jianpin, fuzzy sound, cloud input, English input, and mixed skin.
*   [fcitx-cloudpinyin](https://www.archlinux.org/packages/?name=fcitx-cloudpinyin) uses internet sources to provide input candidates. The selected cloud result will be added to local dictionary. It support all fcitx pinyin input method except [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime).
*   [fcitx-chewing](https://www.archlinux.org/packages/?name=fcitx-chewing) is a popular Zhuyin input engine for Traditional Chinese based on [libchewing](https://www.archlinux.org/packages/?name=libchewing).
*   [fcitx-table-extra](https://www.archlinux.org/packages/?name=fcitx-table-extra) adds [Cangjie](https://en.wikipedia.org/wiki/Cangjie_input_method "wikipedia:Cangjie input method"), [Zhengma](https://en.wikipedia.org/wiki/Zhengma_method "wikipedia:Zhengma method"), [Boshiamy](https://en.wikipedia.org/wiki/Boshiamy_method "wikipedia:Boshiamy method") support.

#### Japanese

*   [fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc), based on [Mozc](/index.php/Mozc "Mozc"), the Open Source Edition of Google Japanese Input.
*   [fcitx-kkc](https://www.archlinux.org/packages/?name=fcitx-kkc), a Japanese Kana Kanji input engine, based on [libkkc](https://www.archlinux.org/packages/?name=libkkc).
*   [fcitx-anthy](https://www.archlinux.org/packages/?name=fcitx-anthy), a popular Japanese input engine. However, it is not actively developed anymore.

#### Other languages

*   [fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul), for typing Korean hangul, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul).
*   [fcitx-unikey](https://www.archlinux.org/packages/?name=fcitx-unikey), for typing Vietnamese characters.
*   [fcitx-sayura](https://www.archlinux.org/packages/?name=fcitx-sayura), for typing Sinhalese.
*   [fcitx-m17n](https://www.archlinux.org/packages/?name=fcitx-m17n), for other languages provided by [M17n](http://www.nongnu.org/m17n/).

### Input method module

To obtain a better experience in Gtk+ and Qt programs, install the [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt4](https://aur.archlinux.org/packages/fcitx-qt4/) and [fcitx-qt5](https://www.archlinux.org/packages/?name=fcitx-qt5) input method modules as your need, or the [fcitx-im](https://www.archlinux.org/groups/x86_64/fcitx-im/) group to install all of them. Without those modules, the input method may work on most applications but you may experience input method hang up, preview window screen location error or no preview error.

Applications below do not use Gtk+/Qt input module:

*   Applications use Tk, motif or xlib
*   Emacs, Opera, OpenOffice, LibreOffice, Skype, Wine, Java, Xterm, urxvt, WPS

### Others

*   [fcitx-ui-light](https://www.archlinux.org/packages/?name=fcitx-ui-light), light UI for fcitx.
*   [fcitx-table-extra](https://www.archlinux.org/packages/?name=fcitx-table-extra), extra table.
*   [fcitx-table-other](https://www.archlinux.org/packages/?name=fcitx-table-other), tables for Latex, Emoji and others.
*   [#GUI configuration tools](#GUI_configuration_tools)

Others packages (including git version) are also available in the [AUR](/index.php/AUR "AUR"). All components of fcitx will requires fcitx to restart after install.

## Usage

**Note:** You need to have [Chinese, Japanese, Korean or Vietnamese font](/index.php/Fonts#Chinese,_Japanese,_Korean,_Vietnamese "Fonts") installed to be able to enter the corresponding characters.

### Desktop Environment Autostart

If you are using any XDG compatible desktop environment such as [KDE](/index.php/KDE "KDE"), [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE"), after you re-login, the autostart should work out of box. If not run the *fcitx* executable. To see if fcitx is working correctly, open an application and press `Ctrl+Space` (the default shortcut for switching the input method) to invoke fcitx and input some words.

If fcitx failed to start with your desktop automatically or if you want to change the parameters to start fcitx, configure [autostart](/index.php/Autostarting#On_Xorg_startup "Autostarting") or edit the `fcitx-autostart.desktop` file in your `~/.config/autostart/` directory (copy it from `/etc/xdg/autostart/` if it doesn't exist yet).

When other input methods with xim support are also running, fcitx may fail to start due to an xim error. Ensure that no other input methods are running before you start fcitx.

Also please set the following environment variables to prefer IM modules for GTK/Qt applications.

### Set environment variables for IM modules

[Define](/index.php/Define "Define") the environment variables to register the input method modules and support xim programs.

 `~/.pam_environment` 
```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx

```

Re-login or reboot to make these environment changes effective.

If *fcitx* process does not start automatically, you might need to add `fcitx &` in your `~/.xinitrc`.

**Note:**

*   Avoid `.bashrc` for this, see [GregsWiki:DotFiles](https://mywiki.wooledge.org/DotFiles "gregswiki:DotFiles").
*   If all Qt apps have problem with fcitx, run *qtconfig* (*qtconfig-qt4*), and go to the third tab, make sure *fcitx* is in the *Default Input Method* combo-box.

### XIM

Optionally, you can use the [X Input Method](https://en.wikipedia.org/wiki/X_Input_Method "wikipedia:X Input Method") (XIM) in your GTK+ and/or Qt programs without installing the above modules in which case you need to change the corresponding lines above as following:

```
GTK_IM_MODULE=xim
QT_IM_MODULE=xim

```

**Warning:** Using XIM can sometimes cause problems including not being able to input, no cursor following, word selection window issue, application freeze on input method restart. For these XIM related problems, Fcitx cannot provide any fix or support. This is the same with any other input method framework, so please use the GTK+ and Qt input method modules instead of xim whenever possible

**Note:** Gtk2 uses `/usr/lib/gtk-2.0/2.10.0/immodules.cache` as immodule cache file since 2.24.20\. If you have set `GTM_IM_MODULE_FILE` environment variable or do not use install script of official packages to update the cache, please change/clear the environment variable and use `/usr/bin/gtk-query-immodules-2.0 --update-cache` to update immodule cache.

**Note:** Qt5 applications no longer support XIM protocol as Qt4 did, and rely on IM modules entirely for communicating with fcitx.

## Configuration

### GUI configuration tools

fcitx provides a [KDE](/index.php/KDE "KDE") configuration module ([kcm-fcitx](https://www.archlinux.org/packages/?name=kcm-fcitx)) and a GTK3 configuration tool ([fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool)).

Run *fcitx-config-gtk3* after [fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool) is installed. Unset *Only Show Current Language* if you want to enable an input method for a different language.

Stop fcitx manually before changing configuration, or the change may be lost.

In order to enable spell checking, press `Ctrl+Alt+h` when fcitx is on an input method provided by fcitx-keyboard.

### Input methods configuration

You can add/remove input methods in the GUI tools. Note that the search is case sensitive.

The first set input method is the inactive state, while all the rest will be active states. You generally want the inactive state to be one of the *Keyboard* options (e.g. "Keyboard - English (US)"). These options just input based on the keyboard layout in the name.

Under *Global Config*, the *Trigger Input Method* shortcut will only switch between the inactive and last used active state. The *Scroll between Input Methods* will by default only scroll between different active states, but can also be set to include the inactive state in the advanced settings. Furthermore, the *Scroll between Input Methods* shortcut has to be pressed in order, e.g. `ALT_SHIFT` will only activate if `alt` is pressed before `shift`.

Configuration settings for IME's can be found by by setting the keyboard to the desired IME and right-clicking the tray icon.

### Change default UI

Fcitx support kimpanel protocol to provide better desktop integration.

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

After installing the [fcitx-cloudpinyin](https://www.archlinux.org/packages/?name=fcitx-cloudpinyin) input method, restart fcitx. If you could not find it in configuration GUI, enable advanced settings. The cloud query result will be added to current input method dictionary automatically.

If your network prevents you from accessing Google, change Cloud Pinyin source to Baidu.

The query result from cloud will list as secondary candidate by default and it is configurable. If the result already exists, only one item is shown.

**Note:** Set query result as first candidate is not recommend because the dictionary order will be changed if query returns an empty result

## Tips and tricks

### Clipboard Access

You can use fcitx to input text in you clipboard (as well as a short clipboard history and primary selection). The default trigger key is `Ctrl-;`. You can change the trigger key as well as other options in the Clipboard addon configure page.

**Note:** This is NOT a clipboard manager, it doesn't hold the selection or change its content as what a clipboard manager is supposed to do. It can only be used to input from the clipboard.

**Warning:** Some clients do not support multi-line input, so you may see the multi-line clipboard content pasted as a single line using fcitx-clipboard. This is either a bug or feature of the program being used and it is not something fcitx is able to help with.

### fcitx-remote

*fcitx-remote* is a commandline tool that can be used to control the fcitx state. It is installed with the [fcitx](https://www.archlinux.org/packages/?name=fcitx) package.

One option worth elaborating upon here is `fcitx-remote -s *imname*`, which switches to the input method identified by `*imname*`. The correct `*imname*` for an in use input method can be found by executing *fcitx-diagnose*, and looking under the "## Input Methods:" section.

## Troubleshooting

### Disable or change *Extra key for trigger input method* [sic]

This setting is under the *Global Config* tab and defaults to *SHIFT Both*, meaning that pressing *either* shift key will immediately change input methods. Although it should only apply when a shift key is pressed individually, it tends to randomly interrupt typing capital letters, selecting text with the keyboard, etc. while using standard keyboard input.

In addition, this setting may revert to default without warning at any time. To ensure fcitx's config cannot be modified, you must make fcitx's config file immutable: `# chattr +i ~/.config/fcitx/config`.

### Diagnose the problem

If you have problems using fcitx, eg. Ctrl+Space fail to work in all applications, then the first thing you should try is to diagnose using `fcitx-diagnose`. The output of `fcitx-diagnose` should contain the clue to most common problems. Providing the output of it will also help when you consult other people(eg. in IRC or forums).

### Emacs

If your `LC_CTYPE` is English, you may not be able to use input method in emacs due to an old emacs bug. You can set your `LC_CTYPE` to something else such as `zh_CN.UTF-8` before emacs starts to get rid of this problem.

Note that the corresponding [locale](/index.php/Locale "Locale") should be [generated](/index.php/Locale#Generating_locales "Locale") on your your system.

The default fontset will use `-*-*-*-r-normal--14-*-*-*-*-*-*-*' as basefont (in `src/xfns.c`), if you do not have one matched (like terminus or 75dpi things, you can look the output of `xlsfonts'), XIM can not be activated.

#### Emacs Daemon

If you are using [emacs daemon/client mode](/index.php/Emacs#As_a_daemon "Emacs"), `LC_CTYPE` should be set when starting the daemon. For example, by running emacs daemon with `LC_CTYPE=zh_CN.UTF-8 emacs --daemon`.

If starting emacs daemon from [systemd](/index.php/Systemd "Systemd"), [set](/index.php/Systemd#Editing_provided_units "Systemd") `Environment="LC_CTYPE=zh_CN.UTF-8" "XMODIFIERS=@im=fcitx"` in the unit file.

(`XMODIFIERS` may need to be set explicitly here as systemd doesn't load `.xprofile`. Check the `initial-environment` variable in emacs to verify both variables are set correctly.)

### Firefox popup menu not work

For [Firefox](/index.php/Firefox "Firefox") above version 13, the popup menu may fail to work due to xim, make sure that [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3) along with a latest version fcitx are installed.

### Ctrl+Space fail to work in GTK programs

This problem sometimes happens especially when the locale is set as English. Please make sure your `GTK_IM_MODULE` is set correctly.

See also [FAQ](http://fcitx-im.org/wiki/FAQ#When_use_Ctrl_.2B_Space.2C_Fcitx_cannot_be_triggered_on)

If you have set the `*_IM_MODULE` environment variables to fcitx but cannot activate fcitx, please check if you have installed the corresponding input method modules.

Some programs can only use xim, if you are using these programs, please make sure your `XMODIFIERS` is set properly and be aware of the problems you may have. These programs include all programs that are not using GTK or Qt (e.g. programs that use tk, motif, or xlib directly), emacs, opera, openoffice, libreoffice, skype.

If you cannot enable fcitx in *gnome-terminal* under Gnome and the above way doesn't work, try:

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

1.  Turn off *fcitx* if it is running in the background.
2.  Disable stuff related to KDE:
    1.  At *System settings > Input devices > Layouts (tab)* make sure that *Configure layouts* is unchecked.
    2.  At *System settings > Input devices > Advanced (tab)* make sure that *Configure keyboard options* is unchecked.
3.  Start *fcitx* to start it. You can close the terminal - *fcitx* will still be running in the background.
4.  Set up your needed layouts (right click on the system tray icon, then *Configure*).
5.  Right click on the system tray icon, then *Exit*

At this point you should have working layouts, native KDE layouts switch icon should appear and you can switch them by mouse scroll or click on it.

### Input method switched to English unintentionally

For instance, in XMind, when the user presses `Enter` to create a node, input method is always switched to English, and has to be switched back to Chinese manually.

To fix this issue, open the *fcitx* GUI configuration tool (provided by [fcitx-configtool](https://www.archlinux.org/packages/?name=fcitx-configtool)), switch to tab *Global Config*, in dropdown menu *Share State Among Window*, select *PerProgram* or *All*.

### xmodmap settings being overwritten

fcitx controls keyboard layout, so your [xmodmap](/index.php/Xmodmap "Xmodmap") settings will be overwritten. Since 4.2.7, Fcitx will try to load `~/.Xmodmap` if it exists.

For more details on how you can save your xmodmap changes see [FAQ](http://fcitx-im.org/wiki/FAQ#xmodmap_settings_being_overwritten)

## See also

*   [Fcitx GitLab](https://gitlab.com/fcitx/fcitx)
*   [Fcitx Wiki](http://fcitx-im.org/)