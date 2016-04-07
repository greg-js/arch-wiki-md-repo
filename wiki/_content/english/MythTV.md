MythTV is an application suite designed to provide an amazing multimedia experience. It provides PVR functionality to a Linux based computer and also supports other media types. Combined with a nice, quiet computer and a decent TV, it makes an excellent centerpiece to a home theater system.

## Contents

*   [1 Structure](#Structure)
    *   [1.1 mythbackend](#mythbackend)
    *   [1.2 mythfrontend](#mythfrontend)
*   [2 Requirements](#Requirements)
*   [3 Getting Started](#Getting_Started)
*   [4 Make a "mythtv" User](#Make_a_.22mythtv.22_User)
*   [5 Installing MythTV](#Installing_MythTV)
    *   [5.1 Backend setup](#Backend_setup)
        *   [5.1.1 Setting up the database](#Setting_up_the_database)
        *   [5.1.2 Setting up the master backend](#Setting_up_the_master_backend)
        *   [5.1.3 Enable the mythbackend daemon](#Enable_the_mythbackend_daemon)
    *   [5.2 Troubleshooting](#Troubleshooting)
        *   [5.2.1 XvMCW](#XvMCW)
        *   [5.2.2 PVR150](#PVR150)
        *   [5.2.3 Opening DVB frontend device failed](#Opening_DVB_frontend_device_failed)
*   [6 Frontend setup](#Frontend_setup)
    *   [6.1 Nvidia XvMC Setup](#Nvidia_XvMC_Setup)
*   [7 MythTV Plugins](#MythTV_Plugins)
    *   [7.1 MythWeb](#MythWeb)
    *   [7.2 Mythweather](#Mythweather)
*   [8 Environment Variables](#Environment_Variables)
*   [9 Hints to a Happy Myth System](#Hints_to_a_Happy_Myth_System)
    *   [9.1 Using GDM to autologin your Mythfrontend](#Using_GDM_to_autologin_your_Mythfrontend)
    *   [9.2 Using XDM to Automically Login to your MythFrontend](#Using_XDM_to_Automically_Login_to_your_MythFrontend)
    *   [9.3 Optmize your system](#Optmize_your_system)
*   [10 References](#References)

## Structure

The MythTV system is split into a backend and a frontend. Each component has its own functions:

### mythbackend

*   Schedule and record television programming
*   Stream video data to the frontend
*   Flag commercial breaks
*   Transcode videos from one format to another

### mythfrontend

*   Provide a pretty GUI
*   Play back recorded content
*   Provide an interface to schedule programs

The frontend and backend may be on separate computers on a network, and there may also be multiple frontends. This architecture allows for a central media distribution system that can reach anywhere a network can. This is a remarkably flexible system, and it even allows very low power machines to act as perfectly usable frontends.

## Requirements

MythTV is a very scalable system. With standard definition television and pure MPEG2 encoding and decoding with hardware acceleration, even a very modest system can act as both frontend and backend. How modest? Some people report being able to use fanless Via systems with Hauppauge PVR cards for both backend and frontend simultaneously. While the author does not condone the use of such a lightweight system, it has been done successfully.

On the other end of the spectrum, high definition TV with MPEG4 transcoding and commercial flagging can require serious horsepower. Most people in the HD realm use high-end Athlon XPs, midrange to high-end Athlon 64s, and high-end Pentium 4s for their backends. The frontend can get away with a somewhat more midrange processor if XvMC playback acceleration is used.

All systems are going to need a tuner card. The Hauppauge PVR series of cards (150, 250, 350, and 500) are very popular for use with MythTV due to fairly decent Linux support and low CPU usage. Other cards, like those based on the BT878 chipset, are also used. Unlike the PVR series, BT878 based cards require significant amounts of CPU power to save the video, as these cards output raw frames and not compressed streams.

The only combination of hardware the author can say works is an Athlon XP 1700+ frontend with 512MB of DDR memory, and a Pentium 4 2.8GHz backend with 512MB of DDR2 memory.

## Getting Started

In order to install MythTV on your system(s), you must have a working Linux installation. Since this is the Arch Linux website, this article will be geared towards Arch. A simple base system [Installation](/index.php/Installation "Installation") with no extras is a suggested starting point.

For the backend, it is also good to have [LAMP](/index.php/LAMP "LAMP") working properly so that anybody can use a web browser to schedule programming through MythWeb. While it is not necessary, it is a very handy feature.

A working [Xorg](/index.php/Xorg "Xorg") (graphical) environment is necessary. For setting MythTV up, a remote access via X11-forwarding mechanism is sufficient.

## Make a "mythtv" User

**Note:** mythtv package installation creates mythtv user.

If the purpose of the box is a stand-alone system, consider making a dedicated user for this purpose. For the rest of the guide, this username is "mythtv."

```
# passwd mythtv <<set the password of your choosing>>

```

## Installing MythTV

[Install](/index.php/Install "Install") the [mythtv](https://www.archlinux.org/packages/?name=mythtv) package and any desired plugins:

*   mythplugins-mytharchive - Create DVDs or archive recorded shows in MythTV
*   mythplugins-mythbrowser - Mini web browser for MythTV
*   mythplugins-mythgallery - Image gallery plugin for MythTV
*   mythplugins-mythgame - Game emulator plugin for MythTV
*   mythplugins-mythmusic - Music playing plugin for MythTV
*   mythplugins-mythnetvision - MythNetvision plugin for MythTV
*   mythplugins-mythnews - News checking plugin for MythTV
*   mythplugins-mythweather - Weather checking plugin for MythTV
*   mythplugins-mythweb - Web interface for the MythTV scheduler
*   mythplugins-mythzoneminder - View CCTV footage from zoneminder in MythTV

At this point a generic MythTV installation is present that must be refined into a backend, a frontend, or both.

### Backend setup

Before setting up your backend, make sure you have a functioning *video capture card* or a *firewire input from a STB*. Unfortunately, that part of setup is outside the scope of this article. If you are in the United States, get an account at [Schedules Direct](http://www.schedulesdirect.org) (this service provides TV listings at a minimal cost). Users outside the United States will need to use screen scrapers ([xmltv](http://wiki.xmltv.org/index.php/Main_Page/)) to do the same job.

#### Setting up the database

**Note:** This is a quick and dirty walk through of MySQL. Be sure you read the [MySQL](/index.php/MySQL "MySQL") article for more details.

[Install](/index.php/Install "Install") [mariadb](https://www.archlinux.org/packages/?name=mariadb) and [start](/index.php/Start "Start") `mysqld.service`.

If other machines in the LAN are expected to connect to the masterbackend server, comment out the "skip-networking" line in `/etc/mysql/my.cnf` at this point.

Setup mysql with a password:

```
# mysql_secure_installation

```

Create the database structure:

```
$ mysql -u root -p </usr/share/mythtv/mc.sql

```

If you have lost or overwritten your mc.sql file, it is always available [here](https://github.com/MythTV/mythtv/blob/master/mythtv/database/mc.sql).

Update your database

```
# mysql_upgrade -u root -p

```

**Note:** With the 0.26 release of mythtv, time zone tables are required to be in MySQL!

To add them, simply execute the following:

```
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p<yourpassword> mysql

```

Some setups refuse frontends from remote machines. To fix this:

```
# mysql -u root -p
mysql> GRANT ALL ON mythconverg.* TO 'user'@'host.net' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.00 sec)
mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

```

*   Replace **user** with the user name running on the frontend (default: mythtv).
*   Replace **host.net** with the host name or IP address of the remote box needing access. Other common values are *%.local* and *192.168.1.%*.
*   Replace **password** with a suitable password (default: mythtv).

**Note:** MySQL / MariaDB treats a "user@host.net" and "user@192.168.1.1" as completely separate users, therefore you may need to use both types

Example:

```
# mysql -u root -p
mysql> GRANT ALL ON mythconverg.* TO 'mythtv'@'192.168.0.%' IDENTIFIED BY 'mythtv';
Query OK, 0 rows affected (0.00 sec)
mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

```

#### Setting up the master backend

Load up your WM (lxde is a good choice for light-weight builds, but anything will work.)

**Note:** Users wishing to just demo the software and those without capture card/hardware may follow [this](http://motorscript.com/mythtv-without-tv-tuner-card) guide.

Now run the mythtv-setup program

```
$ mythtv-setup

```

If your backend runs on a headless server, *mythtv-setup* can be run via [Secure Shell#X11 forwarding](/index.php/Secure_Shell#X11_forwarding "Secure Shell") by running:

```
$ ssh -X user@backend '. /etc/profile.d/perlbin.sh && LANG=C mythtv-setup'

```

*   **General menu**

If this is your master backend, put its IP address in the first and fourth fields, identifying this computer as your master and giving its network IP address.
On the next page, enter the paths where recordings and the live TV buffer will be stored. LVM or RAID solutions provide easily accessible large scale storage. But again, those are outside the scope of this article. Set the live TV buffer to a size you can handle and leave everything else alone.
On the next page, set the settings to your locale. NTSC is mostly used in North America, and be sure to set whether using cable or broadcast.
On the next two pages, leave everything as is unless you know for sure you want to change it. On the next page, if you have a fast backend that can handle recordings and flagging jobs simultaneously, it is recommended to set CPU usage to \"High\", maximum simultaneous jobs to 2, and to check the commercial flagging option.
On the next page, set these options to taste. Automatic commercial flagging is highly recommended. Ignore the next page and finish.

*   **Capture card menu**

Select your card type from the drop down list. Hauppauge PVR users will select the MPEG-2 encoder card option.
Point mythtv-setup to the proper location, usually /dev/v4l/video0

*   **Video sources menu**

This is where it gets important to have a source for TV listings. Schedules Direct users should create a new video source, name it, select the North America (Schedules Direct) option, and fill in their logon information. In order to verify that it is correct, go ahead and retrieve the listings.

*   **Input connections menu**

This menu is rather self-explanatory. All you need to do is pick an input on the capture card and tell myth which video source it connects to. Most users will select their tuner and leave all the other inputs alone. Satellite users will select a video input, and on the next page provide the command to change channels on their STB using an external channel change program. This is also outside the scope of this article.

*   **Channel editor menu**

This menu is safe to ignore

*   Exit the program (Esc)

*   Run mythfilldatabase

```
$ mythfilldatabase

```

This should populate your mysql database with TV listings for the next two weeks (or so).

#### Enable the mythbackend daemon

[Enable](/index.php/Enable "Enable") the `mythbackend.service` systemd unit.

### Troubleshooting

#### XvMCW

If you get a libXvMCW.so.1 shared library error, [install](/index.php/Install "Install") [libxvmc](https://www.archlinux.org/packages/?name=libxvmc).

#### PVR150

If you cannot open /dev/video0 of your PVR150, install the firmware, located in the [ivtv-utils](https://www.archlinux.org/packages/?name=ivtv-utils) package.

#### Opening DVB frontend device failed

The kernel takes time to register the frontend devices (such as those of TurboSight TBS 62x1) and they may not be available when systemd starts `mythbackend.service`. This leads to the following error recorded in the system log:

```
# DVBChan[1](/dev/dvb/adapter0/frontend0): Opening DVB frontend device failed.
# eno:No such file or directory (2)
# DVBChan[1](/dev/dvb/adapter0/frontend0): Failed to open DVB frontend device due to fatal error or too many attempts.
# ChannelBase: CreateChannel() Error: Failed to open device /dev/dvb/adapter0/frontend0
# Problem with capture cardsCard 1failed init

```

The solution consists in starting the `mythbackend.service` only after the devices are available:

*   [Create](/index.php/Edit "Edit") file `/etc/udev/rules.d/99-mythbackend.rules`:

```
#
# Create systemd device units for capture devices
#
SUBSYSTEM=="video4linux", TAG+="systemd"
SUBSYSTEM=="dvb", TAG+="systemd"
SUBSYSTEM=="firewire", TAG+="systemd"

```

*   Override systemd's defaults by [creating](/index.php/Edit "Edit") file `/etc/systemd/system/mythbackend.service.d/override.conf`:

```
# [Unit]
# After=dev-dvb-adapter0-frontend0.device
# Wants=dev-dvb-adapter0-frontend0.device

```

See MythTV wiki's page [Systemd mythbackend Configuration](https://www.mythtv.org/wiki/Systemd_mythbackend_Configuration#Delay_starting_the_backend_until_tuners_have_initialized) for further details.

## Frontend setup

Compared to the backend, getting a frontend running is trivially simple. The frontend machine needs permission to access the database on the backend machine. On the backend machine, follow the instructions to grant remote access in the [MySQL](/index.php/MySQL "MySQL") archlinux wiki. On the frontend machine, install the mythtv pacakages using pacman as above. Afterward, make sure you are in an X environment as a normal user and run mythfrontend. It will pop up a menu asking about the IP address of the backend and the local computer's name and IP address. Fill in this information and your frontend should be functional.

On the other hand, the frontend has more options than a luxury car. All of those are an article on their own. There are a few notable options that should be set to ensure a good working setup. If you do not have an interlaced monitor (and almost nobody does), you will need to deinterlace your television output. Go into the TV playback menu and select kernel deinterlacing or bob2x deinterlacing. Try both and see which you like better. Also, in the general settings page, it is good to set up your [Alsa setup] settings, but those vary so greatly it is not worth suggesting values here.

One problem I encountered running mythfrontend 0.20.0.2007013 on fglrx was that the colors were mixed up. People were blue-skinned etc. It turns out there is a hack for ATI cards in the source, but it is not enabled. Uncomment #define USE_ATI_PROPRIETARY_DRIVER_XVIDEO_HACK in libs/libmythtv/videoout_xv.cpp and rebuild. (this will change names in svn and so future versions)

### Nvidia XvMC Setup

Assuming you have loaded the proprietary Nvidia drivers from pacman you may need to [create](/index.php/Edit "Edit") `/etc/X11/XvMCConfig` with the following line:

 `libXvMCNVIDIA_dynamic.so.1` 

This will allow Mythfrontend to use the XvMC environment for acceleration. Restart Mythfrontend

## MythTV Plugins

There are a number of plugins available for MythTV in the AUR. They range from RSS readers to DVD players. Take a look at them. Simply installing the package on the frontend computer should impart the intended functionality. There is rarely any additional setup, and when there is, the install file will mention it.

### MythWeb

[MythWeb](/index.php/MythWeb "MythWeb") is a web interface for MythTV. Instructions for configuring MythWeb in Arch Linux can be found on the [MythWeb](/index.php/MythWeb "MythWeb") page.

### Mythweather

As of 7-10-08 Mythweather is broken in Extra

extra/mythweather 0.21-1 (mythtv-extras)

## Environment Variables

I found mythbackend would randomly stop running with the following error message: `Cannot locate your home directory. Please set the environment variable HOME or MYTHCONFDIR`

So I did the following as root: `mkdir /home/mythtv ; cp /home/(myusername)/.lircrc /home/mythtv/ ; chown -R (myusername):users /home/mythtv`

And then put the following in /etc/rc.conf `MYTHCONFDIR=/home/mythtv`

## Hints to a Happy Myth System

But not full articles (yet)

*   Run ntpd or openntpd on your backend to make sure it always has the right time.
*   [LIRC](/index.php/LIRC "LIRC") on your frontend allows you to use a remote control, which is wonderful in a living room.
*   Use gdm, kdm, or xdm to automatically log in your frontend, and ~/.xinitrc to load mythfrontend on boot.
*   Set the "automatically run mythfilldatabase" option on one of your frontends to make sure you always have listings.
*   Do not forget to use the verbosity statements and log file location arguments to mythfrontend so you can see when things break.
*   Do not run your frontend as root, create a mythtv user

### Using GDM to autologin your Mythfrontend

[Display manager](/index.php/Display_manager "Display manager")

In your /etc/gdm/custom.conf add the following statements under the [daemon] heading:

```
AutomaticLoginEnable=true
AutomaticLogin=mythtv (assuming your frontend user is mythtv)
```

FYI - GDM will not autologin as root

### Using XDM to Automically Login to your MythFrontend

Find in your /etc/inittab file the following line:

 `id:3:initdefault:` 

Change to:

 `id:5:initdefault:` 

Then add the following below it (or anywhere in the file):

 `x:5:respawn:su - MYTHUSER -c startx` 
**Note:** Remember to change "MYTHUSER" to the username that you want to autologin under.

If you'd like to start mythfrontend on booting into Xorg, edit (or create if none exists) your MYTHUSER's .xinitrc file and add the following line:

 `mythfrontend` 

### Optmize your system

Be sure to have a look at MythTV's extensive wiki documentation on how to keep your data stores happy, as well as optimize your system in various other ways to get the most out of your Myth box.

[MythTV Wiki: Optimizing Performance](http://www.mythtv.org/wiki/Optimizing_Performance)

## References

*   [http://www.mythtv.org](http://www.mythtv.org)
*   [http://mythtv.info](http://mythtv.info)
*   [http://wilsonet.com/mythtv/fcmyth.php](http://wilsonet.com/mythtv/fcmyth.php)
*   [http://www.linhes.org](http://www.linhes.org) [A user friendly MythTV and Linux install that uses Arch Linux]