[Transmission](http://www.transmissionbt.com/) is a light-weight and cross-platform BitTorrent client. It is the default BitTorrent client in many Linux distributions.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuring the GUI version](#Configuring_the_GUI_version)
    *   [2.1 GTK+ temporary cosmetic fix](#GTK.2B_temporary_cosmetic_fix)
*   [3 Transmission daemon and CLI](#Transmission_daemon_and_CLI)
    *   [3.1 Starting and stopping the daemon](#Starting_and_stopping_the_daemon)
    *   [3.2 Run only while connected to network](#Run_only_while_connected_to_network)
        *   [3.2.1 Netctl](#Netctl)
        *   [3.2.2 Wicd](#Wicd)
    *   [3.3 Choosing a user](#Choosing_a_user)
    *   [3.4 Configuring the daemon](#Configuring_the_daemon)
        *   [3.4.1 Watch dir](#Watch_dir)
        *   [3.4.2 CLI Examples](#CLI_Examples)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Cannot access the daemon over the network](#Cannot_access_the_daemon_over_the_network)
    *   [4.2 UDP Failed to set receive/sent buffer](#UDP_Failed_to_set_receive.2Fsent_buffer)
*   [5 See also](#See_also)

## Installation

There are several options in [official repositories](/index.php/Official_repositories "Official repositories"):

*   [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) - daemon, with [CLI](https://en.wikipedia.org/wiki/Command-line_interface "wikipedia:Command-line interface"), and web client ([http://localhost:9091](http://localhost:9091)) interfaces.
*   [transmission-remote-cli](https://www.archlinux.org/packages/?name=transmission-remote-cli) - Curses interface for the daemon.
*   [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) - GTK3 package.
*   [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt) - Qt5 package.

**Note:**

*   The GTK client cannot connect to the daemon, so users wishing to use the daemon will need to consider using the Qt package for a GUI or the remote-cli package for a curses-based GUI.
*   You cannot connect to the daemon over IPv6.[[1]](https://trac.transmissionbt.com/ticket/2236)

## Configuring the GUI version

Both GUI versions, *transmission-gtk* and *transmission-qt*, can function autonomously without a formal back-end daemon.

GUI versions are configured to work out-of-the-box, but the user may wish to change some of the settings. The default path to the GUI configuration files is `~/.config/transmission`.

A guide to configuration options can be found on the Transmission web site: [https://trac.transmissionbt.com/wiki/EditConfigFiles#Options](https://trac.transmissionbt.com/wiki/EditConfigFiles#Options).

### GTK+ temporary cosmetic fix

With GTK+ 3.18, transmission-gtk shows black borders in random places; these can be hidden via `gtk.css`:

 `~/.config/gtk-3.0/gtk.css` 
```
.tr-workarea .overshoot,
.tr-workarea .undershoot { border: none; }

```

## Transmission daemon and CLI

The commands for *transmission-cli* are:

	*transmission-daemon*: starts the daemon.

	*transmission-remote*: invokes the [CLI](https://en.wikipedia.org/wiki/Command-line_interface "wikipedia:Command-line interface") for the daemon, whether local or remote, followed by the command you want the daemon to execute.

	*transmission-remote-cli*: (requires [transmission-remote-cli](https://www.archlinux.org/packages/?name=transmission-remote-cli)) starts the [curses](https://en.wikipedia.org/wiki/curses_(programming_library) interface for the daemon, whether local or remote.

	*transmission-cli*: (deprecated) starts a non-daemonized local instance of *transmission*, for manually downloading a torrent.

	*transmission-show*: returns information on a given torrent file.

	*transmission-create*: creates a new torrent.

	*transmission-edit*: add, delete, or replace a tracker's announce URL.

### Starting and stopping the daemon

As explained in [#Choosing a user](#Choosing_a_user), the transmission daemon can be run:

*   As the user *transmission*, by starting/enabling `transmission.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

	you can change the user as explained in [#Choosing a user](#Choosing_a_user)

*   As your own user, by running under your user name: `$ transmission-daemon` The daemon can then be stopped with: `$ killall transmission-daemon` 

Starting the daemon will create an initial *transmission* configuration file. See [#Configuring the daemon](#Configuring_the_daemon).

An alternative option to stop transmission is to use the *transmission-remote* command:

```
$ transmission-remote --exit

```

### Run only while connected to network

#### Netctl

It may only be desirable to run transmission on certain networks. The following script checks that the connection is to a list of authorized networks and then proceeds to launch transmission-daemon.

 `/etc/netctl/hooks/90-transmission.sh` 
```
#!/bin/bash

# The SSIDs for which we enable this.
declare -A ssids=(
    ["network_1"]=y
    ["network_2"]=y
)

if [[ ${ssids[$SSID]} ]]; then
    case $ACTION in
        CONNECT|REESTABLISHED)
            # Need to wait, otherwise doesn't seem to bind to 9091.
            sleep 30
            systemctl start transmission
            ;;
        *)
            systemctl stop transmission
            ;;
    esac
fi

```

#### Wicd

Create a [start script](#Starting_and_stopping_the_daemon) in folder `/etc/wicd/scripts/postconnect`, and a [stop script](#Starting_and_stopping_the_daemon) in folder `/etc/wicd/scripts/predisconnect`. Remember to make them executable. For example:

 `/etc/wicd/scripts/postconnect/transmission` 
```
#!/bin/bash

systemctl start transmission
```
 `/etc/wicd/scripts/predisconnect/transmission` 
```
#!/bin/bash

systemctl stop transmission
```

### Choosing a user

Choose how you want to run `transmission`:

*   As a separate user, `transmission` by default (recommended for increased security).

By default, *transmission* creates a user and a group `transmission`, with its home files at `/var/lib/transmission/`, and runs as this "user". This is a security precaution, so *transmission*, and its downloads, have no access to files outside of `/var/lib/transmission/`. Configuration, operation, and access to downloads needs to be done with "root" privileges (e.g. by using [sudo](/index.php/Sudo "Sudo")).

*   Under the user's own user name.

To set this up, [override](/index.php/Systemd#Editing_provided_units "Systemd") the provided service file and specify your username:

 `/etc/systemd/system/transmission.service.d/username.conf` 
```
[Service]
User=*your_username*
```

### Configuring the daemon

Create an initial configuration file by [starting the daemon](#Starting_and_stopping_the_daemon).

*   If running Transmission under the username `transmission`, the configuration file will be located at `/var/lib/transmission/.config/transmission-daemon/settings.json`.

*   If running Transmission under your own username, the configuration file will be located at `~/.config/transmission-daemon/settings.json`.

One can customize the daemon by using a Transmission client or using the included web interface accessible via [http://localhost:9091](http://localhost:9091) in a supported browser.

A guide to configuration options can be found on the Transmission web site: [https://trac.transmissionbt.com/wiki/EditConfigFiles#Options](https://trac.transmissionbt.com/wiki/EditConfigFiles#Options)

**Note:** If you want to edit the configuration manually using a text editor, [stop the daemon](#Starting_and_stopping_the_daemon) first; otherwise, it would overwrite its configuration file when it closes.

**Note:** Alternatively, the daemon can be instructed to reload its configuration with SIGHUP, by running `kill -s SIGHUP `pidof transmission-daemon``.

A recommendation for those running under username `transmission` is to create a shared download directory with the correct permissions to allow access to both the `transmission` user and system users, and then to update the configuration file accordingly. For example:

```
# mkdir /mnt/data/torrents
# chown -R facade:transmission /mnt/data/torrents
# chmod -R 775 /mnt/data/torrents

```

Now `/mnt/data/torrents` will be accessible for the system user `facade` and for the `transmission` group to which the `transmission` user belongs. Making the target directory world read/writable is highly discouraged (i.e. do not *chmod* the directory to *777*). Instead, give individual users/groups appropriate permissions to the appropriate directories.

**Note:** If `/mnt/data/torrents` is located on a removable device, e.g. with an `/etc/fstab` entry with the option `nofail`, Transmission will complain that it cannot find your files. To remedy this, you can add `RequiresMountsFor=/mnt/data/torrents` to `/etc/systemd/system/transmission.service.d/transmission.conf` in the section `[Unit]`.

An alternative is to add your user to the `transmission` group (`#usermod -a -G transmission yourusername`) and then modify the permissions on the `/var/lib/transmission` and `/var/lib/transmission/Downloads` directories to allow `rwx` access by members of the `transmission` group.

#### Watch dir

If you want to *Automatically add .torrent files from a folder*, but you find that the `watch-dir` and `watch-dir-enabled` options set in the config file do not work, you can start the transmission daemon with the flag `-c /path/to/watch/dir`.

If you're using systemd, edit the `transmission.service` unit as described in [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd").

#### CLI Examples

If you want to remove all finished torrents you can use the following command with your own username and password

```
# transmission-remote -n 'username:password' -l | grep 100% | awk '{print $1}'| paste -d, -s | xargs -i transmission-remote -t {} -r

```

## Troubleshooting

#### Cannot access the daemon over the network

The daemon is started after `network.service` was initialised. However, if you enable the service `dhcpcd` as opposed to the device-specific service, such as `dhcpcd@enp1s0.service` for example, it may happen that Transmission is started too early and cannot bind to the network interface. Thus, the web interface is unreachable. A possible solution is to add the `Requires` line to the unit's [configuration file](/index.php/Systemd#Editing_provided_units "Systemd"):

 `/etc/systemd/system/transmission.service.d/fixdep.conf` 
```
[Unit]
Requires=network.target
```

### UDP Failed to set receive/sent buffer

The error messages `UDP Failed to set receive buffer` and `UDP Failed to set sent buffer` mean that Transmission would like a bigger sent and receive buffer. These buffers can be changed by adding the following file:

 `/etc/sysctl.d/60-net_buffer.conf` 
```

net.core.rmem_max = 16777216
net.core.wmem_max = 4194304

```

To load the new configuration run `# sysctl --system` and then reload Transmission.

## See also

*   [Transmission wiki](https://trac.transmissionbt.com/wiki)
*   [HeadlessUsage](https://trac.transmissionbt.com/wiki/HeadlessUsage/General)