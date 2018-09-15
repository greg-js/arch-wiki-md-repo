Related articles

*   [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) is a collection of supplemental `build_env` and `tidy` scripts for [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/), a fork of [pacman-git](https://aur.archlinux.org/packages/pacman-git/). Their purpose is to provide macros to [makepkg](/index.php/Makepkg "Makepkg") for several kinds of optimization in build and packaging stages, both in response to [the simplification of makepkg](https://lists.archlinux.org/pipermail/pacman-dev/2016-February/020826.html) and as a proposal [for a future version of pacman](https://lists.archlinux.org/pipermail/pacman-dev/2018-May/022498.html).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Configuration](#Configuration)
*   [2 Build an optimized package](#Build_an_optimized_package)
*   [3 Build an optimized package in a clean chroot](#Build_an_optimized_package_in_a_clean_chroot)
    *   [3.1 Chroot Setup](#Chroot_Setup)
        *   [3.1.1 Install required packages](#Install_required_packages)
        *   [3.1.2 Create a Profile-guided Optimization cache](#Create_a_Profile-guided_Optimization_cache)
    *   [3.2 Using the chroot](#Using_the_chroot)
        *   [3.2.1 Build a package](#Build_a_package)
            *   [3.2.1.1 Building with Profile-guided optimization](#Building_with_Profile-guided_optimization)

## Installation

Install [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/) and [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) from the [AUR](/index.php/AUR "AUR").

To make optimizations available, install their backends: [graphite](https://www.archlinux.org/packages/?name=graphite), [openmp](https://www.archlinux.org/packages/?name=openmp), [upx](https://www.archlinux.org/packages/?name=upx), [optipng](https://www.archlinux.org/packages/?name=optipng), and [nodejs-svgo](https://aur.archlinux.org/packages/nodejs-svgo/)

### Configuration

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) generates an additional [configuration file](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5), from your current [makepkg](/index.php/Makepkg "Makepkg") configuration, with supplementary options for optimization that are disabled by default.

## Build an optimized package

First, edit [`/etc/makepkg-optimize.conf`](/index.php/Makepkg-optimize#Configuration "Makepkg-optimize") and select your preferred optimizations for [`ARCHITECTURE, COMPILE FLAGS`](/index.php/Makepkg#Building_optimized_binaries "Makepkg"), `BUILD ENVIRONMENT`, `GLOBAL PACKAGE OPTIONS` and `COMPRESSION DEFAULTS`.

**Warning:** While many packages build with all optimizations enabled, some will not. It may take a few attempts to find which--if any--optimizations a package is compatible with. Some software may also experience runtime problems caused by over-optimization.

When [building](/index.php/Makepkg#Usage "Makepkg"), pass the [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) configuration file to makepkg:

```
$ makepkg --config /etc/makepkg-optimize.conf

```

**Note:** Building with [Profile-guided optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization") requires that a package be built and installed *twice*. The first phase initiates profile generation in `$PROFDEST/$pkgbase.gen` while the second moves the profiles to `$PROFDEST/$pkgbase.used` and applies them to the software being packaged.

## Build an optimized package in a [clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")

**Note:** Read [Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Classic_Way "DeveloperWiki:Building in a Clean Chroot") and familiarize yourself with the "Classic Way".

It is not necessary to install [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/) or [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) in your Archlinux installation. Alternatively, they can be used to build optimized packages within a [chroot](/index.php/Chroot "Chroot").

### Chroot Setup

After [setting up a chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Setting_Up_A_Chroot "DeveloperWiki:Building in a Clean Chroot"), a few additional steps are needed.

#### Install required packages

First, install [Git](/index.php/Git "Git") and some of the backends for the optimization macros:

```
$ arch-nspawn -M /etc/makepkg.conf "$CHROOT"/root pacman -S git graphite openmp upx optipng

```

Then [download](/index.php/Arch_User_Repository#Acquire_build_files "Arch User Repository"), [build](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Building_in_the_Chroot "DeveloperWiki:Building in a Clean Chroot") and [install](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Manual_package_installation "DeveloperWiki:Building in a Clean Chroot") [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/), [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/), and [nodejs-svgo](https://aur.archlinux.org/packages/nodejs-svgo/).

#### Create a [Profile-guided Optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization") cache

First, create a folder in the same place--both inside and outside of the chroot--to store profiles:

```
# mkdir -m 777 {"$CHROOT"/root,}/mnt/pgo

```

Then edit `$CHROOT/root/etc/makepkg-optimize.conf` and set `PROFDEST=/mnt/pgo` under `PACKAGE OUTPUT`.

### Using the chroot

**Note:** When [updating](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Building_in_the_Chroot "DeveloperWiki:Building in a Clean Chroot") the chroot, [AUR packages](/index.php/Makepkg-optimize#Install_required_packages "Makepkg-optimize") will have to be updated manually

#### Build a package

First, edit [`$CHROOT/root/etc/makepkg-optimize.conf`](/index.php/Makepkg-optimize#Configuration "Makepkg-optimize") and select your preferred optimizations for [`ARCHITECTURE, COMPILE FLAGS`](/index.php/Makepkg#Building_optimized_binaries "Makepkg"), `BUILD ENVIRONMENT`, `GLOBAL PACKAGE OPTIONS` and `COMPRESSION DEFAULTS`.

When [building](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot#Building_in_the_Chroot "DeveloperWiki:Building in a Clean Chroot"), pass the [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) configuration file to makepkg:

```
$ makechrootpkg -c -r "$CHROOT" -- --config /etc/makepkg-optimize.conf

```

##### Building with [Profile-guided optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization")

After the first building phase, bind the PGO folder:

```
# mount -o bind {,"$CHROOT"/"$USER"}/mnt/pgo

```

Once the package is [installed](/index.php/Pacman#Usage.23Additional_commands "Pacman"), test-run its executables.

Then, for the second building phase, remove package cruft but *do not* clean the chroot (do not pass `-c`):

**Note:** If you have rebooted, be sure to rebind the PGO folder. Alternatively, use [fstab](/index.php/Fstab "Fstab") to bind these folders persistently.

```
$ rm -rf *.pkg.tar.xz pkg src; makechrootpkg -r "$CHROOT" -- --config /etc/makepkg-optimize.conf

```