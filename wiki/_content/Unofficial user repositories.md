# Unofficial user repositories

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Please fill in the missing information about repository maintainers. (Discuss in [Talk:Unofficial user repositories#](https://wiki.archlinux.org/index.php/Talk:Unofficial_user_repositories))

Related articles

*   [pacman-key](/index.php/Pacman-key "Pacman-key")
*   [Official repositories](/index.php/Official_repositories "Official repositories")

This article lists binary repositories freely created and shared by the community, often providing pre-built versions of PKGBUILDS found in the [AUR](/index.php/AUR "AUR").

**Warning:** Neither the official Arch Linux Developers nor the Trusted Users perform tests of any sort to verify the contents of these repositories; it is up to each user to decide whether to trust their maintainers, and take full responsibility for whatever their decision brings.

In order to use these repositories, you will have to add them to `/etc/pacman.conf`, as explained in [pacman#Repositories](/index.php/Pacman#Repositories "Pacman"). If a repository is signed, you will have to obtain and locally sign the associated key, as explained in [Pacman-key#Adding unofficial keys](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key").

If you want to create your own custom repository, follow [pacman tips#Custom local repository](/index.php/Pacman_tips#Custom_local_repository "Pacman tips").

**Tip:** To get a list of all servers listed in this page: `curl 'https://wiki.archlinux.org/index.php/Unofficial_user_repositories' | grep 'Server = ' | sed "s/\$arch/$(uname -m)/g" | cut -f 3 -d' '` 

For your convenience you can, for example, open them all in a web browser to inspect the contents of their repositories.

## Contents

*   [1 Adding your repository to this page](#Adding_your_repository_to_this_page)
*   [2 Any](#Any)
    *   [2.1 Signed](#Signed)
        *   [2.1.1 bioinformatics-any](#bioinformatics-any)
        *   [2.1.2 infinality-bundle-fonts](#infinality-bundle-fonts)
        *   [2.1.3 ivasilev](#ivasilev)
        *   [2.1.4 pkgbuilder](#pkgbuilder)
        *   [2.1.5 xyne-any](#xyne-any)
    *   [2.2 Unsigned](#Unsigned)
        *   [2.2.1 archlinuxgr-any](#archlinuxgr-any)
*   [3 Both i686 and x86_64](#Both_i686_and_x86_64)
    *   [3.1 Signed](#Signed_2)
        *   [3.1.1 arcanisrepo](#arcanisrepo)
        *   [3.1.2 archlinuxcn](#archlinuxcn)
        *   [3.1.3 bbqlinux](#bbqlinux)
        *   [3.1.4 catalyst](#catalyst)
        *   [3.1.5 catalyst-hd234k](#catalyst-hd234k)
        *   [3.1.6 city](#city)
        *   [3.1.7 demz-repo-archiso](#demz-repo-archiso)
        *   [3.1.8 demz-repo-core](#demz-repo-core)
        *   [3.1.9 gnome-encfs-manager](#gnome-encfs-manager)
        *   [3.1.10 haskell-core](#haskell-core)
        *   [3.1.11 infinality-bundle](#infinality-bundle)
        *   [3.1.12 ivasilev](#ivasilev_2)
        *   [3.1.13 llvm-svn](#llvm-svn)
        *   [3.1.14 metalgamer](#metalgamer)
        *   [3.1.15 miffe](#miffe)
        *   [3.1.16 nullptr_t](#nullptr_t)
        *   [3.1.17 pipelight](#pipelight)
        *   [3.1.18 repo-ck](#repo-ck)
        *   [3.1.19 seblu](#seblu)
        *   [3.1.20 sergej-repo](#sergej-repo)
        *   [3.1.21 tredaelli-systemd](#tredaelli-systemd)
        *   [3.1.22 herecura](#herecura)
        *   [3.1.23 blackeagle-pre-community](#blackeagle-pre-community)
    *   [3.2 Unsigned](#Unsigned_2)
        *   [3.2.1 arch-deepin](#arch-deepin)
        *   [3.2.2 archaudio](#archaudio)
        *   [3.2.3 archlinuxfr](#archlinuxfr)
        *   [3.2.4 archlinuxgis](#archlinuxgis)
        *   [3.2.5 archlinuxgr](#archlinuxgr)
        *   [3.2.6 archlinuxgr-kde4](#archlinuxgr-kde4)
        *   [3.2.7 arsch](#arsch)
        *   [3.2.8 cinnamon](#cinnamon)
        *   [3.2.9 ede](#ede)
        *   [3.2.10 heftig](#heftig)
        *   [3.2.11 mesa-git](#mesa-git)
        *   [3.2.12 noware](#noware)
        *   [3.2.13 openrc-eudev](#openrc-eudev)
        *   [3.2.14 oracle](#oracle)
        *   [3.2.15 pantheon](#pantheon)
        *   [3.2.16 paulburton-fitbitd](#paulburton-fitbitd)
        *   [3.2.17 pietma](#pietma)
        *   [3.2.18 pfkernel](#pfkernel)
        *   [3.2.19 suckless](#suckless)
        *   [3.2.20 Unity-for-Arch](#Unity-for-Arch)
        *   [3.2.21 Unity-for-Arch-Extra](#Unity-for-Arch-Extra)
        *   [3.2.22 home_tarakbumba_archlinux_Arch_Extra_standard](#home_tarakbumba_archlinux_Arch_Extra_standard)
        *   [3.2.23 MEGAsync_Arch_Extra](#MEGAsync_Arch_Extra)
*   [4 i686 only](#i686_only)
    *   [4.1 Signed](#Signed_3)
        *   [4.1.1 eee-ck](#eee-ck)
        *   [4.1.2 phillid](#phillid)
        *   [4.1.3 xyne-i686](#xyne-i686)
    *   [4.2 Unsigned](#Unsigned_3)
        *   [4.2.1 andrwe](#andrwe)
        *   [4.2.2 kpiche](#kpiche)
        *   [4.2.3 kernel26-pae](#kernel26-pae)
        *   [4.2.4 linux-pae](#linux-pae)
        *   [4.2.5 rfad](#rfad)
        *   [4.2.6 studioidefix](#studioidefix)
*   [5 x86_64 only](#x86_64_only)
    *   [5.1 Signed](#Signed_4)
        *   [5.1.1 apathism](#apathism)
        *   [5.1.2 ashleyis](#ashleyis)
        *   [5.1.3 atom](#atom)
        *   [5.1.4 bioinformatics](#bioinformatics)
        *   [5.1.5 blackleg](#blackleg)
        *   [5.1.6 boyska64](#boyska64)
        *   [5.1.7 coderkun-aur](#coderkun-aur)
        *   [5.1.8 coderkun-aur-audio](#coderkun-aur-audio)
        *   [5.1.9 eatabrick](#eatabrick)
        *   [5.1.10 freifunk-rheinland](#freifunk-rheinland)
        *   [5.1.11 gustawho](#gustawho)
        *   [5.1.12 holo](#holo)
        *   [5.1.13 Linux-pf](#Linux-pf)
        *   [5.1.14 infinality-bundle-multilib](#infinality-bundle-multilib)
        *   [5.1.15 kc9ydn](#kc9ydn)
        *   [5.1.16 linux-lts-ck](#linux-lts-ck)
        *   [5.1.17 linux-lts31x](#linux-lts31x)
        *   [5.1.18 linux-lts31x-ck](#linux-lts31x-ck)
        *   [5.1.19 linux-ck-pax](#linux-ck-pax)
        *   [5.1.20 linux-tresor](#linux-tresor)
        *   [5.1.21 markzz](#markzz)
        *   [5.1.22 qt-debug](#qt-debug)
        *   [5.1.23 quarry](#quarry)
        *   [5.1.24 rstudio](#rstudio)
        *   [5.1.25 siosm-aur](#siosm-aur)
        *   [5.1.26 siosm-selinux](#siosm-selinux)
        *   [5.1.27 subtitlecomposer](#subtitlecomposer)
        *   [5.1.28 xyne-x86_64](#xyne-x86_64)
    *   [5.2 Unsigned](#Unsigned_4)
        *   [5.2.1 alucryd](#alucryd)
        *   [5.2.2 alucryd-multilib](#alucryd-multilib)
        *   [5.2.3 andrwe](#andrwe_2)
        *   [5.2.4 archstudio](#archstudio)
        *   [5.2.5 brtln](#brtln)
        *   [5.2.6 kps](#kps)
        *   [5.2.7 mazdlc](#mazdlc)
        *   [5.2.8 mazdlc-deadbeef-plugins](#mazdlc-deadbeef-plugins)
        *   [5.2.9 mazdlc-kde-frameworks-5](#mazdlc-kde-frameworks-5)
        *   [5.2.10 mikroskeem](#mikroskeem)
        *   [5.2.11 mingw-w64](#mingw-w64)
        *   [5.2.12 pnsft-pur](#pnsft-pur)
        *   [5.2.13 rakudo](#rakudo)
        *   [5.2.14 rightlink](#rightlink)
        *   [5.2.15 seiichiro](#seiichiro)
        *   [5.2.16 studioidefix](#studioidefix_2)
        *   [5.2.17 zrootfs](#zrootfs)
*   [6 armv6h only](#armv6h_only)
    *   [6.1 Unsigned](#Unsigned_5)
        *   [6.1.1 arch-fook-armv6h](#arch-fook-armv6h)
*   [7 armv7h only](#armv7h_only)
    *   [7.1 Unsigned](#Unsigned_6)
        *   [7.1.1 pietma](#pietma_2)

## Adding your repository to this page

If you have your own repository, please add it to this page, so that all the other users will know where to find your packages. Please keep the following rules when adding new repositories:

*   Keep the lists in alphabetical order.
*   Include some information about the maintainer: include at least a (nick)name and some form of contact information (web site, email address, user page on ArchWiki or the forums, etc.).
*   If the repository is of the _signed_ variety, please include a key-id, possibly using it as the anchor for a link to its keyserver; if the key is not on a keyserver, include a link to the key file.
*   Include some short description (e.g. the category of packages provided in the repository).
*   If there is a page (either on ArchWiki or external) containing more information about the repository, include a link to it.
*   If possible, avoid using comments in code blocks. The formatted description is much more readable. Users who want some comments in their `pacman.conf` can easily create it on their own.

## Any

"Any" repositories are architecture-independent. In other words, they can be used on both i686 and x86_64 systems.

### Signed

#### bioinformatics-any

*   **Maintainer:** [decryptedepsilon](https://aur.archlinux.org/account/decryptedepsilon/)
*   **Description:** A repository containing some python packages and genome browser for Bioinformatics
*   **Key-ID:** 60442BA4

```
[bioinformatics-any]
Server = http://decryptedepsilon.bl.ee/repo/any

```

#### infinality-bundle-fonts

*   **Maintainer:** [bohoomil](http://bohoomil.com/)
*   **Description:** infinality-bundle-fonts repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle-fonts]
Server = http://bohoomil.com/repo/fonts

```

#### ivasilev

*   **Maintainer:** [Ianis G. Vasilev](http://ivasilev.net)
*   **Description:** A variety of packages, mostly my own software and AUR builds.
*   **Upstream page:** [http://ivasilev.net/pacman](http://ivasilev.net/pacman)
*   **Key-ID:** 436BB513

**Note:** I mantain 'any', 'i686' and 'x86_64' repos. Each of them includes packages from 'any'. $arch can be replaced with any of the three

```
[ivasilev]
Server = http://ivasilev.net/pacman/any
# Server = http://ivasilev.net/pacman/$arch

```

#### pkgbuilder

*   **Maintainer:** [Chris Warrick](https://chriswarrick.com/)
*   **Description:** A repository for PKGBUILDer, a Python AUR helper.
*   **Upstream page:** [https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder)
*   **Key-ID:** 5EAAEA16

```
[pkgbuilder]
Server = https://pkgbuilder-repo.chriswarrick.com/

```

#### xyne-any

*   **Maintainer:** [Xyne](https://www.archlinux.org/trustedusers/#xyne)
*   **Description:** A repository for Xyne's own projects containing packages for "any" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not needed, as maintainer is a TU

**Note:** Use this repository only if there is no matching `[xyne-*]` repository for your architecture.

```
[xyne-any]
Server = http://xyne.archlinux.ca/repos/xyne

```

### Unsigned

#### archlinuxgr-any

*   **Maintainer:**
*   **Description:** The Hellenic (Greek) unofficial Arch Linux repository with many interesting packages.

```
[archlinuxgr-any]
Server = http://archlinuxgr.tiven.org/archlinux/any

```

## Both i686 and x86_64

Repositories with both i686 and x86_64 versions. The `$arch` variable will be set automatically by pacman.

### Signed

#### arcanisrepo

*   **Maintainer:** [arcanis](https://www.archlinux.org/trustedusers/#arcanis)
*   **Description:** A repository with some AUR packages including packages from VCS
*   **Key-ID:** Not needed, as maintainer is a TU

```
[arcanisrepo]
Server = ftp://repo.arcanis.name/repo/$arch

```

#### archlinuxcn

*   **Maintainers:** [Phoenix Nemo (phoenixlzx)](https://plus.google.com/+PhoenixNemo/), Felix Yan (felixonmars, TU), [lilydjwg](https://twitter.com/lilydjwg), and others
*   **Description:** Packages by the Chinese Arch Linux community (mostly signed)
*   **Git Repo:** [https://github.com/archlinuxcn/repo](https://github.com/archlinuxcn/repo)
*   **Mirrors:** [https://github.com/archlinuxcn/mirrorlist-repo](https://github.com/archlinuxcn/mirrorlist-repo)
*   **Key-ID:** Once the repo is added, _archlinuxcn-keyring_ package must be installed before any other.

```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://repo.archlinuxcn.org/$arch

```

#### bbqlinux

*   **Maintainer:** [Daniel Hillenbrand](https://plus.google.com/u/0/+DanielHillenbrand/about)
*   **Description:** Packages for Android Development
*   **Upstream Page:** [http://bbqlinux.org/](http://bbqlinux.org/)
*   **Key-ID:** Get the _bbqlinux-keyring_ package, as it contains the needed keys.

```
[bbqlinux]
Server = http://packages.bbqlinux.org/$repo/os/$arch

```

#### catalyst

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Upstream Page:** [http://catalyst.wirephire.com](http://catalyst.wirephire.com)
*   **Key-ID:** 653C3094

```
[catalyst]
Server = http://catalyst.wirephire.com/repo/catalyst/$arch
## Mirrors, if the primary server does not work or is too slow:
#Server = http://mirror.hactar.bz/Vi0L0/catalyst/$arch

```

#### catalyst-hd234k

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Upstream Page:** [http://catalyst.wirephire.com](http://catalyst.wirephire.com)
*   **Key-ID:** 653C3094

```
[catalyst-hd234k]
Server = http://catalyst.wirephire.com/repo/catalyst-hd234k/$arch
## Mirrors, if the primary server does not work or is too slow:
#Server = http://mirror.hactar.bz/Vi0L0/catalyst-hd234k/$arch

```

#### city

*   **Maintainer:** [Balló György](https://www.archlinux.org/trustedusers/#bgyorgy)
*   **Description:** Experimental/unpopular packages.
*   **Upstream page:** [http://pkgbuild.com/~bgyorgy/city.html](http://pkgbuild.com/~bgyorgy/city.html)
*   **Key-ID:** Not needed, as maintainer is a TU

```
[city]
Server = http://pkgbuild.com/~bgyorgy/$repo/os/$arch

```

#### demz-repo-archiso

*   **Maintainer:** [Jesus Alvarez (demizer)](http://demizerone.com)
*   **Description:** Packages for installing ZFS from an Arch ISO live disk
*   **Upstream page:** [https://github.com/demizer/archzfs](https://github.com/demizer/archzfs)
*   **Key-ID:** 5E1ABF240EE7A126

```
[demz-repo-archiso]
Server = http://demizerone.com/$repo/$arch

```

#### demz-repo-core

*   **Maintainer:** [Jesus Alvarez (demizer)](http://demizerone.com)
*   **Description:** Packages for ZFS on Arch Linux.
*   **Upstream page:** [https://github.com/demizer/archzfs](https://github.com/demizer/archzfs)
*   **Key-ID:** 5E1ABF240EE7A126

```
[demz-repo-core]
Server = http://demizerone.com/$repo/$arch

```

#### gnome-encfs-manager

*   **Maintainer:** Moritz Molch
*   **Description:** The gnome-encfs-manager can be used to integrate [EncFS](/index.php/EncFS "EncFS")
*   **Upstream page:** [Gnome EncfsM](https://launchpad.net/gencfsm).
*   **Key ID:**

```
[home_moritzmolch_gencfsm_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/moritzmolch:/gencfsm/Arch_Extra/$arch

```

#### haskell-core

*   **Maintainer:** Magnus Therning
*   **Description:** Arch-Haskell repository
*   **Upstream page:** [https://github.com/archhaskell/habs](https://github.com/archhaskell/habs)
*   **Key-ID:** 4209170B

```
[haskell-core]
Server = http://xsounds.org/~haskell/core/$arch

```

#### infinality-bundle

*   **Maintainer:** [bohoomil](http://bohoomil.com/)
*   **Description:** infinality-bundle main repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle]
Server = http://bohoomil.com/repo/$arch

```

#### ivasilev

*   **Maintainer:** [Ianis G. Vasilev](http://ivasilev.net)
*   **Description:** A variety of packages, mostly my own software and AUR builds.
*   **Upstream page:** [http://ivasilev.net/pacman](http://ivasilev.net/pacman)
*   **Key-ID:** 436BB513

**Note:** I mantain 'any', 'i686' and 'x86_64' repos. Each of them includes packages from 'any'. $arch can be replaced with any of the three

```
[ivasilev]
Server = http://ivasilev.net/pacman/$arch

```

#### llvm-svn

*   **Maintainer:** [Luchesar V. ILIEV (kerberizer)](/index.php/User:Kerberizer "User:Kerberizer")
*   **Description:** [llvm-svn](https://aur.archlinux.org/pkgbase/llvm-svn) and [lib32-llvm-svn](https://aur.archlinux.org/pkgbase/lib32-llvm-svn) from AUR: the LLVM compiler infrastructure, the Clang frontend, and the tools associated with it
*   **Key-ID:** [0x76563F75679E4525](https://sks-keyservers.net/pks/lookup?op=vindex&search=0x76563F75679E4525&fingerprint=on&exact=on), fingerprint <tt>D16C F22D 27D1 091A 841C 4BE9 7656 3F75 679E 4525</tt>

```
[llvm-svn]
Server = http://repos.uni-plovdiv.net/archlinux/$repo/$arch

```

#### metalgamer

*   **Maintainer:** [metalgamer](http://metalgamer.eu/)
*   **Description:** Packages I use and/or maintain on the AUR.
*   **Key ID:** F55313FB

```
[metalgamer]
Server = http://repo.metalgamer.eu/$arch

```

#### miffe

*   **Maintainer:** [miffe](https://bbs.archlinux.org/profile.php?id=4059)
*   **Description:** AUR packages maintained by miffe, e.g. linux-mainline
*   **Key ID:** 313F5ABD

```
[miffe]
Server = http://arch.miffe.org/$arch/

```

#### nullptr_t

*   **Maintainers:** Sebastian Lau (nullptr_t),
*   **Description:** AUR packages that have a longer build time on some machines (e.g. [veracrypt](https://aur.archlinux.org/packages/veracrypt/)<sup><small>AUR</small></sup> or [plymouth](/index.php/Plymouth "Plymouth"))
*   **Key-ID:** 1607AC45

```
[nullptr_t]
Server = https://www.slau.me/archlinux/mirrors/$repo/$arch

```

#### pipelight

*   **Maintainer:**
*   **Description:** Pipelight and wine-compholio
*   **Upstream page:** [fds-team.de](http://fds-team.de/)
*   **Key-ID:** E49CC0415DC2D5CA
*   **Keyfile:** [http://repos.fds-team.de/Release.key](http://repos.fds-team.de/Release.key)

```
[pipelight]
Server = http://repos.fds-team.de/stable/arch/$arch

```

#### repo-ck

*   **Maintainer:** [graysky](/index.php/User:Graysky "User:Graysky")
*   **Description:** Kernel and modules with Brain Fuck Scheduler and all the goodies in the ck1 patch set.
*   **Upstream page:** [repo-ck.com](http://repo-ck.com)
*   **Wiki:** [repo-ck](/index.php/Repo-ck "Repo-ck")
*   **Key-ID:** 5EE46C4C

```
[repo-ck]
Server = http://repo-ck.com/$arch

```

#### seblu

*   **Maintainer:** [Sébastien Luttringer](https://www.archlinux.org/developers/#seblu)
*   **Description:** All seblu useful pre-built packages, some homemade (virtualbox-ext-oracle, linux-seblu-meta, bedup).
*   **Key-ID:** Not required, as maintainer is a Developer

```
[seblu]
Server = http://seblu.net/a/$repo/$arch

```

#### sergej-repo

*   **Maintainer:** [Sergej Pupykin](https://www.archlinux.org/trustedusers/#spupykin)
*   **Description:** psi-plus, owncloud-git, ziproxy, android, MySQL, and other stuff. Some packages also available for armv7h.
*   **Key-ID:** Not required, as maintainer is a TU

```
[sergej-repo]
Server = http://repo.p5n.pp.ru/$repo/os/$arch

```

#### tredaelli-systemd

*   **Maintainer:** [Timothy Redaelli](https://www.archlinux.org/trustedusers/#tredaelli)
*   **Description:** systemd rebuilt with unofficial OpenVZ patch (kernel < 2.6.32-042stab111.1)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** `[tredaelli-systemd]` must be put before `[core]` in `/etc/pacman.conf`

```
[tredaelli-systemd]
Server = http://pkgbuild.com/~tredaelli/repo/systemd/$arch

```

#### herecura

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** additional packages not found in the _community_ repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[herecura]
Server = http://repo.herecura.be/$repo/$arch

```

#### blackeagle-pre-community

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** testing of the by me maintaned packages before moving to _community_ repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[blackeagle-pre-community]
Server = http://repo.herecura.be/$repo/$arch

```

### Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

#### arch-deepin

*   **Maintainer:** [metak](https://build.opensuse.org/project/show/home:metakcahura), [fasheng](https://github.com/fasheng)
*   **Description:** Porting software from Linux Deepin to Archlinux.
*   **Upstream page:** [https://github.com/fasheng/arch-deepin](https://github.com/fasheng/arch-deepin)

```
[home_metakcahura_arch-deepin_Arch_Extra]
SigLevel = Never
Server = http://download.opensuse.org/repositories/home:/metakcahura:/arch-deepin/Arch_Extra/$arch
#Server = http://anorien.csc.warwick.ac.uk/mirrors/download.opensuse.org/repositories/home:/metakcahura:/arch-deepin/Arch_Extra/$arch

```

#### archaudio

*   **Maintainer:** [Ray Rashif](/index.php/User:Schivmeister "User:Schivmeister"), [Joakim Hernberg](https://aur.archlinux.org/account/jhernberg)
*   **Description:** Pro-audio packages

```
[archaudio-production]
Server = http://repos.archaudio.org/$repo/$arch

```

#### archlinuxfr

*   **Maintainer:**
*   **Description:**
*   **Upstream page:** [http://afur.archlinux.fr](http://afur.archlinux.fr)

```
[archlinuxfr]
Server = http://repo.archlinux.fr/$arch

```

#### archlinuxgis

*   **Maintainer:**
*   **Description:** Maintainers needed - low bandwidth

```
[archlinuxgis]
Server = http://archlinuxgis.no-ip.org/$arch

```

#### archlinuxgr

*   **Maintainer:**
*   **Description:**

```
[archlinuxgr]
Server = http://archlinuxgr.tiven.org/archlinux/$arch

```

#### archlinuxgr-kde4

*   **Maintainer:**
*   **Description:** KDE4 packages (plasmoids, themes etc) provided by the Hellenic (Greek) Arch Linux community

```
[archlinuxgr-kde4]
Server = http://archlinuxgr.tiven.org/archlinux-kde4/$arch

```

#### arsch

*   **Maintainer:**
*   **Description:** From users of orgizm.net

```
[arsch]
Server = http://arsch.orgizm.net/$arch

```

#### cinnamon

*   **Maintainer:** [jnbek](https://github.com/jnbek)
*   **Description:** Stable and actively developed Cinnamon packages (Applets, Themes, Extensions), plus others (Hotot, qBitTorrent, GTK themes, Perl modules, and more).

```
[cinnamon]
Server = http://archlinux.zoelife4u.org/cinnamon/$arch

```

#### ede

*   **Maintainer:**
*   **Description:** Equinox Desktop Environment repository

```
[ede]
Server = http://ede.elderlinux.org/repos/archlinux/$arch

```

#### heftig

*   **Maintainer:** [Jan Steffens](https://www.archlinux.org/trustedusers/#heftig)
*   **Description:** Includes linux-zen and aurora (Firefox development build - works alongside [firefox](https://www.archlinux.org/packages/?name=firefox) in the _extra_ repository).
*   **Upstream page:** [https://bbs.archlinux.org/viewtopic.php?id=117157](https://bbs.archlinux.org/viewtopic.php?id=117157)

```
[heftig]
Server = http://pkgbuild.com/~heftig/repo/$arch

```

#### mesa-git

*   **Maintainer:** [Laurent Carlier](https://www.archlinux.org/people/trusted-users/#lcarlier)
*   **Description:** Mesa git builds for the _testing_ and _multilib-testing_ repositories

```
[mesa-git]
Server = http://pkgbuild.com/~lcarlier/$repo/$arch

```

#### noware

*   **Maintainer:** Alexandru Thirtheu (alex_giusi_tiri2@yahoo.com) ([Forums](https://bbs.archlinux.org/profile.php?id=65036)) ([Wiki](https://wiki.archlinux.org/index.php/User:AGT)) ([Web Site](http://direct.noware.systems.:2))
*   **Description:** Software which I prefer being present in a repository, than being compiled each time. It eases software maintenance, I find. Almost anything goes.

```
[noware]
Server = http://direct.$repo.systems.:2/repository/arch/$arch

```

#### openrc-eudev

*   **Maintainer:** [Aaditya](/index.php/User:Aaditya "User:Aaditya"), [Nous](/index.php/User:Nous "User:Nous")
*   **Description:** OpenRC and eudev packages, [artoo's way](/index.php/OpenRC#artoo "OpenRC").

```
[openrc-eudev]
Server = http://downloads.sourceforge.net/project/archopenrc/$repo/$arch

```

#### oracle

*   **Maintainer:** [Malvineous](/index.php/User:Malvineous "User:Malvineous")
*   **Description:** Oracle database client

**Warning:** By adding this you are agreeing to the Oracle license at [http://www.oracle.com/technetwork/licenses/instant-client-lic-152016.html](http://www.oracle.com/technetwork/licenses/instant-client-lic-152016.html)

```
[oracle]
Server = http://linux.shikadi.net/arch/$repo/$arch/

```

#### pantheon

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/trustedusers/#alucryd)
*   **Description:** Repository containing Pantheon-related packages

```
[pantheon]
Server = http://pkgbuild.com/~alucryd/$repo/$arch

```

#### paulburton-fitbitd

*   **Maintainer:**
*   **Description:** Contains fitbitd for synchronizing FitBit trackers

```
[paulburton-fitbitd]
Server = http://www.paulburton.eu/arch/fitbitd/$arch

```

#### pietma

*   **Maintainer:** MartiMcFly <martimcfly@autorisation.de>
*   **Description:** Arch User Repository packages [I create or maintain.](https://aur.archlinux.org/packages/?K=martimcfly&SeB=m).
*   **Upstream page:** [http://pietma.com/tag/aur/](http://pietma.com/tag/aur/)

```
[pietma]
SigLevel = Optional TrustAll
Server = http://repository.pietma.com/nexus/content/repositories/archlinux/$arch/$repo

```

#### pfkernel

*   **Maintainer:** [nous](/index.php/User:Nous "User:Nous")
*   **Description:** Generic and optimized binaries of the ARCH kernel patched with BFS, TuxOnIce, BFQ, Aufs3; i.e. linux-pf[-cpu] and linux-pf-lts[-cpu]. Also, openrc and initscripts-openrc.
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/11734958/x86_64/index.html](http://dl.dropbox.com/u/11734958/x86_64/index.html) or start at [http://bit.do/linux-pf](http://bit.do/linux-pf)

```
[pfkernel]
Server = http://dl.dropbox.com/u/11734958/$arch

```

#### suckless

*   **Maintainer:**
*   **Description:** suckless.org packages

```
[suckless]
Server = http://dl.suckless.org/arch/$arch

```

#### Unity-for-Arch

*   **Maintainer:** [https://github.com/chenxiaolong](https://github.com/chenxiaolong)
*   **Description:** [Unity](/index.php/Unity "Unity") packages for Arch

```
[Unity-for-Arch]
SigLevel = Optional TrustAll
Server = http://dl.dropbox.com/u/486665/Repos/$repo/$arch

```

#### Unity-for-Arch-Extra

*   **Maintainer:** [https://github.com/chenxiaolong](https://github.com/chenxiaolong)
*   **Description:** [Unity](/index.php/Unity "Unity") extra packages for Arch

```
[Unity-for-Arch-Extra]
SigLevel = Optional TrustAll
Server = http://dl.dropbox.com/u/486665/Repos/$repo/$arch

```

#### home_tarakbumba_archlinux_Arch_Extra_standard

*   **Maintainer:**
*   **Description:** Contains a few pre-built AUR packages (zemberek, firefox-kde-opensuse, etc.)

```
[home_tarakbumba_archlinux_Arch_Extra_standard]
Server = http://download.opensuse.org/repositories/home:/tarakbumba:/archlinux/Arch_Extra_standard/$arch

```

#### MEGAsync_Arch_Extra

*   **Maintainer:** [https://mega.nz/#sync](https://mega.nz/#sync)
*   **Description:** MEGAsync extra packages for Arch

```
[MEGAsync_Arch_Extra]
SigLevel = Never
Server = https://mega.co.nz/linux/MEGAsync/Arch_Extra/$arch

```

## i686 only

### Signed

#### eee-ck

*   **Maintainer:** Gruppenpest
*   **Description:** Kernel and modules optimized for Asus Eee PC 701, with -ck patchset.
*   **Key-ID:** 27D4A19A
*   **Keyfile** [http://zembla.duckdns.org/repo/gruppenpest.gpg](http://zembla.duckdns.org/repo/gruppenpest.gpg)

```
[eee-ck]
Server = http://zembla.duckdns.org/repo

```

#### phillid

*   **Maintainer:** Phillid
*   **Description:** Various GCC-s and matching binutils-es which target bare-bones formats (for OS dev). The GCC toolchains are shrunk to ~8 MiB each by disabling NLS and everything but the C front-end. Thrown in there is some ham-related stuff I use such as hamlib, xastir, qsstv. Also a couple of legacy packages which are a bit lengthy to build for most people (kdelibs3, qt3).
*   **Key-ID:** 28F1E6CE

```
[phillid]
Server = http://phillid.tk/r/i686/

```

#### xyne-i686

*   **Maintainer:** [Xyne](https://www.archlinux.org/trustedusers/#xyne)
*   **Description:** A repository for Xyne's own projects containing packages for the "i686" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** This includes all packages in [[xyne-any]](#xyne-any).

```
[xyne-i686]
Server = http://xyne.archlinux.ca/repos/xyne

```

### Unsigned

#### andrwe

*   **Maintainer:** Andrwe Lord Weber
*   **Description:** each program I'm using on x86_64 is compiled for i686 too
*   **Upstream page:** [http://andrwe.org/linux/repository](http://andrwe.org/linux/repository)

```
[andrwe]
Server = http://repo.andrwe.org/i686

```

#### kpiche

*   **Maintainer:**
*   **Description:** Stable OpenSync packages.

```
[kpiche]
Server = http://kpiche.archlinux.ca/repo

```

#### kernel26-pae

*   **Maintainer:**
*   **Description:** PAE-enabled 32-bit kernel 2.6.39

```
[kernel26-pae]
Server = http://kernel26-pae.archlinux.ca/

```

#### linux-pae

*   **Maintainer:**
*   **Description:** PAE-enabled 32-bit kernel 3.0

```
[linux-pae]
Server = http://pae.archlinux.ca/

```

#### rfad

*   **Maintainer:** requiem [at] archlinux.us
*   **Description:** Repository made by haxit

```
[rfad]
Server = http://web.ncf.ca/ey723/archlinux/repo/

```

#### studioidefix

*   **Maintainer:**
*   **Description:** Precompiled boxee packages.

```
[studioidefix]
Server = http://studioidefix.googlecode.com/hg/repo/i686

```

## x86_64 only

### Signed

#### apathism

*   **Maintainer:** Ivan Koryabkin ([apathism](https://aur.archlinux.org/account/apathism/))
*   **Upstream page:** [https://apathism.net/](https://apathism.net/)
*   **Description:** Some AUR packages like [psi-plus-git](https://aur.archlinux.org/packages/psi-plus-git/)<sup><small>AUR</small></sup> (with qt5 enabled).
*   **Key-ID:** 3E37398D
*   **Keyfile:** [http://apathism.net/archlinux/apathism.key](http://apathism.net/archlinux/apathism.key)

```
[apathism]
Server = http://apathism.net/archlinux/

```

#### ashleyis

*   **Maintainer:** Ashley Towns ([ashleyis](https://aur.archlinux.org/account/ashleyis/))
*   **Description:** Debug versions of SDL, chipmunk, libtmx and other misc game libraries. also swift-lang and some other AUR packages
*   **Key-ID:** B1A4D311

```
[ashleyis]
Server = http://arch.ashleytowns.id.au/repo/$arch

```

#### atom

*   **Maintainer:** Nicola Squartini ([tensor5](https://github.com/tensor5))
*   **Upstream page:** [https://github.com/tensor5/arch-atom](https://github.com/tensor5/arch-atom)
*   **Description:** Atom text editor and Electron
*   **Key-ID:** B0544167

```
[atom]
Server = http://noaxiom.org/$repo/$arch

```

#### bioinformatics

*   **Maintainer:** [decryptedepsilon](https://aur.archlinux.org/account/decryptedepsilon/)
*   **Description:** A repository containing some software tools for Bioinformatics
*   **Key-ID:** 60442BA4

```
[bioinformatics]
Server = http://decryptedepsilon.bl.ee/repo/x86_64

```

#### blackleg

*   **Maintainer:** Blackleg ([blackleg](https://aur.archlinux.org/account/blackleg))
*   **Upstream page:** [www.blackleg.es](http://www.blackleg.es)
*   **Description:** My AUR's packages and some like: linux-w110er, nvidia-dkms, android-studio, odoo (OpenErp).
*   **Package list:** [Blackleg x86_64 packages](http://www.blackleg.es/x86_64/index.html)
*   **Key-ID:** 611BFDE1

```
[blackleg]
Server = ftp://ftp.blackleg.es/archlinux/$repo/$arch/

```

#### boyska64

*   **Maintainer:** boyska
*   **Description:** Personal repository: cryptography, sdr, mail handling and misc
*   **Key-ID:** 0x7395DCAE58289CA9

```
[boyska64]
Server = http://boyska.degenerazione.xyz/archrepo

```

#### coderkun-aur

*   **Maintainer:** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **Description:** AUR packages with random software. Supporting package deltas and package and database signing.
*   **Upstream page:** [https://www.coderkun.de/arch](https://www.coderkun.de/arch)
*   **Key-ID:** A6BEE374
*   **Keyfile:** [https://www.coderkun.de/coderkun.asc](https://www.coderkun.de/coderkun.asc)

```
[coderkun-aur]
Server = http://arch.coderkun.de/$repo/$arch/

```

#### coderkun-aur-audio

*   **Maintainer:** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **Description:** AUR packages with audio-related (realtime kernels, lv2-plugins, …) software. Supporting package deltas and package and database signing.
*   **Upstream page:** [https://www.coderkun.de/arch](https://www.coderkun.de/arch)
*   **Key-ID:** A6BEE374
*   **Keyfile:** [https://www.coderkun.de/coderkun.asc](https://www.coderkun.de/coderkun.asc)

```
[coderkun-aur-audio]
Server = http://arch.coderkun.de/$repo/$arch/

```

#### eatabrick

*   **Maintainer:** bentglasstube
*   **Description:** Packages for software written by (and a few just compiled by) bentglasstube.

```
[eatabrick]
SigLevel = Required
Server = http://repo.eatabrick.org/$arch

```

#### freifunk-rheinland

*   **Maintainer:** nomaster
*   **Description:** Packages for the Freifunk project: batman-adv, batctl, fastd and dependencies.

```
[freifunk-rheinland]
Server = http://mirror.fluxent.de/archlinux-custom/$repo/os/$arch

```

#### gustawho

*   **Maintainer:** [Gustavo Castro](https://twitter.com/gustawho) <gustawho@gmail.com>
*   **Description:** Scientific tools (mostly physics/math) and AUR packages that would take long to build, such as [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)<sup><small>AUR</small></sup>.
*   **Package list:** [http://gustawho.x10.mx/repo/x86_64](http://gustawho.x10.mx/repo/x86_64)
*   **Upstream page:** [http://gustawho.x10.mx](http://gustawho.x10.mx)
*   **Key-ID:** 2C575D76

```
[gustawho]
Server = http://gustawho.x10.mx/repo/x86_64

```

*   **Note:** If you need firefox-kde-opensuse for i686 and/or the unsigned x86_64 package, try this repo instead:

```
[home_gustawho_Arch_Extra]
SigLevel = Never
Server = http://download.opensuse.org/repositories/home:/gustawho/Arch_Extra/$arch

```

#### holo

*   **Maintainer:** Stefan Majewsky <holo-pacman@posteo.de> (please prefer to report issues at [Github](https://github.com/majewsky/holo-pacman-repo/issues))
*   **Description:** Packages for [Holo configuration management](https://holocm.org), including compatible plugins and tools.
*   **Upstream page:** [https://github.com/majewsky/holo-pacman-repo](https://github.com/majewsky/holo-pacman-repo)
*   **Package list:** [https://repo.holocm.org/archlinux/x86_64](https://repo.holocm.org/archlinux/x86_64)
*   **Key-ID:** 0xF7A9C9DC4631BD1A

```
[holo]
Server = https://repo.holocm.org/archlinux/x86_64

```

#### Linux-pf

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Signed repositories should not use `SigLevel = Optional` (by definition). (Discuss in [Talk:Unofficial user repositories#](https://wiki.archlinux.org/index.php/Talk:Unofficial_user_repositories))

*   **Maintainer:** [Thaodan](/index.php?title=User:Thaodan&action=edit&redlink=1 "User:Thaodan (page does not exist)")
*   **Description:** Generic and optimized binaries of the ARCH kernel patched with BFS, TuxOnIce, BFQ, Aufs3; i.e. linux-pf, just like [linux-pf](https://aur.archlinux.org/packages/linux-pf/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") but additionally optimized for intel CPUs Sandy Bridge, Ivy Bridge, Haswell and generic of course, and some extra packages
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox).

```
[Linux-pf]
Server = https://dl.dropboxusercontent.com/u/172590784/Linux-pf/x86_64/
SigLevel = Optional

```

#### infinality-bundle-multilib

*   **Maintainer:** [bohoomil](http://bohoomil.com/)
*   **Description:** infinality-bundle multilib repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle-multilib]
Server = http://bohoomil.com/repo/multilib/$arch

```

#### kc9ydn

*   **Maintainer:** [KC9YDN](http://kc9ydn.us)
*   **Description:** Consists mostly of amateur radio related apps
*   **Key-ID:** 7DA25A0F

```
[kc9ydn]
Server = http://kc9ydn.us/repo/

```

#### linux-lts-ck

*   **Maintainer:** Claire Farron [clfarron4](https://aur.archlinux.org/account/clfarron4)
*   **Description:** Current ArchLinux LTS kernel with the CK patch
*   **Key-ID:** E6366A92
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/298301785/arch/linux-lts-ck/x86_64/index.html](http://dl.dropbox.com/u/298301785/arch/linux-lts-ck/x86_64/index.html) or start at [http://tiny.cc/linux-lts-ck](http://tiny.cc/linux-lts-ck)

```
[linux-lts-ck]
Server = http://dl.dropbox.com/u/298301785/arch/linux-lts-ck/$arch

```

#### linux-lts31x

*   **Maintainer:** Claire Farron [clfarron4](https://aur.archlinux.org/account/clfarron4)
*   **Description:** Older LTS kernels (3.10 and 3.12 branch)
*   **Key-ID:** E6366A92
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/298301785/arch/linux-lts31x/x86_64/index.html](http://dl.dropbox.com/u/298301785/arch/linux-lts31x/x86_64/index.html) or start at [http://tiny.cc/linux-lts31x](http://tiny.cc/linux-lts31x)

```
[linux-lts31x]
Server = http://dl.dropbox.com/u/298301785/arch/linux-lts31x/$arch

```

#### linux-lts31x-ck

*   **Maintainer:** Claire Farron [clfarron4](https://aur.archlinux.org/account/clfarron4)
*   **Description:** Older LTS kernels (3.10 and 3.12 branch) with the CK patch
*   **Key-ID:** E6366A92
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/298301785/arch/linux-lts31x-ck/x86_64/index.html](http://dl.dropbox.com/u/298301785/arch/linux-lts31x-ck/x86_64/index.html) or start at [http://tiny.cc/linux-lts31x-ck](http://tiny.cc/linux-lts31x-ck)

```
[linux-lts31x-ck]
Server = http://dl.dropbox.com/u/298301785/arch/linux-lts31x-ck/$arch

```

#### linux-ck-pax

*   **Maintainer:** Claire Farron [clfarron4](https://aur.archlinux.org/account/clfarron4)
*   **Description:** Current Arch Kernel with the CK and PaX security patchsets
*   **Key-ID:** E6366A92
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/298301785/arch/linux-ck-pax/x86_64/index.html](http://dl.dropbox.com/u/298301785/arch/linux-ck-pax/x86_64/index.html) or start at [http://tiny.cc/linux-ck-pax](http://tiny.cc/linux-ck-pax)

```
[linux-ck-pax]
Server = http://dl.dropbox.com/u/298301785/arch/linux-ck-pax/$arch

```

#### linux-tresor

*   **Maintainer:** Claire Farron [clfarron4](https://aur.archlinux.org/account/clfarron4)
*   **Description:** Arch Current and LTS kernels with TRESOR
*   **Key-ID:** E6366A92
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/298301785/arch/linux-tresor/x86_64/index.html](http://dl.dropbox.com/u/298301785/arch/linux-tresor/x86_64/index.html) or start at [http://tiny.cc/linux-tresor](http://tiny.cc/linux-tresor)

```
[linux-tresor]
Server = http://dl.dropbox.com/u/298301785/arch/linux-tresor/$arch

```

#### markzz

*   **Maintainer:** [Mark Weiman (markzz)](/index.php/User:Markzz "User:Markzz")
*   **Description:** Packages that markzz maintains or uses on the AUR; this includes Linux with the vfio patchset ([linux-vfio](https://aur.archlinux.org/packages/linux-vfio/)<sup><small>AUR</small></sup> and [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)<sup><small>AUR</small></sup>), and packages to maintain a Debian package repository.
*   **Sources:** [http://git.markzz.net/markzz/repositories/markzz.git/tree](http://git.markzz.net/markzz/repositories/markzz.git/tree)
*   **Key ID:** 3CADDFDD

**Note:** If you want to add the key by installing the _markzz-keyring_ package, temporarily add `SigLevel = Never` into the repository section.

```
[markzz]
Server = http://repo.markzz.com/arch/$repo/$arch

```

#### qt-debug

*   **Maintainer:** [The Compiler](http://blog.the-compiler.org/?page_id=36)
*   **Description:** Qt/PyQt builds with debug symbols
*   **Upstream page:** [https://github.com/The-Compiler/qt-debug-pkgbuild](https://github.com/The-Compiler/qt-debug-pkgbuild)
*   **Key-ID:** D6A1C70FE80A0C82

```
[qt-debug]
Server = http://qutebrowser.org/qt-debug/$arch

```

#### quarry

*   **Maintainer:** [anatolik](https://www.archlinux.org/developers/#anatolik)
*   **Description:** Arch binary repository for [Rubygems](http://rubygems.org/) packages. See [forum announcement](https://bbs.archlinux.org/viewtopic.php?id=182729) for more information.
*   **Sources:** [https://github.com/anatol/quarry](https://github.com/anatol/quarry)
*   **Key-ID:** Not needed, as maintainer is a developer

```
[quarry]
# report issues at https://github.com/anatol/quarry
Server = http://pkgbuild.com/~anatolik/quarry/x86_64/

```

#### rstudio

*   **Maintainer:** [Artem Klevtsov](https://aur.archlinux.org/account/unikum/)
*   **Description:** Rstudio IDE package (git version) and depends.
*   **Key-ID:** 1CB48DD4

```
[rstudio]
Server = http://repo.psylab.info/archlinux/x86_64/

```

#### siosm-aur

*   **Maintainer:** [Timothee Ravier](https://tim.siosm.fr/about/)
*   **Description:** packages also available in the Arch User Repository, sometimes with minor fixes
*   **Upstream page:** [https://tim.siosm.fr/repositories/](https://tim.siosm.fr/repositories/)
*   **Key-ID:** 78688F83

```
[siosm-aur]
Server = http://siosm.fr/repo/$repo/

```

#### siosm-selinux

*   **Maintainer:** [Timothee Ravier](https://tim.siosm.fr/about/)
*   **Description:** packages required for SELinux support – work in progress (notably, missing an Arch Linux-compatible SELinux policy). See the [SELinux](/index.php/SELinux "SELinux") page for details.
*   **Upstream page:** [https://tim.siosm.fr/repositories/](https://tim.siosm.fr/repositories/)
*   **Key-ID:** 78688F83

```
[siosm-selinux]
Server = http://siosm.fr/repo/$repo/

```

#### subtitlecomposer

*   **Maintainer:** Mladen Milinkovic (maxrd2)
*   **Description:** Subtitle Composer stable and nightly builds
*   **Upstream page:** [https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer)
*   **Key-ID:** EA8CEBEE

```
[subtitlecomposer]
Server = http://smoothware.net/$repo/$arch

```

#### xyne-x86_64

*   **Maintainer:** [Xyne](https://www.archlinux.org/trustedusers/#xyne)
*   **Description:** A repository for Xyne's own projects containing packages for the "x86_64" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** This includes all packages in [[xyne-any]](#xyne-any).

```
[xyne-x86_64]
Server = http://xyne.archlinux.ca/repos/xyne

```

### Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

#### alucryd

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/trustedusers/#alucryd)
*   **Description:** Various packages Maxime Gauduin maintains (or not) in the AUR.

```
[alucryd]
Server = http://pkgbuild.com/~alucryd/$repo/x86_64

```

#### alucryd-multilib

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/trustedusers/#alucryd)
*   **Description:** Various packages needed to run Steam without its runtime environment.

```
[alucryd-multilib]
Server = http://pkgbuild.com/~alucryd/$repo/x86_64

```

#### andrwe

*   **Maintainer:** Andrwe Lord Weber
*   **Description:** contains programs I'm using on many systems
*   **Upstream page:** [http://andrwe.dyndns.org/doku.php/blog/repository](http://andrwe.dyndns.org/doku.php/blog/repository) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2013-11-30]</sup>

```
[andrwe]
Server = http://repo.andrwe.org/x86_64

```

#### archstudio

*   **Maintainer:**
*   **Description:** Audio and Music Packages optimized for Intel Core i3, i5, and i7.
*   **Upstream page:** [http://www.xsounds.org/~archstudio](http://www.xsounds.org/~archstudio)

```
[archstudio]
Server = http://www.xsounds.org/~archstudio/x86_64

```

#### brtln

*   **Maintainer:** [Bartłomiej Piotrowski](https://www.archlinux.org/trustedusers/#bpiotrowski)
*   **Description:** Some VCS packages.

```
[brtln]
Server = http://pkgbuild.com/~barthalion/brtln/$arch/

```

#### kps

*   **Maintainer:** kps
*   **Description:** gmt, catalyst-test, ttf-ms-win8, rstudio, meshlab, gcc-gcj, vlc-git, ffmpeg-git (k10 & intel opt.), docear, maperitive, libressl, bkchem ...

```
[kps]
Server = http://kps.bplaced.net/repo/$arch

```

#### mazdlc

*   **Maintainer:** maz-1 <ohmygod19993 at gmail dot com>
*   **Description:** Various packages maintained by maz-1 (mainly Qt5-based packages and multimedia-related packages )
*   **Upstream page:** [https://build.opensuse.org/project/show/home:mazdlc](https://build.opensuse.org/project/show/home:mazdlc)

```
[home_mazdlc_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/mazdlc/Arch_Extra/$arch

```

#### mazdlc-deadbeef-plugins

*   **Maintainer:** maz-1 <ohmygod19993 at gmail dot com>
*   **Description:** Plugins for the feature-rich music player DeaDBeeF.
*   **Upstream page:** [https://build.opensuse.org/project/show/home:mazdlc](https://build.opensuse.org/project/show/home:mazdlc)

```
[home_mazdlc_deadbeef-plugins_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/mazdlc:/deadbeef-plugins/Arch_Extra/$arch

```

#### mazdlc-kde-frameworks-5

*   **Maintainer:** maz-1 <ohmygod19993 at gmail dot com>
*   **Description:** Unstable packages based on kde frameworks 5.
*   **Upstream page:** [https://build.opensuse.org/project/show/home:mazdlc](https://build.opensuse.org/project/show/home:mazdlc)

```
[home_mazdlc_kde-frameworks-5_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/mazdlc:/kde-frameworks-5/Arch_Extra/$arch

```

#### mikroskeem

*   **Maintainer:** mikroskeem <mikroskeem@mikroskeem.eu>
*   **Description:** Openarena and i3 wm-related packages

```
[mikroskeem]
Server = http://nightsnack.cf/~mark/arch-pkgs

```

#### mingw-w64

*   **Maintainer:** [Philip](https://aur.archlinux.org/account/ant32) and [Jeromy](https://aur.archlinux.org/account/nic96) Reimer
*   **Description:** Almost all mingw-w64 packages in the AUR updated every 8 hours.

```
[mingw-w64]
Server = http://downloads.sourceforge.net/project/mingw-w64-archlinux/$arch
#Server = http://amr.linuxd.org/archlinux/$repo/os/$arch

```

#### pnsft-pur

*   **Maintainer:**
*   **Description:** Japanese input method packages Mozc (vanilla) and libkkc

```
[pnsft-pur]
Server = http://downloads.sourceforge.net/project/pnsft-aur/pur/x86_64

```

#### rakudo

*   **Maintainer:** spider-mario <spidermario@free.fr>
*   **Description:** Rakudo Perl6

```
[rakudo]
Server = http://spidermario.free.fr/archlinux/$repo/$arch

```

#### rightlink

*   **Maintainer:** Chris Fordham <chris@fordham-nagy.id.au>
*   **Description:** RightLink version 10 (RL10) is a new version of RightScale's server agent that connects servers managed through RightScale to the RightScale cloud management platform.

```
[rightlink]
Server = https://s3-ap-southeast-2.amazonaws.com/archlinux.rightscale.me/repo

```

#### seiichiro

*   **Maintainer:**
*   **Description:** VDR and some plugins, mms, foo2zjs-drivers

```
[seiichiro]
Server = http://repo.seiichiro0185.org/x86_64

```

#### studioidefix

*   **Maintainer:**
*   **Description:** Precompiled boxee packages.

```
[studioidefix]
Server = http://studioidefix.googlecode.com/hg/repo/x86_64

```

#### zrootfs

*   **Maintainer:** Isabell Cowan <isabellcowan@gmail.com>
*   **Description:** For Haswell architecture processors with size in mind.

```
[zrootfs]
Server = http://www.izzette.com/izzi/zrootfs

```

## armv6h only

### Unsigned

#### arch-fook-armv6h

*   **Maintainer:** Jaska Kivelä <jaska@kivela.net>
*   **Description:** Stuff that I have compiled for my Raspberry PI. Including Enlightenment and home automation stuff.

```
[arch-fook-armv6h]
Server = http://kivela.net/jaska/arch-fook-armv6h

```

## armv7h only

### Unsigned

#### pietma

*   **Maintainer:** MartiMcFly <martimcfly@autorisation.de>
*   **Description:** Arch User Repository packages [I create or maintain.](https://aur.archlinux.org/packages/?K=martimcfly&SeB=m).
*   **Upstream page:** [http://pietma.com/tag/aur/](http://pietma.com/tag/aur/)

```
[pietma]
SigLevel = Optional TrustAll
Server = http://repository.pietma.com/nexus/content/repositories/archlinux/$arch/$repo

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Unofficial_user_repositories&oldid=414397](https://wiki.archlinux.org/index.php?title=Unofficial_user_repositories&oldid=414397)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")