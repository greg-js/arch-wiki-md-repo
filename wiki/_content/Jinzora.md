# Jinzora

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Jinzora](http://sourceforge.net/projects/jinzora/) is a GPL web based multimedia application. It serves as a streaming server as well as a media management platform. This article will show you how to install and configure Jinzora.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Setup the webserver](#Setup_the_webserver)
    *   [1.2 Configure PHP](#Configure_PHP)
    *   [1.3 Download and extract Jinzora](#Download_and_extract_Jinzora)
*   [2 Configuring Jinzora](#Configuring_Jinzora)
    *   [2.1 Run the installer](#Run_the_installer)
    *   [2.2 Save the configuration](#Save_the_configuration)
    *   [2.3 Setting up MPD to play your music](#Setting_up_MPD_to_play_your_music)
*   [3 Troubleshooting](#Troubleshooting)

## Installation

Jinzora can run in two modes, _streaming_ and using _mpd_. If you have not installed MPD already, follow the wiki guide: [mpd](/index.php/Mpd "Mpd") (It is not required for the streaming mode to operate)

### Setup the webserver

Follow the wiki tutorial for installing Apache, PHP and MySQL: [LAMP](/index.php/LAMP "LAMP")

(Note: Installing phpMyAdmin from the above guide is optional; if you are ever likely to make your own website that will use PHP and MySQL, I would suggest you install it. Otherwise you probably will not need it).

### Configure PHP

Jinzora can make use of the GD and iconv library. It is recommend you enable these. Uncomment gd.so and iconv.so in `/etc/php/php.ini`.

```
extension=gd.so
extension=iconv.so

```

The PHP gd extension requires the gd library, [php-gd](https://www.archlinux.org/packages/?name=php-gd), to be [installed](/index.php/Installed "Installed").

Also take a look at the open_basedir setting. Your media directory should be or below the paths specified in this directory.

### Download and extract Jinzora

Download the latest version of Jinzora2 from [http://sourceforge.net/projects/jinzora/](http://sourceforge.net/projects/jinzora/) and extract the contents using [tar](/index.php/Tar "Tar"):

```
# tar -xvf jz2current.tar.gz

```

## Configuring Jinzora

In the `~/httpd/html/jinzora2` directory, run configure.sh

```
# sh configure.sh

```

### Run the installer

The installer will automatically configure Jinzora and create the database. Open up your web browser, go to [http://localhost/jinzora2/index.php](http://localhost/jinzora2/index.php) and follow the instructions

*   Pay attention to these setup steps:
    *   **Page 4 - Installation Type :** Change from 'Streaming' to 'Streaming & Jukebox' if you wish to listen to the music on the computer you are installing Jinzora2 on (it is primarily a streaming application to allow remote access to, and control of, a streaming server running it).
    *   **Page 5 - Main Settings :** If you hover over the boxes here they explain the settings, so choose whatever you want. It is best to choose 'Database' for Backend Type. Also consider using the 'Tag Data' option for 'Data Structure', unless your music is organized on your filesystem exactly the way you want it to be.
    *   **Page 6 - Backend Setup :** Unless you have used Jinzora before, or for some reason wish to manually create a MySQL database for it to use, then select 'True' under 'Create Database'.
    *   **Page 7 - Import Media :** This step may take a few minutes if you have got a few gigs of music; simply enter into the box the directory where your music is stored. When the installer's finished importing the music from this directory, you will have the option to import as many other directories as you want, one after the other.

You can also import more files from the **Settings** interface when Jinzora is up and running. You do not have to do it while installing.

**Note:** While Jinzora was importing my music collection, I had the following error appear twice on the page:

```
Warning: strpos() [function.strpos]: Offset not contained in string. in /home/httpd/html/jinzora2/services/services/tagdata/getid3/module.tag.id3v2.php
on line 1542
```

This seemed to have no adverse effect on the installation though, so if something similar happens to you, do not worry!

### Save the configuration

When you have finished importing your music, click **Proceed to save config**, then **Proceed to launch Jinzora**.

### Setting up MPD to play your music

Edit `~/httpd/html/jinzora2/jukebox/settings.php`: under 'Description', change 'Winamp Media Player' to 'Music Player Daemon' (or whatever you want), and under 'type' change 'winamp3' to 'mpd'.

Change 'password' to be empty (so it just reads '' rather than 'jinzora'), or change this to whatever password you have set in `/etc/mpd.conf`.

Also in this file, change the port from '4800' to '6600', or whatever port you have set MPD to accept connections on in `/etc/mpd.conf`.

If you wish to use Jinzora's streaming functionality, simply go back to your webbrowser, click refresh, select 'Music Player Daemon' from the 'Playback To' dropdown menu and Voila! Your own working copy of Jinzora !

## Troubleshooting

*   If you cannot get any sound despite all of the above, try testing mpd with another GUI client (Glurp is a nice simple one located in the [glurp](https://www.archlinux.org/packages/?name=glurp)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup> package. Add a track to its playlist and try to play it). If you have no sound in this either, you need to further edit `/etc/mpd.conf`. Try uncommenting some of the ALSA settings in this file (assuming you use ALSA).

*   If you know that MPD _is_ working, then try to match up the settings in Jinzora as closely to those in `/etc/mpd.conf` as possible (the settings in Jinzora are accessed from the 4th small green button on the upper left of the 'Slick' interface).

*   If changes to your playlist are ignored, go to System Tools -> Settings Manager -> Main Settings/Playlist and set 'use_ext_playlists' to 'false'.

*   If when you click on the PLAY button of any song / album you are offered a 'playlist.m3u' download, then you have not changed the 'Playback To' option to 'Music Player Daemon'.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Jinzora&oldid=389406](https://wiki.archlinux.org/index.php?title=Jinzora&oldid=389406)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Streaming](/index.php/Category:Streaming "Category:Streaming")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")