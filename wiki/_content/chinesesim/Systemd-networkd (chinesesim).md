相关文章

*   [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")
*   [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Network bridge (简体中文)](/index.php/Network_bridge_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network bridge (简体中文)")
*   [Network configuration (简体中文)](/index.php/Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network configuration (简体中文)")
*   [Wireless network configuration (简体中文)](/index.php/Wireless_network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wireless network configuration (简体中文)")
*   [Category:Network configuration (简体中文)](/index.php/Category:Network_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Network configuration (简体中文)")

**翻译状态：** 本文是英文页面 [Systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-06-18，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd-networkd&diff=0&oldid=575580)可以查看翻译后英文页面的改动。

*systemd-networkd* 是一个管理网络配置的系统守护进程。它会在网络设备出现时检测和配置；它还可以创建虚拟网络设备。这个服务对被 [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") 管理的容器或者虚拟机的复杂网络配置尤其有用，同样也适用于简单的网络配置。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 基本用法](#基本用法)
    *   [1.1 必需的服务和设置](#必需的服务和设置)
    *   [1.2 配置样例](#配置样例)
        *   [1.2.1 使用 DHCP 的有线适配器](#使用_DHCP_的有线适配器)
        *   [1.2.2 使用静态 IP 的有线适配器](#使用静态_IP_的有线适配器)
        *   [1.2.3 无线适配器](#无线适配器)
        *   [1.2.4 Wired and wireless adapters on the same machine](#Wired_and_wireless_adapters_on_the_same_machine)
        *   [1.2.5 Renaming an interface](#Renaming_an_interface)
*   [2 Configuration files](#Configuration_files)
    *   [2.1 network files](#network_files)
        *   [2.1.1 [Match]](#[Match])
        *   [2.1.2 [Link]](#[Link])
        *   [2.1.3 [Network]](#[Network])
        *   [2.1.4 [Address]](#[Address])
        *   [2.1.5 [Route]](#[Route])
        *   [2.1.6 [DHCP]](#[DHCP])
    *   [2.2 netdev files](#netdev_files)
        *   [2.2.1 [Match] section](#[Match]_section)
        *   [2.2.2 [NetDev] section](#[NetDev]_section)
    *   [2.3 link files](#link_files)
        *   [2.3.1 [Match] section](#[Match]_section_2)
        *   [2.3.2 [Link] section](#[Link]_section)
*   [3 Usage with containers](#Usage_with_containers)
    *   [3.1 Basic DHCP network](#Basic_DHCP_network)
    *   [3.2 DHCP with two distinct IP](#DHCP_with_two_distinct_IP)
        *   [3.2.1 Bridge interface](#Bridge_interface)
        *   [3.2.2 Bind ethernet to bridge](#Bind_ethernet_to_bridge)
        *   [3.2.3 Bridge network](#Bridge_network)
        *   [3.2.4 Add option to boot the container](#Add_option_to_boot_the_container)
        *   [3.2.5 Result](#Result)
        *   [3.2.6 Notice](#Notice)
    *   [3.3 Static IP network](#Static_IP_network)
*   [4 Interface and desktop integration](#Interface_and_desktop_integration)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Mount services at boot fail](#Mount_services_at_boot_fail)
    *   [5.2 systemd-resolve not searching the local domain](#systemd-resolve_not_searching_the_local_domain)
    *   [5.3 Connected second PC unable to use bridged LAN](#Connected_second_PC_unable_to_use_bridged_LAN)
*   [6 See also](#See_also)

## 基本用法

[systemd](https://www.archlinux.org/packages/?name=systemd) 是默认 Arch 安装的一部分，包含操作有线网络所需的所有文件。无线适配器可以通过其他服务（比如 [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") 或者 [iwd](/index.php/Iwd "Iwd")）来配置，本文后面的部分也会介绍相关内容。

### 必需的服务和设置

[start/enable](/index.php/Start/enable "Start/enable") `systemd-networkd.service` 以使用 *systemd-networkd*。

[start/enable](/index.php/Start/enable "Start/enable") `systemd-resolved.service` 是可选的，它为本地应用程序提供网络名称（DNS）解析服务。是否使用它可以考虑下面几条：

*   如果 *.network* 文件中指定了 DNS 条目，[systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") 服务是必需的
*   它能够自动地从 DHCP 客户端获取 DNS 地址
*   请搞明白 [resolv.conf](/index.php/Resolv.conf "Resolv.conf") 和 *systemd-resolved* 如何互相影响，以便正确配置要使用的 DNS 服务器。更多相关信息可以参见 [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   注意：即使没有启用 *systemd-networkd*， *systemd-resolved* 也能够提供服务。

### 配置样例

在本节中，所有配置都存储为在 `/etc/systemd/network/` 目录下 形如 `foo.network` 的文件。有关选项的完整列表和处理顺序可以参考 [#Configuration files](#Configuration_files) 和 [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5)。

Systemd/udev 会自动为所有本地以太网，WLAN 和 WWAN 接口分配可预测，稳定的网络接口名。使用 `networkctl list` 以列出系统上所有设备。

在修改了配置文件之后，[restart](/index.php/Restart "Restart") `systemd-networkd.service` 以使得它们生效。

**Note:**

*   配置文件中指定的选项区分大小写。
*   在下面的示例中，`enp1s0` 是有线适配器，`wlp2s0` 是无线适配器。他们的名字在不同系统上可能会有不同的名字。也可以使用通配符，例如，`Name=en*`。
*   如果想要禁用 IPv6 的话，参考 [IPv6#systemd-networkd](/index.php/IPv6#systemd-networkd_2 "IPv6")。
*   在 `[Network]` 段设置 `DHCP=yes` 来同时接收 IPv4 **和** IPv6 DHCP 请求。

#### 使用 DHCP 的有线适配器

 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4
```

#### 使用静态 IP 的有线适配器

 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1
DNS=10.1.10.1
#DNS=8.8.8.8
```

`Address=` 能够被使用多次来指定多个 IPv4 或者 IPv6 地址。 参见 [#network files](#network_files) 或者 [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) 了解更多配置项。

#### 无线适配器

为了能够使用 *systemd-networkd* 连接一个无线网络，需要一个被其他应用，比如 [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") 或 [Iwd](/index.php/Iwd "Iwd")，配置好的无线适配器。

 `/etc/systemd/network/25-wireless.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

如果无线适配器有一个静态地址，它的配置（除了接口的名字）跟有线适配器是一样的。

#### Wired and wireless adapters on the same machine

This setup will enable a DHCP IP for both a wired and wireless connection making use of the metric directive to allow the kernel to decide on-the-fly which one to use. This way, no connection downtime is observed when the wired connection is unplugged.

The kernel's route metric (same as configured with *ip*) decides which route to use for outgoing packets, in cases when several match. This will be the case when both wireless and wired devices on the system have active connections. To break the tie, the kernel uses the metric. If one of the connections is terminated, the other automatically wins without there being a gap with nothing configured (ongoing transfers may still not deal with this nicely but that is at a different OSI layer).

**Note:** The `Metric` option is for static routes while the `RouteMetric` option is for setups not using static routes. See [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) for more details.
 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10
```
 `/etc/systemd/network/25-wireless.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20
```

#### Renaming an interface

Instead of [editing udev rules](/index.php/Network_configuration#Change_interface_name "Network configuration"), a *.link* file can be used to rename an interface. A useful example is to set a predictable interface name for a USB-to-Ethernet adapter based on its MAC address, as those adapters are usually given different names depending on which USB port they are plugged into.

 `/etc/systemd/network/10-ethusb0.link` 
```
[Match]
MACAddress=12:34:56:78:90:ab

[Link]
Description=USB to Ethernet Adapter
Name=ethusb0
```

**Note:** Any user-supplied *.link* **must** have a lexically earlier file name than the default config `99-default.link` in order to be considered at all. For example, name the file `10-ethusb0.link` and not `ethusb0.link`.

## Configuration files

Configuration files are located in `/usr/lib/systemd/network`, the volatile runtime network directory `/run/systemd/network` and the local administration network directory `/etc/systemd/network`. Files in `/etc/systemd/network` have the highest priority.

There are three types of configuration files. They all use a format similar to [systemd unit files](/index.php/Systemd#Writing_unit_files "Systemd").

*   ***.network*** files. They will apply a network configuration for a *matching* device
*   ***.netdev*** files. They will create a *virtual network device* for a *matching* environment
*   ***.link*** files. When a network device appears, [udev](/index.php/Udev "Udev") will look for the first *matching* *.link* file

They all follow the same rules:

*   If **all** conditions in the `[Match]` section are matched, the profile will be activated
*   an empty `[Match]` section means the profile will apply in any case (can be compared to the `*` wildcard)
*   all configuration files are collectively sorted and processed in lexical order, regardless of the directory in which they live
*   files with identical name replace each other

**Tip:**

*   To override a system-supplied file in `/usr/lib/systemd/network` in a permanent manner (i.e even after upgrade), place a file with same name in `/etc/systemd/network` and symlink it to `/dev/null`
*   The `*` wildcard can be used in `VALUE` (e.g `en*` will match any Ethernet device), a boolean can be simple written as `yes` or `no`.
*   Following this [Arch-general thread](https://mailman.archlinux.org/pipermail/arch-general/2014-March/035381.html), the best practice is to setup specific container network settings *inside the container* with **networkd** configuration files.
*   Systemd accepts the values `1, true, yes, on` for a true boolean, and the values `0, false, no, off` for a false boolean

### network files

These files are aimed at setting network configuration variables, especially for servers and containers.

*.network* files have the following sections: `[Match]`, `[Link]`, `[Network]`, `[Address]`, `[Route]`, and `[DHCP]`. Below are commonly configured keys for each section. See [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) for more information and examples.

#### [Match]

*   `MACAddress=` a whitespace-separated list of hardware addresses
*   `Name=` a white-space separated list of device names, which may contain globs (e.g. `en*`). By prefixing with `!`, the list can be inverted.
*   `Host=` the machine hostname
*   `Virtualization=` check whether the system is executed in a virtualized environment or not. A `Virtualization=no` key will only apply on your host machine, while `Virtualization=yes` apply to any container or VM.

#### [Link]

*   `MACAddress=` useful for [MAC address spoofing](/index.php/MAC_address_spoofing#systemd-networkd "MAC address spoofing")
*   `MTUBytes=` setting a larger MTU value (e.g. when using [jumbo frames](/index.php/Jumbo_frames "Jumbo frames")) can significantly speed up your network transfers
*   `Multicast` allow the usage of [multicast](https://en.wikipedia.org/wiki/Multicast_address "wikipedia:Multicast address") on interface(s)

#### [Network]

| Parameter | Description | Accepted Values | Default Value |
| `DHCP=` | Controls DHCPv4 and/or DHCPv6 client support. | boolean, `ipv4`, `ipv6` | `false` |
| `DHCPServer=` | If enabled, a DHCPv4 server will be started. | boolean | `false` |
| `MulticastDNS=` | Enables [multicast DNS](https://tools.ietf.org/html/rfc6762) support. When set to `resolve`, only resolution is enabled, but not host or service registration and announcement. | boolean, `resolve` | `false` |
| `DNSSEC=` | Controls DNSSEC DNS validation support on the link. When set to `allow-downgrade`, compatibility with non-DNSSEC capable networks is increased, by automatically turning off DNSSEC in this case. | boolean, `allow-downgrade` | `false` |
| `DNS=` | Configure static [DNS](/index.php/DNS "DNS") addresses. May be specified more than once. | [`inet_pton`](http://man7.org/linux/man-pages/man3/inet_pton.3.html) |
| `Domains=` | A list of domains which should be resolved using the DNS servers on this link. [more information](https://www.freedesktop.org/software/systemd/man/systemd.network.html#Domains=) | domain name, optionally prefixed with a tilde (`~`) |
| `IPForward=` | If enabled, incoming packets on any network interface will be forwarded to any other interfaces according to the routing table. | boolean, `ipv4`, `ipv6` | `false` |
| `IPv6PrivacyExtensions=` | Configures use of stateless temporary addresses that change over time (see [RFC 4941](https://tools.ietf.org/html/rfc4941)). When `prefer-public`, enables the privacy extensions, but prefers public addresses over temporary addresses. When `kernel`, the kernel's default setting will be left in place. | boolean, `prefer-public`, `kernel` | `false` |

#### [Address]

*   `Address=` this option is **mandatory** unless DHCP is used

#### [Route]

*   `Gateway=` this option is **mandatory** unless DHCP is used
*   `Destination=` the destination prefix of the route, possibly followed by a slash and the prefix length

If `Destination` is not present in `[Route]` section this section is treated as a default route.

**Tip:** You can put the `Address=` and `Gateway=` keys in the `[Network]` section as a short-hand if `[Address]` section contains only an Address key and `[Route]` section contains only a Gateway key.

#### [DHCP]

| Parameter | Description | Accepted Values | Default Value |
| `UseDNS=` | controls whether the DNS servers advertised by the DHCP server are used | boolean | `true` |
| `Anonymize=` | when true, the options sent to the DHCP server will follow the [RFC7844](https://tools.ietf.org/html/rfc7844) (Anonymity Profiles for DHCP Clients) to minimize disclosure of identifying information | boolean | `false` |
| `UseDomains=` | controls whether the domain name received from the DHCP server will be used as DNS search domain. If set to `route`, the domain name received from the DHCP server will be used for routing DNS queries only, but not for searching. This option can sometimes fix local name resolving when using [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") | boolean, `route` | `false` |

### netdev files

These files will create virtual network devices. They have two sections: `[Match]` and `[NetDev]`. Below are commonly configured keys for each section. See [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5) for more information and examples.

#### [Match] section

*   `Host=` the hostname
*   `Virtualization=` check if running in a VM

#### [NetDev] section

Most common keys are:

*   `Name=` the interface name. **mandatory**
*   `Kind=` e.g. *bridge*, *bond*, *vlan*, *veth*, *sit*, etc. **mandatory**

### link files

These files are an alternative to custom udev rules and will be applied by [udev](/index.php/Udev "Udev") as the device appears. They have two sections: `[Match]` and `[Link]`. Below are commonly configured keys for each section. See [systemd.link(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5) for more information and examples.

**Tip:** Use `# udevadm test-builtin net_setup_link /sys/path/to/network/device` to diagnose problems with *.link* files.

#### [Match] section

*   `MACAddress=` the MAC address
*   `Host=` the host name
*   `Virtualization=`
*   `Type=` the device type e.g. vlan

#### [Link] section

*   `MACAddressPolicy=` persistent or random addresses, or
*   `MACAddress=` a specific address

**Note:** the system `/usr/lib/systemd/network/99-default.link` is generally sufficient for most of the basic cases.

## Usage with containers

The service is available with [systemd](https://www.archlinux.org/packages/?name=systemd). You will want to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `systemd-networkd.service` unit on the host and container.

For debugging purposes, it is strongly advised to [install](/index.php/Install "Install") the [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [net-tools](https://www.archlinux.org/packages/?name=net-tools), and [iproute2](https://www.archlinux.org/packages/?name=iproute2) packages.

If you are using [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn"), you may need to modify the `systemd-nspawn@.service` and append boot options to the `ExecStart` line. Please refer to [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1) for an exhaustive list of options.

Note that if you want to take advantage of automatic DNS configuration from DHCP, you need to enable `systemd-resolved` and symlink `/run/systemd/resolve/resolv.conf` to `/etc/resolv.conf`. See [systemd-resolved.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.service.8) for more details.

Before you start to configure your container network, it is useful to:

*   disable all your [netctl](/index.php/Netctl "Netctl") (host and container), [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (host and container), [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") (container only) and `systemd-nspawn@.service` (host only) services to avoid potential conflicts and to ease debugging
*   make sure [packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") is enabled if you want to let containers access the internet. Make sure that your *.network* file does not accidentally turn off forwarding because if you do not have a `IPForward=1` setting in it, `systemd-networkd` will turn off forwarding on this interface, even if you have it enabled globally.
*   make sure you do not have any [iptables](/index.php/Iptables "Iptables") rules which can block traffic
*   when the daemon is started the systemd `networkctl` command displays the status of network interfaces.

For the set-up described below,

*   we will limit the output of the `ip a` command to the concerned interfaces
*   we assume the *host* is your main OS you are booting to and the *container* is your guest virtual machine
*   all interface names and IP addresses are only examples

### Basic DHCP network

This setup will enable a DHCP IP for host and container. In this case, both systems will share the same IP as they share the same interfaces.

 `/etc/systemd/network/*MyDhcp*.network` 
```
[Match]
Name=en*

[Network]
DHCP=ipv4

```

Then, [enable](/index.php/Enable "Enable") and start `systemd-networkd.service` on your container.

You can of course replace `en*` by the full name of your ethernet device given by the output of the `ip link` command.

*   on host and container:

 `$ ip a` 
```
2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.72/24 brd 192.168.1.255 scope global enp7s0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever

```

By default, hostname received from the DHCP server will be used as the transient hostname.

To change it add `UseHostname=false` in section `[DHCPv4]`

 `/etc/systemd/network/*MyDhcp*.network` 
```
[DHCPv4]
UseHostname=false

```

If you did not want to configure a DNS in `/etc/resolv.conf` and want to rely on DHCP for setting it up, you need to [enable](/index.php/Enable "Enable") `systemd-resolved.service` and symlink `/run/systemd/resolve/resolv.conf` to `/etc/resolv.conf`

```
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

See [systemd-resolved.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.service.8) for more details.

**Note:** Users accessing a system partition via `/usr/bin/arch-chroot` from [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), will need to create the symlink outside of the chroot, on the mounted partition. This is due to arch-chroot linking the file to the live environment.

### DHCP with two distinct IP

#### Bridge interface

First, create a virtual bridge interface. We tell systemd to create a device named *br0* that functions as an ethernet bridge.

 `/etc/systemd/network/*MyBridge*.netdev` 
```
[NetDev]
Name=br0
Kind=bridge
```

[Restart](/index.php/Restart "Restart") `systemd-networkd.service` to have systemd create the bridge.

On host and container:

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default 
    link/ether ae:bd:35:ea:0c:c9 brd ff:ff:ff:ff:ff:ff

```

Note that the interface *br0* is listed but is still DOWN at this stage.

#### Bind ethernet to bridge

The next step is to add to the newly created bridge a network interface. In the example below, we add any interface that matches the name *en** into the bridge *br0*.

 `/etc/systemd/network/*bind*.network` 
```
[Match]
Name=en*

[Network]
Bridge=br0
```

The ethernet interface must not have DHCP or an IP address associated as the bridge requires an interface to bind to with no IP: modify the corresponding `/etc/systemd/network/*MyEth*.network` accordingly to remove the addressing.

#### Bridge network

Now that the bridge has been created and has been bound to an existing network interface, the IP configuration of the bridge interface must be specified. This is defined in a third *.network* file, the example below uses DHCP.

 `/etc/systemd/network/*mybridge*.network` 
```
[Match]
Name=br0

[Network]
DHCP=ipv4
```

#### Add option to boot the container

As we want to give a separate IP for host and container, we need to *Disconnect* networking of the container from the host. To do this, add this option `--network-bridge=br0` to your container boot command.

```
# systemd-nspawn --network-bridge=br0 -bD /path_to/my_container

```

#### Result

*   on host

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.87/24 brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever
6: vb-*MyContainer*: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP group default qlen 1000
    link/ether d2:7c:97:97:37:25 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::d07c:97ff:fe97:3725/64 scope link 
       valid_lft forever preferred_lft forever

```

*   on container

 `$ ip a` 
```
2: host0: <BROADCAST,MULTICAST,ALLMULTI,AUTOMEDIA,NOTRAILERS,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 5e:96:85:83:a8:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.73/24 brd 192.168.1.255 scope global host0
       valid_lft forever preferred_lft forever
    inet6 fe80::5c96:85ff:fe83:a85d/64 scope link 
       valid_lft forever preferred_lft forever

```

#### Notice

*   we have now one IP address for `br0` on the host, and one for `host0` in the container
*   two new interfaces have appeared: `vb-*MyContainer*` in the host and `host0` in the container. This comes as a result of the `--network-bridge=br0` option. This option *implies* another option, `--network-veth`. This means a *virtual Ethernet link* has been created between host and container.
*   the DHCP address on `host0` comes from the system `/usr/lib/systemd/network/80-container-host0.network` file.
*   on host

 `$ brctl show` 
```
bridge name	bridge id		STP enabled	interfaces
br0		8000.14dae9b57a88	no		enp7s0
							vb-*MyContainer*

```

the above command output confirms we have a bridge with two interfaces binded to.

*   on host

 `$ ip route` 
```
default via 192.168.1.254 dev br0 
192.168.1.0/24 dev br0  proto kernel  scope link  src 192.168.1.87

```

*   on container

 `$ ip route` 
```
default via 192.168.1.254 dev host0 
192.168.1.0/24 dev host0  proto kernel  scope link  src 192.168.1.73

```

the above command outputs confirm we have activated `br0` and `host0` interfaces with an IP address and Gateway 192.168.1.254\. The gateway address has been automatically grabbed by *systemd-networkd*

 `$ cat /run/systemd/resolve/resolv.conf` 
```
nameserver 192.168.1.254

```

### Static IP network

Setting a static IP for each device can be helpful in case of deployed web services (e.g FTP, http, SSH). Each device will keep the same MAC address across reboots if your system `/usr/lib/systemd/network/99-default.link` file has the `MACAddressPolicy=persistent` option (it has by default). Thus, you will easily route any service on your Gateway to the desired device.

The following configuration needs to be done for this setup:

*   on host

The configuration is very similar to that of [#DHCP with two distinct IP](#DHCP_with_two_distinct_IP). First, a virtual bridge interface needs to be created and the main physical interface needs to be bound to it. This task can be accomplished with the following two files, with contents equal to those available at the DHCP section.

```
/etc/systemd/network/*MyBridge*.netdev
/etc/systemd/network/*MyEth*.network

```

Next, you need to configure the IP and DNS of the newly created virtual bridge interface. The following *MyBridge*.network provides an example configuration:

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DNS=192.168.1.254
Address=192.168.1.87/24
Gateway=192.168.1.254

```

*   on container

First, we shall get rid of the system `/usr/lib/systemd/network/80-container-host0.network` file, which provides a DHCP configuration for the default network interface of the container. To do it in a permanent way (e.g. even after [systemd](https://www.archlinux.org/packages/?name=systemd) upgrades), do the following on the container. This will mask the file `/usr/lib/systemd/network/80-container-host0.network` since files of the same name in `/etc/systemd/network` take priority over `/usr/lib/systemd/network`. Keep in mind that this file can be kept if you only want a static IP on the host, and want the IP address of your containers to be assigned via DHCP.

```
# ln -sf /dev/null /etc/systemd/network/80-container-host0.network

```

Then, configure an static IP for the default `host0` network interface and [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-networkd.service` on your container. An example configuration is provided below:

 `/etc/systemd/network/*MyVeth*.network` 
```
[Match]
Name=host0

[Network]
DNS=192.168.1.254
Address=192.168.1.94/24
Gateway=192.168.1.254

```

## Interface and desktop integration

*systemd-networkd* does not have a proper interactive management interface neither via command-line nor graphical. Still, some tools are available to either display the current state of the network, receive notifications or interact with the wireless configuration:

*   *networkctl* (via CLI) offers a simple dump of the network interface states.

*   When *networkd* is configured with [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), both *wpa_cli* and *wpa_gui* offer the ability to associate and configure WLAN interfaces dynamically.

*   [networkd-notify-git](https://aur.archlinux.org/packages/networkd-notify-git/) can generate simple notifications in response to network interface state changes (such as connection/disconnection and re-association).

*   The [networkd-dispatcher](https://aur.archlinux.org/packages/networkd-dispatcher/) daemon allows executing scripts in response to network interface state changes, similar to *NetworkManager-dispatcher*.

*   As for the DNS resolver *systemd-resolved*, information about current DNS servers can be visualized with `resolvectl status`.

## Troubleshooting

### Mount services at boot fail

If running services like [Samba](/index.php/Samba "Samba")/[NFS](/index.php/NFS "NFS") which fail if they are started before the network is up, you may want to [enable](/index.php/Enable "Enable") the `systemd-networkd-wait-online.service`. This is, however, rarely necessary because most networked daemons start up okay, even if the network has not been configured yet.

### systemd-resolve not searching the local domain

[systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") may not search the local domain when given just the hostname, even when `UseDomains=yes` or `Domains=[domain-list]` is present in the appropriate *.network* file, and that file produces the expected `search [domain-list]` in `resolv.conf`. You can run `networkctl status` or `resolvectl status` to check if the search domains are actually being picked up.

Possible workarounds:

*   Disable [LLMNR](/index.php/Systemd-resolved#LLMNR "Systemd-resolved") to let *systemd-resolved* immediately continue with appending the DNS suffixes
*   Trim `/etc/nsswitch.conf`'s `hosts` database (e.g., by removing `[!UNAVAIL=return]` option after `resolve` service)
*   Switch to using fully-qualified domain names
*   Use `/etc/hosts` to resolve hostnames
*   Fall back to using glibc's `dns` instead of using systemd's `resolve`

### Connected second PC unable to use bridged LAN

First PC have two LAN. Second PC have one LAN and connected to first PC. Lets go second PC to give all access to LAN after bridged interface:

```
# sysctl net.bridge.bridge-nf-filter-pppoe-tagged=0
# sysctl net.bridge.bridge-nf-filter-vlan-tagged=0
# sysctl net.bridge.bridge-nf-call-ip6tables=0
# sysctl net.bridge.bridge-nf-call-iptables=0
# sysctl net.bridge.bridge-nf-call-arptables=0

```

## See also

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)