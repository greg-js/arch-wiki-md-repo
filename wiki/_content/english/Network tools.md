Related articles

*   [Telnet](/index.php/Telnet "Telnet")
*   [Nmap](/index.php/Nmap "Nmap")
*   [Wireshark](/index.php/Wireshark "Wireshark")

This page lists various network tools. *ping* and *ip* are covered by [Network configuration](/index.php/Network_configuration "Network configuration").

## Contents

*   [1 Traceroute](#Traceroute)
*   [2 Netcat](#Netcat)
*   [3 Whois](#Whois)
*   [4 inetd](#inetd)
*   [5 See also](#See_also)

## Traceroute

[Traceroute](https://en.wikipedia.org/wiki/Traceroute "wikipedia:Traceroute") is a tool to display the path of packets across an IP network.

There are several implementations available:

*   [tracepath(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracepath.8) from [iputils](https://www.archlinux.org/packages/?name=iputils) (part of [base](https://www.archlinux.org/groups/x86_64/base/))
*   [traceroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/traceroute.8) from [traceroute](https://www.archlinux.org/packages/?name=traceroute)
*   **MTR** — Combines the functionality of traceroute and ping into one tool.

	[http://www.bitwizard.nl/mtr/](http://www.bitwizard.nl/mtr/) || [mtr](https://www.archlinux.org/packages/?name=mtr), [mtr-gtk](https://www.archlinux.org/packages/?name=mtr-gtk)

## Netcat

See also [Wikipedia:Netcat](https://en.wikipedia.org/wiki/Netcat "wikipedia:Netcat").

*   **GNU Netcat** — GNU rewrite of netcat, the network piping application.

	[http://netcat.sourceforge.net/](http://netcat.sourceforge.net/) || [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat)

*   **openbsd-netcat** — TCP/IP swiss army knife. OpenBSD variant.

	[https://packages.debian.org/sid/netcat-openbsd](https://packages.debian.org/sid/netcat-openbsd) || [netcat-openbsd](https://www.archlinux.org/packages/?name=netcat-openbsd)

Are more complex alternative is [socat](https://www.archlinux.org/packages/?name=socat).

## Whois

See also [Wikipedia:WHOIS](https://en.wikipedia.org/wiki/WHOIS "wikipedia:WHOIS").

*   **whois** — Intelligent WHOIS client.

	[https://github.com/rfc1036/whois](https://github.com/rfc1036/whois) || [whois](https://www.archlinux.org/packages/?name=whois)

*   **jwhois** — An Internet Whois client

	[https://www.gnu.org/software/jwhois/](https://www.gnu.org/software/jwhois/) || [jwhois](https://aur.archlinux.org/packages/jwhois/)

## inetd

Arch Linux does not have [inetd](https://en.wikipedia.org/wiki/inetd "wikipedia:inetd") but you can instead use [systemd](http://0pointer.de/blog/projects/inetd.html) or [xinetd](https://en.wikipedia.org/wiki/xinetd "wikipedia:xinetd") ([xinetd](https://www.archlinux.org/packages/?name=xinetd)).

## See also

*   [List of applications/Security#Network security](/index.php/List_of_applications/Security#Network_security "List of applications/Security")