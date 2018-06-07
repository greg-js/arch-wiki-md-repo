Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")
*   [Nimf](/index.php/Nimf "Nimf")
*   [IBus](/index.php/IBus "IBus")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")
*   [Fcitx](/index.php/Fcitx "Fcitx")

**Warning:** Dasom is no longer maintained, last update was 2016.[[1]](https://github.com/dasom-im)

[Dasom](https://dasom-im.github.io) is a multilingual [input method framework](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
    *   [1.2 Initial setup](#Initial_setup)
*   [2 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dasom-git](https://aur.archlinux.org/packages/dasom-git/) package.

Additionally, you might want to install input method modules packages such as [dasom-gtk-git](https://aur.archlinux.org/packages/dasom-gtk-git/) for GTK+, [dasom-qt-git](https://aur.archlinux.org/packages/dasom-qt-git/) for Qt applications.

### Input method engines

*   [dasom-jeongeum-git](https://aur.archlinux.org/packages/dasom-jeongeum-git/), for typing Korean hangul, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul).

### Initial setup

Add the following lines to your desktop start up script files to register the input method modules and support xim programs.

*   Use `.xprofile` if you are using KDM, GDM, LightDM or SDDM.
*   Use `.xinitrc` if you are using startx or Slim.

```
export GTK_IM_MODULE=dasom
export QT_IM_MODULE=dasom
export XMODIFIERS="@im=dasom"
dasom-daemon
dasom-indicator

```

Re-login to make these environment changes effective.

**Note:** If you are using GNOME, you may need to run the following commands to use dasom:
```
$ gsettings set org.gnome.settings-daemon.plugins.keyboard active false
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/IMModule':<'dasom'>}"

```

## See also

*   [Dasom GitHub](https://github.com/dasom-im/dasom/)
*   [Dasom Homepage](http://dasom-im.github.io)