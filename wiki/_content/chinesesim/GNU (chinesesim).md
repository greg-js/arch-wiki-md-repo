Related articles

*   [Arch Linux (简体中文)](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")
*   [Core utilities (简体中文)](/index.php/Core_utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Core utilities (简体中文)")

**翻译状态：** 本文是英文页面 [GNU](/index.php/GNU "GNU") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-10-22，点击[这里](https://wiki.archlinux.org/index.php?title=GNU&diff=0&oldid=548453)可以查看翻译后英文页面的改动。

From [Wikipedia](https://en.wikipedia.org/wiki/GNU "wikipedia:GNU"):

	GNU 是一种操作系统和一种电脑软件的广泛集合. GNU 完全由免费软件组成, 它们中的大多数都有GNU项目自己的普遍公共合格证（GPL）的许可. GNU "GNU's Not Unix!"的递归缩写.

因为GNU内核, [Hurd](https://www.gnu.org/s/hurd/hurd.html), 还没能生产 [[1]](https://www.gnu.org/software/hurd/hurd/status.html) GNU 通常使用 Linux 内核. [Arch Linux (简体中文)](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)") 就是这样一种 GNU/Linux 发行版, 使用的是比如说 [Bash (简体中文)](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)") shell, GNU 核心工具, the GNU 工具链和许多其他工具和库. 这个页面不打算列出所有 [将近400个](https://www.gnu.org/software/software.html#allgnupkgs) GNU 包，只列出一些重要的.

## Contents

*   [1 Texinfo](#Texinfo)
*   [2 基本系统](#基本系统)
*   [3 工具链](#工具链)
    *   [3.1 构建系统](#构建系统)
*   [4 其他软件](#其他软件)
*   [5 可参阅](#可参阅)

## Texinfo

GNU 软件是用 [Texinfo](https://en.wikipedia.org/wiki/Texinfo "wikipedia:Texinfo") 排版语法来编排的. 你可以通过`info` 程序查阅info文档, 这由 [texinfo](https://www.archlinux.org/packages/?name=texinfo) 包提供, 这是 [base](https://www.archlinux.org/groups/x86_64/base/)的一部分.

大部分GNU软件都提供了 [Man page (简体中文)](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)"), 这个Info文档更全面.

## 基本系统

*   **[GRUB](/index.php/GRUB "GRUB")** — GRUB 是来自 GNU 项目的引导程序.

	[https://www.gnu.org/software/grub/](https://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[Bash](/index.php/Bash "Bash")** — 是一种与其他shell兼容的shell，它合并了许多来自korn shell（ksh）和C shell（csh）的特性.

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[Coreutils](/index.php/Coreutils "Coreutils")** — “核心”组件提供了GNU操作系统的基本文件、shell和文本操作工具.

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/gzip "wikipedia:gzip")** — gzip 既是一种文件格式又是一种压缩和解压的工具.

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar "Tar")** — 它提供了创建和解压tar压缩包的功能，当然还有其它不同的功能.

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## 工具链

大部分来自 [GNU toolchain](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain") 的工具都在 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 组里, 除了 *glibc* 在 [base](https://www.archlinux.org/groups/x86_64/base/)里而GBD都不在它们两个组里.

*   **[GNU make](https://en.wikipedia.org/wiki/Make_(software) "wikipedia:Make (software)")** — GNU make工具用于维护程序组.

	[http://www.gnu.org/software/make](http://www.gnu.org/software/make) || [make](https://www.archlinux.org/packages/?name=make)

*   **[GCC](/index.php/GCC "GCC")** — GNU编译器集合-C和C++前段.

	[https://gcc.gnu.org/](https://gcc.gnu.org/) || [gcc](https://www.archlinux.org/packages/?name=gcc)

*   **[glibc](https://en.wikipedia.org/wiki/GNU_C_Library "wikipedia:GNU C Library")** — GNU的C库实现 library.

	[https://www.gnu.org/software/libc/](https://www.gnu.org/software/libc/) || [glibc](https://www.archlinux.org/packages/?name=glibc) ([base](https://www.archlinux.org/groups/x86_64/base/)的一部分)

*   **[GNU Binutils](https://en.wikipedia.org/wiki/GNU_Binutils "wikipedia:GNU Binutils")** — 一组用来汇编和操作二进制和模板文件的程序。包括 [ld](https://en.wikipedia.org/wiki/GNU_linker "wikipedia:GNU linker").

	[https://www.gnu.org/software/binutils/](https://www.gnu.org/software/binutils/) || [binutils](https://www.archlinux.org/packages/?name=binutils)

*   **[GNU bison](https://en.wikipedia.org/wiki/GNU_bison "wikipedia:GNU bison")** — GNU通用解析器生成器.

	[https://www.gnu.org/software/bison/bison.html](https://www.gnu.org/software/bison/bison.html) || [bison](https://www.archlinux.org/packages/?name=bison)

*   **[GNU m4](https://en.wikipedia.org/wiki/GNU_m4 "wikipedia:GNU m4")** — GNU宏处理器.

	[https://www.gnu.org/software/m4/](https://www.gnu.org/software/m4/) || [m4](https://www.archlinux.org/packages/?name=m4)

*   **[GDB](https://en.wikipedia.org/wiki/GNU_Debugger "wikipedia:GNU Debugger")** — GNU 调试器.

	[https://www.gnu.org/software/gdb/](https://www.gnu.org/software/gdb/) || [gdb](https://www.archlinux.org/packages/?name=gdb)

### 构建系统

来自[维基百科](https://en.wikipedia.org/wiki/GNU_build_system "wikipedia:GNU build system"):

	GNU构造系统，也被叫做自动工具，是一套用来帮助让源码包能移植到类Unix系统的编程工具

*   **[GNU Autoconf](https://en.wikipedia.org/wiki/Autoconf "wikipedia:Autoconf")** — 用来自动设置源码的工具.

	[http://www.gnu.org/software/autoconf](http://www.gnu.org/software/autoconf) || [autoconf](https://www.archlinux.org/packages/?name=autoconf)

*   **[GNU Automake](https://en.wikipedia.org/wiki/Automake "wikipedia:Automake")** — 自动创建make文件的工具.

	[http://www.gnu.org/software/automake](http://www.gnu.org/software/automake) || [automake](https://www.archlinux.org/packages/?name=automake)

*   **[GNU Libtool](https://en.wikipedia.org/wiki/GNU_Libtool "wikipedia:GNU Libtool")** — 支持脚本的通用库.

	[http://www.gnu.org/software/libtool](http://www.gnu.org/software/libtool) || [libtool](https://www.archlinux.org/packages/?name=libtool)

## 其他软件

其它可选的工具能在 [official repositories](/index.php/Official_repositories "Official repositories")找到:

*   [GNOME](/index.php/GNOME "GNOME"), 一种桌面环境
*   [GIMP](/index.php/GIMP "GIMP"), 一种图片编辑器
*   [GTK+](/index.php/GTK%2B "GTK+"), 一种小部件工具包
*   [Gnumeric](/index.php/Gnumeric "Gnumeric"), 一种处理表格的软件
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"), 一种分区管理器
*   [GNU Screen](/index.php/GNU_Screen "GNU Screen"), 一种终端多路复用器
*   [GNU nano](/index.php/GNU_nano "GNU nano"), 一种命令行文本编辑器
*   [GNU Emacs](/index.php/GNU_Emacs "GNU Emacs"), 一种可扩展的、可自定义的、可自文档化文本编辑器
*   [GnuPG](/index.php/GnuPG "GnuPG"), 一种 OpenPGP 实现
*   [GNU Octave](/index.php/GNU_Octave "GNU Octave"), 一种科学编程工具
*   [GNU Readline](/index.php/Readline "Readline"), 用于命令行界面的行编辑库

## 可参阅

*   [https://www.gnu.org/](https://www.gnu.org/)
*   [The GNU Manifesto](https://www.gnu.org/gnu/manifesto)
*   [Wikipedia:List of GNU packages](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")
*   [Arch Hurd Project](https://archhurd.org/) 针对移植Arch Linux到Hurd内核.