A **meta package** and a **package group** can be defined by the [packager](/index.php/Packager "Packager") to denote a set of related packages. Both can allow to install or uninstall this set of packages simultaneously by using the meta package or the group name as a substitute for each individual package name. While a group is not a package, it can be installed in a similar fashion to a package, see [Pacman#Installing package groups](/index.php/Pacman#Installing_package_groups "Pacman") and [PKGBUILD#groups](/index.php/PKGBUILD#groups "PKGBUILD").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Difference between meta package and package group](#Difference_between_meta_package_and_package_group)
*   [2 Meta packages](#Meta_packages)
*   [3 Groups](#Groups)
*   [4 See also](#See_also)

## Difference between meta package and package group

A *meta package*, often (though not always) titled with the "-meta" suffix, provides similar functionality to a package group in that it enables multiple related packages to be installed or uninstalled simultaneously. Meta packages can be installed just like any other package (see [Pacman#Installing specific packages](/index.php/Pacman#Installing_specific_packages "Pacman")). The only difference between a meta package and a regular package is that a meta package is empty and exists purely to link related packages together via dependencies.

The advantage of a meta package, compared to a group, is that any new member packages will be installed when the meta package itself is updated with a new set of dependencies. This is in contrast to a group where new group members will not be automatically installed. The disadvantage of a meta package is that it is not as flexible as a group; you can choose which group members you wish to install but you cannot choose which meta package dependencies you wish to install. Likewise, you can uninstall group members without having to remove the entire group. However, you cannot remove meta package dependencies without having to uninstall the meta package itself.

## Meta packages

The most important meta package is [base](https://www.archlinux.org/packages/?name=base). It contains a minimal package set that defines a basic Arch Linux installation. It includes:

*   basics such as [glibc](https://www.archlinux.org/packages/?name=glibc) and [bash](/index.php/Bash "Bash"),
*   distribution related things such as [pacman](/index.php/Pacman "Pacman") and [systemd](/index.php/Systemd "Systemd")
*   POSIX tools such as [core utilities](/index.php/Core_utilities "Core utilities"), process, file and file compression utilities
*   networking tools such as [iproute2](https://www.archlinux.org/packages/?name=iproute2)

The [kernel](/index.php/Kernel "Kernel") is an optional dependency. See [the announcement when it was introduced](https://www.archlinux.org/news/base-group-replaced-by-mandatory-base-package-manual-intervention-required/), and [reasoning why base is a meta package](https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029435.html).

## Groups

The most important package group is [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/). It contains tools required to build many packages like [GCC](/index.php/GCC "GCC") and [make](/index.php/GNU_make "GNU make"). See also [makepkg#Usage](/index.php/Makepkg#Usage "Makepkg").

## See also

*   [List of all package groups](https://www.archlinux.org/groups/)
*   Examples:
    *   [GNOME#Installation](/index.php/GNOME#Installation "GNOME")
    *   [KDE#Installation](/index.php/KDE#Installation "KDE")
    *   [i3#Installation](/index.php/I3#Installation "I3")