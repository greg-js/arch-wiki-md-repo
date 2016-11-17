**Dynamic DNS** or **DDNS** is a method of updating, in real time, a [DNS](/index.php/DNS "DNS") to point to a changing IP address on the Internet. This is used to provide a persistent domain name for a resource lacking a static IP. To use DDNS, you need to both sign up with a DDNS provider and set up an automatic update tool that will notify the provider when your IP address changes.

## Contents

*   [1 Update tools](#Update_tools)
    *   [1.1 Router](#Router)
    *   [1.2 ddclient](#ddclient)
        *   [1.2.1 Starting ddclient after networking is up](#Starting_ddclient_after_networking_is_up)
    *   [1.3 Other tools](#Other_tools)
*   [2 Other providers](#Other_providers)
    *   [2.1 duiadns](#duiadns)
    *   [2.2 FreeDns.io](#FreeDns.io)
    *   [2.3 Now-DNS](#Now-DNS)
    *   [2.4 System-NS](#System-NS)

## Update tools

### Router

If the device needing DDNS sits behind a router, you should first check if the router itself can update any DDNS services. Although the selection of services may be limited, there are several advantages to using the router: it will probably be easier to set up, will require little to no maintenance, and will have no downtime (if the router is down you won't have Internet anyway).

### ddclient

[ddclient](https://www.archlinux.org/packages/?name=ddclient) is compatible with many DDNS services and is the recommended tool for updating DDNS if your [router](#Router) is not an option. It includes [systemd](/index.php/Systemd "Systemd") support.

After installing, edit the default config `/etc/ddclient/ddclient.conf` to set up your DDNS provider (it includes many examples). Then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `ddclient.service`.

Some of the compatible services are listed below, but you can also check the [examples](http://sourceforge.net/p/ddclient/code/HEAD/tree/trunk/sample-etc_ddclient.conf) and [protocols](http://sourceforge.net/p/ddclient/wiki/protocols/) for more.

<caption>ddclient compatible services</caption>
| Service | Cost | Available Records | Hostname Limit | Config Notes | Alternative tools |
| [Now-DNS](http://now-dns.com/) | Free | A, AAAA | unlimited | Use protocol `dyndns2`, server `now-dns.com/update` |
| [ChangeIP](http://www.changeip.com/) | Free or paid | A, AAAA, CNAME, MX, codomains | 7 free |
| [DNSdynamic](http://www.dnsdynamic.org/) | Free | [example](https://www.dnsdynamic.org/api.php) |
| [Duck DNS](https://www.duckdns.org/) | Free and open source | [duckdns](https://aur.archlinux.org/packages/duckdns/) |
| [FreeDNS](http://freedns.afraid.org/) | Free or paid | CNAME, A, AAAA, MX, NS, TXT, LOC, RP, HINFO, SRV | 5 free | [example](http://freedns.afraid.org/scripts/freedns.clients.php) | [afraid-dyndns-uv](https://aur.archlinux.org/packages/afraid-dyndns-uv/), [petrified](https://aur.archlinux.org/packages/petrified/) |
| [No-IP](http://www.noip.com/) | Free or paid | 3 free, 25+ paid | Use protocol `dyndns2`, server `dynupdate.no-ip.com` | [noip](https://aur.archlinux.org/packages/noip/) |
| [nsupdate.info](https://www.nsupdate.info/) | Free and open source | A, AAAA | Use protocol `dyndns2` | [inadyn-fork](https://aur.archlinux.org/packages/inadyn-fork/) |

#### Starting ddclient after networking is up

If you find that ddclient is unable to update your IP properly, it may be that the ddclient process is starting before networking is up. To fix it, you can edit the unit file to depend on `network-online.target` (added lines in bold):

 `# systemctl edit --full ddclient.service` 
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

### Other tools

Other DDNS updaters that work with several providers are [inadyn-mt](https://aur.archlinux.org/packages/inadyn-mt/) ([supported providers](http://sourceforge.net/projects/inadyn-mt)) and [ndyndns](https://aur.archlinux.org/packages/ndyndns/) (supports DynDNS and Namecheap).

## Other providers

The following DDNS providers are not compatible with [ddclient](#ddclient) so updating your IP with them may require a special tool or some custom scripting. Remember that if the service allows you to update your IP using the command line, you can automate the process using tools such as [cron](/index.php/Cron "Cron") or [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

### duiadns

[Duiadns.org](https://www.duiadns.net) is a free service which can be automated with [duiadns](https://aur.archlinux.org/packages/duiadns/).

### FreeDns.io

[FreeDns.io](https://freedns.io) provides free A and AAAA DNS records and CNAME, TXT and MX records with a premium membership. You can update your IP using their HTTP API (with a 60 requests-per-hour limit). They provide [several example scripts](https://github.com/nkovacne/freedns-samples).

### Now-DNS

[Now-DNS.com](https://now-dns.com) is a free service which is easy and uncomplicated to set up.

### System-NS

[System-NS](http://system-ns.com/) is a free service which can be updated via the command line. See [the official documentation](https://system-ns.com/services/dynamic).