[PeerGuardian Linux](http://sourceforge.net/projects/peerguardian/) (_pgl_) is a privacy oriented firewall application. It blocks connections to and from hosts specified in huge block lists (thousands or millions of IP ranges). _pgl_ is based on the Linux kernel [netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") framework and [iptables](/index.php/Iptables "Iptables").

A more native, efficient solution to achieve the same end is to use the [ipset](/index.php/Ipset "Ipset") kernel module in conjunction with the pg2ipset tool and the ipset-update script.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Server](#Server)
    *   [2.2 LAN](#LAN)
*   [3 Starting up](#Starting_up)
*   [4 Running pgl from within a container](#Running_pgl_from_within_a_container)

## Installation

There are two [AUR](/index.php/AUR "AUR") packages to choose from: [pgl-cli](https://aur.archlinux.org/packages/pgl-cli/) includes only the daemon and CLI tools, while [pgl](https://aur.archlinux.org/packages/pgl/) comes complete with a GUI (written using Qt).

## Configuration

*   `/etc/pgl/blocklists.list` contains a list of URL for retrieving the various block lists.
*   `/etc/pgl/pglcmd.conf`, empty by default, overrides the default settings present in `/usr/lib/pgl/pglcmd.defaults`.
*   `/etc/pgl/allow.p2p` lists custom IP ranges that will not be filtered.

The default lists in `/etc/pgl/blocklists.list` block many potentially legitimate IP address. Users are encouraged to exercise best judgment and the information available at [I-Blocklist](http://www.iblocklist.com/).

It is recommended to disable the filtering of HTTP connections by adding the following to `/etc/pgl/pglcmd.conf`:

 `/etc/pgl/pglcmd.conf`  `WHITE_TCP_OUT="http https"` 

Some program might not be able to reach the outside world. For instance, users of MSN for instant messaging, will need to add port 1863 to the white list:

 `/etc/pgl/pglcmd.conf`  `WHITE_TCP_OUT="http https msnp"` 

Conversely, one could white list all the ports except the ones used by the program to be blocked. The following example only use the block lists to stop incoming traffic on ports 53 (DNS) and 80 (HTTP):

 `/etc/pgl/pglcmd.conf` 

```
WHITE_TCP_IN="0:79 81:65535"
WHITE_UDP_IN="0:52 54:65535"
```

### Server

[systemd](/index.php/Systemd "Systemd") initialization of the system means that it's quite possible for a server to be briefly unprotected, prior to _pgl_ launch. To ensure adequate protection, create a service file named after the original server (i.e. `/etc/systemd/system/httpd.service` and paste the following:

 `/etc/systemd/system/httpd.service` 

```
.include /usr/lib/systemd/system/httpd.service

[Unit]
Wants=pgl.service
After=pgl.service
```

### LAN

By default, _pgl_ blocks traffic on the local IPv4 addresses. To disable this behavior, edit `/etc/pgl/pglcmd.conf` to add an exception using the _WHITE_IP_*_ setting:

 `/etc/pgl/pglcmd.conf`  `WHITE_IP_OUT="192.168.0.0/24"`  `/etc/pgl/pglcmd.conf`  `WHITE_IP_IN="192.168.0.0/24"` 

For further information, please refer to the `# Whitelist IPs #` section of `/usr/lib/pgl/pglcmd.defaults`.

## Starting up

Once comfortable with the configuration of both the daemon and lists, start the `pgl` [service](/index.php/Daemon "Daemon"). To make sure that _pgl_ works as intended, issue this command:

```
# pglcmd test

```

To start _pgl_ automatically at boot, enable the `pgl` service.

## Running pgl from within a container

Users running pgl within a [Linux Container](/index.php/Linux_Container "Linux Container") may need to modify the package included `lxc@.service` to include the loading of key modules needed by pgl.

 `/etc/systemd/system/lxc@.service` 

```
[Unit]
Description=%i LXC
After=network.target

[Service]
Type=forking
ExecStartPre=/usr/bin/modprobe -a xt_NFQUEUE xt_mark xt_iprange
ExecStart=/usr/bin/lxc-start -d -n %i
ExecStop=/usr/bin/lxc-stop -n %i
Delegate=true

[Install]
WantedBy=multi-user.target

```