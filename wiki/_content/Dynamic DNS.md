# Dynamic DNS

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Dynamic DNS** or **DDNS** is a method of updating, in real time, a [DNS](/index.php/DNS "DNS") to point to a changing IP address on the Internet. This is used to provide a persistent domain name for a resource that may change location on the network.

## Contents

*   [1 Dynamic DNS Providers](#Dynamic_DNS_Providers)
    *   [1.1 Afraid and Now-IP](#Afraid_and_Now-IP)
    *   [1.2 DNSdynamic](#DNSdynamic)
    *   [1.3 duiadns](#duiadns)
    *   [1.4 No-IP](#No-IP)
    *   [1.5 System-NS](#System-NS)
    *   [1.6 DuckDNS](#DuckDNS)
    *   [1.7 FreeDns.io](#FreeDns.io)
    *   [1.8 ChangeIP](#ChangeIP)
*   [2 Tools Supporting Multiple Dynamic DNS Services](#Tools_Supporting_Multiple_Dynamic_DNS_Services)
    *   [2.1 Router](#Router)
    *   [2.2 ddclient](#ddclient)
        *   [2.2.1 Starting ddclient after networking is up](#Starting_ddclient_after_networking_is_up)
    *   [2.3 Other](#Other)

## Dynamic DNS Providers

There are many different DDNS providers and some are supported by official or third-party tools. A partial list is given below. Many of these providers are also supported by the generic tools listed in the [section](#Tools_Supporting_Multiple_Dynamic_DNS_Services) below.

### Afraid and Now-IP

[FreeDNS.afraid.org](http://FreeDNS.afraid.org) and [Now-IP.com](https://now-ip.com) are free services which are easy and uncomplicated to set up.

There are several options to enable automatic DDNS updating for these providers:

afraid-dyndns

The package [afraid-dyndns-uv](https://aur.archlinux.org/packages/afraid-dyndns-uv/)<sup><small>AUR</small></sup> is available in the [AUR](/index.php/AUR "AUR").

petrified

The package [petrified](https://aur.archlinux.org/packages/petrified/)<sup><small>AUR</small></sup> is available in the [AUR](/index.php/AUR "AUR").

cron

A cron job to update the service can be configured as follows:

*   Goto your [Dynamic DNS](http://freedns.afraid.org/dynamic/index.php) page at freedns.afraid.org
*   Add A record and select your prefered domain name
*   Press **quick cron example** behind the desired A record
*   Test one of the examples:

```
curl [http://freedns.afraid.org/dynamic/update.php?Ukd](http://freedns.afraid.org/dynamic/update.php?Ukd)...

```

*   Use `crontab -e` to insert the new cronjob:

```
*/6 * * * * sleep 20 ; curl [http://freedns.afraid.org/dynamic/update.php?Ukd...Dk2](http://freedns.afraid.org/dynamic/update.php?Ukd...Dk2) > /tmp/freedns_my_ddns_record.com.log 2>&1 &

```

netctl

To add the record of your IP to freedns.afraid.org along with a network connection through the use with [Netctl](/index.php/Netctl "Netctl"). You can append the following line to your netctl profile.

 `ExecUpPost='curl -ks http://freedns.afraid.org/dynamic/update.php?ZRRJZ...................bzo4Njc1M4DA'` 

### DNSdynamic

[DNSdynamic](http://www.dnsdynamic.org/) "will always be absolutely free" and works with [ddclient](https://www.archlinux.org/packages/?name=ddclient). [This page](https://www.dnsdynamic.org/api.php) has information on how to configure [ddclient](https://www.archlinux.org/packages/?name=ddclient).

### duiadns

[Duiadns.org](https://www.duiadns.net). The package [duiadns](https://aur.archlinux.org/packages/duiadns/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/duiadns)]</sup> is available in the [AUR](/index.php/AUR "AUR").

### No-IP

[noip](https://aur.archlinux.org/packages/noip/)<sup><small>AUR</small></sup> is a dynamic DNS client updater for [no-ip.com](http://www.noip.com) services.

Configure the client by running

```
# noip2 -C

```

See `noip2 -h` for more options. [Start](/index.php/Start "Start") `noip2.service` to run the host updater and [enable](/index.php/Enable "Enable") it to run automatically at boot.

### System-NS

[System-NS](http://system-ns.com/) free DNS service. It can be configured to update using a cron script through the following steps. Make a directory and create a script file within it:

```
$ cd ~
$ mkdir systemns
$ cd systemns
$ vi systemns.sh

```

Put the following text in systemns.sh. You should change the domain and token parameters.

```
#!/bin/bash
wget -q -O- --post-data "type=dynamic&domain=mydomain.system-ns.net&command=set&token=880078764367979fe765c0fa3f4efff1" [http://system-ns.com/api](http://system-ns.com/api) | grep -v '"code":0' | awk '{print d, $0}' "d=$(date)" >> ~/systemns/systemns.log

```

Make the systemns.sh file executable.

```
$ chmod +x systemns.sh

```

Open crontab.

```
$ crontab -e

```

Put this text in the crontab (run every 5 minutes)

```
*/5 * * * * ~/systemns/systemns.sh

```

### DuckDNS

[duckdns](https://aur.archlinux.org/packages/duckdns/)<sup><small>AUR</small></sup> is a dynamic DNS client updater for [DuckDNS.org](https://duckdns.org) services. After installation go to your `/etc/duckdns.d` and copy/edit the `default.cfg`. Just enter the hostname and token you received from DuckDNS. Any file ending on `.cfg` will be read by the script and used to contact the DuckDNS services. The script also writes debug messages to logger.

Do not forget to [enable](/index.php/Enable "Enable") the duckdns.timer so your IP will be updated every 5 minutes.

### FreeDns.io

[FreeDns.io](https://freedns.io) is a dynamic DNS provider. They provide free A and AAAA DNS records for free, and optionally you can apply for a Premium account which includes CNAME, TXT and MX records.

They provide an API which can be called from a script written in any of the most used programming languages, including PHP, Python and Ruby. Samples might be reached [here](https://github.com/nkovacne/freedns-samples). Once chosen and copied to the machine which will update the host, a cron-job should be created in this form:

```
*/5 * * * * ~/update-my-freedns-host

```

(Assuming the ~/update-my-freedns-host script has execution permissions)

This provider allows up to 60 requests per hour, so even a cron-job run every minute is ok, because if your IP doesn’t change in two consecutive requests, it’s not considered a “hit”.

### ChangeIP

[ChangeIP.com](https://changeip.com) provides free A, AAAA, CNAME, MX, URL DNS records, you can also apply for free codomain like {ic|git.example.changeip.com} and many more.

They provide easy [api](http://www.changeip.com/accounts/knowledgebase.php?action=displayarticle&id=34) such as {ic|curl -u 'user:pass' [https://nic.ChangeIP.com/nic/update}](https://nic.ChangeIP.com/nic/update}).

## Tools Supporting Multiple Dynamic DNS Services

### Router

Many routers have built in DDNS services but can be limited in the providers which they update. If your router supports a service, or you are willing to pay or donate for a service, it is recommended to use the router functionality, as it is directly connected with your internet connection and is often more reliable than a service running on a machine.

### ddclient

The package [ddclient](https://www.archlinux.org/packages/?name=ddclient) is available in the [community](/index.php/Community "Community") repository. It includes [systemd](/index.php/Systemd "Systemd") support and can be used with a range of Dynamic DNS providers.

To use the service, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `ddclient.service` unit after filling in the configuration file `/etc/ddclient/ddclient.conf`. An example which updates an Afraid.org account looks like this:

 `/etc/ddclient/ddclient.conf` 

```
daemon=600
cache=/tmp/ddclient.cache
syslog=yes
pid=/var/run/ddclient.pid
use=web, web=checkip.dyndns.com/, web-skip='IP Address'

ssl=yes

## Configuration variables applicable to the 'freedns' protocol are:
#  protocol=freedns             ##
#  server=fqdn.of.service       ## defaults to freedns.afraid.org
#  login=service-login          ## login name and password registered with the service
#  password=service-password    ##
#  fully.qualified.host         ## the host registered with the service.
#
protocol=freedns
login=my-freedns.afraid.org-login
password=my-freedns.afraid.org-password
myhost1.afraid.org
myhost2.afraid.org
```

#### Starting ddclient after networking is up

In some installs, it appears that enabling the `ddclient.service` unit will cause it to start the ddclient process before networking is properly up. The ddclient process is then unable to properly lookup the domain names required and does not retry the lookup later, making the process useless.

Set ddclient to start when the `network-online.target` is reached by editing `ddclient.service` with `systemctl edit --full ddclient.service` and adding or modifying the emphasized lines:

 `/etc/systemd/system/ddclient.service` 

```
[Unit]
Description=Dynamic DNS Update Client
After=network.target
**PartOf=network-online.target**

[Service]
Type=forking
PIDFile=/var/run/ddclient.pid
ExecStart=/usr/bin/ddclient

[Install]
**WantedBy=network-online.target**
```

**Note:**

*   A full replacement must be created, because a drop-in override cannot modify the `[Install]` section of a unit file. Make sure to disable and reenable the `ddclient.service` so that the symlink is put into the right place.
*   It may be necessary to configure the network manager to activate `network-online.target` (for [netctl](/index.php/Netctl "Netctl") see [netctl#Activate network-online.target](/index.php/Netctl#Activate_network-online.target "Netctl")).

### Other

There are other DDNS updaters that work with several providers including:

inadyn-mt

In the [AUR](/index.php/AUR "AUR") as [inadyn-mt](https://aur.archlinux.org/packages/inadyn-mt/)<sup><small>AUR</small></sup>. Supports a large number of providers as [listed here](http://sourceforge.net/projects/inadyn-mt).

ndyndns

In the [AUR](/index.php/AUR "AUR") as [ndyndns](https://aur.archlinux.org/packages/ndyndns/)<sup><small>AUR</small></sup>. Update client for the dynamic DNS services from DynDNS and Namecheap.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dynamic_DNS&oldid=414110](https://wiki.archlinux.org/index.php?title=Dynamic_DNS&oldid=414110)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Domain Name System](/index.php/Category:Domain_Name_System "Category:Domain Name System")