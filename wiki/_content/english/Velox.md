[Velox](https://github.com/michaelforney/velox) is a dynamic tiling window manager for wayland. Is is currently under development.

## Installation

There are two packages available on the [AUR](/index.php/AUR "AUR"), velox and velox-git. [velox](https://aur.archlinux.org/packages/velox/) is supposed to be the more stable package and [velox-git](https://aur.archlinux.org/packages/velox-git/) the upstream version. Even though *velox* is supposed to be the more stable branch, that's not always the case since that branch rarely gets updated and a lot of bug fixes have been pushed since.

The default terminal emulator for velox is [st-wl-git](https://aur.archlinux.org/packages/st-wl-git/) as it has great wayland support. Other terminals such as [urxvt](/index.php/Urxvt "Urxvt") also work, but only under xwayland.

You probably also want to install [dmenu-wl-git](https://aur.archlinux.org/packages/dmenu-wl-git/) from the AUR to be able to more easily launch applications.

## Configuration

Velox is configured from a configuration file. The configuration file should be in the users home folder named .velox.conf and the defalt configuration can be found [here](https://raw.githubusercontent.com/michaelforney/velox/master/velox.conf.sample).

## Starting Velox

If you are using the [velox](https://aur.archlinux.org/packages/velox/) package, you simply execute *velox* from your terminal.

If you are using [velox-git](https://aur.archlinux.org/packages/velox-git/), you will have to install the package [libinput](https://www.archlinux.org/packages/?name=libinput) from the extras reposiroty as well as [swc-git](https://aur.archlinux.org/packages/swc-git/) from the AUR since the velox-git AUR package is out of date. When these packages are installed, you simply execute *swc-launch velox* from your terminal.