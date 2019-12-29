Related articles

*   [pacman-key](/index.php/Pacman-key "Pacman-key")
*   [Official repositories](/index.php/Official_repositories "Official repositories")

This article lists binary repositories freely created and shared by the community, often providing pre-built versions of PKGBUILDS found in the [AUR](/index.php/AUR "AUR").

In order to use these repositories, add them to `/etc/pacman.conf`, as explained in [pacman#Repositories and mirrors](/index.php/Pacman#Repositories_and_mirrors "Pacman"). If a repository is signed, you must obtain and locally sign the associated key, as explained in [pacman/Package signing#Adding unofficial keys](/index.php/Pacman/Package_signing#Adding_unofficial_keys "Pacman/Package signing").

If you want to create your own custom repository, follow [pacman/Tips and tricks#Custom local repository](/index.php/Pacman/Tips_and_tricks#Custom_local_repository "Pacman/Tips and tricks").

**Warning:** The official Arch Linux Developers and the Trusted Users do not perform tests of any sort to verify the contents of these repositories. You must decide whether to trust their maintainers and you take full responsibility for any consequences of using any unofficial repository.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Adding your repository to this page](#Adding_your_repository_to_this_page)
*   [2 Signed](#Signed)
    *   [2.1 andontie-aur](#andontie-aur)
    *   [2.2 arcanisrepo](#arcanisrepo)
    *   [2.3 arch4edu](#arch4edu)
    *   [2.4 archlinuxcn](#archlinuxcn)
    *   [2.5 archstrike](#archstrike)
    *   [2.6 archzfs](#archzfs)
    *   [2.7 archzfs-kernels](#archzfs-kernels)
    *   [2.8 ashleyis](#ashleyis)
    *   [2.9 Bennix Repo](#Bennix_Repo)
    *   [2.10 blackeagle-pre-community](#blackeagle-pre-community)
    *   [2.11 chaotic-aur](#chaotic-aur)
    *   [2.12 catalyst](#catalyst)
    *   [2.13 catalyst-hd234k](#catalyst-hd234k)
    *   [2.14 city](#city)
    *   [2.15 coderkun-aur](#coderkun-aur)
    *   [2.16 coderkun-aur-audio](#coderkun-aur-audio)
    *   [2.17 devkitpro](#devkitpro)
    *   [2.18 disastrousaur](#disastrousaur)
    *   [2.19 dvzrv](#dvzrv)
    *   [2.20 ear](#ear)
    *   [2.21 eatabrick](#eatabrick)
    *   [2.22 eschwartz](#eschwartz)
    *   [2.23 ffy00](#ffy00)
    *   [2.24 fusion809](#fusion809)
    *   [2.25 grawlinson](#grawlinson)
    *   [2.26 gnome-devel](#gnome-devel)
    *   [2.27 herecura](#herecura)
    *   [2.28 holo](#holo)
    *   [2.29 ivasilev](#ivasilev)
    *   [2.30 jlk](#jlk)
    *   [2.31 llvm-svn](#llvm-svn)
    *   [2.32 markzz](#markzz)
    *   [2.33 maximbaz](#maximbaz)
    *   [2.34 me176c](#me176c)
    *   [2.35 miffe](#miffe)
    *   [2.36 mikelpint](#mikelpint)
    *   [2.37 Minerva W Science](#Minerva_W_Science)
    *   [2.38 mobile](#mobile)
    *   [2.39 nah](#nah)
    *   [2.40 nickcao](#nickcao)
    *   [2.41 origincode](#origincode)
    *   [2.42 pkgbuilder](#pkgbuilder)
    *   [2.43 post-factum kernels](#post-factum_kernels)
    *   [2.44 QOwnNotes](#QOwnNotes)
    *   [2.45 qt-debug](#qt-debug)
    *   [2.46 quarry](#quarry)
    *   [2.47 repo-ck](#repo-ck)
    *   [2.48 seblu](#seblu)
    *   [2.49 seiichiro](#seiichiro)
    *   [2.50 selinux](#selinux)
    *   [2.51 sergej-repo](#sergej-repo)
    *   [2.52 siosm-aur](#siosm-aur)
    *   [2.53 sublime-text](#sublime-text)
    *   [2.54 subtitlecomposer](#subtitlecomposer)
    *   [2.55 trinity](#trinity)
    *   [2.56 valveaur](#valveaur)
    *   [2.57 xuanrui](#xuanrui)
    *   [2.58 xyne-x86_64](#xyne-x86_64)
    *   [2.59 home-thaodan](#home-thaodan)
*   [3 Unsigned](#Unsigned)
    *   [3.1 alucryd](#alucryd)
    *   [3.2 alucryd-multilib](#alucryd-multilib)
    *   [3.3 andrwe](#andrwe)
    *   [3.4 archgeotux](#archgeotux)
    *   [3.5 archlinuxfr](#archlinuxfr)
    *   [3.6 archlinuxgr](#archlinuxgr)
    *   [3.7 archlinuxgr-kde4](#archlinuxgr-kde4)
    *   [3.8 aur-av-bin](#aur-av-bin)
    *   [3.9 craftdestiny](#craftdestiny)
    *   [3.10 dx37essentials](#dx37essentials)
    *   [3.11 heftig](#heftig)
    *   [3.12 jkanetwork](#jkanetwork)
    *   [3.13 kodi-devel-prebuilt](#kodi-devel-prebuilt)
    *   [3.14 mesa-git](#mesa-git)
    *   [3.15 Mountain](#Mountain)
    *   [3.16 oracle](#oracle)
    *   [3.17 ownstuff](#ownstuff)
    *   [3.18 pantheon](#pantheon)
    *   [3.19 pietma](#pietma)
    *   [3.20 pnsft-pur](#pnsft-pur)
    *   [3.21 stx4](#stx4)
    *   [3.22 titanium](#titanium)
    *   [3.23 userrepository](#userrepository)

## Adding your repository to this page

If you have your own repository, please add it to this page, so that all the other users will know where to find your packages. Please keep the following rules when adding new repositories:

*   Keep the lists in alphabetical order.
*   Include some information about the maintainer: include at least a (nick)name and some form of contact information (web site, email address, user page on ArchWiki or the forums, etc.).
*   If the repository is of the *signed* variety, please include a key-id, possibly using it as the anchor for a link to its keyserver; if the key is not on a keyserver, include a link to the key file.
*   Include some short description (e.g. the category of packages provided in the repository).
*   If there is a page (either on ArchWiki or external) containing more information about the repository, include a link to it.
*   If possible, avoid using comments in code blocks. The formatted description is much more readable. Users who want some comments in their `pacman.conf` can easily create it on their own.

Some repositories may also have packages for architectures beside x86_64\. The `$arch` variable will be set automatically by pacman.

## Signed

### andontie-aur

*   **Maintainer:** Holly M.
*   **Description:** A repo containing the most popular AUR packages, as well as some I use all the time. New packages can be requested on the upstream website.
*   **Key-ID:** EA50C866329648EE
*   **Upstream page:** [https://aur.andontie.net](https://aur.andontie.net)

```
[andontie-aur]
Server = https://aur.andontie.net/$arch

```

### arcanisrepo

*   **Maintainer:** [arcanis](https://www.archlinux.org/people/trusted-users/#arcanis)
*   **Description:** A repository with some AUR packages including packages from VCS
*   **Key-ID:** Not needed, as maintainer is a TU

```
[arcanisrepo]
Server = https://repo.arcanis.me/repo/$arch

```

(It is also available via FTP with the same URL.)

### arch4edu

*   **Maintainers:** [Jingbei Li (petronny)](https://github.com/petronny), and [others](https://github.com/arch4edu/arch4edu/graphs/contributors)
*   **Description:** arch4edu is a community repository for Archlinux and ArchlinuxARM that strives to provide the latest versions of most software used by college students.
*   **Git Repo:** [https://github.com/arch4edu/arch4edu](https://github.com/arch4edu/arch4edu)
*   **Issue tracking:** [https://github.com/arch4edu/arch4edu/issues](https://github.com/arch4edu/arch4edu/issues) for packaging issues, out-of-date notifications, package requests, and related questions
*   **Mirrors:** [https://github.com/arch4edu/arch4edu/wiki/Add-arch4edu-to-your-Archlinux](https://github.com/arch4edu/arch4edu/wiki/Add-arch4edu-to-your-Archlinux)
*   **Key-ID:** 7931B6D628C8D3BA

```
[arch4edu]
Server = https://mirrors.tuna.tsinghua.edu.cn/arch4edu/$arch
## or other mirrors in https://github.com/arch4edu/arch4edu/wiki/Add-arch4edu-to-your-Archlinux

```

### archlinuxcn

*   **Maintainers:** [Phoenix Nemo (phoenixlzx)](https://plus.google.com/+PhoenixNemo/), [Felix Yan (felixonmars, dev)](https://www.archlinux.org/people/developers/#fyan), [lilydjwg](https://twitter.com/lilydjwg), [farseerfc (TU)](https://www.archlinux.org/people/trusted-users/#farseerfc), and [others](https://github.com/archlinuxcn/repo/graphs/contributors)
*   **Description:** Packages by the Chinese Arch Linux community, all signed. Be aware that i686 packages are not fully maintained and tested, create an issue if you find some problems.
*   **Git Repo:** [https://github.com/archlinuxcn/repo](https://github.com/archlinuxcn/repo)
*   **Issue tracking:** [https://github.com/archlinuxcn/repo/issues](https://github.com/archlinuxcn/repo/issues) for packaging issues, out-of-date notifications, package requests, and related questions
*   **Mirrors:** [https://github.com/archlinuxcn/mirrorlist-repo](https://github.com/archlinuxcn/mirrorlist-repo) (Mostly for users in mainland China), or install *archlinuxcn-mirrorlist-git* from the repo.
*   **Key-ID:** Once the repo is added, *archlinuxcn-keyring* package must be installed before any other so you do not get errors about PGP signatures. *archlinuxcn-keyring* package itself is signed by TU.

```
[archlinuxcn]
Server = http://repo.archlinuxcn.org/$arch
## or install archlinuxcn-mirrorlist-git and use the mirrorlist
#Include = /etc/pacman.d/archlinuxcn-mirrorlist

```

### archstrike

*   **Maintainer:** [The ArchStrike Team](https://archstrike.org/team)
*   **Description:** A repository for security professionals and enthusiasts
*   **Upstream page:** [https://archstrike.org/](https://archstrike.org/)
*   **Key-ID:** 9D5F1C051D146843CDA4858BDE64825E7CBC0D51

**Note:** ArchStrike specific instructions can be found at [https://archstrike.org/wiki/setup](https://archstrike.org/wiki/setup)

```
[archstrike]
Server = https://mirror.archstrike.org/$arch/$repo

```

### archzfs

*   **Maintainer:** [Jan Houben (minextu)](https://aur.archlinux.org/account/minextu)
*   **Description:** Packages for ZFS on Arch Linux.
*   **Upstream page:** [https://github.com/archzfs/archzfs](https://github.com/archzfs/archzfs)
*   **Key-ID:** F75D9D76

```
[archzfs]
Server = http://archzfs.com/$repo/x86_64

```

### archzfs-kernels

*   **Maintainer:** [Endre Szabo](https://aur.archlinux.org/account/endre/)
*   **Description:** Official kernel packages matching the most recent [ZFS packages](#_archzfs) kernel version dependencies. Use this to be able to upgrade your kernel package every time whilst using ZFS packages above :)
*   **Upstream page:** [https://end.re/archzfs-kernels/](https://end.re/archzfs-kernels/)
*   **Key-ID:** Not needed as packages are from core repos and signed officially.

```
[archzfs-kernels]
Server = http://end.re/$repo/

```

### ashleyis

*   **Maintainer:** Ashley Towns ([ashleyis](https://aur.archlinux.org/account/ashleyis/))
*   **Description:** Debug versions of SDL, chipmunk, libtmx and other misc game libraries. also swift-lang and some other AUR packages
*   **Key-ID:** B1A4D311

```
[ashleyis]
Server = http://arch.ashleytowns.id.au/repo/$arch

```

### Bennix Repo

*   **Maintainer:** Ben P. Dorsi-Todaro ([Tech Me Out](https://techmeout.org))
*   **Description:** Packages [Ben P. Dorsi-Todaro](http://ben-dorsi-todaro.com/) uses and are not listed in repos, or packages built by [Big Ben's Web Hosting](http://www.bigbenshosting.com/)
*   **Key-ID:** F14BB858F6253DA0

```
[bigben-repo]
SigLevel = Optional TrustAll
Server = http://bennix.net/bigben-repo/

```

### blackeagle-pre-community

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** testing of the by me maintaned packages before moving to *community* repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[blackeagle-pre-community]
Server = https://repo.herecura.be/$repo/$arch

```

### chaotic-aur

*   **Maintainer:** [PedroHLC](https://github.com/pedrohlc)
*   **Description:** Auto builds AUR packages the maintainer uses, update them hourly (a few are daily). Hosted in São Carlos, SP, Brazil. Has a mirror in Germany. x86_64 only. Has over 1400 packages.
*   **Key-ID:** [[1]](http://pool.sks-keyservers.net/pks/lookup?search=0x3056513887B78AEB&fingerprint=on&op=index), fingerprint `EF92 5EA6 0F33 D0CB 85C4 4AD1 3056 5138 87B7 8AEB`
*   **Note:** See [maintainer's notes](https://lonewolf.pedrohlc.com/chaotic-aur).

```
[chaotic-aur]
Server = http://lonewolf-builder.duckdns.org/$repo/x86_64
Server = http://chaotic.bangl.de/$repo/x86_64

```

### catalyst

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Key-ID:** 653C3094

```
[catalyst]
Server = http://167.86.114.169/arch/catalyst/$arch

```

### catalyst-hd234k

*   **Maintainer:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **Description:** ATI Catalyst proprietary drivers.
*   **Key-ID:** 653C3094

```
[catalyst-hd234k]
Server = http://167.86.114.169/arch/catalyst-hd234k/$arch

```

### city

*   **Maintainer:** [Balló György](https://www.archlinux.org/people/trusted-users/#bgyorgy)
*   **Description:** Experimental/unpopular packages.
*   **Upstream page:** [https://pkgbuild.com/~bgyorgy/city.html](https://pkgbuild.com/~bgyorgy/city.html)
*   **Key-ID:** Not needed, as maintainer is a TU

```
[city]
Server = https://pkgbuild.com/~bgyorgy/$repo/os/$arch

```

### coderkun-aur

*   **Maintainer:** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **Description:** AUR packages with random software. Supporting package deltas and package and database signing.
*   **Upstream page:** [https://www.suruatoel.xyz/arch](https://www.suruatoel.xyz/arch)
*   **Key-ID:** 39E27199A6BEE374
*   **Keyfile:** [https://www.suruatoel.xyz/coderkun.asc](https://www.suruatoel.xyz/coderkun.asc)

```
[coderkun-aur]
Server = http://arch.suruatoel.xyz/$repo/$arch/

```

### coderkun-aur-audio

*   **Maintainer:** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **Description:** AUR packages with audio-related (realtime kernels, lv2-plugins, …) software. Supporting package deltas and package and database signing.
*   **Upstream page:** [https://www.suruatoel.xyz/arch](https://www.suruatoel.xyz/arch)
*   **Key-ID:** 39E27199A6BEE374
*   **Keyfile:** [https://www.suruatoel.xyz/coderkun.key](https://www.suruatoel.xyz/coderkun.key)

```
[coderkun-aur-audio]
Server = http://arch.suruatoel.xyz/$repo/$arch/

```

### devkitpro

*   **Maintainer:** [wintermute](https://devkitpro.org/)
*   **Description:** Provides Homebrew toolchains for the Nintendo Wii, Gamecube, DS, GBA, Gamepark gp32 and Nintendo Switch
*   **Upstream page:** [https://devkitpro.org/wiki/devkitPro_pacman](https://devkitpro.org/wiki/devkitPro_pacman)
*   **Key-ID:** F7FD5492264BB9D0

**Note:** Repository has its own additional keyring at [https://downloads.devkitpro.org/devkitpro-keyring-r1.787e015-2-any.pkg.tar.xz](https://downloads.devkitpro.org/devkitpro-keyring-r1.787e015-2-any.pkg.tar.xz).

```
[dkp-libs]
Server = https://downloads.devkitpro.org/packages
[dkp-linux]
Server = https://downloads.devkitpro.org/packages/linux

```

### disastrousaur

*   **Maintainer:** [TheGoliath](https://aur.archlinux.org/account/TheGoliath)
*   **Description:** Well known AUR package managers, many of the most popular packages available on the AUR, as well as those that I favor myself
*   **Upstream page:** [https://mirror.repohost.de/disastrousaur](https://mirror.repohost.de/disastrousaur)
*   **Key-ID:** CBAE582A876533FD
*   **Keyfile:** [https://mirror.repohost.de/disastrousaur.key](https://mirror.repohost.de/disastrousaur.key)

**Warning:** disastrousaur and disastrousarm have now been merged under the disastrousaur name Please make sure you have changed the Server URL for your repos accordingly. Builds for other architectures may come out as I got enough time getting things running.

```
[disastrousaur]
Server = https://mirror.repohost.de/$repo/$arch

```

### dvzrv

*   **Maintainer:** [David Runge](https://www.archlinux.org/people/developers/#dvzrv)
*   **Description:** [Realtime kernel patchset](/index.php/Realtime_kernel_patchset "Realtime kernel patchset") (aka. [linux-rt](https://aur.archlinux.org/packages/linux-rt/) and [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/))
*   **Key-ID:** Not needed, as maintainer is a developer/TU

```
[dvzrv]
Server = https://pkgbuild.com/~dvzrv/repo/$arch

```

### ear

*   **Maintainer:** [Ward Segers](https://wardsegers.be),
*   **Description:** Editicalu's ArchLinux Repository. Contains precompiled AUR packages (mostly the ones maintained by editicalu)
*   **Homepage:** [https://ear.wardsegers.be/](https://ear.wardsegers.be/)
*   **Upstream page:** [https://gitlab.com/editicalu/ear](https://gitlab.com/editicalu/ear)
*   **Keyfile:** [https://ear.wardsegers.be/signingkey.asc](https://ear.wardsegers.be/signingkey.asc)
*   **Key-ID:** A9C4E7734638ACF8

**Note:** Instructions can be found at [https://ear.wardsegers.be](https://ear.wardsegers.be)

```
[ear]
Server = https://ear.wardsegers.be/$arch

```

### eatabrick

*   **Maintainer:** bentglasstube
*   **Description:** Packages for software written by (and a few just compiled by) bentglasstube.

```
[eatabrick]
Server = http://repo.eatabrick.org/$arch

```

### eschwartz

*   **Maintainer:** [Eli Schwartz](https://www.archlinux.org/people/trusted-users/#eschwartz)
*   **Description:** Personal repo with AUR packages and some core packages from git (including glibc and pacman). Contains debug packages.
*   **Key-ID:** Not needed, as maintainer is a TU

```
[eschwartz]
Server = https://pkgbuild.com/~eschwartz/repo/$arch

```

### ffy00

*   **Maintainer:** [Filipe Laíns](https://www.archlinux.org/people/trusted-users/#FFY00)
*   **Description:** Personal repo. Contains some packages related to the D language.
*   **Key-ID:** Not needed, as maintainer is a TU

```
[ffy00]
Server = https://pkgbuild.com/~ffy00/repo

```

### fusion809

*   **Maintainer:** [Horne](https://aur.archlinux.org/account/fusion809%7CBrenton)] (brentonhorne77 at gmail dot com).
*   **Description:** Provides a few AUR and other packages I like. Like CodeLite and bleeding-edge (latest release within 1 day of its release) GVim (GTK 2 interface).
*   **Package list:** [http://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/](http://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/)
*   **Key-ID:** 03264DDCD606DC98
*   **Keyfile:** [https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/home_fusion809_Arch_Extra.key](https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/home_fusion809_Arch_Extra.key)

```
[home_fusion809_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/$arch

```

### grawlinson

*   **Maintainer:** [George Rawlinson](https://aur.archlinux.org/account/grawlinson)
*   **Description:** AUR packages maintained by the user as well as some experimental packages.
*   **Package list:** [https://repo.nullpointer.io](https://repo.nullpointer.io)
*   **Key-ID:** 25ea6900d9ea5ebc
*   **Keyfile:** [https://nullpointer.io/grawlinson.key](https://nullpointer.io/grawlinson.key)

```
[grawlinson]
Server = https://repo.nullpointer.io

```

### gnome-devel

*   **Maintainer:** [Andres Fernandez](https://plus.google.com/+AndresFernandezperonista), [Fernando Fernandez](https://plus.google.com/+FernandoFernandezBerel)
*   **Description:** GNOME development releases. For testing purposes only.
*   **Package list:** [https://softwareperonista.com.ar/repo/archlinux/gnome-devel/x86_64/](https://softwareperonista.com.ar/repo/archlinux/gnome-devel/x86_64/)
*   **Key-ID:** DDCE9FD63370080B

**Note:** Must be put above `[testing]` repository.

```
[gnome-devel]
Server = https://softwareperonista.com.ar/repo/archlinux/gnome-devel/$arch

```

### herecura

*   **Maintainer:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **Description:** additional packages not found in the *community* repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[herecura]
Server = https://repo.herecura.be/$repo/$arch

```

### holo

*   **Maintainer:** Stefan Majewsky <holo-pacman@posteo.de> (please prefer to report issues at [Github](https://github.com/majewsky/holo-pacman-repo/issues))
*   **Description:** Packages for [Holo configuration management](https://holocm.org), including compatible plugins and tools.
*   **Upstream page:** [https://github.com/majewsky/holo-pacman-repo](https://github.com/majewsky/holo-pacman-repo)
*   **Package list:** [https://repo.holocm.org/archlinux/x86_64](https://repo.holocm.org/archlinux/x86_64)
*   **Key-ID:** 0xF7A9C9DC4631BD1A

```
[holo]
Server = https://repo.holocm.org/archlinux/x86_64

```

### ivasilev

*   **Maintainer:** [Ianis G. Vasilev](https://ivasilev.net)
*   **Description:** A variety of packages, mostly my own software and AUR builds.
*   **Upstream page:** [https://ivasilev.net/pacman](https://ivasilev.net/pacman)
*   **Key-ID:** [17DAB671](https://pgp.mit.edu/pks/lookup?op=vindex&search=0xB77A3C8832838F1F80ADFD7E1D0507B417DAB671)

```
[ivasilev]
Server = https://ivasilev.net/pacman/$arch

```

### jlk

*   **Maintainer:** [Jakub Klinkovský](/index.php/User:Lahwaacz "User:Lahwaacz")
*   **Description:** Various packages from the ABS and AUR. Modified packages are in the `modified` group.
*   **Upstream page:** [https://jlk.fjfi.cvut.cz/arch/repo/README.html](https://jlk.fjfi.cvut.cz/arch/repo/README.html)
*   **Key-ID:** 932BA3FA0C86812A32D1F54DAB5964AEB9FEDDDC

```
[jlk]
Server = https://jlk.fjfi.cvut.cz/arch/repo

```

### llvm-svn

*   **Maintainer:** [Luchesar V. ILIEV (kerberizer)](/index.php/User:Kerberizer "User:Kerberizer")
*   **Description:** [llvm-svn](https://aur.archlinux.org/pkgbase/llvm-svn) and [lib32-llvm-svn](https://aur.archlinux.org/pkgbase/lib32-llvm-svn) from AUR: the LLVM compiler infrastructure, the Clang frontend, and the tools associated with it
*   **Key-ID:** [0x76563F75679E4525](https://sks-keyservers.net/pks/lookup?op=vindex&search=0x76563F75679E4525&fingerprint=on&exact=on), fingerprint `D16C F22D 27D1 091A 841C 4BE9 7656 3F75 679E 4525`

```
[llvm-svn]
Server = https://repos.uni-plovdiv.net/archlinux/$repo/$arch

```

### markzz

*   **Maintainer:** [Mark Weiman (markzz)](/index.php/User:Markzz "User:Markzz")
*   **Description:** Packages that markzz maintains or uses on the AUR; this includes Linux with the vfio patchset ([linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) and [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)), and packages for analysis of network data.
*   **Key ID:** DEBB9EE4

**Note:** If you want to add the key by installing the *markzz-keyring* package, temporarily add `SigLevel = Never` into the repository section.

```
[markzz]
Server = https://repo.markzz.com/arch/$repo/$arch

```

### maximbaz

*   **Maintainer:** [Maxim Baz](https://www.archlinux.org/people/trusted-users/#maximbaz)
*   **Description:** Personal repo with AUR packages.
*   **Key-ID:** Not needed, as maintainer is a TU

```
[maximbaz]
Server = https://pkgbuild.com/~maximbaz/repo/

```

### me176c

*   **Maintainer:** [lambdadroid](https://github.com/lambdadroid)
*   **Description:** Packages for [ASUS MeMO Pad 7 (ME176C(X))](/index.php/ASUS_MeMO_Pad_7_(ME176C(X)) "ASUS MeMO Pad 7 (ME176C(X))")
*   **Key-ID:** 2B1138A8BB59D786A3BF42AAD996DA70572407FB

```
[me176c]
Server = https://me176c.uber.space/archlinux

```

### miffe

*   **Maintainer:** [miffe](https://bbs.archlinux.org/profile.php?id=4059)
*   **Description:** AUR packages maintained by miffe, e.g. linux-mainline
*   **Key ID:** 313F5ABD

```
[miffe]
Server = https://arch.miffe.org/$arch/

```

### mikelpint

*   **Maintainer:** [Mikel Pintado (Mikelpint)](/index.php/User:Mikelpint "User:Mikelpint")
*   **Description:** Packages that mikelpint maintains in the AUR.
*   **Key ID:** 5CA78FC65B189E2B

```
[mikelpint]
Server = https://mikelpint.github.io/repository/archlinux/repo

```

### Minerva W Science

*   **Maintainer:** Minerva W
*   **Description:** [OpenFOAM](/index.php/OpenFOAM "OpenFOAM") packages.
*   **Key-ID:** 3FF21B78117507DA
*   **Keyfile:** [https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/x86_64/home_Minerva_W_Science_Arch_Extra.key](https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/x86_64/home_Minerva_W_Science_Arch_Extra.key)

```
[home_Minerva_W_Science_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/$arch 

```

### mobile

*   **Maintainer:** [farwayer](https://keybase.io/farwayer)
*   **Description:** React Native and Android development
*   **Upstream page:** [https://keybase.pub/farwayer/arch/mobile/](https://keybase.pub/farwayer/arch/mobile/)
*   **Key ID:** 7943315502A936D7

```
[mobile]
Server = https://farwayer.keybase.pub/arch/$repo

```

### nah

*   **Maintainer:** [phillid](https://yeah.nah.nz)
*   **Description:** Pre-built versions of the (slow-to-build) graph-tool python libraries, mingw-w64
*   **Key ID:** 7BF3D17D0884BF5B

```
[nah]
Server = https://repo.nah.nz/$repo

```

### nickcao

*   **Maintainer:** [NickCao](https://nichi.co/about)
*   **Description:** Some (useful for some) packages from me, and some aur packages I personally use.
*   **Key-ID:** 09CC69622E8D4EE343B4E8954D0BA456DF028C15

```
[nickcao]
Server = https://repo.nichi.co/$arch

```

### origincode

*   **Maintainer:** [OriginCode](https://aur.archlinux.org/account/OriginCode)
*   **Description:** A few staging or testing packages from [#archlinuxcn](#archlinuxcn), and some daily use packages.
*   **Key-ID:** 0A5BAD445D80C1CC & 62BF97502AE10D22

```
[origincode]
Server = https://repo.origincode.me/repo/$arch

```

### pkgbuilder

*   **Maintainer:** [Chris Warrick](https://chriswarrick.com/)
*   **Description:** A repository for PKGBUILDer, a Python AUR helper.
*   **Upstream page:** [https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder)
*   **Key-ID:** 5EAAEA16

```
[pkgbuilder]
Server = https://pkgbuilder-repo.chriswarrick.com/

```

### post-factum kernels

*   **Maintainer**: [Oleksandr Natalenko aka post-factum](https://aur.archlinux.org/account/post-factum)
*   **Upstream page**: [https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README)
*   **Description**: [pf-kernel](/index.php/Kernel#Major_patchsets "Kernel") packages by its developer, post-factum
*   **Key-ID:**: 95C357D2AF5DA89D
*   **Keyfile**: [https://download.opensuse.org/repositories/home:/post-factum:/kernels/Arch/x86_64/home_post-factum_kernels_Arch.key](https://download.opensuse.org/repositories/home:/post-factum:/kernels/Arch/x86_64/home_post-factum_kernels_Arch.key)

```
[home_post-factum_kernels_Arch]
Server = https://download.opensuse.org/repositories/home:/post-factum:/kernels/Arch/$arch

```

### QOwnNotes

*   **Maintainer:** [Patrizio Bekerle](https://aur.archlinux.org/account/pbek) (pbek), QOwnNotes author
*   **Description:** QOwnNotes is a open source notepad and todo list manager with markdown support and [ownCloud](/index.php/OwnCloud "OwnCloud") integration.
*   **Key-ID:** FFC43FC94539B8B0
*   **Keyfile:** [https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/x86_64/home_pbek_QOwnNotes_Arch_Extra.key](https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/x86_64/home_pbek_QOwnNotes_Arch_Extra.key)

```
[home_pbek_QOwnNotes_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/$arch

```

### qt-debug

*   **Maintainer:** [The Compiler](https://aur.archlinux.org/account/The-Compiler)
*   **Description:** Qt/PyQt builds with debug symbols
*   **Upstream page:** [https://github.com/qutebrowser/qt-debug-pkgbuild](https://github.com/qutebrowser/qt-debug-pkgbuild)
*   **Key-ID:** D6A1C70FE80A0C82

```
[qt-debug]
Server = https://qutebrowser.org/qt-debug/$arch

```

### quarry

*   **Maintainer:** [anatolik](https://www.archlinux.org/people/developers/#anatolik)
*   **Description:** Arch binary repository for [Rubygems](http://rubygems.org/) packages. See [forum announcement](https://bbs.archlinux.org/viewtopic.php?id=182729) for more information.
*   **Sources:** [https://github.com/anatol/quarry](https://github.com/anatol/quarry)
*   **Key-ID:** Not needed, as maintainer is a developer

```
[quarry]
Server = https://pkgbuild.com/~anatolik/quarry/x86_64/

```

### repo-ck

Kernel and modules with Brain Fuck Scheduler and all the goodies in the ck1 patch set.

See [/Repo-ck](/index.php/Unofficial_user_repositories/Repo-ck "Unofficial user repositories/Repo-ck").

### seblu

*   **Maintainer:** [Sébastien Luttringer](https://www.archlinux.org/people/developers/#seblu)
*   **Description:** All seblu useful pre-built packages, some homemade (linux-seblu-meta, zfs-dkms, spotify, masterpdfeditor, etc).
*   **Key-ID:** Not required, as maintainer is a Developer

```
[seblu]
Server = https://al1.seblu.net/$repo/$arch
Server = https://al2.seblu.net/$repo/$arch

```

### seiichiro

*   **Maintainer:** [Stefan Brand (seiichiro0185)](https://www.seiichiro0185.org)
*   **Description:** AUR-packages I use frequently
*   **Key-ID:** 805517CC

```
[seiichiro]
Server = https://www.seiichiro0185.org/repo/$arch

```

### selinux

*   **Maintainer:** [swordfeng](https://github.com/swordfeng)
*   **Description:** Unofficial (personal) builds for [SELinux](/index.php/SELinux "SELinux") packages. PKGBUILDs are taken from AUR instead of the upstream GitHub repo.
*   **Upstream page:** [https://github.com/archlinuxhardened/selinux](https://github.com/archlinuxhardened/selinux)
*   **Key-ID:** 7691FA63FE91CAFDD42A4AF08323B00E97DF0E6D (subkey B988167F59A3AF8368D55D65A7862FD48B72D83B is specifically used for signing packages)
*   **Keyfile:** [https://repo.taiho.moe/key.asc](https://repo.taiho.moe/key.asc)

```
[selinux]
Server = https://repo.taiho.moe/$repo

```

### sergej-repo

*   **Maintainer:** [Sergej Pupykin](https://www.archlinux.org/people/trusted-users/#spupykin)
*   **Description:** psi-plus, owncloud-git, ziproxy, android, MySQL, and other stuff. Some packages also available for armv7h.
*   **Key-ID:** Not required, as maintainer is a TU

```
[sergej-repo]
Server = http://repo.p5n.pp.ru/$repo/os/$arch

```

### siosm-aur

*   **Maintainer:** [Timothee Ravier](https://tim.siosm.fr/about/)
*   **Description:** packages also available in the Arch User Repository, sometimes with minor fixes
*   **Upstream page:** [https://tim.siosm.fr/repositories/](https://tim.siosm.fr/repositories/)
*   **Key-ID:** 78688F83

```
[siosm-aur]
Server = http://siosm.fr/repo/$repo/

```

### sublime-text

*   **Maintainer:** Sublime Text developer
*   **Description:** Sublime Text editor packages from developer's repository
*   **Upstream page:** [https://www.sublimetext.com/docs/3/linux_repositories.html#pacman](https://www.sublimetext.com/docs/3/linux_repositories.html#pacman)
*   **Key-ID:** 8A8F901A

```
[sublime-text]
Server = https://download.sublimetext.com/arch/stable/x86_64

```

### subtitlecomposer

*   **Maintainer:** Mladen Milinkovic (maxrd2)
*   **Description:** Subtitle Composer stable and nightly builds
*   **Upstream page:** [https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer)
*   **Key-ID:** EF9D9B26

```
[subtitlecomposer]
Server = https://smoothware.net/$repo/$arch

```

### trinity

*   **Maintainer:** Michael J. Manley <mmanley@ntge.net>
*   **Description:** [Trinity](/index.php/Trinity "Trinity") Desktop Environment
*   **Key-ID:** 5F710C1E

```
[trinity]
Server = https://repo.nasutek.com/arch/contrib/trinity/x86_64

```

### valveaur

*   **Maintainer:** John Schoenick <johns@valvesoftware.com> ([https://valvesoftware.com](https://valvesoftware.com))
*   **Description:** A repository by Valve Software Providing The Linux-fsync kernel and modules, including the futex-wait-multiple patchset for testing with Proton fsync & Mesa with the ACO compiler patchset.
*   **Upstream page:** [https://steamcommunity.com/linux](https://steamcommunity.com/linux)
*   **Key-ID:** 8DC2CE3A3D245E64

```
[valveaur]
Server = http://repo.steampowered.com/arch/valveaur

```

### xuanrui

*   **Maintainer:** [Xuanrui Qi (xuanruiqi)](https://aur.archlinux.org/account/xuanruiqi)
*   **Description:** xuanruiqi's own packages and frequently-used packages, mainly of interest to functional programmers.
*   **Upstream Page:** [https://www.xuanruiqi.com/linux.html](https://www.xuanruiqi.com/linux.html)
*   **Key-ID:** 6E06FBC8

```
[xuanrui]
Server = https://arch.xuanruiqi.com/repo

```

### xyne-x86_64

*   **Maintainer:** [Xyne](https://www.archlinux.org/people/trusted-users/#xyne)
*   **Description:** A repository for Xyne's own projects.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

```
[xyne-x86_64]
# Server = https://xyne.archlinux.ca/repos/xyne # It returns error 404 or 406 (varying). Use the line below:
Server = http://xyne.archlinux.ca/bin/repo.php?file=

```

### home-thaodan

*   **Maintainer**: [Thaodan](https://aur.archlinux.org/account/Thaodan)
*   **Upstream page**: [https://gitlab.com/Thaodan/linux-pf](https://gitlab.com/Thaodan/linux-pf)
*   **Description**: [pf-kernel](/index.php/Kernel#Major_patchsets "Kernel") and other packages by pf-kernel fork developer, Thaodan
*   **Gitlab Project**: [https://gitlab.com/Thaodan/repo-home-thaodan-repo](https://gitlab.com/Thaodan/repo-home-thaodan-repo)
*   **Key-ID:**: BBFE2FD421597395E4FC8C8DF6C85FEE79D661A4

```
[home-thaodan]
Server = https://thaodan.de/public/archlinux/home-thaodan/$arch

```

## Unsigned

**Note:** Users will need to add the following to these entries: `SigLevel = PackageOptional`

### alucryd

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **Description:** Various packages Maxime Gauduin maintains (or not) in the AUR.

```
[alucryd]
Server = https://pkgbuild.com/~alucryd/$repo/x86_64

```

### alucryd-multilib

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **Description:** Various packages needed to run Steam without its runtime environment.

```
[alucryd-multilib]
Server = https://pkgbuild.com/~alucryd/$repo/x86_64

```

### andrwe

*   **Maintainer:** Andrwe Lord Weber
*   **Description:** contains programs I'm using on many systems
*   **Upstream page:** [http://andrwe.org/linux/repository](http://andrwe.org/linux/repository)

```
[andrwe]
Server = http://repo.andrwe.org/$arch

```

### archgeotux

*   **Maintainer:** Samuel Mesa
*   **Description:** Geospatial and geographic information system applications
*   **Upstream page:** [https://archgeotux.sourceforge.io/](https://archgeotux.sourceforge.io/)

```
[archgeotux]
Server = https://downloads.sourceforge.net/project/archgeotux/$arch

```

### archlinuxfr

*   **Maintainer:**
*   **Description:**
*   **Upstream page:** [http://afur.archlinux.fr](http://afur.archlinux.fr)

```
[archlinuxfr]
Server = http://repo.archlinux.fr/$arch

```

### archlinuxgr

*   **Maintainer:**
*   **Description:** many interesting packages provided by the Hellenic (Greek) Arch Linux community

```
[archlinuxgr]
Server = http://archlinuxgr.tiven.org/archlinux/$arch

```

### archlinuxgr-kde4

*   **Maintainer:**
*   **Description:** KDE4 packages (plasmoids, themes etc) provided by the Hellenic (Greek) Arch Linux community

```
[archlinuxgr-kde4]
Server = http://archlinuxgr.tiven.org/archlinux-kde4/$arch

```

### aur-av-bin

*   **Maintainer:** [milkii](https://aur.archlinux.org/account/milk/) (ping me on Freenode)
*   **Description:** Precompiled Arch Linux binary packages of mostly A/V related software from the AUR.
*   **Upstream page:** [https://github.com/mxmilkb/aur-av-bin](https://github.com/mxmilkb/aur-av-bin)

```
[aur-av-bin]
SigLevel = PackageOptional
Server = https://github.com/mxmilkb/aur-av-bin/releases/download/repository

```

### craftdestiny

*   **Maintainer:** [LinuxVieLoisir](https://craftdestiny.ovh)
*   **Description:** A Craft Destiny repository is there to avoid long compilation on some software. It also adds some very useful additional software.

```
[craftdestiny]
Server = https://miroir.craftdestiny.ovh/archlinux-repo/

```

### dx37essentials

*   **Maintainer:** [DragonX256](https://aur.archlinux.org/account/DragonX256)
*   **Description:** Personal repository. Contains packages from AUR, which I using every day.
*   **Git repo:** [https://gitlab.com/DX37/dx37essentials](https://gitlab.com/DX37/dx37essentials)
*   **Upstream page:** [https://dx37.gitlab.io/dx37essentials](https://dx37.gitlab.io/dx37essentials)

```
[dx37essentials]
Server = https://dx37.gitlab.io/$repo/$arch

```

### heftig

*   **Maintainer:** [Jan Steffens](https://www.archlinux.org/people/developers/#heftig)
*   **Description:** Includes pulseaudio-git, pavucontrol-git, and firefox-developer-edition
*   **Upstream page:** [https://bbs.archlinux.org/viewtopic.php?id=117157](https://bbs.archlinux.org/viewtopic.php?id=117157)

```
[heftig]
Server = https://pkgbuild.com/~heftig/repo/$arch

```

### jkanetwork

*   **Maintainer:** kprkpr <kevin01010 at gmail dot com>
*   **Maintainer:** Joselucross <jlgarrido97 at gmail dot com>
*   **Description:** Packages of AUR like pimagizer,stepmania,yaourt,linux-mainline,wps-office,grub-customizer,some IDE.. Open for all that wants to contribute
*   **Upstream page:** [http://repo.jkanetwork.com/](http://repo.jkanetwork.com/)

```
[jkanetwork]
Server = http://repo.jkanetwork.com/repo/$repo/

```

### kodi-devel-prebuilt

*   **Maintainer:** asm0dey <pavel.finkelshtein+AUR@gmail.com>
*   **Description:** Prebuilt packages of kodi-devel from AUR
*   **Upstream page:** [kodi-devel](https://aur.archlinux.org/packages/kodi-devel/)

```
[kodi-devel-prebuilt]
Server = https://asm0dey.github.io/$repo/$arch
SigLevel = PackageOptional

```

### mesa-git

*   **Maintainer:** [Laurent Carlier](https://www.archlinux.org/people/trusted-users/#lcarlier)
*   **Description:** Mesa git builds for the *testing* and *multilib-testing* repositories

```
[mesa-git]
Server = https://pkgbuild.com/~lcarlier/$repo/$arch

```

### Mountain

*   **Maintainer:** [Minzord](https://mountainlinux.wordpress.com)
*   **Description:** Popular AUR Packages and some Driver Wifi.

```
[Mountain]
SigLevel = Never
Server = https://mountain-linux.github.io/Mountain/$arch

```

### oracle

*   **Maintainer:** [User:Malvineous](/index.php/User:Malvineous "User:Malvineous")
*   **Description:** [Oracle Database client](/index.php/Oracle_Database_client "Oracle Database client") and associated tools, built from AUR packages and hosted on AWS S3 using [Makefile scripts](https://github.com/Malvineous/archlinux-pacman-repo).
*   **Conditions:** By using this repository you agree to the [Oracle Technology Network Development and Distribution License Terms for Instant Client](http://www.oracle.com/technetwork/licenses/instant-client-lic-152016.html).

```
[oracle]
Server = http://linux.shikadi.net/arch/$repo/$arch/

```

### ownstuff

*   **Maintainer:** [Martchus](https://aur.archlinux.org/account/Martchus)
*   **Description:** A lot of packages from the AUR, e.g. a great number packages for mingw-w64 and Android cross compilation, fonts, Perl modules, tools like [tageditor](https://aur.archlinux.org/packages/tageditor/), [syncthingtray](https://aur.archlinux.org/packages/syncthingtray/), [subtitlecomposer](https://aur.archlinux.org/packages/subtitlecomposer/) and [qmplay2](https://aur.archlinux.org/packages/qmplay2/)
*   **Upstream page**: [https://github.com/Martchus/PKGBUILDs](https://github.com/Martchus/PKGBUILDs) (sources beside the AUR) and [https://martchus.no-ip.biz/repoindex](https://martchus.no-ip.biz/repoindex) (package browser/search)

```
[ownstuff-testing]
Server = https://ftp.f3l.de/~martchus/$repo/os/$arch
Server = https://martchus.no-ip.biz/repo/arch/$repo/os/$arch

[ownstuff]
Server = https://ftp.f3l.de/~martchus/$repo/os/$arch
Server = https://martchus.no-ip.biz/repo/arch/$repo/os/$arch

```

**Note:** The testing repository is supposed to be used together with the official testing repositories.

### pantheon

*   **Maintainer:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **Description:** Repository containing Pantheon-related packages

```
[pantheon]
Server = https://pkgbuild.com/~alucryd/$repo/$arch

```

### pietma

*   **Maintainer:** MartiMcFly <martimcfly@autorisation.de>
*   **Description:** Arch User Repository packages [I create or maintain.](https://aur.archlinux.org/packages/?K=martimcfly&SeB=m).
*   **Upstream page:** [http://pietma.com/tag/aur/](http://pietma.com/tag/aur/)

```
[pietma]
Server = http://repository.pietma.com/nexus/content/repositories/archlinux/$arch/$repo

```

### pnsft-pur

*   **Maintainer:** [ponsfoot](https://aur.archlinux.org/account/ponsfoot)
*   **Description:** Japanese input method packages Mozc (vanilla) and libkkc

```
[pnsft-pur]
Server = https://osdn.net/projects/ponsfoot-aur/storage/pur/x86_64/

```

### stx4

*   **Maintainer:** StarterX4 <starterx4[at]gmail.com>
*   **Description:** Any – some fonts and fakepkgs; x86_64 – archived yet might useful packages (like PacmanXG4) and some AUR soft (like OpenBoard).
*   **Upstream Page:** [https://keybase.pub/starterx4/repos/arch/](https://keybase.pub/starterx4/repos/arch/)

```
[stx4-any]
SigLevel = Never
Server = https://starterx4.keybase.pub/repos/arch/any/stx4

[stx4-x86_64]
SigLevel = Never
Server = https://starterx4.keybase.pub/repos/arch/x86_64/stx4

```

### titanium

*   **Maintainer:** Pyrerune <pyrerune@gmail.com>
*   **Description:** Repository containing software I develop.

```
[titanium]
Server = https://pyrerune.github.io/titanium/$arch

```

### userrepository

*   **Maintainer:** [Bruno Miguel](https://twitter.com/brunomiguel) <brunoalexandremiguel@gmail.com>
*   **Description:** Repository containing software from AUR

```
[userrepository]
Server = https://userrepository.eu

```