[Syncthing](https://syncthing.net) is an open-source file synchronization client/server application, written in Go, implementing its own, equally free Block Exchange Protocol. All transit communications between syncthing nodes are encrypted, and all nodes are uniquely identified with cryptographic certificates.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Use Inotify](#Use_Inotify)
*   [4 Run a Relay](#Run_a_Relay)
*   [5 Troubleshooting](#Troubleshooting)

## Installation

Syncthing can be [installed](/index.php/Install "Install") with the [syncthing](https://www.archlinux.org/packages/?name=syncthing) or the [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) package. This latter includes additional features such as synchronization by inotify, desktop notifications and integration with Nautilus, Nemo and Caja.

After installing, you can either run the _syncthing_ binary manually from a terminal, or start it as a [systemd/User](/index.php/Systemd/User "Systemd/User") instance using the provided `syncthing.service`. Alternatively, you can [utilize](/index.php/Systemctl#Using_units "Systemctl") the `syncthing@.service` if you require it to run without an active user session.

The systemd services need to be started for a specific user in any case. To do this run `systemctl --user start syncthing.service` to start the service or `systemctl --user enable syncthing.service` to activate the service. See [Autostart-syncthing with systemd](http://docs.syncthing.net/users/autostart.html#using-systemd) for detailed information on the services.

When syncthing is started, a web interface will be provided by default on [localhost port 8384](http://localhost:8384). If you started syncthing manually, it should open the admin page in your browser.

**Note:** In syncthing releases before 0.11 (or when you have updated from 0.10) the web interface is available at port 8080\. Since port 8080 often conflicts with web development utilities [the default port has been changed to port 8384](https://github.com/syncthing/syncthing/commit/960c0cbddf8802ae440f2f9ae33bced4e2d72e44) ('ST' in ASCII). Custom port number can be configured under "GUI Listen Addresses" in the settings, configuration from versions prior to 0.11 were **not** adjusted automatically.

**Tip:** You can run multiple copies of syncthing, but only one instance per user as syncthing locks the database to it. Check logs for errors related to locked database.

## Configuration

After installation Syncthing already has a proper start-up configuration. You may now add new servers and/or folders by visiting the web interface. For detailed instructions on how to set up a simple network, read [Syncthing's getting started](http://docs.syncthing.net/intro/getting-started.html).

After a successful first start, it will create the default repository at `~/Sync`. You can see this in the web admin interface. On the right is the list of nodes you have added. On the left is the list of repositories, which are folders you can choose to share with other nodes.

To add another node, click "Add Node" underneath the list of nodes. You will be prompted for their Node ID (which can be found on the other machine by clicking `Edit > Show ID`) as well as a short name and the address. If you specify "dynamic" for the address, the syncthing announce server will be used to automatically exchange addresses between nodes. If you want to know more about Node IDs, including the cryptographic implications, you can read the appropriate [Syncthing documentation page](http://docs.syncthing.net/dev/device-ids.html).

After saving the configuration, you will be prompted to restart the syncthing server, and once restarted, the changes will be applied.

Next, you can either change the configuration of the default node (click its name and then `Edit`), or create a new one to share data with. Simply tick the node you wish to share the data with, and they will have permission to access it.

## Use Inotify

Inotify (inode notify) is a Linux kernel subsystem that acts to extend filesystems to notice changes to the filesystem, and report those changes to applications. Syncthing does not support Inotify yet but there is an official extension module which talks to the Syncthing REST API. The usage of Inotify avoids expensive rescans every minute. The rescan interval of each folder is automatically increased to avoid expensive, regular rescans. Syncthing-inotify can be installed with the [syncthing-inotify](https://www.archlinux.org/packages/?name=syncthing-inotify) package. If Syncthing is managed through systemd, it is ensured by systemd dependencies that `syncthing-inotify.service` is started and stopped automatically.

## Run a Relay

Since version 0.12 Syncthing has the ability to connect two devices via a relay when there exists no direct path between them. There is a default set of relays that is used out of the box. Relayed connections are encrypted in the usual manner, end to end, so the relay has no more insight into the connection than any other random eavesdropper on the internet [[1]](https://forum.syncthing.net/t/syncthing-v0-12-beryllium-bedbug-release-notes-v0-12-0-beta1/5480?u=rumpelsepp). To run a relay install [syncthing-relaysrv-git](https://aur.archlinux.org/packages/syncthing-relaysrv-git/) from AUR, then [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `syncthing-relaysrv.service` service.

More information about the [syncthing-relaysrv-git](https://aur.archlinux.org/packages/syncthing-relaysrv-git/) package are available in the [Syncthing forum](https://forum.syncthing.net/t/syncthing-relaysrv-for-arch-linux/5862u=rumpelsepp).

Per default the relay joins the [Syncthing relay pool](https://relays.syncthing.net/) and is publicy available. Rate limiting and other options can be configured via command line flags (check `syncthing-relaysrv -help`). To edit the command line flags just create a [drop-in snippet](/index.php/Systemd#Drop-in_snippets "Systemd") for `syncthing-relaysrv.service` and replace the `ExecStart` directive:

 `/etc/systemd/system/syncthing-relaysrv.service.d/override.conf` 

```
[Service]
ExecStart=
ExecStart=/usr/bin/syncthing-relaysrv FLAGS
```

A traffic statistics page is available at port 22070, e.g. [http://78.47.248.86:22070/status](http://78.47.248.86:22070/status).

## Troubleshooting

See [Debugging syncthing](http://docs.syncthing.net/dev/debugging.html).