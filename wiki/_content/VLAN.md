# VLAN

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Network Configuration](/index.php/Network_Configuration "Network Configuration")
*   [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")
*   [Netctl](/index.php/Netctl "Netctl")

Virtual LANs give you the ability to sub-divide a LAN. Linux can accept **VLAN** tagged traffic and presents each **VLAN ID** as a different network interface (eg: `eth0.100` for **VLAN ID** `100`)

This article explains how to configure a VLAN using [iproute2](https://www.archlinux.org/packages/?name=iproute2) and [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") or [netctl](/index.php/Netctl "Netctl").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Create the VLAN device](#Create_the_VLAN_device)
    *   [1.2 Add an IP](#Add_an_IP)
    *   [1.3 Turning down the device](#Turning_down_the_device)
    *   [1.4 Removing the device](#Removing_the_device)
    *   [1.5 Starting at boot](#Starting_at_boot)
        *   [1.5.1 systemd-networkd](#systemd-networkd)
        *   [1.5.2 netctl](#netctl)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 udev renames the virtual devices](#udev_renames_the_virtual_devices)

## Configuration

Previously Arch Linux used the `vconfig` command to setup VLANs. This had been superseded by the `ip` command. Make sure you have [iproute2](https://www.archlinux.org/packages/?name=iproute2) installed.

In the following examples, lets assume the **interface** is `eth0`, the assigned **name** is `eth0.100` and the **vlan id** is `100`.

### Create the VLAN device

Add the VLAN with the following command:

```
# ip link add link eth0 name eth0.100 type vlan id 100

```

Run `ip link` to confirm that it has been created.

This interface behaves like a normal interface. All traffic routed to it will go through the master interface (in this example, `eth0`) but with a VLAN tag. Only VLAN aware devices can accept them if configured correctly else the traffic is dropped.

Using a **name** like `eth0.100` is just convention and not enforced; you can alternatively use `eth0_100` or something descriptive like `IPTV`. To see the VLAN ID on an interface, in case you used an unconventional name:

```
# ip -d link show eth0.100

```

The `-d` flag shows full details on an interface:

```
# ip -d addr show
4: eno1.100@eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
   link/ether 96:4a:9c:84:36:51 brd ff:ff:ff:ff:ff:ff promiscuity 0 
   **vlan protocol 802.1Q id 100 <REORDER_HDR>** 
   inet6 fe80::944a:9cff:fe84:3651/64 scope link 
      valid_lft forever preferred_lft forever

```

### Add an IP

Now add an IPv4 address to the just created vlan link, and activate the link:

```
# ip addr add 192.168.100.1/24 brd 192.168.100.255 dev eth0.100
# ip link set dev eth0.100 up

```

### Turning down the device

To cleanly shutdown the setting before you remove the link, you can do:

 `# ip link set dev eth0.100 down` 

### Removing the device

Removing a VLAN interface is significantly less convoluted

 `# ip link delete eth0.100` 

### Starting at boot

#### systemd-networkd

Use the following configuration files:

 `/etc/systemd/network/_eno1_.network` 

```
[Match]
Name=eno1

[Network]
DHCP=v4
VLAN=eno1.100
VLAN=eno1.200

```

 `/etc/systemd/network/_eno1.100_.netdev` 

```
[NetDev]
Name=eno1.100
Kind=vlan

[VLAN]
Id=100

```

 `/etc/systemd/network/_eno1.200_.netdev` 

```
[NetDev]
Name=eno1.200
Kind=vlan

[VLAN]
Id=200

```

Then [enable](/index.php/Enable "Enable") `systemd-networkd.service`. See [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") for details.

#### netctl

You can use [netctl](/index.php/Netctl "Netctl") for this purpose, see the self-explanatory example profiles in `/etc/netctl/examples/vlan-{dhcp,static}` .

## Troubleshooting

### udev renames the virtual devices

An annoyance is that [udev](/index.php/Udev "Udev") may try to rename virtual devices as they are added, thus ignoring the **name** configured for them (in this case `eth0.100`).

For instance, if the following commands are issued:

```
# ip link add link eth0 name eth0.100 type vlan id 100
# ip link show 

```

This could generate the following output:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP qlen 1000
    link/ether aa:bb:cc:dd:ee:ff brd ff:ff:ff:ff:ff:ff
3: rename1@eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state DOWN 
    link/ether aa:bb:cc:dd:ee:ff brd ff:ff:ff:ff:ff:ff

```

**udev** has ignored the configured virtual interface name `eth0.100` and autonamed it **rename1**.

The solution is to edit `/etc/udev/rules.d/network_persistent.rules` and append **DRIVERS=="?*"** to the end of the physical interface's configuration line.

For example, for the interface **aa:bb:cc:dd:ee:ff** (eth0):

 `/etc/udev/rules.d/network_persistent.rules` 

```
SUBSYSTEM=="net", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="eth0", DRIVERS=="?*"

```

A reboot should mean that VLANs configure correctly with the names assigned to them.

Retrieved from "[https://wiki.archlinux.org/index.php?title=VLAN&oldid=383952](https://wiki.archlinux.org/index.php?title=VLAN&oldid=383952)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")