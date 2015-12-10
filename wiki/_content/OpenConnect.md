# OpenConnect

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [OpenConnect](http://www.infradead.org/openconnect.html):

OpenConnect is a client for Cisco's AnyConnect SSL VPN, which is supported by the ASA5500 Series, by IOS 12.4(9)T or later on Cisco SR500, 870, 880, 1800, 2800, 3800, 7200 Series and Cisco 7301 Routers, and probably others.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 NetworkManager](#NetworkManager)
    *   [2.2 Command Line](#Command_Line)
    *   [2.3 Integration in netctl](#Integration_in_netctl)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openconnect](https://www.archlinux.org/packages/?name=openconnect) package.

## Usage

OpenConnect can be used with NetworkManager, or manually via the command line.

### NetworkManager

[Install](/index.php/Install "Install") the [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect) package. Then configure and connect with `nm-applet` (network manager's tray icon) or similar utility. After installation, [restart](/index.php/Restart "Restart") the `NetworkManager.service`.

See [NetworkManager](/index.php/NetworkManager "NetworkManager") for details.

### Command Line

Simply run openconnect as root and enter your username and password when prompted:

```
# openconnect _vpnserver_

```

More advanced invocation with username and password:

```
# echo -n _password_ | openconnect -u _user_ --passwd-on-stdin _vpnserver_

```

### Integration in netctl

A simple <tt>tuntap</tt> netctl.profile(5) can be used to integrate OpenConnect in the normal [Netctl](/index.php/Netctl "Netctl") workflow.

```
Description='VPN'
Interface=vpn
Connection=tuntap
Mode=tun
#User=root
#Group=root

BindsToInterfaces=(enp0s25 wlp2s0)
IP=no

PIDFILE=/run/openconnect_${Interface}.pid
SERVER=vpn.example.net
AUTHGROUP="VPN"                                     # might be asked by openconnect before asking for password
USERNAME=user 
PASSWORD=`su ${USERNAME} -c "pass vpn/${USERNAME}"` # assuming the user uses pass(1) to keep their passwords safe

ExecUpPost="echo ${PASSWORD} | /usr/bin/openconnect --background --pid-file=${PIDFILE} --interface=${Interface} --authgroup='${AUTHGROUP}' --user=${USERNAME} --passwd-on-stdin ${SERVER}"
ExecDownPre="kill -INT $(cat ${PIDFILE}) ; ip link delete ${Interface}"

```

Saved as, e.g., <tt>/etc/netctl/vpn</tt>, this allows such manipulations as

```
$ netctl start vpn
$ netctl restart vpn
$ netctl stop vpn

```

## See also

*   [OpenConnect](http://www.infradead.org/openconnect.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenConnect&oldid=402332](https://wiki.archlinux.org/index.php?title=OpenConnect&oldid=402332)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtual Private Network](/index.php/Category:Virtual_Private_Network "Category:Virtual Private Network")