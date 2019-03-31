[Zeitgeist](https://launchpad.net/zeitgeist-project) is a service which logs user activities and events, anywhere from files opened to websites visited or conversations held via email and more. It makes this information readily available for other applications to use in the form of timelines and statistics. See the [Wikipedia article](https://en.wikipedia.org/wiki/Zeitgeist_(framework) for a more detailed description of Zeitgeist itself.

## Installation

[Install](/index.php/Install "Install") [zeitgeist](https://www.archlinux.org/packages/?name=zeitgeist) from the [official repositories](/index.php/Official_repositories "Official repositories"), which includes the daemon and the datahub. The daemon receives metadata from data sources, and provides them to applications using D-Bus. The datahub provides passive plugins which insert events into Zeitgeist.

To configure what gets logged by Zeitgeist, install [activity-log-manager](https://www.archlinux.org/packages/?name=activity-log-manager) which provides a graphical user interface where you can filter out specific folders, file types, and applications.

To monitor and inspect Zeitgeist's log at a low level, install [zeitgeist-explorer](https://www.archlinux.org/packages/?name=zeitgeist-explorer) which provides a graphical user interface where you can see the events logged in real-time just like Wireshark.

### Data providers

The following applications are just some of the apps which are able to send metadata to Zeitgeist. In some cases this functionality must be enabled manually.

*   [Midori](/index.php/Midori "Midori")
*   [pantheon-code](https://www.archlinux.org/packages/?name=pantheon-code)
*   [pantheon-files](https://www.archlinux.org/packages/?name=pantheon-files)
*   [pantheon-music](https://www.archlinux.org/packages/?name=pantheon-music)
*   [Zim](/index.php/Zim "Zim")

### Applications

The following applications can be used to browse or search for recent activity using the Zeitgeist engine:

*   **Catfish** — Versatile file searching tool.

	[https://docs.xfce.org/apps/catfish/start](https://docs.xfce.org/apps/catfish/start) || [catfish](https://www.archlinux.org/packages/?name=catfish)

*   **GNOME Activity Journal** — Browse a chronological log of your activities and easily find files, contacts, etc.

	[https://launchpad.net/gnome-activity-journal](https://launchpad.net/gnome-activity-journal) || [gnome-activity-journal](https://aur.archlinux.org/packages/gnome-activity-journal/)

*   **Recent Events applet (Cairo-Dock plugin)** — Applet for [Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock") using Zeitgeist.

	[http://www.glx-dock.org/](http://www.glx-dock.org/) || [cairo-dock-plug-ins](https://www.archlinux.org/packages/?name=cairo-dock-plug-ins)

*   **Synapse** — Semantic launcher written in Vala that you can use to start applications as well as find and access relevant documents and files by making use of the Zeitgeist engine.

	[https://launchpad.net/synapse-project](https://launchpad.net/synapse-project) || [synapse](https://www.archlinux.org/packages/?name=synapse)