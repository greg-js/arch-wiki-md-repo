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

[Install](/index.php/Install "Install") the [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect) package. Then configure and connect with *nm-applet* (network manager's tray icon utility from [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)) or similar utility. After installation, [restart](/index.php/Restart "Restart") the `NetworkManager.service`.

See [NetworkManager](/index.php/NetworkManager "NetworkManager") for details.

### Command Line

Simply run openconnect as root and enter your username and password when prompted:

```
# openconnect *vpnserver*

```

More advanced invocation with username and password:

```
# echo -n *password* | openconnect -u *user* --passwd-on-stdin *vpnserver*

```

Often VPN provider are offering different authentication groups for different access configurations like for example for a full tunnel or split tunnel connection. To show the different offered auth-groups and to get more information about the connection to the server in general use:

```
# openconnect --authenticate *vpnserver*

```

Here is an example of how to to connect to a Juniper Pulse Secure Pulse Client. Only version 7.06 and higher are compatible.

```
# sudo openconnect --no-cert-check --authgroup="Single-Factor Pulse Clients" --juniper *example.com*/dana-na/auth/url_6/welcome.cgi

```

### Integration in netctl

A simple <tt>tuntap</tt> netctl.profile(5) can be used to integrate OpenConnect in the normal [Netctl](/index.php/Netctl "Netctl") workflow. For example:

 `/etc/netctl/vpn` 
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
AUTHGROUP='<AUTHGROUP>'
LOCAL_USERNAME=<USERNAME>
REMOTE_USERNAME=<VPN_USERNAME>
# Assuming the use of pass(1): 
PASSWORD="`su ${LOCAL_USERNAME} -c "pass ${REMOTE_USERNAME}" | head -n 1`" 

ExecUpPost="echo '${PASSWORD}' | /usr/bin/openconnect --background --pid-file=${PIDFILE} --interface='${Interface}' --authgroup='${AUTHGROUP}' --user='${REMOTE_USERNAME}' --passwd-on-stdin ${SERVER}"
ExecDownPre="kill -INT $(cat ${PIDFILE}) ; ip link delete ${Interface}"

```

This allows execution like:

```
$ netctl start vpn
$ netctl restart vpn
$ netctl stop vpn

```

Note that this relies on `LOCAL_USERNAME` having a [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG") running, with the passphrase for the PGP key already cached, as it is not possible for [pass](/index.php/Pass "Pass") to trigger an interactive query from this environment.

## See also

*   [OpenConnect](http://www.infradead.org/openconnect.html)