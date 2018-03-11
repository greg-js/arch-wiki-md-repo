相关文章

*   [显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")
*   [窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")
*   [默认应用程序](/index.php/%E9%BB%98%E8%AE%A4%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F "默认应用程序")

[桌面环境](https://en.wikipedia.org/wiki/Desktop_environment "wikipedia:Desktop environment")通过汇集使用相同组件库的程序，为用户提供了*完全的*图形用户界面。

## Contents

*   [1 概况](#.E6.A6.82.E5.86.B5)
*   [2 桌面环境列表](#.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83.E5.88.97.E8.A1.A8)
    *   [2.1 官方支持](#.E5.AE.98.E6.96.B9.E6.94.AF.E6.8C.81)
    *   [2.2 非官方支持](#.E9.9D.9E.E5.AE.98.E6.96.B9.E6.94.AF.E6.8C.81)
*   [3 桌面环境比较](#.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83.E6.AF.94.E8.BE.83)
    *   [3.1 资源占用](#.E8.B5.84.E6.BA.90.E5.8D.A0.E7.94.A8)
    *   [3.2 相似之处](#.E7.9B.B8.E4.BC.BC.E4.B9.8B.E5.A4.84)
*   [4 自己打造桌面环境](#.E8.87.AA.E5.B7.B1.E6.89.93.E9.80.A0.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)

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

## 桌面环境比较

这一部分对几种流行的桌面环境进行比较，仅供用户参考。

参阅 [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

<caption>Overview of desktop environments</caption>
| Desktop environment | Widget toolkit | Window manager | Taskbar | Terminal emulator | File manager | Calculator | Text editor | Image viewer | Media player | Web browser | Display manager |
| [Budgie](/index.php/Budgie_Desktop "Budgie Desktop") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | budgie-wm
[budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) | budgie-panel
[budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | [GDM](/index.php/GDM "GDM")
[gdm](https://www.archlinux.org/packages/?name=gdm) |
| [Cinnamon](/index.php/Cinnamon "Cinnamon") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | Muffin
[muffin](https://www.archlinux.org/packages/?name=muffin) | Cinnamon
[cinnamon](https://www.archlinux.org/packages/?name=cinnamon) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [Nemo](/index.php/Nemo "Nemo")
[nemo](https://www.archlinux.org/packages/?name=nemo) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Deepin](/index.php/Deepin "Deepin") | [GTK+](/index.php/GTK%2B "GTK+") 2/3, [Qt](/index.php/Qt "Qt") 5
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | Deepin Window Manager
[deepin-wm](https://www.archlinux.org/packages/?name=deepin-wm) | Deepin Dock
[deepin-dock](https://www.archlinux.org/packages/?name=deepin-dock) | Deepin Terminal
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal) | Deepin File Manager
[deepin-file-manager](https://www.archlinux.org/packages/?name=deepin-file-manager) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | Deepin Image Viewer
[deepin-image-viewer](https://www.archlinux.org/packages/?name=deepin-image-viewer) | Deepin Movie
[deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie) | [Chromium](/index.php/Chromium "Chromium")
[chromium](https://www.archlinux.org/packages/?name=chromium) | [LightDM](/index.php/LightDM "LightDM") Deepin Greeter
[deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui) |
| [EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment") | [FLTK](http://www.fltk.org/)
[fltk](https://www.archlinux.org/packages/?name=fltk) | [PekWM](/index.php/PekWM "PekWM")
[ede](https://aur.archlinux.org/packages/ede/) | EDE Panel
[ede](https://aur.archlinux.org/packages/ede/) | [XTerm](/index.php/Xterm "Xterm")
[xterm](https://www.archlinux.org/packages/?name=xterm) | Fluff
[fluff](https://aur.archlinux.org/packages/fluff/) | Calculator
[ede](https://aur.archlinux.org/packages/ede/) | Editor
[fltk-editor](https://aur.archlinux.org/packages/fltk-editor/) | Image Viewer
[ede](https://aur.archlinux.org/packages/ede/) | flmusic
[flmusic](https://aur.archlinux.org/packages/flmusic/) | [Dillo](/index.php/Dillo "Dillo")
[dillo](https://www.archlinux.org/packages/?name=dillo) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Enlightenment](/index.php/Enlightenment "Enlightenment") | [EFL](https://www.enlightenment.org/about-efl)
[efl](https://www.archlinux.org/packages/?name=efl) | [Enlightenment](https://www.enlightenment.org/about-enlightenment)
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [Enlightenment](https://www.enlightenment.org/about-enlightenment)
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [Terminology](https://www.enlightenment.org/about-terminology)
[terminology](https://www.archlinux.org/packages/?name=terminology) | [Enlightenment](https://www.enlightenment.org/about-enlightenment)
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | Equate
[equate-git](https://aur.archlinux.org/packages/equate-git/) | Ecrire
[ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) | [Ephoto](https://www.enlightenment.org/about-ephoto)
[ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) | [Rage](https://www.enlightenment.org/about-rage)
[rage](https://aur.archlinux.org/packages/rage/) | [Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")
[links](https://www.archlinux.org/packages/?name=links) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [GNOME](/index.php/GNOME "GNOME") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")
[mutter](https://www.archlinux.org/packages/?name=mutter) | [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell")
[gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | [GDM](/index.php/GDM "GDM")
[gdm](https://www.archlinux.org/packages/?name=gdm) |
| [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")
[metacity](https://www.archlinux.org/packages/?name=metacity) | [GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")
[gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | [GDM](/index.php/GDM "GDM")
[gdm](https://www.archlinux.org/packages/?name=gdm) |
| [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") | [Qt](/index.php/Qt "Qt") 5
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")
[kwin](https://www.archlinux.org/packages/?name=kwin) | [Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_5#Desktop "wikipedia:KDE Plasma 5")
[plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) | [Konsole](http://konsole.kde.org/)
[konsole](https://www.archlinux.org/packages/?name=konsole) | [Dolphin](http://dolphin.kde.org/)
[dolphin](https://www.archlinux.org/packages/?name=dolphin) | [KCalc](http://www.kde.org/applications/utilities/kcalc/)
[kcalc](https://www.archlinux.org/packages/?name=kcalc) | [KWrite/Kate](http://kate-editor.org/)
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [Gwenview](http://gwenview.sourceforge.net/)
[gwenview](https://www.archlinux.org/packages/?name=gwenview) | [Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)
[dragon](https://www.archlinux.org/packages/?name=dragon) | [Konqueror](http://www.konqueror.org/)
[konqueror](https://www.archlinux.org/packages/?name=konqueror) | [SDDM](/index.php/SDDM "SDDM")
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [Liri](/index.php/Liri "Liri") | [Qt](/index.php/Qt "Qt") 5
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | Green Island
[greenisland](https://aur.archlinux.org/packages/greenisland/) | Liri Shell
[liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/) | Liri Terminal
[liri-terminal-git](https://aur.archlinux.org/packages/liri-terminal-git/) | Liri Files
[liri-files-git](https://aur.archlinux.org/packages/liri-files-git/) | Liri Calculator
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=liri-calculator-git)</small> | Liri Text
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=liri-text-git)</small> | EyeSight
[eyesight](https://aur.archlinux.org/packages/eyesight/) | Liri Player
[liri-player-git](https://aur.archlinux.org/packages/liri-player-git/) | Liri Browser
[liri-browser-git](https://aur.archlinux.org/packages/liri-browser-git/) | SDDM
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [LXDE](/index.php/LXDE "LXDE") (GTK+ 2) | [GTK+](/index.php/GTK%2B "GTK+") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | [LXPanel](http://wiki.lxde.org/en/LXPanel)
[lxpanel](https://www.archlinux.org/packages/?name=lxpanel) | [LXTerminal](http://wiki.lxde.org/en/LXTerminal)
[lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | [PCManFM](/index.php/PCManFM "PCManFM")
[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [Leafpad](http://tarot.freeshell.org/leafpad/)
[leafpad](https://www.archlinux.org/packages/?name=leafpad) | [GPicView](http://wiki.lxde.org/en/GPicView)
[gpicview](https://www.archlinux.org/packages/?name=gpicview) | [LXMusic](http://wiki.lxde.org/en/LXMusic)
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LXDM](/index.php/LXDM "LXDM")
[lxdm](https://www.archlinux.org/packages/?name=lxdm) |
| [LXDE](/index.php/LXDE "LXDE") (GTK+ 3) | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | [LXPanel](http://wiki.lxde.org/en/LXPanel)
[lxpanel-gtk3](https://www.archlinux.org/packages/?name=lxpanel-gtk3) | [LXTerminal](http://wiki.lxde.org/en/LXTerminal)
[lxterminal-gtk3](https://www.archlinux.org/packages/?name=lxterminal-gtk3) | [PCManFM](/index.php/PCManFM "PCManFM")
[pcmanfm-gtk3](https://www.archlinux.org/packages/?name=pcmanfm-gtk3) | [Galculator](http://galculator.sourceforge.net/)
[galculator](https://www.archlinux.org/packages/?name=galculator) | L3afpad
[l3afpad](https://www.archlinux.org/packages/?name=l3afpad) | [GPicView](http://wiki.lxde.org/en/GPicView)
[gpicview-gtk3](https://www.archlinux.org/packages/?name=gpicview-gtk3) | [LXMusic](http://wiki.lxde.org/en/LXMusic)
[lxmusic-gtk3](https://www.archlinux.org/packages/?name=lxmusic-gtk3) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LXDM](/index.php/LXDM "LXDM")
[lxdm-gtk3](https://www.archlinux.org/packages/?name=lxdm-gtk3) |
| [LXQt](/index.php/LXQt "LXQt") | [Qt](/index.php/Qt "Qt") 5
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | LXQt Panel
[lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel) | QTerminal
[qterminal](https://www.archlinux.org/packages/?name=qterminal) | PCManFM-Qt
[pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) | [SpeedCrunch](http://speedcrunch.org/)
[speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch) | Notepadqq
[notepadqq](https://www.archlinux.org/packages/?name=notepadqq) | LxImage-Qt
[lximage-qt](https://www.archlinux.org/packages/?name=lximage-qt) | SMPlayer
[smplayer](https://www.archlinux.org/packages/?name=smplayer) | QupZilla
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | SDDM
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [MATE](/index.php/MATE "MATE") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | Marco
[marco](https://www.archlinux.org/packages/?name=marco) | MATE Panel
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel) | MATE Terminal
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Caja
[caja](https://www.archlinux.org/packages/?name=caja) | MATE Calc
[mate-calc](https://www.archlinux.org/packages/?name=mate-calc) | pluma
[pluma](https://www.archlinux.org/packages/?name=pluma) | Eye of MATE
[eom](https://www.archlinux.org/packages/?name=eom) | [Parole](http://docs.xfce.org/apps/parole/start)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Pantheon](/index.php/Pantheon "Pantheon") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Gala](https://launchpad.net/gala)
[gala-git](https://aur.archlinux.org/packages/gala-git/) | [Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/) | [Pantheon Terminal](https://launchpad.net/pantheon-terminal)
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | [Pantheon Files](https://launchpad.net/pantheon-files)
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) | [Pantheon Calculator](https://launchpad.net/pantheon-calculator)
[pantheon-calculator](https://aur.archlinux.org/packages/pantheon-calculator/) | [Scratch](https://launchpad.net/scratch)
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) | [Pantheon Photos](https://launchpad.net/pantheon-photos)
[pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) | [Audience](https://launchpad.net/audience)
[audience](https://www.archlinux.org/packages/?name=audience) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | [LightDM](/index.php/LightDM "LightDM") Pantheon Greeter
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/) |
| [Sugar](/index.php/Sugar "Sugar") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")
[metacity](https://www.archlinux.org/packages/?name=metacity) | Sugar
[sugar](https://www.archlinux.org/packages/?name=sugar) | Terminal
[sugar-activity-terminal](https://www.archlinux.org/packages/?name=sugar-activity-terminal) | Sugar Journal
[sugar](https://www.archlinux.org/packages/?name=sugar) | Calculate
[sugar-activity-calculate](https://www.archlinux.org/packages/?name=sugar-activity-calculate) | Write
[sugar-activity-write](https://www.archlinux.org/packages/?name=sugar-activity-write) | ImageViewer
[sugar-activity-imageviewer](https://www.archlinux.org/packages/?name=sugar-activity-imageviewer) | Jukebox
[sugar-activity-jukebox](https://www.archlinux.org/packages/?name=sugar-activity-jukebox) | Browse
[sugar-activity-browse](https://www.archlinux.org/packages/?name=sugar-activity-browse) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| theShell | [Qt](/index.php/Qt "Qt") 5
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")
[kwin](https://www.archlinux.org/packages/?name=kwin) | theShell
[theshell](https://aur.archlinux.org/packages/theshell/) | theTerminal
[theterminal](https://aur.archlinux.org/packages/theterminal/) | theFile
[thefile](https://aur.archlinux.org/packages/thefile/) | theCalculator
[thecalculator](https://aur.archlinux.org/packages/thecalculator/) | [KWrite/Kate](http://kate-editor.org/)
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [Gwenview](http://gwenview.sourceforge.net/)
[gwenview](https://www.archlinux.org/packages/?name=gwenview) | theMedia
[themedia](https://aur.archlinux.org/packages/themedia/) | theWeb
[theweb](https://aur.archlinux.org/packages/theweb/) | [LightDM](/index.php/LightDM "LightDM") Contemporary Greeter
[lightdm-webkit-theme-contemporary](https://aur.archlinux.org/packages/lightdm-webkit-theme-contemporary/) |
| [Trinity](/index.php/Trinity "Trinity") | TQt | TWin | Kicker | Konsole | Konqueror | KCalc | Kwrite / Kate | Kuickshow | Kaffeine | Konqueror | TDM |
| [Xfce](/index.php/Xfce "Xfce") | [GTK+](/index.php/GTK%2B "GTK+") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Xfwm4](http://docs.xfce.org/xfce/xfwm4/start)
[xfwm4](https://www.archlinux.org/packages/?name=xfwm4) | [Xfce Panel](http://docs.xfce.org/xfce/xfce4-panel/start)
[xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel) | [Terminal](http://www.xfce.org/projects/terminal)
[xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | [Thunar](/index.php/Thunar "Thunar")
[thunar](https://www.archlinux.org/packages/?name=thunar) | [Galculator](http://galculator.sourceforge.net/)
[galculator](https://www.archlinux.org/packages/?name=galculator) | Mousepad
[mousepad](https://www.archlinux.org/packages/?name=mousepad) | [Ristretto](http://goodies.xfce.org/projects/applications/ristretto)
[ristretto](https://www.archlinux.org/packages/?name=ristretto) | [Parole](http://docs.xfce.org/apps/parole/start)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |

### 资源占用

此处在资源占用（CPU、内存、磁盘空间）上比较各种桌面环境。

*   GNOME和KDE：属于**高资源占用**桌面环境。相对来讲，它们**功能更为丰富**，是最完整的桌面环境。

*   E17、LXDE和Xfce：属于**轻量**桌面环境。它们通常是为低能耗设备或是旧机器设计的，占用更少资源。

### 相似之处

许多人说，KDE像Windows，GNOME像Mac。这样的评价不怎么客观，毕竟它们并不能模拟Windows或是Mac。参见：[KDE比GNOME更像Windows吗](http://www.psychocats.net/ubuntucat/is-kde-more-windows-like-than-gnome/)（[中文版](http://fyyz.me/is-kde-more-windows-like-than-gnome/)），[KDE vs GNOME](http://www.jeffwu.net/?p=71)，[经典文章：Linux不是Windows](http://linux.oneandoneis2.org/LNW.htm)。

## 自己打造桌面环境

桌面环境是安装完整图形环境的最简单的方法。但是，如果主流桌面环境并不能满足用户的需求，那么用户也可以通过多种方法来构建和定制他们自己的图形环境。通常，构建一个自定义的环境包括选择一个合适的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")，一个[任务栏](/index.php/List_of_applications#Taskbars_.2F_panels_.2F_docks "List of applications")以及一些应用程序(一个极简的应用程序选择方案至少包括一个终端模拟器([terminal emulator](/index.php/Terminal_emulator "Terminal emulator"))，文件管理器([file manager](/index.php/File_manager "File manager"))和文本编辑器([text editor](/index.php/Text_editor "Text editor")))。

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