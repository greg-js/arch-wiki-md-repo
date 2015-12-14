# OpenVPN Checklist Guide

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article summarizes the install process required for OpenVPN. See [OpenVPN](/index.php/OpenVPN "OpenVPN") instead for a walkthrough.

## Contents

*   [1 Install](#Install)
*   [2 Prepare data](#Prepare_data)
*   [3 Generate the certificates](#Generate_the_certificates)
*   [4 Setting up the server](#Setting_up_the_server)
*   [5 Setting up the clients](#Setting_up_the_clients)

## Install

[Install](/index.php/Install "Install") the packages [openvpn](https://www.archlinux.org/packages/?name=openvpn) and [easy-rsa](https://www.archlinux.org/packages/?name=easy-rsa) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Prepare data

*   Copy `/usr/share/easy-rsa/` to `/etc/openvpn/easy-rsa` and cd there
*   Edit the `vars` file with the information you want, then source it. Read [Create a Public Key Infrastructure Using the easy-rsa Scripts](/index.php/Create_a_Public_Key_Infrastructure_Using_the_easy-rsa_Scripts "Create a Public Key Infrastructure Using the easy-rsa Scripts") for details.

 `# source ./vars` 

*   Clean up any previous keys:

 `# ./clean-all` 

## Generate the certificates

*   Create the "certificate authority" key

 `#  ./build-ca` 

*   Create certificate and private key for the server

 `#  ./build-key-server _<server-name>_` 

*   Create the Diffie-Hellman pem file for the server. Do not enter a challenge password or company name when you set these up.

 `#  ./build-dh` 

*   Create a certificate for each client.

 `# ./build-key _<client-name>_` 

All certificates are stored in `keys` directory. If you mess up, you can start all over by doing a `./clean-all`

Copy to each client the `ca.crt`, and their respective crt and key files.

## Setting up the server

*   Create `/etc/openvpn/myvpnserver.conf` with a content like this:

 `/etc/openvpn/myvpnserver.conf` 

```
port _<port>_
proto tcp
dev tun0

ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/_<server-name>_.crt
key /etc/openvpn/easy-rsa/keys/_<server-name>_.key
dh /etc/openvpn/easy-rsa/keys/_<your pem file>_

server _<desired base ip>_ 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
comp-lzo
user nobody
group nobody
persist-key
persist-tun
status /var/log/openvpn-status.log
verb 3

log-append /var/log/openvpn
status /tmp/vpn.status 10

```

*   Start and, optionally, enable for autostart on boot, the daemon. (In this example, is `openvpn@myvpnserver.service`)

Read [Daemon](/index.php/Daemon "Daemon") for more information.

## Setting up the clients

*   Create a .conf file for each client like this:

 `a-client-conf-file.conf` 

```
client
remote _<server>_ _<port>_
dev tun0
proto tcp
resolv-retry infinite
nobind
persist-key
persist-tun
verb 2
ca ca.crt
cert _<client crt file with full path>_
key _<client key file with full path>_
comp-lzo

```

*   Start the connection with

 `# openvpn a-client-conf-file.conf &` 

Optionally, enable for autostart on boot the daemon. (In this example, is `openvpn@a-client-conf-file.service`)

Read [Daemon](/index.php/Daemon "Daemon") for more information.

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenVPN_Checklist_Guide&oldid=412147](https://wiki.archlinux.org/index.php?title=OpenVPN_Checklist_Guide&oldid=412147)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtual Private Network](/index.php/Category:Virtual_Private_Network "Category:Virtual Private Network")