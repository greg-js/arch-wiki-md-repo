Related articles

*   [TeX Live FAQ](/index.php/TeX_Live_FAQ "TeX Live FAQ")
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK")
*   [Ooolatex](/index.php/Ooolatex "Ooolatex")
*   [List of applications/Documents#Scientific_documents](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents")

**翻译状态：** 本文是英文页面 [TeXLive](/index.php/TeXLive "TeXLive") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-07，点击[这里](https://wiki.archlinux.org/index.php?title=TeXLive&diff=0&oldid=478813)可以查看翻译后英文页面的改动。

[TeX Live](https://www.tug.org/texlive/)是"安装和运行[TeX](/index.php/Category:TeX "Category:TeX")文档制作系统的简单方式。它提供了一个全面的Tex系统，提供的二进制文件适用于大多数Unix风格操作系统(包括GNU/Linux)的二进制文件，当然也有Windows。它包含了全部主要的Tex相关的属于自由软件的程序，宏包，字体，还有对世界上很多语种的支持。"

Tex Live是[LaTeX](https://en.wikipedia.org/wiki/LaTeX "wikipedia:LaTeX")， [ConTeXt](https://en.wikipedia.org/wiki/ConTeXt "wikipedia:ConTeXt")和其他友商最流行的发行版本之一。

查看[Category:TeX (简体中文)](/index.php/Category:TeX_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:TeX (简体中文)")以获得更多信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 手动安装TeXLive](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85TeXLive)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
    *   [2.1 纸张大小](#.E7.BA.B8.E5.BC.A0.E5.A4.A7.E5.B0.8F)
    *   [2.2 升级时出现 "formats not generated" 错误](#.E5.8D.87.E7.BA.A7.E6.97.B6.E5.87.BA.E7.8E.B0_.22formats_not_generated.22_.E9.94.99.E8.AF.AF)
    *   [2.3 字体](#.E5.AD.97.E4.BD.93)
*   [3 中文化](#.E4.B8.AD.E6.96.87.E5.8C.96)
*   [4 TeXLive Local Manager](#TeXLive_Local_Manager)
*   [5 安装 .sty 文件](#.E5.AE.89.E8.A3.85_.sty_.E6.96.87.E4.BB.B6)
    *   [5.1 手工安装](#.E6.89.8B.E5.B7.A5.E5.AE.89.E8.A3.85)
    *   [5.2 使用 PKGBUILD 安装](#.E4.BD.BF.E7.94.A8_PKGBUILD_.E5.AE.89.E8.A3.85)
*   [6 更新 babelbib 语言定义](#.E6.9B.B4.E6.96.B0_babelbib_.E8.AF.AD.E8.A8.80.E5.AE.9A.E4.B9.89)
*   [7 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

Tex Live 主要在[官方仓库](/index.php/Official_repositories "Official repositories")的两个软件组中:

*   [texlive-most](https://www.archlinux.org/groups/x86_64/texlive-most/) 包括Tex Live应用
*   [texlive-lang](https://www.archlinux.org/groups/x86_64/texlive-lang/) 提供个性化的设置和非英语特性

必要的软件包[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 包含了基本的 texmf-dist 目录树(宏包和字体)，[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 包含二进制文件，库文件，和 texmf 目录树。[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 基于上游发行版的"medium"安装方案。所有其它的包基于TeX Live同名的包。想确定每个包重包含了哪些CTAN包，查看这些文件：

```
  /var/lib/texmf-var/arch/installedpkgs/<package>_<revnr>.pkgs

```

**注意:** [texlive-langextra](https://www.archlinux.org/packages/?name=texlive-langextra) 提供了对 African, Arabic, Armenian, Croatian, Hebrew, Indic, Mongolian, Tibetan 和 Vietnamese 的语言支持.

### 手动安装TeXLive

参见[LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Custom_installation_with_TeX_Live) 和 [TeX Live Guide](https://tug.org/texlive/doc/texlive-en/texlive-en.html#x1-140003). 对于需要Tex Live的程序 (例如 kile) 你可以参考 [texlive-dummy](https://aur.archlinux.org/packages/texlive-dummy/) 包.

## 使用

用下面方法验证安装：

```
$ tex '\empty Hello world!\bye'
$ pdftex '\empty Hello world!\bye'

```

可以分别生成 DVI 和 PDF 文件.

[TeX editor 汇总](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents")了可用的图形界面. 一些在线服务可以不用 TeX Live 就编辑 TeX 文档，请参考[LaTeX wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Online_solutions).

*   处理updmap字体映射的方法已经在2009年6月得到改善，安装应该比过去更加可靠。同时，如果你遇到关于不可用的字体映射文件的错误信息，简单地手工移除 `updmap.cfg` 文件 (最好使用 `updmap-sys --edit`)。你也可以运行 `updmap-sys --syncwithtrees` 自动地注释掉配置文件中的有关map的行。

*   ConTeX格式(MKII和MKIV)不会在安装时自动生成。参见 [**the ConTeXT wiki**](http://wiki.contextgarden.net) 获取更多的指导。

*   包含文档和源码已经从仓库中移除。可以通过 [tllocalmgr](#TeXLive_Local_Manager) 手动编译或在 [http://tug.org/texlive/Contents/live/doc.html](http://tug.org/texlive/Contents/live/doc.html) 或者在 CTAN 上在线查阅。

*   TeX Live (上游) 现在提供了一个升级CTAN中包的工具。在此基础上，我们也计划定期升级我们的包(我们已经写了几乎自动完成这个任务的工具)。

*   有些包含在TeX Live中的工具和实用程序依赖 [ghostscript](https://www.archlinux.org/packages/?name=ghostscript)，[perl](https://www.archlinux.org/packages/?name=perl)，[python2](https://www.archlinux.org/packages/?name=python2) 和 [ruby](https://www.archlinux.org/packages/?name=ruby)。

*   寻求有关TeX Live的支持参见：[http://tug.org/texlive/doc.html](http://tug.org/texlive/doc.html) and [http://tug.org/texlive/doc/texlive-en/texlive-en.html](http://tug.org/texlive/doc/texlive-en/texlive-en.html)

*   系统级的配置文件在 `/usr/share/texmf-config`。单用户的在 `~/.texlive/texmf-config`。`$TEXMFHOME` 是 `~/texmf`、 `$TEXMFVAR` 是 `~/.texlive/texmf-var`。

*   本地目录树在`/usr/local/share/texmf`: 这个文件夹对于 **tex** 组是可写的。

### 纸张大小

要将默认的纸张大小设为 "Letter"，而不是当前的默认值 A4：

```
$ texconfig

```

这个命令也可以更改其他有用的设定。

### 升级时出现 "formats not generated" 错误

参见 [this bug report](https://bugs.archlinux.org/task/16467)。(**如果你没有使用实验性的排版引擎 *LuaTeX*，你可以忽略这个。**) 这种情况通常发生在当`language.def` 且/或 `language.dat` 断句样式包含早期 `texlive-core`的引用时，特别是对文件名频繁变化的最新实验性德语断句样式的引用。现在它们应该指向 `dehyph{n,t}-x-2009-06-19.tex`。

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

另外，[texlive-core](https://www.archlinux.org/packages/?name=texlive-core) 提供的 `/etc/fonts/conf.avail/09-texlive-fonts.conf` 文件包含了TeX Live使用的目录列表。用下面命令使用此文件：

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

[texlive-localmanager-git](https://aur.archlinux.org/packages/texlive-localmanager-git/)提供了一个在 archlinux 上管理 TeXLive 的新工具。详情请参考[用法说明](https://git.archlinux.org/users/remy/texlive-localmanager.git/tree/tllocalmgr#n809)。

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

如果某个 sty 文件仅是给特定用户使用，可以放到 `~/texmf/` 目录。例如 `wrapfig.sty` 文件放到 `~/texmf/tex/latex/wrapfig/wrapfig.sty`. 不需要重新运行 `mktexlsr` 等，因为 tex 每次运行的时候都会搜索 `~/texmf`。

### 手工安装

通常，一个新的.sty文件在`/usr/share/texmf-dist/tex/latex/<package name>/*`中。如果你没有这个目录创建它。这个目录将被自动搜索当 *tex (pdftex/latex/xelatex.....)命令被执行。更多的讨论见这里: [https://bbs.archlinux.org/viewtopic.php?id=85757](https://bbs.archlinux.org/viewtopic.php?id=85757) 。

### 使用 PKGBUILD 安装

在整个系统的层面上安装latex包，出于简化安装和维护的考虑你应该使用 PKGBUILD。[AUR](/index.php/AUR "AUR")中的软件包[texlive-gantt](https://aur.archlinux.org/packages/texlive-gantt/)示例.

## 更新 babelbib 语言定义

如果 babelbib 没有需要的最新语言定义，可以从 [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/) 获取最新定义并放到 `/usr/share/texmf-dist/tex/latex/babelbib/`. 例如：

```
# cd /usr/share/texmf-dist/tex/latex/babelbib/ 
# wget [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/romanian.bdf](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/romanian.bdf)
# wget [...all-other-language-files...]
# wget [https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/babelbib.sty](https://www.tug.org/texlive/devsrc/Master/texmf-dist/tex/latex/babelbib/babelbib.sty)

```

运行 `texhash` 更新 TeX 数据库:

```
# texhash

```

## 更多信息

*   [TeX Live FAQ](/index.php/TeX_Live_FAQ "TeX Live FAQ") - Frequently asked qustions about TeX，TeXLive，and how it is packaged on Arch Linux
*   [LaTeX](/index.php/LaTeX "LaTeX") - Basic information on LaTeX
*   [TeX Live and CJK](/index.php/TeX_Live_and_CJK "TeX Live and CJK") - CJK (Chinese，Japanese，Korean) characters