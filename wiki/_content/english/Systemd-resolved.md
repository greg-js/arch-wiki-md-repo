Related articles

*   [systemd](/index.php/Systemd "Systemd")
*   [resolv.conf](/index.php/Resolv.conf "Resolv.conf")
*   [Avahi](/index.php/Avahi "Avahi")
*   [Stubby](/index.php/Stubby "Stubby")
*   [openresolv](/index.php/Openresolv "Openresolv")

[systemd-resolved](https://www.freedesktop.org/wiki/Software/systemd/resolved/) is a [systemd](/index.php/Systemd "Systemd") service that provides network name resolution to local applications via a [D-Bus](/index.php/D-Bus "D-Bus") interface, the `resolve` [NSS](/index.php/NSS "NSS") service ([nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8)), and a local DNS stub listener on `127.0.0.53`. See [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) for the usage.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 DNS](#DNS)
        *   [2.1.1 Setting DNS servers](#Setting_DNS_servers)
            *   [2.1.1.1 Automatically](#Automatically)
            *   [2.1.1.2 Manually](#Manually)
            *   [2.1.1.3 Fallback](#Fallback)
        *   [2.1.2 DNSSEC](#DNSSEC)
        *   [2.1.3 DNS over TLS](#DNS_over_TLS)
    *   [2.2 mDNS](#mDNS)
    *   [2.3 LLMNR](#LLMNR)
*   [3 Lookup](#Lookup)

## Installation

*systemd-resolved* is a part of the [systemd](https://www.archlinux.org/packages/?name=systemd) package that is [installed](/index.php/Installed "Installed") by default.

## Configuration

*systemd-resolved* provides resolver services for [Domain Name System (DNS)](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") (including [DNSSEC](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions") and [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS")), [Multicast DNS (mDNS)](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS") and [Link-Local Multicast Name Resolution (LLMNR)](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution "wikipedia:Link-Local Multicast Name Resolution").

The resolver can be configured by editing `/etc/systemd/resolved.conf` and/or drop-in *.conf* files in `/etc/systemd/resolved.conf.d/`. See [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

To use *systemd-resolved* [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `systemd-resolved.service`.

**Tip:** To understand the context around the choices and switches, one can turn on detailed debug information for *systemd-resolved* as described in [systemd#Diagnosing a service](/index.php/Systemd#Diagnosing_a_service "Systemd").

### DNS

*systemd-resolved* has four different modes for handling the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") (described in [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#.2FETC.2FRESOLV.CONF)). We will focus here on the two most relevant modes.

1.  The *systemd-resolved'*s **recommended** mode of operation: the DNS stub file `/run/systemd/resolve/stub-resolv.conf` contains both the local stub `127.0.0.53` as the only DNS servers and a list of search domains.
2.  The mode in which *systemd-resolved* is a client of the `/etc/resolv.conf`. This mode preserves `/etc/resolv.conf` and is **compatible** with the procedures described in this page.

The service users are advised to redirect the `/etc/resolv.conf` file to the local stub DNS resolver file `/run/systemd/resolve/stub-resolv.conf` managed by *systemd-resolved*. This propagates the systemd managed configuration to all the clients. This can be done by replacing `/etc/resolv.conf` with a symbolic link to the systemd stub:

```
# ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf

```

**Tip:** The mode of operation of *systemd-resolved* is detected automatically, depending on whether `/etc/resolv.conf` is a symlink to the local stub DNS resolver file or contains server names.

#### Setting DNS servers

In order to check the DNS actually used by *systemd-resolved*, the command to use is:

```
$ resolvectl status

```

##### Automatically

*systemd-resolved* can get name servers and search domains in two ways:

1.  If the used [network manager](/index.php/Network_manager "Network manager") supports *systemd-resolved*; currently those are [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager "NetworkManager").
2.  If the used [DHCP](/index.php/DHCP "DHCP") and [VPN](/index.php/VPN "VPN") clients support using *resolvconf* to set name servers and search domains. See [openresolv#Users](/index.php/Openresolv#Users "Openresolv") for a list of software that use *resolvconf*.

For the first case no configuration is required since *systemd-resolved* will be detected by folowing the `/etc/resolv.conf` symlink.

For the second case you need to [install](/index.php/Install "Install") [systemd-resolvconf](https://www.archlinux.org/packages/?name=systemd-resolvconf), it will provide the `/usr/bin/resolvconf` symlink.

**Note:**

*   *systemd-resolved'*s *resolvconf* interface is limited and may not work with all software that use it. See [resolvectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvectl.1) for more information.
*   The *resolvconf* interface in systemd 290 does not set nameservers. See [FS#59459](https://bugs.archlinux.org/task/59459) and [systemd issue 9423](https://github.com/systemd/systemd/issues/9423).

##### Manually

In local DNS stub mode, alternative DNS servers are provided in the [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5) file:

 `/etc/systemd/resolved.conf.d/dns_servers.conf` 
```
[Resolve]
DNS=91.239.100.100 89.233.43.71
```

**Note:** [Network managers](/index.php/Network_manager "Network manager") have their own DNS settings that override *systemd-resolved'*s default.

##### Fallback

If *systemd-resolved* does not receive DNS server addresses from the [network manager](/index.php/Network_manager "Network manager") and no DNS servers are configured [manually](#Manually) then *systemd-resolved* falls back to the fallback DNS addresses to ensure that DNS resolution always works.

**Note:** Currently *systemd-resolved* uses [Google DNS](/index.php/Alternative_DNS_services#Google "Alternative DNS services") as the fallback DNS.

The addresses can be changed by setting `FallbackDNS=` in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5). E.g.:

 `/etc/systemd/resolved.conf.d/fallback_dns.conf` 
```
[Resolve]
FallbackDNS=127.0.0.1 ::1
```

To disable the fallback DNS funtionality set the `FallbackDNS` option without specifying any addresses:

 `/etc/systemd/resolved.conf.d/fallback_dns.conf` 
```
[Resolve]
FallbackDNS=
```

#### DNSSEC

[DNSSEC](/index.php/DNSSEC "DNSSEC") validation in disabled in the [systemd](https://www.archlinux.org/packages/?name=systemd) package ([FS#59391](https://bugs.archlinux.org/task/59391)). It can be enabled by setting `DNSSEC=true`:

 `/etc/systemd/resolved.conf.d/dnssec.conf` 
```
[Resolve]
DNSSEC=true
```

Test DNSSEC validation by querying a domain with a invalid signature:

 `$ resolvectl query sigfail.verteiltesysteme.net` 
```
sigfail.verteiltesysteme.net: resolve call failed: DNSSEC validation failed: invalid

```

Now test a domain with valid signature:

 `$ resolvectl query sigok.verteiltesysteme.net` 
```
sigok.verteiltesysteme.net: 134.91.78.139

-- Information acquired via protocol DNS in 266.3ms.
-- Data is authenticated: yes

```

#### DNS over TLS

**Warning:** As of version 239:

*   Only opportunistic mode is supported making *systemd-resolved* vulnerable to downgrade attacks.
*   DNS server certificates are not checked making *systemd-resolved* vulnerable to man-in-the-middle attacks. See [systemd issue 9397](https://github.com/systemd/systemd/issues/9397).

DNS over TLS is disabled by default. To enable it change the `DNSOverTLS=` setting in the `[Resolve]` section in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

 `/etc/systemd/resolved.conf.d/dns_over_tls.conf` 
```
[Resolve]
DNSOverTLS=opportunistic
```

**Note:** The used DNS server must support DNS over TLS otherwise *systemd-resolved* will disable DNS over TLS for the connection.

### mDNS

*systemd-resolved* is capable of working as a [multicast DNS](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS") resolver and responder.

The resolver provides [hostname](/index.php/Hostname "Hostname") resolution using a "*hostname*.local" naming scheme.

mDNS will only be activated for the connection if both the systemd-resolved's global setting (`MulticastDNS=` in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5)) and the [network manager's](/index.php/Network_manager "Network manager") per-connection setting is enabled. By default *systemd-resolved* enables mDNS responder, but both [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager "NetworkManager") do not enable it for connections.

*   For [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") the setting is `MulticastDNS=` in the `[Network]` section. See [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).
*   For [NetworkManager](/index.php/NetworkManager "NetworkManager") the setting is `mdns=` in the `[connection]` section, see [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5). The values are `0` - disabled, `1` - resolver only, `2` - resolver and responder. [[1]](https://cgit.freedesktop.org/NetworkManager/NetworkManager/tree/libnm-core/nm-setting-connection.h#n102)

**Tip:** The default for all [NetworkManager](/index.php/NetworkManager "NetworkManager") connections can be set by creating a configuration file in `/etc/NetworkManager/conf.d/` and setting `connection.mdns=` in the `[connection]` section. For example the following will enable mDNS resolver for all connections: `/etc/NetworkManager/conf.d/mdns.conf` 
```
[connection]
connection.mdns=1
```

See [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).

If you plan to use mDNS and use a [firewall](/index.php/Firewall "Firewall"), make sure to open UDP port `5353`.

### LLMNR

[Link-Local Multicast Name Resolution](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution "wikipedia:Link-Local Multicast Name Resolution") is a [hostname](/index.php/Hostname "Hostname") resolution protocol created by Microsoft.

LLMNR will only be activated for the connection if both the systemd-resolved's global setting (`LLMNR=` in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5)) and the [network manager's](/index.php/Network_manager "Network manager") per-connection setting is enabled. By default *systemd-resolved* enables LLMNR responder, [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") enables it by default and [NetworkManager](/index.php/NetworkManager "NetworkManager") does not have a setting to control it.

For [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") the setting is `LLMNR=` in the `[Network]` section. See [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).

**Warning:** Since [NetworkManager](/index.php/NetworkManager "NetworkManager") lacks control over per-connection LLMNR setting, if do not plan to use LLMNR the only option is to disable it globally in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5). E.g.: `/etc/systemd/resolved.conf.d/disable_llmnr.conf` 
```
[Resolve]
LLMNR=false
```

If you plan to use LLMNR and use a [firewall](/index.php/Firewall "Firewall"), make sure to open UDP and TCP ports `5355`.

## Lookup

To query DNS records, mDNS or LLMNR hosts you can use the *resolvectl* utility.

For example, to query a DNS record:

 `$ resolvectl query archlinux.org` 
```
archlinux.org: 2a01:4f8:172:1d86::1
               138.201.81.199

-- Information acquired via protocol DNS in 48.4ms.
-- Data is authenticated: no

```