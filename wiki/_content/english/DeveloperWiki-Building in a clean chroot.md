## Contents

*   [1 Introduction](#Introduction)
*   [2 Why](#Why)
*   [3 Convenience way](#Convenience_way)
*   [4 Classic way](#Classic_way)
    *   [4.1 Setting up a chroot](#Setting_up_a_chroot)
        *   [4.1.1 Custom pacman.conf](#Custom_pacman.conf)
    *   [4.2 Building in the chroot](#Building_in_the_chroot)
        *   [4.2.1 Pre-install required packages](#Pre-install_required_packages)
        *   [4.2.2 Passing arguments to makepkg](#Passing_arguments_to_makepkg)
*   [5 Handling major rebuilds](#Handling_major_rebuilds)

## Introduction

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

## Why

Building in a clean chroot prevents missing dependencies in packages, whether due to unwanted linking or packages missing in the depends array in the PKGBUILD. It also allows users to build a package for the stable repositories (core, extra, community) while having packages from [testing] installed.

## Convenience way

To quickly build a package in a clean chroot without any further tinkering, one can use the helper scripts from the [devtools](https://www.archlinux.org/packages/?name=devtools) package.

These helper scripts should be called in the same directory where the PKGBUILD is, just like with makepkg. For instance, `extra-x86_64-build` automatically sets up a chroot from a clean chroot matrix in `/var/lib/archbuild`, updates it, and builds a package for the extra repository. For multilib builds there is just `multilib-build` without an architecture. Consult the table below for information on which script to use when building for a specific repository and architecture.

The `-c` parameter resets the chroot matrix, which can be useful in case of breakage. It is not needed for building in a clean chroot.

**Note:** [core] is omitted because those packages are required to go through [testing] first before landing in [core].

**Note:** If the objective is to build a [core] package for your own local usage, it may be desirable to use the stable repositories instead of the testing. In this case you may simply use the extra build scripts.

| Target repository | Architecture | Build script to use | Pacman configuration file used |
| extra / community | x86_64 | extra-x86_64-build | /usr/share/devtools/pacman-extra.conf |
| testing / community-testing | x86_64 | testing-x86_64-build | /usr/share/devtools/pacman-testing.conf |
| staging / community-staging | x86_64 | staging-x86_64-build | /usr/share/devtools/pacman-staging.conf |
| multilib | x86_64 | multilib-build | /usr/share/devtools/pacman-multilib.conf |
| multilib-testing | x86_64 | multilib-testing-build | /usr/share/devtools/pacman-multilib-testing.conf |
| multilib-staging | x86_64 | multilib-staging-build | /usr/share/devtools/pacman-multilib-staging.conf |

## Classic way

### Setting up a chroot

The [devtools](https://www.archlinux.org/packages/?name=devtools) package provides tools for creating and building within clean chroots. Install it if not done already.

To make a clean chroot, create a directory in which the chroot will reside. For example, `$HOME/chroot`.

```
$ mkdir ~/chroot

```

Define the `CHROOT` variable:

```
$ CHROOT=$HOME/chroot

```

Now create the chroot (the sub directory `root` is required because the `$CHROOT` directory will get other sub directories for clean working copies):

```
$ mkarchroot $CHROOT/root base-devel

```

**Note:** One can also define the `CHROOT` variable in `$HOME/.bashrc` using the export command if the location is to be repeatedly used.

**Note:** On [btrfs](/index.php/Btrfs "Btrfs") disks, the chroot is created as a subvolume, so you have to remove it by removing the subvolume with `# btrfs subvolume delete $CHROOT/root`.

Edit `~/.makepkg.conf` to set the packager name and any makeflags. Also adjust the [mirrorlist](/index.php/Pacman#Repositories_and_mirrors "Pacman") in `$CHROOT/root/etc/pacman.d/mirrorlist` and enable the [testing](/index.php/Testing "Testing") repository in `$CHROOT/root/etc/pacman.conf`, if desired.

**Note:** The `~` and `$HOME` variable are resolved to `/root/` by the *makechrootpkg* script (described below).

#### Custom pacman.conf

Alternatively, provide a custom `pacman.conf` and `makepkg.conf` with the following:

```
$ mkarchroot -C <pacman.conf> -M <makepkg.conf> $CHROOT/root base-devel

```

**Warning:** Using a custom `pacman.conf` or `makepkg.conf` during the initial creation of clean chroot can result in unintended custom adjustments to the chroot environment. *Use with caution.*

### Building in the chroot

Firstly, make sure the base chroot (`$CHROOT/root`) is up to date:

```
$ arch-nspawn $CHROOT/root pacman -Syu

```

Then, build a package by calling `makechrootpkg` in the directory containing its [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"):

```
$ makechrootpkg -c -r $CHROOT

```

**Note:** Passing the `-c` flag to `makechrootpkg` ensures that the working chroot (`$CHROOT/$USER`) is cleaned before building.

#### Pre-install required packages

To build a package with dependencies unavailable from the repositories enabled in `$CHROOT/root/pacman.conf`, pre-install them to the working chroot with `-I <package>`:

```
$ makechrootpkg -c -r $CHROOT -I build-dependency-1.0-1-x86_64.pkg.tar.xz -I required-package-2.0-2-x86_64.pkg.tar.xz

```

#### Passing arguments to makepkg

To pass arguments to [makepkg](/index.php/Makepkg#Usage "Makepkg"), list them after an [end-of-options marker](http://wiki.bash-hackers.org/dict/terms/end_of_options); e.g., to force a check():

```
$ makechrootpkg -c -r $CHROOT -- --check

```

## Handling major rebuilds

The cleanest way to handle a major rebuild is to use the [staging] repositories. Build the first package against [extra] and push it to [staging]. Then rebuild all following packages against [staging] and push them there.

If you can't use [staging], you can build against custom packages using a command like this:

```
# extra-x86_64-build -- -I ~/packages/foobar/foobar-2-1-any.pkg.tar.xz

```

You can specify more than one package to be installed using multiple -I arguments.

A simpler, but dirtier way to handle a major rebuild is to install all built packages in the chroot, never cleaning it. Build the first package using:

```
# extra-x86_64-build

```

And build all following packages using:

```
# makechrootpkg -n -r /var/lib/archbuild/extra-x86_64

```

Running namcap (the -n argument) implies installing the package in the chroot. *-build also does this by default.