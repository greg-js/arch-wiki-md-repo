**[常用程序](/index.php/List_of_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications (简体中文)")**

* * *

[互联网](/index.php/List_of_Applications/Internet_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Internet (简体中文)") – [多媒体](/index.php/List_of_Applications/Multimedia_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Multimedia (简体中文)") – [工具](/index.php/List_of_Applications/Utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Utilities (简体中文)") – [文档](/index.php/List_of_Applications/Documents_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Documents (简体中文)") – [安全](/index.php/List_of_Applications/Security_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Security (简体中文)") – [科学](/index.php/List_of_Applications/Science_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Science (简体中文)") – [其它](/index.php/List_of_Applications/Other_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Other (简体中文)")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 工具](#工具)
    *   [1.1 分区工具](#分区工具)
    *   [1.2 挂载](#挂载)
        *   [1.2.1 Udisks](#Udisks)
    *   [1.3 基本 Shell 命令](#基本_Shell_命令)
    *   [1.4 集成式开发环境](#集成式开发环境)
    *   [1.5 虚拟终端](#虚拟终端)
        *   [1.5.1 基于 VTE](#基于_VTE)
        *   [1.5.2 KMS-based](#KMS-based)
        *   [1.5.3 framebuffer-based](#framebuffer-based)
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

### 虚拟终端

参见 [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

资深用户爱用虚拟终端，也难怪会有那么多 X11 虚拟终端冒出来了。大多虚拟终端在模拟 Xterm, Xterm 又向 VT102 看齐，最后 VT102 更是在模仿打字机，所以您应该品读 [Wikipedia article](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") 和 [other sources](https://google.com/search?q=linux+terminal+emulators) 以把握个大概。

*   **Eterm** — 取代 Xterm 且为 [Enlightenment](/index.php/Enlightenment "Enlightenment") 而打造。

	[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — 基于 linux kernel mode setting (KMS).

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — [KDE](/index.php/KDE "KDE") 专用。

	[http://kde.org/applications/system/konsole/](http://kde.org/applications/system/konsole/) || [kdebase-konsole](https://www.archlinux.org/packages/?name=kdebase-konsole)

*   **[Mrxvt](https://en.wikipedia.org/wiki/mrxvt "wikipedia:mrxvt")** — 基于 rxvt, 支持 Tabs.

	[http://materm.sourceforge.net/wiki/pmwiki.php](http://materm.sourceforge.net/wiki/pmwiki.php) || [mrxvt](https://aur.archlinux.org/packages/mrxvt/)

*   **QTerminal** — 基于 Qt, 轻量。

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal-git](https://aur.archlinux.org/packages/qterminal-git/)

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — 公认已取代 Xterm 的虚拟终端。

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://aur.archlinux.org/packages/rxvt/)

*   **[st](/index.php/St "St")** — 简单，在Ｘ下可用。

	[http://st.suckless.org](http://st.suckless.org) || [st](https://aur.archlinux.org/packages/st/)

*   **Terminal** — 支持多窗口，滚动缓冲以及众多理想功能，从属 GNUstep.

	[http://gap.nongnu.org/terminal/index.html](http://gap.nongnu.org/terminal/index.html) || [gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)

*   **[terminator](/index.php/Terminator "Terminator")** — 支持多 Panels.

	[http://gnometerminator.blogspot.it/](http://gnometerminator.blogspot.it/) || [terminator](https://www.archlinux.org/packages/?name=terminator)

*   **Terminology** — Enlightenment 项目专用，有众多金光闪闪的功能：文件缩略图，多媒体播放器。

	[http://enlightenment.org/p.php?p=about/terminology](http://enlightenment.org/p.php?p=about/terminology) || [terminology](https://www.archlinux.org/packages/?name=terminology)

*   **[Tilda](https://en.wikipedia.org/wiki/Tilda_(software) "wikipedia:Tilda (software)")** — 受众多 FPS 游戏，如 Quake, Doom 和半条命，启发而诞生。

	[http://sourceforge.net/projects/tilda/files/](http://sourceforge.net/projects/tilda/files/) || [tilda](https://www.archlinux.org/packages/?name=tilda)

*   **[urxvt](/index.php/Urxvt "Urxvt")** — 基于 Perl, rxvt, 高度可扩展，支持 Unicode, 多 Tab, 访问 URL, Quake 风格的下拉式，伪・透明。

	[http://software.schmorp.de/pkg/rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode) || [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)

*   **[xterm](/index.php/Xterm "Xterm")** — Ｘ最简单的虚拟终端了，它还为不能在窗口系统下直接用的程序，提供了兼容于 DEC VT102 和 Tektronix 4014 的终端。

	[http://invisible-island.net/xterm/](http://invisible-island.net/xterm/) || [xterm](https://www.archlinux.org/packages/?name=xterm)

*   **[Yakuake](https://en.wikipedia.org/wiki/Yakuake "wikipedia:Yakuake")** — 基于 Konsole, 下拉式，Quake 风格。

	[http://yakuake.kde.org/](http://yakuake.kde.org/) || [yakuake](https://www.archlinux.org/packages/?name=yakuake)

#### 基于 VTE

[VTE](http://developer.gnome.org/vte/unstable/) (Virtual Terminal Emulator) 最早是由 GNOME 开发并广泛使用的虚拟终端，它还派生了众多大大小小的分支。

*   **evilvte** — 很轻量，可定制性强，支持 Tabs, 自动隐藏，换编码。

	[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte](https://aur.archlinux.org/packages/evilvte/)

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — [GNOME](/index.php/GNOME "GNOME") 专用，支持 Unicode, 不支持透明。

	[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — GNOME 桌面的，下拉式的。

	[http://guake.org/](http://guake.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **Terra** — 基于 GTK+3.0, 同一个窗口上可以分割成众多小窗口。

	[https://github.com/ozcanesen/terra-terminal](https://github.com/ozcanesen/terra-terminal) || [terra](https://aur.archlinux.org/packages/terra/)

*   **[LilyTerm](/index.php/LilyTerm "LilyTerm")** — 很轻量。

	[http://lilyterm.luna.com.tw/](http://lilyterm.luna.com.tw/) || [lilyterm](https://www.archlinux.org/packages/?name=lilyterm)

*   **LXTerminal** — [LXDE](/index.php/LXDE "LXDE") 组件之一，也可单独安装。

	[http://wiki.lxde.org/en/LXTerminal](http://wiki.lxde.org/en/LXTerminal) || [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)

*   **MATE terminal** — [Wikipedia:GNOME terminal](https://en.wikipedia.org/wiki/GNOME_terminal "wikipedia:GNOME terminal") 在 [MATE](/index.php/MATE "MATE") 桌面上的 Fork.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)

*   **ROXTerm** — 有 Tab 机制。

	[http://roxterm.sourceforge.net/](http://roxterm.sourceforge.net/) || [roxterm](https://aur.archlinux.org/packages/roxterm/)

*   **sakura** — 基于 GTK+ 和 VTE.

	[http://www.pleyades.net/david/projects/sakura](http://www.pleyades.net/david/projects/sakura) || [sakura](https://www.archlinux.org/packages/?name=sakura)

*   **Stjerm** — 基于 GTK+, 下拉式，提供简约的界面，内存占用少，与合成窗口管理器有很好的互动，比如 Compiz.

	[https://code.google.com/p/stjerm-terminal-emulator/](https://code.google.com/p/stjerm-terminal-emulator/) || [stjerm-git](https://aur.archlinux.org/packages/stjerm-git/)

*   **[Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — [Xfce](/index.php/Xfce "Xfce") 桌面专用虚拟终端，支持颜色提示符，Tab 机制。

	[http://docs.xfce.org/apps/terminal/start](http://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

*   **Termit** — 简单，基于 VTE, 支持 Tabs, 书签，编码转换。

	[https://wiki.github.com/nonstop/termit/](https://wiki.github.com/nonstop/termit/) || [termit](https://aur.archlinux.org/packages/termit/)

*   **[Termite](/index.php/Termite "Termite")** — 适合命令行控，专为平铺式窗口管理器打造，还有 Tab 机制。

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

#### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

#### framebuffer-based

In GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") could be refered to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators that based on the in-kernel virtual device, i.e. **fbdev**.

*   **[fbterm](/index.php/Fbterm "Fbterm")** — A fast framebuffer-based terminal emulator with many amazing features. Development stopped.

	[http://code.google.com/p/fbterm/](http://code.google.com/p/fbterm/) || [fbterm](https://www.archlinux.org/packages/?name=fbterm)

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

	[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)

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