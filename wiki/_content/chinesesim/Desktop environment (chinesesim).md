在X图形系统基础上，**桌面环境**为计算机提供*完全的*图形用户界面（GUI）。

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

用户可以自由搭配不同桌面环境的程序，桌面环境只是提供一个完整的和方便的方法完成这项任务。请注意，用户可以自由地混合和匹配来自多个桌面环境中的应用。 例如，KDE 用户可以安装和运行 GNOME 应用程序如Epiphany web 浏览器，他/她宁愿在 KDE 的 Konqueror web 浏览器。 这种方法的一个缺点是,许多应用程序提供的桌面环境项目严重依赖其DE各自底层库。因此，从一系列桌面环境中安装应用程序将需要安装更多的依赖关系。用户为了节省磁盘空间，避免软件膨胀[software bloat](https://en.wikipedia.org/wiki/software_bloat "wikipedia:software bloat")通常避免这样的混合环境中,或考虑轻量级替代方案。

此外，桌面环境自带的程序，与该桌面环境整合最佳。从表面上看，混合环境中的部件工具包会造成视觉上的差异。(也就是说,接口将使用不同的图标和小部件样式)。 在用户体验方面，混合环境中的行为可能同样可能造成混乱或意外的行为。(例如单点击与双击图标;拖和拖放功能)

在安装桌面环境之前，X 服务器安装是必需的。详细信息，请参阅 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")。

## 桌面环境列表

### 官方支持

[Cinnamon](/index.php/Cinnamon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cinnamon (简体中文)")：Cinnamon 致力于提供传统的用户体验。Cinnamon 是一个fork GNOME 3的项目。[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/)[cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

	[E17](/index.php/E17_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "E17 (简体中文)")

	E17，即Enlightenment桌面环境，基于Enlightenment库，该桌面环境提供了高效又美观的窗口管理器。同时还附带了文件管理器、桌面图标、桌面部件等必备组件。它提供了高级的美化功能，同时又适用于旧机器和嵌入式设备。

	[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")

	GNOME计划带来了两个东西：一是很好很强大的GNOME桌面环境，是目前最主流的桌面环境之一；二是GNOME开发平台，帮助开发整合于用户桌面的实用程序。GNOME是自由的、易用的、国际化的、面向开发者的、有强力支持的。

	[KDE Plasma](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")

	KDE Plasma桌面是一个熟悉的工作环境。Plasma Desktop桌面提供了一个现代桌面计算体验所需的所有工具，这样你就可以从一开始就有生产力。

	[LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")

	正如其名，LXDE（Lightweight X11 Desktop Environment，轻量X11桌面环境）是一个快速、简洁、轻量的桌面环境。它由来自全球各地的开发者维护，具有界面美观、多语言支持、键盘快捷键等诸多实用特性。比起其他桌面环境，LXDE占用更少的CPU、内存，是为上网本、移动设备、旧机器特别设计的轻量桌面环境。

	[LXQt](/index.php/LXQt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXQt (简体中文)")

	LXQt 是轻量级桌面环境 LXDE 的下一代产品，基于 Qt 开发。 它是合并的LXDE Qt和Razor-qt项目之间的产品: 一个轻量级，模块化，速度极快的和用户友好的桌面环境。[http://lxqt.org/](http://lxqt.org/)[lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

	[MATE](/index.php/MATE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MATE (简体中文)")

	Mate 使用传统方式为 Linux 用户提供了直观和有吸引力的桌面。操作方式和Gnome2几乎一样。

	[Xfce](/index.php/Xfce "Xfce")

	轻量桌面环境Xfce，是Unix模块化、重用代码理念的践行者。其中包含各种功能的组件，是真正现代的桌面环境。各个组件划分成不同的包，用户可以自由选取需要的安装使用。

	[ROX](/index.php/ROX_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ROX (简体中文)")

	ROX是一个高效、友好的桌面环境。它的核心是文件浏览器，秉承传统Unix的“一切皆文件”理念，而非把一切都放在菜单、向导什么的里面。ROX致力于打造设计完善且功能清晰的桌面环境，把一些小型程序结合在一起（而不是搞整合的万能软件）。

### 非官方支持

*   **[Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop")** — Budgie 桌面是一个轻量级桌面环境设计充分考虑了现代用户，它着重于简洁和漂亮。此外，它类似于 Chrome/ Chromium OS桌面布局

	[https://solus-project.com/budgie/](https://solus-project.com/budgie/) || [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)

*   **[CDE](/index.php/CDE "CDE")** — The Common Desktop Environment (CDE) is a desktop environment for Unix and OpenVMS, based on the Motif widget toolkit. It was part of the UNIX98 Workstation Product Standard, and was long the "classic" Unix desktop associated with commercial Unix workstations.

	[http://sourceforge.net/projects/cdesktopenv/](http://sourceforge.net/projects/cdesktopenv/) || [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/)

*   **[Deepin Desktop Environment](/index.php/Deepin_Desktop_Environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Deepin Desktop Environment (简体中文)")** — Deepin桌面界面和应用程序功能的直观和优雅的设计。四处移动，共享和搜索等已经成为一个简单的愉悦体验。

	[http://www.linuxdeepin.com/](http://www.linuxdeepin.com/) || [deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/)

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — “Equinox桌面环境”是一个DE设计简单,非常轻,快。

	[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback is a shell for GNOME 3 which was initially called GNOME fallback mode. The desktop layout and the underlying technology is similar to GNOME 2.

	[https://wiki.gnome.org/GnomeFlashback](https://wiki.gnome.org/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **GNUstep** — GNUstep是一个免费的、面向对象、跨平台开发环境,力求简洁和优雅。

	[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker) [gworkspace](https://aur.archlinux.org/packages/gworkspace/)

*   **[Hawaii](/index.php/Hawaii "Hawaii")** — Hawaii 一个轻量级的、一致的和快速的桌面环境,依赖于Qt5，QtQuick和Wayland ,旨在提供最佳的用户体验在它所运行的设备。

	[http://www.maui-project.org/](http://www.maui-project.org/) || [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina是一个轻量级桌面环境用QT5写在FreeBSD,使用Fluxbox窗口管理。

	[http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/](http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/) || [lumina-desktop-git](https://aur.archlinux.org/packages/lumina-desktop-git/)

*   **Maynard** — Maynard 是[Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi") 桌面环境设计的(但不限于它) 在[Wayland](/index.php/Wayland "Wayland")运行。

	[https://github.com/raspberrypi/maynard](https://github.com/raspberrypi/maynard) || [maynard-git](https://aur.archlinux.org/packages/maynard-git/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon 是elementary OS 操作系统的默认桌面环境。它是从头开始使用 Vala和GTK3工具包写。至于易用性和外观，桌面与GNOME Shell和Mac OS X有一些相似之处。

	[http://elementaryos.org/](http://elementaryos.org/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)

*   **[ROX](/index.php/ROX "ROX")** — ROX is a fast, user friendly desktop which makes extensive use of drag-and-drop. The interface revolves around the file manager, following the traditional UNIX view that 'everything is a file' rather than trying to hide the filesystem beneath start menus, wizards, or druids. The aim is to make a system that is well designed and clearly presented. The ROX style favors using several small programs together instead of creating all-in-one mega-applications.

	[http://rox.sourceforge.net/desktop/](http://rox.sourceforge.net/desktop/) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[Sugar](/index.php/Sugar "Sugar")** — Sugar是一个为5-12岁孩子提供学习帮助的桌面环境，并且集成了多媒体的活动。在为全世界每一位孩子提供素质教育机会的计划中，Sugar是其核心组成部分 — 目前全世界有将近一百万小孩使用该桌面环境，他们讲着25种语言，来自40多个国家。在Sugar的帮助下，他们有机会接受素质教育，从而成就自己的人生。

	[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://aur.archlinux.org/packages/sugar/)

*   **[Trinity](/index.php/Trinity "Trinity")** — The Trinity Desktop Environment (TDE) project is a computer desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — Unity 就是一个GNOME shell 被Canonical的Ubuntu开发。

	[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || [unity](https://aur.archlinux.org/packages/unity/)

## 桌面环境比较

这一部分对几种流行的桌面环境进行比较，仅供用户参考。

参阅 [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

<caption>桌面环境比较</caption>
| 桌面环境 | 窗口小部件工具 | 窗口管理器 | 任务栏 | 终端 | 文件管理器 | 日历 | 文本编辑器 | 图片查看器 | 媒体播放器 | 浏览器 | 显示管理 |
| [Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | budgie-wm
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) | budgie-panel
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [Budgie Media Player](https://github.com/evolve-os/budgie-media-player)
[budgie-git](https://aur.archlinux.org/packages/budgie-git/) | [Chromium](/index.php/Chromium "Chromium")
[chromium](https://www.archlinux.org/packages/?name=chromium) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Cinnamon](/index.php/Cinnamon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cinnamon (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
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
| [Deepin_Desktop_Environment](/index.php/Deepin_Desktop_Environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Deepin Desktop Environment (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Compiz](/index.php/Compiz "Compiz")
[compiz](https://aur.archlinux.org/packages/compiz/) | Dock
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/) | Deepin Terminal
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | DPlayer
[deepin-media-player](https://aur.archlinux.org/packages/deepin-media-player/) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") Deepin Greeter
[deepin-desktop-environment](https://aur.archlinux.org/packages/deepin-desktop-environment/) |
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
| [Enlightenment](/index.php/Enlightenment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Enlightenment (简体中文)") | [Elementary](https://www.enlightenment.org/about-efl)
[elementary](https://www.archlinux.org/packages/?name=elementary) | Enlightenment
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | Enlightenment
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [Terminology](https://www.enlightenment.org/about-terminology)
[terminology](https://www.archlinux.org/packages/?name=terminology) | Enligthenment
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | Equate
[equate-git](https://aur.archlinux.org/packages/equate-git/) | Ecrire
[ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) | Ephoto
[ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) | [Rage](https://www.enlightenment.org/about-rage)
[rage](https://aur.archlinux.org/packages/rage/) | Elbow
[elbow-git](https://aur.archlinux.org/packages/elbow-git/) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
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
| [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
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
| GNUstep | [GNUstep](http://gnustep.org/)
[gnustep-core](https://www.archlinux.org/groups/x86_64/gnustep-core/) | [Window Maker](/index.php/Window_Maker "Window Maker")
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker) | [Window Maker](/index.php/Window_Maker "Window Maker")
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker) | [Terminal](http://gap.nongnu.org/terminal/index.html)
[gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/) | [GWorkspace](http://www.gnustep.org/experience/GWorkspace.html)
[gworkspace](https://aur.archlinux.org/packages/gworkspace/) | [Calculator](http://www.gnustep.org/experience/examples.html)
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/) | [Ink](http://www.gnustep.org/experience/examples.html)
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/) | [LaternaMagica](http://gap.nongnu.org/laternamagica/index.html)
[laternamagica](https://aur.archlinux.org/packages/laternamagica/) | [Cynthiune](http://gap.nongnu.org/cynthiune/index.html)
[cynthiune](https://aur.archlinux.org/packages/cynthiune/) | [SWK Browser](http://wiki.gnustep.org/index.php/SimpleWebKit)
[swkbrowser-svn](https://aur.archlinux.org/packages/swkbrowser-svn/) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Hawaii](/index.php/Hawaii "Hawaii") | [Qt](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)") 5
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | Green Island
[greenisland-git](https://aur.archlinux.org/packages/greenisland-git/) | Hawaii Shell
[hawaii-shell-git](https://aur.archlinux.org/packages/hawaii-shell-git/) | Terminal
[hawaii-terminal-git](https://aur.archlinux.org/packages/hawaii-terminal-git/) | Swordfish
[swordfish-git](https://aur.archlinux.org/packages/swordfish-git/) | [SpeedCrunch](http://speedcrunch.org/)
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/) | JuffEd
[juffed-qt5-git](https://aur.archlinux.org/packages/juffed-qt5-git/) | EyeSight
[eyesight-git](https://aur.archlinux.org/packages/eyesight-git/) | SMPlayer
[smplayer](https://www.archlinux.org/packages/?name=smplayer) | QupZilla
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | SDDM
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)") 4 | [Qt](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)") 4/5
[qt4](https://www.archlinux.org/packages/?name=qt4) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")
[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) | [Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_4#Desktop "wikipedia:KDE Plasma 4")
[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) | [Konsole](http://konsole.kde.org/)
[konsole](https://www.archlinux.org/packages/?name=konsole) | [Dolphin](http://dolphin.kde.org/)
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin) | [KCalc](http://www.kde.org/applications/utilities/kcalc/)
[kcalc](https://www.archlinux.org/packages/?name=kcalc) | [KWrite/Kate](http://kate-editor.org/)
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [Gwenview](http://gwenview.sourceforge.net/)
[gwenview](https://www.archlinux.org/packages/?name=gwenview) | [Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer) | [Konqueror](http://www.konqueror.org/)
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror) | [KDM](/index.php/KDM "KDM")
[kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/) |
| [KDE Plasma](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)") 5 | [Qt](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)") 4/5
[qt4](https://www.archlinux.org/packages/?name=qt4) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")
[kwin](https://www.archlinux.org/packages/?name=kwin) | [Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_5#Desktop "wikipedia:KDE Plasma 5")
[plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) | [Konsole](http://konsole.kde.org/)
[konsole](https://www.archlinux.org/packages/?name=konsole) | [Dolphin](http://dolphin.kde.org/)
[kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin) | [KCalc](http://www.kde.org/applications/utilities/kcalc/)
[kcalc](https://www.archlinux.org/packages/?name=kcalc) | [KWrite/Kate](http://kate-editor.org/)
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [Gwenview](http://gwenview.sourceforge.net/)
[gwenview](https://www.archlinux.org/packages/?name=gwenview) | [Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)
[kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer) | [Konqueror](http://www.konqueror.org/)
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror) | [SDDM](/index.php/SDDM "SDDM")
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | [LXPanel](http://wiki.lxde.org/en/LXPanel)
[lxpanel](https://www.archlinux.org/packages/?name=lxpanel) | [LXTerminal](http://wiki.lxde.org/en/LXTerminal)
[lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | [PCManFM](/index.php/PCManFM "PCManFM")
[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [Leafpad](http://tarot.freeshell.org/leafpad/)
[leafpad](https://www.archlinux.org/packages/?name=leafpad) | [GPicView](http://wiki.lxde.org/en/GPicView)
[gpicview](https://www.archlinux.org/packages/?name=gpicview) | [LXMusic](http://wiki.lxde.org/en/LXMusic)
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LXDM](/index.php/LXDM "LXDM")
[lxdm](https://www.archlinux.org/packages/?name=lxdm) |
| [LXQt](/index.php/LXQt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXQt (简体中文)") | [Qt](/index.php/Qt "Qt") 5
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | LXQt Panel
[lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel) | QTerminal
[qterminal](https://aur.archlinux.org/packages/qterminal/) | PCManFM-Qt
[pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) | [SpeedCrunch](http://speedcrunch.org/)
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/) | JuffEd
[juffed-qt5-git](https://aur.archlinux.org/packages/juffed-qt5-git/) | LxImage-Qt
[lximage-qt](https://aur.archlinux.org/packages/lximage-qt/) | SMPlayer
[smplayer](https://www.archlinux.org/packages/?name=smplayer) | QupZilla
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | SDDM
[sddm](https://www.archlinux.org/packages/?name=sddm) |
| [MATE](/index.php/MATE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MATE (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | Marco
[marco](https://www.archlinux.org/packages/?name=marco) | MATE Panel
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel) | MATE Terminal
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Caja
[caja](https://www.archlinux.org/packages/?name=caja) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | pluma
[pluma](https://www.archlinux.org/packages/?name=pluma) | Eye of MATE
[eom](https://www.archlinux.org/packages/?name=eom) | [Parole](http://docs.xfce.org/apps/parole/start)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [MATE](/index.php/MATE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MATE (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | Marco
[marco-gtk3](https://www.archlinux.org/packages/?name=marco-gtk3) | MATE Panel
[mate-panel-gtk3](https://www.archlinux.org/packages/?name=mate-panel-gtk3) | MATE Terminal
[mate-terminal-gtk3](https://www.archlinux.org/packages/?name=mate-terminal-gtk3) | Caja
[caja-gtk3](https://www.archlinux.org/packages/?name=caja-gtk3) | [Galculator](http://galculator.sourceforge.net/)
[galculator](https://www.archlinux.org/packages/?name=galculator) | pluma
[pluma-gtk3](https://www.archlinux.org/packages/?name=pluma-gtk3) | Eye of MATE
[eom-gtk3](https://www.archlinux.org/packages/?name=eom-gtk3) | [Parole](http://docs.xfce.org/apps/parole/start)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori-gtk3](https://www.archlinux.org/packages/?name=midori-gtk3) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| Maynard | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | Weston
[weston](https://www.archlinux.org/packages/?name=weston) | Maynard
[maynard-git](https://aur.archlinux.org/packages/maynard-git/) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Epiphany](/index.php/Epiphany "Epiphany")
[epiphany](https://www.archlinux.org/packages/?name=epiphany) | - |
| [Pantheon](/index.php/Pantheon "Pantheon") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Gala](https://launchpad.net/gala)
[gala-bzr](https://aur.archlinux.org/packages/gala-bzr/) | [Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/) | [Pantheon Terminal](https://launchpad.net/pantheon-terminal)
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | [Pantheon Files](https://launchpad.net/pantheon-files)
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [Scratch](https://launchpad.net/scratch)
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) | [Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")
[shotwell](https://www.archlinux.org/packages/?name=shotwell) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Midori](/index.php/Midori "Midori")
[midori-gtk3](https://www.archlinux.org/packages/?name=midori-gtk3) | [LightDM](/index.php/LightDM "LightDM") Pantheon Greeter
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/) |
| [ROX](/index.php/ROX "ROX") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [OroboROX](http://rox.sourceforge.net/desktop/OroboROX.html)
[oroborox](https://aur.archlinux.org/packages/oroborox/) | [ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)
[rox](https://www.archlinux.org/packages/?name=rox) | [ROXTerm](http://roxterm.sourceforge.net/)
[roxterm-gtk2](https://aur.archlinux.org/packages/roxterm-gtk2/) | [ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)
[rox](https://www.archlinux.org/packages/?name=rox) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [Edit](http://rox.sourceforge.net/desktop/Edit.html)
[rox-edit](https://aur.archlinux.org/packages/rox-edit/) | [Picky](http://rox.sourceforge.net/desktop/picky.html)
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picky)</small> | [MusicBox](http://rox.sourceforge.net/desktop/Software/Audio_Video/MusicBox.html)
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=musicbox)</small> | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Sugar](/index.php/Sugar "Sugar") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")
[metacity](https://www.archlinux.org/packages/?name=metacity) | Sugar
[sugar](https://aur.archlinux.org/packages/sugar/) | Terminal
[sugar-activity-terminal](https://aur.archlinux.org/packages/sugar-activity-terminal/) | Sugar Journal
[sugar](https://aur.archlinux.org/packages/sugar/) | Calculate
[sugar-activity-calculate](https://aur.archlinux.org/packages/sugar-activity-calculate/) | Write
[sugar-activity-write](https://aur.archlinux.org/packages/sugar-activity-write/) | ImageViewer
[sugar-activity-imageviewer](https://aur.archlinux.org/packages/sugar-activity-imageviewer/) | Jukebox
[sugar-activity-jukebox](https://aur.archlinux.org/packages/sugar-activity-jukebox/) | Browse
[sugar-activity-browse](https://aur.archlinux.org/packages/sugar-activity-browse/) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Trinity](/index.php/Trinity "Trinity") | TQt | TWin | Kicker | Konsole | Konqueror | KCalc | Kwrite / Kate | Kuickshow | Kaffeine | Konqueror | TDM |
| [Unity](/index.php/Unity_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unity (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Compiz](/index.php/Compiz "Compiz")
[compiz-ubuntu](https://aur.archlinux.org/packages/compiz-ubuntu/) | Unity
[unity](https://aur.archlinux.org/packages/unity/) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus-ubuntu](https://aur.archlinux.org/packages/nautilus-ubuntu/) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") Unity Greeter
[lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) |
| [xfce](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)") | [GTK+](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)") 2/3
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

#### 资源占用

此处在资源占用（CPU、内存、磁盘空间）上比较各种桌面环境。

*   GNOME和KDE：属于**高资源占用**桌面环境。相对来讲，它们**功能更为丰富**，是最完整的桌面环境。

*   E17、LXDE和Xfce：属于**轻量**桌面环境。它们通常是为低能耗设备或是旧机器设计的，占用更少资源。

#### 相似之处

许多人说，KDE像Windows，GNOME像Mac。这样的评价不怎么客观，毕竟它们并不能模拟Windows或是Mac。参见：[KDE比GNOME更像Windows吗](http://www.psychocats.net/ubuntucat/is-kde-more-windows-like-than-gnome/)（[中文版](http://fyyz.me/is-kde-more-windows-like-than-gnome/)），[KDE vs GNOME](http://www.jeffwu.net/?p=71)，[经典文章：Linux不是Windows](http://linux.oneandoneis2.org/LNW.htm)。

## 自己打造桌面环境

Desktop environments represent the simplest means of installing a *complete* graphical environment. However, users are free to build and customize their graphical environment in any number of ways if none of the popular desktop environments meet their requirements. Generally, building a custom environment involves selection of a suitable [window manager](/index.php/Window_manager "Window manager"), a [taskbar](/index.php/List_of_applications#Taskbars_.2F_panels_.2F_docks "List of applications") and a number of applications (a minimalist selection usually includes a [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"), [file manager](/index.php/List_of_applications#File_managers "List of applications"), and [text editor](/index.php/Text_editor "Text editor")).

Other applications that are usually provided by desktop environments are:

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