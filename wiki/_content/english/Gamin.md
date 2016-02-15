[Gamin](https://en.wikipedia.org/wiki/Gamin "wikipedia:Gamin") is a file and directory monitoring system defined to be a subset of the FAM (File Alteration Monitor) system. It is a service provided by a library which allows for the detection of modification to a file or directory.

Gamin re-implements the [FAM](/index.php/FAM "FAM") specification with [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify"). It is newer and more actively maintained than FAM, maintains compatibility with FAM and can replace it in almost every case. It is a [GNOME](/index.php/GNOME "GNOME") project, but does not have GNOME dependencies.

## Installation

If FAM is installed, first [disable](/index.php/Disable "Disable") `fam.service`; then remove the [fam](https://aur.archlinux.org/packages/fam/) package, ignoring any reverse dependencies:

```
# pacman -Rdd fam

```

Now you can install the [gamin](https://www.archlinux.org/packages/?name=gamin) package.

## External links

*   [FAM, Gamin and inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)