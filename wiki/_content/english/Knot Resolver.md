Related articles

*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")

[Knot Resolver](https://www.knot-resolver.cz/) is a full (recursive), caching DNS resolver. It is designed to scale from small home-office networks to providing DNS servers at the scale of ISPs. Knot Resolver supports [DNSSEC](/index.php/DNSSEC "DNSSEC").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Knot Resolver and dnsmasq](#Knot_Resolver_and_dnsmasq)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [knot-resolver](https://aur.archlinux.org/packages/knot-resolver/) package.

## Configuration

[Start/enable](/index.php/Start/enable "Start/enable") `kresd.socket`.

To use the DNS server locally, use the `127.0.0.1` nameserver, see [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution").

By default, the resolver will listen on localhost, port `53`. If the resolver should be accessible from other hosts, extend the `kresd.socket` definition by [editing](/index.php/Edit "Edit") `kresd.socket` or `kresd-tls.socket` (for DNS-over-TLS connections) and add the appropriate directives, for example:

```
[Socket]
ListenDatagram=192.0.2.115:53
ListenStream=192.0.2.115:53

```

**Note:** Unless you specifically want to run an open DNS resolver, do not listen on a public (internet-facing) IP address.

If the resolver should respect entries from the `/etc/hosts` file, add a `hints.add_hosts()` line to `/etc/knot-resolver/kresd.conf`.

### Knot Resolver and dnsmasq

If [dnsmasq](/index.php/Dnsmasq "Dnsmasq") is used for managing DHCP, then advertising a kresd instance works like any other external DNS server would: By adding an `dhcp-option=option:dns-server,<Server Address>` line to the dnsmasq configuration file.

Note that a default configuration of dnsmasq will clash with the default configuration of kresd, since both will attempt to use port `53`. [Disable the dnsmasq DNS functionality](/index.php/Dnsmasq#Configuration "Dnsmasq") (`port=0`), or assign a different port to either service.

## See also

*   kresd.systemd(7)
*   [Knot Resolver documentation](https://knot-resolver.readthedocs.io/en/stable/daemon.html)