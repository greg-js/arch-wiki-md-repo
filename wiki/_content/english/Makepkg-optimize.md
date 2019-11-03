Related articles

*   [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) is a collection of supplemental [tidy](https://git.archlinux.org/pacman.git/commit/?id=295a3491adc4af5c8634ac82777212ed9c664457), [buildenv](https://git.archlinux.org/pacman.git/commit/?id=508b4e3ec0cb3e365942f4dc0626edda4789932b), and [executable](https://git.archlinux.org/pacman.git/commit/?id=0bb04fa16a82db133dd010478c1256bc8500c5e7) scripts for [pacman](/index.php/Pacman "Pacman") which provide macros for several kinds of optimization in the `build()` and `package()` stages.

**Note:** As with any package in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) has no official support. You should read, and you may post [comments](/index.php/User:Quequotion/Arch_User_Repository#Commenting_on_packages "User:Quequotion/Arch User Repository") on its AUR page.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Configuration](#Configuration)
*   [2 Build an optimized package](#Build_an_optimized_package)
*   [3 Build an optimized package in a clean chroot](#Build_an_optimized_package_in_a_clean_chroot)
    *   [3.1 Chroot setup](#Chroot_setup)
        *   [3.1.1 Install makepkg-optimize and backends](#Install_makepkg-optimize_and_backends)
        *   [3.1.2 Create a PGO cache](#Create_a_PGO_cache)
    *   [3.2 Using the chroot](#Using_the_chroot)
        *   [3.2.1 Build a package](#Build_a_package)
            *   [3.2.1.1 Building with PGO](#Building_with_PGO)

## Installation

Install [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) and, to make optimizations available, install their backends: [openmp](https://www.archlinux.org/packages/?name=openmp), [upx](https://www.archlinux.org/packages/?name=upx), [optipng](https://www.archlinux.org/packages/?name=optipng), and [svgo](https://aur.archlinux.org/packages/svgo/).

### Configuration

[makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) generates a redundant [configuration file](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5), `/etc/makepkg-optimize.conf`, from your current [makepkg](/index.php/Makepkg "Makepkg") configuration.

This file lists supplementary [COMPILE FLAGS](/index.php/Makepkg#Building_optimized_binaries "Makepkg"), [BUILD ENVIRONMENT](https://aur.archlinux.org/cgit/aur.git/tree/buildenv_ext.conf?h=makepkg-optimize) options, [GLOBAL PACKAGE OPTIONS](https://aur.archlinux.org/cgit/aur.git/tree/pkgopts_ext.conf?h=makepkg-optimize), [PACKAGE OUTPUT](https://aur.archlinux.org/cgit/aur.git/tree/destdirs_ext.conf?h=makepkg-optimize) options, and [COMPRESSION DEFAULTS](https://aur.archlinux.org/cgit/aur.git/tree/compress-param_max.conf?h=makepkg-optimize), all of which are disabled by default.

**Warning:** Some packages may fail to build with certain optimizations and over-optimization may cause problems for some programs--such as decreased performance and segmentation faults.

## Build an optimized package

After [selecting your preferred optimizations](#Configuration), pass the configuration file when [building](/index.php/Makepkg#Usage "Makepkg"):

```
$ makepkg --config /etc/makepkg-optimize.conf

```

**Note:** [Profile-guided optimization](https://en.wikipedia.org/wiki/Profile-guided_optimization "wikipedia:Profile-guided optimization") requires that a package be built and installed *twice*. The first phase initiates profile generation in `$PROFDEST/*pkgbase*.gen`; the second moves them to `$PROFDEST/*pkgbase*.used` and applies them.

## Build an optimized package in a clean chroot

Alternatively, `makepkg-optimize` can be used to build optimized packages within a [chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Classic_way "DeveloperWiki:Building in a clean chroot").

### Chroot setup

After [setting up a chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Setting_up_a_chroot "DeveloperWiki:Building in a clean chroot"), a few additional steps are needed.

#### Install makepkg-optimize and backends

First, install some of the backends for the optimization macros to the base chroot:

```
$ arch-nspawn "$CHROOT"/root pacman -S openmp upx optipng

```

Then [download](/index.php/Arch_User_Repository#Acquire_build_files "Arch User Repository") and [build](/index.php/DeveloperWiki:Building_in_a_clean_chroot#Building_in_the_chroot "DeveloperWiki:Building in a clean chroot") [makepkg-optimize](https://aur.archlinux.org/packages/makepkg-optimize/) and [svgo](https://aur.archlinux.org/packages/svgo/).

To install them in the base chroot, copy their package files into it and install them, e.g.:

```
# cp svgo-1.2.2-2-any.pkg.tar.xz "$CHROOT"/root/root/
$ arch-nspawn "$CHROOT"/root pacman -U /root/svgo-1.2.2-2-any.pkg.tar.xz

```

**Warning:** This voids the warranty on your "clean" chroot!

#### Create a PGO cache

To use PGO, create a folder in the same place, inside and outside of the chroot, to store [profiles](https://gcc.gnu.org/onlinedocs/gcc/Gcov-Data-Files.html):

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

##### Building with PGO

After the first building phase, bind the [PGO cache](#Create_a_PGO_cache):

```
# mount -o bind {,"$CHROOT"/root}/mnt/pgo
# mount -o bind "$CHROOT"/{root,"$USER"}/mnt/pgo

```

**Tip:** Use [fstab](/index.php/Fstab "Fstab") to [bind](https://serverfault.com/a/613184) these folders at boot.

[Install](/index.php/Pacman#Additional_commands "Pacman") the package and test-run its executables.

**Note:** Profiles are generated on program `exit()`. Persistent daemons, such as [systemd](/index.php/Systemd "Systemd"), may require a reboot to produce profiles. If you have rebooted, be sure to rebind the PGO cache before rebuilding.

After thoroughly utilizing the software, [rebuild](#Build_a_package) and reinstall the package.