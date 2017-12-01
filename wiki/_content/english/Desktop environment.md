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
| [Budgie](/index.php/Budgie_Desktop "Budgie Desktop") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) | [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nautilus](https://www.archlinux.org/packages/?name=nautilus) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](/index.php/Gedit "Gedit") | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | [gdm](https://www.archlinux.org/packages/?name=gdm) |
| [Cinnamon](/index.php/Cinnamon "Cinnamon") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [muffin](https://www.archlinux.org/packages/?name=muffin) | [cinnamon](https://www.archlinux.org/packages/?name=cinnamon) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nemo](https://www.archlinux.org/packages/?name=nemo) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [firefox](https://www.archlinux.org/packages/?name=firefox) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Deepin](/index.php/Deepin "Deepin") | [gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [deepin-wm](https://www.archlinux.org/packages/?name=deepin-wm) | [deepin-dock](https://www.archlinux.org/packages/?name=deepin-dock) | [deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal) | [deepin-file-manager](https://www.archlinux.org/packages/?name=deepin-file-manager) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [deepin-image-viewer](https://www.archlinux.org/packages/?name=deepin-image-viewer) | [deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie) | [chromium](https://www.archlinux.org/packages/?name=chromium) | [deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui) |
| [EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment") | [fltk](https://www.archlinux.org/packages/?name=fltk) | [pekwm](https://www.archlinux.org/packages/?name=pekwm) | [ede](https://aur.archlinux.org/packages/ede/) | [xterm](https://www.archlinux.org/packages/?name=xterm) | [fluff](https://aur.archlinux.org/packages/fluff/) | [zalc](https://aur.archlinux.org/packages/zalc/) | [fltk-editor](https://aur.archlinux.org/packages/fltk-editor/) | [ede](https://aur.archlinux.org/packages/ede/) | [flmusic](https://aur.archlinux.org/packages/flmusic/) | [dillo](https://www.archlinux.org/packages/?name=dillo) | [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [Enlightenment](/index.php/Enlightenment "Enlightenment") | [efl](https://www.archlinux.org/packages/?name=efl) | [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [terminology](https://www.archlinux.org/packages/?name=terminology) | [enlightenment](https://www.archlinux.org/packages/?name=enlightenment) | [equate-git](https://aur.archlinux.org/packages/equate-git/) | [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/) | [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/) | [rage](https://aur.archlinux.org/packages/rage/) | [links](https://www.archlinux.org/packages/?name=links) | [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) |
| [GNOME](/index.php/GNOME "GNOME") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [mutter](https://www.archlinux.org/packages/?name=mutter) | [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nautilus](https://www.archlinux.org/packages/?name=nautilus) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | [gdm](https://www.archlinux.org/packages/?name=gdm) |
| [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [metacity](https://www.archlinux.org/packages/?name=metacity) | [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel) | [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) | [nautilus](https://www.archlinux.org/packages/?name=nautilus) | [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator) | [gedit](https://www.archlinux.org/packages/?name=gedit) | [eog](https://www.archlinux.org/packages/?name=eog) | [totem](https://www.archlinux.org/packages/?name=totem) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | [gdm](https://www.archlinux.org/packages/?name=gdm) |
| [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [kwin](https://www.archlinux.org/packages/?name=kwin) | [plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop) | [konsole](https://www.archlinux.org/packages/?name=konsole) | [dolphin](https://www.archlinux.org/packages/?name=dolphin) | [kcalc](https://www.archlinux.org/packages/?name=kcalc) | [kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [gwenview](https://www.archlinux.org/packages/?name=gwenview) | [dragon](https://www.archlinux.org/packages/?name=dragon) | [konqueror](https://www.archlinux.org/packages/?name=konqueror) | [sddm](https://www.archlinux.org/packages/?name=sddm) |
| [Liri](/index.php/Liri "Liri") | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [greenisland](https://aur.archlinux.org/packages/greenisland/) | [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/) | [liri-terminal-git](https://aur.archlinux.org/packages/liri-terminal-git/) | [liri-files-git](https://aur.archlinux.org/packages/liri-files-git/) | [liri-calculator-git](https://aur.archlinux.org/packages/liri-calculator-git/) | [liri-text-git](https://aur.archlinux.org/packages/liri-text-git/) | [eyesight](https://aur.archlinux.org/packages/eyesight/) | liri-player | [liri-browser-git](https://aur.archlinux.org/packages/liri-browser-git/) | [sddm](https://www.archlinux.org/packages/?name=sddm) |
| [LXDE](/index.php/LXDE "LXDE") GTK+ 2 | [gtk2](https://www.archlinux.org/packages/?name=gtk2) | [openbox](https://www.archlinux.org/packages/?name=openbox) | [lxpanel](https://www.archlinux.org/packages/?name=lxpanel) | [lxterminal](https://www.archlinux.org/packages/?name=lxterminal) | [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) | [galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2) | [leafpad](https://www.archlinux.org/packages/?name=leafpad) | [gpicview](https://www.archlinux.org/packages/?name=gpicview) | [lxmusic](https://www.archlinux.org/packages/?name=lxmusic) | [midori](https://www.archlinux.org/packages/?name=midori) | [lxdm](https://www.archlinux.org/packages/?name=lxdm) |
| [LXDE](/index.php/LXDE "LXDE") GTK+ 3 | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [openbox](https://www.archlinux.org/packages/?name=openbox) | [lxpanel-gtk3](https://www.archlinux.org/packages/?name=lxpanel-gtk3) | [lxterminal-gtk3](https://www.archlinux.org/packages/?name=lxterminal-gtk3) | [pcmanfm-gtk3](https://www.archlinux.org/packages/?name=pcmanfm-gtk3) | [galculator](https://www.archlinux.org/packages/?name=galculator) | [l3afpad](https://www.archlinux.org/packages/?name=l3afpad) | [gpicview-gtk3](https://www.archlinux.org/packages/?name=gpicview-gtk3) | [lxmusic-gtk3](https://www.archlinux.org/packages/?name=lxmusic-gtk3) | [midori](https://www.archlinux.org/packages/?name=midori) | [lxdm-gtk3](https://www.archlinux.org/packages/?name=lxdm-gtk3) |
| [LXQt](/index.php/LXQt "LXQt") | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [openbox](https://www.archlinux.org/packages/?name=openbox) | [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel) | [qterminal](https://www.archlinux.org/packages/?name=qterminal) | [pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) | [speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch) | [notepadqq](https://www.archlinux.org/packages/?name=notepadqq) | [lximage-qt](https://www.archlinux.org/packages/?name=lximage-qt) | [smplayer](https://www.archlinux.org/packages/?name=smplayer) | [qupzilla](https://www.archlinux.org/packages/?name=qupzilla) | [sddm](https://www.archlinux.org/packages/?name=sddm) |
| [MATE](/index.php/MATE "MATE") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [marco](https://www.archlinux.org/packages/?name=marco) | [mate-panel](https://www.archlinux.org/packages/?name=mate-panel) | [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal) | [caja](https://www.archlinux.org/packages/?name=caja) | [mate-calc](https://www.archlinux.org/packages/?name=mate-calc) | [pluma](https://www.archlinux.org/packages/?name=pluma) | [eom](https://www.archlinux.org/packages/?name=eom) | [parole](https://www.archlinux.org/packages/?name=parole) | [midori](https://www.archlinux.org/packages/?name=midori) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| [Pantheon](/index.php/Pantheon "Pantheon") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [gala-git](https://aur.archlinux.org/packages/gala-git/) | [plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/) | [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal) | [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files) | [pantheon-calculator](https://aur.archlinux.org/packages/pantheon-calculator/) | [scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor) | [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) | [pantheon-videos](https://www.archlinux.org/packages/?name=pantheon-videos) | [epiphany](https://www.archlinux.org/packages/?name=epiphany) | 

[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/)

 |
| [Sugar](/index.php/Sugar "Sugar") | [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [metacity](https://www.archlinux.org/packages/?name=metacity) | [sugar](https://www.archlinux.org/packages/?name=sugar) | [sugar-activity-terminal](https://www.archlinux.org/packages/?name=sugar-activity-terminal) | [sugar](https://www.archlinux.org/packages/?name=sugar) | [sugar-activity-calculate](https://www.archlinux.org/packages/?name=sugar-activity-calculate) | [sugar-activity-write](https://www.archlinux.org/packages/?name=sugar-activity-write) | [sugar-activity-imageviewer](https://www.archlinux.org/packages/?name=sugar-activity-imageviewer) | [sugar-activity-jukebox](https://www.archlinux.org/packages/?name=sugar-activity-jukebox) | [sugar-activity-browse](https://www.archlinux.org/packages/?name=sugar-activity-browse) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |
| theShell | [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) | [kwin](https://www.archlinux.org/packages/?name=kwin) | [theshell](https://aur.archlinux.org/packages/theshell/) | [theterminal](https://aur.archlinux.org/packages/theterminal/) | [thefile](https://aur.archlinux.org/packages/thefile/) | [thecalculator](https://aur.archlinux.org/packages/thecalculator/) | [kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate) | [gwenview](https://www.archlinux.org/packages/?name=gwenview) | [themedia](https://aur.archlinux.org/packages/themedia/) | [konqueror](https://www.archlinux.org/packages/?name=konqueror) | [lightdm-webkit-theme-contemporary](https://aur.archlinux.org/packages/lightdm-webkit-theme-contemporary/) |
| [Trinity](/index.php/Trinity "Trinity") | TQt | TWin | Kicker | Konsole | Konqueror | KCalc | Kwrite Kate | Kuickshow | Kaffeine | Konqueror | TDM |
| [Xfce](/index.php/Xfce "Xfce") | [gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) | [xfwm4](https://www.archlinux.org/packages/?name=xfwm4) | [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel) | [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal) | [thunar](https://www.archlinux.org/packages/?name=thunar) | [galculator](https://www.archlinux.org/packages/?name=galculator) | [mousepad](https://www.archlinux.org/packages/?name=mousepad) | [ristretto](https://www.archlinux.org/packages/?name=ristretto) | [parole](https://www.archlinux.org/packages/?name=parole) | [midori](https://www.archlinux.org/packages/?name=midori) | [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) |

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