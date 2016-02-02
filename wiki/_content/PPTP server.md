# PPTP server

[Point-to-Point Tunneling Protocol](https://en.wikipedia.org/wiki/PPTP "wikipedia:PPTP") (PPTP) is a method for implementing virtual private networks. PPTP uses a control channel over TCP and a GRE tunnel operating to encapsulate PPP packets.

This entry will show you on how to create a PPTP server in Arch.

**Warning:** The PPTP protocol is inherently insecure. See [http://poptop.sourceforge.net/dox/protocol-security.phtml](http://poptop.sourceforge.net/dox/protocol-security.phtml) for details.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 iptables firewall configuration](#iptables_firewall_configuration)
    *   [2.2 UFW firewall configuration](#UFW_firewall_configuration)
*   [3 Start the server](#Start_the_server)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Error 619 on the client side](#Error_619_on_the_client_side)
    *   [4.2 pptpd[xxxxx]: Long config file line ignored](#pptpd.5Bxxxxx.5D:_Long_config_file_line_ignored)
    *   [4.3 ppp0: ppp: compressor dropped pkt](#ppp0:_ppp:_compressor_dropped_pkt)

## Installation

[Install](/index.php/Install "Install") the [pptpd](https://www.archlinux.org/packages/?name=pptpd) package.

## Configuration

**Tip:** Configuration examples can be found in the `/usr/share/doc/pptpd` directory.

A typical configuration may look like:

 `/etc/pptpd.conf` 

```
# See man pptpd.conf to get more information about this file

# pppd options file. By default, /etc/ppp/options is used
option /etc/ppp/options.pptpd

# Server IP in local network
localip 192.168.1.2

# IP address ranges used to assign IPs to new connecting clients
# Here we define two ranges for our 192.168.1.* subnet: 234-238 and 245
remoteip 192.168.1.234-238,192.168.1.245

```

Now create the pppd options file, in our example this is `/etc/ppp/options.pptpd`:

 `/etc/ppp/options.pptpd` 

```
# Read man pppd to see the full list of available options

# The name of the local system for authentication purposes
name pptpd

# Refuse PAP, CHAP or MS-CHAP connections but accept connections with
# MS-CHAPv2 or MPPE with 128-bit encryption
refuse-pap
refuse-chap
refuse-mschap
require-mschap-v2
require-mppe-128

# Add entry to the ARP system table
proxyarp

# For the serial device to ensure exclusive access to the device
lock

# Disable BSD-Compress and Van Jacobson TCP/IP header compression
nobsdcomp
novj
novjccomp

# Disable file logging
nolog

# DNS servers for Microsoft Windows clients. Using Google's public servers here
ms-dns 8.8.8.8
ms-dns 8.8.4.4

```

**Note:** Ensure that empty line at the end of the file exists to prevent possible parsing issues.

Now create credentials file for authenticating users:

 `/etc/ppp/chap-secrets` 

```
# <username> <server name> <password> <ip addresses>
user2    pptpd    123    *

```

Now you can be authenticated with _user2_ as username and _123_ for password.

Create a sysctl configuration file `/etc/sysctl.d/30-ipforward.conf` and enable kernel packet forwarding that allow connecting clients to have access to your subnet (see also [Internet Share#Enable packet forwarding](/index.php/Internet_Share#Enable_packet_forwarding "Internet Share")):

 `/etc/sysctl.d/30-ipforward.conf`  `net.ipv4.ip_forward=1` 

Now apply changes to let the sysctl configuration take effect:

```
# sysctl --system

```

### iptables firewall configuration

Configure your iptables settings to enable access for PPTP Clients

```
# Accept all packets via ppp* interfaces (for example, ppp0)
iptables -A INPUT -i ppp+ -j ACCEPT
iptables -A OUTPUT -o ppp+ -j ACCEPT

# Accept incoming connections to port 1723 (PPTP)
iptables -A INPUT -p tcp --dport 1723 -j ACCEPT

# Accept GRE packets
iptables -A INPUT -p 47 -j ACCEPT
iptables -A OUTPUT -p 47 -j ACCEPT

# Enable IP forwarding
iptables -F FORWARD
iptables -A FORWARD -j ACCEPT

# Enable NAT for eth0 и ppp* interfaces
iptables -A POSTROUTING -t nat -o eth0 -j MASQUERADE
iptables -A POSTROUTING -t nat -o ppp+ -j MASQUERADE

```

**Note:** Ensure that "eth0" is replaced with the actual ethernet interface connected to the server.

Now save the new iptables rules with:

```
# iptables-save > /etc/iptables/iptables.rules

```

Read [Iptables](/index.php/Iptables "Iptables") for more information.

### UFW firewall configuration

Configure your ufw settings to enable access for PPTP Clients.

You must change default forward policy in `/etc/default/ufw`

 `/etc/default/ufw`  `DEFAULT_FORWARD_POLICY="ACCEPT"` 

Now change `/etc/ufw/before.rules`, add following code after header and before *filter line

 `/etc/ufw/before.rules` 

```
# nat Table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Allow traffic from clients to eth0
-A POSTROUTING -s 172.16.36.0/24 -o eth0 -j MASQUERADE

# commit to apply changes
COMMIT

```

Open pptp port 1723

```
ufw allow 1723

```

Restart ufw for good measure

```
ufw disable
ufw enable

```

## Start the server

Now you can [start and enable](/index.php/Systemd#Using_units "Systemd") your PPTP Server using `pptpd.service`.

## Troubleshooting

As with any service, see [Systemd#Troubleshooting](/index.php/Systemd#Troubleshooting "Systemd") to investigate errors.

### Error 619 on the client side

Search for the `logwtmp` option in `/etc/pptpd.conf` and comment it out. When this is enabled, _wtmp_ will be used to record client connections and disconnections.

```
#logwtmp

```

### pptpd[xxxxx]: Long config file line ignored

Add a blank line at the end of `/etc/pptpd.conf`. [[1]](http://sourceforge.net/p/poptop/bugs/35/)

### ppp0: ppp: compressor dropped pkt

If you have this error while a client is connected to the server, add the following script to `/etc/ppp/ip-up.d/mppefixmtu.sh`:

```
#!/bin/sh
CURRENT_MTU="`ip link show $1 | grep -Po '(?<=mtu )([0-9]+)'`"
FIXED_MTU="`expr $CURRENT_MTU + 4`"
ip link set $1 mtu $FIXED_MTU

```

Make the script executable:

```
# chmod 755 /etc/ppp/ip-up.d/mppefixmtu.sh

```

See also: [[2]](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=330973)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PPTP_server&oldid=408921](https://wiki.archlinux.org/index.php?title=PPTP_server&oldid=408921)"