[OpenConnect](http://www.infradead.org/openconnect.html) is a client for Cisco's [AnyConnect SSL VPN](https://www.cisco.com/go/asm) and Pulse Secure's [Pulse Connect Secure](/index.php/Pulse_Connect_Secure "Pulse Connect Secure").

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Juniper Pulse Client](#Juniper_Pulse_Client)
*   [3 Integration](#Integration)
    *   [3.1 NetworkManager](#NetworkManager)
    *   [3.2 netctl](#netctl)

## Installation

[Install](/index.php/Install "Install") the [openconnect](https://www.archlinux.org/packages/?name=openconnect) package.

## Usage

See [openconnect(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/openconnect.8). Simply run openconnect as root and enter your username and password when prompted:

```
# openconnect *vpnserver*

```

More advanced invocation with username and password. Input the password after running the command.

```
# openconnect -u *user* --passwd-on-stdin *vpnserver*

```

Often VPN provider are offering different authentication groups for different access configurations like for example for a full tunnel or split tunnel connection. To show the different offered auth-groups and to get more information about the connection to the server in general use:

```
# openconnect --authenticate *vpnserver*

```

#### Juniper Pulse Client

In order to connect to a [Pulse Connect Secure](/index.php/Pulse_Connect_Secure "Pulse Connect Secure") server you need to know the SHA-1 of its certificate.

```
# openconnect --servercert=sha1:<HASH> --authgroup="single-Factor Pulse Clients" --protocol=nc <VPN_SERVER_ADDRESS>/dana-na/auth/url_6/welcome.cgi --pid-file="/var/run/work-vpn.pid" --user=<USERNAME>

```

## Integration

### NetworkManager

[Install](/index.php/Install "Install") the [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect) package. Then configure and connect with *nm-applet* (network manager's tray icon utility from [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)) or similar utility. After installation, [restart](/index.php/Restart "Restart") the `NetworkManager.service`.

See [NetworkManager](/index.php/NetworkManager "NetworkManager") for details.

### netctl

A simple `tuntap` netctl.profile(5) can be used to integrate OpenConnect in the normal [Netctl](/index.php/Netctl "Netctl") workflow. For example:

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
ExecDownPre="kill -INT $(cat ${PIDFILE}) ; resolvconf -d ${Interface} ; ip link delete ${Interface}"

```

This allows execution like:

```
$ netctl start vpn
$ netctl restart vpn
$ netctl stop vpn

```

Note that this relies on `LOCAL_USERNAME` having a [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG") running, with the passphrase for the PGP key already cached.

If [pass](/index.php/Pass "Pass")’ interactive query is wanted, use the following line for `PASSWORD`:

```
DISPLAY=":0"
PASSWORD="`su ${LOCAL_USERNAME} -c "DISPLAY=${DISPLAY} pass ${REMOTE_USERNAME}" | head -n 1`"

```

Adjust the `DISPLAY` variable as necessary.