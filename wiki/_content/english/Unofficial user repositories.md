Related articles

*   [pacman-key](/index.php/Pacman-key "Pacman-key")
*   [Official repositories](/index.php/Official_repositories "Official repositories")

This article lists binary repositories freely created and shared by the community, often providing pre-built versions of PKGBUILDS found in the [AUR](/index.php/AUR "AUR").

**Warning:** Neither the official Arch Linux Developers nor the Trusted Users perform tests of any sort to verify the contents of these repositories; it is up to each user to decide whether to trust their maintainers, and take full responsibility for whatever their decision brings.

In order to use these repositories, you will have to add them to `/etc/pacman.conf`, as explained in [pacman#Repositories and mirrors](/index.php/Pacman#Repositories_and_mirrors "Pacman"). If a repository is signed, you will have to obtain and locally sign the associated key, as explained in [Pacman-key#Adding unofficial keys](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key").

If you want to create your own custom repository, follow [pacman tips#Custom local repository](/index.php/Pacman_tips#Custom_local_repository "Pacman tips").

## Contents

*   [1 Adding your repository to this page](#Adding_your_repository_to_this_page)
*   [2 Any](#Any)
    *   [2.1 Signed](#Signed)
        *   [2.1.1 ivasilev](#ivasilev)
        *   [2.1.2 pkgbuilder](#pkgbuilder)
        *   [2.1.3 xyne-any](#xyne-any)
    *   [2.2 Unsigned](#Unsigned)
        *   [2.2.1 archlinuxgr-any](#archlinuxgr-any)
*   [3 x86_64](#x86_64)
    *   [3.1 Signed](#Signed_2)
        *   [3.1.1 arcanisrepo](#arcanisrepo)
        *   [3.1.2 archlinuxcn](#archlinuxcn)
        *   [3.1.3 archsec](#archsec)
        *   [3.1.4 archstrike](#archstrike)
        *   [3.1.5 archzfs](#archzfs)
        *   [3.1.6 ashleyis](#ashleyis)
        *   [3.1.7 atom](#atom)
        *   [3.1.8 aurpackages](#aurpackages)
        *   [3.1.9 aur-archlinux](#aur-archlinux)
        *   [3.1.10 blackeagle-pre-community](#blackeagle-pre-community)
        *   [3.1.11 boyska64](#boyska64)
        *   [3.1.12 catalyst](#catalyst)
        *   [3.1.13 catalyst-hd234k](#catalyst-hd234k)
        *   [3.1.14 city](#city)
        *   [3.1.15 coderkun-aur](#coderkun-aur)
        *   [3.1.16 coderkun-aur-audio](#coderkun-aur-audio)
        *   [3.1.17 decryptedepsilon](#decryptedepsilon)
        *   [3.1.18 eatabrick](#eatabrick)
        *   [3.1.19 gustawho](#gustawho)
        *   [3.1.20 haskell-core](#haskell-core)
        *   [3.1.21 haskell-happstack](#haskell-happstack)
        *   [3.1.22 haskell-web](#haskell-web)
        *   [3.1.23 herecura](#herecura)
        *   [3.1.24 holo](#holo)
        *   [3.1.25 ivasilev](#ivasilev_2)
        *   [3.1.26 jlk](#jlk)
        *   [3.1.27 jrpi](#jrpi)
        *   [3.1.28 jrpi-haskell](#jrpi-haskell)
        *   [3.1.29 llvm-svn](#llvm-svn)
        *   [3.1.30 markzz](#markzz)
        *   [3.1.31 miffe](#miffe)
        *   [3.1.32 mikelpint](#mikelpint)
        *   [3.1.33 mobile](#mobile)
        *   [3.1.34 qt-debug](#qt-debug)
        *   [3.1.35 quarry](#quarry)
        *   [3.1.36 repo-ck](#repo-ck)
        *   [3.1.37 seblu](#seblu)
        *   [3.1.38 seiichiro](#seiichiro)
        *   [3.1.39 sergej-repo](#sergej-repo)
        *   [3.1.40 siosm-aur](#siosm-aur)
        *   [3.1.41 subtitlecomposer](#subtitlecomposer)
        *   [3.1.42 tredaelli-systemd](#tredaelli-systemd)
        *   [3.1.43 Webkit2Gtk-unstable](#Webkit2Gtk-unstable)
        *   [3.1.44 xyne-x86_64](#xyne-x86_64)
    *   [3.2 Unsigned](#Unsigned_2)
        *   [3.2.1 andrwe](#andrwe)
        *   [3.2.2 alucryd](#alucryd)
        *   [3.2.3 alucryd-multilib](#alucryd-multilib)
        *   [3.2.4 archlinuxfr](#archlinuxfr)
        *   [3.2.5 archlinuxgr](#archlinuxgr)
        *   [3.2.6 archlinuxgr-kde4](#archlinuxgr-kde4)
        *   [3.2.7 arsch](#arsch)
        *   [3.2.8 heftig](#heftig)
        *   [3.2.9 home_fusion809_Arch_Extra](#home_fusion809_Arch_Extra)
        *   [3.2.10 home_Minerva_W_Science_Arch_Extra](#home_Minerva_W_Science_Arch_Extra)
        *   [3.2.11 home_Pival81_arch_xapps_Arch_Extra](#home_Pival81_arch_xapps_Arch_Extra)
        *   [3.2.12 home_post-factum_Arch_Extra](#home_post-factum_Arch_Extra)
        *   [3.2.13 home_tarakbumba_archlinux_Arch_Extra_standard](#home_tarakbumba_archlinux_Arch_Extra_standard)
        *   [3.2.14 home-thaodan](#home-thaodan)
        *   [3.2.15 jkanetwork](#jkanetwork)
        *   [3.2.16 matrixim](#matrixim)
        *   [3.2.17 mesa-git](#mesa-git)
        *   [3.2.18 mingw-w64](#mingw-w64)
        *   [3.2.19 neo_chen](#neo_chen)
        *   [3.2.20 noware](#noware)
        *   [3.2.21 ownstuff](#ownstuff)
        *   [3.2.22 pantheon](#pantheon)
        *   [3.2.23 pietma](#pietma)
        *   [3.2.24 pnsft-pur](#pnsft-pur)
        *   [3.2.25 QOwnNotes](#QOwnNotes)
        *   [3.2.26 rakudo](#rakudo)
        *   [3.2.27 rust-git](#rust-git)
        *   [3.2.28 trinity](#trinity)
        *   [3.2.29 zrootfs](#zrootfs)

## Adding your repository to this page

If you have your own repository, please add it to this page, so that all the other users will know where to find your packages. Please keep the following rules when adding new repositories:

*   Keep the lists in alphabetical order.
*   Include some information about the maintainer: include at least a (nick)name and some form of contact information (web site, email address, user page on ArchWiki or the forums, etc.).
*   If the repository is of the *signed* variety, please include a key-id, possibly using it as the anchor for a link to its keyserver; if the key is not on a keyserver, include a link to the key file.
*   Include some short description (e.g. the category of packages provided in the repository).
*   If there is a page (either on ArchWiki or external) containing more information about the repository, include a link to it.
*   If possible, avoid using comments in code blocks. The formatted description is much more readable. Users who want some comments in their `pacman.conf` can easily create it on their own.

## Any

"Any" repositories are architecture-independent. In other words, they can be used on x86_64, but also on i686 and ARM systems.

### Signed

#### ivasilev

*   **Maintainer:** [Ianis G. Vasilev](https://ivasilev.net)
*   **Description:** A variety of packages, mostly my own software and AUR builds.
*   **Upstream page:** [https://ivasilev.net/pacman](https://ivasilev.net/pacman)
*   **Key-ID:** [17DAB671](https://pgp.mit.edu/pks/lookup?op=vindex&search=0xB77A3C8832838F1F80ADFD7E1D0507B417DAB671)

**Note:** I maintain **any** and **x86_64** repos. **x86_64** includes packages from **any**. **$arch** can be overridden by both.

```
[ivasilev]
Server = https://ivasilev.net/pacman/any
# Server = https://ivasilev.net/pacman/$arch

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

*   **Maintainer:** [Xyne](https://www.archlinux.org/people/trusted-users/#xyne)
*   **Description:** A repository for Xyne's own projects containing packages for "any" architecture.
*   **Upstream page:** [https://xyne.archlinux.ca/projects/](https://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not needed, as maintainer is a TU

**Note:** Use this repository only if there is no matching `[xyne-*]` repository for your architecture.

```
[xyne-any]
Server = https://xyne.archlinux.ca/repos/xyne/

```

### Unsigned

#### archlinuxgr-any

*   **Maintainer:**
*   **Description:** The Hellenic (Greek) unofficial Arch Linux repository with many interesting packages.

```
[archlinuxgr-any]
Server = https://archlinuxgr.tiven.org/archlinux/any

```

## x86_64

Some repositories may also have packages for architectures beside x86_64\. The `$arch` variable will be set automatically by pacman.

### Signed

#### arcanisrepo

*   **Maintainer:** [arcanis](https://www.archlinux.org/people/trusted-users/#arcanis)
*   **Description:** A repository with some AUR packages including packages from VCS
*   **Key-ID:** Not needed, as maintainer is a TU

```
[arcanisrepo]
Server = https://repo.arcanis.me/repo/$arch

```

(It is also available via FTP with the same url.)

#### archlinuxcn

*   **Maintainers:** [Phoenix Nemo (phoenixlzx)](https://plus.google.com/+PhoenixNemo/), [Felix Yan (felixonmars, dev)](https://www.archlinux.org/people/developers/#fyan), [lilydjwg](https://twitter.com/lilydjwg), [farseerfc (TU)](https://www.archlinux.org/people/trusted-users/#farseerfc), and [others](https://github.com/archlinuxcn/repo/graphs/contributors)
*   **Description:** Packages by the Chinese Arch Linux community, all signed. Be aware that i686 packages are not fully maintained and tested, create an issue if you find some problems.
*   **Git Repo:** [https://github.com/archlinuxcn/repo](https://github.com/archlinuxcn/repo)
*   **Issue tracking:** [https://github.com/archlinuxcn/repo/issues](https://github.com/archlinuxcn/repo/issues) for packaging issues, out-of-date notifications, package requests, and related questions
*   **Mirrors:** [https://github.com/archlinuxcn/mirrorlist-repo](https://github.com/archlinuxcn/mirrorlist-repo) (Mostly for users in mainland China), or install *archlinuxcn-mirrorlist-git* from the repo.
*   **Key-ID:** Once the repo is added, *archlinuxcn-keyring* package must be installed before any other so you do not get errors about PGP signatures. *archlinuxcn-keyring* package itself is signed by TU.

```
[archlinuxcn]
Server = http://repo.archlinuxcn.org/$arch
## or use a CDN (beta)
#Server = https://cdn.repo.archlinuxcn.org/$arch
## or install archlinuxcn-mirrorlist-git and use the mirrorlist
#Include = /etc/pacman.d/archlinuxcn-mirrorlist

```

#### archsec

*   **Maintainer:** [The ArchSec Team](https://archsec.info)
*   **Description:** A repository of binaries compiled from a hardened toolchain
*   **Upstream page:** [https://archsec.info/](https://archsec.info/)
*   **Key-ID:** 500773F3B282BEDB4D960B0F3C6F2219257C9E23

**Note:** ArchSec-specific instructions can be found at [https://archsec.info/docs/config/](https://archsec.info/docs/config/)

```
[archsec]
Server = https://archsec.info/$repo/$arch

```

#### archstrike

*   **Maintainer:** [The ArchStrike Team](https://archstrike.org/team)
*   **Description:** A repository for security professionals and enthusiasts
*   **Upstream page:** [https://archstrike.org/](https://archstrike.org/)
*   **Key-ID:** 9D5F1C051D146843CDA4858BDE64825E7CBC0D51

**Note:** ArchStrike specific instructions can be found at [https://archstrike.org/wiki/setup](https://archstrike.org/wiki/setup)

```
[archstrike]
Server = https://mirror.archstrike.org/$arch/$repo

```

#### archzfs

*   **Maintainer:** [Jesus Alvarez (demizer)](http://archzfs.com)
*   **Description:** Packages for ZFS on Arch Linux.
*   **Upstream page:** [https://github.com/archzfs/archzfs](https://github.com/archzfs/archzfs)
*   **Key-ID:** 5E1ABF240EE7A126

```
[archzfs]
Server = http://archzfs.com/$repo/x86_64

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

#### aurpackages

*   **Maintainer:** Mark Vainomaa <mikroskeem@mikroskeem.eu>
*   **Description:** AUR packages I tend to use every day. Will be updated weekly
*   **Key-ID:** 2A07EF8371AFC028

```
[aurpackages]
Server = https://r.mikroskeem.eu

```

#### aur-archlinux

*   **Maintainer:** Marc Mettke <marc@itmettke.de>
*   **Description:** Auto Build of Most Popular AUR Packages
*   **Archive:** [https://repo.itmettke.de/aur-archive/](https://repo.itmettke.de/aur-archive/)
*   **Key-ID:** 7448C890582975CD

```
[aur-archlinux]
Server = https://repo.itmettke.de/aur/$repo/$arch

```

#### blackeagle-pre-community

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** testing of the by me maintaned packages before moving to *community* repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[blackeagle-pre-community]
Server = https://repo.herecura.be/$repo/$arch

```

#### boyska64

*   **Maintainer:** boyska
*   **Description:** Personal repository: cryptography, sdr, mail handling and misc; don't expect packages to be upgraded promptly, I am a zealot of slackness
*   **Key-ID:** 0x7395DCAE58289CA9

```
[boyska64]
Server = http://boyska.degenerazione.xyz/archrepo

```

#### catalyst

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Key-ID:** 653C3094

```
[catalyst]
Server = https://mirror.hactar.xyz/Vi0L0/catalyst/$arch

```

#### catalyst-hd234k

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Key-ID:** 653C3094

```
[catalyst-hd234k]
Server = https://mirror.hactar.xyz/Vi0L0/catalyst-hd234k/$arch

```

#### city

*   **Maintainer:** [Balló György](https://www.archlinux.org/people/trusted-users/#bgyorgy)
*   **Description:** Experimental/unpopular packages.
*   **Upstream page:** [https://pkgbuild.com/~bgyorgy/city.html](https://pkgbuild.com/~bgyorgy/city.html)
*   **Key-ID:** Not needed, as maintainer is a TU

```
[city]
Server = https://pkgbuild.com/~bgyorgy/$repo/os/$arch

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
*   **Keyfile:** [https://www.coderkun.de/coderkun.key](https://www.coderkun.de/coderkun.key)

```
[coderkun-aur-audio]
Server = http://arch.coderkun.de/$repo/$arch/

```

#### decryptedepsilon

*   **Maintainer:** [decryptedepsilon](https://aur.archlinux.org/account/decryptedepsilon/)
*   **Description:** AUR packages that I usually install (dropbox, jdk, atom, spotify, tor-browser-en, paper-icon-theme-git)
*   **Upstream page:** [http://www.decryptedepsilon.bl.ee/repo/x86_64](http://www.decryptedepsilon.bl.ee/repo/x86_64)
*   **Key-ID:** 60442BA4
*   **Keyfile:** [http://www.decryptedepsilon.bl.ee/decryptedepsilon.asc](http://www.decryptedepsilon.bl.ee/decryptedepsilon.asc)

```
[decryptedepsilon]
Server = http://decryptedepsilon.bl.ee/repo/$arch/

```

#### eatabrick

*   **Maintainer:** bentglasstube
*   **Description:** Packages for software written by (and a few just compiled by) bentglasstube.

```
[eatabrick]
Server = http://repo.eatabrick.org/$arch

```

#### gustawho

*   **Maintainer:** [Gustavo Castro](https://twitter.com/gustawho) <gustawho@openmailbox.com>
*   **Description:** Scientific tools (mostly physics/math) and AUR packages that take long to build (such as [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)).
*   **Package list:** [https://gustawho.com/pacman](https://gustawho.com/pacman)
*   **Upstream page:** [https://gustawho.com](https://gustawho.com)
*   **Key-ID:** [76578671](https://gustawho.com/repo/gustawho.key)

```
[gustawho]
Server = https://gustawho.com/repo/$arch

```

#### haskell-core

See [ArchHaskell#haskell-core](/index.php/ArchHaskell#haskell-core "ArchHaskell").

#### haskell-happstack

See [ArchHaskell#haskell-happstack](/index.php/ArchHaskell#haskell-happstack "ArchHaskell").

#### haskell-web

See [ArchHaskell#haskell-web](/index.php/ArchHaskell#haskell-web "ArchHaskell").

#### herecura

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** additional packages not found in the *community* repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[herecura]
Server = https://repo.herecura.be/$repo/$arch

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

#### ivasilev

*   **Maintainer:** [Ianis G. Vasilev](https://ivasilev.net)
*   **Description:** A variety of packages, mostly my own software and AUR builds.
*   **Upstream page:** [https://ivasilev.net/pacman](https://ivasilev.net/pacman)
*   **Key-ID:** [17DAB671](https://pgp.mit.edu/pks/lookup?op=vindex&search=0xB77A3C8832838F1F80ADFD7E1D0507B417DAB671)

**Note:** I maintain **any** and **x86_64** repos. **x86_64** includes packages from **any**. **$arch** can be overridden by both.

```
[ivasilev]
Server = https://ivasilev.net/pacman/$arch

```

#### jlk

*   **Maintainer:** [Jakub Klinkovský](/index.php/User:Lahwaacz "User:Lahwaacz")
*   **Description:** Various packages from the ABS and AUR. Modified packages are in the `modified` group.
*   **Upstream page:** [http://jlk.fjfi.cvut.cz/arch/repo/README.html](http://jlk.fjfi.cvut.cz/arch/repo/README.html)
*   **Key-ID:** 932BA3FA0C86812A32D1F54DAB5964AEB9FEDDDC

```
[jlk]
Server = http://jlk.fjfi.cvut.cz/arch/repo

```

#### jrpi

*   **Maintainer:** [João Miguel](/index.php/User:JMCF125 "User:JMCF125")
*   **Upstream page:** [https://jrpi.mooo.com/Programação?lang=en#Repositories](https://jrpi.mooo.com/Programação?lang=en#Repositories)
*   **Description:** Some packages from the AUR, patched official packages and old packages.
*   **Package list:** [https://jrpi.mooo.com/Repositórios/principal/](https://jrpi.mooo.com/Repositórios/principal/)
*   **Key-ID:** 300F3A7E6DE3712674AF1BA3C734821C2C9A679F

```
[jrpi]
Server = https://jrpi.mooo.com/Repositórios/principal/

```

#### jrpi-haskell

*   **Maintainer:** [João Miguel](/index.php/User:JMCF125 "User:JMCF125")
*   **Upstream page:** [https://jrpi.mooo.com/Programação?lang=en#Repositories](https://jrpi.mooo.com/Programação?lang=en#Repositories)
*   **Description:** Haskell packages (created with cblrepo but not available in haskell-core).
*   **Package list:** [https://jrpi.mooo.com/Repositórios/haskell/](https://jrpi.mooo.com/Repositórios/haskell/)
*   **Key-ID:** 300F3A7E6DE3712674AF1BA3C734821C2C9A679F

```
[jrpi-haskell]
Server = https://jrpi.mooo.com/Repositórios/haskell/

```

#### llvm-svn

*   **Maintainer:** [Luchesar V. ILIEV (kerberizer)](/index.php/User:Kerberizer "User:Kerberizer")
*   **Description:** [llvm-svn](https://aur.archlinux.org/pkgbase/llvm-svn) and [lib32-llvm-svn](https://aur.archlinux.org/pkgbase/lib32-llvm-svn) from AUR: the LLVM compiler infrastructure, the Clang frontend, and the tools associated with it
*   **Key-ID:** [0x76563F75679E4525](https://sks-keyservers.net/pks/lookup?op=vindex&search=0x76563F75679E4525&fingerprint=on&exact=on), fingerprint `D16C F22D 27D1 091A 841C 4BE9 7656 3F75 679E 4525`

```
[llvm-svn]
Server = https://repos.uni-plovdiv.net/archlinux/$repo/$arch

```

#### markzz

*   **Maintainer:** [Mark Weiman (markzz)](/index.php/User:Markzz "User:Markzz")
*   **Description:** Packages that markzz maintains or uses on the AUR; this includes Linux with the vfio patchset ([linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) and [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)), and packages to maintain a Debian package repository.
*   **Key ID:** 3CADDFDD

**Note:** If you want to add the key by installing the *markzz-keyring* package, temporarily add `SigLevel = Never` into the repository section.

```
[markzz]
Server = https://repo.markzz.com/arch/$repo/$arch

```

#### miffe

*   **Maintainer:** [miffe](https://bbs.archlinux.org/profile.php?id=4059)
*   **Description:** AUR packages maintained by miffe, e.g. linux-mainline
*   **Key ID:** 313F5ABD

```
[miffe]
Server = https://arch.miffe.org/$arch/

```

#### mikelpint

*   **Maintainer:** [Mikel Pintado (Mikelpint)](/index.php/User:Mikelpint "User:Mikelpint")
*   **Description:** Packages that mikelpint maintains in the AUR.
*   **Key ID:** 5CA78FC65B189E2B

```
[mikelpint]
Server = https://mikelpint.github.io/repository/archlinux/repo

```

#### mobile

*   **Maintainer:** [farwayer](https://keybase.io/farwayer)
*   **Description:** React Native and Android development
*   **Upstream page:** [https://keybase.pub/farwayer/arch/mobile/](https://keybase.pub/farwayer/arch/mobile/)
*   **Key ID:** 7943315502A936D7

```
[mobile]
Server = https://farwayer.keybase.pub/arch/$repo

```

#### qt-debug

*   **Maintainer:** [The Compiler](http://blog.the-compiler.org/?page_id=36)
*   **Description:** Qt/PyQt builds with debug symbols
*   **Upstream page:** [https://github.com/qutebrowser/qt-debug-pkgbuild](https://github.com/qutebrowser/qt-debug-pkgbuild)
*   **Key-ID:** D6A1C70FE80A0C82

```
[qt-debug]
Server = http://qutebrowser.org/qt-debug/$arch

```

#### quarry

*   **Maintainer:** [anatolik](https://www.archlinux.org/people/developers/#anatolik)
*   **Description:** Arch binary repository for [Rubygems](http://rubygems.org/) packages. See [forum announcement](https://bbs.archlinux.org/viewtopic.php?id=182729) for more information.
*   **Sources:** [https://github.com/anatol/quarry](https://github.com/anatol/quarry)
*   **Key-ID:** Not needed, as maintainer is a developer

```
[quarry]
Server = https://pkgbuild.com/~anatolik/quarry/x86_64/

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

*   **Maintainer:** [Sébastien Luttringer](https://www.archlinux.org/people/developers/#seblu)
*   **Description:** All seblu useful pre-built packages, some homemade (virtualbox-ext-oracle, linux-seblu-meta, bedup).
*   **Key-ID:** Not required, as maintainer is a Developer

```
[seblu]
Server = http://al.seblu.net/$repo/$arch

```

#### seiichiro

*   **Maintainer:** [Stefan Brand (seiichiro0185)](https://www.seiichiro0185.org)
*   **Description:** AUR-packages I use frequently
*   **Key-ID:** 805517CC

```
[seiichiro]
Server = https://www.seiichiro0185.org/repo/$arch

```

#### sergej-repo

*   **Maintainer:** [Sergej Pupykin](https://www.archlinux.org/people/trusted-users/#spupykin)
*   **Description:** psi-plus, owncloud-git, ziproxy, android, MySQL, and other stuff. Some packages also available for armv7h.
*   **Key-ID:** Not required, as maintainer is a TU

```
[sergej-repo]
Server = http://repo.p5n.pp.ru/$repo/os/$arch

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

#### subtitlecomposer

*   **Maintainer:** Mladen Milinkovic (maxrd2)
*   **Description:** Subtitle Composer stable and nightly builds
*   **Upstream page:** [https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer)
*   **Key-ID:** EF9D9B26

```
[subtitlecomposer]
Server = http://smoothware.net/$repo/$arch

```

#### tredaelli-systemd

*   **Maintainer:** [Timothy Redaelli](https://www.archlinux.org/people/trusted-users/#tredaelli)
*   **Description:** systemd rebuilt with unofficial OpenVZ patch (kernel < 2.6.32-042stab111.1)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** `[tredaelli-systemd]` must be put before `[core]` in `/etc/pacman.conf`

```
[tredaelli-systemd]
Server = https://pkgbuild.com/~tredaelli/repo/systemd/$arch

```

#### Webkit2Gtk-unstable

*   **Maintainer:** [Mariusz Wojcik](/index.php/User:Mrmariusz "User:Mrmariusz")
*   **Description:** Latest Webkit2Gtk build for early adopters.
*   **Upstream Page:** [https://webkitgtk.org/](https://webkitgtk.org/)
*   **Key-ID:** 346854B5

```
[home_mrmariusz_ArchLinux]
Server = https://download.opensuse.org/repositories/home:/mrmariusz/ArchLinux/$arch

```

#### xyne-x86_64

*   **Maintainer:** [Xyne](https://www.archlinux.org/people/trusted-users/#xyne)
*   **Description:** A repository for Xyne's own projects containing packages for the "x86_64" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** This includes all packages in [[xyne-any]](#xyne-any).

```
[xyne-x86_64]
Server = https://xyne.archlinux.ca/repos/xyne

```

### Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

#### andrwe

*   **Maintainer:** Andrwe Lord Weber
*   **Description:** contains programs I'm using on many systems
*   **Upstream page:** [http://andrwe.org/linux/repository](http://andrwe.org/linux/repository)

```
[andrwe]
Server = http://repo.andrwe.org/$arch

```

#### alucryd

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **Description:** Various packages Maxime Gauduin maintains (or not) in the AUR.

```
[alucryd]
Server = https://pkgbuild.com/~alucryd/$repo/x86_64

```

#### alucryd-multilib

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **Description:** Various packages needed to run Steam without its runtime environment.

```
[alucryd-multilib]
Server = https://pkgbuild.com/~alucryd/$repo/x86_64

```

#### archlinuxfr

*   **Maintainer:**
*   **Description:**
*   **Upstream page:** [http://afur.archlinux.fr](http://afur.archlinux.fr)

```
[archlinuxfr]
Server = http://repo.archlinux.fr/$arch

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

#### heftig

*   **Maintainer:** [Jan Steffens](https://www.archlinux.org/people/developers/#heftig)
*   **Description:** Includes pulseaudio-git, pavucontrol-git, and firefox-developer-edition
*   **Upstream page:** [https://bbs.archlinux.org/viewtopic.php?id=117157](https://bbs.archlinux.org/viewtopic.php?id=117157)

```
[heftig]
Server = https://pkgbuild.com/~heftig/repo/$arch

```

#### home_fusion809_Arch_Extra

*   **Maintainer:** [Brenton Horne](/index.php?title=User:Fusion809&action=edit&redlink=1 "User:Fusion809 (page does not exist)") (brentonhorne77 at gmail dot com).

*   **Description:** Provides a few AUR and other packages I like. Like CodeLite, bleeding-edge (latest release within 1 day of its release) GVim (GTK+2 interface) and Sway (specifically release candidates when they're available).

```
[home_fusion809_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/$arch

```

#### home_Minerva_W_Science_Arch_Extra

*   **Maintainer:**
*   **Description:** [OpenFOAM](/index.php/OpenFOAM "OpenFOAM") packages.

```
[home_Minerva_W_Science_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/$arch 

```

#### home_Pival81_arch_xapps_Arch_Extra

*   **Maintainer:** Valerio Pizzi ([Pival81](https://github.com/Pival81) <pival801@gmail.com>)
*   **Description:** [XApps](https://github.com/linuxmint/xapps) packages.

```
[home_Pival81_arch_xapps_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/Pival81:/arch:/xapps/Arch_Extra/$arch 

```

#### home_post-factum_Arch_Extra

*   **Maintainer**: [Oleksandr Natalenko aka post-factum](https://aur.archlinux.org/account/post-factum)
*   **Upstream page**: [https://pfactum.github.io/pf-kernel/](https://pfactum.github.io/pf-kernel/)
*   **Description**: [pf-kernel](/index.php/Kernels#Major_patchsets "Kernels") and other packages by its developer, post-factum

```
[home_post-factum_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/post-factum/Arch_Extra/$arch

```

#### home_tarakbumba_archlinux_Arch_Extra_standard

*   **Maintainer:**
*   **Description:** Contains a few pre-built AUR packages (zemberek, etc.)

```
[home_tarakbumba_archlinux_Arch_Extra_standard]
Server = https://download.opensuse.org/repositories/home:/tarakbumba:/archlinux/Arch_Extra_standard/$arch

```

#### home-thaodan

*   **Maintainer**: [Thaodan](https://aur.archlinux.org/account/Thaodan)
*   **Upstream page**: [https://gitlab.com/Thaodan/linux-pf](https://gitlab.com/Thaodan/linux-pf)
*   **Description**: [pf-kernel](/index.php/Kernels#Major_patchsets "Kernels") and other packages by pf-kernel fork developer, Thaodan

```
[home-thaodan]
Server = https://thaodan.de/home/bidar/home-thaodan/$arch

```

#### jkanetwork

*   **Maintainer:** kprkpr <kevin01010 at gmail dot com>
*   **Maintainer:** Joselucross <jlgarrido97 at gmail dot com>
*   **Description:** Packages of AUR like pimagizer,stepmania,yaourt,linux-mainline,wps-office,grub-customizer,some IDE.. Open for all that wants to contribute
*   **Upstream page:** [http://repo.jkanetwork.com/](http://repo.jkanetwork.com/)

```
[jkanetwork]
Server = http://repo.jkanetwork.com/repo/$repo/

```

#### matrixim

*   **Maintainer:** [Iru Cai](https://aur.archlinux.org/account/mytbk)
*   **Description:** Packages related to [Matrix](https://matrix.org) messaging protocol, and software run on [https://matrixim.cc](https://matrixim.cc) -- my website and Matrix homeserver.

```
[matrixim]
Server = https://repo.matrixim.cc/$repo/$arch

```

#### mesa-git

*   **Maintainer:** [Laurent Carlier](https://www.archlinux.org/people/trusted-users/#lcarlier)
*   **Description:** Mesa git builds for the *testing* and *multilib-testing* repositories

```
[mesa-git]
Server = https://pkgbuild.com/~lcarlier/$repo/$arch

```

#### mingw-w64

*   **Maintainer:** [Philip](https://aur.archlinux.org/account/ant32) and [Jeromy](https://aur.archlinux.org/account/nic96) Reimer
*   **Description:** Almost all mingw-w64 packages in the AUR.

**Note:** This repo is not actively maintained anymore. It has not been updated since 2016-01-04.

```
[mingw-w64]
Server = https://downloads.sourceforge.net/project/mingw-w64-archlinux/$arch
#Server = http://amr.linuxd.org/archlinux/$repo/os/$arch

```

#### neo_chen

*   **Maintainer:** Kolei Chen (Neo_Chen) <chenkolei@gmail.com>
*   **Description:** Some uncommon AUR Package

**Note:** This repo runs on a unstable Desktop.

```
[neo_chen]
Server = https://neolinuxworkstation.nerdpol.ovh/~neo_chen/neo_chen_repo/
Server = https://thunix.org/~neo_chen/neo_chen_repo/
Server = http://sl-sgp.asn.yt/~neo_chen_repo/

```

#### noware

**Note:** As of August 2017 both website and repositories at [http://direct.noware.systems](http://direct.noware.systems) are down due to server-side hardware problems. This might be resolved at some point in the future.

*   **Maintainer:** Alexandru Thirtheu (alex_giusi_tiri2@yahoo.com) ([Forums](https://bbs.archlinux.org/profile.php?id=65036)) ([Wiki](/index.php?title=User:AGT&action=edit&redlink=1 "User:AGT (page does not exist)")) ([Web Site](http://direct.noware.systems.:2))
*   **Description:** Software which I prefer being present in a repository, than being compiled each time. It eases software maintenance, I find. Almost anything goes.

```
[noware]
Server = http://direct.$repo.systems.:2/repository/arch/$arch

```

#### ownstuff

*   **Maintainer:** [Martchus](https://aur.archlinux.org/account/Martchus)
*   **Description:** A lot of packages from the AUR, eg. a great number of mingw-w64 packages, fonts, tools like [Tag Editor](https://aur.archlinux.org/packages/tageditor), [Syncthing Tray](https://aur.archlinux.org/packages/syncthingtray) and [Subtitle Composer](https://aur.archlinux.org/packages/subtitlecomposer)
*   **Upstream page**: [https://github.com/Martchus/PKGBUILDs](https://github.com/Martchus/PKGBUILDs) (sources beside the AUR) and [https://martchus.no-ip.biz/repoindex](https://martchus.no-ip.biz/repoindex) (package browser/search)

```
[ownstuff]
Server = http://martchus.no-ip.biz/repo/arch/$repo/os/$arch

```

#### pantheon

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **Description:** Repository containing Pantheon-related packages

```
[pantheon]
Server = https://pkgbuild.com/~alucryd/$repo/$arch

```

#### pietma

*   **Maintainer:** MartiMcFly <martimcfly@autorisation.de>
*   **Description:** Arch User Repository packages [I create or maintain.](https://aur.archlinux.org/packages/?K=martimcfly&SeB=m).
*   **Upstream page:** [http://pietma.com/tag/aur/](http://pietma.com/tag/aur/)

```
[pietma]
Server = http://repository.pietma.com/nexus/content/repositories/archlinux/$arch/$repo

```

#### pnsft-pur

*   **Maintainer:**
*   **Description:** Japanese input method packages Mozc (vanilla) and libkkc

```
[pnsft-pur]
Server = https://downloads.sourceforge.net/project/pnsft-aur/pur/x86_64

```

#### QOwnNotes

*   **Maintainer:** [http://www.qownnotes.org](http://www.qownnotes.org)
*   **Description:** QOwnNotes is a open source notepad and todo list manager with markdown support and [ownCloud](/index.php/OwnCloud "OwnCloud") integration.

```
[home_pbek_QOwnNotes_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/$arch

```

#### rakudo

*   **Maintainer:** spider-mario <spidermario@free.fr>
*   **Description:** Rakudo Perl6

```
[rakudo]
Server = https://spider-mario.quantic-telecom.net/archlinux/$repo/$arch

```

#### rust-git

*   **Maintainer:** Tatsuyuki Ishi <ishitatsuyuki@gmail.com>
*   **Description:** Packages of rust-git and others. Normally updated weekly.

```
[rust-git]
Server = https://tatsuyuki.kdns.info/archlinux/$repo/$arch

```

#### trinity

*   **Maintainer:** Michael Manley <mmanley@nasutek.com>
*   **Description:** [Trinity](/index.php/Trinity "Trinity") Desktop Environment

```
[trinity]
Server = http://repo.nasutek.com/arch/contrib/trinity/x86_64

```

#### zrootfs

*   **Maintainer:** Isabell Cowan <isabellcowan@gmail.com>
*   **Description:** For Haswell and Broadwell architecture processors with size in mind.

**Note:** This repo has not been maintained since 2016-03-14\. There are no guarantees as to how long it will be kept online.

```
[zrootfs]
Server = https://www.izzette.com/izzi/zrootfs-old

```