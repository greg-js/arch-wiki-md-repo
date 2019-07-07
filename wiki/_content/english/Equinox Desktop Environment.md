The [Equinox Desktop Environment](https://equinox-project.org/) (EDE) is a [desktop environment](/index.php/Desktop_environment "Desktop environment") designed to be simple, extremely light-weight and fast.

It primarily offers the most basic things: A window manager ([PekWM](/index.php/PekWM "PekWM") is used by default), a simple GUI including a panel, a daemon watching removable media and a notification daemon. Other than that there's not much more than some configuration programs, a calculator, etc. Beginning with version 2.0, EDE follows the FreeDesktop.org guidelines.

Unlike any other desktop environment, EDE² is based upon the [FLTK toolkit](http://fltk.org). It's especially fit for systems with little RAM or for users who want to completely customize their system and need a GUI that is not already bloated with functions and applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Custom repository](#Custom_repository)
*   [2 Starting the DE](#Starting_the_DE)
*   [3 Applications](#Applications)
    *   [3.1 Some recommendations](#Some_recommendations)

## Installation

EDE can be [installed](/index.php/Install "Install") from the [AUR](/index.php/AUR "AUR") with the [ede](https://aur.archlinux.org/packages/ede/) package.

Alternatively, you can obtain it from the [#Custom repository](#Custom_repository).

### Custom repository

To enable EDE's [unofficial user repository](/index.php/Unofficial_user_repository "Unofficial user repository"), add the following lines to your `/etc/pacman.conf`:

```
[ede]
SigLevel = Optional
Server = http://ede.elderlinux.org/repos/archlinux/$arch

```

Next [refresh the package lists](/index.php/Mirrors#Force_pacman_to_refresh_the_package_lists "Mirrors") and [install](/index.php/Install "Install") the EDE packages via [pacman](/index.php/Pacman "Pacman"):

*   *edelib*
*   *ede-common*
*   *ede*
*   *ede-wallpapers* (optional)

## Starting the DE

To bring up EDE you can either use a [Display manager](/index.php/Display_manager "Display manager") or use startx. If you choose the later, just write the following to the .xinitrc of your user:

```
 exec startede

```

## Applications

Since EDE is a bare-bone DE, you will have to add even the most common applications like a file manager or an editor yourself. It's all your freedom and choice.

Due to the nature of the DE, it obviously makes sense to install light-weight software. There are however not that many [FLTK](http://fltk.org) applications available so you will likely have to relay on a second toolkit like [GTK](/index.php/GTK "GTK") for example.

### Some recommendations

*   File manager: [PCManFM](/index.php/PCManFM "PCManFM")
*   Browser: [Dillo](/index.php/Dillo "Dillo") or [Midori](/index.php/Midori "Midori")
*   Editor: [Leafpad](http://tarot.freeshell.org/leafpad/)
*   Terminal emulator: [Xterm](/index.php/Xterm "Xterm")