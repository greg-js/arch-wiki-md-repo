[Private Internet Access](https://www.privateinternetaccess.com/) is a subscription-based VPN service.

## Contents

*   [1 Manual](#Manual)
    *   [1.1 Installation](#Installation)
    *   [1.2 Usage](#Usage)
*   [2 Automatic](#Automatic)
    *   [2.1 Official installation script](#Official_installation_script)
    *   [2.2 Packages](#Packages)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Internet "kill switch"](#Internet_.22kill_switch.22)

## Manual

### Installation

Download [[1]](http://www.privateinternetaccess.com/openvpn/openvpn-strong.zip). Unzip the file and move all files to `/etc/openvpn/client`. Ensure the files have `root` as the owner.

**Tip:** Rename the `.opvn` extensions to `.conf` and remove or replace spaces in configuration file names to be able to use [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN").

**Note:** You will need to [disable ipv6](/index.php/Disable_ipv6 "Disable ipv6") since it [is not supported by PIA](https://helpdesk.privateinternetaccess.com/hc/en-us/articles/232324908-Why-Do-You-Block-IPv6-).

### Usage

See [OpenVPN#Starting OpenVPN](/index.php/OpenVPN#Starting_OpenVPN "OpenVPN").

**Tip:** To automatically login, append the name of the file containing your username and password immediately after `auth-user-pass` in the configuration file(s). See this option in [openvpn(8)](http://man7.org/linux/man-pages/man8/openvpn.8.html) for more information.

To test to see if you have successfully connected to the VPN, see [this article](https://helpdesk.privateinternetaccess.com/hc/en-us/articles/231734668-Security-Best-Practices-Part-5-Testing-Your-Security).

## Automatic

### Official installation script

Private Internet Access has an installation script that sets up [NetworkManager](/index.php/NetworkManager "NetworkManager") for use with the VPN. Download the script [here](http://www.privateinternetaccess.com/installer/pia-nm.sh) and then run to set up.

### Packages

*   **openvpn-pia** — The package automates the method listed in the [#Manual](#Manual) section, including renaming the configuartion files to be used with [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN"), as well as setting up the OpenVPN parameter `auth-user-pass` with a file for automatic login. Upon installation read `/usr/share/doc/openvpn-pia/README` for setup.

	[https://www.privateinternetaccess.com/](https://www.privateinternetaccess.com/) || [openvpn-pia](https://aur.archlinux.org/packages/openvpn-pia/)

*   **pia-nm** — Installs [NetworkManager](/index.php/NetworkManager "NetworkManager") configuration files for the VPN, similar to the [#Official installation script](#Official_installation_script).

	[https://www.privateinternetaccess.com/](https://www.privateinternetaccess.com/) || [pia-nm](https://aur.archlinux.org/packages/pia-nm/)

*   **[Private Internet Access/AUR](/index.php/Private_Internet_Access/AUR "Private Internet Access/AUR")** — Installs profiles for [NetworkManager](/index.php/NetworkManager "NetworkManager"), [ConnMan](/index.php/ConnMan "ConnMan"), and [OpenVPN](/index.php/OpenVPN "OpenVPN").

	[https://www.privateinternetaccess.com/](https://www.privateinternetaccess.com/) || [private-internet-access-vpn](https://aur.archlinux.org/packages/private-internet-access-vpn/)

## Tips and tricks

### Internet "kill switch"

The following [iptables](/index.php/Iptables "Iptables") rules only allow network traffic through the `tun` interface, with the exception that traffic is allowed to PIA's DNS servers and to port 1197, which is used in establishing the VPN connection:

 `/etc/iptables/iptables.rules` 
```
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT DROP [0:10]
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -i tun+ -j ACCEPT
-A OUTPUT -o lo -j ACCEPT
-A OUTPUT -d 209.222.18.222/32 -j ACCEPT
-A OUTPUT -d 209.222.18.218/32 -j ACCEPT
-A OUTPUT -p udp -m udp --dport 1197 -j ACCEPT
-A OUTPUT -o tun+ -j ACCEPT
-A OUTPUT -j REJECT --reject-with icmp-net-unreachable
COMMIT
```

This ensures that if you are disconnected from the VPN uknowingly, no network traffic is allowed in or out.

If you wish to additionally access devices on your LAN, you will need to explicity allow them. For example, to allow access to devices on `192.0.0.0/24`, add the following two rules (before any REJECT rule):

```
-A INPUT -s 192.168.0.0/24 -j ACCEPT
-A OUTPUT -d 192.168.0.0/24 -j ACCEPT

```

Additionally, the above rules block the ICMP protocol, which is probably not desired. See [this thread](https://bbs.archlinux.org/viewtopic.php?id=224655) for potential pitfalls of using these iptables rules as well as more details.