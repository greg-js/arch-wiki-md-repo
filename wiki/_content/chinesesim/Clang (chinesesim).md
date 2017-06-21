**翻译状态：** 本文是英文页面 [Clang](/index.php/Clang "Clang") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-06-21，点击[这里](https://wiki.archlinux.org/index.php?title=Clang&diff=0&oldid=480131)可以查看翻译后英文页面的改动。

[Clang](http://clang.llvm.org/)*是基于LLVM的C/C++/Objective C编译器。它基于BSD许可证。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 用Clang构建软件包](#.E7.94.A8Clang.E6.9E.84.E5.BB.BA.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [3 使用静态分析工具](#.E4.BD.BF.E7.94.A8.E9.9D.99.E6.80.81.E5.88.86.E6.9E.90.E5.B7.A5.E5.85.B7)
*   [4 参考](#.E5.8F.82.E8.80.83)

## 安装

从 [Official repositories](/index.php/Official_repositories "Official repositories") 安装 [clang](https://www.archlinux.org/packages/?name=clang)。

## 用Clang构建软件包

在 `/etc/makepkg.conf` 中添加 `export CC=clang` 和 (for C++) `export CXX=clang++` 。如果您正在使用 `debug` 构建，还可以从 `DEBUG_CFLAGS` 和 `DEBUG_CXXFLAGS` 中删除 `-fvar-tracking-assignments` 因为clang 不支持它。

注意：对于指定GCC特定构建选项的软件包，可能存在需要编辑源软件包，pkgbuild或注释掉makepkg.conf.pport中的clang行的构建错误。

## 使用静态分析工具

要分析项目，只需在构建命令的前面放置 `scan-build`。 例如：

```
$ scan-build make

```

**Tip:** 如果您的项目已经被编译， `scan-build`将不会重建，也不会对其进行分析。要强制重新编译和分析，请使用 `-B`开关： `$ scan-build make -B` 

也可以分析具体文件：

```
$ scan-build gcc -c t1.c t2.c

```

## 参考

*   [scan-build: running the analyzer from the command line](http://clang-analyzer.llvm.org/scan-build.html)