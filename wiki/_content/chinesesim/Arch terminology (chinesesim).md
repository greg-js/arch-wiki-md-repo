**翻译状态：** 本文是英文页面 [Arch_terminology](/index.php/Arch_terminology "Arch terminology") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-19，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_terminology&diff=0&oldid=492867)可以查看翻译后英文页面的改动。

本页面试图揭开 Arch Linux 社区术语的神秘面纱。您可以自由的添加或更改任何术语，但是请使用某个章节的编辑选项。如果想添加新术语请按照字母顺序。

## Contents

*   [1 ABS](#ABS)
*   [2 Arch Linux](#Arch_Linux)
*   [3 Arch 之道](#Arch_之道)
*   [4 Arch Linux Archive](#Arch_Linux_Archive)
*   [5 AUR](#AUR)
*   [6 TU, 可信用户](#TU,_可信用户)
*   [7 bbs](#bbs)
*   [8 community/[community]](#community/[community])
*   [9 core/[core]](#core/[core])
*   [10 custom/user repository](#custom/user_repository)
*   [11 Developer](#Developer)
*   [12 extra/[extra]](#extra/[extra])
*   [13 initramfs](#initramfs)
*   [14 initrd](#initrd)
*   [15 KISS](#KISS)
*   [16 makepkg](#makepkg)
*   [17 namcap](#namcap)
*   [18 package](#package)
*   [19 软件包维护者](#软件包维护者)
*   [20 pacman](#pacman)
*   [21 pacman.conf](#pacman.conf)
*   [22 PKGBUILD](#PKGBUILD)
*   [23 仓库/repo](#仓库/repo)
*   [24 RTFM](#RTFM)
*   [25 testing/[testing]](#testing/[testing])
*   [26 udev](#udev)
*   [27 wiki](#wiki)

## ABS

[Arch 编译系统](/index.php/Arch_Build_System "Arch Build System") (ABS) 可以:

*   为没有打包的软件制作软件包
*   定制/修改已有的软件包，满足您的需求（启用或禁用选项)
*   用自定义的编译选项编译整个系统，"类似 Gentoo"
*   让内核模块在自定义内核上工作

ABS 不是必须的，但是很有用。

## Arch Linux

应该用下面术语指代 Arch：

*   **Arch Linux**
*   **Arch** (Linux implied)
*   **archlinux** (UNIX name)

Archlinux、ArchLinux、archLinux、aRcHlInUx 等等称呼都不是标准的。

'Arch' 在 "Arch Linux" 中的官方读音是 /ˈɑrtʃ/ ，就像单词 "archer"，或者 "arch-nemesis" 中的读音，但不是在单词 "ark" 或者 "archangel" 中的读音。

## Arch 之道

一个[Arch Linux 原则](/index.php/Arch_Linux#Principles "Arch Linux") 的非正式传统说法。

## Arch Linux Archive

[Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") (a.k.a ALA), 之前被称为　Arch Linux Rollback Machine (a.k.a ARM), 保存历史上的官方软件仓库快照，ISO　镜像和　boot straps　压缩包。

## AUR

[Arch用户软件仓库](https://aur.archlinux.org)（Arch User Repository，AUR）是为用户而建、由用户主导的Arch软件仓库。AUR中的软件包以软件包生成脚本（[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")）的形式提供，用户自己通过[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")生成包，再由[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装。创建AUR的初衷是方便用户维护和分享新软件包，并由官方定期从中挑选软件包进入[community](/index.php/Community_repository "Community repository")仓库。本文介绍用户访问和使用AUR的方法。

许多官方仓库软件包都来自AUR。通过AUR，大家相互分享新的软件包生成脚本（[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")和其他相关文件）。用户还可以为软件包投票。如果一个软件包投票足够多、没有协议问题、打包质量好，那么它就很有希望被收录进官方[community]仓库（以后就可以直接通过[pacman](/index.php/Pacman "Pacman") 或 [abs](/index.php/ABS "ABS") 安装了）。

通过[这个](https://aur.archlinux.org)页面可以访问 AUR。

## TU, 可信用户

[trusted user](/index.php/Trusted_user "Trusted user")(可信用户)是 AUR 和 [community] 仓库的维护人员。可信用户可以在需要的时候将软件包从 AUR 移动到 [community] 仓库。老的可信用户可以通过投票指定新的 TU.

可信用户遵循 [AUR 可信用户准测](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") 和 [TU 法](https://aur.archlinux.org/trusted-user/TUbylaws.html)。

## bbs

**B**ulletin **b**oard **s**ystem, 在 Arch 中指 [用户论坛](https://bbs.archlinux.org)。

## community/[community]

[community] 仓库存储 [可信用户](/index.php/Trusted_Users "Trusted Users") 预先编译的软件包。[community] 中的大部分软件包都来自 [AUR](/index.php/AUR "AUR").

## core/[core]

[core] 仓库包含 Arch linux 需要的基本软件包，一个可用命令行需要的所有软件包都在 [core] 中。

## custom/user repository

任何人都可以创建供其它人使用的仓库，需要一批软件包，针对这些软件包编写 [pacman](/index.php/Pacman "Pacman") 可读的数据库文件。然后把这些软件放到网上，其他人就可以把你的仓库加到 pacman 配置文件并使用了。参考 [Custom local repository](/index.php/Custom_local_repository "Custom local repository").

## Developer

无偿为 Arch 提供帮助的人，半个上帝，[开发者](https://www.archlinux.org/people/developers/) 等级仅在我们的上帝 Judd Vinet 和 Aaron Griffin 之下。

## extra/[extra]

Arch 的官方软件包很精简，但是我们提供了丰富，更完整的 "附加" 软件仓库，包含大量不会进入到 core 的软件包。此仓库在强大社区的支持下，越来越大。桌面软件环境，窗口管理器和常用程序都位于此仓库。

## initramfs

请阅读 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

## initrd

已经过时，有时会作为 initramfs 的别名使用。

## KISS

Keep It Simple, Stupid 的简写. [简单](/index.php/Arch_Linux#Simplicity "Arch Linux") 是 Arch Linux 坚持的原则。

## makepkg

[makepkg](/index.php/Makepkg "Makepkg") 会读取 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 文件，然后按脚本编译软件包。所需的是 Linux 平台编译环境， [wget](https://www.archlinux.org/packages/?name=wget) 和一些编译脚本。脚本编译的优点是只需要做一次工作。一旦有了编译脚本，只需要执行 makepkg，它会执行剩余的工作: 下载并验证源代码，检查依赖关系，配置编译时间，编译软件包，安装软件包到临时目录，进行定制，生成元数据，然后打包供 [pacman](/index.php/Pacman "Pacman") 使用。

## namcap

[namcap](/index.php/Namcap "Namcap") 是软件包分析工具，可以检查 Arch Linux 软件包和 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 文件. 可以用规则检查文件列表、文件本身或单独的 PKGBUILD 文件。工具的输出和错误标记请参考 [Namcap](/index.php/Namcap "Namcap")。

## package

软件包是一个包含如下内容的压缩包:

*   应用程序所有(编译后)的文件
*   软件的元数据，包含程序名称、版本、依赖关系 ...
*   [pacman](/index.php/Pacman "Pacman") 需要的安装文件
*   (可选) 方便使用的文件，例如启动/禁用脚本

Arch 软件包管理器 [pacman](/index.php/Pacman "Pacman") 可以安装、更新和删除这些软件包。使用软件包而不是自行编译软件包有如下好处：

*   更新方便: pacman 会在有软件包更新时进行安装
*   依赖检查: pacman 会帮你处理依赖关系，所以你只需要给出需要安装的软件包，pacman 会安装所有需要的其它软件包
*   完全清理: pacman 有一个软件包的完整文件列表，删除软件时不会有残留.

**注意:** 不同的 GNU/Linux 发行版使用不同的软件包和软件包管理程序，所以不能使用 pacman 在 Arch 上安装 Debian 软件。

## 软件包维护者

软件包维护者的任务是在软件更新后更新软件包并提交软件包的Bug。包含：

*   Arch Linux 核心开发人员，负责官方软件仓库(core, extra 和 testing)的维护.
*   [可信用户](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") 是维护非官方软件的维护者.
*   一般用户可以在 [AUR](/index.php/AUR "AUR") 中维护 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 和本地源代码文件。

软件包维护者是软件的当前负责人，之前的维护者和贡献者应该在 PKGBUILD 中注明。

## pacman

[pacman](https://archlinux.org/pacman/)[软件包管理器](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system")是 Arch Linux 的一大亮点。它将一个简单的二进制包格式和易用的构建系统结合了起来(参见[makepkg](/index.php/Makepkg "Makepkg")和[ABS](/index.php/ABS "ABS"))。不管软件包是来自官方的 Arch 库还是用户自己创建，*pacman* 都能方便得管理。

*pacman* 通过和主服务器同步软件包列表来进行系统更新，这使得注重安全的系统管理员的维护工作成为轻而易举的事情。这种服务器/客户端模式可以使用一条命令就下载/安装软件包，同时安装必需的依赖包。

## pacman.conf

[pacman](/index.php/Pacman "Pacman") 的配置文件，位于 `/etc`. 完整介绍请参考[pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5).

## PKGBUILD

[PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 是编译 Arch Linux 软件包使用的脚本。详情参考 [Creating packages (简体中文)](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)").

## 仓库/repo

软件仓库是包含一个或多个从 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 编译出来的软件包. [官方软件仓库](/index.php/Official_repositories "Official repositories")分成多个部分以方便管理。Pacman 使用这些仓库查找和安装软件包。一个仓库可以是本地的，也可以是远程的(先下载软件包再安装).

## [RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM")

"Read The Fucking (or Fine) Manual". 很多新 Linux/Arch 用户在询问一个在程序手册里面明确定义的问题时，都会收到这个简单的短语。

这个回复通常意味着用户在发问前没有做足自己的功课。如果有人这么回复你，并不是要侮辱你，仅仅是对你的不努力有些失望。收到这个信息后，最正确的动作是阅读手册页面。

*   要阅读某个特定程序的手册`man 程序名称`,

如果没有找到需要的信息，还可以查看下面内容：

*   搜索 [wiki](/index.php/Special:Search "Special:Search")
*   搜索 [论坛](https://bbs.archlinux.org)
*   搜索 [邮件列表](https://www.google.com/#hl=en&q=arch+site:archlinux.org%2Fpipermail%2F)
*   搜索 [web](https://www.google.com)

## testing/[testing]

主要的软件包在正式发布前，会放在此仓库进行测试，查看是否有 bug 和安装问题。默认是不启用，可以在 `/etc/pacman.conf` 中启用。

## udev

[udev](/index.php/Udev "Udev") 提供了一个动态的设备目录，仅包含实际存在的设备。它会在 `/dev` 目录创建或删除设备，或者重命名网络接口。

通常 udev 作为 udevd(8) 运行并在设备添加/移除时收到内核的 uevent 通知。

如果 udev 收到了设备事件，会根据配置规则和 sysfs 中的信息进行匹配，确认设备。匹配规则可以提供额外的设备信息或指定设备节点名称和软链接，并要求 udev 在事件处理时运行额外的程序。

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[这里!](/index.php/Main_page "Main page") 一个寻找 Arch Linux 文档的地方，任何人都可以修改这些文档。