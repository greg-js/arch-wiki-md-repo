Related articles

*   [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64")

The *multilib* repository is an [official repository](/index.php/Official_repositories "Official repositories") which allows the user to run and build 32-bit applications on 64-bit installations of Arch Linux.

## Contents

*   [1 Directory structure](#Directory_structure)
*   [2 Enabling](#Enabling)
*   [3 Disabling](#Disabling)
*   [4 See also](#See_also)

## Directory structure

With the multilib repository enabled, the 32-bit compatible libraries are located under `/usr/lib32/`.

## Enabling

To use the [multilib](/index.php/Official_repositories#multilib "Official repositories") repository, uncomment the `[multilib]` section in `/etc/pacman.conf` (Please be sure to uncomment both lines):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Then [upgrade](/index.php/Upgrade "Upgrade") the system and install the desired multilib packages.

**Tip:** Run `pacman -Sl multilib` to list all packages in the *multilib* repository. 32-bit library package names begin with `lib32-`.

## Disabling

To revert to a pure 64-bit system:

Execute the following command to remove all packages that were installed from *multilib*:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

If you have conflicts with gcc-libs reinstall the [gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs) package and the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group.

Comment out the `[multilib]` section in `/etc/pacman.conf`:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

Then [upgrade](/index.php/Upgrade "Upgrade") the system.

## See also

*   [Makepkg#Build 32-bit packages on a 64-bit system](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg")
*   [64-bit FAQ](/index.php/64-bit_FAQ "64-bit FAQ")
*   [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib) mailing list