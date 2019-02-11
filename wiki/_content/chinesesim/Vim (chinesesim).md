相关文章

*   [List of applications/Documents#Vi_text_editors](/index.php/List_of_applications/Documents#Vi_text_editors "List of applications/Documents")

**翻译状态：** 本文是英文页面 [Vim](/index.php/Vim "Vim") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-3-1，点击[这里](https://wiki.archlinux.org/index.php?title=Vim&diff=0&oldid=468006)可以查看翻译后英文页面的改动。

[Vim](https://en.wikipedia.org/wiki/Vim_(text_editor) "wikipedia:Vim (text editor)")是一个终端文本编辑器。作为[Vi](https://en.wikipedia.org/wiki/Vi "wikipedia:Vi")的一个扩展版本，它具有以下附加功能：语法突出显示，全面的帮助系统，本地脚本（vimscript），文本选择的可视模式和文件比较（vimdiff）。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 用法](#用法)
*   [3 配置](#配置)
    *   [3.1 剪贴板](#剪贴板)
    *   [3.2 语法高亮](#语法高亮)
    *   [3.3 自动换行显示](#自动换行显示)
    *   [3.4 使用鼠标](#使用鼠标)
    *   [3.5 跨行移动光标](#跨行移动光标)
*   [4 文件合并](#文件合并)
*   [5 技巧和建议](#技巧和建议)
    *   [5.1 显示行号](#显示行号)
    *   [5.2 拼写检查](#拼写检查)
    *   [5.3 记录光标位置](#记录光标位置)
    *   [5.4 用 vim 替代 vi](#用_vim_替代_vi)
    *   [5.5 DOS/Windows回车问题](#DOS/Windows回车问题)
    *   [5.6 gVim窗口底部的空格](#gVim窗口底部的空格)
*   [6 插件](#插件)
    *   [6.1 安装](#安装_2)
        *   [6.1.1 使用内置包管理器](#使用内置包管理器)
        *   [6.1.2 使用插件管理器](#使用插件管理器)
        *   [6.1.3 使用Arch软件库](#使用Arch软件库)
    *   [6.2 cscope](#cscope)
        *   [6.2.1 Taglist](#Taglist)
*   [7 参阅](#参阅)
    *   [7.1 官方资源](#官方资源)
    *   [7.2 教程](#教程)
        *   [7.2.1 视频](#视频)
        *   [7.2.2 游戏](#游戏)
    *   [7.3 配置范例](#配置范例)
        *   [7.3.1 颜色方案](#颜色方案)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")下面两个软件包中的一个：

*   [vim](https://www.archlinux.org/packages/?name=vim) — 提供Python 2/3, Lua, Ruby 和 Perl 解释器支持，但没有 GTK/X 支持
*   [gvim](https://www.archlinux.org/packages/?name=gvim) — 除了提供和`vim`一样的功能外，还提供GTK/X支持。

**注意:**

*   [vim](https://www.archlinux.org/packages/?name=vim)包不包含 [Xorg](/index.php/Xorg "Xorg") 支持。具体而言，Vim缺失 `+clipboard` 特性，因而不能够使用 *primary* 和 *clipboard* [剪贴板](/index.php/Clipboard "Clipboard")。[gvim](https://www.archlinux.org/packages/?name=gvim)同时提供命令行版本带`+clipboard`的Vim。
*   非官方源[herecura](/index.php/Unofficial_user_repositories#herecura "Unofficial user repositories")也提供数个Vim/gVim变种版本: `vim-cli` `vim-gvim-common` `vim-gvim-gtk` `vim-gvim-qt` `vim-rt` 和 `vim-tiny`。

## 用法

有关如何使用Vim的基本概述，请遵循vim教程运行**vimtutor**（控制台版本）或**gvimtutor**（图形界面版本）。

Vim包含了一个广泛的帮助系统，可以用`:h *subject*`命令来访问。*subject*可以是命令，配置选项，热键绑定，插件等。使用`:h`命令（不带任何*subject*）来获取帮助系统的相关信息以及在不同的主题之间切换。

## 配置

Vim的用户特定配置文件位于主目录`~/.vimrc`，当前用户的Vim文件位于`~/.vim/`；全局配置文件为`/etc/vimrc`，全局Vim文件位于`/usr/share/vim/`。

**注意:** 常用的功能，如语法高亮在 `defaults.vim` 中启用，当没有 `~.vimrc` 时加载。将 `skip_defaults_vim=1` 添加到 `/etc/vimrc`以完全禁用加载 `defaults.vim`。 [[1]](https://github.com/vim/vim/issues/1033)

### 剪贴板

Vim命令如 `:yank` 或 `:paste` 使用未命名寄存器，默认情况下对应于 `"*` 寄存器。如果 `+clipboard` 功能可用，`"*` 寄存器发送到X中的 `PRIMARY` 缓冲区。

要更改默认寄存器，您可以 `:set clipboard=unnamedplus` 使用 `"+` 寄存器。`"+` 寄存器对应于X中的 `CLIPBOARD` 缓冲区。

欲见更多信息，请参见 `:help 'clipboard'`。

**提示：** 可以创建复制和粘贴操作的自定义快捷方式。参见例如 [[2]](http://superuser.com/a/189198) 用于绑定 `ctrl + c`，`ctrl + v` 和 `ctrl + x`。

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

Vim可以使用鼠标，但只在某些终端上起作用：

*   基于[xterm](/index.php/Xterm "Xterm")/[urxvt](/index.php/Urxvt "Urxvt")的终端模拟器
*   带有[gpm](https://www.archlinux.org/packages/?name=gpm)的Linux控制台（更多细节请参阅[Console mouse support](/index.php/Console_mouse_support "Console mouse support")）
*   [PuTTY](/index.php/PuTTY "PuTTY")。

要开启这个功能，将下面这行代码加入`~/.vimrc`中：

```
set mouse=a

```

`mouse=a` 选项在 `defaults.vim` 中设置。

{{注意| 如果可以访问X服务器，复制/粘贴将使用`"*` 寄存器，参见[#Clipboard](#Clipboard)。按住`shift key`键可以使用xterm处理鼠标按钮。

### 跨行移动光标

默认情况下，在行首按`←`或者在行尾按`→`不能将光标移动至上一行或下一行。

如要改变默认行为，将`set whichwrap=b,s,<,>,[,]`加至你的`~/.vimrc`文件中。

## 文件合并

Vim自带了一个文件差异编辑器（一个用来显示多个文件之间的差异还可以方便的将其合并的程序）。用*vimdiff*来启动它——指定所需文件即可：`vimdiff *file1* *file2*`。以下是*vimdiff*-specific命令的清单。

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

使用`:*line number*` or `*line number*gg`跳转到指定行号。跳转都记录在一个跳转列表中，更多细节参考`:h jump-motions`。

### 拼写检查

Vim有拼写检查的功能，用下面的命令开启：

```
set spell

```

Vim默认只安装了英语字典。更多字典可以通过搜索vim-spell在[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中找到。其他字典可以在[Vim的FTP archive](http://ftp.vim.org/vim/runtime/spell/)中找到。把下载的字典文件存入`~/.vim/spell/`中，并使用以下命令启用：`:setlocal spell spelllang=*en_us*`(将`*en_us*` 换成所需的字典的名称)。

| 行为 | 快捷键 |
| 下一个拼写错误 | `]s` |
| 上一个拼写错误 | `[s` |
| 拼写纠正建议 | `z=` |
| 拼写正确，添加到用户正确字典 | `zg` |
| 在会话中当作正确拼写 | `zG` |
| 拼写错误，添加到用户错误字典 | `zw` |
| 在会话中当作正确拼写 | `zW` |
| 重新进行拼写检查 | `:spellr` |

**提示：**

*   如果需要针对两种语言进行拼写检查（例如英语与德语），在`~/.vimrc`或`/etc/vimrc`中添加`set spelllang=*en,de*`并重启Vim即可。
*   您可以通过使用FileType插件和用于文件类型检测的自定义规则，为任意文件类型（例如*.txt*）启用拼写检查。 要对以*.txt*结尾的任何文件启用拼写检查，请创建文件 `/usr/share/vim/vimfiles/ftdetect/plaintext.vim`，并将 `autocmd BufRead,BufNewFile *.txt setfiletype plaintext` 插入该文件。接下来，将 `autocmd FileType plaintext setlocal spell spelllang=*en_us*` 插入到`~/.vimrc` 或 `/etc/vimrc` 中，然后重新启动Vim。

*   如果想只对LaTeX（或TeX）文档起用拼写检查，在`~/.vimrc`或`/etc/vimrc`添加`autocmd FileType **tex** setlocal spell spelllang=*en_us*`，重启Vim即可。至于非英语语言，替换上述语句中的`en_us`为相应语言代码即可。

### 记录光标位置

Vim可以记录上次打开某一文件时的光标位置，并在下次打开同一文件时将光标移动到该位置。要开启该功能，在配置文件`~/.vimrc`中加入以下内容：

```
augroup resCur
  autocmd!
  autocmd BufReadPost * call setpos(".", getpos("'\""))
augroup END

```

### 用 vim 替代 vi

创建一个[alias](/index.php/Alias "Alias")，如下：

 `alias vi=vim` 

或者，如果你想输入`sudo vi`而得到`vim`，安装[vi-vim-symlink](https://aur.archlinux.org/packages/vi-vim-symlink/)，它将移除`vi`并用一个符号链接`vim`代替。

### DOS/Windows回车问题

打开MS-DOS或Windows下创建的文本文件时，经常会在每行行末出现一个`^M`。这是因为Linux使用Unix风格的换行，用一个换行符（LF）来表示一行的结束，但在Windows、MS-DOS中使用一个回车符（CR）接一个换行符（LF）来表示，因而回车符就显示为`^M`。

可使用下面的命令删除文件中的回车符：

```
:%s/^M//g

```

注意，`^`代表控制字符。输入`^M`的方法是按下`Ctrl+v,Ctrl+m`。

另一个解决方法是，安装 [dos2unix](https://www.archlinux.org/packages/?name=dos2unix)，然后执行 `dos2unix <文件名>`。

**注意:** 另一个简单的方法是更改 `fileformat` 设置。 `set ff=unix` 以转化DOS/Windows行尾为Unix行尾。要做到相反，只要 `set ff=dos`，就可以将Unix行尾转换成DOS/Windows行尾。

### gVim窗口底部的空格

如果[窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")设置为忽略窗口大小提示，gVim会将非功能区域填充为GTK主题背景色。

解决方案是调整gVim在窗口底部保留的空间大小。将下面的代码加入 `~/.vimrc`中：

```
set guiheadroom=0

```

**注意:** 如果将其设为0，将无法看到底部的水平滚动条。

## 插件

向Vim添加插件可以提高您的效率。 插件可以改变Vim的界面，添加新命令，代码完成支持，使用Vim集成其他程序和实用程序，添加对其他语言的支持等等。

**提示：** 有关常用插件的列表，请参阅 [Vim Awesome](http://vimawesome.com/)

### 安装

#### 使用内置包管理器

Vim 8增加了加载原生第三方插件的可能性。可以通过在〜/.vim/pack/foo中存储第三方软件包来使用此功能。

#### 使用插件管理器

插件管理器允许以类似的方式安装和管理插件，而与在何种平台上运行Vim无关。它本身是一个插件，其功能是作为其他Vim插件包管理器。

*   [Vundle](https://github.com/gmarik/Vundle.vim)是现在最流行的Vim插件管理器。
*   [Vim-plug](https://github.com/junegunn/vim-plug)是一个极简的Vim插件管理器，有许多的特性，比如按需插件加载和并行升级。
*   [pathogen.vim](https://github.com/tpope/vim-pathogen)是一个简单的用于管理Vim的runtimepath的插件。
*   [Dein.vim](https://github.com/Shougo/dein.vim) 是一个替代 [NeoBundle](https://github.com/Shougo/neobundle.vim) 的插件管理器，可以在这里找到 [vim-dein-git](https://aur.archlinux.org/packages/vim-dein-git/).

#### 使用Arch软件库

[vim-plugins](https://www.archlinux.org/groups/x86_64/vim-plugins/)分类下有许多插件。 使用`pacman -Sg vim-plugins`来列出可用的插件，然后你可用pacman[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")。

### cscope

[Cscope](http://cscope.sourceforge.net/)是用于浏览项目的工具。 通过导航到字/符号/函数并调用cscope（通常使用快捷键），它可以找到：调用函数的函数，函数定义等等。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")[cscope](https://www.archlinux.org/packages/?name=cscope)包。

将cscope默认文件复制到Vim将自动读取的位置:

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
nnoremap <C-l> :TlistToggle<CR>

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
*   [vim Tutorial and Primer](https://www.danielmiessler.com/study/vim/)
*   [vi Tutorial and Reference Guide](http://usalug.org/vi.html)
*   [Graphical vi-Vim Cheat Sheet and Tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
*   [Vim Introduction and Tutorial](http://blog.interlinked.org/tutorials/vim_tutorial.html)
*   [Open Vim](http://www.openvim.com/) - Vim教学工具集合
*   [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
*   [Learning Vim in 2014](http://benmccormick.org/learning-vim-in-2014/)
*   [Seven habits of effective text editing](http://www.moolenaar.net/habits.html)
*   [Basic Vim Tips](http://bencrowder.net/files/vim-fu/)

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
*   [Fast vimrc/colorscheme from askapache](https://www.askapache.com/linux/fast-vimrc/)
*   [Basic .vimrc](https://gist.github.com/anonymous/c966c0757f62b451bffa)
*   [Usevim](http://www.usevim.com/)

#### 颜色方案

*   [Vivify](http://bytefluent.com/vivify/)
*   [Vim colorscheme customization](https://linuxtidbits.wordpress.com/2014/10/14/vim-customize-installed-colorschemes/)