# Zeitgeist

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Zeitgeist](http://zeitgeist-project.com/) is a service which logs user activities and events, anywhere from files opened to websites visited or conversations held via email and more. It makes this information readily available for other applications to use in the form of timelines and statistics. See the [Wikipedia article](https://en.wikipedia.org/wiki/Zeitgeist_(framework) "wikipedia:Zeitgeist (framework)") for a more detailed description of Zeitgeist itself.

## Installation

Install [zeitgeist](https://www.archlinux.org/packages/?name=zeitgeist) from the [official repositories](/index.php/Official_repositories "Official repositories"), which includes the daemon and the datahub. The daemon receives metadata from data sources, and provides them to applications using D-Bus. The datahub provides passive plugins which insert events into Zeitgeist.

To configure what gets logged by Zeitgeist, install [activity-log-manager](https://www.archlinux.org/packages/?name=activity-log-manager) which provides a graphical user interface where you can filter out specific folders, file types, and applications. The GNOME Control Center also has a Privacy module where you can make similar adjustments.

To monitor and inspect Zeitgeist's log at a low level, install [zeitgeist-explorer](https://aur.archlinux.org/packages/zeitgeist-explorer/)<sup><small>AUR</small></sup> which provides a graphical user interface where you can see the events logged in real-time just like wireshark.

### Data providers

The following applications are just some of the apps which are able to send metadata to Zeitgeist. In some cases this functionality must be enabled manually.

*   [bijiben](https://www.archlinux.org/packages/?name=bijiben)
*   [gedit](https://www.archlinux.org/packages/?name=gedit)
*   [midori](https://www.archlinux.org/packages/?name=midori)
*   [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)
*   [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox)
*   [totem](https://www.archlinux.org/packages/?name=totem)
*   [zim](https://www.archlinux.org/packages/?name=zim)

[zeitgeist-datasources](https://aur.archlinux.org/packages/zeitgeist-datasources/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/zeitgeist-datasources)]</sup> can be also installed from the [AUR](/index.php/AUR "AUR"), which provides some third party plugins for other applcations.

### Applications

The following applications can be used to browse or search for recent activity using the Zeitgeist engine:

*   [cairo-dock-plug-ins](https://www.archlinux.org/packages/?name=cairo-dock-plug-ins)
*   [catfish](https://www.archlinux.org/packages/?name=catfish)
*   [gnome-activity-journal](https://www.archlinux.org/packages/?name=gnome-activity-journal)
*   [synapse](https://www.archlinux.org/packages/?name=synapse)
*   [unity](https://aur.archlinux.org/packages/unity/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/unity)]</sup>

For more information see [http://zeitgeist-project.com/experience/](http://zeitgeist-project.com/experience/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Zeitgeist&oldid=392871](https://wiki.archlinux.org/index.php?title=Zeitgeist&oldid=392871)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services")