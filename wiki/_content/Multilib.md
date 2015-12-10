# Multilib

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64")

Enabling the _multilib_ repository allows the user to run and build 32-bit applications on 64-bit installations of Arch Linux. _multilib_ creates a directory containing 32-bit instruction set libraries inside `/usr/lib32/`, which 32-bit binary applications may need when executed.

## Contents

*   [1 Directory structure](#Directory_structure)
*   [2 Enabling](#Enabling)
*   [3 Disabling](#Disabling)
*   [4 See also](#See_also)

## Directory structure

A 64-bit installation of Arch Linux with _multilib_ enabled follows a directory structure similar to Debian. The 32-bit compatible libraries are located under `/usr/lib32/`, and the native 64-bit libraries under `/usr/lib/`.

## Enabling

To use the [multilib](/index.php/Official_repositories#multilib "Official repositories") repository, uncomment the `[multilib]` section in `/etc/pacman.conf` (Please be sure to uncomment both lines):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Then update the package list and upgrade with `pacman -Syu`.

**Note:** Do not just run `pacman -Sy`, see [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance").

## Disabling

To revert to a pure 64-bit system, uninstalling _multilib_:

Execute the following command to remove all packages that were installed from _multilib_:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

If you have conflicts with gcc-libs reinstall the 64-bit versions and try the previous command again:

```
# pacman -S gcc-libs base-devel

```

Comment out the `[multilib]` section in `/etc/pacman.conf`:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

Then update the package list and upgrade with `pacman -Syu`.

## See also

*   [64-bit FAQ](/index.php/64-bit_FAQ "64-bit FAQ")
*   [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib) mailing list

Retrieved from "[https://wiki.archlinux.org/index.php?title=Multilib&oldid=411025](https://wiki.archlinux.org/index.php?title=Multilib&oldid=411025)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")