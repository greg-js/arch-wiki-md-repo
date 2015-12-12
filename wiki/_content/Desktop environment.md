# Desktop environment

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Default applications](/index.php/Default_applications "Default applications")

A [desktop environment](https://en.wikipedia.org/wiki/Desktop_environment "wikipedia:Desktop environment") provides a _complete_ graphical user interface (GUI) for a system by bundling together a variety of X clients written using a common widget toolkit and set of libraries.

## Contents

*   [1 Overview](#Overview)
*   [2 List of desktop environments](#List_of_desktop_environments)
    *   [2.1 Officially supported](#Officially_supported)
    *   [2.2 Unofficially supported](#Unofficially_supported)
*   [3 Comparison of desktop environments](#Comparison_of_desktop_environments)
    *   [3.1 Resource use](#Resource_use)
*   [4 Custom environments](#Custom_environments)

## Overview

A desktop environment bundles together a variety of X clients to provide common graphical user interface elements such as icons, toolbars, wallpapers, and desktop widgets. Additionally, most desktop environments include a set of integrated applications and utilities. Most importantly, desktop environments provide their own [window manager](/index.php/Window_manager "Window manager"), which can however usually be replaced with another compatible one.

The user is free to configure their GUI environment in any number of ways. Desktop environments simply provide a complete and convenient means of accomplishing this task. Note that users are free to mix-and-match applications from multiple desktop environments. For example, a KDE user may install and run GNOME applications such as the Epiphany web browser, should he/she prefer it over KDE's Konqueror web browser. One drawback of this approach is that many applications provided by desktop environment projects rely heavily upon their DE's respective underlying libraries. As a result, installing applications from a range of desktop environments will require installation of a larger number of dependencies. Users seeking to conserve disk space and avoid [software bloat](https://en.wikipedia.org/wiki/software_bloat "wikipedia:software bloat") often avoid such mixed environments, or look into lightweight alternatives.

Furthermore, DE-provided applications tend to integrate better with their native environments. Superficially, mixing environments with different widget toolkits will result in visual discrepancies (that is, interfaces will use different icons and widget styles). In terms of user experience, mixed environments may not behave similarly (e.g. single-clicking versus double-clicking icons; drag-and-drop functionality) potentially causing confusion or unexpected behavior.

Prior to installing a desktop environment, a functional X server installation is required. See [Xorg](/index.php/Xorg "Xorg") for detailed information.

## List of desktop environments

### Officially supported

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — Cinnamon strives to provide a traditional user experience. Cinnamon is a fork of GNOME 3.

[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")** — Deepin desktop interface and apps feature an intuitive and elegant design. Moving around, sharing and searching etc. has become simply a joyful experience.

[http://www.deepin.org/](http://www.deepin.org/) || [deepin](https://www.archlinux.org/groups/x86_64/deepin/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — The Enlightenment desktop shell provides an efficient window manager based on the Enlightenment Foundation Libraries along with other essential desktop components like a file manager, desktop icons and widgets. It supports themes, while still being capable of performing on older hardware or embedded devices.

[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME "GNOME")** — The GNOME desktop environment is an attractive and intuitive desktop with both a modern (_GNOME_) and a classic (_GNOME Classic_) session.

[http://www.gnome.org/gnome-3/](http://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback is a shell for GNOME 3 which was initially called GNOME fallback mode. The desktop layout and the underlying technology is similar to GNOME 2.

[https://wiki.gnome.org/GnomeFlashback](https://wiki.gnome.org/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **[KDE Plasma](/index.php/KDE "KDE")** — The KDE Plasma desktop environment is a familiar working environment. Plasma Desktop offers all the tools required for a modern desktop computing experience so you can be productive right from the start.

[https://www.kde.org/workspaces/plasmadesktop/](https://www.kde.org/workspaces/plasmadesktop/) || KDE 4: [kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace), Plasma 5: [plasma](https://www.archlinux.org/groups/x86_64/plasma/)

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

[https://solus-project.com/budgie/](https://solus-project.com/budgie/) || [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup>

*   **[Common Desktop Environment](/index.php/Common_Desktop_Environment "Common Desktop Environment")** — The Common Desktop Environment (CDE) is a desktop environment for Unix and OpenVMS, based on the Motif widget toolkit. It was part of the UNIX98 Workstation Product Standard, and was long the "classic" Unix desktop associated with commercial Unix workstations.

[http://sourceforge.net/projects/cdesktopenv/](http://sourceforge.net/projects/cdesktopenv/) || [cdesktopenv](https://aur.archlinux.org/packages/cdesktopenv/)<sup><small>AUR</small></sup>

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — The "Equinox Desktop Environment" is a DE designed to be simple, extremely light-weight and fast.

[http://equinox-project.org/](http://equinox-project.org/) || [ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup>

*   **GNUstep** — GNUstep is a free, object-oriented, cross-platform development environment that strives for simplicity and elegance.

[http://gnustep.org/](http://gnustep.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

*   **[Hawaii](/index.php/Hawaii "Hawaii")** — Hawaii is a lightweight, coherent and fast desktop environment that relies on Qt 5, QtQuick and Wayland and is designed to offer the best UX for the device where it is running.

[http://www.maui-project.org/](http://www.maui-project.org/) || [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)<sup><small>AUR</small></sup>

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina is a lightweight desktop environment written in QT 5 for FreeBSD that uses Fluxbox for window management.

[http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/](http://blog.pcbsd.org/2014/04/quick-lumina-desktop-faq/) || [lumina-desktop-git](https://aur.archlinux.org/packages/lumina-desktop-git/)<sup><small>AUR</small></sup>

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — Pantheon is the default desktop environment originally created for the elementary OS distribution. It is written from scratch using Vala and the GTK3 toolkit. With regards to usability and appearance, the desktop has some similarities with GNOME Shell and Mac OS X.

[http://elementaryos.org/](http://elementaryos.org/) || [pantheon-session-bzr](https://aur.archlinux.org/packages/pantheon-session-bzr/)<sup><small>AUR</small></sup>

*   **Papyros** — Papyros is a modern desktop shell which adheres to Google's Material Design guidelines.

[http://papyros.io/](http://papyros.io/) || [papyros-shell](https://aur.archlinux.org/packages/papyros-shell/)<sup><small>AUR</small></sup>

*   **ROX** — ROX is a fast, user friendly desktop which makes extensive use of drag-and-drop. The interface revolves around the file manager, following the traditional UNIX view that 'everything is a file' rather than trying to hide the filesystem beneath start menus, wizards, or druids. The aim is to make a system that is well designed and clearly presented. The ROX style favors using several small programs together instead of creating all-in-one mega-applications.

[http://rox.sourceforge.net/desktop/](http://rox.sourceforge.net/desktop/) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[Sugar](/index.php/Sugar "Sugar")** — The Sugar Learning Platform is a computer environment composed of Activities designed to help children from 5 to 12 years of age learn together through rich-media expression. Sugar is the core component of a worldwide effort to provide every child with the opportunity for a quality education — it is currently used by nearly one-million children worldwide speaking 25 languages in over 40 countries. Sugar provides the means to help people lead fulfilling lives through access to a quality education that is currently missed by so many.

[http://wiki.sugarlabs.org/](http://wiki.sugarlabs.org/) || [sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup>

*   **[Trinity](/index.php/Trinity "Trinity")** — The Trinity Desktop Environment (TDE) project is a computer desktop environment for Unix-like operating systems with a primary goal of retaining the overall KDE 3.5 computing style.

[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || See [Trinity](/index.php/Trinity "Trinity")

*   **[Unity](/index.php/Unity "Unity")** — Unity is a shell for GNOME designed by Canonical for Ubuntu.

[http://unity.ubuntu.com/](http://unity.ubuntu.com/) || See [Unity](/index.php/Unity "Unity")

## Comparison of desktop environments

_This section attempts to draw a comparison between popular desktop environments. Note that first-hand experience is the only effective way to truly evaluate whether a desktop environment best suits your needs._

See also [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

<table class="wikitable"><caption>Overview of desktop environments</caption>

<tbody>

<tr>

<th>Desktop environment</th>

<th>Widget toolkit</th>

<th>Window manager</th>

<th>Taskbar</th>

<th>Terminal emulator</th>

<th>File manager</th>

<th>Calculator</th>

<th>Text editor</th>

<th>Image viewer</th>

<th>Media player</th>

<th>Web browser</th>

<th>Display manager</th>

</tr>

<tr>

<td>[Budgie Desktop](/index.php/Budgie_Desktop "Budgie Desktop")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>budgie-wm  
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup></td>

<td>budgie-panel  
[budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/)<sup><small>AUR</small></sup></td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[Chromium](/index.php/Chromium "Chromium")  
[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Cinnamon](/index.php/Cinnamon "Cinnamon")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Muffin  
[muffin](https://www.archlinux.org/packages/?name=muffin)</td>

<td>Cinnamon  
[cinnamon](https://www.archlinux.org/packages/?name=cinnamon)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[Nemo](/index.php/Nemo "Nemo")  
[nemo](https://www.archlinux.org/packages/?name=nemo)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2/3, [Qt](/index.php/Qt "Qt") 5  
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>Deepin Window Manager  
[deepin-wm](https://www.archlinux.org/packages/?name=deepin-wm)</td>

<td>Deepin Dock  
[deepin-dock](https://www.archlinux.org/packages/?name=deepin-dock)</td>

<td>Deepin Terminal  
[deepin-terminal](https://www.archlinux.org/packages/?name=deepin-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>Deepin Movie  
[deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie)</td>

<td>[Chromium](/index.php/Chromium "Chromium")  
[chromium](https://www.archlinux.org/packages/?name=chromium)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Deepin Greeter  
[deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui)</td>

</tr>

<tr>

<td>[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")</td>

<td>[FLTK](http://www.fltk.org/)  
[fltk](https://www.archlinux.org/packages/?name=fltk)</td>

<td>[PekWM](/index.php/PekWM "PekWM")  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>EDE Panel  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>[XTerm](/index.php/Xterm "Xterm")  
[xterm](https://www.archlinux.org/packages/?name=xterm)</td>

<td>Fluff  
[fluff](https://aur.archlinux.org/packages/fluff/)<sup><small>AUR</small></sup></td>

<td>Calculator  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>Editor  
[fltk-editor](https://aur.archlinux.org/packages/fltk-editor/)<sup><small>AUR</small></sup></td>

<td>Image Viewer  
[ede](https://aur.archlinux.org/packages/ede/)<sup><small>AUR</small></sup></td>

<td>flmusic  
[flmusic](https://aur.archlinux.org/packages/flmusic/)<sup><small>AUR</small></sup></td>

<td>[Dillo](/index.php/Dillo "Dillo")  
[dillo](https://www.archlinux.org/packages/?name=dillo)</td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Enlightenment](/index.php/Enlightenment "Enlightenment")</td>

<td>[Elementary](https://www.enlightenment.org/about-efl)  
[elementary](https://www.archlinux.org/packages/?name=elementary)</td>

<td>Enlightenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>Enlightenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>[Terminology](https://www.enlightenment.org/about-terminology)  
[terminology](https://www.archlinux.org/packages/?name=terminology)</td>

<td>Enligthenment  
[enlightenment](https://www.archlinux.org/packages/?name=enlightenment)</td>

<td>Equate  
[equate-git](https://aur.archlinux.org/packages/equate-git/)<sup><small>AUR</small></sup></td>

<td>Ecrire  
[ecrire-git](https://aur.archlinux.org/packages/ecrire-git/)<sup><small>AUR</small></sup></td>

<td>Ephoto  
[ephoto-git](https://aur.archlinux.org/packages/ephoto-git/)<sup><small>AUR</small></sup></td>

<td>[Rage](https://www.enlightenment.org/about-rage)  
[rage](https://aur.archlinux.org/packages/rage/)<sup><small>AUR</small></sup></td>

<td>Elbow  
[elbow-git](https://aur.archlinux.org/packages/elbow-git/)<sup><small>AUR</small></sup></td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[GNOME](/index.php/GNOME "GNOME")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")  
[mutter](https://www.archlinux.org/packages/?name=mutter)</td>

<td>[GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell "wikipedia:GNOME Shell")  
[gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")  
[metacity](https://www.archlinux.org/packages/?name=metacity)</td>

<td>[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")  
[gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Epiphany](/index.php/Epiphany "Epiphany")  
[epiphany](https://www.archlinux.org/packages/?name=epiphany)</td>

<td>[GDM](/index.php/GDM "GDM")  
[gdm](https://www.archlinux.org/packages/?name=gdm)</td>

</tr>

<tr>

<td>GNUstep</td>

<td>[GNUstep](http://gnustep.org/)  
[gnustep-core](https://www.archlinux.org/groups/x86_64/gnustep-core/)</td>

<td>[Window Maker](/index.php/Window_Maker "Window Maker")  
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker)</td>

<td>[Window Maker](/index.php/Window_Maker "Window Maker")  
[windowmaker](https://www.archlinux.org/packages/?name=windowmaker)</td>

<td>[Terminal](http://gap.nongnu.org/terminal/index.html)  
[gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-terminal)]</sup></td>

<td>[GWorkspace](http://www.gnustep.org/experience/GWorkspace.html)  
[gworkspace](https://aur.archlinux.org/packages/gworkspace/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gworkspace)]</sup></td>

<td>[Calculator](http://www.gnustep.org/experience/examples.html)  
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-examples)]</sup></td>

<td>[Ink](http://www.gnustep.org/experience/examples.html)  
[gnustep-examples](https://aur.archlinux.org/packages/gnustep-examples/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-examples)]</sup></td>

<td>[LaternaMagica](http://gap.nongnu.org/laternamagica/index.html)  
[laternamagica](https://aur.archlinux.org/packages/laternamagica/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/laternamagica)]</sup></td>

<td>[Cynthiune](http://gap.nongnu.org/cynthiune/index.html)  
[cynthiune](https://aur.archlinux.org/packages/cynthiune/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cynthiune)]</sup></td>

<td>[SWK Browser](http://wiki.gnustep.org/index.php/SimpleWebKit)  
[swkbrowser-svn](https://aur.archlinux.org/packages/swkbrowser-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/swkbrowser-svn)]</sup></td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Hawaii](/index.php/Hawaii "Hawaii")</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>Green Island  
[greenisland-git](https://aur.archlinux.org/packages/greenisland-git/)<sup><small>AUR</small></sup></td>

<td>Hawaii Shell  
[hawaii-shell-git](https://aur.archlinux.org/packages/hawaii-shell-git/)<sup><small>AUR</small></sup></td>

<td>Terminal  
[hawaii-terminal-git](https://aur.archlinux.org/packages/hawaii-terminal-git/)<sup><small>AUR</small></sup></td>

<td>Swordfish  
[swordfish-git](https://aur.archlinux.org/packages/swordfish-git/)<sup><small>AUR</small></sup></td>

<td>[SpeedCrunch](http://speedcrunch.org/)  
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/)<sup><small>AUR</small></sup></td>

<td>JuffEd  
[juffed-qt5-git](https://aur.archlinux.org/packages/juffed-qt5-git/)<sup><small>AUR</small></sup></td>

<td>EyeSight  
[eyesight-git](https://aur.archlinux.org/packages/eyesight-git/)<sup><small>AUR</small></sup></td>

<td>SMPlayer  
[smplayer](https://www.archlinux.org/packages/?name=smplayer)</td>

<td>QupZilla  
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla)</td>

<td>SDDM  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[KDE](/index.php/KDE "KDE") 4</td>

<td>[Qt](/index.php/Qt "Qt") 4/5  
[qt4](https://www.archlinux.org/packages/?name=qt4) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>[Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_4#Desktop "wikipedia:KDE Plasma 4")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

<td>[Konsole](http://konsole.kde.org/)  
[konsole](https://www.archlinux.org/packages/?name=konsole)</td>

<td>[Dolphin](http://dolphin.kde.org/)  
[dolphin](https://www.archlinux.org/packages/?name=dolphin)</td>

<td>[KCalc](http://www.kde.org/applications/utilities/kcalc/)  
[kcalc](https://www.archlinux.org/packages/?name=kcalc)</td>

<td>[KWrite/Kate](http://kate-editor.org/)  
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate)</td>

<td>[Gwenview](http://gwenview.sourceforge.net/)  
[gwenview](https://www.archlinux.org/packages/?name=gwenview)</td>

<td>[Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)  
[dragon](https://www.archlinux.org/packages/?name=dragon)</td>

<td>[Konqueror](http://www.konqueror.org/)  
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)</td>

<td>[KDM](/index.php/KDM "KDM")  
[kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)</td>

</tr>

<tr>

<td>[KDE Plasma](/index.php/KDE "KDE") 5</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")  
[kwin](https://www.archlinux.org/packages/?name=kwin)</td>

<td>[Plasma Desktop](https://en.wikipedia.org/wiki/KDE_Plasma_5#Desktop "wikipedia:KDE Plasma 5")  
[plasma-desktop](https://www.archlinux.org/packages/?name=plasma-desktop)</td>

<td>[Konsole](http://konsole.kde.org/)  
[konsole](https://www.archlinux.org/packages/?name=konsole)</td>

<td>[Dolphin](http://dolphin.kde.org/)  
[dolphin](https://www.archlinux.org/packages/?name=dolphin)</td>

<td>[KCalc](http://www.kde.org/applications/utilities/kcalc/)  
[kcalc](https://www.archlinux.org/packages/?name=kcalc)</td>

<td>[KWrite/Kate](http://kate-editor.org/)  
[kwrite](https://www.archlinux.org/packages/?name=kwrite) [kate](https://www.archlinux.org/packages/?name=kate)</td>

<td>[Gwenview](http://gwenview.sourceforge.net/)  
[gwenview](https://www.archlinux.org/packages/?name=gwenview)</td>

<td>[Dragon Player](http://www.kde.org/applications/multimedia/dragonplayer/)  
[dragon](https://www.archlinux.org/packages/?name=dragon)</td>

<td>[Konqueror](http://www.konqueror.org/)  
[kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)</td>

<td>[SDDM](/index.php/SDDM "SDDM")  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[LXDE](/index.php/LXDE "LXDE") (GTK+ 2)</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>[LXPanel](http://wiki.lxde.org/en/LXPanel)  
[lxpanel](https://www.archlinux.org/packages/?name=lxpanel)</td>

<td>[LXTerminal](http://wiki.lxde.org/en/LXTerminal)  
[lxterminal](https://www.archlinux.org/packages/?name=lxterminal)</td>

<td>[PCManFM](/index.php/PCManFM "PCManFM")  
[pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>[Leafpad](http://tarot.freeshell.org/leafpad/)  
[leafpad](https://www.archlinux.org/packages/?name=leafpad)</td>

<td>[GPicView](http://wiki.lxde.org/en/GPicView)  
[gpicview](https://www.archlinux.org/packages/?name=gpicview)</td>

<td>[LXMusic](http://wiki.lxde.org/en/LXMusic)  
[lxmusic](https://www.archlinux.org/packages/?name=lxmusic)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LXDM](/index.php/LXDM "LXDM")  
[lxdm](https://www.archlinux.org/packages/?name=lxdm)</td>

</tr>

<tr>

<td>[LXDE](/index.php/LXDE "LXDE") (GTK+ 3)</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>[LXPanel](http://wiki.lxde.org/en/LXPanel)  
[lxpanel-gtk3](https://aur.archlinux.org/packages/lxpanel-gtk3/)<sup><small>AUR</small></sup></td>

<td>[LXTerminal](http://wiki.lxde.org/en/LXTerminal)  
[lxterminal-gtk3](https://aur.archlinux.org/packages/lxterminal-gtk3/)<sup><small>AUR</small></sup></td>

<td>[PCManFM](/index.php/PCManFM "PCManFM")  
[pcmanfm-gtk3](https://aur.archlinux.org/packages/pcmanfm-gtk3/)<sup><small>AUR</small></sup></td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator](https://www.archlinux.org/packages/?name=galculator)</td>

<td>L3afpad  
[l3afpad](https://www.archlinux.org/packages/?name=l3afpad)</td>

<td>[GPicView](http://wiki.lxde.org/en/GPicView)  
[gpicview-gtk3](https://aur.archlinux.org/packages/gpicview-gtk3/)<sup><small>AUR</small></sup></td>

<td>[LXMusic](http://wiki.lxde.org/en/LXMusic)  
[lxmusic-gtk3](https://aur.archlinux.org/packages/lxmusic-gtk3/)<sup><small>AUR</small></sup></td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LXDM](/index.php/LXDM "LXDM")  
[lxdm-gtk3](https://aur.archlinux.org/packages/lxdm-gtk3/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>[LXQt](/index.php/LXQt "LXQt")</td>

<td>[Qt](/index.php/Qt "Qt") 5  
[qt5-base](https://www.archlinux.org/packages/?name=qt5-base)</td>

<td>[Openbox](/index.php/Openbox "Openbox")  
[openbox](https://www.archlinux.org/packages/?name=openbox)</td>

<td>LXQt Panel  
[lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel)</td>

<td>QTerminal  
[qterminal](https://aur.archlinux.org/packages/qterminal/)<sup><small>AUR</small></sup></td>

<td>PCManFM-Qt  
[pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt)</td>

<td>[SpeedCrunch](http://speedcrunch.org/)  
[speedcrunch-git](https://aur.archlinux.org/packages/speedcrunch-git/)<sup><small>AUR</small></sup></td>

<td>JuffEd  
[juffed-qt5-git](https://aur.archlinux.org/packages/juffed-qt5-git/)<sup><small>AUR</small></sup></td>

<td>LxImage-Qt  
[lximage-qt](https://aur.archlinux.org/packages/lximage-qt/)<sup><small>AUR</small></sup></td>

<td>SMPlayer  
[smplayer](https://www.archlinux.org/packages/?name=smplayer)</td>

<td>QupZilla  
[qupzilla](https://www.archlinux.org/packages/?name=qupzilla)</td>

<td>SDDM  
[sddm](https://www.archlinux.org/packages/?name=sddm)</td>

</tr>

<tr>

<td>[MATE](/index.php/MATE "MATE") (GTK+ 2)</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2/3  
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Marco  
[marco](https://www.archlinux.org/packages/?name=marco)</td>

<td>MATE Panel  
[mate-panel](https://www.archlinux.org/packages/?name=mate-panel)</td>

<td>MATE Terminal  
[mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)</td>

<td>Caja  
[caja](https://www.archlinux.org/packages/?name=caja)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>pluma  
[pluma](https://www.archlinux.org/packages/?name=pluma)</td>

<td>Eye of MATE  
[eom](https://www.archlinux.org/packages/?name=eom)</td>

<td>[Parole](http://docs.xfce.org/apps/parole/start)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori-gtk2](https://www.archlinux.org/packages/?name=midori-gtk2)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[MATE](/index.php/MATE "MATE") (GTK+ 3)</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>Marco  
[marco-gtk3](https://www.archlinux.org/packages/?name=marco-gtk3)</td>

<td>MATE Panel  
[mate-panel-gtk3](https://www.archlinux.org/packages/?name=mate-panel-gtk3)</td>

<td>MATE Terminal  
[mate-terminal-gtk3](https://www.archlinux.org/packages/?name=mate-terminal-gtk3)</td>

<td>Caja  
[caja-gtk3](https://www.archlinux.org/packages/?name=caja-gtk3)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator](https://www.archlinux.org/packages/?name=galculator)</td>

<td>pluma  
[pluma-gtk3](https://www.archlinux.org/packages/?name=pluma-gtk3)</td>

<td>Eye of MATE  
[eom-gtk3](https://www.archlinux.org/packages/?name=eom-gtk3)</td>

<td>[Parole](http://docs.xfce.org/apps/parole/start)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Pantheon](/index.php/Pantheon "Pantheon")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Gala](https://launchpad.net/gala)  
[gala-bzr](https://aur.archlinux.org/packages/gala-bzr/)<sup><small>AUR</small></sup></td>

<td>[Plank](https://launchpad.net/plank)/[Wingpanel](https://launchpad.net/wingpanel)  
[plank](https://www.archlinux.org/packages/?name=plank) [wingpanel](https://aur.archlinux.org/packages/wingpanel/)<sup><small>AUR</small></sup></td>

<td>[Pantheon Terminal](https://launchpad.net/pantheon-terminal)  
[pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal)</td>

<td>[Pantheon Files](https://launchpad.net/pantheon-files)  
[pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[Scratch](https://launchpad.net/scratch)  
[scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor)</td>

<td>[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")  
[shotwell](https://www.archlinux.org/packages/?name=shotwell)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Pantheon Greeter  
[lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>ROX</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2  
[gtk2](https://www.archlinux.org/packages/?name=gtk2)</td>

<td>[OroboROX](http://rox.sourceforge.net/desktop/OroboROX.html)  
[oroborox](https://aur.archlinux.org/packages/oroborox/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/oroborox)]</sup></td>

<td>[ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)  
[rox](https://www.archlinux.org/packages/?name=rox)</td>

<td>[ROXTerm](http://roxterm.sourceforge.net/)  
[roxterm-gtk2](https://aur.archlinux.org/packages/roxterm-gtk2/)<sup><small>AUR</small></sup></td>

<td>[ROX-Filer](http://rox.sourceforge.net/desktop/ROX-Filer.html)  
[rox](https://www.archlinux.org/packages/?name=rox)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)</td>

<td>[Edit](http://rox.sourceforge.net/desktop/Edit.html)  
[rox-edit](https://aur.archlinux.org/packages/rox-edit/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rox-edit)]</sup></td>

<td>[Picky](http://rox.sourceforge.net/desktop/picky.html)  
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picky)</small></td>

<td>[MusicBox](http://rox.sourceforge.net/desktop/Software/Audio_Video/MusicBox.html)  
<small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=musicbox)</small></td>

<td>[Midori](/index.php/Midori "Midori")  
[midori-gtk2](https://www.archlinux.org/packages/?name=midori-gtk2)</td>

<td>[XDM](/index.php/XDM "XDM")  
[xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)</td>

</tr>

<tr>

<td>[Sugar](/index.php/Sugar "Sugar")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")  
[metacity](https://www.archlinux.org/packages/?name=metacity)</td>

<td>Sugar  
[sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup></td>

<td>Terminal  
[sugar-activity-terminal](https://aur.archlinux.org/packages/sugar-activity-terminal/)<sup><small>AUR</small></sup></td>

<td>Sugar Journal  
[sugar](https://aur.archlinux.org/packages/sugar/)<sup><small>AUR</small></sup></td>

<td>Calculate  
[sugar-activity-calculate](https://aur.archlinux.org/packages/sugar-activity-calculate/)<sup><small>AUR</small></sup></td>

<td>Write  
[sugar-activity-write](https://aur.archlinux.org/packages/sugar-activity-write/)<sup><small>AUR</small></sup></td>

<td>ImageViewer  
[sugar-activity-imageviewer](https://aur.archlinux.org/packages/sugar-activity-imageviewer/)<sup><small>AUR</small></sup></td>

<td>Jukebox  
[sugar-activity-jukebox](https://aur.archlinux.org/packages/sugar-activity-jukebox/)<sup><small>AUR</small></sup></td>

<td>Browse  
[sugar-activity-browse](https://aur.archlinux.org/packages/sugar-activity-browse/)<sup><small>AUR</small></sup></td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

<tr>

<td>[Trinity](/index.php/Trinity "Trinity")</td>

<td>TQt</td>

<td>TWin</td>

<td>Kicker</td>

<td>Konsole</td>

<td>Konqueror</td>

<td>KCalc</td>

<td>Kwrite / Kate</td>

<td>Kuickshow</td>

<td>Kaffeine</td>

<td>Konqueror</td>

<td>TDM</td>

</tr>

<tr>

<td>[Unity](/index.php/Unity "Unity")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 3  
[gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Compiz](/index.php/Compiz "Compiz")  
[compiz-ubuntu](https://aur.archlinux.org/packages/compiz-ubuntu/)<sup><small>AUR</small></sup></td>

<td>[Unity](/index.php/Unity "Unity")</td>

<td>[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")  
[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)</td>

<td>[GNOME Files](/index.php/GNOME_Files "GNOME Files")  
[nautilus](https://www.archlinux.org/packages/?name=nautilus)</td>

<td>[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")  
[gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)</td>

<td>[gedit](/index.php/Gedit "Gedit")  
[gedit](https://www.archlinux.org/packages/?name=gedit)</td>

<td>[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")  
[eog](https://www.archlinux.org/packages/?name=eog)</td>

<td>[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")  
[totem](https://www.archlinux.org/packages/?name=totem)</td>

<td>[Firefox](/index.php/Firefox "Firefox")  
[firefox](https://www.archlinux.org/packages/?name=firefox)</td>

<td>[LightDM](/index.php/LightDM "LightDM") Unity Greeter  
[lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>[Xfce](/index.php/Xfce "Xfce")</td>

<td>[GTK+](/index.php/GTK%2B "GTK+") 2/3  
[gtk2](https://www.archlinux.org/packages/?name=gtk2) [gtk3](https://www.archlinux.org/packages/?name=gtk3)</td>

<td>[Xfwm4](http://docs.xfce.org/xfce/xfwm4/start)  
[xfwm4](https://www.archlinux.org/packages/?name=xfwm4)</td>

<td>[Xfce Panel](http://docs.xfce.org/xfce/xfce4-panel/start)  
[xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)</td>

<td>[Terminal](http://www.xfce.org/projects/terminal)  
[xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)</td>

<td>[Thunar](/index.php/Thunar "Thunar")  
[thunar](https://www.archlinux.org/packages/?name=thunar)</td>

<td>[Galculator](http://galculator.sourceforge.net/)  
[galculator](https://www.archlinux.org/packages/?name=galculator)</td>

<td>Mousepad  
[mousepad](https://www.archlinux.org/packages/?name=mousepad)</td>

<td>[Ristretto](http://goodies.xfce.org/projects/applications/ristretto)  
[ristretto](https://www.archlinux.org/packages/?name=ristretto)</td>

<td>[Parole](http://docs.xfce.org/apps/parole/start)  
[parole](https://www.archlinux.org/packages/?name=parole)</td>

<td>[Midori](/index.php/Midori "Midori")  
[midori](https://www.archlinux.org/packages/?name=midori)</td>

<td>[LightDM](/index.php/LightDM "LightDM") GTK+ Greeter  
[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter)</td>

</tr>

</tbody>

</table>

### Resource use

In terms of system resources, GNOME and KDE are _expensive_ desktop environments. Not only do complete installations consume more disk space than lightweight alternatives (Enlightenment, LXDE, LXQt and Xfce) but also more CPU and memory resources while in use. This is because GNOME and KDE are relatively _full-featured_: they provide the most complete and well-integrated environments.

Enlightenment, LXDE, LXQt and Xfce, on the other hand, are _lightweight_ desktop environments. They are designed to work well on older or lower-power hardware and generally consume fewer system resources while in use. This is achieved by cutting back on _extra_ features (which some would term _bloat_).

## Custom environments

Desktop environments represent the simplest means of installing a _complete_ graphical environment. However, users are free to build and customize their graphical environment in any number of ways if none of the popular desktop environments meet their requirements. Generally, building a custom environment involves selection of a suitable [window manager](/index.php/Window_manager "Window manager"), a [taskbar](/index.php/List_of_applications#Taskbars_.2F_panels_.2F_docks "List of applications") and a number of applications (a minimalist selection usually includes a [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"), [file manager](/index.php/List_of_applications#File_managers "List of applications"), and [text editor](/index.php/Text_editor "Text editor")).

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Desktop_environment&oldid=411673](https://wiki.archlinux.org/index.php?title=Desktop_environment&oldid=411673)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")