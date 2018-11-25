Related articles

*   [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) is a collection of supplemental `build_env` and `tidy` scripts for [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/). They provide macros to [makepkg](/index.php/Makepkg "Makepkg") for several kinds of optimization in `build()` and `package()` stages, both in response to [the simplification of makepkg](https://lists.archlinux.org/pipermail/pacman-dev/2016-February/020826.html) and as a proposal [for a future version of pacman](https://lists.archlinux.org/pipermail/pacman-dev/2018-November/022933.html).

**Warning:** Arch Linux only has official support for [pacman](https://www.archlinux.org/packages/?name=pacman) from [core](/index.php/Core "Core"). When using an alternate version, please mention so in support requests.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Configuration](#Configuration)
*   [2 Build an optimized package](#Build_an_optimized_package)
*   [3 Build an optimized package in a clean chroot](#Build_an_optimized_package_in_a_clean_chroot)
    *   [3.1 Chroot setup](#Chroot_setup)
        *   [3.1.1 Install makepkg-optimize and backends](#Install_makepkg-optimize_and_backends)
        *   [3.1.2 Create a profile-guided optimization cache](#Create_a_profile-guided_optimization_cache)
    *   [3.2 Using the chroot](#Using_the_chroot)
        *   [3.2.1 Build a package](#Build_a_package)
            *   [3.2.1.1 Building with profile-guided optimization](#Building_with_profile-guided_optimization)

## Installation

Install [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/) and [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) from the [AUR](/index.php/AUR "AUR").

To make optimizations available, install their backends: [graphite](https://www.archlinux.org/packages/?name=graphite), [openmp](https://www.archlinux.org/packages/?name=openmp), [upx](https://www.archlinux.org/packages/?name=upx), [optipng](https://www.archlinux.org/packages/?name=optipng), and [nodejs-svgo](https://aur.archlinux.org/packages/nodejs-svgo/)

### Configuration

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) generates an additional [configuration file](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5), `/etc/makepkg-optimize.conf`, from your current [makepkg](/index.php/Makepkg "Makepkg") configuration with supplementary options for [COMPILE FLAGS](/index.php/Makepkg#Building_optimized_binaries "Makepkg"), [BUILD ENVIRONMENT](https://aur.archlinux.org/cgit/aur.git/tree/buildenv_ext.conf?h=makepkg-optimize), [GLOBAL PACKAGE OPTIONS](https://aur.archlinux.org/cgit/aur.git/tree/pkgopts_ext.conf?h=makepkg-optimize), [PACKAGE OUTPUT](https://aur.archlinux.org/cgit/aur.git/tree/destdirs_ext.conf?h=makepkg-optimize), and [COMPRESSION DEFAULTS](https://aur.archlinux.org/cgit/aur.git/tree/compress-param_max.conf?h=makepkg-optimize) that are disabled by default.

**Warning:** Some packages may fail to build with certain optimizations and over-optimization may cause problems for some programs--such as decreased performance and segmentation faults.

## Build an optimized package

First, edit the configuration file and [select your preferred optimizations](#Configuration).

When [building](/index.php/Makepkg#Usage "Makepkg"), pass the configuration file:

```
$ makepkg --config /etc/makepkg-optimize.conf

```

**Note:** [Profile-guided optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization") requires that a package be built and installed *twice*. The first phase initiates profile generation in `$PROFDEST/$pkgbase.gen`; the second applies them and moves them to `$PROFDEST/$pkgbase.used`.

## Build an optimized package in a clean chroot

Alternatively, [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/) or [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) can be used to build optimized packages within a [chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Classic_way "DeveloperWiki:Building in a clean chroot").

### Chroot setup

After [setting up a chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Setting_up_a_chroot "DeveloperWiki:Building in a clean chroot"), a few additional steps are needed.

#### Install makepkg-optimize and backends

First, install some of the backends for the optimization macros to the base chroot:

```
$ arch-nspawn "$CHROOT"/root pacman -S graphite openmp upx optipng

```

Then [download](/index.php/Arch_User_Repository#Acquire_build_files "Arch User Repository") and [build](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Building_in_the_chroot "DeveloperWiki:Building in a clean chroot") [pacman-buildenv_ext-git](https://aur.archlinux.org/packages/pacman-buildenv_ext-git/), [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/), and [nodejs-svgo](https://aur.archlinux.org/packages/nodejs-svgo/).

To install them in the base chroot, copy their package files into it and install them, e.g.:

```
# cp nodejs-svgo-1.1.1-1-any.pkg.tar.xz "$CHROOT"/root/root/
$ arch-nspawn "$CHROOT"/root pacman -U /root/nodejs-svgo-1.1.1-1-any.pkg.tar.xz

```

#### Create a profile-guided optimization cache

First, create a folder in the same place, inside and outside of the chroot, to store [profiles](https://gcc.gnu.org/onlinedocs/gcc/Gcov-Data-Files.html):

```
# mkdir -m 777 {"$CHROOT"/root,}/mnt/pgo

```

Then edit `$CHROOT/root/etc/makepkg-optimize.conf` and set `PROFDEST=/mnt/pgo`.

### Using the chroot

**Note:** When [updating](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Building_in_the_chroot "DeveloperWiki:Building in a clean chroot") the chroot, [AUR packages](#Install_makepkg-optimize_and_backends) have to be updated manually.

#### Build a package

First, edit `$CHROOT/root/etc/makepkg-optimize.conf` and [select your preferred optimizations](#Configuration).

When [building](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Building_in_the_chroot "DeveloperWiki:Building in a clean chroot"), pass the configuration file to `makepkg`:

```
$ makechrootpkg -c -r "$CHROOT" -- --config /etc/makepkg-optimize.conf

```

##### Building with profile-guided optimization

After the first building phase, bind the [PGO cache](#Create_a_profile-guided_optimization_cache):

```
# mount -o bind {,"$CHROOT"/"$USER"}/mnt/pgo

```

**Tip:** Alternatively, use [fstab](/index.php/Fstab "Fstab") to bind these folders persistently.

Once the package is [installed](/index.php/Pacman#Additional_commands "Pacman"), test-run its executables.

**Note:** Profiles are generated on `exit()`. Persistent daemons, such as [systemd](/index.php/Systemd "Systemd"), may require a reboot to produce profiles; if you have rebooted, be sure to rebind the PGO cache before rebuilding.

For the second building phase, do *not* pass `-c` to `makechrootpkg`, but clean `$srcdir` and overwrite the previous package by passing `-Cf` to `makepkg`:

```
$ makechrootpkg -r "$CHROOT" -- -Cf --config /etc/makepkg-optimize.conf

```