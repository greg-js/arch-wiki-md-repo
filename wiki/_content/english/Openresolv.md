[Openresolv](https://roy.marples.name/projects/openresolv) is a [resolvconf](https://en.wikipedia.org/wiki/resolvconf "wikipedia:resolvconf") implementation, i.e. a [resolv.conf](/index.php/Resolv.conf "Resolv.conf") management framework.

## Installation

[Install](/index.php/Install "Install") the [openresolv](https://www.archlinux.org/packages/?name=openresolv) package.

## Usage

Openresolv provides [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) and is configured in `/etc/resolvconf.conf`. See [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) for supported options.

Running `resolvconf -u` will generate `/etc/resolv.conf`.

Openresolv can additionally be configured to pass DNS server addresses to [unbound](/index.php/Unbound "Unbound"), [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), [BIND](/index.php/BIND "BIND") and [pdnsd](/index.php/Pdnsd "Pdnsd") resolvers. See the [official documentation](https://roy.marples.name/projects/openresolv/config) for instructions.

## Users

Stand-alone DHCP clients:

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd") has a hook which uses *resolvconf* if it is installed.

[Network managers](/index.php/Network_manager "Network manager"):

*   [netctl](/index.php/Netctl "Netctl") (used by default)
*   [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager")

[VPN](/index.php/VPN "VPN") clients:

*   [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN")
*   [strongSwan](/index.php/StrongSwan "StrongSwan")
*   [WireGuard](/index.php/WireGuard "WireGuard")