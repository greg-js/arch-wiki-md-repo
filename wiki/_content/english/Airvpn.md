A VPN based on OpenVPN and operated by activists and hacktivists in defence of net neutrality, privacy and against censorship.

## Contents

*   [1 Configuring OpenVPN to connect as a client to an AirVPN server](#Configuring_OpenVPN_to_connect_as_a_client_to_an_AirVPN_server)
    *   [1.1 Using the all in one config file](#Using_the_all_in_one_config_file)
    *   [1.2 Using seperate keys and certs](#Using_seperate_keys_and_certs)
    *   [1.3 Troubleshooting](#Troubleshooting)
        *   [1.3.1 Sample configuration](#Sample_configuration)

## Configuring OpenVPN to connect as a client to an AirVPN server

### Using the all in one config file

You can use the opvn file gotten from AirVPN's config generator as a conf file. Simply download the ovpn file after going through the generator, change the filename to air.conf, and place it in /etc/openvpn/client. It is reccomended to chmod 400 this file to prevent tampering or unauthorized reading. You should then [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") openvpn-client@air.service.

### Using seperate keys and certs

[OpenVPN](/index.php/OpenVPN "OpenVPN") describes configuration from scratch for both servers and clients, including generating keys and certificates.

If you're interested in simply getting openvpn to work with credentials provided by a third-party VPN service, just [install](/index.php/Install "Install") the [openvpn](https://www.archlinux.org/packages/?name=openvpn) package available in the [official repositories](/index.php/Official_repositories "Official repositories").

Airvpn generates your config for you, if you have an account and are logged in. You can choose a server, port, and proxy settings, and download a zip file with certificates and settings. On the ["OpenVPN Configuration Generator"](https://airvpn.org/generator) page, select "Separate keys/certs from the .ovpn file" in advanced mode (on 01.16.2017).

You should now have an archive air.zip containing 4 files:

```
 air.ovpn ca.crt  user.crt  user.key

```

Extract them to /etc/openvpn/client:

```
 # bsdtar -C /etc/openvpn/client -xf ~/air.zip

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
# openvpn --config /etc/openvpn/client/air.ovpn

```

You should get a couple dozen verbose connection logs, hopefully ending in something like

```
Sat Jan 21 02:16:47 2012 Initialization Sequence Completed

```

Background openvpn if you'd like:

```
 CTRL-Z 
   [1]+  Stopped          sudo openvpn --config /etc/openvpn/client/air.ovpn
 bg
 sudo openvpn --config /etc/openvpn/client/air.ovpn &

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