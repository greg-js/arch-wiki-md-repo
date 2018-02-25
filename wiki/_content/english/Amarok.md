[Amarok](https://amarok.kde.org/) is a music player and organizer for Linux with an intuitive [Qt](/index.php/Qt "Qt") interface that integrates very well with [KDE](/index.php/KDE "KDE").

## Contents

*   [1 Installation](#Installation)
*   [2 Customization](#Customization)
    *   [2.1 Integration with GNOME](#Integration_with_GNOME)
    *   [2.2 Scripts and applets](#Scripts_and_applets)
    *   [2.3 Moodbar](#Moodbar)
*   [3 SHOUTcast](#SHOUTcast)
*   [4 Ampache/MP3 streaming](#Ampache.2FMP3_streaming)
*   [5 Collection database](#Collection_database)
    *   [5.1 MySQL](#MySQL)
    *   [5.2 PostgreSQL](#PostgreSQL)
*   [6 Audio CD playback](#Audio_CD_playback)
*   [7 Firefly/Daap share](#Firefly.2FDaap_share)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [amarok](https://www.archlinux.org/packages/?name=amarok) package.

Amarok now depends on Phonon, so you will have to have a working back-end selected for it. See [KDE#Phonon](/index.php/KDE#Phonon "KDE"). You may also need to install a few [codecs](/index.php/Codecs "Codecs") for use by the chosen back-end.

## Customization

### Integration with GNOME

See [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for visual integration of the main GUI.

### Scripts and applets

New scripts and applets can be found either directly from within Amarok (*Tools > Script Manager > Get More Scripts*) or at [kde-apps.org](http://kde-apps.org/content/search.php).

### Moodbar

The moodbar is a feature which turn your standard progress slider bar into a progress slider bar coloured depending on the mood of your track.

Install [moodbar](https://aur.archlinux.org/packages/moodbar/) from the [AUR](/index.php/AUR "AUR").

Then go to *Settings > Configure Amarok* and check "Show moodbar in progress slider".

**Note:** As of February 19th Amarok 2 does **not** generate moodfiles, you can either try to follow this tutorial [[1]](http://amarok.kde.org/wiki/Moodbar) to create them yourself or get Amarok1 from AUR and let it generate all the .mood files for you. For the Amarok1 solution go to *Settings > Configure Amarok*, and in the general tab check the "use moods" and "store moods data files with music" boxes.

## SHOUTcast

To get SHOUTcast use the "SHOUTcast service" script. Start Amarok, go *Tools > Script Manager > Get More Scripts*, search for *SHOUTcast* install *Shoutcast Service*, restart Amarok. Then you have it in "Internet" context.

See also: [How can I use Amarok to stream to my own radio station?](https://userbase.kde.org/Amarok/Manual/Various/FAQ/en#How_can_I_use_Amarok_to_stream_to_my_own_radio_station.3F), which recommends [Internet DJ Console](http://giss.tv/sahabuntu/doc/idjc.html), available in the AUR ([idjc](https://aur.archlinux.org/packages/idjc/)).

## Ampache/MP3 streaming

If you are streaming MP3s directly or with the Ampache plugin, you are not able to seek in tracks if you are not using the [GStreamer](/index.php/GStreamer "GStreamer") backend. Install the needed packages: [phonon-qt4-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt4-gstreamer) [phonon-qt5-gstreamer](https://www.archlinux.org/packages/?name=phonon-qt5-gstreamer) [gst-libav](https://www.archlinux.org/packages/?name=gst-libav). Then go inside Amarok to *Settings > Configure Amarok > Playback > Configure Phonon >* *tab* *Backend. Here make GStreamer the prefered backend*

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

Not yet supported, [see more](http://amarok.kde.org/blog/archives/812-MySQL-in-Amarok-2-The-Reality.html)

## Audio CD playback

If you are not using KDE as your Desktop Environment, Amarok may not have the utilities it needs to play back Audio CDs. [Install](/index.php/Install "Install") [audiocd-kio](https://www.archlinux.org/packages/?name=audiocd-kio) to obtain this functionality.

## Firefly/Daap share

To make Daap shares visible in Amarok enable the "DAAP Collection" plugin in the Amarok settings.

Install [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns) and complete the hosts line in `/etc/nsswitch.conf` to look like:

```
hosts: files mdns4_minimal [NOTFOUND=return] nis dns mdns4

```

start `avahi-daemon` [systemd](/index.php/Systemd "Systemd") service.

## See also

[List of applications#Audio players](/index.php/List_of_applications#Audio_players "List of applications")