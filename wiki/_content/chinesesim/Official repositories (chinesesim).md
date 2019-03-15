相关文章

*   [Mirrors (简体中文)](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)")
*   [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")
*   [Unofficial user repositories (简体中文)](/index.php/Unofficial_user_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unofficial user repositories (简体中文)")

**翻译状态：** 本文是英文页面 [Official repositories](/index.php/Official_repositories "Official repositories") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-15，点击[这里](https://wiki.archlinux.org/index.php?title=Official+repositories&diff=0&oldid=568183)可以查看翻译后英文页面的改动。

[软件仓库](https://en.wikipedia.org/wiki/software_repository "wikipedia:software repository")是获取软件包的地方。

Arch Linux [软件包维护员](/index.php/Package_Maintainer "Package Maintainer") 维护了基本和流行的软件包，用户则可以通过[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包管理器安装使用这些软件。

官方软件仓库中的软件包会持续更新，老版本被移除。Arch 没有主版本的概念：每个软件在上游有新版本时单独更新。在某个时间点上，软件仓库中的所有软件都是相互兼容的。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 稳定仓库](#稳定仓库)
    *   [1.1 core](#core)
*   [2 extra](#extra)
*   [3 community](#community)
*   [4 multilib](#multilib)
*   [5 启用](#启用)
*   [6 禁用](#禁用)
*   [7 testing 仓库](#testing_仓库)
    *   [7.1 testing](#testing)
    *   [7.2 community-testing](#community-testing)
    *   [7.3 multilib-testing](#multilib-testing)
    *   [7.4 gnome-unstable](#gnome-unstable)
    *   [7.5 kde-unstable](#kde-unstable)
    *   [7.6 禁用测试仓库](#禁用测试仓库)
*   [8 Staging repositories](#Staging_repositories)
*   [9 历史背景](#历史背景)

## 稳定仓库

### core

core 仓库位于 [仓库镜像](/index.php/Mirror "Mirror") 的 `.../core/os/` 目录。

该仓库软件实现下面基本功能:

*   启动 Arch 系统。
*   [连接网络](/index.php/Network_configuration "Network configuration")
*   [building packages编译软件包](/index.php/Creating_packages "Creating packages")
*   检查、修复[文件系统](/index.php/File_systems "File systems")
*   系统安装（例如[openssh](https://www.archlinux.org/packages/?name=openssh)）。

已经上述软件包的依赖。

该仓库对包质量有严格要求。软件包更新需要经过开发者和用户的审察批准。对于低使用率的软件，公布合理的更新缘由（例如：发布通知、请求审核、在 testing 仓库审核几天到几周不等），后经开发者简单的审核即可。

以前的核心系统安装盘中包含了这些软件包，可以离线安装基本系统，现在安装盘都是网络安装。[这里](/index.php/Pacman_tips#Installing_packages_from_a_CD.2FDVD_or_USB_stick "Pacman tips")有从[core]或其他仓库创建本地软件仓库的方法。}}

## extra

extra 仓库位于[仓库镜像](/index.php/Mirror "Mirror")的 `.../extra/os/` 目录。

它包含不适合[core]库标准的大量软件包，比如：Xorg，窗口管理器，网页浏览器，媒体播放器，脚本语言支持等等。

## community

community 仓库位[仓库镜像](/index.php/Mirror "Mirror")的 `.../community/os/` 目录。

包含由[TU](/index.php/Trusted_User "Trusted User")接管、获得足够多打分的[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")软件包。该仓库中的某些软件包还可能收录进[core]或[extra]仓库。

## multilib

[multilib](/index.php/Multilib "Multilib") 仓库位于[仓库镜像](/index.php/Mirror "Mirror")的 `.../multilib/os/` 目录。

包含64位系统中需要的32位软件和库，例如： [wine](https://www.archlinux.org/packages/?name=wine) 等。

## 启用

想使用 multilib 仓库，编辑 `/etc/pacman.conf`，取消下面内容的注释：

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

更新软件包列表并升级系统 `pacman -Syu`.

**Note:** 不要仅运行 `pacman -Sy`, [Arch 不支持部分升级](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance").

**Tip:** 运行 `pacman -Sl multilib` 来列出在*multilib*仓库里的所有软件包，32位库的软件包以 `lib32-` 开头

## 禁用

要恢复到纯 64 位系统，删除 *multilib*:

运行下面命令可以删除所有从 *multilib* 安装的软件:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

如果有 gcc-libs 冲突，重新安装 64-bit 版本并执行下面命令：

```
# pacman -S gcc-libs base-devel

```

在 `/etc/pacman.conf` 中注释掉 `[multilib]` 段落：

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

用 `pacman -Syu` 更新软件包列表和软件包.

## testing 仓库

**警告:**

*   谨慎启用 testing 仓库，其中的软件包可能损坏系统。仅当你有足够的经验应对问题时，再考虑启用。
*   如果你启用 testing 仓库，你一定要同时启用 community-testing 仓库。

### testing

testing 仓库位于[仓库镜像](/index.php/Mirror "Mirror")的 `../testing/os/` 目录中。

testing 仓库很特别，它包含即将进入 core 、 extra 软件库的候选软件包。

下列软件包会进入 testing 库：

*   更新该软件包可能损坏系统，需要进行测试。
*   更新该软件包，可能需要其他相关软件包重建，软件包在[testing]库中等候全部相关软件包准备到位。

testing 库是唯一可能和其它官方软件仓库有软件包名称冲突的仓库。如果要启用，应该在 `pacman.conf` 文件里把它设置为第一个仓库。

testing 库并不是“最新”软件包的仓库。它的目的是存放一些由于是[core]软件集合的一部分或者由于其它方面的问题，可能引起**系统崩溃**的软件包更新。我们**强烈建议**使用 testing 库的用户订阅[arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public)邮件列表，监视[testing 仓库论坛](https://bbs.archlinux.org/viewforum.php?id=49)，并在Bug Tracker报告bug。

### community-testing

community-testing 库的功能类似 testing ，不过是为 community 库设计的测试仓库。

### multilib-testing

multilib-testing 和 testing 类似，只是其中的软件包将进入 multilib。

### gnome-unstable

[GNOME](/index.php/GNOME "GNOME") 桌面环境的下一个稳定版本，在进入主 *testing* 仓库前，会先放到 gnome-unstable.

要启用它，在 `/etc/pacman.conf` 中加入:

```
[gnome-unstable]
Include = /etc/pacman.d/mirrorlist

```

*gnome-unstable* 项需要在所有仓库的最上面(保证在 *testing* 上面).

如果有软件包相关的问题，请在 [Arch bug tracker](https://bugs.archlinux.org/) 汇报，其它问题请 [上游的 GNOME Gitlab](https://gitlab.gnome.org)汇报。

### kde-unstable

包含 [KDE](/index.php/KDE "KDE") Plasma 和应用程序的 *beta* 或 *候选发行版本*.

要启用它，将下面内容加入 `/etc/pacman.conf`:

```
[kde-unstable]
Include = /etc/pacman.d/mirrorlist

```

*kde-unstable* 项需要在所有仓库的最上面(保证在 *testing* 上面).

请 [报告](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") 遇到的问题。

### 禁用测试仓库

如果要禁用之前启用的测试仓库，应该：

1.  从 `/etc/pacman.conf` 中删除配置
2.  执行 `pacman -Syuu` 将从这些仓库安装的软件还原到主仓库版本。这是可选操作，如果在第一步后碰到任何问题，请先执行此操作。

## Staging repositories

**Warning:** Do not enable the *staging* repositories for any reason. Your system will unquestionably break after performing an update. This repository is only meant for backend developer use.

This repository contains broken packages and is used solely by developers during rebuilds of many packages at once. In order to rebuild packages that depend on, for example, a new shared library, the shared library itself must first be built and uploaded to the staging repositories to be made available to other developers. As soon as all dependent packages are rebuilt, the group of packages is then moved to testing or to the main repositories, whichever is more appropriate.

See [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2010-August/017579.html) for more historical details.

## 历史背景

大部分仓库是因为历史原因分开的。原本，当这个发行版只有一小部分用户时，是只有一个软件仓库的，它就是现在的 **core** ──那时候它叫做 **official** 。这个仓库主要存放了Judd Vinet选定的应用程序，当然现在已经不是这样了：它被设计为只包含“每种类型”程序中的一个 ── 一个桌面环境、一个主浏览器等等。

后来有用户不满Judd的选择，由于[ABS系统](/index.php/Arch_Build_System "Arch Build System")使用简单，所以他们就用ABS来创建自己的软件包。这些软件包被放入一个名为**unofficial**的软件仓库，而这个仓库由除Judd以外的开发人员维护。最终，新仓库获得开发人员同样的支持，所以就不再使用 official 和 unofficial 这两个名称了。大约在0.5版本的时候，两个仓库更名为 **current** 和 **extra** 。

在2007.8.1版本发布之后， current 更名为 core ，以免让人误解它包含的内容。如今，这两个仓库在开发人员和社区眼中都是相同分量的。不过 core 还是有些不同的，主要区别在于安装光盘和发布的快照中的软件包都只在 core 当中。这个仓库可以实现一个完整的Linux系统，但并不一定是你想要的Linux系统。

在0.5或者0.6版本的时候，仓库里有大量的软件包没有开发者愿意去维护。于是一位开发人员（Xentac）建立了“受信用户仓库”（Trusted User Repositories），作为存放被信任的用户（TU）自行创建的软件包的仓库。**staging**仓库里的软件包可以被Arch Linux的开发人员选拔入官方仓库，不过除此之外，开发人员和受信用户或多或少还是有所不同的。

就这样过了一段时间，逐渐的受信用户对他们的软件仓库感到厌倦，而非受信用户又期望可以将自己的软件包与大家分享。这导致了[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")的出现。慢慢的TU们形成更为严密的组织，如今他们共同维护**community**软件仓库。TU是一个独立于Arch Linux开发人员之外的组织，两者并没太多交流。不过，热门的软件包仍然会偶尔从 community 选拔入 **extra** 。[AUR](https://aur.archlinux.org/)也允许非受信用户提交PKGBUILD给其他用户自愿使用。

在2006年，**core**仓库里未被正确编译的内核[导致许多用户系统崩溃](https://www.archlinux.org/news/please-avoid-kernel-261614-1/)。之后，“core仓库审核机制”引入：所有[core]仓库软件包更新前，必须先在一个叫做 **testing** 的仓库进行测试，必须在其他开发者同意后，软件包才能正式移入 core 。后来， core 中出现一些低使用率的软件，审核机制对它们有所宽松。

2009年末至2010年初，出现了一些新的文件系统，人们希望在安装系统时就使用它们（即纳入 core ）。鉴于 core 从来没有给出明确的界定，人们决定给它一个更为明确的定义（见下）。