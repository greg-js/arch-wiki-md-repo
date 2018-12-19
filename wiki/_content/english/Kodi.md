[Kodi](https://kodi.tv/) (formerly known as XBMC) is an award-winning free and open source (GPL) software media player and entertainment hub that can be installed on Linux, OSX, Windows, iOS and Android, featuring a 10-foot user interface for use with televisions and remote controls. These can all be played directly from a CD/DVD, or from the hard-drive. Kodi can also play multimedia from a computer over a local network (LAN), or play media streams directly from the Internet. It can also be used to play and record live TV using a tuner, a backend server and a PVR plugin; more information about this can be found on the [Kodi wiki](https://kodi.wiki/view/PVR).

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Running standalone](#Running_standalone)
    *   [3.1 kodi-standalone service](#kodi-standalone_service)
    *   [3.2 Xsession with LightDM](#Xsession_with_LightDM)
    *   [3.3 Socket activation](#Socket_activation)
    *   [3.4 Start from remote control with LIRC / irexec](#Start_from_remote_control_with_LIRC_/_irexec)
*   [4 Using a remote control](#Using_a_remote_control)
    *   [4.1 Using the Android or iOS app](#Using_the_Android_or_iOS_app)
    *   [4.2 Using a physical remote control](#Using_a_physical_remote_control)
    *   [4.3 HDMI-CEC](#HDMI-CEC)
*   [5 Sharing media and a centralized database across multiple nodes](#Sharing_media_and_a_centralized_database_across_multiple_nodes)
    *   [5.1 NFS server export example](#NFS_server_export_example)
    *   [5.2 Install and setup the MySQL server](#Install_and_setup_the_MySQL_server)
    *   [5.3 Setup Kodi to use the MySQL library and the NFS exports](#Setup_Kodi_to_use_the_MySQL_library_and_the_NFS_exports)
        *   [5.3.1 Setup Kodi to use the common MySQL database](#Setup_Kodi_to_use_the_common_MySQL_database)
        *   [5.3.2 Setup network shares](#Setup_network_shares)
    *   [5.4 Cloning the configuration to other nodes on the network](#Cloning_the_configuration_to_other_nodes_on_the_network)
*   [6 Tips and Tricks](#Tips_and_Tricks)
    *   [6.1 Keep a log of what is watched](#Keep_a_log_of_what_is_watched)
    *   [6.2 Speedup video playback (synchronized audio and video) up to 1.5x](#Speedup_video_playback_(synchronized_audio_and_video)_up_to_1.5x)
    *   [6.3 CLI for kodi](#CLI_for_kodi)
    *   [6.4 Hardware video acceleration](#Hardware_video_acceleration)
    *   [6.5 Adjusting CD/DVD drive speed](#Adjusting_CD/DVD_drive_speed)
    *   [6.6 Use port 80 for webserver](#Use_port_80_for_webserver)
    *   [6.7 Using ALSA](#Using_ALSA)
    *   [6.8 Audio Passthrough](#Audio_Passthrough)
        *   [6.8.1 Fix for delayed startup on wifi](#Fix_for_delayed_startup_on_wifi)
    *   [6.9 Run kodi in a window manager](#Run_kodi_in_a_window_manager)
    *   [6.10 USB DAC not working](#USB_DAC_not_working)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Accessing Kodi logs](#Accessing_Kodi_logs)
    *   [7.2 Fullscreen mode stretches Kodi across multiple displays](#Fullscreen_mode_stretches_Kodi_across_multiple_displays)
    *   [7.3 Video tearing on Intel HD Graphics](#Video_tearing_on_Intel_HD_Graphics)
    *   [7.4 Soft subtitles not displaying](#Soft_subtitles_not_displaying)
    *   [7.5 H.264 playback is using only a single core](#H.264_playback_is_using_only_a_single_core)
    *   [7.6 Kodi hangs on exit, fully occupying one CPU core, UI unresponsive](#Kodi_hangs_on_exit,_fully_occupying_one_CPU_core,_UI_unresponsive)
*   [8 See also](#See_also)

## Installation

The official stable release can be [installed](/index.php/Install "Install") via the [kodi](https://www.archlinux.org/packages/?name=kodi) package. Alternatively, recent alpha, beta, or RC builds are available from [kodi-devel](https://aur.archlinux.org/packages/kodi-devel/). Be sure to review/install optional dependencies listed by pacman to enable additional functionality.

All of the official addons in the [kodi-addons](https://www.archlinux.org/groups/x86_64/kodi-addons/) group are disabled by default and need to be enabled in Kodi's addon menu after installation.

## Running

The [kodi](https://www.archlinux.org/packages/?name=kodi) package supplies two binaries for two different use cases:

1.  `/usr/bin/kodi` is meant to be run by any user on an on-demand basis. Use it like any other program on the system.
2.  `/usr/bin/kodi-standalone` is meant to be run as the only graphical application, for example on a [HTPC](https://en.wikipedia.org/wiki/Home_theater_PC "wikipedia:Home theater PC"). See [#Running standalone](#Running_standalone) for more information.

## Running standalone

Using standalone mode is advantageous for several reasons:

1.  The default `kodi` user is unprivileged and cannot access a shell.
2.  When paired with a systemd unit (or equivalent, see below), this setup makes the box on which kodi is running more like an appliance.

**Warning:** Select **only one** of the methods listed below.

### kodi-standalone service

The [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/) package provides `kodi.service` and automatically creates the unprivileged user to run Kodi in standalone mode. Although the correct [driver](/index.php/Xorg#Driver_installation "Xorg") is an assumed dependency, no extra Xorg packages are needed.

[Start](/index.php/Start "Start") `kodi.service` and [enable](/index.php/Enable "Enable") it to run at boot time.

**Note:**

*   If `kodi.service` fails to start, see [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg").
*   The home directory for the created `kodi` user is `/var/lib/kodi/`.

### Xsession with LightDM

**Note:**

*   This assumes that a kodi user named `kodi` is on the system and that the following file is present as described.
*   [lightdm](https://www.archlinux.org/packages/?name=lightdm) does not pull in an X server as a required dependency, it is optional. The X server listed as an optional dependency ([xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr)) does not work when run as root by `lightdm.service` ([FS#52067](https://bugs.archlinux.org/task/52067), [LightDM Bug 852577](https://bugs.launchpad.net/lightdm/+bug/852577)). [Install xorg-server](/index.php/Xorg#Installation "Xorg").

To use LightDM with automatic login, see [LightDM#Enabling autologin](/index.php/LightDM#Enabling_autologin "LightDM") and [LightDM#Enabling interactive passwordless login](/index.php/LightDM#Enabling_interactive_passwordless_login "LightDM"). *Kodi* includes `kodi.desktop` as [xsession](/index.php/Xsession "Xsession").

 `/etc/lightdm/lightdm.conf` 
```
[Seat:seat0]
pam-service=lightdm-autologin
autologin-user=kodi
autologin-user-timeout=0
user-session=kodi
```

### Socket activation

Socket activation can be used to start Kodi when the user starts a remote control app or on a connection to Kodi's html control port. Start listening by [starting](/index.php/Starting "Starting") `kodi@*user*.socket` (replace *user* with the user running Kodi to be started as).

There are no packaged `kodi@.socket` and `kodi@.socket` files, one must create them manually. Depending on the setup, one can optionally change the port in `kodi@.socket`.

 `/etc/systemd/system/kodi@.service` 
```
# This fails if the user does not have an X session.
[Unit]
Description=Launch Kodi on main display
Conflicts=kodi.socket

[Service]
Type=simple
Environment=DISPLAY=:0.0
Nice=-1
ExecStart=/usr/bin/su %i /usr/bin/kodi
ExecStopPost=/usr/bin/systemctl --no-block start kodi@%i.socket

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

### Start from remote control with LIRC / irexec

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

Create a [drop-in](/index.php/Systemd#Drop-in_files "Systemd") for `kodi.service`:

 `/etc/systemd/system/kodi.service.d/lirc.conf` 
```
[Service]
ExecStart =
ExecStart = /usr/bin/irexec
```

[Start](/index.php/Start "Start") `kodi.service` and [enable](/index.php/Enable "Enable") it to run at boot time.

## Using a remote control

As Kodi is geared toward being a remote-controlled media center via an official app, physical remote control, or USB/bluetooth keyboard/mouse.

### Using the Android or iOS app

Both Android and iOS users can use the official app (currently free of charge) to control kodi once it is correctly setup to do so. Steps to configure both Kodi and the app are detailed on the [Official Kodi Remote](https://kodi.wiki/view/Official_Kodi_Remote) page.

### Using a physical remote control

Any PC with a supported IR receiver/remote, can use [LIRC](/index.php/LIRC "LIRC") or even kernel supported modules to drive it. Configuring specific remotes with lirc is covered on the [LIRC](/index.php/LIRC "LIRC") article.

To work properly with Kodi, a file that maps the lirc events to Kodi keypresses is needed. Create an [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML") file at `~/.kodi/userdata/Lircmap.xml` (note the capital 'L').

**Note:** Users running Kodi started with [kodi-standalone-service](https://aur.archlinux.org/packages/kodi-standalone-service/) will find the `kodi` user's home (`~`) under `/var/lib/kodi/` and should substitute this in for the shortcut above. Also make sure that if creating this file as the root user, it gets proper [ownership](/index.php/Ownership "Ownership") as `kodi:kodi` when finished.

`Lircmap.xml` format is as follows:

```
<lircmap>
  <remote device="devicename">
      <XBMC_button>LIRC_button</XBMC_button>
      ...
  </remote>
</lircmap>
```

*   **Device Name** is whatever LIRC calls the remote. This is set using the **Name** directive in lircd.conf and can be viewed by running `irw` and pressing a few buttons on the remote. IRW will report the name of the button pressed and the name of the remote will appear on the end of the line.
*   **XBMC_button** is the name of the button as defined in [keymap.xml](https://kodi.wiki/view/Keymap).
*   **LIRC_button** is the name as defined in `lircd.conf`. If `lircd.conf` was autogenerated using `irrecord`, these are the names selected for the buttons. Refer back to [LIRC](/index.php/LIRC "LIRC") for more information.
*   A very thorough [LIRC](https://kodi.wiki/view/LIRC) page hosted on the Kodi Wiki should be consulted for more help and information on this subject as this is out of scope of this article.

### HDMI-CEC

With a supported [USB-CEC adapter](https://www.pulse-eight.com/p/104/usb-hdmi-cec-adapter), Kodi can be used to automatically turn on and off the TV and other home theater equipment. Volume control from Kodi can be sent to a supported amplifier, one can manage DVD or Blu-Ray players from inside Kodi, and redirect the active source on the TV to whichever equipment needs it, all from one remote control. For more information see the [official Kodi wiki page on CEC](https://kodi.wiki/view/CEC) and [libCEC FAQ](http://libcec.pulse-eight.com/faq).

Install [libcec](https://www.archlinux.org/packages/?name=libcec).

When connected, the USB-CEC's `/dev` entry (usually `/dev/ttyACM*`) will default to being owned by the `uucp` group, so in order to use the device the user running Kodi needs to belong to that group. The user also needs to belong to the `lock` group, otherwise Kodi will be unable to connect to the device. See [Users and groups#Group management](/index.php/Users_and_groups#Group_management "Users and groups") for instructions on how to add users to groups.

*   Add all users that will use Kodi to the `uucp` and `lock` [user groups](/index.php/User_group "User group").
*   If [running kodi-standalone](#Running_standalone), add the user `kodi` to the `uucp` and `lock` [user groups](/index.php/User_group "User group").

**Note:** Trying to use the USB-CEC without belonging to above groups may lead to problems, including Kodi crashes, so make sure the correct user belongs to both groups.

## Sharing media and a centralized database across multiple nodes

If multiple PCs on the same network are running Kodi, they can be configured to share a single media library (video and music). The advantage of this is media and key metadata are stored in one place, and are shared/updated by all nodes on the network. For example, users of this setup can:

*   Stop watching a movie or show in one room then finish watching it in another room automatically.
*   Share watched and unwatched status for media on all nodes.
*   Simplify the setup with only a single library to maintain.

As well, the media itself can be located in one space thus allowing a lighter footprint of client systems (ie no need for large HDD space).

Several things are needed for this to work:

*   Network exposed media (via protocols that Kodi can read, e.g. NFS or Samba).
*   A [MySQL](/index.php/MySQL "MySQL") server.

**Warning:** When sharing a database, ALL clients need to be on the same major version of Kodi due to versioned requirements of the database schema. Refer to [this](https://kodi.wiki/view/Databases#Database_Versions) table for a list of database versions.

**Note:** The following guide is only an example of one configuration and is not meant to be limiting but illustrative. Key steps are shown but a detailed discussion is not offered.

These assumptions are used for the guide, substitute as needed:

*   The media is located under following mount points: `/mnt/shows` `/mnt/movies` `/mnt/music`.
*   The network addresses of all nodes are within the 192.168.0.* subnet range.
*   The IP address of the machine running both the NFS exports and the MySQL database is 192.168.0.105.
*   Each Kodi box is referred to as a node.
*   The Linux user running Kodi is 'kodi' on all nodes.

For additional info, refer to the [official Kodi wiki](https://kodi.wiki/view/MySQL/Setting_up_MySQL#Arch_Linux).

### NFS server export example

This section provides an example using exports, see [NFS](/index.php/NFS "NFS") for install and usage.

**Note:** Users only need one box on the LAN to serve the content, therefore, do not repeat this for each node. The following example assumes the user is running Arch Linux, but any NFS server will work, be it Linux or BSD, etc.

Create an empty directory in NFS root for each media directory to be shared. E.g.:

```
# mkdir -p /srv/nfs/{shows,movies,music}

```

[Bind mount](/index.php/NFS#Server "NFS") the media directories to the empty directories in `/srv/nfs/`.

Setup [exports](/index.php/NFS#Server "NFS"):

 `/etc/exports.d/kodi.exports` 
```
/srv/nfs          192.168.0.0/24(ro,fsid=0,no_subtree_check)
/srv/nfs/shows    192.168.0.0/24(ro,no_subtree_check,insecure)
/srv/nfs/movies   192.168.0.0/24(ro,no_subtree_check,insecure)
/srv/nfs/music    192.168.0.0/24(ro,no_subtree_check,insecure)
```

### Install and setup the MySQL server

See [MariaDB](/index.php/MariaDB "MariaDB") for installation and configuration instructions.

To create a database for Kodi, use the following commands:

```
$ mysql -u root -p
   <<enter the mysqld root password assigned in the first step>>
MariaDB [(none)]> CREATE USER 'kodi' IDENTIFIED BY 'kodi';
MariaDB [(none)]> GRANT ALL ON *.* TO 'kodi';
MariaDB [(none)]> flush privileges;
MariaDB [(none)]> \q

```

### Setup Kodi to use the MySQL library and the NFS exports

Since this example makes use of NFS shares, an optional dependency of Kodi is now required to access them. Ensure that each of the Kodi nodes has [libnfs](https://www.archlinux.org/packages/?name=libnfs) installed.

#### Setup Kodi to use the common MySQL database

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

#### Setup network shares

Load Kodi and define the network shares that correspond to the exports by browsing to the following within the interface *Video > Files > Add Videos > Browse > Network Filesystem(NFS)*.

After a few seconds, the IP address corresponding to the NFS server should appear.

Select `/srv/nfs/shows` from the list of share and then *OK* from the menu on the right. Assign this share the category of *TV Shows* to setup the appropriate scraper and to populate the MySQL database with the correct metadata.

Repeat this browsing process for the "movies" and "music" and then exit Kodi once properly configured. At this point, the MySQL tables should have been created.

**Note:** Even if Kodi is running on the same box that is also running the NFS exports and MySQL server, one **must** setup the media using the nfs shares only.

### Cloning the configuration to other nodes on the network

To set up another Kodi node on the network to use this library, simply copy `~/.kodi/userdata/advancedsettings.xml` to that box and restart Kodi. There is NO need to copy any other files or to do any other setup steps on the new kodi node. The nfs exports, the metadata for the programming, any stop/start times, view status, etc. are all stored in the MySQL tables.

**Note:** One can optionally define other media sources that are not managed by kodi database, but they will be specific to that particular node.

## Tips and Tricks

### Keep a log of what is watched

Keep track of every video watched on kodi with [kodi-logger](https://aur.archlinux.org/packages/kodi-logger/).

### Speedup video playback (synchronized audio and video) up to 1.5x

To enable speed-up and slow-down with audio/video sync (0.8x - 1.5x) do the following:

*   Create the following file that will map the `[` and `]` keys to the `tempo down` and `tempo up` actions, respectively:

 `~/.kodi/userdata/keymaps/custom.xml` 
```
<keymap>
  <FullscreenVideo>
    <keyboard>
      <opensquarebracket>PlayerControl(tempodown)</opensquarebracket>
      <closesquarebracket>PlayerControl(tempoup)</closesquarebracket>
    </keyboard>
  </FullscreenVideo>
  <VideoMenu>
    <keyboard>
      <opensquarebracket>PlayerControl(tempodown)</opensquarebracket>
      <closesquarebracket>PlayerControl(tempoup)</closesquarebracket>
    </keyboard>
  </VideoMenu>
</keymap>
```

*   Restart kodi which will read in these changes.
*   Navigate to *System > Player > Videos > Playback* and enable "Sync playback to display" option.

Play some video content and enjoy the ability to adjust the speed using the keys discussed above.

### CLI for kodi

*   [kodi-eventclients](https://www.archlinux.org/packages/?name=kodi-eventclients) package provides `kodi-send` which can send valid [kodi action](https://kodi.wiki/view/Action_IDs) or [kodi function](https://kodi.wiki/view/List_of_built-in_functions#List_of_functions) to kodi from the shell.

*   [texturecache](https://aur.archlinux.org/packages/texturecache/) can handle many aspects of library management, from clean-up of unused images, to searching, to querying what is currently playing.

### Hardware video acceleration

Enable and configure [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") to speed up playback performance.

Restart Kodi and enable the hardware backend(s) in Playback under Settings.

### Adjusting CD/DVD drive speed

The *eject* program from the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package does a nice job for this, but its setting is cleared as soon as the media is changed.

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

Restart Kodi and set port `80` in the configuration menu (*Services > Webserver > Port*).

### Using ALSA

If [PulseAudio](/index.php/PulseAudio "PulseAudio") does not work properly, try using [ALSA](/index.php/ALSA "ALSA") directly by starting Kodi with the `AE_SINK=ALSA` [environment variable](/index.php/Environment_variable "Environment variable"). The Kodi wiki for NUC devices provides [instructions](https://kodi.wiki/view/HOW-TO:Install_Kodi_on_an_Intel_NUC#disable_PulseAudio)

If using `kodi-standalone`, change the `APP` variable in `/usr/bin/kodi-standalone` to

```
APP="${bindir}/pasuspender -- env AE_SINK=ALSA ${bindir}/${bin_name} --standalone $@"

```

### Audio Passthrough

To allow the receiver to decode the audio by enabling passthrough. This is useful for files encoded in TrueHD or Atmos. If using PulseAudio, follow the instructions at [https://kodi.wiki/view/PulseAudio](https://kodi.wiki/view/PulseAudio) to first enable passthrough in PulseAudio. Then the passthrough options will appear in Kodi. If using ALSA, the passthrough options will appear in Kodi without modifications.

**Warning:** PulseAudio requires the output in Kodi to be set to 2 channel. Audio encoded in formats not passed through will only be sent as stereo audio. Use ALSA to support passthrough and passing decoded surround audio signals

**Note:** PulseAudio does not support TrueHD, DTS-MA, or Atmos passthrough. Use ALSA to pass these to through the receiver.

#### Fix for delayed startup on wifi

If running with WiFi only (wired network unplugged) while [#Sharing media and a centralized database across multiple nodes](#Sharing_media_and_a_centralized_database_across_multiple_nodes), kodi will likely start before the wireless network is up, which will result in failure to connect to the shares and to the mysql server. Assuming the network is managed by the default [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), this can be fixed by using two [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd"), one for `kodi.service` and another for `systemd-networkd-wait-online.service`:

```
# systemctl edit systemd-networkd-wait-online.service
[Service]
ExecStart=
ExecStart=/usr/lib/systemd/systemd-networkd-wait-online --ignore eth0

```

```
# systemctl edit kodi
[Unit]
After=remote-fs.target network-online.target
Wants=network-online.target

```

### Run kodi in a window manager

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

### USB DAC not working

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

### Accessing Kodi logs

In case of an error the first point to start investigation can be `~/.kodi/temp/kodi.log`.

### Fullscreen mode stretches Kodi across multiple displays

For a multi-monitor setup, Kodi may default to stretching across all screens. One can restrict the fullscreen mode to one display by setting the [environment variable](/index.php/Environment_variable "Environment variable") `SDL_VIDEO_FULLSCREEN_HEAD` to the number of the desired target display. For example, having Kodi show up on display 0, add the following line to the Kodi user's `~/.bashrc` configuration:

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

**Tip:** By default, press `O` during playback to show codec information and CPU usage. More information about this overlay can be found at [https://kodi.wiki/view/Codecinfo](https://kodi.wiki/view/Codecinfo).

If the hardware does not or cannot make use of acceleration, disable it and explicitly set video decoding to software. This is because [H.264 decoding is only multithreaded when video decoding is set to software](https://forum.kodi.tv/showthread.php?tid=170084&pid=1789661#pid1789661).

To achieve this, go to *System Settings > Video*. Set the `settings level` to `Advanced` or `Expert`. Then go to *Acceleration* and set `Decoding method` to `software`.

### Kodi hangs on exit, fully occupying one CPU core, UI unresponsive

This problem can arise with third-party plugins installed, there is some issue with their termination[[1]](https://www.linuxquestions.org/questions/linux-software-2/kodi-freezes-on-exit-kodi-bin-won't-die-4175588180/),[[2]](https://www.reddit.com/r/archlinux/comments/5029oo/kodi_freezes_on_exit_kodibin_wont_die/).

Workaround: find proper UI description file (`DialogButtonMenu.xml`) and tweak exit button type from internal Kodi's `Quit()` function call to sending signal from outside system to Kodi. Here is one-liner that makes modifications to any skin from the default Kodi package:

```
# find /usr/share/kodi/addons/skin.* -name DialogButtonMenu.xml -exec sed -i 's%<onclick>Quit()</onclick>%<onclick>System.Exec ("killall --signal SIGHUP kodi.bin")</onclick>%' {} \;

```

## See also

*   [Kodi Wiki](https://kodi.wiki/view/Main_Page) - Excellent resource with much information about Arch Linux specifically
*   [Wikipedia:Kodi (software)](https://en.wikipedia.org/wiki/Kodi_(software) "wikipedia:Kodi (software)")
*   [http://www.hdpfans.com/thread-329076-1-1.html](http://www.hdpfans.com/thread-329076-1-1.html) - Kodi/xbmc Chinese plug-in library installation method
*   [https://github.com/taxigps/xbmc-addons-chinese](https://github.com/taxigps/xbmc-addons-chinese) - xbmc-addons-chinese: Addon scripts, plugins, and skins for XBMC Media Center. Special for chinese laguage.