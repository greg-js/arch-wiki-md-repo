**翻译状态：** 本文是英文页面 [Emacs](/index.php/Emacs "Emacs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-08，点击[这里](https://wiki.archlinux.org/index.php?title=Emacs&diff=0&oldid=229169)可以查看翻译后英文页面的改动。

[Emacs](https://en.wikipedia.org/wiki/Emacs "wikipedia:Emacs")是一个扩展方便，定制能力强，文档丰富的动态交互编辑器。Emacs的核心构建在[Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp")解释器之上，其中Emacs Lisp是大部分Emacs的内建函数和拓展模块的实现语言。Emacs可以在命令行界面下(CLI)工作良好，在图形界面系统下，使用GTK作为默认的图形界面构建工具。在文本编辑能力上，Emacs常常拿来和[vim](/index.php/Vim "Vim")比较。

**Note:** 入门建议直接使用starterkit扩展。本文档实际帮助不大

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 快速入门](#.E5.BF.AB.E9.80.9F.E5.85.A5.E9.97.A8)
    *   [2.1 运行Emacs](#.E8.BF.90.E8.A1.8CEmacs)
        *   [2.1.1 图形界面下打开方式](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E4.B8.8B.E6.89.93.E5.BC.80.E6.96.B9.E5.BC.8F)
        *   [2.1.2 虚拟终端下的常见方式](#.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF.E4.B8.8B.E7.9A.84.E5.B8.B8.E8.A7.81.E6.96.B9.E5.BC.8F)
            *   [2.1.2.1 去掉颜色](#.E5.8E.BB.E6.8E.89.E9.A2.9C.E8.89.B2)
        *   [2.1.3 作为守护进程](#.E4.BD.9C.E4.B8.BA.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [2.2 基本术语和约定](#.E5.9F.BA.E6.9C.AC.E6.9C.AF.E8.AF.AD.E5.92.8C.E7.BA.A6.E5.AE.9A)
    *   [2.3 移动](#.E7.A7.BB.E5.8A.A8)
    *   [2.4 文件和缓冲区](#.E6.96.87.E4.BB.B6.E5.92.8C.E7.BC.93.E5.86.B2.E5.8C.BA)
    *   [2.5 编辑](#.E7.BC.96.E8.BE.91)
    *   [2.6 移除，召回和区域](#.E7.A7.BB.E9.99.A4.EF.BC.8C.E5.8F.AC.E5.9B.9E.E5.92.8C.E5.8C.BA.E5.9F.9F)
    *   [2.7 查找和替换](#.E6.9F.A5.E6.89.BE.E5.92.8C.E6.9B.BF.E6.8D.A2)
    *   [2.8 缩进和前缀参数](#.E7.BC.A9.E8.BF.9B.E5.92.8C.E5.89.8D.E7.BC.80.E5.8F.82.E6.95.B0)
    *   [2.9 窗口和外框架](#.E7.AA.97.E5.8F.A3.E5.92.8C.E5.A4.96.E6.A1.86.E6.9E.B6)
    *   [2.10 获得帮助](#.E8.8E.B7.E5.BE.97.E5.B8.AE.E5.8A.A9)
    *   [2.11 模式](#.E6.A8.A1.E5.BC.8F)
*   [3 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [3.1 TRAMP](#TRAMP)
    *   [3.2 键盘宏和寄存器](#.E9.94.AE.E7.9B.98.E5.AE.8F.E5.92.8C.E5.AF.84.E5.AD.98.E5.99.A8)
    *   [3.3 正则表达式](#.E6.AD.A3.E5.88.99.E8.A1.A8.E8.BE.BE.E5.BC.8F)
*   [4 定制](#.E5.AE.9A.E5.88.B6)
    *   [4.1 多种配置](#.E5.A4.9A.E7.A7.8D.E9.85.8D.E7.BD.AE)
    *   [4.2 加载扩展程序](#.E5.8A.A0.E8.BD.BD.E6.89.A9.E5.B1.95.E7.A8.8B.E5.BA.8F)
    *   [4.3 Local and custom variables](#Local_and_custom_variables)
    *   [4.4 Custom colors and theme](#Custom_colors_and_theme)
    *   [4.5 SyncTeX support](#SyncTeX_support)
*   [5 Documentation](#Documentation)
    *   [5.1 Contextual help](#Contextual_help)
    *   [5.2 The manuals](#The_manuals)
*   [6 拓展模块](#.E6.8B.93.E5.B1.95.E6.A8.A1.E5.9D.97)
*   [7 疑难杂症](#.E7.96.91.E9.9A.BE.E6.9D.82.E7.97.87)
    *   [7.1 彩色输出的问题](#.E5.BD.A9.E8.89.B2.E8.BE.93.E5.87.BA.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [7.2 菜单显示为空](#.E8.8F.9C.E5.8D.95.E6.98.BE.E7.A4.BA.E4.B8.BA.E7.A9.BA)
    *   [7.3 X 窗口下的字符显示问题](#X_.E7.AA.97.E5.8F.A3.E4.B8.8B.E7.9A.84.E5.AD.97.E7.AC.A6.E6.98.BE.E7.A4.BA.E9.97.AE.E9.A2.98)
    *   [7.4 启动速度慢](#.E5.90.AF.E5.8A.A8.E9.80.9F.E5.BA.A6.E6.85.A2)
        *   [7.4.1 错误的网络配置](#.E9.94.99.E8.AF.AF.E7.9A.84.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
        *   [7.4.2 初始化文件加载慢](#.E5.88.9D.E5.A7.8B.E5.8C.96.E6.96.87.E4.BB.B6.E5.8A.A0.E8.BD.BD.E6.85.A2)
    *   [7.5 不能打开配置文件: ...](#.E4.B8.8D.E8.83.BD.E6.89.93.E5.BC.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6:_...)
    *   [7.6 Dead-accent keys problem: '<dead-acute> is undefined'](#Dead-accent_keys_problem:_.27.3Cdead-acute.3E_is_undefined.27)
    *   [7.7 C-M-% and some other bindings do not work in emacs nox](#C-M-.25_and_some_other_bindings_do_not_work_in_emacs_nox)
    *   [7.8 Emacs client gets stuck when switching back to it](#Emacs_client_gets_stuck_when_switching_back_to_it)
    *   [7.9 Emacs-nox output gets messy](#Emacs-nox_output_gets_messy)
    *   [7.10 Shift + Arrow keys not working in emacs within tmux](#Shift_.2B_Arrow_keys_not_working_in_emacs_within_tmux)
*   [8 替代方案](#.E6.9B.BF.E4.BB.A3.E6.96.B9.E6.A1.88)
    *   [8.1 mg](#mg)
    *   [8.2 zile](#zile)
    *   [8.3 uemacs](#uemacs)
*   [9 资源](#.E8.B5.84.E6.BA.90)

## 安装

Emacs有众多变体发行版本(有时候称作_emacsen_). 最常见的莫过于 [GNU Emacs](http://www.gnu.org/software/emacs/)，在[Official repositories](/index.php/Official_repositories "Official repositories")可以找到

```
$ pacman -S emacs

```

如果你总是在终端下工作的话，你可能会选择[emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)。这是一个没有GTK+依赖的版本（也没有声音支持）。

终端版Emacs存在以下问题：它支持更少的颜色和更少的字体控制功能（缺少在线控制字体大小、在一篇文档中使用多种字体等功能）。而且对于一些需要高级特性的功能比如Speedbar或者GUD（调试环境），它也不支持。另外在控制复杂的外观（face）时，emacs-nox比Emacs要慢。

如果你想体验Emacs的所有扩展功能而不用装一堆依赖的话，你可以使用PKGBUILD来按你的需求定制Emacs。不使用`gtk3`可以让Emacs避免使用gconf。图像和声音的支持也可以去除。在Emacs的源代码目录下运行`./configure --help`可以看看有哪些配置选项。

 `PKGBUILD` 

```
# ...
  ./configure --prefix=/usr --sysconfdir=/etc --libexecdir=/usr/lib \
    --localstatedir=/var --with-x-toolkit=gtk2 --with-xft \
    --without-gconf --without-sound
# ...

```

另外一个常见的变体就是[xemacs](https://www.archlinux.org/packages/?name=xemacs).

## 快速入门

一般印象是Emacs十分复杂，学习曲线陡峭，但很多资深学习者并不这样认为，反而认为其非常易懂和可定制。因为其源码和配置文件语义化程度较高。简单了解下自定义和高扩展带来的好处花不了多少时间。何况还有很多成熟的功能拓展模块，很方便添加，可以让Emacs为任何文本编辑的需求配置强大的环境。

Emacs自带一个入门教程，你可以点击欢迎界面上的第一个链接来打开它; 或者从菜单栏中选择_Help->Emacs Tutorial_，或者按'F1'键然后按't'. 我们设计这篇文章来为你在Emacs入门学习中提供额外的资源。

Emacs也包括一系列引用链接，既有适合初学者的内容，也有骨灰级玩家所喜爱的．参见`/usr/share/emacs/<version>/etc/refcards/` (将<version>换成你的emacs版本).

### 运行Emacs

在启动Emacs之前，你要先学会怎么关闭它（尤其是你要在终端里运行它的话）：用`Ctrl+x``Ctrl+c`来关闭它。

#### 图形界面下打开方式

图形界面下可以直接点击图标打开。

#### 虚拟终端下的常见方式

打开Emacs:

```
$ emacs

```

不打开图形界面，直接在终端中运行:

```
$ emacs -nw

```

也可以直接用下面的命令来打开一个文件:

```
$ emacs filename.txt

```

##### 去掉颜色

默认的emacs会带有颜色主题，如果不需要，可以关闭之：

```
$ emacs -nw --color=no

```

#### 作为守护进程

Emacs由于每次启动都需要加载大量自定义的配置文件，所以打开时候会有点慢。从Emacs23开始, Emacs可以以守护进程的形式运行，这样每个用户都可以链接到Emacs。以守护进程运行Emacs:

```
$ emacs --daemon

```

你可能在启动时打开一个守护进程，然后再将守护进程链接到窗口。另外，也可以将图形和终端客户端同时链接到守护进程上，这样启动图形界面速度就很快了。

如果你仅仅想链接到守护进程，用下面的命令(注意,在桌面环境下这个命令会打开一个图形客户端，而在像tty这种命令行下，它会打开一个命令行版的emacs):

```
$ emacsclient

```

如果你想在桌面环境下打开一个命令行版的emacs，使用下面的命令:

```
$ emacsclient -t

```

另外，你可以在后面加上 `-a ""` 参数. 现在，你第一次使用这个命令时，它会把emacs作为守护进程来启动，它会留在后台以加快以后的启动速度(也会记住缓冲区).

更聪明点，你可以在.bashrc中加上下面的别名:

```
alias em='emacsclient -t -a ""'  #在终端中开启emacs
alias emc='emacsclient -nc -a ""'  #启动emacs图形界面
EDITOR='emacsclient -a ""'
```

在[xfce](/index.php/Xfce "Xfce")桌面环境中，如果你想使用 emacsclient -c 来代替 emacs %f 打开一个新文件, 你可以修改你的 /usr/share/applications/emacs.desktop 文件，把下面这一行

```
$ Exec=emacs %f

```

修改为

```
$ Exec=emacsclient -c

```

使用这种方法，每次你打开一个文件时就只会启动客户端，因此速度非常快!

### 基本术语和约定

Emacs使用一些刚开始看起来很奇怪的术语和约定，我们会在合适的时候介绍。但是，对于部分术语，我们必须要在前面介绍，因为它们对于使用Emacs来说是非常基础的。

第一个要介绍的术语是_缓冲区_的概念。一个缓冲区就是Emacs中的数据的一种表示方式，比如，当使用Emacs打开一个文件时，这个文件从磁盘中被读出来，它的内容被存储在了缓冲区里面，它的内容可以在这个缓冲区里面被编辑并且可以重新写进磁盘中。缓冲区中的内容不仅仅可以是文本，也可以是图片和widget。现在，让缓冲区可以显示应用程序的工作正在进行！换个角度思考，在磁盘中数据是以文件形式保存的，而在Emacs中，数据是以缓冲区的形式存在的。

在Emacs中，对于按键组合的约定你可能很陌生。比如:

**C-x** 代表 Ctrl-x

**M-x** 代表 Meta-x

**注意:** 'Meta'一般代表Alt键，也可以用Esc键替代。

举个例子，退出Emacs使用下面的按键组合**C-x C-c**。这个可以读做，"按住Ctrl键再按'x'，释放，再按住Ctrl键再按'c'。虽然Emacs提供了一个菜单栏，但是强烈建议学习使用按键组合。这个指南将参考Emacs的按键绑定的约定。

### 移动

光标移动和其它图形编辑器非常类似，鼠标和方向键可以用来改变光标（在Emacs中称为_点_）的位置。在Emacs中，方向键代表的标准移动命令也有其它辅助的绑定。向前(forward)移动一个字符，使用 **C-f**，向后(back)移动一个字符，使用**C-b**。 **C-n** 和 **C-p** 分别用于移动到下(next)一行和移动到上(previous)一行。再声明一下，强烈推荐使用组合键而不是使用方向键和鼠标。

可以想像，Emacs提供了更多的光标高级移动命令，包括移动一个单词和一个句子。 **M-f** 表示光标向前移动一个单词， **M-b** 表示向后移动一个单词。类似地，**M-e** 把光标移动到一个句子的末尾(end)， **M-a** 移动到句子的开头。

直到现在，所有的移动命令都是和光标有关的。**M-<** 表示把光标移动到缓冲区的开头，和它相反的是 **M->**, 把光标移动到缓冲区的末尾。要把光标移动到某一特定行，使用**M-g g**. **M-g g** 会提示输入行号。同样，要移动到一行的开头或者结尾，分别使用**C-a** 和 **C-e**。

**Note:** 这些命令（实际上是全部命令）的绑定，在不同的模式(mode)中，_稍微_会有不同。然而，覆盖的命令提供不同的功能这种情况很少见。更多信息请看[Modes](/index.php/Emacs#Modes "Emacs")。

### 文件和缓冲区

Emacs 提供了一系列命令来对文件操作，其中最常用的会在这里详细说明。**C-x C-f** 用来打开一个文件(在Emacs中叫做'查找文件')。如果指定的文件不存在，Emacs会打开一个空的缓冲区。保存一个缓冲区会创建一个包含缓冲区内容的文件。**C-x C-s** 就是用来保存缓冲区的。要保存一个文件名不一样的缓冲区，使用**C-x C-w** (这其实是'write-file'这条命令的助记符), 它会在写入磁盘之前提示输入新文件名。也可以使用**C-x s**来保存所有的缓冲区, 如果某个缓冲区在上次保存之后被修改了，则会提示进行哪项操作。

**Note:** 如果指向某个文件的缓冲区还在打开的话，**C-x C-f** 是不会重新从磁盘中读取文件的。要从磁盘中重新读取文件，先使用**C-x k**关掉缓冲区，再使用**C-x C-f**打开文件，或者使用**M-x revert-buffer**.

很多互动的命令，比如"find-file" 或者 "write-file" 会在Emacs窗口的底部栏提示输入。这栏称为_minibuffer_。和很多*nix shell一样，minibuffer支持很多基本的操作和TAB补全。按两下**<TAB>**可以显示一个补全的选项列表，并且，如果你喜欢，可以用鼠标从列表中选择。minibuffer的补全在很多输入（包括命令和文件名）中都可以用。

minibuffer也提供一个记住历史的特性。通过**Up Arrow** 或者 **C-p**可以取得这条命令的上一个条目.

要在任意时刻退出minibuffer，使用**C-g**.

打开几个文件后，切换缓冲区是非常必要的。打开一个指向那个缓冲区的文件可以切换到那个缓冲区。但是这不是最高效的方法。Emacs提供**C-x b**来提示要显示的新缓冲区(这里可以使用TAB补全)。输入一个不存在的缓冲区，则会新建一个空的缓冲区。

**Note:** 要切换到上一个缓冲区，使用**C-x b <RET>**, 因为上一个缓冲区是默认的缓冲区。

使用**C-x C-b**可以显示所有打开缓冲区的列表。如果某个缓冲区不需要使用了，使用**C-x k**来关掉它。

### 编辑

Emacs 内建有很多编辑命令。可能最重要的还没有介绍的是'undo'，它的快捷键为 _C-__ 或者 _C-/_ .移动光标的命令通常都有对应的删除字符的命令。例如， **M-<backspace>** 可以用来删除一个光标后的词，**M-d**可以用来删除光标前面的一个词。删除光标至行尾或者句尾的字符可以分别用**C-k** 或者 **M-k**。

通常我们都约定一行不能超过80个字符。这是为了代码的可读性，尤其是一行中的字符可能会接触到窗口边缘。在Emacs，自动地插入或者删除换行符称为_filling_。我们可以用 **M-q** 重整当前的段落（重新分配换行符，删除段落中多余的空格和tab键）

字符和单词可以分别通过 **C-t** 和 **M-t** 进行交换。比如： `Hello World!` → `World! Hello`

单词的大小写也可以调整。**M-l** 把光标处的单词变成小写 (`HELLO` → `hello`); **M-u** 把光标处的单词变成大写(`hello` → `HELLO`)， **M-c** 把光标处的单词的第一个字母变成大写，并把后面的变成小写(`hElLo` → `Hello`).

### 移除，召回和区域

一个_区域_（region)是指在两个位置之间的一段字。其中一个位置被称为_标记_(mark)，另一个是光标。**C-<SPC>**用来设置标记的位置，紧接着就可以通过移动光标来创造一个区域。在GNU Emacs 23.1及以后的版本中，这个区域默认是可见的。有许多命令是针对区域的，其中最常用的就是_kill_命令。

在Emacs中，剪切和粘贴分别对应的命令叫做_kill_和_yank_。许多删除多个字符的命令（包括上面提到的**C-k**和**M-d**命令）实际上是把文字剪切下来，附加到一个叫_kill-ring_的地方。kill-ring 就是一个被删掉的文字的列表。在默认情况下，kill-ring会保存最多60次删除记录。连续的删除会连在一起。

**C-w** 和 **M-w** 可以用来删除或复制一个区域。

要想把删掉的文字插入进来（也就是'yanking'），可以用**C-y**命令。**C-y** 可以连续用好多次来重复插入。按刚刚所讲，之前删除的文字会排成一个列表，但是**C-y**只能获取列表中的第一个，也就是最后删掉的一个。再之前删掉的可以通过**M-y**来获取。它会把**C-y**刚刚插入的文字用再早删除的文字替换掉。**M-y** 必须紧跟着**C-y**命令执行，可以执行很多次以遍历kill-ring。

### 查找和替换

在文本编辑中进行字符串查找是很常见的任务。按**C-s**可以正向搜索，按**C-r‘’‘则可以反向搜索。这些命令提示要搜索的字符串。搜索是增量的，你再次按键时会显示下一个匹配的位置，并且可以使用**C-s’‘’向前或者使用**C-r‘’‘向后。找到匹配结果之后，可以按下**<RET>**结束搜索。另外，如果你想回到发起搜索的位置，可以使用**C-g**。**

一旦搜索完成（不是由**C-g**之类的指令引起），当前搜索的字符串将会作为下一次搜索的默认参数。使用’‘’C-s C-s**或者**C-r C-r**可以达到这样的效果。**

I-search 有一些有用的命令，使用**M-e**来编辑当且搜索区域，使用**M-c**来触发大小写敏感匹配。

正则表达式搜索除了指令不同之外，其他方面和以上都相同。使用**C-M-s**或者**C-M-r**来使用正则表达式搜索。相应地，用**C-s**和**C-r**可以前后移动，和普通的搜索没什么两样。

除了搜索之外，进行字符串替换也是有必要的。原始文本和替换文本都会有提示，替换的时候也会有提示。尽管有很多选项提供（按**?**可以了解完整的选项），最常用的还是**y**（进行替换），**n**（跳过），以及**!**（替换当前及之后所有匹配）。

### 缩进和前缀参数

Indentation is usually performed with either **<TAB>**, to indent a single line, or with **C-M-\**, to indent a region.

Exactly how text is indented usually depends on the _major-mode_ which is active. Major-modes often define indentation styles specialising in indenting a certain type of text. (See [Modes](/index.php/Emacs#Modes "Emacs") for more information.)

In some cases, a suitable major-mode may not exist for a file type, in which case, manual indentation may be necessary. Create a region (see [Killing, yanking and regions](/index.php/Emacs#Killing.2C_yanking_and_regions "Emacs")) then perform indentation with **C-u <n> C-x <TAB>** (where '<n>' is the number of columns which the text within the region should be indented). For example:

Increase the region's indentation by four columns:

```
C-u 4 C-x <TAB>

```

Decrease the region's indentation by two columns.

```
C-u -2 C-x <TAB>

```

**Note:** The trick behind this is **C-u**, which corresponds to the 'universal-argument' command. Providing a 'universal-argument' is a way to provide more information to a command (this information is referred to as a 'prefix argument'). In this case, we provided the amount of indentation desired to the command invoked by **C-x <TAB>**. Without providing an argument, **C-x <TAB>** will only increase indentation by 1 column.

### 窗口和外框架

Emacs的设计是可以同时方便地编辑多个文件。这是通过把Emacs的接口分成三个层次来实现的，即buffer（之前介绍过了），_window_和_frame_。

_window_ 是显示buffer的一个viewport（社区）。一个window一次只能显示一个buffer。但是一个buffer可以在多个window中显示。在窗口下面有一个_mode-line_，它用于显示当前buffer的信息。

_frame_ 是Emacs的一个"窗口"（这是标准的术语。比如，'窗口'是现代桌面的称谓），它包含了标题栏，菜单栏，还有一个或多个'window'（这是Emacs的术语，比如上面提到的'window'）。

从现在起，这些Emacs中存在的名词的定义就可以使用了。

要把window水平分隔和垂直分隔，分别使用**C-x 2**和**C-x 3**。这种效果其实就是在当前frame中开户另外一个window。要在多个window中循环切换，使用**C-x o**。

与分隔一个window相反的是删除window。要删掉当前window，使用**C-x 0**，要删掉除了当前window之外的其它window，使用**C-x 1**。

和window一样，创建和删除frame也是可以的。**C-x 5 2**会创建一个frame，**C-x 5 0**会删除当前的frame，**C-x 5 1**会删除除了当前frame之外的其它frame。

**注意:** 这些命令不影响buffer。比如删除一个window并不会删除在window中显示的buffer。

### 获得帮助

Emacs在设计的时候就自文档化了。比如，要查看一个命令的名字或者它的键的绑定，Emacs提供了很多帮助信息。下面是列出来的最有用的一些帮助命令：

```
**C-h t**        启动Emacs官方教程

**C-h b**        列出来所有的有效键绑定

**C-h k**        查找一个键被绑定在了哪个命令上

**C-h w**        查找一个命令被绑定在了哪些键上

**C-h a**        查找一个匹配一段描述的命令

**C-h m**        显示当前激活的所有模式的信息

**C-h f**        显示给定函数的描述信息

```

### 模式

一个Emacs模式是用Emacs Lisp语言写的一个控制相关缓冲区行为的扩展。一般来说，它给编辑文本提供缩进，语法高亮和键绑定的功能。复杂的模式可以把Emacs变成一个完美的IDE (Integrated Development Environment). Emacs 一般会使用一个文件的扩展来确定应该加载那个模式。

一些编写shell脚本比较有用的模式有sh-mode, line-number-mode 和 column-number-mode。它们可以并行地通过下面的方式激活:

**M-x sh-mode <RET>**

**M-x column-number-mode <RET>**

line-number-mode 默认是激活的，它可以通过下面的命令来打开/关闭：

**M-x line-number-mode <RET>**

sh-mode 是一个 _major-mode_. Major-modes 调整Emacs，并且经常提供了一些特定的命令来编辑某种类型的文本。一个缓冲区只能激活一种major-mode。除了支持语法高亮和缩进，sh-mode还定义了几条命令来帮助快速开发shell脚本。下面是其中的几条：

```
**C-c (**	 插入一个函数定义

**C-c C-f**	 插入一个for循环

**C-c TAB**	 插入一条if语句

**C-c C-w**	 插入一个while循环

**C-c C-l**	 插入一个从1到n的有下标的循环

```

'line-number-mode' 和 'column-number-mode' 是 _minor-modes_. Minor-modes 可以用来扩充major-mode的功能，多个minor-mode可以同时激活。

## 提示和技巧

前面的部分给出了基本编辑命令的概述，没有给出Emacs的一个指示。这个部分讲述一些高级的技巧和功能。

### TRAMP

TRAMP (Transparent Remote Access, Multiple Protocols) ，顾名思义，是一个可以通过很多协议透明访问远程文件的一个扩展。当提示输入一个文件名，输入特定的格式就可以使用TRAMPP。比如：

在打开`/etc/hosts`文件之前提示输入root的密码以获取root权限：

```
C-x C-f /su::/etc/hosts

```

要通过SSH使用'myuser'用户名登录'myhost'主机并打开文件`~/example.txt`：

```
C-x C-f /ssh:myuser@myhost:~/example.txt

```

TRAMP的路径一般是这种格式'/[protocol]:[[user@]host]:<file>'。TRAMP支持的不只上面的两个简单例子。请查看Emacs里面的TRAMPP info手册了解更多的信息。

### 键盘宏和寄存器

这一部分会提供一个实用的指南来使用一些更强大的编辑特性。也就是“键盘宏”和“寄存器”。

我们的目标是产生一个字符列表和它们在这个列表中对应的位置。虽然这可以通过手工格式化来完成，但是这样会很慢而且容易出错。如果我们采用一些Emacs更高级的编辑功能却可以起到四两拨千斤的功效。在介绍这个方法之前，需要先了解一些技术背后的细节。

要介绍的第一个特性就是_寄存器_。寄存器的功能是用来保存和获取各种各样的数据。每个寄存器用一个字母来命名，这个字母就是用来调用这个寄存器的。

另一个要介绍的就是_键盘宏_。一个键盘宏存储了一个命令序列以便以后可以重复使用。下面就一步一步地讲解这个方法。

首先我们从一个包含如下字符的缓冲区开始：

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

通过`number-to-register' 命令 (**C-x r n**)我们来准备一个寄存器，把数字'0'存储在寄存器'k'中：

```
C-x r n k

```

当光标在缓冲区开头的时候，开始录制键盘宏 (**C-x (**) 然后开始对字符串进行格式化：

```
C-x ( C-f M-4 .

```

插入 (**C-x r i**) 然后将寄存器'k'加1 (**C-x r +**) 。开头的 (**C-u**) 命令是用来在插入文字之后让光标移到插入的文字后面：

```
C-u C-x r i k C-x r + k

```

最后我们来插入一个回车来结束格式化。Emacs可以重复以上过程，从我们定义键盘宏的位置开始，直到最后一个字符。**C-x e**命令停止宏的录制并开始执行这段宏。开头的 **M-0** 命令是用来让宏在出错的时候停下来，这样在它走到这行的结尾就会停下来。

```
<RET> M-0 C-x e

```

下面是结果：

```
 A....0
 B....1
 C....2
 [...]
 x....49
 y....50
 z....51

```

### 正则表达式

From the Emacs Manual: "A regular expression, or _regexp_ for short, is a pattern that denotes a (possibly infinite) set of strings." This section will not go into any detail regarding regular expressions themselves (as there is simply too much to cover). It will however provide a quick demonstration of their power. See [Regular Expressions](http://www.gnu.org/software/emacs/manual/html_node/elisp/Regular-Expressions.html#Regular-Expressions) section in the Emacs Manual for further reading.

Given the same scenario presented above: A list of characters which are to be formatted to represent their respective position in the list. (see [Keyboard macros and registers](/index.php/Emacs#Keyboard_macros_and_registers "Emacs")). Again, starting with a buffer containing.

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

At the beginning of the buffer, use **C-M-%** (if the key-sequence is difficult to perform, it may be more comfortable to use **M-x query-replace-regexp**). At the prompt:

```
\(.\)

```

which simply matches one character. Then, when prompted for the replacement:

```
\1....\#^J

```

**Note:** '^J' represents where a newline should be placed, it should not be entered into the prompt. The newline must instead be inserted literally using **C-q C-j**.

The replacement expression reads: "Insert the matched text between the first set of parentheses (in this case, a single character), followed by 4 periods then insert an automatically incremented number followed by a newline.

Finally, press **!** to apply this across the entire buffer. All of the formatting that was performed in the previous section was performed with a single regexp replacement.

## 定制

Emacs能通过~/.emacs或者**M-x customize**来定制。本段落将着眼于手动定制 ~/.emacs，并且提供了一些常用配置的样例。配置命令提供了一个适应的途径，通过它你能够渐渐熟悉Emacs。

这里的所有例子都能在Emacs中奏效。比如，在Emacs中计算表达式： **C-M-x** 同时指到任何需要求值的地方。

或者

**C-x C-e** 指到最后的“）”。

用'y'和'n'来代替频繁地输入'yes’和'no‘是一个好的方法：

```
(defalias 'yes-or-no-p 'y-or-n-p)

```

取消光标闪烁：

```
(blink-cursor-mode -1)

```

类似地，开启上一节提到的列号模式：

```
(column-number-mode 1)

```

它们两者之间的相似不是偶然：光标闪烁模式和列号模式都是'副参模式'，按照规则，'副参模式’能通过正负值来设置。如果参数省略，'副参模式'将被开/关。

这里有其他一些'副参模式'的例子，下面的参数将会关闭滚动栏、菜单栏、工具栏。

```
(scroll-bar-mode -1)
(menu-bar-mode -1)
(tool-bar-mode -1)

```

变量'auto-mode-alist'修改之后能够改变默认的“主参模式”。下面的例子把'.tut'和'.req'修改成了'.text-mode'。

```
(setq auto-mode-alist
  (append
    '(("\\.tut$" . text-mode)
      ("\\.req$" . text-mode))
    auto-mode-alist))

```

Settings can also be applied on a per-mode basis. A common method for this is to add a function to a _hook_. For example, to force indentation to use spaces instead of tabs, but only in text-mode:

```
(add-hook 'text-mode-hook (lambda () (setq indent-tabs-mode nil)))

```

Similarly, to only use spaces for indentation everywhere:

```
(setq-default indent-tabs-mode nil)

```

Keybindings can be adjusted in two ways. The first of which is 'define-key'. 'define-key' creates a keybinding for a command but only in one mode. The example below will make **F8** delete any whitespace from the end of each line of a 'text-mode' buffer:

```
(define-key text-mode-map (kbd "<f8>") 'delete-trailing-whitespace)

```

The other method is 'global-set-key'. This is used to bind a key to a command everywhere. To bind 'query-replace-regexp' (**C-M-%**) to '<f7>'.

```
(global-set-key (kbd "<f7>") 'query-replace-regexp)

```

Binding a command to an alternate key does not replace any existing bindings. Which is to say, 'query-replace-regexp' would be bound to both **F7** and **C-M-%** after the above example.

Almost anything within Emacs can be configured. Browsing through the [Emacs Wiki](http://emacswiki.org/) should give a solid place to start.

### 多种配置

你可以使用少量配置然后告诉Emacs来加载其他配置。

例如，我们来定义两个配置文件。

 `.emacs` 

```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/plugins" nil t)
(load "~/.emacs.d/theme" nil t)

```

这是我们在后台载入的完整配置。但是plugins文件太大导致载入太慢，如果我们要打开一个新的Emacs窗口，可能就不会使用plugins配置，每次加载它实在是太笨重了。

 `.emacs-light` 

```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/theme" nil t)

```

现在我们这样来加载Emacs：

```
emacs -q -l ~/.emacs-light

```

你可以为这个命令创建一个别名。

### 加载扩展程序

你能用require来加载扩展程序，例如这样：

```
(require 'mediawiki)

```

如果你试着在一个买有安装mediawiki的机器上使用相同的配置，Emacs会提示错误。并且，所有制定的扩展代码都会失效。

一个小的技巧是测试require的返回值。

```
(if (require 'mediawiki nil t)
    (progn
      (setq mediawiki-site-alist '(
             ("ArchLinux" "[https://wiki.archlinux.org/](https://wiki.archlinux.org/)" "UserName" "" "Main Page")
             )
           )
      (setq mediawiki-mode-hook
            (lambda ()
              (visual-line-mode 1)
              (turn-off-auto-fill)
              ))
 ))

```

### Local and custom variables

You can define variables in your configuration file that can be later one modified locally for a file.

```
(defcustom my-compiler "gcc" "Some documentation")

```

Now in any file you can define local variables in two ways:

*   On the very first line, write

```
// -*- my-compiler:g++; mode:c++ -*-

```

*   If you cannot (or do not want to) write this on the first line, you can put it at the end:

```
// Local Variables:
// my-compiler: g++
// mode: c++
// End:

```

Note that the beginning characters need to be comments for the current language, that's why here we used two backslashes for C++. For Elisp you would use

```
;; -*- mode:emacs-lisp -*-

```

There is two functions that may help you in defining the variables: _add-file-local-variable_ and _add-file-local-variable-prop-line_.

Finally, custom variable are considered insecure by default. If you try to open a file that contains local variable redefining insecure custom variables, Emacs will ask you for confirmation.

If you know what you are doing, you can declare the variable as secure, thus removing the Emacs prompt for confirmation. You need to specify a predicate that any new value has to verify so that it can be considered safe.

```
(defcustom my-compiler "gcc" "Some documentation" :safe 'stringp)

```

In the previous example, if you attempt to set anything else than a string, Emacs will consider it insecure.

### Custom colors and theme

Colors can be easily customized using the _face_ facility.

```
(set-face-background  'region                 "color-17")
(set-face-foreground  'region                 "white")
(set-face-bold-p      'font-lock-builtin-face t ) 

```

You can have let Emacs tell you the name of the face where the point is. Use the _customize-face_ function for that. The facility will show you how to set colors, bold, underline, etc.

Emacs in console can handle 256 colors, but you will have to use an appropriate terminal for that. For instance URxvt has support for 256 colors. You can use the _list-colors-display_ for a comprehensive list of supported colors. This is highly terminal-dependent.

### SyncTeX support

Emacs is definitely one of the most powerful LaTeX editor. This is mostly due to the fact you can adapt or create a LaTeX mode to fit your needs best.

Still, there might be some challenges, like SyncTeX support. First you need to make sure your TeX distribution has it. If you installed TeX Live manually, you may need to install the _synctex_ package.

```
# umask 022 && tlmgr install synctex

```

SyncTeX support is viewer-dependent. Here we will use Zathura as an example, so the code needs to be adapted if you want to use another PDF viewer.

```
(defcustom tex-my-viewer "zathura --fork -s -x \"emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"'\"'\"%{input}\"'\"'\")) (goto-line %{line}))'\"" 
  "PDF Viewer for TeX documents. You may want to fork the viewer
so that it detects when the same document is launched twice, and
persists when Emacs gets closed.

Simple command:

  zathura --fork

We can use

  emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"%{input}\")) (goto-line %{line}))'

to reverse-search a pdf using SyncTeX. Note that the quotes and double-quotes matter and must be escaped appropriately."
:safe 'stringp)

```

Here we define our custom variable. If you are using AucTeX or Emacs default LaTeX-mode, you will have to set the viewer accordingly.

Now open a LaTeX source file with Emacs, compile the document, and launch the viewer. Zathura will spawn. If you press `Ctrl+Left click` Emacs should place the point at the corresponding position.

## Documentation

You may find yourself overwhelmed by the amount of Emacs features. You may find it difficult to know how to use Emacs Lisp to customize your favorite modes, or even to create your own modes / packages. Thankfully Emacs takes a strong point to auto-documenting everything: its internals, current configuration, bindings, etc. Almost everything is documented.

### Contextual help

Emacs is self-documenting by design. As such, a great deal of information is available to determine the name of a specific command or its keybinding, for example. The following is a listing of some of the most helpful of these:

```
**C-h a**        Find a command matching a description.

```

```
**C-h b**        List all active keybindings.

```

```
**C-h f**        Describe the given function.

```

```
**C-h k**        Find which command a key is bound to.

```

```
**C-h m**        Display information regarding the currently active modes.

```

```
**C-h t**        Start the Emacs tutorial.

```

```
**C-h v**        Describe the given variable.

```

```
**C-h w**        Find which key(s) a command is bound to.

```

### The manuals

If you really want to master Emacs, the most recommanded source of documentation remains the official manuals:

*   Emacs: the complete Emacs user manual.
*   Emacs FAQ.
*   Emacs Lisp Intro: if you never used any programming language before.
*   Elisp: if you are already familiar with a programming language.

You can access it as PDFs from [GNU.org](http://www.gnu.org/software/emacs/manual/) or directly from Emacs itself thanks to the embedded 'info' reader: **C-h i**. Press **m** to choose a book.

Some users prefer to read books using 'info' because of its convenient shortcuts, its paragraphs adapting to window width and the font adapted to current screen resolution. Some find it less irritating to the eyes. Finally you can easily copy content from the book to any Emacs buffer, and you can even execute Lisp code snippets directly from the examples.

You may want to read the **Info** book to know more about it: **C-h i m info <RET>**. Press **?** while in info mode for a quick list of shortcuts.

## 拓展模块

虽然Emacs包含了成百上千种模式(mode)，库和其它扩展，还有更多的扩展来增强Emacs。大多数扩展会详细说明安装它的时候要对~/.emacs作什么改动。这些说明一般会在一个elisp源文件开头的注释中，或者在一个README中（如果这个扩展包含了多个源文件）。

在'community'仓库中有很多流行的扩展，更多的扩展还放在了[AUR](/index.php/AUR "AUR")。这些软件包的名字有一个'emacs-'前缀（比如emacs-lua-mode）。在很多情况下，在安装的过程会显示怎样修改~/.emacs以安装该扩展到Emacs中。

想知道怎样激活一个不在上面提到的地方的扩展，查看[Emacs Wiki](http://emacswiki.org/)中的相应页面，一般会提供一个配置的例子。Emacs Wiki也是一个寻找扩展的优秀资源。

你也可以使用[Emacs Lisp Package Archive (ELPA)](http://tromey.com/elpa/) 来自动安装软件包。打开那个网站看说明。ELPA已经包括在了Emacs24中;它已经作为Emacs生态系统中的一部分了。

## 疑难杂症

### 彩色输出的问题

Emacs默认使用原生的转义串来输出颜色。也就是说，它会在要显示颜色的地方显示奇怪的字符。

在`~/.emacs`中加入下面的代码解决这个问题：

```
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)

```

### 菜单显示为空

一些菜单显示为空，这是GNU Emacs 23.1的一个bug（使用GTK toolkit的时候）。好像在Emacs的CVS trunk中已经修复了。对应的[Debian bug report](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=550541) 有一个应对措施。

### X 窗口下的字符显示问题

当你使用X窗口启动emacs时，如果发现主窗口中的所有字符都是黑框白块（就像你没有安装正确的字体看到的字符一样），那么你需要安装 [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) 或者 [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) 并且重启X窗口。

### 启动速度慢

启动速度慢经常是由下面两种情况引起的。

要确定是哪种情况，这样打开Emacs：

```
$ emacs -q

```

如果Emacs还是启动很慢，则是[错误的网络配置](/index.php/Emacs#Incorrect_network_configuration "Emacs")。如果不是，则可以确定是[.emacs的问题](/index.php/Emacs#Init_file_loads_slowly "Emacs")。

#### 错误的网络配置

当启动Emacs的时候，一些错误，特别是在/etc/hosts中的，经常会导致5秒以上的延迟。在网络配置指南中查看'[set the hostname](/index.php/Configuring_network#Set_the_hostname "Configuring network")' 了解更多内容。

#### 初始化文件加载慢

一个很简单的方法查找原因是注释掉（比如在行开头使用';'）你的~/.emacs（或者~/.emacs.d/init.el）里面可疑的地方，然后再启动Emacs，看速度是否有改善。记住，使用"require"和"load"会减慢启动速度，特别是用在很大的插件上。一般来说，他们应该用在当目标是Emacs启动的时候就需要或者提供仅仅是一个扩展的"autoloads"。否则，直接使用'autoload'函数。比如，不是这样：

```
(require 'anything)

```

你应该这样:

```
(autoload 'anything "anything" "Select anything" t)

```

### 不能打开配置文件: ...

这个错误最常见的原因是'load-path'变量没有包含某些插件的目录。要解决这个问题，在加载插件前，把需要加载的插件目录加入到要搜索的list中：

```
 (add-to-list 'load-path "/path/to/directory/")

```

当尝试使用一个插件的包，而这个包又被Emacs加上了非'/usr'的前缀时，load-path需要更新。把下面的代码放到使用这个插件的包的代码的前面：

```
 (add-to-list 'load-path "/usr/share/emacs/site-lisp")

```

如果手动编译Emacs，记住默认的前缀是'/usr/local'。

### Dead-accent keys problem: '<dead-acute> is undefined'

Searching about this bug on Google, we find this link: [http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html)

Explaining the problem: in recent versions of b72

```
Emacs, the normal way to use accent keys doesn't work as expected. Trying to accent a word like 'fiancé' will produce the message above.

```

A way to solve it is just put the line above on your startup file, `~/.emacs`:

```
  (require 'iso-transl)

```

And no, it isn't a bug, but a feature of new Emacs versions. Reading the subsequent messages about it on the mail list, we found it ([http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html)):

	_It seems that nothing is loaded automatically because there is a choice betwee iso-transl and iso-acc. Both seem to provide an input method with C-x 8 or Alt-<accent> prefix, but what you and I are doing is just pressing a dead key (^, ´, `, ~, ¨) for the accent and then another key to "compose" the accented character. And there is no Alt key used in this! And according to documentation it seems be appropriate for 8-bit encodings, so it should be pretty useless in UTF-8\. I reported this bug when it was introduced, but the bug seems to be_

a3b

```
classified as a feature ... Maybe it's just because the file is auto-loaded though pretty useless. 

```

### C-M-% and some other bindings do not work in emacs nox

This is because terminals are more limited than Xorg. Some terminals may handle more bindings than other, though. Two solutions:

*   either use the graphical version,
*   or change the binding to a supported one.

Example:

 `.emacs` 

```
(global-set-key (kbd "C-M-y") 'query-replace-regexp)

```

### Emacs client gets stuck when switching back to it

If you are using Emacs daemon, then you should know that input is blocking. If one Emacs instance is in the minibuffer (after an **M-x** for instance), then all other instance will wait for it to finish. Press **C-g** to cancel any input to make sure this Emacs session is not blocking.

### Emacs-nox output gets messy

When working in a terminal, the color, indentation, or anything related to the output might become crazy. This is (probably?) because Emacs was sent a special character at some point which may conflict with the current terminal. There is not much to be done but restarting emacs. If someone has a workaround or a more detailed explanation on the issue, feel free to contribute.

Graphical Emacs does not suffer from this issue.

### Shift + Arrow keys not working in emacs within tmux

First you must enable xterm-keys in your [tmux](/index.php/Tmux "Tmux") config.

 `.tmux.conf` 

```
setw -g xterm-keys on

```

But, this will break other key combinations. To fix them, put the following in your emacs config.

 `.emacs` 

```
;; handle tmux's xterm-keys
;; put the following line in your ~/.tmux.conf:
;;   setw -g xterm-keys on
(if (getenv "TMUX")
    (progn
      (let ((x 2) (tkey ""))
	(while (<= x 8)
	  ;; shift
	  (if (= x 2)
	      (setq tkey "S-"))
	  ;; alt
	  (if (= x 3)
	      (setq tkey "M-"))
	  ;; alt + shift
	  (if (= x 4)
	      (setq tkey "M-S-"))
	  ;; ctrl
	  (if (= x 5)
	      (setq tkey "C-"))
	  ;; ctrl + shift
	  (if (= x 6)
	      (setq tkey "C-S-"))
	  ;; ctrl + alt
	  (if (= x 7)
	      (setq tkey "C-M-"))
	  ;; ctrl + alt + shift
	  (if (= x 8)
	      (setq tkey "C-M-S-"))

	  ;; arrows
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d A" x)) (kbd (format "%s<up>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d B" x)) (kbd (format "%s<down>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d C" x)) (kbd (format "%s<right>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d D" x)) (kbd (format "%s<left>" tkey)))
	  ;; home
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d H" x)) (kbd (format "%s<home>" tkey)))
	  ;; end
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d F" x)) (kbd (format "%s<end>" tkey)))
	  ;; page up
	  (define-key key-translation-map (kbd (format "M-[ 5 ; %d ~" x)) (kbd (format "%s<prior>" tkey)))
	  ;; page down
	  (define-key key-translation-map (kbd (format "M-[ 6 ; %d ~" x)) (kbd (format "%s<next>" tkey)))
	  ;; insert
	  (define-key key-translation-map (kbd (format "M-[ 2 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; delete
	  (define-key key-translation-map (kbd (format "M-[ 3 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; f1
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d P" x)) (kbd (format "%s<f1>" tkey)))
	  ;; f2
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d Q" x)) (kbd (format "%s<f2>" tkey)))
	  ;; f3
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d R" x)) (kbd (format "%s<f3>" tkey)))
	  ;; f4
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d S" x)) (kbd (format "%s<f4>" tkey)))
	  ;; f5
	  (define-key key-translation-map (kbd (format "M-[ 15 ; %d ~" x)) (kbd (format "%s<f5>" tkey)))
	  ;; f6
	  (define-key key-translation-map (kbd (format "M-[ 17 ; %d ~" x)) (kbd (format "%s<f6>" tkey)))
	  ;; f7
	  (define-key key-translation-map (kbd (format "M-[ 18 ; %d ~" x)) (kbd (format "%s<f7>" tkey)))
	  ;; f8
	  (define-key key-translation-map (kbd (format "M-[ 19 ; %d ~" x)) (kbd (format "%s<f8>" tkey)))
	  ;; f9
	  (define-key key-translation-map (kbd (format "M-[ 20 ; %d ~" x)) (kbd (format "%s<f9>" tkey)))
	  ;; f10
	  (define-key key-translation-map (kbd (format "M-[ 21 ; %d ~" x)) (kbd (format "%s<f10>" tkey)))
	  ;; f11
	  (define-key key-translation-map (kbd (format "M-[ 23 ; %d ~" x)) (kbd (format "%s<f11>" tkey)))
	  ;; f12
	  (define-key key-translation-map (kbd (format "M-[ 24 ; %d ~" x)) (kbd (format "%s<f12>" tkey)))
	  ;; f13
	  (define-key key-translation-map (kbd (format "M-[ 25 ; %d ~" x)) (kbd (format "%s<f13>" tkey)))
	  ;; f14
	  (define-key key-translation-map (kbd (format "M-[ 26 ; %d ~" x)) (kbd (format "%s<f14>" tkey)))
	  ;; f15
	  (define-key key-translation-map (kbd (format "M-[ 28 ; %d ~" x)) (kbd (format "%s<f15>" tkey)))
	  ;; f16
	  (define-key key-translation-map (kbd (format "M-[ 29 ; %d ~" x)) (kbd (format "%s<f16>" tkey)))
	  ;; f17
	  (define-key key-translation-map (kbd (format "M-[ 31 ; %d ~" x)) (kbd (format "%s<f17>" tkey)))
	  ;; f18
	  (define-key key-translation-map (kbd (format "M-[ 32 ; %d ~" x)) (kbd (format "%s<f18>" tkey)))
	  ;; f19
	  (define-key key-translation-map (kbd (format "M-[ 33 ; %d ~" x)) (kbd (format "%s<f19>" tkey)))
	  ;; f20
	  (define-key key-translation-map (kbd (format "M-[ 34 ; %d ~" x)) (kbd (format "%s<f20>" tkey)))

	  (setq x (+ x 1))
	  ))
      )
  )

```

## 替代方案

有很多Emacs的实现。GNU/Emacs 可能是最受欢迎的了。
更轻量的兼容性较好的Emacs可以在Arch仓库或在[AUR](https://aur.archlinux.org/)中找到。

### mg

mg（原来叫MicroGnuEmacs)，是用C语言实现的轻量级Emacs。

可以从{{ic|community}中安装mg

```
# pacman -S mg

```

或者从官方网站[page](http://homepage.boetes.org/software/mg/)中下载源代码。

### zile

引用官方网站[page](https://www.gnu.org/software/zile/)的描述，"GNU Zile is a lightweight Emacs clone. Zile is short for Zile Is Lossy Emacs. Zile has been written to be as similar as possible to Emacs; every Emacs user should feel at home.",意思是'GNU Zile'是一个轻量级的Emacs的克隆。Zile是'Zile Is Lossy Emacs'的缩写。 Zile的实现与Emacs如此相似以至于每个Emacs用户使用Zile一定会有一种宾至如归的感觉。

zile 可以在`extra`中找到

```
# pacman -S zile

```

最新的tarball可以在GNU的官方源[mirrors](http://ftp.sh.cvut.cz/MIRRORS/gnu/pub/gnu/zile/)中找到。

### uemacs

uemacs 是由Linus Torvalds定制的微型Emacs版本。 它可以在 [AUR](https://aur.archlinux.org/) 的 [uemacs](https://aur.archlinux.org/packages.php?ID=31502)中找到。

## 资源

*   [GNU Emacs home page](http://www.gnu.org/software/emacs/)
*   [GNU Emacs Manual](http://www.gnu.org/software/emacs/manual/emacs.html)
*   [Emacs Wiki](http://www.emacswiki.org/cgi-bin/wiki/)
*   [WikEmacs - a more readable, but less complete Emacs Wiki](http://wikemacs.org)
*   [Useful introduction to Emacs and its shortcuts](http://www2.lib.uchicago.edu/keith/tcl-course/emacs-tutorial.html)
*   [The Church of Emacs](http://www.dina.kvl.dk/~abraham/religion/)
*   [Official reference card](http://repo.or.cz/w/emacs.git/blob/HEAD:/etc/refcards/refcard.pdf)