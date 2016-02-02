# Inkscape

[Inkscape](http://inkscape.org/) is a vector graphics editor application. It is distributed under a free software license, the GNU GPL. Its stated goal is to become a powerful graphics tool while being fully compliant with the XML, SVG, and CSS standards.[[1]](https://en.wikipedia.org/wiki/Inkscape)

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Build error with libpng 1.2.x](#Build_error_with_libpng_1.2.x)
    *   [2.2 Segfaults with qtcurve-gtk2](#Segfaults_with_qtcurve-gtk2)
*   [3 See also](#See_also)

## Installation

[inkscape](https://www.archlinux.org/packages/?name=inkscape) can be installed from the [official repositories](/index.php/Official_repositories "Official repositories"). The development version is available in the [AUR](/index.php/AUR "AUR") as [inkscape-bzr](https://aur.archlinux.org/packages/inkscape-bzr/).

## Troubleshooting

### Build error with libpng 1.2.x

If inkscape fails to build with the following error:

```
In file included from /usr/include/libpng12/png.h:474,
from sp-image.cpp:44:
/usr/include/libpng12/pngconf.h:328: error: expected constructor, destructor, or type conversion before '.' token
/usr/include/libpng12/pngconf.h:329: error: '__dont__' does not name a type

```

You should be able to solve that by simply commenting the two mentioned Lines in `/usr/include/libpng12/pngconf.h` out:

```
//__pngconf.h__ already includes setjmp.h;
//__dont__ include it again.;

```

(I have got no idea what else those changes influence, so you might want to undo them after inkscape is built. This could be related to Debian Bug#522477 and might get fixed in libpng 1.4)

### Segfaults with qtcurve-gtk2

There is a problem with qtcurve-gtk2 1.8.18-3 that makes inkscape segfault shortly after launch. The bug is fixed upstream ([Bug 343704](https://bugs.kde.org/show_bug.cgi?id=343704#c3)) but no release is yet available and the AUR package qtcurve-git is not compatible with KDE Frameworks 5\. Best option today to use qtcurve and inkscape is to use speps patched packages from [FS#43631](https://bugs.archlinux.org/task/43631#comment132113).

## See also

*   [Multimedia in Arch Linux](/index.php/Multimedia_in_Arch_Linux "Multimedia in Arch Linux")
*   [Inkscape Homepage](http://inkscape.org/)
*   [Inkscape at Wikipedia](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Inkscape&oldid=407774](https://wiki.archlinux.org/index.php?title=Inkscape&oldid=407774)"