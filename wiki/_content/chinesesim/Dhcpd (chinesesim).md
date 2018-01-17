Related articles

*   [dhcpcd (简体中文)](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)")

**翻译状态：** 本文是英文页面 [Dhcpd](/index.php/Dhcpd "Dhcpd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-14，点击[这里](https://wiki.archlinux.org/index.php?title=Dhcpd&diff=0&oldid=472034)可以查看翻译后英文页面的改动。

dhcpd is the [Internet Systems Consortium](http://www.isc.org/downloads/dhcp/) DHCP Server. It is useful for instance on a machine acting as a router on a LAN.

**注意:** *dhcpd* (DHCP **(server)** daemon) is not the same as [dhcpcd](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") (DHCP **client** daemon).

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 只侦听单一网口](#.E5.8F.AA.E4.BE.A6.E5.90.AC.E5.8D.95.E4.B8.80.E7.BD.91.E5.8F.A3)
        *   [3.1.1 配置 dhcpd](#.E9.85.8D.E7.BD.AE_dhcpd)
        *   [3.1.2 服务文件](#.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
    *   [3.2 用于 PXE](#.E7.94.A8.E4.BA.8E_PXE)

## 安装

[Install](/index.php/Install "Install") the [dhcp](https://www.archlinux.org/packages/?name=dhcp) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

## 使用

*dhcpd* includes a unit file `dhcpd4.service`, which can be used to [control](/index.php/Enable "Enable") the daemon. It starts the daemon for *all* [network interfaces](/index.php/Network_interfaces "Network interfaces"). See [#Listening on only one interface](#Listening_on_only_one_interface) for alternative.

## 配置

Assign a static IPv4 address to the interface you want to use (in our examples we will use `eth0`). The first 3 bytes of this address cannot be exactly the same as those of another interface.

```
# ip link set up dev eth0
# ip addr add 139.96.30.100/24 dev eth0 # arbitrary address

```

**提示：** Usually, the one of next three subnets is used for private networks, which are specially reserved and won't conflict with any host in the Internet:

*   `192.168/16` (subnet `192.168.0.0`, netmask `255.255.0.0`)
*   `172.16/12` (subnet `172.16.0.0`, netmask `255.240.0.0`)
*   `10/8` (for large networks; subnet `10.0.0.0`, netmask `255.0.0.0`)

See also [RFC 1918](http://www.ietf.org/rfc/rfc1918.txt).

To have your static ip assigned at boot, see [Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration").

The default `dhcpd.conf` contains many uncommented examples, so relocate it:

```
# mv /etc/dhcpd.conf /etc/dhcpd.conf.example

```

The minimal configuration file may look like:

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;
}

```

If you need to provide a fixed IP address for a single specific device, you can use the following syntax

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;

  host macbookpro{
   hardware ethernet 70:56:81:22:33:44;
   fixed-address 139.96.30.199;
  }
}

```

`domain-name-servers` option contains addresses of DNS servers which are supplied to clients. In our example we are using Google's public DNS servers. If you know a local DNS servers (for example, provided by your ISP), you should use it. If you've configured your own DNS on a local machine, then use its address in your subnet (e. g. `139.96.30.100` in our example).

`subnet-mask` and `routers` defines a subnet mask and a list of available routers on the subnet. In most cases for small networks you can use `255.255.255.0` as a mask and specify an IP address of the machine on which you're configuring DHCP server as a router.

`subnet` blocks defines options for separate subnets, which are mapped to the network interfaces on which *dhcpd* is running. In our example this is one subnet `139.96.30.0/24` for single interface `eth0`, for which we defined the range of available IP addresses. Addresses from this range will be assigned to the connecting clients.

### 只侦听单一网口

If your computer is already part of one or several networks, it could be a problem if your computer starts giving ip addresses to machines from the other networks. It can be done by either configuring dhcpd or starting it as a daemon with [systemctl](/index.php/Systemd#Using_units "Systemd").

#### 配置 dhcpd

In order to exclude an interface, you must create an empty declaration for the subnet that will be configured on that interface.

This is done by editing the configuration file (for example):

 `/etc/dhcpd.conf` 
```
# No DHCP service in DMZ network (192.168.2.0/24)
subnet 192.168.2.0 netmask 255.255.255.0 {
}

```

#### 服务文件

There is no service files provided by default to use *dhcpd* only on one interface so you need to create one:

 `/etc/systemd/system/dhcpd4@.service` 
```
[Unit]
Description=IPv4 DHCP server on %I
Wants=network.target
After=network.target

[Service]
Type=forking
PIDFile=/run/dhcpd4.pid
ExecStart=/usr/bin/dhcpd -4 -q -pf /run/dhcpd4.pid %I
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target

```

This is a template unit, which binds it to a particular interface, for example `dhcpd4@*eth0*.service` where *eth0* is an interface shown with `ip link`.

### 用于 PXE

PXE Configuration is done with the following two options:

 `/etc/dhcpd.conf` 
```
next-server 192.168.0.2;
filename "/pxelinux.0";

```

This section can either be in an entire `subnet` or just in a `host` definition. `next-server` is the IP of the TFTP Server, and `filename` is the filename of the image to boot. For more information see [PXE](/index.php/PXE "PXE").