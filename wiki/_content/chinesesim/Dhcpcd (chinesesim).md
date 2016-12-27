**翻译状态：** 本文是英文页面 [Dhcpcd](/index.php/Dhcpcd "Dhcpcd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-12-26，点击[这里](https://wiki.archlinux.org/index.php?title=Dhcpcd&diff=0&oldid=460097)可以查看翻译后英文页面的改动。

*dhcpcd* is a DHCP and DHCPv6 client. It is currently the most feature-rich open source DHCP client, see the [home page](http://roy.marples.name/projects/dhcpcd/) for the full list of features.

**提示：** *dhcpcd* (DHCP **client** daemon) is not the same as [dhcpd](/index.php/Dhcpd "Dhcpd") (DHCP **(server)** daemon).

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行](#.E8.BF.90.E8.A1.8C)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 DHCP 静态路由](#DHCP_.E9.9D.99.E6.80.81.E8.B7.AF.E7.94.B1)
    *   [3.2 DHCP 客户端标识](#DHCP_.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.A0.87.E8.AF.86)
    *   [3.3 禁用 ARP 检测以加速 DHCP](#.E7.A6.81.E7.94.A8_ARP_.E6.A3.80.E6.B5.8B.E4.BB.A5.E5.8A.A0.E9.80.9F_DHCP)
    *   [3.4 静态配置文件](#.E9.9D.99.E6.80.81.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
        *   [3.4.1 Fallback 配置文件](#Fallback_.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
*   [4 钩子](#.E9.92.A9.E5.AD.90)
    *   [4.1 10-wpa_supplicant](#10-wpa_supplicant)
*   [5 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [5.1 移除旧的 DHCP 租约](#.E7.A7.BB.E9.99.A4.E6.97.A7.E7.9A.84_DHCP_.E7.A7.9F.E7.BA.A6)
    *   [5.2 多重时引导使用不同 IP](#.E5.A4.9A.E9.87.8D.E6.97.B6.E5.BC.95.E5.AF.BC.E4.BD.BF.E7.94.A8.E4.B8.8D.E5.90.8C_IP)
*   [6 排错](#.E6.8E.92.E9.94.99)
    *   [6.1 客户端 ID](#.E5.AE.A2.E6.88.B7.E7.AB.AF_ID)
    *   [6.2 检查 DHCP 问题时首先释放 IP](#.E6.A3.80.E6.9F.A5_DHCP_.E9.97.AE.E9.A2.98.E6.97.B6.E9.A6.96.E5.85.88.E9.87.8A.E6.94.BE_IP)
    *   [6.3 不匹配的路由](#.E4.B8.8D.E5.8C.B9.E9.85.8D.E7.9A.84.E8.B7.AF.E7.94.B1)
    *   [6.4 dhcpcd 和 systemd 网络接口](#dhcpcd_.E5.92.8C_systemd_.E7.BD.91.E7.BB.9C.E6.8E.A5.E5.8F.A3)
    *   [6.5 超时延迟](#.E8.B6.85.E6.97.B6.E5.BB.B6.E8.BF.9F)
*   [7 参阅](#.E5.8F.82.E9.98.85)

## 安装

The [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) package is available to be [installed](/index.php/Install "Install"). It is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group, so it is likely already installed on your system.

You might be interested in [dhcpcd-ui](https://aur.archlinux.org/packages/dhcpcd-ui/), which is a [GTK+](/index.php/GTK%2B "GTK+") frontend for the *dhcpcd* daemon (and optionally [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")). It features a configuration dialogue and the ability to enter a pass phrase for wireless networks.

## 运行

*dhcpcd* includes two unit files which can be used to [control](/index.php/Enable "Enable") the daemon:

*   `dhcpcd.service` starts the daemon for *all* [network interfaces](/index.php/Network_interfaces "Network interfaces");
*   the template unit `dhcpcd@.service` binds it to a particular interface, for example `dhcpcd@*interface*.service` where *interface* is an interface shown with `ip link`.

Using the template unit is recommended; see [#dhcpcd and systemd network interfaces](#dhcpcd_and_systemd_network_interfaces) for details.

To start *dhcpcd* manually, run the following command:

 `# dhcpcd *eth0*` 
```
dhcpcd: version 5.1.1 starting
dhcpcd: *eth0*: broadcasting for a lease
...
dhcpcd: *eth0*: leased 192.168.1.70 for 86400 seconds

```

## 配置

The main configuration is done in `/etc/dhcpcd.conf`, see [dhcpcd.conf(5)](http://roy.marples.name/man/html5/dhcpcd.conf.html) for details. Some of the frequently used options are highlighted below.

### DHCP 静态路由

If you need to add a static route client-side, create a new dhcpcd hook-script in `/usr/lib/dhcpcd/dhcpcd-hooks`. The example shows a new hook-script which adds a static route to a VPN subnet on `10.11.12.0/24` via a gateway machine at `192.168.192.5`:

 `/usr/lib/dhcpcd/dhcpcd-hooks/40-vpnroute` 
```
ip route add 10.11.12.0/24 via 192.168.192.5

```

The `40` prefix means that it is the final hook-script to run when dhcpcd starts.

### DHCP 客户端标识

The DHCP client may be uniquely identified in different ways by the server:

1.  hostname (or the hostname value sent by the client),
2.  MAC address of the network interface controller through which the connection is being made, linked to this is the third,
3.  Identity Association ID (IAID), which is an abstraction layer to differentiate different use-cases and/or interfaces on a single host,
4.  DHCP Unique Identifier (DUID).

For a further description, see [RFC 3315](https://tools.ietf.org/html/rfc3315#section-4.2).

It depends on the DHCP-server configuration which options are optional or required to request a DHCP IP lease.

**提示：** The *dhcpcd* default configuration should be sufficient usually. The listed identifiers are determined automatically and manual configuration changes only be required in case of problems.

If the *dhcpcd* default configuration fails to obtain an IP, the following options are available to use in `dhcpcd.conf`:

*   `hostname` sends the hostname set in `/etc/hostname`
*   `clientid` sends the MAC address as identifier
*   `iaid <interface>` derives the IAID to use for DHCP discovery. It has to be used in an interface block (started by `interface <interface>`, see [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1388376#p1388376)), but more frequently the next option is used:
*   `duid` triggers using a combination of DUID and IAID as identifier.

The DUID value is set in `/etc/dhcpcd.duid`. For efficient DHCP lease operation it is important that it is unique for the system and applies to all network interfaces alike, while the IAID represents an identifier for each of the systems' interfaces (see [RFC 4361](http://tools.ietf.org/html/rfc4361#section-6.1)).

Care must be taken on a network running [Dynamic DNS](https://en.wikipedia.org/wiki/Dynamic_DNS "wikipedia:Dynamic DNS") to ensure that all three IDs are unique. If duplicate DUID values are presented to the DNS server, e.g. in the case where a virtual machine has been cloned and the hostname and MAC have been made unique but the DUID has not been changed, then the result will be that as each client with the duplicated DUID requests a lease the server will remove the predecessor from the DNS record.

### 禁用 ARP 检测以加速 DHCP

*dhcpcd* contains an implementation of a recommendation of the DHCP standard ([RFC2131](http://www.ietf.org/rfc/rfc2131.txt) section 2.2) to check via ARP if the assigned IP address is really not taken. This seems mostly useless in home networks, so you can save about 5 seconds on every connect by adding the following line to `/etc/dhcpcd.conf`:

```
noarp

```

This is equivalent to passing `--noarp` to `dhcpcd`, and disables the described ARP probing, speeding up connections to networks with DHCP.

### 静态配置文件

Required settings are explained in [Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration"). These typically include the [device name](/index.php/Network_configuration#Device_names "Network configuration"), *IP address*, *router address*, and *name server*.

Configure a static profile for *dhcpcd* in `/etc/dhcpcd.conf`, for example:

 `/etc/dhcpcd.conf` 
```
interface eth0
static ip_address=192.168.0.10/24	
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8.8
```

More complicated configurations are possible, for example combining with the `arping` option. See [dhcpcd.conf(5)](http://roy.marples.name/man/html5/dhcpcd.conf.html) for details.

#### Fallback 配置文件

It is possible to configure a static profile within *dhcpcd* and fall back to it when DHCP lease fails. This is useful particularly for [headless machines](https://en.wikipedia.org/wiki/Headless_computer "wikipedia:Headless computer") such as [Raspberry Pi](/index.php/Raspberry_Pi "Raspberry Pi"), where the static profile can be used as "recovery" profile to ensure that it is always possible to connect to the machine.

The following example configures a `static_eth0` profile with `192.168.1.23` as IP address, `192.168.1.1` as gateway and name server, and makes this profile fallback for interface `eth0`.

 `/etc/dhcpcd.conf` 
```
# define static profile
profile static_eth0
static ip_address=192.168.1.23/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1

# fallback to static profile on eth0
interface *eth0*
fallback static_eth0
```

## 钩子

*dhcpcd* executes all scripts found in `/usr/lib/dhcpcd/dhcpcd-hooks/` in a lexical order. See [dhcpcd(5)](http://roy.marples.name/man/html5/dhcpcd.conf.html) and [dhcpcd-run-hooks(8)](http://roy.marples.name/man/html8/dhcpcd-run-hooks.html) for details.

**提示：**

*   Each script can be disabled using the `nohook` option in `dhcpcd.conf`.
*   The `env` option can be used to set an environment variable for **all** hooks. For example, you can force the hostname hook to always set the hostname with `env force_hostname=YES`.

### 10-wpa_supplicant

创建一个符号链接以激活这个钩子（即便包已更新也应先确认在用版本为最新版）：

```
# ln -s /usr/share/dhcpcd/hooks/10-wpa_supplicant /usr/lib/dhcpcd/dhcpcd-hooks/

```

**提示：** 从 [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)-6.10.0-1 版开始，钩子默认不再自动激活，参阅 [[2]](http://roy.marples.name/projects/dhcpcd/info/5d7b3cbea2808602), [[3]](http://roy.marples.name/projects/dhcpcd/info/28fd82a29a6d54ad), [[4]](http://roy.marples.name/projects/dhcpcd/info/9b0662ecd9a8b839).

`10-wpa_supplicant` 这个钩子一旦激活，它将在满足下列条件时自动加载相应无线网络接口的 [WPA supplicant](/index.php/WPA_supplicant_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "WPA supplicant (简体中文)")：

*   当前没有 *wpa_supplicant* 进程侦听该接口；
*   存在某个 *wpa_supplicant* 配置文件。*dhcpcd* 将检查下列文件：

```
/etc/wpa_supplicant/wpa_supplicant-*interface*.conf
/etc/wpa_supplicant/wpa_supplicant.conf
/etc/wpa_supplicant-*interface*.conf
/etc/wpa_supplicant.conf

```

上列为默认检查顺序，但可以向 `/etc/dhcpcd.conf` 中添加 `env wpa_supplicant_conf=*<配置文件路径>*` 配置项以自定义搜索路径。

**提示：** 钩子在找到第一个配置文件后将停止搜索，因此当存在多个*wpa_supplicant* 配置文件时应做出适当安排，否则 *dhcpcd* 可能使用非预期的错误文件。

如果同时还用 *wpa_supplicant* 自身管理无线网络连接，钩子会创建非预期的连接。例如，如果你停用了 *wpa_supplicant* ，钩子会再次启动接口。还有，如果使用[自动切换配置](/index.php/Netctl_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.87.AA.E5.8A.A8.E5.88.87.E6.8D.A2.E9.85.8D.E7.BD.AE "Netctl (简体中文)")，*wpa_supplicant* 将使用 `/run/network/wpa_supplicant_*interface*.conf` 配置文件自动启动，因此不仅没必要用钩子再次启动它，而且会导致引导时解析 `/etc/wpa_supplicant/wpa_supplicant.conf` 文件错误，因其只包含默认包版本的范例配置。

在 `dhcpcd.conf` 中添加 `nohook wpa_supplicant` 可禁用钩子。

## 提示与技巧

### 移除旧的 DHCP 租约

The file `/var/lib/dhcpcd/dhcpcd-*interface*.lease`, where `*interface*` is the name of the interface on which you have a lease, contains the actual DHCP lease reply sent by the DHCP server. It is used to determine the last lease from the server, and its `mtime` attribute is used to determine when it was issued. This last lease information is then used to request the same IP address previously held on a network, if it is available. If you do not want that, simply delete this file.

If the DHCP server still assigns the same IP address, this may happen because it is configured to keep the assignment stable and recognizes the requesting DHCP client id or DUID (see [#DHCP Client Identifier](#DHCP_Client_Identifier)). You can test it by stopping *dhcpcd* and removing or renaming `/etc/dhcpcd.duid`. *dhcpcd* will generate a new one on next run.

Keep in mind that the DUID is intended as persistent machine identifier across reboots and interfaces. If you are transferring the system to new computer, preserving this file should make it appear as old one.

### 多重时引导使用不同 IP

If you are dualbooting Arch and OS X or Windows and want each to receive different IP addresses, you can exert control about the IPs leased by specifying a different DUID in each operating system installation.

In Windows (post XP) the DUID should be stored in the

```
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Dhcpv6DUID 

```

registry key.

On OS X it is directly accessible in `Network\adapter\dhcp preferences panel`.

If you are using a [dnsmasq](/index.php/Dnsmasq "Dnsmasq") DHCP server, the different DUIDs can be used in appropriate `dhcp-host=` rules in its configuration.

## 排错

### 客户端 ID

If you are on a network with DHCPv4 that filters Client IDs based on MAC addresses, you may need to change the following line:

 `/etc/dhcpcd.conf` 
```
# Use the same DUID + IAID as set in DHCPv6 for DHCPv4 Client ID as per RFC4361\. 
duid

```

To:

 `/etc/dhcpcd.conf` 
```
# Use the hardware address of the interface for the Client ID (DHCPv4).
clientid

```

Else, you may not obtain a lease since the DHCP server may not read your [DHCPv6-style](https://en.wikipedia.org/wiki/DHCPv6 "wikipedia:DHCPv6") Client ID correctly. See [RFC 4361](http://tools.ietf.org/html/rfc4361) for more information.

### 检查 DHCP 问题时首先释放 IP

A problem may occur when DHCP gets a wrong IP assignment, such as when two routers are tied together through a VPN. The router that is connected through the VPN may be assigning IP address. To fix it, as root, release the IP address:

```
# dhcpcd -k

```

Then request a new one:

```
# dhcpcd

```

You may have to run those two commands many times.

### 不匹配的路由

For some (noncompliant) routers, you will not be able to connect properly unless you comment the line

```
require dhcp_server_identifier

```

in `/etc/dhcpcd.conf`. This should not cause issues unless you have multiple DHCP servers on your network (not typical); see [this page](http://technet.microsoft.com/en-us/library/cc977442.aspx) for more information.

### dhcpcd 和 systemd 网络接口

`dhcpcd.service` can be [enabled](/index.php/Enabled "Enabled") without specifying an interface. This may, however, create a race condition at boot with *systemd-udevd* trying to apply a predictable network interface name:

```
error changing net interface name wlan0 to wlp4s0: Device or resource busy" 

```

To avoid it, enable *dhcpcd* per interface it should bind to as described in [#Running](#Running). The downside of the template unit is, however, that it does not support hot-plugging of a wired connection and will fail if the network cable is not connected. To work-around the failure, see [#Timeout delay](#Timeout_delay).

### 超时延迟

If *dhcpcd* operates on a single interface and fails to obtain a lease after 30 seconds (for example when the server is not ready or the cable not plugged), it will exit with an error.

To have *dhcpcd* wait indefinitely for one-time, set the `timeout` option to `0`:

 `/etc/systemd/system/dhcpcd@.service.d/timeout.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dhcpcd -w -q **-t 0** %I
```

To have it wait indefinetely, let the unit restart after it exited:

 `/etc/systemd/system/dhcpcd@.service.d/dhcpcdrestart.conf` 
```
[Service]
Restart=always
```

After making changes, [reload the configuration](/index.php/Systemd#Editing_provided_units "Systemd").

## 参阅

*   [dhcpcd(8)](http://roy.marples.name/man/html8/dhcpcd.html)
*   [dhcpcd.conf(5)](http://roy.marples.name/man/html5/dhcpcd.conf.html)