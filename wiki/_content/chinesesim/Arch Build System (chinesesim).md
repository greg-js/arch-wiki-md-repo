相关文章

*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Kernel Compilation with ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")
*   [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")
*   [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")
*   [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")

**翻译状态：** 本文是英文页面 [Arch_Build_System](/index.php/Arch_Build_System "Arch Build System") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-31，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Build_System&diff=0&oldid=491300)可以查看翻译后英文页面的改动。

本文简要介绍 Arch 编译系统，同时提供一个使用教程。这不是一个完整的参考指南！

## Contents

*   [1 什么是 ABS](#什么是_ABS)
    *   [1.1 类 ports 系统又是什么？](#类_ports_系统又是什么？)
    *   [1.2 ABS 的概念与之相似](#ABS_的概念与之相似)
    *   [1.3 ABS概览](#ABS概览)
        *   [1.3.1 SVN目录树](#SVN目录树)
*   [2 我为什么要用ABS](#我为什么要用ABS)
*   [3 如何使用 ABS](#如何使用_ABS)
    *   [3.1 使用 SVN 获取 PKGBUILD](#使用_SVN_获取_PKGBUILD)
        *   [3.1.1 前提](#前提)
        *   [3.1.2 非递归checkout](#非递归checkout)
        *   [3.1.3 Checkout软件包](#Checkout软件包)
    *   [3.2 使用 Git 获取 PKGBUILD](#使用_Git_获取_PKGBUILD)
    *   [3.3 构建软件包](#构建软件包)
*   [4 技巧](#技巧)
    *   [4.1 保留修改过的软件包](#保留修改过的软件包)
    *   [4.2 Checkout旧版本软件包](#Checkout旧版本软件包)
*   [5 其它工具](#其它工具)

## 什么是 ABS

ABS(Arch Build System)指的是Arch的构建系统。这是一种从源代码编译软件的类 ports 系统。在Arch中，[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 专门管理二进制软件包(包括那些由ABS创建的)，而ABS则是一系列工具，负责把源代码编译成可安装的`.pkg.tar.xz` 软件包。

### 类 ports 系统又是什么？

'Ports'是 *BSD 使用的一种系统，可以自动下载源代码、解压缩、打补丁、编译和安装。一个“port”仅仅是指用户电脑上的一个目录，根据即将安装的相应软件来命名，包含一些文件来指导源码的下载和编译安装，典型的方式是找到那个目录(或者说port)，进行`make`或 `make install clean`，然后系统就会下载、编译和安装你想要的软件了。

### ABS 的概念与之相似

**ABS**由一个目录树构成，可以用SVN checkout。这个目录树表示(但不包含)所有**官方 Arch 软件**。ABS子目录**并不包含软件包或源代码**，而是包含一个[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 文件(有时也会有其它文件)。在有PKGBUILD文件的目录里运行[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")命令，将在目录中编译软件，并打包。然后就可以通过[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")进行安装或升级了。

### ABS概览

'ABS'可以作为一个总括性术语来使用，因为它包含并依赖于若干其他部件。因此，尽管从严格意义上来讲并不精确，ABS可指代包含以下工具的完整工具集：

	SVN目录树

	目录树包含所有官方软件包的构建所需文件，不包括软件包本身和源代码。在[svn](https://www.archlinux.org/svn/)和[git](https://projects.archlinux.org/svntogit/packages.git/)仓库中。

	[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")

	[Bash](/index.php/Bash "Bash")脚本，包含软件的源代码位置和编译打包指令。

	[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")

	ABS的 shell 命令工具，读取 PKGBUILD，下载源码，根据`makepkg.conf` 中的`PKGEXT`编译并创建 `.pkg.tar.gz` 或 `.pkg.tar.xz`包。也可以用makepkg从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")或第三方代码构建自定义软件包。参考[Creating packages](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)")。

	[Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")

	pacman是完全独立的，但是在安装或移除软件包、解决依赖性时都是必需的。它或者被 makepkg 调用或者被手动执行。

	[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")

	ArchLinux社区的用户维护的软件仓库独立于ABS，包含[unsupported]的PKGBUILDs。它们同样可以可以通过ABS的makepkg工具来编译并打包成可安装软件。ABS 树位于本地机器，而 AUR 则是网站界面。包含成千上万用户共享的 PKGBUILD。如果需要编译官方 Arch 树之外的软件包，AUR 中已经存在的可能性非常大。

**Warning:** 官方PKGBUILD假定包是在干净的chroot环境中构建的([built in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot")). 在*脏*的环境中构建可能会失败或者在运行时有意外行为。 因为如果编译系统动态检查依赖的话，编译结果会受到当前可用包的影响。

#### SVN目录树

*core*, *extra*和*testing* [官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库") 可从官方SVN的*packages* 仓库[checkout](#非递归checkout). 而*community*和*multilib*在*community* SVN仓库。

每个包有各自的子目录，其中又有`repos`和`trunk`目录。`repos`又进一步按仓库名(如*core*)和架构细分。`repos`里的PKGBUILD和其它文件用来构建官方包。`trunk`里的文件是正在开发的，并最终复制到`repos`。

例如，[acl](https://www.archlinux.org/packages/?name=acl)的目录结构像这样：

```
acl
acl/repos
acl/repos/core-i686
acl/repos/core-i686/PKGBUILD
acl/repos/core-x86_64
acl/repos/core-x86_64/PKGBUILD
acl/trunk
acl/trunk/PKGBUILD

```

源代码并不直接包含在ABS目录中，而是构建时从`PKGBUILD`里指定的源代码URL下载。

## 我为什么要用ABS

ABS 可以用来:

*   编译或重新编译软件包
*   从源代码编译Arch官方源里没有的软件(详情请参照[创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)"))
*   定制现有的软件包以满足你的特定需求(通过开启或禁用相关选项)
*   用你的编译器的flags重新构建整个系统，“就像FreeBSD那样” 。(使用[pacbuilder-svn](https://aur.archlinux.org/packages/pacbuilder-svn/)不支持 git 仓库)
*   干净地编译安装你自己定制的内核。(参照[内核编译(简体中文)](/index.php/Kernel_Compilation_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel Compilation (简体中文)"))
*   使内核模块(比如某些显卡驱动)在你定制的内核下正常工作
*   修改 PKGBUILD 中的版本就能方便的编译和安装新的、老的、beta 或者开发版本的 Arch 软件包

使用 Arch Linux 不一定会用到 ABS，但 ABS 确实可以自动化进行许多源码编译工作。

## 如何使用 ABS

要获取需要的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")，从源代码编译软件包，需要使用 [Svn](/index.php/Svn "Svn") 或支持 [Git](/index.php/Git "Git") 的 [asp](https://www.archlinux.org/packages/?name=asp)。

### 使用 SVN 获取 PKGBUILD

#### 前提

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[subversion](https://www.archlinux.org/packages/?name=subversion)包。

#### 非递归checkout

**Warning:** 不要下载整个仓库，请按下面的说明操作。整个SVN非常大，不只会占用大量的空间，archlinux.org服务器也会因为下载产生费用。非正常使用可能会导致你的地址被封禁。不要对公共SVN进行任何脚本操作。

要checkout *core*, *extra*，和*testing*仓库:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/packages

```

要checkout *community*和*multilib*仓库:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/community

```

两条命令都只是创建了空目录，但它知道这是SVN checkout目录。

#### Checkout软件包

在刚才checkout的SVN仓库(*packages*或*community*)中执行：

```
$ svn update *package-name*

```

这条命令把指定的包同步到你的checkout目录。以后在顶层目录执行*svn update*时，这个包也会更新。

如果指定的包不存在，svn不会产生警告，只是显示类似"At revision 115847"而不创建文件。出现这种情况时：

*   检查软件包名的拼写
*   检查包是不是被移到了另一个仓库 (例如从community到主仓库)
*   到 [https://www.archlinux.org/packages](https://www.archlinux.org/packages) 检查这个包是不是从另一个基础包构建的 (例如[python-tensorflow](https://www.archlinux.org/packages/?name=python-tensorflow)是在[tensorflow](https://www.archlinux.org/packages/?name=tensorflow) PKGBUILD里构建的)

**Tip:** 要check旧版本，参考[#Checkout旧版本软件包](#Checkout旧版本软件包).

如果想在最新的版本进行编译，定期执行:

```
$ svn update

```

### 使用 Git 获取 PKGBUILD

先安装 [install](/index.php/Install "Install") 软件包 [asp](https://www.archlinux.org/packages/?name=asp)。

要获取某个软件包的 svntogit 仓库：

```
$ asp checkout *pkgname*

```

这个命令会将软件包的 git 仓库克隆到一个目录。

要更新本地仓库，在仓库目录执行 `asp update`，然后执行 `git pull`.

可以使用 git 的其它命令获取软件包的老版本，或记录自定也改动，详情请参考 [git](/index.php/Git "Git") 页面。

仅要获取某个软件包当前版本的快照，执行:

```
$ asp export *pkgname*

```

### 构建软件包

关于如何配置*makepkg*来从[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")构建软件包，请参考[makepkg (简体中文)#配置](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#配置 "Makepkg (简体中文)")。

把[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")所在目录复制到新的位置。在新目录按需要进行修改。 并按照[makepkg (简体中文)#使用](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用 "Makepkg (简体中文)")来构建和安装软件包。

## 技巧

### 保留修改过的软件包

Pacman 进行升级时会将修改后的软件包升级到仓库中的最新版本，可以通过下面方式避免这个行为：

在 PKGBUILD 中将软件包加入 `modified` 组.

 `PKGBUILD`  `groups=('modified') ` 

然后将此组加入`/etc/pacman.conf` 的 `IgnoreGroup`：

 `/etc/pacman.conf`  `IgnoreGroup = modified` 

当系统生升级发现官方仓库中有新版本时，pacman会显示软件包因为在*IgnoreGroup*中而被忽略的提示，这时需要从 ABS 编译更新的软件包以防止部分升级。

### Checkout旧版本软件包

在checkout[#非递归checkout](#非递归checkout)的SVN仓库目录 (即"packages"或"community") 中查看日志:

```
$ svn log *package-name*

```

从历史记录中找出要checkout的版本。例如要checkout版本`r1729`:

```
$ svn update -r1729 *package-name*

```

已存在的*package-name*目录会更新成指定版本。

也可以指定一个日期，如果当天没有对应版本，svn会找出之前的最近版本。下面的例子checks out了2009-03-03的版本:

```
$ svn update -r{20090303} *package-name*

```

要checkout被移动到另一个仓库之前的包，只需查看日志，找到移动之前的日期或版本即可。

## 其它工具

*   [pbget](http://xyne.archlinux.ca/projects/pbget/) - 从web接口直接获取某个包的PKGBUILD，支持AUR.
*   [asp](https://github.com/falconindy/asp) - 管理Arch Linux包构建源文件的工具。使用了git接口获取新的源。