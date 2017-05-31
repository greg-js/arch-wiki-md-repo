Kodi (formerly known as XBMC) is an award-winning free and open source (GPL) software media player and entertainment hub that can be installed on Linux, OSX, Windows, iOS and Android, featuring a 10-foot user interface for use with televisions and remote controls. These can all be played directly from a CD/DVD, or from the hard-drive. Kodi can also play multimedia from a computer over a local network (LAN), or play media streams directly from the Internet. It can also be used to play and record live TV using a tuner, a backend server and a PVR plugin; more information about this can be found on the [Kodi wiki](http://kodi.wiki/?title=PVR).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Autostarting at boot or starting on-demand](#Autostarting_at_boot_or_starting_on-demand)
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
        *   [2.3.1 Using the Android or iOS app](#Using_the_Android_or_iOS_app)
        *   [2.3.2 Using a physical remote control](#Using_a_physical_remote_control)
    *   [2.4 HDMI-CEC with Pulse Eight USB-CEC](#HDMI-CEC_with_Pulse_Eight_USB-CEC)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 Keep a log of what is watched](#Keep_a_log_of_what_is_watched)
    *   [3.2 CLI tool for kodi](#CLI_tool_for_kodi)
    *   [3.3 Enable Hardware video acceleration](#Enable_Hardware_video_acceleration)
    *   [3.4 Slowing down CD/DVD drive speed](#Slowing_down_CD.2FDVD_drive_speed)
    *   [3.5 Use port 80 for webserver](#Use_port_80_for_webserver)
    *   [3.6 Using ALSA](#Using_ALSA)
    *   [3.7 Raspberry Pi (all generations)](#Raspberry_Pi_.28all_generations.29)
    *   [3.8 TV is not detected unless powered on first](#TV_is_not_detected_unless_powered_on_first)
        *   [3.8.1 Run kodi in a window manager](#Run_kodi_in_a_window_manager)
        *   [3.8.2 USB DAC not working](#USB_DAC_not_working)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Accessing kodi logs](#Accessing_kodi_logs)
    *   [4.2 Fullscreen mode stretches Kodi across multiple displays](#Fullscreen_mode_stretches_Kodi_across_multiple_displays)
    *   [4.3 Video tearing on Intel HD Graphics](#Video_tearing_on_Intel_HD_Graphics)
    *   [4.4 Soft subtitles not displaying](#Soft_subtitles_not_displaying)
    *   [4.5 H.264 playback is using only a single core](#H.264_playback_is_using_only_a_single_core)
    *   [4.6 Kodi hangs on exit, fully occupying one CPU core, UI unresponsive](#Kodi_hangs_on_exit.2C_fully_occupying_one_CPU_core.2C_UI_unresponsive)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [kodi](https://www.archlinux.org/packages/?name=kodi) package. Be sure to install the optional dependencies listed by pacman that apply to your specific use-case.

**Note:** Users of Arch ARM should be aware that several different kodi packages with specific hardware support are available.

## Configuration

### Autostarting at boot or starting on-demand

The [kodi](https://www.archlinux.org/packages/?name=kodi) package supplies two binaries for two different use cases:

1.  `/usr/bin/kodi` is meant to be run by any user on a on-demand basis. Use it like any other program on the system.
2.  `/usr/bin/kodi-standalone` is meant to be run by an unprivileged user.

Setting up the system and running the standalone binary is advantageous for several reasons:

1.  An unprivileged user cannot access a shell by definition.
2.  Running without a full blown DE is lighter and more simplistic.
3.  When paired with a systemd unit (or equivalent, see below), this make the box on which kodi is running more like an appliance and very robust.

There are several methods to it this described below.

**Warning:** Select **only one** of the methods listed below.

#### Kodi-standalone-service

The [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/) package provides `kodi.service` and automatically creates the unprivileged user to run Kodi in standalone mode. Although the correct [driver](/index.php/Xorg#Driver_installation "Xorg") is an assumed dependency, no extra Xorg packages are needed. [Start](/index.php/Start "Start") `kodi.service` and [enable](/index.php/Enable "Enable") it to run at boot time. No additional configuration should be required for most users, however, if `kodi.service` fails to start, see [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

**Note:**

*   The kodi user is unprivileged meaning it cannot login (default shell is `/usr/bin/nologin`).
*   The home directory for the kodi user created is `/var/lib/kodi` not `/home/kodi`.

**Warning:** Users of Arch ARM should not attempt to install this package as breakage will occur!

#### Xsession with LightDM

**Note:** This assumes that the user has created an kodi user named kodiuser on the system and that the following file is present as described.

**Note:** lightdm does not pull in an X server as a required dependency, it is optional. The X server listed as an optional dependency (xephyr) does not work when run as root by lightdm.service ([Bug to have optional dependency modified](https://bugs.archlinux.org/?string=52067)) ([Upstream Bug](https://bugs.launchpad.net/lightdm/+bug/852577)). Install [xorg-server](/index.php/Xorg#Installation "Xorg").

To use LightDM with automatic login, see [LightDM#Enabling autologin](/index.php/LightDM#Enabling_autologin "LightDM") and [LightDM#Enabling interactive passwordless login](/index.php/LightDM#Enabling_interactive_passwordless_login "LightDM"). *Kodi* includes `kodi.desktop` as [xsession](/index.php/Xsession "Xsession").

 `/etc/lightdm/lightdm.conf` 
```
[Seat:seat0]
pam-service=lightdm-autologin
autologin-user=kodiuser
autologin-user-timeout=0
user-session=kodi
```

#### Socket activation

Socket activation can be used to start Kodi when the user starts a remote control app or on a connection to Kodi's html control port. Start listening with *systemctl start kodi@user.socket* (replace *user* with the user running Kodi to be started as).

The [kodi-standalone-socket-activation](https://aur.archlinux.org/packages/kodi-standalone-socket-activation/) package provides `kodi@.service` but not `kodi@.socket`. Depending on the setup, one may want to change the port in *kodi@.socket*. This can be done by manually using the following systemd files.

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

Kodi can be configured to start via a key press. Users will need [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/) and [lirc](https://www.archlinux.org/packages/?name=lirc). This can be useful on setups running 24/7 and having kodi up on demand.

See the corresponding [LIRC](/index.php/LIRC "LIRC") article and create a functional setup with a remote. Also, the package [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/) has to be installed.

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

Adopt `button` to whatever button on the remote is to start Kodi. One can use *irw* (see [LIRC#Usage](/index.php/LIRC#Usage "LIRC")) to find out the correct values for `remote` and `button`.

Next copy `kodi.service` from `/usr/lib/systemd/system/` to `/etc/systemd/system/` and change the line

```
ExecStart = /usr/bin/kodi-standalone -l /run/lirc/lircd

```

to

```
ExecStart = /usr/bin/irexec

```

[Start](/index.php/Start "Start") `kodi.service` and [enable](/index.php/Enable "Enable") it to run at boot time.

### Sharing a database across multiple nodes

If multiple PCs on the same network are running Kodi, they can be configured to share a single media library (video and music). The advantage of this is that key metadata are stored in one place, and are shared/updated by all nodes on the network. For example, users of this setup can:

*   Stop watching a movie or show in one room then finish watching it in another room automatically.
*   Share watched and unwatched status for media on all nodes.
*   Simplify the setup with only a single library to maintain.

Several key things are needed for this to work:

*   Network exposed media (via protocols that Kodi can read, e.g. NFS or Samba).
*   A MySQL server (Arch uses [mariadb](https://www.archlinux.org/packages/?name=mariadb)).

**Note:** The following guide is only an example of one configuration and is not meant to be limiting but illustrative. Key steps are shown but a detailed discussion is not offered.

These assumptions are used for the guide, substitute to reflect your setup:

*   The media is located under following mount points: `/mnt/tv-shows` `/mnt/movies` `/mnt/music`.
*   The network addresses of all nodes are within the 192.168.0.* subnet range.
*   The IP address of the machine running both the NFS exports and the MySQL database is 192.168.0.105.
*   Each Kodi box is referred to as a node.
*   The Linux user running Kodi is 'kodi' on all nodes.

For additional info, refer to the [official Kodi wiki](http://kodi.wiki/index.php?title=HOW-TO:Share_libraries_using_MySQL/Setting_up_MySQL#tab=Arch_Linux).

#### Setup an NFS server

This section provides an example using NFS exports, but as mentioned above, any protocol that Kodi can read is acceptable.

**Warning:** Kodi is using [libnfs](https://www.archlinux.org/packages/?name=libnfs) to access NFS shares which only supports NFSv3 (see [#37](https://github.com/sahlberg/libnfs/issues/37) and [#156](https://github.com/sahlberg/libnfs/issues/156)). Therefore do not setup a NFSv4-only server or Kodi will only be able to list the shares but cannot access them.

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
/mnt/tv-shows /srv/nfs/tv-shows none bind 0 0
/mnt/movies   /srv/nfs/movies   none bind 0 0
/mnt/music    /srv/nfs/music    none bind 0 0

```

Share the content in `/etc/exports`:

```
/srv/nfs          192.168.0.0/24(ro,fsid=0,no_subtree_check)
/srv/nfs/tv-shows 192.168.0.0/24(ro,no_subtree_check,insecure)
/srv/nfs/movies   192.168.0.0/24(ro,no_subtree_check,insecure)
/srv/nfs/music    192.168.0.0/24(ro,no_subtree_check,insecure)

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

```

```
$ mysql -u root -p
   <<enter the mysqld root password assigned in the first step>>
MariaDB [(none)]> CREATE USER 'kodi' IDENTIFIED BY 'kodi';
MariaDB [(none)]> GRANT ALL ON *.* TO 'kodi';
MariaDB [(none)]> flush privileges;
MariaDB [(none)]> \q

```

One can optionally disable binary logging if the mysql server is only used for kodi by editing `/etc/mysql/my.cnf` and commenting the following line:

```
#log-bin=mysql-bin

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

**Tip:** If using [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/), the default for the profile is `/var/lib/kodi/.kodi` and be sure to chown the newly created file to the kodi user and group, i.e. `chown -R kodi:kodi /var/lib/kodi`

##### Setup network shares

Load Kodi and define the network shares that correspond to the exports by browsing to the following within the interface:

```
Video>Files>Add Videos>Browse>Network Filesystem(NFS)

```

After a few seconds, the IP address corresponding to the NFS server should appear.

Select `/srv/nfs/tv-shows` from the list of share and then "OK" from the menu on the right. Assign this share the category of "TV Shows" to setup the appropriate scraper and to populate the MySQL database with the correct metadata.

Repeat this browsing process for the "movies" and "music" and then exit Kodi once properly configured. At this point, the MySQL tables should have been created.

**Note:** Even if Kodi is running on the same box that is also running the NFS exports and MySQL server, one **must** setup the media using the nfs shares only!

#### Cloning the configuration to other nodes on the network

To set up another Kodi node on the network to use this library, simply copy `~/.kodi/userdata/advancedsettings.xml` to that box and restart Kodi.

**Note:** There is NO need to copy any other files or to do any other setup steps on the new kodi node. The nfs exports, the metadata for the programming, any stop/start times, view status, etc. are all stored in the MySQL tables.

### Using a remote control

As Kodi is geared toward being a remote-controlled media center via an official app, physical remote control, or USB/bluetooth keyboard/mouse.

#### Using the Android or iOS app

Both Android and iOS users can use the official app (currently free of charge) to control kodi once it is correctly setup to do so. Steps to configure both Kodi and the app are detailed on the [Official Kodi Remote](http://kodi.wiki/view/Official_Kodi_Remote) page.

#### Using a physical remote control

Any PC with a supported IR receiver/remote, can use remote using [LIRC](/index.php/LIRC "LIRC") or using the native kernel supported modules. Configuring specific remotes with lirc is covered on the [LIRC](/index.php/LIRC "LIRC") article.

To work properly with Kodi, a file will be required that maps the lirc events to Kodi keypresses. Create an [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML") file at `~/.kodi/userdata/Lircmap.xml` (note the capital 'L').

**Note:** Users running Kodi started with [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/) will find the kodi home (~) under `/var/lib/kodi` and should substitute this in for the shortcut above. Also make sure that if creating this file as the root user, it gets proper ownership as kodi:kodi when finished.

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

*   A very thorough [Lircmap.xml page](http://kodi.wiki/index.php?title=Lircmap.xml) hosted on the [Kodi Wiki](http://kodi.wiki/index.php?title=Main_Page) should be consulted for more help and information on this subject as this is out of scope of this article.

### HDMI-CEC with Pulse Eight USB-CEC

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

### Keep a log of what is watched

Keep track of every video watched on kodi with [kodi-logger](https://aur.archlinux.org/packages/kodi-logger/).

### CLI tool for kodi

A powerful CLI tool for use with kodi is [texturecache](https://aur.archlinux.org/packages/texturecache/). Users can accomplish many task from library management to querying what is currently playing.

### Enable Hardware video acceleration

Enable and configure [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") to speed up playback performance.

Restart Kodi and enable the hardware backend(s) in Playback under Settings.

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

[Restart](/index.php/Restart "Restart") `kodi.service` and set port `80` in the configuration menu (*Services->Webserver->Port*).

### Using ALSA

If [PulseAudio](/index.php/PulseAudio "PulseAudio") does not work properly, try using ALSA directly by starting Kodi with the `AE_SINK=ALSA` environment variable. The Kodi wiki for NUC devices provides [instructions](http://kodi.wiki/view/HOW-TO:Install_Kodi_on_an_Intel_NUC#disable_PulseAudio)

### Raspberry Pi (all generations)

Kodi runs smoothly on the Raspberry Pi (RPi), RPi2, and RPi3\. Some helpful tips to consider:

*   [Install](/index.php/Install "Install") either the *kodi-rbp* (stable) or *kodi-rbp-git* (dev) package instead of *kodi* from the [Arch Linux ARM repository](http://archlinuxarm.org/packages).
*   This package ships with a systemd service to run in standalone mode.
*   The memory reserved for GPU is 64 MB by default. This is insufficient for GPU accelerated HD video playback. Users can increase this value via a simple edit to the `gpu_mem` tag in `/boot/config.txt`. A value of at least 128 MB is recommended for RPi version 1 while a value of 256 is recommended for RPi2 and 3.

### TV is not detected unless powered on first

Some TVs (LG brand for example) only report their capabilities via EDID through HDMI when powered on **before** the RPi. The effects of this can manifest in one of two ways:

1.  Despite being connected, the TV will be unable to detect a signal from the HDMI source until the RPi is rebooted.
2.  The signal will be detected but incorrectly by the RPi to the point of the GUI looking distorted when compared to having the TV on first, then rebooting the RPi.

Both conditions are easily fixed. See: [Raspberry_Pi_FAQ#TV_is_not_detected_unless_powered_on_first](http://kodi.wiki/view/Raspberry_Pi_FAQ#TV_is_not_detected_unless_powered_on_first).

#### Run kodi in a window manager

Users running kodi in a [Window manager](/index.php/Window_manager "Window manager") may see a black screen at exit. To fix this, try switching to another tty. A possible solution is to run kodi with this script (running as the root user):

 `kodi.sh` 
```
#!/bin/bash
kodi-standalone
sudo chvt 2 
sleep 1
sudo chvt 1

```

To make sure that [sudo](/index.php/Sudo "Sudo") does not ask for password for `chvt` add this line to `sudoers` file:

 `/etc/sudoers` 
```
*UserNameHere* ALL=NOPASSWD: /usr/bin/chvt

```

#### USB DAC not working

Users of USB DAC/sound cards may experience distorted sound/clicks/pops or no sound at all when selecting it from Audio settings. A possible fix:

Open `guisettings.xml` (it should be under `/var/lib/kodi/.kodi/userdata/` if using the supplied `kodi.service`) and change

```
<processquality default="**true**">**101**</processquality>

```

to

```
<processquality default="**false**">**100**</processquality>

```

## Troubleshooting

### Accessing kodi logs

In case of an error the first point to start investigation can be `~/.kodi/temp/kodi.log`.

### Fullscreen mode stretches Kodi across multiple displays

For a multi-monitor setup, Kodi may default to stretching across all screens. One can restrict the fullscreen mode to one display by setting the environment variable SDL_VIDEO_FULLSCREEN_HEAD to the number of the desired target display. For example, having Kodi show up on display 0, add the following line to the Kodi user's `~/.bashrc` configuration:

```
SDL_VIDEO_FULLSCREEN_HEAD=0

```

**Note:** Mouse cursor will be held inside screen with Kodi.

### Video tearing on Intel HD Graphics

Users observing tearing when watching a movie try this: [https://bbs.archlinux.org/viewtopic.php?id=176651](https://bbs.archlinux.org/viewtopic.php?id=176651)

Try a different X11 compositor like [compton](https://www.archlinux.org/packages/?name=compton) as an alternative with [Xfce](/index.php/Xfce "Xfce") which reduces video tearing. There is no essential need to install the intel driver. A tutorial how to configure compton with Xfce can be found [here](http://duncanlock.net/blog/2013/06/07/how-to-switch-to-compton-for-beautiful-tear-free-compositing-in-xfce/).

### Soft subtitles not displaying

The [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package is used to extract the subtitles.

### H.264 playback is using only a single core

**Tip:** By default, press `O` during playback to show codec information and CPU usage. More information about this overlay can be found [here](http://kodi.wiki/view/Codecinfo).

If your setup does not or cannot make use of hardware acceleration, disable it and explicitly set video decoding to software. This is because [H.264 decoding is only multithreaded when video decoding is set to software](http://forum.kodi.tv/showthread.php?tid=170084&pid=1789661#pid1789661). To achieve this, go to `System Settings` and then to `Video`. Set the `settings level` to `Advanced` or `Expert` and go to `Acceleration`. There, set `Decoding method` to `software`.

### Kodi hangs on exit, fully occupying one CPU core, UI unresponsive

This problem can arise with third-party plugins installed, there is some issue with their termination[[1]](https://www.linuxquestions.org/questions/linux-software-2/kodi-freezes-on-exit-kodi-bin-won't-die-4175588180/),[[2]](https://www.reddit.com/r/archlinux/comments/5029oo/kodi_freezes_on_exit_kodibin_wont_die/).

Workaround: find proper UI description file (*DialogButtonMenu.xml*) and tweak exit button type from internal Kodi's *Quit()* function call to sending signal from outside system to Kodi. Here is one-liner that makes modifications to any skin from your default Kodi package:

```
find /usr/share/kodi/addons/skin.* -name DialogButtonMenu.xml | xargs sudo sed -i "s%<onclick>Quit()</onclick>%<onclick>System.Exec ("killall --signal SIGHUP kodi.bin")</onclick>%"

```

## See also

*   [Kodi Wiki](http://kodi.wiki/index.php?title=Main_Page) - Excellent resource with much information about Arch Linux specifically
*   [http://superrepo.org/](http://superrepo.org/) - xbmc Plug-in library
*   [http://www.hdpfans.com/thread-329076-1-1.html](http://www.hdpfans.com/thread-329076-1-1.html) - Kodi/xbmc Chinese plug-in library installation method
*   [https://github.com/taxigps/xbmc-addons-chinese](https://github.com/taxigps/xbmc-addons-chinese) - xbmc-addons-chinese

**Note:** xbmc-addons-chinese:Addon scripts, plugins, and skins for XBMC Media Center. Special for chinese laguage.