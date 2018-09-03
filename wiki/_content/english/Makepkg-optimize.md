Related articles

*   [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) is a collection of supplemental `build_env` and `tidy` scripts for [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/), a fork of [pacman-git](https://aur.archlinux.org/packages/pacman-git/). Their purpose is to provide macros to [makepkg](/index.php/Makepkg "Makepkg") for several kinds of optimization in build and packaging stages, both in response to [the simplification of makepkg](https://lists.archlinux.org/pipermail/pacman-dev/2016-February/020826.html) and as a proposal [for a future version of pacman](https://lists.archlinux.org/pipermail/pacman-dev/2018-May/022498.html).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Configuration](#Configuration)
*   [2 Build an optimized package](#Build_an_optimized_package)
*   [3 Build an optimized package in a clean chroot](#Build_an_optimized_package_in_a_clean_chroot)
    *   [3.1 Chroot Setup (First time only)](#Chroot_Setup_.28First_time_only.29)
        *   [3.1.1 Proceeding *without* an AUR helper](#Proceeding_without_an_AUR_helper)
        *   [3.1.2 Proceeding *with* an AUR helper](#Proceeding_with_an_AUR_helper)
    *   [3.2 Using the chroot (Ever after)](#Using_the_chroot_.28Ever_after.29)
        *   [3.2.1 Keep your chroot up-to-date](#Keep_your_chroot_up-to-date)
        *   [3.2.2 Build a package](#Build_a_package)
            *   [3.2.2.1 When building with Profile-guided optimization](#When_building_with_Profile-guided_optimization)

## Installation

Install [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/) and [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) from the [AUR](/index.php/AUR "AUR").

To make optimizations available, install their backends: [graphite](https://www.archlinux.org/packages/?name=graphite), [openmp](https://www.archlinux.org/packages/?name=openmp), [upx](https://www.archlinux.org/packages/?name=upx), [optipng](https://www.archlinux.org/packages/?name=optipng), and [nodejs-svgo](https://aur.archlinux.org/packages/nodejs-svgo/)

### Configuration

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) generates an additional [configuration file](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5), `/etc/makepkg-optimize.conf`, from your current [makepkg](/index.php/Makepkg "Makepkg") configuration, with supplementary options for optimization that are disabled by default.

Edit this file and select your preferred optimizations for [`ARCHITECTURE, COMPILE FLAGS`](/index.php/Makepkg#Building_optimized_binaries "Makepkg"), `BUILD ENVIRONMENT`, `GLOBAL PACKAGE OPTIONS` and `COMPRESSION DEFAULTS`.

## Build an optimized package

In a directory containing a PKGBUILD, call [makepkg](/index.php/Makepkg "Makepkg") and specify the [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) configuration file:

```
$ makepkg --config /etc/makepkg-optimize.conf

```

**Note:** Building with [Profile-guided optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization") requires that a package be built and installed *twice*. The first phase initiates profile generation in `$PROFDEST/$pkgbase.gen` while the second moves the profiles to `$PROFDEST/$pkgbase.used` and applies them to the software being packaged.

**Warning:** While many packages build with all optimizations enabled, some will not. You may have to make a few attempts to find which--if any--optimizations a package is compatible with. Some software may also experience runtime problems caused by over-optimization.

## Build an optimized package in a clean chroot

**Note:** Read [Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Classic_Way "DeveloperWiki:Building in a Clean Chroot") and familiarize yourself with the "Classic" method.

It is not necessary to install [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/) or [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) in your Archlinux installation. Alternatively, they can be used to build optimized packages within a [chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").

### Chroot Setup (First time only)

After [setting up a chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Classic_Way.23Setting_Up_A_Chroot "DeveloperWiki:Building in a Clean Chroot"), a few additional steps are needed to build optimized packages.

Create a folder in the same place--both inside and outside of the chroot--to store [PGO](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization") profiles:

```
# mkdir -m 777 {"$CHROOT"/root,}/mnt/pgo

```

Edit `$CHROOT/root/etc/makepkg-optimize.conf` and set `PROFDEST=/mnt/pgo` under `PACKAGE OUTPUT`.

Create an unprivileged user inside the chroot:

```
# systemd-nspawn -D "$CHROOT"/root useradd "$USER"
# systemd-nspawn -D "$CHROOT"/root passwd "$USER"

```

Install some of the backends for [makepkg-optimize](/index.php/AUR "AUR")'s macros:

```
# systemd-nspawn -D "$CHROOT"/root pacman -S graphite openmp upx optipng

```

#### Proceeding *without* an [AUR helper](/index.php/AUR_helper "AUR helper")

**Tip:** [AUR](/index.php/AUR "AUR") packages can be installed within the chroot without the aid of an AUR helper by [downloading their PKGBUILDs](/index.php/Arch_User_Repository#Acquire_build_files "Arch User Repository"), then [building and installing them](/index.php/Arch_User_Repository#Build_and_install_the_package "Arch User Repository").

Install git in the chroot:

```
# systemd-nspawn -D "$CHROOT"/root pacman -S git

```

Log in to the chroot as an unprivileged user:

```
# arch-chroot -u "$USER" "$CHROOT"/root

```

Change to a permissive directory, such as `/home/$USER` or `/tmp` inside the chroot, then [clone](/index.php/Arch_User_Repository#Acquire_build_files "Arch User Repository"), [build and install](/index.php/Arch_User_Repository#Build_and_install_the_package "Arch User Repository") [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/), [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/), and [nodejs-svgo](https://aur.archlinux.org/packages/nodejs-svgo/).

#### Proceeding *with* an [AUR helper](/index.php/AUR_helper "AUR helper")

**Tip:** Installing an AUR helper inside the chroot saves several steps per [AUR](/index.php/AUR "AUR") package built and is especially useful for building packages with AUR dependencies, but generally goes against Arch policy.

Install [pikaur](https://github.com/actionless/pikaur/blob/master/README.md#installation) by [the above method](/index.php/Makepkg-optimize#Proceeding_without_an_AUR_helper "Makepkg-optimize").

Set up [sudo](/index.php/Sudo "Sudo") for the unprivileged user in the chroot:

```
# echo "$USER ALL=(root) NOPASSWD: /usr/bin/pacman" >> "$CHROOT"/root/etc/sudoers

```

Install AUR packages with pikaur:

```
$ arch-nspawn -M /etc/makepkg.conf "$CHROOT"/root -u "$USER" pikaur -S pacman-buildenv_ext-git makepkg-optimize nodejs-svgo

```

### Using the chroot (Ever after)

#### Keep your chroot up-to-date

Without an [AUR helper](/index.php/AUR_helper "AUR helper") ([update AUR packages individually](/index.php/Makepkg-optimize#Proceeding_without_an_AUR_helper "Makepkg-optimize")):

```
$ arch-nspawn -M /etc/makepkg.conf "$CHROOT"/root -u "$USER" pacman -Syu

```

Alternatively, with pikaur:

```
$ arch-nspawn -M /etc/makepkg.conf "$CHROOT"/root -u "$USER" pikaur -Syua

```

#### Build a package

Edit `$CHROOT/root/etc/makepkg-optimize.conf` and select your preferred optimizations for [`ARCHITECTURE, COMPILE FLAGS`](/index.php/Makepkg#Building_optimized_binaries "Makepkg"), `BUILD ENVIRONMENT`, `GLOBAL PACKAGE OPTIONS` and `COMPRESSION DEFAULTS`.

In a directory containing a PKGBUILD, call makechrootpkg with this configuration file:

```
$ makechrootpkg -c -r "$CHROOT" -- --config /etc/makepkg-optimize.conf

```

##### When building with [Profile-guided optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization")

Bind the PGO folder:

```
# mount -o bind {,"$CHROOT"/"$USER"}/mnt/pgo

```

Install the package and test run its executables.

For the second phase, remove cruft and rebuild the package, but *do not* clean the chroot. If you have rebooted, be sure to rebind the PGO folder first:

```
$ rm -rf *.pkg.tar.xz pkg src; makechrootpkg -r "$CHROOT" -- --config /etc/makepkg-optimize.conf

```