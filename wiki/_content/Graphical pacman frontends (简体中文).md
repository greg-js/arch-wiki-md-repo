# Graphical pacman frontends (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**翻译状态：** 本文是英文页面 [Pacman_GUI_Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-04-11，点击[这里](https://wiki.archlinux.org/index.php?title=Pacman_GUI_Frontends&diff=0&oldid=363006)可以查看翻译后英文页面的改动。

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

这里列出 [pacman](/index.php/Pacman "Pacman") 命令行工具的图形前端。本列表包括完整功能的 GUI 前端，信息化工具，以及一些系统托盘提示器。本列表也包含基于 Gtk2 或者 Qt 的软件类别。

**警告:** 这些工具都不是由Arch Linux/Pacman 开发人员官方支持的。

## Contents

*   [1 Pacman 图形化前端](#Pacman_.E5.9B.BE.E5.BD.A2.E5.8C.96.E5.89.8D.E7.AB.AF)
    *   [1.1 X11](#X11)
    *   [1.2 GNOME/GTK+](#GNOME.2FGTK.2B)
    *   [1.3 KDE/Qt](#KDE.2FQt)
    *   [1.4 NCurses](#NCurses)
*   [2 Pacman / AUR Package Browser](#Pacman_.2F_AUR_Package_Browser)
    *   [2.1 Pacinfo](#Pacinfo)
*   [3 System Tray Notifiers](#System_Tray_Notifiers)
    *   [3.1 Aarchup](#Aarchup)
    *   [3.2 Pacupdate](#Pacupdate)
    *   [3.3 Yapan](#Yapan)
    *   [3.4 ZenMan](#ZenMan)
    *   [3.5 pkgnotify.sh](#pkgnotify.sh)
*   [4 Inactive Software Packages](#Inactive_Software_Packages)

## Pacman 图形化前端

### X11

*   **PacmanXG4** — 是一个 pacman 的 GUI 前端。不依赖于 GTK 或者 Qt，仅仅依赖 X11。它可以完成以下功能：

*   安装/移除/升级软件包
*   搜索/过滤软件包
*   获取软件包信息，包括截图
*   降级软件包 (需要 AUR/downgrade 工具)
*   刷新包数据库，同步镜像
*   一键式系统升级
*   Find out which package a specific file belongs to (include file with pkgfile utility)
*   包缓冲管理
*   yaourt 支持

[http://almin-soft.ru/index.php?programmy/pacmanxg/tags/pacmanxg](http://almin-soft.ru/index.php?programmy/pacmanxg/tags/pacmanxg) (ru, present "Google site translate" ability) || [pacmanxg4-bin](https://aur.archlinux.org/packages/pacmanxg4-bin/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pacmanxg4-bin)]</sup>

*   **PacmanExpress** — 是一个 pacman 的 GUI 前端。不依赖于GTK或者QT,而仅仅依赖于X11。它是PacmanXG的一个轻量级版本。

*   Interface "all in one box"
*   没有提示。 安装/移除 软件包的操作将立即生效。（操作时要小心）
*   可同时执行不过多个操作（删除包时须小心）
*   yaourt 支持

[http://almin-soft.ru/index.php?programmy/pacmanexpress/tags/pacmanexpress](http://almin-soft.ru/index.php?programmy/pacmanexpress/tags/pacmanexpress) (ru, present "Google site translate" ability) || [pacmanexpress](https://aur.archlinux.org/packages/pacmanexpress/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pacmanexpress)]</sup>

*   **tkPacman** — GUI 是一个 pacman 的 GUI 前端。依赖于 Tcl/Tk 和 X11 却不是 GTK+ 或 QT。

It only interacts with the package database via the CLI of 'pacman'. So, installing and removing packages with tkPacman or with pacman leads to exactly the same result.

*   Browse packages available in repositories
*   Browse installed packages
*   Many ways to filter packages (word, group, repo, upgrades, orphans, explicit, foreign, fileowner)
*   Display detailed information for packages
*   Display list of files belonging to installed packages
*   Refresh package database
*   Full system upgrade
*   Install a package from a local file
*   View pacman.log file

[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)<sup><small>AUR</small></sup>

### GNOME/GTK+

*   **zenity_pacgui** — Pacman 的 Zenity 界面。

[http://sourceforge.net/projects/zenitypacgui/](http://sourceforge.net/projects/zenitypacgui/) || [zenity_pacgui](https://aur.archlinux.org/packages/zenity_pacgui/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/zenity_pacgui)]</sup>

*   **Argon** — 轻量级的 python GUI 软件包管理器

*   安装/移除软件包，以及系统升级。
*   包含AUR（通过 pacaur）
*   高级包列表top-level package list
*   可设置的升级提示器

[http://code.google.com/p/arch-argon](http://code.google.com/p/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)<sup><small>AUR</small></sup>

### KDE/Qt

*   **AppSet** — 是一个先进而又功能丰富的图形化软件包管理器。AppSet 有以下功能：

*   软件分类（games, office, multimedia, internet 等等）
*   在内嵌的浏览器中显示当前选中的软件包主页。
*   在内嵌的feed阅读器中显示发布新闻。
*   升级，安装和移除软件包。
*   在系统通知区域有图标显示可用的更新。
*   定期更新数据库。
*   报告依赖相关的信息 (例如当试图移除一个被其他包依赖的软件包时)。
*   清空缓存命令 (释放磁盘空间)。
*   智能的启动器可以自动使用已安装的工具来获取管理员权限 (通过搜索 kdesu/gksu 或者最少一个由 sudo 命令启动的 xterm)
*   目前以Paker为后端，提供AUR支持。

AppSet 仅需要 QT 库作为安装依赖。它可以在任何桌面环境中运行。 目前仅使用 Pacman 运行于 Arch Linux。

[http://appset.sourceforge.net/](http://appset.sourceforge.net/) || [appset-qt](https://aur.archlinux.org/packages/appset-qt/)<sup><small>AUR</small></sup>

*   **Octopi** — 用 Qt 写成的强大的 Pacman 图形化界面。其特点包括：

*   低资源消耗（包括内存）
*   快速
*   支持 Arch, ArchBang, Chakra 和 Manjaro Linux （注：貌似支持所有基于 Pacman 软件包管理工具的发行版）
*   支持 Cinnamon, KDE 4.x, XFCE, LXDE, LXQt, MATE, Openbox and TDE
*   支持系统托盘处图标通知
*   支持 Pacman 数据库同步，系统升级和缓存清理
*   支持 Yaourt 和 pacaur
*   安装/重新安装/升级/移除 选定的软件包 - 查看这些命令输出的需求 – 在一个基于 trasaction 抽象
*   查看已安装的软件包（包括打开和编辑文件）
*   要查看提示框里的软件包描述，只需在上面移动鼠标即可

Octopi 需要安装 Qt4/5 依赖库

[http://octopiproject.wordpress.com/](http://octopiproject.wordpress.com/) || [octopi](https://aur.archlinux.org/packages/octopi/)<sup><small>AUR</small></sup>

### NCurses

基于curses的包管理器前端。功能:

*   **pcurses** — 基于 curses 的图形化软件包管理器, 有以下功能:

*   正则表达式过滤和查询任何包的特性信息
*   自定义颜色编码
*   自定义排序
*   执行附加命令，可对包列表字符串进行替换
*   用户自定义marcos和hotkeys

[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **yaourt-gui** — Yaourt-GUI 是为了那些刚开始使用Archlinux的新用户设计的。 Written in bash, it offers a gui from terminal to the common tasks of yaourt and pacman

[http://alexiobash.com/yaourt-gui-a-bash-gui-per-yaourt-3/](http://alexiobash.com/yaourt-gui-a-bash-gui-per-yaourt-3/) || [yaourt-gui](https://aur.archlinux.org/packages/yaourt-gui/)<sup><small>AUR</small></sup>

## Pacman / AUR Package Browser

*   **PkgBrowser** — 用于搜索，查询软件包，显示选中软件包的详细信息。

*   查询和检索包括 AUR 在内的软件包。
*   它只是一个纯粹的显示信息的应用，不能用来安装、删除和升级软件包。
*   By design, is an accessory to CLI package management via pacman（未知原文意思，暂不翻译）
*   请自行通过帮助菜单访问进一步细节。

**论坛页面:** [https://bbs.archlinux.org/viewtopic.php?id=117297](https://bbs.archlinux.org/viewtopic.php?id=117297)  

[https://code.google.com/p/pkgbrowser/](https://code.google.com/p/pkgbrowser/) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)<sup><small>AUR</small></sup>

### Pacinfo

Pacinfo 用于显示已安装软件包并显示信息，例如软件截图，已安装的文件，安装日期等等。 基于 Mono/GTK#

**AUR 包:** [https://aur.archlinux.org/packages.php?ID=46065](https://aur.archlinux.org/packages.php?ID=46065)  
**主页:** [http://code.google.com/p/pacinfo/](http://code.google.com/p/pacinfo/)  

## System Tray Notifiers

### Aarchup

aarchup 是一个 archup 的分支。 拥有和 archup 相同的功能外加一些扩充功能。 请查阅关于两者更新日志之间差异的主题 [https://bbs.archlinux.org/viewtopic.php?id=119129](https://bbs.archlinux.org/viewtopic.php?id=119129)

*   主页: [https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/)
*   AUR 软件包详细信息: [https://aur.archlinux.org/packages.php?ID=49100](https://aur.archlinux.org/packages.php?ID=49100)
*   软件截图: [http://i.imgur.com/yTNvg.png](http://i.imgur.com/yTNvg.png)

### Pacupdate

Pacupdate 是一款轻量级的软件更新提醒工具。 如果 Pacupdate 发现一个可用的更新, 它会推送一个消息在系统托盘处.

*   主页 (过时): [http://code.google.com/p/pacupdate/](http://code.google.com/p/pacupdate/) **不要** 用'pacman -Sy foo'安装软件包 [可能会导致包损坏](https://bbs.archlinux.org/viewtopic.php?id=89328)。
*   AUR 软件包详细信息: [https://aur.archlinux.org/packages.php?ID=25082](https://aur.archlinux.org/packages.php?ID=25082)
*   Screenshots:

### Yapan

Yapan - Yet Another Package mAnager Notifier - is written in C++ and Qt. It shows an icon in the system tray and popup notifications for new packages and supports other package manager like clyde or yaourt.

*   Homepage: [https://bitbucket.org/otsug/yapan/wiki/Home](https://bitbucket.org/otsug/yapan/wiki/Home) , [https://bbs.archlinux.org/viewtopic.php?id=113078](https://bbs.archlinux.org/viewtopic.php?id=113078)
*   AUR Package Details: [https://aur.archlinux.org/packages.php?ID=46213](https://aur.archlinux.org/packages.php?ID=46213)
*   Screenshots: [https://bitbucket.org/otsug/yapan/wiki/Home](https://bitbucket.org/otsug/yapan/wiki/Home)

### ZenMan

PacMan frontend (tray update notifier) for GTK/GNOME/zenity/libnotify.

*   Homepage:
*   AUR Package Details: [https://aur.archlinux.org/packages.php?ID=25948](https://aur.archlinux.org/packages.php?ID=25948)
*   Screenshots: [http://show.harvie.cz/screenshots/zenman-screenshot-2.png](http://show.harvie.cz/screenshots/zenman-screenshot-2.png)

### pkgnotify.sh

A very simple 14 line shell script that displays the number of available updates in the dzen2 title window and a list of these updates in the slave window. Depends on yaourt, dzen2 and inotify-tools.

*   Homepage: [http://pointfree.net/repo/?r=dzen2_scripts;a=headblob;f=/src/pkgnotify/pkgnotify.sh](http://pointfree.net/repo/?r=dzen2_scripts;a=headblob;f=/src/pkgnotify/pkgnotify.sh)
*   AUR Package Details:
*   Screenshots: [http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2](http://andreasbwagner.tumblr.com/post/853471635/arch-linux-update-notifier-for-dzen2)

## Inactive Software Packages

*   [Wakka](https://code.google.com/p/wakka-package-manager/) - Next generation of gtkpacman
*   [GtkPacman](http://gtkpacman.berlios.de/)
*   [Guzuta](http://guzuta.berlios.de/)
*   [Shaman](http://chakra-project.org/wiki/index.php/Shaman)
*   [pacmon](http://code.google.com/p/pacmon/)
*   [Paku](https://gna.org/projects/paku/)
*   [YAPG](http://www.kde-apps.org/content/show.php/YAPG+-+Yet+Another+Pacman+Gui+?content=60052)
*   [zenity_pacgui](http://sourceforge.net/projects/zenitypacgui/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Graphical_pacman_frontends_(简体中文)&oldid=411645](https://wiki.archlinux.org/index.php?title=Graphical_pacman_frontends_(简体中文)&oldid=411645)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Arch User Repository (简体中文)](/index.php/Category:Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Arch User Repository (简体中文)")
*   [Package management (简体中文)](/index.php/Category:Package_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Package management (简体中文)")
*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")