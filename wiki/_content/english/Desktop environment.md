Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Wayland](/index.php/Wayland "Wayland")
*   [Default applications](/index.php/Default_applications "Default applications")

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

The user is free to configure their GUI environment in any number of ways. Desktop environments simply provide a complete and convenient means of accomplishing this task. Note that users are free to mix-and-match applications from multiple desktop environments. For example, a KDE user may install and run GNOME applications such as the Epiphany web browser, should he/she prefer it over KDE's Konqueror web browser. One drawback of this approach is that many applications provided by desktop environment projects rely heavily upon their DE's respective underlying libraries. As a result, installing applications from a range of desktop environments will require installation of a larger number of dependencies. Users seeking to conserve disk space often avoid such mixed environments, or chose alternatives which do depend on only few external libraries.

Furthermore, DE-provided applications tend to integrate better with their native environments. Superficially, mixing environments with different widget toolkits will result in visual discrepancies (that is, interfaces will use different icons and widget styles). In terms of usability, mixed environments may not behave similarly (e.g. single-clicking versus double-clicking icons; drag-and-drop functionality) potentially causing confusion or unexpected behavior.

Prior to installing a desktop environment, a functional X server installation is required. See [Xorg](/index.php/Xorg "Xorg") for detailed information. Some desktop environments may also support [Wayland](/index.php/Wayland "Wayland") as an alternative to X, but most of these are still experimental.

## List of desktop environments

### Officially supported

