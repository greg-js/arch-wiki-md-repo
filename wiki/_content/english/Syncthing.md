Related articles

*   [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync")
*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")

[Syncthing](https://syncthing.net) is an open-source file synchronization client/server application, written in [Go](/index.php/Go "Go"), implementing its own, equally free [Block Exchange Protocol](https://docs.syncthing.net/specs/bep-v1.html). All transit communications between syncthing nodes are encrypted using [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security"), and all nodes are uniquely identified with cryptographic certificates.

## Contents

*   [1 Installation](#Installation)
*   [2 Running Syncthing](#Running_Syncthing)
    *   [2.1 Starting Syncthing](#Starting_Syncthing)
    *   [2.2 Autostarting Syncthing](#Autostarting_Syncthing)
        *   [2.2.1 System service](#System_service)
        *   [2.2.2 User service](#User_service)
    *   [2.3 Syncthing-GTK](#Syncthing-GTK)
    *   [2.4 Web-GUI](#Web-GUI)
*   [3 Configuration](#Configuration)
    *   [3.1 Local network setup](#Local_network_setup)
    *   [3.2 Using inotify](#Using_inotify)
*   [4 Participate in the infrastructure](#Participate_in_the_infrastructure)
    *   [4.1 Running a relay](#Running_a_relay)
    *   [4.2 Running a discovery server](#Running_a_discovery_server)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Stop journal spam](#Stop_journal_spam)
    *   [5.2 Run in VirtualBox](#Run_in_VirtualBox)
    *   [5.3 Running through a proxy](#Running_through_a_proxy)
*   [6 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the [syncthing](https://www.archlinux.org/packages/?name=syncthing) package.

Syncthing provides a [#Web-GUI](#Web-GUI) for control and monitoring. A GUI wrapper and notifier, [#Syncthing-GTK](#Syncthing-GTK) provided in a separate package also exists.

## Running Syncthing

### Starting Syncthing

Run the `syncthing` binary manually from a terminal. The multiple optional parameters are described in [syncthing(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/syncthing.1).

**Note:** You can run multiple copies of syncthing, but only one instance per user as syncthing locks the database to it. Check logs for errors related to locked database.

### Autostarting Syncthing

Syncthing can be installed as a [systemd](/index.php/Systemd "Systemd") system-wide service or as a [user service](/index.php/Systemd/User "Systemd/User") to run automatically at startup.

#### System service

Running Syncthing as a system service ensures that it is running at startup even if the user has no active session, it is intended to be used on a server. [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `syncthing@*myusername*.service` where *myusername* is the actual name of the Syncthing user.

#### User service

Running Syncthing as a [user service](/index.php/Systemd/User "Systemd/User") ensures that Syncthing only starts after the user has logged into the system (e.g., via the graphical login screen, or ssh). Thus, the user service is intended to be used on a (multiuser) desktop computer. To use the user service, [start/enable](/index.php/Start/enable "Start/enable") the user unit `syncthing.service` (i.e. with the `--user` flag).

**Tip:** It's also possible to run the sytemd-user service at boot (i.e. without logging in) using [Systemd/User#Automatic start-up of systemd user instances](/index.php/Systemd/User#Automatic_start-up_of_systemd_user_instances "Systemd/User").

### Syncthing-GTK

[syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) provides a [GTK+](/index.php/GTK%2B "GTK+") graphical user interface, desktop notifications and integration with the file managers [Nautilus](/index.php/Nautilus "Nautilus"), [Nemo](/index.php/Nemo "Nemo") and Caja. Syncthing can be launched by Syncthing-GTK: use the interface settings to run syncthing-gtk at startup, and to state whether to launch the syncthing daemon.

**Note:** When launching the syncthing daemon using both systemd and syncthing-gtk, it might happen that two syncthing instances run concurrently leading to high CPU consumption: one launched by syncthing-gtk, and the other (slightly later) by systemd. To solve this, either avoid launching synchting using systemd, or configure syncthing-gtk to wait for the syncthing daemon.

### Web-GUI

Syncthing provides a web interface accessible by default on [http://localhost:8384](http://localhost:8384).

**Tip:** To access the GUI remotely, see the [FAQ](https://docs.syncthing.net/users/faq.html#how-do-i-access-the-web-gui-from-another-computer).

## Configuration

After installation Syncthing already has a proper start-up configuration. You may now add new servers and/or folders by visiting the web interface. For detailed instructions on how to set up a simple network, read [Syncthing's getting started](http://docs.syncthing.net/intro/getting-started.html).

After a successful first start, it will create the default repository at `~/Sync`. You can see this in the web admin interface. On the right is the list of nodes you have added. On the left is the list of repositories, which are folders you can choose to share with other nodes.

To add another node, click "Add Node" underneath the list of nodes. You will be prompted for their Node ID (which can be found on the other machine by clicking `Edit > Show ID`) as well as a short name and the address. If you specify "dynamic" for the address, the syncthing announce server will be used to automatically exchange addresses between nodes. If you want to know more about Node IDs, including the cryptographic implications, you can read the appropriate [Syncthing documentation page](http://docs.syncthing.net/dev/device-ids.html).

After saving the configuration, you will be prompted to restart the syncthing server, and once restarted, the changes will be applied.

Next, you can either change the configuration of the default node (click its name and then `Edit`), or create a new one to share data with. Simply tick the node you wish to share the data with, and they will have permission to access it.

### Local network setup

In the typical case several machines, like laptops and androids, share a local area network *(LAN)* behind a network address translation *(NAT)* router, it is advised for a versatile configuration to:

*   Activate both local and global discovery on each node to allow discovery in all situations, including when a mobile device leaves the LAN and connects to the internet from the outside,

*   Use a different [listen address port](https://docs.syncthing.net/users/config.html#listen-addresses) for each machine, like `tcp://:22010`, `tcp://:22011`, `tcp://:22012` and so forth. This will differentiate them on the global discovery servers and avoid the *"Connected to myself - should not happen"* message on the other local devices whenever they leave the NAT.

*   Enable if possible [UPnP](https://en.wikipedia.org/wiki/universal_plug_and_play "wikipedia:universal plug and play") port forwarding or manually forward each port. When a new node is discovered, Syncthing tries to use its listening port. If this port happens to be closed, it will seek an open port locally: whenever *NAT traversal* is enabled in Syncthing, it will attempt to use UPnP to map a random external port to the internal listening port chosen, for example 22010\. If this is not desirable or not possible, each port should be manually forwarded to the right machine on the LAN. Eventually, if no open port can be found on both sides, [relaying](https://docs.syncthing.net/users/relaying.html) will be used.

### Using inotify

[inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") *(inode notify)* is a Linux kernel subsystem that acts to extend filesystems to notice changes to the filesystem, and report those changes to applications. The inotify functionality is integrated in Syncthing and can be enabled in the advanced configuration menu for individual folders. The setting is located at: *Actions* > *Advanced* > (click on the folder button you want) > *FS Watcher Enabled*. It is expected to be exposed in the folder configuration UI in the near future.

Alternatively, inotify support is provided by [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) but in this case inotify will only work while the GUI is running.

**Tip:** To prevent errors like *Too many open files*, increase the default `fs.inotify.max_user_watches` value, by [appending](/index.php/Append "Append") the following line: `/etc/sysctl.d/40-max-user-watches.conf`  `fs.inotify.max_user_watches=524288` 

## Participate in the infrastructure

One can participate in the [Syncthing infrastructure](https://docs.syncthing.net/dev/infrastructure.html) by running a global discovery server or a relay server.

### Running a relay

Syncthing has the ability to connect two devices via a [relay](https://docs.syncthing.net/users/relaying.html) when it is not possible to establish a direct connection between them. Relayed connections are end-to-end encrypted in the usual manner, so the relay has no insight into the connection other than the knowledge of the IP addresses and device IDs.

Anyone can run a [relay server](https://docs.syncthing.net/users/strelaysrv.html) and it will automatically join the [Syncthing relay pool](https://relays.syncthing.net/) and be available to all Syncthing's users. To run your own relay, [install](/index.php/Install "Install") [syncthing-relaysrv](https://www.archlinux.org/packages/?name=syncthing-relaysrv) and [Start/Enable](/index.php/Systemd#Using_units "Systemd") `syncthing-relaysrv.service`. Rate limiting and other options can be configured via the command line. These options can be set in the `ExecStart` directive of the service [drop-in file](/index.php/Systemd#Drop-in_files "Systemd") as follows:

 `/etc/systemd/system/syncthing-relaysrv.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/syncthing-relaysrv -global-rate 500000 -provided-by *relayprovidername*
```

**Note:** The relay listens by default to port *22067* for data and *22070* for service status (used for public statistics), they should therefore be open for TCP connections. The default ports can be respectively overridden with the `-listen` and `-status-srv` options if necessary.

**Tip:** The traffic statistics of a particular relay are accessible by default on port 22070, e.g. [http://108.28.183.249:22070/status](http://108.28.183.249:22070/status)

### Running a discovery server

[Global discovery](https://docs.syncthing.net/specs/globaldisco-v3.html) is used by Syncthing to find peers on the internet. Any device announces itself at startup to the discovery server which stores the device ID, IP address, port and current time. Then on request, for a given device ID, it returns the information stored in JSON format, for instance.

As an example, the request `[https://discovery-v4-2.syncthing.net/v2/?device=ITZRNXE-YNROGBZ-HXTH5P7-VK5NYE5-QHRQGE2-7JQ6VNJ-KZUEDIU-5PPR5AM](https://discovery-v4-2.syncthing.net/v2/?device=ITZRNXE-YNROGBZ-HXTH5P7-VK5NYE5-QHRQGE2-7JQ6VNJ-KZUEDIU-5PPR5AM)` returns `{"seen":"2017-12-06T14:04:39.005929Z","addresses":["tcp://212.129.18.55:22000"]}` .

Anyone can run a [discovery server](https://docs.syncthing.net/users/stdiscosrv.html), to run your own, [install](/index.php/Install "Install") the [syncthing-discosrv](https://aur.archlinux.org/packages/syncthing-discosrv/) package.

The discovery server requires certificates to run, which should ideally be placed in `/var/discosrv`. The user/group `syncthing` needs permissions to be able to read the certificate files. You need to edit the systemd unit file to correctly point to the certificates (and to undertake any other configuration change you may want, see [list](https://docs.syncthing.net/users/stdiscosrv.html#configuring)).

 `/usr/lib/systemd/system/syncthing-discosrv.service` 
```
[Unit]
Description=Syncthing discovery server
After=network.target

[Service]
User=syncthing
Group=syncthing
ExecStart=/usr/bin/syncthing-discosrv -db-dsn /var/discosrv/discosrv.db -cert /var/discosrv/cert.pem -key /var/discosrv/key.pem
Restart=on-failure
SuccessExitStatus=2

PrivateDevices=true
ProtectSystem=full
ProtectHome=true
NoNewPrivileges=true

[Install]
WantedBy=multi-user.target
```

To point the client to your discovery server, change the `Global Discovery Servers` variable under Settings to `https://yourserver:8443/` (default port) or whatever port you have reconfigured to. The variable takes a comma-separated list of discovery servers. It is possible to include multiple ones, including the default one.

If you are using self-signed certificates, the client refuses to connect unless you append the discovery server ID to its domain. The ID is printed to stdout upon launching the discovery server. Amend the *Global Discovery Servers* entry to add the ID: `https://yourserver.com:8443/?id=AAAAAAA-BBBBBBB-CCCCCCC-DDDDDDD-EEEEEEE-FFFFFFF-GGGGGGG-HHHHHHH`.

## Tips and tricks

### Stop journal spam

Syncthing can be quite noisy even while it is not doing anything. The service ExecStart can be overridden to filter output directly without an extra script (adjust "grep" as needed):

 `/etc/systemd/system/syncthing@.service.d/nospam.conf` 
```
[Service]
ExecStart=
ExecStart=/bin/bash -c 'set -o pipefail; /usr/bin/syncthing -no-browser -no-restart -logflags=0 | grep -v "INFO: "'
```

### Run in VirtualBox

It is possible to have Syncthing connect both locally and globally within a [VirtualBox](/index.php/VirtualBox "VirtualBox") virtual machine (VM) while keeping its network adapter in the [standard NAT](https://www.virtualbox.org/manual/ch06.html#network_nat) mode (as opposed to [bridged networking](https://www.virtualbox.org/manual/ch06.html#network_bridged) attached to the host computer's adapter).

To enable this mode, Syncthing should listen to a port in the VM different from the listening port already used by the host. For example, if the default 22000 port is used by the host, one could use 22001 in the VM. The listening port in the VM can be changed through Syncthing's [Sync Protocol Listen Addresses](https://docs.syncthing.net/users/config.html#listen-addresses) to `tcp://:22001` in the GUI *Settings*.

The 22001/TCP port of the host must be forwarded to the guest in this configuration. This can be done with the following command:

```
$ VBoxManage modifyvm *myvmname* --natpf1 "syncthing,tcp,,22001,,22001"

```

In this setup, relaying should not be necessary: local devices can connect to the VM on port 22001 while global devices are accessible as long as they have themselves an open port.

**Note:** local discovery in this setup is limited because the discovery listening port 21027 is already used by the host. The guest is therefore not able to build a table of local announcements though it can still broadcast to the local network via the VM NAT and announce itself. The steps described above allow to run a functioning server in the default NAT configuration but bridged networking is recommended for an optimal setup.

### Running through a proxy

Syncthing can be run through a proxy to enable use behind a corporate firewalls or tunneling via SSH. According to the [using proxies](https://docs.syncthing.net/users/proxying.html) documentation it is necessary to set the `all_proxy` environment variable, and it must indicate a *socks5* proxy type.

*   If the service is run from a script or from the command line, you must set the variables beforehand as follows:

```
export all_proxy="socks5://*proxy_address*:*proxy_port*"
export no_proxy="127.0.0.1"

```

*   If it is run as a service, you must define the variables in the service configuration file as follows:

 `/etc/systemd/system/multi-user.target.wants/syncthing@*myusername*.service` 
```
[Service]
Environment="all_proxy=socks5://*proxy_address*:*proxy_port*"
Environment="no_proxy=127.0.0.1"
```

You must then reload systemd daemons configurations:

```
# systemctl daemon-reload

```

and [restart](/index.php/Restart "Restart") the `syncthing@*myusername*.service`.

## Troubleshooting

See [Debugging Syncthing](http://docs.syncthing.net/dev/debugging.html).