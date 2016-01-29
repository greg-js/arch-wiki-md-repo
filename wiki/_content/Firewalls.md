# Firewalls

A firewall is a system designed to prevent unauthorized access to or from a private network (which could be just one machine). Firewalls can be implemented in only hardware or software, or a combination of both. Firewalls are frequently used to prevent unauthorized Internet users from accessing private networks connected to the Internet, especially intranets. All messages entering or leaving the intranet pass through the firewall, which examines each message and allows, proxys, or denies the traffic based on specified security criteria.

The firewalls listed in this article are overwhelmingly based on the [iptables](/index.php/Iptables "Iptables") program. Consider configuring the iptables process yourself according to its wiki page (listed below) to keep to the [The Arch Way](/index.php/The_Arch_Way "The Arch Way").

There are many posts on the forums about different firewall apps and scripts so here they all are condensed into one page - please add your comments about each firewall, especially ease of use and a security check at [Shields Up](http://www.grc.com/x/ne.dll?bh0bkyd2).

**Note:** Checks at Shields Up are only a valid measure of your router should you have one in the LAN. To accurately evaluate a software firewall, one needs to directly connect the box to the cable modem.

## Contents

*   [1 Firewall guides and tutorials](#Firewall_guides_and_tutorials)
    *   [1.1 External firewall tutorials](#External_firewall_tutorials)
*   [2 iptables](#iptables)
    *   [2.1 Console frontends](#Console_frontends)
    *   [2.2 Graphic frontends](#Graphic_frontends)
*   [3 nftables](#nftables)
*   [4 Other](#Other)
*   [5 See Also](#See_Also)

## Firewall guides and tutorials

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") - Setting up a comprehensive firewall with [iptables](/index.php/Iptables "Iptables").
*   [Uncomplicated Firewall](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") - the wiki page for the simple [iptables](/index.php/Iptables "Iptables") frontend, [ufw](https://www.archlinux.org/packages/?name=ufw), provides a nice tutorial for a basic configuration.
*   [Router](/index.php/Router "Router") Setup Guide - A tutorial for turning a computer into an [internet gateway/router](https://en.wikipedia.org/wiki/Router_(computing) "wikipedia:Router (computing)"). It focuses on [security](/index.php/Security "Security") and configuring your gateway to have as few insecure holes to the internet as possible.

#### External firewall tutorials

*   [http://www.frozentux.net/documents/iptables-tutorial/](http://www.frozentux.net/documents/iptables-tutorial/) A complete and simple tutorial to [iptables](/index.php/Iptables "Iptables").
*   [http://www.ibiblio.org/pub/linux/docs/HOWTO/other-formats/html_single/IP-Masquerade-HOWTO.html](http://www.ibiblio.org/pub/linux/docs/HOWTO/other-formats/html_single/IP-Masquerade-HOWTO.html) Masq is a form of Network Address Translation or NAT that allows internally networked computers that do not have one or more registered Internet IP addresses to have the ability to communicate to the Internet via your Linux boxes single Internet IP address.
*   [http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/](http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/) Masquerading, [transparent proxying](https://en.wikipedia.org/wiki/Proxy_server#Transparent_proxy "wikipedia:Proxy server"), [port forwarding](https://en.wikipedia.org/wiki/Port_forwarding "wikipedia:Port forwarding"), and other forms of [Network Address Translations](https://en.wikipedia.org/wiki/Network_address_translation "wikipedia:Network address translation") with the 2.4 Linux Kernels.

## iptables

The Linux kernel includes [iptables](/index.php/Iptables "Iptables") as a built-in firewall solution. Configuration may be managed directly through the userspace utilities or by installing one of several GUI configuration tools.

### Console frontends

*   **Arno's firewall** — Secure firewall for both single and multi-homed machines. Very easy to configure, handy to manage and highly customizable. Supports: NAT and SNAT, port forwarding, ADSL ethernet modems with both static and dynamically assigned IPs, MAC address filtering, stealth port scan detection, DMZ and DMZ-2-LAN forwarding, protection against SYN/ICMP flooding, extensive user definable logging with rate limiting to prevent log flooding, all IP protocols and VPNs such as IPsec, plugin support to add extra features.

NaN

*   **ferm** — Tool to maintain complex firewalls, without having the trouble to rewrite the complex rules over and over again. It allows the entire firewall rule set to be stored in a separate file, and to be loaded with one command. The firewall configuration resembles structured programming-like language, which can contain levels and lists.

NaN

*   **Firehol** — Language to express firewalling rules, not just a script that produces some kind of a firewall. It makes building even sophisticated firewalls easy - the way you want it.

NaN

*   **Firetable** — Firewall with "human readable" syntax.

NaN

*   **[Shorewall](/index.php/Shorewall "Shorewall")** — High-level tool for configuring Netfilter. You describe your firewall/gateway requirements using entries in a set of configuration files.

NaN

*   **[ufw](/index.php/Ufw "Ufw")** — Simple front-end for iptables.

NaN

*   **[PeerGuardian Linux](/index.php/PeerGuardian_Linux "PeerGuardian Linux")** — Privacy oriented firewall application. It blocks connections to and from hosts specified in huge block lists (thousands or millions of IP ranges).

NaN

*   **Vuurmuur** — Powerful firewall manager. It has a simple and easy to learn configuration that allows both simple and complex configurations. The configuration can be fully configured through an [ncurses](https://www.archlinux.org/packages/?name=ncurses) GUI, which allows secure remote administration through SSH or on the console. Vuurmuur supports traffic shaping, has powerful monitoring features, which allow the administrator to look at the logs, connections and bandwidth usage in realtime.

NaN

### Graphic frontends

*   **Firestarter** — Good GUI for iptables writen on GTK2, it has the ability to use both white and black lists for regulating traffic, it is very simple and easy to use, with good documentation available on their website.

NaN

*   **Firewall Builder** — GUI firewall configuration and management tool that supports iptables (netfilter), ipfilter, pf, ipfw, Cisco PIX (FWSM, ASA) and Cisco routers extended access lists. The program runs on Linux, FreeBSD, OpenBSD, Windows and Mac OS X and can manage both local and remote firewalls.

NaN

*   **firewalld** — Daemon and graphical interface for configuring network and firewall zones as well as setting up and configuring firewall rules.

NaN

*   **[Gufw](/index.php/Uncomplicated_Firewall#Gufw "Uncomplicated Firewall")** — GTK-based front-end to [ufw](https://www.archlinux.org/packages/?name=ufw) which happens to be a CLI front-end to iptables (gufw->ufw->iptables), is super easy and super simple to use.

NaN

*   **KMyFirewall** — KDE3 GUI for iptables. Firewall editing capabilities are simple enough to use to be suitable for beginners, but also allow for sophisticated tweaking of the firewall settings.

NaN

*   **[PeerGuardian Linux](/index.php/PeerGuardian_Linux "PeerGuardian Linux")** — Privacy oriented firewall application. It blocks connections to and from hosts specified in huge block lists (thousands or millions of IP ranges).

NaN

*   **[kcm-ufw](/index.php/Uncomplicated_Firewall#kcm-ufw "Uncomplicated Firewall")** — KDE alternative to Gufw.

NaN

## nftables

[nftables](/index.php/Nftables "Nftables") is a netfilter project that aims to replace the existing ip-, ip6-, arp-, and ebtables framework. It is supposed to replace iptables one day.

## Other

*   **[EtherApe](https://en.wikipedia.org/wiki/EtherApe "wikipedia:EtherApe")** — Graphical network monitor for various OSI layers and protocols.

NaN

*   **[Fail2ban](/index.php/Fail2ban "Fail2ban")** — Bans IPs after too many failed authentification attempts against common daemons.

NaN

## See Also

*   [http://wiki.debian.org/Firewalls](http://wiki.debian.org/Firewalls) - Debian Wiki's list of firewalls

Retrieved from "[https://wiki.archlinux.org/index.php?title=Firewalls&oldid=416044](https://wiki.archlinux.org/index.php?title=Firewalls&oldid=416044)"