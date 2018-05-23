This article lists [domain name system](https://en.wikipedia.org/wiki/Domain_name_system "wikipedia:Domain name system") (DNS) services that may replace an internet service provider's DNS service. To use one of these servers, see [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution").

## Contents

*   [1 Cisco Umbrella (formerly OpenDNS)](#Cisco_Umbrella_.28formerly_OpenDNS.29)
*   [2 Cloudflare](#Cloudflare)
*   [3 Comodo](#Comodo)
*   [4 DNS.WATCH](#DNS.WATCH)
*   [5 Google](#Google)
*   [6 OpenNIC](#OpenNIC)
*   [7 Quad9](#Quad9)
*   [8 UncensoredDNS](#UncensoredDNS)
*   [9 Yandex](#Yandex)

## Cisco Umbrella (formerly OpenDNS)

[OpenDNS](https://www.opendns.com/home-internet-security/) provided free alternative nameservers, was [bought by Cisco in Nov. 2016](https://umbrella.cisco.com/products/features/opendns-cisco-umbrella) and continues to offer OpenDNS as end-user product of its "Umbrella" product suite with focus on Security Enforcement, Security Intelligence and Web Filtering. The old nameservers [still work](https://www.opendns.com/setupguide/) but are [pre-configured to block adult content](https://www.opendns.com/home-internet-security/):

IPv4 nameservers

```
208.67.222.222
208.67.220.220

```

IPv6 nameservers

```
2620:0:ccc::2
2620:0:ccd::2

```

## Cloudflare

[Cloudflare](https://1.1.1.1/) provides a service committed to never writing the querying IP addresses to disk and wiping all logs within 24 hours, with the exception of providing data to APNIC labs for research purposes. APNIC and Cloudfare committed to treat all data with high privacy standards in their [research agreement statement](https://labs.apnic.net/?p=1127).

IPv4 nameservers:

```
1.1.1.1
1.0.0.1

```

IPv6 nameservers:

```
2606:4700:4700::1111
2606:4700:4700::1001

```

## Comodo

[Comodo](http://securedns.dnsbycomodo.com/) provides another IPv4 set, with optional (non-free) web-filtering. Implied in this feature is that the service hijacks the queries.

```
8.26.56.26 
8.20.247.20

```

## DNS.WATCH

[DNS.WATCH](https://dns.watch/) focuses on neutrality and security and provides two servers located in Germany with no logging and with DNSSEC enabled. Note they welcome commercial sponsorship.

```
84.200.69.80    # resolver1.dns.watch 
84.200.70.40    # resolver2.dns.watch

```

## Google

[Google's nameservers](https://developers.google.com/speed/public-dns/) can be used as an alternative:

IPv4 nameservers

```
8.8.8.8
8.8.4.4

```

IPv6 nameservers

```
2001:4860:4860::8888
2001:4860:4860::8844

```

## OpenNIC

[OpenNIC](http://www.opennicproject.org/) provides free uncensored nameservers located in multiple countries. The full list of public servers is available at [servers.opennic.org](https://servers.opennic.org/) and a shortlist of nearest nameservers for optimal performance is generated on their [home page](https://www.opennic.org/).

To retrieve a list of nearest nameservers, an [API](https://wiki.opennic.org/api/geoip) is also available and returns, based on the [URL parameters](https://wiki.opennic.org/api/geoip#url_parameters) provided, a list of nameservers in the desired format. For example to get the 200 nearest IPv4 servers, one can use [https://api.opennicproject.org/geoip/?list&ipv=4&res=200&adm=0&bl&wl](https://api.opennicproject.org/geoip/?list&ipv=4&res=200&adm=0&bl&wl).

Alternatively, the anycast servers below can be used; while reliable their latency [fluctuates a lot](https://wiki.opennic.org/opennic/dont_anycast).

IPv4 nameservers (Worldwide Anycast)

```
185.121.177.177
185.121.177.53

```

IPv6 nameservers (Worldwide Anycast)

```
2a05:dfc7:5::53
2a05:dfc7:5::5353

```

**Note:**

*   The use of OpenNIC DNS servers will allow host name resolution in the traditional Top-Level Domain (TLD) registries, but also in OpenNIC or afiliated operated namespaces: *.o*, *.libre*, *.dyn*...
*   The tool **opennic-up** — automates the renewal of the DNS servers with the most responsive OpenNIC servers

	[https://github.com/kewlfft/opennic-up](https://github.com/kewlfft/opennic-up) || [opennic-up](https://aur.archlinux.org/packages/opennic-up/)

## Quad9

[Quad9](https://quad9.net/#/) is a free DNS service founded by [IBM](https://www.ibm.com/security), [Packet Clearing House](https://www.pch.net) and [Global Cyber Alliance](https://www.globalcyberalliance.org); its primary unique feature is a blocklist which avoids resolving known malicious domains. The addresses below are worldwide anycast.

IPv4 nameservers

```
9.9.9.9    ## "secure", with blocklist and DNSSEC
9.9.9.10    ## no blocklist, no DNSSEC

```

IPv6 nameservers

```
2620:fe::fe    ## "secure", with blocklist and DNSSEC
2620:fe::10    ## no blocklist, no DNSSEC

```

## UncensoredDNS

[UncensoredDNS](http://censurfridns.dk) is a free uncensored DNS service. It is run by a private individual and consists in one anycast served by multiple servers and one unicast node hosted in Denmark.

IPv4 nameservers

```
91.239.100.100    ## anycast.censurfridns.dk
89.233.43.71      ## unicast.censurfridns.dk

```

IPv6 nameservers

```
2001:67c:28a4::   ## anycast.censurfridns.dk
2a01:3a0:53:53::  ## unicast.censurfridns.dk

```

**Note:** Its servers listen to port 5353 as well as the standard port 53\. This can be used in case your ISP hijacks port 53.

## Yandex

[Yandex.DNS](https://dns.yandex.com/advanced/) has servers in Russia, Eastern and Western Europe and has three options, *Basic*, *Safe* and *Family*:

Basic Yandex.DNS - Quick and reliable DNS

```
77.88.8.8              # Preferred IPv4 DNS
77.88.8.1              # Alternate IPv4 DNS

2a02:6b8::feed:0ff     # Preferred IPv6 DNS
2a02:6b8:0:1::feed:0ff # Alternate IPv6 DNS

```

Safe Yandex.DNS - Protection from virus and fraudulent content

```
77.88.8.88             # Preferred IPv4 DNS
77.88.8.2              # Alternate IPv4 DNS

2a02:6b8::feed:bad     # Preferred IPv6 DNS
2a02:6b8:0:1::feed:bad # Alternate IPv6 DNS

```

Family Yandex.DNS - Without adult content

```
77.88.8.7              # Preferred IPv4 DNS
77.88.8.3              # Alternate IPv4 DNS

2a02:6b8::feed:a11     # Preferred IPv6 DNS
2a02:6b8:0:1::feed:a11 # Alternate IPv6 DNS

```

Yandex.DNS' speed is the same in the three modes. In *Basic* mode, there is no traffic filtering. In *Safe* mode, protection from infected and fraudulent sites is provided. *Family* mode enables protection from dangerous sites and blocks sites with adult content.