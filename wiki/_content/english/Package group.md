A **package group** is a set of related packages, defined by the [packager](/index.php/Packager "Packager"), which can be installed or uninstalled simultaneously by using the group name as a substitute for each individual package name. While a group is not a package, it can be installed in a similar fashion to a package, see [Pacman#Installing package groups](/index.php/Pacman#Installing_package_groups "Pacman") and [PKGBUILD#groups](/index.php/PKGBUILD#groups "PKGBUILD").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Groups](#Groups)
    *   [1.1 base](#base)
    *   [1.2 base-devel](#base-devel)
*   [2 Difference to a meta package](#Difference_to_a_meta_package)
*   [3 See also](#See_also)

## Groups

The most important package groups are:

### base

The [base](https://www.archlinux.org/groups/x86_64/base/) group contains:

*   essential software like the [kernel](/index.php/Kernel "Kernel"), [Bash](/index.php/Bash "Bash"), the [core utilities](/index.php/Core_utilities "Core utilities") and [pacman](/index.php/Pacman "Pacman")
*   non-essential software like [dhcpcd](/index.php/Dhcpcd "Dhcpcd"), [netctl](/index.php/Netctl "Netctl"), [nano](/index.php/Nano "Nano") and [vi](/index.php/Vi "Vi").

### base-devel

The [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group contains tools required to build many packages like [GCC](/index.php/GCC "GCC") and [make](/index.php/GNU_make "GNU make"). See also [makepkg#Usage](/index.php/Makepkg#Usage "Makepkg").

## Difference to a meta package

A *meta package*, often (though not always) titled with the "-meta" suffix, provides similar functionality to a package group in that it enables multiple related packages to be installed or uninstalled simultaneously. Meta packages can be installed just like any other package (see [Pacman#Installing specific packages](/index.php/Pacman#Installing_specific_packages "Pacman")). The only difference between a meta package and a regular package is that a meta package is empty and exists purely to link related packages together via dependencies.

The advantage of a meta package, compared to a group, is that any new member packages will be installed when the meta package itself is updated with a new set of dependencies. This is in contrast to a group where new group members will not be automatically installed. The disadvantage of a meta package is that it is not as flexible as a group; you can choose which group members you wish to install but you cannot choose which meta package dependencies you wish to install. Likewise, you can uninstall group members without having to remove the entire group. However, you cannot remove meta package dependencies without having to uninstall the meta package itself.

## See also

*   [List of all package groups](https://www.archlinux.org/groups/)
*   Examples:
    *   [GNOME#Installation](/index.php/GNOME#Installation "GNOME")
    *   [KDE#Installation](/index.php/KDE#Installation "KDE")
    *   [i3#Installation](/index.php/I3#Installation "I3")