Related articles

*   [dhcpcd (简体中文)](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)")

**翻译状态：** 本文是英文页面 [Dhcpd](/index.php/Dhcpd "Dhcpd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-14，点击[这里](https://wiki.archlinux.org/index.php?title=Dhcpd&diff=0&oldid=472034)可以查看翻译后英文页面的改动。

dhcpd 是 [Internet Systems Consortium](http://www.isc.org/downloads/dhcp/) DHCP 的服务，它被用作局域网环境中的路由管理。

**注意:** *dhcpd* (DHCP **(server)** daemon) 不是 [dhcpcd](/index.php/Dhcpcd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dhcpcd (简体中文)") (DHCP **client** daemon).

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 只侦听单一网口](#.E5.8F.AA.E4.BE.A6.E5.90.AC.E5.8D.95.E4.B8.80.E7.BD.91.E5.8F.A3)
        *   [3.1.1 配置 dhcpd](#.E9.85.8D.E7.BD.AE_dhcpd)
        *   [3.1.2 服务文件](#.E6.9C.8D.E5.8A.A1.E6.96.87.E4.BB.B6)
    *   [3.2 用于 PXE](#.E7.94.A8.E4.BA.8E_PXE)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [dhcp](https://www.archlinux.org/packages/?name=dhcp) 包，其位于[official repositories](/index.php/Official_repositories "Official repositories")。

## 使用

*dhcpd* 包括一个`dhcpd4.service`的单元文件, 可用于创建守护进程. It starts the daemon for *all* [network interfaces](/index.php/Network_interfaces "Network interfaces"). 可查看 [#只侦听单一网口](#.E5.8F.AA.E4.BE.A6.E5.90.AC.E5.8D.95.E4.B8.80.E7.BD.91.E5.8F.A3) 了解单一网口配置。

## 配置

Assign a static IPv4 address to the interface you want to use (in our examples we will use `eth0`). The first 3 bytes of this address cannot be exactly the same as those of another interface.

```
# ip link set up dev eth0
# ip addr add 139.96.30.100/24 dev eth0 # arbitrary address

```

**提示：** 通常有三个预留的网段用于私有网络，它们不会与任何互联网中的主机发生冲突:

*   `192.168/16` (subnet `192.168.0.0`, netmask `255.255.0.0`)
*   `172.16/12` (subnet `172.16.0.0`, netmask `255.240.0.0`)
*   `10/8` (for large networks; subnet `10.0.0.0`, netmask `255.0.0.0`)

查阅 [RFC 1918](http://www.ietf.org/rfc/rfc1918.txt).

要在引导时分配静态IP地址，查看 [Network configuration#Static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration")。

默认的`dhcpd.conf` 文件包含许多注释的例子，复制一份该文件:

```
# mv /etc/dhcpd.conf /etc/dhcpd.conf.example

```

最精简的配置文件如下：

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;
}

```

如果你要为设备提供一个固定的IP地址，可使用以下语法：

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

`domain-name-servers` 选项包含提供给客户的DNS服务器地址，这个例子中使用了谷歌公共DNS服务器。如果你知道一个本地的DNS服务器 (例如服务商提供的)，那么你应该使用这个更DNS。如果DNS服务器部署在本地设备上，应该使用子网络中的地址(如 `139.96.30.100` )。

`subnet-mask` and `routers` defines a subnet mask and a list of available routers on the subnet. In most cases for small networks you can use `255.255.255.0` as a mask and specify an IP address of the machine on which you're configuring DHCP server as a router.

`subnet` blocks defines options for separate subnets, which are mapped to the network interfaces on which *dhcpd* is running. In our example this is one subnet `139.96.30.0/24` for single interface `eth0`, for which we defined the range of available IP addresses. Addresses from this range will be assigned to the connecting clients.

### 只侦听单一网口

如果你的计算机已经时一个或多个网络中的一部分，你的计算机从其他网络获取ip地址可能会有问题。它可以从配置好了的dhcpd服务或者使用或者使用[systemctl](/index.php/Systemd#Using_units "Systemd")的dhcp守护进程上获取。

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