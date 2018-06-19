Related articles

*   [Fail2ban](/index.php/Fail2ban "Fail2ban")
*   [Nftables](/index.php/Nftables "Nftables")
*   [Sshguard](/index.php/Sshguard "Sshguard")
*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Sysctl#TCP/IP stack hardening](/index.php/Sysctl#TCP.2FIP_stack_hardening "Sysctl")

*iptables* is a command line utility for configuring Linux kernel [firewall](/index.php/Firewall "Firewall") implemented within the [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") project. The term *iptables* is also commonly used to refer to this kernel-level firewall. It can be configured directly with iptables, or by using one of the many [frontends](#Console_frontends) and [GUIs](#Graphic_frontends). *iptables* is used for [IPv4](https://en.wikipedia.org/wiki/IPv4 "wikipedia:IPv4") and *ip6tables* is used for [IPv6](/index.php/IPv6 "IPv6"). Both *iptables* and *ip6tables* have the same syntax, but some options are specific to either IPv4 or IPv6.

[nftables](/index.php/Nftables "Nftables") was released in [release with Linux kernel 3.13](http://www.phoronix.com/scan.php?page=news_item&px=MTQ5MDU), and will one day replace iptables as the main Linux firewall utility.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Front-ends](#Front-ends)
        *   [1.1.1 Console](#Console)
        *   [1.1.2 Graphical](#Graphical)
*   [2 Basic concepts](#Basic_concepts)
    *   [2.1 Tables](#Tables)
    *   [2.2 Chains](#Chains)
    *   [2.3 Rules](#Rules)
    *   [2.4 Traversing Chains](#Traversing_Chains)
    *   [2.5 Modules](#Modules)
*   [3 Configuration and usage](#Configuration_and_usage)
    *   [3.1 From the command line](#From_the_command_line)
        *   [3.1.1 Showing the current rules](#Showing_the_current_rules)
        *   [3.1.2 Resetting rules](#Resetting_rules)
        *   [3.1.3 Editing rules](#Editing_rules)
    *   [3.2 Guides](#Guides)
*   [4 Logging](#Logging)
    *   [4.1 Limiting log rate](#Limiting_log_rate)
    *   [4.2 Viewing logged packets](#Viewing_logged_packets)
    *   [4.3 syslog-ng](#syslog-ng)
    *   [4.4 ulogd](#ulogd)
*   [5 See also](#See_also)

## Installation

The stock Arch Linux kernel is compiled with iptables support. You will only need to [install](/index.php/Install "Install") the userland utilities, which are provided by the package [iptables](https://www.archlinux.org/packages/?name=iptables). (The [iproute2](https://www.archlinux.org/packages/?name=iproute2) package from the [base](https://www.archlinux.org/groups/x86_64/base/) group depends on iptables, so the iptables package should be installed on your system by default.)

### Front-ends

#### Console

*   **Arno's firewall** — Secure firewall for both single and multi-homed machines. Very easy to configure, handy to manage and highly customizable. Supports: NAT and SNAT, port forwarding, ADSL ethernet modems with both static and dynamically assigned IPs, MAC address filtering, stealth port scan detection, DMZ and DMZ-2-LAN forwarding, protection against SYN/ICMP flooding, extensive user definable logging with rate limiting to prevent log flooding, all IP protocols and VPNs such as IPsec, plugin support to add extra features.

	[http://rocky.eld.leidenuniv.nl/](http://rocky.eld.leidenuniv.nl/) || [arno-iptables-firewall](https://aur.archlinux.org/packages/arno-iptables-firewall/)

*   **ferm** — Tool to maintain complex firewalls, without having the trouble to rewrite the complex rules over and over again. It allows the entire firewall rule set to be stored in a separate file, and to be loaded with one command. The firewall configuration resembles structured programming-like language, which can contain levels and lists.

	[http://ferm.foo-projects.org/](http://ferm.foo-projects.org/) || [ferm](https://www.archlinux.org/packages/?name=ferm)

*   **[FireHOL](https://en.wikipedia.org/wiki/FireHOL "wikipedia:FireHOL")** — Language to express firewalling rules, not just a script that produces some kind of a firewall. It makes building even sophisticated firewalls easy - the way you want it.

	[http://firehol.sourceforge.net/](http://firehol.sourceforge.net/) || [firehol](https://aur.archlinux.org/packages/firehol/)

*   **Firetable** — Tool to maintain an IPtables firewall. Each interface can be configured separately via its own configuration file, which holds an easy and human readable syntax.

	[https://gitlab.com/hsleisink/firetable](https://gitlab.com/hsleisink/firetable) || [firetable](https://aur.archlinux.org/packages/firetable/)

*   **[firewalld](https://en.wikipedia.org/wiki/firewalld "wikipedia:firewalld") (firewall-cmd)** — Daemon and console interface for configuring network and firewall zones as well as setting up and configuring firewall rules.

	[https://firewalld.org/](https://firewalld.org/) || [firewalld](https://www.archlinux.org/packages/?name=firewalld)

*   **[Shorewall](/index.php/Shorewall "Shorewall")** — High-level tool for configuring Netfilter. You describe your firewall/gateway requirements using entries in a set of configuration files.

	[http://www.shorewall.net/](http://www.shorewall.net/) || [shorewall](https://www.archlinux.org/packages/?name=shorewall)

*   **[Uncomplicated Firewall](/index.php/Ufw "Ufw")** — Simple front-end for iptables.

	[https://launchpad.net/ufw](https://launchpad.net/ufw) || [ufw](https://www.archlinux.org/packages/?name=ufw)

*   **[PeerGuardian](/index.php/PeerGuardian_Linux "PeerGuardian Linux") (pglcmd)** — Privacy oriented firewall application. It blocks connections to and from hosts specified in huge block lists (thousands or millions of IP ranges).

	[http://sourceforge.net/projects/peerguardian/](http://sourceforge.net/projects/peerguardian/) || [pgl](https://aur.archlinux.org/packages/pgl/)

*   **Vuurmuur** — Powerful firewall manager. It has a simple and easy to learn configuration that allows both simple and complex configurations. The configuration can be fully configured through an [ncurses](https://www.archlinux.org/packages/?name=ncurses) GUI, which allows secure remote administration through SSH or on the console. Vuurmuur supports traffic shaping, has powerful monitoring features, which allow the administrator to look at the logs, connections and bandwidth usage in realtime.

	[https://www.vuurmuur.org/](https://www.vuurmuur.org/) || [vuurmuur](https://aur.archlinux.org/packages/vuurmuur/)

#### Graphical

*   **Firewall Builder** — GUI firewall configuration and management tool that supports iptables (netfilter), ipfilter, pf, ipfw, Cisco PIX (FWSM, ASA) and Cisco routers extended access lists. The program runs on Linux, FreeBSD, OpenBSD, Windows and macOS and can manage both local and remote firewalls.

	[http://fwbuilder.sourceforge.net/](http://fwbuilder.sourceforge.net/) || [fwbuilder](https://www.archlinux.org/packages/?name=fwbuilder)

*   **[firewalld](https://en.wikipedia.org/wiki/firewalld "wikipedia:firewalld") (firewall-config)** — Daemon and graphical interface for configuring network and firewall zones as well as setting up and configuring firewall rules.

	[https://firewalld.org/](https://firewalld.org/) || [firewalld](https://www.archlinux.org/packages/?name=firewalld)

*   **[Gufw](/index.php/Uncomplicated_Firewall#Gufw "Uncomplicated Firewall")** — GTK-based front-end to [ufw](https://www.archlinux.org/packages/?name=ufw) which happens to be a CLI front-end to iptables (gufw->ufw->iptables), is super easy and super simple to use.

	[http://gufw.org/](http://gufw.org/) || [gufw](https://www.archlinux.org/packages/?name=gufw)

*   **[PeerGuardian](/index.php/PeerGuardian_Linux "PeerGuardian Linux") GUI (pglgui)** — Privacy oriented firewall application. It blocks connections to and from hosts specified in huge block lists (thousands or millions of IP ranges).

	[http://sourceforge.net/projects/peerguardian/](http://sourceforge.net/projects/peerguardian/) || [pgl](https://aur.archlinux.org/packages/pgl/)

## Basic concepts

iptables is used to inspect, modify, forward, redirect, and/or drop IPv4 packets. The code for filtering IPv4 packets is already built into the kernel and is organized into a collection of *tables*, each with a specific purpose. The tables are made up of a set of predefined *chains*, and the chains contain rules which are traversed in order. Each rule consists of a predicate of potential matches and a corresponding action (called a *target*) which is executed if the predicate is true; i.e. the conditions are matched. iptables is the user utility which allows you to work with these chains/rules. Most new users find the complexities of linux IP routing quite daunting, but, in practice, the most common use cases (NAT and/or basic Internet firewall) are considerably less complex.

The key to understanding how iptables works is [this chart](http://www.frozentux.net/iptables-tutorial/images/tables_traverse.jpg). The lowercase word on top is the table and the upper case word below is the chain. Every IP packet that comes in *on any network interface* passes through this flow chart from top to bottom. A common source of confusion is that packets entering from, say, an internal interface are handled differently than packets from an Internet-facing interface. All interfaces are handled the same way; it's up to you to define rules that treat them differently. Of course some packets are intended for local processes, hence come in from the top of the chart and stop at <Local Process>, while other packets are generated by local processes; hence start at <Local Process> and proceed downward through the flowchart. A detailed explanation of how this flow chart works can be found [here](http://www.frozentux.net/iptables-tutorial/iptables-tutorial.html#TRAVERSINGOFTABLES).

In the vast majority of use cases you won't need to use the **raw**, **mangle**, or **security** tables at all. Consequently, the following chart depicts a simplified network packet flow through *iptables*:

```
                               XXXXXXXXXXXXXXXXXX
                             XXX     Network    XXX
                               XXXXXXXXXXXXXXXXXX
                                       +
                                       |
                                       v
 +-------------+              +------------------+
 |table: filter| <---+        | table: nat       |
 |chain: INPUT |     |        | chain: PREROUTING|
 +-----+-------+     |        +--------+---------+
       |             |                 |
       v             |                 v
 [local process]     |           ****************          +--------------+
       |             +---------+ Routing decision +------> |table: filter |
       v                         ****************          |chain: FORWARD|
****************                                           +------+-------+
Routing decision                                                  |
****************                                                  |
       |                                                          |
       v                        ****************                  |
+-------------+       +------>  Routing decision  <---------------+
|table: nat   |       |         ****************
|chain: OUTPUT|       |               +
+-----+-------+       |               |
      |               |               v
      v               |      +-------------------+
+--------------+      |      | table: nat        |
|table: filter | +----+      | chain: POSTROUTING|
|chain: OUTPUT |             +--------+----------+
+--------------+                      |
                                      v
                               XXXXXXXXXXXXXXXXXX
                             XXX    Network     XXX
                               XXXXXXXXXXXXXXXXXX

```

### Tables

iptables contains five tables:

1.  `raw` is used only for configuring packets so that they are exempt from connection tracking.
2.  `filter` is the default table, and is where all the actions typically associated with a firewall take place.
3.  `nat` is used for [network address translation](https://en.wikipedia.org/wiki/Network_address_translation "wikipedia:Network address translation") (e.g. port forwarding).
4.  `mangle` is used for specialized packet alterations.
5.  `security` is used for [Mandatory Access Control](/index.php/Security#Mandatory_access_control "Security") networking rules (e.g. SELinux -- see [this article](http://lwn.net/Articles/267140/) for more details).

In most common use cases you will only use two of these: **filter** and **nat**. The other tables are aimed at complex configurations involving multiple routers and routing decisions and are in any case beyond the scope of these introductory remarks.

### Chains

Tables consist of *chains*, which are lists of rules which are followed in order. The default table, `filter`, contains three built-in chains: `INPUT`, `OUTPUT` and `FORWARD` which are activated at different points of the packet filtering process, as illustrated in the [flow chart](http://www.frozentux.net/iptables-tutorial/chunkyhtml/images/tables_traverse.jpg). The nat table includes `PREROUTING`, `POSTROUTING`, and `OUTPUT` chains.

See [iptables(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8) for a description of built-in chains in other tables.

By default, none of the chains contain any rules. It is up to you to append rules to the chains that you want to use. Chains *do* have a default policy, which is generally set to `ACCEPT`, but can be reset to `DROP`, if you want to be sure that nothing slips through your ruleset. The default policy always applies at the end of a chain only. Hence, the packet has to pass through all existing rules in the chain before the default policy is applied.

User-defined chains can be added to make rulesets more efficient or more easily modifiable. See [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") for an example of how user-defined chains are used.

### Rules

Packet filtering is based on *rules*, which are specified by multiple *matches* (conditions the packet must satisfy so that the rule can be applied), and one *target* (action taken when the packet matches all conditions). The typical things a rule might match on are what interface the packet came in on (e.g eth0 or eth1), what type of packet it is (ICMP, TCP, or UDP), or the destination port of the packet.

Targets are specified using the `-j` or `--jump` option. Targets can be either user-defined chains (i.e. if these conditions are matched, jump to the following user-defined chain and continue processing there), one of the special built-in targets, or a target extension. Built-in targets are `ACCEPT`, `DROP`, `QUEUE` and `RETURN`, target extensions are, for example, `REJECT` and `LOG`. If the target is a built-in target, the fate of the packet is decided immediately and processing of the packet in current table is stopped. If the target is a user-defined chain and the fate of the packet is not decided by this second chain, it will be filtered against the remaining rules of the original chain. Target extensions can be either *terminating* (as built-in targets) or *non-terminating* (as user-defined chains), see [iptables-extensions(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iptables-extensions.8) for details.

### Traversing Chains

A network packet received on any interface traverses the traffic control chains of tables in the order shown in the [flow chart](http://www.frozentux.net/iptables-tutorial/chunkyhtml/images/tables_traverse.jpg). The first routing decision involves deciding if the final destination of the packet is the local machine (in which case the packet traverses through the `INPUT` chains) or elsewhere (in which case the packet traverses through the `FORWARD` chains). Subsequent routing decisions involve deciding what interface to assign to an outgoing packet. At each chain in the path, every rule in that chain is evaluated in order and whenever a rule matches, the corresponding target/jump action is executed. The 3 most commonly used targets are `ACCEPT`, `DROP`, and jump to a user-defined chain. While built-in chains can have default policies, user-defined chains can not. If every rule in a chain that you jumped fails to provide a complete match, the packet is dropped back into the calling chain as illustrated [here](http://www.frozentux.net/iptables-tutorial/images/table_subtraverse.jpg). If at any time a complete match is achieved for a rule with a `DROP` target, the packet is dropped and no further processing is done. If a packet is `ACCEPT`ed within a chain, it will be `ACCEPT`ed in all superset chains also and it will not traverse any of the superset chains any further. However, be aware that the packet will continue to traverse all other chains in other tables in the normal fashion.

### Modules

There are many modules which can be used to extend iptables such as connlimit, conntrack, limit and recent. These modules add extra functionality to allow complex filtering rules.

## Configuration and usage

iptables is a [systemd](/index.php/Systemd "Systemd") service and is [started](/index.php/Start "Start") accordingly. However, the service won't start unless it finds an `/etc/iptables/iptables.rules` file, which is not provided by the Arch [iptables](https://www.archlinux.org/packages/?name=iptables) package. So to start the service for the first time:

```
# touch /etc/iptables/iptables.rules

```

or

```
# cp /etc/iptables/empty.rules /etc/iptables/iptables.rules

```

Then [start](/index.php/Start "Start") the `iptables.service` unit. As with other services, if you want iptables to be loaded automatically on boot, you must [enable](/index.php/Enable "Enable") it.

iptables rules for IPv6 are, by default, stored in `/etc/iptables/ip6tables.rules`, which is read by `ip6tables.service`. You can start it the same way as above.

After adding rules via command-line as shown in the following sections, the configuration file is not changed automatically — you have to save it manually:

```
# iptables-save > /etc/iptables/iptables.rules

```

If you edit the configuration file manually, you have to [reload](/index.php/Reload "Reload") iptables.

Or you can load it directly through iptables:

```
# iptables-restore < /etc/iptables/iptables.rules

```

### From the command line

#### Showing the current rules

The basic command to list current rules is `--list-rules` (`-S`), which is similar in output format to the *iptables-save* utility. The main difference of the two is that the latter outputs the rules of all tables per default, while all *iptables* commands default to the `filter` table only.

When working with iptables on the command line, the `--list` (`-L`) command accepts more modifiers and shows more information. For example, you can check the current ruleset and the number of hits per rule by using the command:

 `# iptables -nvL` 
```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
 pkts bytes target     prot opt in     out     source               destination
```

If the output looks like the above, then there are no rules (i.e. nothing is blocked) in the default `filter` table. An other table can be specified with the `-t` option.

To show the line numbers when listing rules, append `--line-numbers` to that input. The line numbers are a useful shorthand when [#Editing rules](#Editing_rules) on the command line.

#### Resetting rules

You can flush and reset iptables to default using these commands:

```
# iptables -F
# iptables -X
# iptables -t nat -F
# iptables -t nat -X
# iptables -t mangle -F
# iptables -t mangle -X
# iptables -t raw -F
# iptables -t raw -X
# iptables -t security -F
# iptables -t security -X
# iptables -P INPUT ACCEPT
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT ACCEPT

```

The `-F` command with no arguments flushes all the chains in its current table. Similarly, `-X` deletes all empty non-default chains in a table.

Individual chains may be flushed or deleted by following `-F` and `-X` with a `[chain]` argument.

#### Editing rules

Rules can be edited by appending `-A` a rule to a chain, inserting `-I` it at a specific position on the chain, replacing `-R` an existing rule, or deleting `-D` it. The first three commands are exemplified in the following.

First of all, our computer is not a router (unless, of course, it [is a router](/index.php/Router "Router")). We want to change the default policy on the `FORWARD` chain from `ACCEPT` to `DROP`.

```
# iptables -P FORWARD DROP

```

**Warning:** The rest of this section is meant to teach the syntax and concepts behind iptables rules. It is not intended as a means for securing servers. For improving the security of your system, see [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") for a minimally secure iptables configuration and [Security](/index.php/Security "Security") for hardening Arch Linux in general.

The [Dropbox](https://en.wikipedia.org/wiki/Dropbox_(service) LAN sync feature [broadcasts packets every 30 seconds](https://isc.sans.edu/port.html?port=17500) to all computers it can see. If we happen to be on a LAN with Dropbox clients and do not use this feature, then we might wish to reject those packets.

```
# iptables -A INPUT -p tcp --dport 17500 -j REJECT --reject-with icmp-port-unreachable

```

```
# iptables -nvL --line-numbers

```

```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

**Note:** We use `REJECT` rather than `DROP` here, because [RFC 1122 3.3.8](https://tools.ietf.org/html/rfc1122#page-69) requires hosts return ICMP errors whenever possible, instead of dropping packets. [This page](http://www.chiark.greenend.org.uk/~peterb/network/drop-vs-reject) explains why it is almost always better to REJECT rather than DROP packets.

Now, say we change our mind about Dropbox and decide to install it on our computer. We also want to LAN sync, but only with one particular IP on our network. So we should use `-R` to replace our old rule. Where `10.0.0.85` is our other IP:

```
# iptables -R INPUT 1 -p tcp --dport 17500 ! -s 10.0.0.85 -j REJECT --reject-with icmp-port-unreachable

```

```
# iptables -nvL --line-numbers

```

```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 REJECT     tcp  --  *      *      !10.0.0.85            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

We have now replaced our original rule with one that allows `10.0.0.85` to access port `17500` on our computer. But now we realize that this is not scalable. If our friendly Dropbox user is attempting to access port `17500` on our device, we should allow him immediately, not test him against any firewall rules that might come afterwards!

So we write a new rule to allow our trusted user immediately. Using `-I` to insert the new rule before our old one:

```
# iptables -I INPUT -p tcp --dport 17500 -s 10.0.0.85 -j ACCEPT -m comment --comment "Friendly Dropbox"

```

```
# iptables -nvL --line-numbers

```

```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 ACCEPT     tcp  --  *      *       10.0.0.85            0.0.0.0/0            tcp dpt:17500 /* Friendly Dropbox */
2        0     0 REJECT     tcp  --  *      *      !10.0.0.85            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

And replace our second rule with one that rejects everything on port `17500`:

```
# iptables -R INPUT 2 -p tcp --dport 17500 -j REJECT --reject-with icmp-port-unreachable

```

Our final rule list now looks like this:

```
# iptables -nvL --line-numbers

```

```
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination
1        0     0 ACCEPT     tcp  --  *      *       10.0.0.85            0.0.0.0/0            tcp dpt:17500 /* Friendly Dropbox */
2        0     0 REJECT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:17500 reject-with icmp-port-unreachable

Chain FORWARD (policy DROP 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

Chain OUTPUT (policy ACCEPT 0 packets, 0 bytes)
num   pkts bytes target     prot opt in     out     source               destination

```

### Guides

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Router](/index.php/Router "Router")

## Logging

The `LOG` target can be used to log packets that hit a rule. Unlike other targets like `ACCEPT` or `DROP`, the packet will continue moving through the chain after hitting a `LOG` target. This means that in order to enable logging for all dropped packets, you would have to add a duplicate `LOG` rule before each DROP rule. Since this reduces efficiency and makes things less simple, a `logdrop` chain can be created instead.

Create the chain with:

```
# iptables -N logdrop

```

And add the following rules to the newly created chain:

```
# iptables -A logdrop -m limit --limit 5/m --limit-burst 10 -j LOG
# iptables -A logdrop -j DROP

```

Explanation for `limit` and `limit-burst` options is given [below](#Limiting_log_rate).

Now whenever we want to drop a packet and log this event, we just jump to the `logdrop` chain, for example:

```
# iptables -A INPUT -m conntrack --ctstate INVALID -j logdrop

```

### Limiting log rate

The above `logdrop` chain uses the limit module to prevent the *iptables* log from growing too large or causing needless hard drive writes. Without limiting an erroneously configured service trying to connect, or an attacker, could fill the drive (or at least the `/var` partition) by causing writes to the iptables log.

The limit module is called with `-m limit`. You can then use `--limit` to set an average rate and `--limit-burst` to set an initial burst rate. In the `logdrop` example above:

```
iptables -A logdrop -m limit --limit 5/m --limit-burst 10 -j LOG

```

appends a rule which will log all packets that pass through it. The first 10 consecutive packets will be logged, and from then on only 5 packets per minute will be logged. The "limit burst" count is reset every time the "limit rate" is not broken, i.e. logging activity returns to normal automatically.

### Viewing logged packets

Logged packets are visible as kernel messages in the [systemd journal](/index.php/Systemd_journal "Systemd journal").

To view all packets that were logged since the machine was last booted:

```
# journalctl -k | grep "IN=.*OUT=.*" | less

```

### syslog-ng

Assuming you are using [syslog-ng](/index.php/Syslog-ng "Syslog-ng"), you can control where iptables' log output goes this way:

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv); };

```

to

```
filter f_everything { level(debug..emerg) and not facility(auth, authpriv) and not filter(f_iptables); };

```

This will stop logging iptables output to `/var/log/everything.log`.

If you also want iptables to log to a different file than `/var/log/iptables.log`, you can simply change the file value of destination `d_iptables` here (still in `syslog-ng.conf`)

```
destination d_iptables { file("/var/log/iptables.log"); };

```

### ulogd

[ulogd](http://www.netfilter.org/projects/ulogd/index.html) is a specialized userspace packet logging daemon for netfilter that can replace the default `LOG` target. The package [ulogd](https://www.archlinux.org/packages/?name=ulogd) is available in the `[community]` repository.

## See also

*   [Wikipedia article](https://en.wikipedia.org/wiki/iptables "wikipedia:iptables")
*   [Port knocking](/index.php/Port_knocking "Port knocking")
*   [Official iptables web site](http://www.netfilter.org/projects/iptables/index.html)
*   [iptables Tutorial 1.2.2](http://www.frozentux.net/iptables-tutorial/iptables-tutorial.html) by Oskar Andreasson
*   [Debian Wiki - iptables](https://wiki.debian.org/iptables "debian:iptables")
*   [Secure use of connection tracking helpers](https://home.regit.org/netfilter-en/secure-use-of-helpers/)