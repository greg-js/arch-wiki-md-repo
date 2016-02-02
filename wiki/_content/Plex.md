# Plex

Plex is a media player system and software suite consisting of many player applications for 10-foot user interfaces and an associated media server that organizes personal media stored on local devices. Integrated Plex Channels provide users with access to a growing number of online content providers such as YouTube, Vimeo, TEDTalks, and CNN among others. Plex also provides integration for cloud services including Dropbox, Box, Google Drive, Copy and Bitcasa.

Plex for Linux is split into a closed-source server Plex Media Server, and an open-source client Plex Home Theater, a fork of the popular XBMC.

## Contents

*   [1 Plex Media Server (PMS)](#Plex_Media_Server_.28PMS.29)
    *   [1.1 Installation](#Installation)
    *   [1.2 Setup](#Setup)
    *   [1.3 Plugins](#Plugins)
    *   [1.4 Security](#Security)
    *   [1.5 Resource Management](#Resource_Management)
    *   [1.6 Network](#Network)
    *   [1.7 Remote access through vpn](#Remote_access_through_vpn)
        *   [1.7.1 Requirements](#Requirements)
        *   [1.7.2 How to](#How_to)
    *   [1.8 Troubleshooting](#Troubleshooting)
*   [2 Plex Home Theater (PHT)](#Plex_Home_Theater_.28PHT.29)
    *   [2.1 Installation](#Installation_2)
*   [3 Kodi and PleXBMC](#Kodi_and_PleXBMC)
    *   [3.1 Installation](#Installation_3)

## Plex Media Server (PMS)

### Installation

Install the [plex-media-server](https://aur.archlinux.org/packages/plex-media-server/)<sup><small>AUR</small></sup> package, or the [plex-media-server-plexpass](https://aur.archlinux.org/packages/plex-media-server-plexpass/)<sup><small>AUR</small></sup> package if you have a Plex Pass.

### Setup

[Enable](/index.php/Enable "Enable") and start `plexmediaserver.service`.

To begin configuring PMS, browse to `[http://localhost:32400/web/](http://localhost:32400/web/)`.

To configure PMS remotely, you must first create an SSH tunnel (setup can only be done from `localhost`)

`ssh ip.address.of.server -L 8888:localhost:32400`

and then browse to `[http://localhost:8888/web/](http://localhost:8888/web/)`.

### Plugins

PMS can be expanded with additional plugins. For example, PMS can be used as an IPTV client with the [IPTV plugin](https://github.com/Cigaras/IPTV.bundle).

Plugins can be installed inside `$PLEX_MEDIA_SERVER_APPLICATION_SUPPORT_DIR/Plex Media Server/Plug-ins`.

### Security

It is recommended to store your media files outside of your home directory, as making it accessible to PMS would mean lowering its security. Having a separate `/media` or `/mnt/media` partition is a good setup for use with PMS.

You can further increase security via systemd, by creating a `/etc/systemd/system/plexmediaserver.service.d/restrict.conf` file containing the following:

```
[Service]
ReadOnlyDirectories=/
ReadWriteDirectories=/var/lib/plex /tmp

```

**Note:** Those mechanisms are currently limited, see [DeveloperWiki:Security#ReadOnly/ReadWrite](/index.php/DeveloperWiki:Security#ReadOnly.2FReadWrite "DeveloperWiki:Security"). For instance, ReadOnlyDirectories do not apply to any submount, you have to list them as well.

### Resource Management

Originally, PMS used ulimit to limit its allocated resources, however this is not compatible with running as a regular user. Instead, you can now set a maximum amount of memory via, again, systemd. For example, you can add:

```
MemoryLimit=4G

```

to the file mentioned above.

### Network

**Note:** PMS supports both IPv4 and IPv6\. This section only assumes the use of IPv4.

PMS and its DLNA server require several ports to be open:

*   Plex Media Server: TCP 32400
*   Plex DLNA Server: TCP 32469, UDP 1900
*   Network Discovery: UDP 32410, 32412, 32413, 32414
*   Bonjour/Avahi Network Discovery (legacy): UDP 5353

A short example with iptables:

```
# iptables -A INPUT -p tcp -m multiport --dports 32400,32469 -j ACCEPT
# iptables -A INPUT -p udp -m multiport --dports 1900,32410,32412,32413,32414 -j ACCEPT

```

### Remote access through vpn

#### Requirements

If you share your libraries with some friends, but want the data to go through your vpn connection, you will need two things:

*   A vpn provider that allows static port forwarding
*   Remote Access enabled on your [plex server settings](http://127.0.0.1:32400/web/index.html#!/settings/server)

#### How to

1.  Go to your vpn provider settings and ask for a port. _(We're going to assume ours gave us the port 11652)_
2.  Then add the following command to your boot sequence _(rc.local for example)_

    	`# iptables -t nat -A PREROUTING -i tun0 -p tcp --dport 11652 -j REDIRECT --to-ports 32400`

    	_(We're going to assume you're using the tun0 interface for openvpn)_

3.  Finally, go to your plex server settings, enable advanced settings and define the custom port at 11652

**Warning:** Don't forget to replace the 11652 example port with yours!

### Troubleshooting

Logs are located in:

```
$PLEX_MEDIA_SERVER_APPLICATION_SUPPORT_DIR/Plex Media Server/Logs

```

In case there are no logs or they are not helpful, you might want to launch PMS manually to get some terminal output:

```
sudo -u plex /usr/bin/bash
source /etc/conf.d/plexmediaserver
export LD_LIBRARY_PATH=/opt/plexmediaserver
/opt/plexmediaserver/Plex\ Media\ Server

```

## Plex Home Theater (PHT)

### Installation

[Install](/index.php/Install "Install") the [openpht](https://aur.archlinux.org/packages/openpht/)<sup><small>AUR</small></sup> package.

Plex Home Theater can be launched by running `plexhometheater.sh` from your terminal.

## Kodi and PleXBMC

With the PleXBMC add-on, Kodi can be used as a replacement for PHT.

### Installation

Install the [kodi](https://www.archlinux.org/packages/?name=kodi) package, then follow the instructions over [here](http://kodi.wiki/view/Add-on:PleXBMC).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Plex&oldid=415966](https://wiki.archlinux.org/index.php?title=Plex&oldid=415966)"