**翻译状态：** 本文是英文页面 [Arch_Linux](/index.php/Arch_Linux "Arch Linux") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-12，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Linux&diff=0&oldid=390802)可以查看翻译后英文页面的改动。

Arch Linux是一种独立开发的通用 [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)")/[x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") GNU/Linux发行版，灵活度高可用于各种场合。其开发注重设计简便、简洁和优雅编程。初始安装的Arch只是一个基本系统，随后用户可以根据自己的喜好安装需要的软件并配置成符合自己理想的系统。官方并未提供图形界面配置工具，大多数系统配置需要通过命令行。Arch采用滚动升级模式，尽全力提供最新的稳定版软件。

## Contents

*   [1 原则](#.E5.8E.9F.E5.88.99)
    *   [1.1 简洁](#.E7.AE.80.E6.B4.81)
    *   [1.2 现代](#.E7.8E.B0.E4.BB.A3)
    *   [1.3 实用](#.E5.AE.9E.E7.94.A8)
    *   [1.4 以用户为中心](#.E4.BB.A5.E7.94.A8.E6.88.B7.E4.B8.BA.E4.B8.AD.E5.BF.83)
*   [2 软件包管理](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.AE.A1.E7.90.86)
*   [3 社区](#.E7.A4.BE.E5.8C.BA)
*   [4 历史](#.E5.8E.86.E5.8F.B2)
    *   [4.1 早期](#.E6.97.A9.E6.9C.9F)
    *   [4.2 中期](#.E4.B8.AD.E6.9C.9F)
    *   [4.3 A. Griffin 时代](#A._Griffin_.E6.97.B6.E4.BB.A3)

## 原则

以下核心原则构成了我们通常所指的 Arch 之道，或者说 Arch 的哲学，或许最好的结词是 Keep It Simple, Stupid（对应中文为“保持简单，且一目了然”）。

### 简洁

*精于心简于形* -列昂纳多.达.芬奇

Arch Linux 将简洁定义为：**避免任何不必要的添加、修改和复杂增加**。它提供的软件都来自原始开发者([上游](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)"))，仅进行和发行版(下游)相关的最小修改。

*   不包含上游不愿意接受的补丁。绝大部分 Arch 下游补丁都已经被上游接受，下一个正式版本里会包含。
*   配置文件也是来自上游，仅包含发行版必须的调整，比如特殊的文件系统路径变动。Arch 不会在安装一个软件包后就自动启动服务。
*   软件包通常都和一个上游项目直接对应。仅在极少数情况下才会拆分软件包。

### 现代

Arch尽全力保持软件处于最新的稳定版本，只要不出现系统软件包破损，都尽量用最新版本。Arch采用[滚动升级](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release")策略，安装之后可以持续升级，无需重装。只敲一个命令，Arch就可以保持最新。

Arch向GNU/Linux用户提供了许多新特性，包括[systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")初始化系统、现代的文件系统（Ext2/3/4、Reiser、XFS、JFS、BTRFS）、LVM2/EVMS、软件磁盘阵列（软RAID）、udev支持、initcpio（附带mkinitcpio）以及最新的内核。

### 实用

*正确性明显是首要标准。如果一个系统无法按照要求运行，那么其他都是空谈。* — Bertrand Meyer

Arch is 注重实用性，避免意识形态之争。最终的设计决策都是由开发者的共识决定。开发者依赖基于事实的技术分析和讨论，避免政治因素，不会被流行观点左右。

Arch Linux 的仓库中包含大量的软件包和编译脚本。用户可以按照需要进行自由选择。仓库中既提供了开源、自由的软件，也提供了闭源软件。**实用性大于意识形态**.

### 以用户为中心

许多 Linux 发行版都试图变得更“用户友好”，Arch Linux 则一直是，永远会是“以用户为中心”。此发行版是为了满足贡献者的需求，而不是为了吸引尽可能多的用户。Arch 适用于乐于自己动手的用户，他们愿意花时间阅读文档，解决自己的问题。

Arch 鼓励每一个用户报告问题、完善 Wiki 社区文档、为其它用户提供技术支持。[Arch 用户仓库](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 收集用户贡献的软件包。Arch 开发者都是志愿者，活跃的贡献者很快就能称为开发人员。

正如 Arch Linux 项目的创立者 Judd Vinet 所说：“它（Arch）完全由你自己塑造而成。”

## 软件包管理

Arch有一个易用的二进制[包管理系统](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager")----[Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")），它可以让你仅凭一条命令就升级整个系统。Pacman用C语言编写，具有轻量、简便和快速的特点。Arch还提供一个类似ports的包构建系统（[Arch Build System](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")），通过它可以轻松从源码构建和安装软件包，并用一个命令完成同步。你甚至可以用一个命令重新构建整个系统。

Arch的官方源提供了数千种高质量的i686/x86-64二进制包来满足你的软件需求。另外，为鼓励社区开发和贡献代码，Arch还提供[Arch User Repository](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")，它包含了数千个由用户维护的[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")脚本，配合[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")工具，从编译到打包一气呵成。用户还能轻松构建和维护属于自己的自定义软件源。

## 社区

Arch社区是值得信赖、充满活力并且好客的：我们鼓励所有的*Archers*都来积极参与，为发行版作出贡献，帮助核心软件的开发，维护软件包，报告或修复[bug](https://bugs.archlinux.org/)，改进 [ArchWiki文档库](/index.php/Main_page "Main page")，在[论坛](https://bbs.archlinux.org/)、[邮件列表](https://mailman.archlinux.org/mailman/listinfo/)和[IRC 频道](/index.php/IRC_channels "IRC channels") 中帮助其他用户解决问题、交换观点，或是分享自己开发的应用程序。Arch Linux是众多地球人的选择，并且有一些[国际社区](/index.php/International_communities "International communities")提供不同语言的帮助以及文档库。

如果你想成为社区的活跃成员，请点击[参与](/index.php/Getting_involved_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Getting involved (简体中文)")。

## 历史

### 早期

加拿大程序员和吉他师 Judd Vinet 从 2001 年早期开始开发 Arch Linux，并在2002年3月11日正式发行0.1版。它受到[Slackware](http://www.slackware.com/), [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"), [PLD Linux](http://www.pld-linux.org/) 和 [CRUX](http://crux.nu/) 的启发，但是那时候这些发行版缺少软件包管理工具。所以 Vinet 以同样的简洁原则建立发行版，并编写了 [pacman](/index.php/Pacman "Pacman") 软件包，自动处理软件包的安装、删除和更新。

### 中期

[这个](https://dev.archlinux.org/~dan/archstats.svg) 表格见证了Arch Linux 社区的稳步扩大. 而且从早期开始，Arch 就树立起了 [开放、友好和社区互助的形象](http://www.osnews.com/story/4827)。

### A. Griffin 时代

2007下半年，Judd Vinet 退出了Arch的开发，并[把统治权交给美国程序员 Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), 也就是 Phrakture，目前他依然是 Arch 开发者。

这些年来，Arch 社区不断成长，最近也收到大量的 [关注和评论](/index.php/Arch_Linux_Press_Review "Arch Linux Press Review")。

Arch 开发者都是不收工资的志愿者，目前也没有通过 Arch Linux 赚钱的计划。Arch 开发的详细历史可以浏览 [Wayback Machine 的 Arch 部分](http://web.archive.org/web/*/archlinux.org) 和 [Arch Linux 新闻存档](https://www.archlinux.org/news/)。