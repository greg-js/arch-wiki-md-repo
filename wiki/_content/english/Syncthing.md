Related articles

*   [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync")
*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")

[Syncthing](https://syncthing.net) is an open-source file synchronization client/server application, written in [Go](/index.php/Go "Go"), implementing its own, equally free [Block Exchange Protocol](https://docs.syncthing.net/specs/bep-v1.html). All transit communications between syncthing nodes are encrypted, and all nodes are uniquely identified with cryptographic certificates.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Syncthing](#Starting_Syncthing)
    *   [2.1 Run Syncthing](#Run_Syncthing)
    *   [2.2 System service](#System_service)
    *   [2.3 User service](#User_service)
    *   [2.4 Syncthing-GTK](#Syncthing-GTK)
*   [3 Accessing the web-interface](#Accessing_the_web-interface)
*   [4 Configuration](#Configuration)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Use inotify](#Use_inotify)
    *   [5.2 Run a Relay](#Run_a_Relay)
    *   [5.3 Stop journal spam](#Stop_journal_spam)
    *   [5.4 Discovery Server](#Discovery_Server)
    *   [5.5 Run in VirtualBox](#Run_in_VirtualBox)
*   [6 Troubleshooting](#Troubleshooting)

## Installation

Syncthing can be [installed](/index.php/Install "Install") with the [syncthing](https://www.archlinux.org/packages/?name=syncthing) package.

Synchronization by *inotify* can be added with either the [syncthing-inotify](https://www.archlinux.org/packages/?name=syncthing-inotify) or the [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) package, see [#Use inotify](#Use_inotify) for caveats. *syncthing-gtk* also provides a GTK interface, [desktop notifications](/index.php/Desktop_notifications "Desktop notifications") and integration with [Nautilus](/index.php/Nautilus "Nautilus"), [Nemo](/index.php/Nemo "Nemo") and Caja.

## Starting Syncthing

### Run Syncthing

Run the `syncthing` binary manually from a terminal.

**Note:** You can run multiple copies of syncthing, but only one instance per user as syncthing locks the database to it. Check logs for errors related to locked database.

### System service

Running Syncthing as a system service ensures that it is running at startup even if the user has no active session, it is intended to be used on a server.

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `syncthing@*myuser*.service` where *myuser* is the actual name of your user.

### User service

Running Syncthing as a [user service](/index.php/Systemd/User "Systemd/User") ensures that Syncthing only starts after the user has logged into the system (e.g., via the graphical login screen, or ssh). Thus, the user service is intended to be used on a (multiuser) desktop computer. To use the user service, [start/enable](/index.php/Start/enable "Start/enable") the user unit `syncthing.service` (i.e. with the `--user` flag).

The systemd services need to be started for a specific user in any case, see [Autostart-syncthing with systemd](http://docs.syncthing.net/users/autostart.html#using-systemd) for detailed information on the services.

### Syncthing-GTK

Syncthing can also be launched by [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk). Use interface UI settings to start [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) at startup, and to state whether to launch the syncthing daemon.

When launching the syncthing daemon using both systemd and [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk), it might happen that two syncthing instances run concurrently leading to high CPU consumption: one launched by syncthing-gtk, and the other (slightly later) by systemd. To solve this, either avoid launching synchting using systemd, or configure syncthing-gtk to wait for the syncthing daemon.

## Accessing the web-interface

When Syncthing is started, a web interface will be provided by default on [http://localhost:8384](http://localhost:8384).

**Tip:** To access the configuration GUI remotely, see the [FAQ](https://docs.syncthing.net/users/faq.html#how-do-i-access-the-web-gui-from-another-computer).

## Configuration

After installation Syncthing already has a proper start-up configuration. You may now add new servers and/or folders by visiting the web interface. For detailed instructions on how to set up a simple network, read [Syncthing's getting started](http://docs.syncthing.net/intro/getting-started.html).

After a successful first start, it will create the default repository at `~/Sync`. You can see this in the web admin interface. On the right is the list of nodes you have added. On the left is the list of repositories, which are folders you can choose to share with other nodes.

To add another node, click "Add Node" underneath the list of nodes. You will be prompted for their Node ID (which can be found on the other machine by clicking `Edit > Show ID`) as well as a short name and the address. If you specify "dynamic" for the address, the syncthing announce server will be used to automatically exchange addresses between nodes. If you want to know more about Node IDs, including the cryptographic implications, you can read the appropriate [Syncthing documentation page](http://docs.syncthing.net/dev/device-ids.html).

After saving the configuration, you will be prompted to restart the syncthing server, and once restarted, the changes will be applied.

Next, you can either change the configuration of the default node (click its name and then `Edit`), or create a new one to share data with. Simply tick the node you wish to share the data with, and they will have permission to access it.

## Tips and tricks

### Use inotify

**Note:** There is no need to [enable](/index.php/Enable "Enable") the `syncthing-inotify` service when using the `syncthing` service.

[Inotify](https://en.wikipedia.org/wiki/Inotify "w:Inotify") (inode notify) is a Linux kernel subsystem that acts to extend filesystems to notice changes to the filesystem, and report those changes to applications. Syncthing does not support *inotify* yet but there is an official extension module which talks to the Syncthing REST API. The usage of *inotify* avoids expensive rescans every minute. The *inotify* extension can be installed with the [syncthing-inotify](https://www.archlinux.org/packages/?name=syncthing-inotify) package. [Restart](/index.php/Restart "Restart") the `syncthing` [service](/index.php?title=Service&action=edit&redlink=1 "Service (page does not exist)") for changes to take effect.

Alternatively, *inotify* support is provided by [syncthing-gtk](https://www.archlinux.org/packages/?name=syncthing-gtk) (which does not depend on [syncthing-inotify](https://www.archlinux.org/packages/?name=syncthing-inotify)) but in this case *inotify* will only work while the GUI is running.

Increase the default `fs.inotify.max_user_watches` value to prevent errors like *Too many open files*, by [appending](/index.php/Append "Append") the following line:

 `/etc/sysctl.d/40-max-user-watches.conf`  `fs.inotify.max_user_watches=524288` 

### Run a Relay

Syncthing has the ability to connect two devices via a [relay](https://docs.syncthing.net/users/relaying.html) when it is not possible to establish a direct connection between them. Relayed connections are end-to-end encrypted in the usual manner, so the relay has no insight into the connection other than the knowledge of the IP addresses and device IDs.

Anyone can run a [relay server](https://docs.syncthing.net/users/strelaysrv.html) and it will automatically join the [Syncthing relay pool](https://relays.syncthing.net/) and be available to all Syncthing's users. To run your own relay, [install](/index.php/Install "Install") [syncthing-relaysrv](https://www.archlinux.org/packages/?name=syncthing-relaysrv) and [Start/Enable](/index.php/Systemd#Using_units "Systemd") `syncthing-relaysrv.service`. Rate limiting and other options can be configured via the command line. These options can be set in the `ExecStart` directive of the service [drop-in file](/index.php/Systemd#Drop-in_files "Systemd") as follows:

 `/etc/systemd/system/syncthing-relaysrv.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/syncthing-relaysrv -global-rate 500000 -provided-by relayprovidername
```

**Note:** The relay listens by default to port 22067 for data and 22070 for service status (used for public statistics). They can be respectively overridden with the `-listen` and `-status-srv` options. These ports should therefore be open for TCP connections.

**Tip:** The traffic statistics of a particular relay are accessible by default on port 22070, e.g. [http://108.28.183.249:22070/status](http://108.28.183.249:22070/status)

### Stop journal spam

Syncthing can be quite noisy even while it isn't doing anything. The service ExecStart can be overridden like this to filter output directly without an extra script (adjust "grep" as needed):

 `/etc/systemd/system/syncthing@.service.d/nospam.conf` 
```
[Service]
ExecStart=
ExecStart=/bin/bash -c 'set -o pipefail; /usr/bin/syncthing -no-browser -no-restart -logflags=0 | grep -v "INFO: "'
```

### Discovery Server

The Syncthing Discovery Server is available in the AUR under [syncthing-discosrv](https://aur.archlinux.org/packages/syncthing-discosrv/). The official documentation is provided [here](https://docs.syncthing.net/users/stdiscosrv.html).

Note that the discovery server requires certificates to run, which should ideally be placed in `/var/discosrv`. The user/group `syncthing` needs permissions to be able to read the certificate files. You need to edit the systemd unit file to correctly point to the certificates (and to undertake any other configuration change you may want, see [list](https://docs.syncthing.net/users/stdiscosrv.html#configuring)).

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

To point the client to your discovery server, change the `Global Discovery Servers` variable under Settings to `https://yourserver:8443/` (default port) or whatever port you have reconfigured to. The variable takes a comma-separated list of discovery servers. It is possible to include multiple ones, including the default one.

If you are using self-signed certificates, the client refuses to connect unless you append the discovery server ID to its domain. The ID is printed to stdout upon launching the discovery server. Amend the *Global Discovery Servers* entry to add the ID: `https://yourserver.com:8443/?id=AAAAAAA-BBBBBBB-CCCCCCC-DDDDDDD-EEEEEEE-FFFFFFF-GGGGGGG-HHHHHHH`.

### Run in VirtualBox

It is possible to have Syncthing connect both locally and globally within a [VirtualBox](/index.php/VirtualBox "VirtualBox") virtual machine keeping its network adapter in the standard [NAT](https://www.virtualbox.org/manual/ch06.html#network_nat) mode (as opposed to [bridged networking](https://www.virtualbox.org/manual/ch06.html#network_bridged) attached to the host computer's adapter).

To achieve this, Syncthing should use a port in the VM different from the port it uses on the host. If the default 22000 port is used by the host for listening, one could use 22001 in the VM. This is carried out by setting Syncthing's [Sync Protocol Listen Addresses](https://docs.syncthing.net/users/config.html#listen-addresses) to `tcp://:22001` in the VM and by opening the corresponding port of the virtual machine: the 22001/TCP host's port should be forwarded to the guest's same port:

 `$ VBoxManage modifyvm myvmname --natpf1 "syncthing,tcp,,22001,,22001"` 

In this setup, relaying should not be necessary: local devices will connect to the VM on port 22001 while global devices should be accessible as long as they have an open port.

## Troubleshooting

See [Debugging Syncthing](http://docs.syncthing.net/dev/debugging.html).