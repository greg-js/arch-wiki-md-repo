**翻译状态：** 本文是英文页面 [P7zip](/index.php/P7zip "P7zip") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-5-17，点击[这里](https://wiki.archlinux.org/index.php?title=P7zip&diff=0&oldid=373802)可以查看翻译后英文页面的改动。

p7zip 是 [7-Zip](https://en.wikipedia.org/wiki/7zip "wikipedia:7zip") 的 [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") 系统移植，支持 Linux.

## Contents

*   [1 安装 & 使用](#安装_&_使用)
*   [2 例程](#例程)
*   [3 在7z， 7za 与 7zr 二进制之间的不同](#在7z，_7za_与_7zr_二进制之间的不同)
*   [4 扩展链接](#扩展链接)

## 安装 & 使用

你可以从[official repositories](/index.php/Official_repositories "Official repositories")中[安装](/index.php/Pacman "Pacman")[p7zip](https://www.archlinux.org/packages/?name=p7zip)的安装包。

运行下面的命令就可以运行该程序：

```
# 7z

```

## 例程

从存档中解压文件，不使用路径则默认解压到当前目录下，运行下面命令：

```
# 7za e <archive name>

```

运行下面的命令你可以解压它并使它包含全部路径：

```
# 7za x <archive name>

```

## 在7z， 7za 与 7zr 二进制之间的不同

安装包包含了三种二进制， `/usr/bin/7z`，`/usr/bin/7za`，和 `/usr/bin/7zr`。 它们的菜单页解释它们的不同之处：:

*   7z 使用插件处理格式文件。
*   7za 是独立可执行的。 7za 可以不需要其它任何插件的处理较少格式而不像 7z。
*   7zr 是独立可执行的。 7zr 可以不需要其它任何插件的处理较少格式而不像 7z。 7zr是一个轻量级的 7za 只用来解压7z 格式的文件。

## 扩展链接

*   [Homepage.](http://p7zip.sourceforge.net/)
*   [7zip homepage.](http://www.7-zip.org/download.html)