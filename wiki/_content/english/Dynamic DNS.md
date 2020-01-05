According to [Wikipedia](https://en.wikipedia.org/wiki/Dynamic_DNS "wikipedia:Dynamic DNS"):

	**Dynamic DNS** (**DDNS** or **DynDNS**) is a method of automatically updating a [name server](https://en.wikipedia.org/wiki/name_server "wikipedia:name server") in the [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") (DNS), often in real time, with the active DDNS configuration of its configured hostnames, addresses or other information.

	The term is used to describe two different concepts. The first is "dynamic DNS updating" which refers to systems that are used to update traditional DNS records without manual editing. These mechanisms are explained in [RFC 2136](https://tools.ietf.org/html/rfc2136 "rfc:2136"), and use the [TSIG](https://en.wikipedia.org/wiki/TSIG "wikipedia:TSIG") mechanism to provide security. The second kind of dynamic DNS permits lightweight and immediate updates often using an update client, which do not use the RFC2136 standard for updating DNS records. These clients provide a persistent addressing method for devices that change their location, configuration or [IP address](https://en.wikipedia.org/wiki/IP_address "wikipedia:IP address") frequently.

For RFC2136 there is [nsupdate(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsupdate.1) from [bind-tools](https://www.archlinux.org/packages/?name=bind-tools). For dynamic DNS services there are several packages available, see [#Update clients](#Update_clients).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Router](#Router)
*   [2 Update clients](#Update_clients)
    *   [2.1 Multi-service clients](#Multi-service_clients)
    *   [2.2 Single-service clients](#Single-service_clients)
    *   [2.3 ddclient](#ddclient)
        *   [2.3.1 Use an external website to determine IP address](#Use_an_external_website_to_determine_IP_address)
        *   [2.3.2 Starting ddclient after networking is up](#Starting_ddclient_after_networking_is_up)
*   [3 Other providers](#Other_providers)

## Router

If the device needing DDNS sits behind a router, you should first check if the router itself can update any DDNS services. Although the selection of services may be limited, there are several advantages to using the router: it will probably be easier to set up, will require little to no maintenance, and will have no downtime (if the router is down you will not have Internet anyway).

## Update clients

Note that some dynamic DNS providers do not require a dedicated client and can be updated with [curl](https://www.archlinux.org/packages/?name=curl).

### Multi-service clients

*   **[ddclient](#ddclient)** — Update dynamic DNS entries for accounts on many dynamic DNS services.

	[https://github.com/ddclient/ddclient](https://github.com/ddclient/ddclient) || [ddclient](https://www.archlinux.org/packages/?name=ddclient)

*   **ddnsc** — A simple & lightweight client written in python.

	[https://github.com/shyaminayesh/ddnsc](https://github.com/shyaminayesh/ddnsc) || [ddnsc](https://aur.archlinux.org/packages/ddnsc/)

*   **inadyn-fork** — Dynamic DNS client with SSL/TLS support.

	[http://troglobit.com/inadyn.html](http://troglobit.com/inadyn.html) || [inadyn-fork](https://aur.archlinux.org/packages/inadyn-fork/), [inadyn-fork-git](https://aur.archlinux.org/packages/inadyn-fork-git/)

*   **inadyn-mt** — A simple dynamic DNS client based on inadyn.

	[http://inadyn-mt.sourceforge.net/](http://inadyn-mt.sourceforge.net/) || [inadyn-mt](https://aur.archlinux.org/packages/inadyn-mt/)

*   **ndyndns** — Supports DynDNS and Namecheap.

	[https://github.com/niklata/ndyndns](https://github.com/niklata/ndyndns) || [ndyndns](https://aur.archlinux.org/packages/ndyndns/)

### Single-service clients

*   **duckdns** — Update your DuckDNS.org entries from your computer with systemd.

	[https://www.duckdns.org/](https://www.duckdns.org/) || [duckdns](https://aur.archlinux.org/packages/duckdns/), [duckdns-ipv6](https://aur.archlinux.org/packages/duckdns-ipv6/)

*   **noip** — Dynamic DNS Client Updater for no-ip.com services.

	[http://www.no-ip.com/downloads.php?page=linux](http://www.no-ip.com/downloads.php?page=linux) || [noip](https://aur.archlinux.org/packages/noip/)

*   **petrified** — Bash client to update dynamic DNS at freedns.afraid.org.

	[https://gitlab.com/troyengel/petrified](https://gitlab.com/troyengel/petrified) || [petrified](https://aur.archlinux.org/packages/petrified/)

### ddclient

[ddclient](https://www.archlinux.org/packages/?name=ddclient) is compatible with many DDNS services and is the recommended tool for updating DDNS if your [router](#Router) is not an option. It includes [systemd](/index.php/Systemd "Systemd") support.

After installing, edit the default config `/etc/ddclient/ddclient.conf` to set up your DDNS provider (it includes many examples). Then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `ddclient.service`.

The configuration can be tested by running `ddclient` with the `-noquiet` and `-debug` options:

```
# ddclient -daemon=0 -noquiet -debug

```

Some of the compatible services are listed below, but you can also check the [examples](http://sourceforge.net/p/ddclient/code/HEAD/tree/trunk/sample-etc_ddclient.conf) and [protocols](http://sourceforge.net/p/ddclient/wiki/protocols/) for more.

<caption>ddclient compatible services</caption>
| Service | Config Notes |
| [Now-DNS](http://now-dns.com/) | [example](https://now-dns.com/client/ddclient.conf) |
| [ChangeIP](http://www.changeip.com/) | [example](https://sourceforge.net/p/ddclient/wiki/protocols/#changeip) |
| [Duck DNS](https://www.duckdns.org/) | [example](https://sourceforge.net/p/ddclient/wiki/protocols/#duckdns) |
| [FreeDNS](http://freedns.afraid.org/) | [example](http://freedns.afraid.org/scripts/freedns.clients.php) |
| [No-IP](http://www.noip.com/) | Use protocol `noip`, server `dynupdate.no-ip.com` |
| [nsupdate.info](https://www.nsupdate.info/) | Use protocol `dyndns2` |
| [Dyn DNS](https://dyn.com/dns/) | [example](https://sourceforge.net/p/ddclient/wiki/protocols/#dyndns2) |
| [Namecheap](https://www.namecheap.com/) | [example](https://sourceforge.net/p/ddclient/wiki/protocols/#namecheap) |
| [Dynu](https://www.dynu.com/) | [example](https://www.dynu.com/DynamicDNS/IPUpdateClient/DDClient) |

**Note:** Free users of no-ip are required to manually confirm their domain(s) every 30 days. Domain confirmation is not required for Enhanced users though. More info at [Why is My Hostname Pending Deletion?](http://www.noip.com/support/knowledgebase/why-is-my-hostname-pending-deletion/)

#### Use an external website to determine IP address

If ddclient is unable to detect your IP address, you can configure ddclient to fetch your IP from an external webpage such as [checkip.dyndns.org](http://checkip.dyndns.org/). This address is used by default when `use=web` is specified. It is also recommended to increase the check interval to avoid frequent requests to the IP check service:

 `/etc/ddclient/ddclient.conf` 
```
daemon=900
# obtain IP address from web status page
use=web
```

An alternative IP check service can be specified with the `web` key:

 `/etc/ddclient/ddclient.conf` 
```
daemon=900
# obtain IP address from web status page
use=web, web=myonlineportal.net/checkip
```

#### Starting ddclient after networking is up

If you find that ddclient is unable to update your IP properly, it may be that the ddclient process is starting before networking is up. To fix it, you can edit the unit file to depend on `network-online.target`:

 `# systemctl edit ddclient.service` 
```
[Unit]
After=network-online.target
Wants=network-online.target
```

Additional configuration for `network-online.target` may be necessary, see [[1]](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget#cutthecraphowdoimakenetwork.targetworkforme).

## Other providers

Other DDNS providers are not compatible with [ddclient](#ddclient) so updating your IP with them may require a special tool or some custom scripting. Remember that if the service allows you to update your IP using the command line, you can automate the process using tools such as [cron](/index.php/Cron "Cron") or [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").