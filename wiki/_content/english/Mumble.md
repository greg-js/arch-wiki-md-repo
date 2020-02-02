From [Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Mumble_(software) "wikipedia:Mumble (software)"):

	Mumble is a voice over IP (VoIP) application primarily designed for use by gamers, similar to programs such as TeamSpeak and Ventrilo.

This page goes over installation and configuration of both the client portion of the software (Mumble) and the server portion (Murmur).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Client](#Client)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
*   [2 Server](#Server)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration_2)
        *   [2.2.1 Network](#Network)
        *   [2.2.2 Config File](#Config_File)
        *   [2.2.3 Startup](#Startup)
        *   [2.2.4 SSL/TLS](#SSL/TLS)
        *   [2.2.5 SuperUser](#SuperUser)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Push-to-talk on Wayland](#Push-to-talk_on_Wayland)

## Client

### Installation

[Install](/index.php/Install "Install") the [mumble](https://www.archlinux.org/packages/?name=mumble) package (or [mumble-git](https://aur.archlinux.org/packages/mumble-git/) for the development version).

For [JACK](/index.php/JACK "JACK") support, install the [mumble-jack](https://aur.archlinux.org/packages/mumble-jack/) package.

To use the Mumble overlay with 32-bit games, install [lib32-libmumble](https://aur.archlinux.org/packages/lib32-libmumble/).

### Configuration

When you first launch the client, a configuration wizard will take you through the setup process. Settings can be changed later through the menu.

For a discussion of advanced settings, see the [official documentation](https://wiki.mumble.info/wiki/). The [Mumbleguide](https://wiki.mumble.info/wiki/Mumbleguide) is a good starting point.

## Server

The Mumble project maintains a good guide for setting up the server here: [Murmurguide](http://mumble.sourceforge.net/Murmurguide). What follows is a quick-and-dirty, abridged version of that guide.

### Installation

[Install](/index.php/Install "Install") the [murmur](https://www.archlinux.org/packages/?name=murmur) or [murmur-git](https://aur.archlinux.org/packages/murmur-git/) package. Both come with ICE support.

The postinstall script will tell you to reload dbus and set the supervisor password. SQLite is used as the default database. The default configuration does not use dbus, so you can ignore that if you want. Setting the supervisor password is recommended, however.

### Configuration

#### Network

If you use a [firewall](/index.php/Firewall "Firewall"), you will need to open TCP and UDP ports 64738. Depending on your network, you may also need to set a static IP, port forwarding, etc.

#### Config File

The default Murmur config file is at `/etc/murmur.ini` and is heavily commented. Reading through all the comments is highly recommended. More information can be found on the Mumble wiki [here](https://wiki.mumble.info/wiki/Murmur.ini).

#### Startup

[Enable](/index.php/Enable "Enable") and then [start](/index.php/Start "Start") `murmur.service`. If all went smoothly, you should have a functioning Murmur server.

#### SSL/TLS

Obtain either a self-signed certificate as described in [OpenSSL](/index.php/OpenSSL "OpenSSL"), or a publicly trusted one with [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt").

Edit `murmur.ini` and tell it where your key and cert are:

 `/etc/murmur.ini` 
```
sslCert=/etc/letsencrypt/live/$domain/cert.pem
sslKey=/etc/letsencrypt/live/$domain/privkey.pem
sslCA=/etc/letsencrypt/live/$domain/fullchain.pem
```

#### SuperUser

To set the SuperUser password, use the following command.

```
# murmurd -ini /etc/murmur.ini -supw PASSWORD

```

## Troubleshooting

### Push-to-talk on Wayland

Currently with [Wayland](/index.php/Wayland "Wayland")/[GNOME](/index.php/GNOME "GNOME")/[Sway](/index.php/Sway "Sway"), push-to-talk won't work without the window being in focus. Not allowing clients to sniff on the input when they do not have focus is a feature in [Wayland](/index.php/Wayland "Wayland"), and it will be kept that way. A proposal for a patch exists at their source [repository](https://github.com/mumble-voip/mumble/issues/3243?_pjax=%23js-repo-pjax-container) and a [merge request](https://github.com/mumble-voip/mumble/pull/3675) has been merged and is slated for Mumble version 1.4.0\. Tips for integrating this patch with Sway exist in the merge request.