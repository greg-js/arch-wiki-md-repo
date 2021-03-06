[Wake-on-LAN](https://en.wikipedia.org/wiki/Wake-on-LAN "wikipedia:Wake-on-LAN") (WoL) is a feature to switch on a computer via the network.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware settings](#Hardware_settings)
*   [2 Software configuration](#Software_configuration)
    *   [2.1 Enable WoL on the network adapter](#Enable_WoL_on_the_network_adapter)
    *   [2.2 Make it persistent](#Make_it_persistent)
        *   [2.2.1 systemd.link](#systemd.link)
        *   [2.2.2 systemd service](#systemd_service)
        *   [2.2.3 udev](#udev)
        *   [2.2.4 cron](#cron)
        *   [2.2.5 netctl](#netctl)
        *   [2.2.6 NetworkManager](#NetworkManager)
    *   [2.3 Enable WoL in TLP](#Enable_WoL_in_TLP)
*   [3 Trigger a wake up](#Trigger_a_wake_up)
    *   [3.1 On the same LAN](#On_the_same_LAN)
    *   [3.2 Across the internet](#Across_the_internet)
*   [4 Miscellaneous](#Miscellaneous)
    *   [4.1 Check reception of the magic packets](#Check_reception_of_the_magic_packets)
        *   [4.1.1 Using netcat](#Using_netcat)
        *   [4.1.2 Using ngrep](#Using_ngrep)
    *   [4.2 Example of WoL script](#Example_of_WoL_script)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Wake-up after shutdown](#Wake-up_after_shutdown)
        *   [5.1.1 Fix using BIOS Settings](#Fix_using_BIOS_Settings)
        *   [5.1.2 Fix by Kernel quirks](#Fix_by_Kernel_quirks)
    *   [5.2 Battery draining problem](#Battery_draining_problem)
    *   [5.3 Realtek](#Realtek)
    *   [5.4 alx driver support](#alx_driver_support)
*   [6 See also](#See_also)

## Hardware settings

The target computer's motherboard and [Network Interface Controller](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller") have to support Wake-on-LAN. The target computer has to be physically connected (with a cable) to a router or to the source computer for WoL to work properly. Some wireless cards have support for Wake on Wireless (WoWLAN or WoW).

The Wake-on-LAN feature also has to be enabled in the computer's BIOS. Different motherboard manufacturers use slightly different language for this feature. Look for terminology such as "PCI Power up", "Allow PCI wake up event" or "Boot from PCI/PCI-E".

Note that some motherboards are affected by a bug that can cause immediate or random [#Wake-up after shutdown](#Wake-up_after_shutdown) whenever the BIOS WoL feature is enabled.

## Software configuration

### Enable WoL on the network adapter

Depending on the hardware, the network driver may have WoL switched off by default.

To query this status or to change the settings, install [ethtool](https://www.archlinux.org/packages/?name=ethtool), determine the name of the [network interface](/index.php/Network_interface "Network interface"), and query it using the command:

 `# ethtool *interface* | grep Wake-on` 
```
Supports Wake-on: pumbag
Wake-on: d
```

The *Wake-on* values define what activity triggers wake up: `d` (disabled), `p` (PHY activity), `u` (unicast activity), `m` (multicast activity), `b` (broadcast activity), `a` (ARP activity), and `g` (magic packet activity). The value `g` is required for WoL to work, if not, the following command enables the WoL feature in the driver:

```
# ethtool -s *interface* wol g

```

**Note:** Setting one of `u`, `m` or `b` along with `g` might also be necessary to enable the feature.

This command might not last beyond the next reboot and in this case must be repeated via some mechanism. Common solutions are listed in the following subsections.

### Make it persistent

#### systemd.link

Link-level configuration is possible through [systemd-networkd#link files](/index.php/Systemd-networkd#link_files "Systemd-networkd"). The actual setup is performed by the `net_setup_link` udev builtin. Add the `WakeOnLan` option to the network link file:

 `/etc/systemd/network/50-wired.link` 
```
[Match]
MACAddress=*aa:bb:cc:dd:ee:ff*

[Link]
NamePolicy=kernel database onboard slot path
MACAddressPolicy=persistent
**WakeOnLan=magic**
```

Also see [systemd.link(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5) for more information.

**Note:**

*   Only the first matching file is is applied. The content of the default link file `/usr/lib/systemd/network/99-default.link` shipped with systemd has to be included, otherwise the interface might be misconfigured.
*   To be considered, the file name should alphabetically come before the default `99-default.link`. For example `50-wired.link` works.
*   This configuration applies only to the link-level, and is independent of network-level daemons such as [NetworkManager](/index.php/NetworkManager "NetworkManager") or [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd").
*   In the `Match` section, `OriginalName=` can also be used to identify the interface.

#### systemd service

This is an equivalent of previous `systemd.link` option, but uses a standalone systemd service.

 `/etc/systemd/system/wol@.service` 
```
[Unit]
Description=Wake-on-LAN for %i
Requires=network.target
After=network.target

[Service]
ExecStart=/usr/bin/ethtool -s %i wol g
Type=oneshot

[Install]
WantedBy=multi-user.target
```

Alternatively install the [wol-systemd](https://aur.archlinux.org/packages/wol-systemd/) package, then activate this new service by [starting](/index.php/Starting "Starting") `wol@*interface*.service`.

#### udev

[udev](/index.php/Udev "Udev") is capable of running any command as soon as a device is visible. The following rule will turn on WOL on all [network interfaces](/index.php/Network_interface "Network interface") whose name matches `enp*`. The file name is important and must start with a number between 81 and 99 so that it runs **after** `80-net-setup-link.rules`, which renames interfaces with predicable names. Otherwise, `NAME` would be undefined and the rule would not run.

 `/etc/udev/rules.d/**81**-wol.rules`  `ACTION=="add", SUBSYSTEM=="net", NAME=="enp*", RUN+="/usr/bin/ethtool -s $name wol g"` 

The `$name` placeholder will be replaced by the value of the `NAME` variable for the matched device.

#### cron

A command can be run each time the computer is (re)booted using "@reboot" in a crontab. First, make sure [cron](/index.php/Cron#Installation "Cron") is enabled, and then [edit a crontab](/index.php/Cron#Basic_commands "Cron") for the root user that contains the following line:

```
@reboot /usr/bin/ethtool -s *interface* wol g

```

#### netctl

If using [netctl](/index.php/Netctl "Netctl"), one can make this setting persistent by adding the following the netctl profile:

 `/etc/netctl/*profile*`  `ExecUpPost='/usr/bin/ethtool -s *interface* wol g'` 

#### NetworkManager

NetworkManager provides [Wake-on-LAN ethernet support](https://www.phoronix.com/scan.php?page=news_item&px=NetworkManager-WoL-Control). One way to enable Wake-on-LAN by magic packet is through *nmcli*.

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

Then reboot, possibly two times. To disable Wake-on-Lan, substitute `magic` with `ignore`.

The Wake-on-LAN settings can also be changed from the GUI using [nm-connection-editor](https://www.archlinux.org/packages/?name=nm-connection-editor).

You can disable Wake-on-Lan for all connections permanently by adding a dedicated configuration file :

 `/etc/NetworkManager/conf.d/*wake-on-lan.conf*` 
```
[connection]
ethernet.wake-on-lan = ignore
wifi.wake-on-wlan = ignore
```

### Enable WoL in TLP

When using [TLP](/index.php/TLP "TLP") for suspend/hibernate, the `WOL_DISABLE` setting should be set to `N` in `/etc/default/tlp` to allow resuming the computer with WoL.

## Trigger a wake up

To trigger WoL on a target machine, its **MAC address** must be known. To obtain it, execute the following command from the machine:

 `$ ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp1s0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc fq_codel master br0 state UP group default qlen 1000
    link/ether **48:05:ca:09:0e:6a** brd ff:ff:ff:ff:ff:ff
```

Here the MAC address is `48:05:ca:09:0e:6a`.

In its simplest form, Wake-on-LAN broadcasts the magic packet containing the MAC address within the current network subnet, below the IP protocol layer. The knowledge of an IP address for the target computer is not necessary.

If used to wake up a computer over the internet or in a different subnet, it typically relies on the router to relay the packet and broadcast it. In this scenario, the external IP address of the router must be known and in some cases the internal IP address of the target machine is needed to ensure the NAT (Network Address Translator) router manages to communicate with the target machine.

Applications that are able to send magic packets for Wake-on-LAN:

*   **gWakeOnLAN** — GTK utility to awake turned off computers through the Wake-on-LAN feature.

	[https://muflone.com/gwakeonlan/english/](https://muflone.com/gwakeonlan/english/) || [gwakeonlan](https://www.archlinux.org/packages/?name=gwakeonlan)

*   **wol** — Implements Wake-on-LAN functionality in a small program. It wakes up hardware that is Magic Packet compliant. Note: This application will need the port changed to 9 from the default(40000) using the -p argument/flag.

	[https://sourceforge.net/projects/wake-on-lan/](https://sourceforge.net/projects/wake-on-lan/) || [wol](https://www.archlinux.org/packages/?name=wol)

### On the same LAN

If you are connected directly to another computer through a network cable, or the traffic within a LAN is not firewalled, then using Wake-on-LAN should be straightforward since there is no need to worry about port redirects.

In the simplest case the default broadcast address `255.255.255.255` is used:

```
$ wol *target_MAC_address*

```

To broadcast the magic packet only to a specific subnet or host, use the `-i` switch:

```
$ wol -i *target_IP* *target_MAC_address*

```

### Across the internet

When the source and target computers are separated by a NAT router, different solution can be envisaged:

*   If the router supports *WoL*, one can rely on it to properly broadcast the packet into the local network.

Otherwise Wake-on-Lan can be achieved via [port forwarding](https://en.wikipedia.org/wiki/Port_forwarding "wikipedia:Port forwarding"). The router needs to be configured using one of these two options:

*   Forward a different port to each target machine. This requires any target machine to have a static IP address on its LAN.
*   Forward a single port to the [broadcast address](https://en.wikipedia.org/wiki/Broadcast_address "wikipedia:Broadcast address"). Most routers do not allow to forward to broadcast, however if you can get shell access to your router, through telnet, ssh, serial cable or other mean, run the command: `$ ip neighbor add 192.168.1.254 lladdr FF:FF:FF:FF:FF:FF dev net0` This example assumes the network is *192.168.1.0/24* and uses *net0* as network interface. Now, forward UDP port 9 to 192.168.1.254\. This solution was successfully tested on a Linksys WRT54G running [Tomato](https://en.wikipedia.org/wiki/Tomato_(firmware) "wikipedia:Tomato (firmware)"), and on the Verizon FIOS ActionTec router. For notes on how to do it on a router with [DD-WRT](https://en.wikipedia.org/wiki/DD-WRT "wikipedia:DD-WRT") firmware, see [this tutorial](http://www.dd-wrt.com/wiki/index.php/WOL#Remote_Wake_On_LAN_via_Port_Forwarding) and for a router with [OpenWrt](https://en.wikipedia.org/wiki/OpenWrt "wikipedia:OpenWrt") firmware, see [this tutorial](https://wiki.openwrt.org/doc/uci/wol).

In any case, run the following command from the source computer to trigger wake-up:

```
$ wol -p *forwarded_port* -i *router_IP* *target_MAC_address*

```

## Miscellaneous

### Check reception of the magic packets

In order to make sure the WoL packets reach the target computer, one can listen to the UDP port, usually port 9, for magic packets. The magic packet frame expected contains 6 bytes of FF followed by 16 repetitions of the target computer's MAC (6 bytes each) for a total of 102 bytes.

#### Using netcat

This can be performed by installing [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) on the target computer and using the following command:

```
# nc --udp --listen --local-port=9 --hexdump

```

Then wait for the incoming traffic to appear in the `nc` terminal.

#### Using ngrep

Install [ngrep](https://www.archlinux.org/packages/?name=ngrep) on the target computer and type the following command:

```
# ngrep '\xff{6}(.{6})\1{15}' -x port 9

```

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

### Wake-up after shutdown

It is known that some motherboards are affected by a bug that can cause immediate or random wake-up after a *shutdown* whenever the BIOS WoL feature is enabled (as discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=173648) for example).

#### Fix using BIOS Settings

The following actions in the BIOS preferences can solve this issue with some motherboards:

1.  Disable all references to *xHCI* in the USB settings (note this will also disable USB 3.0 at boot time)
2.  Disable *EuP 2013* if it is explicitly an option
3.  Optionally enable wake-up on keyboard actions

**Note:** There are mixed opinions as to the value of #3 above and it may be motherboard dependent.

#### Fix by Kernel quirks

The issue can also be solved by adding the following kernel boot parameter: `xhci_hcd.quirks=270336` This activates the following quirks:

*   `XHCI_SPURIOUS_REBOOT`
*   `XHCI_SPURIOUS_WAKEUP`

### Battery draining problem

Some laptops have a battery draining problem after shutdown [[1]](http://ubuntuforums.org/archive/index.php/t-1729782.html). This might be caused by enabled WOL. To solve this problem, disable it by using ethtool as mentioned above.

```
# ethtool -s net0 wol d

```

### Realtek

Users with Realtek 8168 8169 8101 8111(C) based NICs (cards / and on-board) may notice a problem where the NIC seems to be disabled on boot and has no Link light. See [Network configuration/Ethernet#Realtek no link / WOL problem](/index.php/Network_configuration/Ethernet#Realtek_no_link_/_WOL_problem "Network configuration/Ethernet").

If the link light on the network switch is enabled when the computer is turned off but wake on LAN is still not working, booting the system using the [r8168](https://www.archlinux.org/packages/?name=r8168) kernel module at least once and then switching back to the r8169 kernel module included with the kernel seems to fix it at least in the following configurations:

*   MSI B85M-E45 motherboard, BIOS version V10.9, onboard Realtek 8111G chipset

For the `r8168` module you might need to set the `s5wol=1` [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules") to enable the wake on LAN functionality.

### alx driver support

For some newer Atheros-based NICs (such as Atheros AR8161 and Killer E2500), WOL support has been disabled in the mainline `alx` module due to a bug causing unintentional wake-up (see [this patch discussion](http://www.spinics.net/lists/netdev/msg242477.html)). A patch can be applied (or installed as a [dkms](/index.php/Dkms "Dkms") module) which both restores WOL support and fixes the underlying bug, as outlined in [this thread](https://bugzilla.kernel.org/show_bug.cgi?id=61651).

See also the pre-patched sources in [[2]](https://github.com/Snugface/alx).

## See also

*   [Wake-On-Lan](http://www.depicus.com/wake-on-lan/woli.aspx)