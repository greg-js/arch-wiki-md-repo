Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")
*   [Dasom](/index.php/Dasom "Dasom")
*   [IBus](/index.php/IBus "IBus")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")
*   [Fcitx](/index.php/Fcitx "Fcitx")

**Warning:** As of May 2018 Nimf is no longer publicly maintained, the GitHub repository has been archived.[[1]](https://github.com/cogniti/nimf/issues/104)

[Nimf](https://github.com/cogniti/nimf) is a multilingual [input method framework](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method") which inherits [Dasom](/index.php/Dasom "Dasom").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
    *   [1.2 Initial setup](#Initial_setup)
*   [2 Editing Settings](#Editing_Settings)
*   [3 See also](#See_also)

## Installation

Just [Install](/index.php/Install "Install") the [nimf-git](https://aur.archlinux.org/packages/nimf-git/) package.

### Input method engines

*   nimf-libhangul, for typing Korean hangul, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul) (bundled in [nimf-git](https://aur.archlinux.org/packages/nimf-git/)).
*   nimf-sunpinyin, for typing Chinese using Pinyin, based on [sunpinyin](https://www.archlinux.org/packages/?name=sunpinyin) (bundled in [nimf-git](https://aur.archlinux.org/packages/nimf-git/)).
*   nimf-anthy, for typing Japanese, based on [anthy](https://www.archlinux.org/packages/?name=anthy) (In development. bundled in [nimf-git](https://aur.archlinux.org/packages/nimf-git/)).
*   nimf-chewing, for typing Chinese using Zhuyin, based on [libchewing](https://www.archlinux.org/packages/?name=libchewing) (In development. bundled in [nimf-git](https://aur.archlinux.org/packages/nimf-git/)).
*   nimf-rime, for typing Chinese, based on [librime](https://www.archlinux.org/packages/?name=librime) (In development. bundled in [nimf-git](https://aur.archlinux.org/packages/nimf-git/)).

### Initial setup

Add the following lines to your desktop start up script files to register the input method modules and support xim programs.

*   Use `.xprofile` if you are using KDM, GDM, LightDM or SDDM.
*   Use `.xinitrc` if you are using startx or Slim.

```
export GTK_IM_MODULE=nimf
export QT4_IM_MODULE="nimf"
export QT_IM_MODULE=nimf
export XMODIFIERS="@im=nimf"
nimf-daemon

```

Re-login to make these environment changes effective.

**Note:** If you are using GNOME, you may need to run the following commands to use nimf:
```
$ gsettings set org.gnome.settings-daemon.plugins.keyboard active false
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'nimf'>}"

```

## Editing Settings

Use `nimf-settings` to edit nimf settings. You can launch `nimf-settings` from your preferred terminal, or from the `nimf-indicator` menu which appears in system tray area.

## See also

*   [Nimf GitHub](https://github.com/cogniti/nimf)