[vpnc](https://www.unix-ag.uni-kl.de/~massar/vpnc/) is a VPN client for Cisco hardware VPNs.

## Installation

[Install](/index.php/Install "Install") the [vpnc](https://www.archlinux.org/packages/?name=vpnc) package.

## Configuration

The vpnc configuration files are in `/etc/vpnc`. It contains a `default.conf` file that you can copy and modify for your setup.

Executing `vpnc --long-help` will provide the names and descriptions of the various configuration options. For instance, in that output you will see

```
 --gateway <ip/hostname>
     IP/name of your IPSec gateway
 conf-variable: IPSec gateway<ip/hostname>

```

which translates into a line like this in your configuration file:

```
IPSec gateway gateway.example.com

```

## Starting

The `vpnc` package comes with a [systemd](/index.php/Systemd#Using_units "Systemd") unit `vpnc@.service`. If you want to use the configuration file `/etc/vpnc/client.conf`, you would start it with `systemctl start vpnc@client`.