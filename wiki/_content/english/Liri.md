Liri is a desktop environment with modern design and features. Liri is the merge between [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) and the [Liri Project](https://github.com/liri-project).

**Warning:** Liri is currently in alpha stage and there might be issues.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Other applications](#Other_applications)
*   [2 Starting the desktop](#Starting_the_desktop)
    *   [2.1 Run with a graphical login manager](#Run_with_a_graphical_login_manager)
    *   [2.2 Run from a tty](#Run_from_a_tty)
    *   [2.3 Run with systemd user session](#Run_with_systemd_user_session)
*   [3 See also](#See_also)

## Installation

Install [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Otherwise you can follow these instructions:

Add the following lines to your `/etc/pacman.conf` file:

 `/etc/pacman.conf` 
```
[liri-unstable]
SigLevel = Optional TrustAll
Server = [https://repo.liri.io/archlinux/unstable/$arch/](https://repo.liri.io/archlinux/unstable/$arch/)
```

Then run:

```
sudo pacman -Syu
sudo pacman -S liri-shell-git

```

### Other applications

For additional functionality, you may wish to install the following:

*   **liri-browser** — Material design web browser for Liri.

	[https://github.com/lirios/browser](https://github.com/lirios/browser) || [liri-browser-git](https://aur.archlinux.org/packages/liri-browser-git/)

*   **liri-files** — Material design file manager for Liri.

	[https://github.com/lirios/files](https://github.com/lirios/files) || [liri-files-git](https://aur.archlinux.org/packages/liri-files-git/)

*   **liri-player** — Material design media player for Liri.

	[https://github.com/lirios/player](https://github.com/lirios/player) || [liri-player-git](https://aur.archlinux.org/packages/liri-player-git/)

*   **liri-settings** — Settings application and modules for Liri.

	[https://github.com/lirios/settings](https://github.com/lirios/settings) || [liri-settings-git](https://aur.archlinux.org/packages/liri-settings-git/)

*   **liri-terminal** — Terminal for Liri.

	[https://github.com/lirios/terminal](https://github.com/lirios/terminal) || [liri-terminal-git](https://aur.archlinux.org/packages/liri-terminal-git/)

## Starting the desktop

### Run with a graphical login manager

Login managers that support Wayland such as [SDDM](/index.php/SDDM "SDDM") and [GDM](/index.php/GDM "GDM") can run a Liri session.

### Run from a tty

Log in to a tty and type:

 `$ liri-session` 

The session manager automatically detects the hardware and will run the compositor accordingly.

However the mode can be forced, for example to force nested mode and run inside Weston:

 `$ liri-session -platform wayland` 
**Note:** Do not use ~/.xinitrc to start Liri. [Xinit](/index.php/Xinit "Xinit") is commonly used to start [Xorg](/index.php/Xorg "Xorg"), but Liri uses Wayland, which is a newer graphical protocol.

### Run with systemd user session

First you need to setup D-Bus with systemd user session as examplained on [Systemd/User#D-Bus](/index.php/Systemd/User#D-Bus "Systemd/User"). Then enable the liri.service unit with:

 `$ systemctl --user enable liri.service` 

Every time you want to start a Liri session:

 `$ systemctl --user isolate liri.target` 

logind integration is know not to work with systemd user session at the moment, hence some features might not be working. systemd user session is pretty new and the developers are testing Liri with it.

## See also

*   [Official web site](https://liri.io/)
*   [Liri's GitHub page](https://github.com/lirios)