*   **[Budgie](/index.php/Budgie_Desktop "Budgie Desktop")** — Budgie is a desktop environment designed with the modern user in mind, it focuses on simplicity and elegance.

	[https://budgie-desktop.org/](https://budgie-desktop.org/) || [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop)

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon strives to provide a traditional user experience. Cinnamon is a fork of GNOME 3.

	[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin "Deepin")** — Deepin desktop interface and apps feature an intuitive and elegant design. Moving around, sharing and searching etc. has become simply a joyful experience.

	[https://www.deepin.org/](https://www.deepin.org/) || [deepin](https://www.archlinux.org/groups/x86_64/deepin/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — The Enlightenment desktop shell provides an efficient window manager based on the Enlightenment Foundation Libraries along with other essential desktop components like a file manager, desktop icons and widgets. It supports themes, while still being capable of performing on older hardware or embedded devices.

	[https://www.enlightenment.org/](https://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME "GNOME")** — The GNOME desktop environment is an attractive and intuitive desktop with both a modern (*GNOME*) and a classic (*GNOME Classic*) session.

	[https://www.gnome.org/gnome-3/](https://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback is a shell for GNOME 3 which was initially called GNOME fallback mode. The desktop layout and the underlying technology is similar to GNOME 2.

	[https://wiki.gnome.org/Projects/GnomeFlashback](https://wiki.gnome.org/Projects/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **[KDE Plasma](/index.php/KDE_Plasma "KDE Plasma")** — The KDE Plasma desktop environment is a familiar working environment. Plasma offers all the tools required for a modern desktop computing experience so you can be productive right from the start.

	[https://www.kde.org/plasma-desktop](https://www.kde.org/plasma-desktop) || [plasma](https://www.archlinux.org/groups/x86_64/plasma/)

*   **[LXDE](/index.php/LXDE "LXDE")** — The Lightweight X11 Desktop Environment is a fast and energy-saving desktop environment. It comes with a modern interface, multi-language support, standard keyboard short cuts and additional features like tabbed file browsing. Fundamentally designed to be lightweight, LXDE strives to be less CPU and RAM intensive than other environments.

	[http://lxde.org/](http://lxde.org/) || GTK+ 2: [lxde](https://www.archlinux.org/groups/x86_64/lxde/), GTK+ 3: [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/)

*   **[LXQt](/index.php/LXQt "LXQt")** — LXQt is the Qt port and the upcoming version of LXDE, the Lightweight Desktop Environment. It is the product of the merge between the LXDE-Qt and the Razor-qt projects: A lightweight, modular, blazing-fast and user-friendly desktop environment.

	[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE "MATE")** — Mate provides an intuitive and attractive desktop to Linux users using traditional metaphors. MATE started as a fork of GNOME 2, but now uses GTK+ 3.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Sugar](/index.php/Sugar "Sugar")** — The Sugar Learning Platform is a computer environment composed of Activities designed to help children from 5 to 12 years of age learn together through rich-media expression. Sugar is the core component of a worldwide effort to provide every child with the opportunity for a quality education — it is currently used by nearly one-million children worldwide speaking 25 languages in over 40 countries. Sugar provides the means to help people lead fulfilling lives through access to a quality education that is currently missed by so many.

	[https://sugarlabs.org/](https://sugarlabs.org/) || [sugar](https://www.archlinux.org/packages/?name=sugar) + [sugar-fructose](https://www.archlinux.org/groups/x86_64/sugar-fructose/)

*   **[Xfce](/index.php/Xfce "Xfce")** — Xfce embodies the traditional [UNIX philosophy](https://en.wikipedia.org/wiki/UNIX_philosophy "wikipedia:UNIX philosophy") of modularity and re-usability. It consists of a number of components that provide the full functionality one can expect of a modern desktop environment, while remaining relatively light. They are packaged separately and you can pick among the available packages to create the optimal personal working environment.

	[http://www.xfce.org/](http://www.xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

### Unofficially supported

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — The "Equinox Desktop Environment" is a DE designed to be simple, extremely light-weight and fast.

	[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **[Liri](/index.php/Liri "Liri")** — Liri is a desktop environment with modern design and features. Liri is the merge between [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) and the [Liri Project](https://github.com/liri-project). Highly experimental.

	[https://liri.io/](https://liri.io/) || [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina is a lightweight desktop environment written in Qt 5 for FreeBSD that uses Fluxbox for window management.

	[https://lumina-desktop.org/](https://lumina-desktop.org/) || [lumina-desktop](https://aur.archlinux.org/packages/lumina-desktop/)

*   **[Moksha](/index.php/Moksha "Moksha")** — Fork of Enlightenment currently used as default desktop environment in Ubuntu-based Bodhi Linux.

	[http://www.bodhilinux.com/moksha-desktop/](http://www.bodhilinux.com/moksha-desktop/) || [moksha](https://aur.archlinux.org/packages/moksha/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with GNOME Shell and macOS.

	[https://elementary.io/](https://elementary.io/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)

*   **theShell** — theShell is a desktop environment that tries to be as transparent as possible. It uses Qt 5 as its widget toolkit and KWin as its window manager. It also incorporates a personal assistant.

	[https://vicr123.github.io/theshell](https://vicr123.github.io/theshell) || [theshell](https://aur.archlinux.org/packages/theshell/)

*   **[Trinity](/index.php/Trinity "Trinity")** — The Trinity Desktop Environment (TDE) project is a computer desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

## Comparison of desktop environments

*This section attempts to draw a comparison between popular desktop environments. Note that first-hand experience is the only effective way to truly evaluate whether a desktop environment best suits your needs.*

See also [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

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
[liri-calculator-git](https://aur.archlinux.org/packages/liri-calculator-git/) | Liri Text
[liri-text-git](https://aur.archlinux.org/packages/liri-text-git/) | EyeSight
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
[pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) | Pantheon Videos
[pantheon-videos](https://www.archlinux.org/packages/?name=pantheon-videos) | [Epiphany](/index.php/Epiphany "Epiphany")
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
[themedia](https://aur.archlinux.org/packages/themedia/) | [Konqueror](http://www.konqueror.org/)
[konqueror](https://www.archlinux.org/packages/?name=konqueror) | [LightDM](/index.php/LightDM "LightDM") Contemporary Greeter
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

### Resource use

In terms of system resources, GNOME and KDE are *expensive* desktop environments. Not only do complete installations consume more disk space than lightweight alternatives (LXDE, LXQt and Xfce) but also more CPU and memory resources while in use. This is because GNOME and KDE are relatively *full-featured*: they provide the most complete and well-integrated environments.

LXDE, LXQt and Xfce, on the other hand, are *lightweight* desktop environments. They are designed to work well on older or lower-power hardware and generally consume fewer system resources while in use. This is achieved by cutting back on *extra* features (which some would term *bloat*).

## Custom environments

Desktop environments represent the simplest means of installing a *complete* graphical environment. However, users are free to build and customize their graphical environment in any number of ways if none of the popular desktop environments meet their requirements. Generally, building a custom environment involves selection of a suitable [window manager](/index.php/Window_manager "Window manager"), a [taskbar](/index.php/List_of_applications#Taskbars "List of applications") and a number of applications (a minimalist selection usually includes a [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"), [file manager](/index.php/List_of_applications#File_managers "List of applications"), and [text editor](/index.php/Text_editor "Text editor")).

Other applications that are usually provided by desktop environments are:

*   Application launcher: [List of applications#Application launchers](/index.php/List_of_applications#Application_launchers "List of applications")
*   Clipboard manager: [Clipboard#List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard")
*   Desktop compositor: [Xorg#Composite](/index.php/Xorg#Composite "Xorg")
*   Desktop wallpaper setter and desktop icon: [List of applications#Wallpaper setters](/index.php/List_of_applications#Wallpaper_setters "List of applications") and [Openbox#Icon programs](/index.php/Openbox#Icon_programs "Openbox")
*   Display manager: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager")
*   Display power saving settings: [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   Logout dialogue: [Oblogout](/index.php/Oblogout "Oblogout")
*   Mount tool: [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications")
*   Notification daemon: [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications")
*   Polkit authentication agent: [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")
*   Screen locker: [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")
*   Sound volume manager: [List of applications#Volume managers](/index.php/List_of_applications#Volume_managers "List of applications")

### Custom window manager

In many desktop environments, it is possible to replace the supplied window manager. See below for instructions specific to your environment.

	GNOME

Alternative window managers cannot be used with GNOME Shell however [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") provides sessions for Metacity and [Compiz](/index.php/Compiz "Compiz"). Furthermore, it is possible to define your own [custom GNOME sessions](/index.php/GNOME/Tips_and_tricks#Custom_GNOME_sessions "GNOME/Tips and tricks") which use alternative components.

	Cinnamon

Alternative window managers cannot be used with [Cinnamon](/index.php/Cinnamon "Cinnamon").

	Other desktop environments

*   KDE - See [KDE#Using an alternative window manager](/index.php/KDE#Using_an_alternative_window_manager "KDE").

*   MATE - See [MATE#Use a different window manager with MATE](/index.php/MATE#Use_a_different_window_manager_with_MATE "MATE").

*   Xfce - See [Xfce#Default window manager](/index.php/Xfce#Default_window_manager "Xfce").

*   LXDE - See [LXDE#Replace Openbox](/index.php/LXDE#Replace_Openbox "LXDE").

*   LXQt - See [LXQt#Replace Openbox](/index.php/LXQt#Replace_Openbox "LXQt").

*   Budgie - See [Budgie Desktop#Replace Budgie WM](/index.php/Budgie_Desktop#Replace_Budgie_WM "Budgie Desktop").

*   theShell - In theShell settings, under the "Danger" category, enter the command to start the window manager in "Window Manager Command"