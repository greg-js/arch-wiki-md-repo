[GNU Screen](http://www.gnu.org/s/screen/) 是一个封装器，允许命令行程序和启动它的shell相分离。例如，可以在X下的终端中启动一个程序，关闭X，而继续使用此程序。以下有技巧和提示。

如果想看教程，Gentoo的维基有一个很好的教程：[http://wiki.gentoo.org/wiki/Screen](http://wiki.gentoo.org/wiki/Screen)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 基础](#.E5.9F.BA.E7.A1.80)
    *   [2.1 常见命令](#.E5.B8.B8.E8.A7.81.E5.91.BD.E4.BB.A4)
*   [3 从窗口 1 开始](#.E4.BB.8E.E7.AA.97.E5.8F.A3_1_.E5.BC.80.E5.A7.8B)
*   [4 嵌套的 Screen 会话](#.E5.B5.8C.E5.A5.97.E7.9A.84_Screen_.E4.BC.9A.E8.AF.9D)
*   [5 消除残余的编辑文本](#.E6.B6.88.E9.99.A4.E6.AE.8B.E4.BD.99.E7.9A.84.E7.BC.96.E8.BE.91.E6.96.87.E6.9C.AC)
*   [6 使用 256 色](#.E4.BD.BF.E7.94.A8_256_.E8.89.B2)
*   [7 在 Rxvt-Unicode (urxvt) 中使用 256 色](#.E5.9C.A8_Rxvt-Unicode_.28urxvt.29_.E4.B8.AD.E4.BD.BF.E7.94.A8_256_.E8.89.B2)
*   [8 信息状态栏](#.E4.BF.A1.E6.81.AF.E7.8A.B6.E6.80.81.E6.A0.8F)
*   [9 关闭欢迎信息](#.E5.85.B3.E9.97.AD.E6.AC.A2.E8.BF.8E.E4.BF.A1.E6.81.AF)
*   [10 让标题栏动态显示 urxvt|xterm|aterm 窗口名称](#.E8.AE.A9.E6.A0.87.E9.A2.98.E6.A0.8F.E5.8A.A8.E6.80.81.E6.98.BE.E7.A4.BA_urxvt.7Cxterm.7Caterm_.E7.AA.97.E5.8F.A3.E5.90.8D.E7.A7.B0)
*   [11 使用 X 滚动机制](#.E4.BD.BF.E7.94.A8_X_.E6.BB.9A.E5.8A.A8.E6.9C.BA.E5.88.B6)
*   [12 添加 GRUB 条目来启动进入 Screen](#.E6.B7.BB.E5.8A.A0_GRUB_.E6.9D.A1.E7.9B.AE.E6.9D.A5.E5.90.AF.E5.8A.A8.E8.BF.9B.E5.85.A5_Screen)
*   [13 修正启动 screen 时 Midnight Commander 无反应的问题](#.E4.BF.AE.E6.AD.A3.E5.90.AF.E5.8A.A8_screen_.E6.97.B6_Midnight_Commander_.E6.97.A0.E5.8F.8D.E5.BA.94.E7.9A.84.E9.97.AE.E9.A2.98)
*   [14 See Also](#See_Also)

## 安装

可以用[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中的 [screen](https://www.archlinux.org/packages/?name=screen) 包来[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") GNU Screen.

## 基础

可以通过 `Ctrl+a` 和其他键来输入命令。通过 `~/.screenrc` 中的*escape*选项来改变 escape 键。例如：

```
escape ``

```

将 escape 键设为 ```。

### 常见命令

C-a ?

	列出命令和默认按键（非常重要）

C-a "

	窗口列表

C-a 0

	打开窗口 0

C-a A

	重命名当前窗口

C-a c

	创建新窗口

C-a S

	将当前区域划分为两个区域

C-a <TAB>

	将输入焦点转至下一区域

C-a C-a

	在当前区域和之前区域间转换

C-a <ESC>

	进入复制模式（用 `enter` 键来选择一段文本）

C-a ]

	粘贴文本

C-a Q

	关闭除当前区域外所有区域

C-a d

	从当前 screen 会话断开，并保持其运行。用 `screen -r` 来恢复。

## 从窗口 1 开始

默认的第一个窗口是 0 号。如果不想要窗口 0，而是从 1 号开始，将以下内容写入 `~/.screenrc`：

```
bind c screen 1
bind ^c screen 1
bind 0 select 10                                                            
screen 1

```

## 嵌套的 Screen 会话

在一个嵌套的 screen 会话中卡住是非常容易的。一个常见的情况是：你从一个 screen 会话内启动了一个 ssh 会话，在这个 ssh 会话中，你又启动了 screen。默认地，响应 C-a 命令的是最先启动的外层screen。如果要向内层 screen 输入命令，用 C-a a 加上你的命令。例如： C-a a d

	断开内层 screen 会话

C-a a K

	杀死内层 screen 会话

## 消除残余的编辑文本

当你在 screen 内打开文本编辑器再关掉它，文本内容仍然会在终端上显示。要解决这点，将下列内容加入 `~/.screenrc` 中：

```
altscreen on

```

## 使用 256 色

默认地，screen 使用 8 色终端模拟器。如果你用的是支持 256 色的终端，可以通过如下命令来支持更多的色彩：

```
term screen-256color

```

如果在 [xterm](/index.php/Xterm "Xterm") 中仍不能显示 256 色，试试下面的命令：

```
attrcolor b ".I"    # 允许加粗色彩--由于某些原因是必须的
termcapinfo xterm 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'   # 告诉screen如何设置颜色。AB 指背景，AF 指前景
defbce on    # 使用当前背景色来显示删除的字符

```

## 在 Rxvt-Unicode (urxvt) 中使用 256 色

如果你用的是[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中的 [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)，你可以将下面这行加入你的 `~/.screenrc` 来启用256色：

```
terminfo rxvt-unicode 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'

```

## 信息状态栏

默认的信息状态栏可能会有些简单。你可以使它变得更有用：

```
hardstatus off
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{B} %m-%d %{W} %c %{g}]'

```

## 关闭欢迎信息

将下面这行加入到 `~/.screenrc`：

```
startup_message off

```

## 让标题栏动态显示 urxvt|xterm|aterm 窗口名称

这非常简单，只是将你当前的 `hardstatus` 栏变成 `caption` 栏，并编辑对应项：

```
backtick 1 5 5 true
termcapinfo rxvt* 'hs:ts=\E]2;:fs=\007:ds=\E]2;\007'
hardstatus string "screen (%n: %t)"
caption string "%{= kw}%Y-%m-%d;%c %{= kw}%-Lw%{= kG}%{+b}[%n %t]%{-b}%{= kw}%+Lw%1`"
caption always

```

这会在你的终端模拟器标题栏显示 "screen (0 bash)" 之类的内容。标题栏提供日期、当前时间，并给 screen 窗口加上颜色。

## 使用 X 滚动机制

滚动缓存可以用 C-a [ 来查看。但是这很不方便。要使用滚动条，如 xterm 或 konsole，将下面这行加入 `~/.screenrc`：

```
termcapinfo xterm* ti@:te@

```

## 添加 GRUB 条目来启动进入 Screen

如果你主要使用 [X](/index.php/Xorg "Xorg")，但偶尔将Screen作为窗口管理器运行，这里有种通过为 Screen 添加 [GRUB](/index.php/GRUB "GRUB") 条目的方法。

GRUB 允许你指明想要的运行级别，因此在这里我们使用运行级别 4。复制一条合适的 GRUB 条目，并给内核选项表添加 `4`，像这样：

```
# (0) Arch Linux
title  Arch Linux Screen
root   (hd0,2)
kernel /vmlinuz-linux root=/dev/disk/your_disk ro acpi_no_auto_ssdt irqpoll 4
initrd /initramfs-linux.img

```

给 `/etc/inittab` 添加一些条目来指明哪些将在运行级别 4 下进行，将 <user> 换为你的用户名：

```
# GNU Screen on runlevel 4
scr2:4:respawn:/sbin/mingetty --autologin <user> tty1 linux

```

上面这行使用 mingetty 来[启动时自动登陆](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")。你需要安装[Official repositories (简体中文)|官方软件仓库]]中的 ([mingetty](https://aur.archlinux.org/packages/mingetty/)。inittab 的行分隔符是冒号。第一部分(scr*)仅仅是一个id。第二部分是运行级别：只在运行级别 4 下进行（默认地 4 没有被使用--3 是默认的字符界面登陆，5 是 X 登陆）。'Respawn' 让 init 重复这条命令（即自动登陆），如果用户注销。 当我们使用运行级别 4 时，我们需要没有其他任何程序在虚拟终端 1 下运行。所以将 `4`从 agetty 的第一行移去：

```
c1:235:respawn:/sbin/agetty -8 38400 vc/1 linux

```

一旦我们登陆，我们想要保证 screen 已经启动。将下列内容添加到你的`~/.bash_profile`：

```
vico="$(tty | grep -oE ....$)"
case "$vico" in
  tty1) TERM=screen; exec /usr/bin/screen -R arch;;
esac

```

这会检查当前运行级别，如果是 4 就在自动登陆后立即启动一个 screen 会话。

也可以改成 X 之后在一个虚拟终端里运行 screen，只需检查当前的 tty 而不是运行级别即可。下面是检查我们是否在虚拟终端 3 上：

```
vico="$(tty | grep -oE ....$)"
case "$vico" in
  vc/3) TERM=screen; exec /usr/bin/screen;;
esac

```

将 inittab/mingetty 设为在运行级别 5 下自动登陆到 vc/3 即可。

## 修正启动 screen 时 Midnight Commander 无反应的问题

这个问题在某些情况下（需要进一步检查）[old gpm bug](https://bugzilla.redhat.com/show_bug.cgi?id=168076) 会出现。所以在 screen 内运行 mc，会得到无反应的 screen 窗口。尝试在运行 mc 之前杀死 gpm 守护进程，或是在 `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` 中禁止 gpm。 In some cases (need deeper inspection) [old gpm bug](https://bugzilla.redhat.com/show_bug.cgi?id=168076) gets alive. So, then you try to run mc inside screen, you get a frozen screen window. Try to kill gpm daemon before starting mc and/or disable it in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`.

## See Also

*   [MacOSX Hints - Automatically using screen in your shell](http://www.macosxhints.com/article.php?story=20021114055617124)
*   [Gentoo Wiki - Tutorial for screen](http://wiki.gentoo.org/wiki/Screen)
*   [Arch Forums - Regarding 256 color issue with urxvt](https://bbs.archlinux.org/viewtopic.php?id=50647)
*   [Arch Forums - .screenrc configs with screenshots](https://bbs.archlinux.org/viewtopic.php?id=55618)
*   [tmux](/index.php/Tmux "Tmux"), another multiplexer