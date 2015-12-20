# Window manager (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

相关文章

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Start X at Login](/index.php/Start_X_at_Login "Start X at Login")

窗口管理器（window manager，简称WM）是图形用户界面的一部分。用户可以选择安装[桌面环境](/index.php/Desktop_Environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop Environment (简体中文)")，他们通常已经提供了完整的用户界面，包括图标、窗口、工具栏、壁纸和桌面部件。

## Contents

*   [1 X窗口系统](#X.E7.AA.97.E5.8F.A3.E7.B3.BB.E7.BB.9F)
*   [2 窗口管理器](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.1 类型](#.E7.B1.BB.E5.9E.8B)
    *   [2.2 窗口管理器列表](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E5.88.97.E8.A1.A8)
*   [3 窗口管理器列表](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E5.88.97.E8.A1.A8_2)
    *   [3.1 堆叠式（悬浮式）窗口管理器](#.E5.A0.86.E5.8F.A0.E5.BC.8F.EF.BC.88.E6.82.AC.E6.B5.AE.E5.BC.8F.EF.BC.89.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [3.2 平铺式（瓦片式）窗口管理器](#.E5.B9.B3.E9.93.BA.E5.BC.8F.EF.BC.88.E7.93.A6.E7.89.87.E5.BC.8F.EF.BC.89.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [3.3 动态窗口管理器](#.E5.8A.A8.E6.80.81.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)

## X窗口系统

[X窗口系统](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System")提供基本的图形用户界面支持。使用桌面环境之前，必须首先安装X服务器。[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")是这套系统的开源实现。

_X为GUI环境提供基本的框架：在屏幕上描绘、体现图像与移动程序窗口，同时也受理、运行、及管理电脑与鼠标、键盘的交互程序。不过，X并没有管理到用户界面，而是由其他以X为基础的实现来负责。正因为如此，以X为基础环境所开发成的视觉样式非常地多，不同的程序可能有截然不同的接口体现。X作为系统内核之上的程序应用层发挥作用。_

用户可以通过各种方法，自由配置GUI环境。

## 窗口管理器

窗口管理器是提供窗口边框的X客户端，它控制图形程序的外观和行为方式：边框、标题栏、大小、以及调整大小等操作。很多窗口管理器还有其他功能，比如[Window Maker](/index.php/Window_Maker "Window Maker")提供了[应用程序面板](http://www.dockapps.org)，[Fluxbox](/index.php/Fluxbox "Fluxbox")提供窗口标签功能，此外还有启动程序的菜单、窗口管理器配置菜单等。

窗口管理器一般不提供额外的组件，比如图标之类的，它们一般由[桌面环境](/index.php/Desktop_Environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop Environment (简体中文)")提供。因此，窗口管理器通常不怎么耗费系

### 类型

*   **堆叠式**（或**悬浮式**）窗口管理器，顾名思义，不同窗口可以相互重叠，就像桌子上随意摆放的白纸一样。Windows（中的explorer）、Mac OS X这样的商业系统所用的窗口管理器也是这种。
*   **平铺式**（或直译**瓦片式**）窗口管理器，其中的窗口不能够重叠，而是像瓦片一样挨个摆放。这种窗口管理器一般比较依赖键盘操作，较少使用鼠标。此类窗口管理器一般也是高度可定制的。
*   **动态**窗口管理器，结合上述两种窗口管理器，可以动态切换窗口放置方式。

### 窗口管理器列表

*   [堆叠式（悬浮式）窗口管理器](/index.php/Category:Stacking_WMs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Stacking WMs (简体中文)")
*   [平铺式（瓦片式）窗口管理器](/index.php/Category:Tiling_WMs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Tiling WMs (简体中文)")
*   [动态窗口管理器](/index.php/Category:Dynamic_WMs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Dynamic WMs (简体中文)")

窗口管理器的比较参见 [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") 和 [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers")。

## 窗口管理器列表

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

### 堆叠式（悬浮式）窗口管理器

*   **aewm** — aewm is a modern, minimal window manager for X11\. It is controlled entirely with the mouse, but contains no visible UI apart from window frames. The command set is sort of like vi: designed back in the dawn of time (1997) to squeeze speed out of low-memory machines, completely unintuitive and new-user-hostile, but quick and elegant in its own way.

[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/)<sup><small>AUR</small></sup> [unsupported]

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — AfterStep is a window manager for the Unix X Window System. Originally based on the look and feel of the NeXTStep interface, it provides end users with a consistent, clean, and elegant desktop. The goal of AfterStep development is to provide for flexibility of desktop configuration, improving aestetics, and efficient use of system resources.

[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep](https://aur.archlinux.org/packages/afterstep/)<sup><small>AUR</small></sup> [unsupported]

*   **[Blackbox](https://en.wikipedia.org/wiki/Blackbox "wikipedia:Blackbox")** — Blackbox is the fast, lightweight window manager for the X Window System you have been looking for, without all those annoying library dependencies. Blackbox is built with C++ and contains completely original code (even though the graphics implementation is similar to that of WindowMaker).

[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — Compiz is an OpenGL compositing manager that uses GLX_EXT_texture_from_pixmap for binding redirected top-level windows to texture objects. It has a flexible plug-in system and it is designed to run well on most graphics hardware.

[http://www.compiz.org/](http://www.compiz.org/) || [compiz-core](https://aur.archlinux.org/packages/compiz-core/)<sup><small>AUR</small></sup>

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Enlightenment is not just a window manager for Linux/X11 and others, but also a whole suite of libraries to help you create beautiful user interfaces with much less work than doing it the old fashioned way and fighting with traditional toolkits, not to mention a traditional window manager.

[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — A minimalist window manager for the X Window System. 'Minimalist' here does not mean it is too bare to be usable - it just means it omits a lot of the stuff that make other window managers _un_usable.

[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)<sup><small>AUR</small></sup>

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Fluxbox is a window manager for X that was based on the Blackbox 0.61.1 code. It is very light on resources and easy to handle but yet full of features to make an easy and extremely fast desktop experience. It is built using C++ and licensed under the MIT License.

[http://www.fluxbox.org/](http://www.fluxbox.org/) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Flwm is my attempt to combine the best ideas I have seen in several window managers. The primary influence and code base is from wm2 by Chris Cannam.

[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/)<sup><small>AUR</small></sup> [unsupported]

*   **[FVWM](/index.php/FVWM "FVWM")** — FVWM is an extremely powerful ICCCM-compliant multiple virtual desktop window manager for the X Window system. Development is active, and support is excellent.

[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **[Goomwwm](/index.php?title=Goomwwm&action=edit&redlink=1 "Goomwwm (page does not exist)")** — Goomwwm is an X11 window manager implemented in C as a cleanroom software project. It manages windows in a minimal floating layout, while providing flexible keyboard-driven controls for window switching, sizing, moving, tagging, and tiling. It is also fast, lightweight, modeless, Xinerama-aware, and EWMH compatible wherever possible.

[http://aerosuidae.net/goomwwm/](http://aerosuidae.net/goomwwm/) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/)<sup><small>AUR</small></sup> [unsupported]

*   **[Hackedbox](https://en.wikipedia.org/wiki/Hackedbox "wikipedia:Hackedbox")** — Hackedbox is a stripped down version of Blackbox - The X11 Window Manager. The toolbar and Slit have been removed. The goal of Hackedbox is to be a small "feature-set" window manager, with no bloat. There are no plans to add any functionality, only bugfixes and speed enhancements whenever possible.

[http://scrudgeware.org/projects/Hackedbox/](http://scrudgeware.org/projects/Hackedbox/) || [hackedbox](https://aur.archlinux.org/packages/hackedbox/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/hackedbox)]</sup> [unsupported]

*   **[IceWM](/index.php/IceWM "IceWM")** — IceWM is a window manager for the X Window System. The goal of IceWM is speed, simplicity, and not getting in the user's way.

[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **[JWM](/index.php/JWM "JWM")** — JWM is a window manager for the X11 Window System. JWM is written in C and uses only Xlib at a minimum.

[http://joewing.net/programs/jwm/](http://joewing.net/programs/jwm/) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Karmen is a window manager for X, written by Johan Veenhuizen. It is designed to "just work." There is no configuration file and no library dependencies other than Xlib. The input focus model is click-to-focus. Karmen aims at ICCCM and EWMH compliance.

[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/)<sup><small>AUR</small></sup> [unsupported]

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — KWin, the standard KDE window manager in KDE 4.0, ships with the first version of built-in support for compositing, making it also a compositing manager. This allows KWin to provide advanced graphical effects, similar to Compiz, while also providing all the features from previous KDE releases (such as very good integration with the rest of KDE, advanced configurability, focus stealing prevention, a well-tested window manager, robust handling of misbehaving applications/toolkits, etc.).

[http://techbase.kde.org/Projects/KWin](http://techbase.kde.org/Projects/KWin) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>

*   **lwm** — lwm is a window manager for X that tries to keep out of your face. There are no icons, no button bars, no icon docks, no root menus, no nothing: if you want all that, then other programs can provide it. There is no configurability either: if you want that, you want a different window manager; one that helps your operating system in its evil conquest of your disc space and its annexation of your physical memory.

[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — This is not the Metacity home page. There is no Metacity home page. This is for the same reason there is no flashy logo: Metacity strives to be quiet, small, stable, get on with its job, and stay out of your attention.

[http://blogs.gnome.org/metacity/](http://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Openbox](/index.php/Openbox "Openbox")** — Openbox is a highly configurable, next generation window manager with extensive standards support. The *box visual style is well known for its minimalistic appearance. Openbox uses the *box visual style, while providing a greater number of options for theme developers than previous *box implementations. The theme documentation describes the full range of options found in Openbox themes.

[http://openbox.org/wiki/Main_Page](http://openbox.org/wiki/Main_Page) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — pawm is a window manager for the X Window system. So it is not a 'desktop' and does not offer you a huge pile of useless options, just the facilities needed to run your X applications and at the same time having a friendly and easy to use interface.

[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://www.archlinux.org/packages/?name=pawm)

*   **[pekwm](/index.php/Pekwm "Pekwm")** — pekwm is a window manager that once upon a time was based on the aewm++ window manager, but it has evolved enough that it no longer resembles aewm++ at all. It has a much expanded feature-set, including window grouping (similar to Ion, PWM, or Fluxbox), auto-properties, Xinerama, keygrabber that supports keychains, and much more.

[http://www.pekwm.org/projects/pekwm](http://www.pekwm.org/projects/pekwm) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — Sawfish is an extensible window manager using a Lisp-based scripting language. Its policy is very minimal compared to most window managers. Its aim is simply to manage windows in the most flexible and attractive manner possible. All high-level WM functions are implemented in Lisp for future extensibility or redefinition.

[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)<sup><small>AUR</small></sup> [unsupported]

*   **TinyWM** — TinyWM is a tiny window manager that I created as an exercise in minimalism. It is also maybe helpful in learning some of the very basics of creating a window manager. It is only around 50 lines of C. There is also a Python version using python-xlib.

[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tinywm)]</sup> [unsupported]

*   **[twm](/index.php/Twm "Twm")** — twm is a window manager for the X Window System. It provides titlebars, shaped windows, several forms of icon management, user-defined macro functions, click-to-type and pointer-driven keyboard focus, and user-specified key and pointer button bindings.

[http://cgit.freedesktop.org/xorg/app/twm/](http://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **WindowLab** — WindowLab is a small and simple window manager of novel design. It has a click-to-focus but not raise-on-focus policy, a window resizing mechanism that allows one or many edges of a window to be changed in one action, and an innovative menubar that shares the same part of the screen as the taskbar. Window titlebars are prevented from going off the edge of the screen by constraining the mouse pointer, and when appropriate the pointer is also constrained to the taskbar/menubar in order to make target menu items easier to hit.

[http://nickgravgaard.com/windowlab/](http://nickgravgaard.com/windowlab/) || [windowlab](https://www.archlinux.org/packages/?name=windowlab)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — Window Maker is an X11 window manager originally designed to provide integration support for the GNUstep Desktop Environment. In every way possible, it reproduces the elegant look and feel of the NEXTSTEP user interface. It is fast, feature rich, easy to configure, and easy to use. It is also free software, with contributions being made by programmers from around the world.

[http://windowmaker.org/](http://windowmaker.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

*   **WM2** — wm2 is a window manager for X. It provides an unusual style of window decoration and as little functionality as its author feels comfortable with in a window manager. wm2 is not configurable, except by editing the source and recompiling the code, and is really intended for people who don't particularly want their window manager to be too friendly.

[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)<sup><small>AUR</small></sup>

*   **Xfwm** — The Xfce window manager manages the placement of application windows on the screen, provides beautiful window decorations, manages workspaces or virtual desktops and natively supports multiscreen mode. It provides its own compositing manager (from the X.Org Composite extension) for true transparency and shadows. The Xfce window manager also includes a keyboard shortcuts editor for user specific commands and basic windows manipulations and provides a preferences dialog for advanced tweaks.

[http://www.xfce.org/projects/xfwm4/](http://www.xfce.org/projects/xfwm4/) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### 平铺式（瓦片式）窗口管理器

*   **dswm** — dswm (Deep Space Window Manager) is an offshoot of [Stumpwm](/index.php/Stumpwm "Stumpwm")

[https://github.com/dss-project/dswm](https://github.com/dss-project/dswm) || [dswm](https://aur.archlinux.org/packages/dswm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dswm)]</sup> [unsupported]

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — herbstluftwm is a manual tiling window manager for X11 using Xlib and Glib. The layout is based on splitting frames into subframes which can be split again or can be filled with windows (similar to i3/ musca). Tags (or workspaces or virtual desktops or …) can be added/removed at runtime. Each tag contains an own layout. Exactly one tag is viewed on each monitor. The tags are monitor independent (similar to xmonad). It is configured at runtime via ipc calls from herbstclient. So the configuration file is just a script which is run on startup. (similar to wmii/ musca)

[http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm](http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm) || [herbstluftwm-git](https://aur.archlinux.org/packages/herbstluftwm-git/)<sup><small>AUR</small></sup> [unsupported]

*   **[Ion3](/index.php/Ion3 "Ion3")** — Ion is a tiling tabbed X11 window manager designed with keyboard users in mind. It was one of the first of the “new wave" of tiling windowing environments (the other being LarsWM, with quite a different approach) and has since spawned an entire category of tiling window managers for X11 – none of which really manage to reproduce the feel and functionality of Ion. It uses Lua as an embedded interpreter which handles all of the configuration.

[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/)<sup><small>AUR</small></sup> [unsupported]

*   **[Notion](/index.php/Notion "Notion")** — Notion is a tiling, tabbed window manager for the X window system that utilizes 'tiles' and 'tabbed' windows.
    *   Tiling: you divide the screen into non-overlapping 'tiles'. Every window occupies one tile, and is maximized to it
    *   Tabbing: a tile may contain multiple windows - they will be 'tabbed'
    *   Static: most tiled window managers are 'dynamic', meaning they automatically resize and move around tiles as windows appear and disappear. Notion, by contrast, does not automatically change the tiling.

Notion is a fork of Ion3.

[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Ratpoison is a simple Window Manager with no fat library dependencies, no fancy graphics, no window decorations, and no rodent dependence. It is largely modeled after GNU Screen which has done wonders in the virtual terminal market. Ratpoison is configured with a simple text file. The information bar in Ratpoison is somewhat different, as it shows only when needed. It serves as both an application launcher as well as a notification bar. Ratpoison does not include a system tray.

[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Stumpwm is a tiling, keyboard driven X11 Window Manager written entirely in Common Lisp. Stumpwm attempts to be customizable yet visually minimal. It does have various hooks to attach your personal customizations, and variables to tweak, and can be reconfigured and reloaded while running. There are no window decorations, no icons, no buttons, and no system tray. Its information bar can be set to show constantly or only when needed.

[http://www.nongnu.org/stumpwm/](http://www.nongnu.org/stumpwm/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/stumpwm-git)]</sup> [unsupported]

*   **[subtle](/index.php/Subtle "Subtle")** — subtle is a manual tiling window manager with a rather uncommon approach of tiling: Per default there is no typical layout enforcement, windows are placed on a position (gravity) in a custom grid. The user can change the gravity of each window either directly per grabs or with rules defined by tags in the config. It has workspace tags and automatic client tagging, mouse and keyboard control as well as an extendable statusbar.

[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle](https://aur.archlinux.org/packages/subtle/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/subtle)]</sup>

*   **[WMFS](/index.php/WMFS "WMFS")** — WMFS (Window Manager From Scratch) is a lightweight and highly configurable tiling window manager for X. It can be configured with a configuration file, supports Xft (FreeType) fonts and is compliant with the Extended Window Manager Hints (EWMH) specifications, Xinerama and Xrandr. WMFS can be driven with Vi based commands (ViWMFS).

[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/)<sup><small>AUR</small></sup> [unsupported]

### 动态窗口管理器

*   **[awesome](/index.php/Awesome "Awesome")** — awesome is a highly configurable, next generation framework window manager for X. It is very fast, extensible and licensed under the GNU GPLv2 license. Configured in Lua, it has a system tray, information bar, and launcher built in. There are extensions available to it written in Lua. Awesome uses XCB as opposed to Xlib, which may result in a speed increase. Awesome has other features as well, such as an early replacement for notification-daemon, a right-click menu similar to that of the *box window managers, and many other things.

[http://awesome.naquadah.org/](http://awesome.naquadah.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — catwm is a small window manager, even simpler than dwm, written in C. Configuration is done by modifying the config.h file and recompiling.

[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/)<sup><small>AUR</small></sup> [unsupported]

*   **[dwm](/index.php/Dwm "Dwm")** — dwm is a dynamic window manager for X. It manages windows in tiled, monocle and floating layouts. All of the layouts can be applied dynamically, optimising the environment for the application in use and the task performed. does not include a tray app or automatic launcher, although dmenu integrates well with it, as they are from the same author. It has no text configuration file. Configuration is done entirely by modifying the C source code, and it must be recompiled and restarted each time it is changed. The program size is already at the self-imposed line limit, restricting further development.

[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://www.archlinux.org/packages/?name=dwm)

*   **[echinus](/index.php/Echinus "Echinus")** — Simple and lightweight tiling and floating window manager for X11\. Started as a dwm fork with easier configuration, echinus became full-featured re-parenting window manager with EWMH support. It has an EWMH-compatible panel/taskbar, called [ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup>

[http://plhk.ru/echinus](http://plhk.ru/echinus) || [echinus](https://aur.archlinux.org/packages/echinus/)<sup><small>AUR</small></sup> [unsupported]

*   **[euclid-wm](/index.php?title=Euclid-wm&action=edit&redlink=1 "Euclid-wm (page does not exist)")** — euclid-wm is a simple and lightweight tiling and floating window manager for X11, with support for minimizing windows. A text configuration file controls key bindings and settings. It started as a dwm fork with easier configuration, and became a full-featured reparenting window manager with EWMH support. It has an EWMH-compatible panel/taskbar called [ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup>.

[http://euclid-wm.sourceforge.net/index.php](http://euclid-wm.sourceforge.net/index.php) || [euclid-wm](https://aur.archlinux.org/packages/euclid-wm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/euclid-wm)]</sup> [unsupported]

*   **[i3](/index.php/I3 "I3")** — i3 is a tiling window manager, completely written from scratch. i3 was created because wmii, our favorite window manager at the time, did not provide some features we wanted (multi-monitor done right, for example) had some bugs, did not progress since quite some time and was not easy to hack at all (source code comments/documentation completely lacking). Notable differences are in the areas of multi-monitor support and the tree metaphor. For speed the Plan 9 interface of wmii is not implemented.

[http://i3wm.org/](http://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[monsterwm](/index.php/Monsterwm "Monsterwm")** — is a minimal, lightweight, tiny but monsterous dynamic tiling window manager. It will try to stay as small as possible. Currently under 700 lines with the config file included. It provides a set of four different layout modes (vertical stack, bottom stack, grid and monocle/fullscreen) by default, and has floating mode support. It also features multi-monitor support. Each monitor and virtual desktop have their own properties, unaffected by other monitors' or desktops' settings. Configuration is done entirely by modifying the C source code, and it must be recompiled and restarted each time it is changed. There are many available patches supported upstream, in the form of different git branches.

[https://github.com/c00kiemon5ter/monsterwm](https://github.com/c00kiemon5ter/monsterwm) || [monsterwm-git](https://aur.archlinux.org/packages/monsterwm-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/monsterwm-git)]</sup>

*   **[Musca](/index.php/Musca "Musca")** — A simple dynamic window manager for X, with features nicked from ratpoison and dwm. Musca operates as a tiling window manager by default. The user determines how the screen is divided into non-overlapping frames, with no restrictions on layout. Application windows always fill their assigned frame, with the exception of transient windows and popup dialog boxes which float above their parent application at the appropriate size. Once visible, applications do not change frames unless so instructed.

[http://aerosuidae.net/musca.html](http://aerosuidae.net/musca.html) || [musca](https://aur.archlinux.org/packages/musca/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/musca)]</sup> [unsupported]

*   **[snapwm](/index.php/Snapwm "Snapwm")** — is a small, lightweight dynamic tiling window manager based on catwm and dminiwm. It has a built in status bar with clickable workspaces and five modes (vertical, horizontal, grid, fullscreen, and stacking). It has other features, like status colors, pertag, attachaside, a reloadable rc file, transparency support, dmenu integration and more.

[https://github.com/moetunes/Nextwm](https://github.com/moetunes/Nextwm) ||

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Spectrwm is a small dynamic tiling window manager for X11, largely inspired by xmonad and dwm. It tries to stay out of the way so that valuable screen real estate can be used for much more important stuff. It has sane defaults and is configured with a text file. It was written by hackers for hackers and it strives to be small, compact and fast. It has a built-in status bar fed from a user-defined script

[https://opensource.conformal.com/wiki/spectrwm](https://opensource.conformal.com/wiki/spectrwm) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm) [community]

*   **[Wingo](/index.php/Wingo "Wingo")** — Wingo is a fully featured true hybrid window manager that supports per-monitor workspaces, and neither the floating or tiling modes are after thoughts. This allows one to have tiling on one workspace while floating on the other. Wingo can be scripted with its own command language, is completely themeable, and supports user defined hooks. Wingo is written in Go and has no runtime dependencies.

[https://github.com/BurntSushi/wingo](https://github.com/BurntSushi/wingo) || [wingo-git](https://aur.archlinux.org/packages/wingo-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wingo-git)]</sup> [unsupported]

*   **[wmii](/index.php/Wmii "Wmii")** — wmii is a small, dynamic window manager for X11\. It is scriptable, has a 9P filesystem interface and supports classic and tiling (Acme-like) window management. It aims to maintain a small and clean (read hackable and beautiful) codebase. The default configuration is in bash and [rc (the Plan 9 shell)](http://rc.cat-v.org), but programs exist written in ruby, and any program that can work with text can configure it. It has a status bar and launcher built in, and also an optional system tray (`witray`).

[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://www.archlinux.org/packages/?name=wmii)

*   **[xmonad](/index.php/Xmonad "Xmonad")** — xmonad is a dynamically tiling X11 window manager that is written and configured in Haskell. In a normal WM, you spend half your time aligning and searching for windows. xmonad makes work easier, by automating this. For all configuration changes, xmonad must be recompiled, so the Haskell compiler (over 100MB) must be installed. A large library called [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) provides many additional features

[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Window_manager_(简体中文)&oldid=412839](https://wiki.archlinux.org/index.php?title=Window_manager_(简体中文)&oldid=412839)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")
*   [Desktop environments (简体中文)](/index.php/Category:Desktop_environments_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Desktop environments (简体中文)")