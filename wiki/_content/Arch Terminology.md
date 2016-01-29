# Arch Terminology

This page is intended to be a page to demystify common terms used among the Arch Linux community. Feel free to add or modify any terms, but please use that particular section's edit option. If you decide to add one, please put it in alphabetical order.

## Contents

*   [1 Arch Linux](#Arch_Linux)
*   [2 ABS](#ABS)
*   [3 ARM](#ARM)
*   [4 AUR](#AUR)
*   [5 PKGBUILD](#PKGBUILD)
*   [6 TU, Trusted User](#TU.2C_Trusted_User)
*   [7 bbs](#bbs)
*   [8 community/[community]](#community.2F.5Bcommunity.5D)
*   [9 core/[core]](#core.2F.5Bcore.5D)
*   [10 custom/user repository](#custom.2Fuser_repository)
*   [11 Developer](#Developer)
*   [12 extra/[extra]](#extra.2F.5Bextra.5D)
*   [13 initramfs](#initramfs)
*   [14 initrd](#initrd)
*   [15 makepkg](#makepkg)
*   [16 namcap](#namcap)
*   [17 package](#package)
*   [18 Package maintainer](#Package_maintainer)
*   [19 pacman](#pacman)
*   [20 pacman.conf](#pacman.conf)
*   [21 repository/repo](#repository.2Frepo)
*   [22 RTFM](#RTFM)
*   [23 taurball](#taurball)
*   [24 testing/[testing]](#testing.2F.5Btesting.5D)
*   [25 udev](#udev)
*   [26 wiki](#wiki)

## Arch Linux

Arch should be referred to as:

*   **Arch Linux**
*   **Arch** (Linux implied)
*   **archlinux** (UNIX name)

Archlinux, ArchLinux, archLinux, aRcHlInUx, etc. are all weird, and weirder mutations.

Officially, the 'Arch' in "Arch Linux" is pronounced /ˈɑrtʃ/ as in an "archer"/bowman, or "arch-nemesis", and not as in "ark" or "archangel".

## ABS

The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") (ABS) is useful to:

*   Make new packages of software for which no packages are yet available
*   Customize/modify existing packages to fit your needs (enabling or disabling options)
*   Re-build your entire system using your compiler flags, "a la Gentoo"
*   Getting kernel modules working with your custom kernel

ABS is not necessary to use Arch Linux, but it is useful.

## ARM

The [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine") is a mirror that does not remove old versions of the packages and is thus very useful if you need to downgrade your system.

## AUR

The [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) is a community driven repository for Arch users. The AUR was initially conceived to organize the sharing of [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") amongst the wider community and to expedite the inclusion of popular user-contributed packages into the [core] and [extra] repositories via the AUR [community] repository.

The AUR is the birthplace of new Arch packages. Users contribute their own packages to the AUR. The AUR community votes for their favourite packages and eventually, once a package has garnered enough votes, an AUR Trusted User may take it to the [community] repository, which is accessible via [pacman](/index.php/Pacman "Pacman") and the [ABS](/index.php/ABS "ABS").

You can access the Arch Linux User Community Repository [here](https://aur.archlinux.org).

## PKGBUILD

[PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") are small scripts that are used to build Arch Linux packages. See [Creating packages](/index.php/Creating_packages "Creating packages") for more detail.

## TU, Trusted User

A [trusted user](/index.php/Trusted_user "Trusted user") is someone who maintains the AUR and the [community] repository. Trusted Users may move a package into the [community] repository if it has been voted as popular. TUs are appointed by a majority vote by the existing TUs.

Trusted users follow the [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") and [TU by-laws](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## bbs

**B**ulletin **b**oard **s**ystem, but in Arch's case, it is just the support forum located [here](https://bbs.archlinux.org).

## community/[community]

The [community] repository is where pre-built packages are made available by [Trusted Users](/index.php/Trusted_Users "Trusted Users"). A majority of the packages in [community] come from the [AUR](/index.php/AUR "AUR").

To access the [community] repository, uncomment it in `/etc/pacman.conf`.

## core/[core]

The [core] repository contains the bare packages needed for an Arch Linux system. [core] has everything needed to get a working command-line system.

## custom/user repository

Anyone can create a repository and put it online for other users. To create a repository, you need a set of packages and a [pacman](/index.php/Pacman "Pacman")-compatible database file for your packages. Host your files online and everyone will be able to use your repository by adding it as a regular repository.

See [Custom local repository](/index.php/Custom_local_repository "Custom local repository").

## Developer

Half-gods working to improve Arch for no financial gain. [Developers](https://www.archlinux.org/developers/) are outranked only by our gods, Judd Vinet and Aaron Griffin, who in turn are outranked by tacos.

## extra/[extra]

Arch's official package set is fairly streamlined, but we supplement this with a larger, more complete "extra" repository that contains a lot of the stuff that never made it into our core package set. This repository is constantly growing with the help of packages submitted from our strong community. This is where desktop environments, window managers and common programs are found.

## initramfs

See [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

## initrd

Obsolete. Nowadays often used as a synonym for initramfs.

## makepkg

[makepkg](/index.php/Makepkg "Makepkg") will build packages for you. makepkg will read the metadata required from a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") file. All it needs is a build-capable Linux platform, [wget](https://www.archlinux.org/packages/?name=wget), and some build scripts. The advantage to a script-based build is that you only really do the work once. Once you have the build script for a package, you just need to run makepkg and it will do the rest: download and validate source files, check dependencies, configure the build time settings, build the package, install the package into a temporary root, make customizations, generate meta-info, and package the whole thing up for [pacman](/index.php/Pacman "Pacman") to use.

## namcap

[namcap](/index.php/Namcap "Namcap") is a package analysis utility that looks for problems with Arch Linux packages or their [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") files. It can apply rules to the file list, the files themselves, or individual PKGBUILD files.

Rules return lists of messages. Each message can be one of three types: error, warning, or information (think of them as notes or comments). Errors (designated by 'E:') are things that namcap is very sure are wrong and need to be fixed. Warnings (designated by 'W:') are things that namcap thinks should be changed but if you know what you are doing then you can leave them. Information (designated 'I:') are only shown when you use the info argument. Information messages give information that might be helpful but is not anything that needs changing.

## package

A package is an archive containing

*   all of the (compiled) files of an application
*   metadata about the application, such as application name, version, dependencies, ...
*   installation files and directives for [pacman](/index.php/Pacman "Pacman")
*   (optionally) extra files to make your life easier, such as a start/stop script

Arch's package manager pacman can install, update, and remove those packages. Using packages instead of compiling and installing programs yourself has various benefits:

*   easily updatable: pacman will update existing packages as soon as updates are available
*   dependency checks: pacman handles dependencies for you, you only need to specify the program and pacman installs it together with every other program it needs
*   clean removal: pacman has a list of every file in a package. This way, no files are left behind when you decide to remove a package.

**Note:** Different GNU/Linux distributions use different packages and package managers, meaning that you cannot use pacman to install a Debian package on Arch.

## Package maintainer

The role of the package maintainer is to update packages as new versions become available upstream and to field support questions relating to bugs in said packages. The term may be applied to any of the following:

*   A core Arch Linux developer who maintains a software package in one of the official repositories (core, extra, or testing).
*   A [Trusted User](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") of the community who maintains software packages in the unsupported/unofficial community repository.
*   A normal user who maintains a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and local source files in the [AUR](/index.php/AUR "AUR").

The maintainer of a package is the person currently responsible for the package. Previous maintainers should be listed as contributors in the PKGBUILD along with others who have contributed to the package.

## pacman

The [pacman](/index.php/Pacman "Pacman") package manager is one of the great highlights of Arch Linux. It combines a simple binary package format with an easy-to-use build system (see [ABS](/index.php/ABS "ABS")). Pacman makes it possible to easily manage and customize packages, whether they be from the official Arch repositories or the user's own creations. The repository system allows users to build and maintain their own custom package repositories, which encourages community growth and contribution (see [AUR](/index.php/AUR "AUR")).

Pacman can keep a system up to date by synchronizing package lists with the master server, making it a breeze for the security-conscious system administrator to maintain. This server/client model also allows you to download/install packages with a simple command, complete with all required dependencies (similar to Debian's apt-get).

NB: Pacman was written by Judd Vinet, the creator of Arch Linux. It is used as a package management tool by other distributions as well, such as FrugalWare, Rubix, UfficioZero (in Italy, based on Ubuntu), and, of course, [Arch based distributions](/index.php/Arch_based_distributions_(active) "Arch based distributions (active)") such as Archie and AEGIS.

## pacman.conf

This is the configuration file of [pacman](/index.php/Pacman "Pacman"). It is located in `/etc`. For a full explanation of its powers, type this at the command line:

```
man pacman.conf

```

## repository/repo

The repository has the pre-compiled packages of one or (usually) more [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). Official repositories are

*   [core]: containing the latest version of packages required for a full CLI system
*   [extra]: containing the latest version of packages not needed for a working system but are needed for an enjoyable system ;)
*   [community]: containing packages that came from [AUR](/index.php/AUR "AUR") and got enough user votes

Pacman uses these repositories to search for packages and install them. A repository can be local (i.e. on your own computer) or remote (i.e. the packages are downloaded before they are installed).

## [RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM")

"Read The Fucking (or Fine) Manual". This simple message is replied to a lot of new Linux/Arch users who ask about the functionality of a program when it is clearly defined in the program's manual.

It is often used when a user fails to make any attempt to find a solution to the problem themselves. If someone tells you this, they are not trying to offend you; they are just frustrated with your lack of effort.

The best thing to do if you are told to do this is to read the manual page.

*   To read the program manual page for a particular program, type this at the command line:

```
man PROGRAM-NAME

```

where PROGRAM-NAME is the name of the program you need more information about.

If you do not find the answer to your question in the program manual, there are more ways to find the answer. You can:

*   search the [wiki](/index.php/Special:Search "Special:Search")
*   search the [forum](https://bbs.archlinux.org)
*   search the [mailing lists](https://www.google.com/#hl=en&q=arch+site:archlinux.org%2Fpipermail%2F)
*   search the [web](https://www.google.com)

## taurball

The tarballed [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and local source files that are required by makepkg to create an installable binary package. The name is derived from the practice of uploading such tarballs to the [AUR](/index.php/AUR "AUR"), hence "tAURball".

## testing/[testing]

This is the repository where major packages/updates to packages are kept prior to release into the main repositories, so they can be bug tested and upgrade issues can be found. It is disabled by default but can be enabled in `/etc/pacman.conf`

## udev

[udev](/index.php/Udev "Udev") provides a dynamic device directory containing only the files for actually present devices. It creates or removes device node files in the `/dev` directory, or it renames network interfaces.

Usually udev runs as udevd(8) and receives uevents directly from the kernel if a device is added/removed to/from the system.

If udev receives a device event, it matches its configured rules against the available device attributes provided in sysfs to identify the device. Rules that match may provide additional device information or specify a device node name and multiple symlink names and instruct udev to run additional programs as part of the device event handling.

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[This!](/index.php/Main_page "Main page") A place to find documentation about Arch Linux. Anyone can add and modify the documentation.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_Terminology&oldid=387828](https://wiki.archlinux.org/index.php?title=Arch_Terminology&oldid=387828)"