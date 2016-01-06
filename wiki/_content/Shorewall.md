# Shorewall

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[The Shoreline Firewall](http://www.shorewall.net/), more commonly known as "Shorewall", is high-level tool for configuring Netfilter.

You describe your firewall/gateway requirements using entries in a set of configuration files. Shorewall reads those configuration files and with the help of the iptables utility, Shorewall configures Netfilter to match your requirements.

Shorewall can be used on a dedicated firewall system, a multi-function gateway/router/server or on a standalone GNU/Linux system. Shorewall does not use Netfilter's ipchains compatibility mode and can thus take advantage of Netfilter's connection state tracking capabilities.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 /etc/shorewall/interfaces](#.2Fetc.2Fshorewall.2Finterfaces)
    *   [2.2 /etc/shorewall/policy](#.2Fetc.2Fshorewall.2Fpolicy)
    *   [2.3 /etc/shorewall/rules](#.2Fetc.2Fshorewall.2Frules)
    *   [2.4 /etc/shorewall/masq](#.2Fetc.2Fshorewall.2Fmasq)
        *   [2.4.1 SSH](#SSH)
        *   [2.4.2 Port forwarding (DNAT)](#Port_forwarding_.28DNAT.29)
    *   [2.5 /etc/shorewall/shorewall.conf](#.2Fetc.2Fshorewall.2Fshorewall.conf)
*   [3 Start](#Start)

## Installation

[Install](/index.php/Install "Install") the [shorewall](https://www.archlinux.org/packages/?name=shorewall) package.

## Configuration

These settings are based on the [two-interface documentation on the Shorewall web site](http://www.shorewall.net/two-interface.htm).

Use some example configuration files that come with the shorewall package

```
# cp /usr/share/doc/shorewall/Samples/one-interface/* /etc/shorewall/     # If you have a desktop-type system with a single network interface
# cp /usr/share/doc/shorewall6/Samples6/one-interface/* /etc/shorewall6/  # If you have a desktop-type system with a single network interface, pkg shorewall6
# cp /usr/share/doc/shorewall/Samples/two-interfaces/* /etc/shorewall/    # If you have a router with two network interfaces
# cp /usr/share/doc/shorewall/Samples/three-interfaces/* /etc/shorewall/  # If you have a router with three network interfaces

```

### /etc/shorewall/interfaces

**Change** the interface settings to match the names used for our Ethernet devices and to allow DHCP traffic on the local network. Edit `/etc/shorewall/interfaces`

original

```
net     eth0          dhcp,tcpflags,nosmurfs,routefilter,logmartians
loc     eth1          tcpflags,nosmurfs,routefilter,logmartians

```

new

```
net     wan          dhcp,tcpflags,nosmurfs,routefilter,logmartians
loc     lan          dhcp,tcpflags,nosmurfs,routefilter,logmartians

```

### /etc/shorewall/policy

**Change** the policy file to allow the router (this machine) to access the Internet. Edit `/etc/shorewall/policy`

original

```
###############################################################################
#SOURCE         DEST            POLICY          LOG LEVEL       LIMIT:BURST

loc             net             ACCEPT
net             all             DROP            info
# THE FOLLOWING POLICY MUST BE LAST
all             all             REJECT          info

```

new

```
###############################################################################
#SOURCE         DEST            POLICY          LOG LEVEL       LIMIT:BURST
$FW             net             ACCEPT
loc             net             ACCEPT
net             all             DROP            info
# THE FOLLOWING POLICY MUST BE LAST
all             all             REJECT          info

```

### /etc/shorewall/rules

DNS look-ups are handled (actually forwarded) by dnsmasq, so Shorewall needs to allow those connections. **Add** these lines to `/etc/shorewall/rules`

```
#       Accept DNS connections from the local network to the firewall
#
DNS(ACCEPT)     loc              $FW

```

### /etc/shorewall/masq

**Change** the network interface to the one connected to your external (WAN) network and **change** the IP to the one used in your local network.

```
eth0        192.168.1.0/24

```

#### SSH

**OPTIONAL:** You can **add** these lines if you want to be able to SSH into the router from computers on the Internet

```
#       Accept SSH connections from the internet for administration
#
SSH(ACCEPT)     net             $FW         TCP      <SSH port used>

```

#### Port forwarding (DNAT)

*   /etc/shorewall/rules : here is an example for a webserver on our LAN with IP 10.0.0.85\. You can reach it on port 5000 of our "external" IP.

```
DNAT        net        loc:10.0.0.85:80        tcp        5000

```

### /etc/shorewall/shorewall.conf

When you are finished making above changes, enable shorewall by a **change** in it's config file `/etc/shorewall/shorewall.conf`:

original

```
STARTUP_ENABLED=No

```

new

```
STARTUP_ENABLED=Yes

```

See [man page](http://shorewall.net/manpages/shorewall.conf.html) for more info.

## Start

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `shorewall.service`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Shorewall&oldid=414461](https://wiki.archlinux.org/index.php?title=Shorewall&oldid=414461)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Firewalls](/index.php/Category:Firewalls "Category:Firewalls")