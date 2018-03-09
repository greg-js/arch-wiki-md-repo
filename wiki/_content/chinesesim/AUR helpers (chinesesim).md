这里列出一些助手工具，可以帮助用户从 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 搜索和/或安装包。

**警告:** 这些工具都不是官方支持的。参见 [[1]](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254).

图形化 pacman 前端列表，其中的一些也支持 AUR，参见 [pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends").

## Contents

*   [1 助手列表](#.E5.8A.A9.E6.89.8B.E5.88.97.E8.A1.A8)
    *   [1.1 aurbuild](#aurbuild)
    *   [1.2 aurget](#aurget)
    *   [1.3 aurora](#aurora)
    *   [1.4 aurpac](#aurpac)
    *   [1.5 aurploader](#aurploader)
    *   [1.6 aursh](#aursh)
    *   [1.7 autoaur](#autoaur)
    *   [1.8 burp](#burp)
    *   [1.9 cower](#cower)
    *   [1.10 haskell-archlinux](#haskell-archlinux)
    *   [1.11 makeaur](#makeaur)
    *   [1.12 meat](#meat)
    *   [1.13 owl](#owl)
    *   [1.14 pacaur](#pacaur)
    *   [1.15 packer](#packer)
    *   [1.16 pacmoon](#pacmoon)
    *   [1.17 paktahn](#paktahn)
    *   [1.18 pbfetch](#pbfetch)
    *   [1.19 pbget](#pbget)
    *   [1.20 pkgman](#pkgman)
    *   [1.21 powaur](#powaur)
    *   [1.22 spinach](#spinach)
    *   [1.23 srcman](#srcman)
    *   [1.24 yaourt](#yaourt)
*   [2 比较表](#.E6.AF.94.E8.BE.83.E8.A1.A8)

## 助手列表

### aurbuild

aurbuild 是从 AUR 下载或编译软件包的工具。

*   网站: [http://aurbuild.berlios.de/](http://aurbuild.berlios.de/)
*   软件包: [https://aur.archlinux.org/packages.php?ID=1775](https://aur.archlinux.org/packages.php?ID=1775)

### aurget

Aurget的目标是要成为一个简单的,像pacman一样操作的AUR工具. 它努力使AUR使用更方便;用户无论是查找、下载、编译、安装或是更新AUR包都会更迅速. Aurget的设计是不替换pacman的任何命令

*   网站: [http://pbrisbin.com/posts/aurget/](http://pbrisbin.com/posts/aurget/)
*   包: [https://aur.archlinux.org/packages.php?ID=31933](https://aur.archlinux.org/packages.php?ID=31933)

### aurora

Aurora 是一个极简的 [AUR](/index.php/AUR "AUR") 前端. 它允许用户安装AUR包, 下载AUR包 (用于手动安装) 并且还提供了一个aur升级功能. 它不替换pacman.

*   网站: [http://bitbucket.org/bbenne10/aurora](http://bitbucket.org/bbenne10/aurora)
*   包: [https://aur.archlinux.org/packages.php?ID=41732](https://aur.archlinux.org/packages.php?ID=41732)

### aurpac

快速轻巧的 [AUR](/index.php/AUR "AUR") 和 [pacman](/index.php/Pacman "Pacman") 前端.

*   网站: [http://3ed.jogger.pl/2009/02/15/aurpac/](http://3ed.jogger.pl/2009/02/15/aurpac/)
*   Package: [https://aur.archlinux.org/packages.php?ID=23919](https://aur.archlinux.org/packages.php?ID=23919)

### aurploader

Aurploader 提示用户输入 AUR 用户名和密码，然后上传 PKGBUILD 包至 AUR. 在上传每个包之前, 用户需要选择一个分类. 当上传完成后, 用户可以选择是否需要保存cookie文件来让脚本再次运行时无需输入 AUR 用户名和密码.

*   网站: [http://xyne.archlinux.ca/info/aurploader](http://xyne.archlinux.ca/info/aurploader)
*   Package: [https://aur.archlinux.org/packages.php?ID=23393](https://aur.archlinux.org/packages.php?ID=23393)

### aursh

**注意:** 从 2010-09-30 开始，它不再被积极开发。

AurShell是一个像Shell一样的软件。通过各种插件的支持，它可以从AUR、ABS上安装软件，甚至封装pacman的功能。

*   网站: [https://github.com/husio/aursh/](https://github.com/husio/aursh/)
*   软件包: [https://aur.archlinux.org/packages.php?ID=33423](https://aur.archlinux.org/packages.php?ID=33423)

### autoaur

autoaur 是一个用于自动集中下载, 更新, 创建和安装 AUR 包的脚本.

*   网站: [autoaur](/index.php?title=Autoaur&action=edit&redlink=1 "Autoaur (page does not exist)")
*   Package: [autoaur](https://aur.archlinux.org/packages/autoaur/)

### burp

burp 是一个快速而简单的用C语言开发的 AUR 上传软件. 支持坚实的cookie无缝登陆.

*   网站: [https://github.com/falconindy/burp](https://github.com/falconindy/burp)
*   Package: [burp-git](https://aur.archlinux.org/packages/burp-git/)

### cower

Cower 是一个快速简单的 AUR 搜索和下载代理软件, 并同时会检查更新和下载依赖包.

*   网站: [https://github.com/falconindy/cower](https://github.com/falconindy/cower)
*   Forum: [https://bbs.archlinux.org/viewtopic.php?id=97137](https://bbs.archlinux.org/viewtopic.php?id=97137)
*   Package: [cower](https://aur.archlinux.org/packages/cower/)

### haskell-archlinux

haskell-archlinux 是一个采用 Haskell 程序语言，以可编程方式访问 AUR 和包元数据的库.

*   网站: [http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux)
*   Package: [https://aur.archlinux.org/packages.php?ID=29267](https://aur.archlinux.org/packages.php?ID=29267)

### makeaur

Makeaur is a wrapper for pacman and makepkg that allows users to easily install packages from the Arch User Repository.

*   网站: [http://github.com/ghost1227/makeaur/](http://github.com/ghost1227/makeaur/)
*   Package: [https://aur.archlinux.org/packages.php?ID=23678](https://aur.archlinux.org/packages.php?ID=23678)

### meat

**Note:** Meat is in actually under development/alpha state.

Meat is a front-end for cower ( see above ) and it is fully written in bash.

*   网站: [http://github.com/e36freak/meat](http://github.com/e36freak/meat)
*   Package: [https://aur.archlinux.org/packages.php?ID=50075](https://aur.archlinux.org/packages.php?ID=50075)

### owl

owl is a [pacman](/index.php/Pacman "Pacman") and [cower](/index.php/AUR_helpers#cower "AUR helpers") wrapper focused on simplicity.

*   网站: [https://github.com/baskerville/owl](https://github.com/baskerville/owl)

### pacaur

Pacaur is a fast workflow AUR wrapper, using [cower](/index.php/AUR_helpers#cower "AUR helpers") as backend. It aims on speed and simplicity, with an uncluttered interface. It is inspired by [pbfetch](/index.php/AUR_helpers#pbfetch "AUR helpers").

*   网站: [https://github.com/Spyhawk/pacaur](https://github.com/Spyhawk/pacaur)
*   论坛: [https://bbs.archlinux.org/viewtopic.php?pid=937423](https://bbs.archlinux.org/viewtopic.php?pid=937423)
*   Package: [https://aur.archlinux.org/packages.php?ID=49145](https://aur.archlinux.org/packages.php?ID=49145)

### packer

Packer is a wrapper for pacman and the AUR. It was designed to be a simple and very fast replacement for the basic functionality of Yaourt. It has commands to install, update, search, and show information for any package in the main repositories and in the AUR. Use pacman for other commands, such as removing a package.

*   网站: [http://github.com/bruenig/packer](http://github.com/bruenig/packer)
*   论坛: [https://bbs.archlinux.org/viewtopic.php?id=88115](https://bbs.archlinux.org/viewtopic.php?id=88115)
*   Package: [https://aur.archlinux.org/packages.php?ID=33378](https://aur.archlinux.org/packages.php?ID=33378)
*   Wiki: [https://github.com/bruenig/packer/wiki](https://github.com/bruenig/packer/wiki)

### pacmoon

pacmoon is a script for compiling arch linux packages from the AUR and repositories. It can automatically install make dependencies as binaries when necessary and update the entire system or just packages listed. It keeps track of which files have been compiled so that in the event of compiled packages getting replaced with a binary (like during an upgrade process) then pacmoon can recompile only the necessary packages.

*   网站: [http://chilon.net/pacmoon](http://chilon.net/pacmoon)
*   Package: [https://aur.archlinux.org/packages.php?ID=41911](https://aur.archlinux.org/packages.php?ID=41911)

### paktahn

Paktahn is a yaourt replacement. It is under active development and already includes improvements such as a local cache for fast searches and interactive installation.

*   网站: [http://github.com/skypher/paktahn](http://github.com/skypher/paktahn)
*   论坛: [https://bbs.archlinux.org/viewtopic.php?id=77674&p=1](https://bbs.archlinux.org/viewtopic.php?id=77674&p=1)
*   Package: [https://aur.archlinux.org/packages.php?ID=30242](https://aur.archlinux.org/packages.php?ID=30242)

### pbfetch

Pbfetch is a script which can be used as a pacman-independent AUR helper or a pacman wrapper with additional AUR functionality. Pbfetch aims to be a simple and fast versus the well established yaourt. Pbfetch can be used as a shortcut to simply download PKGBUILDs from AUR or automatically build with dependency resolution among other things. The user can select which AUR packages to upgrade using a simple menu as well as update all AUR packages.

*   网站/Source: [https://github.com/dalingrin/pbfetch](https://github.com/dalingrin/pbfetch)
*   论坛: [https://bbs.archlinux.org/viewtopic.php?id=87789](https://bbs.archlinux.org/viewtopic.php?id=87789)
*   Package: [https://aur.archlinux.org/packages.php?ID=33256](https://aur.archlinux.org/packages.php?ID=33256)

### pbget

Pbget is a simple command-line tool for retrieving PKGBUILDs and local source files for Arch Linux. It is able to retrieve files from the official SVN and CVS web interface, the AUR and the ABS rsync server.

*   网站: [http://xyne.archlinux.ca/info/pbget](http://xyne.archlinux.ca/info/pbget)
*   Package: [https://aur.archlinux.org/packages.php?ID=23848](https://aur.archlinux.org/packages.php?ID=23848)

### pkgman

pkgman is a script which helps to manage a local repository. It retrieves the PKGBUILD and related files for given name from ABS or AUR and lets you edit them, automatically generates checksums, backs up the source tarball, builds and adds the package to your local repository. Then you can install it as usual with pacman. It also has AUR support for submitting tarballs and leaving comments.

*   网站: [http://sourceforge.net/apps/mediawiki/pkgman/index.php](http://sourceforge.net/apps/mediawiki/pkgman/index.php)
*   论坛: [https://bbs.archlinux.org/viewtopic.php?id=49023](https://bbs.archlinux.org/viewtopic.php?id=49023)
*   Package: [https://aur.archlinux.org/packages.php?ID=17100](https://aur.archlinux.org/packages.php?ID=17100)

### powaur

powaur is a minimalistic AUR helper with a pacman-like interface.

*   网站: [https://github.com/yanhan/powaur](https://github.com/yanhan/powaur)
*   论坛: [https://bbs.archlinux.org/viewtopic.php?pid=938688](https://bbs.archlinux.org/viewtopic.php?pid=938688)
*   Package: [https://aur.archlinux.org/packages.php?ID=49296](https://aur.archlinux.org/packages.php?ID=49296)

### spinach

Spinach is a tiny Bash AUR helper with few dependencies.

*   网站: [http://floft.net/wiki/Scripts/Spinach](http://floft.net/wiki/Scripts/Spinach)
*   Package: [https://aur.archlinux.org/packages.php?ID=46993](https://aur.archlinux.org/packages.php?ID=46993)

### srcman

srcman is a pacman/makepkg wrapper written in Bash, which transparently handles pacman operations on 'source packages'. This means, for example, that packages can be specified for installation either explicitly (pacman's -U operation) or can be installed from a (source) repository (-S operation). The address of an AUR pacman database can be found in the corresponding forum thread, by the way. The primary goal of this project is to provide a complete pacman wrapper and therefore, srcman supports all current pacman operations for binary *and* source packages.

*   网站: [https://bbs.archlinux.org/viewtopic.php?id=65501](https://bbs.archlinux.org/viewtopic.php?id=65501)
*   Package: [https://aur.archlinux.org/packages.php?ID=23945](https://aur.archlinux.org/packages.php?ID=23945)

### yaourt

[Yaourt](/index.php/Yaourt "Yaourt") (Yet Another User Repository Tool 用户的另一个软件仓库管理工具)是一个社区为增加pacman对AUR的无缝访问而做的, 它允许和自动化软件包编译和安装您在AUR选择成千上万的PKGBUILDs, 和成千上万的Arch仓库里的软件. Yaourt使用和pacman完全相同的语法,可以为您节约学习新语法的时间(仅仅添加了几个新参数)。Yaourt的强大功能给简单的pacman添加了更实用的功能并使其美观，如彩色输出，交互式界面等等

*   网站: [http://archlinux.fr/yaourt-en](http://archlinux.fr/yaourt-en)
*   包: [https://aur.archlinux.org/packages.php?ID=5863](https://aur.archlinux.org/packages.php?ID=5863)

## 比较表

| 程序 | 语言 | 依赖支持 | Core/extra/community 支持 | 活跃开发 | 使用方法 |
| [Aurget](#aurget) | Bash | 是 | 否 | 是 | 如 `aurget --help` |
| [AurShell](#aursh) | Python | 否 | 否 | 否 | aursh (runs Aurshell program, wherein a number of different commands can be used) |
| [Aurora](#aurora) | Python3 | 基本(使用 makepkg) | 否 | 是 | 如 `aurora --help` |
| [Clyde](#clyde) | Lua | 是 | 是 | 否 | 与 pacman 一致 (e.g., clyde -S <pkgname>) |
| [Cower](#cower) | C | 是 | 否 | 是 | 如 `cower -h` |
| [Makeaur](#makeaur) | Bash | 否 | 否 | 已经被 fork | makeaur <pkgname> |
| [Owl](#owl) | Dash | 是 | 是 | 是 | Run `owl` without arguments |
| [Pacaur](#pacaur) | Bash, backend in C (cower) | 是 | 是 | 否 | 与 pacman 一致, and/or AUR specific arguments . See also `pacaur -h`. |
| [Packer](#packer) | Bash | 是 | 是 | 是 | 与 pacman 一致 (e.g., packer -S <pkgname>) |
| [pacmoon](#pacmoon) | Zsh | 是 | 是 | 是 | Similar to emerge from portage e.g. pacmoon -av <pkgname> |
| [Paktahn](#paktahn) | Lisp | 是 | 是 | 是 | 与 pacman 一致 (e.g., pak -S <pkgname>) |
| [pbfetch](#pbfetch) | Bash | 是 | 是 | 是 | 与 pacman 一致, and/or AUR specific arguments (additional arguments for PKGBUILD editing, etc) |
| [powaur](#powaur) | C | 否 | 有限 | 是 | 与 pacman 一致 (e.g. powaur -S <pkgname>) |
| [tupac](#tupac) | PHP | 是 | 是 | 按需要更新 | 与 pacman 一致 (e.g., tupac -S <pkgname>) |
| [Yaourt](#yaourt) | Bash, back-end in C | 是 | 是 | 是 | 与 pacman 一致 (e.g., yaourt -S <pkgname>) |