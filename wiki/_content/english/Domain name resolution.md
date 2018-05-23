Related articles

*   [Improving performance#Network](/index.php/Improving_performance#Network "Improving performance")
*   [Alternative DNS services](/index.php/Alternative_DNS_services "Alternative DNS services")

This article explains how to configure [domain name](https://en.wikipedia.org/wiki/Domain_name "wikipedia:Domain name") resolution and resolve domain names.

## Contents

*   [1 Name Service Switch](#Name_Service_Switch)
*   [2 Glibc resolver](#Glibc_resolver)
    *   [2.1 Limit lookup time](#Limit_lookup_time)
    *   [2.2 Hostname lookup delayed with IPv6](#Hostname_lookup_delayed_with_IPv6)
    *   [2.3 Local domain names](#Local_domain_names)
*   [3 Systemd-resolved](#Systemd-resolved)
*   [4 DNS in Linux](#DNS_in_Linux)
*   [5 Lookup utilities](#Lookup_utilities)
*   [6 Preserve DNS settings](#Preserve_DNS_settings)
    *   [6.1 Prevent NetworkManager modifications](#Prevent_NetworkManager_modifications)
    *   [6.2 Openresolv](#Openresolv)
    *   [6.3 Modify the dhcpcd config](#Modify_the_dhcpcd_config)
    *   [6.4 Write-protect resolv.conf](#Write-protect_resolv.conf)
*   [7 See also](#See_also)

## Name Service Switch

The [Name Service Switch](https://en.wikipedia.org/wiki/Name_Service_Switch "wikipedia:Name Service Switch") (NSS) facility is part of the GNU C Library ([glibc](https://www.archlinux.org/packages/?name=glibc)) and backs the [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3) API, used to resolve domain names. NSS allows system databases to be provided by separate services, whose search order can be configured by the administrator in [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5). The database responsible for domain name resolution is the `hosts` database, for which glibc offers the following services:

	`file`

	`/etc/hosts`, see [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)

	`dns`

	The [#Glibc resolver](#Glibc_resolver).

[#Systemd-resolved](#Systemd-resolved) provides the `resolve` NSS service.

## Glibc resolver

Nameservers and settings of the glibc resolver are configured in [resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5) (`/etc/resolv.conf`).

Nameservers listed first are tried first, lines can be commented out with a number sign. You may include a maximum of three nameservers.

Changes made to resolv.conf take effect immediately.

**Tip:** If you require more flexibility, e.g. more than three nameservers, you can use a local DNS resolver like [dnsmasq](/index.php/Dnsmasq "Dnsmasq") or [unbound](/index.php/Unbound "Unbound"). In this case the nameserver IP address will likely be `127.0.0.1`.

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

*systemd-resolved* has four different modes for handling *resolv.conf* (described in [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#%2FETC%2FRESOLV.CONF)). We will focus here on the two most relevant modes.

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

## DNS in Linux

ISPs usually provide working [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") servers. A router may also add an extra DNS server in case it has its own cache server. Switching between DNS servers is transparent for Windows users, because if a DNS server is slow or does not work it will immediately switch to a better one. However, Linux usually takes longer to timeout, which could be the reason why you are getting a delay.

## Lookup utilities

Use *drill* (provided by package [ldns](https://www.archlinux.org/packages/?name=ldns)) before any changes, repeat after making the adjustments and compare the query time(s). The following command uses the nameservers set in `/etc/resolv.conf`:

```
$ drill www.archlinux.org

```

You can also specify a specific nameserver's ip address, bypassing the settings in your `/etc/resolv.conf`:

```
$ drill @*ip.of.name.server* www.archlinux.org

```

For example to test Google's name servers:

```
$ drill @8.8.8.8 www.archlinux.org

```

To test a local name server (such as [unbound](/index.php/Unbound "Unbound")) do:

```
$ drill @127.0.0.1 www.archlinux.org

```

## Preserve DNS settings

[dhcpcd](/index.php/Dhcpcd "Dhcpcd"), [netctl](/index.php/Netctl "Netctl"), [NetworkManager](/index.php/NetworkManager "NetworkManager"), and various other processes can overwrite `/etc/resolv.conf`. This is usually desirable behavior, but sometimes DNS settings need to be set manually (e.g. when using a static IP address). There are several ways to accomplish this.

*   If you are using *dhcpcd*, see [#Modify the dhcpcd config](#Modify_the_dhcpcd_config) below.
*   If you are using [netctl](/index.php/Netctl "Netctl") and static IP address assignment, do not use the `DNS*` options in your profile, otherwise *resolvconf* is called and `/etc/resolv.conf` overwritten.

### Prevent NetworkManager modifications

To stop *NetworkManager* from modifying `/etc/resolv.conf`, edit `/etc/NetworkManager/NetworkManager.conf` and add the following in the `[main]` section:

```
dns=none

```

`/etc/resolv.conf` might be a broken symlink that you will need to remove after doing that. Then, just create a new `/etc/resolv.conf` file.

*NetworkManager* also offers hooks via so called dispatcher scripts that can be used to alter the `/etc/resolv.conf` after network changes. See [NetworkManager#Network services with NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") and [NetworkManager(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.8) for more information.

### Openresolv

[openresolv](https://www.archlinux.org/packages/?name=openresolv) provides a utility *resolvconf*, which is a framework for managing multiple DNS configurations. See [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) and [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) for more information.

The configuration is done in `/etc/resolvconf.conf` and running `resolvconf -u` will generate `/etc/resolv.conf`.

Note that *NetworkManager* can be configured to use *openresolv*, see [NetworkManager#Configure NetworkManager resolv.conf management mode to use resolvconf](/index.php/NetworkManager#Configure_NetworkManager_resolv.conf_management_mode_to_use_resolvconf "NetworkManager").

### Modify the dhcpcd config

*dhcpcd'*s configuration file may be edited to prevent the *dhcpcd* daemon from overwriting `/etc/resolv.conf`. To do this, add the following to the last section of `/etc/dhcpcd.conf`:

```
nohook resolv.conf

```

Alternatively, you can create a file called `/etc/resolv.conf.head` containing your DNS servers. *dhcpcd* will prepend this file to the beginning of `/etc/resolv.conf`.

Or you can configure dhcpcd to use the same DNS servers every time. To do this, add the following line at the end of your `/etc/dhcpcd.conf`, where `*dns-server-ip-addressses*` is a space separated list of DNS IP addresses.

```
static domain_name_servers=*dns-server-ip-addresses*

```

For example, to set it to Google's DNS servers:

```
static domain_name_servers=8.8.8.8 8.8.4.4

```

### Write-protect resolv.conf

Another way to protect your `/etc/resolv.conf` from being modified by anything is setting the immutable (write-protection) attribute:

```
# chattr +i /etc/resolv.conf

```

## See also

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)