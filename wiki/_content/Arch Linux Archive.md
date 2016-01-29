# Arch Linux Archive

Related articles

*   [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages")

The **Arch Linux Archive** (a.k.a **ALA**), formerly known as **Arch Linux Rollback Machine** (a.k.a **ARM**), stores _official repositories snapshots_, _iso images_ and _bootstrap tarballs_ across time.

**You can use it to**

*   Downgrade to a previous version of one package (last version is broken, I want the previous one)
*   Restore all your packages at a precise moment (my system is broken, I want to go back 2 months ago)
*   Find a previous version of an ISO image

## Contents

*   [1 Location](#Location)
*   [2 Directories](#Directories)
    *   [2.1 /repos](#.2Frepos)
    *   [2.2 /packages](#.2Fpackages)
    *   [2.3 /iso](#.2Fiso)
*   [3 agetpkg](#agetpkg)
    *   [3.1 Download a previous version of ferm package](#Download_a_previous_version_of_ferm_package)
    *   [3.2 Download xterm version 296](#Download_xterm_version_296)
    *   [3.3 List all zsh versions](#List_all_zsh_versions)
    *   [3.4 Install all gvfs packages in version 1.26.0 release 3](#Install_all_gvfs_packages_in_version_1.26.0_release_3)
    *   [3.5 Download all pwgen packages](#Download_all_pwgen_packages)
*   [4 FAQ](#FAQ)
    *   [4.1 How to downgrade one package](#How_to_downgrade_one_package)
    *   [4.2 How to restore all my packages at a specific date](#How_to_restore_all_my_packages_at_a_specific_date)
*   [5 Sources](#Sources)
*   [6 Future plan](#Future_plan)
*   [7 History](#History)

## Location

The Arch Linux Archive is currently available at [https://archive.archlinux.org/](https://archive.archlinux.org/) (former [http://ala.seblu.net/](http://ala.seblu.net/)).

Previous locations listed below are deprecated and will be closed soon:

*   [http://seblu.net/a/archive](http://seblu.net/a/archive)
*   [ftp://seblu.net/archlinux/archive](ftp://seblu.net/archlinux/archive)

The following locations listed below are now closed:

*   [http://seblu.net/a/arm](http://seblu.net/a/arm)
*   [ftp://seblu.net/archlinux/arm](ftp://seblu.net/archlinux/arm)

## Directories

The **Archive** is split into 3 main directories detailed below.

```
├── iso
├── packages
└── repos

```

### /repos

The [repos](http://ala.seblu.net/repos) directory contains daily snapshots of official mirror organized by date like in the following example.

```
repos
├── 2013
│   ├── 08
│   │   └── 31
│   │       ├── community
│   │       ├── community-staging
│   │       ├── community-testing
│   │       ├── core
│   │       ├── extra
│   │       ├── gnome-unstable
│   │       ├── kde-unstable
│   │       ├── lastsync
│   │       ├── multilib
│   │       ├── multilib-staging
│   │       ├── multilib-testing
│   │       ├── pool
│   │       ├── staging
│   │       └── testing
│   ├── 09
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │   ├── 21
│   │   └── 22
│   ├── 10
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 11
│   └── 12
├── 2014
│   ├── 01
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 02
│   ├── 03
│   ├── ...
│   └── 09
│       ├── 01
│       ├── ...
│       └── 28
├── last
├── month
└── week

```

Note: The last 3 special directories (**last**, **week** and **month**) which links respectively to the last synced repository, to the last monday and to the first of the current month.

### /packages

The [packages](http://ala.seblu.net/packages) directory contains all versions of each package with their signatures. One directory by package and package directories are grouped by their first letter.

```
├── packages
│   ├── a
│   │   ├── awesome
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz.sig
│   │   │   ├── ...
│   │   │ 
│   │   ├── ...
│   │   ├── awstats
│   │   └── axel
│   │   
│   ├── b
│   ├── ...
│   └── z

```

You can use the magic subdirectory [.all](http://ala.seblu.net/packages/.all) to access all packages by their name. In a nutshell, all versions of each package in one flat directory. No clear-text listing allowed here.

```
├── packages
│   ├── .all
│   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   ├── ...
│   │   ├── zsh-5.0.2-3-i686.pkg.tar.xz
│   │   ├── zsh-5.0.2-4-i686.pkg.tar.xz
│   │   └── ...

```

An lightweight index, named [index.0.xz](http://ala.seblu.net/packages/.all/index.0.xz) is available to list all package in once.

### /iso

The [iso](http://ala.seblu.net/iso) directory contains official ISO images and bootstrap tarballs sorted by release date.

```
├── 2014.09.03
├── 2014.10.01
├── 2014.11.01
├── 2014.12.01
├── 2015.07.01
├── 2015.08.01
├── 2015.09.01
└── 2015.10.01
    ├── arch
    ├── archlinux-2015.10.01-dual.iso
    ├── archlinux-2015.10.01-dual.iso.sig
    ├── archlinux-2015.10.01-dual.iso.torrent
    ├── archlinux-bootstrap-2015.10.01-i686.tar.gz
    ├── archlinux-bootstrap-2015.10.01-i686.tar.gz.sig
    ├── archlinux-bootstrap-2015.10.01-x86_64.tar.gz
    ├── archlinux-bootstrap-2015.10.01-x86_64.tar.gz.sig
    ├── md5sums.txt
    └── sha1sums.txt

```

## agetpkg

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

**This article or section is a candidate for moving to [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages").**

**Notes:** (Discuss in [Talk:Archive#agetpkg](https://wiki.archlinux.org/index.php/Talk:Archive#agetpkg))

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** As of October 2015, the fate of the package is discussed in [arch-dev-public](https://lists.archlinux.org/pipermail/arch-dev-public/2015-October/027480.html). (Discuss in [Talk:Arch Linux Archive#](https://wiki.archlinux.org/index.php/Talk:Arch_Linux_Archive))

[agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/)<sup><small>AUR</small></sup> is a command line tool used to quickly list/get/install packages stored in the Archive.

##### Download a previous version of ferm package

```
agetpkg ferm

```

##### Download xterm version 296

```
agetpkg ^xterm 296

```

##### List all zsh versions

```
agetpkg -l zsh$

```

##### Install all gvfs packages in version 1.26.0 release 3

```
agetpkg -i gvfs 1.26.0 3

```

##### Download all pwgen packages

```
agetpkg -g -a pwgen

```

## FAQ

### How to downgrade one package

You can use [#agetpkg](#agetpkg) to easily download a specific package version from the Archive.

Or you can do it manually:

1.  Run your favorite internet browser and go to [https://archive.archlinux.org/packages](https://archive.archlinux.org/packages);
2.  Go to the package you need and download it;
3.  Run `pacman -U _pkgname_.pkg.tar.xz` as root.

### How to restore all my packages at a specific date

To restore all the package you have at a specific date, let says 30th March 2014, you have to stuck [pacman](/index.php/Pacman "Pacman") at this date, by editing your `/etc/pacman.conf` and use the following server directive:

```
[core]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[extra]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[community]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

or by replace your `/etc/pacman.d/mirrorlist` by the following content:

```
##                                                                              
## Arch Linux repository mirrorlist                                             
## Generated on 2042-01-01                                                      
##
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

Then update the database and force downgrade:

```
# pacman -Syyuu

```

**Note:** It's not safe to mix Archive and up-to-date mirrors. In case of download failure, you can fall-back on an upstream package and you will have packages not from the same epoch as the rest of the system.

## Sources

*   [archivetools](https://github.com/seblu/archivetools) -- Software to run an Archive server
*   [agetpkg](https://github.com/seblu/agetpkg) -- Software to easy downgrade package from the Archive

## Future plan

*   Move to official infrastructure.
*   Automatic clean-up after a defined amount of time?
*   Archive more stuff?

## History

*   The original ARM (_Archlinux Rollback Machine_) was closed on 2013-08-18.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)
*   The new one is hosted on [seblu.net](http://seblu.net) since 2013-08-31.
*   New URL and closing the old ARM hierarchy on 2015-10-13\. A new software, agetpkg was introduced.
*   Moved to [archive.archlinux.org](https://archive.archlinux.org) on 2015-12-19.[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2015-December/027635.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_Linux_Archive&oldid=416307](https://wiki.archlinux.org/index.php?title=Arch_Linux_Archive&oldid=416307)"