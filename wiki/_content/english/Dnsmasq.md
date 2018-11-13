Related articles

*   [BIND](/index.php/BIND "BIND")
*   [DNSCrypt](/index.php/DNSCrypt "DNSCrypt")
*   [DNSSEC](/index.php/DNSSEC "DNSSEC")
*   [Pdnsd](/index.php/Pdnsd "Pdnsd")
*   [unbound](/index.php/Unbound "Unbound")

[dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) provides a [DNS server](https://en.wikipedia.org/wiki/Name_server "wikipedia:Name server"), a [DHCP server](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol") with support for [DHCPv6](https://en.wikipedia.org/wiki/DHCPv6 "wikipedia:DHCPv6") and [PXE](https://en.wikipedia.org/wiki/Preboot_Execution_Environment "wikipedia:Preboot Execution Environment"), and a [TFTP server](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol "wikipedia:Trivial File Transfer Protocol"). It is designed to be lightweight and have a small footprint, suitable for resource constrained routers and firewalls. dnsmasq can also be configured to cache DNS queries for improved DNS lookup speeds to previously visited sites.

## Contents

*   [1 Installation](#Installation)
*   [2 Start the daemon](#Start_the_daemon)
*   [3 Configuration](#Configuration)
    *   [3.1 DNS server](#DNS_server)
        *   [3.1.1 DNS addresses file and forwarding](#DNS_addresses_file_and_forwarding)
            *   [3.1.1.1 openresolv](#openresolv)
            *   [3.1.1.2 Manual forwarding](#Manual_forwarding)
        *   [3.1.2 Adding a custom domain](#Adding_a_custom_domain)
        *   [3.1.3 Test](#Test)
    *   [3.2 DHCP server](#DHCP_server)
        *   [3.2.1 Test](#Test_2)
    *   [3.3 TFTP server](#TFTP_server)
    *   [3.4 PXE server](#PXE_server)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Prevent OpenDNS redirecting Google queries](#Prevent_OpenDNS_redirecting_Google_queries)
    *   [4.2 Override addresses](#Override_addresses)
    *   [4.3 More than one instance](#More_than_one_instance)
        *   [4.3.1 Static](#Static)
        *   [4.3.2 Dynamic](#Dynamic)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package.

## Start the daemon

[Start/enable](/index.php/Start/enable "Start/enable") `dnsmasq.service`.

To see if dnsmasq started properly, check the system's journal:

```
$ journalctl -u dnsmasq.service

```

The network will also need to be restarted so the DHCP client can create a new `/etc/resolv.conf`.

## Configuration

To configure dnsmasq, you need to edit `/etc/dnsmasq.conf`. The file contains extensive comments explaining its options. For all available options see [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8).

**Warning:** dnsmasq by default enables its DNS server. If you do not require it, you need to explicitly disable it by setting DNS port to `0`: `port=0` 

**Tip:** To check configuration file(s) syntax, execute:
```
$ dnsmasq --test

```

### DNS server

To set up dnsmasq as a DNS caching daemon on a single computer specify a `listen-address` directive, adding in the localhost IP address:

```
listen-address=::1,127.0.0.1

```

To use this computer to listen on its LAN IP address for other computers on the network. It is recommended that you use a static LAN IP in this case. E.g.:

```
listen-address=::1,127.0.0.1,192.168.1.1

```

Set the number of cached domain names with `cache-size=*size*` (the default is `150`):

```
cache-size=1000

```

To validate [DNSSEC](/index.php/DNSSEC "DNSSEC") load the DNSSEC trust anchors provided by the [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) package and set the option `dnssec`:

```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec

```

See [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) for more options you might want to use.

#### DNS addresses file and forwarding

After configuring dnsmasq, you need to add the localhost addresses as the only nameservers in `/etc/resolv.conf`. This causes all queries to be sent to dnsmasq.

Since dnsmasq is not a recursive DNS server you must set up forwarding to an external DNS server. This can be done automatically by using [openresolv](/index.php/Openresolv "Openresolv") or by manually specifying the DNS server address in dnsmasq's configuration.

##### openresolv

If your network manager supports *resolvconf*, instead of directly altering `/etc/resolv.conf`, you can use [openresolv](/index.php/Openresolv "Openresolv") to generate configuration files for dnsmasq. [[1]](https://roy.marples.name/projects/openresolv/config)

Edit `/etc/resolvconf.conf` and add the loopback addresses as name servers, and configure openresolv to write out dnsmasq configuration:

 `/etc/resolvconf.conf` 
```
# Use the local name server
name_servers="::1 127.0.0.1"

# Write out dnsmasq extended configuration and resolv files
dnsmasq_conf=/etc/dnsmasq-openresolv.conf
dnsmasq_resolv=/etc/dnsmasq-resolv.conf
```

Run `resolvconf -u` so that the configuration files get created. If the files do not exist `dnsmasq.service` will fail to start.

Edit dnsmasq's configuration file to use openresolv's generated configuration:

```
# Read configuration generated by openresolv
conf-file=/etc/dnsmasq-openresolv.conf
resolv-file=/etc/dnsmasq-resolv.conf

```

##### Manual forwarding

First you must set localhost addresses as the only nameservers in `/etc/resolv.conf`:

 `/etc/resolv.conf` 
```
nameserver ::1
nameserver 127.0.0.1

```

See [Domain name resolution#Overwriting of /etc/resolv.conf](/index.php/Domain_name_resolution#Overwriting_of_/etc/resolv.conf "Domain name resolution") on how to protect `/etc/resolv.conf` from modification.

The upstream DNS server addresses must then be specified in dnsmasq's configuration file as `server=*server_address*`. Also add `no-resolv` so dnsmasq does not needlessly read `/etc/resolv.conf` which only contains the localhost addresses of itself.

```
no-resolv

# Google's nameservers, for example
server=8.8.8.8
server=8.8.4.4
```

Now DNS queries will be resolved with dnsmasq, only checking external servers if it cannot answer the query from its cache.

#### Adding a custom domain

It is possible to add a custom domain to hosts in your (local) network:

```
local=/lan/
domain=lan

```

In this example it is possible to ping a host/device (e.g. defined in your `/etc/hosts` file) as `*hostname*.lan`.

Uncomment `expand-hosts` to add the custom domain to hosts entries:

```
expand-hosts

```

Without this setting, you will have to add the domain to entries of `/etc/hosts`.

#### Test

To do a lookup speed test choose a website that has not been visited since dnsmasq has been started (*drill* is part of the [ldns](https://www.archlinux.org/packages/?name=ldns) package):

```
$ drill archlinux.org | grep "Query time"

```

Running the command again will use the cached DNS IP and result in a faster lookup time if dnsmasq is setup correctly:

 `$ drill archlinux.org | grep "Query time"` 
```
;; Query time: 18 msec

```
 `$ drill archlinux.org | grep "Query time"` 
```
;; Query time: 2 msec

```

To test if DNSSEC validation is working see [DNSSEC#Testing](/index.php/DNSSEC#Testing "DNSSEC").

### DHCP server

By default dnsmasq has the DHCP functionality turned off, if you want to use it you must turn it on. Here are the important settings:

```
# Only listen to routers' LAN NIC.  Doing so opens up tcp/udp port 53 to
# localhost and udp port 67 to world:
interface=<LAN-NIC>

# dnsmasq will open tcp/udp port 53 and udp port 67 to world to help with
# dynamic interfaces (assigning dynamic ips). Dnsmasq will discard world
# requests to them, but the paranoid might like to close them and let the 
# kernel handle them:
bind-interfaces

# Optionally set a domain name
domain=example.com

# Set default gateway
dhcp-option=3,0.0.0.0

# Set DNS servers to announce
dhcp-option=6,0.0.0.0

# Dynamic range of IPs to make available to LAN PC and the lease time. 
# Ideally set the lease time to 5m only at first to test everything works okay before you set long-lasting records.
dhcp-range=192.168.111.50,192.168.111.100,12h

# If you’d like to have dnsmasq assign static IPs to some clients, bind the LAN computers
# NIC MAC addresses:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50
dhcp-host=aa:bb:cc:ff:dd:ee,192.168.111.51

```

See [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) for more options.

#### Test

From a computer that is connected to the one with dnsmasq on it, configure it to use DHCP for automatic IP address assignment, then attempt to log into the network normally.

If you inspect the `/var/lib/misc/dnsmasq.leases` file on the server, you should be able to see the lease.

### TFTP server

dnsmasq has built-in [TFTP](/index.php/TFTP "TFTP") server.

To use it, create a directory for TFTP root (e.g. `/srv/tftp`) to put transferable files in.

For increased security it is advised to use dnsmasq's TFTP secure mode. In secure mode only files owned by the `dnsmasq` user will be served over TFTP. You will need to [chown](/index.php/Chown "Chown") TFTP root and all files in it to `dnsmasq` user to use this feature.

Enable TFTP:

```
enable-tftp
tftp-root=/srv/tftp
tftp-secure

```

See [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) for more options.

### PXE server

PXE requires DHCP and TFTP servers, both functions can be provided by dnsmasq.

**Tip:** dnsmasq can run in "proxy-DHCP" mode and add PXE booting options to a network with an already running DHCP server:
```
interface=*enp0s0*
bind-dynamic
dhcp-range=*192.168.0.1*,proxy
```

1.  set up [#TFTP server](#TFTP_server) and [#DHCP server](#DHCP_server)
2.  copy and configure a PXE compatible bootloader (e.g. [PXELINUX](/index.php/PXELINUX "PXELINUX")) on TFTP root
3.  enable PXE in `/etc/dnsmasq.conf`:

**Note:**

*   file paths are relative to TFTP root
*   if the file has a `.0` suffix, you must exclude the suffix in `pxe-service` options

To simply send one file:

```
dhcp-boot=lpxelinux.0

```

To send a file depending on client architecture:

```
pxe-service=x86PC, "PXELINUX (BIOS)", "bios/lpxelinux"
pxe-service=X86-64_EFI, "PXELINUX (EFI)", "efi64/syslinux.efi"

```

**Note:** In case `pxe-service` does not work (especially for UEFI-based clients), combination of `dhcp-match` and `dhcp-boot` can be used. See [RFC4578](https://tools.ietf.org/html/rfc4578#section-2.1) for more `client-arch` numbers for use with dhcp boot protocol.

```
dhcp-match=set:efi-x86_64,option:client-arch,7
dhcp-match=set:efi-x86_64,option:client-arch,9
dhcp-match=set:efi-x86,option:client-arch,6
dhcp-match=set:bios,option:client-arch,0
dhcp-boot=tag:efi-x86_64,"efi64/syslinux.efi"
dhcp-boot=tag:efi-x86,"efi32/syslinux.efi"
dhcp-boot=tag:bios,"bios/lpxelinux.0"

```

See [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) for more options.

The rest is up to the [bootloader](/index.php/Bootloader "Bootloader").

## Tips and tricks

### Prevent OpenDNS redirecting Google queries

To prevent OpenDNS from redirecting all Google queries to their own search server, add to `/etc/dnsmasq.conf`:

 `server=/www.google.com/<ISP DNS IP>` 

### Override addresses

In some cases, such as when operating a captive portal, it can be useful to resolve specific domains names to a hard-coded set of addresses. This is done with the `address` config:

```
address=/example.com/1.2.3.4

```

Furthermore, it's possible to return a specific address for all domain names that are not answered from `/etc/hosts` or DHCP by using a special wildcard:

```
address=/#/1.2.3.4

```

### More than one instance

If we want two or more dnsmasq servers works per interface(s).

#### Static

To do this staticly, server per interface, use `interface` and `bind-interface` options. This enforce start second dnsmasq.

#### Dynamic

In this case we can exclude per interface and bind any others:

```
except-interface=lo
bind-dynamic

```

**Note:** This is default in [libvirt](/index.php/Libvirt "Libvirt").

## See also

*   [Caching Nameserver using dnsmasq, and a few other tips and tricks.](http://www.g-loaded.eu/2010/09/18/caching-nameserver-using-dnsmasq/)