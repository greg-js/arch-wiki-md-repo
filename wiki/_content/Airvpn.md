# Airvpn

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Configuring OpenVPN to connect as a client to an AirVPN server

[OpenVPN](/index.php/OpenVPN "OpenVPN") describes configuration from scratch for both servers and clients, including generating keys and certificates.

If you're interested in simply getting openvpn to work with credentials provided by a third-party VPN service, just [install](/index.php/Pacman "Pacman") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package available in the [official repositories](/index.php/Official_repositories "Official repositories").

Airvpn generates your config for you, if you have an account and are logged in. You can choose a server, port, and proxy settings, and download a zip file with certificates and settings. I downloaded it from ["Access without a client"](https://airvpn.org/index.php?option=com_air&view=access&Itemid=100) on 01.20.2012\.

You should now have an archive air.zip containing 4 files:

```
 air.ovpn ca.crt  user.crt  user.key

```

Extract them to /etc/openvpn:

```
 # bsdtar -C /etc/openvpn -xf ~/air.zip

```

Note that user.key is your secret key. Don't share it or let it be compromised!

Open air.ovpn and note the lines

```
ca "ca.crt"
user "user.crt"
key  "user.key"

```

These assume that these three files are in the same directory as air.ovpn. If you move them elsewhere, set their new absolute paths in air.ovpn; else it won't be able to find them.

Set permissions on the files and delete the zip:

```
 # chmod 400 air.ovpn ca.crt  user.crt  user.key
 # shred --remove ~/air.zip

```

Point openvpn at the config file as superuser:

```
# openvpn --config /etc/openvpn/air.ovpn

```

You should get a couple dozen verbose connection logs, hopefully ending in something like

```
Sat Jan 21 02:16:47 2012 Initialization Sequence Completed

```

Background openvpn if you'd like:

```
 CTRL-Z 
   [1]+  Stopped          sudo openvpn --config /etc/openvpn/air.ovpn
 bg
 sudo openvpn --config /etc/openvpn/air.ovpn &

```

I'm not sure how to start this automatically. Perhaps putting a small script in /etc/rc.conf.d/ would be appropriate. For security's sake I don't want to guess at it, since some VPN users can't risk leaking untunnelled data. Presumably it should start before any torrent clients, irc, etc.

### Troubleshooting

If you have a custom kernel, note that OpenVPN requires TUN/TAP modules enabled as described in [OpenVPN](/index.php/OpenVPN "OpenVPN"). They should already work on default kernels.

I was setting this up on a virtual Arch system running in Virtualbox on a Windows 7 host machine. While testing I already had my Windows client tunnelling all traffic through my Windows AirVPN client. Trying to initialize a second tunnel from within the VM failed with an authentication failure, until I turned off the Windows client.

If the files are chmod 400, you must execute openvpn as superuser or it will fail with "Error opening configuration file."

See [OpenVPN](/index.php/OpenVPN "OpenVPN") for lots more.

#### Sample configuration

Sample configuration profiles are included in `/usr/share/openvpn/examples/`, but here is one for reference:

```
##############################################
## Air VPN | [https://airvpn.org](https://airvpn.org) | OpenVPN Client Configuration
##############################################

client
dev tun
proto tcp
remote 123.123.1.147 443
resolv-retry infinite
nobind
persist-key
persist-tun
ca "ca.crt"
cert "user.crt"
key "user.key"
ns-cert-type server
cipher AES-256-CBC
comp-lzo
verb 3

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Airvpn&oldid=366759](https://wiki.archlinux.org/index.php?title=Airvpn&oldid=366759)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtual Private Network](/index.php/Category:Virtual_Private_Network "Category:Virtual Private Network")