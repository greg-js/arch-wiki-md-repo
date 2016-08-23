This article lists binary repositories freely created and shared by the community, often providing pre-built versions of PKGBUILDS found in the [AUR](/index.php/AUR "AUR").

**Warning:** Neither the official Arch Linux Developers nor the Trusted Users perform tests of any sort to verify the contents of these repositories; it is up to each user to decide whether to trust their maintainers, and take full responsibility for whatever their decision brings.

In order to use these repositories, you will have to add them to `/etc/pacman.conf`, as explained in [pacman#Repositories and mirrors](/index.php/Pacman#Repositories_and_mirrors "Pacman"). If a repository is signed, you will have to obtain and locally sign the associated key, as explained in [Pacman-key#Adding unofficial keys](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key").

If you want to create your own custom repository, follow [pacman tips#Custom local repository](/index.php/Pacman_tips#Custom_local_repository "Pacman tips").

**Tip:** To get a list of all servers listed in this page: `curl 'https://wiki.archlinux.org/index.php/Unofficial_user_repositories' | grep 'Server = ' | sed "s/\$arch/$(uname -m)/g" | cut -f 3 -d' '` 

For your convenience you can, for example, open them all in a web browser to inspect the contents of their repositories.

## Contents

*   [1 Adding your repository to this page](#Adding_your_repository_to_this_page)
*   [2 Any](#Any)
    *   [2.1 Signed](#Signed)
        *   [2.1.1 infinality-bundle-fonts](#infinality-bundle-fonts)
        *   [2.1.2 ivasilev](#ivasilev)
        *   [2.1.3 pkgbuilder](#pkgbuilder)
        *   [2.1.4 xyne-any](#xyne-any)
        *   [2.1.5 youtube-dl](#youtube-dl)
    *   [2.2 Unsigned](#Unsigned)
        *   [2.2.1 archlinuxgr-any](#archlinuxgr-any)
*   [3 Both i686 and x86_64](#Both_i686_and_x86_64)
    *   [3.1 Signed](#Signed_2)
        *   [3.1.1 arcanisrepo](#arcanisrepo)
        *   [3.1.2 arch-openrc](#arch-openrc)
        *   [3.1.3 archlinuxcn](#archlinuxcn)
        *   [3.1.4 blackeagle-pre-community](#blackeagle-pre-community)
        *   [3.1.5 catalyst](#catalyst)
        *   [3.1.6 catalyst-hd234k](#catalyst-hd234k)
        *   [3.1.7 city](#city)
        *   [3.1.8 haskell-core](#haskell-core)
        *   [3.1.9 haskell-happstack](#haskell-happstack)
        *   [3.1.10 haskell-web](#haskell-web)
        *   [3.1.11 herecura](#herecura)
        *   [3.1.12 infinality-bundle](#infinality-bundle)
        *   [3.1.13 ivasilev](#ivasilev_2)
        *   [3.1.14 llvm-svn](#llvm-svn)
        *   [3.1.15 nuvolaplayer](#nuvolaplayer)
        *   [3.1.16 miffe](#miffe)
        *   [3.1.17 repo-ck](#repo-ck)
        *   [3.1.18 seblu](#seblu)
        *   [3.1.19 seiichiro](#seiichiro)
        *   [3.1.20 sergej-repo](#sergej-repo)
        *   [3.1.21 tredaelli-systemd](#tredaelli-systemd)
        *   [3.1.22 Webkit2Gtk-unstable](#Webkit2Gtk-unstable)
    *   [3.2 Unsigned](#Unsigned_2)
        *   [3.2.1 archaudio](#archaudio)
        *   [3.2.2 archlinuxfr](#archlinuxfr)
        *   [3.2.3 archlinuxgr](#archlinuxgr)
        *   [3.2.4 archlinuxgr-kde4](#archlinuxgr-kde4)
        *   [3.2.5 arsch](#arsch)
        *   [3.2.6 cinnamon](#cinnamon)
        *   [3.2.7 heftig](#heftig)
        *   [3.2.8 home_Minerva_W_Science_Arch_Extra](#home_Minerva_W_Science_Arch_Extra)
        *   [3.2.9 mesa-git](#mesa-git)
        *   [3.2.10 noware](#noware)
        *   [3.2.11 openrc-eudev](#openrc-eudev)
        *   [3.2.12 pantheon](#pantheon)
        *   [3.2.13 pietma](#pietma)
        *   [3.2.14 trinity](#trinity)
        *   [3.2.15 home_tarakbumba_archlinux_Arch_Extra_standard](#home_tarakbumba_archlinux_Arch_Extra_standard)
        *   [3.2.16 QOwnNotes](#QOwnNotes)
*   [4 i686 only](#i686_only)
    *   [4.1 Signed](#Signed_3)
        *   [4.1.1 xyne-i686](#xyne-i686)
    *   [4.2 Unsigned](#Unsigned_3)
        *   [4.2.1 andrwe](#andrwe)
        *   [4.2.2 kpiche](#kpiche)
        *   [4.2.3 kernel26-pae](#kernel26-pae)
        *   [4.2.4 linux-pae](#linux-pae)
*   [5 x86_64 only](#x86_64_only)
    *   [5.1 Signed](#Signed_4)
        *   [5.1.1 archzfs](#archzfs)
        *   [5.1.2 ashleyis](#ashleyis)
        *   [5.1.3 atom](#atom)
        *   [5.1.4 boyska64](#boyska64)
        *   [5.1.5 coderkun-aur](#coderkun-aur)
        *   [5.1.6 coderkun-aur-audio](#coderkun-aur-audio)
        *   [5.1.7 decryptedepsilon](#decryptedepsilon)
        *   [5.1.8 eatabrick](#eatabrick)
        *   [5.1.9 freifunk-rheinland](#freifunk-rheinland)
        *   [5.1.10 holo](#holo)
        *   [5.1.11 infinality-bundle-multilib](#infinality-bundle-multilib)
        *   [5.1.12 linux-kalterfx](#linux-kalterfx)
        *   [5.1.13 nullptr_t](#nullptr_t)
        *   [5.1.14 markzz](#markzz)
        *   [5.1.15 qt-debug](#qt-debug)
        *   [5.1.16 quarry](#quarry)
        *   [5.1.17 siosm-aur](#siosm-aur)
        *   [5.1.18 subtitlecomposer](#subtitlecomposer)
        *   [5.1.19 xyne-x86_64](#xyne-x86_64)
    *   [5.2 Unsigned](#Unsigned_4)
        *   [5.2.1 alucryd](#alucryd)
        *   [5.2.2 alucryd-multilib](#alucryd-multilib)
        *   [5.2.3 andrwe](#andrwe_2)
        *   [5.2.4 brtln](#brtln)
        *   [5.2.5 jkanetwork](#jkanetwork)
        *   [5.2.6 mikroskeem](#mikroskeem)
        *   [5.2.7 mingw-w64](#mingw-w64)
        *   [5.2.8 pkgbuild-current](#pkgbuild-current)
        *   [5.2.9 pnsft-pur](#pnsft-pur)
        *   [5.2.10 rakudo](#rakudo)
        *   [5.2.11 rightlink](#rightlink)
        *   [5.2.12 zrootfs](#zrootfs)

## Adding your repository to this page

If you have your own repository, please add it to this page, so that all the other users will know where to find your packages. Please keep the following rules when adding new repositories:

*   Keep the lists in alphabetical order.
*   Include some information about the maintainer: include at least a (nick)name and some form of contact information (web site, email address, user page on ArchWiki or the forums, etc.).
*   If the repository is of the *signed* variety, please include a key-id, possibly using it as the anchor for a link to its keyserver; if the key is not on a keyserver, include a link to the key file.
*   Include some short description (e.g. the category of packages provided in the repository).
*   If there is a page (either on ArchWiki or external) containing more information about the repository, include a link to it.
*   If possible, avoid using comments in code blocks. The formatted description is much more readable. Users who want some comments in their `pacman.conf` can easily create it on their own.

## Any

"Any" repositories are architecture-independent. In other words, they can be used on both i686 and x86_64 systems.

### Signed

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

#### youtube-dl

*   **Maintainer:** [Case_Of](https://bbs.archlinux.org/profile.php?id=94876)
*   **Description:** A repository for latest release of youtube-dl package.
*   **Key-ID:** 9F213FB2

**Note:** Install the package with `pacman -S youtube-dl/youtube-dl`.

```
[youtube-dl]
Server = http://youtube-dl.tk

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
Server = ftp://repo.arcanis.me/repo/$arch

```

(It is also available via HTTP with the same url.)

#### arch-openrc

*   **Maintainer:** [Chris Cromer](https://bbs.archlinux.org/profile.php?id=84785)
*   **Description:** Packages to install and maintain OpenRC with sysvinit for Arch Linux.
*   **Upstream sources page:** [https://github.com/cromerc/packages-openrc](https://github.com/cromerc/packages-openrc)
*   **Upstream packages/ISO page:** [https://sourceforge.net/projects/archopenrc/files/arch-openrc/](https://sourceforge.net/projects/archopenrc/files/arch-openrc/)
*   **Key-ID:** 97BEEEC2

```
[arch-openrc]
Server = http://downloads.sourceforge.net/project/archopenrc/$repo/$arch

```

#### archlinuxcn

*   **Maintainers:** [Phoenix Nemo (phoenixlzx)](https://plus.google.com/+PhoenixNemo/), Felix Yan (felixonmars, TU), [lilydjwg](https://twitter.com/lilydjwg), and others
*   **Description:** Packages by the Chinese Arch Linux community (mostly signed)
*   **Git Repo:** [https://github.com/archlinuxcn/repo](https://github.com/archlinuxcn/repo)
*   **Mirrors:** [https://github.com/archlinuxcn/mirrorlist-repo](https://github.com/archlinuxcn/mirrorlist-repo) (Mostly for users in mainland China)
*   **Key-ID:** Once the repo is added, *archlinuxcn-keyring* package must be installed before any other so you do not get errors about PGP signatures.

```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://repo.archlinuxcn.org/$arch
## or use a CDN (beta)
#Server = https://cdn.repo.archlinuxcn.org/$arch

```

#### blackeagle-pre-community

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** testing of the by me maintaned packages before moving to *community* repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[blackeagle-pre-community]
Server = http://repo.herecura.be/$repo/$arch

```

#### catalyst

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Upstream Page:** [http://catalyst.wirephire.com](http://catalyst.wirephire.com)
*   **Key-ID:** 653C3094

```
[catalyst]
Server = http://mirror.hactar.bz/Vi0L0/catalyst/$arch

```

#### catalyst-hd234k

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Upstream Page:** [http://catalyst.wirephire.com](http://catalyst.wirephire.com)
*   **Key-ID:** 653C3094

```
[catalyst-hd234k]
Server = http://mirror.hactar.bz/Vi0L0/catalyst-hd234k/$arch

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
Server = http://repo.herecura.be/$repo/$arch

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

```
[ivasilev]
Server = http://ivasilev.net/pacman/$arch

```

#### llvm-svn

*   **Maintainer:** [Luchesar V. ILIEV (kerberizer)](/index.php/User:Kerberizer "User:Kerberizer")
*   **Description:** [llvm-svn](https://aur.archlinux.org/pkgbase/llvm-svn) and [lib32-llvm-svn](https://aur.archlinux.org/pkgbase/lib32-llvm-svn) from AUR: the LLVM compiler infrastructure, the Clang frontend, and the tools associated with it
*   **Key-ID:** [0x76563F75679E4525](https://sks-keyservers.net/pks/lookup?op=vindex&search=0x76563F75679E4525&fingerprint=on&exact=on), fingerprint `D16C F22D 27D1 091A 841C 4BE9 7656 3F75 679E 4525`

```
[llvm-svn]
Server = http://repos.uni-plovdiv.net/archlinux/$repo/$arch

```

#### nuvolaplayer

*   **Maintainer:** [Patrick Burroughs (Celti) <celti@celti.name>](https://www.celti.name/)
*   **Description:** Packages for the [Nuvola Player](https://tiliado.eu/nuvolaplayer) cloud music player and its various integrations. Includes both stable and git versions. The [build scripts](https://repo.celti.name/nuvolaplayer/) used to manage the repository (using makepkg-template, makechrootpkg, and repose) are available. Both the packages and the database are signed.
*   **Key-ID:** `[123C 3F8B 058A 707F 8664 3316 FA68 2BD8 910C F4EA](https://sks-keyservers.net/pks/lookup?op=vindex&search=0x123C3F8B058A707F86643316FA682BD8910CF4EA)`

```
[nuvolaplayer]
Server = https://repo.celti.name/archlinux/$repo/$arch

```

#### miffe

*   **Maintainer:** [miffe](https://bbs.archlinux.org/profile.php?id=4059)
*   **Description:** AUR packages maintained by miffe, e.g. linux-mainline
*   **Key ID:** 313F5ABD

```
[miffe]
Server = http://arch.miffe.org/$arch/

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

#### seiichiro

*   **Maintainer:** [Stefan Brand (seiichiro0185)](https://www.seiichiro0185.org)
*   **Description:** AUR-packages I use frequently
*   **Key-ID:** 805517CC

```
[seiichiro]
Server = http://www.seiichiro0185.org/repo/$arch

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

#### Webkit2Gtk-unstable

*   **Maintainer:** [Mariusz Wojcik](/index.php/User:Mrmariusz "User:Mrmariusz")
*   **Description:** Latest Webkit2Gtk build for early adopters.
*   **Upstream Page:** [https://webkitgtk.org/](https://webkitgtk.org/)
*   **Key-ID:** 346854B5

```
[home_mrmariusz_ArchLinux]
Server = http://download.opensuse.org/repositories/home:/mrmariusz/ArchLinux/$arch

```

### Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

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

#### heftig

*   **Maintainer:** [Jan Steffens](https://www.archlinux.org/trustedusers/#heftig)
*   **Description:** Includes pulseaudio-git, pavucontrol-git, and firefox-developer-edition
*   **Upstream page:** [https://bbs.archlinux.org/viewtopic.php?id=117157](https://bbs.archlinux.org/viewtopic.php?id=117157)

```
[heftig]
Server = http://pkgbuild.com/~heftig/repo/$arch

```

#### home_Minerva_W_Science_Arch_Extra

*   **Maintainer:**
*   **Description:** [OpenFOAM](/index.php/OpenFOAM "OpenFOAM") packages.

```
[home_Minerva_W_Science_Arch_Extra]
SigLevel = Never
Server = http://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/$arch 

```

#### mesa-git

*   **Maintainer:** [Laurent Carlier](https://www.archlinux.org/people/trusted-users/#lcarlier)
*   **Description:** Mesa git builds for the *testing* and *multilib-testing* repositories

```
[mesa-git]
Server = http://pkgbuild.com/~lcarlier/$repo/$arch

```

#### noware

*   **Maintainer:** Alexandru Thirtheu (alex_giusi_tiri2@yahoo.com) ([Forums](https://bbs.archlinux.org/profile.php?id=65036)) ([Wiki](/index.php?title=User:AGT&action=edit&redlink=1 "User:AGT (page does not exist)")) ([Web Site](http://direct.noware.systems.:2))
*   **Description:** Software which I prefer being present in a repository, than being compiled each time. It eases software maintenance, I find. Almost anything goes.

```
[noware]
Server = http://direct.$repo.systems.:2/repository/arch/$arch

```

#### openrc-eudev

*   **Maintainer:** [nous](/index.php/User:Nous "User:Nous")
*   **Description:** OpenRC init system, initscripts, eudev and nosystemd packages from the AUR.
*   **Upstream page:** [https://sourceforge.net/projects/archopenrc](https://sourceforge.net/projects/archopenrc)
*   **Upstream sources:** [https://github.com/cromerc/arch-openrc](https://github.com/cromerc/arch-openrc), [https://github.com/cromerc/arch-nosystemd](https://github.com/cromerc/arch-nosystemd) and the AUR

```
[openrc-eudev]
Server=http://downloads.sourceforge.net/project/archopenrc/$repo/$arch
Server=ftp://ftp.heanet.ie/mirrors/sourceforge/a/ar/archopenrc/$repo/$arch

```

#### pantheon

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/trustedusers/#alucryd)
*   **Description:** Repository containing Pantheon-related packages

```
[pantheon]
Server = http://pkgbuild.com/~alucryd/$repo/$arch

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

#### trinity

*   **Maintainer:** [Michael Manley](/index.php?title=User:Mmanley&action=edit&redlink=1 "User:Mmanley (page does not exist)")
*   **Description:** [Trinity](/index.php/Trinity "Trinity") Desktop Environment

```
[trinity]
Server = http://repo.nasutek.com/arch/contrib/trinity/$arch

```

#### home_tarakbumba_archlinux_Arch_Extra_standard

*   **Maintainer:**
*   **Description:** Contains a few pre-built AUR packages (zemberek, etc.)

```
[home_tarakbumba_archlinux_Arch_Extra_standard]
Server = http://download.opensuse.org/repositories/home:/tarakbumba:/archlinux/Arch_Extra_standard/$arch

```

#### QOwnNotes

*   **Maintainer:** [http://www.qownnotes.org](http://www.qownnotes.org)
*   **Description:** QOwnNotes is a open source notepad and todo list manager with markdown support and [ownCloud](/index.php/OwnCloud "OwnCloud") integration.

```
[home_pbek_QOwnNotes_Arch_Extra]
SigLevel = Optional TrustAll
Server = http://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/$arch

```

## i686 only

### Signed

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

## x86_64 only

### Signed

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

#### infinality-bundle-multilib

*   **Maintainer:** [bohoomil](http://bohoomil.com/)
*   **Description:** infinality-bundle multilib repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle-multilib]
Server = http://bohoomil.com/repo/multilib/$arch

```

#### linux-kalterfx

*   **Maintainer**: Anna Ivanova ([kalterfive](https://aur.archlinux.org/account/kalterfive))
*   **Upstream page**: [https://deadsoftware.ru/files/linux-kalterfx](https://deadsoftware.ru/files/linux-kalterfx)
*   **Description**: A stable kernel with [pf-kernel](#Linux-pf), [reiser4](/index.php/Reiser4 "Reiser4") and smack
*   **Key-ID**: A0C04F15
*   **Keyfile**: [https://keybase.io/kalterfive/key.asc](https://keybase.io/kalterfive/key.asc)

```
[linux-kalterfx]
Server = https://deadsoftware.ru/files/linux-kalterfx/repo/$arch

```

#### nullptr_t

*   **Maintainers:** nullptr_t,
*   **Description:** Cherry-picked non-properitary packages and admin tools from AUR (e.g. [plymouth](/index.php/Plymouth "Plymouth"), nemo-extensions and a few more)
*   **Key-ID:** B4767A17CEC5B4E9

```
[nullptr_t]
Server = https://archlinux.0ptr.de/mirrors/$repo/$arch

```

#### markzz

*   **Maintainer:** [Mark Weiman (markzz)](/index.php/User:Markzz "User:Markzz")
*   **Description:** Packages that markzz maintains or uses on the AUR; this includes Linux with the vfio patchset ([linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) and [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)), and packages to maintain a Debian package repository.
*   **Sources:** [http://git.markzz.net/markzz/repositories/markzz.git/tree](http://git.markzz.net/markzz/repositories/markzz.git/tree)
*   **Key ID:** 3CADDFDD

**Note:** If you want to add the key by installing the *markzz-keyring* package, temporarily add `SigLevel = Never` into the repository section.

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
Server = http://pkgbuild.com/~anatolik/quarry/x86_64/

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
*   **Upstream page:** [http://andrwe.org/linux/repository](http://andrwe.org/linux/repository)

```
[andrwe]
Server = http://repo.andrwe.org/x86_64

```

#### brtln

*   **Maintainer:** [Bartłomiej Piotrowski](https://www.archlinux.org/trustedusers/#bpiotrowski)
*   **Description:** Some VCS packages.

```
[brtln]
Server = http://pkgbuild.com/~barthalion/brtln/$arch/

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

#### mikroskeem

*   **Maintainer:** mikroskeem <mikroskeem@mikroskeem.eu>
*   **Description:** Openarena, i3 wm, and neovim-related packages

```
[mikroskeem]
Server = https://nightsnack.cf/~mark/arch-pkgs

```

#### mingw-w64

*   **Maintainer:** [Philip](https://aur.archlinux.org/account/ant32) and [Jeromy](https://aur.archlinux.org/account/nic96) Reimer
*   **Description:** Almost all mingw-w64 packages in the AUR.

```
[mingw-w64]
Server = http://downloads.sourceforge.net/project/mingw-w64-archlinux/$arch
#Server = http://amr.linuxd.org/archlinux/$repo/os/$arch

```

#### pkgbuild-current

*   **Maintainer**: [Brenton Horne](https://fusion809.github.io) (fusion809)
*   **Description**: most of the packages in the [fusion809/PKGBUILDs](https://github.com/fusion809/PKGBUILDs) GitHub repository. Full list of packages can be found [here](https://github.com/fusion809/PKGBUILDs/releases/tag/current).
*   **Upstream page**: [https://fusion809.github.io/PKGBUILDs](https://fusion809.github.io/PKGBUILDs)

```
[pkgbuild-current]
Server = https://github.com/fusion809/PKGBUILDs/releases/download/current

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
Server = https://spider-mario.quantic-telecom.net/archlinux/$repo/$arch

```

#### rightlink

*   **Maintainer:** Chris Fordham <chris@fordham-nagy.id.au>
*   **Description:** RightLink version 10 (RL10) is a new version of RightScale's server agent that connects servers managed through RightScale to the RightScale cloud management platform.

```
[rightlink]
Server = https://s3-ap-southeast-2.amazonaws.com/archlinux.rightscale.me/repo

```

#### zrootfs

*   **Maintainer:** Isabell Cowan <isabellcowan@gmail.com>
*   **Description:** For Haswell and Broadwell architecture processors with size in mind (out of date 2016-03-14).

```
[zrootfs]
Server = http://www.izzette.com/izzi/zrootfs-old

```