[Private Internet Access](https://www.privateinternetaccess.com/) is a subscription-based VPN service.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Manual](#Manual)
    *   [1.1 NetworkManager applet approach](#NetworkManager_applet_approach)
        *   [1.1.1 Installation](#Installation)
        *   [1.1.2 Configuration](#Configuration)
        *   [1.1.3 Usage](#Usage)
    *   [1.2 OpenVPN command line approach](#OpenVPN_command_line_approach)
        *   [1.2.1 Installation](#Installation_2)
        *   [1.2.2 Usage](#Usage_2)
*   [2 Automatic](#Automatic)
    *   [2.1 Official installation script](#Official_installation_script)
    *   [2.2 Official Linux client](#Official_Linux_client)
    *   [2.3 Packages](#Packages)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Internet "kill switch"](#Internet_"kill_switch")
    *   [3.2 Setting PIA DNS](#Setting_PIA_DNS)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 I can't connect to OpenVPN using PIA manager, or OpenVPN doesn't work](#I_can't_connect_to_OpenVPN_using_PIA_manager,_or_OpenVPN_doesn't_work)

## Manual

**Note:**

*   [Disable ipv6](/index.php/Disable_ipv6 "Disable ipv6") since it is not supported by PIA.[[1]](https://helpdesk.privateinternetaccess.com/hc/en-us/articles/232324908-Why-Do-You-Block-IPv6-)
*   Ensure you are using PIA's [DNS](/index.php/DNS "DNS") servers, listed on their website.

### NetworkManager applet approach

#### Installation

Download [OpenVPN configuration files from PIA](https://www.privateinternetaccess.com/openvpn/openvpn.zip). Extract the ZIP file to a place in your user home directory or elsewhere that is memorable for future access.

Install and configure [NetworkManager](/index.php/NetworkManager "NetworkManager") along with the NetworkManager applet and OpenVPN plugin.

#### Configuration

1.  Right click on the NetworkManager applet from your desktop environment, and click Edit Connections. Click the Plus sign in the bottom left corner of the Network Connections window that appears.
2.  When you choose a connection type, click the drop down menu and scroll all the way down until you reach "Import a saved VPN configuration". Select that option. Now, click Create.
3.  Navigate to the directory you extracted all of the openvpn files to earlier, then open one of the files from that folder. Generally speaking, you will want to open the file that is associated with the connection you specifically want.
4.  After you have opened one of the openvpn files, the window that appears should be "Editing <connection type>". Type in your Username and Password that you received from Private Internet Access. There is an icon in the password box indicating user permission of the credentials; change the settings as you wish.
5.  Now, click Advanced. Next to "Use LZO data compression", click the drop down menu to select "adaptive" and next to "Set vitrual device type", click the menu and make sure "TUN" is selected.
6.  Next, go to the security tab and select as cipher "AES-128-CBC" and as HMAC Authentication "SHA-1".
7.  Click the OK button at the bottom left of the window to save this change.
8.  Go to the IPv6 tab and select for "Method" "Ignored" since PIA blocks IPv6 addresses [[2]](https://www.privateinternetaccess.com/helpdesk/kb/articles/why-do-you-block-ipv6-2).
9.  Click Save at the bottom left of the "Editing <connection type>" window.

#### Usage

Left click on the NetworkManager applet. There is a VPN Connections menu. Inside it should be the VPN connection you saved. Click on it to connect to Private Internet Access.

When a gold lock has appeared over the NetworkManager applet, you are successfully connected to Private Internet Access. Visit [Private Internet Access](https://www.privateinternetaccess.com/) and confirm that you are connected by referring to the status message at the top of their homepage.

**Note:** If the VPN asks for a password, and you would like to avoid entering the password each time you attempt to connect, be sure to click the icon in the password box as noted previously regarding permission of credentials and change it to all users.

### OpenVPN command line approach

#### Installation

Download [OpenVPN configurations from PIA](https://www.privateinternetaccess.com/openvpn/openvpn-strong.zip). Unzip the file and move all files to `/etc/openvpn/client`. Ensure the files have `root` as the owner.

**Tip:** To be able to use [OpenVPN#systemd service configuration](/index.php/OpenVPN#systemd_service_configuration "OpenVPN") (e.g `systemctl start openvpn-client@*<config>*`), rename the all the files and replace `.opvn` extension with `.conf` and replace spaces in configuration file names with underscores.

#### Usage

See [OpenVPN#Starting OpenVPN](/index.php/OpenVPN#Starting_OpenVPN "OpenVPN").

**Tip:** To automatically login, append the name of the file containing your username and password immediately after `auth-user-pass` in the configuration file(s). See this option in [openvpn(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openvpn.8)for more information.

To test to see if you have successfully connected to the VPN, see [this article](https://helpdesk.privateinternetaccess.com/hc/en-us/articles/231734668-Security-Best-Practices-Part-5-Testing-Your-Security).

## Automatic

### Official installation script

Private Internet Access has an installation script that sets up [NetworkManager](/index.php/NetworkManager "NetworkManager") for use with the VPN. Download the script [here](http://www.privateinternetaccess.com/installer/pia-nm.sh) and then run to set up.

### Official Linux client

Private Internet Access now has an official client for Linux with support for Arch. Download the client from [this page](https://www.privateinternetaccess.com/pages/download), unzip the file (e.g. `pia-v81-installer-linux.tar.gz`) and run the installation script (.e.g. `# ./pia-v81-installer-linux.sh`).

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

This ensures that if you are disconnected from the VPN unknowingly, no network traffic is allowed in or out.

If you wish to additionally access devices on your LAN, you will need to explicitly allow them. For example, to allow access to devices on `192.0.0.0/24`, add the following two rules (before any REJECT rule):

```
-A INPUT -s 192.168.0.0/24 -j ACCEPT
-A OUTPUT -d 192.168.0.0/24 -j ACCEPT

```

Additionally, the above rules block the ICMP protocol, which is probably not desired. See [this thread](https://bbs.archlinux.org/viewtopic.php?id=224655) for potential pitfalls of using these iptables rules as well as more details.

### Setting PIA DNS

If you find that Network Manager is controlling your host's DNS settings, and therefore your host cannot resolve any address, you will have to manually set the DNS server and attributes. You should note a symbolic link when running the following command

```
ls -l /etc/resolv.conf

```

Remove the symbolic link with `rm /etc/resolv.conf` Then create a new `/etc/resolv.conf` and add the following

 `/etc/resolv.conf ` 
```
nameserver 209.222.18.222
nameserver 209.222.18.218
```

Next regenerate resolvconf by typing:

```
# resolvconf -u

```

Finally make the file immutable so no other application can modify it

```
chattr +i /etc/resolv.conf

```

## Troubleshooting

### I can't connect to OpenVPN using PIA manager, or OpenVPN doesn't work

PIA manager still uses OpenVPN under the hood, so even if you don't directly use one of the OpenVPN methods, you still need it. Firstly, check that it's installed. If you used one of the installation scripts, this should be done for you.

If you're getting errors like `#<Errno::ECONNREFUSED: Connection refused - connect(2) for "127.0.0.1" port 31749>`, that probably means TAP/TUN is not currently running. Either your kernel does not have it, in which case install a kernel which does (or compile a fresh one), or it isn't currently running, in which case it needs to be started:

```
# modprobe tun

```