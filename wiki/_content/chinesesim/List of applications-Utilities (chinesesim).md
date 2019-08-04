**[常用程序](/index.php/List_of_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications (简体中文)")**

* * *

[互联网](/index.php/List_of_Applications/Internet_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Internet (简体中文)") – [多媒体](/index.php/List_of_Applications/Multimedia_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Multimedia (简体中文)") – [工具](/index.php/List_of_Applications/Utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Utilities (简体中文)") – [文档](/index.php/List_of_Applications/Documents_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Documents (简体中文)") – [安全](/index.php/List_of_Applications/Security_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Security (简体中文)") – [科学](/index.php/List_of_Applications/Science_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Science (简体中文)") – [其它](/index.php/List_of_Applications/Other_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Other (简体中文)")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 工具](#工具)
    *   [1.1 终端](#终端)
        *   [1.1.1 命令行 shells](#命令行_shells)
        *   [1.1.2 终端模拟器](#终端模拟器)
            *   [1.1.2.1 基于 VTE](#基于_VTE)
            *   [1.1.2.2 基于 KMS](#基于_KMS)
            *   [1.1.2.3 基于帧缓冲器（framebuffer）](#基于帧缓冲器（framebuffer）)
        *   [1.1.3 终端分页器](#终端分页器)
        *   [1.1.4 终端复用器](#终端复用器)
    *   [1.2 分区工具](#分区工具)
    *   [1.3 挂载](#挂载)
        *   [1.3.1 Udisks](#Udisks)
    *   [1.4 基本 Shell 命令](#基本_Shell_命令)
    *   [1.5 集成式开发环境](#集成式开发环境)
    *   [1.6 文件](#文件)
        *   [1.6.1 文件管理器](#文件管理器)
            *   [1.6.1.1 命令行](#命令行)
            *   [1.6.1.2 图形环境](#图形环境)
        *   [1.6.2 桌面搜索引擎](#桌面搜索引擎)
        *   [1.6.3 压缩与解压](#压缩与解压)
            *   [1.6.3.1 命令行](#命令行_2)
            *   [1.6.3.2 图形环境](#图形环境_2)
        *   [1.6.4 文件合并及比较](#文件合并及比较)
        *   [1.6.5 批量命名](#批量命名)
    *   [1.7 磁盘清理](#磁盘清理)
    *   [1.8 磁盘使用情况分析](#磁盘使用情况分析)
    *   [1.9 时钟同步](#时钟同步)
    *   [1.10 系统监视器](#系统监视器)
    *   [1.11 系统信息检测](#系统信息检测)
        *   [1.11.1 命令行](#命令行_3)
        *   [1.11.2 图形环境](#图形环境_3)
    *   [1.12 键盘布局切换](#键盘布局切换)
    *   [1.13 电源管理](#电源管理)
    *   [1.14 剪贴板管理](#剪贴板管理)
    *   [1.15 壁纸设置](#壁纸设置)
    *   [1.16 软件包管理](#软件包管理)
    *   [1.17 输入法](#输入法)
    *   [1.18 Trash management](#Trash_management)
    *   [1.19 File synchronization](#File_synchronization)
    *   [1.20 Finders](#Finders)

## 工具

### 终端

#### 命令行 shells

参见： [Command-line shell](/index.php/Command-line_shell "Command-line shell").

以及： [Wikipedia:Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells "wikipedia:Comparison of command shells").

#### 终端模拟器

终端模拟器是包含一个终端的图形界面窗口。它们大多是模仿 Xterm，后者向 VT102 看齐，而 VT102 模仿的是打字机。更多的背景信息参见：[Wikipedia:Terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator").

[Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators") 有包含得更全面的列表。

*   **Alacritty** — 跨平台，GPU硬件加速

	[https://github.com/jwilm/alacritty](https://github.com/jwilm/alacritty) || [alacritty](https://www.archlinux.org/packages/?name=alacritty)

*   **aterm** — 可以改变透明度的 Xterm 替代品，自从2008年之后就不再推荐使用（被 urxvt 替代）

	[http://aterm.sourceforge.net/](http://aterm.sourceforge.net/) || [aterm](https://aur.archlinux.org/packages/aterm/)

*   **Cool Retro Term** — 模仿阴极显示器显示效果

	[https://github.com/Swordfish90/cool-retro-term](https://github.com/Swordfish90/cool-retro-term) || [cool-retro-term](https://www.archlinux.org/packages/?name=cool-retro-term)

*   **Eterm** — 为 [Enlightenment](/index.php/Enlightenment "Enlightenment") 桌面设计，目的是作为 xterm 替代品

	[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)

*   **Hyper** — 支持 JS/CSS

	[https://github.com/zeit/hyper](https://github.com/zeit/hyper) || [hyper](https://aur.archlinux.org/packages/hyper/)

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — [KDE](/index.php/KDE "KDE") 桌面自带的.

	[https://www.kde.org/applications/system/konsole/](https://www.kde.org/applications/system/konsole/) || [konsole](https://www.archlinux.org/packages/?name=konsole)

*   **[kitty](/index.php/Kitty "Kitty")** — A modern, hackable, featureful, OpenGL based terminal emulator

	[https://github.com/kovidgoyal/kitty](https://github.com/kovidgoyal/kitty) || [kitty](https://www.archlinux.org/packages/?name=kitty)

*   **mlterm** — 多语言支持，支持各种字符集和编码

	[https://sourceforge.net/projects/mlterm/](https://sourceforge.net/projects/mlterm/) || [mlterm](https://aur.archlinux.org/packages/mlterm/)

*   **[PuTTY](/index.php/PuTTY "PuTTY")** — 高度可配置，主要用于 ssh/telnet/serial

	[https://www.chiark.greenend.org.uk/~sgtatham/putty/](https://www.chiark.greenend.org.uk/~sgtatham/putty/) || [putty](https://www.archlinux.org/packages/?name=putty)

*   **QTerminal** — 轻量化，基于 Qt

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal](https://www.archlinux.org/packages/?name=qterminal)

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — xterm的人气替代.

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://aur.archlinux.org/packages/rxvt/)

*   **shellinabox** — 基于 web 的 SSH 终端

	[https://github.com/shellinabox/shellinabox](https://github.com/shellinabox/shellinabox) || [shellinabox-git](https://aur.archlinux.org/packages/shellinabox-git/)

*   **[st](/index.php/St "St")** — X 的一个简单的终端实现

	[http://st.suckless.org](http://st.suckless.org) || [st](https://aur.archlinux.org/packages/st/)

*   **Terminology** — 由 Enlightenment project 团队开发，有一些创新的功能：文件缩略图、多媒体播放

	[https://www.enlightenment.org/about-terminology](https://www.enlightenment.org/about-terminology) || [terminology](https://www.archlinux.org/packages/?name=terminology)

*   **[urxvt](/index.php/Urxvt "Urxvt")** — 支持触摸、打开URL、伪透明度、Quake 样式的下拉模式和unicode编码，同时凭借 Perl 来实现高度可扩展性

	[http://software.schmorp.de/pkg/rxvt-unicode.html](http://software.schmorp.de/pkg/rxvt-unicode.html) || [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)

*   **[xterm](/index.php/Xterm "Xterm")** — X 窗口系统的一个简单的终端模拟器，提供兼容 DEC VT102 和 Tektronix 4014 的终端来运行不是为窗口系统设计的程序

	[http://invisible-island.net/xterm/](http://invisible-island.net/xterm/) || [xterm](https://www.archlinux.org/packages/?name=xterm)

*   **[Yakuake](/index.php/Yakuake "Yakuake")** — 基于 Konsole 的 Quake 样式的下拉终端

	[https://yakuake.kde.org/](https://yakuake.kde.org/) || [yakuake](https://www.archlinux.org/packages/?name=yakuake)

##### 基于 VTE

[VTE](https://developer.gnome.org/vte/unstable/) 虚拟终端模拟器(Virtual Terminal Emulator) 是 GNOME 早期开发的在 GNOME 终端里使用的小插件。它催生了很多拥有相似功能的终端。

*   **Deepin Terminal** — Deepin 桌面的终端模拟器

	[https://www.deepin.org/en/original/deepin-terminal/](https://www.deepin.org/en/original/deepin-terminal/) || [deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal)

*   **evilvte** — 非常轻量化、高度可定制，支持标签页、自动隐藏和多种字符编码

	[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte-git](https://aur.archlinux.org/packages/evilvte-git/)

*   **Germinal** — 极简主义，提供一个无边框、最大化窗口的终端，默认连接到一个 tmux 会话，有标签页和面板功能

	[http://www.imagination-land.org/tags/germinal.html](http://www.imagination-land.org/tags/germinal.html) || [germinal](https://aur.archlinux.org/packages/germinal/)

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — [GNOME](/index.php/GNOME "GNOME") 桌面自带，支持 Unicode 和 伪透明度

	[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — 一个下拉终端

	[http://guake-project.org/](http://guake-project.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **LXTerminal** — 与桌面无关的终端模拟器，本来是为 [LXDE](/index.php/LXDE "LXDE") 设计的

	[https://wiki.lxde.org/en/LXTerminal](https://wiki.lxde.org/en/LXTerminal) || [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)

*   **MATE terminal** — [Wikipedia:GNOME terminal](https://en.wikipedia.org/wiki/GNOME_terminal "wikipedia:GNOME terminal") 的一个分支，为 [MATE](/index.php/MATE "MATE") 桌面设置.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)

*   **Pantheon Terminal** — 超级轻量化，好看、简洁，默认配置已经很好用，几乎不需要做设置

	[https://github.com/elementary/terminal](https://github.com/elementary/terminal) || [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal)

*   **ROXTerm** — 有标签页和小 footprint

	[http://roxterm.sourceforge.net/](http://roxterm.sourceforge.net/) || [roxterm](https://aur.archlinux.org/packages/roxterm/)

*   **sakura** — 基于GTK+ 和 VTE

	[http://www.pleyades.net/david/projects/sakura](http://www.pleyades.net/david/projects/sakura) || [sakura](https://www.archlinux.org/packages/?name=sakura)

*   **[Terminator](/index.php/Terminator "Terminator")** — 支持多个可调整大小的终端面板

	[https://gnometerminator.blogspot.com/](https://gnometerminator.blogspot.com/) || [terminator](https://www.archlinux.org/packages/?name=terminator)

*   **[Termite](/index.php/Termite "Termite")** — 以键盘为中心的、基于 VTE 的终端，为在平铺式和标签式窗口管理器里使用作优化

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

*   **[Tilda](/index.php/Tilda "Tilda")** — 可配置的下拉终端模拟器

	[https://github.com/lanoxx/tilda/](https://github.com/lanoxx/tilda/) || [tilda](https://www.archlinux.org/packages/?name=tilda)

*   **Tilix** — 给 GNOME 的平铺式终端模拟器Tiling terminal emulator for GNOME.

	[https://gnunn1.github.io/tilix-web/](https://gnunn1.github.io/tilix-web/) || [tilix](https://www.archlinux.org/packages/?name=tilix)

*   **tinyterm** — 基于 VTE 的轻量化终端模拟器

	[https://github.com/lahwaacz/tinyterm](https://github.com/lahwaacz/tinyterm) || [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/)

*   **[Xfce Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — [Xfce](/index.php/Xfce "Xfce") 桌面的带彩色提示和和标签页化的界面的终端模拟器.

	[https://docs.xfce.org/apps/terminal/start](https://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

##### 基于 KMS

下面这些终端模拟器是基于 [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") 的，没有 X 也可以运行。

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — 一个基于 KMS/DRM 的系统控制台（getty），对于 Linux 操作系统内置一个终端模拟器

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

##### 基于帧缓冲器（framebuffer）

在 GNU/Linux 术语里，[framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") 可以指代 Linux 内核里的一个虚拟设备 (**fbdev**) 或者 X 的虚拟帧缓冲系统 (**xvfb**)。下面列出的是基于 **fbdev** 的。

*   **yaft** — 没有 X 也可以运行，支持 UCS2 glyphs、 壁纸和256色

	[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)

#### 终端分页器

参见 [Wikipedia:Terminal pager](https://en.wikipedia.org/wiki/Terminal_pager "wikipedia:Terminal pager")。

*   **[more](https://en.wikipedia.org/wiki/More_(command) "wikipedia:More (command)")** — 一个简单（功能也简单）的分页器。是 util-linux 的一部分。

	[https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/about/](https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/about/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[less](/index.php/Core_utilities#Essentials "Core utilities")** — 类似 more，但是支持前滚和后滚，包括文件的部分加载

	[https://www.gnu.org/software/less/](https://www.gnu.org/software/less/) || [less](https://www.archlinux.org/packages/?name=less)

*   **[most](https://en.wikipedia.org/wiki/Most_(Unix) "wikipedia:Most (Unix)")** — 支持多窗口、左右滚动和显示颜色

	[http://www.jedsoft.org/most/](http://www.jedsoft.org/most/) || [most](https://www.archlinux.org/packages/?name=most)

*   **mcview** — 支持显示颜色和鼠标的分页器，与 midnight commander 捆绑在一起

	[http://midnight-commander.org/](http://midnight-commander.org/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   [Vim](/index.php/Vim "Vim") 也可以 [做分页器](/index.php/Vim#Vim_as_a_pager "Vim").

#### 终端复用器

参见 [Wikipedia:Terminal multiplexer](https://en.wikipedia.org/wiki/Terminal_multiplexer "wikipedia:Terminal multiplexer").

*   **abduco** — 用于连接和断开会话的工具，支持让进程独立于控制它的终端

	[http://www.brain-dump.org/projects/abduco/](http://www.brain-dump.org/projects/abduco/) || [abduco](https://www.archlinux.org/packages/?name=abduco)

*   **[byobu](https://en.wikipedia.org/wiki/Byobu_(software) "wikipedia:Byobu (software)")** — GPLv3 许可证的 tmux 或 screen 插件。要求已经安装一个终端复用器。

	[http://byobu.co/](http://byobu.co/) || [byobu](https://aur.archlinux.org/packages/byobu/)

*   **[dtach](/index.php/Dtach "Dtach")** — 模拟 [GNU Screen](/index.php/GNU_Screen "GNU Screen") 的断开连接功能的程序

	[http://dtach.sourceforge.net/](http://dtach.sourceforge.net/) || [dtach](https://aur.archlinux.org/packages/dtach/)

*   **dvtm** — [dwm](/index.php/Dwm "Dwm") 样式的控制台窗口管理器

	[http://brain-dump.org/projects/dvtm/](http://brain-dump.org/projects/dvtm/) || [dvtm](https://www.archlinux.org/packages/?name=dvtm)

*   **[GNU Screen](/index.php/GNU_Screen "GNU Screen")** — 复用一个终端的终端内全屏窗口管理器

	[https://www.gnu.org/software/screen/](https://www.gnu.org/software/screen/) || [screen](https://www.archlinux.org/packages/?name=screen)

*   **mtm** — 只有四个命令的简单复用器：change focus, split, close, 和 screen redraw.

	[https://github.com/deadpixi/mtm](https://github.com/deadpixi/mtm) || [mtm-git](https://aur.archlinux.org/packages/mtm-git/)

*   **[tmux](/index.php/Tmux "Tmux")** — BSD 许可证的终端复用器

	[https://tmux.github.io/](https://tmux.github.io/) || [tmux](https://www.archlinux.org/packages/?name=tmux)

### 分区工具

参阅 [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### 挂载

*   **9mount** — Mount 9p filesystems.

	[http://sqweek.net/code/9mount/](http://sqweek.net/code/9mount/) || [9mount](https://aur.archlinux.org/packages/9mount/)

*   **cryptmount** — Mount an encrypted file system as a regular user.

	[http://cryptmount.sourceforge.net/](http://cryptmount.sourceforge.net/) || [cryptmount](https://aur.archlinux.org/packages/cryptmount/)

*   **ldm** — A lightweight daemon that mounts drives automagically using *udev*

	[https://github.com/LemonBoy/ldm](https://github.com/LemonBoy/ldm) || [ldm](https://aur.archlinux.org/packages/ldm/)

*   **pmount** — Mount *source* as a regular user to an automatically created destination `/media/*source_name*`.

	[http://pmount.alioth.debian.org/](http://pmount.alioth.debian.org/) || [pmount](https://aur.archlinux.org/packages/pmount/)

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

	[http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device](http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device) || [pmount-safe-removal](https://aur.archlinux.org/packages/pmount-safe-removal/)

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on *udev* and glib.

	[http://ignorantguru.github.io/udevil](http://ignorantguru.github.io/udevil) || [udevil](https://www.archlinux.org/packages/?name=udevil)

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

	[http://winshares.sourceforge.net/](http://winshares.sourceforge.net/) || [ws](https://aur.archlinux.org/packages/ws/)

#### Udisks

*   **bashmount** — A bash script to mount and manage removable media as a regular user with udisks.

	[https://github.com/jamielinux/bashmount](https://github.com/jamielinux/bashmount) || [bashmount](https://aur.archlinux.org/packages/bashmount/)

*   **udiskie** — Automatic disk mounting service using *udisks*

	[https://pypi.python.org/pypi/udiskie](https://pypi.python.org/pypi/udiskie) || [udiskie](https://www.archlinux.org/packages/?name=udiskie)

*   **udisks_functions** — Bash functions and aliases for *udisks2*

	[https://bbs.archlinux.org/viewtopic.php?id=109307](https://bbs.archlinux.org/viewtopic.php?id=109307) || [udisks_functions](https://aur.archlinux.org/packages/udisks_functions/)

*   **udisksvm** — GUI *udisks* wrapper for removable media

	[https://bbs.archlinux.org/viewtopic.php?id=112397](https://bbs.archlinux.org/viewtopic.php?id=112397) || [udisksvm](https://aur.archlinux.org/packages/udisksvm/)

### 基本 Shell 命令

*   **[Core utilities](/index.php/Core_utilities "Core utilities")** — The basic file, shell and text manipulation utilities of the GNU operating system

	[http://www.gnu.org/software/coreutils](http://www.gnu.org/software/coreutils) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

### 集成式开发环境

See also [Wikipedia:Comparison of integrated development environments](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "wikipedia:Comparison of integrated development environments").

*   **[Anjuta](/index.php/Anjuta "Anjuta")** — Versatile IDE with project management, an application wizard, an interactive debugger, a source editor, version control support and many more tools.

	[http://www.anjuta.org/](http://www.anjuta.org/) || [anjuta](https://www.archlinux.org/packages/?name=anjuta)

*   **[Aptana Studio](https://en.wikipedia.org/wiki/Aptana#Aptana_Studio "wikipedia:Aptana")** — IDE based on Eclipse, but geared towards web development, with support for HTML, CSS, Javascript, Ruby on Rails, PHP, Adobe AIR and others.

	[http://www.aptana.org/](http://www.aptana.org/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **[Bluefish](https://en.wikipedia.org/wiki/Bluefish_(text_editor) "wikipedia:Bluefish (text editor)")** — GTK+ editor/IDE with an MDI interface, syntax highlighting and support for Python plugins.

	[http://bluefish.openoffice.nl/](http://bluefish.openoffice.nl/) || [bluefish](https://www.archlinux.org/packages/?name=bluefish)

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — A WYSIWYG content editor for the World Wide Web. Powered by Gecko, the rendering engine of [Firefox](/index.php/Firefox "Firefox"), it can edit Web pages in conformance to Web Standards. It runs on Mac OS X, Windows and Linux.

	[http://bluegriffon.org/](http://bluegriffon.org/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[Bluej](https://en.wikipedia.org/wiki/Bluej "wikipedia:Bluej")** — Fully featured Java IDE used mainly for educational and beginner purposes.

	[http://bluej.org/](http://bluej.org/) || [bluej](https://aur.archlinux.org/packages/bluej/)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "wikipedia:Brackets (text editor)")** — A free open-source editor written in HTML, CSS, and Javascript with a primary focus on Web Development. It was created by Adobe Systems, licensed under the MIT License, and is currently maintained on GitHub.

	[http://brackets.io/](http://brackets.io/) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — Open source and cross-platform C/C++ IDE.

	[http://www.codeblocks.org/](http://www.codeblocks.org/) || [codeblocks](https://www.archlinux.org/packages/?name=codeblocks)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

	[https://c9.io/](https://c9.io/) || [cloud9](https://aur.archlinux.org/packages/cloud9/)

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

	[http://eclipse.org/](http://eclipse.org/) || [eclipse](https://www.archlinux.org/packages/?name=eclipse)

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Multi-platform text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

	[http://www.editra.org](http://www.editra.org) || [editra-svn](https://aur.archlinux.org/packages/editra-svn/)

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — Full-featured Python 3.x and Ruby IDE in PyQt4.

	[http://eric-ide.python-projects.org/](http://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric) [eric4](https://aur.archlinux.org/packages/eric4/)

*   **[Gambas](/index.php/Gambas "Gambas")** — Free development environment based on a Basic interpreter with object extensions.

	[http://gambas.sourceforge.net/en/main.html](http://gambas.sourceforge.net/en/main.html) || [gambas3-ide](https://www.archlinux.org/packages/?name=gambas3-ide)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Text editor using the GTK+ toolkit with basic features of an integrated development environment.

	[https://geany.org](https://geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **IEP** — Cross-platform Python IDE focused on interactivity and introspection, which makes it very suitable for scientific computing.

	[http://iep-project.org/](http://iep-project.org/) || [iep](https://aur.archlinux.org/packages/iep/)

*   **[IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA")** — IDE for Java, Groovy and other programming languages with advanced refactoring features.

	[http://www.jetbrains.com/idea/](http://www.jetbrains.com/idea/) || [intellij-idea-community-edition](https://www.archlinux.org/packages/?name=intellij-idea-community-edition)

*   **[KDevelop](https://en.wikipedia.org/wiki/KDevelop "wikipedia:KDevelop")** — Feature-full, plugin extensible IDE for C/C++ and other programming languages.

	[http://kdevelop.org/](http://kdevelop.org/) || [kdevelop](https://www.archlinux.org/packages/?name=kdevelop)

*   **[Komodo Edit](https://en.wikipedia.org/wiki/Komodo_Edit "wikipedia:Komodo Edit")** — A free, multi-language editor.

	[http://www.activestate.com/komodo-edit](http://www.activestate.com/komodo-edit) || [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/)

*   **[Lazarus](https://en.wikipedia.org/wiki/Lazarus_(IDE) "wikipedia:Lazarus (IDE)")** — Cross-platform IDE for Object Pascal.

	[http://lazarus.freepascal.org/](http://lazarus.freepascal.org/) || [lazarus](https://www.archlinux.org/packages/?name=lazarus)

*   **LiteIDE** — A simple, open source, cross-platform Go IDE.

	[https://github.com/visualfc/liteide](https://github.com/visualfc/liteide) || [liteide](https://www.archlinux.org/packages/?name=liteide)

*   **MonkeyStudio** — Monkey Studio (MkS) is a cross platform IDE written in C++/Qt 4\. Syntax highlighting for more than 22 programming languages.

	[http://monkeystudio.org/](http://monkeystudio.org/) || [monkeystudio](https://aur.archlinux.org/packages/monkeystudio/)

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

	[http://monodevelop.com/](http://monodevelop.com/) || [monodevelop](https://aur.archlinux.org/packages/monodevelop/)

*   **MPLAB** — IDE for Microchip PIC and dsPIC development

	[http://www.microchip.com/mplabx](http://www.microchip.com/mplabx) || [microchip-mplabx-bin](https://aur.archlinux.org/packages/microchip-mplabx-bin/)

*   **[NetBeans](/index.php/Netbeans "Netbeans")** — Integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

	[http://netbeans.org/](http://netbeans.org/) || [netbeans](https://www.archlinux.org/packages/?name=netbeans)

*   **[Ninja-IDE](https://en.wikipedia.org/wiki/Ninja-IDE "wikipedia:Ninja-IDE")** — from the recursive acronym: "Ninja-IDE Is Not Just Another IDE", is a cross-platform integrated development environment (IDE); runs on Linux/X11, Mac OS X and Windows OSs. Used, for example, for Python development

	[http://ninja-ide.org/](http://ninja-ide.org/) || [ninja-ide](https://aur.archlinux.org/packages/ninja-ide/)

*   **[Phpstorm](https://en.wikipedia.org/wiki/PhpStorm "wikipedia:PhpStorm")** — JetBrains PhpStorm is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform, providing an editor for PHP, HTML and JavaScript with on-the-fly code analysis, error prevention and automated refactorings for PHP and JavaScript code.

	[https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/) || [phpstorm](https://aur.archlinux.org/packages/phpstorm/) [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)

*   **[PyCharm](https://en.wikipedia.org/wiki/PyCharm "wikipedia:PyCharm")** — IDE used for programming in Python with support for code analysis, debugging, unit testing, version control and web development with Django.

	[http://www.jetbrains.com/pycharm/](http://www.jetbrains.com/pycharm/) || [pycharm-community](https://aur.archlinux.org/packages/pycharm-community/)

*   **[QDevelop](https://en.wikipedia.org/wiki/QDevelop "wikipedia:QDevelop")** — Free and cross-platform IDE for Qt.

	[http://biord-software.org/qdevelop/](http://biord-software.org/qdevelop/) || [qdevelop-svn](https://aur.archlinux.org/packages/qdevelop-svn/)

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — Lightweight, cross-platform C++ integrated development environment with a focus on Qt.

	[http://qt-project.org/downloads#qt-creator](http://qt-project.org/downloads#qt-creator) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **[Scratch](https://en.wikipedia.org/wiki/Scratch "wikipedia:Scratch")** — A multimedia authoring tool for educational and entertainment purposes, such as creating interactive projects and simple sprite-based games. It is used primarly by unskilled users (such as children) as an entry to [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming "wikipedia:Event-driven programming"). *Scratch* is free software under GPL v2 and [Scratch Source Code License](http://wiki.scratch.mit.edu/wiki/Scratch_Source_Code_License).

	[http://scratch.mit.edu](http://scratch.mit.edu) || [scratch](https://www.archlinux.org/packages/?name=scratch)

*   **Spyder** — Scientific PYthon Development EnviRonment providing MATLAB-like features.

	[http://code.google.com/p/spyderlib/](http://code.google.com/p/spyderlib/) || [spyder](https://www.archlinux.org/packages/?name=spyder)

### 文件

#### 文件管理器

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### 命令行

*   **[Midnight Commander](https://en.wikipedia.org/wiki/Midnight_commander "wikipedia:Midnight commander")** — 终端双面板文件管理器

	[http://www.midnight-commander.org](http://www.midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **pilot** — [Alpine](/index.php/Alpine "Alpine")的文件管理器

	[http://www.washington.edu/alpine](http://www.washington.edu/alpine) || [alpine](https://aur.archlinux.org/packages/alpine/)

*   **[Ranger](/index.php/Ranger "Ranger")** — vi风格快捷键,可定制,特性丰富

	[http://nongnu.org/ranger](http://nongnu.org/ranger) || [ranger](https://www.archlinux.org/packages/?name=ranger)

*   **[Vifm](/index.php/Vifm "Vifm")** — 基于ncurses的双面板文件管理器,vi风格快捷键

	[http://vifm.sourceforge.net/](http://vifm.sourceforge.net/) || [vifm](https://www.archlinux.org/packages/?name=vifm)

##### 图形环境

*   **Dolphin** — KDE 4的默认文件管理器

	[http://dolphin.kde.org/](http://dolphin.kde.org/) || [kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)

*   **emelFM2** — 双面板文件管理器

	[http://emelfm2.net/](http://emelfm2.net/) || [emelfm2](https://www.archlinux.org/packages/?name=emelfm2)

*   **Konqueror** — KDE环境下的文件管理器

	[http://www.konqueror.org/](http://www.konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **Krusader** — KDE环境下的高级双面板(commander风格)文件管理器

	[http://www.krusader.org/](http://www.krusader.org/) || [krusader](https://www.archlinux.org/packages/?name=krusader)

*   **[GNOME Files](/index.php/GNOME_Files "GNOME Files")** — Gnome默认文件管理器,重量级,可扩展、支持自定义脚本

	[http://projects.gnome.org/nautilus/](http://projects.gnome.org/nautilus/) || [nautilus](https://www.archlinux.org/packages/?name=nautilus)

*   **[PCManFM](/index.php/PCManFM "PCManFM")** — 轻量级文件管理器,支持标签,可以管理桌面背景(可选)

	[http://pcmanfm.sourceforge.net/](http://pcmanfm.sourceforge.net/) || [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)

*   **qtfm** — 小型轻量级文件管理器,完全基于Qt

	[http://www.qtfm.org/](http://www.qtfm.org/) || [qtfm](https://aur.archlinux.org/packages/qtfm/)

*   **ROX-Filer** — 小型快速文件管理器,可以管理桌面背景和面板(可选)

	[http://rox.sourceforge.net](http://rox.sourceforge.net) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **Sunflower** — 小型,高度可定制的双面板文件管理器,支持插件

	[http://code.google.com/p/sunflower-fm/](http://code.google.com/p/sunflower-fm/) || [sunflower](https://aur.archlinux.org/packages/sunflower/)

*   **[Thunar](/index.php/Thunar "Thunar")** — 可以作为daemon运行,启动和加载目录速度很快.可以配置自定义动作

	[http://thunar.xfce.org/index.html](http://thunar.xfce.org/index.html) || [thunar](https://www.archlinux.org/packages/?name=thunar)

*   **tuxcmd** — 双面板文件管理器，Total Commander风格，已停止开发

	[http://tuxcmd.sourceforge.net/description.php](http://tuxcmd.sourceforge.net/description.php) || [tuxcmd](https://www.archlinux.org/packages/?name=tuxcmd)

*   **Xfe** — X环境下的类似视窗操作系统的Explorer或Commander的管理器

	[http://roland65.free.fr/xfe/index.php/](http://roland65.free.fr/xfe/index.php/) || [xfe](https://aur.archlinux.org/packages/xfe/)

#### 桌面搜索引擎

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

*   **Catfish** — 万能文件搜索工具

	[https://launchpad.net/catfish-search](https://launchpad.net/catfish-search) || [catfish](https://www.archlinux.org/packages/?name=catfish)

*   **Docfetcher** — 基于 Java, 开源，桌面搜索

	[http://docfetcher.sourceforge.net](http://docfetcher.sourceforge.net) || [docfetcher](https://aur.archlinux.org/packages/docfetcher/)

*   **Gnome Search Tool** — Gnome 首席搜索工具

	[http://gnome.org](http://gnome.org) || [gnome-search-tool](https://www.archlinux.org/packages/?name=gnome-search-tool)

*   **Gnome Search Tool No Nautilus** — 去除了 [GNOME Files](/index.php/GNOME_Files "GNOME Files") 和 *gnome-desktop* 的 *gnome-search-tool*

	|| [gnome-search-tool-no-nautilus](https://aur.archlinux.org/packages/gnome-search-tool-no-nautilus/)

*   **Pinot** — 个性化元搜索

	[http://code.google.com/p/pinot-search/](http://code.google.com/p/pinot-search/) || [pinot](https://www.archlinux.org/packages/?name=pinot)

*   **Recoll** — 基于 Xapian 后端的全文本搜索

	[http://www.lesbonscomptes.com/recoll/](http://www.lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **Searchmonkey** — 强大的 GUI 搜索工具，支持正则表达式

	[http://searchmonkey.sourceforge.net/](http://searchmonkey.sourceforge.net/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)

*   **[Strigi](https://en.wikipedia.org/wiki/Strigi "wikipedia:Strigi")** — 爬虫，Qt GUI，快速

	[http://strigi.sourceforge.net/](http://strigi.sourceforge.net/) || [strigi](https://aur.archlinux.org/packages/strigi/)

*   **[Tracker](https://en.wikipedia.org/wiki/MetaTracker_(software) "wikipedia:MetaTracker (software)")** — 一体化索引，搜索工具，元数据

	[http://projects.gnome.org/tracker/index.html](http://projects.gnome.org/tracker/index.html) || [tracker](https://www.archlinux.org/packages/?name=tracker)

#### 压缩与解压

See also [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers").

##### 命令行

*   **atool** — 管理多种压缩文件的脚本.

	[http://www.nongnu.org/atool/](http://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **[p7zip](/index.php/P7zip "P7zip")** — 终端下的7zip的POSIX系统移植版本.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip](https://www.archlinux.org/packages/?name=p7zip)

##### 图形环境

*   **Ark** — KDE环境下的压缩文件管理器.

	[http://kde.org/applications/utilities/ark/](http://kde.org/applications/utilities/ark/) || [kdeutils-ark](https://www.archlinux.org/packages/?name=kdeutils-ark)

*   **File Roller** — Gnome环境下的默认压缩文件管理器.

	[http://fileroller.sourceforge.net/](http://fileroller.sourceforge.net/) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

*   **Peazip** — 一个开源的文件及压缩文件管理器

	[http://www.peazip.org/peazip-linux.html](http://www.peazip.org/peazip-linux.html) || [peazip](https://aur.archlinux.org/packages/peazip/)

*   **Squeeze** — 终端工具的次轻量级的前端.

	[http://squeeze.xfce.org/](http://squeeze.xfce.org/) || [squeeze](https://aur.archlinux.org/packages/squeeze/)

*   **Xarchive** — 多种工具的GTK+ 2前端.

	[http://xarchive.sourceforge.net/](http://xarchive.sourceforge.net/) || [xarchive](https://aur.archlinux.org/packages/xarchive/)

*   **Xarchiver** — 独立的轻量级桌面压缩文件管理器.

	[http://xarchiver.sourceforge.net/](http://xarchiver.sourceforge.net/) || [xarchiver](https://www.archlinux.org/packages/?name=xarchiver)

*   **[p7zip](/index.php/P7zip "P7zip")** — 终端下的7zip的POSIX系统移植版本.包括7zFM图形界面.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip](https://www.archlinux.org/packages/?name=p7zip)

#### 文件合并及比较

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

*   **colordiff** — 相当于 diff, 但自带语法高亮。

	[http://www.colordiff.org/](http://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **Diffuse** — 简单小巧的文本合并工具，由 Python 编写成

	[http://diffuse.sourceforge.net/](http://diffuse.sourceforge.net/) || [diffuse](https://www.archlinux.org/packages/?name=diffuse)

*   **KDiff3** — KDE 文件及目录的比较及合并工具

	[http://kdiff3.sourceforge.net/](http://kdiff3.sourceforge.net/) || [kdiff3](https://www.archlinux.org/packages/?name=kdiff3)

*   **[Kompare](https://en.wikipedia.org/wiki/Kompare "wikipedia:Kompare")** — 在源文件之间 Diff/Patch 的前端，支持众多比较格式，还允许大量显示格式的选项

	[http://kde.org/applications/development/kompare](http://kde.org/applications/development/kompare) || [kdesdk-kompare](https://www.archlinux.org/packages/?name=kdesdk-kompare)

*   **[Meld](https://en.wikipedia.org/wiki/Meld_(software) "wikipedia:Meld (software)")** — 可视化比较及合并工具，适用于文件，目录和版本控制项目

	[http://meld.sourceforge.net](http://meld.sourceforge.net) || [meld](https://www.archlinux.org/packages/?name=meld)

*   **xxdiff** — 专注于文件或目录之间差异的图形化浏览器

	[http://furius.ca/xxdiff/](http://furius.ca/xxdiff/) || [xxdiff](https://aur.archlinux.org/packages/xxdiff/)

[Vim](/index.php/Vim "Vim") 和 [Emacs](/index.php/Emacs "Emacs") 均通过 [vimdiff](/index.php/Vim#Merging_files_.28vimdiff.29 "Vim") 和 `ediff` 提供了合并功能。

#### 批量命名

### 磁盘清理

### 磁盘使用情况分析

*   **ncdu** — 简单的，使用ncurses的磁盘使用情况分析工具器.

	[http://dev.yorhel.nl/ncdu](http://dev.yorhel.nl/ncdu) || [ncdu](https://www.archlinux.org/packages/?name=ncdu)

*   **gt5** — diff 风格的 du 浏览器

	[http://gt5.sourceforge.net](http://gt5.sourceforge.net) || [gt5](https://aur.archlinux.org/packages/gt5/)

*   **Baobab** — 一个C/gtk+的Gnome环境的磁盘分析程序.

	[http://www.marzocca.net/linux/baobab](http://www.marzocca.net/linux/baobab) || [baobab](https://www.archlinux.org/packages/?name=baobab)

*   **Filelight** — 显示可互动的图像，用环状的饼图可视化磁盘使用情况.

	[http://www.methylblue.com/filelight](http://www.methylblue.com/filelight) || [filelight](https://www.archlinux.org/packages/?name=filelight)

*   **gdmap** — 根据文件夹或文件的大小绘制由一系列矩形组成的图像.

	[http://gdmap.sourceforge.net/](http://gdmap.sourceforge.net/) || [gdmap](https://www.archlinux.org/packages/?name=gdmap)

### 时钟同步

### 系统监视器

*   **adesklet SystemMonitor** — [adesklets](https://en.wikipedia.org/wiki/Adesklets "wikipedia:Adesklets") 的一系列模块系统监视器。

	[http://adesklets.sourceforge.net/desklets.html](http://adesklets.sourceforge.net/desklets.html) || [adesklet-systemmonitor](https://aur.archlinux.org/packages/adesklet-systemmonitor/)

*   **[Conky](/index.php/Conky "Conky")** — 轻量、可定制的系统监视器。

	[http://conky.sourceforge.net/](http://conky.sourceforge.net/) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **dstat** — 万能的资源统计工具。

	[http://dag.wieers.com/home-made/dstat/](http://dag.wieers.com/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — 既简单，又灵活的系统监视器，由 GTK+ 编写成，可集成大量插件。

	[http://members.dslextreme.com/users/billw/gkrellm/gkrellm.html](http://members.dslextreme.com/users/billw/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

*   **gnome-system-monitor** — [GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 的系统监视器。

	[https://help.gnome.org/users/gnome-system-monitor/](https://help.gnome.org/users/gnome-system-monitor/) || [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor)

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — 简易的交互式进程查看器。

	[http://htop.sourceforge.net/](http://htop.sourceforge.net/) || [htop](https://www.archlinux.org/packages/?name=htop)

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard 专用的任务管理器、性能监视器。

	[http://userbase.kde.org/KSysGuard/](http://userbase.kde.org/KSysGuard/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **linux process explorer** — Linux 的图像化任务管理器。

	[http://sourceforge.net/projects/procexp/](http://sourceforge.net/projects/procexp/) || [procexp](https://aur.archlinux.org/packages/procexp/)

*   **LXTask** — [LXDE (简体中文)](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)") 的轻量任务管理器。

	[http://wiki.lxde.org/en/LXTask](http://wiki.lxde.org/en/LXTask) || [lxtask](https://www.archlinux.org/packages/?name=lxtask)

*   **[Trayfreq](/index.php/Trayfreq "Trayfreq")** — 一个轻量的电池监视器、CPU 计数器。

	[http://trayfreq.sourceforge.net](http://trayfreq.sourceforge.net) || [trayfreq](https://aur.archlinux.org/packages/trayfreq/)

### 系统信息检测

#### 命令行

*   **alsi** — Arch Linux 一个系统信息工具，它甚至可适用于其它 Linux 发行版，连编辑脚本都不需要。

	[http://trizenx.blogspot.ro/2012/08/alsi.html](http://trizenx.blogspot.ro/2012/08/alsi.html) || [alsi](https://aur.archlinux.org/packages/alsi/)

*   **archey** — 基于 Python 3 的简单脚本，能显示 Arch Logo 及若干基本系统信息。

	[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey](https://aur.archlinux.org/packages/archey/)

*   **archey2** — 基于 Python 2 的简单脚本，能显示 Arch Logo 及若干基本系统信息。

	[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey2](https://aur.archlinux.org/packages/archey2/)

*   **archey3-git** — 又一个能显示 Arch Logo 及若干基本系统信息的 Python 脚本

	[http://www.generictestdomain.net/archey3/](http://www.generictestdomain.net/archey3/) || [archey3-git](https://aur.archlinux.org/packages/archey3-git/)

*   **Dmidecode** — 能基于 SMBIOS/DMI 标准报告储存于您系统 BIOS 中的硬件信息。

	[http://www.nongnu.org/dmidecode/](http://www.nongnu.org/dmidecode/) || [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)

#### 图形环境

*   **CPU-G** — 显示您硬件若干有用信息的工具，和 Windows 下的 CPU-Z 很相似。

	[http://cpug.sourceforge.net/](http://cpug.sourceforge.net/) || [cpu-g](https://aur.archlinux.org/packages/cpu-g/)

*   **hardinfo** — 显示您硬件和操作系统若干有用信息的工具，和 Windows 下的设备管理器很相似。

	[http://hardinfo.berlios.de/HomePage](http://hardinfo.berlios.de/HomePage) || [hardinfo](https://www.archlinux.org/packages/?name=hardinfo)

*   **i-Nex** — 一个收集并显示所有硬件参数的工具，采用了和 Windows 工具 CPU-Z 很相似的界面。

	[http://i-nex.linux.pl/](http://i-nex.linux.pl/) || [i-nex](https://aur.archlinux.org/packages/i-nex/)

*   **lshw-gtk** — 一个提供很详细的硬件信息的小工具，同时具备了 CLI 和 GTK 界面。

	[http://ezix.org/project/wiki/HardwareLiSter](http://ezix.org/project/wiki/HardwareLiSter) || [lshw-gtk](https://aur.archlinux.org/packages/lshw-gtk/)

### 键盘布局切换

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

	[http://fbxkb.sourceforge.net/](http://fbxkb.sourceforge.net/) || [fbxkb](https://aur.archlinux.org/packages/fbxkb/)

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

	[http://sourceforge.net/projects/xxkb/](http://sourceforge.net/projects/xxkb/) || [xxkb](https://www.archlinux.org/packages/?name=xxkb)

*   **qxkb** — A keyboard switcher written in Qt.

	[http://code.google.com/p/qxkb/](http://code.google.com/p/qxkb/) || [qxkb](https://aur.archlinux.org/packages/qxkb/)

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

	[http://www.xneur.ru/](http://www.xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/), [gxneur](https://aur.archlinux.org/packages/gxneur/) (GUI)

### 电源管理

见 [Power saving#Packages](/index.php/Power_saving#Packages "Power saving").

### 剪贴板管理

### 壁纸设置

### 软件包管理

*   **Aurnotify** — 提示你最喜爱的来自AUR的软件的新动态.

	[http://adesklets.sourceforge.net/desklets.html](http://adesklets.sourceforge.net/desklets.html) || [aurnotify](https://aur.archlinux.org/packages/aurnotify/)

*   **Pkgtools** — 一个Arch Linux软件管理的脚本合集. 包含 **pkgfile** – 命令来查找哪个包含了某个文件

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **[Yaourt](/index.php/Yaourt "Yaourt")** — 一个pacman前端，有更多特性和对aur的支持.

	[http://www.archlinux.fr/yaourt-en/](http://www.archlinux.fr/yaourt-en/) || [yaourt](https://aur.archlinux.org/packages/yaourt/)

参考阅读[AUR helpers](/index.php/AUR_helpers "AUR helpers").

### 输入法

参见 [Wikipedia:Input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

*   **[Fcitx (简体中文)](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")** — 可扩展，超灵活的输入工具。

	[http://fcitx-im.org](http://fcitx-im.org) || [fcitx](https://www.archlinux.org/packages/?name=fcitx)

*   **Hime** — 基于 GTK2/GTK3 的输入平台。

	[http://hime-ime.github.io/](http://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)

*   **[IBus (简体中文)](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")** — Linux 新一代输入 BUS.

	[http://ibus.googlecode.com](http://ibus.googlecode.com) || [ibus](https://www.archlinux.org/packages/?name=ibus)

*   **[Rime IME](/index.php/Rime_IME "Rime IME")** — Rime 输入引擎。

	[http://code.google.com/p/rimeime/](http://code.google.com/p/rimeime/) || [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) or [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)

*   **[UIM](/index.php/UIM "UIM")** — 多语言输入库。

	[http://code.google.com/p/uim/](http://code.google.com/p/uim/) || [uim](https://www.archlinux.org/packages/?name=uim)

### Trash management

*   **trash-cli** — A command-line interface implementing FreeDesktop.org's Trash specification.

	[http://github.com/andreafrancia/trash-cli](http://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

### File synchronization

*   **[rsync](/index.php/Rsync "Rsync")** — An incremental transfer and synchronization program.

	[http://rsync.samba.org](http://rsync.samba.org) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Open, trustworthy and decentralized cloud synchronization service.

	[https://syncthing.net](https://syncthing.net) || [syncthing](https://www.archlinux.org/packages/?name=syncthing)

*   **[Unison](/index.php/Unison "Unison")** — Bidirectional sync. It keeps track of changes like a VCS.

	[http://www.cis.upenn.edu/~bcpierce/unison](http://www.cis.upenn.edu/~bcpierce/unison) || [unison](https://www.archlinux.org/packages/?name=unison)

### Finders

*   **fuzzy-find** — Fuzzy completion for finding files.

	[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **fzf** — General-purpose command-line fuzzy finder.

	[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf)

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint

	[https://rmlint.readthedocs.org/en/latest/](https://rmlint.readthedocs.org/en/latest/) || [rmlint](https://www.archlinux.org/packages/?name=rmlint)