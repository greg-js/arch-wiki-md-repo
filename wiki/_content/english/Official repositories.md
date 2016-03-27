A [software repository](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository") is a storage location from which software packages are retrieved for installation.

Arch Linux **official repositories** contain essential and popular software, readily accessible via [pacman](/index.php/Pacman "Pacman"). They are maintained by [package maintainers](/index.php/Arch_terminology#Package_maintainer "Arch terminology").

Packages in the official repositories are constantly upgraded: when a package is upgraded, its old version is removed from the repository. There are no major Arch releases: each package is upgraded as new versions become available from upstream sources. Each repository is always coherent, i.e. the packages that it hosts always have reciprocally compatible versions.

## Contents

*   [1 Repositories](#Repositories)
    *   [1.1 core](#core)
    *   [1.2 extra](#extra)
    *   [1.3 community](#community)
    *   [1.4 multilib](#multilib)
        *   [1.4.1 gnome-unstable](#gnome-unstable)
    *   [1.5 testing](#testing)
        *   [1.5.1 community-testing](#community-testing)
        *   [1.5.2 multilib-testing](#multilib-testing)
        *   [1.5.3 Disabling testing repositories](#Disabling_testing_repositories)
*   [2 Historical background](#Historical_background)

## Repositories

### core

This repository can be found in `.../core/os/` on your favorite [mirror](/index.php/Mirror "Mirror").

core contains packages for:

*   booting Arch Linux
*   [connecting to the Internet](/index.php/Network_configuration "Network configuration")
*   [building packages](/index.php/Creating_packages "Creating packages")
*   management and repair of supported [file systems](/index.php/File_systems "File systems")
*   the system setup process (e.g. [openssh](https://www.archlinux.org/packages/?name=openssh))

as well as dependencies of the above (not necessarily makedepends)

*core* has fairly strict quality requirements. Developers/users need to signoff on updates before package updates are accepted. For packages with low usage, a reasonable exposure is enough: informing people about update, requesting signoffs, keeping in testing up to a week depending on the severity of the change, lack of outstanding bug reports, along with the implicit signoff of the package maintainer.

**Note:** To create a local repository with packages from *core* (or other repositories) without an internet connection see [Installing packages from a CD/DVD or USB stick](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips").

### extra

This repository can be found in `.../extra/os/` on your favorite mirror.

*extra* contains all packages that do not fit in *core*. Example: Xorg, window managers, web browsers, media players, tools for working with languages such as Python and Ruby, and a lot more.

### community

This repository can be found in `.../community/os/` on your favorite mirror.

*community* contains packages that have been adopted by [Trusted Users](/index.php/Trusted_Users "Trusted Users") from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Some of these packages may eventually make the transition to the [core](#core) or [extra](#extra) repositories as the developers consider them crucial to the distribution.

### multilib

This repository can be found in `.../multilib/os/` on your favorite mirror.

*multilib* contains 32 bit software and libraries that can be used to run and build 32 bit applications on 64 bit installs (e.g. [wine](https://www.archlinux.org/packages/?name=wine), [skype](https://www.archlinux.org/packages/?name=skype), etc).

For more information, see [Multilib](/index.php/Multilib "Multilib").

#### gnome-unstable

**Warning:** Be careful when enabling the *gnome-unstable* repository. Your system may break after performing an update. Only experienced users who know how to deal with potential system breakage should use it.

This repository contains the latest version of the [Gnome](/index.php/Gnome "Gnome") desktop environment. It can be enabled by adding the lines below to your `/etc/pacman.conf` file as top repository.

```
 [gnome-unstable]
 Include = /etc/pacman.d/mirrorlist

```

Please report packaging related bugs in our [bugtracker](https://bugs.archlinux.org/), while anything else should be reported upstream to [GNOME Bugzilla](https://bugzilla.gnome.org/).

Before opening new bug tickets, please check if the issue already has been reported and take a look at the [Testing Repo Forum](https://bbs.archlinux.org/viewforum.php?id=49) first.

### testing

**Warning:** Be careful when enabling the *testing* repository. Your system may break after performing an update. Only experienced users who know how to deal with potential system breakage should use it.

This repository can be found in `.../testing/os/` on your favorite mirror.

*testing* contains packages that are candidates for the *core* or *extra* repositories.

New packages go into *testing* if:

*   They are destined for the *core* repo. Everything in *core* must go through *testing*

*   They are expected to break something on update and need to be tested first.

*testing* is the only repository that can have name collisions with any of the other official repositories. If enabled, it has to be the first repository listed in your `/etc/pacman.conf` file.

**Note:** *testing* is not for the "newest of the new" package versions. Part of its purpose is to hold package updates that have the potential to break the system, either by being part of the *core* set of packages, or by being critical in other ways. As such, users of *testing* are strongly encouraged to subscribe to the [arch-dev-public mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public), watch the [testing repository forum](https://bbs.archlinux.org/viewforum.php?id=49), and to [report all bugs](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

If you enable *testing*, you must also enable *community-testing*.

#### community-testing

This repository is like the *testing* repository, but for packages that are candidates for the *community* repository.

If you enable it, you must also enable *testing*.

#### multilib-testing

This repository is like the *testing* repository, but for packages that are candidates for the *multilib* repository.

If you enable it, you must also enable *testing*.

#### Disabling testing repositories

If you enabled testing repositories, but later on decided to disable them, you should:

1.  Remove (comment out) them from `/etc/pacman.conf`
2.  Perform a `# pacman -Syyuu` to "rollback" your updates from these repositories.

The second item is optional, but keep it in mind if you notice any problems.

## Historical background

Most of the repository splits are for historical reasons. Originally, when Arch Linux was used by very few users, there was only one repository known as **official** (now *core*). At the time, *official* basically contained Judd Vinet's preferred applications. It was designed to contain one of each "type" of program -- one DE, one major browser, etc.

There were users back then that did not like Judd's selection, so since the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") is so easy to use, they created packages of their own. These packages went into a repository called **unofficial**, and were maintained by developers other than Judd. Eventually, the two repositories were both considered equally supported by the developers, so the names *official* and *unofficial* no longer reflected their true purpose. They were subsequently renamed to **current** and **extra** sometime near the release version 0.5.

Shortly after the 2007.8.1 release, *current* was renamed **core** in order to prevent confusion over what exactly it contains. The repositories are now more or less equal in the eyes of the developers and the community, but *core* does have some differences. The main distinction is that packages used for Installation CDs and release snapshots are taken only from *core*. This repository still gives a complete Linux system, though it may not be the Linux system you want.

Some time around 0.5/0.6, there were a lot of packages that the developers did not want to maintain. [Jason Chu](https://www.archlinux.org/fellows/#jason) set up the "Trusted User Repositories", which were unofficial repositories in which trusted users could place packages they had created. There was a **staging** repository where packages could be promoted into the official repositories by one of the Arch Linux developers, but other than this, the developers and trusted users were more or less distinct.

This worked for a while, but not when trusted users got bored with their repositories, and not when untrusted users wanted to share their own packages. This led to the development of the [AUR](https://aur.archlinux.org/). The TUs were conglomerated into a more closely knit group, and they now collectively maintain the **community** repository. The Trusted Users are still a separate group from the Arch Linux developers, and there is not a lot of communication between them. However, popular packages are still promoted from *community* to *extra* on occasion. The [AUR](https://aur.archlinux.org/) also allows untrusted users to submit PKGBUILDs.

After a kernel in *core* [broke many user systems](https://www.archlinux.org/news/please-avoid-kernel-261614-1/), the "core signoff policy" was introduced. Since then, all package updates for *core* need to go through a **testing** repository first, and only after multiple signoffs from other developers are they allowed to move. Over time, it was noticed that various *core* packages had low usage, and user signoffs or even lack of bug reports became informally accepted as criteria to accept such packages.

In late 2009/the beginning of 2010, with the advent of some new filesystems and the desire to support them during installation, along with the realization that *core* was never clearly defined (just "important packages, handpicked by developers"), the repository received a more accurate description.