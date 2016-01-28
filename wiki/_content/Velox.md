# Velox

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Velox](https://github.com/michaelforney/velox) is a dynamic tiling window manager for wayland. Is is currently under development.

## Installation

There are two packages available on the [AUR](/index.php/AUR "AUR"), velox and velox-git. [velox](https://aur.archlinux.org/packages/velox/)<sup><small>AUR</small></sup> is supposed to be the more stable package and [velox-git](https://aur.archlinux.org/packages/velox-git/)<sup><small>AUR</small></sup> the upstream version. Even though _velox_ is supposed to be the more stable branch, that's not always the case since that branch rarely gets updated and a lot of bug fixes has been pushed since.

The default terminal emulator for velox is [st-wl-git](https://aur.archlinux.org/packages/st-wl-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/st-wl-git)]</sup> as it has great wayland support. Other terminals such as [urxvt](/index.php/Urxvt "Urxvt") also work, but only under xwayland.

You probably also want to install [dmenu-wl-git](https://aur.archlinux.org/packages/dmenu-wl-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu-wl-git)]</sup> from the AUR to be able to more easily launch applications.

## Configuration

Velox is configured from a configuration file. The configuration file should be in the users home folder named .velox.conf and the defalt configuration can be found [here](https://raw.githubusercontent.com/michaelforney/velox/master/velox.conf.sample).

## Starting Velox

If you are using the [velox](https://aur.archlinux.org/packages/velox/)<sup><small>AUR</small></sup> package, you simply execute _velox_ from your terminal.

If you are using [velox-git](https://aur.archlinux.org/packages/velox-git/)<sup><small>AUR</small></sup>, you will have to install the package [libinput](https://www.archlinux.org/packages/?name=libinput) from the extras reposiroty as well as [swc-git](https://aur.archlinux.org/packages/swc-git/)<sup><small>AUR</small></sup> from the AUR since the velox-git AUR package is out of date. When these packages are installed, you simply execute _swc-launch velox_ from your terminal.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Velox&oldid=392781](https://wiki.archlinux.org/index.php?title=Velox&oldid=392781)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")