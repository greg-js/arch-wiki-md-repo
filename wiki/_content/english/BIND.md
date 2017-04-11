Berkeley Internet Name Daemon (BIND) is the reference implementation of the Domain Name System (DNS) protocols.

**Note:** The organization developing BIND is serving security notices to paying customers up to four days before Linux distributions or the general public.[[1]](https://kb.isc.org/article/AA-00861/0/ISC-Software-Defect-and-Security-Vulnerability-Disclosure-Policy.html)

## Contents

*   [1 Installation](#Installation)
*   [2 Forwarding](#Forwarding)
*   [3 A configuration template for running a domain](#A_configuration_template_for_running_a_domain)
    *   [3.1 1\. Creating a zonefile](#1._Creating_a_zonefile)
    *   [3.2 2\. Configuring master server](#2._Configuring_master_server)
    *   [3.3 3\. Setting this to be your default DNS server](#3._Setting_this_to_be_your_default_DNS_server)
*   [4 Configuring BIND to serve DNSSEC signed zones](#Configuring_BIND_to_serve_DNSSEC_signed_zones)
*   [5 Automatically listen on new interfaces](#Automatically_listen_on_new_interfaces)
*   [6 Running BIND in a chrooted environment](#Running_BIND_in_a_chrooted_environment)
    *   [6.1 Creating the Jail House](#Creating_the_Jail_House)
    *   [6.2 Service File](#Service_File)
*   [7 See also](#See_also)

## Installation

These few steps show you how to install BIND and set it up as a local caching-only server.

[Install](/index.php/Install "Install") the [bind](https://www.archlinux.org/packages/?name=bind) package.

Optionally edit `/etc/named.conf` and add this into the options section, to only allow connections from the localhost:

```
listen-on { 127.0.0.1; };

```

Edit [resolv.conf](/index.php/Resolv.conf "Resolv.conf") to use the local DNS server, 127.0.0.1.

[Start](/index.php/Start "Start") `named.service`.

## Forwarding

When BIND acts as a forwarding DNS server, it merely acts as a cache for known queries, and naively forwards all other requests to a predefined upstream DNS server - such as the one managed by your ISP, or some well-known global DNS service like OpenNIC or Google DNS servers.

To setup a forwarding DNS server, add these lines to `/etc/named.conf` in either the global options section or in a specific zone, and change IP address according to your setup.

```
options {
 listen-on { 192.168.66.1; };
 forwarders { 8.8.8.8; 8.8.4.4; };
};

```

Do not forget to [restart](/index.php/Restart "Restart") `named.service`.

## A configuration template for running a domain

This is a simple tutorial in howto setup a simple home network DNS-server with bind. In our example we use "domain.tld" as our domain.

For a more elaborate example see [Two-in-one DNS server with BIND9](http://www.howtoforge.com/two_in_one_dns_bind9_views). Another guide at [Linux Home Server HOWTO - Domain name system (BIND)](http://www.brennan.id.au/08-Domain_Name_System_BIND.html) will show you how to set up internal network name resolution in no time; short, on-point and very informative.

### 1\. Creating a zonefile

```
# nano /var/named/domain.tld.zone

```

```
$TTL 7200
; domain.tld
@       IN      SOA     ns01.domain.tld. postmaster.domain.tld. (
                                        2007011601 ; Serial
                                        28800      ; Refresh
                                        1800       ; Retry
                                        604800     ; Expire - 1 week
                                        86400 )    ; Minimum
                IN      NS      ns01
                IN      NS      ns02
ns01            IN      A       0.0.0.0
ns02            IN      A       0.0.0.0
localhost       IN      A       127.0.0.1
@               IN      MX 10   mail
imap            IN      CNAME   mail
smtp            IN      CNAME   mail
@               IN      A       0.0.0.0
www             IN      A       0.0.0.0
mail            IN      A       0.0.0.0
@               IN      TXT     "v=spf1 mx"

```

$TTL defines the default time-to-live in seconds for all record types. In this example it is 2 hours.

**Serial must be incremented manually before restarting named every time you change a resource record for the zone.** If you forget to do it slaves will not re-transfer the zone: they only do it if the serial is greater than that of the last time they transferred the zone.

### 2\. Configuring master server

Add your zone to `/etc/named.conf`:

```
zone "domain.tld" IN {
        type master;
        file "domain.tld.zone";
        allow-update { none; };
        notify no;
};

```

[Start/enable](/index.php/Start/enable "Start/enable") `named.service` and you are done.

Otherwise [reload](/index.php/Reload "Reload") the configuration files.

The latter option will keep your nameserver available while still allowing the configuration change.

### 3\. Setting this to be your default DNS server

If you are running your own DNS server, you might as well use it for all DNS lookups. This will require the ability to do *recursive* lookups. In order to prevent [DNS Amplification Attacks](https://www.us-cert.gov/ncas/alerts/TA13-088A), recursion is turned off by default for most resolvers. The default Arch `/etc/named.conf` file allows for recursion only on the loopback interface:

```
allow-recursion { 127.0.0.1; };

```

So to facilitate general DNS lookups from your host, your [resolv.conf](/index.php/Resolv.conf "Resolv.conf") configuration file must have 127.0.0.1 as a name server. See [Resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") on how to keep this from being overwritten.

If you want to provide name service for your local network; e.g. 192.168.0, you must add the appropriate range of IP addresses to `/etc/named.conf`:

```
allow-recursion { 192.168.0.0/24; 127.0.0.1; };

```

## Configuring BIND to serve DNSSEC signed zones

See [DNSSEC#BIND (serving signed DNS zones)](/index.php/DNSSEC#BIND_.28serving_signed_DNS_zones.29 "DNSSEC")

## Automatically listen on new interfaces

By default bind scan for new interfaces and stop listening on interfaces which no longer exist every hours. You can tune this value by adding :

```
interface-interval <rescan-timeout-in-minutes>;

```

parameter into `named.conf` options section. Max value is 28 days. (40320 min)
You can disable this feature by setting its value to 0.

Then restart the service.

## Running BIND in a chrooted environment

Running in a [chroot](/index.php/Chroot "Chroot") environment is not required but improves security.

### Creating the Jail House

In order to do this, we first need to create a place to keep the jail, we shall use `/srv/named`, and then put the required files into the jail.

```
 mkdir -p /srv/named/{dev,etc,usr/lib/engines,var/{run,log,named}}
 # Copy over required system files
 cp -av /etc/{localtime,named.conf} /srv/named/etc/
 cp -av /usr/lib/engines/* /srv/named/usr/lib/engines/
 cp -av /var/named/* /srv/named/var/named/.
 # Set up required dev nodes
 mknod /srv/named/dev/null c 1 3
 mknod /srv/named/dev/random c 1 8
 # Set Ownership of the files
 chown -R named:named /srv/named

```

This should create the required file system for the jail.

### Service File

Next we need to create the new service file which will allow force bind into the chroot

```
 cp -av /usr/lib/systemd/system/named.service /etc/systemd/system/named-chroot.service

```

we need to edit how the service calls bind.

 `/etc/systemd/system/named-chroot.service` 
```
  ExecStart=/usr/bin/named -4 -f -u named -t "/srv/named"

```

Now, reload systemd `systemctl daemon-reload`. Then [start](/index.php/Start "Start") `named-chroot.service`

## See also

*   [BIND 9 Administrator Reference Manual](https://www.isc.org/downloads/bind/doc/)
*   [BIND 9 DNS Administration Reference Book](http://www.reedmedia.net/books/bind-dns/)
*   [DNS and BIND by Cricket Liu and Paul Albitz](http://shop.oreilly.com/product/9780596100575.do)
*   [Pro DNS and BIND](http://www.netwidget.net/books/apress/dns/intro.html)
*   [Internet Systems Consortium, Inc. (ISC)](http://www.isc.org/)
*   [DNS Glossary](http://www.menandmice.com/knowledgehub/dnsglossary)
*   [Archived mailing list discussion on BIND's future](https://lists.archlinux.org/pipermail/arch-dev-public/2013-March/024588.html)