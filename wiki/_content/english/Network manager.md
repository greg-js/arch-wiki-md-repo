A network manager lets you manage network connection settings in so called network profiles to facilitate switching networks. For manual network configuration see [Network configuration](/index.php/Network_configuration "Network configuration").

**Note:** There are many solutions to choose from, but remember that all of them are mutually exclusive; you should not run two daemons simultaneously.

| Network manager | handles wired
connections | GUI | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | CLI tools | [PPP](https://en.wikipedia.org/wiki/Point-to-Point_Protocol "wikipedia:Point-to-Point Protocol") support
(e.g. 3G modem) |
| [ConnMan](/index.php/ConnMan "ConnMan") | Yes | 8 unofficial | No | [connmanctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connmanctl.1) | Yes |
| [netctl](/index.php/Netctl "Netctl") | Yes | 2 unofficial | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [netctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1), wifi-menu | Yes |
| [NetworkManager](/index.php/NetworkManager "NetworkManager") | Yes | Yes | No | [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1), [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1) | Yes |
| [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") | Yes | No | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | No |  ? |
| [Wicd](/index.php/Wicd "Wicd") | Yes | Yes | No | [wicd-cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-cli.8), [wicd-curses(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-curses.8) | No |
| [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar") | No | Yes | No | No | No |

See also [List of applications#Network managers](/index.php/List_of_applications#Network_managers "List of applications").