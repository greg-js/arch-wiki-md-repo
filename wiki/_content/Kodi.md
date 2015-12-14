# Kodi

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Kodi (previously known as XBMC), is a free, [open source (GPL)](http://www.gnu.org/copyleft/gpl.html) multimedia player that originally ran on the first-generation [XBox](https://en.wikipedia.org/wiki/Microsoft_Xbox "wikipedia:Microsoft Xbox"), and now runs on Linux, OS X, Windows, Android and iOS. Kodi can be used to play/view the most popular video, audio, and picture formats, and many more lesser-known formats, including:

*   Video - DVD-Video, VCD/SVCD, MPEG-1/2/4, DivX, XviD, Matroska
*   Audio - MP3, AAC.
*   Picture - JPG, GIF, PNG.

These can all be played directly from a CD/DVD, or from the hard-drive. Kodi can also play multimedia from a computer over a local network (LAN), or play media streams directly from the Internet. For more information, see the [Kodi FAQ](http://kodi.wiki/index.php?title=Kodi_FAQ).

As of version 12, it can also be used to play and record live TV using a tuner, a backend server and a PVR plugin; more information about this can be found on the [Kodi wiki](http://kodi.wiki/?title=PVR).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Autostarting at boot or ondemand](#Autostarting_at_boot_or_ondemand)
        *   [2.1.1 Kodi-standalone-service](#Kodi-standalone-service)
        *   [2.1.2 Xsession with LightDM](#Xsession_with_LightDM)
        *   [2.1.3 Socket activation](#Socket_activation)
        *   [2.1.4 Start from remote control with LIRC / irexec](#Start_from_remote_control_with_LIRC_.2F_irexec)
    *   [2.2 Sharing a database across multiple nodes](#Sharing_a_database_across_multiple_nodes)
        *   [2.2.1 Setup an NFS server](#Setup_an_NFS_server)
        *   [2.2.2 Install and setup the MySQL server](#Install_and_setup_the_MySQL_server)
        *   [2.2.3 Setup Kodi to use the MySQL library and the NFS exports](#Setup_Kodi_to_use_the_MySQL_library_and_the_NFS_exports)
            *   [2.2.3.1 Setup Kodi to use the common MySQL database](#Setup_Kodi_to_use_the_common_MySQL_database)
            *   [2.2.3.2 Setup network shares](#Setup_network_shares)
        *   [2.2.4 Cloning the configuration to other nodes on the network](#Cloning_the_configuration_to_other_nodes_on_the_network)
    *   [2.3 Using a remote control](#Using_a_remote_control)
        *   [2.3.1 MCE remote with Lirc and Systemd](#MCE_remote_with_Lirc_and_Systemd)
        *   [2.3.2 HDMI-CEC with Pulse Eight USB-CEC](#HDMI-CEC_with_Pulse_Eight_USB-CEC)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 Fixing the Wunderground Weather Add-on](#Fixing_the_Wunderground_Weather_Add-on)
    *   [3.2 Fullscreen mode stretches Kodi across multiple displays](#Fullscreen_mode_stretches_Kodi_across_multiple_displays)
    *   [3.3 Video tearing on Intel HD Graphics](#Video_tearing_on_Intel_HD_Graphics)
    *   [3.4 Slowing down CD/DVD drive speed](#Slowing_down_CD.2FDVD_drive_speed)
    *   [3.5 Use port 80 for webserver](#Use_port_80_for_webserver)
    *   [3.6 Using ALSA](#Using_ALSA)
    *   [3.7 Soft subtitles not displaying](#Soft_subtitles_not_displaying)
    *   [3.8 H.264 playback is using only a single core](#H.264_playback_is_using_only_a_single_core)
    *   [3.9 Raspberry Pi](#Raspberry_Pi)
*   [4 See also](#See_also)

## Installation

**Note:** There are device specific packages on Arch Linux ARM. While they should work out of the box on the specific device, they are NOT necessarily compatible with the kodi package!

[Install](/index.php/Install "Install") the [kodi](https://www.archlinux.org/packages/?name=kodi) package. Be sure to install the optional dependencies listed by pacman that apply to your specific use-case.

## Configuration

### Autostarting at boot or ondemand

The [kodi](https://www.archlinux.org/packages/?name=kodi) package supplies a stand-alone wrapper script `/usr/bin/kodi-standalone` that allows a minimal system to run the application without a full blown DE. There are several methods to enable it described below.

**Warning:** Select **only one** of the methods listed below.

#### Kodi-standalone-service

The [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/)<sup><small>AUR</small></sup> package provides `kodi.service` and creates the needed user to run Kodi in standalone mode. This is a drop-in replacement of the package-legacy systemd service and post install script which Arch developers have removed from the package when the Xorg package updated to 1.16-1 (see [this commit](https://projects.archlinux.org/svntogit/community.git/commit/trunk?h=packages/xbmc&id=9763c6d32678f3a3f45c195bfae92eee209d504f)). Functionally, there is no difference.

[Start](/index.php/Start "Start") `kodi.service` and [enable](/index.php/Enable "Enable") it to run at boot time.

**Note:**

*   The Xorg video driver for your specific hardware is an assumed dependency.
*   No additional configuration is required.

#### Xsession with LightDM

**Note:** This assumes that the user has created an kodi user on the system and that the following file is present as described.

 `/etc/X11/Xwrapper.config`  `needs_root_rights = yes` 

To use LightDM with automatic login, see [LightDM#Enabling autologin](/index.php/LightDM#Enabling_autologin "LightDM"). _Kodi_ includes `kodi.desktop` as [xsession](/index.php/Xsession "Xsession").

 `/etc/lightdm/lightdm.conf` 

```
[LightDM]
minimum-vt=1
run-directory=/run/lightdm

[SeatDefaults]
session-wrapper=/etc/lightdm/Xsession
pam-service=lightdm-autologin
autologin-user=kodi
autologin-user-timeout=0
user-session=kodi
```

#### Socket activation

Socket activation can be used to start Kodi when the user starts a remote control app or on a connection to Kodi's html control port. Start listening with _systemctl start kodi@user.socket_ (replace _user_ with the user running Kodi to be started as).

The [kodi-standalone-socket-activation](https://aur.archlinux.org/packages/kodi-standalone-socket-activation/)<sup><small>AUR</small></sup> package provides `kodi@.service` and `kodi@.socket` which can be used to run Kodi in standalone mode listening on port 8082. Depending on the setup, one may want to change the port in _kodi@.socket_. This can be done by manually using the following systemd files.

 `/etc/systemd/system/kodi@.service` 

```
[Unit]
Description=Launch Kodi on main display

[Service]
Type=oneshot
Environment=DISPLAY=:0.0
Nice=-1
ExecStart=/usr/bin/su %i /usr/bin/kodi
ExecStartPost=/usr/bin/bash -c "sleep 15 && systemctl start kodi@%i.socket"

[Install]
WantedBy=multi-user.target
```

 `/etc/systemd/system/kodi@.socket` 

```
[Unit]
Conflicts=kodi@%i.service

[Socket]
# listen for WOL packets
#ListenDatagram=9

# change this to Kodi's http control port
ListenStream=8082

[Install]
WantedBy=sockets.target
```

#### Start from remote control with LIRC / irexec

With the help of the packages [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/)<sup><small>AUR</small></sup> and [lirc](https://www.archlinux.org/packages/?name=lirc) you can setup a configuration where you can start Kodi by pressing a key on your remote. This can be useful on a Raspberry Pi if you want to have it running 24/7 but do not want Kodi to be open 24/7, for instance if you use the Pi as Wifi-Access Point and PVR-Client. This way you can close Kodi and allow your PVR-Server to suspend/hibernate but still have your Wifi accessible - and start Kodi again without the need of a keyboard.

You need to have a working setup of [LIRC](/index.php/LIRC "LIRC"), the package [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/)<sup><small>AUR</small></sup> has to be installed.

Generate the file `/var/lib/kodi/.lircrc` with the following content:

 `/var/lib/kodi/.lircrc` 

```

begin
prog = irexec
remote = devinput
button = KEY_MEDIA
config = pgrep kodi-standalone || /usr/bin/kodi-standalone -l /run/lirc/lircd
repeat = 0
end

```

Adopt `button` to whatever button on your remote you want to assign to start Kodi. You can use irw ([LIRC#Testing the Remote](/index.php/LIRC#Testing_the_Remote "LIRC")) to find out the correct values for `remote` and `button`.

Next copy `kodi.service` from `/usr/lib/systemd/system/` to `/etc/systemd/system/` and change the line

```
ExecStart = /usr/bin/kodi-standalone -l /run/lirc/lircd

```

to

```
ExecStart = /usr/bin/irexec

```

At last start and enable the service:

```
# systemctl enable kodi.service
# systemctl start kodi.service

```

### Sharing a database across multiple nodes

One can easily configure Kodi to share a single media library (video and music). The advantage of this is that key metadata are stored in one place, and are shared/updated by all nodes on the network. For example, users of this setup can:

*   Stop watching a movie or show in one room then finish watching it in another room automatically.
*   Share watched and unwatched status for media on all nodes.
*   Simplify the setup with only a single library to maintain.

Several key things are needed for this to work:

*   Network exposed media (via protocols that Kodi can read, e.g. NFS or Samba).
*   A MySQL server.

**Note:** The following guide is only an example of one configuration and is not meant to be limiting but illustrative. Key steps are shown but a detailed discussion is not offered.

These assumptions are used for the guide, substitute to reflect your setup:

*   The media is located under following mount points: `/mnt/tv-shows` `/mnt/movies` `/mnt/music`.
*   The network addresses of all nodes are within the 192.168.0.* subnet range.
*   The user wishes to use NFSv4 exports.
*   The IP address of the machine running both the NFS exports and the MySQL database is 192.168.0.105.
*   Each Kodi box is referred to as a node.
*   The Linux user running Kodi is 'kodi' on all nodes.

For additional info, refer to the [official Kodi wiki](http://kodi.wiki/index.php?title=HOW-TO:Share_libraries_using_MySQL/Setting_up_MySQL#tab=Arch_Linux).

#### Setup an NFS server

This section provides an example using NFS exports (NFSv4), but as mentioned above, any protocol that Kodi can read is acceptable.

**Note:** Users only need one box on the LAN to serve the content, therefore, do not repeat this for each node. The following example assumes the user is running Arch Linux, but any NFS server will work, be it Linux or BSD, etc.

The NFS server is provided by [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) and this only needs to be installed on the box serving up the content.

Setup the shares:

```
# mkdir -p /srv/nfs/{tv-shows,movies,music}
# mount --bind /mnt/tv-shows /srv/nfs/tv-shows
# mount --bind /mnt/movies /srv/nfs/movies
# mount --bind /mnt/music /srv/nfs/music

```

Add the corresponding entries for these bind mounts to `/etc/fstab`:

```
...

/mnt/tv-shows /srv/nfs/tv-shows none bind 0 0
/mnt/movies /srv/nfs/movies none bind 0 0
/mnt/music /srv/nfs/music none bind 0 0

```

Share the content in `/etc/exports`:

```
/srv/nfs 192.168.0.0/24(ro,fsid=0,no_subtree_check)
/srv/nfs/tv-shows 192.168.0.0/24(ro,no_subtree_check,insecure)
/srv/nfs/movies 192.168.0.0/24(ro,no_subtree_check,insecure)
/srv/nfs/music 192.168.0.0/24(ro,no_subtree_check,insecure)

```

**Tip:** This example sets-up read-only exports. See `man exports` for additional options and configurations.

Whenever changes are made to `/etc/exports`, always refresh the exports:

```
# exportfs -rav

```

[Start](/index.php/Start "Start") `rpcbind.service` and `nfs-server.service` and [enable](/index.php/Enable "Enable") them to start automatically.

Optionally check with:

```
# showmount -e localhost
Export list for localhost:
/srv/nfs/tv-shows 192.168.0.0/24
/srv/nfs/movies 192.168.0.0/24
/srv/nfs/music 192.168.0.0/24

```

**Note:** If the box is using a firewall, ensure that it is not blocking connections. This is beyond the scope of this article.

#### Install and setup the MySQL server

The box running the library needs to be available 24/7 and is commonly the same box that holds the media.

**Note:** The following example assumes the user is running Arch Linux, but any MySQL server will work, be it Linux or BSD, etc.

The MySQL server is provided by [mariadb](https://www.archlinux.org/packages/?name=mariadb) and this only needs to be installed on one box that all nodes can access.

[Start](/index.php/Start "Start") `mysqld.service` and [enable](/index.php/Enable "Enable") it to run at boot time.

First time setup:

```
# mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
# mysql_secure_installation
   <<follow the in-script prompts and answer "Y" to all the questions>>
$ mysql -u root -p
   <<enter the mysqld root password assigned in the first step>>
MariaDB [(none)]> CREATE USER 'kodi'@'localhost' IDENTIFIED BY 'kodi';
MariaDB [(none)]> GRANT ALL ON *.* TO 'kodi';
MariaDB [(none)]> \q

```

No other setup to the MySQL server should be needed.

**Note:** If the box is using a firewall, ensure that it is not blocking connections. This is beyond the scope of this article.

#### Setup Kodi to use the MySQL library and the NFS exports

Since this example makes use of NFS shares, an optional dependency of Kodi is now required to access them. Ensure that each of the Kodi nodes has [libnfs](https://www.archlinux.org/packages/?name=libnfs) installed.

##### Setup Kodi to use the common MySQL database

To tell Kodi to use the common database, insure that Kodi is not running, then create the following file:

 `~/.kodi/userdata/advancedsettings.xml` 

```
<advancedsettings>
  <videodatabase>
    <type>mysql</type>
    <host>192.168.0.105</host>
    <port>3306</port>
    <user>kodi</user>
    <pass>kodi</pass>
  </videodatabase>

  <musicdatabase>
    <type>mysql</type>
    <host>192.168.0.105</host>
    <port>3306</port>
    <user>kodi</user>
    <pass>kodi</pass>
  </musicdatabase>

  <videolibrary>
    <importwatchedstate>true</importwatchedstate>
    <importresumepoint>true</importresumepoint>
  </videolibrary>
</advancedsettings>

```

**Tip:** If using [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/)<sup><small>AUR</small></sup>, the default for the profile is /var/lib/kodi/.kodi and be sure to chown the newly created file to the kodi user and group, i.e. `# chown -R kodi:kodi /var/lib/kodi`

##### Setup network shares

**Warning:** This only needs to be done once, on only one of the nodes. Once completed, configuration of subsequent nodes is a drop-in operation of ~/.kodi/userdata/advancedsettings.xml; no other configuration is needed!

**Note:** Even if Kodi is running on the same box that is also running the NFS exports and MySQL server, one _MUST_ setup the media using the nfs shares only!

Load Kodi and define the network shares that correspond to the exports by browsing to the following within the interface:

```
Video>Files>Add Videos>Browse>Network Filesystem(NFS)

```

After a few seconds, the IP address corresponding to the NFS server should appear.

Select "/srv/nfs/tv-shows" from the list of share and then "OK" from the menu on the right. Assign this share the category of "TV Shows" to setup the appropriate scraper and to populate the MySQL database with the correct metadata.

Repeat this browsing process for the "movies" and "music" and then exit Kodi once properly configured. At this point, the MySQL tables should have been created.

#### Cloning the configuration to other nodes on the network

Setting up another Kodi node on the network to use this library is trivial. Simply copy `~/.kodi/userdata/advancedsettings.xml` to that box and restart Kodi.

**Note:** There is NO need to do any other setup steps to define the sources since the nfs exports, the metadata for the programming, any stop/start times, view status, etc. are all stored in the MySQL tables. If problems are encountered after this file is added to the profile directory and after Kodi is restarted, it is recommended to simply re-create the Kodi profile on that node, and again copy over the advancedsettings.xml file. This way, only a trivial amount of configuration to the GUI itself is required which is often easier than troubleshooting conflicting local databases, sources, and the like.

### Using a remote control

As Kodi is geared toward being a remote-controlled media center; any PC with a supported IR receiver/remote, can use remote using [LIRC](/index.php/LIRC "LIRC") or using the native kernel supported modules. To work properly with Kodi, a file will be required that maps the lirc events to Kodi keypresses. Create an [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML") file at `~/.kodi/userdata/Lircmap.xml` (note the capital 'L').

**Note:** Users running Kodi from the included service file will find the kodi home (~) under `/var/lib/kodi` and should substitute this in for the shortcut above. Also make sure that if creating this file as the root user, it gets proper ownership as kodi:kodi when finished.

Lircmap.xml format is as follows:

```
<lircmap>
  <remote device="devicename">
      <XBMC_button>LIRC_button</XBMC_button>
      ...
  </remote>
</lircmap>
```

*   **Device Name** is whatever LIRC calls the remote. This is set using the **Name** directive in lircd.conf and can be viewed by running `$ irw` and pressing a few buttons on the remote. IRW will report the name of the button pressed and the name of the remote will appear on the end of the line.

*   **XBMC_button** is the name of the button as defined in [keymap.xml](http://kodi.wiki/index.php?title=Keymap.xml).

*   **LIRC_button** is the name as defined in `lircd.conf`. If lircd.conf was autogenerated using `# irrecord`, these are the names selected for the buttons. Refer back to [LIRC](/index.php/LIRC "LIRC") for more information.

*   A very thorough [Lircmap.xml](http://kodi.wiki/index.php?title=Lircmap.xml) page over at the [Kodi Wiki](http://kodi.wiki/index.php?title=Main_Page) should be consulted for more help and information on this subject as this is out of scope of this article.

#### MCE remote with Lirc and Systemd

Install [lirc](https://www.archlinux.org/packages/?name=lirc) and link the mce config:

```
# ln -s /usr/share/lirc/mceusb/lircd.conf.mceusb /etc/lirc/lircd.conf

```

Then, make sure the remote is using the lirc protocol:

```
$ cat /sys/class/rc/rc0/protocols

```

If not, issue:

```
# echo lirc > /sys/class/rc/rc0/protocols

```

A udev rule can be added to make lirc the default. A write rule does not seem to work, so a simple RUN command can be executed instead.

 `/etc/udev/rules.d/99-lirc.rules`  `KERNEL=="rc*", SUBSYSTEM=="rc", ATTR{protocols}=="*lirc*", RUN+="/bin/sh -c 'echo lirc > $sys$devpath/protocols'"` 

Finally, [enable](/index.php/Enable "Enable") and start `lirc.socket`.

This should give a fully working mce remote.

#### HDMI-CEC with Pulse Eight USB-CEC

An elegant way of getting remote functions in Kodi is using [CEC](https://en.wikipedia.org/wiki/Consumer_Electronics_Control#CEC "wikipedia:Consumer Electronics Control"), a protocol that is part of the HDMI specification. Most modern TVs support CEC, although some manufacturers advertise the feature under other names. Apart from a CEC-enabled TV some hardware that takes the CEC signals coming from the TV and present them in a way that Kodi can understand is also needed. One such device is the [USB-CEC adapter](http://www.pulse-eight.com/store/products/104-usb-hdmi-cec-adapter.aspx) from Pulse Eight. Hooking up the USB-CEC is pretty simple, but in order for it to work in Arch we have to do a few things.

Install `libcec`.

When connected, the USB-CEC's `/dev` entry (usually `/dev/ttyACM*`) will default to being owned by the `uucp` group, so in order to use the device the user running Kodi needs to belong to that group. The user also needs to belong to the `lock` group, otherwise Kodi will be unable to connect to the device. To add a user to both groups, run

```
# usermod -aG uucp,lock [username]

```

If more than one user uses Kodi, repeat the command for all those users. If, for example, one is using `kodi-standalone`, the relevant command is

```
# usermod -aG uucp,lock kodi

```

Remember that modifying the groups of any logged in users means those users need to log out and login again in order for the changes to take effect.

**Note:** Trying to use the USB-CEC without belonging to above groups may lead to problems, including Kodi crashes, so make sure the correct user belongs to both groups.

## Tips and Tricks

### Fixing the Wunderground Weather Add-on

The wunderground now requires users to have an API key in order to receive weather data. An API key is available free of charge for kodi users. To obtain a key, and to configure the add-on follow these steps:

1.  Sign up for an API key at [wunderground](http://www.wunderground.com/weather/api/d/login.html)'s automated system.
2.  Format the key for kodi's wunderground.py script (it expects the key to be reversed and base64 encoded, see below).
3.  Enter the formatted key into **WAIK** variable in `~/.kodi/addons/weather.wunderground/resources/lib/wunderground.py`

To reverse and base64 encode the API key, run this two-liner using your own API key in the "key" variable.

```
$ key=9cc49125b91eb85a
$ echo $key|rev|base64
YTU4YmUxOWI1MjE5NGNjOQo=

```

For this example key, the first few lines of `~/.kodi/addons/weather.wunderground/resources/lib/wunderground.py` would look like this:

```
# -*- coding: utf-8 -*-

import urllib2, gzip, base64
from StringIO import StringIO

WAIK             = 'YTU4YmUxOWI1MjE5NGNjOQo='

```

### Fullscreen mode stretches Kodi across multiple displays

For a multi-monitor setup, Kodi may default to stretching across all screens. One can restrict the fullscreen mode to one display by setting the environment variable SDL_VIDEO_FULLSCREEN_HEAD to the number of the desired target display. For example, having Kodi show up on display 0, add the following line to the Kodi user's `~/.bashrc` configuration:

```
SDL_VIDEO_FULLSCREEN_HEAD=0

```

**Note:** Mouse cursor will be held inside screen with Kodi.

### Video tearing on Intel HD Graphics

Users observing tearing when watching a movie try this: [https://bbs.archlinux.org/viewtopic.php?id=176651](https://bbs.archlinux.org/viewtopic.php?id=176651)

### Slowing down CD/DVD drive speed

The `eject` program from the `util-linux` package does a nice job for this, but its setting is cleared as soon as the media is changed.

This udev-rule reduces the speed permanently:

 `/etc/udev/rules.d/dvd-speed.rules`  `KERNEL=="sr0", ACTION=="change", ENV{DISK_MEDIA_CHANGE}=="1", RUN+="/usr/bin/eject -x 2 /dev/sr0"` 

Replace `sr0` with the device name of the optical drive. Replace `-x 2` with `-x 4` if the preference is 4x-speed instead of 2x-speed.

After creating the file, reload the udev rules with

```
# udevadm control --reload

```

### Use port 80 for webserver

Kodi has a webservice that allows interaction through a web-interface. By default, it uses port `8080` as `80` requires root privileges. Use the following to permit it to use low port numbers:

```
 # setcap 'cap_net_bind_service=+ep' /usr/lib/kodi/kodi.bin

```

[Restart](/index.php/Restart "Restart") `kodi.service` and set port `80` in the configuration menu (_Services->Webserver->Port_).

### Using ALSA

If [PulseAudio](/index.php/PulseAudio "PulseAudio") does not work properly, try using ALSA directly by starting Kodi with the `AE_SINK=ALSA` environment variable.

### Soft subtitles not displaying

The [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package is used to extract the subtitles.

### H.264 playback is using only a single core

**Tip:** By default, press `O` during playback to show codec information and CPU usage. More information about this overlay can be found [here](http://kodi.wiki/view/Codecinfo).

If your setup doesn't or can't make use of hardware acceleration, disable it and explicitly set video decoding to software. This is because [H.264 decoding is only multithreaded when video decoding is set to software](http://forum.kodi.tv/showthread.php?tid=170084&pid=1789661#pid1789661). To achieve this, go to `System Settings` and then to `Video`. Set the `settings level` to `Advanced` or `Expert` and go to `Acceleration`. There, set `Decoding method` to `software`.

### Raspberry Pi

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** udev rule has anything but a statisfactory explanation for chmod 0666 (Discuss in [Talk:Kodi#](https://wiki.archlinux.org/index.php/Talk:Kodi))

Kodi runs smoothly on both the Raspberry Pi (RPi) and the RPi 2\. Some helpful tips to consider:

*   [Install](/index.php/Install "Install") the _kodi-rbp_ package instead of _kodi_ from the [Arch Linux ARM repository](http://archlinuxarm.org/packages).
*   This package ships with a systemd service to run in standalone mode.
*   The memory reserved for GPU is 64 MB by default. This is insufficient for GPU accelerated HD video playback. Users can increase this value via a simple edit to the `gpu_mem` tag in `/boot/config.txt`. A value of at least 128 MB is recommended.
*   Install _omxplayer-git_, _xorg-xrefresh_ and _xorg-xset_ to get hardware acceleration working.
*   Add the udev rule `SUBSYSTEM=="tty", KERNEL=="tty0", GROUP="tty", MODE="0666"` to `/etc/udev/rules.d/raspberrypi.rules` to enable typing with a physical keyboard.

## See also

*   [Kodi Wiki](http://kodi.wiki/index.php?title=Main_Page) - Excellent resource with much information about Arch Linux specifically
*   [http://superrepo.org/](http://superrepo.org/) - xbmc Plug-in library
*   [http://www.hdpfans.com/thread-329076-1-1.html](http://www.hdpfans.com/thread-329076-1-1.html) - Kodi/xbmc Chinese plug-in library installation method
*   [https://github.com/taxigps/xbmc-addons-chinese](https://github.com/taxigps/xbmc-addons-chinese) - xbmc-addons-chinese

**Note:** xbmc-addons-chinese:Addon scripts, plugins, and skins for XBMC Media Center. Special for chinese laguage.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kodi&oldid=412116](https://wiki.archlinux.org/index.php?title=Kodi&oldid=412116)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")