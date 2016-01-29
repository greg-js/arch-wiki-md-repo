# Amarok

Related articles

*   [Amarok 1.4](/index.php/Amarok_1.4 "Amarok 1.4")

[Amarok](http://amarok.kde.org/) is a music player and organizer for Linux with an intuitive [Qt](/index.php/Qt "Qt") interface that integrates very well with [KDE](/index.php/KDE "KDE").

Amarok 2 has not yet and will not implement all features from [Amarok 1.4](/index.php/Amarok_1.4 "Amarok 1.4")[[1]](http://amarok.kde.org/blog/archives/809-Missing-features-in-Amarok-2.html), so if you are not satisfied with the new version and would rather have the old one back, refer to that article.

## Contents

*   [1 Installation](#Installation)
*   [2 Customization](#Customization)
    *   [2.1 Integration with GNOME](#Integration_with_GNOME)
    *   [2.2 Scripts and applets](#Scripts_and_applets)
    *   [2.3 Moodbar](#Moodbar)
*   [3 SHOUTcast](#SHOUTcast)
*   [4 Ampache/MP3 Streaming](#Ampache.2FMP3_Streaming)
*   [5 Collection database](#Collection_database)
    *   [5.1 MySQL](#MySQL)
    *   [5.2 PostgreSQL](#PostgreSQL)
*   [6 Audio CD Playback](#Audio_CD_Playback)
*   [7 Firefly/Daap share](#Firefly.2FDaap_share)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [amarok](https://www.archlinux.org/packages/?name=amarok) from the [official repositories](/index.php/Official_repositories "Official repositories").

Amarok now depends on Phonon, so you will have to have a working back-end selected for it. See [KDE#Phonon](/index.php/KDE#Phonon "KDE"). You may also need to install a few [codecs](/index.php/Codecs "Codecs") for use by the chosen back-end.

## Customization

### Integration with GNOME

See [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for visual integration of the main GUI.

### Scripts and applets

New scripts and applets can be found either directly from within Amarok (_Tools > Script Manager > Get More Scripts_) or at [kde-apps.org](http://kde-apps.org/content/search.php).

### Moodbar

The moodbar is a feature which turn your standard progress slider bar into a progress slider bar coloured depending on the mood of your track.

Install [moodbar](https://aur.archlinux.org/packages/moodbar/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

Then go to _Settings > Configure Amarok_ and check "Show moodbar in progress slider".

**Note:** As of February 19th Amarok 2 does **not** generate moodfiles, you can either try to follow this tutorial [[2]](http://amarok.kde.org/wiki/Moodbar)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-04-23]</sup> to create them yourself or get Amarok1 from AUR and let it generate all the .mood files for you. For the Amarok1 solution go to _Settings > Configure Amarok_, and in the general tab check the "use moods" and "store moods data files with music" boxes.

## SHOUTcast

For reasons which have not been adequately explained Amarok developers have removed the SHOUTcast Internet radio features from version 2.1.90 onwards. See the [discussion page](https://wiki.archlinux.org/index.php/Talk:Amarok_2#Shoutcast), the forum [here](http://forum.kde.org/viewtopic.php?f=116&t=83718) and the thread starting [here](http://mail.kde.org/pipermail/amarok/2009-November/009696.html).

You can get back SHOUTcast by using the "SHOUTcast service" script. Start Amarok, go _Tools > Script Manager > Get More Scripts_, search for _SHOUTcast_ install _Shoutcast Service_, restart Amarok. Then you have it in "Internet" context.

[Amarok 1.4](/index.php/Amarok_1.4 "Amarok 1.4") and [VLC](/index.php/VLC "VLC") continue to support the SHOUTcast Internet radio station index and streaming as before.

See also: [How can I use Amarok to stream to my own radio station?](http://amarok.kde.org/wiki/FAQ#How_can_I_use_Amarok_to_stream_to_my_own_radio_station.3F)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-07-5]</sup>, which recommends [Internet DJ Console](http://giss.tv/sahabuntu/doc/idjc.html), available in the AUR ([idjc](https://aur.archlinux.org/packages/idjc/)<sup><small>AUR</small></sup>).

## Ampache/MP3 Streaming

If you are streaming MP3s directly or with the Ampache plugin, you are not able to seek in tracks if you are not using the [GStreamer](/index.php/GStreamer "GStreamer") backend. Install the needed packages: [phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer) [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) [gstreamer0.10](https://www.archlinux.org/packages/?name=gstreamer0.10) [gstreamer0.10-plugins](https://www.archlinux.org/groups/x86_64/gstreamer0.10-plugins/). Then go inside Amarok to _Settings > Configure Amarok > Playback > Configure Phonon >_ _tab_ _Backend. Here make GStreamer the prefered backend_

## Collection database

Amarok 2.x can use Sqlite (default) or MySQL to store the collection database. Users with large collections and more demanding performance requirements might prefer to use mysql.

### MySQL

For basic MySQL configuration refer to the [MySQL](/index.php/MySQL "MySQL") page.

When using Amarok with MySQL you need to create a MySQL user that can access the database. To do use, enter the following:

```
# mysql -p -u root
# CREATE DATABASE amarokdb;
# USE amarokdb;
# GRANT ALL ON amarokdb.* TO amarokuser@localhost IDENTIFIED BY 'password-user';
# FLUSH PRIVILEGES;
# quit

```

This creates a database called 'amarokdb' and a user with name 'amarokuser' with the password 'password-user' who can access said database from localhost. If you want to connect to your database computer from a different computer, change the line to

```
# GRANT ALL ON amarok.* TO amarokuser@'%' IDENTIFIED BY  'password-user';

```

To configure amarok to use MySQL, enter the Configure Amarok screen, choose Database and mark "used external MySQL database". Enter the server (usually "localhost" if on your local box, else the name of the remote box), the username ("amarokuser" in this example) and your chosen password-user. Do not forget to select the path to your music collection.

### PostgreSQL

Not yet supported, [see more](http://amarok.kde.org/blog/archives/812-MySQL-in-Amarok-2-The-Reality.html)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-04-23]</sup>

## Audio CD Playback

If you are not using KDE as your Desktop Environment, Amarok may not have the utilities it needs to play back Audio CDs. [Install](/index.php/Install "Install") [kdemultimedia-audiocd-kio](https://www.archlinux.org/packages/?name=kdemultimedia-audiocd-kio) from the [official repositories](/index.php/Official_repositories "Official repositories") to obtain this functionality.

## Firefly/Daap share

To make Daap shares visible in Amarok enable the "DAAP Collection" plugin in the Amarok settings.

Install [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns) and complete the hosts line in `/etc/nsswitch.conf` to look like:

```
hosts: files mdns4_minimal [NOTFOUND=return] nis dns mdns4

```

start `avahi-daemon` [systemd](/index.php/Systemd "Systemd") service.

## See also

[List of applications#Audio players](/index.php/List_of_applications#Audio_players "List of applications")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Amarok&oldid=412036](https://wiki.archlinux.org/index.php?title=Amarok&oldid=412036)"