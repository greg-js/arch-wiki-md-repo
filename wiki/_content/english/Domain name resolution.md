Related articles

*   [Alternative DNS services](/index.php/Alternative_DNS_services "Alternative DNS services")
*   [Network configuration](/index.php/Network_configuration "Network configuration")

In general, a [domain name](https://en.wikipedia.org/wiki/Domain_name "wikipedia:Domain name") represents an IP address and is associated to it in the [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") (DNS). This article explains how to configure domain name resolution and resolve domain names.

## Contents

*   [1 Name Service Switch](#Name_Service_Switch)
    *   [1.1 Check if you can resolve domain names](#Check_if_you_can_resolve_domain_names)
*   [2 Glibc resolver](#Glibc_resolver)
    *   [2.1 Overwriting of resolv.conf](#Overwriting_of_resolv.conf)
    *   [2.2 Limit lookup time](#Limit_lookup_time)
    *   [2.3 Hostname lookup delayed with IPv6](#Hostname_lookup_delayed_with_IPv6)
    *   [2.4 Local domain names](#Local_domain_names)
*   [3 Systemd-resolved](#Systemd-resolved)
*   [4 Performance](#Performance)
*   [5 Privacy](#Privacy)
*   [6 Lookup utilities](#Lookup_utilities)
*   [7 See also](#See_also)

## Name Service Switch

	*"NSS" redirects here. For Mozilla cryptographic libraries, see [Network Security Services](/index.php/Network_Security_Services "Network Security Services").*

The [Name Service Switch](https://en.wikipedia.org/wiki/Name_Service_Switch "wikipedia:Name Service Switch") (NSS) facility is part of the GNU C Library ([glibc](https://www.archlinux.org/packages/?name=glibc)) and backs the [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3) API, used to resolve domain names. NSS allows system databases to be provided by separate services, whose search order can be configured by the administrator in [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5). The database responsible for domain name resolution is the `hosts` database, for which glibc offers the following services:

*   `file`: reads the `/etc/hosts` file, see [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   `dns`: the [glibc resolver](#Glibc_resolver) which reads `/etc/resolv.conf`, see [resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5)

[Systemd](/index.php/Systemd "Systemd") provides three NSS services for hostname resolution:

*   [nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8) - a caching DNS stub resolver, described in [#Systemd-resolved](#Systemd-resolved)
*   [nss-myhostname(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-myhostname.8) - provides hostname resolution without having to edit `/etc/hosts`, described in [Network configuration#Local hostname resolution](/index.php/Network_configuration#Local_hostname_resolution "Network configuration")
*   [nss-mymachines(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-mymachines.8) - provides hostname resolution for the names of local [systemd-machined(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-machined.8) containers

### Check if you can resolve domain names

NSS databases can be queried with [getent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getent.1). You can resolve a domain name through NSS using:

```
$ getent hosts *domain_name*

```

**Note:** While most programs resolve domain names using NSS, some may read `resolv.conf` and/or `/etc/hosts` directly. See [Network configuration#Local hostname resolution](/index.php/Network_configuration#Local_hostname_resolution "Network configuration").

## Glibc resolver

The glibc resolver reads `/etc/resolv.conf` for every resolution to determine the nameservers and options to use.

[resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5) lists nameservers together with some configuration options. Nameservers listed first are tried first, up to three nameservers may be listed. Lines starting with a number sign are ignored.

**Note:** The glibc resolver does not cache queries. See [#Performance](#Performance) for more information.

### Overwriting of resolv.conf

[Network managers](/index.php/Network_manager "Network manager") tend to overwrite `resolv.conf`, for specifics see the corresponding section:

*   [dhcpcd#resolv.conf](/index.php/Dhcpcd#resolv.conf "Dhcpcd")
*   [netctl#resolv.conf](/index.php/Netctl#resolv.conf "Netctl")
*   [NetworkManager#resolv.conf](/index.php/NetworkManager#resolv.conf "NetworkManager")

To prevent programs from overwriting `resolv.conf` you can also write-protect it by setting the immutable [file attribute](/index.php/File_attribute "File attribute").

**Tip:** If you want multiple processes to write to `resolv.conf`, you can use [openresolv](/index.php/Openresolv "Openresolv").

### Limit lookup time

If you are confronted with a very long hostname lookup (may it be in [pacman](/index.php/Pacman "Pacman") or while browsing), it often helps to define a small timeout after which an alternative nameserver is used. To do so, put the following in `/etc/resolv.conf`.

```
options timeout:1

```

### Hostname lookup delayed with IPv6

If you experience a 5 second delay when resolving hostnames it might be due to a DNS-server/Firewall misbehaving and only giving one reply to a parallel A and AAAA request ([source](http://udrepper.livejournal.com/20948.html)). You can fix that by setting the following option in `/etc/resolv.conf`:

```
options single-request

```

### Local domain names

If you want to be able to use the hostname of local machine names without the fully qualified domain names, then add a line to `resolv.conf` with the local domain such as:

```
domain example.com

```

That way you can refer to local hosts such as `mainmachine1.example.com` as simply `mainmachine1` when using the *ssh* command, but the *drill* command still requires the fully qualified domain names in order to perform lookups.

## Systemd-resolved

[systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) is a [systemd](/index.php/Systemd "Systemd") service that provides network name resolution to local applications via a [D-Bus](/index.php/D-Bus "D-Bus") interface, the `resolve` NSS service ([nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8)), and a local DNS stub listener on `127.0.0.53`.

*systemd-resolved* has four different modes for handling the [glibc resolver](#Glibc_resolver)'s *resolv.conf* (described in [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#.2FETC.2FRESOLV.CONF)). We will focus here on the two most relevant modes.

1.  The mode in which *systemd-resolved* is a client of the `/etc/resolv.conf`. This mode preserves `/etc/resolv.conf` and is **compatible** with the procedures described in this page.
2.  The *systemd-resolved'*s **recommended** mode of operation: the DNS stub file as indicated below contains both the local stub `127.0.0.53` as the only DNS servers and a list of search domains.

 `/run/systemd/resolve/stub-resolv.conf` 
```
nameserver 127.0.0.53
search lan

```

The service users are advised to redirect the `/etc/resolv.conf` file to the local stub DNS resolver file `/run/systemd/resolve/stub-resolv.conf` managed by *systemd-resolved*. This propagates the systemd managed configuration to all the clients. This can be done by deleting or renaming the existing `/etc/resolv.conf` and replacing it by a symbolic link to the systemd stub:

```
# ln -s /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf

```

In this mode, the DNS servers are provided in the [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5) file:

 `/etc/systemd/resolved.conf` 
```
[Resolve]
**DNS=91.239.100.100 89.233.43.71**
...
```

In order to check the DNS actually used by *systemd-resolved*, the command to use is:

```
$ systemd-resolve --status

```

**Tip:**

*   To understand the context around the DNS choices and switches, one can turn on detailed debug information for *systemd-resolved* as described in [Systemd#Diagnosing a service](/index.php/Systemd#Diagnosing_a_service "Systemd").
*   The mode of operation of *systemd-resolved* is detected automatically, depending on whether `/etc/resolv.conf` is a symlink to the local stub DNS resolver file or contains server names.

## Performance

The [#Glibc resolver](#Glibc_resolver) does not cache queries. If you want local caching use [#Systemd-resolved](#Systemd-resolved) or set up a local caching [DNS server](/index.php/DNS_server "DNS server") and use `127.0.0.1`.

**Tip:** The *drill* or *dig* [#Lookup utilities](#Lookup_utilities) report the query time.

Internet service providers usually provide working DNS servers. A router may also add an extra DNS server in case it has its own cache server. Switching between DNS servers is transparent for Windows users, because if a DNS server is slow or does not work it will immediately switch to a better one. However, Linux usually takes longer to timeout, which could cause delays.

## Privacy

Most DNS servers keep a log of IP addresses and sites visited on a more or less temporary basis. The data collected can be used to perform various statistical studies. Personally-identifying information have value and can also be rented or sold to third parties. [Alternative DNS services](/index.php/Alternative_DNS_services "Alternative DNS services") provides a list of popular services, check their privacy policy for information about how user data is handled.

## Lookup utilities

To query specific DNS servers and DNS/[DNSSEC](/index.php/DNSSEC "DNSSEC") records you can use dedicated DNS lookup utilities. These tools implement DNS themselves and do not use [NSS](#Name_Service_Switch).

*   [ldns](https://www.archlinux.org/packages/?name=ldns) provides [drill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/drill.1), which is a tool designed to retrieve information out of the DNS.

For example, to query a specific nameserver with *drill* for the TXT records of a domain:

```
$ drill @*nameserver* TXT *domain*

```

If you do not specify a DNS server *drill* uses the nameservers defined in `/etc/resolv.conf`.

*   [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) provides [dig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dig.1), [host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/host.1), [nslookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nslookup.1) and a bunch of `dnssec-` tools.

## See also

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)