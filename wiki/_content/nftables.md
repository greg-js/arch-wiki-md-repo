# nftables

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** As of October, 2015: while nftables has been around for a while, few people seem to have practical experience using it. The documentation often leaves questions open. If you'd like to pioneer, help out and document how you got it to work. The best place to ask questions is the [Netfilter mailing list](http://netfilter.org/mailinglists.html#ml-user). (Discuss in [Talk:Nftables#](https://wiki.archlinux.org/index.php/Talk:Nftables))

Related articles

*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [iptables](/index.php/Iptables "Iptables")

[nftables](http://netfilter.org/projects/nftables/) is a netfilter project that aims to replace the existing ip-, ip6-, arp-, and ebtables framework. It provides a new packet filtering framework, a new user-space utility (nft), and a compatibility layer for ip- and ip6tables. It uses the existing hooks, connection tracking system, user-space queueing component, and logging subsystem of netfilter.

You can also visit the [official nftables wiki page](http://wiki.nftables.org) for more information.

The first release is available in Linux 3.13, which is in the _core_ repository ([linux](https://www.archlinux.org/packages/?name=linux)), and nftables (the user-space components) is available in the _extra_ repository ([nftables](https://www.archlinux.org/packages/?name=nftables)), and on the [AUR](/index.php/AUR "AUR") in package [nftables-git](https://aur.archlinux.org/packages/nftables-git/)<sup><small>AUR</small></sup>.

## Contents

*   [1 Overview](#Overview)
*   [2 nft](#nft)
*   [3 Tables](#Tables)
    *   [3.1 Family](#Family)
    *   [3.2 Listing](#Listing)
    *   [3.3 Creation](#Creation)
    *   [3.4 Deletion](#Deletion)
*   [4 Chains](#Chains)
    *   [4.1 Listing](#Listing_2)
    *   [4.2 Creation](#Creation_2)
        *   [4.2.1 Properties](#Properties)
            *   [4.2.1.1 Types](#Types)
            *   [4.2.1.2 Hooks](#Hooks)
            *   [4.2.1.3 Priorities](#Priorities)
    *   [4.3 Deletion](#Deletion_2)
*   [5 Rules](#Rules)
    *   [5.1 Listing](#Listing_3)
    *   [5.2 Creation](#Creation_3)
        *   [5.2.1 Matches](#Matches)
        *   [5.2.2 Jumps](#Jumps)
    *   [5.3 Insertion](#Insertion)
    *   [5.4 Deletion](#Deletion_3)
    *   [5.5 Atomic Reloading](#Atomic_Reloading)
*   [6 File Definitions](#File_Definitions)
*   [7 Getting Started](#Getting_Started)
*   [8 Samples](#Samples)
    *   [8.1 Simple IP/IPv6 Firewall](#Simple_IP.2FIPv6_Firewall)
    *   [8.2 Limit rate IP/IPv6 Firewall](#Limit_rate_IP.2FIPv6_Firewall)
    *   [8.3 Jump](#Jump)
*   [9 Practical examples](#Practical_examples)
    *   [9.1 Different rules for different interfaces](#Different_rules_for_different_interfaces)
    *   [9.2 Masquerading](#Masquerading)
*   [10 Loading rules at boot](#Loading_rules_at_boot)
*   [11 Logging to Syslog](#Logging_to_Syslog)
*   [12 See also](#See_also)

## Overview

nftables consists of three main components: a kernel implementation, the libnl netlink communication and the nftables user-space front-end. The kernel provides a netlink configuration interface, as well as run-time rule-set evaluation using a small classification language interpreter. libnl contains the low-level functions for communicating with the kernel; the nftables front-end is what the user interacts with.

## nft

nftables' user-space utility `nft` now performs most of the rule-set evaluation before handing rule-sets to the kernel. Because of this, nftables provides no default tables or chains; although, a user can emulate an iptables-like setup.

**Note:** [nftables](https://www.archlinux.org/packages/?name=nftables) contains `/etc/nftables.conf` which has a "filter" table. Rules in this table are designed to allow some protocols and reject everything else.

It works in a fashion similar to ifconfig or iproute2\. The commands are a long, structured sequence rather than using argument switches like in iptables. For example:

```
nft add rule ip6 filter input ip6 saddr ::1 accept

```

`add` is the command. `rule` is a subcommand of `add`. `ip6` is an argument of `rule`, telling it to use the ip6 family. `filter` and `input` are arguments of `rule` specifying the table and chain to use, respectively. The rest that follows is a rule definition, which includes matches (`ip`), their parameters (`saddr`), parameter arguments (`::1`), and jumps (`accept`).

The following is an incomplete list of the commands available in nft:

```
list
  tables [family]
  table [family] <name>
  chain [family] <table> <name>

add
  table [family] <name>
  chain [family] <table> <name> [chain definitions]
  rule [family] <table> <chain> <rule definition>

table [family] <name> (shortcut for `add table`)

insert
  rule [family] <table> <chain> <rule definition>

delete
  table [family] <name>
  chain [family] <table> <name>
  rule [family] <table> <handle>

flush
  table [family] <name>
  chain [family] <table> <name>

```

`family` is optional, see [section on family](#Family) below.

## Tables

The purpose of tables is to hold chains. Unlike tables in iptables, there are no built-in tables in nftables. How many tables one uses, or their naming, is largely a matter of style and personal preference. However, each table has a (network) family and and only applies to packets of this family. Tables can have one of five families specified, which unifies the various iptables utilities into one:

<table class="wikitable">

<tbody>

<tr>

<th>nftables family</th>

<th>iptables utility</th>

</tr>

<tr>

<td>ip</td>

<td>iptables</td>

</tr>

<tr>

<td>ip6</td>

<td>ip6tables</td>

</tr>

<tr>

<td>inet</td>

<td>iptables and ip6tables</td>

</tr>

<tr>

<td>arp</td>

<td>arptables</td>

</tr>

<tr>

<td>bridge</td>

<td>ebtables</td>

</tr>

</tbody>

</table>

### Family

`ip` (i.e. IPv4) is the default family and will be used if family is not specified.

IPv6 is specified as `ip6`.

To create one rule that applies to both IPv4 and IPv6, use `inet`. This requires Linux >=3.15\. `inet` allows for the unification of the `ip` and `ip6` families to make defining rules for both easier.

**Note:** `inet` does not work for `nat`-type chains, only for `filter`-type chains. ([source](http://www.spinics.net/lists/netfilter/msg56411.html))

### Listing

You can list the current tables in a family with the `nft list` command.

```
# nft list tables
# nft list tables ip6

```

You can list a full table definition by specifying a table name:

```
# nft list table _foo_
# nft list table _ip6 foo_

```

### Creation

Tables can be added via two commands — one just being a shortcut for the other. Here is an example of how to add an ip table called foo and an ip6 table called foo:

```
# nft add table _foo_
# nft table _ip6 foo_

```

You can have two tables with the same name as long as they are in different families.

### Deletion

Tables can only be deleted if there are no chains in them.

```
# nft delete table _foo_
# nft delete table _ip6 foo_

```

## Chains

The purpose of chains is to hold rules. Unlike chains in iptables, there are no built-in chains in nftables. This means that if no chain uses any types or hooks in the netfilter framework, packets that would flow through those chains will not be touched by nftables, unlike iptables.

### Listing

The `nft list table foo` command will list all the chains in the foo table. You can also list rules from an individual chain.

```
# nft list chain _foo_ _bar_
# nft list chain _ip6 foo bar_

```

These commands will list the `bar` chains in the ip and ip6 `foo` tables.

### Creation

Chains can be added when a table is created in a file definition or one at time via the `nft add chain` command.

```
# nft add chain _foo_ _bar_
# nft add chain _ip6 foo bar_

```

These commands will add a chain called `bar` to the ip and ip6 `foo` tables.

#### Properties

Because nftables has no built-in chains, it allows chains to access certain features of the netfilter framework.

```
# nft add chain filter input \{ type filter hook input priority 0\; \}

```

This command tells nftables to add a chain called `input` to the `filter` table and defines its type, hook, and priority. These properties essentially replace the built-in tables and chains in iptables.

##### Types

There are three types a chain can have and they correspond to the tables used in iptables:

*   filter
*   nat
*   route (mangle)

##### Hooks

There are five hooks a chain can use and they correspond to the chains used in iptables:

*   input
*   output
*   forward
*   prerouting
*   postrouting

##### Priorities

**Note:** Priorities do not currently appear to have any effect on which chain sees packets first.

**Note:** Since the priority seems to be an unsigned integer, negative priorities will be converted into very high priorities.

Priorities tell nftables which chains packets should pass through first. They are integers, and the higher the integer, the higher the priority.

### Deletion

Chains can only be deleted if there are no rules in them.

```
# nft delete chain _foo bar_
# nft delete chain _ip6 foo bar_

```

These commands delete the `bar` chains from the ip and ip6 `foo` tables.

## Rules

The purpose of rules is to identify packets (match) and carry out tasks (jump). Like in iptables, there are various matches and jumps available, though not all of them are feature-complete in nftables.

### Listing

You can list the current rules in a table with the `nft list` command, using the same method as listing a table. You can also list rules from an individual chain.

```
# nft list chain _foo bar_
# nft list chain _ip6 foo bar_

```

These commands will list the rules in the `bar` chains in the ip and ip6 `foo` tables.

### Creation

Rules can be added when a table is created in a file definition or one at time via the `nft add rule` command.

```
# nft add rule foo bar ip saddr 127.0.0.1 accept
# nft add rule ip6 foo bar ip saddr ::1 accept

```

These commands will add a rule to the `bar` chains in the ip and ip6 `foo` tables that matches an `ip` packet when its `saddr` (source address) is 127.0.0.1 (IPv4) or ::1 (IPv6) and accepts those packets.

#### Matches

There are various matches available in nftables and, for the most part, coincide with their iptables counterparts. The most noticeable difference is that there are no generic or implicit matches anymore. A generic match was one that was always available, such as `--protocol` or `--source`. Implicit matches were protocol-specific, such as `--sport` when a packet was determined to be TCP.

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

The following is an incomplete list of match arguments (for a more complete list, see `man 8 nft`):

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

#### Jumps

Jumps work the same as they do in iptables, except multiple jumps can now be used in one rule.

```
# nft add rule filter input tcp dport 22 log accept

```

The following is an incomplete list of jumps:

*   accept (accept a packet)
*   reject (reject a packet)
*   drop (drop a packet)
*   snat (perform source NAT on a packet)
*   dnat (perform destination NAT on a packet)
*   log (log a packet)
*   counter (keep a counter on a packet; counters are optional in nftables)
*   return (stop traversing the chain)
*   jump <chain> (jump to another chain)
*   goto <chain> (jump to another chain, but do not return)

### Insertion

Rules can be prepended to chains with the `nft insert rule` command.

```
# nft insert rule filter input ct state established,related accept

```

### Deletion

Individual rules can only be deleted by their handles. The `nft --handle list` command must be used to determine rule handles. Note the `--handle` switch, which tells `nft` to list handles in its output.

The following determines the handle for a rule and then deletes it. The `--number` argument is useful for viewing some numeric output, like unresolved IP addresses.

 `# nft --handle --numeric list chain filter input` 

```
table ip fltrTable {
     chain input {
          type filter hook input priority 0;
          ip saddr 127.0.0.1 accept # handle 10
     }
}

```

```
# nft delete rule fltrTable input handle 10

```

All the chains in a table can be flushed with the `nft flush table` command. Individual chains can be flushed using either the `nft flush chain` or `nft delete rule` commands.

```
# nft flush table foo
# nft flush chain foo bar
# nft delete rule ip6 foo bar

```

The first command flushes all of the chains in the ip `foo` table. The second flushes the `bar` chain in the ip `foo` table. The third deletes all of the rules in `bar` chain in the ip6 `foo` table.

### Atomic Reloading

Flush the current ruleset:

```
# echo "flush ruleset" > /tmp/nftables 

```

Dump the current ruleset:

```
# nft list ruleset >> /tmp/nftables

```

Now you can edit /tmp/nftables and apply your changes with:

```
# nft -f /tmp/nftables

```

## File Definitions

File definitions can be used by the `nft -f` command, which acts like the `iptables-restore` command. However, unlike `iptables-restore`, this command does not flush out your existing ruleset, to do so you have to prepend the flush command.

 `/etc/nftables/filter.rules` 

```
flush table ip filter
table ip filter {
     chain input {
          type filter hook input priority 0;
          ct state established,related accept
          ip saddr 127.0.0.1 accept
          tcp dport 22 log accept
          reject
     }
}

```

To export your rules (like `iptables-save`):

```
# nft list ruleset

```

## Getting Started

The below example shows _nft_ commands to configure a basic **IPv4** only firewall. If you want to filter both IPv4 **and** IPv6 you should look at the other examples in `/usr/share/nftables` or just start with the default provided in `/etc/nftables.conf` which already works with IPv4/IPv6.

To get an [iptables](/index.php/Iptables "Iptables")-like chain set up, you will first need to use the provided IPv4 filter file:

```
# nft -f /usr/share/nftables/ipv4-filter

```

To list the resulting chain:

```
# nft list table filter

```

Drop output to a destination:

```
# nft add rule ip filter output ip daddr 1.2.3.4 drop

```

Drop packets destined for local port 80:

```
# nft add rule ip filter input tcp dport 80 drop

```

Delete all rules in a chain:

```
# nft delete rule filter output

```

## Samples

### Simple IP/IPv6 Firewall

 `firewall.rules` 

```
# A simple firewall

flush ruleset

table firewall {
  chain incoming {
    type filter hook input priority 0;

    # established/related connections
    ct state established,related accept

    # invalid connections
    ct state invalid drop

    # loopback interface
    iifname lo accept

    # icmp
    icmp type echo-request accept

    # open tcp ports: sshd (22), httpd (80)
    tcp dport {ssh, http} accept

    # everything else
    drop
  }
}

table ip6 firewall {
  chain incoming {
    type filter hook input priority 0;

    # established/related connections
    ct state established,related accept

    # invalid connections
    ct state invalid drop

    # loopback interface
    iifname lo accept

    # icmp
    # routers may also want: mld-listener-query, nd-router-solicit
    icmpv6 type {echo-request,nd-neighbor-solicit} accept

    # open tcp ports: sshd (22), httpd (80)
    tcp dport {ssh, http} accept

    # everything else
    drop
  }
}

```

### Limit rate IP/IPv6 Firewall

 `firewall.2.rules` 

```
table firewall {
    chain incoming {
        type filter hook input priority 0;

        # no ping floods:
        ip protocol icmp limit rate 10/second accept
        ip protocol icmp drop

        ct state established,related accept
        ct state invalid drop

        iifname lo accept

	# avoid brute force on ssh:
        tcp dport ssh limit rate 15/minute accept

        reject
    }
}

table ip6 firewall {
    chain incoming {
        type filter hook input priority 0;

        # no ping floods:
        ip6 nexthdr icmpv6 limit rate 10/second accept
        ip6 nexthdr icmpv6 drop

        ct state established,related accept
        ct state invalid drop

        # loopback interface
        iifname lo accept

	# avoid brute force on ssh:
        tcp dport ssh limit rate 15/minute accept

        reject
    }
}

```

### Jump

When using jumps in config file, it is necessary to define the target chain first. Otherwise one could end up with `Error: Could not process rule: No such file or directory`.

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

## Practical examples

### Different rules for different interfaces

If your box has more than one network interface, and you'd like to use different rules for different interfaces, you may want to use a "dispatching" filter chain, and then interface-specific filter chains. For example, let's assume your box acts as a home router, you want to run a web server accessible over the LAN (interface nsp3s0), but not from the public internet (interface enp2s0), you may want to consider a structure like this:

```
table inet filter {
  chain input { # this chain serves as a dispatcher
    type filter hook input priority 0;

    iifname lo accept # always accept loopback
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

nftables has a special keyword `masquerade` "where the source address is automagically set to the address of the output interface" ([source](http://wiki.nftables.org/wiki-nftables/index.php/Performing_Network_Address_Translation_%28NAT%29#Masquerading)). This is particularly useful for situations in which the IP address of the interface is unpredictable or unstable, such as the upstream interface of routers connecting to many ISPs. Without it, the Network Address Translation rules would have to be updated every time the IP address of the interface changed.

To use it:

*   use kernel >=3.18 (true if you use the default kernel)
*   make sure masquerading is enabled in the kernel (true if you use the default kernel), otherwise during kernel configuration, set

```
CONFIG_NFT_MASQ=m

```

*   the `masquerade` keyword can only be used in chains of type `nat`, which in turn cannot be contained in a table with family `inet`. Use a table with family `ip` and/or `ip6` instead.
*   masquerading is a kind of source NAT, so only works in the output path.

Example for a machine with two interfaces: LAN connected to `nsp3s0`, and public internet connected to `enp2s0`:

```
table ip nat {
  chain prerouting {
    type nat hook prerouting priority 0;
  }
  chain postrouting {
    type nat hook postrouting priority 0;
    oifname "enp0s2" masquerade
  }
}

```

## Loading rules at boot

To automatically load rules on system boot, simply enable the nftables systemd service by executing `systemctl enable nftables`

The rules will be loaded from `/etc/nftables.conf` by default.

**Note:** You may have to create `/etc/modules-load.d/nftables.conf` with all of the nftables related modules you require as entries for the systemd service to work correctly. You can get a list of modules using this command: `lsmod | grep nf` Otheriwse, you could end up with the dreaded `Error: Could not process rule: No such file or directory` error.

## Logging to Syslog

If you use a Linux kernel < 3.17, you have to modprobe `xt_LOG` to enable logging.

## See also

*   [netfilter nftables wiki](http://people.netfilter.org/wiki-nftables/index.php/)
*   [First release of nftables](https://lwn.net/Articles/324251/)
*   [nftables quick howto](https://home.regit.org/netfilter-en/nftables-quick-howto/)
*   [The return of nftables](https://lwn.net/Articles/564095/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Nftables&oldid=407938](https://wiki.archlinux.org/index.php?title=Nftables&oldid=407938)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Firewalls](/index.php/Category:Firewalls "Category:Firewalls")