The freedesktop project provides the [Icon Theme Specification](http://standards.freedesktop.org/icon-theme-spec/latest/), which applies to most linux desktop environments and tries to unify the look of a whole bunch of icons in an _icon-theme_. Freedesktop also provides the [Icon Naming Specification](http://standards.freedesktop.org/icon-naming-spec/latest/), which defines a standard naming scheme for icons believed to be installed on any system. The default theme _hicolor_ should include them all.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Icons and emblems](#Icons_and_emblems)
    *   [1.2 Mime type icons](#Mime_type_icons)
    *   [1.3 Icon themes](#Icon_themes)
        *   [1.3.1 From a package](#From_a_package)
        *   [1.3.2 Manually](#Manually)
*   [2 fstab / gvfs](#fstab_.2F_gvfs)
*   [3 Xfce icons](#Xfce_icons)

## Installation

### Icons and emblems

To append a custom icon to an existing icon theme `xdg-icon-resource` can be used. This will resize and copy the icon to `$HOME/.local/share/icons/`. With this method, custom emblems can also be added. Examples:

```
$ xdg-icon-resource install --size 128 --context emblems archuser-example.png # add as emblem
$ xdg-icon-resource install --size 128 archuser-example.png # add as normal icon

```

### Mime type icons

Todays file managers do not rely on the traditional mime type which `file --mime` outputs. Instead definitions from `/usr/share/mime/` are used. Calling an icon according to the definition found there and copying it to `~/.local/share/icons` will cause the file manager to display the custom mime type icon. This command illustrates the method:

 `Creates a custom icon for keepass database files (*.kdb)` 

```
# grep kdb /usr/share/mime/globs | egrep -o '.+\/[^:]+' | tr '/' '-'
application-x-keepass ;# rename your icon according to this output
xdg-icon-resource install --size 128 --context mimetypes application-x-keepass.png

```

### Icon themes

**Tip:** It is recommended to install the [hicolor-icon-theme](https://www.archlinux.org/packages/?name=hicolor-icon-theme) package as many programs will deposit their icons in `/usr/share/icons/hicolor` and most other icon themes will inherit icons from the Hicolor icon theme.

#### From a package

*   [Official repositories](/index.php/Official_repositories "Official repositories") — ["icon-theme" search](https://www.archlinux.org/packages/?sort=&q=icon-theme&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR "AUR") — ["icon-theme" search](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=icon-theme&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

#### Manually

If you cannot find a package for the icon theme you are looking for, you will need to install it manually.

*   Firstly, find and download your desired icon pack. Many different icon themes can be downloaded from the following sites: [Customize.org](http://www.customize.org), [Opendesktop.org](http://opendesktop.org) and [Xfce-look.org](http://xfce-look.org/).

*   Then navigate to the directory which contains the icon pack and extract it. Example `tar -xzf /home/user/downloads/icon-pack.tar.gz`.

*   Move the extracted folder containing the icons to either `~/.icons` or `~/.local/share/icons` (user only) or to `/usr/share/icons` (systemwide).

*   Optional: run `gtk-update-icon-cache -f -t ~/.icons/<theme_name>` to update the icon cache.

*   Select the icon theme using the appropriate configuration tool for your [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager").

## fstab / gvfs

According to this [document](https://github.com/GNOME/gvfs/blob/master/monitor/udisks2/what-is-shown.txt) file managers using [GVFS](/index.php/GVFS "GVFS") (like nautilus or thunar) can display icons for custom locations, like NFS shares. All you need are some extended mount options inside `/etc/fstab` with icon names supported by your selected icon theme:

 `/etc/fstab` 

```
hostname:/ /mnt/ nfs4 defaults,_netdev,user,rw,exec,comment=x-gvfs-show,x-gvfs-name=Network%20Attached%20Storage,x-gvfs-icon=network-server,x-gvfs-symbolic-icon=network-server,timeo=14,noatime 0 0

```

## Xfce icons

Not all icon themes provide a complete set of icons for the [Xfce](/index.php/Xfce "Xfce") environment. Listed below are a number of icon themes that do.

*   [faenza-icon-theme](https://www.archlinux.org/packages/?name=faenza-icon-theme) and [faience-icon-theme](https://www.archlinux.org/packages/?name=faience-icon-theme) (depends on faenza)
*   [rave-x-colors](https://aur.archlinux.org/packages/rave-x-colors/) - An icon theme based on Faenza with fully colored folders and support for dark panels.
*   [vibrancy-colors](https://aur.archlinux.org/packages/vibrancy-colors/) - A flat, modern icon theme with fully colored folders and support for dark panels.
*   [gnome-colors-icon-theme](https://aur.archlinux.org/packages/gnome-colors-icon-theme/) - a set of icons, similar to the [GNOME](/index.php/GNOME "GNOME") icon theme, with good Xfce support.
*   [echo-icon-theme-git](https://aur.archlinux.org/packages/echo-icon-theme-git/) - previously the default icon theme for Fedora. The non git version does not contain all of the Xfce icons.
*   [gnome-icon-theme-xfce](https://aur.archlinux.org/packages/gnome-icon-theme-xfce/) - a package which adds the missing icons to the [GNOME](/index.php/GNOME "GNOME") icon theme.
*   [elementary-xfce-icons](https://aur.archlinux.org/packages/elementary-xfce-icons/) - Elementary icons forked from upstream, extended and maintained for Xfce.