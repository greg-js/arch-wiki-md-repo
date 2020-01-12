Related articles

*   [iptables](/index.php/Iptables "Iptables")

[nftables](https://netfilter.org/projects/nftables/) is a netfilter project that aims to replace the existing {ip,ip6,arp,eb}tables framework. It provides a new packet filtering framework, a new user-space utility (nft), and a compatibility layer for {ip,ip6}tables. It uses the existing hooks, connection tracking system, user-space queueing component, and logging subsystem of netfilter.

It consists of three main components: a kernel implementation, the libnl [netlink](https://en.wikipedia.org/wiki/Netlink "wikipedia:Netlink") communication and the nftables user-space front-end. The kernel provides a netlink configuration interface, as well as run-time rule-set evaluation, libnl contains the low-level functions for communicating with the kernel, and the nftables front-end is what the user interacts with via nft.

You can also visit the [official nftables wiki page](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) for more information.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Tables](#Tables)
        *   [3.1.1 Create table](#Create_table)
        *   [3.1.2 List tables](#List_tables)
        *   [3.1.3 List chains and rules in a table](#List_chains_and_rules_in_a_table)
        *   [3.1.4 Delete table](#Delete_table)
        *   [3.1.5 Flush table](#Flush_table)
    *   [3.2 Chains](#Chains)
        *   [3.2.1 Create chain](#Create_chain)
            *   [3.2.1.1 Regular chain](#Regular_chain)
            *   [3.2.1.2 Base chain](#Base_chain)
        *   [3.2.2 List rules](#List_rules)
        *   [3.2.3 Edit a chain](#Edit_a_chain)
        *   [3.2.4 Delete a chain](#Delete_a_chain)
        *   [3.2.5 Flush rules from a chain](#Flush_rules_from_a_chain)
    *   [3.3 Rules](#Rules)
        *   [3.3.1 Add rule](#Add_rule)
            *   [3.3.1.1 Expressions](#Expressions)
        *   [3.3.2 Deletion](#Deletion)
    *   [3.4 Atomic reloading](#Atomic_reloading)
*   [4 Examples](#Examples)
    *   [4.1 Workstation](#Workstation)
    *   [4.2 Server](#Server)
    *   [4.3 Limit rate](#Limit_rate)
    *   [4.4 Jump](#Jump)
    *   [4.5 Different rules for different interfaces](#Different_rules_for_different_interfaces)
    *   [4.6 Masquerading](#Masquerading)
    *   [4.7 NAT with port forwarding](#NAT_with_port_forwarding)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Simple stateful firewall](#Simple_stateful_firewall)
        *   [5.1.1 Single machine](#Single_machine)
    *   [5.2 Prevent brute-force attacks](#Prevent_brute-force_attacks)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Working with Docker](#Working_with_Docker)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the userspace utilities package [nftables](https://www.archlinux.org/packages/?name=nftables) or the git version [nftables-git](https://aur.archlinux.org/packages/nftables-git/).

**Tip:** Most [iptables front-ends](/index.php/Iptables#Front-ends "Iptables") feature no direct or indirect support of nftables, but may introduce it.[[2]](https://www.spinics.net/lists/netfilter/msg58215.html) One graphical front-end that supports both, nftables and iptables, is [firewalld](/index.php/Firewalld "Firewalld").[[3]](https://firewalld.org/2018/07/nftables-backend)

## Usage

*nftables* makes a distinction between temporary rules made in the command line and permanent ones loaded from or saved to a file. The default file is `/etc/nftables.conf` which already contains a simple IPv4/IPv6 firewall table named "inet filter".

To use it [start/enable](/index.php/Start/enable "Start/enable") the `nftables.service`.

You can check the ruleset with

```
# nft list ruleset

```

**Note:** You may have to create `/etc/modules-load.d/nftables.conf` with all of the nftables related modules you require as entries for the systemd service to work correctly. You can get a list of modules using this command: `$ grep -Eo '^nf\w+' /proc/modules` Otherwise, you could end up with the dreaded `Error: Could not process rule: No such file or directory` error.

## Configuration

nftables' user-space utility *nft* performs most of the rule-set evaluation before handing rule-sets to the kernel. Rules are stored in chains, which in turn are stored in tables. The following sections indicate how to create and modify these constructs.

All changes below are temporary. To make changes permanent, save your ruleset to `/etc/nftables.conf` which is loaded by `nftables.service`:

```
# nft -s list ruleset > /etc/nftables.conf

```

**Note:** `nft list` does not output variable definitions, if you have any in `/etc/nftables.conf` they will be lost. Any variables used in rules will be replaced by their value.

To read input from a file use the `-f`/`--file` option:

```
# nft -f *filename*

```

Note that any rules already loaded are not automatically flushed.

See [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8) for a complete list of all commands.

### Tables

Tables hold [#Chains](#Chains). Unlike tables in iptables, there are no built-in tables in nftables. The number of tables and their names is up to the user. However, each table only has one address family and only applies to packets of this family. Tables can have one of five families specified:

| nftables family | iptables utility |
| ip | iptables |
| ip6 | ip6tables |
| inet | iptables and ip6tables |
| arp | arptables |
| bridge | ebtables |

`ip` (i.e. IPv4) is the default family and will be used if family is not specified.

To create one rule that applies to both IPv4 and IPv6, use `inet`. `inet` allows for the unification of the `ip` and `ip6` families to make defining rules for both easier.

See [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8#ADDRESS_FAMILIES) for a complete description of address families.

In all of the following, `*family*` is optional, and if not specified is set to `ip`.

#### Create table

The following adds a new table:

```
# nft add table *family* *table*

```

#### List tables

To list all tables:

```
# nft list tables

```

#### List chains and rules in a table

To list all chains and rules of a specified table do:

```
# nft list table *family* *table*

```

For example, to list all the rules of the `filter` table of the `inet` family:

```
# nft list table inet filter

```

#### Delete table

To delete a table do:

```
# nft delete table *family* *table*

```

Tables can only be deleted if there are no chains in them.

#### Flush table

To flush all rules from a table do:

```
# nft flush table *family* *table*

```

### Chains

The purpose of chains is to hold [#Rules](#Rules). Unlike chains in iptables, there are no built-in chains in nftables. This means that if no chain uses any types or hooks in the netfilter framework, packets that would flow through those chains will not be touched by nftables, unlike iptables.

Chains have two types. A *base* chain is an entry point for packets from the networking stack, where a hook value is specified. A *regular* chain may be used as a jump target for better organization.

In all of the following `*family*` is optional, and if not specified is set to `ip`.

#### Create chain

##### Regular chain

The following adds a regular chain named `*chain*` to the table named `*table*`:

```
# nft add chain *family* *table* *chain*

```

For example, to add a regular chain named `tcpchain` to the `filter` table of the `inet` address family do:

```
# nft add chain inet filter tcpchain

```

##### Base chain

To add a base chain specify hook and priority values:

```
# nft add chain *family* *table* *chain* '{ type *type* hook *hook* priority *priority* ; }'

```

`*type*` can be `filter`, `route`, or `nat`.

For IPv4/IPv6/Inet address families `*hook*` can be `prerouting`, `input`, `forward`, `output`, or `postrouting`. See [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8#ADDRESS_FAMILIES) for a list of hooks for other families.

`*priority*` takes either a priority name or an its integer value. See [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8#CHAINS) for a list of standard priority names and values. Chains with lower numbers are processed first and can be negative. [[4]](https://wiki.nftables.org/wiki-nftables/index.php/Configuring_chains#Base_chain_types)

For example, to add a base chain that filters input packets:

```
# nft add chain inet filter input '{ type filter hook input priority 0; }'

```

Replace `add` with `create` in any of the above to add a new chain but return an error if the chain already exists.

#### List rules

The following lists all rules of a chain:

```
# nft list chain *family* *table* *chain*

```

For example, the following lists the rules of the chain named `output` in the `inet` table named `filter`:

```
# nft list chain inet filter output

```

#### Edit a chain

To edit a chain, simply call it by its name and define the rules you want to change.

```
# nft chain *family table chain* '{ [ type *type* hook *hook* device *device* priority *priority* ; policy *policy* ; ] }'

```

For example, to change the input chain policy of the default table from `accept` to `drop`

```
# nft chain inet filter input '{ policy drop ; }'

```

#### Delete a chain

To delete a chain do:

```
# nft delete chain *family* *table* *chain*

```

The chain must not contain any rules or be a jump target.

#### Flush rules from a chain

To flush rules from a chain do:

```
# nft flush chain *family* *table* *chain*

```

### Rules

Rules are either constructed from expressions or statements and are contained within chains.

#### Add rule

**Tip:** The *iptables-translate* utility translates [iptables](/index.php/Iptables "Iptables") rules to nftables format.

To add a rule to a chain do:

```
# nft add rule *family* *table* *chain* handle *handle* *statement*

```

The rule is appended at `*handle*`, which is optional. If not specified, the rule is appended to the end of the chain.

To prepend the rule to the position do:

```
# nft insert rule *family* *table* *chain* handle *handle* *statement*

```

If `*handle*` is not specified, the rule is prepended to the chain.

##### Expressions

Typically a `*statement*` includes some expression to be matched and then a verdict statement. Verdict statements include `accept`, `drop`, `queue`, `continue`, `return`, `jump *chain*`, and `goto *chain*`. Other statements than verdict statements are possible. See [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8) for more information.

There are various expressions available in nftables and, for the most part, coincide with their iptables counterparts. The most noticeable difference is that there are no generic or implicit matches. A generic match was one that was always available, such as `--protocol` or `--source`. Implicit matches were protocol-specific, such as `--sport` when a packet was determined to be TCP.

The following is an incomplete list of the matches available:

*   meta (meta properties, e.g. interfaces)
*   icmp (ICMP protocol)
*   icmpv6 (ICMPv6 protocol)
*   ip (IP protocol)
*   ip6 (IPv6 protocol)
*   tcp (TCP protocol)
*   udp (UDP protocol)
*   sctp (SCTP protocol)
*   ct (connection tracking)

The following is an incomplete list of match arguments (for a more complete list, see [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)):

```
meta:
  oif <output interface INDEX>
  iif <input interface INDEX>
  oifname <output interface NAME>
  iifname <input interface NAME>

  (oif and iif accept string arguments and are converted to interface indexes)
  (oifname and iifname are more dynamic, but slower because of string matching)

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

#### Deletion

Individual rules can only be deleted by their handles. The `nft --handle list` command must be used to determine rule handles. Note the `--handle` switch, which tells `nft` to list handles in its output.

The following determines the handle for a rule and then deletes it. The `--numeric` argument is useful for viewing some numeric output, like unresolved IP addresses.

 `# nft --handle --numeric list chain inet filter input` 
```
table inet fltrTable {
     chain input {
          type filter hook input priority 0;
          ip saddr 127.0.0.1 accept # handle 10
     }
}

```

```
# nft delete rule inet fltrTable input handle 10

```

All the chains in a table can be flushed with the `nft flush table` command. Individual chains can be flushed using either the `nft flush chain` or `nft delete rule` commands.

```
# nft flush table foo
# nft flush chain foo bar
# nft delete rule ip6 foo bar

```

The first command flushes all of the chains in the ip `foo` table. The second flushes the `bar` chain in the ip `foo` table. The third deletes all of the rules in `bar` chain in the ip6 `foo` table.

### Atomic reloading

Flush the current ruleset:

```
# echo "flush ruleset" > /tmp/nftables 

```

Dump the current ruleset:

```
# nft -s list ruleset >> /tmp/nftables

```

Now you can edit /tmp/nftables and apply your changes with:

```
# nft -f /tmp/nftables

```

## Examples

### Workstation

 `/etc/nftables.conf` 
```
flush ruleset

table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		iif lo accept comment "Accept any localhost traffic"
		ct state invalid drop comment "Drop invalid connections"
		ct state established,related accept comment "Accept traffic originated from us"

		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept comment "Accept ICMPv6"
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept comment "Accept ICMP"
		ip protocol igmp accept comment "Accept IGMP"

		udp dport mdns ip6 daddr ff02::fb accept comment "Accept mDNS"
		udp dport mdns ip daddr 224.0.0.251 accept comment "Accept mDNS"

		udp sport 1900 udp dport >= 1024 ip6 saddr { fd00::/8, fe80::/10 } meta pkttype unicast limit rate 4/second burst 20 packets accept comment "Accept UPnP IGD port mapping reply"
		udp sport 1900 udp dport >= 1024 ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } meta pkttype unicast limit rate 4/second burst 20 packets accept comment "Accept UPnP IGD port mapping reply"

		udp sport netbios-ns udp dport >= 1024 meta pkttype unicast ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept Samba Workgroup browsing replies"
		udp sport netbios-ns udp dport >= 1024 meta pkttype unicast ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept Samba Workgroup browsing replies"

		counter comment "Count any other traffic"
	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### Server

 `/etc/nftables.conf` 
```
flush ruleset

table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		iif lo accept comment "Accept any localhost traffic"
		ct state invalid drop comment "Drop invalid connections"
		ct state established,related accept comment "Accept traffic originated from us"

		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept comment "Accept ICMPv6"
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept comment "Accept ICMP"
		ip protocol igmp accept comment "Accept IGMP"

		udp dport mdns ip6 daddr ff02::fb accept comment "Accept mDNS"
		udp dport mdns ip daddr 224.0.0.251 accept comment "Accept mDNS"

		tcp dport ssh accept comment "Accept SSH on port 22"

		tcp dport { http, https, 8008, 8080 } accept comment "Accept HTTP (ports 80, 443, 8008, 8080)"

		meta l4proto { tcp, udp } th dport 2049 ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NFS"
		meta l4proto { tcp, udp } th dport 2049 ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NFS"

		udp dport netbios-ns ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NetBIOS Name Service (nmbd)"
		udp dport netbios-ns ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NetBIOS Name Service (nmbd)"
		udp dport netbios-dgm ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NetBIOS Datagram Service (nmbd)"
		udp dport netbios-dgm ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NetBIOS Datagram Service (nmbd)"
		tcp dport netbios-ssn ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NetBIOS Session Service (smbd)"
		tcp dport netbios-ssn ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NetBIOS Session Service (smbd)"
		tcp dport microsoft-ds ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept Microsoft Directory Service (smbd)"
		tcp dport microsoft-ds ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept Microsoft Directory Service (smbd)"

		udp sport bootpc udp dport bootps ip saddr 0.0.0.0 ip daddr 255.255.255.255 accept comment "Accept DHCPDISCOVER (for DHCP-Proxy)"
		udp sport { bootpc, 4011 } udp dport { bootps, 4011 } ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept PXE"
		udp dport tftp ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept TFTP"
		udp dport tftp ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept TFTP"

	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### Limit rate

```
table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		iif lo accept comment "Accept any localhost traffic"
		ct state invalid drop comment "Drop invalid connections"

		ip protocol icmp icmp type echo-request limit rate over 10/second burst 4 packets drop comment "No ping floods"
		ip6 nexthdr icmpv6 icmpv6 type echo-request limit rate over 10/second burst 4 packets drop comment "No ping floods"

		ct state established,related accept comment "Accept traffic originated from us"

		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept comment "Accept ICMPv6"
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept comment "Accept ICMP"
		ip protocol igmp accept comment "Accept IGMP"

		tcp dport ssh ct state new limit rate 15/minute accept comment "Avoid brute force on SSH"

	}

}

```

### Jump

When using jumps in config file, it is necessary to define the target chain first. Otherwise one could end up with `Error: Could not process rule: No such file or directory`.

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

### Different rules for different interfaces

If your box has more than one network interface, and you would like to use different rules for different interfaces, you may want to use a "dispatching" filter chain, and then interface-specific filter chains. For example, let us assume your box acts as a home router, you want to run a web server accessible over the LAN (interface `enp3s0`), but not from the public internet (interface `enp2s0`), you may want to consider a structure like this:

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

Alternatively you could choose only one `iifname` statement, such as for the single upstream interface, and put the default rules for all other interfaces in one place, instead of dispatching for each interface.

### Masquerading

nftables has a special keyword `masquerade` "where the source address is automagically set to the address of the output interface" ([source](https://wiki.nftables.org/wiki-nftables/index.php/Performing_Network_Address_Translation_%28NAT%29#Masquerading)). This is particularly useful for situations in which the IP address of the interface is unpredictable or unstable, such as the upstream interface of routers connecting to many ISPs. Without it, the Network Address Translation rules would have to be updated every time the IP address of the interface changed.

To use it:

*   make sure masquerading is enabled in the kernel (true if you use the default kernel), otherwise during kernel configuration, set `CONFIG_NFT_MASQ=m`.
*   the `masquerade` keyword can only be used in chains of type `nat`.
*   masquerading is a kind of source NAT, so only works in the output path.

Example for a machine with two interfaces: LAN connected to `enp3s0`, and public internet connected to `enp2s0`:

```
table inet nat {
  chain prerouting {
    type nat hook prerouting priority -100;
  }
  chain postrouting {
    type nat hook postrouting priority 100;
    oifname "enp2s0" masquerade
  }
}

```

Since the table type is `inet` both IPv4 and IPv6 packets will be masqueraded. If you want only ipv4 packets to be masqueraded (since extra adress space of IPv6 makes NAT not required) `meta nfproto ipv4` expression can be used infront of `oifname "enp2s0" masquerade` or the table type can be changed to `ip`.

### NAT with port forwarding

This example will forward ports 22 and 80 to `*destination_ip*`. You will need to set `net.ipv4.ip_forward` and `net.ipv4.conf.*wan_interface*.forwarding` to `1` via [sysctl](/index.php/Sysctl "Sysctl").

```
table ip nat {
  chain prerouting {
    type nat hook prerouting priority -100;

    tcp dport { ssh, http } dnat to *destination_ip*
  }

  chain postrouting {
    type nat hook postrouting priority 100;

    ip daddr *destination_ip* masquerade
  }
}

```

## Tips and tricks

### Simple stateful firewall

See [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") for more information.

#### Single machine

Flush the current ruleset:

```
# nft flush ruleset

```

Add a table:

```
# nft add table inet filter

```

Add the input, forward, and output base chains. The policy for input and forward will be to drop. The policy for output will be to accept.

```
# nft add chain inet filter input '{ type filter hook input priority 0 ; policy drop ; }'
# nft add chain inet filter forward '{ type filter hook forward priority 0 ; policy drop ; }'
# nft add chain inet filter output '{ type filter hook output priority 0 ; policy accept ; }'

```

Add two regular chains that will be associated with tcp and udp:

```
# nft add chain inet filter TCP
# nft add chain inet filter UDP

```

Related and established traffic will be accepted:

```
# nft add rule inet filter input ct state related,established accept

```

All loopback interface traffic will be accepted:

```
# nft add rule inet filter input iif lo accept

```

Drop any invalid traffic:

```
# nft add rule inet filter input ct state invalid drop

```

Accept ICMP and IGMP:

```
# nft add rule inet filter input ip6 nexthdr icmpv6 icmpv6 type '{ destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report }' accept
# nft add rule inet filter input ip protocol icmp icmp type '{ destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem }' accept
# nft add rule inet filter input ip protocol igmp accept

```

New udp traffic will jump to the UDP chain:

```
# nft add rule inet filter input ip protocol udp ct state new jump UDP

```

New tcp traffic will jump to the TCP chain:

```
# nft add rule inet filter input 'ip protocol tcp tcp flags & (fin|syn|rst|ack) == syn ct state new jump TCP'

```

Reject all traffic that was not processed by other rules:

```
# nft add rule inet filter input ip protocol udp reject
# nft add rule inet filter input ip protocol tcp reject with tcp reset
# nft add rule inet filter input counter reject with icmp type prot-unreachable

```

At this point you should decide what ports you want to open to incoming connections, which are handled by the TCP and UDP chains. For example to open connections for a web server add:

```
# nft add rule inet filter TCP tcp dport 80 accept

```

To accept HTTPS connections for a webserver on port 443:

```
# nft add rule inet filter TCP tcp dport 443 accept

```

To accept SSH traffic on port 22:

```
# nft add rule inet filter TCP tcp dport 22 accept

```

To accept incoming DNS requests:

```
# nft add rule inet filter TCP tcp dport 53 accept
# nft add rule inet filter UDP udp dport 53 accept

```

Be sure to make your changes permanent when satisifed.

### Prevent brute-force attacks

[Sshguard](/index.php/Sshguard "Sshguard") is program that can detect brute-force attacks and modify firewalls based on IP addresses it temporarily blacklists. See [Sshguard#nftables](/index.php/Sshguard#nftables "Sshguard") on how to set up nftables to be used with it.

## Troubleshooting

### Working with Docker

Using nftables can interfere with [Docker](/index.php/Docker "Docker") networking (and probably other container runtimes as well). In particular the drop policy for the `forward` chain will block packets originating in docker containers. If you want to keep the `forward` rule in your `inet` table, you can use the following:

1.  [Install](/index.php/Install "Install") [iptables-nft](https://www.archlinux.org/packages/?name=iptables-nft) to provide an iptables compatible interface for nftables that docker can use.
2.  Use the following for the `forward` chain in your `inet` table:

    ```
    chain forward {
      type filter hook forward priority security; policy drop
      mark 1 accept

    ```

3.  Add a rule to the DOCKER-USER chain in the `ip filter` table to mark packets if docker is running:

    ```
    table ip filter {
      chain DOCKER-USER {
        mark set 1
      }
    }

    ```

This works by marking packets if docker is active, and accepting the packets in this case, since docker has already filtered them (the forward chain defined by docker uses a drop policy).

## See also

*   [netfilter nftables wiki](https://wiki.nftables.org/)
*   [debian:nftables](https://wiki.debian.org/nftables "debian:nftables")
*   [gentoo:nftables](https://wiki.gentoo.org/wiki/nftables "gentoo:nftables")
*   [First release of nftables](https://lwn.net/Articles/324251/)
*   [nftables quick howto](https://home.regit.org/netfilter-en/nftables-quick-howto/)
*   [The return of nftables](https://lwn.net/Articles/564095/)
*   [What comes after ‘iptables’? Its successor, of course: `nftables`](https://developers.redhat.com/blog/2016/10/28/what-comes-after-iptables-its-successor-of-course-nftables/)