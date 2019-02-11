**翻译状态：** 本文是英文页面 [Arch_Linux](/index.php/Arch_Linux "Arch Linux") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-10，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Linux&diff=0&oldid=507441)可以查看翻译后英文页面的改动。

Arch Linux 是通用 x86-64 GNU/Linux 发行版。Arch采用滚动升级模式，尽全力提供最新的稳定版软件。初始安装的Arch只是一个基本系统，随后用户可以根据自己的喜好安装需要的软件并配置成符合自己理想的系统.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 原则](#原则)
    *   [1.1 简洁](#简洁)
    *   [1.2 现代](#现代)
    *   [1.3 实用](#实用)
    *   [1.4 以用户为中心](#以用户为中心)
*   [2 通用](#通用)
*   [3 历史](#历史)
    *   [3.1 早期](#早期)
    *   [3.2 中期](#中期)
    *   [3.3 ArchWiki 的诞生](#ArchWiki_的诞生)
    *   [3.4 A. Griffin 时代](#A._Griffin_时代)
    *   [3.5 Arch 安装脚本](#Arch_安装脚本)
    *   [3.6 Systemd 时代](#Systemd_时代)
    *   [3.7 抛弃 i686 支持](#抛弃_i686_支持)

## 原则

以下核心原则构成了我们通常所指的 Arch 之道，或者说 Arch 的哲学，或许最好的结词是 Keep It Simple, Stupid（对应中文为“保持简单，且一目了然”）。

### 简洁

Arch Linux 将简洁定义为：**避免任何不必要的添加、修改和复杂增加**。它提供的软件都来自原始开发者([上游](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)"))，仅进行和发行版(下游)相关的最小修改。

*   不包含上游不愿意接受的补丁。绝大部分 Arch 下游补丁都已经被上游接受，下一个正式版本里会包含。
*   配置文件也是来自上游，仅包含发行版必须的调整，比如特殊的文件系统路径变动。Arch 不会在安装一个软件包后就自动启动服务。
*   软件包通常都和一个上游项目直接对应。仅在极少数情况下才会拆分软件包。
*   官方不支持图形化配置界面，建议用户使用命令行或文本编辑器修改设置。

### 现代

Arch尽全力保持软件处于最新的稳定版本，只要不出现系统软件包破损，都尽量用最新版本。Arch采用[滚动升级](https://en.wikipedia.org/wiki/Rolling_release "wikipedia:Rolling release")策略，安装之后可以持续升级。

Arch向GNU/Linux用户提供了许多新特性，包括[systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")初始化系统、现代的[文件系统](/index.php/File_systems "File systems")、LVM2/EVMS、软件磁盘阵列（软RAID）、udev支持、initcpio（附带mkinitcpio）以及最新的内核。

### 实用

Arch 注重实用性，避免意识形态之争。最终的设计决策都是由开发者的共识决定。开发者依赖基于事实的技术分析和讨论，避免政治因素，不会被流行观点左右。

Arch Linux 的仓库中包含大量的软件包和编译脚本。用户可以按照需要进行自由选择。仓库中既提供了开源、自由的软件，也提供了闭源软件。**实用性大于意识形态**.

### 以用户为中心

许多 Linux 发行版都试图变得更“用户友好”，Arch Linux 则一直是，永远会是“以用户为中心”。此发行版是为了满足贡献者的需求，而不是为了吸引尽可能多的用户。Arch 适用于乐于自己动手的用户，他们愿意花时间阅读文档，解决自己的问题。

Arch 鼓励每一个用户 [参与](/index.php/Getting_involved "Getting involved") 和贡献，报告和帮助修复 [bugs](https://bugs.archlinux.org/)，提供软件包补丁和参加核心 [项目](https://projects.archlinux.org/)：Arch 开发者都是志愿者，通过持续的贡献成为团队的一员。*Archers* 可以自行贡献软件包到 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), 提升 [ArchWiki 文档质量](/index.php/Main_page "Main page"), 在 [论坛](https://bbs.archlinux.org/), [邮件列表](https://mailman.archlinux.org/mailman/listinfo/), [IRC](/index.php/IRC_channels "IRC channels") 中给其它用户提供技术支持. Arch Linux 是全球很多用户的选择，已经有很多 [国际社区](/index.php/International_communities "International communities")提供帮助和文档翻译。

## 通用

Arch Linux 是通用发行版，初始安装仅提供命令行环境：用户不需要删除大量不需要的软件包，而是可以从[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")成千上万的高质量软件包中进行选择，搭建自己的系统。支持[x86-64](https://en.wikipedia.org/wiki/x86-64 "wikipedia:x86-64") 架构。( [对 i686 架构的支持已经结束](https://www.archlinux.org/news/the-end-of-i686-support/) ）

Arch有一个易用的[包管理系统](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager")[Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")，仅凭一条命令就升级整个系统。Arch还提供一个类似ports的包构建系统（[Arch Build System](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")），通过它可以轻松从源码构建和安装软件包，并用一个命令完成同步。你甚至可以用一个命令重新构建整个系统。Arch还提供[Arch User Repository](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")，它包含了数千个由用户维护的[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")脚本，配合[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")工具，从编译到打包一气呵成。用户还能轻松构建和维护属于自己的自定义软件源。

## 历史

这些年来，Arch 社区不断成长，最近也收到大量的 [关注和评论](/index.php/Arch_Linux_Press_Review "Arch Linux Press Review")。

Arch 开发者都是不收工资的志愿者，目前也没有通过 Arch Linux 赚钱的计划。Arch 开发的详细历史可以浏览 [Wayback Machine 的 Arch 部分](http://web.archive.org/web/*/archlinux.org) 和 [Arch Linux 新闻存档](https://www.archlinux.org/news/)。

### 早期

加拿大程序员和吉他师 Judd Vinet 从 2001 年早期开始开发 Arch Linux，并在2002年3月11日正式发行0.1版。它受到[Slackware](http://www.slackware.com/), [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"), [PLD Linux](http://www.pld-linux.org/) 和 [CRUX](http://crux.nu/) 的启发，但是那时候这些发行版缺少软件包管理工具。所以 Vinet 以同样的简洁原则建立发行版，并编写了 [pacman](/index.php/Pacman "Pacman") 软件包，自动处理软件包的安装、删除和更新。

### 中期

[这个](/images/8/8d/Archstats2002-2011.png "Archstats2002-2011.png")图表见证了Arch Linux 社区的稳步扩大. 而且从早期开始，Arch 就树立起了 [开放、友好和社区互助的形象](http://www.osnews.com/story/4827)。

### ArchWiki 的诞生

2005年7月8日，用 MediaWiki 搭建的 ArchWiki [开始运行](/index.php/ArchWiki:About#Early_history "ArchWiki:About")。

### A. Griffin 时代

2007下半年，Judd Vinet 退出了Arch的开发，并[把统治权交给美国程序员 Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), 也就是 Phrakture，目前他依然是 Arch 开发者。

### Arch 安装脚本

2012 年 7 月的 Arch Linux 安装介质中 [弃用了](https://www.archlinux.org/news/install-media-20120715-released/) 基于菜单的 Arch 安装框架。并编写了几个便于安装过程中使用的脚本。

### Systemd 时代

2012 到 2013 年间 Arch 用 Systemd 替换了 System V init ：[[1]](https://www.archlinux.org/news/install-medium-20121006-introduces-systemd/)[[2]](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/)[[3]](https://www.archlinux.org/news/end-of-initscripts-support/)[[4]](https://www.archlinux.org/news/final-sysvinit-deprecation-warning/)

### 抛弃 i686 支持

鉴于在开发者和社区中 i686 架构的使用程度逐渐式微，[i686支持已经于2017年11月底被抛弃](https://www.archlinux.org/news/the-end-of-i686-support/) 。