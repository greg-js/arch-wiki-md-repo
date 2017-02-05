Liri is a desktop environment with modern design and features. Liri is the merge between [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) and the [Liri Project](https://github.com/liri-project).

**Warning:** Liri is currently in alpha stage and there might be issues.

## Contents

*   [1 Installation](#Installation)
*   [2 Run with a graphical login manager](#Run_with_a_graphical_login_manager)
*   [3 Run from a tty](#Run_from_a_tty)
*   [4 Run with systemd user session](#Run_with_systemd_user_session)
*   [5 See also](#See_also)

## Installation

Install [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Run with a graphical login manager

Login managers that support Wayland such as [sddm](/index.php/Sddm "Sddm") and [gdm](/index.php/Gdm "Gdm") can run a Liri session.

## Run from a tty

Log in to a tty and type:

 `$ liri-session` 

The session manager automatically detects the hardware and will run the compositor accordingly.

However the mode can be forced, for example to force nested mode and run inside Weston:

 `$ liri-session -platform wayland` 
**Note:** Do not use ~/.xinitrc to start Liri. [Xinit](/index.php/Xinit "Xinit") is commonly used to start [Xorg](/index.php/Xorg "Xorg"), but Liri uses Wayland, which is a newer graphical protocol.

## Run with systemd user session

First you need to setup D-Bus with systemd user session as examplained on [Systemd/User#D-Bus](/index.php/Systemd/User#D-Bus "Systemd/User"). Then enable the liri.service unit with:

 `$ systemctl --user enable liri.service` 

Every time you want to start a Liri session:

 `$ systemctl --user isolate liri.target` 

logind integration is know not to work with systemd user session at the moment, hence some features might not be working. systemd user session is pretty new and the developers are testing Liri with it.

## See also

*   [Official web site](https://liri.io/)
*   [Liri's GitHub page](https://github.com/lirios)