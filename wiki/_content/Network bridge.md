# Network bridge

A bridge is a piece of software used to unite two or more network segments. A bridge behaves like a virtual network switch, working transparently (the other machines do not need to know or care about its existence). Any real devices (e.g. `eth0`) and virtual devices (e.g. `tap0`) can be connected to it.

This article explains how to create a bridge that contains at least an ethernet device. This is useful for things like the bridge mode of [QEMU](/index.php/QEMU "QEMU"), setting a software based access point, etc.

## Contents

*   [1 Creating a bridge](#Creating_a_bridge)
    *   [1.1 With iproute2](#With_iproute2)
    *   [1.2 With bridge-utils](#With_bridge-utils)
    *   [1.3 With netctl](#With_netctl)
    *   [1.4 With systemd-networkd](#With_systemd-networkd)
    *   [1.5 With NetworkManager](#With_NetworkManager)
*   [2 Assigning an IP address](#Assigning_an_IP_address)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Wireless interface on a bridge](#Wireless_interface_on_a_bridge)
*   [4 See also](#See_also)

## Creating a bridge

There are a number of ways to create a bridge.

### With iproute2

This section describes the management of a network bridge using the _ip_ tool from the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package, which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

Create a new bridge and change its state to up:

```
# ip link add name _bridge_name_ type bridge
# ip link set _bridge_name_ up

```

To add an interface (e.g. eth0) into the bridge, its state must be up:

```
# ip link set eth0 up

```

Adding the interface into the bridge is done by setting its master to `_bridge_name_`:

```
# ip link set eth0 master _bridge_name_

```

To show the existing bridges and associated interfaces, use the _bridge_ utility (also part of [iproute2](https://www.archlinux.org/packages/?name=iproute2)). See `man bridge` for details.

```
# bridge link

```

This is how to remove an interface from a bridge:

```
# ip link set eth0 nomaster

```

The interface will still be up, so you may also want to bring it down:

```
# ip link set eth0 down

```

To delete a bridge issue the following command:

```
# ip link delete _bridge_name_ type bridge

```

This will automatically remove all interfaces from the bridge. The slave interfaces will still be up, though, so you may also want to bring them down after.

### With bridge-utils

This section describes the management of a network bridge using the legacy _brctl_ tool from the [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) package, which is available in the [official repositories](/index.php/Official_repositories "Official repositories"). See `man brctl` for full listing of options.

Create a new bridge:

```
# brctl addbr _bridge_name_

```

Add a device to a bridge, for example `eth0`:

```
# brctl addif _bridge_name_ eth0

```

**Note:** Adding an interface to a bridge will cause the interface to lose its existing IP address. If you're connected remotely via the interface you intend to add to the bridge, you will lose your connection. This problem can be worked around by scripting the bridge to be created at system startup.

Show current bridges and what interfaces they are connected to:

```
$ brctl show

```

Set the bridge device up:

```
# ip link set up dev _bridge_name_

```

Delete a bridge, you need to first set it to _down_:

```
# ip link set dev _bridge_name_ down
# brctl delbr _bridge_name_

```

**Note:** To enable the [bridge-netfilter](http://ebtables.netfilter.org/documentation/bridge-nf.html) functionality, you need to manually load the `br_netfilter` module:

```
# modprobe br_netfilter

```

See also [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

### With netctl

See [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl").

### With systemd-networkd

See [systemd-networkd#Bridge interface](/index.php/Systemd-networkd#Bridge_interface "Systemd-networkd").

### With NetworkManager

Gnome's NetworkManager can create bridges, but currently will not auto-connect to them. Open Network Settings, add a new interface of type Bridge, add a new bridged connection, and select the MAC address of the device to attach to the bridge.

Now, find the UUID of the attached device (by default named "bridge0 slave 1"):

```
$ nmcli connection

```

Finally, enable that connection:

```
$ nmcli con up <UUID>

```

If NetworkManager's default interface for the device you added to the bridge connects automatically, you may want to disable that by clicking the gear next to it in Network Settings, and unchecking "Connect automatically" under "Identity."

## Assigning an IP address

When the bridge is fully set up, it can be assigned an IP address:

```
# ip addr add dev _bridge_name_ 192.168.66.66/24

```

## Tips and tricks

### Wireless interface on a bridge

To add a wireless interface to a bridge, you first have to assign the wireless interface to an access point or start an access point with [hostapd](/index.php/Software_access_point "Software access point"). Otherwise the wireless interface will not be added to the bridge.

See also [Bridging with a wireless NIC](https://wiki.debian.org/BridgeNetworkConnections#Bridging_with_a_wireless_NIC) on Debian wiki.

## See also

*   [Official documentation for bridge-utils](http://www.linuxfoundation.org/collaborate/workgroups/networking/bridge)
*   [Official documentation for iproute2](http://www.linuxfoundation.org/collaborate/workgroups/networking/iproute2)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Network_bridge&oldid=414091](https://wiki.archlinux.org/index.php?title=Network_bridge&oldid=414091)"