Related articles

*   [iptables](/index.php/Iptables "Iptables")

**翻译状态：** 本文是英文页面 [Nftables](/index.php/Nftables "Nftables") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-04-17，点击[这里](https://wiki.archlinux.org/index.php?title=Nftables&diff=0&oldid=571364)可以查看翻译后英文页面的改动。

[nftables](http://netfilter.org/projects/nftables/) 是一个netfilter项目，旨在替换现有的{ip,ip6,arp,eb}tables框架，为{ip,ip6}tables提供一个新的包过滤框架、一个新的用户空间实用程序（nft）和一个兼容层。它使用现有的钩子、链接跟踪系统、用户空间排队组件和netfilter日志子系统。

它由三个主要组件组成：内核实现、libnl netlink通信和nftables用户空间前端。 内核提供了一个netlink配置接口以及运行时规则集评估，libnl包含了与内核通信的基本函数，nftables前端是用户通过nft交互。

您还可以访问[nftables官方wiki页面](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page)获取更多信息。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 用法](#用法)
*   [3 配置](#配置)
    *   [3.1 表（Tables）](#表（Tables）)
        *   [3.1.1 创建表](#创建表)
        *   [3.1.2 列出表](#列出表)
        *   [3.1.3 列出表中的链和规则](#列出表中的链和规则)
        *   [3.1.4 删除表](#删除表)
        *   [3.1.5 清空表](#清空表)
    *   [3.2 链（Chains）](#链（Chains）)
        *   [3.2.1 创建链](#创建链)
            *   [3.2.1.1 常规链](#常规链)
            *   [3.2.1.2 基本链](#基本链)
        *   [3.2.2 列出规则](#列出规则)
        *   [3.2.3 编辑链](#编辑链)
        *   [3.2.4 删除链](#删除链)
        *   [3.2.5 清空链中的规则](#清空链中的规则)
    *   [3.3 规则（Rules）](#规则（Rules）)
        *   [3.3.1 添加规则](#添加规则)
            *   [3.3.1.1 表达式](#表达式)
        *   [3.3.2 删除](#删除)
    *   [3.4 自动重载](#自动重载)
*   [4 配置示例](#配置示例)
    *   [4.1 工作站](#工作站)
    *   [4.2 简单的IPv4/IPv6防火墙](#简单的IPv4/IPv6防火墙)
    *   [4.3 IPv4/IPv6防火墙限流](#IPv4/IPv6防火墙限流)
    *   [4.4 跳转](#跳转)
    *   [4.5 不同接口采用不同规则](#不同接口采用不同规则)
    *   [4.6 Masquerading](#Masquerading)
*   [5 提示和技巧](#提示和技巧)
    *   [5.1 简单可用的防火墙](#简单可用的防火墙)
        *   [5.1.1 单一计算机](#单一计算机)
    *   [5.2 防止暴力攻击](#防止暴力攻击)
*   [6 参考](#参考)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")用户空间实用程序包[nftables](https://www.archlinux.org/packages/?name=nftables)或者git版本[nftables-git](https://aur.archlinux.org/packages/nftables-git/)。

**提示：** 大部分[iptables前端](/index.php/Iptables#Front-ends "Iptables")没有直接或间接支持nftables，但可以导入到其中。[[1]](https://www.spinics.net/lists/netfilter/msg58215.html) [firewalld](/index.php/Firewalld "Firewalld")是一个同时支持nftables和iptables的图形前端。[[2]](https://firewalld.org/2018/07/nftables-backend)

## 用法

*nftables*区分命令行输入的临时规则和从文件加载或保存到文件的永久规则。 默认配置文件是`/etc/nftables.conf`，其中已经包含一个名为"inet filter"的简单ipv4/ipv6防火墙列表。

[start/enable](/index.php/Start/enable "Start/enable") `nftables.service`。

检查规则集：

```
# nft list ruleset

```

**注意:** 要使systemd服务正确运行，可能需要创建包含nftables所有相关模块的`/etc/modules-load.d/nftables.conf`文件。可以用以下命令获取模块列表： `$ lsmod | grep '^nf'` 否则，可能会出现错误： `Error: Could not process rule: No such file or directory`

## 配置

nftables的用户空间实用程序*nft*评估大多数规则集并传递到内核。规则存储在链中，链存储在表中。以下部分说明如何创建和修改这些结构。

以下所有更改都是临时的。要永久更改，请见规则集保存到`nftables.service`加载的`/etc/nftables.conf`中：

```
# nft list ruleset > /etc/nftables.conf

```

**注意:**

*   `nft list`不输出变量的定义，如果在`/etc/nftables.conf`中有任何变量定义将会丢失。规则中使用的变量将替换为其变量值。
*   `nft list ruleset`在nftables v0.7 （Scrooge McDuck）在同时使用ICMP和ICMPv6时有语法限制。如果导出用作新的规则集将会导致错误。有关信息和解决方案，请参阅 [stackexchange post](https://unix.stackexchange.com/questions/408497/nftables-configuration-error-conflicting-protocols-specified-inet-service-v-i?rq=1)。

要从文件读取输入，请使用`-f`参数：

```
# nft -f *filename*

```

注意，任何已加载的规则不会自动清空。

有关命令的完整列表，参见[nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)。

### 表（Tables）

表包含[#链](#链)。与iptables中的表不同，nftables中没有内置表。表的数量和名称由用户决定。但是，每个表只有一个地址簇，并且只适用于该簇的数据包。表可以指定五个簇中的一个：

| nftables簇 | iptables实用程序 |
| ip | iptables |
| ip6 | ip6tables |
| inet | iptables和ip6tables |
| arp | arptables |
| bridge | ebtables |

`ip`（即IPv4）是默认簇，如果未指定簇，则使用该簇。

要创建同时适用于IPv4和IPv6的规则，请使用`inet`。`inet`允许统一`ip`和`ip6`簇，以便更容易地定义规则。

**注意:** `inet`不能用于`nat`类型的链，只能用于`filter`类型的链。（[source](http://www.spinics.net/lists/netfilter/msg56411.html)）

有关地址簇的完整描述，请参见[nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)中的`ADDRESS FAMILIES`章节。

在以下情况中，`*family*`是可选的，如果未指定则设为`ip`。

#### 创建表

创建一个新的表：

```
# nft add table *family* *table*

```

#### 列出表

列出所有表：

```
# nft list tables

```

#### 列出表中的链和规则

列出指定表中的所有链和规则：

```
# nft list table *family* *table*

```

例如，要列出`inet`簇中`filter`表中的所有规则：

```
# nft list table inet filter

```

#### 删除表

删除一个表：

```
# nft delete table *family* *table*

```

只能删除不包含链的表。

#### 清空表

要清空一个表中的所有规则：

```
# nft flush table *family* *table*

```

### 链（Chains）

链的目的是保存[#规则](#规则)。与iptables中的链不同，nftables没有内置链。这意味着与iptables不同，如果链没有使用netfilter框架中的任何类型或钩子，则流经这些链的数据包不会被nftables触及。

链有两种类型。*基本*链是来自网络栈的数据包的入口点，其中指定了钩子值。*常规*链可以作为更好地处理的跳转目标。

在以下情况中，`*family*`是可选的，如果未指定则设为`ip`。

#### 创建链

##### 常规链

将名为`*chain*`的常规链添加到名为`*table*`的表中：

```
# nft add chain *family* *table* *chain*

```

例如，将名为`tcpchain`的常规链添加到`inet`簇中名为`filter`的表中：

```
# nft add chain inet filter tcpchain

```

##### 基本链

添加基本链，需要指定钩子和优先级值：

```
# nft add chain *family* *table* *chain* { type *type* hook *hook* priority *priority* \; }

```

`*type*`可以是`filter`、`route`或者`nat`。

IPv4/IPv6/Inet地址簇中，`*hook*`可以是`prerouting`、`input`、`forward`、`output`或者`postrouting`。其他地址簇中的钩子列表请参见[nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)。

`*priority*`采用整数值。数字较小的链优先处理，并且可以是负数。[[3]](https://wiki.nftables.org/wiki-nftables/index.php/Configuring_chains#Base_chain_types)

例如，添加筛选输入数据包的基本链：

```
# nft add chain inet filter input { type filter hook input priority 0\; }

```

将上面命令中的`add`替换为`create`则可以添加一个新的链，但如果链已经存在，则返回错误。

#### 列出规则

列出一个链中的所有规则：

```
# nft list chain *family* *table* *chain*

```

例如，要列出`inet`中`filter`表的`output`链中的所有规则：

```
# nft list chain inet filter output

```

#### 编辑链

要编辑一个链，只需按名称调用并定义要更改的规则。

```
# nft chain *family table chain* { [ type *type* hook *hook* device *device* priority *priority* \; policy <policy> \; ] }

```

例如，将默认表中的input链策略从`accept`更改为`drop`：

```
# nft chain inet filter input { policy drop \; }

```

#### 删除链

删除一个链：

```
# nft delete chain *family* *table* *chain*

```

要删除的链不能包含任何规则或者跳转目标。

#### 清空链中的规则

清空一个链的规则：

```
# nft flush chain *family* *table* *chain*

```

### 规则（Rules）

规则由语句或表达式构成，包含在链中。

#### 添加规则

**提示：** *iptables-translate*实用程序何以将[iptables](/index.php/Iptables "Iptables")规则转换成nftables格式。

将一条规则添加到链中：

```
# nft add rule *family* *table* *chain* handle *handle* *statement*

```

规则添加到`*handle*`处，这是可选的。如果不指定，则规则添加到链的末尾。

将规则插入到指定位置：

```
# nft insert rule *family* *table* *chain* handle *handle* *statement*

```

如果未指定`*handle*`，则规则插入到链的开头。

##### 表达式

通常情况下，`*statement*`包含一些要匹配的表达式，然后是判断语句。结论语句包括`accept`、`drop`、`queue`、`continue`、`return`、`jump *chain*`和`goto *chain*`。也可能是其他陈述。有关信息信息，请参阅[nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)。

nftables中有多种可用的表达式，并且在大多数情况下，与iptables的对应项一致。最明显的区别是没有一般或隐式匹配。一般匹配是始终可用的匹配，如`--protocol`或`--source`。隐式匹配是用于特定协议的匹配，如TCP数据包的`--sport`。

以下是可用匹配的部分列表：

*   meta （元属性，如接口）
*   icmp （ICMP协议）
*   icmpv6 （ICMPv6协议）
*   ip （IP协议）
*   ip6 （IPv6协议）
*   tcp （TCP协议）
*   udp （UDP协议）
*   sctp （SCTP协议）
*   ct （链接跟踪）

以下是匹配参数的部分列表（完整列表请参见[nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)）：

```
meta:
  oif <output interface INDEX>
  iif <input interface INDEX>
  oifname <output interface NAME>
  iifname <input interface NAME>

  （oif 和 iif 接受字符串参数并转换为接口索引）
  （oifname 和 iifname 更具动态性，但因字符串匹配速度更慢）

icmp:
  type <icmp type>

icmpv6:
  type <icmpv6 type>

ip:
  protocol <protocol>
  daddr <destination address>
  saddr <source address>

ip6:
  daddr <destination address>
  saddr <source address>

tcp:
  dport <destination port>
  sport <source port>

udp:
  dport <destination port>
  sport <source port>

sctp:
  dport <destination port>
  sport <source port>

ct:
  state <new | established | related | invalid>

```

**注意:** *nft*不使用`/etc/services`文件匹配端口号和名称，而是使用[内置列表](https://git.netfilter.org/nftables/plain/src/services.c)。要在命令行显示端口映射，请使用 `nft describe tcp dport`。

#### 删除

单个规则只能通过其句柄删除。使用`nft --handle list`命令确定规则的句柄。请注意，`--handle`开关告诉`nft`输出句柄列表。

下面命令确定一个规则的句柄，然后删除。`--number`参数用于查看数字输出，如未解析的IP地址。

 `# nft --handle --numeric list chain inet filter input` 
```
table ip fltrTable {
     chain input {
          type filter hook input priority 0;
          ip saddr 127.0.0.1 accept # handle 10
     }
}

```

```
# nft delete rule inet fltrTable input handle 10

```

可以用`nft flush table`命令清空表中的所有的链。可以用`nft flush chain`或者`nft delete rule`命令清空单个链。

```
# nft flush table foo
# nft flush chain foo bar
# nft delete rule ip6 foo bar

```

第一个命令清空`foo`表中的所有链。第二个命令清空ip `foo`表中的`bar`链。第三个命令删除ip6 `foo`表`bar`两种的所有规则。

### 自动重载

清空当前规则集：

```
# echo "flush ruleset" > /tmp/nftables 

```

导出当前规则集：

```
# nft list ruleset >> /tmp/nftables

```

可以直接修改/tmp/nftables文件，使更改生效则运行：

```
# nft -f /tmp/nftables

```

## 配置示例

### 工作站

 `/etc/nftables.conf` 
```
flush ruleset

table inet filter {
        chain input {
                type filter hook input priority 0;

                # accept any localhost traffic
                iif lo accept

                # accept traffic originated from us
                ct state established,related accept

		# accept ICMP & IGMP
		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept
		ip protocol igmp accept

                # activate the following line to accept common local services
                #tcp dport { 22, 80, 443 } ct state new accept

                # count and drop any other traffic
                counter drop
        }
}

```

### 简单的IPv4/IPv6防火墙

 `firewall.rules` 
```
# A simple firewall

flush ruleset

table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		# established/related connections
		ct state established,related accept

		# invalid connections
		ct state invalid drop

		# loopback interface
		iif lo accept

		# ICMP & IGMP
		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept
		ip protocol igmp accept

		# SSH (port 22)
		tcp dport ssh accept

		# HTTP (ports 80 & 443)
		tcp dport { http, https } accept
	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### IPv4/IPv6防火墙限流

 `firewall.2.rules` 
```
table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		ct state invalid drop

		iif lo accept

		# no ping floods:
		ip protocol icmp icmp type echo-request limit rate over 10/second burst 4 packets  drop
		ip6 nexthdr icmpv6 icmpv6 type echo-request limit rate over 10/second burst 4 packets drop

		ct state established,related accept

		# ICMP & IGMP
		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept
		ip protocol igmp accept

		# avoid brute force on ssh:
		tcp dport ssh ct state new limit rate 15/minute accept

	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### 跳转

在配置文件中使用跳转时，必须确保已经定义目标链。否则会引起错误`Error: Could not process rule: No such file or directory`。

 `jump.rules` 
```
table inet filter {
    chain web {
        tcp dport http accept
        tcp dport 8080 accept
    }
    chain input {
        type filter hook input priority 0;
        ip saddr 10.0.2.0/24 jump web
        drop
    }
}

```

### 不同接口采用不同规则

如果设备有多个网络接口，并且需要对不同接口采用不同的规则，则可能需要使用“调度”筛选链，然后使用特定接口筛选链。例如，假设设备用作家庭路由器，你需要在LAN（接口enp3s0）运行一个web服务器，但不用于internet（接口enp2s0），可以考虑以下的结构：

```
table inet filter {
  chain input { # this chain serves as a dispatcher
    type filter hook input priority 0;

    iif lo accept # always accept loopback
    iifname enp2s0 jump input_enp2s0
    iifname enp3s0 jump input_enp3s0

    reject with icmp type port-unreachable # refuse traffic from all other interfaces
  }
  chain input_enp2s0 { # rules applicable to public interface interface
    ct state {established,related} accept
    ct state invalid drop
    udp dport bootpc accept
    tcp dport bootpc accept
    reject with icmp type port-unreachable # all other traffic
  }
  chain input_enp3s0 {
    ct state {established,related} accept
    ct state invalid drop
    udp dport bootpc accept
    tcp dport bootpc accept
    tcp port http accept
    tcp port https accept
    reject with icmp type port-unreachable # all other traffic
  }
  chain ouput { # we let everything out
    type filter hook output priority 0;
    accept
  }
 }

```

或者，可以只选择一个`iifname`语句，如单个上游接口，并将其他接口的默认规则放在一起，而不是为每个接口进行调度。

### Masquerading

nftables有一个特殊的关键字`masquerade` "where the source address is automagically set to the address of the output interface（源地址自动设置为出口地址）" ([[http://wiki.nftables.org/wiki-ip地址改变时更新规则。](http://wiki.nftables.org/wiki-ip地址改变时更新规则。)

使用方法：

*   确保在内核中启用Masquerading（默认内核已启用），否则在内核配置过程中设置

```
CONFIG_NFT_MASQ=m

```

*   `masquerade`关键字只能用于`nat`类型的链，而`nat`链又不能在`inet`簇的表中。要用`ip`和/或`ip6`簇的表。
*   masquerading是一中源NAT，只能工作于输出路径。

具有两个接口的计算机的示例：LAN连接到`nsp3s0`，internet连接到`enp2s0`：

```
table ip nat {
  chain prerouting {
    type nat hook prerouting priority 0;
  }
  chain postrouting {
    type nat hook postrouting priority 100;
    oifname "enp0s2" masquerade
  }
}

```

## 提示和技巧

### 简单可用的防火墙

详细信息参见 [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") 。

#### 单一计算机

清空当前规则集：

```
# nft flush ruleset

```

添加一个表：

```
# nft add table inet filter

```

添加input、forward和output三个基本链。input和forward的默认策略是drop。output的默认策略是accept。

```
# nft add chain inet filter input { type filter hook input priority 0 \; policy drop \; }
# nft add chain inet filter forward { type filter hook forward priority 0 \; policy drop \; }
# nft add chain inet filter output { type filter hook output priority 0 \; policy accept \; }

```

添加两个与TCP和UDP关联的常规链：

```
# nft add chain inet filter TCP
# nft add chain inet filter UDP

```

related和established的流量会accept：

```
# nft add rule inet filter input ct state related,established accept

```

loopback接口的流量会accept：

```
# nft add rule inet filter input iif lo accept

```

无效的流量会drop：

```
# nft add rule inet filter input ct state invalid drop

```

新的echo请求（ping）会accept：

```
# nft add rule inet filter input ip protocol icmp icmp type echo-request ct state new accept

```

新的UDP流量跳转到UDP链：

```
# nft add rule inet filter input ip protocol udp ct state new jump UDP

```

新的TCP流量跳转到TCP链：

```
# nft add rule inet filter input ip protocol tcp tcp flags \& \(fin\|syn\|rst\|ack\) == syn ct state new jump TCP

```

未由其他规则处理的所有通信会reject：

```
# nft add rule inet filter input ip protocol udp reject
# nft add rule inet filter input ip protocol tcp reject with tcp reset
# nft add rule inet filter input counter reject with icmp type prot-unreachable

```

此时，应决定对传入连接打开哪些端口，这些由TCP和UDP链处理。例如，要打开web服务器的连接端口，添加：

```
# nft add rule inet filter TCP tcp dport 80 accept

```

要打开web服务器HTTPS连接端口443：

```
# nft add rule inet filter TCP tcp dport 443 accept

```

允许SSH连接端口22：

```
# nft add rule inet filter TCP tcp dport 22 accept

```

允许传入DNS请求：

```
# nft add rule inet filter TCP tcp dport 53 accept
# nft add rule inet filter UDP udp dport 53 accept

```

确保更改是永久的。

### 防止暴力攻击

[Sshguard](/index.php/Sshguard "Sshguard")是可以检测暴力攻击的程序，并根据临时黑名单IP地址修改防火墙。有关如何与nftables一起使用的问题，请参阅[Sshguard#nftables](/index.php/Sshguard#nftables "Sshguard")。

## 参考

*   [netfilter nftables wiki](https://wiki.nftables.org/)
*   [debian:nftables](https://wiki.debian.org/nftables "debian:nftables")
*   [gentoo:nftables](https://wiki.gentoo.org/wiki/nftables "gentoo:nftables")
*   [First release of nftables](https://lwn.net/Articles/324251/)
*   [nftables quick howto](https://home.regit.org/netfilter-en/nftables-quick-howto/)
*   [The return of nftables](https://lwn.net/Articles/564095/)
*   [What comes after ‘iptables’? Its successor, of course: `nftables`](http://developers.redhat.com/blog/2016/10/28/what-comes-after-iptables-its-successor-of-course-nftables/)