# resolv.conf

The configuration file for DNS resolvers is `/etc/resolv.conf`. From its [man page](http://www.kernel.org/doc/man-pages/online/pages/man5/resolv.conf.5.html):

	_"The resolver is a set of routines in the C library that provide access to the Internet Domain Name System (DNS). The resolver configuration file contains information that is read by the resolver routines the first time they are invoked by a process. The file is designed to be human readable and contains a list of keywords with values that provide various types of resolver information._

	_If this file does not exist, only the name server on the local machine will be queried; the domain name is determined from the hostname and the domain search path is constructed from the domain name."_

## Contents

*   [1 DNS in Linux](#DNS_in_Linux)
*   [2 Alternative DNS servers](#Alternative_DNS_servers)
    *   [2.1 OpenNIC](#OpenNIC)
    *   [2.2 OpenDNS](#OpenDNS)
    *   [2.3 Google](#Google)
    *   [2.4 Comodo](#Comodo)
    *   [2.5 Yandex](#Yandex)
    *   [2.6 UncensoredDNS](#UncensoredDNS)
*   [3 Preserve DNS settings](#Preserve_DNS_settings)
    *   [3.1 With NetworkManager](#With_NetworkManager)
    *   [3.2 Using openresolv](#Using_openresolv)
    *   [3.3 Modify the dhcpcd config](#Modify_the_dhcpcd_config)
    *   [3.4 Write-protect /etc/resolv.conf](#Write-protect_.2Fetc.2Fresolv.conf)
    *   [3.5 Use timeout option to reduce hostname lookup time](#Use_timeout_option_to_reduce_hostname_lookup_time)

## DNS in Linux

Your ISP (usually) provides working [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") servers, and a router may also add an extra DNS server in case you have your own cache server. Switching between DNS servers does not represent a problem for Windows users, because if a DNS server is slow or does not work it will immediately switch to a better one. However, Linux usually takes longer to timeout, which could be the reason why you are getting a delay.

Use _drill_ (provided by package [ldns](https://www.archlinux.org/packages/?name=ldns)) before any changes, repeat after making the adjustments in the section below and compare the query time(s):

```
$ drill www5.yahoo.com

```

You can also specify a nameserver:

```
$ drill @ip.of.name.server www5.yahoo.com

```

## Alternative DNS servers

To use alternative DNS servers, edit `/etc/resolv.conf` and add them to the top of the file so they are used first, optionally removing or commenting out already listed servers.

**Note:**

*   Currently, you may include a maximum of three `nameserver` lines. In order to overcome this limitation, you can use a locally caching nameserver like [dnsmasq](/index.php/Dnsmasq "Dnsmasq").
*   Changes made to `/etc/resolv.conf` take effect immediately.

### OpenNIC

[OpenNIC](http://www.opennicproject.org/) provides free uncensored nameservers with additional features.

**Tip:** OpenNIC offers many [different nameservers](http://wiki.opennicproject.org/Tier2) located in multiple countries. Pick some of the [nearest nameservers](http://www.opennicproject.org/nearest-servers/) for optimal performance.

```
# OpenNIC IPv4 nameservers (US)
nameserver 107.170.95.180
nameserver 75.127.14.107

```

### OpenDNS

[OpenDNS](https://opendns.com) provides free alternative nameservers:

```
# OpenDNS IPv4 nameservers
nameserver 208.67.222.222
nameserver 208.67.220.220

```

```
# OpenDNS IPv6 nameservers
nameserver 2620:0:ccc::2
nameserver 2620:0:ccd::2

```

### Google

[Google's nameservers](https://developers.google.com/speed/public-dns/) can be used as an alternative:

```
# Google IPv4 nameservers
nameserver 8.8.8.8
nameserver 8.8.4.4

```

```
# Google IPv6 nameservers
nameserver 2001:4860:4860::8888
nameserver 2001:4860:4860::8844

```

### Comodo

[Comodo](http://securedns.dnsbycomodo.com/) provides another IPv4 set, with optional (non-free) web-filtering. Implied in this feature is that the service hijacks the queries.

```
# Comodo nameservers 
nameserver 8.26.56.26 
nameserver 8.20.247.20

```

### Yandex

[Yandex.DNS](https://dns.yandex.ru/advanced/) have three options:

```
# Basic Yandex.DNS - Quick and reliable DNS
nameserver 77.88.8.8              # Preferred IPv4 DNS
nameserver 77.88.8.1              # Alternate IPv4 DNS

nameserver 2a02:6b8::feed:0ff     # Preferred IPv6 DNS
nameserver 2a02:6b8:0:1::feed:0ff # Alternate IPv6 DNS

```

```
# Safe Yandex.DNS - Protection from virus and fraudulent content
nameserver 77.88.8.88             # Preferred IPv4 DNS
nameserver 77.88.8.2              # Alternate IPv4 DNS

nameserver 2a02:6b8::feed:bad     # Preferred IPv6 DNS
nameserver 2a02:6b8:0:1::feed:bad # Alternate IPv6 DNS

```

```
# Family Yandex.DNS - Without adult content
nameserver 77.88.8.7              # Preferred IPv4 DNS
nameserver 77.88.8.3              # Alternate IPv4 DNS

nameserver 2a02:6b8::feed:a11     # Preferred IPv6 DNS
nameserver 2a02:6b8:0:1::feed:a11 # Alternate IPv6 DNS

```

Yandex.DNS' speed is the same in all three modes. In "Basic" mode, there is no traffic filtering. In "Safe" mode, protection from infected and fraudulent sites is provided. "Family" mode enables protection from dangerous sites and blocks sites with adult content.

### UncensoredDNS

[UncensoredDNS](http://censurfridns.dk) is a free uncensored DNS resolver who also answers queries on port 5353 if you are behind a firewall blocking outgoing port 53.

```
# censurfridns.dk IPv4 nameservers
nameserver 91.239.100.100    ## anycast.censurfridns.dk
nameserver 89.233.43.71      ## ns1.censurfridns.dk

```

```
# censurfridns.dk IPv6 nameservers
nameserver 2001:67c:28a4::             ## anycast.censurfridns.dk
nameserver 2002:d596:2a92:1:71:53::    ## ns1.censurfridns.dk

```

## Preserve DNS settings

[dhcpcd](/index.php/Dhcpcd "Dhcpcd"), [netctl](/index.php/Netctl "Netctl"), [NetworkManager](/index.php/NetworkManager "NetworkManager"), and various other processes can overwrite `/etc/resolv.conf`. This is usually desirable behavior, but sometimes DNS settings need to be set manually (e.g. when using a static IP address). There are several ways to accomplish this.

*   If you are using _dhcpcd_, see [#Modify the dhcpcd config](#Modify_the_dhcpcd_config) below.
*   If you are using [netctl](/index.php/Netctl "Netctl") and static IP address assignment, do not use the `DNS*` options in your profile, otherwise _resolvconf_ is called and `/etc/resolv.conf` overwritten.

### With NetworkManager

To stop NetworkManager from modifying `/etc/resolv.conf`, edit `/etc/NetworkManager/NetworkManager.conf` and add the following in the `[main]` section:

```
dns=none

```

`/etc/resolv.conf` might be a broken symlink that you will need to remove after doing that. Then, just create a new `/etc/resolv.conf` file.

### Using openresolv

[openresolv](https://www.archlinux.org/packages/?name=openresolv) provides a utility _resolvconf_, which is a framework for managing multiple DNS configurations. See `man 8 resolvconf` and `man 5 resolvconf.conf` for more information.

The configuration is done in `/etc/resolvconf.conf` and running `resolvconf -u` will generate `/etc/resolv.conf`.

### Modify the dhcpcd config

_dhcpcd'_s configuration file may be edited to prevent the _dhcpcd_ daemon from overwriting `/etc/resolv.conf`. To do this, add the following to the last section of `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

Alternatively, you can create a file called `/etc/resolv.conf.head` containing your DNS servers. _dhcpcd_ will prepend this file to the beginning of `/etc/resolv.conf`.

Or you can configure dhcpcd to use the same DNS servers every time. To do this, add the following line at the end of your `/etc/dhcpcd.conf`:

```
static domain_name_servers=8.8.4.4 8.8.8.8

```

### Write-protect /etc/resolv.conf

Another way to protect your `/etc/resolv.conf` from being modified by anything is setting the immutable (write-protection) attribute:

```
# chattr +i /etc/resolv.conf

```

### Use timeout option to reduce hostname lookup time

If you are confronted with a very long hostname lookup (may it be in [pacman](/index.php/Pacman "Pacman") or while browsing), it often helps to define a small timeout after which an alternative nameserver is used. To do so, put the following in `/etc/resolv.conf`.

```
options timeout:1

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Resolv.conf&oldid=406220](https://wiki.archlinux.org/index.php?title=Resolv.conf&oldid=406220)"