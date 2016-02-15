Amarok is a music player and organizer for Linux with an intuitive interface. Version 1.4 is the most recent one released for KDE3 (although does run under KDE4 and Gnome as explained below). With KDE4 came [Amarok 2.x](/index.php/Amarok_2.x "Amarok 2.x"). However, you might still be interested in running this obsolete (until forked) version, because the developers have not yet and/or do not want to port all the 1.4 features to 2.0, they see it as an entirely different program.[[1]](http://amarok.kde.org/blog/archives/809-Missing-features-in-Amarok-2.html)

On the other hand, if you have never used Amarok 1.4 before, you may find [Amarok 2.x](/index.php/Amarok_2.x "Amarok 2.x") sufficient.

## Contents

*   [1 Features](#Features)
*   [2 Installation](#Installation)
    *   [2.1 AUR](#AUR)
*   [3 Configuration](#Configuration)
    *   [3.1 Integration with KDE4](#Integration_with_KDE4)
    *   [3.2 Integration with Gnome](#Integration_with_Gnome)
    *   [3.3 Scripts](#Scripts)
        *   [3.3.1 transKode](#transKode)
    *   [3.4 Collection database](#Collection_database)
        *   [3.4.1 MySQL](#MySQL)
        *   [3.4.2 PostgreSQL](#PostgreSQL)
    *   [3.5 Shoutcast](#Shoutcast)

## Features

*   Playback for several audio formats (mp3, flac, ogg, aac, ...)
*   Advanced collection management (filters, hierarchies)
*   Tabular playlist display with user-selectable columns, column order and sort column.
*   Efficient clear user interface.
*   An excellent Cover Manager that fetches album art (from amazon.com - or when patched like the AUR version from last.fm), including query editor
*   Smart and dynamic playlists
*   On-screen display with user-configurable track information
*   Lyrics and Wikipedia (artist, song, album) look-up
*   Media Device (iPod etc) support (2-way music transfer, syncing, cleaning, configurable mount/eject)
*   Support for [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") and Sqlite databases
*   Last.fm streams with personal account/neighbor/custom/global tags
*   Shoutcast internet radio directory and streaming
*   General streaming capabilities (Radio Streams, Podcasts)
*   A Magnatune store
*   Tray icon control with play/pause/next [close the main window without killing Amarok ;)]
*   Small separate player window
*   Mass tagging features
*   Fill in tags from MusicBrainz
*   Visualization support
*   Different playback modes (random track/album, repeat track/album/playlist)
*   Equalizer with presets and custom settings
*   Audio CD playing and burning support
*   Music statistics, rankings, scores, and Mood system
*   Community-contributed scripts manager (Transcoding, alternative scripts, etc.)

## Installation

### AUR

Build and install [amarok1](https://aur.archlinux.org/packages/amarok1/) from the AUR.

## Configuration

### Integration with KDE4

**Note:** You can make the colors precisely match your KDE4 color scheme by obtaining the three RGB values from the color selection dialogs in _System Settings > General > Appearance > Colors > Colors_

In KDE4, you can set up the colors and fonts for KDE3 applications (such as Amarok 1.4 and Kaffeine <1.0) without kcontrol by editing the file `~/.kde/share/config/kdeglobals`.

For example:

```
[General]
XftAntialias=true
XftHintStyle=hintmedium
alternateBackground=232,232,232
background=224,223,223
buttonBackground=232,231,231
buttonForeground=20,19,18
desktopFont=Tahoma,8,-1,5,50,0,0,0,0,0
fixed=Courier New,8,-1,5,50,0,0,0,0,0
font=Tahoma,8,-1,5,50,0,0,0,0,0
foreground=20,19,18
linkColor=66,109,161
menuFont=Tahoma,8,-1,5,50,0,0,0,0,0
selectBackground=65,141,212
selectForeground=0,0,0
smallestReadableFont=Tahoma,7,-1,5,50,0,0,0,0,0
toolBarFont=Tahoma,8,-1,5,50,0,0,0,0,0
visitedLinkColor=95,82,107
widgetStyle=oxygen
windowBackground=255,255,255
windowForeground=20,19,18

[Icons]
Theme=oxygen

```

Oxygen icons to make Amarok version 1.4 fit better with KDE4 can be found at [kde-look.org](http://www.kde-look.org/content/show.php/Amarok+Oxygen!?content=82038).

Also set the colours and fonts in

_Settings > Configure Amarok > Appearance_

and

_Settings > Configure Amarok > OSD_.

### Integration with Gnome

See [here](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for visual integration of the main GUI. There are also various plugins that allow Amarok to use [libnotify](/index.php/Libnotify "Libnotify") instead of its own OSD, for example: [LibnotifymaroK](http://www.kde-apps.org/content/show.php?action=content&content=106237)

### Scripts

Scripts can be found either directly from within Amarok (_Tools/Scripts/Get new scripts_) or from [kde-apps.org](http://kde-apps.org/content/search.php) in the [Multimedia/Amarok Scripts](http://kde-apps.org/?xcontentmode=56) section, or by using the kde-apps.org search function and selecting _Amarok Script_ as the type.

#### transKode

If you want to convert between audio formats from within Amarok, install [transKode](https://aur.archlinux.org/packages.php?ID=7025) from the AUR.

### Collection database

Amarok 1.4 can use sqlite (default), mysql or postgresql to store the collection database. Users with large collections and more demanding performance requirements might prefer one of the latter two options.

#### MySQL

For basic MySQL configuration refer to the [MySQL](/index.php/MySQL "MySQL") page.

When using Amarok with MySQL you need to create a MySQL user that can access the database. To do use, enter the following:

```
# mysql -p -u root
# CREATE DATABASE amarok;
# USE amarok;
# GRANT ALL ON amarok.* TO amarok@localhost IDENTIFIED BY 'AMAROK_PASSWORD';
# FLUSH PRIVILEGES;
# quit

```

This creates a database called 'amarok' and a user of the same name with the password "AMAROK_PASSWORD" who can access said database from localhost. If you want to connect to your database computer from a different computer, change the line to

```
# GRANT ALL ON amarok.* TO amarok@'%' IDENTIFIED BY 'AMAROK_PASSWORD';

```

To configure amarok to use MySQL, enter the Configure Amarok screen, choose Collection and change the database type to MySQL. Enter the host name (usually "localhost" if on your local box, else the name of the remote box), the username ("amarok" in this example) and your chosen password. Do not forget to select the path to your music collection. Exit with OK and update your database.

#### PostgreSQL

Amarok version 1.4 can utilise a PostgreSQL database for the music collection. This feature is absent in version 2.x and unfortunately it is not intended to reintroduce it.

See [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). Install postgresql, and then set up a user and database for amarok.

If there is no existing collection then simply set the hostname, database, user and password in the Amarok settings, and then scan the music files to build the database.

To migrate an existing sqlite database to postgresql:

*   backup your collection.db
*   switch to PostgreSQL and rebuild your collection
*   quit amarok
*   get your statistics back with the following commands:

```
cd ~/.kde/share/apps/amarok && \
sqlite3 collection.db .dump | grep 'INSERT INTO "statistics"' |\
sed -e 's/,0)/,FALSE)/' -e 's/,1)/,TRUE)/' |\
psql -U <amarok-user> <amarok-db>

```

Of course, replace <amarok-user> and <amarok-db> accordingly. We need sed because otherwise psql complains we are trying to insert an integer into a boolean field.

### Shoutcast

For [reasons](/index.php/Amarok_2#SHOUTcast "Amarok 2") which have not been adequately explained, Amarok developers have removed the Shoutcast internet radio features from version 2.1.90 onwards.

Amarok version 1.4 as well as [VLC](/index.php/VLC "VLC") continue to support the Shoutcast internet radio station index and streaming as before. The index is at

_Playlists > Radio Streams > Shoutcast Streams_