Related articles

*   [Network configuration](/index.php/Network_configuration "Network configuration")

In general, a [domain name](https://en.wikipedia.org/wiki/Domain_name "wikipedia:Domain name") represents an IP address and is associated to it in the [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") (DNS). This article explains how to configure domain name resolution and resolve domain names.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Name Service Switch](#Name_Service_Switch)
    *   [1.1 Resolve a domain name using NSS](#Resolve_a_domain_name_using_NSS)
*   [2 Glibc resolver](#Glibc_resolver)
    *   [2.1 Overwriting of /etc/resolv.conf](#Overwriting_of_/etc/resolv.conf)
    *   [2.2 Limit lookup time](#Limit_lookup_time)
    *   [2.3 Hostname lookup delayed with IPv6](#Hostname_lookup_delayed_with_IPv6)
    *   [2.4 Local domain names](#Local_domain_names)
*   [3 Lookup utilities](#Lookup_utilities)
*   [4 Resolver performance](#Resolver_performance)
*   [5 Privacy and security](#Privacy_and_security)
*   [6 Third-party DNS services](#Third-party_DNS_services)
*   [7 DNS servers](#DNS_servers)
    *   [7.1 Authoritative-only servers](#Authoritative-only_servers)
*   [8 See also](#See_also)

## Name Service Switch

The [Name Service Switch](https://en.wikipedia.org/wiki/Name_Service_Switch "wikipedia:Name Service Switch") (NSS) facility is part of the GNU C Library ([glibc](https://www.archlinux.org/packages/?name=glibc)) and backs the [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3) API, used to resolve domain names. NSS allows system databases to be provided by separate services, whose search order can be configured by the administrator in [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5). The database responsible for domain name resolution is the *hosts* database, for which glibc offers the following services:

*   *file*: reads the `/etc/hosts` file, see [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   *dns*: the [glibc resolver](#Glibc_resolver) which reads `/etc/resolv.conf`, see [resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5)

[Systemd](/index.php/Systemd "Systemd") provides three NSS services for hostname resolution:

*   [nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8) - a caching DNS stub resolver, described in [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [nss-myhostname(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-myhostname.8) - provides hostname resolution without having to edit `/etc/hosts`, described in [Network configuration#Local hostname resolution](/index.php/Network_configuration#Local_hostname_resolution "Network configuration")
*   [nss-mymachines(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-mymachines.8) - provides hostname resolution for the names of local [systemd-machined(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-machined.8) containers

### Resolve a domain name using NSS

NSS databases can be queried with [getent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getent.1). A domain name can be resolved through NSS using:

```
$ getent hosts *domain_name*

```

**Note:** While most programs resolve domain names using NSS, some may read `/etc/resolv.conf` and/or `/etc/hosts` directly. See [Network configuration#Local hostname resolution](/index.php/Network_configuration#Local_hostname_resolution "Network configuration").

## Glibc resolver

The glibc resolver reads `/etc/resolv.conf` for every resolution to determine the nameservers and options to use.

[resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5) lists nameservers together with some configuration options. Nameservers listed first are tried first, up to three nameservers may be listed. Lines starting with a number sign (`#`) are ignored.

**Note:** The glibc resolver does not cache queries. To improve query lookup time you can set up a caching resolver. See [#DNS servers](#DNS_servers) for more information.

### Overwriting of /etc/resolv.conf

[Network managers](/index.php/Network_manager "Network manager") tend to overwrite `/etc/resolv.conf`, for specifics see the corresponding section:

*   [dhcpcd#/etc/resolv.conf](/index.php/Dhcpcd#/etc/resolv.conf "Dhcpcd")
*   [netctl#resolv.conf](/index.php/Netctl#resolv.conf "Netctl")
*   [NetworkManager#/etc/resolv.conf](/index.php/NetworkManager#/etc/resolv.conf "NetworkManager")

To prevent programs from overwriting `/etc/resolv.conf` you can also write-protect it by setting the immutable [file attribute](/index.php/File_attribute "File attribute"):

```
# chattr +i /etc/resolv.conf

```

**Tip:** If you want multiple processes to write to `/etc/resolv.conf`, you can use [resolvconf](/index.php/Resolvconf "Resolvconf").

### Limit lookup time

If you are confronted with a very long hostname lookup (may it be in [pacman](/index.php/Pacman "Pacman") or while browsing), it often helps to define a small timeout after which an alternative nameserver is used. To do so, put the following in `/etc/resolv.conf`.

```
options timeout:1

```

### Hostname lookup delayed with IPv6

If you experience a 5 second delay when resolving hostnames it might be due to a DNS-server/Firewall misbehaving and only giving one reply to a parallel A and AAAA request.[[1]](https://udrepper.livejournal.com/20948.html) You can fix that by setting the following option in `/etc/resolv.conf`:

```
options single-request

```

### Local domain names

If you want to be able to use the hostname of local machine names without the fully qualified domain names, then add a line to `/etc/resolv.conf` with the local domain such as:

```
domain example.com

```

That way you can refer to local hosts such as `mainmachine1.example.com` as simply `mainmachine1` when using the *ssh* command, but the *drill* command still requires the fully qualified domain names in order to perform lookups.

## Lookup utilities

To query specific DNS servers and DNS/[DNSSEC](/index.php/DNSSEC "DNSSEC") records you can use dedicated DNS lookup utilities. These tools implement DNS themselves and do not use [NSS](#Name_Service_Switch).

*   [ldns](https://www.archlinux.org/packages/?name=ldns) provides [drill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/drill.1), which is a tool designed to retrieve information out of the DNS.

For example, to query a specific nameserver with *drill* for the TXT records of a domain:

```
$ drill @*nameserver* TXT *domain*

```

If you do not specify a DNS server *drill* uses the nameservers defined in `/etc/resolv.conf`.

*   [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) provides [dig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dig.1), [host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/host.1), [nslookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nslookup.1) and a bunch of `dnssec-` tools.

**Tip:** Some DNS servers ship with their own DNS lookup utilities. E.g. [knot](https://www.archlinux.org/packages/?name=knot) has [khost(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/khost.1) and [kdig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kdig.1), [Unbound](/index.php/Unbound "Unbound")—[unbound-host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unbound-host.1).

## Resolver performance

The Glibc resolver does not cache queries. If you want local caching use [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") or set up a local caching [DNS server](#DNS_servers) and use `127.0.0.1` as your name server.

**Tip:**

*   The *drill* or *dig* [lookup utilities](#Lookup_utilities) report the query time.
*   A router usually sets its own caching resolver as the network's DNS server thus providing DNS cache for the whole network.
*   If it takes too long to switch to the next DNS server you can try [decreasing the timeout](#Limit_lookup_time).

## Privacy and security

The DNS protocol is unencrypted and does not account for confidentiality, integrity or authentication, so if you use an untrusted network or a malicious ISP, your DNS queries can be eavesdropped and the responses [manipulated](https://en.wikipedia.org/wiki/Man-in-the-middle_attack "wikipedia:Man-in-the-middle attack"). Furthermore, DNS servers can conduct [DNS hijacking](https://en.wikipedia.org/wiki/DNS_hijacking "wikipedia:DNS hijacking").

You need to trust your DNS server to treat your queries confidentially. DNS servers are provided by ISPs and [third-parties](#Third-party_DNS_services). Alternatively you can run your own [recursive name server](#DNS_servers), which however takes more effort. If you use a [DHCP](/index.php/DHCP "DHCP") client in untrusted networks, be sure to set static name servers to avoid using and being subject to arbitrary DNS servers. To secure your communication with a remote DNS server you can use an encrypted protocol, like [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS"), [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") or [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt"), provided that both the upstream server and your [resolver](#DNS_servers) support the protocol. To verify that responses are actually from [authoritative name servers](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server"), you can validate [DNSSEC](/index.php/DNSSEC "DNSSEC"), provided that both the upstream server(s) and your [resolver](#DNS_servers) support it.

Be aware that client software, such as major web browsers, may also (start to) implement some of the protocols. While the encryption of queries may often be seen as a bonus, it also means the software sidetracks queries around the system resolver configuration.[[2]](https://hacks.mozilla.org/2018/05/a-cartoon-intro-to-dns-over-https/#trr-and-doh)

## Third-party DNS services

**Note:** Before using a third-party DNS service, check its privacy policy for information on how user data is handled. User data has value and can be sold to other parties.

There are various [third-party DNS services](https://en.wikipedia.org/wiki/Public_recursive_name_server#List_of_public_DNS_service_operators "wikipedia:Public recursive name server") available, some of which also have dedicated software:

*   **dingo** — A DNS client for Google DNS over HTTPS

	[https://github.com/pforemski/dingo](https://github.com/pforemski/dingo) || [dingo](https://www.archlinux.org/packages/?name=dingo)

*   **opennic-up** — Automates the renewal of the DNS servers with the most responsive OpenNIC servers

	[https://github.com/kewlfft/opennic-up](https://github.com/kewlfft/opennic-up) || [opennic-up](https://aur.archlinux.org/packages/opennic-up/)

## DNS servers

[DNS](/index.php/DNS "DNS") servers can be [authoritative](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server") and [recursive](https://en.wikipedia.org/wiki/Name_server#Recursive_query "wikipedia:Name server"). If they are neither, they are called **stub resolvers** and simply forward all queries to another recursive name server. Stub resolvers are typically used to introduce DNS caching on the local host or network. Note that the same can also be achieved with a fully-fledged name server. This section compares the available DNS servers, for a more detailed comparison, refer to [Wikipedia:Comparison of DNS server software](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software "wikipedia:Comparison of DNS server software").

| Name | Package | [Authoritative](https://en.wikipedia.org/wiki/Authoritative_name_server "wikipedia:Authoritative name server") | [Recursive](https://en.wikipedia.org/wiki/Name_server#Recursive_query "wikipedia:Name server") | [Cache](https://en.wikipedia.org/wiki/Name_server#Caching_name_server "wikipedia:Name server") | [resolvconf](/index.php/Resolvconf "Resolvconf") | [Validates](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions#The_lookup_procedure "wikipedia:Domain Name System Security Extensions")
[DNSSEC](/index.php/DNSSEC "DNSSEC") | [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt") | [DNS
over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS") | [DNS
over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") |
| [dnscrypt-proxy](/index.php/Dnscrypt-proxy "Dnscrypt-proxy") | [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) | No | No | Yes | No | No | Resolver | No | Resolver |
| [Rescached](/index.php/Rescached "Rescached") | [rescached-git](https://aur.archlinux.org/packages/rescached-git/) | No | No | Yes | [Yes](https://github.com/shuLhan/rescached-go#integration-with-openresolv) | No | No | No | Limited |
| [Stubby](/index.php/Stubby "Stubby") | [stubby](https://www.archlinux.org/packages/?name=stubby) | No | No | No | No | Yes | No | Resolver | No |
| [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") | [systemd](https://www.archlinux.org/packages/?name=systemd) | No | No | Yes | [Yes](/index.php/Systemd-resolvconf "Systemd-resolvconf") | Yes | No | Insecure resolver | [No](https://github.com/systemd/systemd/issues/8639) |
| [dnsmasq](/index.php/Dnsmasq "Dnsmasq") | [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) | Partial | No | Yes | [Yes](/index.php/Openresolv#Subscribers "Openresolv") | Yes | No | [No](http://lists.thekelleys.org.uk/pipermail/dnsmasq-discuss/2018q2/012131.html) | No |
| [BIND](/index.php/BIND "BIND") | [bind](https://www.archlinux.org/packages/?name=bind) | Yes | Yes | Yes | [Yes](/index.php/Openresolv#Subscribers "Openresolv") | Yes | No | [No](https://kb.isc.org/docs/aa-01386) | No |
| [Knot Resolver](/index.php/Knot_Resolver "Knot Resolver") | [knot-resolver](https://aur.archlinux.org/packages/knot-resolver/) | Yes | Yes | Yes | No | Yes | No | Yes | [No](https://gitlab.labs.nic.cz/knot/knot-resolver/issues/243) |
| [MaraDNS](https://en.wikipedia.org/wiki/MaraDNS "wikipedia:MaraDNS") | [maradns](https://aur.archlinux.org/packages/maradns/) | Yes | Yes | Yes | No | No | No | No | No |
| [pdnsd](/index.php/Pdnsd "Pdnsd") | [pdnsd](https://www.archlinux.org/packages/?name=pdnsd) | Yes | Yes | Permanent | [Yes](/index.php/Openresolv#Subscribers "Openresolv") | No | No | No | No |
| [PowerDNS Recursor](https://www.powerdns.com/recursor.html) | [powerdns-recursor](https://www.archlinux.org/packages/?name=powerdns-recursor) | Yes | Yes | Yes | [No](https://roy.marples.name/projects/openresolv/config#pdns_recursor) | Yes | No | No | No |
| [Unbound](/index.php/Unbound "Unbound") | [unbound](https://www.archlinux.org/packages/?name=unbound) | Yes | Yes | Yes | [Yes](/index.php/Openresolv#Subscribers "Openresolv") | Yes | Server | Yes | [No](https://nlnetlabs.nl/bugs-script/show_bug.cgi?id=1200) |

1.  Only forwards using DNS over HTTPS when Rescached itself is queried using DNS over HTTPS.[[3]](https://github.com/shuLhan/rescached-go#integration-with-dns-over-https)
2.  From [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5): *Note as the resolver is not capable of authenticating the server, it is vulnerable for "man-in-the-middle" attacks.*[[4]](https://github.com/systemd/systemd/issues/9397) Also, the only supported mode is "opportunistic", which *makes DNS-over-TLS vulnerable to "downgrade" attacks*.[[5]](https://github.com/systemd/systemd/issues/10755)
3.  From [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software#cite_note-masqauth-25 "wikipedia:Comparison of DNS server software"): dnsmasq has limited authoritative support, intended for internal network use rather than public Internet use.

### Authoritative-only servers

| Name | Package | [DNSSEC](/index.php/DNSSEC "DNSSEC") | Geographic
balancing |
| [gdnsd](https://gdnsd.org/) | [gdnsd](https://www.archlinux.org/packages/?name=gdnsd) | No | Yes |
| [Knot DNS](https://www.knot-dns.cz/) | [knot](https://www.archlinux.org/packages/?name=knot) | Yes | [Yes](https://www.knot-dns.cz/docs/2.7/singlehtml/#geoip-geography-based-responses) |
| [NSD](/index.php/NSD "NSD") | [nsd](https://www.archlinux.org/packages/?name=nsd) | No | No |
| [PowerDNS](https://www.powerdns.com/auth.html) | [powerdns](https://www.archlinux.org/packages/?name=powerdns) | Yes | Yes |

## See also

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)
*   [RFC:7706](https://tools.ietf.org/html/rfc7706 "rfc:7706") - Decreasing Access Time to Root Servers by Running One on Loopback