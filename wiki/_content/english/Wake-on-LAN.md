[Wake-on-LAN](https://en.wikipedia.org/wiki/Wake-on-LAN "wikipedia:Wake-on-LAN") (WoL) is a feature to switch on a computer via the network.

## Contents

*   [1 Hardware settings](#Hardware_settings)
*   [2 Software configuration](#Software_configuration)
    *   [2.1 Enable WoL on the network adapter](#Enable_WoL_on_the_network_adapter)
    *   [2.2 Make it persistent](#Make_it_persistent)
        *   [2.2.1 netctl](#netctl)
        *   [2.2.2 systemd.link](#systemd.link)
        *   [2.2.3 systemd service](#systemd_service)
        *   [2.2.4 udev](#udev)
        *   [2.2.5 cron](#cron)
        *   [2.2.6 NetworkManager](#NetworkManager)
    *   [2.3 Enable WoL in TLP](#Enable_WoL_in_TLP)
*   [3 Trigger a wake up](#Trigger_a_wake_up)
    *   [3.1 On the same LAN](#On_the_same_LAN)
    *   [3.2 Across the internet](#Across_the_internet)
        *   [3.2.1 Forward a port to the broadcast address](#Forward_a_port_to_the_broadcast_address)
*   [4 Miscellaneous](#Miscellaneous)
    *   [4.1 Check reception of the magic packets](#Check_reception_of_the_magic_packets)
    *   [4.2 Example of WoL script](#Example_of_WoL_script)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Battery draining problem](#Battery_draining_problem)
    *   [5.2 Realtek](#Realtek)
    *   [5.3 alx driver support](#alx_driver_support)
*   [6 See also](#See_also)

## Hardware settings

The target computer's motherboard and [Network Interface Controller](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller") have to support Wake-on-LAN. The target computer has to be physically connected (with a cable) to a router or to the source computer, wireless cards do not support WoL.

The Wake-on-LAN feature also has to be enabled in the computer's BIOS. Different motherboard manufacturers use slightly different language for this feature. Look for terminology such as "PCI Power up", "Allow PCI wake up event" or "Boot from PCI/PCI-E".

It is known that some motherboards are affected by a bug that can cause immediate or random wake-up after a *shutdown* whenever the BIOS WoL feature is enabled (as discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=173648) for example). The following actions in the BIOS preferences can solve this issue with some motherboards:

1.  Disable all references to *xHCI* in the USB settings (note this will also disable USB 3.0 at boot time)
2.  Disable *EuP 2013* if it is explicitly an option
3.  Optionally enable wake-up on keyboard actions

**Note:** There are mixed opinions as to the value of #3 above and it may be motherboard dependent.

## Software configuration

### Enable WoL on the network adapter

Depending on the hardware, the network driver may have WoL switched off by default.

To query this status or to change the settings, install [ethtool](https://www.archlinux.org/packages/?name=ethtool) and query the network device via this command:

 `# ethtool *interface* | grep Wake-on` 
```
Supports Wake-on: pumbag
Wake-on: d
```

The *Wake-on* values define what activity triggers wake up: `d` (disabled), `p` (PHY activity), `u` (unicast activity), `m` (multicast activity), `b` (broadcast activity), `a` (ARP activity), and `g` (magic packet activity). The value `g` is required for WoL to work, if not, the following command enables the WoL feature in the driver:

```
# ethtool -s *interface* wol g

```

This command might not last beyond the next reboot and in this case must be repeated via some mechanism. Common solutions are listed in the following subsections.

### Make it persistent

#### netctl

If using netctl, one can make this setting persistent by adding the following the netctl profile:

 `/etc/netctl/*profile*`  `ExecUpPost='/usr/bin/ethtool -s *interface* wol g'` 

#### systemd.link

Link-level configuration is possible through systemd. The actual setup is performed by the `net_setup_link` udev builtin. Add the `WakeOnLan` option to the network link file:

 `/etc/systemd/network/50-wired.link` 
```
[Link]
WakeOnLan=magic
...
```

**Note:** This configuration applies only to the link-level, and is independent of network-level daemons such as [NetworkManager](/index.php/NetworkManager "NetworkManager") or [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd").

See [systemd-networkd#link files](/index.php/Systemd-networkd#link_files "Systemd-networkd") and [systemd.link(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5) for more information.

#### systemd service

This is an equivalent of previous `systemd.link` option, but uses a standalone systemd service.

 `/etc/systemd/system/wol@.service` 
```
[Unit]
Description=Wake-on-LAN for %i
Requires=network.target
After=network.target

[Service]
ExecStart=/usr/bin/ethtool -s %i wol g
Type=oneshot

[Install]
WantedBy=multi-user.target
```

Alternatively install the [wol-systemd](https://aur.archlinux.org/packages/wol-systemd/) package.

Then activate this new service by [starting](/index.php/Starting "Starting") `wol@*interface*.service`.

#### udev

[udev](/index.php/Udev "Udev") is capable of running any command as soon as a device is visible. The following rule will turn on WOL on all [network interfaces](/index.php/Network_interface "Network interface") whose name matches `enp*`:

 `/etc/udev/rules.d/99-wol.rules` 
```
ACTION=="add", SUBSYSTEM=="net", NAME=="enp*", RUN+="/usr/bin/ethtool -s $name wol g"

```

The `$name` placeholder will be replaced by the value of the `NAME` variable for the matched device.

**Note:** The name of the configuration file is important. Due to the introduction of [persistent device names](/index.php/Network_configuration#Device_names "Network configuration") in systemd v197, it is important that the rules matching a specific network interface are named lexicographically after `80-net-name-slot.rules`, so that they are applied after the devices gain the persistent names.

**Warning:** [udev](/index.php/Udev "Udev") will match the device as soon it becomes available, be this in the [initramfs](/index.php/Initramfs "Initramfs") (before the switch_root) or the main system. The order is not deterministic; there is no guarantee. Be sure that your initramfs includes the necessary udev rules (from `/etc/udev/rules.d`) and supporting binaries (`/usr/bin/ethtool`).

#### cron

A command can be run each time the computer is (re)booted using "@reboot" in a crontab. First, make sure [cron](/index.php/Cron#Installation "Cron") is enabled, and then [edit a crontab](/index.php/Cron#Basic_commands "Cron") for the root user that contains the following line:

```
@reboot /usr/bin/ethtool -s [net-device] wol g

```

#### NetworkManager

In version 1.0.6 NetworkManager [adds Wake-on-LAN controls](https://www.phoronix.com/scan.php?page=news_item&px=NetworkManager-WoL-Control). One way to enable Wake-on-LAN by magic packet is through nmcli.

First, search for the name of the wired connection:

 `# nmcli con show` 
```
NAME    UUID                                  TYPE            DEVICE
wired1  612e300a-c047-4adb-91e2-12ea7bfe214e  802-3-ethernet  enp0s25
```

By following, one can view current status of Wake-on-LAN settings:

 `# nmcli c show "wired1" | grep 802-3-ethernet.wake-on-lan` 
```
802-3-ethernet.wake-on-lan:             default
802-3-ethernet.wake-on-lan-password:    --
```

Enable Wake-on-LAN by magic packet on that connection:

```
# nmcli c modify "wired1" 802-3-ethernet.wake-on-lan magic

```

Then reboot, possibly two times.

From version 1.2.0 Wake-on-LAN settings can be changed graphically using [nm-connection-editor](https://www.archlinux.org/packages/?name=nm-connection-editor).

### Enable WoL in TLP

When using [TLP](/index.php/TLP "TLP") for suspend/hibernate, the `WOL_DISABLE` setting should be set to `N` in `/etc/default/tlp` to allow resuming the computer with WoL.

## Trigger a wake up

To trigger WoL on a target machine, its MAC address and external or internal IP should be known.

To obtain the internal IP address and MAC address of the target computer, execute the following command:

 `$ ip addr` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
   inet 127.0.0.1/8 scope host lo
      valid_lft forever preferred_lft forever
   inet6 ::1/128 scope host
      valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc fq_codel master br0 state UP group default qlen 1000
    link/ether **48:05:ca:09:0e:6a** brd ff:ff:ff:ff:ff:ff
    inet **192.168.1.20/24** brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::6a05:caff:fe09:e6a/64 scope link
       valid_lft forever preferred_lft forever

```

Here the internal IP address is `192.168.1.20` and the MAC address is `48:05:ca:09:0e:6a`.

One program able to send magic packets for WoL is [wol](https://www.archlinux.org/packages/?name=wol).

### On the same LAN

If you are connected directly to another computer through a network cable, or the traffic within a LAN is not firewalled, then using Wake-on-LAN should be very easy since there is no need to worry about port redirects.

In the simplest case the default broadcast address `255.255.255.255` is used:

```
$ wol *target_MAC_address*

```

To broadcast the magic packet only to a specific subnet or host, use the `-i` switch:

```
$ wol -i *target_IP* *target_MAC_address*

```

**Tip:** If you intend to continue using Wake-on-LAN, it is recommended to assign a static IP address to the target computer.

### Across the internet

When the source and target computers are separated by a router, Wake-on-LAN can be achieved via [port forwarding](https://en.wikipedia.org/wiki/Port_forwarding "wikipedia:Port forwarding"). The router needs to be configured using one of these two options:

*   Forward a different port to each target machine. This requires any target machine to have a static IP address on its LAN.
*   Forward a single port to the [broadcast address](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address"). This is likely not possible on your router with the stock firmware, in this case refer to [#Forward a port to the broadcast address](#Forward_a_port_to_the_broadcast_address) for workarounds.

In both cases, run the following command from the source computer to trigger wake-up:

```
$ wol -p *forwarded_port* -i *router_IP* *target_MAC_address*

```

#### Forward a port to the broadcast address

Most routers do not allow to forward to broadcast, however if you can get shell access to your router (through telnet, ssh, serial cable, etc), you can implement this workaround:

```
$ ip neighbor add 192.168.1.254 lladdr FF:FF:FF:FF:FF:FF dev net0

```

(The above command assumes your network is *192.168.1.0/24* and uses *net0* as network interface). Now, forward UDP port 9 to 192.168.1.254\. This has worked for me on a Linksys WRT54G running [Tomato](https://en.wikipedia.org/wiki/Tomato_(firmware) "wikipedia:Tomato (firmware)"), and on the Verizon FIOS ActionTec router.

For notes on how to do it on a router with [DD-WRT](https://en.wikipedia.org/wiki/DD-WRT "wikipedia:DD-WRT") firmware, see [this tutorial](http://www.dd-wrt.com/wiki/index.php/WOL#Remote_Wake_On_LAN_via_Port_Forwarding).

For notes on how to do it on a router with [OpenWrt](https://en.wikipedia.org/wiki/OpenWrt "wikipedia:OpenWrt") firmware, see [this tutorial](https://wiki.openwrt.org/doc/uci/wol).

## Miscellaneous

### Check reception of the magic packets

In order to make sure the WoL packets reach the target computer, one can listen to the UDP port, usually port 9, for magic packets.

This can be performed by installing [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) from the [official repositories](/index.php/Official_repositories "Official repositories") on the target computer and using the following command:

```
# nc --udp --listen --local-port=9 --hexdump

```

Then wait for the incoming traffic to appear in the `nc` terminal.

The magic packet frame expected contains 6 bytes of FF followed by 16 repetitions of the target computer's MAC (6 bytes each) for a total of 102 bytes.

### Example of WoL script

Here is a script that illustrates the use of `wol` with different machines:

```
#!/bin/bash

# definition of MAC addresses
monster=01:12:46:82:ab:4f
ghost=01:1a:d2:56:6b:e6

echo "Which PC to wake?"
echo "m) monster"
echo "g) ghost"
echo "q) quit"
read input1
case $input1 in
  m)
    /usr/bin/wol $monster
    ;;
  g)
    # uses wol over the internet provided that port 9 is forwarded to ghost on ghost's router
    /usr/bin/wol --port=9 --host=ghost.mydomain.org $ghost
    ;;
  Q|q)
    break
    ;;
esac
```

## Troubleshooting

### Battery draining problem

Some laptops have a battery draining problem after shutdown [[1]](http://ubuntuforums.org/archive/index.php/t-1729782.html). This might be caused by enabled WOL. To solve this problem, disable it by using ethtool as mentioned above.

```
# ethtool -s net0 wol d

```

### Realtek

Users with Realtek 8168 8169 8101 8111(C) based NICs (cards / and on-board) may notice a problem where the NIC seems to be disabled on boot and has no Link light. See [Network configuration#Realtek no link / WOL problem](/index.php/Network_configuration#Realtek_no_link_.2F_WOL_problem "Network configuration").

If the link light on the network switch is enabled when the computer is turned off but wake on LAN is still not working, booting the system using the [r8168](https://www.archlinux.org/packages/?name=r8168) kernel module at least once and then switching back to the r8169 kernel module included with the kernel seems to fix it at least in the following configurations:

*   MSI B85M-E45 motherboard, BIOS version V10.9, onboard Realtek 8111G chipset

For the `r8168` module you might need to set the `s5wol=1` [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules") to enable the wake on LAN functionality.

### alx driver support

For some newer Atheros-based NICs (such as Atheros AR8161 and Killer E2500), WOL support has been disabled in the mainline `alx` module due to a bug causing unintentional wake-up (see [this patch discussion](http://www.spinics.net/lists/netdev/msg242477.html)). A patch can be applied (or installed as a [dkms](/index.php/Dkms "Dkms") module) which both restores WOL support and fixes the underlying bug, as outlined in [this thread](https://bugzilla.kernel.org/show_bug.cgi?id=61651).

## See also

*   [Wake-On-Lan](http://www.depicus.com/wake-on-lan/woli.aspx)