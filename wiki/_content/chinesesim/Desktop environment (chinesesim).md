相关文章

*   [显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")
*   [窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")
*   [默认应用程序](/index.php/%E9%BB%98%E8%AE%A4%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F "默认应用程序")

[桌面环境](https://en.wikipedia.org/wiki/Desktop_environment "wikipedia:Desktop environment")通过汇集使用相同组件库的程序，为用户提供了*完全的*图形用户界面。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 概况](#概况)
*   [2 桌面环境列表](#桌面环境列表)
    *   [2.1 官方支持](#官方支持)
    *   [2.2 非官方支持](#非官方支持)
*   [3 自己打造桌面环境](#自己打造桌面环境)
    *   [3.1 使用其它窗口管理器](#使用其它窗口管理器)

## 概况

桌面环境结合X客户端，提供通用图形用户界面元素,如图标、工具栏、壁纸,桌面小部件。 大多数桌面环境包括提供一套整合的应用程序和实用工具。 最重要的是，桌面环境提供他们自己的 [window manager](/index.php/Window_manager "Window manager"), 但是通常被替换为另一个兼容的。

用户可以自由搭配不同桌面环境的程序，桌面环境只是提供一个完整的和方便的方法完成这项任务。请注意，用户可以自由地混合和匹配来自多个桌面环境中的应用。 例如，KDE 用户可以安装和运行 GNOME 应用程序如Epiphany web 浏览器，他/她宁愿在 KDE 的 Konqueror web 浏览器。 这种方法的一个缺点是,许多应用程序提供的桌面环境项目严重依赖其DE各自底层库。因此，从一系列桌面环境中安装应用程序将需要安装更多的依赖关系。用户为了节省磁盘空间，通常不会使用这样的混合环境,他们会考虑轻量级替代方案。

此外，桌面环境自带的程序，与该桌面环境整合最佳。从表面上看，混合环境中的部件工具包会造成视觉上的差异。(也就是说,接口将使用不同的图标和小部件样式)。 在用户体验方面，混合环境中的行为可能同样可能造成混乱或意外的行为。(例如单点击与双击图标;拖和拖放功能)

在安装桌面环境之前，X 服务器安装是必需的。详细信息，请参阅 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")。

## 桌面环境列表

### 官方支持

*   **[Budgie](/index.php/Budgie_Desktop "Budgie Desktop")** — Budgie 是一款专为现代用户而设计的桌面环境，它专注于简单和优雅。

	[https://budgie-desktop.org/](https://budgie-desktop.org/) || [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop)

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon 致力于提供传统的用户体验。Cinnamon 是一个 fork GNOME 3 的项目。

	[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin "Deepin")** — Deepin 桌面界面和应用程序功能的直观和优雅的设计。四处移动，共享和搜索等已经成为一个简单的愉悦体验。

	[https://www.deepin.org/](https://www.deepin.org/) || [deepin](https://www.archlinux.org/groups/x86_64/deepin/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Enlightenment desktop shell 提供了基于 Enlightenment Foundation Libraries 的高效窗口管理器以及其他基本桌面组件，如文件管理器，桌面图标和小部件。它支持主题，并能够在较旧的硬件或嵌入式设备上执行。

	[https://www.enlightenment.org/](https://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME "GNOME")** — GNOME桌面环境是一个既具有现代（'GNOME'）又有经典（'GNOME Classic'）会话的迷人而直观的桌面。

	[https://www.gnome.org/gnome-3/](https://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback 是 GNOME 3的一个 shell ，最初称为 GNOME 后备模式。桌面布局和底层技术与 GNOME 2 类似。

	[https://wiki.gnome.org/Projects/GnomeFlashback](https://wiki.gnome.org/Projects/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **[KDE Plasma](/index.php/KDE_Plasma "KDE Plasma")** — KDE Plasma桌面环境是一个熟悉的工作环境。Plasma 提供了现代桌面计算体验所需的所有工具，因此您可以从一开始就提高生产力。

	[https://www.kde.org/plasma-desktop](https://www.kde.org/plasma-desktop) || [plasma](https://www.archlinux.org/groups/x86_64/plasma/)

*   **[LXDE](/index.php/LXDE "LXDE")** — 轻量级X11桌面环境是一个快速和节能的桌面环境。它配备了现代界面，多语言支持，标准键盘快捷键和附加功能，如标签式文件浏览。 LXDE的基本设计是轻量级的，其努力比其他环境更少地占用CPU和内存。

	[http://lxde.org/](http://lxde.org/) || GTK+ 2: [lxde](https://www.archlinux.org/groups/x86_64/lxde/), GTK+ 3: [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/)

*   **[LXQt](/index.php/LXQt "LXQt")** — LXQt 是轻量级桌面环境 LXDE 的下一代产品，基于 Qt 开发。 它是合并的LXDE Qt和Razor-qt项目之间的产品: 一个轻量级，模块化，速度极快的和用户友好的桌面环境。

	[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE "MATE")** — Mate为使用传统隐喻的Linux用户提供了一个直观而有吸引力的桌面。 MATE最初是GNOME 2的一个分支，但现在使用GTK + 3。

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Sugar](/index.php/Sugar "Sugar")** — Sugar是一个为5-12岁孩子提供学习帮助的桌面环境，并且集成了多媒体的活动。在为全世界每一位孩子提供素质教育机会的计划中，Sugar是其核心组成部分 — 目前全世界有将近一百万小孩使用该桌面环境，他们讲着25种语言，来自40多个国家。在Sugar的帮助下，他们有机会接受素质教育，从而成就自己的人生。

	[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://www.archlinux.org/packages/?name=sugar)

	[Xfce](/index.php/Xfce "Xfce")

	轻量桌面环境Xfce，是Unix模块化、重用代码理念的践行者。其中包含各种功能的组件，是真正现代的桌面环境。各个组件划分成不同的包，用户可以自由选取需要的安装使用。

	[ROX](/index.php/ROX_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ROX (简体中文)")

	ROX是一个高效、友好的桌面环境。它的核心是文件浏览器，秉承传统Unix的“一切皆文件”理念，而非把一切都放在菜单、向导什么的里面。ROX致力于打造设计完善且功能清晰的桌面环境，把一些小型程序结合在一起（而不是搞整合的万能软件）。

### 非官方支持

*   **[CDE](/index.php/CDE "CDE")** — The Common Desktop Environment (CDE) is a desktop environment for Unix and OpenVMS, based on the Motif widget toolkit. It was part of the UNIX98 Workstation Product Standard, and was long the "classic" Unix desktop associated with commercial Unix workstations.

	[http://sourceforge.net/projects/cdesktopenv/](http://sourceforge.net/projects/cdesktopenv/) || [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/)

*   **[Liri](/index.php/Liri "Liri")** — Liri 是具有现代设计和功能的桌面环境。合并了 [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) 和 [Liri Project](https://github.com/liri-project)。实验版本。

	[https://liri.io/](https://liri.io/) || [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina是一个轻量级桌面环境用QT5写在FreeBSD,使用Fluxbox窗口管理。

	[http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/](http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/) || [lumina-desktop-git](https://aur.archlinux.org/packages/lumina-desktop-git/)

*   **Maynard** — Maynard 是[Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi") 桌面环境设计的(但不限于它) 在[Wayland](/index.php/Wayland "Wayland")运行。

	[https://github.com/raspberrypi/maynard](https://github.com/raspberrypi/maynard) || [maynard-git](https://aur.archlinux.org/packages/maynard-git/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon 是elementary OS 操作系统的默认桌面环境。它是从头开始使用 Vala和GTK3工具包写。至于易用性和外观，桌面与GNOME Shell和Mac OS X有一些相似之处。

	[https://elementary.io/](https://elementary.io/) || [pantheon-session-git](https://aur.archlinux.org/packages/pantheon-session-git/)

*   **theShell** — theShell is a desktop environment that tries to be as transparent as possible. It uses Qt 5 as its widget toolkit and KWin as its window manager. It also incorporates a personal assistant.

	[https://vicr123.github.io/theshell](https://vicr123.github.io/theshell) || [theshell](https://aur.archlinux.org/packages/theshell/)

*   **[Trinity](/index.php/Trinity "Trinity")** — The Trinity Desktop Environment (TDE) project is a computer desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

## 自己打造桌面环境

桌面环境是安装完整图形环境的最简单的方法。但是，如果主流桌面环境并不能满足用户的需求，那么用户也可以通过多种方法来构建和定制他们自己的图形环境。通常，构建一个自定义的环境包括选择一个合适的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")，一个[任务栏](/index.php/List_of_applications#Taskbars_/_panels_/_docks "List of applications")以及一些应用程序(一个极简的应用程序选择方案至少包括一个终端模拟器([terminal emulator](/index.php/Terminal_emulator "Terminal emulator"))，文件管理器([file manager](/index.php/File_manager "File manager"))和文本编辑器([text editor](/index.php/Text_editor "Text editor")))。

通常由桌面环境提供的其它应用程序有：

*   Application launcher: [List of applications#Application launchers](/index.php/List_of_applications#Application_launchers "List of applications")
*   Clipboard manager: [Clipboard#List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard")
*   Desktop compositor: [Xorg#Composite](/index.php/Xorg#Composite "Xorg")
*   Desktop wallpaper setter and desktop icon: [List of applications#Wallpaper setters](/index.php/List_of_applications#Wallpaper_setters "List of applications") and [Openbox#Icon programs](/index.php/Openbox#Icon_programs "Openbox")
*   Display manager: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager")
*   Display power saving settings: [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   Logout dialogue: [List of applications#Logout dialogue](/index.php/List_of_applications#Logout_dialogue "List of applications")
*   Mount tool: [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications")
*   Notification daemon: [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications")
*   Polkit authentication agent: [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")
*   Screen locker: [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")
*   Sound volume manager: [List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications")

### 使用其它窗口管理器

*   [Budgie#Use a different window manager](/index.php/Budgie#Use_a_different_window_manager "Budgie")
*   [Cinnamon#Use a different window manager](/index.php/Cinnamon#Use_a_different_window_manager "Cinnamon")
*   [GNOME#Use a different window manager](/index.php/GNOME#Use_a_different_window_manager "GNOME")
*   [KDE#Use a different window manager](/index.php/KDE#Use_a_different_window_manager "KDE")
*   [LXDE#Use a different window manager](/index.php/LXDE#Use_a_different_window_manager "LXDE")
*   [LXQt#Use a different window manager](/index.php/LXQt#Use_a_different_window_manager "LXQt")
*   [MATE#Use a different window manager](/index.php/MATE#Use_a_different_window_manager "MATE")
*   [Xfce#Use a different window manager](/index.php/Xfce#Use_a_different_window_manager "Xfce")