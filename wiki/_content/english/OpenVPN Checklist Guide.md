This article summarizes the install process required for OpenVPN. See [OpenVPN](/index.php/OpenVPN "OpenVPN") instead for a walkthrough.

## Contents

*   [1 Install](#Install)
*   [2 Prepare data](#Prepare_data)
*   [3 Generate the certificates](#Generate_the_certificates)
*   [4 Setting up the server](#Setting_up_the_server)
*   [5 Setting up the clients](#Setting_up_the_clients)

## Install

[Install](/index.php/Install "Install") the packages [openvpn](https://www.archlinux.org/packages/?name=openvpn) and [easy-rsa](https://www.archlinux.org/packages/?name=easy-rsa).

## Prepare data

*   Copy `/etc/easy-rsa` to `/etc/openvpn/easy-rsa` and cd there
*   Edit the `vars` file with the information you want. Read [Create a Public Key Infrastructure Using the easy-rsa Scripts](/index.php/Create_a_Public_Key_Infrastructure_Using_the_easy-rsa_Scripts "Create a Public Key Infrastructure Using the easy-rsa Scripts") for details.
*   Clean up any previous keys:

 `# easyrsa clean-all` 

## Generate the certificates

*   Create the "certificate authority" key

 `# easyrsa build-ca nopass` 

*   Create certificate and private key for the server

 `# easyrsa build-server-full *<server-name>* nopass` 

*   Create the Diffie-Hellman pem file for the server.

 `# easyrsa gen-dh` 

*   Create a certificate for each client.

 `# easyrsa build-client-full *<client-name>* nopass` 

All certificates are stored in `pki` directory. If you mess up, you can start all over by doing a `easyrsa clean-all`

Copy to each client the `ca.crt`, and their respective crt and key files.

## Setting up the server

*   Create `/etc/openvpn/server/myvpnserver.conf` with a content like this:

 `/etc/openvpn/server/myvpnserver.conf` 
```
port *<port>*
proto tcp
dev tun0

ca /etc/openvpn/easy-rsa/pki/ca.crt
cert /etc/openvpn/easy-rsa/pki/issued/*<server-name>*.crt
key /etc/openvpn/easy-rsa/pki/private/*<server-name>*.key
dh /etc/openvpn/easy-rsa/pki/*<your pem file>*

server *<desired base ip>* 255.255.255.0
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

*   Start and, optionally, enable for autostart on boot, the daemon. (In this example, is `openvpn-server@myvpnserver.service`)

Read [Daemon](/index.php/Daemon "Daemon") for more information.

## Setting up the clients

*   Create a .conf file for each client like this:

 `/etc/openvpn/client/a-client-conf-file.conf` 
```
client
remote *<server>* *<port>*
dev tun0
proto tcp
resolv-retry infinite
nobind
persist-key
persist-tun
verb 2
ca ca.crt
cert *<client crt file with full path>*
key *<client key file with full path>*
comp-lzo

```

*   Start the connection with

 `# openvpn a-client-conf-file.conf &` 

Optionally, enable for autostart on boot the daemon. (In this example, is `openvpn-client@a-client-conf-file.service`)

Read [Daemon](/index.php/Daemon "Daemon") for more information.