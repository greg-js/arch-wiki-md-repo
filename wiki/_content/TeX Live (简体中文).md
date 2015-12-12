# TeX Live (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**翻译状态：** 本文是英文页面 [TeXLive](/index.php/TeXLive "TeXLive") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-04-08，点击[这里](https://wiki.archlinux.org/index.php?title=TeXLive&diff=0&oldid=251936)可以查看翻译后英文页面的改动。

[TeX Live](http://www.tug.org/texlive/)是"研究和运行[TeX](/index.php/Category:TeX "Category:TeX")文档制作系统的简单方式。它提供了一个全面的Tex系统和针对充满Unix味道的操作系统(包括GNU/Linux)的二进制文件，当然也有Windows版本。它包含了全部主要的Tex相关的程序，宏包，自由软件字体，还有对世界上很多语种的支持。"

查看[Category:TeX (简体中文)](/index.php/Category:TeX_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:TeX (简体中文)")以获得更多信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 texlive-most](#texlive-most)
    *   [1.2 texlive-lang](#texlive-lang)
    *   [1.3 另一种方法：网络安装TeXLive](#.E5.8F.A6.E4.B8.80.E7.A7.8D.E6.96.B9.E6.B3.95.EF.BC.9A.E7.BD.91.E7.BB.9C.E5.AE.89.E8.A3.85TeXLive)
*   [2 重要信息](#.E9.87.8D.E8.A6.81.E4.BF.A1.E6.81.AF)
    *   [2.1 纸张大小](#.E7.BA.B8.E5.BC.A0.E5.A4.A7.E5.B0.8F)
    *   [2.2 升级时出现 "formats not generated" 错误](#.E5.8D.87.E7.BA.A7.E6.97.B6.E5.87.BA.E7.8E.B0_.22formats_not_generated.22_.E9.94.99.E8.AF.AF)
    *   [2.3 字体](#.E5.AD.97.E4.BD.93)
*   [3 中文化](#.E4.B8.AD.E6.96.87.E5.8C.96)
*   [4 TeXLive Local Manager](#TeXLive_Local_Manager)
    *   [4.1 "langukenglish" 错误](#.22langukenglish.22_.E9.94.99.E8.AF.AF)
*   [5 安装 .sty 文件](#.E5.AE.89.E8.A3.85_.sty_.E6.96.87.E4.BB.B6)
    *   [5.1 手工安装.sty文件](#.E6.89.8B.E5.B7.A5.E5.AE.89.E8.A3.85.sty.E6.96.87.E4.BB.B6)
    *   [5.2 使用PKGBUILD安装 .sty](#.E4.BD.BF.E7.94.A8PKGBUILD.E5.AE.89.E8.A3.85_.sty)
*   [6 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

Tex Live宏包主要在[官方仓库](/index.php/Official_repositories "Official repositories")的两个软件包中:

*   [texlive-most](https://www.archlinux.org/groups/x86_64/texlive-most/) 包括Tex Live应用
*   [texlive-lang](https://www.archlinux.org/groups/x86_64/texlive-lang/) 提供个性化的设置和非英语特性

必要的软件包[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 包含了基本的 texmf-dist 目录树(宏包和字体)，[texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin) 包含二进制文件，库文件，和 texmf 目录树(核心部件)。[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 基于在TexLive DVD中 “中等的” 安装。其它的包基于TeX Live中齐名的宏包。去了解没个软件包中包含CTAN中哪些宏包，查看这些文件：

```
  /var/lib/texmf-var/arch/installedpkgs/<package>_<revnr>.pkgs

```

### texlive-most

<table width="100%">

<tbody>

<tr valign="top">

<td>

*   [texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin)
*   [texlive-core](https://www.archlinux.org/packages/?name=texlive-core)
*   [texlive-bibtexextra](https://www.archlinux.org/packages/?name=texlive-bibtexextra)
*   [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra)
*   [texlive-formatsextra](https://www.archlinux.org/packages/?name=texlive-formatsextra)
*   [texlive-games](https://www.archlinux.org/packages/?name=texlive-games)

</td>

<td>

*   [texlive-genericextra](https://www.archlinux.org/packages/?name=texlive-genericextra)
*   [texlive-htmlxml](https://www.archlinux.org/packages/?name=texlive-htmlxml)
*   [texlive-humanities](https://www.archlinux.org/packages/?name=texlive-humanities)
*   [texlive-latexextra](https://www.archlinux.org/packages/?name=texlive-latexextra)
*   [texlive-music](https://www.archlinux.org/packages/?name=texlive-music)

</td>

<td>

*   [texlive-pictures](https://www.archlinux.org/packages/?name=texlive-pictures)
*   [texlive-plainextra](https://www.archlinux.org/packages/?name=texlive-plainextra)
*   [texlive-pstricks](https://www.archlinux.org/packages/?name=texlive-pstricks)
*   [texlive-publishers](https://www.archlinux.org/packages/?name=texlive-publishers)
*   [texlive-science](https://www.archlinux.org/packages/?name=texlive-science)

</td>

</tr>

</tbody>

</table>

### texlive-lang

*   [texlive-langcjk](https://www.archlinux.org/packages/?name=texlive-langcjk)
*   [texlive-langcyrillic](https://www.archlinux.org/packages/?name=texlive-langcyrillic)
*   [texlive-langgreek](https://www.archlinux.org/packages/?name=texlive-langgreek)
*   [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra)

**注意:** `texlive-langextra` 取代了 African，Arab，Armenian，Croatian，Hebrew，Indic，Mongolian，Tibetan 和 Vietnamese 软件包.

### 另一种方法：网络安装TeXLive

手动安装Tex Live使用Arch的方式因此给你更多的控制并能让你更好的理解过程。这是唯一的能获取不到100MB适合你需要的全功能LaTeX套件的方式，而不用安装成百上千的你从不会用上的包。

这里可以找到一份详细的TeX Live网络安装指导[[http://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live](http://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live) LaTeX Wikibook].

有关网络安装的更多信息参见：[http://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003](http://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003)

这里有一个关于网络安装优缺点的 [讨论](https://bbs.archlinux.org/viewtopic.php?id=109427).

其它依赖texlive的程序如kile现在可以从源里获得。

## 重要信息

*   处理updmap字体映射的方法已经在2009年6月得到改善，安装应该比过去更加可靠。同时，如果你遇到关于不可用的字体映射文件的错误信息，简单地手工移除 `updmap.cfg` 文件 (最好使用 `updmap-sys --edit`)。你也可以运行 `updmap-sys --syncwithtrees` 自动地注释掉配置文件中的有关map的行。

*   ConTeX格式(MKII和MKIV)不会在安装时自动生成。参见 [**the ConTeXT wiki**](http://wiki.contextgarden.net) 获取更多的指导。

*   包含文档和源码的包在 [community] 仓库中。你也可以在 [http://tug.org/texlive/Contents/live/doc.html](http://tug.org/texlive/Contents/live/doc.html) 或者在 CTAN 上在线查阅。

*   TeX Live (上游) 现在提供了一个升级CTAN中包的工具。在此基础上，我们也计划定期升级我们的包(我们已经写了几乎自动完成这个任务的工具)。

*   有些包含在TeX Live中的工具和实用程序依赖 [ghostscript](https://www.archlinux.org/packages/?name=ghostscript)，[perl](https://www.archlinux.org/packages/?name=perl)，and [ruby](https://www.archlinux.org/packages/?name=ruby)。

*   寻求有关TeX Live的支持参见：[http://tug.org/texlive/doc.html](http://tug.org/texlive/doc.html) and [http://tug.org/texlive/doc/texlive-en/texlive-en.html](http://tug.org/texlive/doc/texlive-en/texlive-en.html)

*   系统级的配置文件在 `/usr/share/texmf-config`。单用户的在 `~/.texlive/texmf-config`。`$TEXMFHOME` 是 `~/texmf`、 `$TEXMFVAR` 是 `~/.texlive/texmf-var`。

*   本地目录树在`/usr/local/share/texmf`: 这个文件夹对于 **tex** 组是可写的。

### 纸张大小

美国用户建议运行

```
$ texconfig

```

将默认的纸张大小设为 "Letter"，而不是当前的默认值 A4。这个命令也可以更改其他有用的设定。不更改这个设定右边距将大于左边距，可能造成略有瑕疵的输出。

### 升级时出现 "formats not generated" 错误

参见 [this bug report](https://bugs.archlinux.org/task/16467)。(**如果你没有使用实验性的排版引擎 _LuaTeX_，你可以忽略这个。**) 这种情况通常发生在当`language.def` 且/或 `language.dat` 断句样式包含早期 `texlive-core`的引用时，特别是对文件名频繁变化的最新实验性德语断句样式的引用。现在它们应该指向 `dehyph{n,t}-x-2009-06-19.tex`。

解决这个问题，你或者删除这些文件: `/usr/share/texmf-config/tex/generic/config/language.{def,dat}` 或者升级它们使用最新版本： `/usr/share/texmf/tex/generic/config/language.{def,dat}` 然后运行：

```
# fmtutil-sys --missing

```

### 字体

默认情况下不自动提供给Fontconfig随各种Tex Live包提供的字体。如果你想让比如 XeTeX 或者 [LibreOffice](/index.php/LibreOffice "LibreOffice")使用它们，最简单的方法是做如下符号链接：

```
 ln -s /usr/share/texmf-dist/fonts/opentype/public/<some_fonts_you_want> ~/.fonts/OTF/ (or TTF or Type1) 

```

将它们提供给fontconfig(就是让这些字体可以被TeX使用--edit)，运行：

```
 fc-cache ~/.fonts
 mkfontscale ~/.fonts/OTF (or TTF or Type1) 
 mkfontdir ~/.fonts/OTF (or TTF or Type1)

```

另外，[texlive-bin](https://www.archlinux.org/packages/?name=texlive-bin) 提供的 `/etc/fonts/conf.avail/09-texlive-fonts.conf` 文件包含了TeX Live使用的目录列表。用下面命令使用此文件：

 `# ln -s /etc/fonts/conf.avail/09-texlive-fonts.conf /etc/fonts/conf.d/09-texlive-fonts.conf` 

然后更新 fontconfig:

 `# fc-cache && mkfontscale && mkfontdir` 

**注意:** 这个可能会和XeTeX/XeLaTeX冲突，如果同样的字体分别对所有TeX和Fontconfig都能用。例如，如果一个字体的多个拷贝出现在搜索路径中。

## 中文化

推荐使用ctex来解决中文化问题。可以在.tex文件中这样：

```
   \documentclass{article}
   \usepackage{ctex}
   \begin{document}
   中文宏包测试
   \end{document}

```

或者这样：

```
   \documentclass{ctexart}
   \begin{document}
   中文宏包测试
   \end{document}

```

CTeX宏包现在已经在texlive2011中，确保安装需要的中文字体如楷体、宋体、仿宋、隶书、幼圆。因为仿宋和幼圆的字体名称在不同系统可能不同，开发者并没有设置默认字体。需要手动更改:

```
   /usr/share/texmf-dist/tex/latex/ctex/fontset/ctex-xecjk-winfonts.def

```

**Note:** 要参照系统中安装字体的名字来修改，特别注意楷体和仿宋

**可以参考以下步骤：**

1\. 首先查看系统中已安装楷体的名称（注意Kai第一个字母大写）：

```
   fc-list |grep Kai

```

这时假定你得到如下结果：

```
   楷体_GB2312,KaiTi_GB2312:style=Regular

```

记住KaiTi_GB2312这个名字

2\. 然后用编辑器打开配置文件：

```
   sudo vim /usr/share/texmf-dist/tex/latex/ctex/fontset/ctex-xecjk-winfonts.def

```

3\. 找到所有`[SIMKAI.TTF]`改成KaiTi_GB2312.(把中括号去掉）

仿宋按同样方法处理。

熟练的用户可以自己设置字体,更多用法请参照ctex文档。 也可以使用Xelatex，详情请参见文档。

## TeXLive Local Manager

现在有一个Firmicus提供的用来方便在archlinux上管理TeXLive的新工具。 参见 [AUR](/index.php/Arch_User_Repository "Arch User Repository") 中的 [texlive-localmanager-git](https://aur.archlinux.org/packages/texlive-localmanager-git/)<sup><small>AUR</small></sup>。

```
Usage: tllocalmgr  
       tllocalmgr [options] [command] [args]

       Running tllocalmgr alone starts the TeXLive local manager shell 
       for Arch Linux。This shell is capable of command-line completion!
       There you can look at the available updates with the command 'status' 
       and you can install individual CTAN packages using 'install' or 'update'
       under $TEXMFLOCAL。This is done by creating a package texlive-local-<pkg>
       and installing it with pacman。Note that this won’t interfere with your 
       standard texlive installation，but files under $TEXMFLOCAL will take
       precedence。 

       Here are the commands available in the shell:

Commands:       
              status   --   Current status of TeXLive installation
           shortinfo * --   Print a one-liner description of CTAN packages
                info * --   Print info on CTAN packages
              update * --   Locally update CTAN packages
             install * --   Locally install new CTAN packages
          installdoc * --   Locally install documentation of CTAN packages
          installsrc * --   Locally install sources of CTAN packages
           listfiles * --   List all files in CTAN packages
              search * --   Search info on CTAN packages
         searchfiles * --   Search for files in CTAN packages
             texhash   --   Refresh the TeX file database
               clean   --   Clean local build tree
                help   --   Print helpful information
                quit   --   Quit tllocalmgr

        The commands followed by * take one of more package names as arguments.
        Note that these can be completed automatically by pressing TAB.

        You can also run tllocalmgr as a standard command-line program，with
        one of the above commands as argument，then the corresponding task will
        be performed and the program will exit (except when the command is 'status').

        tllocalmgr accepts the following options:

Options:     --help          Shows this help
             --version       Show the version number
             --forceupdate   Force updating the TeXLive database
             --skipupdate    Skip updating the TeXLive database
             --localsearch   Search only installed packages
             --location      #TODO?
             --mirror        CTAN mirror to use (default is mirror.ctan.org)
             --nocolor       #TODO

```

### "langukenglish" 错误

当运行`tllocalmgr` 命令遇到以下问题,

```
Cannot get object for collection-langukenglish at /usr/bin/tllocalmgr line 103

```

参见 ary0在aur的解决方案: [texlive-localmanager](https://aur.archlinux.org/packages/texlive-localmanager/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/texlive-localmanager)]</sup>。总之，编辑 `/usr/share/texmf-var/arch/tlpkg/TeXLive/Arch.pm` 并且将 "langukenglish" 从显示的部分移除:

```
my @core_colls =
qw/ basic context genericrecommended fontsrecommended langczechslovak
langdutch langfrench langgerman langitalian langpolish langportuguese
langspanish **langukenglish** latex latexrecommended luatex mathextra metapost
texinfo xetex /;

```

## 安装 .sty 文件

TeX Live (和teTeX) 使用自己的目录索引(文件名为 `ls-R`)，复制文件到 Tex 树后需要刷新索引，否则会找不到它们。命令是：

```
mktexlsr

```

或

```
texhash

```

或

```
texconfig[-sys] rehash

```

搜索索引的命令是：

```
kpsewhich

```

可以通过如下命令检查 TeX 能否找到某个文件：

```
kpsewhich <filename>

```

若能找到，会输出文件的完整路径。

### 手工安装.sty文件

通常，一个新的.sty文件在`/usr/share/texmf-dist/tex/latex/<package name>/*`中。如果你没有这个目录创建它。这个目录将被自动搜索当 *tex (pdftex/latex/xelatex.....)命令被执行。更多的讨论见这里: [https://bbs.archlinux.org/viewtopic.php?id=85757](https://bbs.archlinux.org/viewtopic.php?id=85757) 。

### 使用PKGBUILD安装 .sty

在整个系统的层面上安装latex包，出于简化安装和维护的考虑你应该使用PKGBUILD。看这个例子：

```
# Original autor: Martin Kumm <pluto@ls68.de> 
# Maintainer: masterkorp  <masterkorp@gmail.com>    irc: masterkorp at freenode.org
# Last edited: 2nd April 2011

pkgname=texlive-gantt
pkgver=1.3
pkgrel=1
license=('GPL')
depends=('texlive-core')
pkgdesc="A LaTeX package for drawing gantt plots using pgf/tikz"
url="[http://www.martin-kumm.de/tex_gantt_package.php](http://www.martin-kumm.de/tex_gantt_package.php)"
arch=('any')
install=texlive-gantt.install
source=([http://www.martin-kumm.de/tex/gantt.sty](http://www.martin-kumm.de/tex/gantt.sty))
md5sums=('e942191eb0024633155aa3188b4bbc06')

build()
{
	mkdir -p $pkgdir/usr/share/texmf/tex/latex/gantt
	cp $srcdir/gantt.sty $pkgdir/usr/share/texmf/tex/latex/gantt
}
```

这是 .install 文件:

```
post_install() {
  post_remove
  echo "The file was installed in:"
  kpsewhich gantt.sty
}

post_upgrade() {
  post_install
}

post_remove() {
  echo "Upgrading package database..."
  mktexlsr
}

```

来自[AUR](/index.php/AUR "AUR")软件包[texlive-gantt](https://aur.archlinux.org/packages/texlive-gantt/)<sup><small>AUR</small></sup>.

## 更多信息

*   [TeX Live FAQ](/index.php/TeX_Live_FAQ "TeX Live FAQ") - Frequently asked qustions about TeX，TeXLive，and how it is packaged on Arch Linux
*   [LaTeX](/index.php/LaTeX "LaTeX") - Basic information on LaTeX
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK") - CJK (Chinese，Japanese，Korean) characters

Retrieved from "[https://wiki.archlinux.org/index.php?title=TeX_Live_(简体中文)&oldid=411630](https://wiki.archlinux.org/index.php?title=TeX_Live_(简体中文)&oldid=411630)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [TeX (简体中文)](/index.php/Category:TeX_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:TeX (简体中文)")
*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")