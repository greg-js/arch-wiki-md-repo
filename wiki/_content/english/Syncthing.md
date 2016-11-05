[Syncthing](https://syncthing.net) is an open-source file synchronization client/server application, written in Go, implementing its own, equally free Block Exchange Protocol. All transit communications between syncthing nodes are encrypted, and all nodes are uniquely identified with cryptographic certificates.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Syncthing](#Starting_Syncthing)
    *   [2.1 Run binary](#Run_binary)
    *   [2.2 System service](#System_service)
    *   [2.3 User service](#User_service)
*   [3 Accessing the web-interface](#Accessing_the_web-interface)
*   [4 Configuration](#Configuration)
*   [5 Use Inotify](#Use_Inotify)
    *   [5.1 Custom Settings](#Custom_Settings)
*   [6 Run a Relay](#Run_a_Relay)
*   [7 Stop journal spam](#Stop_journal_spam)
*   [8 Discovery Server](#Discovery_Server)
*   [9 Troubleshooting](#Troubleshooting)

## Installation

Syncthing can be [installed](/index.php/Install "Install") with the [syncthing](https://www.archlinux.org/packages/?name=syncthing) or the [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) package. This latter includes additional features such as synchronization by inotify, desktop notifications and integration with Nautilus, Nemo and Caja.

After installing, you can [start Syncthing](#Starting_Syncthing).

## Starting Syncthing

**Tip:** You can run multiple copies of syncthing, but only one instance per user as syncthing locks the database to it. Check logs for errors related to locked database.

### Run binary

Run the `syncthing` binary manually from a terminal.

### System service

Running Syncthing as a system service ensures that it is running at startup even if the user has no active session, it is intended to be used on a server.

Enable and start the service. Replace *myuser* with the actual Syncthing user after the @:

```
# systemctl enable syncthing@myuser.service
# systemctl start syncthing@myuser.service 

```

### User service

Running Syncthing as a [user service](/index.php/Systemd/User "Systemd/User") ensures that Syncthing only starts after the user has logged into the system (e.g., via the graphical login screen, or ssh). Thus, the user service is intended to be used on a (multiuser) desktop computer. It avoids unnecessarily running Syncthing instances. Run this provided `syncthing.service`:

```
$ systemctl --user enable syncthing.service
$ systemctl --user start syncthing.service

```

The systemd services need to be started for a specific user in any case, see [Autostart-syncthing with systemd](http://docs.syncthing.net/users/autostart.html#using-systemd) for detailed information on the services.

## Accessing the web-interface

**Tip:** Syncthing can only be accessed on the running computer. Change `<address>127.0.0.1:8384</address>` in `~/.config/syncthing/config.xml` to `<address>0.0.0.0:8384</address>` and restart the [systemd](/index.php/Systemd "Systemd") service to allow access from another computer.

When Syncthing is started, a web interface will be provided by default on [localhost port 8384](http://localhost:8384). If you started syncthing manually, it should open the admin page in your browser.

**Note:** In syncthing releases before 0.11 (or when you have updated from 0.10) the web interface is available at port 8080\. Since port 8080 often conflicts with web development utilities [the default port has been changed to port 8384](https://github.com/syncthing/syncthing/commit/960c0cbddf8802ae440f2f9ae33bced4e2d72e44) ('ST' in ASCII). Custom port number can be configured under "GUI Listen Addresses" in the settings, configuration from versions prior to 0.11 were **not** adjusted automatically.

## Configuration

After installation Syncthing already has a proper start-up configuration. You may now add new servers and/or folders by visiting the web interface. For detailed instructions on how to set up a simple network, read [Syncthing's getting started](http://docs.syncthing.net/intro/getting-started.html).

After a successful first start, it will create the default repository at `~/Sync`. You can see this in the web admin interface. On the right is the list of nodes you have added. On the left is the list of repositories, which are folders you can choose to share with other nodes.

To add another node, click "Add Node" underneath the list of nodes. You will be prompted for their Node ID (which can be found on the other machine by clicking `Edit > Show ID`) as well as a short name and the address. If you specify "dynamic" for the address, the syncthing announce server will be used to automatically exchange addresses between nodes. If you want to know more about Node IDs, including the cryptographic implications, you can read the appropriate [Syncthing documentation page](http://docs.syncthing.net/dev/device-ids.html).

After saving the configuration, you will be prompted to restart the syncthing server, and once restarted, the changes will be applied.

Next, you can either change the configuration of the default node (click its name and then `Edit`), or create a new one to share data with. Simply tick the node you wish to share the data with, and they will have permission to access it.

## Use Inotify

Inotify (inode notify) is a Linux kernel subsystem that acts to extend filesystems to notice changes to the filesystem, and report those changes to applications. Syncthing does not support Inotify yet but there is an official extension module which talks to the Syncthing REST API. The usage of Inotify avoids expensive rescans every minute. The rescan interval of each folder is automatically increased to avoid expensive, regular rescans. Syncthing-inotify can be installed with the [syncthing-inotify](https://www.archlinux.org/packages/?name=syncthing-inotify) package. If Syncthing is managed through systemd, it is ensured by systemd dependencies that `syncthing-inotify.service` is started and stopped automatically.

### Custom Settings

Run `$ syncthing-inotify -help` for available options, such as setting the API key.

To set options for syncthing-inotify service, create a `.conf` file in `/etc/systemd/user/syncthing-inotify.service.d/` (When running as [#User service](#User_service)) and/or `/etc/systemd/system/syncthing-inotify@**user**.service.d/` ([#System service](#System_service)), e.g.:

 `/etc/systemd/user/syncthing-inotify.service.d/start.conf` 
```
[Unit]
ExecStart=
ExecStart=/usr/bin/syncthing-inotify -logflags=0 -api="0M6ubcgtcy7KBLucu0jeXrgqB8U7YKp9"
RuntimeDirectory=syncthing-inotify
```

## Run a Relay

Since version 0.12 Syncthing has the ability to connect two devices via a relay when there exists no direct path between them. There is a default set of relays that is used out of the box. Relayed connections are encrypted in the usual manner, end to end, so the relay has no more insight into the connection than any other random eavesdropper on the internet [[1]](https://forum.syncthing.net/t/syncthing-v0-12-beryllium-bedbug-release-notes-v0-12-0-beta1/5480?u=rumpelsepp). To run a relay install [syncthing-relaysrv](https://www.archlinux.org/packages/?name=syncthing-relaysrv), then [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `syncthing-relaysrv.service` service.

There is also a git version in the [AUR](/index.php/AUR "AUR"). More information about the [syncthing-relaysrv-git](https://aur.archlinux.org/packages/syncthing-relaysrv-git/) package are available in the [Syncthing forum](https://forum.syncthing.net/t/syncthing-relaysrv-for-arch-linux/5862).

Per default the relay joins the [Syncthing relay pool](https://relays.syncthing.net/) and is publicy available. Rate limiting and other options can be configured via command line flags (check `syncthing-relaysrv -help`). To edit the command line flags just create a [drop-in snippet](/index.php/Systemd#Drop-in_files "Systemd") for `syncthing-relaysrv.service` and replace the `ExecStart` directive:

 `/etc/systemd/system/syncthing-relaysrv.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/syncthing-relaysrv FLAGS
```

A traffic statistics page is available at port 22070, e.g. [http://78.47.248.86:22070/status](http://78.47.248.86:22070/status).

## Stop journal spam

Syncthing can be quite noise even while it isn't doing anything. The service ExecStart can be overridden like this to filter output directly without an extra script (adjust "grep" as needed):

 `/etc/systemd/system/syncthing@.service.d/nospam.conf` 
```
[Service]
ExecStart=
ExecStart=/bin/bash -c 'set -o pipefail; /usr/bin/syncthing -no-browser -no-restart -logflags=0 | grep -v "INFO: "'
```

## Discovery Server

The Syncthing Discovery Server is available in the AUR under [syncthing-discosrv](https://aur.archlinux.org/packages/syncthing-discosrv/). Documentation is provided [here](https://docs.syncthing.net/users/discosrv.html).

Note, that the discovery server requires certificates to run, which should ideally be placed in `/var/discosrv`, and the user/group `syncthing` needs permissions to able to read the certificate files. Currently, you will need to edit the systemd unit file to correctly point to the certificates (as well as any other configuration changes you want to undertake, see [list](https://docs.syncthing.net/users/discosrv.html#configuring)).

 `/usr/lib/systemd/system/syncthing-discosrv.service` 
```
[Unit]
Description=Syncthing discovery server
After=network.target

[Service]
User=syncthing
Group=syncthing
ExecStart=/bin/sh -c "/usr/bin/syncthing-discosrv -db-dsn='file:///var/discosrv/discosrv.db' -cert /var/discosrv/chain.pem -key /var/discosrv/key.pem"
Restart=on-failure
SuccessExitStatus=2

PrivateDevices=true
ProtectSystem=full
ProtectHome=true
NoNewPrivileges=true

[Install]
WantedBy=multi-user.target
```

To point the client at your discovery server, change the `Global Discovery Servers` variable under Settings, to point to `https://yourserver:8443/` (default port) or whatever port you have reconfigured to. The variable takes a comma-seperated list of discovery servers, it is possible to include multiple ones, including the default one.

If you are using self-signed certificates, the client will refuse to connect unless you append the discovery server ID to its domain. The ID is printed to stdout upon launching the discovery server. Amend the Global Discovery Servers entry to add the ID: `https://yourserver.com:8443/?id=AAAAAAA-BBBBBBB-CCCCCCC-DDDDDDD-EEEEEEE-FFFFFFF-GGGGGGG-HHHHHHH`.

## Troubleshooting

See [Debugging syncthing](http://docs.syncthing.net/dev/debugging.html).