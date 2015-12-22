# Dasom

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [IBus](/index.php/IBus "IBus")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")
*   [Fcitx](/index.php/Fcitx "Fcitx")

[Dasom](http://dasom-im.github.io) is a multilingual [input method framework](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Input method engines](#Input_method_engines)
    *   [1.2 Initial setup](#Initial_setup)
*   [2 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dasom-git](https://aur.archlinux.org/packages/dasom-git/)<sup><small>AUR</small></sup> package.

Additionally, you might want to install input method modules packages such as [dasom-gtk-git](https://aur.archlinux.org/packages/dasom-gtk-git/)<sup><small>AUR</small></sup> for GTK+, [dasom-qt-git](https://aur.archlinux.org/packages/dasom-qt-git/)<sup><small>AUR</small></sup> for Qt applications.

### Input method engines

*   [dasom-jeongeum-git](https://aur.archlinux.org/packages/dasom-jeongeum-git/)<sup><small>AUR</small></sup>, for typing Korean hangul, based on [libhangul](https://www.archlinux.org/packages/?name=libhangul).

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dasom&oldid=413089](https://wiki.archlinux.org/index.php?title=Dasom&oldid=413089)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internationalization](/index.php/Category:Internationalization "Category:Internationalization")