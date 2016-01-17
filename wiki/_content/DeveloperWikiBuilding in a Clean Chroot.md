# DeveloperWiki:Building in a Clean Chroot

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Introduction](#Introduction)
*   [2 Why](#Why)
*   [3 Convenience Way](#Convenience_Way)
*   [4 Classic Way](#Classic_Way)
    *   [4.1 Setting Up A Chroot](#Setting_Up_A_Chroot)
        *   [4.1.1 Custom pacman.conf](#Custom_pacman.conf)
    *   [4.2 Building in the Chroot](#Building_in_the_Chroot)
    *   [4.3 Manual package installation](#Manual_package_installation)
    *   [4.4 Installation after building](#Installation_after_building)
*   [5 Handling Major Rebuilds](#Handling_Major_Rebuilds)

## Introduction

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

## Why

Building in a clean chroot prevents missing dependencies in packages, whether due to unwanted linking or packages missing in the depends array in the PKGBUILD. It also allows users to build a package for the stable repositories (core, extra, community) while having packages from [testing] installed.

## Convenience Way

To quickly build a package in a clean chroot without any further tinkering, one can use the helper scripts from the [devtools](https://www.archlinux.org/packages/?name=devtools) package.

These helper scripts should be called in the same directory where the PKGBUILD is, just like with makepkg. For instance, `extra-i686-build` automatically sets up a chroot from a clean chroot matrix in `/var/lib/archbuild`, updates it, and builds a package for the extra repository. For multilib builds there is just `multilib-build` without an architecture. Consult the table below for information on which script to use when building for a specific repository and architecture.

The `-c` parameter resets the chroot matrix, which can be useful in case of breakage. It is not needed for building in a clean chroot.

**Note:** [core] is omitted because those packages are required to go through [testing] first before landing in [core].

**Note:** If the objective is to build a [core] package for your own local usage, it may be desirable to use the stable repositories instead of the testing. In this case you may simply use the extra build scripts.

<table class="wikitable">

<tbody>

<tr>

<th>Target repository</th>

<th>Architecture</th>

<th>Build script to use</th>

<th>Pacman configuration file used</th>

</tr>

<tr>

<td>extra / community</td>

<td>i686</td>

<td>extra-i686-build</td>

<td>/usr/share/devtools/pacman-extra.conf</td>

</tr>

<tr>

<td>extra / community</td>

<td>x86_64</td>

<td>extra-x86_64-build</td>

<td>/usr/share/devtools/pacman-extra.conf</td>

</tr>

<tr>

<td>testing / community-testing</td>

<td>i686</td>

<td>testing-i686-build</td>

<td>/usr/share/devtools/pacman-testing.conf</td>

</tr>

<tr>

<td>testing / community-testing</td>

<td>x86_64</td>

<td>testing-x86_64-build</td>

<td>/usr/share/devtools/pacman-testing.conf</td>

</tr>

<tr>

<td>staging / community-staging</td>

<td>i686</td>

<td>staging-i686-build</td>

<td>/usr/share/devtools/pacman-staging.conf</td>

</tr>

<tr>

<td>staging / community-staging</td>

<td>x86_64</td>

<td>staging-x86_64-build</td>

<td>/usr/share/devtools/pacman-staging.conf</td>

</tr>

<tr>

<td>multilib</td>

<td>x86_64</td>

<td>multilib-build</td>

<td>/usr/share/devtools/pacman-multilib.conf</td>

</tr>

<tr>

<td>multilib-testing</td>

<td>x86_64</td>

<td>multilib-testing-build</td>

<td>/usr/share/devtools/pacman-multilib-testing.conf</td>

</tr>

<tr>

<td>multilib-staging</td>

<td>x86_64</td>

<td>multilib-staging-build</td>

<td>/usr/share/devtools/pacman-multilib-staging.conf</td>

</tr>

</tbody>

</table>

## Classic Way

### Setting Up A Chroot

The devtools package provides tools for creating and building within clean chroots. Install it if not done already:

```
# pacman -S devtools

```

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
# mkarchroot $CHROOT/root base-devel

```

**Note:** One can also define the `CHROOT` variable in `$HOME/.bashrc` using the export command if the location is to be repeatedly used.

**Note:** On [btrfs](/index.php/Btrfs "Btrfs") disks, the chroot is created as a subvolume, so you have to remove it by removing the subvolume with `# btrfs subvolume delete $CHROOT/root`.

Edit `~/.makepkg.conf` to set the packager name and any makeflags. Also adjust the [mirrorlist](/index.php/Pacman#Repositories "Pacman") in `$CHROOT/root/etc/pacman.d/mirrorlist` and enable the [testing](/index.php/Testing "Testing") repository in `$CHROOT/root/etc/pacman.conf`, if desired.

#### Custom pacman.conf

Alternatively, provide a custom `pacman.conf` and `makepkg.conf` with the following:

```
# mkarchroot -C <pacman.conf> -M <makepkg.conf> $CHROOT/root base-devel

```

**Warning:** Using a custom `pacman.conf` or `makepkg.conf` during the initial creation of clean chroot can result in unintended custom adjustments to the chroot environment. _Use with caution._

### Building in the Chroot

Firstly, make sure the chroot is up to date with:

```
# arch-nspawn $CHROOT/root pacman -Syu

```

Then, to build a package in the chroot, run the following from the dir containing the PKGBUILD:

```
$ makechrootpkg -c -r $CHROOT

```

Passing the -c flag to makechrootpkg ensures that the working chroot (named `$CHROOT/$USERNAME`) is cleaned before building starts.

### Manual package installation

Packages can be installed manually to the working chroot by using:

```
# makechrootpkg -r $CHROOT -I package-1.0-1-i686.pkg.tar.xz

```

If done from a directory that contains a PKGBUILD, the package will then be built. Avoid being in such a directory if you want to just install the package.

### Installation after building

Tell makechrootpkg to simply install a package to the rw layer of the chroot after building by passing the -i arg. Unrecognized args get passed to makepkg, so this calls `makepkg` with the -i arg.

```
# makechrootpkg -r $CHROOT -- -i

```

## Handling Major Rebuilds

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=DeveloperWiki:Building_in_a_Clean_Chroot&oldid=415572](https://wiki.archlinux.org/index.php?title=DeveloperWiki:Building_in_a_Clean_Chroot&oldid=415572)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [DeveloperWiki](/index.php/Category:DeveloperWiki "Category:DeveloperWiki")