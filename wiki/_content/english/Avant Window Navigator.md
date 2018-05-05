Related articles

*   [GNOME](/index.php/GNOME "GNOME")

[Avant Window Navigator](https://launchpad.net/awn) (AWN) is a lightweight dock written in C. It has support for launchers, task lists and third party applets.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Additional dependencies](#Additional_dependencies)
    *   [1.2 Compositing](#Compositing)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 External applets](#External_applets)
        *   [4.1.1 DockbarX](#DockbarX)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/) package. The [awn-extras-applets](https://aur.archlinux.org/packages/awn-extras-applets/) package provides additional applets.

### Additional dependencies

The most of the applets require some additional packages, which are listed in optdepends. Make sure that you installed them before enable an applet:

| Applet name | Dependencies | Optional dependences |
| animal-farm | [fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod) |
| battery | [upower](https://www.archlinux.org/packages/?name=upower) |
| comics | [python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) [python2-rsvg](https://aur.archlinux.org/packages/python2-rsvg/) |
| cairo-clock | [python2-rsvg](https://aur.archlinux.org/packages/python2-rsvg/) | [python2-dateutil](https://www.archlinux.org/packages/?name=python2-dateutil) |
| calendar | [python2-dateutil](https://www.archlinux.org/packages/?name=python2-dateutil) [python2-gdata](https://www.archlinux.org/packages/?name=python2-gdata) [python2-vobject](https://www.archlinux.org/packages/?name=python2-vobject) |
| cpufreq | [gnome-applets](https://www.archlinux.org/packages/?name=gnome-applets) |
| dialect | [python-xklavier](https://aur.archlinux.org/packages/python-xklavier/) |
| feeds | [python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) |
| hardware-sensors | [python2-rsvg](https://aur.archlinux.org/packages/python2-rsvg/) | [hddtemp](https://www.archlinux.org/packages/?name=hddtemp) [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) |
| media-control | [banshee](https://aur.archlinux.org/packages/banshee/) |
| media-player | [gstreamer0.10-python](https://aur.archlinux.org/packages/gstreamer0.10-python/) |
| mail | [python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) |
| slickswitcher | [python2-wnck](https://www.archlinux.org/packages/?name=python2-wnck) | [python2-gconf](https://www.archlinux.org/packages/?name=python2-gconf) |
| stacks | [python2-libgnome](https://www.archlinux.org/packages/?name=python2-libgnome) [python2-gnomedesktop](https://www.archlinux.org/packages/?name=python2-gnomedesktop) |
| thinkhdaps | [python2-pyinotify](https://www.archlinux.org/packages/?name=python2-pyinotify) |
| tomboy-applet | [tomboy](https://www.archlinux.org/packages/?name=tomboy) |
| volume-control | [gstreamer0.10-python](https://aur.archlinux.org/packages/gstreamer0.10-python/) |

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