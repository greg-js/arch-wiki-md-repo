# Deluge

Related articles

*   [rTorrent](/index.php/RTorrent "RTorrent")
*   [systemd](/index.php/Systemd "Systemd")
*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [iptables](/index.php/Iptables "Iptables")
*   [OpenSSL](/index.php/OpenSSL "OpenSSL")

[Deluge](http://deluge-torrent.org/) is a lightweight but full-featured BitTorrent application written in Python 2\. It has a variety of features, including but not limited to: a client/server model, DHT support, magnet links, a plugin system, UPnP support, full-stream encryption, proxy support, and three different client applications. When the server daemon is running, users can connect to it via a console client, a GTK+-based GUI, or a Web-based UI. A full list of features can be viewed [here](http://dev.deluge-torrent.org/wiki/About).

## Contents

*   [1 Installation](#Installation)
*   [2 Daemon setup](#Daemon_setup)
    *   [2.1 System service](#System_service)
    *   [2.2 User service](#User_service)
*   [3 Configuration](#Configuration)
    *   [3.1 Firewall](#Firewall)
*   [4 Clients](#Clients)
    *   [4.1 Console](#Console)
    *   [4.2 GTK+](#GTK.2B)
    *   [4.3 Web](#Web)
        *   [4.3.1 System service](#System_service_2)
        *   [4.3.2 User service](#User_service_2)
        *   [4.3.3 Setup](#Setup)
*   [5 Headless setup](#Headless_setup)
    *   [5.1 Create a user](#Create_a_user)
    *   [5.2 Allow remote](#Allow_remote)
    *   [5.3 Firewall](#Firewall_2)
    *   [5.4 Connect](#Connect)
        *   [5.4.1 SSH Tunnel](#SSH_Tunnel)
*   [6 See Also](#See_Also)

## Installation

[deluge](https://www.archlinux.org/packages/?name=deluge) is available. Due to changes in twisted, [python2-service-identity](https://www.archlinux.org/packages/?name=python2-service-identity) is optionally needed. Without it, users may experience a lengthy warning and have their client reject many valid certificate/hostname mappings.

The GTK+ UI requires additional dependencies as does the Web UI. Inspect the pacman output to determine which are right for the intended application:

```
[python2-notify](https://www.archlinux.org/packages/?name=python2-notify): libnotify notifications
[pygtk](https://www.archlinux.org/packages/?name=pygtk): needed for gtk ui
[librsvg](https://www.archlinux.org/packages/?name=librsvg): needed for gtk ui
[python2-mako](https://www.archlinux.org/packages/?name=python2-mako): needed for web ui

```

## Daemon setup

**Warning:** If multiple users are running a daemon, the default port (58846) will need to be changed for each user.

Deluge comes with a daemon called `deluged`. If it is not running when one of the clients is run, it will be started. It is useful, however, to have it started with systemd to allow torrents to run without starting a client and/or Xorg. This can be accomplished in one of two ways: a system service or a user service.

### System service

A system service will allow `deluged` to run at boot without the need to start Xorg or a client. Deluge comes with a system service called `deluged.service`, which can be [started](/index.php/Start "Start") and enabled without change, which will run the deluge daemon as the **deluge** user, which is created by the package. To run the daemon as another user, copy `/usr/lib/systemd/system/deluged.service` to `/etc/systemd/system/deluged.service` and change the User parameter within the file, such as the **torrent** user:

```
User=**torrent**

```

In that case, create a user called **torrent**.

### User service

A user service will allow `deluged` to run when `systemd --user` is started. This is accomplished by creating a user service file:

 `/etc/systemd/user/deluged.service` 

```
[Unit]
Description=Deluge Daemon
After=network.target

[Service]
ExecStart=/usr/bin/deluged -d -P %h/.config/deluge/deluge.pid

[Install]
WantedBy=default.target

```

The deluge user service can now be [started](/index.php/Start "Start") and enabled by the user.

The `deluged` user service can also be placed in `$HOME/.config/systemd/user/`. See [systemd/User](/index.php/Systemd/User "Systemd/User") for more information on user services.

## Configuration

Deluge can be configured through any of the clients as well as by simply editing the JSON-formatted configuration files located in `$HOME/.config/deluge/`. **$HOME** refers to the home directory of the user that `deluged` is running as. This means that if the daemon is running as the **deluge** user, the default home directory is `/srv/deluge/`.

### Firewall

Deluge requires at least one port open for TCP and UDP to allow incoming connections for seeding. If deluge complaining that it cannot open a port for incoming connections, users must open port(s) to be used. In this example, ports 56881 through 56889 are opened for TCP and UDP:

```
# iptables -A INPUT -p tcp --dport 56881:56889 -j ACCEPT
# iptables -A INPUT -p udp --dport 56881:56889 -j ACCEPT

```

User who are behind a NAT router/firewall must setup the corresponding ports to be forwarded. UPnP may also be used, but that will not work with the local firewall on the system because it requires predefined ports.

**Note:** One can limit this to a single port, just be sure to enable both TCP and UDP.

On many default configurations, when using iptables with connection tracking (conntrack) set to drop "INVALID" packets, sometimes a great deal of legitimate torrent traffic (especially DHT traffic) is dropped as "invalid." This is typically caused by either conntrack's memory restrictions, or from long periods between packets among peers (see [[1]](http://libtorrent.rakshasa.no/wiki/RTorrentUsingDHT) towards the bottom and [[2]](http://www.linuxquestions.org/questions/showthread.php?p=5145026)). Symptoms of this problem include torrents not seeding, especially when the torrent client has been active for more than a day or two continuously, and consistently low overhead traffic (in one experience, less than 3KiB/s in either in or out) with DHT enabled, even when deluge/libtorrent has been continuously running for more than forty-eight hours and many torrents are active. For this reason, it may be necessary to disable connection tracking of all torrent traffic for optimal performance, even with the listening ports set to ACCEPT (as the causes for dropping INVALID packets, for instance conntrack's memory problems, may supercede any rules to accept traffic to/from those ports).

To fully turn off connection tracking for torrents, specify ports for both Incoming and Outgoing traffic in Deluge, for instance, 56881-56889 for incoming connections and 56890-57200 for outgoing connections.

**Note:** Limiting incoming connections is not recommended with libtorrent as this will limit the ability to keep multiple connections to the same client, even for different torrents.

Then issue the following commands (after substituting the relevant port ranges):

```
# iptables -t raw -I PREROUTING -p udp --dport 56881:57200 -j NOTRACK
# iptables -t raw -I OUTPUT -p udp --sport 56881:57200 -j NOTRACK
# iptables -t raw -I PREROUTING -p tcp --dport 56881:57200 -j NOTRACK
# iptables -t raw -I OUTPUT -p tcp --sport 56881:57200 -j NOTRACK
# iptables -I INPUT -p icmp --icmp-type 3 -j ACCEPT
# iptables -I INPUT -p icmp --icmp-type 4 -j ACCEPT
# iptables -I INPUT -p icmp --icmp-type 11 -j ACCEPT
# iptables -I INPUT -p icmp --icmp-type 12 -j ACCEPT

```

The ICMP allowances are desirable because once connection tracking is disabled on those ports, those important ICMP messages (types 3 (Destination Unreachable), 4 (Source Quench), 11 (Time Exceeded) and 12 (Parameter Problem)) would otherwise be declared INVALID themselves (as netfilter would not know of any connections that they are associated with), and they would potentially be blocked.

**Warning:** A port range of 1024:65535 would break every DNS query.

## Clients

### Console

The console client can be run with:

```
$ deluge-console

```

Enter the `help` command for a list of available commands.

### GTK+

**Note:** It is wise to disable Classic Mode in _Edit -> Preferences -> Interface_ for daemon (server) setups.

The GTK+ client can be run with:

```
$ deluge-gtk

```

or:

```
$ deluge

```

The GTK+ client has a number of useful plugins:

*   AutoAdd - Monitors directories for .torrent files
*   Blocklist - Downloads and imports an IP blocklist
*   Execute - Event-based command execution
*   Extractor - Extracts archived files upon completion _**(beware of random high disk I/O usage)**_
*   Label - Allows labels to be assigned to torrents, as well as state, tracker, and keyword filters
*   Notifications - Provides notifications (email, pop-up, blink, sound) for events as well as other plugins
*   Scheduler - Limits active torrents and their speed on a per-hour, per-day basis
*   WebUi - Allows the Web UI to be started via the GTK+ client

### Web

**Note:** It is recommended that you use https for the Web client.

**Warning:**

*   If multiple users are running a daemon, the default port (8112) will need to be changed for each user.
*   The deluge Web client comes with a default password. See the Setup section.

The Web UI can be started by running `deluge-web`, through a plugin in the GTK+ UI, or via systemd. It has many of the same features of the GTK+ UI, including the plugin system.

#### System service

Deluge comes with a system service file called `deluge-web.service`. The process for this is the same as starting `deluged.service`, except with `deluge-web` instead of `deluged`. This service will also run as the **deluge** user unless the service file is modified in the same way as `deluged.service`.

#### User service

A user service will allow `deluge-web` to run when `systemd --user` is started. This is accomplished by creating a user service file:

 `/etc/systemd/user/deluge-web.service` 

```
[Unit]
Description=Deluge Web UI
After=deluged.service

[Service]
ExecStart=/usr/bin/deluge-web --ssl

[Install]
WantedBy=default.target

```

The deluge user service can now be [started](/index.php/Start "Start") and enabled by the user.

The `deluge-web` user service can also be placed in `$HOME/.config/systemd/user/`. See [systemd/User](/index.php/Systemd/User "Systemd/User") for more information on user services.

#### Setup

When `deluge-web` is initially started, it will create `$HOME/.config/deluge/web.conf`. The password in this file is hashed with SHA1 and salted. The default password is "deluge".

Users may be greeted by a warning from the browser that the SSL certificate is untrusted. Add an exception to this in the browser to continue on. See the [OpenSSL](/index.php/OpenSSL "OpenSSL") page for information on creating your own certificate.

## Headless setup

Deluge is quite useful on a headless system, often referred to as a seed box, because of its client/server model. To set up deluge on a headless system, set up the daemon as shown above.

### Create a user

To allow interaction with the server remotely, create a user in `$HOME/.config/deluge/auth`. For example:

```
$ echo "delugeuser:p422WoRd:10" >> $HOME/.config/deluge/auth

```

**Note:**

*   The user/password created does not have to match any system users, and to maintain good security practices it should **not**!
*   The user/password in this file are not hashed or salted like in the web client config.
*   The user/password must match the user/password found in /srv/deluge/.config/deluge/auth otherwise the authentication fails.

The number **10** corresponds to a level of **Admin**. Refer to the following table for additional values:

| Level Name | Level Value |
| None | 0 |
| Read Only | 1 |
| Normal | 5 |
| Admin | 10 |

**Note:** In Deluge 1.35, these values have no effect, but multiuser options are under development.

### Allow remote

The default settings disallow remote connections. Change the "allow_remote" setting in `$HOME/.config/deluge/core.conf`:

```
"allow_remote": true,

```

### Firewall

Open the port for remote access. The following example uses the default daemon port (58846):

```
# iptables -A INPUT -p tcp --dport 58846 -j ACCEPT

```

See [iptables](/index.php/Iptables "Iptables") for more information on firewall rules.

Users behind a NAT router/firewall must forward the port to access the daemon from outside the network if this behavior is desired.

### Connect

In the console client:

```
connect <host>[:<port>] <user> <password>

```

In the GTK+ client, _Edit > Connection Manager > Add_.

In the Web client, _Connection Manager > Add_.

#### SSH Tunnel

An SSH tunnel can be created to use an encrypted connection on any client. This requires an extra loopback address to be added, but this can be automated at boot. Without this step, the connection would be considered local. The actual command to establish an SSH tunnel cannot be automated as it requires user input. There are a few possible ways to go about doing that.

 `/etc/systemd/system/extra_lo_addr.service` 

```
[Unit]
Description=extra loopback address
Wants=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/sbin/ip addr add 127.0.0.2/8 dev lo
ExecStop=/sbin/ip addr del 127.0.0.2/8 dev lo

[Install]
WantedBy=multi-user.target

```

```
$ ssh -fNL 127.0.0.2:58846:localhost:58846 <ssh host>

```

The port **58846** should be replaced with the port the deluge server is running on and **<ssh host>** should be replaced with the server hosting both deluge and the SSH server.

## See Also

*   [Deluge homepage](http://deluge-torrent.org/)
*   [Deluge wiki](http://dev.deluge-torrent.org/wiki)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Deluge&oldid=418593](https://wiki.archlinux.org/index.php?title=Deluge&oldid=418593)"