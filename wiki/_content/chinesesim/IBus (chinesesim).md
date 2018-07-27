相关文章

*   [Fcitx](/index.php/Fcitx "Fcitx")
*   [SCIM](/index.php/SCIM "SCIM")
*   [UIM](/index.php/UIM "UIM")

[IBus](https://en.wikipedia.org/wiki/Intelligent_Input_Bus 和 [UIM](/index.php/UIM "UIM") 类似。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 输入法引擎](#.E8.BE.93.E5.85.A5.E6.B3.95.E5.BC.95.E6.93.8E)
    *   [1.2 初始安装](#.E5.88.9D.E5.A7.8B.E5.AE.89.E8.A3.85)
    *   [1.3 GNOME](#GNOME)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 小贴士及技巧](#.E5.B0.8F.E8.B4.B4.E5.A3.AB.E5.8F.8A.E6.8A.80.E5.B7.A7)
    *   [3.1 使用拼音](#.E4.BD.BF.E7.94.A8.E6.8B.BC.E9.9F.B3)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [4.1 Kimpanel](#Kimpanel)
    *   [4.2 rxvt-unicode](#rxvt-unicode)
    *   [4.3 GTK 应用程序](#GTK_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [4.4 中文输入](#.E4.B8.AD.E6.96.87.E8.BE.93.E5.85.A5)
    *   [4.5 LibreOffice](#LibreOffice)
    *   [4.6 修改 Gnome-shell 中 ibus 候选框的字体和字号](#.E4.BF.AE.E6.94.B9_Gnome-shell_.E4.B8.AD_ibus_.E5.80.99.E9.80.89.E6.A1.86.E7.9A.84.E5.AD.97.E4.BD.93.E5.92.8C.E5.AD.97.E5.8F.B7)

## 安装

从官方仓库安装[ibus](https://www.archlinux.org/packages/?name=ibus)软件包：

```
# pacman -S ibus

```

此外，为了启动[ibus](https://www.archlinux.org/packages/?name=ibus)的Qt应用程序支持, 安装[ibus-qt](https://www.archlinux.org/packages/?name=ibus-qt)软件库：

```
# pacman -S ibus-qt 

```

### 输入法引擎

你至少需要一个支持你所想用的语言的输入法。可用的输入法包括：

*   ibus-anthy: 一个日文输入法引擎，基于[anthy](https://www.archlinux.org/packages/?name=anthy)。
*   ~~ibus-pinyin: 一个智能中文语音输入法引擎，支持汉语拼音与注音符号。设计者为Ibus的主要作者，而且有许多的高级功能（如英文拼错修改）。~~ 该软件暂时没有维护，而且最新的 ibus 引擎上部分功能不能使用。作为替代，请使用[ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin)。
*   ibus-rime:一个强大的智能中文输入法,支持拼音、注音或者没有音调的拼音、双拼、粤拼、中州韵、仓颉和五笔86。
*   ibus-chewing:一个智能中文语音输入法引擎，支持注音符号，基于[libchewing](https://www.archlinux.org/packages/?name=libchewing)。
*   ibus-hangul: 一个韩文输入法，基于[libhangul](https://www.archlinux.org/packages/?name=libhangul)。
*   ibus-unikey: 支持越南文字的输入法引擎。
*   ibus-table: 一个支持查表型输入法的输入法引擎。
*   ibus-m17n: 一个m17n输入法引擎，可以用m17n-db数据库中的输入法来输入许多语言。
*   **ibus-mozc** - 个日文输入法引擎, 基于 [Mozc](/index.php/Mozc "Mozc"). 包含在 [mozc](https://aur.archlinux.org/packages/mozc/) 包中。
*   ibus-keymagic:一个复合型智能输入法，它被设计成可以工作于所有语言，但需要和kms脚本生成的km2键盘布局共同使用。

查看所有可用的输入法：

```
$ pacman -Ss ^ibus-*

```

其他软包也供给于[AUR](/index.php/AUR "AUR")。

### 初始安装

现在运行ibus-setup的初始程序(当要用Ibus的用户):

```
$ ibus-setup

```

它会启动后台程序，并给你这条信息：

```
IBus has been started! If you cannot use IBus, please add below lines in $HOME/.bashrc, and relogin your desktop.
（译：IBus已启动！如果您还不能用Ibus,请您先将以下的三行代码加到$HOME/.bashrc，再重新登录。)
  export GTK_IM_MODULE=ibus
  export XMODIFIERS=@im=ibus
  export QT_IM_MODULE=ibus

```

**注意:** 虽然Ibus使用一个后台程序，但是它不是被*systemd*管理的那种后台程序：普通用户也可以运行，当你登录时，它会启动。

**注意:** 但是，如果ibus尚未启动，先将那些"export"的代码复制到$HOME/.xprofile，并将这行代码加到该文件：“ibus-daemon -x -d”,再重新登录。

之后，你会看到一张设置屏幕。Ibus运行时，可以随时访问该屏幕，在系统托盘中的Ibus图符点击右键，选择"Preferences"（选项）即可。详见[Configuration](#Configuration).

如果Ibus在Qt、KDE应用程序中不工作，保证ibus-qt软件库已安装，并在Qt设置编辑器中将Ibus制定为默认输入法引擎：

```
$ qtconfig-qt4

```

在 "Interface" -> "Default Input Method" （译：“界面”->“默认输入法引擎”） 中,选择“ibus”,而不是"xim"。

### GNOME

GNOME现在已经默认集成了IBus， 所以你只需要安装的输入法引擎,并在*Region & Language* 中的 “ Input Sources” 添加进去。在你添加至少两个输入源后，GNOME会在托盘中显示输入选择图标。如果如此操作之后你没有成功，很可能你没有完成locale-gen。默认切换输入法的快捷键是 `Super+space`; 请忽视ibus-setup中的添加方法，这不会真的添加新的输入法。

## 配置

**注意:** 如果你想输入汉、日、韩、越南文字，需要安装[东亚字体](/index.php/Fonts_FAQ#Chinese.2C_Japanese.2C_Korean.2C_Vietnamese "Fonts FAQ")。

默认的 "General"（常规）设置应该可以用，但是最好点击“Input Methods”（输入法），在下拉式列表框中选择你的输入法，点击“Add"（添加）。 Ibus 配置好后，可以按 Ctrl+Space 使用（按多次为在已安装语言之间切换）。在每个窗口当中，Ibus 会记住你所用的输入法，所以每个新打开的窗口都需要重新启动。 你可以置换这个特性，在系统托盘的图符上点击右键，选择“Preferences“（首选项）,然后点击“Advanced”（高级）的标签即可。

**注意:** IBus 默认覆盖 [Xmodmap](/index.php/Xmodmap "Xmodmap") 的设置。你可以禁用这个特性，在”references”（首选项）中点击“Advanced”（高级），勾选“Use system keyboard layout”选项。

## 小贴士及技巧

### 使用拼音

当使用 ibus-pinyin时,

*   首先用拼音（无声调）打你想输入的字。
*   反复地按上和下选择一个字（如果有必要，启程前往下一页）。
*   按Space使用一个字。
*   你也可以用上页和下页，并使用1-5的数字键选择你需要的字。
*   你可以一次输入组成一个词或一条短语的若干字（如"zhongwen"可以输入"中文"). ibus-pinyin会记住你最经常打的字，并渐渐做适合你的打字配置文件的建议。

## 疑难解答

### Kimpanel

目前IBus的主界面只支持GTK，[Kimpanel](https://www.archlinux.org/packages/?name=Kimpanel) 提供了原生的 Qt/KDE 输入界面。 但是，目前 kimpanel 在Arch Linux 环境下因并不能很好地工作（部分原因是[FS#19580](https://bugs.archlinux.org/task/19580)），因此需要额外地配置一下。

安装Kimpanel:

```
# pacman -S kdeplasma-addons-applets-kimpanel

```

下载和你的 KDE 版本对应的 kdeplasma-addons 的源文件，并解压缩。

```
$ wget -c [http://download.kde.org/stable/4.x.x/src/kdeplasma-addons-4.x.x.tar.bz2](http://download.kde.org/stable/4.x.x/src/kdeplasma-addons-4.x.x.tar.bz2)
$ tar -xvf kdeplasma-addons-4.x.x.tar.bz2

```

拷贝系统里没有的文件:

```
# mkdir /usr/share/ibus/ui/qt
# cp kdeplasma-addons-4.x.x/applets/kimpanel/backend/ibus/panel.py /usr/share/ibus/ui/qt/panel.py
# cp kdeplasma-addons-4.x.x/applets/kimpanel/backend/ibus/qtpanel.xml /usr/share/ibus/component/qtpanel.xml

```

编辑 `/usr/share/ibus/ui/qt/panel.py`:

```
#!/usr/bin/env **python2**
# vim:set et sts=4 sw=4:
...

```

编辑 `/usr/share/ibus/component/qtpanel.xml`:

```
<?xml version=1.0 encoding=utf-8?>
<!-- filename: **qtpanel.xml** -->
<component>
    <name>org.freedesktop.IBus.Panel</name>
    <description>Qt Panel Component</description>
    <exec>**/usr/lib/ibus/ibus-ui-qt**</exec>
    <version>0.0.1</version>
    <author>Wang Hoi <zealot.hoi@gmail.com></author>
    <license>LGPL</license>
    <homepage></homepage>
    <textdomain>ibus</textdomain>
</component>

```

拷贝 `/usr/lib/ibus/ibus-ui-gtk` 文件到 `/usr/lib/ibus/ibus-ui-qt` 并编辑:

```
# cp /usr/lib/ibus/ibus-ui-gtk /usr/lib/ibus/ibus-ui-qt

```

```
#!/bin/sh
#
# ibus - The Input Bus
#
# Copyright (c) 2007-2010 Peng Huang <shawn.p.huang@gmail.com>
# Copyright (c) 2007-2010 Red Hat, Inc.
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2 of the License, or (at your option) any later version.
#
# This library is distributed in the hope that it will be useful,                                                                              
# but WITHOUT ANY WARRANTY; without even the implied warranty of                                                                               
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the                                                                                
# GNU Lesser General Public License for more details.                                                                                          
#                                                                                                                                              
# You should have received a copy of the GNU Lesser General Public                                                                             
# License along with this program; if not, write to the                                                                                        
# Free Software Foundation, Inc., 59 Temple Place, Suite 330,                                                                                  
# Boston, MA  02111-1307  USA                                                                                                                  

prefix=/usr                                                                                                                                    
exec_prefix=${prefix}                                                                                                                          
datarootdir=${prefix}/share                                                                                                                    
export IBUS_PREFIX=/usr
export IBUS_DATAROOTDIR=${prefix}/share
export IBUS_LOCALEDIR=${datarootdir}/locale

exec python2 **/usr/share/ibus/ui/qt/panel.py** $@

```

最后，在你的任务栏上添加小工具 `Input Methode Panel` 并运行 `ibus-setup`:

```
$ ibus-setup

```

### rxvt-unicode

如果有 ibus 与 *rxvt-unicode* 包的问题，以下的步骤应该能够解决。

将以下的两行代码添加到你的 `~/.Xresources` 文件（可能不需要，先尝试，如果问题出现，再添加代码）：

```
  URxvt.inputMethod: ibus
  URxvt.preeditType: OnTheSpot,None

```

然后用以下的命令启动Ibus:

```
  ibus-daemon --xim

```

如果 ibus-daemon 自动开启（如在 `~/.xinitrc` 或 `~/.xsession` 中)，但是以前执行 `ibus-daemon &` 没有用 `--xim` 选项，确保先结束已打开的进程，再尝试新命令。

### GTK 应用程序

有些用户在 GTK 应用程序下使用输入法时会因为无法找到g tk.immodules 文件而出现问题。在 $HOME/.bashrc中加入

```
 (gtk2) export GTK_IM_MODULE_FILE=/etc/gtk-2.0/gtk.immodules
 (gtk3) export GTK_IM_MODULE_FILE=/usr/lib/gtk-3.0/3.0.0/immodules.cache

```

应该会解决问题。

**注意:** 如果你设置为gtk2，那么你无法使用gtk3的应用程序比如gedit, 如果你设置为gtk3，那么你无法使用gtk2的应用程序比如xfce

### 中文输入

如果你在输入中文时遇到问题，检查你的 locale 设置。比如在香港，export LANG=zh_HK.utf8。

**注意:** ibus 在 1.4 版本后有些大的修正，你可能无法使用 ibus-pinyin 或 ibus-sunpinyin 输入中文。解决方法有：

*   安装 ibus-libpinyin。

你可以安装 [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin)。

如需 ibus 随 gnome 启动，把这些加入 `~/.profile` 后重启 gnome。

```
   export GTK_IM_MODULE=ibus
   export XMODIFIERS=@im=ibus
   export QT_IM_MODULE=ibus
   ibus-daemon -d -x

```

更详细的解决方案可以查看 [这里](http://forum.ubuntu.org.cn/viewtopic.php?f=155&t=346639)。

### LibreOffice

如果 IBus 确实已经启动，但是在 LibreOffice 里没有出现输入窗口，你需要在 ~/.bashrc 里加入这行：

```
export XMODIFIERS=@im=ibus

```

然后你需要用 "--xim -d" 参数来启动 ibus， 你可以在 ~/.xinitrc 中加入这行：

```
ibus-daemon --xim -d

```

但是可怕的是你必须在终端中启动 LibreOffice。

如果你使用 KDE 而上面的方法没用，而你也不介意在 GTK2 模式下运行 LibreOffice，安装 "libreoffice-gnome" 然后在 ~/.xprofile 中添加此行：

```
export OOO_FORCE_DESKTOP="gnome"

```

这会使 IBus 在 LibreOffice 正常使用，你也可以在任何地方启动 LibreOffice -- 而不只是在终端。

### 修改 Gnome-shell 中 ibus 候选框的字体和字号

很多人对 Gnome-shell 不能独立的设置 ibus 输入法的候选词字体和字号颇有微词，下面，介绍一种修改的办法。 首先，你需要安装一个 Gnome-Shell 主题，且激活它，然后你需要修改主题的 gnome-shell.css 文件。这个文件一般在目录 /usr/share/themes/主题名/gnome-shell/ 下。使用你喜欢的编辑器打开它，搜索 .candidate-popup-content 字段（如果没有就新建一个）：

```
.candidate-popup-content {
}

```

然后根据需要添加以下两行（添加后应该是下框中的样子），通过本设置可以改变输入的字母的字体和字号：

```
.candidate-popup-content {
       /* 设置字体 */
	font-family: "Microsoft YaHei UI", serif,cantarell,sans-serif;
       /* 设置号 */
	font-size: 15px;
}

```

如果需要修改候选框的字体和字号，你需要搜索 .candidate-box 字段（如果没有就新建一个）：

```
.candidate-box {
}

```

然后根据需要添加以下两行（添加后应该是下框中的样子），通过本设置可以改变输入的字母的字体和字号：

```
.candidate-box {
       /* 设置字体 */
	font-family: "Microsoft YaHei UI", serif,cantarell,sans-serif;
       /* 设置号 */
	font-size: 15px;
}

```