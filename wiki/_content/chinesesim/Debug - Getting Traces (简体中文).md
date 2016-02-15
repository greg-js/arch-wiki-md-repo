**翻译状态：** 本文是英文页面 [Debug_-_Getting_Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-06-16，点击[这里](https://wiki.archlinux.org/index.php?title=Debug_-_Getting_Traces&diff=0&oldid=257963)可以查看翻译后英文页面的改动。

这篇文章目的在于帮助你创建一个调试用的Arch软件包，并且使用它来提供回溯和调试信息来将软件bug报告给开发者。

## Contents

*   [1 发现包的名称](#.E5.8F.91.E7.8E.B0.E5.8C.85.E7.9A.84.E5.90.8D.E7.A7.B0)
    *   [1.1 一些调试信息的事实](#.E4.B8.80.E4.BA.9B.E8.B0.83.E8.AF.95.E4.BF.A1.E6.81.AF.E7.9A.84.E4.BA.8B.E5.AE.9E)
    *   [1.2 找到包](#.E6.89.BE.E5.88.B0.E5.8C.85)
*   [2 获取 PKGBUILD](#.E8.8E.B7.E5.8F.96_PKGBUILD)
    *   [2.1 使用AUR](#.E4.BD.BF.E7.94.A8AUR)
    *   [2.2 使用ABS](#.E4.BD.BF.E7.94.A8ABS)
*   [3 编译设置](#.E7.BC.96.E8.AF.91.E8.AE.BE.E7.BD.AE)
    *   [3.1 全局设定](#.E5.85.A8.E5.B1.80.E8.AE.BE.E5.AE.9A)
    *   [3.2 仅单个软件包设定](#.E4.BB.85.E5.8D.95.E4.B8.AA.E8.BD.AF.E4.BB.B6.E5.8C.85.E8.AE.BE.E5.AE.9A)
    *   [3.3 Qt](#Qt)
    *   [3.4 KDE应用](#KDE.E5.BA.94.E7.94.A8)
*   [4 构建和安装软件包](#.E6.9E.84.E5.BB.BA.E5.92.8C.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [5 获得回溯](#.E8.8E.B7.E5.BE.97.E5.9B.9E.E6.BA.AF)
*   [6 总结](#.E6.80.BB.E7.BB.93)
*   [7 参见](#.E5.8F.82.E8.A7.81)

## 发现包的名称

### 一些调试信息的事实

当查看调试信息，如下：

```
[...]
Backtrace was generated from '/usr/bin/epiphany'

**(no debugging symbols found)**
Using host libthread_db library "/lib/libthread_db.so.1".
**(no debugging symbols found)**
[Thread debugging using libthread_db enabled]
[New Thread -1241265952 (LWP 12630)]
(no debugging symbols found)
0xb7f25410 in __kernel_vsyscall ()
#0  0xb7f25410 in __kernel_vsyscall ()
#1  0xb741b45b in **??** () from /lib/libpthread.so.0
[...]

```

你可以看到在出现`??`的地方调试信息是缺失的，库的名称和执行的函数也是。相似的，当这一行`(no debugging symbols found)`出现在调试信息中时，它意味着你不得不寻找指出的文件。

### 找到包

使用[Pacman](/index.php/Pacman "Pacman")来获取包信息：

```
# pacman -Qo /lib/libthread_db.so.1
/lib/libthread_db.so.1 is owned by _glibc_ 2.5-8

```

于是我们找到这个版本为2.5-8叫作[glibc](https://www.archlinux.org/packages/?name=glibc)的包。通过重复这一步，我们能够创建一个我们不得不自己编译的软件包列表，来获取完整的堆栈回溯。

## 获取 PKGBUILD

为了从源码构建一个软件包，需要PKGBUILD包。通常你可以从以下位置获得PKGBUILD：

1.  [AUR](/index.php/AUR "AUR") 或者
2.  [ABS](/index.php/ABS "ABS")

### 使用AUR

使用 [AUR search page](https://aur.archlinux.org/packages.php)来找到相应的软件包。如果不在其中，这个包就在Arch Linux的官方镜像树中。如果(在aur中)找到了，点击它的名字并且下载`Tarball`。使用 `tar`命令来解压它并且更改目录

```
$ tar xvzf name_of_tarball.tar.gz
$ cd name_of_tarball

```

### 使用ABS

如果这个包是官方树的一部分，安装[ABS](/index.php/ABS "ABS"), 获取软件包的源码然后构建它：

```
$ ABSROOT=. abs core/glibc
$ cd core/glibc
$ makepkg -s

```

## 编译设置

这个阶段，如果你将使用`makepkg`仅仅为了调试目的，你可以更改的它的全局配置文件。其它情况下，你应该仅仅更改每个你想要重新构建的软件包的PKGBUILD。

### 全局设定

至于pacman 4.1`etc/makepkg.conf`已经在`DEBUG_CFLAGS`和`DEBUG_CXXFLAGS`有编译标志。为了使用它们，开启`debug`makepkg选项并且禁用`strip`。

更改`makepkg`的配置文件`~/.makepkg.conf`使之包含：

```
 OPTIONS+=(debug !strip)

```

这些设定会强迫编译调试信息并禁用剥离(strip)可执行文件。(如果你不禁用`strip`，调试信息也会生成，但是在单独的`"foo"-debug`包中。)

### 仅单个软件包设定

更改`foo`的PKGBUILD文件使之包含以下行：

```
options=(debug !strip)

```

在`build()`函数内，在最开始添加以下行：

```
export CFLAGS="$CFLAGS -g -O1"
export CXXFLAGS="$CXXFLAGS -g -O1"

```

**Note:** 不推荐降低优化级别到 -O1 以下，因为这样 gcc 就会使用和优化版本大相径庭的 GNU C 库函数版本了。而且头文件所包含内容的改变和禁用的函数可能会让编译不通过。

### Qt

除了之前的通用设置，还需要添加`-developer-build`选项到`PKGBUILD`的`configure`脚本中。如果安装了 qtwebkit，编译 Qt 可能会出问题，所以需要先临时删除软件包[qtwebkit](https://www.archlinux.org/packages/?name=qtwebkit)，使用下面的删除命令以忽略依赖检查：

```
# pacman -Rdd qtwebkit

```

编译完 Qt 后再重新安装 qtwebkit。

### KDE应用

KDE 程序使用 cmake 进行编译，要编译进调试信息，请将`-DCMAKE_BUILD_TYPE` 修改为 `Debug`。

## 构建和安装软件包

当在PKGBUILD的文件夹中使用`makepkg`，这可能花费些时间：

```
# makepkg

```

然后安装这个软件包：

```
# pacman -U glibc-2.5-8-i686.pkg.tar.gz

```

## 获得回溯

真正的回溯 (或堆栈回溯)现在可以通过例如GNU调试器[gdb](https://www.archlinux.org/packages/?name=gdb)来获得。 通过以下任一命令运行它：

```
# gdb /path/to/file

```

或：

```
# gdb
(gdb) exec /path/to/file

```

路径是可选的，如果已经在`$PATH`变量中设定过了。

然后在`gdb`中，键入`run`连同以下任何你想要程序运行时的参数，例如：

```
(gdb) run --no-daemon --verbose

```

开始执行这个文件。做任何必要的来激发这个bug。对于实际日志，键入以下行：

```
(gdb) set logging file trace.log
(gdb) set logging on

```

然后：

```
(gdb) bt

```

然后输出回溯到在`gdb`运行的目录中`trace.log`。退出时，键入：

```
(gdb) set logging off
(gdb) quit

```

**Tip:** 调试python写成的应用时：(你得更改python的PKGBUILD重新编译python)

```
# gdb /usr/bin/python
(gdb) run <python application>

```

你也可以调试一个已经运行的程序，例如：

```
 # gdb --pid=$(pidof firefox)
 (gdb) continue

```

## 总结

使用完整的堆栈回溯来告知开发者你之前发现的bug。他们会很感激，并且将帮助你改善你喜爱的程序。

## 参见

*   [Reporting bug guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Gentoo Linux Documentation — How to get meaningful backtraces in Gentoo](http://www.gentoo.org/proj/en/qa/backtraces.xml)