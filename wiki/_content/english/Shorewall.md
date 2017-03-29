[The Shoreline Firewall](http://www.shorewall.net/), more commonly known as "Shorewall", is a high-level tool for configuring Netfilter.

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
    *   [2.5 /etc/shorewall/stoppedrules](#.2Fetc.2Fshorewall.2Fstoppedrules)
    *   [2.6 /etc/shorewall/shorewall.conf](#.2Fetc.2Fshorewall.2Fshorewall.conf)
*   [3 Start](#Start)
*   [4 Traffic shaping](#Traffic_shaping)

## Installation

[Install](/index.php/Install "Install") the [shorewall](https://www.archlinux.org/packages/?name=shorewall) or [shorewall6](https://www.archlinux.org/packages/?name=shorewall6) package.

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

**Note:**

As of version 5.0.14, /etc/shorewall/masq has been deprecated in favor of /etc/shorewall/snat. Add the following line to /etc/shorewall/snat instead of modifying masq.

```
MASQUERADE        192.168.1.0/24        eth0

```

**Change** the network interface to the one connected to your external (WAN) network and **change** the IP to the one used in your local network.

```
eth0        192.168.1.0/24

```

#### SSH

**OPTIONAL:** You can **add** these lines to /etc/shorewall/rules if you want to be able to SSH into the router from computers on the Internet

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

### /etc/shorewall/stoppedrules

If you have a network name other than eth1 for the network interface in /etc/shorewall/interfaces, you need to update stoppedrules with the correct name.

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

## Traffic shaping

Read [Shorewall's Traffic Shaping/Control](http://www.shorewall.net/traffic_shaping.htm) guide.

Here is my config as an example:

*   /etc/shorewall/tcdevices : here is where you define the interface you want to have shaped and its rates. I have got a ADSL connection with a 4MBit down/256KBit up profile.

```
ppp0        4mbit        256kbit 

```

*   /etc/shorewall/tcclasses : here you define the minimum (rate) and maximum (ceil) throughput per class. You will assign each one to a type of traffic to shape.

```
# interactive traffic (ssh)
ppp0            1       full    full    0
# online gaming
ppp0            2       full/2  full    5
# http
ppp0            3       full/4  full    10
# rest
ppp0            4       full/6  full    15              default

```

*   /etc/shorewall/tcrules : this file contains the types of traffic and the class it belongs to.

```
1       0.0.0.0/0       0.0.0.0/0       tcp     ssh
2       0.0.0.0/0       0.0.0.0/0       udp     27000:28000
3       0.0.0.0/0       0.0.0.0/0       tcp     http
3       0.0.0.0/0       0.0.0.0/0       tcp     https

```

I have split it up my traffic in 4 groups:

1.  interactive traffic or ssh: although it takes up almost no bandwidth, it is very annoying if it lags due to leechers on the LAN. This gets the highest priority.
2.  online gaming: needless to say you cannot play when your ping sucks. ;)
3.  webtraffic: can be a bit slower
4.  everything else: every sort of download, they are the cause of the lag anyway.