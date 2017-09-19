[Inkscape](http://inkscape.org/) is a vector graphics editor application. It is distributed under a free software license, the GNU GPL. Its stated goal is to become a powerful graphics tool while being fully compliant with the XML, SVG, and CSS standards.[wikipedia:Inkscape](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Build error with libpng 1.2.x](#Build_error_with_libpng_1.2.x)
    *   [2.2 Tooltips unreadable with KDE Plasma](#Tooltips_unreadable_with_KDE_Plasma)
*   [3 See also](#See_also)

## Installation

[inkscape](https://www.archlinux.org/packages/?name=inkscape) can be installed from the [official repositories](/index.php/Official_repositories "Official repositories"). The development version is available in the [AUR](/index.php/AUR "AUR") as [inkscape-git](https://aur.archlinux.org/packages/inkscape-git/).

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

### Tooltips unreadable with KDE Plasma

Under KDE's system settings go to colors > options and disable "Apply colors to non-QT-applications". Restart Inkscape if was running before the change.

## See also

*   [Multimedia in Arch Linux](/index.php/Multimedia_in_Arch_Linux "Multimedia in Arch Linux")
*   [Inkscape Homepage](http://inkscape.org/)
*   [Inkscape at Wikipedia](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")