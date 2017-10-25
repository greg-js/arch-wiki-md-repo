Related articles

*   [DNSCrypt](/index.php/DNSCrypt "DNSCrypt")
*   [dnsmasq](/index.php/Dnsmasq "Dnsmasq")
*   [Pdnsd](/index.php/Pdnsd "Pdnsd")
*   [Unbound](/index.php/Unbound "Unbound")
*   [PowerDNS](/index.php/PowerDNS "PowerDNS")

[BIND](https://www.isc.org/downloads/bind/) is the most widely used Domain Name System (DNS) server.

**Note:** The organization developing BIND is serving security notices to paying customers up to four days before Linux distributions or the general public.[[1]](https://kb.isc.org/article/AA-00861/0/ISC-Software-Defect-and-Security-Vulnerability-Disclosure-Policy.html)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Restrict access to localhost](#Restrict_access_to_localhost)
    *   [2.2 Set up DNS forwarding](#Set_up_DNS_forwarding)
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

[Install](/index.php/Install "Install") the [bind](https://www.archlinux.org/packages/?name=bind) package.

To use BIND as the system's DNS server prepend `nameserver 127.0.0.1` to [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

[Start/enable](/index.php/Start/enable "Start/enable") the `named.service` systemd unit.

## Configuration

BIND is configured in `/etc/named.conf`. The available options are documented in the `named.conf` man page.

[Reload](/index.php/Reload "Reload") the `named.service` unit to apply configuration changes.

### Restrict access to localhost

To only allow connections from localhost add the following line to the options section in `/etc/named.conf`:

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

This is a simple tutorial in howto setup a simple home network DNS-server with bind. In our example we use "domain.tld" as our domain.

For a more elaborate example see [Two-in-one DNS server with BIND9](http://www.howtoforge.com/two_in_one_dns_bind9_views).

Another guide at [Linux Home Server HOWTO - Domain name system (BIND): Adding your domain](http://www.brennan.id.au/08-Domain_Name_System_BIND.html#yourdomain) will show you how to set up internal network name resolution in no time; short, on-point and very informative.

### 1\. Creating a zonefile

Create `/var/named/domain.tld.zone`.

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

[Reload](/index.php/Reload "Reload") the `named.service` unit to apply the configuration change.

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

*   [http://www.dnssec.net/practical-documents](http://www.dnssec.net/practical-documents)
    *   [http://www.cymru.com/Documents/secure-bind-template.html](http://www.cymru.com/Documents/secure-bind-template.html) **(configuration template!)**
    *   [http://www.bind9.net/manuals](http://www.bind9.net/manuals)
    *   [http://www.bind9.net/BIND-FAQ](http://www.bind9.net/BIND-FAQ)
*   [http://blog.techscrawl.com/2009/01/13/enabling-dnssec-on-bind/](http://blog.techscrawl.com/2009/01/13/enabling-dnssec-on-bind/)
*   Or use an external mechanisms such as OpenDNSSEC (fully-automatic key rollover)

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

Stop the old named service

```
 systemctl stop named.service

```

Disable the old named service

```
 systemctl disable named.service

```

Enable the new chroot named service

```
 systemctl enable named-chroot.service

```

Now reload systemd

```
 systemctl daemon-reload

```

Then [start](/index.php/Start "Start") `named-chroot.service` using

```
 systemctl start named-chroot.service

```

Check the service status

```
 systemctl status named-chroot.service

```

If you see any errors, reboot your system. Then check again and it should then be loading the **named-chroot.service** automatically and not **named.service**.

You can check all enabled services using

```
 sudo systemctl list-unit-files | grep enabled

```

## See also

*   [BIND 9 Administrator Reference Manual](https://www.isc.org/downloads/bind/doc/)
*   [BIND 9 DNS Administration Reference Book](http://www.reedmedia.net/books/bind-dns/)
*   [DNS and BIND by Cricket Liu and Paul Albitz](http://shop.oreilly.com/product/9780596100575.do)
*   [Pro DNS and BIND](http://www.netwidget.net/books/apress/dns/intro.html)
*   [Internet Systems Consortium, Inc. (ISC)](http://www.isc.org/)
*   [DNS Glossary](http://www.menandmice.com/knowledgehub/dnsglossary)
*   [Archived mailing list discussion on BIND's future](https://lists.archlinux.org/pipermail/arch-dev-public/2013-March/024588.html)