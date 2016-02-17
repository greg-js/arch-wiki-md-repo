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
*   [3 FAQ](#FAQ)
    *   [3.1 How to downgrade one package](#How_to_downgrade_one_package)
    *   [3.2 How to restore all my packages at a specific date](#How_to_restore_all_my_packages_at_a_specific_date)
*   [4 History](#History)

## Location

The Arch Linux Archive is currently available at [https://archive.archlinux.org/](https://archive.archlinux.org/) (former [http://ala.seblu.net/](http://ala.seblu.net/)).

Previous locations listed below are deprecated and will be closed soon:

*   [http://seblu.net/a/archive](http://seblu.net/a/archive)
*   [ftp://seblu.net/archlinux/archive](ftp://seblu.net/archlinux/archive)

The following locations listed below are now closed:

*   [http://seblu.net/a/arm](http://seblu.net/a/arm)
*   [ftp://seblu.net/archlinux/arm](ftp://seblu.net/archlinux/arm)

The [source code](https://github.com/seblu/archivetools) is also available for setting up your own mirror.

## Directories

The **Archive** is split into 3 main directories detailed below.

```
├── iso
├── packages
└── repos

```

### /repos

The [repos](https://archive.archlinux.org/repos) directory contains daily snapshots of official mirror organized by date like in the following example.

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

The [packages](https://archive.archlinux.org/packages) directory contains all versions of each package with their signatures. One directory by package and package directories are grouped by their first letter.

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

You can use the magic subdirectory [.all](https://archive.archlinux.org/packages/.all) to access all packages by their name. It acts as a flat directory containing all versions of every package.

```
├── packages
│   ├── .all
│   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   ├── ...
│   │   ├── zsh-5.0.2-3-i686.pkg.tar.xz
│   │   ├── zsh-5.0.2-4-i686.pkg.tar.xz
│   │   └── ...

```

You can download the full package list (there are over a hundred thousand packages) as a compressed index: [index.0.xz](https://archive.archlinux.org/packages/.all/index.0.xz).

 `$ curl https://archive.archlinux.org/packages/.all/index.0.xz | unxz` 

```
0ad-a14-1-i686
0ad-a14-1-x86_64
0ad-a14-2-i686
...
zziplib-0.13.62-1-x86_64
zziplib-0.13.62-2-i686
zziplib-0.13.62-2-x86_64
```

### /iso

The [iso](https://archive.archlinux.org/iso) directory contains official ISO images and bootstrap tarballs sorted by release date.

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

## FAQ

### How to downgrade one package

Find the package you want under [/packages](#.2Fpackages). Download it and install it using `pacman -U`.

See also [Downgrading packages#Automation](/index.php/Downgrading_packages#Automation "Downgrading packages") for tools that simplify the process.

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

**Note:** It's [not safe](/index.php/Partial_upgrades "Partial upgrades") to mix Archive and up-to-date mirrors. In case of download failure, you can fall-back on an upstream package and you will have packages not from the same epoch as the rest of the system.

## History

*   The original ARM (_Archlinux Rollback Machine_) was closed on 2013-08-18.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)
*   The new one is hosted on [seblu.net](http://seblu.net) since 2013-08-31.
*   New URL and closing the old ARM hierarchy on 2015-10-13\. A new software, agetpkg was introduced.
*   Moved to [archive.archlinux.org](https://archive.archlinux.org) on 2015-12-19.[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2015-December/027635.html)