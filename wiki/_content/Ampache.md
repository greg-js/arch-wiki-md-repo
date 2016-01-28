# Ampache

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Be careful. This article can be outdated **since 3.8 release**. (Discuss in [Talk:Ampache#](https://wiki.archlinux.org/index.php/Talk:Ampache))

This document describes how to set up Ampache on an Arch Linux LAMP server. Ampache is a Web-based Audio file manager. It is implemented with MySQL, and PHP. It allows you to view, edit, and play your audio files via the web. It has support for playlists, artist and album views, album art, random play, playback via Http/On the Fly Transcoding and Downsampling, Ampache is excellent if you want to be able to listen to your music collection anywhere.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Logging](#Logging)
    *   [4.2 Transcoding](#Transcoding)
    *   [4.3 Downsampling](#Downsampling)
*   [5 Using with Amarok](#Using_with_Amarok)
*   [6 See also](#See_also)

## Installation

You need three things to run Ampache. A webserver, [PHP](/index.php/PHP "PHP") and [MySQL](/index.php/MySQL "MySQL"). Please refere to the [LAMP](/index.php/LAMP "LAMP") article for more information.

[Install](/index.php/Install "Install") one Ampache package:

*   [ampache](https://aur.archlinux.org/packages/ampache/)<sup><small>AUR</small></sup> - Stable release

*   [ampache-git](https://aur.archlinux.org/packages/ampache-git/)<sup><small>AUR</small></sup> - Development version

## Configuration

PHP is installed as a dependency of Ampache. You need to edit the PHP configuration file `/etc/php/php.ini` in order to enable iconv support for ampache.

Uncomment (remove the initial semi-colon from) the following line in the `php.ini` file:

```
;extension=iconv.so

```

When Ampache is installed, point your browser to [http://localhost/ampache](http://localhost/ampache) (substitute the address of your Ampache server for localhost if you did not install it locally).

If you encounter any problems here, use [http://localhost/ampache/test.php](http://localhost/ampache/test.php) to double check your configuration.

*   On the first page choose your the installation language.

*   On the second page enter the following:
    *   Desired Database Name - Choose a unique name then you will recognize when you edit your MySQL databases.
    *   MySQL Hostname - localhost is fine.
    *   MySQL Administrative Username - root is the default
    *   MySQL Administrative Password - root's password.
    *   Create Database User for New Database? - Yes.
    *   Ampache Database Username - Same thing here, unique and recognizable.
    *   Ampache Database User Password - Please note that this is only MySQL info, this is not your Ampache user account
    *   Overwrite Existing
    *   Use Existing Database

*   On the third page you are going to edit the `ampache.cfg.php` file
    *   Web Path - Your path to ampache.
    *   Desired Database Name - Same as on the second page.
    *   MySQL Hostname - localhost.
    *   MySQL Username - Same as Ampache Database Username, or root if you did not create a database user.
    *   MySQL Password - MySQL Username's password.
*   Press write config
*   Move the `ampache.cfg.php` to the `ampache/config` directory.
*   Press check for config.

*   On the fourth page you are going to create an admin account. This step is self explanatory.
    *   Username
    *   Password
    *   Confirm Password

## Troubleshooting

If you are having problems adding catalogs, please check your permission settings. More catalog toubleshooting [here](http://ampache.org/wiki/install:catalog#permissions).

If you are still having problems check your Open basedir setting in php.ini. You can either comment out the open_basedir all together or add the directory in which your files reside. The second option is preferred. To comment out a line all you need to do is add a semicolon at the beginning of the line.

```
;open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/

```

## Tips and tricks

### Logging

Is something not working as intended? Let's get some logging going!

There are five levels of logging in Ampache, 5 being the highest.

To enable logging you just need to set the debug value to true and set debug_level to your desired level.

```
; Debug
; If this is enabled Ampache will get really chatty
; warning this can crash browser during catalog builds due to 
; the amount of text that is dumped out this will also cause 
; ampache to write to the log file
; DEFAULT: false
debug = "true"

; Debug Level
; This should always be set in conjunction with the
; debug option, it defines how prolific you want the
; debugging in ampache to be. values are 1-5\. 
; 1 == Errors only
; 2 == Error + Failures (login attempts etc.)
; 3 == ??
; 4 == ?? (Profit!)
; 5 == Information (cataloging progress etc.)
; DEFAULT: 5
debug_level = 5
```

Last thing you have to do is specify where you want the log to reside. Remember that the `http` user needs write permissons to the file.

```
; Path to Log File
; This defines where you want ampache to log events to
; this will only happen if debug is turned on. Do not
; include trailing slash. You will need to make sure that
; your HTTP server has write access to the specified directory
; DEFAULT: NULL
log_path = "/var/log/ampache"
```

### Transcoding

If you want to use Ampache's on the fly transcoding you need the packages specified in `config/ampache.cfg`, the packages needed for transcoding the most common audio file formats are listed in Ampache stable's _.install_ file. You also need to configure the specific lines in `ampache.cfg`.

The following example enables M4A transcoding to MP3.

Please note that you need both lame, used for all audio file formats, and faad, m4a specific, installed.

```
; List of filetypes to transcode
transcode_m4a           = true
transcode_m4a_target    = mp3 

; These are the commands that will be run to transcode the file
transcode_cmd_m4a       = "faad -f 2 -w %FILE% | lame -r -b %SAMPLE% -S - -"

```

### Downsampling

Downsampling requires the same packages as transcoding so follow the steps above for each audio file format you need. The example above enables downsampling of m4a files.

You also need to uncomment and specify the minimum and maximum bitrate you prefer.

```
max_bit_rate = 576

min_bit_rate = 48
```

## Using with Amarok

*   [Amarok and Ampache](http://ampache.org/wiki/config:amarok)

Using the Ampache web interface, we need to allow API access to Ampache from our local network. To do this go to the Admin tab and then click on Show Acls. Find Add API / RPC Host and click on it. Name your ACL Entry, ("My Network" for ex). If you want API + Streaming + Web Interface access pick RPC + All under type.

In Amarok, go to _Settings > Services_. Make sure the Ampache Service is enabled and then click _Settings_ button on Ampache plugin.

*   Name : This is an internal name for Amarok, up to you.
*   Server : This is the fully qualified address for your Ampache server including the http://.
*   Username : This is your username to the Ampache web interface.
*   Password : This is your password to the Ampache web interface

## See also

[https://github.com/ampache/ampache/](https://github.com/ampache/ampache/) - Official site

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ampache&oldid=412037](https://wiki.archlinux.org/index.php?title=Ampache&oldid=412037)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")