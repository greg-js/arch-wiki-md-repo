[Zeitgeist](http://zeitgeist-project.com/) is a service which logs user activities and events, anywhere from files opened to websites visited or conversations held via email and more. It makes this information readily available for other applications to use in the form of timelines and statistics. See the [Wikipedia article](https://en.wikipedia.org/wiki/Zeitgeist_(framework) for a more detailed description of Zeitgeist itself.

## Installation

Install [zeitgeist](https://www.archlinux.org/packages/?name=zeitgeist) from the [official repositories](/index.php/Official_repositories "Official repositories"), which includes the daemon and the datahub. The daemon receives metadata from data sources, and provides them to applications using D-Bus. The datahub provides passive plugins which insert events into Zeitgeist.

To configure what gets logged by Zeitgeist, install [activity-log-manager](https://www.archlinux.org/packages/?name=activity-log-manager) which provides a graphical user interface where you can filter out specific folders, file types, and applications. The GNOME Control Center also has a Privacy module where you can make similar adjustments.

To monitor and inspect Zeitgeist's log at a low level, install [zeitgeist-explorer](https://www.archlinux.org/packages/?name=zeitgeist-explorer) which provides a graphical user interface where you can see the events logged in real-time just like wireshark.

### Data providers

The following applications are just some of the apps which are able to send metadata to Zeitgeist. In some cases this functionality must be enabled manually.

*   [midori](https://www.archlinux.org/packages/?name=midori)
*   [noise-player](https://www.archlinux.org/packages/?name=noise-player)
*   [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files)
*   [scratch-text-editor](https://www.archlinux.org/packages/?name=scratch-text-editor)
*   [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)
*   [zim](https://www.archlinux.org/packages/?name=zim)

### Applications

The following applications can be used to browse or search for recent activity using the Zeitgeist engine:

*   [cairo-dock-plug-ins](https://www.archlinux.org/packages/?name=cairo-dock-plug-ins)
*   [catfish](https://www.archlinux.org/packages/?name=catfish)
*   [gnome-activity-journal](https://www.archlinux.org/packages/?name=gnome-activity-journal)
*   [synapse](https://www.archlinux.org/packages/?name=synapse)

For more information see [http://zeitgeist-project.com/experience/](http://zeitgeist-project.com/experience/)