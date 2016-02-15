**翻译状态：** 本文是英文页面 [Downgrading_Packages](/index.php/Downgrading_Packages "Downgrading Packages") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-09-19，点击[这里](https://wiki.archlinux.org/index.php?title=Downgrading_Packages&diff=0&oldid=221655)可以查看翻译后英文页面的改动。

本文将会向你展示如何把一个包降级到以前的版本。通常，并不推荐降级包，只有在现有包存在Bug的情况下才推荐降级。

在降级之前，好好考虑下你为什么要降级。如果是因为现有包有Bug，请花上几分钟帮忙把它报告给Arch的Bug追踪系统或软件包的项目地址。我们和上游的开发者们都会很感激报告Bug的用户。因为Bug 报告中的任何额外信息都有可能节省大量的测试时间，帮助我们发行更加稳定的软件。

## Contents

*   [1 原因](#.E5.8E.9F.E5.9B.A0)
*   [2 细节](#.E7.BB.86.E8.8A.82)
*   [3 如何降级软件包](#.E5.A6.82.E4.BD.95.E9.99.8D.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [4 如何找到旧版本](#.E5.A6.82.E4.BD.95.E6.89.BE.E5.88.B0.E6.97.A7.E7.89.88.E6.9C.AC)
    *   [4.1 过期源](#.E8.BF.87.E6.9C.9F.E6.BA.90)
    *   [4.2 ARM](#ARM)
    *   [4.3 手动编译](#.E6.89.8B.E5.8A.A8.E7.BC.96.E8.AF.91)
*   [5 更改仓库](#.E6.9B.B4.E6.94.B9.E4.BB.93.E5.BA.93)
*   [6 FAQ](#FAQ)
    *   [6.1 由于依赖问题我无法降级](#.E7.94.B1.E4.BA.8E.E4.BE.9D.E8.B5.96.E9.97.AE.E9.A2.98.E6.88.91.E6.97.A0.E6.B3.95.E9.99.8D.E7.BA.A7)
    *   [6.2 怎么才能阻止Pacman升级我已降级的包？](#.E6.80.8E.E4.B9.88.E6.89.8D.E8.83.BD.E9.98.BB.E6.AD.A2Pacman.E5.8D.87.E7.BA.A7.E6.88.91.E5.B7.B2.E9.99.8D.E7.BA.A7.E7.9A.84.E5.8C.85.EF.BC.9F)
    *   [6.3 我想把我的系统回溯到昨天的状态](#.E6.88.91.E6.83.B3.E6.8A.8A.E6.88.91.E7.9A.84.E7.B3.BB.E7.BB.9F.E5.9B.9E.E6.BA.AF.E5.88.B0.E6.98.A8.E5.A4.A9.E7.9A.84.E7.8A.B6.E6.80.81)

## 原因

降级一个软件包实质就是卸载当前版本的软件包再安装旧版本的软件包。这个”旧版本“可以是当前版本之前的任何一个版本。

降级的原因包括：当前软件包有Bug，当前软件包未包含你需要的功能，实验性的目的。不管哪种情况，用户都认为：降级软件包是解决目前包出现问题的一个有效办法。

降级一个包有时意味着其它包也要跟着它一起降级。对于那些装了一堆实验性或测试性软件包的用户，我们推荐直接重装整个系统而不是一个个降级软件包。

## 细节

但是，用户必须注意以下几点：

*   注意每个包的依赖性。每个版本的包所需要的库往往是不同的，相关文件的功能跟以前的版本可能完全是不一样的。所以在降级的时候，你也要同时将那些库更改到相应的版本。
*   注意是否在降级过程中一些必须的文件会被删除。Arch Linux的滚动发行策略使得它不会在软件仓库中保存任何旧软件。下面会详述这个问题。
*   注意在降级过程中对配置文件或脚本做出的更改。在目前，我们会依赖pacman来帮我们处理这个问题。

## 如何降级软件包

*   问: 当我运行 `pacman -Syu` 将软件包从版本甲升级到版本乙之后，发现这个软件包导致系统出现了一些问题，我该怎样将该软件包重新降级到版本甲呢？
*   答: 如果该包不是很重要的话，你可以降级的。先查看你系统的`/var/cache/pacman/pkg`目录，看看旧版本的软件包是不是还保存在那儿 (如果你最近没有执行 `pacman -Scc`以清空包缓存的话，应该在那儿)。 如果在，你可以执行`pacman -U pkgname-olderpkgver.pkg.tar.gz`来安装旧版本。如果pacman提示文件冲突的话，你可以通过加上`-f`参数以强制执行，即 `pacman -U --force pkgname-olderpkgver.pkg.tar.gz`。

这个过程会移除现有的包，仔细的计算所有依赖的改变，然后安装你选择的旧版本的软件包以及合适的依赖。

**注意:** 如果你改变了操作系统的一个基本的组件包，你也许需要降级许多包。这些软件包可能在过程中被删除，需要手动一点一点的安装回来；同时，后续升级时要小心，不要重新安装不想要的软件包版本。

在 [AUR](/index.php/AUR "AUR") 中有一个包叫做[downgrade](https://aur.archlinux.org/packages/downgrade/)。它是一个简单的 Bash 脚本，它会从你的缓存中寻找旧版本的包，如果没有的话它会搜索 [A.R.M.](#ARM)。你可以选择一个旧包来安装。它基本上自动化了上面所述的过程。查看 `downgrade --help` 获取使用方法的信息。

另一个更强大的工具是[downgrader](https://aur.archlinux.org/packages/downgrader/)，它可以处理 pacman 的 log，能从 ARM、本地缓存降级，并且可以处理包列表 (如果在升级一些包后不稳定，而你不确定包的名字)

## 如何找到旧版本

目前有三种方法

### 过期源

如果系统上找不到旧版本，请检查未即时同步的源，从里面下载软件包。软件源同步状态可以从[这里](https://www.archlinux.org/mirrors/status/)获得。

### ARM

[Arch Rollback Machine](http://ala.seblu.net/) (ARM) 里包含2009年9月1日以来所有仓库的归档。目前（2009年11月21日），这个网站还不稳定，根据以前的报道，丢失了2008年10月1日到目前的一些数据。

如果你对ARM感兴趣的话，最好是到它的宣传论坛了解一下相关信息，这样可以了解它的最新进度。它的宣传论坛在这里：[[1]](https://bbs.archlinux.org/viewtopic.php?id=53665).

据说，ARM想达到这样一个目的：使得使用wget+pacman可以方便的将你的系统回溯到某个时间点。但他们还没有给出这个自动化过程的具体解释。

### 手动编译

最糟糕的情况，如果这些地方都没有找到，那你就需要自己动手编译旧版本的软件包了。如果决定这样做，就可以从abs中先取出该软件包的PKGBUILD文件，然后修改相应的内容（通常是版本号）。或者访问 [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) 搜索你需要的降级的软件包，然后点 "查看修改" 链接，选择“查看日志“。找到你需要的版本然后点击路径。然后下载相应的文件再用makepkg编译即可。

对于AUR包来说，只能在http://pkgbuild.com/git/aur-mirror.git/ 处找到旧包的PKGBUILD，或者你可以到[Unofficial User Repositories]]处找到旧的二进制包。

## 更改仓库

要使用ARM仓库的话，注释掉原来的仓库，添加适当的ARM仓库地址即可：

```
[core]
#Server=http://mirrors.gigenet.com/archlinux/core/os/i686
Server=http://arm.konnichi.com/2009/11/01/core/os/i686

```

在这个例子中，这个配置会把当前系统的包回溯到2009年11月1日的状态。请注意，所有的仓库都是官方仓库的快照。所以你只需要更改`/etc/pacman.d/mirrorlist`处的镜像，把ARM的镜像放在最前头。 然后运行：

```
pacman -Syy  # refresh the sync databases
pacman -Suu  # downgrade all packages with a lower version in the repos

```

仅仅这样并不能保证无缝的回溯，因为有时候相对于版本号会有包冲突等问题。

更多信息请参考[pacman](/index.php/Pacman "Pacman")

## FAQ

### 由于依赖问题我无法降级

你可以使用`-d`选项在升级或删除包的时候忽略依赖的限制，比如，`pacman -Ud pkgpkgname-olderpkgver.pkg.tar.gz`，但这样做有可能破坏你的系统。

### 怎么才能阻止Pacman升级我已降级的包？

在`pacman.conf`中设置`IgnorePkg = package1 package2`会使Pacman在更新时忽略你列出的包。

### 我想把我的系统回溯到昨天的状态

如果你使用[LVM](/index.php/LVM "LVM")，并且开启了periodic snapshots的话，这很容易实现。