Related articles

*   [GNOME](/index.php/GNOME "GNOME")

[Avant Window Navigator](https://launchpad.net/awn) (AWN) is a lightweight dock written in C. It has support for launchers, task lists and third party applets.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Compositing](#Compositing)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 External applets](#External_applets)
        *   [4.1.1 DockbarX](#DockbarX)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/) package. The [awn-extras-applets](https://aur.archlinux.org/packages/awn-extras-applets/) package provides additional applets.

The most of the applets require some additional packages, which are listed in optdepends. Make sure that you installed them before enable an applet.

### Compositing

To fully utilize AWN and it's themes, you will need a composite manager like [Compiz](/index.php/Compiz "Compiz") or [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") installed and configured correctly. If you are running AWN in a desktop environment like [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce") or [KDE](/index.php/KDE "KDE"), simply enable the composite manager or the desktop effects in the system settings. The [composite](/index.php/Composite "Composite") option in X is enabled by default.

## Usage

Run Awn in the background:

 `$ avant-window-navigator &` 

To launch AWN at startup, check **Start Awn automatically** option in Dock Preferences dialog (see below), or [autostart](/index.php/Autostart "Autostart") the command `avant-window-navigator --startup &`.

## Configuration

To configure AWN applets, themes and general settings, run:

 `$ awn-settings` 

or right-click the dock and go to **Dock Preferences**.

## Tips and tricks

### External applets

#### DockbarX

You may want to try [DockbarX](https://launchpad.net/dockbar), a task manager applet with advanced behaviour configuration and support for window previews. It is available from the [AUR](/index.php/AUR "AUR"): [dockbarx](https://aur.archlinux.org/packages/dockbarx/).

## See also

*   [AWN on Launchpad](https://launchpad.net/awn)