A firewall is a system designed to prevent unauthorized access to or from a private network (which could be just one machine). Firewalls can be implemented in only hardware or software, or a combination of both. Firewalls are frequently used to prevent unauthorized Internet users from accessing private networks connected to the Internet, especially intranets. All messages entering or leaving the intranet pass through the firewall, which examines each message and allows, proxys, or denies the traffic based on specified security criteria.

There is a nice list of firewalls [here](http://wiki.debian.org/Firewalls).

There are many posts on the forums about different firewall apps and scripts so here they all are condensed into one page - please add your comments about each firewall, especially ease of use and a security check at [Shields Up](https://www.grc.com/x/ne.dll?bh0bkyd2)

## Contents

*   [1 iptables](#iptables)
*   [2 iptables front-ends](#iptables_front-ends)
    *   [2.1 Arno's Firewall](#Arno's_Firewall)
    *   [2.2 ferm](#ferm)
    *   [2.3 Firehol](#Firehol)
    *   [2.4 Firetable](#Firetable)
    *   [2.5 gShield](#gShield)
    *   [2.6 Shorewall](#Shorewall)
    *   [2.7 uruk](#uruk)
    *   [2.8 ufw](#ufw)
    *   [2.9 Vuurmuur](#Vuurmuur)
*   [3 iptables grafička sučelja](#iptables_grafička_sučelja)
    *   [3.1 Firestarter](#Firestarter)
    *   [3.2 Guarddog](#Guarddog)
    *   [3.3 Gufw](#Gufw)
    *   [3.4 KMyFirewall](#KMyFirewall)
*   [4 Firewall Builder](#Firewall_Builder)

## [iptables](/index.php/Iptables "Iptables")

The Linux kernel itself has very powerful firewall called iptables. Other firewalls are usually just frontends.

See the [iptables article](/index.php/Iptables "Iptables") for more information.

**More info:**

*   [Simple stateful firewall](/index.php/Simple_stateful_firewall_HOWTO "Simple stateful firewall HOWTO")
*   [Router](/index.php/Router "Router")
*   man iptables [http://unixhelp.ed.ac.uk/CGI/man-cgi?iptables+8](http://unixhelp.ed.ac.uk/CGI/man-cgi?iptables+8)
*   [http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/](http://tldp.org/HOWTO/Masquerading-Simple-HOWTO/)
*   [http://netfilter.org/documentation/HOWTO/NAT-HOWTO.html](http://netfilter.org/documentation/HOWTO/NAT-HOWTO.html)
*   [http://www.frozentux.net/documents/iptables-tutorial/](http://www.frozentux.net/documents/iptables-tutorial/)

## iptables front-ends

### Arno's Firewall

[Arno's IPTABLES Firewall Script](http://rocky.eld.leidenuniv.nl/) is a secure firewall for both single and multi-homed machines.

The script:

*   EASY to configure and highly customizable
*   daemon script included
*   a filter script that makes your firewall log more readable

Supports:

*   NAT and SNAT
*   port forwarding
*   ADSL ethernet modems with both static and dynamically assigned IPs
*   MAC address filtering
*   stealth port scan detection
*   DMZ and DMZ-2-LAN forwarding
*   protection against SYN/ICMP flooding
*   extensive user definable logging with rate limiting to prevent log flooding
*   all IP protocols and VPNs such as IPSec
*   plugin support to add extra features.

### ferm

[ferm](http://ferm.foo-projects.org/) (which stands for "For Easy Rule Making") is a tool to maintain complex firewalls, without having the trouble to rewrite the complex rules over and over again. ferm allows the entire firewall rule set to be stored in a separate file, and to be loaded with one command. The firewall configuration resembles structured programming-like language, which can contain levels and lists.

### Firehol

[FireHOL](http://firehol.sourceforge.net/) is a language to express firewalling rules, not just a script that produces some kind of a firewall. It makes building even sophisticated firewalls easy - the way you want it. The result is actually iptables rules.

`firehol` is available in the community repository.

### Firetable

[Firetable](http://projects.leisink.org/firetable) is an iptables-based firewall with "human readable" syntax.

`firetable` is available in [AUR](/index.php/AUR "AUR").

### gShield

[gShield](http://muse.linuxmafia.org/gshield/) is a really simple iptables configuration system. (Nothing to do with gnome) Easy to configure, blocks everything not needed (almost) by default. Controlled by only one configuration file. It gave me all stealth on grc.com

`gshield` is available in [AUR](/index.php/AUR "AUR").

Pros:

*   Easy to configure
*   Only one configuration file
*   Will give you a iptables configuration, which is the best firewall

Cons:

*   No GUI

### Shorewall

[The Shoreline Firewall](http://www.shorewall.net/), more commonly known as "Shorewall", is high-level tool for configuring Netfilter. You describe your firewall/gateway requirements using entries in a set of configuration files. Shorewall reads those configuration files and with the help of the iptables utility, Shorewall configures Netfilter to match your requirements. Shorewall can be used on a dedicated firewall system, a multi-function gateway/router/server or on a standalone GNU/Linux system. Shorewall does not use Netfilter's ipchains compatibility mode and can thus take advantage of Netfilter's connection state tracking capabilities.

`shorewall` is available in the `community` repository.

### uruk

[uruk](http://mdcc.cx/uruk/) loads an rc file, which defines network service access policy, and invokes iptables to set up firewall rules implementing this policy.

uruk is not available in any Arch Linux repository.

### ufw

ufw (uncomplicated firewall) is a simple frontend for iptables and is available in the `community` repository. For a simple firewall with ssh access, perform the following:

```
sudo ufw allow ssh/tcp
sudo ufw logging on
sudo ufw enable

```

This saves the rules for iptables. Edit your rc.conf to enable ufw at boot (in DAEMONS array).

ufw also has the capability of package provided or custom created application rules via the /etc/ufw/applications.d/ directory. For applications like [Samba](/index.php/Samba "Samba") which utilizes multiple UDP and TCP ports an application rule file makes enabling all ports easy:

```
sudo vi /etc/ufw/applications.d/samba

```

```
[Samba]
title=Windows file and printer server for Unix
description=Tools to access a server's filespace and printers via SMB
ports=137,138/udp|139,445/tcp

```

Note the "|" is used to separate the UDP ports and the TCP ports. Commas are used to separate the port numbers themselves.

For applications that utilize different ports depending on configuration, like [Apache](/index.php/Apache "Apache"), rule files can contain multiple rule sets.

```
sudo vi /etc/ufw/applications.d/apache

```

```
[Apache]
title=Web Server
description=A high performance Unix-based HTTP server
ports=80/tcp

[Apache Secure]
title=Web Server (HTTPS)
description=A high performance Unix-based HTTP server
ports=443/tcp

[Apache Full]
title=Web Server (HTTP,HTTPS)
description=A high performance Unix-based HTTP server
ports=80,443/tcp

```

To list the available application settings use:

```
sudo ufw app list
Available applications:
 Apache
 Apache Full
 Apache Secure
 Samba

```

To enable just [Apache](/index.php/Apache "Apache")'s HTTPS service:

```
sudo ufw allow Apache Secure

```

To enable access to [Samba](/index.php/Samba "Samba") only within your LAN:

```
sudo ufw allow from 192.168.0.0/24 to any app Samba

```

Further Documentation and Source Citation: [Ubuntu Firewall Help](https://help.ubuntu.com/community/UFW)

### Vuurmuur

[Vuurmuur](http://www.vuurmuur.org/) Vuurmuur is a powerful firewall manager built on top of iptables. It has a simple and easy to learn configuration that allows both simple and complex configurations. The configuration can be fully configured through an ncurses GUI, which allows secure remote administration through SSH or on the console. Vuurmuur supports traffic shaping, has powerful monitoring features, which allow the administrator to look at the logs, connections and bandwidth usage in realtime.

`Vuurmuur` and is available in [AUR](/index.php/AUR "AUR").

## iptables grafička sučelja

### Firestarter

[Firestarter](http://www.fs-security.com/) je dobro grafičko sučelje, ima mogućnost da koristi crnu i belu listu za regulaciju prometa, veoma je jednostavan za upotrebu, sa odličnim uputstvom dostupnim na njihovom sajtu.

Firestarter ima gnome međuzavisnosti i dostupan je iz [AUR](/index.php/AUR "AUR") riznice.

### Guarddog

[Guarddog](http://www.simonzone.com/software/guarddog/)je zaista lagan program za konfigurisanje iptables. Nakon podešavanja osnovnih parametara, prolazi sve zaštitne testove.

Guarddog zahteva kdelibs3 i dostupan je u [AUR](/index.php/AUR "AUR") riznici.

Da bi se firewall podešavanja primenila prilikom pokretanja računara */etc/rc.firewall* iznutra */etc/rc.local* ili nešto slično.

### Gufw

[Gufw](http://gufw.tuxfamily.org/index.html) je lagan za upotrebu Ubuntu / Linux firewall, od [ufw](/index.php/Firewalls#ufw "Firewalls").

Gufw je lagan, intuitivan, za upravljanje Linux firewall.

### KMyFirewall

[KMyFirewall](http://kmyfirewall.sourceforge.net/) je KDE3 GUI za iptables.

Ovaj firewall je dovoljno uprošten da ga i početnici mogu koristiti, ali takođe poseduje i sofisticirana podešavanja za napredne korisnike.

KMyFirewall zahteva kdelibs3 i dostupan je u [AUR](/index.php/AUR "AUR") riznici.

## Firewall Builder

[Firewall Builder](http://www.fwbuilder.org/) is "a GUI firewall configuration and management tool that supports iptables (netfilter), ipfilter, pf, ipfw, Cisco PIX (FWSM, ASA) and Cisco routers extended access lists. [...] The program runs on Linux, FreeBSD, OpenBSD, Windows and Mac OS X and can manage both local and remote firewalls." Source: [http://www.fwbuilder.org/](http://www.fwbuilder.org/)

`fwbuilder` is available in the `extra` repository.