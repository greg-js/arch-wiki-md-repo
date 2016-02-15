**翻译状态：** 本文是英文页面 [Unofficial_user_repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-14，点击[这里](https://wiki.archlinux.org/index.php?title=Unofficial_user_repositories&diff=0&oldid=330211)可以查看翻译后英文页面的改动。

这篇文章列出了由社区创建的自由共享二进制软件包的软件仓库，其中很多的包都是由[AUR](/index.php/AUR "AUR")中可以找到的PKGBUILD文件预编译打包而成。

**警告:** 无论Arch Linux的开发者还是授信用户都不会对这些软件仓库做任何的测试与验证。需要每一个用户自己决定是否信任这些软件仓库的维护者，并且对软件源维护者做出的任何决定导致的后果负责。

想要使用这些软件仓库，你需要把他们添加到 `/etc/pacman.conf`，详情请看 [pacman (简体中文)#软件仓库](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BD.AF.E4.BB.B6.E4.BB.93.E5.BA.93 "Pacman (简体中文)")。如果一个软件仓库进行了签名，你必须要在本地签署这些key，详见[Pacman-key (简体中文)#导入非官方密钥](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AF.BC.E5.85.A5.E9.9D.9E.E5.AE.98.E6.96.B9.E5.AF.86.E9.92.A5 "Pacman-key (简体中文)")。

如果你想自己建立一个软件仓库，请看 [pacman tips (简体中文)#自建本地仓库](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.87.AA.E5.BB.BA.E6.9C.AC.E5.9C.B0.E4.BB.93.E5.BA.93 "Pacman tips (简体中文)").

## Contents

*   [1 Adding your repository to this page](#Adding_your_repository_to_this_page)
*   [2 Any](#Any)
    *   [2.1 Signed](#Signed)
        *   [2.1.1 bioinformatics-any](#bioinformatics-any)
        *   [2.1.2 infinality-bundle-fonts](#infinality-bundle-fonts)
        *   [2.1.3 xyne-any](#xyne-any)
    *   [2.2 Unsigned](#Unsigned)
        *   [2.2.1 archlinuxgr-any](#archlinuxgr-any)
*   [3 Both i686 and x86_64](#Both_i686_and_x86_64)
    *   [3.1 Signed](#Signed_2)
        *   [3.1.1 arcanisrepo](#arcanisrepo)
        *   [3.1.2 archlinuxcn](#archlinuxcn)
        *   [3.1.3 atom-editor-git](#atom-editor-git)
        *   [3.1.4 bbqlinux](#bbqlinux)
        *   [3.1.5 catalyst](#catalyst)
        *   [3.1.6 catalyst-hd234k](#catalyst-hd234k)
        *   [3.1.7 city](#city)
        *   [3.1.8 demz-repo-archiso](#demz-repo-archiso)
        *   [3.1.9 demz-repo-core](#demz-repo-core)
        *   [3.1.10 gnome-encfs-manager](#gnome-encfs-manager)
        *   [3.1.11 haskell-core](#haskell-core)
        *   [3.1.12 infinality-bundle](#infinality-bundle)
        *   [3.1.13 lxqt-git](#lxqt-git)
        *   [3.1.14 metalgamer](#metalgamer)
        *   [3.1.15 pipelight](#pipelight)
        *   [3.1.16 repo-ck](#repo-ck)
        *   [3.1.17 sergej-repo](#sergej-repo)
    *   [3.2 Unsigned](#Unsigned_2)
        *   [3.2.1 alucryd](#alucryd)
        *   [3.2.2 archaudio](#archaudio)
        *   [3.2.3 archie-repo](#archie-repo)
        *   [3.2.4 archlinuxfr](#archlinuxfr)
        *   [3.2.5 archlinuxgis](#archlinuxgis)
        *   [3.2.6 archlinuxgr](#archlinuxgr)
        *   [3.2.7 archlinuxgr-kde4](#archlinuxgr-kde4)
        *   [3.2.8 archstuff](#archstuff)
        *   [3.2.9 arsch](#arsch)
        *   [3.2.10 aurbin](#aurbin)
        *   [3.2.11 cinnamon](#cinnamon)
        *   [3.2.12 ede](#ede)
        *   [3.2.13 heftig](#heftig)
        *   [3.2.14 herecura-stable](#herecura-stable)
        *   [3.2.15 herecura-testing](#herecura-testing)
        *   [3.2.16 mesa-git](#mesa-git)
        *   [3.2.17 oracle](#oracle)
        *   [3.2.18 pantheon](#pantheon)
        *   [3.2.19 paulburton-fitbitd](#paulburton-fitbitd)
        *   [3.2.20 pfkernel](#pfkernel)
        *   [3.2.21 suckless](#suckless)
        *   [3.2.22 unity](#unity)
        *   [3.2.23 unity-extra](#unity-extra)
        *   [3.2.24 home_tarakbumba_archlinux_Arch_Extra_standard](#home_tarakbumba_archlinux_Arch_Extra_standard)
*   [4 i686 only](#i686_only)
    *   [4.1 Signed](#Signed_3)
        *   [4.1.1 eee-ck](#eee-ck)
        *   [4.1.2 xyne-i686](#xyne-i686)
    *   [4.2 Unsigned](#Unsigned_3)
        *   [4.2.1 andrwe](#andrwe)
        *   [4.2.2 esclinux](#esclinux)
        *   [4.2.3 kpiche](#kpiche)
        *   [4.2.4 kernel26-pae](#kernel26-pae)
        *   [4.2.5 linux-pae](#linux-pae)
        *   [4.2.6 rfad](#rfad)
        *   [4.2.7 studioidefix](#studioidefix)
*   [5 x86_64 only](#x86_64_only)
    *   [5.1 Signed](#Signed_4)
        *   [5.1.1 apathism](#apathism)
        *   [5.1.2 bioinformatics](#bioinformatics)
        *   [5.1.3 boyska64](#boyska64)
        *   [5.1.4 coderkun-aur](#coderkun-aur)
        *   [5.1.5 coderkun-aur-audio](#coderkun-aur-audio)
        *   [5.1.6 coderkun-aur-nonfree](#coderkun-aur-nonfree)
        *   [5.1.7 freifunk-rheinland](#freifunk-rheinland)
        *   [5.1.8 heimdal](#heimdal)
        *   [5.1.9 infinality-bundle-multilib](#infinality-bundle-multilib)
        *   [5.1.10 siosm-aur](#siosm-aur)
        *   [5.1.11 siosm-selinux](#siosm-selinux)
        *   [5.1.12 subtitlecomposer](#subtitlecomposer)
        *   [5.1.13 xyne-x86_64](#xyne-x86_64)
        *   [5.1.14 quarry](#quarry)
    *   [5.2 Unsigned](#Unsigned_4)
        *   [5.2.1 andrwe](#andrwe_2)
        *   [5.2.2 archstudio](#archstudio)
        *   [5.2.3 brtln](#brtln)
        *   [5.2.4 hawaii](#hawaii)
        *   [5.2.5 kps](#kps)
        *   [5.2.6 miusystem](#miusystem)
        *   [5.2.7 pnsft-pur](#pnsft-pur)
        *   [5.2.8 mingw-w64](#mingw-w64)
        *   [5.2.9 rightscale](#rightscale)
        *   [5.2.10 seiichiro](#seiichiro)
        *   [5.2.11 studioidefix](#studioidefix_2)
        *   [5.2.12 zen](#zen)
        *   [5.2.13 mazdlc](#mazdlc)
        *   [5.2.14 mazdlc-deadbeef-plugins](#mazdlc-deadbeef-plugins)
        *   [5.2.15 mazdlc-kde-frameworks-5](#mazdlc-kde-frameworks-5)
*   [6 armv6h only](#armv6h_only)
    *   [6.1 Unsigned](#Unsigned_5)
        *   [6.1.1 arch-fook-armv6h](#arch-fook-armv6h)

## Adding your repository to this page

**注意:** 本文为[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")的翻译，添加自己的仓库，请移步[英文原始页面](/index.php/Unofficial_user_repositories "Unofficial user repositories")。

如果你有自己的仓库，请添加到本页面中，这样其他用户就会知道哪里去找你的软件。 在添加新的仓库时请保持队形，并遵守下列规则：

*   请按罗马字首排序列表。
*   包含维护者的一些信息：包括至少一个名字（昵称也行）以及一些具有联系方式的信息（网址，邮箱，用户ArchWiki页面或者论坛帖子等等）。
*   如果仓库是签名的，请添加一个key-id，最好把它编辑成一个链到密匙服务器的连接，直接连到密钥文件上。
*   包含一些简短的描述（软件包的分类什么的）
*   如果你有一个介绍性的网页（无论是ArchWiki或者其他网站），请添加一个连接。
*   If possible, avoid using comments in code blocks. The formatted description is much more readable. Users who want some comments in their `pacman.conf` can easily create it on their own.

## Any

"Any" 表示与系统架构无关。也就是说可以同时运行于 i686 和 x86_64 系统中。

### Signed

#### bioinformatics-any

*   **维护者** [decryptedepsilon](https://aur.archlinux.org/account/decryptedepsilon/)
*   **描述：** A repository containing some python packages and genome browser for Bioinformatics
*   **Key-ID:** 60442BA4

```
[bioinformatics-any]
Server = http://decryptedepsilon.bl.ee/repo/any

```

#### infinality-bundle-fonts

*   **维护者** [bohoomil](http://bohoomil.com/)
*   **描述：** infinality-bundle-fonts repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle-fonts]
Server = http://bohoomil.com/repo/fonts

```

#### xyne-any

*   **维护者** [Xyne](https://www.archlinux.org/trustedusers/#xyne)
*   **描述：** A repository for Xyne's own projects containing packages for "any" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not needed, as maintainer is a TU

**Note:** Use this repository only if there is no matching `[xyne-*]` repository for your architecture.

```
[xyne-any]
Server = http://xyne.archlinux.ca/repos/xyne

```

### Unsigned

#### archlinuxgr-any

*   **维护者**
*   **描述：** The Hellenic (Greek) unofficial Arch Linux repository with many interesting packages.

```
[archlinuxgr-any]
Server = http://archlinuxgr.tiven.org/archlinux/any

```

## Both i686 and x86_64

Repositories with both i686 and x86_64 versions. The `$arch` variable will be set automatically by pacman.

### Signed

#### arcanisrepo

*   **维护者** [arcanis](https://www.archlinux.org/trustedusers/#arcanis)
*   **描述：** A repository with some AUR packages including packages from VCS
*   **Key-ID:** Not needed, as maintainer is a TU

```
[arcanisrepo]
Server = ftp://repo.arcanis.name/repo/$arch

```

#### archlinuxcn

*   **维护者:** [Phoenix Nemo (phoenixlzx)](https://plus.google.com/+PhoenixNemo/), Felix Yan (felixonmars, TU), [lilydjwg](https://twitter.com/lilydjwg), and others
*   **描述：** The Chinese Arch Linux communities packages.
*   **Git Repo:** [https://github.com/archlinuxcn/repo](https://github.com/archlinuxcn/repo)
*   **镜像:** [https://github.com/archlinuxcn/mirrorlist-repo](https://github.com/archlinuxcn/mirrorlist-repo)
*   **Key-ID:** 添加 archlinuxcn 源之后，必须先安装 “archlinuxcn-keyring” 钥匙环，之后才可以安装任何其它包。

```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://repo.archlinuxcn.org/$arch

```

#### atom-editor-git

*   **维护者** Matthew Stobbs
*   **Upstream page:** [https://atom.io/](https://atom.io/)
*   **描述：** The Atom Editor, created by the people behind github, to mimic Sublime Text.
*   **Key-ID:** 26EBCC57

```
[atom-editor-git]
Server = http://repo.stobbstechnical.com/$arch

```

#### bbqlinux

*   **维护者** [Daniel Hillenbrand](https://plus.google.com/u/0/+DanielHillenbrand/about)
*   **描述：** Packages for Android Development
*   **Upstream Page:** [http://bbqlinux.org/](http://bbqlinux.org/)
*   **Key-ID:** Get the bbqlinux-keyring package, as it contains the needed keys.

```
[bbqlinux]
Server = http://packages.bbqlinux.org/$arch

```

#### catalyst

*   **维护者** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **描述：** ATI Catalyst proprietary drivers.
*   **Upstream Page:** [http://catalyst.wirephire.com](http://catalyst.wirephire.com)
*   **Key-ID:** 653C3094

```
[catalyst]
Server = http://catalyst.wirephire.com/repo/catalyst/$arch
## Mirrors, if the primary server does not work or is too slow:
#Server = http://70.239.162.206/catalyst-mirror/repo/catalyst/$arch
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/catalyst/$arch
#Server = http://mirror.hactar.bz/Vi0L0/catalyst/$arch

```

#### catalyst-hd234k

*   **维护者** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **描述：** ATI Catalyst proprietary drivers.
*   **Upstream Page:** [http://catalyst.wirephire.com](http://catalyst.wirephire.com)
*   **Key-ID:** 653C3094

```
[catalyst-hd234k]
Server = http://catalyst.wirephire.com/repo/catalyst-hd234k/$arch
## Mirrors, if the primary server does not work or is too slow:
#Server = http://70.239.162.206/catalyst-mirror/repo/catalyst-hd234k/$arch
#Server = http://mirror.rts-informatique.fr/archlinux-catalyst/repo/catalyst-hd234k/$arch
#Server = http://mirror.hactar.bz/Vi0L0/catalyst-hd234k/$arch

```

#### city

*   **维护者** [Balló György](https://www.archlinux.org/trustedusers/#bgyorgy)
*   **描述：** Experimental/unpopular packages.
*   **Upstream page:** [http://pkgbuild.com/~bgyorgy/city.html](http://pkgbuild.com/~bgyorgy/city.html)
*   **Key-ID:** Not needed, as maintainer is a TU

```
[city]
Server = http://pkgbuild.com/~bgyorgy/$repo/os/$arch

```

#### demz-repo-archiso

*   **维护者** [Jesus Alvarez (demizer)](http://demizerone.com)
*   **描述：** Packages for installing ZFS from an Arch ISO live disk
*   **Upstream page:** [https://github.com/demizer/archzfs](https://github.com/demizer/archzfs)
*   **Key-ID:** 0EE7A126

#### demz-repo-core

*   **维护者** [Jesus Alvarez (demizer)](http://demizerone.com)
*   **描述：** Packages for ZFS on Arch Linux.
*   **Upstream page:** [https://github.com/demizer/archzfs](https://github.com/demizer/archzfs)
*   **Key-ID:** 0EE7A126

```
[demz-repo-core]
Server = http://demizerone.com/$repo/$arch

```

```
[demz-repo-archiso]
Server = http://demizerone.com/$repo/$arch

```

#### gnome-encfs-manager

*   **维护者** Moritz Molch
*   **描述：** The gnome-encfs-manager can be used to integrate [EncFS](/index.php/EncFS "EncFS")
*   **Upstream page:** [Gnome EncfsM](https://launchpad.net/gencfsm).
*   **Key ID:**

```
[home_moritzmolch_gencfsm_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/moritzmolch:/gencfsm/Arch_Extra/$arch

```

#### haskell-core

*   **维护者** Magnus Therning
*   **描述：** Arch-Haskell repository
*   **Upstream page:** [https://github.com/archhaskell/habs](https://github.com/archhaskell/habs)
*   **Key-ID:** 4209170B

```
[haskell-core]
Server = http://xsounds.org/~haskell/core/$arch

```

#### infinality-bundle

*   **维护者** [bohoomil](http://bohoomil.com/)
*   **描述：** infinality-bundle main repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle]
Server = http://bohoomil.com/repo/$arch

```

#### lxqt-git

*   **维护者** [stobbsm](http://www.stobbstechnical.com/)
*   **描述：** lxqt-git weekly build repository
*   **Key-ID:** 26EBCC57

```
[lxqt-git]
Server = http://repo.stobbstechnical.com/$arch

```

#### metalgamer

*   **维护者** [metalgamer](http://metalgamer.eu/)
*   **描述：** Packages I use and/or maintain on the AUR.
*   **Key ID:** F55313FB

```
[metalgamer]
Server = http://repo.metalgamer.eu/$arch

```

#### pipelight

*   **维护者**
*   **描述：** Pipelight and wine-compholio
*   **Upstream page:** [fds-team.de](http://fds-team.de/)
*   **Key-ID:** E49CC0415DC2D5CA
*   **Keyfile:** [http://repos.fds-team.de/Release.key](http://repos.fds-team.de/Release.key)

```
[pipelight]
Server = http://repos.fds-team.de/stable/arch/$arch
```

#### repo-ck

*   **维护者** [graysky](/index.php/User:Graysky "User:Graysky")
*   **描述：** Kernel and modules with Brain Fuck Scheduler and all the goodies in the ck1 patch set.
*   **Upstream page:** [repo-ck.com](http://repo-ck.com)
*   **Wiki:** [repo-ck](/index.php/Repo-ck "Repo-ck")
*   **Key-ID:** 5EE46C4C

```
[repo-ck]
Server = http://repo-ck.com/$arch

```

#### sergej-repo

*   **维护者** [Sergej Pupykin](https://www.archlinux.org/trustedusers/#spupykin)
*   **描述：** psi-plus, owncloud-git, ziproxy, android, MySQL, and other stuff. Some packages also available for armv7h.
*   **Key-ID:** Not required, as maintainer is a TU

```
[sergej-repo]
Server = http://repo.p5n.pp.ru/$repo/os/$arch

```

### Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

#### alucryd

*   **维护者** [Maxime Gauduin](https://www.archlinux.org/trustedusers/#alucryd)
*   **描述：** Repository containing various packages Maxime Gauduin maintains (or not) in the AUR.

```
[alucryd]
Server = http://pkgbuild.com/~alucryd/$repo/$arch

```

#### archaudio

*   **维护者** [Ray Rashif](/index.php/User:Schivmeister "User:Schivmeister"), [Joakim Hernberg](https://aur.archlinux.org/account/jhernberg)
*   **描述：** Pro-audio packages

```
[archaudio-production]
Server = http://repos.archaudio.org/$repo/$arch

```

#### archie-repo

*   **维护者** [Kalinda](https://aur.archlinux.org/account/Kalinda/)
*   **描述：** Repo for wine-silverlight, pipelight, and some misc packages.

```
[archie-repo]
Server = http://andontie.net/archie-repo/$arch

```

#### archlinuxfr

*   **维护者**
*   **描述：**
*   **Upstream page:** [http://afur.archlinux.fr](http://afur.archlinux.fr)

```
[archlinuxfr]
Server = http://repo.archlinux.fr/$arch

```

#### archlinuxgis

*   **维护者**
*   **描述：** Maintainers needed - low bandwidth

```
[archlinuxgis]
Server = http://archlinuxgis.no-ip.org/$arch

```

#### archlinuxgr

*   **维护者**
*   **描述：**

```
[archlinuxgr]
Server = http://archlinuxgr.tiven.org/archlinux/$arch

```

#### archlinuxgr-kde4

*   **维护者**
*   **描述：** KDE4 packages (plasmoids, themes etc) provided by the Hellenic (Greek) Arch Linux community

```
[archlinuxgr-kde4]
Server = http://archlinuxgr.tiven.org/archlinux-kde4/$arch

```

#### archstuff

**Note:** Off-line since 2014-01-06.

*   **维护者**
*   **描述：** AUR's most voted and many bin32-* and lib32-* packages.

```
[archstuff]
Server = http://archstuff.vs169092.vserver.de/$arch

```

#### arsch

*   **维护者**
*   **描述：** From users of orgizm.net

```
[arsch]
Server = http://arsch.orgizm.net/$arch

```

#### aurbin

*   **维护者**
*   **描述：** Automated build of AUR packages
*   **Upstream page:** [http://aurbin.net/](http://aurbin.net/)

```
[aurbin]
Server = http://aurbin.net/$arch

```

#### cinnamon

*   **维护者** [jnbek](https://github.com/jnbek)
*   **描述：** Stable and actively developed Cinnamon packages (Applets, Themes, Extensions), plus others (Hotot, qBitTorrent, GTK themes, Perl modules, and more).

```
[cinnamon]
Server = http://archlinux.zoelife4u.org/cinnamon/$arch

```

#### ede

*   **维护者**
*   **描述：** Equinox Desktop Environment repository

```
[ede]
Server = http://ede.elderlinux.org/repos/archlinux/$arch

```

#### heftig

*   **维护者** [Jan Steffens](https://www.archlinux.org/trustedusers/#heftig)
*   **描述：** Includes linux-zen and aurora (Firefox development build - works alongside [firefox](https://www.archlinux.org/packages/?name=firefox) in the _extra_ repository).
*   **Upstream page:** [https://bbs.archlinux.org/viewtopic.php?id=117157](https://bbs.archlinux.org/viewtopic.php?id=117157)

```
[heftig]
Server = http://pkgbuild.com/~heftig/repo/$arch

```

#### herecura-stable

*   **维护者**
*   **描述：** additional packages not found in the _community_ repository

```
[herecura-stable]
Server = http://repo.herecura.be/herecura-stable/$arch

```

#### herecura-testing

*   **维护者**
*   **描述：** additional packages for testing build against stable arch

```
[herecura-testing]
Server = http://repo.herecura.be/herecura-testing/$arch

```

#### mesa-git

*   **维护者**
*   **描述：** Mesa git builds for the _testing_ and _multilib-testing_ repositories

```
[mesa-git]
Server = http://pkgbuild.com/~lcarlier/$repo/$arch

```

#### oracle

*   **维护者**
*   **描述：** Oracle database client

**Warning:** By adding this you are agreeing to the Oracle license at [http://www.oracle.com/technetwork/licenses/instant-client-lic-152016.html](http://www.oracle.com/technetwork/licenses/instant-client-lic-152016.html)

```
[oracle]
Server = http://linux.shikadi.net/arch/$repo/$arch/

```

#### pantheon

*   **维护者** [Maxime Gauduin](https://www.archlinux.org/trustedusers/#alucryd)
*   **描述：** Repository containing Pantheon-related packages

```
[pantheon]
Server = http://pkgbuild.com/~alucryd/$repo/$arch

```

#### paulburton-fitbitd

*   **维护者**
*   **描述：** Contains fitbitd for synchronizing FitBit trackers

```
[paulburton-fitbitd]
Server = http://www.paulburton.eu/arch/fitbitd/$arch

```

#### pfkernel

*   **维护者** [nous](/index.php/User:Nous "User:Nous")
*   **描述：** Generic and optimized binaries of the ARCH kernel patched with BFS, TuxOnIce, BFQ, Aufs3, linux-pf, kernel26-pf, gdm-old, nvidia-pf, nvidia-96xx, xchat-greek, arora-git
*   **Note:** To browse through the repository, one needs to append `index.html` after the server URL (this is an intentional quirk of Dropbox). For example, for x86_64, point your browser to [http://dl.dropbox.com/u/11734958/x86_64/index.html](http://dl.dropbox.com/u/11734958/x86_64/index.html) or start at [http://tiny.cc/linux-pf](http://tiny.cc/linux-pf)

```
[pfkernel]
Server = http://dl.dropbox.com/u/11734958/$arch

```

#### suckless

*   **维护者**
*   **描述：** suckless.org packages

```
[suckless]
Server = http://dl.suckless.org/arch/$arch

```

#### unity

*   **维护者**
*   **描述：** unity packages for Arch

```
[unity]
Server = http://unity.xe-xe.org/$arch

```

#### unity-extra

*   **维护者**
*   **描述：** unity extra packages for Arch

```
[unity-extra]
Server = http://unity.xe-xe.org/extra/$arch

```

#### home_tarakbumba_archlinux_Arch_Extra_standard

*   **维护者**
*   **描述：** Contains a few pre-built AUR packages (zemberek, firefox-kde-opensuse, etc.)

```
[home_tarakbumba_archlinux_Arch_Extra_standard]
Server = http://download.opensuse.org/repositories/home:/tarakbumba:/archlinux/Arch_Extra_standard/$arch

```

## i686 only

### Signed

#### eee-ck

*   **维护者** Gruppenpest
*   **描述：** Kernel and modules optimized for Asus Eee PC 701, with -ck patchset.
*   **Key-ID:** 27D4A19A
*   **Keyfile** [http://zembla.frozenslumber.com/repo/gruppenpest.gpg](http://zembla.frozenslumber.com/repo/gruppenpest.gpg)

```
[eee-ck]
Server = http://zembla.frozenslumber.com/repo

```

#### xyne-i686

*   **维护者** [Xyne](https://www.archlinux.org/trustedusers/#xyne)
*   **描述：** A repository for Xyne's own projects containing packages for the "i686" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** This includes all packages in [[xyne-any]](#xyne-any).

```
[xyne-i686]
Server = http://xyne.archlinux.ca/repos/xyne

```

### Unsigned

#### andrwe

*   **维护者** Andrwe Lord Weber
*   **描述：** each program I'm using on x86_64 is compiled for i686 too
*   **Upstream page:** [http://andrwe.org/linux/repository](http://andrwe.org/linux/repository)

```
[andrwe]
Server = http://repo.andrwe.org/i686

```

#### esclinux

**Note:** Off-line since 2014-07-02.

*   **维护者**
*   **描述：** Mostly games, interactive fiction, and abc notation stuff already on the AUR.

```
[esclinux]
Server = http://download.tuxfamily.org/esclinuxcd/ressources/repo/i686/

```

#### kpiche

*   **维护者**
*   **描述：** Stable OpenSync packages.

```
[kpiche]
Server = http://kpiche.archlinux.ca/repo

```

#### kernel26-pae

*   **维护者**
*   **描述：** PAE-enabled 32-bit kernel 2.6.39

```
[kernel26-pae]
Server = http://kernel26-pae.archlinux.ca/

```

#### linux-pae

*   **维护者**
*   **描述：** PAE-enabled 32-bit kernel 3.0

```
[linux-pae]
Server = http://pae.archlinux.ca/

```

#### rfad

*   **维护者** requiem [at] archlinux.us
*   **描述：** Repository made by haxit

```
[rfad]
Server = http://web.ncf.ca/ey723/archlinux/repo/

```

#### studioidefix

*   **维护者**
*   **描述：** Precompiled boxee packages.

```
[studioidefix]
Server = http://studioidefix.googlecode.com/hg/repo/i686

```

## x86_64 only

### Signed

#### apathism

*   **维护者** Koryabkin Ivan ([apathism](https://aur.archlinux.org/account/apathism/))
*   **Upstream page:** [https://apathism.net/](https://apathism.net/)
*   **描述：** AUR packages that would take long to build, such as [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/).
*   **Key-ID:** 3E37398D
*   **Keyfile:** [http://apathism.net/archlinux/apathism.key](http://apathism.net/archlinux/apathism.key)

```
[apathism]
Server = http://apathism.net/archlinux/

```

#### bioinformatics

*   **维护者** [decryptedepsilon](https://aur.archlinux.org/account/decryptedepsilon/)
*   **描述：** A repository containing some software tools for Bioinformatics
*   **Key-ID:** 60442BA4

```
[bioinformatics]
Server = http://decryptedepsilon.bl.ee/repo/x86_64

```

#### boyska64

*   **维护者** boyska
*   **描述：** Personal repository: cryptography, sdr, mail handling and misc
*   **Key-ID:** 0x7395DCAE58289CA9

```
[boyska64]
Server = http://boyska.s.pt-labs.net/archrepo

```

#### coderkun-aur

*   **维护者** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **描述：** AUR packages with random software.
*   **Key-ID:** A6BEE374
*   **Keyfile:** [http://arch.coderkun.de/coderkun.asc](http://arch.coderkun.de/coderkun.asc)

```
[coderkun-aur]
Server = http://arch.coderkun.de/$repo/$arch/

```

#### coderkun-aur-audio

*   **维护者** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **描述：** AUR packages with audio-related (realtime kernels, lv2-plugins, …) software.
*   **Key-ID:** A6BEE374
*   **Keyfile:** [http://arch.coderkun.de/coderkun.asc](http://arch.coderkun.de/coderkun.asc)

```
[coderkun-aur-audio]
Server = http://arch.coderkun.de/$repo/$arch/

```

#### coderkun-aur-nonfree

*   **维护者** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **描述：** AUR packages with proprietary (dropbox, nvidia, …) software.
*   **Key-ID:** A6BEE374
*   **Keyfile:** [http://arch.coderkun.de/coderkun.asc](http://arch.coderkun.de/coderkun.asc)

```
[coderkun-aur-nonfree]
Server = http://arch.coderkun.de/$repo/$arch/

```

#### freifunk-rheinland

*   **维护者** nomaster
*   **描述：** Packages for the Freifunk project: batman-adv, batctl, fastd and dependencies.

```
[freifunk-rheinland]
Server = http://mirror.fluxent.de/archlinux-custom/$repo/os/$arch

```

#### heimdal

**Note:** Offline since 2014-03-06.

*   **维护者**
*   **描述：** Packages are compiled against Heimdal instead of MIT KRB5\. Meant to be dropped before `[core]` in `pacman.conf`. All packages are signed.
*   **Upstream page:** [https://github.com/Kiwilight/Heimdal-Pkgbuilds](https://github.com/Kiwilight/Heimdal-Pkgbuilds)

**Warning:** Be careful. Do not use this unless you know what you are doing because many of these packages override packages from the _core_ and _extra_ repositories

```
[heimdal]
Server = http://www.kiwilight.com/heimdal/$arch/

```

#### infinality-bundle-multilib

*   **维护者** [bohoomil](http://bohoomil.com/)
*   **描述：** infinality-bundle multilib repository.
*   **Upstream page:** [Infinality bundle & fonts](http://bohoomil.com/)
*   **Key-ID:** 962DDE58

```
[infinality-bundle-multilib]
Server = http://bohoomil.com/repo/multilib/$arch

```

#### siosm-aur

*   **维护者** [Timothee Ravier](https://tim.siosm.fr/about/)
*   **描述：** packages also available in the Arch User Repository, sometimes with minor fixes
*   **Upstream page:** [https://tim.siosm.fr/repositories/](https://tim.siosm.fr/repositories/)
*   **Key-ID:** 78688F83

```
[siosm-aur]
Server = http://repo.siosm.fr/$repo/

```

#### siosm-selinux

*   **维护者** [Timothee Ravier](https://tim.siosm.fr/about/)
*   **描述：** packages required for SELinux support – work in progress (notably, missing an Arch Linux-compatible SELinux policy). See the [SELinux](/index.php/SELinux "SELinux") page for details.
*   **Upstream page:** [https://tim.siosm.fr/repositories/](https://tim.siosm.fr/repositories/)
*   **Key-ID:** 78688F83

```
[siosm-selinux]
Server = http://repo.siosm.fr/$repo/

```

#### subtitlecomposer

*   **维护者** Mladen Milinkovic (maxrd2)
*   **描述：** Subtitle Composer stable and nightly builds
*   **Upstream page:** [https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer)
*   **Key-ID:** EA8CEBEE

```
[subtitlecomposer]
Server = http://smoothware.net/$repo/$arch

```

#### xyne-x86_64

*   **维护者** [Xyne](https://www.archlinux.org/trustedusers/#xyne)
*   **描述：** A repository for Xyne's own projects containing packages for the "x86_64" architecture.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

**Note:** This includes all packages in [[xyne-any]](#xyne-any).

```
[xyne-x86_64]
Server = http://xyne.archlinux.ca/repos/xyne

```

#### quarry

*   **维护者** [anatolik](https://www.archlinux.org/developers/#anatolik)
*   **描述：** Arch binary repository for [Rubygems](http://rubygems.org/) packages. See [forum announcement](https://bbs.archlinux.org/viewtopic.php?id=182729) for more information.
*   **Key-ID:** Not needed, as maintainer is a developer

```
[quarry]
Server = http://pkgbuild.com/~anatolik/quarry/x86_64/

```

### Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

#### andrwe

*   **维护者** Andrwe Lord Weber
*   **描述：** contains programs I'm using on many systems
*   **Upstream page:** [http://andrwe.dyndns.org/doku.php/blog/repository](http://andrwe.dyndns.org/doku.php/blog/repository) 

```
[andrwe]
Server = http://repo.andrwe.org/x86_64

```

#### archstudio

*   **维护者**
*   **描述：** Audio and Music Packages optimized for Intel Core i3, i5, and i7.
*   **Upstream page:** [http://www.xsounds.org/~archstudio](http://www.xsounds.org/~archstudio)

```
[archstudio]
Server = http://www.xsounds.org/~archstudio/x86_64

```

#### brtln

*   **维护者** [Bartłomiej Piotrowski](https://www.archlinux.org/trustedusers/#bpiotrowski)
*   **描述：** Some VCS packages.

```
[brtln]
Server = http://pkgbuild.com/~barthalion/brtln/$arch/

```

#### hawaii

*   **维护者**
*   **描述：** hawaii Qt5/Wayland-based desktop environment
*   **Upstream page:** [http://www.maui-project.org/](http://www.maui-project.org/)

```
[hawaii]
Server = http://archive.maui-project.org/archlinux/$repo/os/$arch

```

#### kps

*   **维护者** kps
*   **描述：** gmt, catalyst-test, ttf-ms-win8, rstudio, meshlab, gcc-gcj, vlc-git, ffmpeg-git (k10 & intel opt.), docear, maperitive, libressl, bkchem ...

```
[kps]
Server = http://kps.bplaced.net/repo/$arch

```

#### miusystem

*   **维护者** Theodore Keloglou <theodore.keloglou@gmail.com>
*   **描述：** Packages that I use and might interest others

```
[miusystem]
Server = https://miusystem.com/archlinux-repo

```

#### pnsft-pur

*   **维护者**
*   **描述：** Japanese input method packages Mozc (vanilla) and libkkc

```
[pnsft-pur]
Server = http://downloads.sourceforge.net/project/pnsft-aur/pur/x86_64

```

#### mingw-w64

*   **维护者**
*   **描述：** Almost all mingw-w64 packages in the AUR updated every 8 hours.
*   **Upstream page:** [http://arch.linuxx.org](http://arch.linuxx.org)

```
[mingw-w64]
Server = http://downloads.sourceforge.net/project/mingw-w64-archlinux/$arch
Server = http://arch.linuxx.org/archlinux/$repo/os/$arch

```

#### rightscale

*   **维护者** Chris Fordham <chris@fordham-nagy.id.au>
*   **描述：** RightLink version 10 (RL10) is a new version of RightScale's server agent that connects servers managed through RightScale to the RightScale cloud management platform.

```
[rightscale]
Server = https://s3-ap-southeast-2.amazonaws.com/archlinux.rightscale.me/repo

```

#### seiichiro

*   **维护者**
*   **描述：** VDR and some plugins, mms, foo2zjs-drivers

```
[seiichiro]
Server = http://repo.seiichiro0185.org/x86_64

```

#### studioidefix

*   **维护者**
*   **描述：** Precompiled boxee packages.

```
[studioidefix]
Server = http://studioidefix.googlecode.com/hg/repo/x86_64

```

#### zen

**Note:** Offline since 2014-03-06.

*   **维护者**
*   **描述：** Various and zengeist AUR packages.

```
[zen]
Server = http://zloduch.cz/archlinux/x86_64

```

#### mazdlc

*   **维护者:** maz-1 <ohmygod19993 at gmail dot com>
*   **描述:** maz-1维护的多个软件包 (主要为基于Qt5的软件和多媒体相关软件)
*   **Upstream page:** [https://build.opensuse.org/project/show/home:mazdlc](https://build.opensuse.org/project/show/home:mazdlc)

```
[home_mazdlc_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/mazdlc/Arch_Extra/$arch

```

#### mazdlc-deadbeef-plugins

*   **维护者:** maz-1 <ohmygod19993 at gmail dot com>
*   **描述:** DeaDBeeF音乐播放器的插件
*   **Upstream page:** [https://build.opensuse.org/project/show/home:mazdlc](https://build.opensuse.org/project/show/home:mazdlc)

```
[home_mazdlc_deadbeef-plugins_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/mazdlc:/deadbeef-plugins/Arch_Extra/$arch

```

#### mazdlc-kde-frameworks-5

*   **维护者:** maz-1 <ohmygod19993 at gmail dot com>
*   **描述:** 基于kde frameworks 5的不稳定版软件包
*   **Upstream page:** [https://build.opensuse.org/project/show/home:mazdlc](https://build.opensuse.org/project/show/home:mazdlc)

```
[home_mazdlc_kde-frameworks-5_Arch_Extra]
Server = http://download.opensuse.org/repositories/home:/mazdlc:/kde-frameworks-5/Arch_Extra/$arch

```

## armv6h only

### Unsigned

#### arch-fook-armv6h

*   **维护者** Jaska Kivelä <jaska@kivela.net>
*   **描述：** Stuff that I have compiled for my Raspberry PI. Including Enlightenment and home automation stuff.

```
[arch-fook-armv6h]
Server = http://kivela.net/jaska/arch-fook-armv6h

```