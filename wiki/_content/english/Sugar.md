A product of the [OLPC](https://en.wikipedia.org/wiki/One_Laptop_per_Child "wikipedia:One Laptop per Child") initiative, [Sugar](https://en.wikipedia.org/wiki/Sugar_(software) "wikipedia:Sugar (software)") is a Desktop Environment akin to [KDE](/index.php/KDE "KDE") and [GNOME](/index.php/GNOME "GNOME"), but geared towards children and education. If you have a young son, daughter, brother, sister, puppy or alien, the best way to introduce them to the world of Arch Linux is by deploying an Arch/Sugar platform and then forgetting about it.

Sugar has a special [Taxonomy](http://wiki.sugarlabs.org/go/Taxonomy) to name the parts of its system. The graphical interface itself constitute the **Glucose** group. This is the core system can reasonably expect to be present when installing Sugar. But to really use the environment, you need activities (some sort of applications). Base activities are part of **Fructose**. Then, **Sucrose** is constituted by both Glucose and Fructose and represents what should be distributed as a basic sugar desktop environment. Extra activities are part of **Honey**. Note that Ribose (the underlaying operating system) is here replaced by Arch.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 From [city] repository](#From_.5Bcity.5D_repository)
    *   [1.2 From AUR](#From_AUR)
    *   [1.3 From Activity Library](#From_Activity_Library)
*   [2 Starting Sugar](#Starting_Sugar)
*   [3 Packaging](#Packaging)
    *   [3.1 Notes](#Notes)
*   [4 See also](#See_also)

## Installation

**Note:** Sugar is on its way to the [official repositories](/index.php/Official_repositories "Official repositories"). Until this happens, packages are available in the unofficial [[city] repository](http://pkgbuild.com/~bgyorgy/city.html) (see below).

### From [city] repository

*   For the core system (_Glucose_), install [sugar](https://aur.archlinux.org/packages/sugar/), available in the [[city] repository](http://pkgbuild.com/~bgyorgy/city.html). It provides the graphical interface and a desktop session, but not very useful on its own.
*   The _sugar-fructose_ group contains the base activities (_Fructose_) including a web browser, a text editor, a media player and a terminal emulator.
*   The [sugar-runner](https://aur.archlinux.org/packages/sugar-runner/) package provides a helper script that makes it possible to launch Sugar within another desktop environment, or from the command line directly.

### From AUR

Install [sugar](https://aur.archlinux.org/packages/sugar/) from the [AUR](/index.php/AUR "AUR").

**Activities**

Activities are available under name `sugar-activity-**activity**` from AUR.

**Etoys**

`etoys` is provided separately as it is part of glucose but also include the fructose activity. It is available as [etoys](https://aur.archlinux.org/packages/etoys/) in AUR.

### From Activity Library

The [Sugar Activity Library](http://wiki.sugarlabs.org/go/Activity_Library) provides many [Activity Bundles](http://wiki.sugarlabs.org/go/Development_Team/Almanac/Activity_Bundles) packaged as zip files with the ".xo" extension. These bundles can be downloaded and installed to the user's directory from Sugar, but the installation does not ensure that the dependencies are satisfied. Therefore it's not the recommended way to install activities, because they likely fail to start due missing dependencies. Commonly used dependencies:

*   For web activities, install [webkit2gtk](https://www.archlinux.org/packages/?name=webkit2gtk) from the official repositories.
*   For GTK+ 2 based activities, install [sugar-toolkit](https://aur.archlinux.org/packages/sugar-toolkit/) from AUR.

In order to check why the activity fails to start, look at the log file located at `~/.sugar/default/logs/[app_id]-1.log`.

## Starting Sugar

Sugar can be started either graphically, using a [display manager](/index.php/Display_manager "Display manager"), or manually from the console.

**Graphically**

Select the session _Sugar_ from the display manager's session menu.

**Manually**

If [sugar-runner](https://aur.archlinux.org/packages/sugar-runner/) installed, Sugar can be launched with the `sugar-runner` command.

Alternative method is to add `exec sugar` to the `~/.xinitrc` file. After that, Sugar can be launched with the `startx` command (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details). After setting up the `~/.xinitrc` file, it can also be arranged to [Start X at login](/index.php/Start_X_at_login "Start X at login").

## Packaging

Almost all activities have the same building procedure, a `setup.py` that calls functions shipped with sugar. Below is a typical `PKGBUILD`:

 `PKGBUILD` 

```
# Contributor: Name <name@mail.com>
pkgname=sugar-activity-calculate
_realname=Calculate
pkgver=30
pkgrel=1
pkgdesc="A calculator for Sugar."
arch=('i686' 'x86_64')
url="[http://www.sugarlabs.org/](http://www.sugarlabs.org/)"
license=('GPL')
groups=('sucrose' 'fructose')
depends=('sugar')
source=([http://download.sugarlabs.org/sources/sucrose/fructose/${_realname}/${_realname}-$pkgver.tar.bz2](http://download.sugarlabs.org/sources/sucrose/fructose/${_realname}/${_realname}-$pkgver.tar.bz2))
md5sums=('011bd911516f27d05194320164c7dcd7')

build() {
  cd "$srcdir/${_realname}-$pkgver"
  ./setup.py install --prefix="$pkgdir/usr" || return 1
}
# vim:set ts=2 sw=2 et:
```

### Notes

*   Activity building procedure is not made for packaging and using `--prefix` can be dangerous if the application uses this path internally. I think the correct way to do this would be to patch the installation procedure in `sugar` so it accepts an argument such as `--destdir=`.

*   I _suggest_ that we prefix sugar activities packages in AUR with `sugar-activity-`.

## See also

*   [The Official Website of Sugar](http://sugarlabs.org/)
*   [Activities for Sugar](http://activities.sugarlabs.org/)