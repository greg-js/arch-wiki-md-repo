相关文章

*   [pacman-key (简体中文)](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman-key (简体中文)")
*   [Official Repositories (简体中文)](/index.php/Official_Repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official Repositories (简体中文)")

**翻译状态：** 本文是英文页面 [Unofficial_user_repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2020-2-6，点击[这里](https://wiki.archlinux.org/index.php?title=Unofficial_user_repositories&diff=0&oldid=596774)可以查看翻译后英文页面的改动。

这篇文章列出了由社区创建的自由共享二进制软件包的软件仓库，其中很多的包都是由[AUR](/index.php/AUR "AUR")中可以找到的PKGBUILD文件预编译打包而成。

**警告:** 无论Arch Linux的开发者还是授信用户都不会对这些软件仓库做任何的测试与验证。需要每一个用户自己决定是否信任这些软件仓库的维护者，并且对软件源维护者做出的任何决定导致的后果负责。

想要使用这些软件仓库，你需要把他们添加到 `/etc/pacman.conf`，详情请看 [pacman (简体中文)#软件仓库](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#软件仓库 "Pacman (简体中文)")。如果一个软件仓库进行了签名，你必须要在本地签署这些key，详见[Pacman-key (简体中文)#导入非官方密钥](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#导入非官方密钥 "Pacman-key (简体中文)")。

如果你想自己建立一个软件仓库，请看 [pacman tips (简体中文)#自建本地仓库](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#自建本地仓库 "Pacman tips (简体中文)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 加入你自己的仓库](#加入你自己的仓库)
    *   [1.1 archlinuxcn](#archlinuxcn)
*   [2 Signed](#Signed)
    *   [2.1 andontie-aur](#andontie-aur)
    *   [2.2 AniNIX](#AniNIX)
    *   [2.3 arcanisrepo](#arcanisrepo)
    *   [2.4 arch4edu](#arch4edu)
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

## 加入你自己的仓库

**注意:** 本文为[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")的翻译，添加自己的仓库，请移步[英文原始页面](/index.php/Unofficial_user_repositories "Unofficial user repositories")。

如果你有自己的仓库，请添加到本页面中，这样其他用户就会知道哪里去找你的软件。 在添加新的仓库时请保持队形，并遵守下列规则：

*   请按罗马字首排序列表。
*   包含维护者的一些信息：包括至少一个名字（昵称也行）以及一些具有联系方式的信息（网址，邮箱，用户ArchWiki页面或者论坛帖子等等）。
*   如果仓库是签名的，请添加一个key-id，最好把它编辑成一个链到密匙服务器的连接，直接连到密钥文件上。
*   包含一些简短的描述（软件包的分类什么的）
*   如果你有一个介绍性的网页（无论是ArchWiki或者其他网站），请添加一个连接。
*   如果可能，不要在配置文件中添加注释，而是写在前面的描述中。
*   一些仓库也有除 x86_64 架构以外的软件包。 变量 `$arch` 将会被 pacman 自动设置。

### archlinuxcn

*   **维护者s:** [Phoenix Nemo (phoenixlzx)](https://plus.google.com/+PhoenixNemo/), [Felix Yan (felixonmars, dev)](https://www.archlinux.org/people/developers/#fyan), [lilydjwg](https://twitter.com/lilydjwg), [farseerfc (TU)](https://www.archlinux.org/people/trusted-users/#farseerfc), and [others](https://github.com/archlinuxcn/repo/graphs/contributors)
*   **描述:** Packages by the Chinese Arch Linux community, all signed. Be aware that i686 packages are not fully maintained and tested, create an issue if you find some problems.由中国 Arch Linux 社区提供的软件包均已签名。 请注意，i686 软件包尚未完全维护和测试，如果发现一些问题，请创建一个 issue 。
*   **Git Repo:** [https://github.com/archlinuxcn/repo](https://github.com/archlinuxcn/repo)
*   **Issue tracking:** [https://github.com/archlinuxcn/repo/issues](https://github.com/archlinuxcn/repo/issues) for packaging issues, out-of-date notifications, package requests, and related questions
*   **Mirrors:** [https://github.com/archlinuxcn/mirrorlist-repo](https://github.com/archlinuxcn/mirrorlist-repo) (Mostly for users in mainland China), or install *archlinuxcn-mirrorlist-git* from the repo.
*   **Key-ID:** 添加 archlinuxcn 源之后，必须先安装 *archlinuxcn-keyring* 钥匙环，之后才可以安装任何其它包，否则会出现 GPG 错误。*archlinuxcn-keyring* 本身由 TU 签名。

```
[archlinuxcn]
Server = http://repo.archlinuxcn.org/$arch
## or install archlinuxcn-mirrorlist-git and use the mirrorlist
#Include = /etc/pacman.d/archlinuxcn-mirrorlist

```

## Signed

### andontie-aur

*   **维护者:** Holly M.
*   **描述:** 包含最流行的 AUR 软件包以及我一直使用的软件包的仓库。在上游网站请求新软件包。
*   **Key-ID:** EA50C866329648EE
*   **Upstream page:** [https://aur.andontie.net](https://aur.andontie.net)

```
[andontie-aur]
Server = https://aur.andontie.net/$arch

```

### AniNIX

*   **维护者:** [DarkFeather](http://foundation.aninix.net/DarkFeather)
*   **描述:** 支持开源网络安全研究的自行编写的和 AUR 软件包 Self-written and AUR packages to support open-source cybersecurity research
*   '**Key-ID:** 904DE6275579CB589D85720C1CC1E3F4ED06F296
*   **Upstream page:** [https://aninix.net](https://aninix.net)
*   **Git and issue tracking:** [https://foundation.aninix.net/](https://foundation.aninix.net/)
*   **Contact:** [ircs://aninix.net:6697/#lobby](ircs://aninix.net:6697/#lobby)

```
[AniNIX]
Server = https://maat.aninix.net/

[aur]
Server = https://maat.aninix.net/aur/

```

### arcanisrepo

*   **维护者:** [arcanis](https://www.archlinux.org/people/trusted-users/#arcanis)
*   **描述:** 包含一些 AUR 软件包（包括来自 VCS 的软件包）的存储库
*   **Key-ID:** 不必，维护者是授信用户

```
[arcanisrepo]
Server = https://repo.arcanis.me/repo/$arch

```

(It is also available via FTP with the same URL.)

### arch4edu

*   **维护者s:** [Jingbei Li (petronny)](https://github.com/petronny), and [others](https://github.com/arch4edu/arch4edu/graphs/contributors)
*   **描述:** arch4edu是 Archlinux 和 ArchlinuxARM 的社区存储库，致力于提供大学生使用的大多数软件的最新版本。
*   **Git Repo:** [https://github.com/arch4edu/arch4edu](https://github.com/arch4edu/arch4edu)
*   **Issue tracking:** [https://github.com/arch4edu/arch4edu/issues](https://github.com/arch4edu/arch4edu/issues) for packaging issues, out-of-date notifications, package requests, and related questions
*   **Mirrors:** [https://github.com/arch4edu/arch4edu/wiki/Add-arch4edu-to-your-Archlinux](https://github.com/arch4edu/arch4edu/wiki/Add-arch4edu-to-your-Archlinux)
*   **Key-ID:** 7931B6D628C8D3BA

```
[arch4edu]
Server = https://mirrors.tuna.tsinghua.edu.cn/arch4edu/$arch
## or other mirrors in https://github.com/arch4edu/arch4edu/wiki/Add-arch4edu-to-your-Archlinux

```

### archstrike

*   **维护者:** [The ArchStrike Team](https://archstrike.org/team)
*   **描述:** 安全专业人员和爱好者的存储库
*   **Upstream page:** [https://archstrike.org/](https://archstrike.org/)
*   **Key-ID:** 9D5F1C051D146843CDA4858BDE64825E7CBC0D51

**Note:** 可以在 [https://archstrike.org/wiki/setup](https://archstrike.org/wiki/setup) 上找到 ArchStrike 的特定说明。

```
[archstrike]
Server = https://mirror.archstrike.org/$arch/$repo

```

### archzfs

*   **维护者:** [Jan Houben (minextu)](https://aur.archlinux.org/account/minextu)
*   **描述:** Arch Linux 上 ZFS 的软件包。
*   **Upstream page:** [https://github.com/archzfs/archzfs](https://github.com/archzfs/archzfs)
*   **Key-ID:** F75D9D76

```
[archzfs]
Server = http://archzfs.com/$repo/x86_64

```

### archzfs-kernels

*   **维护者:** [Endre Szabo](https://aur.archlinux.org/account/endre/)
*   **描述:** Official kernel packages matching the most recent [ZFS packages](#_archzfs) kernel version dependencies. Use this to be able to upgrade your kernel package every time whilst using ZFS packages above :)
*   **Upstream page:** [https://end.re/archzfs-kernels/](https://end.re/archzfs-kernels/)
*   **Key-ID:** Not needed as packages are from core repos and signed officially.

```
[archzfs-kernels]
Server = http://end.re/$repo/

```

### ashleyis

*   **维护者:** Ashley Towns ([ashleyis](https://aur.archlinux.org/account/ashleyis/))
*   **描述:** Debug versions of SDL, chipmunk, libtmx and other misc game libraries. also swift-lang and some other AUR packages
*   **Key-ID:** B1A4D311

```
[ashleyis]
Server = http://arch.ashleytowns.id.au/repo/$arch

```

### Bennix Repo

*   **维护者:** Ben P. Dorsi-Todaro ([Tech Me Out](https://techmeout.org))
*   **描述:** [Ben P. Dorsi-Todaro](http://ben-dorsi-todaro.com/)使用且未在仓库中列出，或[Big Ben's Web Hosting](http://www.bigbenshosting.com/)的软件包
*   **Key-ID:** F14BB858F6253DA0

```
[bigben-repo]
SigLevel = Optional TrustAll
Server = http://bennix.net/bigben-repo/

```

### blackeagle-pre-community

*   **维护者:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **描述:** testing of the by me maintaned packages before moving to *community* repository
*   **Key-ID:** Not required, as maintainer is a TU

```
[blackeagle-pre-community]
Server = https://repo.herecura.be/$repo/$arch

```

### chaotic-aur

*   **维护者:** [PedroHLC](https://github.com/pedrohlc), and [Librewish](https://github.com/librewish)
*   **描述:** 自动构建维护者使用的AUR软件包，每小时更新一次（有一些每天更新一次）。托管在巴西圣卡洛斯。在德国和美国有镜像。 Only x86_64。拥有1600多个包。
*   **Key-ID:** [[1]](http://pool.sks-keyservers.net/pks/lookup?search=0x3056513887B78AEB&fingerprint=on&op=index), fingerprint `EF92 5EA6 0F33 D0CB 85C4 4AD1 3056 5138 87B7 8AEB`
*   **Note:** See [maintainer's notes](https://lonewolf.pedrohlc.com/chaotic-aur).

```
[chaotic-aur]
Server = http://lonewolf-builder.duckdns.org/$repo/x86_64
Server = http://chaotic.bangl.de/$repo/x86_64
Server = https://repo.kitsuna.net/x86_64

```

### catalyst

*   **维护者:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **描述:** ATI Catalyst 专有驱动程序。
*   **Key-ID:** 653C3094

```
[catalyst]
Server = http://167.86.114.169/arch/catalyst/$arch

```

### catalyst-hd234k

*   **维护者:** [Vi0l0](/index.php/User:Vi0L0 "User:Vi0L0")
*   **描述:** ATI Catalyst 专有驱动程序。
*   **Key-ID:** 653C3094

```
[catalyst-hd234k]
Server = http://167.86.114.169/arch/catalyst-hd234k/$arch

```

### city

*   **维护者:** [Balló György](https://www.archlinux.org/people/trusted-users/#bgyorgy)
*   **描述:** 实验性/不受欢迎的软件包。
*   **Upstream page:** [https://pkgbuild.com/~bgyorgy/city.html](https://pkgbuild.com/~bgyorgy/city.html)
*   **Key-ID:** Not needed, as maintainer is a TU

```
[city]
Server = https://pkgbuild.com/~bgyorgy/$repo/os/$arch

```

### coderkun-aur

*   **维护者:** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **描述:** AUR packages with random software. Supporting package deltas and package and database signing.带有随机软件的AUR软件包。支持软件包增量以及软件包和数据库签名。
*   **Upstream page:** [https://www.suruatoel.xyz/arch](https://www.suruatoel.xyz/arch)
*   **Key-ID:** 39E27199A6BEE374
*   **Keyfile:** [https://www.suruatoel.xyz/coderkun.asc](https://www.suruatoel.xyz/coderkun.asc)

```
[coderkun-aur]
Server = http://arch.suruatoel.xyz/$repo/$arch/

```

### coderkun-aur-audio

*   **维护者:** [coderkun](https://aur.archlinux.org/account/coderkun/)
*   **描述:** 带有音频相关软件的AUR软件包(realtime kernels, lv2-plugins, …)。 支持软件包增量以及软件包和数据库签名。
*   **Upstream page:** [https://www.suruatoel.xyz/arch](https://www.suruatoel.xyz/arch)
*   **Key-ID:** 39E27199A6BEE374
*   **Keyfile:** [https://www.suruatoel.xyz/coderkun.key](https://www.suruatoel.xyz/coderkun.key)

```
[coderkun-aur-audio]
Server = http://arch.suruatoel.xyz/$repo/$arch/

```

### devkitpro

*   **维护者:** [wintermute](https://devkitpro.org/)
*   **描述:** 提供 Nintendo Wii，Gamecube，DS，GBA，Gamepark gp32 和 Nintendo Switch 的 Homebrew 工具链
*   **Upstream page:** [https://devkitpro.org/wiki/devkitPro_pacman](https://devkitpro.org/wiki/devkitPro_pacman)
*   **Key-ID:** F7FD5492264BB9D0

**Note:** 存储库在 [https://downloads.devkitpro.org/devkitpro-keyring-r1.787e015-2-any.pkg.tar.xz](https://downloads.devkitpro.org/devkitpro-keyring-r1.787e015-2-any.pkg.tar.xz) 中具有自己的附加密钥环.

```
[dkp-libs]
Server = https://downloads.devkitpro.org/packages
[dkp-linux]
Server = https://downloads.devkitpro.org/packages/linux

```

### disastrousaur

*   **维护者:** [TheGoliath](https://aur.archlinux.org/account/TheGoliath)
*   **描述:** 著名的 AUR 软件包管理器，AUR 上许多最受欢迎的软件包以及我所喜欢的软件包
*   **Upstream page:** [https://mirror.repohost.de/disastrousaur](https://mirror.repohost.de/disastrousaur)
*   **Key-ID:** CBAE582A876533FD
*   **Keyfile:** [https://mirror.repohost.de/disastrousaur.key](https://mirror.repohost.de/disastrousaur.key)

**Warning:** 现在 Disasterusaur 和 Disasterusarm 已合并为 Disasterusaur 名称。请确保已相应更改仓库的服务器URL。 当我有足够的时间实行，可能会出现其他体系的构建.

```
[disastrousaur]
Server = https://mirror.repohost.de/$repo/$arch

```

### dvzrv

*   **维护者:** [David Runge](https://www.archlinux.org/people/developers/#dvzrv)
*   **描述:** [Realtime kernel patchset](/index.php/Realtime_kernel_patchset "Realtime kernel patchset") (aka. [linux-rt](https://aur.archlinux.org/packages/linux-rt/) and [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/))
*   **Key-ID:** Not needed, as maintainer is a developer/TU

```
[dvzrv]
Server = https://pkgbuild.com/~dvzrv/repo/$arch

```

### ear

*   **维护者:** [Ward Segers](https://wardsegers.be),
*   **描述:** Editicalu's ArchLinux Repository. Contains precompiled AUR packages (mostly the ones maintained by editicalu)
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

*   **维护者:** bentglasstube
*   **描述:** Packages for software written by (and a few just compiled by) bentglasstube.

```
[eatabrick]
Server = http://repo.eatabrick.org/$arch

```

### eschwartz

*   **维护者:** [Eli Schwartz](https://www.archlinux.org/people/trusted-users/#eschwartz)
*   **描述:** 带有 AUR 软件包和 git 中一些核心软件包的个人仓库（包括 glibc 和 pacman ）。 包含调试包。
*   **Key-ID:** Not needed, as maintainer is a TU

```
[eschwartz]
Server = https://pkgbuild.com/~eschwartz/repo/$arch

```

### ffy00

*   **维护者:** [Filipe Laíns](https://www.archlinux.org/people/trusted-users/#FFY00)
*   **描述:** 个人仓库。包含一些与D语言有关的软件包。
*   **Key-ID:** Not needed, as maintainer is a TU

```
[ffy00]
Server = https://pkgbuild.com/~ffy00/repo

```

### fusion809

*   **维护者:** [Horne](https://aur.archlinux.org/account/fusion809%7CBrenton)] (brentonhorne77 at gmail dot com).
*   **描述:** 提供一些 AUR 和其他我喜欢的软件包。 类似于 CodeLite 和 bleeding-edge (latest release within 1 day of its release) GVim (GTK 2 interface).
*   **Package list:** [http://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/](http://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/)
*   **Key-ID:** 03264DDCD606DC98
*   **Keyfile:** [https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/home_fusion809_Arch_Extra.key](https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/x86_64/home_fusion809_Arch_Extra.key)

```
[home_fusion809_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/fusion809/Arch_Extra/$arch

```

### grawlinson

*   **维护者:** [George Rawlinson](https://aur.archlinux.org/account/grawlinson)
*   **描述:** 用户维护的AUR软件包以及一些实验软件包。
*   **Package list:** [https://repo.nullpointer.io](https://repo.nullpointer.io)
*   **Key-ID:** 25ea6900d9ea5ebc
*   **Keyfile:** [https://nullpointer.io/grawlinson.key](https://nullpointer.io/grawlinson.key)

```
[grawlinson]
Server = https://repo.nullpointer.io

```

### gnome-devel

*   **维护者:** [Andres Fernandez](https://plus.google.com/+AndresFernandezperonista), [Fernando Fernandez](https://plus.google.com/+FernandoFernandezBerel)
*   **描述:** GNOME development releases. For testing purposes only.
*   **Package list:** [https://softwareperonista.com.ar/repo/archlinux/gnome-devel/x86_64/](https://softwareperonista.com.ar/repo/archlinux/gnome-devel/x86_64/)
*   **Key-ID:** DDCE9FD63370080B

**Note:** Must be put above `[testing]` repository.

```
[gnome-devel]
Server = https://softwareperonista.com.ar/repo/archlinux/gnome-devel/$arch

```

### herecura

*   **维护者:** [Ike Devolder](https://www.archlinux.org/people/trusted-users/#idevolder)
*   **描述:** 在 *community* 库未找到的额外的软件包
*   **Key-ID:** Not required, as maintainer is a TU

```
[herecura]
Server = https://repo.herecura.be/$repo/$arch

```

### holo

*   **维护者:** Stefan Majewsky <holo-pacman@posteo.de> (please prefer to report issues at [Github](https://github.com/majewsky/holo-pacman-repo/issues))
*   **描述:** Packages for [Holo configuration management](https://holocm.org), including compatible plugins and tools.
*   **Upstream page:** [https://github.com/majewsky/holo-pacman-repo](https://github.com/majewsky/holo-pacman-repo)
*   **Package list:** [https://repo.holocm.org/archlinux/x86_64](https://repo.holocm.org/archlinux/x86_64)
*   **Key-ID:** 0xF7A9C9DC4631BD1A

```
[holo]
Server = https://repo.holocm.org/archlinux/x86_64

```

### ivasilev

*   **维护者:** [Ianis G. Vasilev](https://ivasilev.net)
*   **描述:** 各种软件包，主要是我自己的软件和AUR构建。
*   **Upstream page:** [https://ivasilev.net/pacman](https://ivasilev.net/pacman)
*   **Key-ID:** [17DAB671](https://pgp.mit.edu/pks/lookup?op=vindex&search=0xB77A3C8832838F1F80ADFD7E1D0507B417DAB671)

```
[ivasilev]
Server = https://ivasilev.net/pacman/$arch

```

### jlk

*   **维护者:** [Jakub Klinkovský](/index.php/User:Lahwaacz "User:Lahwaacz")
*   **描述:** Various packages from the ABS and AUR. Modified packages are in the `modified` group.
*   **Upstream page:** [https://jlk.fjfi.cvut.cz/arch/repo/README.html](https://jlk.fjfi.cvut.cz/arch/repo/README.html)
*   **Key-ID:** 932BA3FA0C86812A32D1F54DAB5964AEB9FEDDDC

```
[jlk]
Server = https://jlk.fjfi.cvut.cz/arch/repo

```

### llvm-svn

*   **维护者:** [Luchesar V. ILIEV (kerberizer)](/index.php/User:Kerberizer "User:Kerberizer")
*   **描述:** [llvm-svn](https://aur.archlinux.org/pkgbase/llvm-svn) and [lib32-llvm-svn](https://aur.archlinux.org/pkgbase/lib32-llvm-svn) from AUR: the LLVM compiler infrastructure, the Clang frontend, and the tools associated with it
*   **Key-ID:** [0x76563F75679E4525](https://sks-keyservers.net/pks/lookup?op=vindex&search=0x76563F75679E4525&fingerprint=on&exact=on), fingerprint `D16C F22D 27D1 091A 841C 4BE9 7656 3F75 679E 4525`

```
[llvm-svn]
Server = https://repos.uni-plovdiv.net/archlinux/$repo/$arch

```

### markzz

*   **维护者:** [Mark Weiman (markzz)](/index.php/User:Markzz "User:Markzz")
*   **描述:** Packages that markzz maintains or uses on the AUR; this includes Linux with the vfio patchset ([linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) and [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)), and packages for analysis of network data.
*   **Key ID:** DEBB9EE4

**Note:** If you want to add the key by installing the *markzz-keyring* package, temporarily add `SigLevel = Never` into the repository section.

```
[markzz]
Server = https://repo.markzz.com/arch/$repo/$arch

```

### maximbaz

*   **维护者:** [Maxim Baz](https://www.archlinux.org/people/trusted-users/#maximbaz)
*   **描述:** Personal repo with AUR packages.
*   **Key-ID:** Not needed, as maintainer is a TU

```
[maximbaz]
Server = https://pkgbuild.com/~maximbaz/repo/

```

### me176c

*   **维护者:** [lambdadroid](https://github.com/lambdadroid)
*   **描述:** Packages for [ASUS MeMO Pad 7 (ME176C(X))](/index.php/ASUS_MeMO_Pad_7_(ME176C(X)) "ASUS MeMO Pad 7 (ME176C(X))")
*   **Key-ID:** 2B1138A8BB59D786A3BF42AAD996DA70572407FB

```
[me176c]
Server = https://me176c.uber.space/archlinux

```

### miffe

*   **维护者:** [miffe](https://bbs.archlinux.org/profile.php?id=4059)
*   **描述:** miffe 维护的 AUR 软件包, e.g. linux-mainline
*   **Key ID:** 313F5ABD

```
[miffe]
Server = https://arch.miffe.org/$arch/

```

### mikelpint

*   **维护者:** [Mikel Pintado (Mikelpint)](/index.php/User:Mikelpint "User:Mikelpint")
*   **描述:** Packages that mikelpint maintains in the AUR.
*   **Key ID:** 5CA78FC65B189E2B

```
[mikelpint]
Server = https://mikelpint.github.io/repository/archlinux/repo

```

### Minerva W Science

*   **维护者:** Minerva W
*   **描述:** [OpenFOAM](/index.php/OpenFOAM "OpenFOAM") packages.
*   **Key-ID:** 3FF21B78117507DA
*   **Keyfile:** [https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/x86_64/home_Minerva_W_Science_Arch_Extra.key](https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/x86_64/home_Minerva_W_Science_Arch_Extra.key)

```
[home_Minerva_W_Science_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/Minerva_W:/Science/Arch_Extra/$arch 

```

### mobile

*   **维护者:** [farwayer](https://keybase.io/farwayer)
*   **描述:** React Native and Android development
*   **Upstream page:** [https://keybase.pub/farwayer/arch/mobile/](https://keybase.pub/farwayer/arch/mobile/)
*   **Key ID:** 7943315502A936D7

```
[mobile]
Server = https://farwayer.keybase.pub/arch/$repo

```

### nah

*   **维护者:** [phillid](https://yeah.nah.nz)
*   **描述:** Pre-built versions of the (slow-to-build) graph-tool python libraries, mingw-w64
*   **Key ID:** 7BF3D17D0884BF5B

```
[nah]
Server = https://repo.nah.nz/$repo

```

### nickcao

*   **维护者:** [NickCao](https://nichi.co/about)
*   **描述:** Some (useful for some) packages from me, and some aur packages I personally use.
*   **Key-ID:** 09CC69622E8D4EE343B4E8954D0BA456DF028C15

```
[nickcao]
Server = https://repo.nichi.co/$arch

```

### origincode

*   **维护者:** [OriginCode](https://aur.archlinux.org/account/OriginCode)
*   **描述:** A few staging or testing packages from [#archlinuxcn](#archlinuxcn), and some daily use packages.
*   **Key-ID:** 0A5BAD445D80C1CC & 62BF97502AE10D22

```
[origincode]
Server = https://repo.origincode.me/repo/$arch

```

### pkgbuilder

*   **维护者:** [Chris Warrick](https://chriswarrick.com/)
*   **描述:** A repository for PKGBUILDer, a Python AUR helper.
*   **Upstream page:** [https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder)
*   **Key-ID:** 5EAAEA16

```
[pkgbuilder]
Server = https://pkgbuilder-repo.chriswarrick.com/

```

### post-factum kernels

*   **维护者**: [Oleksandr Natalenko aka post-factum](https://aur.archlinux.org/account/post-factum)
*   **Upstream page**: [https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README)
*   **描述**: [pf-kernel](/index.php/Kernel#Major_patchsets "Kernel") packages by its developer, post-factum
*   **Key-ID:**: 95C357D2AF5DA89D
*   **Keyfile**: [https://download.opensuse.org/repositories/home:/post-factum:/kernels/Arch/x86_64/home_post-factum_kernels_Arch.key](https://download.opensuse.org/repositories/home:/post-factum:/kernels/Arch/x86_64/home_post-factum_kernels_Arch.key)

```
[home_post-factum_kernels_Arch]
Server = https://download.opensuse.org/repositories/home:/post-factum:/kernels/Arch/$arch

```

### QOwnNotes

*   **维护者:** [Patrizio Bekerle](https://aur.archlinux.org/account/pbek) (pbek), QOwnNotes author
*   **描述:** QOwnNotes是一个开源记事本和待办事项列表管理器，具有降价支持和 [ownCloud](/index.php/OwnCloud "OwnCloud") integration.
*   **Key-ID:** FFC43FC94539B8B0
*   **Keyfile:** [https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/x86_64/home_pbek_QOwnNotes_Arch_Extra.key](https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/x86_64/home_pbek_QOwnNotes_Arch_Extra.key)

```
[home_pbek_QOwnNotes_Arch_Extra]
Server = https://download.opensuse.org/repositories/home:/pbek:/QOwnNotes/Arch_Extra/$arch

```

### qt-debug

*   **维护者:** [The Compiler](https://aur.archlinux.org/account/The-Compiler)
*   **描述:** Qt/PyQt builds with debug symbols
*   **Upstream page:** [https://github.com/qutebrowser/qt-debug-pkgbuild](https://github.com/qutebrowser/qt-debug-pkgbuild)
*   **Key-ID:** D6A1C70FE80A0C82

```
[qt-debug]
Server = https://qutebrowser.org/qt-debug/$arch

```

### quarry

*   **维护者:** [anatolik](https://www.archlinux.org/people/developers/#anatolik)
*   **描述:** Arch binary repository for [Rubygems](http://rubygems.org/) packages. See [forum announcement](https://bbs.archlinux.org/viewtopic.php?id=182729) for more information.
*   **Sources:** [https://github.com/anatol/quarry](https://github.com/anatol/quarry)
*   **Key-ID:** Not needed, as maintainer is a developer

```
[quarry]
Server = https://pkgbuild.com/~anatolik/quarry/x86_64/

```

### repo-ck

Kernel and modules with Brain Fuck Scheduler and all the goodies in the ck1 patch set. 带有Brain Fuck Scheduler的内核和模块以及ck1补丁程序集中的所有功能。

See [/Repo-ck](/index.php?title=Unofficial_user_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Repo-ck&action=edit&redlink=1 "Unofficial user repositories (简体中文)/Repo-ck (page does not exist)").

### seblu

*   **维护者:** [Sébastien Luttringer](https://www.archlinux.org/people/developers/#seblu)
*   **描述:** 所有seblu有用的预制包，有些是自制的 (linux-seblu-meta, zfs-dkms, spotify, masterpdfeditor, etc).
*   **Key-ID:** Not required, as maintainer is a Developer

```
[seblu]
Server = https://al1.seblu.net/$repo/$arch
Server = https://al2.seblu.net/$repo/$arch

```

### seiichiro

*   **维护者:** [Stefan Brand (seiichiro0185)](https://www.seiichiro0185.org)
*   **描述:** AUR-packages I use frequently
*   **Key-ID:** 805517CC

```
[seiichiro]
Server = https://www.seiichiro0185.org/repo/$arch

```

### selinux

*   **维护者:** [swordfeng](https://github.com/swordfeng)
*   **描述:** Unofficial (personal) builds for [SELinux](/index.php/SELinux "SELinux") packages. PKGBUILDs are taken from AUR instead of the upstream GitHub repo.
*   **Upstream page:** [https://github.com/archlinuxhardened/selinux](https://github.com/archlinuxhardened/selinux)
*   **Key-ID:** 7691FA63FE91CAFDD42A4AF08323B00E97DF0E6D (subkey B988167F59A3AF8368D55D65A7862FD48B72D83B is specifically used for signing packages)
*   **Keyfile:** [https://repo.taiho.moe/key.asc](https://repo.taiho.moe/key.asc)

```
[selinux]
Server = https://repo.taiho.moe/$repo

```

### sergej-repo

*   **维护者:** [Sergej Pupykin](https://www.archlinux.org/people/trusted-users/#spupykin)
*   **描述:** psi-plus, owncloud-git, ziproxy, android, MySQL, and other stuff. Some packages also available for armv7h.
*   **Key-ID:** Not required, as maintainer is a TU

```
[sergej-repo]
Server = http://repo.p5n.pp.ru/$repo/os/$arch

```

### siosm-aur

*   **维护者:** [Timothee Ravier](https://tim.siosm.fr/about/)
*   **描述:** packages also available in the Arch User Repository, sometimes with minor fixes
*   **Upstream page:** [https://tim.siosm.fr/repositories/](https://tim.siosm.fr/repositories/)
*   **Key-ID:** 78688F83

```
[siosm-aur]
Server = http://siosm.fr/repo/$repo/

```

### sublime-text

*   **维护者:** Sublime Text developer
*   **描述:** Sublime Text editor packages from developer's repository
*   **Upstream page:** [https://www.sublimetext.com/docs/3/linux_repositories.html#pacman](https://www.sublimetext.com/docs/3/linux_repositories.html#pacman)
*   **Key-ID:** 8A8F901A

```
[sublime-text]
Server = https://download.sublimetext.com/arch/stable/x86_64

```

### subtitlecomposer

*   **维护者:** Mladen Milinkovic (maxrd2)
*   **描述:** Subtitle Composer stable and nightly builds
*   **Upstream page:** [https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer)
*   **Key-ID:** EF9D9B26

```
[subtitlecomposer]
Server = https://smoothware.net/$repo/$arch

```

### trinity

*   **维护者:** Michael J. Manley <mmanley@ntge.net>
*   **描述:** [Trinity](/index.php/Trinity "Trinity") 桌面环境
*   **Key-ID:** 5F710C1E

```
[trinity]
Server = https://repo.nasutek.com/arch/contrib/trinity/x86_64

```

### valveaur

*   **维护者:** John Schoenick <johns@valvesoftware.com> ([https://valvesoftware.com](https://valvesoftware.com))
*   **描述:** A repository by Valve Software Providing The Linux-fsync kernel and modules, including the futex-wait-multiple patchset for testing with Proton fsync & Mesa with the ACO compiler patchset. Valve Software的存储库，提供Linux-fsync内核和模块，包括futex-wait-multiple补丁集，用于使用Proton fsync＆Mesa和ACO编译器补丁集进行测试。
*   **Upstream page:** [https://steamcommunity.com/linux](https://steamcommunity.com/linux)
*   **Key-ID:** 8DC2CE3A3D245E64

```
[valveaur]
Server = http://repo.steampowered.com/arch/valveaur

```

### xuanrui

*   **维护者:** [Xuanrui Qi (xuanruiqi)](https://aur.archlinux.org/account/xuanruiqi)
*   **描述:** xuanruiqi's own packages and frequently-used packages, mainly of interest to functional programmers.
*   **Upstream Page:** [https://www.xuanruiqi.com/linux.html](https://www.xuanruiqi.com/linux.html)
*   **Key-ID:** 6E06FBC8

```
[xuanrui]
Server = https://arch.xuanruiqi.com/repo

```

### xyne-x86_64

*   **维护者:** [Xyne](https://www.archlinux.org/people/trusted-users/#xyne)
*   **描述:** A repository for Xyne's own projects.
*   **Upstream page:** [http://xyne.archlinux.ca/projects/](http://xyne.archlinux.ca/projects/)
*   **Key-ID:** Not required, as maintainer is a TU

```
[xyne-x86_64]
# Server = https://xyne.archlinux.ca/repos/xyne # It returns error 404 or 406 (varying). Use the line below:
Server = http://xyne.archlinux.ca/bin/repo.php?file=

```

### home-thaodan

*   **维护者**: [Thaodan](https://aur.archlinux.org/account/Thaodan)
*   **Upstream page**: [https://gitlab.com/Thaodan/linux-pf](https://gitlab.com/Thaodan/linux-pf)
*   **描述**: [pf-kernel](/index.php/Kernel#Major_patchsets "Kernel") and other packages by pf-kernel fork developer, Thaodan
*   **Gitlab Project**: [https://gitlab.com/Thaodan/repo-home-thaodan-repo](https://gitlab.com/Thaodan/repo-home-thaodan-repo)
*   **Key-ID:**: BBFE2FD421597395E4FC8C8DF6C85FEE79D661A4

```
[home-thaodan]
Server = https://thaodan.de/public/archlinux/home-thaodan/$arch

```

## Unsigned

**Note:** 用户将需要在这些条目中添加以下内容: `SigLevel = PackageOptional`

### alucryd

*   **维护者:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **描述:** Various packages Maxime Gauduin maintains (or not) in the AUR.

```
[alucryd]
Server = https://pkgbuild.com/~alucryd/$repo/x86_64

```

### alucryd-multilib

*   **维护者:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **描述:** 在没有运行时环境的情况下运行 Steam 所需的各种软件包.

```
[alucryd-multilib]
Server = https://pkgbuild.com/~alucryd/$repo/x86_64

```

### andrwe

*   **维护者:** Andrwe Lord Weber
*   **描述:** contains programs I'm using on many systems
*   **Upstream page:** [http://andrwe.org/linux/repository](http://andrwe.org/linux/repository)

```
[andrwe]
Server = http://repo.andrwe.org/$arch

```

### archgeotux

*   **维护者:** Samuel Mesa
*   **描述:** Geospatial and geographic information system applications
*   **Upstream page:** [https://archgeotux.sourceforge.io/](https://archgeotux.sourceforge.io/)

```
[archgeotux]
Server = https://downloads.sourceforge.net/project/archgeotux/$arch

```

### archlinuxfr

*   **维护者:**
*   **描述:**
*   **Upstream page:** [http://afur.archlinux.fr](http://afur.archlinux.fr)

```
[archlinuxfr]
Server = http://repo.archlinux.fr/$arch

```

### archlinuxgr

*   **维护者:**
*   **描述:** many interesting packages provided by the Hellenic (Greek) Arch Linux community

```
[archlinuxgr]
Server = http://archlinuxgr.tiven.org/archlinux/$arch

```

### archlinuxgr-kde4

*   **维护者:**
*   **描述:** KDE4 packages (plasmoids, themes etc) provided by the Hellenic (Greek) Arch Linux community

```
[archlinuxgr-kde4]
Server = http://archlinuxgr.tiven.org/archlinux-kde4/$arch

```

### aur-av-bin

*   **维护者:** [milkii](https://aur.archlinux.org/account/milk/) (ping me on Freenode)
*   **描述:** 预编译的 Arch Linux 二进制软件包，主要包含来自 AUR 的与音频及音乐相关的软件。
*   **Upstream page:** [https://github.com/mxmilkb/aur-av-bin](https://github.com/mxmilkb/aur-av-bin)

```
[aur-av-bin]
SigLevel = PackageOptional
Server = https://github.com/mxmilkb/aur-av-bin/releases/download/repository

```

### craftdestiny

*   **维护者:** [LinuxVieLoisir](https://craftdestiny.ovh)
*   **描述:** A Craft Destiny repository is there to avoid long compilation on some software. It also adds some very useful additional software.

```
[craftdestiny]
Server = https://miroir.craftdestiny.ovh/archlinux-repo/

```

### dx37essentials

*   **维护者:** [DragonX256](https://aur.archlinux.org/account/DragonX256)
*   **描述:** Personal repository. Contains packages from AUR, which I using every day.
*   **Git repo:** [https://gitlab.com/DX37/dx37essentials](https://gitlab.com/DX37/dx37essentials)
*   **Upstream page:** [https://dx37.gitlab.io/dx37essentials](https://dx37.gitlab.io/dx37essentials)

```
[dx37essentials]
Server = https://dx37.gitlab.io/$repo/$arch

```

### heftig

*   **维护者:** [Jan Steffens](https://www.archlinux.org/people/developers/#heftig)
*   **描述:** Includes pulseaudio-git, pavucontrol-git, and firefox-developer-edition
*   **Upstream page:** [https://bbs.archlinux.org/viewtopic.php?id=117157](https://bbs.archlinux.org/viewtopic.php?id=117157)

```
[heftig]
Server = https://pkgbuild.com/~heftig/repo/$arch

```

### jkanetwork

*   **维护者:** kprkpr <kevin01010 at gmail dot com>
*   **维护者:** Joselucross <jlgarrido97 at gmail dot com>
*   **描述:** Packages of AUR like pimagizer,stepmania,yaourt,linux-mainline,wps-office,grub-customizer,some IDE.. Open for all that wants to contribute
*   **Upstream page:** [http://repo.jkanetwork.com/](http://repo.jkanetwork.com/)

```
[jkanetwork]
Server = http://repo.jkanetwork.com/repo/$repo/

```

### kodi-devel-prebuilt

*   **维护者:** asm0dey <pavel.finkelshtein+AUR@gmail.com>
*   **描述:** Prebuilt packages of kodi-devel from AUR
*   **Upstream page:** [kodi-devel](https://aur.archlinux.org/packages/kodi-devel/)

```
[kodi-devel-prebuilt]
Server = https://asm0dey.github.io/$repo/$arch
SigLevel = PackageOptional

```

### mesa-git

*   **维护者:** [Laurent Carlier](https://www.archlinux.org/people/trusted-users/#lcarlier)
*   **描述:** Mesa git builds for the *testing* and *multilib-testing* repositories

```
[mesa-git]
Server = https://pkgbuild.com/~lcarlier/$repo/$arch

```

### Mountain

*   **维护者:** [Minzord](https://mountainlinux.wordpress.com)
*   **描述:** Popular AUR Packages and some Driver Wifi.

```
[Mountain]
SigLevel = Never
Server = https://mountain-linux.github.io/Mountain/$arch

```

### oracle

*   **维护者:** [User:Malvineous](/index.php/User:Malvineous "User:Malvineous")
*   **描述:** [Oracle Database client](/index.php/Oracle_Database_client "Oracle Database client") and associated tools, built from AUR packages and hosted on AWS S3 using [Makefile scripts](https://github.com/Malvineous/archlinux-pacman-repo).
*   **Conditions:** By using this repository you agree to the [Oracle Technology Network Development and Distribution License Terms for Instant Client](http://www.oracle.com/technetwork/licenses/instant-client-lic-152016.html).

```
[oracle]
Server = http://linux.shikadi.net/arch/$repo/$arch/

```

### ownstuff

*   **维护者:** [Martchus](https://aur.archlinux.org/account/Martchus)
*   **描述:** A lot of packages from the AUR, e.g. a great number packages for mingw-w64 and Android cross compilation, fonts, Perl modules, tools like [tageditor](https://aur.archlinux.org/packages/tageditor/), [syncthingtray](https://aur.archlinux.org/packages/syncthingtray/), [subtitlecomposer](https://aur.archlinux.org/packages/subtitlecomposer/) and [qmplay2](https://aur.archlinux.org/packages/qmplay2/)
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

*   **维护者:** [Maxime Gauduin](https://www.archlinux.org/people/trusted-users/#alucryd)
*   **描述:** Repository containing Pantheon-related packages

```
[pantheon]
Server = https://pkgbuild.com/~alucryd/$repo/$arch

```

### pietma

*   **维护者:** MartiMcFly <martimcfly@autorisation.de>
*   **描述:** Arch User Repository packages [I create or maintain.](https://aur.archlinux.org/packages/?K=martimcfly&SeB=m).
*   **Upstream page:** [http://pietma.com/tag/aur/](http://pietma.com/tag/aur/)

```
[pietma]
Server = http://repository.pietma.com/nexus/content/repositories/archlinux/$arch/$repo

```

### pnsft-pur

*   **维护者:** [ponsfoot](https://aur.archlinux.org/account/ponsfoot)
*   **描述:** Japanese input method packages Mozc (vanilla) and libkkc

```
[pnsft-pur]
Server = https://osdn.net/projects/ponsfoot-aur/storage/pur/x86_64/

```

### stx4

*   **维护者:** StarterX4 <starterx4[at]gmail.com>
*   **描述:** Any – some fonts and fakepkgs; x86_64 – archived yet might useful packages (like PacmanXG4) and some AUR soft (like OpenBoard).
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

*   **维护者:** Pyrerune <pyrerune@gmail.com>
*   **描述:** Repository containing software I develop.

```
[titanium]
Server = https://pyrerune.github.io/titanium/$arch

```

### userrepository

*   **维护者:** [Bruno Miguel](https://twitter.com/brunomiguel) <brunoalexandremiguel@gmail.com>
*   **描述:** Repository containing software from AUR

```
[userrepository]
Server = https://userrepository.eu

```