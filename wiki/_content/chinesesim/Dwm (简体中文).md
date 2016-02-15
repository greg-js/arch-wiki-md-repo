[dwm](http://dwm.suckless.org/)是[X](/index.php/X "X")下的一个动态窗口管理器。它用平铺的、栈式的和全屏的布局方式，借助一些可选的补丁还可以实现其他的布局。布局可以动态得改变，为程序提供最优的环境和性能。dwm特别轻量快速，用C语言编写，被设计的目标是控制在2000行以下的代码。在xrandr和Xinerama支持下可实现multi-head。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 需求](#.E9.9C.80.E6.B1.82)
    *   [1.2 用ABS下载安装脚本](#.E7.94.A8ABS.E4.B8.8B.E8.BD.BD.E5.AE.89.E8.A3.85.E8.84.9A.E6.9C.AC)
    *   [1.3 编译和安装](#.E7.BC.96.E8.AF.91.E5.92.8C.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 方法一：使用 ABS（推荐）](#.E6.96.B9.E6.B3.95.E4.B8.80.EF.BC.9A.E4.BD.BF.E7.94.A8_ABS.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)
        *   [2.1.1 自定义config.h](#.E8.87.AA.E5.AE.9A.E4.B9.89config.h)
        *   [2.1.2 注意](#.E6.B3.A8.E6.84.8F)
    *   [2.2 方法二：使用Mercurial（高级）](#.E6.96.B9.E6.B3.95.E4.BA.8C.EF.BC.9A.E4.BD.BF.E7.94.A8Mercurial.EF.BC.88.E9.AB.98.E7.BA.A7.EF.BC.89)
*   [3 启动dwm](#.E5.90.AF.E5.8A.A8dwm)
*   [4 配置状态条](#.E9.85.8D.E7.BD.AE.E7.8A.B6.E6.80.81.E6.9D.A1)
    *   [4.1 基本状态条](#.E5.9F.BA.E6.9C.AC.E7.8A.B6.E6.80.81.E6.9D.A1)
    *   [4.2 Conky状态条](#Conky.E7.8A.B6.E6.80.81.E6.9D.A1)
*   [5 基本用法](#.E5.9F.BA.E6.9C.AC.E7.94.A8.E6.B3.95)
    *   [5.1 使用dmenu](#.E4.BD.BF.E7.94.A8dmenu)
    *   [5.2 控制窗口](#.E6.8E.A7.E5.88.B6.E7.AA.97.E5.8F.A3)
        *   [5.2.1 将窗口移动到另一个tag](#.E5.B0.86.E7.AA.97.E5.8F.A3.E7.A7.BB.E5.8A.A8.E5.88.B0.E5.8F.A6.E4.B8.80.E4.B8.AAtag)
        *   [5.2.2 关闭窗口](#.E5.85.B3.E9.97.AD.E7.AA.97.E5.8F.A3)
        *   [5.2.3 窗口布局](#.E7.AA.97.E5.8F.A3.E5.B8.83.E5.B1.80)
    *   [5.3 退出dwm](#.E9.80.80.E5.87.BAdwm)
*   [6 扩展使用](#.E6.89.A9.E5.B1.95.E4.BD.BF.E7.94.A8)
    *   [6.1 补丁和增加的窗口布局（tiling modes）](#.E8.A1.A5.E4.B8.81.E5.92.8C.E5.A2.9E.E5.8A.A0.E7.9A.84.E7.AA.97.E5.8F.A3.E5.B8.83.E5.B1.80.EF.BC.88tiling_modes.EF.BC.89)
        *   [6.1.1 实现为每个标签定制布局](#.E5.AE.9E.E7.8E.B0.E4.B8.BA.E6.AF.8F.E4.B8.AA.E6.A0.87.E7.AD.BE.E5.AE.9A.E5.88.B6.E5.B8.83.E5.B1.80)
    *   [6.2 解决模拟终端窗口缝隙问题](#.E8.A7.A3.E5.86.B3.E6.A8.A1.E6.8B.9F.E7.BB.88.E7.AB.AF.E7.AA.97.E5.8F.A3.E7.BC.9D.E9.9A.99.E9.97.AE.E9.A2.98)
        *   [6.2.1 Urxvt](#Urxvt)
    *   [6.3 在不登出和退出程序程序的情况下重启dwm](#.E5.9C.A8.E4.B8.8D.E7.99.BB.E5.87.BA.E5.92.8C.E9.80.80.E5.87.BA.E7.A8.8B.E5.BA.8F.E7.A8.8B.E5.BA.8F.E7.9A.84.E6.83.85.E5.86.B5.E4.B8.8B.E9.87.8D.E5.90.AFdwm)
    *   [6.4 把右Alt键作为Mod4（Win键）使用](#.E6.8A.8A.E5.8F.B3Alt.E9.94.AE.E4.BD.9C.E4.B8.BAMod4.EF.BC.88Win.E9.94.AE.EF.BC.89.E4.BD.BF.E7.94.A8)
    *   [6.5 防止鼠标下的程序自动获取焦点](#.E9.98.B2.E6.AD.A2.E9.BC.A0.E6.A0.87.E4.B8.8B.E7.9A.84.E7.A8.8B.E5.BA.8F.E8.87.AA.E5.8A.A8.E8.8E.B7.E5.8F.96.E7.84.A6.E7.82.B9)
    *   [6.6 添加个性的快捷键绑定](#.E6.B7.BB.E5.8A.A0.E4.B8.AA.E6.80.A7.E7.9A.84.E5.BF.AB.E6.8D.B7.E9.94.AE.E7.BB.91.E5.AE.9A)
    *   [6.7 解决Java程序不正常的问题](#.E8.A7.A3.E5.86.B3Java.E7.A8.8B.E5.BA.8F.E4.B8.8D.E6.AD.A3.E5.B8.B8.E7.9A.84.E9.97.AE.E9.A2.98)
*   [7 资源](#.E8.B5.84.E6.BA.90)

## 安装

这里建议用[makepkg](/index.php/Makepkg "Makepkg")从[ABS](/index.php/ABS "ABS")安装。这样你可以在稍后的时间简单地重新配置。如果你只是想安装试用一下的话，简单地安装：

```
# pacman -S dwm

```

注意这样是不灵活的，因为dwm的配置要通过修改它的源码来实现。所以接下来的文章假定你从源码编译dwm。

你可能很想同时安装[dmenu](/index.php/Dmenu "Dmenu")，一个X下轻量级的动态菜单：

```
# pacman -S dmenu

```

### 需求

你需要用 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 里的基本编程工具来编译dwm，并且需要用 [abs](https://www.archlinux.org/packages/?name=abs) 来获得安装脚本：

```
# pacman -S base-devel abs

```

### 用ABS下载安装脚本

如果需要的包都准备好了，可以用ABS从仓库里获得最新的安装脚本了：

1.  abs community/dwm

最后，把dwm安装脚本从ABS树里拷贝到一个临时目录，例如：

```
$ cp -r /var/abs/community/dwm ~/dwm

```

### 编译和安装

用 `cd` 进入到编译的目录（上边例子里的`~/dwm`），然后运行：

```
$ makepkg -i

```

这会编译并安装dwm，如果有问题请仔细输出信息。

**Tip:** 如果你以后不更改 (`~/dwm`) 目录, 你可以在以后的时间继续用它来对配置文件做进一步的修改。

## 配置

就像上边提到的那样，dwm是在编译时配置的，确切地说就是修改`config.h`和`config.mk`。然而它提供了一个很好的初始配置，对一些有经验的用户，它是很好调整的。

### 方法一：使用 ABS（推荐）

在这里修改dwm是非常简单的。

#### 自定义config.h

进入[安装过程](#.E5.AE.89.E8.A3.85)中的dwm的源码目录；也就是上边的`~/dwm`。里边的`config.h` 存放着通常的配置信息。这个文件里的大多数配置都很好理解，但其他的可能比较有个性。关于这些配置的详细信息可以查阅[dwm website](http://www.suckless.org/dwm/)。

**Note:** 要确保修改之前保存一份config.h的备份，以防修改中发生错误。

一旦修改完成了，更新[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")里的md5sums:

```
$ makepkg -g >> PKGBUILD

```

这样会避免因为和官方的config.h文件不一样导致校验值错误。

现在，编译并重新安装：

```
$ makepkg -efi

```

假定配置是有效的，这条命令会编译和重新安装dwm，如果出问题了，请仔细查看输入内容获得详细信息。

最后，重启dwm来使用新的配置。

#### 注意

从现在开始，我们不必每次都更新`config.h`的md5sums了，因为会很频繁，我们只需要用`--skipinteg`选项来跳过校验。

```
$ makepkg -efi --skipinteg

```

在往dwm的启动脚本里添加几行后，我们可以[在不登出和退出程序程序的情况下重启dwm](#.E5.9C.A8.E4.B8.8D.E7.99.BB.E5.87.BA.E5.92.8C.E9.80.80.E5.87.BA.E7.A8.8B.E5.BA.8F.E7.A8.8B.E5.BA.8F.E7.9A.84.E6.83.85.E5.86.B5.E4.B8.8B.E9.87.8D.E5.90.AFdwm)。

### 方法二：使用Mercurial（高级）

上游的dwm是用[git](http://git-scm.com)版本控制系统来维护的，在[suckless.org](http://git.suckless.org/dwm)。熟悉Mercurial的人会发现用它来维护配置和补丁会更方便。

## 启动dwm

可以用`startx`或者[SLIM](/index.php/SLIM "SLIM")登陆管理器来启动dwm，只需要在`~/.xinitrc`添加:

```
exec dwm

```

对于[GDM](/index.php/GDM "GDM")，在`~/.Xclients`添加上述内容，然后在会话菜单里选择”运行XClient脚本”。

## 配置状态条

dwm使用根窗口名称来显示状态条信息，可以使用`xsetroot -name`来改变。

### 基本状态条

这个例子显示[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601 "wikipedia:ISO 8601")格式的日期。把下边的内容添加到`~/.xinitrc`或者`~/.Xclients`，或者可以从GDM-3的讨论页中获得更多细节：

```
while true; do
   xsetroot -name "$( date +"%F %R" )"
   sleep 1m    # Update time every minute
done &
exec dwm

```

这是个笔记本使用的，依赖[acpi](https://www.archlinux.org/packages/?name=acpi)包来显示电池信息：

```
while true ; do
    xsetroot -name "$( acpi -b | awk '{ print $3, $4 }' | tr -d ',' )"
    sleep 1m
done &
exec dwm

```

这个脚本显示电池剩余电量和充电状态，用awk命令过滤acpi输出的无用信息，然后用tr去除逗号。

另一个方式是根据电池的状态选择性地输出信息：

```
while true; do
        batt=$(LC_ALL=C acpi -b)

        case $batt in
        *Discharging*)
                batt="${batt#* * * }"
                batt="${batt%%, *} "
                ;;
        *)
                batt=""
                ;;
        esac

        xsetroot -name "$batt$(date +%R)"

        sleep 60
done &

exec dwm

```

最后，要确保在`~/.xinitrc`或者`~/.Xclients`里只有一个dwm实例, 所以把整合起来应该像这样：

```
~/.setbg
autocutsel &
termirssi &
urxvt &

while true; do
   xsetroot -name "$(date +"%F %R")"
   sleep 1m    # Update time every minute
done &
**exec dwm**

```

这是另一个显示alsa音量和电池状态的例子。它一直显示到系统退出为止。

```
#set statusbar
while true
do
   if acpi -a | grep off-line > /dev/null; then
       xsetroot -name "Bat. $( acpi -b | awk '{ print $4 " " $5 }' | tr -d ',' ) | Vol. $(amixer get Master | tail -1 | awk '{ print $5}' | tr -d '[]') | $(date +"%a, %b %d %R")"
   else
       xsetroot -name "Vol. $(amixer get Master | tail -1 | awk '{ print $5}' | tr -d '[]') | $(date +"%a, %b %d %R")"
   fi
   sleep 1s   
done &

```

### Conky状态条

Conky可以使用`xsetroot -name`来往状态条里输出信息:

```
conky | while read -r; do xsetroot -name "$REPLY"; done &
exec dwm

```

要想这样做，conky需要只往终端里输出文本。这是个应用于dual core CPU的简单conkyrc，显示几个状态信息：

```
out_to_console yes
out_to_x no
background no
update_interval 2
total_run_times 0
use_spacer none

TEXT
$mpd_smart :: ${cpu cpu1}% / ${cpu cpu2}%  ${loadavg 1} ${loadavg 2 3} :: ${acpitemp}c :: $memperc% ($mem) :: ${downspeed eth0}K/s ${upspeed eth0}K/s :: ${time %a %b %d %I:%M%P}

```

## 基本用法

### 使用dmenu

Dmenu是dwm的一个有用的扩展。它不是一个单独的列表式菜单，而是生成一个可执行文件的列表并根据输入进行自动补全。比起许多程序启动器，它能与dwm更好地整合。

可以按 `Mod1` + `P` 来启动Dmenu（`Mod1` 缺省是 `Alt` ）。当然你也可以按自己的喜好改变它。然后只需要在上边出现的工具条中输入你想运行的程序的前几个字母，也可以按左右箭头在进行选择，按回车键完成。

更详细的信息请查阅 [dmenu](/index.php/Dmenu "Dmenu").

### 控制窗口

#### 将窗口移动到另一个tag

将当前的活动窗口移到其他的标签页：`Shift` + `Mod1` + `x`, 其中的x是其他的标签页的序号，如果x是5，则表示将当前的活动窗口移到第5号标签页上去。`Mod1` 缺省是 `Alt` 键，这个键值可以在config.h中定义。

#### 关闭窗口

关闭当前的活动窗口： `Shift` + `Mod1` + `C`.

#### 窗口布局

dwm缺省工作在平铺模式。当新窗口不断出现在同一个标签页时，窗口会越来越小。所有窗口会占满整个屏幕（除了目录条）。然而还有其他两种模式：浮动和单页模式。浮动模式对非平铺窗口管理器用户来说更熟悉，它允许用户重新按自己需要摆放窗口。单页模式会让一个窗口在最上边。

要切换到浮动模式，只需要按`Mod1` + `F`。`Mod1`缺省是 `Alt`。如果你看到标签页右上角有X>这样的标志，就进行了浮动模式。

切换到单页模式，按 `Mod1` + `M`。检查上否在单页模式，你会看到[M]标志（如果当前标签页无窗口），或者[n]（n是打开窗口的编号）。

回来平铺模式，按`Mod1` + `T`，你会看到 []= 这样的标志。

### 退出dwm

退出dwm（登出）： `Shift` + `Mod1` + `Q`.

官方关于默认的快捷键的说明: [dwm tutorial](http://dwm.suckless.org/tutorial).

再次说明，快捷键可以根据自己的喜好自由定义，本维基中的快捷键都是指官方默认的快捷键。

## 扩展使用

### 补丁和增加的窗口布局（tiling modes）

The official website has a number of [patches](http://www.suckless.org/dwm/patches) that can add extra functionality to dwm. Users can easily customize dwm by applying the modifications they like. The [Bottom Stack](http://www.suckless.org/dwm/patches/bottom_stack.html) patch provides an additional tiling mode that splits the screen horizontally, as opposed to the default vertically oriented tiling mode. Similarly, bstack horizontal splits the tiles horizontally.

The [gaplessgrid patch](http://dwm.suckless.org/patches/gapless_grid) allows windows to be tiled like a grid.

#### 实现为每个标签定制布局

dwm的缺省行为是将当前选定的布局应用到所有标签上。如果想为每个标签定制布局可以打[pertag](http://dwm.suckless.org/patches/pertag)这个补丁。

### 解决模拟终端窗口缝隙问题

如果你发现模拟终端（例如xterm，Urxvt）的窗口占不满屏幕，这是因为其窗口的大小和字体有关。你可以试图调整字体大小直到恰好合适为止（这也许是很困难的），或者只需要把`config.h` 文件中的 `resizehints` 设置为 False：

```
static Bool resizehints = False; /* False means respect size hints in tiled resizals */

```

这样dwm会忽略所有窗口的改变大小的请求，不只是模拟终端的。这样的缺点是一些模拟终端可能会刷新异常，像显示一些错误的内容。

#### Urxvt

对于 [urxvt](/index.php/Urxvt "Urxvt") 用户另一个方法是打 [hints patch](/index.php/Urxvt#Fix_maximized_window_gaps "Urxvt") 这个补丁然后将dwm改回到默认的选项：

```
static Bool resizehints = **True**;

```

### 在不登出和退出程序程序的情况下重启dwm

如果你要在在线重启dwm（不关闭它以及其他应用程序），修改启动脚本，并让dwm在一个while循环中运行，像这样：

```
while true; do
    # Log stderror to a file 
    dwm 2> ~/.dwm.log
    # No error logging
    #dwm >/dev/null 2>&1
done

```

这样就可以用Mod-Shift-Q快捷键来实现重启。

把上边的内容写到一个其他的文件（例如`~/bin/startdwm`）是一个好主意。然后在 `~/.xinitrc` 文件里添加（exec startdwm）。这样我们可以使用 `killall startdwm` 来真正地退出X会话，或者绑定到一个方便的快捷键上。

### 把右Alt键作为Mod4（Win键）使用

当把Mod4（Win键）作为 `MODKEY` 时，你可能希望右Alt键也可以作为Mod4，这样就两个手都可以按到了

首先，找到右Ctrl键对应的键码：

```
xmodmap -pke | grep Alt_R

```

然后只需要在启动脚本（比如 `~/.xinitrc`）添加如下内容, 把 _113_ 换成之前`xmodmap` 的结果：

```
xmodmap -e "keycode 113 = Super_L"  # reassign Alt_R to Super_L
xmodmap -e "remove mod1 = Super_L"  # make sure X keeps it out of the mod1 group

```

现在，右Alt键就和Mod4键一样了。

### 防止鼠标下的程序自动获取焦点

为了防止鼠标下的程序自动获取焦点，可以注释掉dwm.c中的如下代码：

 `[EnterNotify] = enternotify, ` 

### 添加个性的快捷键绑定

`config.h` 文件中的两个地方涉及到创建修改快捷键，一个是"/* */" 注释中，并一个是"static Key keys[] = {"语句中。

```
static const char *<keybindname>[]   = { "<command>", "<flags>", "<arguments>", NULL };

```

<keybindname> 可以是任何东西， <command> <-flags> and <arguments> 也是，但要用双引号括起来。

```
{ MODKEY,            XK_<key>,      spawn,          {.v = <keybindname> } },

```

这会绑定 Mod+<key> 来执行之前定义的命令。

```
{ MODKEY|ShiftMask,  XK_<key>,      spawn,          {.v = <keybindname> } },

```

这会绑定 Mod+Shift+<key> ，使用要用Ctrl键是 ControlMask 。

单个按键像Fn或者多媒体键必须要用16进制数来表示，可以用xev程序来获得。或者查看 /usr/include/X11/XF86keysym.h 中的定义。

```
{ 0,                 0xff00,    spawn,       {.v = <keybindname> } },

```

这会把0xff00键绑定到<keybindname>。

### 解决Java程序不正常的问题

对于使用JRE 6u20的Java程序在dwm中可能表现异常，因为dwm不是Java的一个已知的窗口管理器，这会导致一些像鼠标释放使菜单消失之类的小问题。可以先安装里的 [community] 里的wmname：

```
# pacman -S wmname

```

然后你只需要用wmname来设置一个Java能识别的WM名称：

```
$ wmname LG3D

```

这不是永久的，所以你可以把它写进.xinitrc。

## 资源

*   [dwm's official website](http://www.suckless.org/dwm)
*   [dmenu](/index.php/Dmenu "Dmenu") - Simple application launcher from the developers of dwm
*   The [dwm thread](https://bbs.archlinux.org/viewtopic.php?id=57549/) on the forums
*   [Hacking dwm thread](https://bbs.archlinux.org/viewtopic.php?id=92895/)
*   Check out the forums' [wallpaper thread](https://bbs.archlinux.org/viewtopic.php?id=57768/) for a selection of dwm wallpapers
*   [HowTo by Snake](http://www.xsnake.net/howto/dwm/dwm-eng.php)
*   [Moved to dwm](http://0x80.org/blog/?p=72)