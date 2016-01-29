# Hawaii

Related articles

*   [Wayland](/index.php/Wayland "Wayland")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Qt](/index.php/Qt "Qt")

From [phoronix.com](http://www.phoronix.com/scan.php?page=news_item&px=MTI4ODA):

NaN

**Warning:** The Hawaii desktop environment has not reached its stable 1.0 release.

## Contents

*   [1 Installation](#Installation)
*   [2 Run with a graphical login manager](#Run_with_a_graphical_login_manager)
*   [3 Run from a tty](#Run_from_a_tty)
*   [4 Run with systemd user session](#Run_with_systemd_user_session)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Portable keybindings](#Portable_keybindings)
*   [6 See also](#See_also)

## Installation

Install [hawaii-meta-git](https://aur.archlinux.org/packages/hawaii-meta-git/)<sup><small>AUR</small></sup> from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Run with a graphical login manager

Login managers that support Wayland such as sddm and gdm can run a Hawaii session.

## Run from a tty

Log in to a tty and type:

 `$ hawaii-session` 

The session manager automatically detects the hardware and will run the compositor accordingly.

However the mode can be forced, for example to force nested mode and run inside Weston:

 `$ hawaii-session --mode=nested` 

**Note:** Do not use ~/.xinitrc to start hawaii. [Xinit](/index.php/Xinit "Xinit") is commonly used to start [Xorg](/index.php/Xorg "Xorg"), but hawaii uses Wayland, which is a newer graphical protocol.

## Run with systemd user session

First you need to setup D-Bus with systemd user session as examplained on [Systemd/User#D-Bus](/index.php/Systemd/User#D-Bus "Systemd/User"). Then enable the hawaii.service unit with:

 `$ systemctl --user enable hawaii.service` 

Every time you want to start a Hawaii session:

 `$ systemctl --user isolate hawaii.target` 

logind integration is know not to work with systemd user session at the moment, hence some features might not be working. systemd user session is pretty new and the developers are testing Hawaii with it.

## Tips and tricks

### Portable keybindings

To export your keyboard shortcut keys, you should do:

 `$ dconf dump /org/hawaiios/desktop/keybindings/ > keybindings-backup.dconf` 

To later import it (for example) on another computer, do:

 `$ dconf load /org/hawaiios/desktop/keybindings/ < keybindings-backup.dconf` 

## See also

*   [http://hawaiios.org](http://hawaiios.org) Official Web site
*   [https://github.com/hawaii-desktop](https://github.com/hawaii-desktop) Hawaii's github page

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hawaii&oldid=406938](https://wiki.archlinux.org/index.php?title=Hawaii&oldid=406938)"