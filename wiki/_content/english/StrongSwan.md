IPSec is an encryption and authentication standard that can be used to build secure Virtual Private Networks (VPNs).

It is natively supported by the Linux kernel, but configuration of encryption keys is left to the user. The [IKE](https://en.wikipedia.org/wiki/Internet_Key_Exchange "wikipedia:Internet Key Exchange") protocols are therefore used in IPSec VPNs to automatically negotiate key exchanges securely using a variety of means, including certificates, pre-shared keys or both.

They are typically implemented in userspace daemons on the server side. [strongSwan](https://strongswan.org/) is an IKE daemon with full support for IKEv1 and IKEv2\. It is natively supported by most modern clients, including Linux, Windows 7, Apple iOS, Mac OSX, FreeBSD and BlackBerry OS.

## Contents

*   [1 Server Configuration](#Server_Configuration)
    *   [1.1 Certificates](#Certificates)
        *   [1.1.1 Certificate Authority](#Certificate_Authority)
        *   [1.1.2 Host Certificate](#Host_Certificate)
        *   [1.1.3 Client Certificate](#Client_Certificate)
    *   [1.2 VPN Variants](#VPN_Variants)
        *   [1.2.1 IPSec in tunnel mode](#IPSec_in_tunnel_mode)
        *   [1.2.2 IPSec in transport mode](#IPSec_in_transport_mode)
        *   [1.2.3 IPSec/L2TP](#IPSec.2FL2TP)
    *   [1.3 Secrets](#Secrets)
    *   [1.4 Networking](#Networking)
    *   [1.5 Troubleshooting](#Troubleshooting)
*   [2 Client configuration](#Client_configuration)
*   [3 See also](#See_also)

## Server Configuration

First, install the [strongswan](https://aur.archlinux.org/packages/strongswan/) package.

### Certificates

The first step is to generate the X.509 certificates, including a certificate authority (CA), a server certificate, and at least one client certificate.

#### Certificate Authority

Let us start by creating a self-signed root CA certificate:

```
$ cd /etc/ipsec.d/
$ ipsec pki --gen --type rsa --size 4096 \
	   --outform pem \
	   > private/strongswanKey.pem
$ chmod 600 private/strongswanKey.pem
$ ipsec pki --self --ca --lifetime 3650 \
	   --in private/strongswanKey.pem --type rsa \
	   --dn "C=CH, O=strongSwan, CN=strongSwan Root CA" \
	   --outform pem \
    > cacerts/strongswanCert.pem

```

The result is a 4096 bit RSA private key `strongswanKey.pem` (line 4) and a self-signed CA certificate `strongswanCert.pem` (line 10) with a validity of 10 years (3650 days). The files are stored in PEM encoded format.

You can change the Distinguished Name (DN) to more relevant values for country (C), organization (O), and common name (CN), but you do not have to.

To list the properties of your newly generated certificate, type in the following command:

```
$ ipsec pki --print --in cacerts/strongswanCert.pem

```

Output:

```
cert:      X509
subject:  "C=CH, O=strongSwan, CN=strongSwan Root CA"
issuer:   "C=CH, O=strongSwan, CN=strongSwan Root CA"
validity:  not before Nov 22 11:55:41 2013, ok
           not after  Nov 20 11:55:41 2023, ok (expires in 3649 days)
serial:    65:39:93:df:a0:f8:40:03
flags:     CA CRLSign self-signed
authkeyId: 45:30:11:da:a4:0e:0b:0a:a3:41:a5:81:41:ab:d8:04:7a:40:6c:c0
subjkeyId: 45:30:11:da:a4:0e:0b:0a:a3:41:a5:81:41:ab:d8:04:7a:40:6c:c0
pubkey:    RSA 4096 bits
keyid:     dc:15:91:95:04:07:a5:13:69:5f:77:65:26:d7:02:3f:60:ec:73:c8
subjkey:   45:30:11:da:a4:0e:0b:0a:a3:41:a5:81:41:ab:d8:04:7a:40:6c:c0

```

**Warning:** The private key `/etc/ipsec.d/private/strongswanKey.pem` of the CA should be moved somewhere safe, ossibly to a special signing host without access to the Internet. Theft of this master signing key would completely compromise your public key infrastructure.

#### Host Certificate

This certificate will be used to authenticate the VPN server. Run the following commands:

```
$ cd /etc/ipsec.d/
$ ipsec pki --gen --type rsa --size 2048 \
  	--outform pem \
  	> private/vpnHostKey.pem
$ chmod 600 private/vpnHostKey.pem
$ ipsec pki --pub --in private/vpnHostKey.pem --type rsa | \
	 ipsec pki --issue --lifetime 730 \
	  --cacert cacerts/strongswanCert.pem \
	  --cakey private/strongswanKey.pem \
	  --dn "C=CH, O=strongSwan, CN=vpn.example.com" \
	  --san vpn.example.com \
	  --flag serverAuth --flag ikeIntermediate \
	  --outform pem > certs/vpnHostCert.pem

```

The result is a 2048 bit RSA private key `vpnHostKey.pem` (line 4). In line 6 we extract its public key and pipe it over to issue `vpnHostCert.pem` (line 13), a host certificate signed by your CA. The certificate has a validity of two years (730 days). It identifies the VPN host by its Fully Qualified Domain Name (FQDN) (here: `vpn.example.com`).

**Warning:** The domain name or IP address of your VPN server, which is later entered in the client's connection properties, MUST be contained either in the subject Distinguished Name (here in CN, line 10) and/or in a subject Alternative Name (line11), but preferably in both. Make sure both times to replace vpn.example.com with your VPN's hostname – or else the connection between client and server will fail!

**Note:** If you are going to use the built-in VPN client of Windows 7, you MUST add the `serverAuth` extended key usage flag to your host certificate as shown above, or the client will refuse to connect.

In addition, OS X 10.7.3 or older requires the `ikeIntermediate` flag, which we also added here.

Since the addition of these two flags probably will not hurt anyone, you should make sure you keep them there.

Let us take a look at the properties of our newly generated certificate.

```
$ ipsec pki --print --in certs/vpnHostCert.pem

```

Output:

```
cert:      X509
subject:  "C=CH, O=strongSwan, CN=vpn.example.com"
issuer:   "C=CH, O=strongSwan, CN=strongSwan Root CA"
validity:  not before Nov 22 21:16:51 2013, ok
           not after  Nov 22 21:16:51 2015, ok (expires in 729 days)
serial:    0c:05:d7:d5:57:0e:d9:48
altNames:  vpn.zeitgeist.se
flags:     serverAuth iKEIntermediate 
authkeyId: 9b:57:35:fb:cd:9e:2d:20:37:1d:61:4c:e7:c4:5b:5e:dc:64:ad:fc
subjkeyId: 5f:12:c2:06:ee:2b:1e:cc:5f:78:54:ff:f0:f3:7b:a0:2b:c0:b4:d6
pubkey:    RSA 2048 bits
keyid:     6f:a7:99:60:27:27:09:96:02:c1:b9:d9:7d:c1:b0:10:e3:e1:d5:45
subjkey:   5f:12:c2:06:ee:2b:1e:cc:5f:78:54:ff:f0:f3:7b:a0:2b:c0:b4:d6

```

#### Client Certificate

Any client will require a personal certificate in order to use the VPN. The process is analogous to generating a host certificate, except that we identify a client certificate by the client's e-mail address rather than a hostname.

```
$ cd /etc/ipsec.d/
$ ipsec pki --gen --type rsa --size 2048 \
	  --outform pem \
	  > private/ClientKey.pem
$ chmod 600 private/ClientKey.pem
$ ipsec pki --pub --in private/ClientKey.pem --type rsa | \
	 ipsec pki --issue --lifetime 730 \
	  --cacert cacerts/strongswanCert.pem \
	  --cakey private/strongswanKey.pem \
	  --dn "C=CH, O=strongSwan, CN=myself@example.com" \
	  --san myself@example.com \
	  --outform pem > certs/ClientCert.pem
$ openssl pkcs12 -export -inkey private/ClientKey.pem \
	  -in certs/ClientCert.pem -name "My own VPN client certificate" \
	  -certfile cacerts/strongswanCert.pem \
	  -caname "strongSwan Root CA" \
	  -out Client.p12

```

The result is a 2048 bit RSA private key `ClientKey.pem` (line 4). In line 6 we extract its public key and pipe it over to issue `ClientCert.pem` (line 12), the first client certificate signed by your CA. The certificate has a validity of two years (730 days) and identifies the client by his e-mail address (here: `myself@example.com`). The last command bundles all needed certificates and keys into a PKCS#12 file with a passphrase, which is the most convenient format for clients.

### VPN Variants

The easiest configuration to get running with is IPSec in tunnel mode, described below.

#### IPSec in tunnel mode

VPN configuration can be found in `/etc/ipsec.conf`. The following contains the necessary options to build a basic, functional VPN server:

 `/etc/ipsec.conf` 

```
# ipsec.conf - strongSwan IPsec configuration file
config setup

  # By default only one client can connect at the same time with an identical
  # certificate and/or password combination. Enable this option to disable
  # this behavior.
  # uniqueids=never

  # Slightly more verbose logging. Very useful for debugging.
  charondebug="cfg 2, dmn 2, ike 2, net 2"

# Default configuration options, used below if an option is not specified.
# See: https://wiki.strongswan.org/projects/strongswan/wiki/ConnSection
conn %default

  # Use IKEv2 by default
  keyexchange=ikev2

  # Prefer modern cipher suites that allow PFS (Perfect Forward Secrecy)
  ike=aes128-sha256-ecp256,aes256-sha384-ecp384,aes128-sha256-modp2048,aes128-sha1-modp2048,aes256-sha384-modp4096,aes256-sha256-modp4096,aes256-sha1-modp4096,aes128-sha256-modp1536,aes128-sha1-modp1536,aes256-sha384-modp2048,aes256-sha256-modp2048,aes256-sha1-modp2048,aes128-sha256-modp1024,aes128-sha1-modp1024,aes256-sha384-modp1536,aes256-sha256-modp1536,aes256-sha1-modp1536,aes256-sha384-modp1024,aes256-sha256-modp1024,aes256-sha1-modp1024!
  esp=aes128gcm16-ecp256,aes256gcm16-ecp384,aes128-sha256-ecp256,aes256-sha384-ecp384,aes128-sha256-modp2048,aes128-sha1-modp2048,aes256-sha384-modp4096,aes256-sha256-modp4096,aes256-sha1-modp4096,aes128-sha256-modp1536,aes128-sha1-modp1536,aes256-sha384-modp2048,aes256-sha256-modp2048,aes256-sha1-modp2048,aes128-sha256-modp1024,aes128-sha1-modp1024,aes256-sha384-modp1536,aes256-sha256-modp1536,aes256-sha1-modp1536,aes256-sha384-modp1024,aes256-sha256-modp1024,aes256-sha1-modp1024,aes128gcm16,aes256gcm16,aes128-sha256,aes128-sha1,aes256-sha384,aes256-sha256,aes256-sha1!

  # Dead Peer Discovery
  dpdaction=clear
  dpddelay=300s

  # Do not renegotiate a connection if it is about to expire
  rekey=no

  # Server side
  left=%any
  leftsubnet=0.0.0.0/0
  leftcert=vpnHostCert.pem

  # Client side
  right=%any
  rightdns=8.8.8.8,8.8.4.4
  rightsourceip=%dhcp

# IKEv2: Newer version of the IKE protocol
conn IPSec-IKEv2
  keyexchange=ikev2
  auto=add

# IKEv2-EAP
conn IPSec-IKEv2-EAP
  also="IPSec-IKEv2"
  rightauth=eap-mschapv2
  rightsendcert=never
  eap_identity=%any

# IKEv1 (Cisco-compatible version)
conn CiscoIPSec
  keyexchange=ikev1
  # forceencaps=yes
  rightauth=pubkey
  rightauth2=xauth
  auto=add

```

#### IPSec in transport mode

#### IPSec/L2TP

The [L2TP/IPsec VPN client setup](/index.php/L2TP/IPsec_VPN_client_setup "L2TP/IPsec VPN client setup") page describes how to setup a client to connect to an IPSec/L2TP server. This variant of an IPSec VPN has the advantage of allowing to tunnel non-IP packets, contrary to pure IPSec, but at the expense of having to run an additional L2TP daemon.

### Secrets

strongSwan needs to know which clients are allowed to connect to the VPN. This is configured in the `/etc/ipsec.secrets` file, like the following example:

 `/etc/ipsec.secrets` 

```
# This file holds shared secrets or RSA private keys for authentication.

# RSA private key for this host, authenticating it to any other host
# which knows the public part.  Suitable public keys, for ipsec.conf, DNS,
# or configuration of other implementations, can be extracted conveniently
# with "ipsec showhostkey".

: RSA ClientKey.pem
user1 : EAP "topsecretpassword"
user2 : XAUTH "evenmoretopsecretpassword"

```

Whenever you edit /etc/ipsec.secrets while strongSwan is running, you must reload the file:

```
$ ipsec rereadsecrets

```

### Networking

You’re almost done setting up your server. There are a few things left to make your VPN server properly route the VPN tunnel:

 `/etc/sysctl.d/10-net-forward.conf` 

```
# VPN
net.ipv4.ip_forward = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0

```

The VPN configuration above automatically assigns an IP address to the client using DHCP, so you need to have a working DHCP server. If the server is running on the same host as strongSwan, you may need to edit `/etc/strongswan.d/charon/dhcp.conf` like this:

 `/etc/strongswan.d/charon/dhcp.conf` 

```
dhcp {
 force_server_address = yes
 server = 192.168.0.255
}

```

You may also need to allow the following protocols in your firewall:

*   ESP (Encrypted Secure Payload): Standard IPSec traffic
*   UDP 4500: IPSec traffic in "NAT Traversal" mode
*   UDP 500: Key exchanges (IKE)

Finally, you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `strongswan` service.

### Troubleshooting

## Client configuration

## See also

*   [strongSwan 5: How to create your own VPN](https://www.zeitgeist.se/2013/11/22/strongswan-howto-create-your-own-vpn/) — The source used to write the initial revision of this article, with permission from the original author.