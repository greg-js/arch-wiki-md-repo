Enabling the *multilib* repository allows the user to run and build 32-bit applications on 64-bit installations of Arch Linux. *multilib* creates a directory containing 32-bit instruction set libraries inside `/usr/lib32/`, which 32-bit binary applications may need when executed.

## Contents

*   [1 Directory structure](#Directory_structure)
*   [2 Enabling](#Enabling)
*   [3 Disabling](#Disabling)
*   [4 See also](#See_also)

## Directory structure

A 64-bit installation of Arch Linux with *multilib* enabled follows a directory structure similar to Debian. The 32-bit compatible libraries are located under `/usr/lib32/`, and the native 64-bit libraries under `/usr/lib/`.

## Enabling

To use the [multilib](/index.php/Official_repositories#multilib "Official repositories") repository, uncomment the `[multilib]` section in `/etc/pacman.conf` (Please be sure to uncomment both lines):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Then update the package list and upgrade with `pacman -Syu`.

**Note:** Do not just run `pacman -Sy`, see [System maintenance#Partial upgrades are unsupported](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance").

## Disabling

To revert to a pure 64-bit system, uninstalling *multilib*:

Execute the following command to remove all packages that were installed from *multilib*:

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

*   [Makepkg#Build 32-bit packages on a 64-bit system](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg")
*   [64-bit FAQ](/index.php/64-bit_FAQ "64-bit FAQ")
*   [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib) mailing list