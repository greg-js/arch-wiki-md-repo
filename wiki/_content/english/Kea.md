Related articles

*   [dhcpd](/index.php/Dhcpd "Dhcpd")

[Kea](https://www.isc.org/kea/) is an open source DHCPv4/DHCPv6 server being developed by ​Internet Systems Consortium. Kea is a high-performance, extensible DHCP server engine that is designed to be easily modified and extended with hooks libraries.

## Installation

[Install](/index.php/Install "Install") the [kea](https://www.archlinux.org/packages/?name=kea) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

*kea* includes two unit files `kea-dhcp4.service` and `kea-dhcp6.service`, which can be used to [control](/index.php/Enable "Enable") the DHCP daemons. By default, they start the daemons on *all* [network interfaces](/index.php/Network_interfaces "Network interfaces") for IPv4 and IPv6, respectively. There are three other daemons that ship with Kea which do not currently come with built systemd unit files. They are kea-ctrl-agent, which can be used to control running Kea daemons, and kea-dhcp-ddns, which is used to send dynamic DNS updates to DNS servers. The kea-netconf daemon is not currently built with this package.

## Configuration

By default, configuration files are stored under /etc/kea. `keactrl.conf` is a ini style configuration file which is used to configure the keactrl command which can be used in leu of systemd to start and stop kea daemons. The other files, `kea-ctrl-agent.conf`, `kea-dhcp-ddns.conf`, `kea-dhcp4.conf`, `kea-dhcp6.conf`, and `kea-netconf.conf` are all JSON formatted config files which control the configuration of the daemons.