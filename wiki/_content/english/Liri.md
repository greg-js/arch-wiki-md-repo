Related articles

*   [Wayland](/index.php/Wayland "Wayland")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Qt](/index.php/Qt "Qt")

[Liri](https://liri.io/) is a desktop environment with modern design and features. Liri is the merge between [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) and the [Liri Project](https://github.com/liri-project).

**Warning:** Liri is currently in alpha stage and there might be issues.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting the desktop](#Starting_the_desktop)
    *   [2.1 Run with a graphical login manager](#Run_with_a_graphical_login_manager)
    *   [2.2 Run from a tty](#Run_from_a_tty)
    *   [2.3 Run with systemd user session](#Run_with_systemd_user_session)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the meta package [liri-git-meta](https://aur.archlinux.org/packages/liri-git-meta/) to get all the LiriOS ecosystem.

Alternatively, it could be installed using [flatpak](https://www.archlinux.org/packages/?name=flatpak). See Flatpak instructions in [LiriOS Download page](https://liri.io/download/#flatpak-panel).

## Starting the desktop

### Run with a graphical login manager

Login managers that support Wayland such as [SDDM](/index.php/SDDM "SDDM") and [GDM](/index.php/GDM "GDM") can run a Liri session.

### Run from a tty

Log in to a tty and type:

 `$ liri-session` 

The session manager automatically detects the hardware and will run the compositor accordingly.

However the mode can be forced, for example to force nested mode and run inside Weston:

 `$ liri-session -platform wayland` 
**Note:** Do not use `~/.xinitrc` to start Liri. [Xinit](/index.php/Xinit "Xinit") is commonly used to start [Xorg](/index.php/Xorg "Xorg"), but Liri uses Wayland, which is a newer graphical protocol.

### Run with systemd user session

First you need to setup D-Bus with systemd user session as explained on [Systemd/User](/index.php/Systemd/User "Systemd/User"). Then [enable](/index.php/Enable "Enable") the `liri.service` unit with:

 `$ systemctl --user enable liri.service` 

Every time you want to [start](/index.php/Start "Start") a Liri session:

 `$ systemctl --user isolate liri.target` 

logind integration is know not to work with systemd user session at the moment, hence some features might not be working. systemd user session is pretty new and the developers are testing Liri with it.

## See also

*   [Official web site](https://liri.io/)
*   [Liri's GitHub page](https://github.com/lirios)