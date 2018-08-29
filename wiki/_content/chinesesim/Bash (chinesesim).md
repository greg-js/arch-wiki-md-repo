**翻译状态：** 本文是英文页面 [Bash](/index.php/Bash "Bash") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-10-15，点击[这里](https://wiki.archlinux.org/index.php?title=Bash&diff=0&oldid=228872)可以查看翻译后英文页面的改动。

**Bash** (Bourne-again Shell) 是一个来自 [GNU Project](/index.php/GNU_Project "GNU Project")的[命令行解释器](/index.php/Command-line_shell "Command-line shell")/编程语言。它的名字是向它的前身——很早以前的 Bourne shell 致敬。Bash 可以运行在大部分类 UNIX 操作系统中，包括 GNU/Linux。

## Contents

*   [1 调用](#.E8.B0.83.E7.94.A8)
    *   [1.1 登录外壳](#.E7.99.BB.E5.BD.95.E5.A4.96.E5.A3.B3)
    *   [1.2 交互式外壳](#.E4.BA.A4.E4.BA.92.E5.BC.8F.E5.A4.96.E5.A3.B3)
    *   [1.3 符合 POSIX](#.E7.AC.A6.E5.90.88_POSIX)
    *   [1.4 传统模式](#.E4.BC.A0.E7.BB.9F.E6.A8.A1.E5.BC.8F)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 配置文件在启动时的引用顺序](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E5.9C.A8.E5.90.AF.E5.8A.A8.E6.97.B6.E7.9A.84.E5.BC.95.E7.94.A8.E9.A1.BA.E5.BA.8F)
    *   [2.2 外壳和环境变量](#.E5.A4.96.E5.A3.B3.E5.92.8C.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
*   [3 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
*   [4 别名](#.E5.88.AB.E5.90.8D)
*   [5 函数](#.E5.87.BD.E6.95.B0)
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 自定义提示符](#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.8F.90.E7.A4.BA.E7.AC.A6)
    *   [6.2 自动命令补全](#.E8.87.AA.E5.8A.A8.E5.91.BD.E4.BB.A4.E8.A1.A5.E5.85.A8)
        *   [6.2.1 高级的补全方法](#.E9.AB.98.E7.BA.A7.E7.9A.84.E8.A1.A5.E5.85.A8.E6.96.B9.E6.B3.95)
        *   [6.2.2 更快的补全操作](#.E6.9B.B4.E5.BF.AB.E7.9A.84.E8.A1.A5.E5.85.A8.E6.93.8D.E4.BD.9C)
    *   [6.3 命令未找到时的钩子拓展(HOOKS)](#.E5.91.BD.E4.BB.A4.E6.9C.AA.E6.89.BE.E5.88.B0.E6.97.B6.E7.9A.84.E9.92.A9.E5.AD.90.E6.8B.93.E5.B1.95.28HOOKS.29)
    *   [6.4 终端中禁用 Ctrl+z](#.E7.BB.88.E7.AB.AF.E4.B8.AD.E7.A6.81.E7.94.A8_Ctrl.2Bz)
    *   [6.5 登出后清空屏幕](#.E7.99.BB.E5.87.BA.E5.90.8E.E6.B8.85.E7.A9.BA.E5.B1.8F.E5.B9.95)
    *   [6.6 ASCII的艺术, fortunes和cowsay](#ASCII.E7.9A.84.E8.89.BA.E6.9C.AF.2C_fortunes.E5.92.8Ccowsay)
    *   [6.7 ASCII历史日历](#ASCII.E5.8E.86.E5.8F.B2.E6.97.A5.E5.8E.86)
    *   [6.8 修正窗口大小调整时的换行](#.E4.BF.AE.E6.AD.A3.E7.AA.97.E5.8F.A3.E5.A4.A7.E5.B0.8F.E8.B0.83.E6.95.B4.E6.97.B6.E7.9A.84.E6.8D.A2.E8.A1.8C)
    *   [6.9 Bash历史补全](#Bash.E5.8E.86.E5.8F.B2.E8.A1.A5.E5.85.A8)
*   [7 资源](#.E8.B5.84.E6.BA.90)

## 调用

Bash调用方式的不同会导致Bash运行方式的不同。下面是在不同模式下运行的Bash的描述。

### 登录外壳

如果Bash由在tty中的`登录`, [SSH](/index.php/SSH "SSH") 守护进程, 或者其它类似的方式而派生出来, 它就被称为登录外壳(shell)。你可以使用命令行选项`-l` 或者 `--login` 来使用这个种模式。

### 交互式外壳

如果Bash在启动的时候既没有使用 `-c` 选项也没有使用非选项参数，那我们就认为它是一个交互式外壳，同时Bash的标准输出和标准错误被链接到终端上。

### 符合 POSIX

通过在Bash启动时使用 `--posix` 命令行参数或者在启动后执行 ‘`set -o posix`’ 来使Bash在增强的POSIX标准下运行。

### 传统模式

在Arch下 `/bin/sh` (过去是Bourne shell)被符号链接至`/bin/bash`。

如果以命令名`sh`来调用Bash, Bash会尽可能地模仿历史版本的`sh`的启动过程，包括 POSIX 兼容性。

在传统模式下登陆运行的shell来源于/etc/profile，然后是~/.profile。

## 配置

通过如下配置文件进行配置:

*   `/etc/profile`
*   `~/.bash_profile`
*   `~/.bash_login`
*   `~/.profile`
*   `/etc/bash.bashrc` (*非标准*: 只对部分发行版有效，Arch包含在这部分中)
*   `~/.bashrc`
*   `~/.bash_logout`

常用的配置文件：

*   `/etc/profile`被所有兼容Bourne shell的shell在登录时引用。它在登录时建立了环境并且加载了应用程序特定(`/etc/profile.d/*.sh`)的设置。
*   `~/.profile`: 此文件在启动一个交互式的登录shell时被Bash所读入和引用。
*   `~/.bashrc` 此文件在启动一个交互式的非登录shell时被Bash所读入和引用。比如当你从桌面环境中打开一个虚拟控制台时。这个文件在用户自定义自己的shell环境时特别有用。

### 配置文件在启动时的引用顺序

这些文件在不同的情形下被Bash所引用。

*   如果交互式+登录shell → `/etc/profile` 然后按以下顺序读取 `~/.bash_profile`, `~/.bash_login`, and `~/.profile`
    *   Bash会在退出时引用{ic|~/.bash_logout}}。
*   如果交互式+非登录shell → `/etc/bash.bashrc` 然后 `~/.bashrc`
*   如果交互式+传统模式 → `/etc/profile` 然后 `~/.profile`

但是，在Arch下，默认的:

*   `/etc/profile` (间接地) 引用 `/etc/bash.bashrc`
*   `/etc/skel/.bash_profile` Arch鼓励用户将`/etc/skel/.bash_profile`复制到 `~/.bash_profile`, 并引用 `~/.bashrc`

这意味着 `/etc/bash.bashrc` 和 `~/.bashrc` 将会为所有的交互式shell所执行, 不管它是不是登录shell.

用户dotfiles的例子可以在`/etc/skel/`中被找到。

**注意:** 传统模式指以`sh`来调用

### 外壳和环境变量

Bash的行为和通过它来运行的程序会被许多的环境变量所影响。环境变量被用于储存有用的值比如命令搜索路径，或者使用哪个浏览器。当一个新的shell或者脚本被执行时，这个shell会继承它的父shell的变量, 因此这个shell会以内部的shell变量启动[[1]](http://www.kingcomputerservices.com/unix_101/understanding_unix_shells_and_environment_variables.htm)。

这些Bash中的shell变量可以被导出以变成环境变量:

```
VARIABLE=content
export VARIABLE

```

或者：

```
export VARIABLE=content

```

环境变量依照惯例放置在`~/.profile`或者`/etc/profile`，这样所有兼容Bourne shell的shell都可以使用。

参阅[Environment variables](/index.php/Environment_variables "Environment variables")以获得更加全面的信息。

## 命令行

Bash的命令行由一个叫做[Readline](/index.php/Readline "Readline")的分离库来管理。Readline提供了很多Bash命令行交互的快捷键，比如说，光标单词间向前向后移动，删除单词等等。管理输入[历史](/index.php/Readline#History "Readline")也是Readline的职责。最后一点也非常重要, 它允许你创造[宏](/index.php/Readline#Macros "Readline")。

## 别名

[alias](https://en.wikipedia.org/wiki/alias "wikipedia:alias")是一个命令, 它让用其它字符串替代一句话成为可能。这个命令常常被用来缩短系统命令，或者用来将默认参数加入到常用命令中。

用户个人的别名(alias)最好保存在`~/.bashrc`, 而系统级的别名(这些别名会影响所有用户)存放在`/etc/bash.bashrc`。

## 函数

Bash也支持函数。下面这个函数可以解压多种类型的压缩文件。将下面这个函数加入`~/.bashrc`中并以这个语法`extract <file1> <file2> ...`使用它。

```
~/.bashrc

```

```
extract() {
    local c e i

    (($#)) || return

    for i; do
        c=''
        e=1

        if [[ ! -r $i ]]; then
            echo "$0: file is unreadable: \`$i'" >&2
            continue
        fi

        case $i in
        *.t@(gz|lz|xz|b@(2|z?(2))|a@(z|r?(.@(Z|bz?(2)|gz|lzma|xz)))))
               c='bsdtar xvf';;
        *.7z)  c='7z x';;
        *.Z)   c='uncompress';;
        *.bz2) c='bunzip2';;
        *.exe) c='cabextract';;
        *.gz)  c='gunzip';;
        *.rar) c='unrar x';;
        *.xz)  c='unxz';;
        *.zip) c='unzip';;
        *)     echo "$0: unrecognized file extension: \`$i'" >&2
               continue;;
        esac

        command $c "$i"
        e=$?З
    done

    return $e
}

```

**注意:** [Bash](/index.php/Bash "Bash")用户应该确保extglob功能被打开: `shopt -s extglob`, 比如说将它加入到`.bashrc`。如果使用[Bash completion](/index.php/Bash#Advanced_completion "Bash")，这个功能将默认被打开。 [Zsh](/index.php/Zsh "Zsh")用户应该这样做: 执行`setopt kshglob`来替代上面的操作。

另一个实现方式就是安装*unp*包。

通常进入到另一个目录后我们会用ls来列出目录下的文件。所以我们可以写一个函数来同时做这两件事情。 这个例子中我们把函数命名为'cl'并且会在给定的目录不存在时报错。

```
~/.bashrc

```

```
cl()
{
if [ -d $1 ]; then
cd $1
ls
else
echo "bash: cl: $1: Directory not found"
fi
}

```

当然ls命令可以被改变以适应你的需求, 比如'ls -hall --color=auto'。

更多bash函数的例子在[这里。](https://bbs.archlinux.org/viewtopic.php?id=30155)

## 提示与技巧

### 自定义提示符

Bash提示符由变量`$PS1`控制。为了让提示符色彩丰富些, 首先要注释掉默认的`$PS1`:

```
#PS1='[\u@\h \W]\$ '

```

然后加入下面这句:

```
PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\] '

```

`$PS1`将shell改变成红色的名称和绿色的控制台文本，这对一个root权限的bash提示符十分有用。欲了解更多关于自定义shell的内容, 参阅[Color Bash Prompt (简体中文)](/index.php/Color_Bash_Prompt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Color Bash Prompt (简体中文)")。

### 自动命令补全

当你键入一些命令比如sudo时，自动补全功能(在键盘上按`Tab`两次)显得尤其有用。

你可以加入以下内容到`~/.bashrc`文件中以实现补全功能:

```
complete -cf your_command

```

比如说，为了激活sudo和man之后的自动补全功能，可以这样:

```
complete -cf sudo
complete -cf man

```

#### 高级的补全方法

尽管Bash原生支持基本的文件名，命令和变量的自动补全， 我们仍然可以通过一些方法扩充它的功能。

包[bash-completion](https://www.archlinux.org/packages/?name=bash-completion)通过将自动补全扩充到一个更加广泛的的命令和他们的选项中去使自动补全在shell中的表现更加强大。激活高级补全的方法也非常简单，只需要安装这个包就可以：

```
# pacman -S bash-completion

```

启动一个新的shell，然后它由于配置文件`/etc/bash.bashrc`的作用就会自动激活补全了。

**注意:** 如果你加入了类似于上文提到的"complete -cf sudo"的设置，并且在Bash自动补全中出现问题，尝试删除那些设置语句。

**注意:** 通常你使用过去的这些命令操作"$ ls file.*<tab><tab>"来补全命令语句，但这可能不会正常的工作，除非你为需要退回到正常全局补全的程序执行下面的命令"$ compopt -o bashdefault <prog>"。参见 [https://bbs.archlinux.org/viewtopic.php?id=128471](https://bbs.archlinux.org/viewtopic.php?id=128471) 和 [https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html)

#### 更快的补全操作

通过加入下面这句话到readline默认的初始化文件(`~/.inputrc`或者`/etc/inputrc`中):

```
set show-all-if-ambiguous on

```

之后没有必要敲击`Tab`(默认绑定)两次来产生可能的补全列表(包括有多种补全可能或者没有补全可能时), 因为一次敲击就可以实现。 作为另外一种选择, 产生补全列表只有在没有可能的补全下(比如, 没有多种补全可能时), 将上面的设置语句替换成下面这条:

```
set show-all-if-unmodified on

```

### 命令未找到时的钩子拓展(HOOKS)

包[pkgfile](/index.php/Pkgfile "Pkgfile")包括一个"command not found"的钩子拓展，这个钩子拓展将在你键入未识别命令时自动搜索[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")。然后显示下面的信息:

 `$ abiword` 
```
abiword may be found in the following packages:
  extra/abiword 2.8.6-7	usr/bin/abiword

```

AUR包提供了另外一个"command not found"钩子拓展。[command-not-found](https://aur.archlinux.org/packages/command-not-found/), 它会产生像这样的输出:

 `$ abiword` 
```
The command 'abiword' is been provided by the following packages:
abiword (2.8.6-7) from extra
	[ abiword ]
abiword (2.8.6-7) from staging
	[ abiword ]
abiword (2.8.6-7) from testing
	[ abiword ]

```

### 终端中禁用 Ctrl+z

你可以为你的命令行界面关闭`Ctrl+z` (暂停/关闭你的命令行界面程序)的功能通过在这个脚本中包装命令

```
#!/bin/bash
trap "" 20
/path_to_your_application/

```

例子:

```
#!/bin/bash
trap "" 20
/usr/bin/adom

```

有了这个例子脚本，当你在玩Adom(游戏)要按`Shift+z`组合键时不小心按下了`Ctrl+z`组合键，你的游戏就不会停止运行了。其实什么都会发生因为我们已经禁用了`Ctrl+z`。

### 登出后清空屏幕

当登出虚拟终端时，为了实现清屏操作，可以加入下面的语句到`~/.bash_logout`:

```
clear
reset

```

### ASCII的艺术, fortunes和cowsay

有了色彩，系统信息和ASCII符号，我们就可以让Bash在登录时展示出一幅ASCII的艺术品。ASCII图片可以在网上找到并粘贴到一个text文件中， 或者通过涂鸦产生。images can be found online and pasted into a text file, or generated from scratch. To set the image to display in a terminal on login, 将下面的字符串

```
cat /path/to/text/file

```

加入`~/.bashrc`的顶部。

Bash也可以随机显示一些伤感的，激动人心的，可笑的，讽刺的短句。你可以`extra`库中下载安装[fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod)包来显示一个例子。

 `$ fortune` 
```
It is Texas law that when two trains meet each other at a railroad crossing,
each shall come to a full stop, and neither shall proceed until the other

has gone.
```

如果要使短句在登录时随机出现，只需要将下面这句话

```
command fortune

```

加入到`~/.bashrc`的顶部。

**Note:** 默认情况下，`fortune`显示的引用短语都是无伤大雅的。尽管如此，包里面确实包含了一些无礼的言论，它们放在`/usr/share/fortune/off`。你可以查看man手册已得到更多的信息。

这两个功能可以合并在一起，通过这个程序[cowsay](https://www.archlinux.org/packages/?name=cowsay)。改变`~/.bashrc`的顶部行来读入下面的命令

```
command cowsay $(fortune)

```

或者

```
command cowthink $(fortune)

```

```
The earth is like a tiny grain of sand, 
only much, much heavier.                
----------------------------------------- 
       \   ^__^
        \  (oo)\_______
           (__)\       )\/\
               ||----w |
               ||     ||

```

ASCII图像通过`.cow`txt文件来生成，它位于`/usr/share/cows`中，并且所有的主题可以都可以通过这个命令`cowsay -l`来列出。这些文件可以依照用户的喜好进行编辑；自定义的图片可以通过涂鸦和在网上寻找的方式获得。创作一个自定义cow文件的最简方法就是在文本编辑器打开一个存在的`.cow`文件，再将浏览器中的ASCII图片复制粘贴到编辑器中，另取名保存即可。你可以用下面的命令测试自定义文件

```
# cowsay -f `cowfile` $(fortune)

```

这个能产生一幅华丽的图画，命令的使用也更加复杂。如果需要更加专业的例子，访问[这里。](http://bambambambam.wordpress.com/2009/07/04/futurama-ascii-with-slashdot-header-quotes-in-your-terminal/) 另外一个例子，这个例子使用了随机产生的cow，随机的脸部表情，并且把fortunes产生文字和图片漂亮的包装在一起。

```
fortune -a | fmt -80 -s | cowsay -$(shuf -n 1 -e b d g p s t w y) -f $(shuf -n 1 -e $(cowsay -l | tail -n +2)) -n

```

```
 ________________________________________ 
( Fry: I must be a robot. Why else would )
( human women refuse to date me?         )
---------------------------------------- 
       o
         o
           o  
              ,'``.._   ,'``.
             :,--._:)\,:,._,.:
             :`--,*@@@:`...';\* 
              `,'@@@@@@@`---'@@`.     
              /@@@@@@@@@@@@@@@@@:
             /@@@@@@@@@@@@@@@@@@@\
           ,'@@@@@@@@@@@@@@@@@@@@@:\.___,-.
          `...,---'``````-..._@@@@|:@@@@@@@\
            (                 )@@@;:@@@@)@@@\  _,-.
             `.              (@@@//@@@@@@@@@@`'@@@@\
              :               `.//@@)@@@@@@)@@@@@,@;
              |`.            _,'/@@@@@@@)@@@@)@,'@,'
              :`.`-..____..=:.-':@@@@@.@@@@@_,@@,'
             ,'\ ``--....-)='    `._,@@\    )@@@'``._
            /@_@`.       (@)      /@@@@@)  ; / \ \`-.'
           (@@@`-:`.     `' ___..'@@_,-'   |/   `.)
            `-. `.`.``-----``--,@@.'
              |/`.\`'        ,',');
                  `         (/  (/

```

**注意:** 如果你想要一幅全色彩的类似于cowsay的艺术图，最好的选择就是[ponysay](https://www.archlinux.org/packages/?name=ponysay)，通过运行命令'ponysay "command or fortune command"'，这个包会在你的终端(在X11或者在TTY中你会获得256全色的ponies)里面显示全色彩的小型马(ponies)图片(版本1.1时超过220种)，命令'ponysay -l'显示完整的小型马(ponies)的列表。 存在于AUR的一种工具可以用来创作更多的小型马(ponies)的图片(也可创造其它类型)，这个工具叫做[util-say-git](https://aur.archlinux.org/packages/util-say-git/)，而这些新的档案需要存储在$HOME/.local/share/ponysay/ponies和$HOME/.local/share/ponysay/ttyponies，它们分别用在桌面和TTy中。

### ASCII历史日历

执行下面命令以安装[calendar](http://www.openbsd.org/cgi-bin/man.cgi?query=calendar&sektion=1)文件在你的`~/.calendar`目录中:

```
$ mkdir -p ~/.calendar
$ curl -o calendar.rpm [http://download.fedora.redhat.com/pub/epel/5/x86_64/calendar-1.25-4.el5.x86_64.rpm](http://download.fedora.redhat.com/pub/epel/5/x86_64/calendar-1.25-4.el5.x86_64.rpm)
$ rpm2cpio calendar.rpm | bsdtar -C ~/.calendar --strip-components=4 -xf - ./usr/share/c*

```

这些会随后显示日历项

```
$ sed -n "/$(date +%m\\/%d\\\|%b\*\ %d)/p" $(find ~/.calendar /usr/share/calendar -maxdepth 1 -type f -name 'c*' 2>/dev/null);

```

### 修正窗口大小调整时的换行

加入你在vi中调整了你的xterm大小，Bash并不会得到resize信号，所以你键入的文本就不会正确的换行，于是它们会重叠提示符。

在`/etc/bash.bashrc` (来自Debian)用下面的设置 :

```
# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

```

### Bash历史补全

Bash历史补全功能绑定到方向键上(下，上)：

```
# ~/.bashrc
bind '"\e[A": history-search-backward'
bind '"\e[B": history-search-forward'

```

或者放在`~/.inputrc`:

```
# ~/.inputrc
"\e[A": history-search-backward
"\e[B": history-search-forward

```

更多的信息在[Readline#History](/index.php/Readline#History "Readline")和[[2]](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)

## 资源

*   [Advanced Bash Scripting Guide](http://tldp.org/LDP/abs/html/) - Very good resource regarding shell scripting using bash
*   [Bash Reference Manual](http://www.gnu.org/software/bash/manual/bashref.html) - Official reference (654K)
*   [Bash Hackers Wiki](http://wiki.bash-hackers.org/doku.php) - Excellent Bash Wiki
*   [Bashscripts.org](http://bashscripts.org) - Forum for bash coders.
*   [Bash Scripting by Example](http://www.ibm.com/developerworks/linux/library/l-bash.html)
*   [Completion Guide](http://www.caliban.org/bash)
*   [Greg's Wiki](http://wooledge.org/mywiki/BashFaq) - Highly recommended
*   [man page](http://www.gnu.org/software/bash/manual/bash.html)
*   [Quote Tutorial](http://www.grymoire.com/Unix/Quote.html)
*   [irc://irc.freenode.net#bash](irc://irc.freenode.net#bash) - Active and friendly Internet Relay Chat channel for Bash.
*   [http://chakra-project.org/wiki/index.php/Startup_files](http://chakra-project.org/wiki/index.php/Startup_files)
*   [The Bourne-Again Shell](http://www.aosabook.org/en/bash.html) - The third chapter of *The Architecture of Open Source Applications*
*   [How to change the title of an xterm](http://tldp.org/HOWTO/Xterm-Title-4.html)