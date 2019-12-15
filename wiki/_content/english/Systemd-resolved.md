Related articles

*   [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")
*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")
*   [Avahi](/index.php/Avahi "Avahi")

[systemd-resolved](https://www.freedesktop.org/wiki/Software/systemd/resolved/) is a [systemd](/index.php/Systemd "Systemd") service that provides network name resolution to local applications via a [D-Bus](/index.php/D-Bus "D-Bus") interface, the `resolve` [NSS](/index.php/Name_Service_Switch "Name Service Switch") service ([nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8)), and a local DNS stub listener on `127.0.0.53`. See [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) for the usage.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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

*systemd-resolved* is a part of the [systemd](https://www.archlinux.org/packages/?name=systemd) package that is installed by default.

## Configuration

*systemd-resolved* provides resolver services for [Domain Name System (DNS)](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") (including [DNSSEC](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions") and [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS")), [Multicast DNS (mDNS)](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS") and [Link-Local Multicast Name Resolution (LLMNR)](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution "wikipedia:Link-Local Multicast Name Resolution").

The resolver can be configured by editing `/etc/systemd/resolved.conf` and/or drop-in *.conf* files in `/etc/systemd/resolved.conf.d/`. See [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

To use *systemd-resolved* [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `systemd-resolved.service`.

**Tip:** To understand the context around the choices and switches, one can turn on detailed debug information for *systemd-resolved* as described in [systemd#Diagnosing a service](/index.php/Systemd#Diagnosing_a_service "Systemd").

### DNS

*systemd-resolved* has four different modes for handling the [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution") (the four modes are described in [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#%2FETC%2FRESOLV.CONF)). We will focus here on the two most relevant modes.

1.  Using the systemd DNS stub file - the systemd DNS stub file `/run/systemd/resolve/stub-resolv.conf` contains the local stub `127.0.0.53` as the only DNS server and a list of search domains. This is the **recommended** mode of operation. The service users are advised to redirect the `/etc/resolv.conf` file to the local stub DNS resolver file `/run/systemd/resolve/stub-resolv.conf` managed by *systemd-resolved*. This propagates the systemd managed configuration to all the clients. This can be done by replacing `/etc/resolv.conf` with a symbolic link to the systemd stub: `# ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf` 
2.  Preserving *resolv.conf* - this mode preserves `/etc/resolv.conf` and *systemd-resolved* is simply a client of this file. This mode is less disruptive as `/etc/resolv.conf` can continue to be managed by other packages.

**Note:** The mode of operation of *systemd-resolved* is detected automatically, depending on whether `/etc/resolv.conf` is a symlink to the local stub DNS resolver file or contains server names.

#### Setting DNS servers

**Tip:** In order to check the DNS actually used by *systemd-resolved*, the command to use is:
```
$ resolvectl status

```

##### Automatically

*systemd-resolved* will work out of the box with a [network manager](/index.php/Network_manager "Network manager") using `/etc/resolv.conf`. No particular configuration is required since *systemd-resolved* will be detected by following the `/etc/resolv.conf` symlink. This is going to be the case with [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") or [NetworkManager](/index.php/NetworkManager "NetworkManager").

However, if the [DHCP](/index.php/DHCP "DHCP") and [VPN](/index.php/VPN "VPN") clients use the [resolvconf](https://en.wikipedia.org/wiki/resolvconf "wikipedia:resolvconf") program to set name servers and search domains (see [openresolv#Users](/index.php/Openresolv#Users "Openresolv") for a list of software that use *resolvconf*), the additional package [systemd-resolvconf](https://www.archlinux.org/packages/?name=systemd-resolvconf) is needed to provide the `/usr/bin/resolvconf` symlink.

**Note:** *systemd-resolved* has a limited *resolvconf* interface and may not work with all the clients, see [resolvectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvectl.1#COMPATIBILITY_WITH_RESOLVCONF%288%29) for more information.

##### Manually

In local DNS stub mode, custom DNS server(s) can be set in the [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5) file:

 `/etc/systemd/resolved.conf.d/dns_servers.conf` 
```
[Resolve]
DNS=192.168.35.1 fd7b:d0bd:7a6e::1
Domains=~.
```

**Note:** Without the `Domains=~.` option in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5), *systemd-resolved* might use the per-link DNS servers, if any of them set `Domains=~.` in the per-link configuration. This option will not affect queries of domain names that match the more specific search domains specified in per-link configuration, they will still be resolved using their respective per-link DNS servers.

##### Fallback

If *systemd-resolved* does not receive DNS server addresses from the [network manager](/index.php/Network_manager "Network manager") and no DNS servers are configured [manually](#Manually) then *systemd-resolved* falls back to the fallback DNS addresses to ensure that DNS resolution always works.

**Note:** The fallback DNS are in this order: [Cloudflare](/index.php/Alternative_DNS_services#Cloudflare "Alternative DNS services"), [Quad9](/index.php/Alternative_DNS_services#Quad9 "Alternative DNS services") (without filtering and without DNSSEC) and [Google](/index.php/Alternative_DNS_services#Google "Alternative DNS services"); see the [systemd PKGBUILD](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/systemd#n103) where the servers are defined.

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

By default [DNSSEC](/index.php/DNSSEC "DNSSEC") validation will only be enabled if the upstream DNS server supports it. If you want to always validate DNSSEC, thus breaking DNS resolution with name servers that do not support it, set `DNSSEC=true`:

 `/etc/systemd/resolved.conf.d/dnssec.conf` 
```
[Resolve]
DNSSEC=true
```

**Tip:** If your DNS server does not support DNSSEC and you experience problems with the default allow-downgrade mode (e.g. [systemd issue 10579](https://github.com/systemd/systemd/issues/10579)), you can explicitly disable systemd-resolved's DNSSEC support by setting `DNSSEC=false`.

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

**Warning:** systemd-resolved only validates the DNS server certificate if it is issued for the server's IP address (a rare occurrence). DNS server certificates without an IP address are not checked making *systemd-resolved* vulnerable to man-in-the-middle attacks. See [systemd issue 9397](https://github.com/systemd/systemd/issues/9397).

DNS over TLS is disabled by default. To enable it change the `DNSOverTLS=` setting in the `[Resolve]` section in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

 `/etc/systemd/resolved.conf.d/dns_over_tls.conf` 
```
[Resolve]
DNSOverTLS=yes
```

**Note:** The used DNS server must support DNS over TLS otherwise all DNS requests will fail.

### mDNS

*systemd-resolved* is capable of working as a [multicast DNS](https://en.wikipedia.org/wiki/Multicast_DNS "wikipedia:Multicast DNS") resolver and responder.

The resolver provides [hostname](/index.php/Hostname "Hostname") resolution using a "*hostname*.local" naming scheme.

mDNS will only be activated for the connection if both the systemd-resolved's global setting (`MulticastDNS=` in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5)) and the [network manager's](/index.php/Network_manager "Network manager") per-connection setting is enabled. By default *systemd-resolved* enables mDNS responder, but both [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager "NetworkManager") do not enable it for connections:

*   For [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") the setting is `MulticastDNS=` in the `[Network]` section. See [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).
*   For [NetworkManager](/index.php/NetworkManager "NetworkManager") the setting is `mdns=` in the `[connection]` section, see [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5). The values are `0` - disabled, `1` - resolver only, `2` - resolver and responder. [[1]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/blob/master/libnm-core/nm-setting-connection.h#L88)[[2]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/301)

**Note:** If [Avahi](/index.php/Avahi "Avahi") has been installed, consider [disabling](/index.php/Disabling "Disabling") `avahi-daemon.service` and `avahi-daemon.socket` to prevent conflicts with *systemd-resolved*.

**Tip:** The default for all [NetworkManager](/index.php/NetworkManager "NetworkManager") connections can be set by creating a configuration file in `/etc/NetworkManager/conf.d/` and setting `connection.mdns=` in the `[connection]` section. For example the following will enable mDNS resolver for all connections: `/etc/NetworkManager/conf.d/mdns.conf` 
```
[connection]
connection.mdns=1
```

See [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).

If you plan to use mDNS and use a [firewall](/index.php/Firewall "Firewall"), make sure to open UDP port `5353`.

### LLMNR

[Link-Local Multicast Name Resolution](https://en.wikipedia.org/wiki/Link-Local_Multicast_Name_Resolution "wikipedia:Link-Local Multicast Name Resolution") is a [hostname](/index.php/Hostname "Hostname") resolution protocol created by Microsoft.

LLMNR will only be activated for the connection if both the systemd-resolved's global setting (`LLMNR=` in [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5)) and the [network manager's](/index.php/Network_manager "Network manager") per-connection setting is enabled. By default *systemd-resolved* enables LLMNR responder; [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [NetworkManager](/index.php/NetworkManager "NetworkManager") enable it for connections.

*   For [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") the setting is `LLMNR=` in the `[Network]` section. See [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).
*   For [NetworkManager](/index.php/NetworkManager "NetworkManager") the setting is `llmnr=` in the `[connection]` section, see [nm-settings(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nm-settings.5). The values are `0` - disabled, `1` - resolver only, `2` - resolver and responder. [[3]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/blob/master/libnm-core/nm-setting-connection.h#L106)[[4]](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/301)

**Tip:** The default for all [NetworkManager](/index.php/NetworkManager "NetworkManager") connections can be set by creating a configuration file in `/etc/NetworkManager/conf.d/` and setting `connection.llmnr=` in the `[connection]` section. For example the following will disable LLMNR for all connections: `/etc/NetworkManager/conf.d/llmnr.conf` 
```
[connection]
connection.llmnr=0
```

See [NetworkManager.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/NetworkManager.conf.5).

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

See [resolvectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvectl.1#EXAMPLES) for more examples.