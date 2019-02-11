Related articles

*   [systemd-resolvconf](/index.php/Systemd-resolvconf "Systemd-resolvconf")

[Openresolv](https://roy.marples.name/projects/openresolv) is a [resolvconf](https://en.wikipedia.org/wiki/resolvconf "wikipedia:resolvconf") implementation, i.e. a [resolv.conf](/index.php/Resolv.conf "Resolv.conf") management framework.

**Tip:** An alternative implementation is [systemd-resolvconf](/index.php/Systemd-resolvconf "Systemd-resolvconf"), but it can only be used with [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Users](#Users)
*   [4 Subscribers](#Subscribers)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Defining multiple values for options](#Defining_multiple_values_for_options)

## Installation

[Install](/index.php/Install "Install") the [openresolv](https://www.archlinux.org/packages/?name=openresolv) package.

## Usage

Openresolv provides [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) and is configured in `/etc/resolvconf.conf`. See [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) for supported options.

Running `resolvconf -u` will generate `/etc/resolv.conf`.

## Users

Stand-alone [DHCP](/index.php/DHCP "DHCP") clients:

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd") has a hook which uses *resolvconf* if it is installed.

[Network managers](/index.php/Network_manager "Network manager"):

*   [netctl](/index.php/Netctl "Netctl") (used by default)
*   [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager")

[VPN](/index.php/VPN "VPN") clients:

*   [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN")
*   [strongSwan](/index.php/StrongSwan "StrongSwan")
*   [WireGuard](/index.php/WireGuard "WireGuard")

## Subscribers

Openresolv can be configured to pass name servers and search domains to DNS resolvers. The supported resolvers are:

*   [BIND](/index.php/BIND "BIND")
*   [dnsmasq#openresolv](/index.php/Dnsmasq#openresolv "Dnsmasq")
*   [pdnsd](/index.php/Pdnsd "Pdnsd")
*   [Unbound](/index.php/Unbound "Unbound")

See the [official documentation](https://roy.marples.name/projects/openresolv/config) for instructions.

## Tips and tricks

### Defining multiple values for options

The man page does not mention it, but to define multiple values, for options that support it (e.g. `name_servers`, `resolv_conf_options` etc.) in `/etc/resolvconf.conf`, you need to write them space separated inside quotes. E.g.:

 `/etc/resolvconf.conf` 
```
resolv_conf_options="edns0 single-request"
name_servers="192.168.35.1 fd7b:d0bd:7a6e::1"
```