**man手册页**（manual pages，“手册”），是类UNIX系统最重要的手册工具。多数类UNIX都预装了它，这也包括Arch。使用man手册页的命令是：`man`。

man手册页被设计成“自足”的文档库，即论述相关问题时无法通过类似超链接的东西引向其他手册页。GNU正努力改变原始的man手册页格式。

## Contents

*   [1 阅读手册页](#.E9.98.85.E8.AF.BB.E6.89.8B.E5.86.8C.E9.A1.B5)
*   [2 格式](#.E6.A0.BC.E5.BC.8F)
*   [3 搜索手册页](#.E6.90.9C.E7.B4.A2.E6.89.8B.E5.86.8C.E9.A1.B5)
*   [4 彩色显示](#.E5.BD.A9.E8.89.B2.E6.98.BE.E7.A4.BA)
    *   [4.1 方法一：使用most](#.E6.96.B9.E6.B3.95.E4.B8.80.EF.BC.9A.E4.BD.BF.E7.94.A8most)
    *   [4.2 方法二：使用less](#.E6.96.B9.E6.B3.95.E4.BA.8C.EF.BC.9A.E4.BD.BF.E7.94.A8less)
*   [5 使用浏览器阅读手册页](#.E4.BD.BF.E7.94.A8.E6.B5.8F.E8.A7.88.E5.99.A8.E9.98.85.E8.AF.BB.E6.89.8B.E5.86.8C.E9.A1.B5)
    *   [5.1 使用本地手册页](#.E4.BD.BF.E7.94.A8.E6.9C.AC.E5.9C.B0.E6.89.8B.E5.86.8C.E9.A1.B5)
    *   [5.2 使用在线手册页](#.E4.BD.BF.E7.94.A8.E5.9C.A8.E7.BA.BF.E6.89.8B.E5.86.8C.E9.A1.B5)

## 阅读手册页

通过以下命令阅读man手册页：

```
$ man _手册名_

```

man手册页分为下面几个部分：

1.  普通命令
2.  内核提供的系统调用
3.  库调用（C库函数）
4.  特殊文件（大多在/dev目录下）和设备
5.  文件格式规范
6.  游戏
7.  杂项（及其规范）
8.  系统管理命令（通常需要root权限）和守护进程

man手册页通过名称和所属分类标识。有些不同分类的man手册页名字可能相同，比如 man(1) 和 man(7)，这时需要额外指明分类以访问需要的手册。例如：

```
$ man 5 passwd

```

会显示有关文件`/etc/passwd`，而非命令 `passwd`，的内容。

通过`whatis`命令，可以只显示需要的man手册页的简要信息。如果只是想获取对命令 ls 的简要说明，使用以下命令：

```
$ whatis ls

```

然后会得到输出：“list directory contents.”（“列目录内容”）。

## 格式

所有man手册页都按照以下标准格式组织：

*   NAME - 手册叙述对象名称，及简要描述。
*   SYNOPSIS - 命令参数格式，或者函数调用格式等。
*   DESCRIPTION - 对叙述对象更加详细的描述。
*   EXAMPLES - 由浅入深的使用示例。
*   OPTIONS - 命令行或者函数调用参数的意义。
*   EXIT STATUS - 不同返回（退出）代码的含义。
*   FILES - 与叙述对象相关的文件。
*   BUGS - 已知的bug。
*   SEE ALSO - 相关内容列表。
*   AUTHOR, HISTORY, COPYRIGHT, LICENSE, WARRANTY - 历史、版权、编者信息。

## 搜索手册页

如果用户压根儿不知道要查阅的手册的名称，该怎么办呢？没事，通过 `-k` 或者 `--apropos` 参数就可以按给定关键词搜索相关手册。例如，要查阅有关密码的手册（“password”）：

关键词搜索特性是从一个专用的缓存生成的。默认情况下你没有这个缓存，所以无论你搜什么，都会提示你_nothing appropriate_。你可以通过下面的命令来生成这个缓存：

```
# mandb

```

每当你安装新的manpage之后都需要运行这个命令，缓存才会更新。

现在你可以开始搜索了。 例如，要查阅有关密码的手册（“password”）：

```
$ man -k password

```

或者：

```
$ man --apropos password

```

还可以直接使用 `apropos` 命令：

```
$ apropos password

```

关键字可以使用正则表达式。

如果你想全文搜索的话，你可以用`-K`选项：

```
$ man -K password

```

## 彩色显示

对很多人来说，彩色手册页比黑白的更加易于大脑消化吸收。

有两种常用的实现man手册页彩色显示的方法：使用 `most` 或 `less` （一“多”一“少”）。前者更加易于配置，但后者功能更强大。

### 方法一：使用most

首先通过[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")安装[most](https://www.archlinux.org/packages/?name=most)：

```
# pacman -S most

```

该工具类似`less`和`more`，支持彩色化文本。

编辑文件`/etc/man_db.conf`，去掉pager项的注释并修改为：

```
DEFINE     pager     most -s

```

然后测试一下吧。

通过修改`~/.mostrc`（不存在的话请自行创建）或全局配置文件可以调整配色。例如：

```
% Color settings
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

以下示例配置`more`的使用类似`less`的快捷键：

```
% less-like keybindings
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

### 方法二：使用less

	<small>_来源： [nion's blog - less colors for man pages](http://nion.modprobe.de/blog/archives/572-less-colors-for-man-pages.html)_</small>

此外，还可以使用`less`彩色输出man手册页。`less`提供更多功能，但需要更复杂的配置，适用于高级用户。

将以下内容加入shell配置文件（如[Bash](/index.php/Bash "Bash")的是`~/.bashrc`）：

```
man() {
	env \
		LESS_TERMCAP_mb=$(printf "\e[1;37m") \
		LESS_TERMCAP_md=$(printf "\e[1;37m") \
		LESS_TERMCAP_me=$(printf "\e[0m") \
		LESS_TERMCAP_se=$(printf "\e[0m") \
		LESS_TERMCAP_so=$(printf "\e[1;47;30m") \
		LESS_TERMCAP_ue=$(printf "\e[0m") \
		LESS_TERMCAP_us=$(printf "\e[0;36m") \
			man "$@"
}
```

要调整颜色，参见：[Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code") for reference.

## 使用浏览器阅读手册页

还可以通过[Lynx](/index.php?title=Lynx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Lynx (简体中文) (page does not exist)")或[Firefox](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)")之类的浏览器阅读man手册页。由于使用浏览器，手册页可以支持超链接。

此外，[KDE](/index.php/KDE "KDE")用户可以直接在Konqueror使用以下地址访问man手册：

```
man:<name>

```

### 使用本地手册页

首先，从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")安装软件包[man2html](https://www.archlinux.org/packages/?name=man2html)。

然后使用它转换man手册页：

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

此外，`man2html`还可以把man页转换为便于打印的文本文件：

```
$ man free | man2html -bare > ~/free.txt

```

Arch提供的man也具有浏览器阅读功能：

```
$ man -H free

```

由`BROWSER`环境变量决定使用的浏览器。也可以使用 `man -Hlynx`（H后无空格）这样的形式手动设置浏览器。

### 使用在线手册页

许多网站提供在线man手册页，详细列表参见：[Wikipedia:Man_page#Repositories_of_manual_pages](https://en.wikipedia.org/wiki/Man_page#Repositories_of_manual_pages "wikipedia:Man page")。

*   [Man7.org.](http://man7.org/linux/man-pages/index.html) Upstream for Arch Linux's [man-pages](https://www.archlinux.org/packages/?name=man-pages).
*   [_Debian GNU/Linux man pages_](http://manpages.debian.net/)
*   [_DragonFlyBSD manual pages_](http://leaf.dragonflybsd.org/cgi/web-man)
*   [_FreeBSD Hypertext Man Pages_](http://www.freebsd.org/cgi/man.cgi)
*   [_Linux and Solaris 10 Man Pages_](http://www.manpages.spotlynx.com/)
*   [_Linux/FreeBSD Man Pages_](http://manpagehelp.net) with user comments
*   [_Linux man pages at die.net_](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [_NetBSD manual pages_](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [_Mac OS X Manual Pages_](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [_On-line UNIX manual pages_](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [_OpenBSD manual pages_](http://www.openbsd.org/cgi-bin/man.cgi)
*   [_Plan 9 Manual — Volume 1_](http://man.cat-v.org/plan_9/)
*   [_Inferno Manual — Volume 1_](http://man.cat-v.org/inferno/)
*   [_Storage Foundation Man Pages_](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [_The Missing Man Project_](http://markhobley.yi.org/manpages/missingman.html) [dead link as of 9 July 2010]
*   [_Gobuntu Manual Pages_](http://en.linuxpages.info/index.php?title=Main_Page) [dead link as of 9 July 2010]
*   [_The UNIX and Linux Forums Man Page Repository_](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [_Ubuntu Manpage Repository_](http://manpages.ubuntu.com/)