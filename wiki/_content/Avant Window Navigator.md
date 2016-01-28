# Avant Window Navigator

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

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

*   **Avant Window Navigator** can be installed with the package [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/)<sup><small>AUR</small></sup>, available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").
*   To get additional applets to use with AWN you will need to install [awn-extras-applets](https://aur.archlinux.org/packages/awn-extras-applets/)<sup><small>AUR</small></sup>.

### Additional dependencies

The most of the applets require some additional packages, which are listed in optdepends. Make sure that you installed them before enable an applet:

<table class="wikitable">

<tbody>

<tr>

<td>Applet name</td>

<td>Dependencies</td>

<td>Optional dependences</td>

</tr>

<tr>

<td>animal-farm</td>

<td>[fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod)</td>

</tr>

<tr>

<td>battery</td>

<td>[upower](https://www.archlinux.org/packages/?name=upower)</td>

</tr>

<tr>

<td>comics</td>

<td>[python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser) [python2-rsvg](https://www.archlinux.org/packages/?name=python2-rsvg)</td>

</tr>

<tr>

<td>cairo-clock</td>

<td>[python2-rsvg](https://www.archlinux.org/packages/?name=python2-rsvg)</td>

<td>[python2-dateutil](https://www.archlinux.org/packages/?name=python2-dateutil)</td>

</tr>

<tr>

<td>calendar</td>

<td>[python2-dateutil](https://www.archlinux.org/packages/?name=python2-dateutil) [python2-gdata](https://www.archlinux.org/packages/?name=python2-gdata) [python2-vobject](https://aur.archlinux.org/packages/python2-vobject/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>cpufreq</td>

<td>[gnome-applets](https://www.archlinux.org/packages/?name=gnome-applets)</td>

</tr>

<tr>

<td>dialect</td>

<td>[python-xklavier](https://aur.archlinux.org/packages/python-xklavier/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python-xklavier)]</sup></td>

</tr>

<tr>

<td>feeds</td>

<td>[python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser)</td>

</tr>

<tr>

<td>hardware-sensors</td>

<td>[python2-rsvg](https://www.archlinux.org/packages/?name=python2-rsvg)</td>

<td>[hddtemp](https://www.archlinux.org/packages/?name=hddtemp) [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors)</td>

</tr>

<tr>

<td>media-control</td>

<td>[banshee](https://www.archlinux.org/packages/?name=banshee)</td>

</tr>

<tr>

<td>media-player</td>

<td>[gstreamer0.10-python](https://www.archlinux.org/packages/?name=gstreamer0.10-python)</td>

</tr>

<tr>

<td>mail</td>

<td>[python2-feedparser](https://www.archlinux.org/packages/?name=python2-feedparser)</td>

</tr>

<tr>

<td>slickswitcher</td>

<td>[python2-wnck](https://www.archlinux.org/packages/?name=python2-wnck)</td>

<td>[python2-gconf](https://www.archlinux.org/packages/?name=python2-gconf)</td>

</tr>

<tr>

<td>stacks</td>

<td>[python2-libgnome](https://www.archlinux.org/packages/?name=python2-libgnome) [python2-gnomedesktop](https://www.archlinux.org/packages/?name=python2-gnomedesktop)</td>

</tr>

<tr>

<td>thinkhdaps</td>

<td>[python2-pyinotify](https://www.archlinux.org/packages/?name=python2-pyinotify)</td>

</tr>

<tr>

<td>tomboy-applet</td>

<td>[tomboy](https://www.archlinux.org/packages/?name=tomboy)</td>

</tr>

<tr>

<td>volume-control</td>

<td>[gstreamer0.10-python](https://www.archlinux.org/packages/?name=gstreamer0.10-python)</td>

</tr>

</tbody>

</table>

### Compositing

To fully utilize AWN and it's themes, you will need a composite manager like [Compiz](/index.php/Compiz "Compiz"), [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Cairo Compmgr](/index.php/Cairo_Compmgr "Cairo Compmgr") installed and configured correctly. If you are running AWN in a desktop environment like [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce") or [KDE](/index.php/KDE "KDE"), simply enable the composite manager or the desktop effects in the system settings. The [composite](/index.php/Composite "Composite") option in X is enabled by default.

## Usage

Run Awn in the background:

 `$ avant-window-navigator &` 

To launch AWN at startup, check **Start Awn automatically** option in Dock Preferences dialog (see below), or add the following command to the [autostart](/index.php/Autostarting#Graphical "Autostarting") file: `avant-window-navigator --startup &`

## Configuration

To configure AWN applets, themes and general settings, run:

 `$ awn-settings` 

or right-click the dock and go to **Dock Preferences**.

## Tips and tricks

### External applets

#### DockbarX

You may want to try [DockbarX](https://launchpad.net/dockbar), a task manager applet with advanced behaviour configuration and support for window previews. It is available from the [AUR](/index.php/AUR "AUR"): [dockbarx](https://aur.archlinux.org/packages/dockbarx/)<sup><small>AUR</small></sup>.

## See also

*   [AWN on Launchpad](https://launchpad.net/awn)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Avant_Window_Navigator&oldid=408677](https://wiki.archlinux.org/index.php?title=Avant_Window_Navigator&oldid=408677)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Application launchers](/index.php/Category:Application_launchers "Category:Application launchers")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")