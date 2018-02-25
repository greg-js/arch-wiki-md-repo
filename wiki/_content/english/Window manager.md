Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Xorg](/index.php/Xorg "Xorg")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Start X at Login](/index.php/Start_X_at_Login "Start X at Login")

A [window manager](https://en.wikipedia.org/wiki/Window_manager "wikipedia:Window manager") (WM) is system software that controls the placement and appearance of windows within a windowing system in a graphical user interface (GUI). It can be part of a [desktop environment](/index.php/Desktop_environment "Desktop environment") (DE) or be used standalone.

## Contents

*   [1 Overview](#Overview)
    *   [1.1 Types](#Types)
*   [2 List of window managers](#List_of_window_managers)
    *   [2.1 Stacking window managers](#Stacking_window_managers)
    *   [2.2 Tiling window managers](#Tiling_window_managers)
    *   [2.3 Dynamic window managers](#Dynamic_window_managers)
*   [3 See also](#See_also)

## Overview

Window managers are X clients that control the appearance and behaviour of the frames ("windows") where the various graphical applications are drawn. They determine the border, titlebar, size, and ability to resize windows, and often provide other functionality such as reserved areas for sticking [dockapps](http://windowmaker.org/dockapps/) like [Window Maker](/index.php/Window_Maker "Window Maker"), or the ability to tab windows like [Fluxbox](/index.php/Fluxbox "Fluxbox"). Some window managers are even bundled with simple utilities like menus to start programs or to configure the WM itself.

The [Extended Window Manager Hints](http://standards.freedesktop.org/wm-spec/wm-spec-latest.html) specification is used to allow window managers interact in standard ways with the server and the other clients.

Some window managers are developed as part of a more comprehensive [desktop environment](/index.php/Desktop_environment "Desktop environment"), usually allowing the other provided applications to better interact with each other, giving a more consistent experience to the user, complete with features like desktop icons, fonts, toolbars, wallpapers, or desktop widgets.

Other window managers are instead designed to be used *standalone*, giving the user complete freedom over the choice of the other applications to be used. This allows the user to create a more lightweight and customized environment, tailored to his/her own specific needs. "Extras" like desktop icons, toolbars, wallpapers, or desktop widgets, if needed, will have to be added with additional dedicated applications.

Some standalone WMs can be also used to replace the default WM of a DE, just like some DE-oriented WMs can be used standalone too.

Prior to installing a window manager, a functional X server installation is required. See [Xorg](/index.php/Xorg "Xorg") for detailed information.

### Types

*   [Stacking](#Stacking_window_managers) (aka floating) window managers provide the traditional desktop metaphor used in commercial operating systems like Windows and OS X. Windows act like pieces of paper on a desk, and can be stacked on top of each other. For available Arch Wiki pages see [Category:Stacking WMs](/index.php/Category:Stacking_WMs "Category:Stacking WMs").
*   [Tiling](#Tiling_window_managers) window managers "tile" the windows so that none are overlapping. They usually make very extensive use of key-bindings and have less (or no) reliance on the mouse. Tiling window managers may be manual, offer predefined layouts, or both. For available Arch Wiki pages see [Category:Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs").
*   [Dynamic](#Dynamic_window_managers) window managers can dynamically switch between tiling or floating window layout. For available Arch Wiki pages see [Category:Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs").

See [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") and [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers") for comparison of window managers.

## List of window managers

### Stacking window managers

*   **[2bwm](/index.php/2bwm "2bwm")** — Fast floating WM, with the particularity of having 2 borders, written over the XCB library and derived from mcwm written by Michael Cardell. In 2bwm everything is accessible from the keyboard but a pointing device can be used for move, resize and raise/lower. The name has recently changed from mcwm-beast to 2bwm.

	[https://github.com/venam/2bwm](https://github.com/venam/2bwm) || [2bwm](https://aur.archlinux.org/packages/2bwm/)

*   **aewm** — Modern, minimal window manager for X11\. It is controlled entirely with the mouse, but contains no visible UI apart from window frames. The command set is sort of like vi: designed back in the dawn of time (1997) to squeeze speed out of low-memory machines, completely unintuitive and new-user-hostile, but quick and elegant in its own way.

	[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/)

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — Window manager for the Unix X Window System. Originally based on the look and feel of the NeXTStep interface, it provides end users with a consistent, clean, and elegant desktop. The goal of AfterStep development is to provide for flexibility of desktop configuration, improving aesthetics, and efficient use of system resources.

	[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep-git](https://aur.archlinux.org/packages/afterstep-git/)

*   **[Blackbox](/index.php/Blackbox "Blackbox")** — Fast, lightweight window manager for the X Window System, without all those annoying library dependencies. Blackbox is built with C++ and contains completely original code (even though the graphics implementation is similar to that of WindowMaker).

	[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — OpenGL compositing manager that uses GLX_EXT_texture_from_pixmap for binding redirected top-level windows to texture objects. It has a flexible plug-in system and it is designed to run well on most graphics hardware.

	[https://launchpad.net/compiz](https://launchpad.net/compiz) || [compiz](https://aur.archlinux.org/packages/compiz/), [compiz-core](https://aur.archlinux.org/packages/compiz-core/)

*   **[cwm](/index.php/Cwm "Cwm")** — Originally deriving from evilwm, but later re-written from scratch. cwm aims to be simple, and offers helpful features such as searching for windows.

	[https://github.com/chneukirchen/cwm](https://github.com/chneukirchen/cwm) || [cwm](https://aur.archlinux.org/packages/cwm/)

*   **eggwm** — A lightweight QT4/QT5 window manager

	[eggwm-qt5](https://aur.archlinux.org/packages/eggwm-qt5/) || [eggwm](https://aur.archlinux.org/packages/eggwm/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Enlightenment is not just a window manager for Linux/X11 and others, but also a whole suite of libraries to help you create beautiful user interfaces with much less work than doing it the old fashioned way and fighting with traditional toolkits, not to mention a traditional window manager.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — Minimalist window manager for the X Window System. 'Minimalist' here does not mean it is too bare to be usable - it just means it omits a lot of the stuff that make other window managers *un*usable.

	[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Window manager for X that was based on the Blackbox 0.61.1 code. It is very light on resources and easy to handle but yet full of features to make an easy and extremely fast desktop experience. It is built using C++ and licensed under the MIT License.

	[https://github.com/fluxbox/fluxbox](https://github.com/fluxbox/fluxbox) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Attempt to combine the best ideas I have seen in several window managers. The primary influence and code base is from wm2 by Chris Cannam.

	[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/)

*   **[FVWM](/index.php/FVWM "FVWM")** — Extremely powerful ICCCM-compliant multiple virtual desktop window manager for the X Window system. Development is active, and support is excellent.

	[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **[Gala](http://elementaryos.org/journal/meet-gala-window-manager)** — A beautiful Window Manager from elementaryos, part of [Pantheon](/index.php/Pantheon "Pantheon"). Also as a compositing manager, based on libmutter.

	[https://launchpad.net/gala](https://launchpad.net/gala) || [gala](https://aur.archlinux.org/packages/gala/), [gala-git](https://aur.archlinux.org/packages/gala-git/)

*   **Goomwwm** — X11 window manager implemented in C as a cleanroom software project. It manages windows in a minimal floating layout, while providing flexible keyboard-driven controls for window switching, sizing, moving, tagging, and tiling. It is also fast, lightweight, modeless, Xinerama-aware, and EWMH compatible wherever possible.

	[https://github.com/seanpringle/goomwwm](https://github.com/seanpringle/goomwwm) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/)

*   **[IceWM](/index.php/IceWM "IceWM")** — Window manager for the X Window System. The goal of IceWM is speed, simplicity, and not getting in the user's way.

	[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **jbwm** — jbwm is a window manager based on evilwm, with a minimal configuration size of approximately 16kb, focused on small binary size and usability, incorporating optional title-bars and XFT title-bar font rendering as compile-time options. jbwm also features easier to use keybindings than evilwm.

	[https://github.com/jefbed/jbwm](https://github.com/jefbed/jbwm) || [jbwm](https://aur.archlinux.org/packages/jbwm/)

*   **[JWM](/index.php/JWM "JWM")** — Window manager for the X11 Window System. JWM is written in C and uses only Xlib at a minimum.

	[https://joewing.net/projects/jwm/index.shtml](https://joewing.net/projects/jwm/index.shtml) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Window manager for X, written by Johan Veenhuizen. It is designed to "just work." There is no configuration file and no library dependencies other than Xlib. The input focus model is click-to-focus. Karmen aims at ICCCM and EWMH compliance.

	[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/)

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — The standard KDE window manager since KDE 4.0, ships with the first version of built-in support for compositing, making it also a compositing manager. This allows KWin to provide advanced graphical effects, similar to Compiz, while also providing all the features from previous KDE releases (such as very good integration with the rest of KDE, advanced configurability, focus stealing prevention, a well-tested window manager, robust handling of misbehaving applications/toolkits, etc.). Also serves as a compositor for [Wayland](/index.php/Wayland "Wayland").

	[https://techbase.kde.org/Projects/KWin](https://techbase.kde.org/Projects/KWin) || [kwin](https://www.archlinux.org/packages/?name=kwin)

*   **lwm** — Window manager for X that tries to keep out of your face. There are no icons, no button bars, no icon docks, no root menus, no nothing: if you want all that, then other programs can provide it. There is no configurability either: if you want that, you want a different window manager; one that helps your operating system in its evil conquest of your disc space and its annexation of your physical memory.

	[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **Marco** — The MATE window manager, fork of Metacity.

	[https://github.com/mate-desktop/marco](https://github.com/mate-desktop/marco) || [marco](https://www.archlinux.org/packages/?name=marco)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — This window manager strives to be quiet, small, stable, get on with its job, and stay out of your attention.

	[https://blogs.gnome.org/metacity/](https://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Muffin](https://en.wikipedia.org/wiki/Mutter_(software)#Muffin "wikipedia:Mutter (software)")** — Window and compositing manager for Cinnamon, fork of Mutter, based on Clutter, uses OpenGL. It cannot be used outside of Cinnamon.

	[https://github.com/linuxmint/muffin/](https://github.com/linuxmint/muffin/) || [muffin](https://www.archlinux.org/packages/?name=muffin)

*   **[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")** — Window and compositing manager for GNOME, based on Clutter, uses OpenGL. Also serves a Wayland compositor.

	[https://git.gnome.org/browse/mutter/](https://git.gnome.org/browse/mutter/) || [mutter](https://www.archlinux.org/packages/?name=mutter)

*   **[MWM](https://en.wikipedia.org/wiki/Motif_Window_Manager "wikipedia:Motif Window Manager")** — The Motif Window Manager (MWM) is an X window manager based on the Motif toolkit.

	[http://sourceforge.net/projects/motif/](http://sourceforge.net/projects/motif/) || [openmotif](https://www.archlinux.org/packages/?name=openmotif)

*   **[Openbox](/index.php/Openbox "Openbox")** — Highly configurable, next generation window manager with extensive standards support. The *box visual style is well known for its minimalistic appearance. Openbox uses the *box visual style, while providing a greater number of options for theme developers than previous *box implementations. The theme documentation describes the full range of options found in Openbox themes.

	[http://openbox.org/](http://openbox.org/) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — Window manager for the X Window system. So it is not a 'desktop' and does not offer you a huge pile of useless options, just the facilities needed to run your X applications and at the same time having a friendly and easy to use interface.

	[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://aur.archlinux.org/packages/pawm/)

*   **[PekWM](/index.php/PekWM "PekWM")** — Window manager that once upon a time was based on the aewm++ window manager, but it has evolved enough that it no longer resembles aewm++ at all. It has a much expanded feature-set, including window grouping (similar to Ion, PWM, or Fluxbox), auto-properties, Xinerama, keygrabber that supports keychains, and much more.

	[https://www.pekwm.org/](https://www.pekwm.org/) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — Extensible window manager using a Lisp-based scripting language. Its policy is very minimal compared to most window managers. Its aim is simply to manage windows in the most flexible and attractive manner possible. All high-level WM functions are implemented in Lisp for future extensibility or redefinition.

	[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)

*   **TinyWM** — Tiny window manager created as an exercise in minimalism. It may be helpful in learning some of the very basics of creating a window manager. It is comprised of approximately 50 lines of C. There is also a Python version using python-xlib.

	[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/) [tinywm-git](https://aur.archlinux.org/packages/tinywm-git/)

*   **[twm](/index.php/Twm "Twm")** — Window manager for the X Window System. It provides titlebars, shaped windows, several forms of icon management, user-defined macro functions, click-to-type and pointer-driven keyboard focus, and user-specified key and pointer button bindings.

	[https://cgit.freedesktop.org/xorg/app/twm/](https://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **[UWM](https://en.wikipedia.org/wiki/UDE "wikipedia:UDE")** — The ultimate window manager for UDE.

	[http://udeproject.sourceforge.net/](http://udeproject.sourceforge.net/) || [ude](https://aur.archlinux.org/packages/ude/)

*   **WindowLab** — Small and simple window manager of novel design. It has a click-to-focus but not raise-on-focus policy, a window resizing mechanism that allows one or many edges of a window to be changed in one action, and an innovative menubar that shares the same part of the screen as the taskbar. Window titlebars are prevented from going off the edge of the screen by constraining the mouse pointer, and when appropriate the pointer is also constrained to the taskbar/menubar in order to make target menu items easier to hit.

	[https://github.com/nickgravgaard/windowlab](https://github.com/nickgravgaard/windowlab) || [windowlab](https://www.archlinux.org/packages/?name=windowlab)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — X11 window manager originally designed to provide integration support for the GNUstep Desktop Environment. In every way possible, it reproduces the elegant look and feel of the NEXTSTEP user interface. It is fast, feature rich, easy to configure, and easy to use. It is also free software, with contributions being made by programmers from around the world.

	[https://windowmaker.org/](https://windowmaker.org/) || [windowmaker](https://aur.archlinux.org/packages/windowmaker/)

*   **WM2** — Window manager for X. It provides an unusual style of window decoration and as little functionality as its author feels comfortable with in a window manager. wm2 is not configurable, except by editing the source and recompiling the code, and is really intended for people who do not particularly want their window manager to be too friendly.

	[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)

*   **[Xfwm](/index.php/Xfwm "Xfwm")** — The [Xfce](/index.php/Xfce "Xfce") window manager manages the placement of application windows on the screen, provides beautiful window decorations, manages workspaces or virtual desktops and natively supports multiscreen mode. It provides its own compositing manager (from the X.Org Composite extension) for true transparency and shadows. The Xfce window manager also includes a keyboard shortcuts editor for user specific commands and basic windows manipulations and provides a preferences dialog for advanced tweaks.

	[https://docs.xfce.org/xfce/xfwm4/start](https://docs.xfce.org/xfce/xfwm4/start) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### Tiling window managers

*   **[Bspwm](/index.php/Bspwm "Bspwm")** — bspwm is a tiling window manager that represents windows as the leaves of a full binary tree. It has support for EWMH and multiple monitors, and is configured and controlled through messages.

	[https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) || [bspwm](https://www.archlinux.org/packages/?name=bspwm)

*   **[EXWM](/index.php/EXWM "EXWM")** — EXWM (Emacs X Window Manager) is a full-featured tiling X window manager for Emacs built on top of XELB. It features hybrid layout modes (tiling & stacking), dynamic workspace support, multi-monitor support, built-in compositing manager, and a system tray.

	[https://github.com/ch11ng/exwm](https://github.com/ch11ng/exwm) || [emacs-exwm-git](https://aur.archlinux.org/packages/emacs-exwm-git/)

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — Manual tiling window manager for X11 using Xlib and Glib. The layout is based on splitting frames into subframes which can be split again or can be filled with windows (similar to i3/ musca). Tags (or workspaces or virtual desktops or …) can be added/removed at runtime. Each tag contains its own layout. Exactly one tag is viewed on each monitor. The tags are monitor independent (similar to xmonad). It is configured at runtime via ipc calls from herbstclient. So the configuration file is just a script which is run on startup. (similar to wmii/musca).

	[https://herbstluftwm.org](https://herbstluftwm.org) || [herbstluftwm](https://www.archlinux.org/packages/?name=herbstluftwm)

*   **howm** — A lightweight, tiling X11 window manager that mimics vi by offering operators, motions and modes. Configuration is done through the included `config.h` file.

	[https://github.com/HarveyHunt/howm](https://github.com/HarveyHunt/howm) || [howm-x11](https://aur.archlinux.org/packages/howm-x11/)

*   **[i3](/index.php/I3 "I3")** — Tiling window manager, completely written from scratch. i3 was created because wmii, our favorite window manager at the time, did not provide some features we wanted (multi-monitor done right, for example), had some bugs, did not progress for quite some time, and was not easy to hack at all (source code comments/documentation completely lacking). Notable differences are in the areas of multi-monitor support and the tree metaphor. For speed the Plan 9 interface of wmii is not implemented.

	[https://i3wm.org/](https://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[Ion3](/index.php/Ion3 "Ion3")** — Tiling tabbed X11 window manager designed with keyboard users in mind. It was one of the first of the “new wave" of tiling windowing environments (the other being LarsWM, with quite a different approach) and has since spawned an entire category of tiling window managers for X11 – none of which really manage to reproduce the feel and functionality of Ion. It uses Lua as an embedded interpreter which handles all of the configuration.

	[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/)

*   **[Notion](/index.php/Notion "Notion")** — Tiling, tabbed window manager for the X window system that utilizes 'tiles' and 'tabbed' windows.
    *   Tiling: you divide the screen into non-overlapping 'tiles'. Every window occupies one tile, and is maximized to it
    *   Tabbing: a tile may contain multiple windows - they will be 'tabbed'.
    *   Static: most tiled window managers are 'dynamic', meaning they automatically resize and move around tiles as windows appear and disappear. Notion, by contrast, does not automatically change the tiling.

	Notion is a fork of Ion3.

	[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Simple Window Manager with no fat library dependencies, no fancy graphics, no window decorations, and no rodent dependence. It is largely modeled after GNU Screen which has done wonders in the virtual terminal market. Ratpoison is configured with a simple text file. The information bar in Ratpoison is somewhat different, as it shows only when needed. It serves as both an application launcher as well as a notification bar. Ratpoison does not include a system tray.

	[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Tiling, keyboard driven X11 Window Manager written entirely in Common Lisp. Stumpwm attempts to be customizable yet visually minimal. It does have various hooks to attach your personal customizations, and variables to tweak, and can be reconfigured and reloaded while running. There are no window decorations, no icons, no buttons, and no system tray. Its information bar can be set to show constantly or only when needed.

	[https://stumpwm.github.io/](https://stumpwm.github.io/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

*   **[subtle](/index.php/Subtle "Subtle")** — Manual tiling window manager with a rather uncommon approach of tiling: Per default there is no typical layout enforcement, windows are placed on a position (gravity) in a custom grid. The user can change the gravity of each window either directly per grabs or with rules defined by tags in the config. It has workspace tags and automatic client tagging, mouse and keyboard control as well as an extendable statusbar.

	[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle-git](https://aur.archlinux.org/packages/subtle-git/)

*   **[sway](/index.php/Sway "Sway")** — Sway is a drop-in replacement for the i3 window manager, but for Wayland instead of X11\. It works with your existing i3 configuration and supports most of i3's features, and a few extras.

	[http://swaywm.org/](http://swaywm.org/) || [sway](https://www.archlinux.org/packages/?name=sway)

*   **[way-cooler](/index.php?title=Way-cooler&action=edit&redlink=1 "Way-cooler (page does not exist)")** — Way Cooler is a tiling Wayland window manager, written in Rust, configurable using Lua, and extendable with D-Bus.

	[http://way-cooler.org/](http://way-cooler.org/) || [way-cooler](https://aur.archlinux.org/packages/way-cooler/)

*   **[WMFS](/index.php/WMFS "WMFS")** — Window Manager From Scratch is a lightweight and highly configurable tiling window manager for X. It can be configured with a configuration file, supports Xft (FreeType) fonts and is compliant with the Extended Window Manager Hints (EWMH) specifications, Xinerama and Xrandr. WMFS can be driven with Vi based commands (ViWMFS).

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/)

*   **[WMFS2](/index.php/WMFS2 "WMFS2")** — Incompatible successor of WMFS. It's even more minimalistic and brings some new stuff.

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs2-git](https://aur.archlinux.org/packages/wmfs2-git/)

### Dynamic window managers

*   **[awesome](/index.php/Awesome "Awesome")** — Highly configurable, next generation framework window manager for X. It is very fast, extensible and licensed under the GNU GPLv2 license. Configured in Lua, it has a system tray, information bar, and launcher built in. There are extensions available to it written in Lua. Awesome uses XCB as opposed to Xlib, which may result in a speed increase. Awesome has other features as well, such as an early replacement for notification-daemon, a right-click menu similar to that of the *box window managers, and many other things.

	[https://awesomewm.org/](https://awesomewm.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — Small window manager, even simpler than dwm, written in C. Configuration is done by modifying the config.h file and recompiling.

	[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/)

*   **[dwm](/index.php/Dwm "Dwm")** — Dynamic window manager for X. It manages windows in tiled, monocle and floating layouts. All of the layouts can be applied dynamically, optimising the environment for the application in use and the task performed. does not include a tray app or automatic launcher, although dmenu integrates well with it, as they are from the same author. It has no text configuration file. Configuration is done entirely by modifying the C source code, and it must be recompiled and restarted each time it is changed.

	[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://aur.archlinux.org/packages/dwm/)

*   **[echinus](/index.php/Echinus "Echinus")** — Simple and lightweight tiling and floating window manager for X11\. Started as a dwm fork with easier configuration, echinus became full-featured re-parenting window manager with EWMH support. It has an EWMH-compatible panel/taskbar, called [ourico](https://aur.archlinux.org/packages/ourico/).

	[http://plhk.ru](http://plhk.ru) || [echinus](https://aur.archlinux.org/packages/echinus/)

*   **[FrankenWM](/index.php/FrankenWM "FrankenWM")** — Basically monsterwm with floating done right. Features that are added on top of basic mwm include: more layouts (fibonacci, equal stack, dual stack), gaps (and borders) are adjustable on the fly, minimize/maximize single windows, hide/show all windows, resizing master and stack individually, invert stack.

	[https://github.com/sulami/FrankenWM](https://github.com/sulami/FrankenWM) || [frankenwm-git](https://aur.archlinux.org/packages/frankenwm-git/)

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Small dynamic tiling window manager for X11, largely inspired by xmonad and dwm. It tries to stay out of the way so that valuable screen real estate can be used for much more important stuff. It has sane defaults and is configured with a text file. It was written by hackers for hackers and it strives to be small, compact and fast. It has a built-in status bar fed from a user-defined script.

	[https://github.com/conformal/spectrwm/wiki](https://github.com/conformal/spectrwm/wiki) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm)

*   **[Qtile](/index.php/Qtile "Qtile")** — Full-featured, hackable tiling window manager written in Python. Qtile is simple, small, and extensible. It's easy to write your own layouts, widgets, and built-in commands.It is written and configured entirely in Python, which means you can leverage the full power and flexibility of the language to make it fit your needs.

	[https://github.com/qtile/qtile](https://github.com/qtile/qtile) || [qtile](https://www.archlinux.org/packages/?name=qtile)

*   **[wmii](/index.php/Wmii "Wmii")** — Small, dynamic window manager for X11\. It is scriptable, has a 9P filesystem interface and supports classic and tiling (Acme-like) window management. It aims to maintain a small and clean (read hackable and beautiful) codebase. The default configuration is in bash and [rc (the Plan 9 shell)](http://rc.cat-v.org), but programs exist written in ruby, and any program that can work with text can configure it. It has a status bar and launcher built in, and also an optional system tray (`witray`).

	[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://www.archlinux.org/packages/?name=wmii)

*   **[xmonad](/index.php/Xmonad "Xmonad")** — Dynamically tiling X11 window manager that is written and configured in Haskell. In a normal WM, you spend half your time aligning and searching for windows. Xmonad makes work easier, by automating this. XMonad is configured in Haskell. For all configuration changes, xmonad must be recompiled, so the Haskell compiler (over 100MB) must be installed. A large library called [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) provides many additional features

	[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

## See also

*   [http://www.gilesorr.com/wm/](http://www.gilesorr.com/wm/)
*   [http://www.slant.co/topics/390/~what-are-the-best-window-managers-for-linux](http://www.slant.co/topics/390/~what-are-the-best-window-managers-for-linux)
*   [https://l3net.wordpress.com/2013/03/17/a-memory-comparison-of-light-linux-desktops/](https://l3net.wordpress.com/2013/03/17/a-memory-comparison-of-light-linux-desktops/)