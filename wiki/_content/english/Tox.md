From the project [home page](https://tox.chat/): "Tox is a distributed, secure messenger with audio and video chat capabilities."

## Installation

In order to use Tox, you should [install](/index.php/Install "Install") a [Tox client](https://wiki.tox.chat/clients):

*   **qTox** — Powerful Tox client written in QT

	[https://wiki.tox.chat/clients/qtox](https://wiki.tox.chat/clients/qtox) || [qtox](https://www.archlinux.org/packages/?name=qtox)

*   **Toxic** — ncurses-based CLI

	[https://wiki.tox.chat/clients/toxic](https://wiki.tox.chat/clients/toxic) || [toxic](https://www.archlinux.org/packages/?name=toxic)

*   **gTox** — GTK3-Style Tox-Client

	[https://github.com/KoKuToru/gTox/](https://github.com/KoKuToru/gTox/) || [gtox-git](https://aur.archlinux.org/packages/gtox-git/)

*   **µTox (uTox)** — Lightweight Tox client

	[https://github.com/uTox/uTox](https://github.com/uTox/uTox) || [utox-git](https://aur.archlinux.org/packages/utox-git/)

*   **Ratox** — FIFO based client

	[http://ratox.2f30.org/](http://ratox.2f30.org/) || [ratox-git](https://aur.archlinux.org/packages/ratox-git/)

*   **qTox** — Powerful Tox client written in QT, current Github Version

	[https://wiki.tox.chat/clients/qtox](https://wiki.tox.chat/clients/qtox) || [qtox-git](https://aur.archlinux.org/packages/qtox-git/)

*   **Ricin** — Lightweight and fully-Hackable Tox client powered by Vala & Gtk3

	[https://ricin.im/](https://ricin.im/) || [ricin-git](https://aur.archlinux.org/packages/ricin-git/)

*   **Tox Pidgin Protocol Plugin** — a plugin for Pidgin which allows the use of the Tox protocol within Pidgin

	[http://tox.dhs.org/](http://tox.dhs.org/) || [tox-prpl-git](https://aur.archlinux.org/packages/tox-prpl-git/)

## Run a node

To be able to connect to others, Tox needs to connect to a [DHT node](https://wiki.tox.chat/users/nodes) first. All DHT nodes are connected to each other, and since everyone is connected to at least one DHT node, you can connect to others one way or the other.

Install [toxcore](https://www.archlinux.org/packages/?name=toxcore). The package creates user 'tox-bootstrapd' and includes a systemd unit file in /usr/lib/systemd/system/tox-bootstrapd.service and a configuration file in /etc/tox-bootstrapd.conf.

Edit the configuration file and add appropriate nodes from [Tox wiki](https://wiki.tox.chat/users/nodes) or [Node status page](https://nodes.tox.chat/).

[Enable](/index.php/Enable "Enable") and start tox-bootstrapd.service, and check if it is running fine and port has been bound:

 `# ss --listening --numeric --processes | grep *node_port*`  `udp        0      0 *:*node_port*                 *:*                                 576/DHT_bootstrap`