Related articles

*   [Comparison of desktop environments](/index.php/Comparison_of_desktop_environments "Comparison of desktop environments")
*   [Category:Freedesktop.org](/index.php/Category:Freedesktop.org "Category:Freedesktop.org")

A [desktop environment](https://en.wikipedia.org/wiki/Desktop_environment "wikipedia:Desktop environment") (**DE**) is an implementation of the [desktop metaphor](https://en.wikipedia.org/wiki/Desktop_metaphor "wikipedia:Desktop metaphor") made of a bundle of programs, which share a common graphical user interface (GUI).

## Contents

*   [1 Overview](#Overview)
*   [2 List of desktop environments](#List_of_desktop_environments)
    *   [2.1 Officially supported](#Officially_supported)
    *   [2.2 Unofficially supported](#Unofficially_supported)
*   [3 Custom environments](#Custom_environments)
    *   [3.1 Use a different window manager](#Use_a_different_window_manager)

## Overview

A desktop environment bundles together a variety of components to provide common graphical user interface elements such as icons, toolbars, wallpapers, and desktop widgets. Additionally, most desktop environments include a set of integrated applications and utilities. Most importantly, desktop environments provide their own [window manager](/index.php/Window_manager "Window manager"), which can however usually be replaced with another compatible one.

The user is free to configure their GUI environment in any number of ways. Desktop environments simply provide a complete and convenient means of accomplishing this task. Note that users are free to mix-and-match applications from multiple desktop environments. For example, a [KDE](/index.php/KDE "KDE") user may install and run [GNOME](/index.php/GNOME "GNOME") applications such as the [Epiphany](/index.php/Epiphany "Epiphany") web browser, should he/she prefer it over KDE's Konqueror web browser. One drawback of this approach is that many applications provided by desktop environment projects rely heavily upon their DE's respective underlying libraries. As a result, installing applications from a range of desktop environments will require installation of a larger number of dependencies. Users seeking to conserve disk space often avoid such mixed environments, or chose alternatives which do depend on only few external libraries.

Furthermore, DE-provided applications tend to integrate better with their native environments. Superficially, mixing environments with different widget toolkits will result in visual discrepancies (that is, interfaces will use different icons and widget styles). In terms of usability, mixed environments may not behave similarly (e.g. single-clicking versus double-clicking icons; drag-and-drop functionality) potentially causing confusion or unexpected behavior.

Prior to installing a desktop environment, a functional X server installation is required. See [Xorg](/index.php/Xorg "Xorg") for detailed information. Some desktop environments may also support [Wayland](/index.php/Wayland "Wayland") as an alternative to X, but most of these are still experimental.

## List of desktop environments

### Officially supported

*   **[Budgie](/index.php/Budgie "Budgie")** — Budgie is a desktop environment designed with the modern user in mind, it focuses on simplicity and elegance.

	[https://budgie-desktop.org/](https://budgie-desktop.org/) || [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop)

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon strives to provide a traditional user experience. Cinnamon is a fork of GNOME 3.

	[http://developer.linuxmint.com/projects/cinnamon-projects.html](http://developer.linuxmint.com/projects/cinnamon-projects.html) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

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

	[https://lxde.org/](https://lxde.org/) || GTK+ 2: [lxde](https://www.archlinux.org/groups/x86_64/lxde/), GTK+ 3: [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/)

*   **[LXQt](/index.php/LXQt "LXQt")** — LXQt is the Qt port and the upcoming version of LXDE, the Lightweight Desktop Environment. It is the product of the merge between the LXDE-Qt and the Razor-qt projects: A lightweight, modular, blazing-fast and user-friendly desktop environment.

	[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE "MATE")** — Mate provides an intuitive and attractive desktop to Linux users using traditional metaphors. MATE started as a fork of GNOME 2, but now uses GTK+ 3.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Sugar](/index.php/Sugar "Sugar")** — The Sugar Learning Platform is a computer environment composed of Activities designed to help children from 5 to 12 years of age learn together through rich-media expression. Sugar is the core component of a worldwide effort to provide every child with the opportunity for a quality education — it is currently used by nearly one-million children worldwide speaking 25 languages in over 40 countries. Sugar provides the means to help people lead fulfilling lives through access to a quality education that is currently missed by so many.

	[https://sugarlabs.org/](https://sugarlabs.org/) || [sugar](https://www.archlinux.org/packages/?name=sugar) + [sugar-fructose](https://www.archlinux.org/groups/x86_64/sugar-fructose/)

*   **[Xfce](/index.php/Xfce "Xfce")** — Xfce embodies the traditional [UNIX philosophy](https://en.wikipedia.org/wiki/UNIX_philosophy "wikipedia:UNIX philosophy") of modularity and re-usability. It consists of a number of components that provide the full functionality one can expect of a modern desktop environment, while remaining relatively light. They are packaged separately and you can pick among the available packages to create the optimal personal working environment.

	[https://xfce.org/](https://xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

### Unofficially supported

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — The "Equinox Desktop Environment" is a desktop environment designed to be simple, extremely light-weight and fast.

	[https://edeproject.org/](https://edeproject.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **[Liri](/index.php/Liri "Liri")** — Liri is a desktop environment with modern design and features. Liri is the merge between [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) and the [Liri Project](https://github.com/liri-project). Highly experimental.

	[https://liri.io/](https://liri.io/) || [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina is a lightweight desktop environment written in Qt 5 for FreeBSD that uses Fluxbox for window management.

	[https://lumina-desktop.org/](https://lumina-desktop.org/) || [lumina-desktop](https://aur.archlinux.org/packages/lumina-desktop/)

*   **[Moksha](/index.php/Moksha "Moksha")** — Fork of Enlightenment currently used as default desktop environment in Ubuntu-based Bodhi Linux.

	[http://www.bodhilinux.com/moksha-desktop/](http://www.bodhilinux.com/moksha-desktop/) || [moksha](https://aur.archlinux.org/packages/moksha/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with GNOME Shell and macOS.

	[https://elementary.io/](https://elementary.io/) || [pantheon-session-git](https://aur.archlinux.org/packages/pantheon-session-git/)

*   **theShell** — theShell is a desktop environment that tries to be as transparent as possible. It uses Qt 5 as its widget toolkit and KWin as its window manager.

	[https://vicr123.com/theshell/](https://vicr123.com/theshell/) || [theshell](https://aur.archlinux.org/packages/theshell/)

*   **[Trinity](/index.php/Trinity "Trinity")** — The Trinity Desktop Environment (TDE) project is a computer desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

## Custom environments

Desktop environments represent the simplest means of installing a *complete* graphical environment. However, users are free to build and customize their graphical environment in any number of ways if none of the popular desktop environments meet their requirements. Generally, building a custom environment involves selection of a suitable [window manager](/index.php/Window_manager "Window manager"), a [taskbar](/index.php/List_of_applications#Taskbars "List of applications") and a number of applications (a minimalist selection usually includes a [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"), [file manager](/index.php/List_of_applications#File_managers "List of applications"), and [text editor](/index.php/Text_editor "Text editor")).

Other components usually provided by desktop environments are:

*   Application launcher: [List of applications#Application launchers](/index.php/List_of_applications#Application_launchers "List of applications")
*   Audio volume control: [List of applications#Volume control](/index.php/List_of_applications#Volume_control "List of applications")
*   [Clipboard manager](/index.php/Clipboard_manager "Clipboard manager")
*   Desktop compositor: [Xorg#Composite](/index.php/Xorg#Composite "Xorg")
*   Desktop wallpaper setter and desktop icon: [List of applications#Wallpaper setters](/index.php/List_of_applications#Wallpaper_setters "List of applications") and [Openbox#Desktop icons and wallpapers](/index.php/Openbox#Desktop_icons_and_wallpapers "Openbox")
*   Display manager: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager")
*   Display power saving settings: [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   Logout dialogue: [Oblogout](/index.php/Oblogout "Oblogout")
*   Mount tool: [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications")
*   Notification daemon: [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications")
*   Polkit authentication agent: [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")
*   Screen locker: [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")
*   Default applications: [XDG MIME Applications#mimeapps.list](/index.php/XDG_MIME_Applications#mimeapps.list "XDG MIME Applications")

### Use a different window manager

If the desktop environment has an article, see its *Use a different window manager* section, otherwise consult the official documentation.

*   [Budgie#Use a different window manager](/index.php/Budgie#Use_a_different_window_manager "Budgie")
*   [Cinnamon#Use a different window manager](/index.php/Cinnamon#Use_a_different_window_manager "Cinnamon")
*   [GNOME#Use a different window manager](/index.php/GNOME#Use_a_different_window_manager "GNOME")
*   [KDE#Use a different window manager](/index.php/KDE#Use_a_different_window_manager "KDE")
*   [LXDE#Use a different window manager](/index.php/LXDE#Use_a_different_window_manager "LXDE")
*   [LXQt#Use a different window manager](/index.php/LXQt#Use_a_different_window_manager "LXQt")
*   [MATE#Use a different window manager](/index.php/MATE#Use_a_different_window_manager "MATE")
*   [Xfce#Use a different window manager](/index.php/Xfce#Use_a_different_window_manager "Xfce")