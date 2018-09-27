Related articles

*   [DNSSEC](/index.php/DNSSEC "DNSSEC")
*   [BIND](/index.php/BIND "BIND")
*   [DNSCrypt](/index.php/DNSCrypt "DNSCrypt")
*   [dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Pdnsd](/index.php/Pdnsd "Pdnsd")
*   [unbound](/index.php/Unbound "Unbound")

[Stubby](https://dnsprivacy.org/wiki/display/DP/DNS+Privacy+Daemon+-+Stubby) is an application that acts as a local DNS Privacy stub resolver (using DNS-over-TLS). Stubby encrypts DNS queries sent from a client machine (desktop or laptop) to a DNS Privacy resolver increasing end user privacy.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Select resolver](#Select_resolver)
    *   [2.2 Modify resolv.conf](#Modify_resolv.conf)
    *   [2.3 Start systemd service](#Start_systemd_service)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Local DNS cache configuration](#Local_DNS_cache_configuration)
        *   [3.1.1 Change port](#Change_port)
            *   [3.1.1.1 dnsmasq](#dnsmasq)
            *   [3.1.1.2 Other DNS cachers](#Other_DNS_cachers)

## Installation

[Install](/index.php/Install "Install") the [stubby](https://www.archlinux.org/packages/?name=stubby) package.

## Configuration

**Tip:** An example configuration file, `/etc/stubby/stubby.yml.example` is provided

To configure *stubby*, perform the following steps:

### Select resolver

Upon installation, Stubby has some default resolvers. They can be found and edited in `/etc/stubby/stubby.yml`. You can use the defaults, uncomment one of prewritten resolvers or find another resolver from [this list](https://dnsprivacy.org/wiki/display/DP/DNS+Privacy+Test+Servers).

Example of a valid resolver configuration:

```
upstream_recursive_servers:

# The Surfnet/Sinodun servers
 - address_data: 145.100.185.15
    tls_auth_name: "dnsovertls.sinodun.com"
    tls_pubkey_pinset:
      - digest: "sha256"
        value: 62lKu9HsDVbyiPenApnc4sfmSYTHOVfFgL3pyB+cBL4=

# The Cloudflare server
- address_data: 1.1.1.1
    tls_port: 853
    tls_auth_name: "cloudflare-dns.com"

```

**Note:** For further information on configuring Stubby see [Configuring Stubby](https://dnsprivacy.org/wiki/display/DP/Configuring+Stubby).

### Modify resolv.conf

After selecting a resolver, modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with address for *localhost*:

 `/etc/resolv.conf` 
```
nameserver ::1
nameserver 127.0.0.1
```

Other programs may overwrite this setting; see [resolv.conf#Overwriting of /etc/resolv.conf](/index.php/Resolv.conf#Overwriting_of_.2Fetc.2Fresolv.conf "Resolv.conf") for details.

### Start systemd service

Finally, [start and enable](/index.php/Enable "Enable") the `stubby.service`.

## Tips and tricks

### Local DNS cache configuration

Stubby does not have a built-in DNS cache, therefore every single query is transmitted and resolved, which can slow down connections. Setting up a dns cache requires installing and configuring a seperate dns cacher.

#### Change port

In order to forward to a local DNS cache, Stubby should listen on a port different from the default `53`, since the DNS cache itself needs to listen on `53` and query Stubby on a different port. Port number `53000` is used as an example in this section. In this example, the port number is larger than 1024 so *stubby* is not required to be run by root.

Edit the value of `listen_addresses` in `/etc/stubby/stubby.yml` as follows:

```
listen_addresses:
  - 127.0.0.1@53000
  -  0::1@53000

```

##### dnsmasq

Configure dnsmasq as a [local DNS cache](/index.php/Dnsmasq#DNS_server "Dnsmasq"). The basic configuration to work with Stubby is the following:

 `/etc/dnsmasq.conf` 
```
no-resolv
proxy-dnssec
server=::1#53000
server=127.0.0.1#53000
listen-address=::1,127.0.0.1
```

[Restart](/index.php/Restart "Restart") `dnsmasq.service` to apply the changes.

##### Other DNS cachers

For more dns cachers, see [DNSCrypt#Local DNS cache configuration](/index.php/DNSCrypt#Local_DNS_cache_configuration "DNSCrypt"). The configurations should be similar if not identical.