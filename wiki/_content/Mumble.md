# Mumble

From [Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Mumble_(software) "wikipedia:Mumble (software)"):

NaN

This page goes over installation and configuration of both the client portion of the software (Mumble) and the server portion (Murmur).

## Contents

*   [1 Client](#Client)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
*   [2 Server](#Server)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration_2)
        *   [2.2.1 Network](#Network)
        *   [2.2.2 Config File](#Config_File)
        *   [2.2.3 Startup](#Startup)
        *   [2.2.4 Self-Signed Certificate](#Self-Signed_Certificate)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Joystick Binds Not Working or Mouse Binds Get Stuck](#Joystick_Binds_Not_Working_or_Mouse_Binds_Get_Stuck)

## Client

### Installation

[Install](/index.php/Install "Install") the [mumble](https://www.archlinux.org/packages/?name=mumble) package (or [mumble-git](https://aur.archlinux.org/packages/mumble-git/)<sup><small>AUR</small></sup> for the development version).

For [JACK](/index.php/JACK "JACK") support, install the [mumble-jack](https://aur.archlinux.org/packages/mumble-jack/)<sup><small>AUR</small></sup> package (or [mumble-jack-git](https://aur.archlinux.org/packages/mumble-jack-git/)<sup><small>AUR</small></sup> for the development version).

### Configuration

When you first launch the client, a configuration wizard will take you through the setup process. Settings can be changed later through the menu.

For a discussion of advanced settings, see the [official documentation](http://mumble.sourceforge.net/). The [Mumbleguide](http://mumble.sourceforge.net/Mumbleguide) is a good starting point.

## Server

The Mumble project maintains a good guide for setting up the server here: [Murmurguide](http://mumble.sourceforge.net/Murmurguide). What follows is a quick-and-dirty, abridged version of that guide.

### Installation

[Install](/index.php/Install "Install") the [murmur](https://www.archlinux.org/packages/?name=murmur) package.

For ICE support, install the [murmur-ice](https://aur.archlinux.org/packages/murmur-ice/)<sup><small>AUR</small></sup> package.

The postinstall script will tell you to reload dbus and set the supervisor password. The default configuration does not use dbus, so you can ignore that if you want. Setting the supervisor password is recommended, however.

### Configuration

#### Network

If you use a [firewall](/index.php/Firewall "Firewall"), you will need to open TCP and UDP ports 64738. Depending on your network, you may also need to set a static IP, port forwarding, etc.

#### Config File

The default Murmur config file is at `/etc/murmur.ini` and is heavily commented. Reading through all the comments is highly recommended.

#### Startup

[Enable](/index.php/Enable "Enable") and then [start](/index.php/Start "Start") `murmur.service`. If all went smoothly, you should have a functioning Murmur server.

#### Self-Signed Certificate

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Not sure if this works when reverse lookups don't work properly. (Discuss in [Talk:Mumble#](https://wiki.archlinux.org/index.php/Talk:Mumble))

By default, murmur will generate a default self-signed certificate. Clients connecting to the server will warn users about the host name not matching and the certificate being untrusted. If your server is in DNS, you can get rid of the hostname mismatch by creating your own self-signed certificate.

Create a secure directory for the certificate and key to live in and switch to it.

```
# mkdir /var/lib/murmur/ssl
# chmod 700 /var/lib/murmur/ssl
# chown murmur:murmur /var/lib/murmur/ssl
# cd /var/lib/murmur/ssl

```

Create a self-signed certificate for your server:

```
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout voip.example.com.key -out voip.example.com.crt

```

Edit murmur.ini and tell it where your key and cert is:

 `/etc/murmur.ini` 

```
sslKey=/var/lib/murmur/ssl/voip.example.com.key
sslCert=/var/lib/murmur/ssl/voip.example.com.crt
```

## Troubleshooting

### Joystick Binds Not Working or Mouse Binds Get Stuck

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** This workaround is no longer effective on the latest mumble versions. [github issue](https://github.com/mumble-voip/mumble/issues/1319#issuecomment-130133952) (Discuss in [Talk:Mumble#](https://wiki.archlinux.org/index.php/Talk:Mumble))

Kernel input devices by default are unreadable by Mumble. This causes Mumble to fall back onto a buggy global bind system. This can be fixed temporarily with

```
# chmod a+r /dev/input/event*

```

or permanently fixed by creating a udev rule

 `/etc/udev/rules.d/99-input-permissions.rules`  `KERNEL=="event*", MODE="0644"` 

but be weary this exposes all your input devices to all your applications!

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mumble&oldid=402931](https://wiki.archlinux.org/index.php?title=Mumble&oldid=402931)"