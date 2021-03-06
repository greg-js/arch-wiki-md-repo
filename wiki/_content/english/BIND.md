Related articles

*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")

[BIND](https://www.isc.org/downloads/bind/) (or named) is the most widely used Domain Name System (DNS) server.

**Note:** The organization developing BIND is serving security notices to paying customers up to four days before Linux distributions or the general public.[[1]](https://kb.isc.org/article/AA-00861/0/ISC-Software-Defect-and-Security-Vulnerability-Disclosure-Policy.html)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Restrict access to localhost](#Restrict_access_to_localhost)
    *   [2.2 Set up DNS forwarding](#Set_up_DNS_forwarding)
*   [3 A configuration template for running a domain](#A_configuration_template_for_running_a_domain)
    *   [3.1 Creating a zonefile](#Creating_a_zonefile)
    *   [3.2 Configuring master server](#Configuring_master_server)
*   [4 Allow recursion](#Allow_recursion)
*   [5 Configuring BIND to serve DNSSEC signed zones](#Configuring_BIND_to_serve_DNSSEC_signed_zones)
    *   [5.1 See also](#See_also)
*   [6 Automatically listen on new interfaces](#Automatically_listen_on_new_interfaces)
*   [7 Running BIND in a chrooted environment](#Running_BIND_in_a_chrooted_environment)
    *   [7.1 Creating the Jail House](#Creating_the_Jail_House)
    *   [7.2 Service File](#Service_File)
*   [8 See also](#See_also_2)

## Installation

[Install](/index.php/Install "Install") the [bind](https://www.archlinux.org/packages/?name=bind) package.

[Start/enable](/index.php/Start/enable "Start/enable") the `named.service` systemd unit.

To use the DNS server locally, use the `127.0.0.1` nameserver (meaning clients like firefox resolve via 127.0.0.1), see [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution"). This will however require you to [#Allow recursion](#Allow_recursion) while a firewall might block outside queries to your local named.

## Configuration

BIND is configured in `/etc/named.conf`. The available options are documented in [named.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/named.conf.5).

[Reload](/index.php/Reload "Reload") the `named.service` unit to apply configuration changes.

### Restrict access to localhost

BIND by defaults listens on port 53 of all interfaces and IP addresses. To only allow connections from localhost add the following line to the options section in `/etc/named.conf`:

```
listen-on { 127.0.0.1; };

```

### Set up DNS forwarding

To make BIND forward DNS queries to another DNS server add the forwarders clause to the options section.

Example to make BIND forward to the Google DNS servers:

```
forwarders { 8.8.8.8; 8.8.4.4; };

```

## A configuration template for running a domain

Following is a simple home nameserver being set up, using *domain.tld* as the domain being served world-wide like this wiki's *archlinux.org* domain is.

A more elaborate example is [DNS server with BIND9](http://www.howtoforge.com/two_in_one_dns_bind9_views), while [this shows](http://www.brennan.id.au/08-Domain_Name_System_BIND.html#yourdomain) how to set up internal network name resolution.

### Creating a zonefile

Create `/var/named/domain.tld.zone`.

```
$TTL 7200
; domain.tld
@       IN      SOA     ns01.domain.tld. postmaster.domain.tld. (
                                        2018111111 ; Serial
                                        28800      ; Refresh
                                        1800       ; Retry
                                        604800     ; Expire - 1 week
                                        86400 )    ; Minimum
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

$TTL defines the default time-to-live in seconds for all record types. Here it is 2 hours.

Serial must be **incremented** manually before restarting named every time you change a resource record for the zone. Otherwise slaves will not re-transfer the zone: they only do it if the serial is **greater** than that of the last time they transferred the zone.

### Configuring master server

Add your zone to `/etc/named.conf`:

```
zone "domain.tld" IN {
        type master;
        file "domain.tld.zone";
        allow-update { none; };
        notify no;
};

```

[Reload](/index.php/Reload "Reload") the `named.service` unit to apply the configuration change.

## Allow recursion

If you are running your own DNS server, you might as well use it for all DNS lookups, or even locally serve the root-zone yourself following [RFC:7706](https://tools.ietf.org/html/rfc7706 "rfc:7706"). The former will require the ability to do *recursive* lookups. In order to prevent [DNS Amplification Attacks](https://www.us-cert.gov/ncas/alerts/TA13-088A), recursion is turned off by default for most resolvers. The default Arch `/etc/named.conf` file allows for recursion only on the loopback interface:

```
allow-recursion { 127.0.0.1; };

```

If you want to provide name service for your local network; e.g. 192.168.0.0/24, you must add the appropriate range of IP addresses to `/etc/named.conf`:

```
allow-recursion { 192.168.0.0/24; 127.0.0.1; };

```

## Configuring BIND to serve DNSSEC signed zones

To enable DNSSEC support you need to add "dnssec-enable yes;" to /etc/named.conf "options" block. Do not forget to check that "edns" is not disabled.

On master DNS server:

*   generate KSK and ZSK keys:

```
 $ dnssec-keygen -a NSEC3RSASHA1 -b 2048 -n ZONE example.com
 $ dnssec-keygen -f KSK -a NSEC3RSASHA1 -b 4096 -n ZONE example.com

```

*   change zone configuration:

```
 zone "example.com" {
       type master;
       allow-transfer { ... };
       auto-dnssec maintain;
       inline-signing yes;
       key-directory "master/";
       file "master/example.com.zone";
 };

```

Now bind will sign zone automatically. (This example assumes that all required files are in /var/named/master/)

Then you should pass DS records (from dsset-example.com. file) to parent zone owner probably using your registrar website. It glues parent zone with your KSK.

KSK (and corresponding DS records) should be changed rarely because of it needs manual intervention, ZSK can be changed more often because of this key is usually shorter to be faster in signature checking.

You can schedule old ZSK key expiration and generate new one using:

```
 $ dnssec-settime -I +172800 -D +345600 Kexample.com.+000+111111.key
 $ dnssec-keygen -S Kexample.com.+000+111111.key -i 152800

```

Bind should automatically use new ZSK key at appropriate time.

### See also

*   [DNSSEC](http://www.dnssec.net/practical-documents)
*   [a BIND configuration template](http://www.cymru.com/Documents/secure-bind-template.html)
*   [man bind](http://www.bind9.net/manuals)
*   [bind FAQ](http://www.bind9.net/BIND-FAQ)

There are external mechanisms such as OpenDNSSEC with fully-automatic key rollover available.

## Automatically listen on new interfaces

By default bind scan for new interfaces and stop listening on interfaces which no longer exist every hour. You can tune this value by adding :

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
 cp -av /usr/lib/engines-1.1/* /srv/named/usr/lib/engines/
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

Now, restart the systemd service.

## See also

*   [BIND 9 Administrator Reference Manual](https://www.isc.org/downloads/bind/doc/)
*   [BIND 9 DNS Administration Reference Book](http://www.reedmedia.net/books/bind-dns/)
*   [DNS and BIND by Liu and Albitz](http://shop.oreilly.com/product/9780596100575.do)
*   [Pro DNS and BIND](http://www.netwidget.net/books/apress/dns/intro.html) with [abbreviated version online](http://www.zytrax.com/books/dns/)
*   [Internet Systems Consortium, Inc. (ISC)](http://www.isc.org/)
*   [DNS Glossary](https://cira.ca/domain-name-system-dns-glossary)
*   [Archived mailing list discussion on BIND's future](https://lists.archlinux.org/pipermail/arch-dev-public/2013-March/024588.html)
*   [root zone transfer made simple - serve root@home](https://www.heise.de/netze/rfc/rfcs/rfc7706.shtml#page-9) copy the /etc/named.conf , restart BIND & enjoy!