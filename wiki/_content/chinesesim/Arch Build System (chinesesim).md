**翻译状态：** 本文是英文页面 [Arch_Build_System](/index.php/Arch_Build_System "Arch Build System") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-04-12，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Build_System&diff=0&oldid=309643)可以查看翻译后英文页面的改动。

本文简要介绍 Arch 编译系统，同时提供一个使用教程。这不是一个完整的参考指南！如果需要更多信息，请参考手册页面。

**注意:** ABS 每天同步一次，所以可能会有一些滞后。

## Contents

*   [1 什么是 ABS](#.E4.BB.80.E4.B9.88.E6.98.AF_ABS)
    *   [1.1 类 ports 系统又是什么？](#.E7.B1.BB_ports_.E7.B3.BB.E7.BB.9F.E5.8F.88.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
    *   [1.2 ABS 的概念与之相似](#ABS_.E7.9A.84.E6.A6.82.E5.BF.B5.E4.B8.8E.E4.B9.8B.E7.9B.B8.E4.BC.BC)
    *   [1.3 ABS概览](#ABS.E6.A6.82.E8.A7.88)
*   [2 我为什么要用ABS](#.E6.88.91.E4.B8.BA.E4.BB.80.E4.B9.88.E8.A6.81.E7.94.A8ABS)
*   [3 如何使用 ABS](#.E5.A6.82.E4.BD.95.E4.BD.BF.E7.94.A8_ABS)
    *   [3.1 安装工具](#.E5.AE.89.E8.A3.85.E5.B7.A5.E5.85.B7)
    *   [3.2 /etc/abs.conf](#.2Fetc.2Fabs.conf)
    *   [3.3 ABS树](#ABS.E6.A0.91)
        *   [3.3.1 下载 ABS 树](#.E4.B8.8B.E8.BD.BD_ABS_.E6.A0.91)
        *   [3.3.2 /etc/makepkg.conf](#.2Fetc.2Fmakepkg.conf)
        *   [3.3.3 修改 /etc/makepkg.conf 中的 PACKAGER 变量](#.E4.BF.AE.E6.94.B9_.2Fetc.2Fmakepkg.conf_.E4.B8.AD.E7.9A.84_PACKAGER_.E5.8F.98.E9.87.8F)
            *   [3.3.3.1 列出所有包 （包括从 AUR 中获取的）](#.E5.88.97.E5.87.BA.E6.89.80.E6.9C.89.E5.8C.85_.EF.BC.88.E5.8C.85.E6.8B.AC.E4.BB.8E_AUR_.E4.B8.AD.E8.8E.B7.E5.8F.96.E7.9A.84.EF.BC.89)
            *   [3.3.3.2 只列出软件仓库中的包](#.E5.8F.AA.E5.88.97.E5.87.BA.E8.BD.AF.E4.BB.B6.E4.BB.93.E5.BA.93.E4.B8.AD.E7.9A.84.E5.8C.85)
            *   [3.3.3.3 建立一个工作目录](#.E5.BB.BA.E7.AB.8B.E4.B8.80.E4.B8.AA.E5.B7.A5.E4.BD.9C.E7.9B.AE.E5.BD.95)
        *   [3.3.4 编译软件包](#.E7.BC.96.E8.AF.91.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [3.3.5 fakeroot](#fakeroot)
    *   [3.4 保留修改过的软件包](#.E4.BF.9D.E7.95.99.E4.BF.AE.E6.94.B9.E8.BF.87.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)

## 什么是 ABS

ABS(Arch Build System)指的是Arch的构建系统。这是一种从源代码编译软件的类 ports 系统。在Arch中，[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 专门管理二进制软件包(包括那些由ABS创建的)，而ABS则是一系列工具，负责把源代码编译成可安装的`.pkg.tar.xz` 软件包。

### 类 ports 系统又是什么？

'Ports'是 *BSD 使用的一种系统，可以自动下载源代码、解压缩、打补丁、编译和安装。一个“port”仅仅是指用户电脑上的一个目录，根据即将安装的相应软件来命名，包含一些文件来指导源码的下载和编译安装，典型的方式是找到那个目录(或者说port)，进行`make`或 `make install clean`，然后系统就会下载、编译和安装你想要的软件了。

### ABS 的概念与之相似

**ABS**由一个目录树构成(the ABS Tree)，位于`/var/abs`。它包含许多子目录，每个子目录都属于某一类别，都以相应的可创建的软件包命名。这个目录树表示(但不包含)所有**官方 Arch 软件**，可以通过 SVN 系统取得。你可以把一个子目录称为一个“ABS”，就像称呼“port“那样。这些“ABS”(或者说子目录)**并不包含软件包或源代码**, 相对地，它包含一个[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 文件(有时也会有其它文件)。PKGBUILD是一个简单的Bash脚本——一个文本文件（包含对编译和打包过程的指示、包含源码包的下载地址）。ABS最重要的部分就是PKGBUILD。运行 ABS [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 命令，将先编译软件，然后在编译目录打包。然后就可以通过 Arch Linux 的软件包管理器[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")进行安装、升级和删除了。

### ABS概览

'ABS'可以作为一个总括性术语来使用，因为它包含并依赖于若干其他部件。因此，尽管从严格意义上来讲并不精确，ABS可指代包含以下工具的完整工具集：

	ABS tree

	`/var/abs/`下的目录结构。包含`/etc/abs.conf`指定的所有 Arch 官方软件。这些树会在安装 [abs](https://www.archlinux.org/packages/?name=abs) 之后，运行`abs`脚本的时候创建。

	[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")

	[Bash](/index.php/Bash "Bash")脚本，包含软件的源代码位置和编译打包指令。

	[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")

	ABS的 shell 命令工具,读取 PKGBUILD，下载源码，根据`makepkg.conf` 中的`PKGEXT`编译并创建 `.pkg.tar.gz` 或 `.pkg.tar.xz`包。

	[Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")

	Pacman是完全独立的，但是在安装或移除软件包、解决依赖性时都是必需的。它或者被 makepkg 调用或者被手动执行。

	[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")

	ArchLinux社区的用户维护的软件仓库独立于ABS，包含[unsupported]的PKGBUILDs。它们同样可以可以通过ABS的makepkg工具来编译并打包成可安装软件。ABS 树位于本地机器，而 AUR 则是网站界面。包含成千上万用户共享的 PKGBUILD。如果需要编译官方 Arch 树之外的软件包，AUR 中已经存在的可能性非常大。

## 我为什么要用ABS

ABS 可以用来:

*   编译或重新编译软件包
*   从源代码编译Arch官方源里没有的软件(详情请参照[创建软件包](/index.php/Creating_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Creating packages (简体中文)"))
*   定制现有的软件包以满足你的特定需求(通过开启或禁用相关选项)
*   用你的编译器的flags重新构建整个系统，“就像FreeBSD那样” 。(使用用[pacbuilder](/index.php/Pacbuilder_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacbuilder (简体中文)"))
*   干净地编译安装你自己定制的内核。(参照[内核编译(简体中文)](/index.php/Kernel_Compilation_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel Compilation (简体中文)"))
*   使内核模块(比如某些显卡驱动)在你定制的内核下正常工作
*   修改 PKGBUILD 中的版本就能方便的编译和安装新的、老的、beta 或者开发版本的 Arch 软件包

使用 Arch Linux 不一定会用到 ABS，但 ABS 确实可以自动化进行许多源码编译工作。

## 如何使用 ABS

使用ABS通过以下步骤来构建软件包:

1.  使用[pacman](/index.php/Pacman "Pacman")来安装[abs](https://www.archlinux.org/packages/?name=abs) 软件包。
2.  以root权限运行`abs`来与 Arch Linux 的服务器同步ABS文件树。
3.  复制需要构建的文件(一般在`/var/abs/<repo>/软件包名称`目录下)到一个用于构建的目录。
4.  切换到构建目录，编辑`PKGBUILD`文件(如果需要的话) 然后运行`makepkg`.
5.  根据PKGBUILD文件中的指令, makepkg 程序会自动下载源码包,解压, 打上补丁, 根据`makepkg.conf`中的`CFLAGS`编译它, 并将二进制文件打包为扩展名为`.pkg.tar.gz`或者`.pkg.tar.xz`的文件中.
6.  安装只需要简单地运行`pacman -U <.pkg.tar.xz文件>`删除软件包也同样使用pacman.

### 安装工具

首先从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包[abs](https://www.archlinux.org/packages/?name=abs).

需要的依赖会被自动安装，比如[rsync](/index.php/Rsync "Rsync"). 安装编译需要的工具链可以通过[软件包组](/index.php/Pacman#Installing_package_groups "Pacman") [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

### /etc/abs.conf

使用root编辑`/etc/abs.conf`，包含你想要的仓库。

删除你想要的软件仓库前的叹号，比如：

```
REPOS=(core extra community !testing)

```

### ABS树

当你第一次运行abs时，它用cvs系统令ABS树与Arch服务器同步。那么ABS树到底是什么呢？它位于/var/abs下，看起来是这样的：

```
| -- core/
|     || -- acl/
|     ||     || -- PKGBUILD
|     || -- attr/
|     ||     || -- PKGBUILD
|     || -- abs/
|     ||     || -- PKGBUILD
|     || -- autoconf/
|     ||     || -- PKGBUILD
|     || -- ...
| -- extra/
|     || -- acpid/
|     ||     || -- PKGBUILD
|     || -- apache/
|     ||     || -- PKGBUILD
|     || -- ...
| -- community/
|     || -- ...

```

所以说ABS树与软件包数据库有着完全一致的结构：

*   一级目录：软件仓库名
*   二级目录：软件的名字。
*   三级目录：PKGBUILD (包含编译软件包需要的信息) 和其它相关文件(补丁和(或)其它打包所需的文件)

ABS目录中并没有编译软件所需的源代码，**PKGBUILD**文件包含了一个URL，源码包将从那里自动下载。

#### 下载 ABS 树

以root身份运行：

```
# abs

```

ABS树会在`/var/abs`下创建。你会发现ABS树有几个分枝，这些分枝与你在`/etc/abs.conf`中的选择相对应。

abs命令也用于定期地同步和更新你的ABS树。

只同步一个软件（格式：所在仓库/名称，比如 core/abs）：

```
# abs <repository>/<package>

```

这样不用下载整个 abs 树就能编译。

#### /etc/makepkg.conf

`/etc/makepkg.conf`设定环境变量和编译器的flags。如果你使用SMP系统也许会希望编辑它。默认的设置是为i686和 x86_64优化的，在这些架构的单CPU系统上很有效。(默认设置可以在SMP机器上使用，但只会利用一个核心／CPU——参见[makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf")).

#### 修改 /etc/makepkg.conf 中的 PACKAGER 变量

设置 `/etc/makepkg.conf`文件中的 PACKAGER 变量是一个可选但又*极力推荐*的步骤。它能提供一个“标志“来快速识别某个包是由你打包或安装的，而不是这个包的官方维护者！使用[expac](https://www.archlinux.org/packages/?name=expac) 可以容易的完成这个工作。

##### 列出所有包 （包括从 AUR 中获取的）

```
$ grep myname /etc/makepkg.conf
PACKAGER="myname <myemail@myserver.com>

```

```
$ expac "%n %p" | grep "myname" | column -t
archey3 myname
binutils myname
gcc myname
gcc-libs myname
glibc myname
tar myname

```

##### 只列出软件仓库中的包

这个例子只列出了包含在`/etc/pacman.conf`的软件仓库中的包：

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)
binutils
gcc
gcc-libs
glibc
tar

```

##### 建立一个工作目录

你必须建立一个工作目录，编译将在那里进行。所有的事情都在那里完成；千万不要直接在ABS树里编译。在你的home文件夹下就很好，当然，有些使用者更愿意在`/var/abs/`下创建一个属于普通用户的“local“文件夹。

建立你的工作目录。比如：

```
$ mkdir -p $HOME/abs

```

把ABS从ABS树(var/abs/repository/pkgname)复制到编译目录。

#### 编译软件包

ABS是一种精致的工具，它为包创建过程提供强大的协助和高度的可定制性，并且生成一个可安装的包文件。ABS方式包括从ABS树自制ABS到工作目录和执行makepkg。在下面的例子中，我们将创建*slim*软件包。

把slim的ABS复制到工作目录。

```
$ cp -r /var/abs/extra/slim/ ~/abs

```

登入工作目录。

```
$ cd ~/abs/slim

```

修改 PKGBUILD 文件以进行增加或移除某些组件，打补丁或修改包的版本等工作。(可选的):

```
$ nano PKGBUILD

```

用普通用户执行makepkg (带 `-s` 参数以便在安装时自动处理依赖关系):

```
$ makepkg -s

```

以root身份安装：

```
# pacman -U slim 1.3.0-2-i686.pkg.tar.xz

```

这样就行了。你已经从源代码编译了slim并用pacman把它干净地安装到了系统中。卸载软件也用pacman来解决。(`pacman -R slim`)

*   ABS方式在某种程度上实现了自动化，为我们增添了便利。同时，通过PKGBUILD，它也保持了完全的透明度以及对编译安装流程的控制。

#### fakeroot

使用ABS编译软件方法与传统编译方法基本相同。 (一般包含 `./configure, make, make install` 等步骤), 不过软件被安装到了一个叫做*fake root* 的环境。 (*fake root*，简单的说，是在编译工作目录下的一个子目录，这个子目录的功能和行为与系统根目录(`/`)相同。与 **fakeroot** 程序结合, makepkg 创建了一个虚拟的根目录, 然后将编译好的二进制文件和其他相关文件以 **root** 用户身份安装到其中)。然后 *fake root*, 或者包含了编译好的软件的子目录，被压缩到以`.pkg.tar.xz`为后缀的压缩文档中，成为*软件包*. 当软件包被调用的时候，pacman 解压缩软件包并将它安装到系统真正的根目录(`/`)中。

### 保留修改过的软件包

Pacman 进行升级时会将修改后的软件包升级到仓库中的最新版本，可以通过下面方式避免这个行为：

在 PKGBUILD 中将软件包加入 `modified` 组.

 `PKGBUILD`  `groups=('modified') ` 

然后将此组加入`/etc/pacman.conf` 的 `IgnoreGroup`：

 `/etc/pacman.conf`  `IgnoreGroup = modified` 

这样软件包的升级就会被忽略，这时需要从 ABS 编译更新的软件包以防止部分升级。