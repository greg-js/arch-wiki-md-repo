**翻译状态：** 本文是英文页面 [Creating_Packages](/index.php/Creating_Packages "Creating Packages") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-15，点击[这里](https://wiki.archlinux.org/index.php?title=Creating_Packages&diff=0&oldid=492423)可以查看翻译后英文页面的改动。

相关文章

*   [Arch 编译系统](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")
*   [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")
*   [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")
*   [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")
*   [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [Patching in ABS](/index.php/Patching_in_ABS "Patching in ABS")
*   [Creating packages for other distributions](/index.php/Creating_packages_for_other_distributions "Creating packages for other distributions")
*   [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")

本文旨在帮助用户利用 Arch Linux 的类似 ports 的软件包构建系统创建自己的软件包。包含了创建 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") – 一个包创建描述文件，由 `makepkg` 使用来从源代码创建二进制包。[Arch 软件包标准](/index.php/Arch_packaging_standards_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch packaging standards (简体中文)")包含当前规则和提高软件包质量的方法。如果已经有了 `PKGBUILD` 文件，请参考 [makepkg (简体中文)](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)").

## Contents

*   [1 概述](#.E6.A6.82.E8.BF.B0)
    *   [1.1 元软件包和软件包组](#.E5.85.83.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.92.8C.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BB.84)
*   [2 准备工作](#.E5.87.86.E5.A4.87.E5.B7.A5.E4.BD.9C)
    *   [2.1 必需的软件包](#.E5.BF.85.E9.9C.80.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.2 下载并测试安装](#.E4.B8.8B.E8.BD.BD.E5.B9.B6.E6.B5.8B.E8.AF.95.E5.AE.89.E8.A3.85)
*   [3 创建PKGBUILD](#.E5.88.9B.E5.BB.BAPKGBUILD)
    *   [3.1 定义PKGBUILD变量](#.E5.AE.9A.E4.B9.89PKGBUILD.E5.8F.98.E9.87.8F)
    *   [3.2 PKGBUILD 函数](#PKGBUILD_.E5.87.BD.E6.95.B0)
        *   [3.2.1 prepare()](#prepare.28.29)
        *   [3.2.2 pkgver()](#pkgver.28.29)
        *   [3.2.3 build()](#build.28.29)
        *   [3.2.4 check()](#check.28.29)
        *   [3.2.5 package()](#package.28.29)
*   [4 测试PKGBUILD文件](#.E6.B5.8B.E8.AF.95PKGBUILD.E6.96.87.E4.BB.B6)
    *   [4.1 检查包的逻辑性](#.E6.A3.80.E6.9F.A5.E5.8C.85.E7.9A.84.E9.80.BB.E8.BE.91.E6.80.A7)
*   [5 把包提交给AUR](#.E6.8A.8A.E5.8C.85.E6.8F.90.E4.BA.A4.E7.BB.99AUR)
*   [6 总结](#.E6.80.BB.E7.BB.93)
    *   [6.1 注意事项](#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
*   [7 更详细的规则](#.E6.9B.B4.E8.AF.A6.E7.BB.86.E7.9A.84.E8.A7.84.E5.88.99)
*   [8 PKGBUILD 生成器](#PKGBUILD_.E7.94.9F.E6.88.90.E5.99.A8)
*   [9 参考](#.E5.8F.82.E8.80.83)

## 概述

Arch Linux 中的软件包是通过 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 工具以及存储在 [PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 文件中的信息编译的。运行`makepkg`时，系统将自动在当前目录下搜索 `PKGBUILD`文件,然后根据`PKGBUILD`把软件源码重新打包。成功编译后得到的二进制文件和可以得到的其他信息如包的版本信息和依赖关系等，都将被打包到一个文件叫`name.pkg.tar.xz` 里，可以通过`pacman -Up <package file>`进行安装。

一个 Arch 软件包仅仅是一个使用 xz 压缩的 tar 压缩包，或者叫 'tarball'。它包含了以下由 makepkg 生成的文件：

*   要安装的二进制文件

*   `.PKGINFO`: 包含所有 pacman 处理软件包的元数据，依赖等等。

*   `.MTREE`: 包含了文件的哈希值与时间戳. pacman 能够根据这些储存在本地数据库的信息校验软件包的完整性.

*   `.INSTALL`: 可选的文件，可以用来在安装/升级/删除操作之后运行命令。(本文件只有在 `PKGBUILD` 中制定才会存在。)

*   `.Changelog`: 一个可选的文件，保存了包管理员描述软件更新的日志。(不是所有包中都存在。)

### 元软件包和软件包组

软件包组是一组软件包，由打包者定义。按组安装/删除时， 通过组名可以替代组中的所有软件包。安装方法参考[Pacman#Installing package groups](/index.php/Pacman#Installing_package_groups "Pacman")和[PKGBUILD#groups](/index.php/PKGBUILD#groups "PKGBUILD").

元软件包，通常以 *-meta* 结尾，可软件包组提供的功能类似，可以同时安装一系列软件，安装方法和其它软件包一样，参考[Pacman#Installing specific packages](/index.php/Pacman#Installing_specific_packages "Pacman"). 元软件包和正常软件包的唯一区别，是元软件包是空的，仅记录其它软件间的依赖关系。

和软件包组相比，元软件包的优点是所有后续加入的软件包都会在更新时被自动安装。而如果有新软件包加入一个组，这个软件吧不会在更新时自动被安装。元软件包的缺点是不如软件包组灵活。使用软件包组时，可以只删除组中的某几个软件，其它软件保持不变。而使用元软件包时，只有删除元软件包之后，才能自由删除其中的单个包。

## 准备工作

### 必需的软件包

首先，确定你已安装必须的工具包。安装 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)应该足够了；它包含**make**和其它一些从源码编译时所需要的工具。

创建包的一个很重要的工具是[makepkg](/index.php/Makepkg "Makepkg")（由[pacman](https://www.archlinux.org/packages/?name=pacman)提供），它主要做以下工作：

1.  检查相关依赖是否安装。
2.  从指定的服务器下载源文件。
3.  解压源文件。
4.  编译软件并将它安装于伪root环境下。
5.  删除二进制文件和库文件的符号连接。
6.  生成包的meta文件。
7.  将伪root环境压缩成一个包文件
8.  将生成的包文件保存到配置的文件夹中（默认为当前工作目录）。

### 下载并测试安装

下载你想打包的软件的源代码压缩包，解压，按照作者所说的步骤安装它。记录下在编译和安装软件过程中需要的所有命令或步骤。你将要在*PKGBUILD*文件中重复这些命令和步骤。

大多数软件作者遵循三步走的安装惯例：

```
./configure
make
make install

```

这是一个能确保程序正常运行的好时机。

## 创建PKGBUILD

当你运行`makepkg`时，它会在当前工作目录寻找一个`PKGBUILD`文件。如果找到`PKGBUILD`文件，它会下载该软件的源代码，根据`PKGBUILD`文件中的指令编译它。PKGBUILD中的指令必须能完全被[Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell) "wikipedia:Bash (Unix shell)")解释。成功完成后，最后的二进制文件和包的元信息（即包的版本、依赖）被一起打包在`pkgname.pkg.tar.xz`文件包中，这个文件包可以使用`pacman -U *<package file>*`来安装。

要开始制作一个包，你应该先创建一个空工作目录，进入该目录，创建一个`PKGBUILD`文件。你可以复制PKGBUILD模板（位于/usr/share/pacman/）到工作目录，或者复制一个类似包的PKGBUILD也可以。如果你只想在别人的基础上更改一些选项的话，后一种方法比较方便。

### 定义PKGBUILD变量

PKGBUILD文件的编写例子可以在`/usr/share/pacman/`处找到。PKGBUILD文件中可能用到的一些变量意义的解释可以在[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")中找到。

*makepkg* 定义了两个变量，你应该在编译和安装的过程中使用它们：

	`srcdir`

	*makepkg*将会把源文件解压到此文件夹或在此文件夹中生成指向 PKGBUILD 里 source 数组中文件的软连接。

	`pkgdir`

	*makepkg*会把该文件夹当成系统根目录，并将软件安装在此文件夹下。

这些变量都是*绝对路径*, 即意味着, 如果你合适地使用这些变量, 就不用担心当前工作目录的影响.

**注意:** `build()`和`package()`函数在运行过程中都应当是非交互的。在这些函数中调用交互工具或脚本可能会中断*makepkg*的运行。（参考[FS#13214](https://bugs.archlinux.org/task/13214)）

**注意:** 如果你是接手别人的包，除了把你的名字列为包维护者（Maintainers）外，你还应当把之前的维护者列为贡献者（Contributors）。

### PKGBUILD 函数

一共有五个函数, 以下按照它们执行的先后顺序列出. 不存在的函数会被忽略.

**注意:** `package()` 函数是每个 PKGBUILD 中必须的函数, 不能省略.

#### prepare()

此函数会执行用于预处理源文件以进行构建的命令, 例如 patching. 此函数执行在 build() 之前, 软件包解压之后. 如果解压过程被跳过 (`makepkg -e`), 那么 `prepare()` 函数就不会被执行.

**注意:** (从 [PKGBUILD(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5)) 中可以知道, 该函数运行在 `bash -e` 模式下, 意味着任何以非零状态退出的命令都会造成该函数中止.

#### pkgver()

`pkgver()` 会在抓取并解压源文件，执行 prepare() 后后执行此函数。

如果你正在[制作 git/svn/hg 等](/index.php/VCS_PKGBUILD_Guidelines "VCS PKGBUILD Guidelines")构建过程相同, 但源文件可能每天甚至每小时更新一次的软件包的时候, 这一特性是十分有用的. 过去的方法是把日期写入到 pkgver 变量中, 但这样一来 makepkg 会在即使软件没有更新的情况下依然重新构建软件包, 因为它会认为软件包的版本改变了. 其他与此有关的命令有 `git describe`, `hg identify -ni` 等等. 请在提交 PKGBUILD 前做好测试, 因为如果 `pkgver()` 执行失败, 整个构建过程都会终止.

**注意:** pkgver 不能含有空格或连接符 (`-`). 通常都会用 sed 来进行修改.

#### build()

现在你需要编写`PKGBUILD`文件中的`build()`函数。这个函数使用通用的shell命令来自动编译软件并创建软件的安装目录。这允许*makepkg*无需详查你的文件系统就可以打包你的软件。

在`build()`函数中第一步就是进入由解压源码包所生成的目录。 *makepkg* 会在执行 `build()` 函数之前更改当前目录为 `$srcdir`; 因此, 大多数情况下第一条命令是这样的(参考示例文件`/usr/share/pacman/PKGBUILD.proto`)：

```
cd "$srcdir/$pkgname-$pkgver"

```

现在，你需要把你当时手动编译软件时用到的命令一一列上。`build()`基本上会自动运行你当时手动输入的命令并在伪root环境下编译该软件。如果你要打包的软件使用了一个配置脚本，最好在配置中加上`--prefix=/usr`。许多软件都将自己安装到`/usr/local`下，我们仅仅推荐当你手动从源码安装时这么做。所有的Arch Linux软件包都应当使用`/usr`目录。

```
./configure --prefix=/usr
make

```

**注意:** 如果你的软件不需要构建任何东西, 请不要使用 `build()` 函数. 但`package()` 函数依然是必须的.

#### check()

用来执行`make check`和其他一些例行测试的地方。如果不需要可以通过在 PKGBUILD/makepkg.conf 中使用 `BUILDENV+=('!check')` 或者给 `makepkg` 传入参数 `--nocheck` 来禁用它。

#### package()

最后一步就是把编译好的文件放到`pkg`文件夹——一个简单的伪root环境。`pkg`目录复制了根目录下软件安装路径的继承关系。如果你需要手动把文件放到根目录下，那么在这里你需要把文件放在`pkg`下相同的文件层级结构中。比如，你想把一个文件安装到`/usr/bin`，那么在伪root环境中对应的路径为`$pkgdir/usr/bin`。极少情况下的安装步骤需要用户手动复制大量的文件到某个地方。大部分软件安装时只需要调用`make install`即可。为了将软件安装到正确的路径，最后一行一般应该这样写：

```
make DESTDIR="$pkgdir/" install

```

**Note:** 有时候在`Makefile`里没有使用`DESTDIR`；你可能需要使用`prefix`来替代。如果软件包是用*autoconf*/*automake*来创建的，那就使用`DESTDIR`；如果`DESTDIR`不起作用，试试`make prefix="$pkgdir/usr/" install`。如果这还不起作用的话，你就需要深入检查软件的安装命令了。

`makepkg --repackage` 命令只运行`package()`函数,它只是将文件打包成软件包，并不运行编译过程。如果你只是更改了PKGBUILD中的依赖，用这个命令来打包可以节省很多时间。

## 测试PKGBUILD文件

你在写`PKGBUILD`的 `build()`方法时，会想频繁的测试你所做的改动以确保没有bug。你可以在包含 `PKGBUILD`的目录下运行`makepkg`命令来确保没有问题。如果`PKGBUILD`没有错误，将会生成一个包，但是如果`PKGBUILD`被破坏或未完成，它将抛出一个错误。

如果运行`makepkg` 成功，在你工作的目录下将会生成一个名为$pkgname-$pkgver.pkg.tar.gz的新文件。这个文件可以使用`pacman -U` 或 `pacman -A`安装，你也可以将它加到本地或网上的软件仓库中。注意，一个包被构建并不代表你的工作就完成了！只有当所有文件的结构都正确才能确保完成，例如你给了一个不正确的前缀就不行。你可以使用pacman的查询功能显示软件包包含的文件及依赖的文件，然后将它于你认为正确的对比。"pacman -Qlp <package file>" 和"pacman -Qip <package file>" 可以完成这项工作。

如果包看起来是正确的，那你的工作就完成了。但是如果你打算发布这个包或PKGBUILD，你就需要确认确认再确认包的依赖关系。

同样要确保安装的软件确实很完美的运行！如果你释放了一个包括所有必需文件的包，但是由于一些配置选项使它不能很好的工作，这真是让人恼火。如果你只是为你自己的系统安装这个软件，你就不必做这个质量保证了，因为只有你一个人需要忍受这些错误。

### 检查包的逻辑性

确定包可以正常使用后，再使用[namcap](/index.php/Namcap "Namcap")来检查错误：

```
$ namcap PKGBUILD
$ namcap *<package file name>*.pkg.tar.xz

```

Namcap将会做以下工作：

1.  检查PKGBUILD文件里的一些常见错误
2.  用`ldd`扫描包中所有的ELF文件，自动报告缺失或可去除的依赖。
3.  启发式搜寻缺失或冗余的依赖。

要养成用namcap检查包的习惯，以避免提交包后再做修复的麻烦。

## 把包提交给AUR

请参考[AUR User Guidelines#Submitting packages](/index.php/AUR_User_Guidelines#Submitting_packages "AUR User Guidelines")，里面详细介绍了提交流程。

## 总结

*   下载你希望打包的软件源代码
*   试着编译安装包到任意目录
*   复制PKGBUILD的文件模板 `/usr/share/pacman/PKGBUILD.proto`到一个临时的目录并重命名为 `PKGBUILD`
*   根据具体情况修改 PKGBUILD 文件
*   运行 `makepkg` 看看输出的打包结果是否正确
*   如果不正确，重复前两个步骤

### 注意事项

*   在开始自动打包之前，请确保你至少已成功手动打包一次，除非你“很清楚”你正在做什么。不幸的是，虽然大多数软件作者遵循了三步走的安装惯例：`./configure`; `make`; `make install`，但事情并不都是这样的，有时候你不得不自己打补丁才能安装成功。经验是：如果你手动无法编译成功或者无法将软件安装到指定子目录下，那你就不必费心打包了。`makepkg`没有任何魔力能消除源代码的问题让你编译成功。
*   在一些情况下，你可能无法直接得到包的源码，可能需要使用`sh installer.run`这样的东西来工作。这时就需要你自己做很多工作了（比如读READMEs，安装指导，手册，或者Gentoo的ebuilds等等）。在一些很变态的情况下，你需要自己编辑源码才能正常安装。但是，`makepkg`需要完全自主运行，不能有用户的干预。因此，如果你想修改makefiles，你需要随PKGBUILD附上一个定制的补丁，然后在`prepare()`函数里安装这个补丁；或者你可以在`prepare()`函数里通过`sed`来修改。

## 更详细的规则

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

## PKGBUILD 生成器

某些软件包的 PKGBUILD 可以通过工具自动生成。

**Note:** 用户需要在提交文件到 [AUR](/index.php/AUR "AUR") 前确保软件包满足高质量标准。

*   [Go](/index.php/Go "Go"): [go-makepkg](https://github.com/seletskiy/go-makepkg)
*   [Haskell](/index.php/Haskell "Haskell"): [cblrepo](https://github.com/magthe/cblrepo)
*   [Python](/index.php/Python "Python"): [pipman-git](https://aur.archlinux.org/packages/pipman-git/), [pip2arch-git](https://aur.archlinux.org/packages/pip2arch-git/), [PyPI2PKGBUILD](https://github.com/anntzer/pypi2pkgbuild)
*   [Ruby](/index.php/Ruby "Ruby"): [gem2arch](https://aur.archlinux.org/packages/gem2arch/), [pacgem](https://aur.archlinux.org/packages/pacgem/)

## 参考

*   [How to correctly create a patch file](https://bbs.archlinux.org/viewtopic.php?id=91408).
*   [Arch Linux Classroom IRC Logs of classes about creating PKGBUILDs](https://archwomen.org/media/project_classroom/classlogs/).
*   [Fakeroot approach for package installation](http://www.linuxfromscratch.org/hints/downloads/files/fakeroot.txt)