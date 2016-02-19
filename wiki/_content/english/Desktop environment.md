A [desktop environment](https://en.wikipedia.org/wiki/Desktop_environment "wikipedia:Desktop environment") provides a *complete* graphical user interface (GUI) for a system by bundling together a variety of components written using a common widget toolkit and set of libraries.

## Contents

*   [1 Overview](#Overview)
*   [2 List of desktop environments](#List_of_desktop_environments)
    *   [2.1 Officially supported](#Officially_supported)
    *   [2.2 Unofficially supported](#Unofficially_supported)
*   [3 Comparison of desktop environments](#Comparison_of_desktop_environments)
    *   [3.1 Resource use](#Resource_use)
*   [4 Custom environments](#Custom_environments)
    *   [4.1 Custom window manager](#Custom_window_manager)

## Overview

A desktop environment bundles together a variety of components to provide common graphical user interface elements such as icons, toolbars, wallpapers, and desktop widgets. Additionally, most desktop environments include a set of integrated applications and utilities. Most importantly, desktop environments provide their own [window manager](/index.php/Window_manager "Window manager"), which can however usually be replaced with another compatible one.

The user is free to configure their GUI environment in any number of ways. Desktop environments simply provide a complete and convenient means of accomplishing this task. Note that users are free to mix-and-match applications from multiple desktop environments. For example, a KDE user may install and run GNOME applications such as the Epiphany web browser, should he/she prefer it over KDE's Konqueror web browser. One drawback of this approach is that many applications provided by desktop environment projects rely heavily upon their DE's respective underlying libraries. As a result, installing applications from a range of desktop environments will require installation of a larger number of dependencies. Users seeking to conserve disk space and avoid [software bloat](https://en.wikipedia.org/wiki/software_bloat "wikipedia:software bloat") often avoid such mixed environments, or look into lightweight alternatives.

Furthermore, DE-provided applications tend to integrate better with their native environments. Superficially, mixing environments with different widget toolkits will result in visual discrepancies (that is, interfaces will use different icons and widget styles). In terms of user experience, mixed environments may not behave similarly (e.g. single-clicking versus double-clicking icons; drag-and-drop functionality) potentially causing confusion or unexpected behavior.

Prior to installing a desktop environment, a functional X server installation is required. See [Xorg](/index.php/Xorg "Xorg") for detailed information. Some desktop environments may also support [Wayland](/index.php/Wayland "Wayland") as an alternative to X, but most of these are still experimental.

## List of desktop environments

### Officially supported

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon strives to provide a traditional user experience. Cinnamon is a fork of GNOME 3.

	[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")** — Deepin desktop interface and apps feature an intuitive and elegant design. Moving around, sharing and searching etc. has become simply a joyful experience.

	[http://www.deepin.org/?language=en](http://www.deepin.org/?language=en) || [deepin](https://www.archlinux.org/groups/x86_64/deepin/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — The Enlightenment desktop shell provides an efficient window manager based on the Enlightenment Foundation Libraries along with other essential desktop components like a file manager, desktop icons and widgets. It supports themes, while still being capable of performing on older hardware or embedded devices.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME "GNOME")** — The GNOME desktop environment is an attractive and intuitive desktop with both a modern (*GNOME*) and a classic (*GNOME Classic*) session.

	[http://www.gnome.org/gnome-3/](http://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback is a shell for GNOME 3 which was initially called GNOME fallback mode. The desktop layout and the underlying technology is similar to GNOME 2.

	[https://wiki.gnome.org/GnomeFlashback](https://wiki.gnome.org/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **[KDE Plasma](/index.php/KDE_Plasma "KDE Plasma")** — The KDE Plasma desktop environment is a familiar working environment. Plasma Desktop offers all the tools required for a modern desktop computing experience so you can be productive right from the start.

	[https://www.kde.org/workspaces/plasmadesktop/](https://www.kde.org/workspaces/plasmadesktop/) || [plasma](https://www.archlinux.org/groups/x86_64/plasma/)

*   **[LXDE](/index.php/LXDE "LXDE")** — The Lightweight X11 Desktop Environment is a fast and energy-saving desktop environment. It comes with a modern interface, multi-language support, standard keyboard short cuts and additional features like tabbed file browsing. Fundamentally designed to be lightweight, LXDE strives to be less CPU and RAM intensive than other environments.

	[http://lxde.org/](http://lxde.org/) || [lxde](https://www.archlinux.org/groups/x86_64/lxde/)

*   **[LXQt](/index.php/LXQt "LXQt")** — LXQt is the Qt port and the upcoming version of LXDE, the Lightweight Desktop Environment. It is the product of the merge between the LXDE-Qt and the Razor-qt projects: A lightweight, modular, blazing-fast and user-friendly desktop environment.

	[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE "MATE")** — Mate provides an intuitive and attractive desktop to Linux users using traditional metaphors. MATE is a fork of GNOME 2.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || GTK+ 2: [mate](https://www.archlinux.org/groups/x86_64/mate/), GTK+ 3 (experimental): [mate-gtk3](https://www.archlinux.org/groups/x86_64/mate-gtk3/)

*   **[Xfce](/index.php/Xfce "Xfce")** — Xfce embodies the traditional UNIX philosophy of modularity and re-usability. It consists of a number of components that provide the full functionality one can expect of a modern desktop environment, while remaining relatively light. They are packaged separately and you can pick among the available packages to create the optimal personal working environment.

	[http://www.xfce.org/](http://www.xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

### Unofficially supported

*   **[Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop")** — Budgie Desktop is a lightweight Desktop Environment designed with the modern user in mind, it focuses on simplicity and elegance. Also it resembles the Chrome/Chromium OS desktop layout.

	[https://solus-project.com/budgie/](https://solus-project.com/budgie/) || [budgie-desktop](https://aur.archlinux.org/packages/budgie-desktop/)

*   **[Common Desktop Environment](/index.php/Common_Desktop_Environment "Common Desktop Environment")** — The Common Desktop Environment (CDE) is a desktop environment for Unix and OpenVMS, based on the Motif widget toolkit. It was part of the UNIX98 Workstation Product Standard, and was long the "classic" Unix desktop associated with commercial Unix workstations.

	[http://sourceforge.net/projects/cdesktopenv/](http://sourceforge.net/projects/cdesktopenv/) || [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/)

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — The "Equinox Desktop Environment" is a DE designed to be simple, extremely light-weight and fast.

	[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **GNUstep** — GNUstep is a free, object-oriented, cross-platform development environment that strives for simplicity and elegance.

	[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

*   **[Hawaii](/index.php/Hawaii "Hawaii")** — Hawaii is a lightweight, coherent and fast desktop environment that relies on Qt 5, QtQuick and Wayland and is designed to offer the best UX for the device where it is running.

	[http://www.maui-project.org/](http://www.maui-project.org/) || [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina is a lightweight desktop environment written in Qt 5 for FreeBSD that uses Fluxbox for window management.

	[http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/](http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/) || [lumina-desktop-git](https://aur.archlinux.org/packages/lumina-desktop-git/)

*   **[Moksha](/index.php/Moksha "Moksha")** — Fork of Enlightenment currently used as default desktop environment in Ubuntu-based Bodhi Linux.

	[http://mokshadesktop.org/](http://mokshadesktop.org/) || [moksha](https://aur.archlinux.org/packages/moksha/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with GNOME Shell and Mac OS X.

	[http://elementaryos.org/](http://elementaryos.org/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)

*   **[Papyros shell](/index.php/Papyros_shell "Papyros shell")** — Papyros shell is a modern desktop shell which adheres to Google's Material Design guidelines.

	[http://papyros.io/](http://papyros.io/) || [papyros-shell](https://aur.archlinux.org/packages/papyros-shell/)

*   **ROX** — ROX is a fast, user friendly desktop which makes extensive use of drag-and-drop. The interface revolves around the file manager, following the traditional UNIX view that 'everything is a file' rather than trying to hide the filesystem beneath start menus, wizards, or druids. The aim is to make a system that is well designed and clearly presented. The ROX style favors using several small programs together instead of creating all-in-one mega-applications.

	[http://rox.sourceforge.net/desktop/](http://rox.sourceforge.net/desktop/) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[Sugar](/index.php/Sugar "Sugar")** — The Sugar Learning Platform is a computer environment composed of Activities designed to help children from 5 to 12 years of age learn together through rich-media expression. Sugar is the core component of a worldwide effort to provide every child with the opportunity for a quality education — it is currently used by nearly one-million children worldwide speaking 25 languages in over 40 countries. Sugar provides the means to help people lead fulfilling lives through access to a quality education that is currently missed by so many.

	[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://aur.archlinux.org/packages/sugar/)

*   **[Trinity](/index.php/Trinity "Trinity")** — The Trinity Desktop Environment (TDE) project is a computer desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — Unity is a shell for GNOME designed by Canonical for Ubuntu.

	[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || See [Unity](/index.php/Unity "Unity")

## Comparison of desktop environments

*This section attempts to draw a comparison between popular desktop environments. Note that first-hand experience is the only effective way to truly evaluate whether a desktop environment best suits your needs.*

See also [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

<caption>Overview of desktop environments</caption>
| Desktop environment | Widget toolkit | Window manager | Taskbar | Terminal emulator | File manager | Calculator | Text editor | Image viewer | Media player | Web browser | Display manager |
| [Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | budgie-wm
[budgie-desktop](https://aur.archlinux.org/packages/budgie-desktop/) | budgie-panel
[budgie-desktop](https://aur.archlinux.org/packages/budgie-desktop/) | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Chromium](/index.php/Chromium "Chromium")
[chromium](https://www.archlinux.org/packages/?name=chromium) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
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
| [Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment") | [GTK+](/index.php/GTK%2B "GTK+") 2/3, [Qt](/index.php/Qt "Qt") 5
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | Deepin Window Manager
[deepin-wm](https://www.archlinux.org/packages/?name=deepin-wm) | Deepin Dock
[deepin-dock](https://www.archlinux.org/packages/?name=deepin-dock) | Deepin Terminal
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | Deepin Movie
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
| [Enlightenment](/index.php/Enlightenment "Enlightenment") | [Elementary](https://www.enlightenment.org/about-efl)
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
| [Hawaii](/index.php/Hawaii "Hawaii") | [Qt](/index.php/Qt "Qt") 5
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
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror) | [SDDM](/index.php/SDDM "SDDM")
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
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LXDM](/index.php/LXDM "LXDM")
[lxdm](https://www.archlinux.org/packages/?name=lxdm) |
| [LXDE](/index.php/LXDE "LXDE") (GTK+ 3) | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Openbox](/index.php/Openbox "Openbox")
[openbox](https://www.archlinux.org/packages/?name=openbox) | [LXPanel](http://wiki.lxde.org/en/LXPanel)
[lxpanel-gtk3](https://aur.archlinux.org/packages/lxpanel-gtk3/) | [LXTerminal](http://wiki.lxde.org/en/LXTerminal)
[lxterminal-gtk3](https://aur.archlinux.org/packages/lxterminal-gtk3/) | [PCManFM](/index.php/PCManFM "PCManFM")
[pcmanfm-gtk3](https://aur.archlinux.org/packages/pcmanfm-gtk3/) | [Galculator](http://galculator.sourceforge.net/)
[galculator](https://www.archlinux.org/packages/?name=galculator) | L3afpad
[l3afpad](https://www.archlinux.org/packages/?name=l3afpad) | [GPicView](http://wiki.lxde.org/en/GPicView)
[gpicview-gtk3](https://aur.archlinux.org/packages/gpicview-gtk3/) | [LXMusic](http://wiki.lxde.org/en/LXMusic)
[lxmusic-gtk3](https://aur.archlinux.org/packages/lxmusic-gtk3/) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LXDM](/index.php/LXDM "LXDM")
[lxdm-gtk3](https://aur.archlinux.org/packages/lxdm-gtk3/) |
| [LXQt](/index.php/LXQt "LXQt") | [Qt](/index.php/Qt "Qt") 5
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
| [MATE](/index.php/MATE "MATE") (GTK+ 2) | [GTK+](/index.php/GTK%2B "GTK+") 2/3
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | Marco
[marco](https://www.archlinux.org/packages/?name=marco) | MATE Panel
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel) | MATE Terminal
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | Caja
[caja](https://www.archlinux.org/packages/?name=caja) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | pluma
[pluma](https://www.archlinux.org/packages/?name=pluma) | Eye of MATE
[eom](https://www.archlinux.org/packages/?name=eom) | [Parole](http://docs.xfce.org/apps/parole/start)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori-gtk2](https://www.archlinux.org/packages/?name=midori-gtk2) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [MATE](/index.php/MATE "MATE") (GTK+ 3) | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | Marco
[marco-gtk3](https://www.archlinux.org/packages/?name=marco-gtk3) | MATE Panel
[mate-panel-gtk3](https://www.archlinux.org/packages/?name=mate-panel-gtk3) | MATE Terminal
[mate-terminal-gtk3](https://www.archlinux.org/packages/?name=mate-terminal-gtk3) | Caja
[caja-gtk3](https://www.archlinux.org/packages/?name=caja-gtk3) | [Galculator](http://galculator.sourceforge.net/)
[galculator](https://www.archlinux.org/packages/?name=galculator) | pluma
[pluma-gtk3](https://www.archlinux.org/packages/?name=pluma-gtk3) | Eye of MATE
[eom-gtk3](https://www.archlinux.org/packages/?name=eom-gtk3) | [Parole](http://docs.xfce.org/apps/parole/start)
[parole](https://www.archlinux.org/packages/?name=parole) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") GTK+ Greeter
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Pantheon](/index.php/Pantheon "Pantheon") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Gala](https://launchpad.net/gala)
[gala-bzr](https://aur.archlinux.org/packages/gala-bzr/) | [Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/) | [Pantheon Terminal](https://launchpad.net/pantheon-terminal)
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | [Pantheon Files](https://launchpad.net/pantheon-files)
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) | [Pantheon Calculator](https://launchpad.net/pantheon-calculator)
[pantheon-calculator](https://aur.archlinux.org/packages/pantheon-calculator/) | [Scratch](https://launchpad.net/scratch)
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) | [Pantheon Photos](https://launchpad.net/pantheon-photos)
[pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) | [Audience](https://launchpad.net/audience)
[audience](https://www.archlinux.org/packages/?name=audience) | [Midori](/index.php/Midori "Midori")
[midori](https://www.archlinux.org/packages/?name=midori) | [LightDM](/index.php/LightDM "LightDM") Pantheon Greeter
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/) |
| ROX | [GTK+](/index.php/GTK%2B "GTK+") 2
[gtk2](https://www.archlinux.org/packages/?name=gtk2) | [OroboROX](http://rox.sourceforge.net/desktop/OroboROX.html)
[oroborox](https://aur.archlinux.org/packages/oroborox/) | [ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)
[rox](https://www.archlinux.org/packages/?name=rox) | [ROXTerm](http://roxterm.sourceforge.net/)
[roxterm-gtk2](https://aur.archlinux.org/packages/roxterm-gtk2/) | [ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)
[rox](https://www.archlinux.org/packages/?name=rox) | [Galculator](http://galculator.sourceforge.net/)
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [Edit](http://rox.sourceforge.net/desktop/Edit.html)
[rox-edit](https://aur.archlinux.org/packages/rox-edit/) | [Picky](http://rox.sourceforge.net/desktop/picky.html)
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picky)</small> | [MusicBox](http://rox.sourceforge.net/desktop/Software/Audio_Video/MusicBox.html)
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=musicbox)</small> | [Midori](/index.php/Midori "Midori")
[midori-gtk2](https://www.archlinux.org/packages/?name=midori-gtk2) | [XDM](/index.php/XDM "XDM")
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Sugar](/index.php/Sugar "Sugar") | [GTK+](/index.php/GTK%2B "GTK+") 3
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
| [Unity](/index.php/Unity "Unity") | [GTK+](/index.php/GTK%2B "GTK+") 3
[gtk3](https://www.archlinux.org/packages/?name=gtk3) | [Compiz](/index.php/Compiz "Compiz")
[compiz-ubuntu](https://aur.archlinux.org/packages/compiz-ubuntu/) | [Unity](/index.php/Unity "Unity") | [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [GNOME Files](/index.php/GNOME_Files "GNOME Files")
[nautilus](https://www.archlinux.org/packages/?name=nautilus) | [GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit")
[gedit](https://www.archlinux.org/packages/?name=gedit) | [Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")
[eog](https://www.archlinux.org/packages/?name=eog) | [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")
[totem](https://www.archlinux.org/packages/?name=totem) | [Firefox](/index.php/Firefox "Firefox")
[firefox](https://www.archlinux.org/packages/?name=firefox) | [LightDM](/index.php/LightDM "LightDM") Unity Greeter
[lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) |
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

### Resource use

In terms of system resources, GNOME and KDE are *expensive* desktop environments. Not only do complete installations consume more disk space than lightweight alternatives (Enlightenment, LXDE, LXQt and Xfce) but also more CPU and memory resources while in use. This is because GNOME and KDE are relatively *full-featured*: they provide the most complete and well-integrated environments.

Enlightenment, LXDE, LXQt and Xfce, on the other hand, are *lightweight* desktop environments. They are designed to work well on older or lower-power hardware and generally consume fewer system resources while in use. This is achieved by cutting back on *extra* features (which some would term *bloat*).

## Custom environments

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

### Custom window manager

In many desktop environments, it is possible to replace the supplied window manager. See below for instructions specific to your environment.

	GNOME

Alternative window managers cannot be used with GNOME Shell however [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") provides sessions for Metacity and [Compiz](/index.php/Compiz "Compiz"). Furthermore, it is possible to define your own [custom GNOME sessions](/index.php/GNOME#Custom_GNOME_sessions "GNOME") which use alternative components.

	Cinnamon

Alternative window managers cannot be used with [Cinnamon](/index.php/Cinnamon "Cinnamon").

	Other desktop environments

*   KDE - See [KDE#Using an alternative window manager](/index.php/KDE#Using_an_alternative_window_manager "KDE").

*   MATE - See [MATE#Use a different window manager with MATE](/index.php/MATE#Use_a_different_window_manager_with_MATE "MATE").

*   Xfce - See [Xfce#Default window manager](/index.php/Xfce#Default_window_manager "Xfce").

*   LXDE - See [LXDE#Replace Openbox](/index.php/LXDE#Replace_Openbox "LXDE").

*   LXQt - See [LXQt#Replace Openbox](/index.php/LXQt#Replace_Openbox "LXQt").