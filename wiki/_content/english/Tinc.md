This article describes a basic installation and configuration of tinc. For further details see the [tinc.conf man page](http://www.tinc-vpn.org/documentation/tinc.conf.5) and the [tinc documentation](http://tinc-vpn.org/docs/).

***tinc** is a Virtual Private Network (VPN) daemon that uses tunnelling and encryption to create a secure private network between hosts on the Internet.*[[1]](http://tinc-vpn.org/)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuring a private network](#Configuring_a_private_network)
    *   [2.1 Configuration of alpha](#Configuration_of_alpha)
    *   [2.2 Configuration of beta](#Configuration_of_beta)
    *   [2.3 Setting up the hosts](#Setting_up_the_hosts)
*   [3 Starting a private network](#Starting_a_private_network)
*   [4 Using TAP devices and bridges](#Using_TAP_devices_and_bridges)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 I've updated my system and now tinc won't start.](#I.27ve_updated_my_system_and_now_tinc_won.27t_start.)
    *   [5.2 I'm running a custom kernel and tinc won't start.](#I.27m_running_a_custom_kernel_and_tinc_won.27t_start.)

## Installation

[Install](/index.php/Install "Install") [tinc](https://www.archlinux.org/packages/?name=tinc) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuring a private network

In this example, we will create a virtual private network *vpnname* between two hosts *alpha* and *beta*, where the former is the entry point for the latter, so that beta tries to connect to alpha on startup.

For each virtual private network you have to create a separate directory in /etc/tinc, e.g.

```
# mkdir /etc/tinc/*vpnname*

```

You can also start by copying the sample configuration

```
# cp -r /usr/share/tinc/examples/sample-config/* /etc/tinc/*vpnname*

```

In /etc/tinc/*vpnname*/tinc.conf you specify the name of the hostmachine (which can differ from the actual hostname of the system) and the location of the tun/tap device.

### Configuration of alpha

/etc/tinc/*vpnname*/tinc.conf

```
Name = alpha
Device = /dev/net/tun

```

/etc/tinc/*vpnname*/tinc-up

```
#!/bin/sh
ip link set $INTERFACE up
ip addr add  192.168.0.1/32 dev $INTERFACE
ip route add 192.168.0.0/24 dev $INTERFACE

```

/etc/tinc/*vpnname*/tinc-down

```
#!/bin/sh
ip route del 192.168.0.0/24 dev $INTERFACE
ip addr del 192.168.0.1/32 dev $INTERFACE
ip link set $INTERFACE down

```

### Configuration of beta

/etc/tinc/*vpnname*/tinc.conf

```
Name = beta
Device = /dev/net/tun
ConnectTo = alpha

```

/etc/tinc/*vpnname*/tinc-up

```
#!/bin/sh
ip link set $INTERFACE up
ip addr add 192.168.0.2/32 dev $INTERFACE
ip route add 192.168.0.0/24 dev $INTERFACE

```

/etc/tinc/*vpnname*/tinc-down

```
#!/bin/sh
ip route del 192.168.0.0/24 dev $INTERFACE
ip addr del 192.168.0.2/32 dev $INTERFACE
ip link set $INTERFACE down

```

### Setting up the hosts

The configuration files for the different hosts are stored in /etc/tinc/*vpnname*/hosts/ directory. In this example we need the two files on each machine.

/etc/tinc/*vpnname*/hosts/alpha

```
Address = 10.0.0.1
Port = 655
Subnet = 192.168.0.1/32

```

/etc/tinc/*vpnname*/hosts/beta

```
Port = 655
Subnet = 192.168.0.2/32

```

After creating a file for each host, you have to generate a key pair using

```
# tincd -n *vpnname* -K

```

which creates the private key in /etc/tinc/*vpnname*/tinc.rsa_key.priv and the public key in the corresponding host-file.

In the last step you need to exchange the host configuration files, so that you have both alpha and beta in /etc/tinc/*vpnname*/hosts/ on each host.

## Starting a private network

After having created the appropriate configuration in /etc/tinc/*vpnname*, you can test the the new private network with

```
# tincd -n *vpnname*

```

If you want to enable it at startup you have to enable the appropriate service

```
# systemctl enable tinc@*vpnname*

```

## Using TAP devices and bridges

Sometimes it is reasonable to use TAP devices instead of TUN devices. For example if you want to add the tinc device to an already existing bridge. Just add the "Mode" option to your tinc.conf.

Remember to do that on **every** host. /etc/tinc/*vpnname*/tinc.conf

```
Name = *node*
Mode = switch
Device = /dev/net/tun
ConnectTo = *other*

```

Possible tinc-up/down files could look like that:

/etc/tinc/*vpnname*/tinc-up

```
#!/bin/sh
ip link set $INTERFACE up
brctl addif *br0* $INTERFACE

```

/etc/tinc/*vpnname*/tinc-down

```
#!/bin/sh
brctl delif *br0* $INTERFACE
ip link set $INTERFACE down

```

And finally restart your tinc daemon:

```
# systemctl restart tinc@*vpnname*

```

## Troubleshooting

### I've updated my system and now tinc won't start.

In case of a linux kernel update you have to either restart your system or reinstall the running kernel package.

### I'm running a custom kernel and tinc won't start.

Make sure you have [TUN/TAP support](/index.php/OpenVPN#Configure_the_system_for_TUN.2FTAP_support "OpenVPN") enabled.