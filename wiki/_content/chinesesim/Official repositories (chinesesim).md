相关文章

*   [Mirrors (简体中文)](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)")
*   [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")
*   [Unofficial user repositories (简体中文)](/index.php/Unofficial_user_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unofficial user repositories (简体中文)")

**翻译状态：** 本文是英文页面 [Official_Repositories](/index.php/Official_Repositories "Official Repositories") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-12-21，点击[这里](https://wiki.archlinux.org/index.php?title=Official_Repositories&diff=0&oldid=286771)可以查看翻译后英文页面的改动。

[软件仓库](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository")（在Debian系发行版中，又叫做“软件源”）是软件包存储的地方。通常我们所说的软件仓库指**在线软件仓库**，亦即用户从互联网获取软件的地方。Arch Linux [软件包维护员](/index.php/Package_Maintainer "Package Maintainer")（包括开发人员以及[受信用户](/index.php/Trusted_Users "Trusted Users")）对基本的、常用的或者流行的软件包进行维护，用户则可以通过[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包管理器安装使用这些软件。本文将带你了解我们的官方软件仓库。

## Contents

*   [1 历史背景](#历史背景)
*   [2 core](#core)
*   [3 extra](#extra)
*   [4 community](#community)
*   [5 multilib](#multilib)
*   [6 testing](#testing)
*   [7 community-testing](#community-testing)
*   [8 multilib-testing](#multilib-testing)

## 历史背景

大部分仓库是因为历史原因分开的。原本，当这个发行版只有一小部分用户时，是只有一个软件仓库的，它就是现在的 **core** ──那时候它叫做 **official** 。这个仓库主要存放了Judd Vinet选定的应用程序，当然现在已经不是这样了：它被设计为只包含“每种类型”程序中的一个 ── 一个桌面环境、一个主浏览器等等。

后来有用户不满Judd的选择，由于[ABS系统](/index.php/Arch_Build_System "Arch Build System")使用简单，所以他们就用ABS来创建自己的软件包。这些软件包被放入一个名为**unofficial**的软件仓库，而这个仓库由除Judd以外的开发人员维护。最终，新仓库获得开发人员同样的支持，所以就不再使用 official 和 unofficial 这两个名称了。大约在0.5版本的时候，两个仓库更名为 **current** 和 **extra** 。

在2007.8.1版本发布之后， current 更名为 core ，以免让人误解它包含的内容。如今，这两个仓库在开发人员和社区眼中都是相同分量的。不过 core 还是有些不同的，主要区别在于安装光盘和发布的快照中的软件包都只在 core 当中。这个仓库可以实现一个完整的Linux系统，但并不一定是你想要的Linux系统。

在0.5或者0.6版本的时候，仓库里有大量的软件包没有开发者愿意去维护。于是一位开发人员（Xentac）建立了“受信用户仓库”（Trusted User Repositories），作为存放被信任的用户（TU）自行创建的软件包的仓库。**staging**仓库里的软件包可以被Arch Linux的开发人员选拔入官方仓库，不过除此之外，开发人员和受信用户或多或少还是有所不同的。

就这样过了一段时间，逐渐的受信用户对他们的软件仓库感到厌倦，而非受信用户又期望可以将自己的软件包与大家分享。这导致了[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")的出现。慢慢的TU们形成更为严密的组织，如今他们共同维护**community**软件仓库。TU是一个独立于Arch Linux开发人员之外的组织，两者并没太多交流。不过，热门的软件包仍然会偶尔从 community 选拔入 **extra** 。[AUR](https://aur.archlinux.org/)也允许非受信用户提交PKGBUILD给其他用户自愿使用。

在2006年，**core**仓库里未被正确编译的内核[导致许多用户系统崩溃](https://www.archlinux.org/news/please-avoid-kernel-261614-1/)。之后，“core仓库审核机制”引入：所有[core]仓库软件包更新前，必须先在一个叫做 **testing** 的仓库进行测试，必须在其他开发者同意后，软件包才能正式移入 core 。后来， core 中出现一些低使用率的软件，审核机制对它们有所宽松。

2009年末至2010年初，出现了一些新的文件系统，人们希望在安装系统时就使用它们（即纳入 core ）。鉴于 core 从来没有给出明确的界定，人们决定给它一个更为明确的定义（见下）。

## core

core 仓库位于Arch镜像的 `.../core/os/` 目录中。

该仓库对包质量有严格要求：

*   软件包更新需要经过开发者和用户的审察批准。
*   对于低使用率的软件，公布合理的更新缘由（例如：发布通知、请求审核、在 testing 仓库审核几天到几周不等），后经开发者简单的审核即可。

该仓库包含下列软件包：

*   启动Arch系统所必需的。
*   链接互联网时可能需要的。
*   编译软件包时需要的。
*   检查、修复文件系统的工具。
*   在安装过程中可能用到的（例如[openssh](https://www.archlinux.org/packages/?name=openssh)）。
*   上述软件包的运行时依赖。

以前的核心系统安装盘中包含了这些软件包，可以离线安装基本系统，现在安装盘都是网络安装。[这里](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips")有从[core]或其他仓库创建本地软件仓库的方法。}}

## extra

extra 仓库位于Arch镜像的 `.../extra/os/` 目录中。它包含不适合[core]库标准的大量软件包，比如：Xorg，窗口管理器，网页浏览器，媒体播放器，脚本语言支持等等。

## community

community 仓库位于Arch镜像的 `.../community/os/` 目录中。

包含由[TU](/index.php/Trusted_User "Trusted User")认证的、获得足够多打分的[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")软件包。该仓库中的某些软件包还可能收录进[core]或[extra]仓库。

## multilib

[multilib](/index.php/Multilib "Multilib") 仓库位于Arch镜像的 `.../multilib/os/` 目录中。

包含64位系统中需要的32位软件和库，例如： [wine](https://www.archlinux.org/packages/?name=wine), [skype](https://aur.archlinux.org/packages/skype/) 等。

## testing

**警告:** 谨慎启用 testing 仓库，其中的软件包可能损坏系统。仅当你有足够的经验应对问题时，再考虑启用。

testing 仓库位于Arch镜像的 `../testing/os/` 目录中。

testing 仓库很特别，它包含即将进入 core 、 extra 软件库的候选软件包。

下列软件包会进入 testing 库：

*   更新该软件包可能损坏系统，需要进行测试。
*   更新该软件包，可能需要其他相关软件包重建，软件包在[testing]库中等候全部相关软件包准备到位。

testing 库是唯一可能和其它官方软件仓库有软件包名称冲突的仓库。如果要启用，应该在 `pacman.conf` 文件里把它设置为第一个仓库。

testing 库并不是“最新”软件包的仓库。它的目的是存放一些由于是[core]软件集合的一部分或者由于其它方面的问题，可能引起**系统崩溃**的软件包更新。我们**强烈建议**使用 testing 库的用户订阅[arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public)邮件列表，监视[testing 仓库论坛](https://bbs.archlinux.org/viewforum.php?id=49)，并在Bug Tracker报告bug。

如果你启用 testing 仓库，你一定要同时启用 community-testing 仓库。

## community-testing

community-testing 库的功能类似 testing ，不过是为 community 库设计的测试仓库。

如果你启用 community-testing 仓库，你一定要同时启用 testing 仓库。

## multilib-testing

multilib-testing 和 testing 类似，只是其中的软件包将进入 multilib。

要启用 multilib-testing ，需要同时启用 testing。