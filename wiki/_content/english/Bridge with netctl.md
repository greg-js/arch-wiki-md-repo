Make sure [netctl](/index.php/Netctl "Netctl") is installed.

Copy `/etc/netctl/examples/bridge` to `/etc/netctl/bridge`.

In this example, we create a bridge called `br0` which has real Ethernet adapter `eth0` and (optionally) a tap device `tap0` connected to it. Of course, edit `br0`, `eth0` and `tap0` to your needs.

 `/etc/netctl/bridge` 
```
Description="Example Bridge connection"
Interface=br0
Connection=bridge
BindsToInterfaces=(eth0 tap0)
IP=dhcp

```

This example creates a statically assigned bridge called `br0` which has real Ethernet adapter `eth0` connected to it. Edit `Interface`, `BindsToInterfaces`, `Address`, and `Gateway` to your needs.

 ` /etc/netctl/bridge` 
```
Description="Example Bridge connection"
Interface=br0
Connection=bridge
BindsToInterfaces=(eth0)
IP=static
Address='192.168.10.20/24'
Gateway='192.168.10.200'
## Ignore (R)STP and immediately activate the bridge
SkipForwardingDelay=yes

```

**Tip:** If you are using static IP, see man pages of [netctl](/index.php/Netctl "Netctl"), and also edit `/etc/resolv.conf` if necessary.

This example ensures that the bridge gets assigned the MAC address of the ethernet device (reference [https://github.com/joukewitteveen/netctl/issues/111](https://github.com/joukewitteveen/netctl/issues/111) )

 `/etc/netctl/bridge` 
```
Description="Bridge eth0-tap0"
Interface=br0
Connection=bridge
BindsToInterfaces=(eth0 tap0)
IP=no
ExecUpPost="ip link set dev br0 address $(cat /sys/class/net/eth0/address); IP=dhcp; ip_set"
ExecDownPre="IP=dhcp"

## Ignore (R)STP and immediately activate the bridge
SkipForwardingDelay=yes

```

You can bridge any combination of network devices editing `BindsToInterfaces` option.

If any of the bridged devices (e.g. `eth0`, `tap0`) had [dhcpcd](/index.php/Dhcpcd "Dhcpcd") enabled, [stop and disable](/index.php/Systemd#Using_units "Systemd") the `dhcpcd@eth0.service` daemon. Or set `IP=no` to the netctl profiles.

Finally, [start and enable](/index.php/Netctl#Just_one_profile "Netctl") your `/etc/netctl/bridge`.