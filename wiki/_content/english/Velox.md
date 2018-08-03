[Velox](https://github.com/michaelforney/velox) is a dynamic tiling window manager for wayland. It is currently under development.

## Installation

[Install](/index.php/Install "Install") the [velox](https://aur.archlinux.org/packages/velox/) package, or [velox-git](https://aur.archlinux.org/packages/velox-git/) for the development version.

The default terminal emulator for velox is [st-wayland-git](https://aur.archlinux.org/packages/st-wayland-git/) as it has great wayland support. Other terminals such as [urxvt](/index.php/Urxvt "Urxvt") also work, but only under xwayland.

You probably also want to install [dmenu-wayland-git](https://aur.archlinux.org/packages/dmenu-wayland-git/) from the AUR to be able to more easily launch applications.

## Configuration

Velox is configured from a configuration file. The configuration file should be in the users home folder named .velox.conf and the defalt configuration can be found [here](https://raw.githubusercontent.com/michaelforney/velox/master/velox.conf.sample).

## Starting Velox

If you are using the [velox](https://aur.archlinux.org/packages/velox/) package, you simply execute *velox* from your terminal.

If you are using [velox-git](https://aur.archlinux.org/packages/velox-git/), you will have to install the package [libinput](https://www.archlinux.org/packages/?name=libinput) from the extras reposiroty as well as [swc-git](https://aur.archlinux.org/packages/swc-git/) from the AUR since the velox-git AUR package is out of date. When these packages are installed, you simply execute *swc-launch velox* from your terminal.