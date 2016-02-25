**翻译状态：** 本文是英文页面 [Vim](/index.php/Vim "Vim") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-24，点击[这里](https://wiki.archlinux.org/index.php?title=Vim&diff=0&oldid=420839)可以查看翻译后英文页面的改动。

[Vim](https://en.wikipedia.org/wiki/Vim_(text_editor) "wikipedia:Vim (text editor)")是[终端](https://en.wikipedia.org/wiki/Computer_terminal#Text_terminals "wikipedia:Computer terminal")文本编辑器[Vi](https://en.wikipedia.org/wiki/Vi "wikipedia:Vi")的加强版本,加入了更多特性来帮助编辑源代码。Vim的一部分增强功能包括文件比较（vimdiff），语法高亮，全面的帮助系统，本地脚本（vimscript），和便于选择的可视化模式。

Vim专注于键盘操作，它并不是像nano或pico一样的简单编辑器。Vim需要花时间来学习，并值得花上更多的时间来掌握。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 用法](#.E7.94.A8.E6.B3.95)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 语法高亮](#.E8.AF.AD.E6.B3.95.E9.AB.98.E4.BA.AE)
    *   [3.2 自动换行显示](#.E8.87.AA.E5.8A.A8.E6.8D.A2.E8.A1.8C.E6.98.BE.E7.A4.BA)
    *   [3.3 使用鼠标](#.E4.BD.BF.E7.94.A8.E9.BC.A0.E6.A0.87)
    *   [3.4 跨行移动光标](#.E8.B7.A8.E8.A1.8C.E7.A7.BB.E5.8A.A8.E5.85.89.E6.A0.87)
*   [4 文件合并](#.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6)
*   [5 技巧和建议](#.E6.8A.80.E5.B7.A7.E5.92.8C.E5.BB.BA.E8.AE.AE)
    *   [5.1 显示行号](#.E6.98.BE.E7.A4.BA.E8.A1.8C.E5.8F.B7)
    *   [5.2 拼写检查](#.E6.8B.BC.E5.86.99.E6.A3.80.E6.9F.A5)
    *   [5.3 记录光标位置](#.E8.AE.B0.E5.BD.95.E5.85.89.E6.A0.87.E4.BD.8D.E7.BD.AE)
    *   [5.4 用 vim 替代 vi](#.E7.94.A8_vim_.E6.9B.BF.E4.BB.A3_vi)
    *   [5.5 DOS/Windows回车问题](#DOS.2FWindows.E5.9B.9E.E8.BD.A6.E9.97.AE.E9.A2.98)
    *   [5.6 gVim窗口底部的空格](#gVim.E7.AA.97.E5.8F.A3.E5.BA.95.E9.83.A8.E7.9A.84.E7.A9.BA.E6.A0.BC)
*   [6 插件](#.E6.8F.92.E4.BB.B6)
    *   [6.1 安装](#.E5.AE.89.E8.A3.85_2)
        *   [6.1.1 使用插件管理器](#.E4.BD.BF.E7.94.A8.E6.8F.92.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [6.1.2 从Arch软件库下载](#.E4.BB.8EArch.E8.BD.AF.E4.BB.B6.E5.BA.93.E4.B8.8B.E8.BD.BD)
    *   [6.2 cscope](#cscope)
        *   [6.2.1 Taglist](#Taglist)
*   [7 参阅](#.E5.8F.82.E9.98.85)
    *   [7.1 官方资源](#.E5.AE.98.E6.96.B9.E8.B5.84.E6.BA.90)
    *   [7.2 教程](#.E6.95.99.E7.A8.8B)
        *   [7.2.1 视频](#.E8.A7.86.E9.A2.91)
        *   [7.2.2 游戏](#.E6.B8.B8.E6.88.8F)
    *   [7.3 配置范例](#.E9.85.8D.E7.BD.AE.E8.8C.83.E4.BE.8B)
        *   [7.3.1 颜色方案](#.E9.A2.9C.E8.89.B2.E6.96.B9.E6.A1.88)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")下面两个软件包中的一个：

*   [vim](https://www.archlinux.org/packages/?name=vim) — 提供Python 2/3, Lua, Ruby 和 Perl 解释器支持，但没有 GTK/X 支持
*   [gvim](https://www.archlinux.org/packages/?name=gvim) — 除了提供和`vim`一样的功能外，还提供了图像界面。

**注意:**

*   [vim](https://www.archlinux.org/packages/?name=vim)包不包含 [Xorg](/index.php/Xorg "Xorg") 支持。因此Vim缺失了 `+clipboard` 特性，Vim也就不能够同X11的 *primary* 和 *clipboard* [剪切板](/index.php/Clipboard "Clipboard")交互。[gvim](https://www.archlinux.org/packages/?name=gvim)包在全面支持图形界面的同时提供了命令行版本带`+clipboard`的Vim。
*   非官方源[herecura](/index.php/Unofficial_user_repositories#herecura "Unofficial user repositories")也提供大量Vim/gVim变种版本: `vim-cli` `vim-gvim-common` `vim-gvim-gtk` `vim-gvim-qt` `vim-rt` 和 `vim-tiny`。

## 用法

要学习一些基本的Vim使用操作，可以运行**vimtutor**（控制台版本）或**gvimtutor**（图形界面版本）阅读Vim教程。

Vim包含了一个广泛的帮助系统，可以用`:h *subject*`命令来访问。*subject*主题可以是命令，配置选项，热键绑定，插件等。使用`:h`命令（不带任何*subject*）来获取帮助系统的相关信息以及在不同的主题之间切换。

## 配置

用户配置文件为`~/.vimrc`，相关的文件位于`~/.vim/`；全局配置文件为`/etc/vimrc`，相关的文件位于`/usr/share/vim/`。

如果需要常用的功能（如语法高亮、打开文件时回到上一次的光标位置等），将配置文件范例加到`/etc/vimrc`中：

 `/etc/vimrc/` 
```
...
runtime! vimrc_example.vim

```

### 语法高亮

启用语法高亮（Vim支持许多语言的语法高亮）：

```
:filetype plugin on
:syntax on

```

### 自动换行显示

`wrap`默认是开启的，这会使Vim在一行文本的长度超过窗口宽度时，自动将放不下的文本显示到下一行。`wrap`只会影响文本的显示，文本本身不会被改变。

自动换行显示一般在该行窗口能容纳下的最后一个字符发生，即使刚好是在一个单词的中间。更为智能的自动换行显示可以用`linebreak`来控制。当用`set linebreak`开启时，自动换行发生在字符串选项`breakat`中列出来的字符之后。默认情况下，`breakat`包含空格和一些标点符号（参考`:help breakat`）。

被换行的字符一般在下一行的开头开始显示，没有任何相应的缩进。[breakindent](https://retracile.net/wiki/VimBreakIndent) 指示Vim在换行时将缩进考虑在内，因而新行将与原本要显示的文本有相同的缩进。`breakindent`行为可以用`breakindentopt`选项来调整，比如说在Python文件中，新行将在原本缩进的基础上再缩进4个空格（更多细节参考`:help breakindentopt`）：

```
autocmd FileType python set breakindentopt=shift:4

```

### 使用鼠标

Vim可以使用鼠标，但只在一些终端上起作用（Linux上的[xterm](/index.php/Xterm "Xterm")和带有[gpm](https://www.archlinux.org/packages/?name=gpm)的Linux控制台，更多细节参阅[Console mouse support](/index.php/Console_mouse_support "Console mouse support")）：

开启这个功能，将下面这行代码加入`~/.vimrc`中：

```
set mouse=a

```

**注意:**

*   这个方法在使用SSH的PuTTY中同样适用。
*   在PuTTY中，通常的高亮/复制行为有所不同，因为在使用鼠标时，Vim会进入可视模式。为了用能鼠标选中文本，需要同时按住`Shift`键。

### 跨行移动光标

默认情况下，在行首按`←`或者在行尾按`→`不能将光标移动至上一行或下一行。

如要改变默认行为，将`set whichwrap=b,s,<,>,[,]`加至你的`~/.vimrc`文件中。

## 文件合并

Vim自带了一个文件差异编辑器（一个用来显示多个文件之间的差异还可以方便的将其合并的程序）。用*vimdiff*来启动它——指定几对文件即可：`vimdiff *file1* *file2*`。以下是*vimdiff*-specific命令的清单。

| 行为 | 快捷键 |
| 下一差异 | `]c` |
| 上一差异 | `[c` |
| 差异导入 | `do` |
| 差异导出 | `dp` |
| 打开折叠 | `zo` |
| 关闭折叠 | `zc` |
| 重新扫描文件 | `:diffupdate` |
| 窗口切换 | `Ctrl+w+w` |

## 技巧和建议

### 显示行号

使用`:set number`来显示行号。默认显示绝对行号，可用`:set relativenumber`开启相对行号。

使用`:*行号*` or `*行号*gg`跳转到指定行号。跳转都记录在一个跳转列表中,更多细节参考`:h jump-motions`。

### 拼写检查

Vim有拼写检查的功能，用下面的命令开启：

```
set spell

```

Vim默认只安装了英语字典。其他的字典可在[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")通过搜索`vim-spell`而寻得。检查可用语言包：

```
# pacman -Ss vim-spell

```

额外的字典可以从[Vim's FTP archive](http://ftp.vim.org/vim/runtime/spell/)获取。把下载的字典文件存入`~/.vim/spell/`，并用 `:setlocal spell spelllang=*en_us*` (将`*en_us*` 换成所需的字典的名称)开启。

| 行为 | 快捷键 |
| 下一个拼写错误 | `]s` |
| 上一个拼写错误 | `[s` |
| 拼写纠正建议 | `z=` |
| 将单词添加到用户正确字典 | `zg` |
| 将单词添加到内部正确字典 | `zG` |
| 将单词添加到用户错误字典 | `zw` |
| 将单词添加到内部正确字典 | `zW` |
| 重新进行拼写检查 | `:spellr` |

**小贴士:**

*   如果需要针对两种语言进行拼写检察（例如英语与德语），在`~/.vimrc`或`/etc/vimrc`中添加`set spelllang=*en,de*`并重启Vim即可。
*   使用用于进行文件类型检测的FileType插件和自建规则，可以对任意文件类型开启拼写检查。例如，要开启对扩展名为`.txt`的文件的拼写检查，创建文件`/usr/share/vim/vimfiles/ftdetect/plaintext.vim`，添加内容`autocmd BufRead,BufNewFile *.txt setfiletype plaintext`，然后在`~/.vimrc`或`/etc/vimrc`添加`autocmd FileType plaintext setlocal spell spelllang=en_us`，重启vim即可。
*   如果想只对LaTeX（或TeX）文档起用拼写检查，在`~/.vimrc`或`/etc/vimrc`添加`autocmd FileType **tex** setlocal spell spelllang=*en_us*`，重启Vim即可。至于非英语语言，替换上述语句中的`en_us`为相应语言代码即可。

### 记录光标位置

Vim可以记录上次打开某一文件时的光标位置，并在下次打开同一文件时将光标移动到该位置。要开启该功能，在配置文件`~/.vimrc`中加入以下内容：

```
augroup resCur
  autocmd!
  autocmd BufReadPost * call setpos(".", getpos("'\""))
augroup END

```

另见：[Vim Wiki上的相关内容](http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session)。

### 用 vim 替代 vi

创建一个[alias](/index.php/Alias "Alias")，如下：

 `alias vi=vim` 

或者,如果你想输入`sudo vi`并得到`vim`, 安装[vi-vim-symlink](https://aur.archlinux.org/packages/vi-vim-symlink/)，它将移除`vi`并用一个符号链接`vim`代替。

### DOS/Windows回车问题

打开MS-DOS或Windows下创建的文本文件时，经常会在每行行末出现一个`^M`。这是因为Linux使用Unix风格的换行，用一个换行符（LF）来表示一行的结束，但在Windows、MS-DOS中使用一个回车符（CR）接一个换行符（LF）来表示，因而回车符就显示为`^M`。

可使用下面的命令删除文件中的回车符：

```
:%s/^M//g

```

注意，`^`代表控制字符。输入`^M`的方法是按下`Ctrl+v,Ctrl+m`。

另一个解决方法是，安装 [dos2unix](https://www.archlinux.org/packages/?name=dos2unix)，然后执行 `dos2unix <文件名>`。

### gVim窗口底部的空格

如果[窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")设置为忽略窗口大小渲染窗口，gVim会将空白区域填充为GTK主题背景色，看起来会比较难看。

解决方案是调整gVim在窗口底部保留的空间大小。将下面的代码加入 `~/.vimrc`中：

```
set guiheadroom=0

```

**注意:** 如果将其设为0，将无法看到底部的水平滚动条。

## 插件

使用插件来提高效率，它能改变Vim的界面，添加新命令，代码自动补全，整合其他程序和工具，添加其他编程语言等功能。

**小贴士:** 参阅[Vim Awesome](http://vimawesome.com/)获取一些热门插件

### 安装

#### 使用插件管理器

插件管理器使安装和管理插件有相似的方法，而与在何种平台上运行Vim无关。它是一个像包管理器一样的用来管理其它Vim插件的插件。

*   [Vundle](https://github.com/gmarik/Vundle.vim)是现在最流行的Vim插件管理器。
*   [Vim-plug](https://github.com/junegunn/vim-plug)是一个极简的Vim插件管理器，有许多的特性，比如按需插件加载和并行升级。
*   [pathogen.vim](https://github.com/tpope/vim-pathogen)是一个简单的用于管理Vim的运行时路径的插件。

#### 从Arch软件库下载

[vim-plugins](https://www.archlinux.org/groups/x86_64/vim-plugins/)分类下有许多插件。 使用`pacman -Sg vim-plugins`来列出可用的插件，然后你可用pacman[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")。

```
pacman -Ss vim-plugins

```

### cscope

[Cscope](http://cscope.sourceforge.net/)是一个工程浏览工具。通过导航到一个词/符号/函数并通过快捷键调用cscope，能快速找到：函数调用及函数定义等。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[cscope](https://www.archlinux.org/packages/?name=cscope)包。

拷贝cscope预设文件，该文件会被Vim自动读为:

```
mkdir -p ~/.vim/plugin
wget -P ~/.vim/plugin [http://cscope.sourceforge.net/cscope_maps.vim](http://cscope.sourceforge.net/cscope_maps.vim) 

```

**注意:** 在Vim的7.x版本中，你可能需要在`~/.vim/plugin/cscope_maps.vim`中取消下列行的注释来启用cscope快捷键：
```
set timeoutlen=4000
set ttimeout
```

创建一个文件，该文件包含了你希望cscope索引的文件的清单（cscope可以操作很多语言，下面的例子用于寻找C++中的*.c*、*.cpp*和*.h*文件）：

```
cd */path/to/projectfolder/*
find . -type f -print | grep -E '\.(c(pp)?|h)$' > cscope.files

```

创建cscope将读取的数据文件：

```
cscope -bq

```

**注意:** 必须从当前路径浏览工程文件，也可以设置`$CSCOPE_DB`变量指向`cscope.out`文件，并导出。

默认快捷键：

```
 Ctrl-\ and
      c: Find functions calling this function
      d: Find functions called by this function
      e: Find this egrep pattern
      f: Find this file
      g: Find this definition
      i: Find files #including this file
      s: Find this C symbol
      t: Find assignments to

```

可随意改变这些快捷键。

#### Taglist

[Taglist](http://vim-taglist.sourceforge.net/)提供源码文件的结构概览，使你能更高效的浏览不同语言的源文件。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[vim-taglist](https://www.archlinux.org/packages/?name=vim-taglist)包。

将下列设置添入文件`~/.vimrc`:

```
let Tlist_Compact_Format = 1
let Tlist_GainFocus_On_ToggleOpen = 1
let Tlist_Close_On_Select = 1
nnoremap <C-l> :TlistToggle<CR>

```

## 参阅

### 官方资源

*   [Vim主页](http://www.vim.org/)
*   [Vim文档](http://vimdoc.sourceforge.net/)
*   [Vim Wiki](http://vim.wikia.com)
*   [Vim脚本](http://www.vim.org/scripts/)

### 教程

*   [中文版《A Byte of Vim》](http://www.swaroopch.com/notes/Vim_zh-cn)
*   [vi教程和参考指南](http://usalug.org/vi.html)
*   [vim Tutorial and Primer](http://www.danielmiessler.com/study/vim/)
*   [vi Tutorial and Reference Guide](http://usalug.org/vi.html)
*   [Graphical vi-Vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
*   [Vim Introduction and Tutorial](http://blog.interlinked.org/tutorials/vim_tutorial.html)
*   [Open Vim](http://www.openvim.com/) - Vim教学工具集合
*   [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
*   [Learning Vim in 2014](http://benmccormick.org/learning-vim-in-2014/)
*   [Seven habits of effective text editing](http://www.moolenaar.net/habits.html)
*   [Basic Vim Tips](http://bencrowder.net/files/vim-fu/)
*   [HOWTO Vim](http://www.gentoo-wiki.info/HOWTO_VIM)

#### 视频

*   [Vimcasts](http://vimcasts.org/) - ogg格式的视频教程。
*   [Vim Tutorial Videos](http://derekwyatt.org/vim/tutorials/) - 从入门到精通，各种视频教程

#### 游戏

*   [Vim Adventures](http://vim-adventures.com/)
*   [VimGolf](http://vimgolf.com/)

### 配置范例

*   [nion's](http://nion.modprobe.de/setup/vimrc)
*   [A detailed configuration from Amir Salihefendic](http://amix.dk/vim/vimrc.html)
*   [Bart Trojanowski](http://www.jukie.net/~bart/conf/vimrc)
*   [Steve Francia's Vim Distribution](https://github.com/spf13/spf13-vim)
*   [W4RH4WK's Vim configuration](https://github.com/W4RH4WK/dotVim)
*   [Fast vimrc/colorscheme from askapache](http://www.askapache.com/linux/fast-vimrc.html)
*   [Basic .vimrc](https://gist.github.com/anonymous/c966c0757f62b451bffa)
*   [Usevim](http://www.usevim.com/)

#### 颜色方案

*   [Vivify](http://bytefluent.com/vivify/)
*   [Vim colorscheme customization](https://linuxtidbits.wordpress.com/2014/10/14/vim-customize-installed-colorschemes/)