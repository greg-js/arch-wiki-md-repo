# Music Player Daemon

Related articles

*   [MPD/Tips and Tricks](/index.php/MPD/Tips_and_Tricks "MPD/Tips and Tricks")
*   [MPD/Troubleshooting](/index.php/MPD/Troubleshooting "MPD/Troubleshooting")

**[MPD](http://www.musicpd.org/)** (**m**usic **p**layer **d**aemon) is an audio player that has a server-client architecture. It plays audio files, organizes playlists and maintains a music database all while using very few resources. In order to interface with it, a separate [client](#Clients) is needed.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Global configuration](#Global_configuration)
        *   [2.1.1 Music directory](#Music_directory)
        *   [2.1.2 Start MPD](#Start_MPD)
            *   [2.1.2.1 Socket activation](#Socket_activation)
        *   [2.1.3 Configure audio](#Configure_audio)
        *   [2.1.4 Changing user](#Changing_user)
        *   [2.1.5 Timeline of MPD startup](#Timeline_of_MPD_startup)
    *   [2.2 Local configuration (per user)](#Local_configuration_.28per_user.29)
        *   [2.2.1 Autostart on tty login](#Autostart_on_tty_login)
        *   [2.2.2 Autostart in X](#Autostart_in_X)
        *   [2.2.3 Autostart with systemd](#Autostart_with_systemd)
        *   [2.2.4 Scripted configuration](#Scripted_configuration)
        *   [2.2.5 Scripted configuration for bit perfect playback](#Scripted_configuration_for_bit_perfect_playback)
    *   [2.3 Multi-mpd setup](#Multi-mpd_setup)
        *   [2.3.1 Running an icecast server](#Running_an_icecast_server)
        *   [2.3.2 Satellite setup](#Satellite_setup)
*   [3 Clients](#Clients)
    *   [3.1 Console](#Console)
    *   [3.2 Graphical](#Graphical)
    *   [3.3 Web](#Web)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mpd](https://www.archlinux.org/packages/?name=mpd) package, or [mpd-git](https://aur.archlinux.org/packages/mpd-git/)<sup><small>AUR</small></sup> for the development version.

**Note:** An alternative plug-in based implementation called [Mopidy](http://www.mopidy.com) exists. It is available as [mopidy](https://www.archlinux.org/packages/?name=mopidy) and [mopidy-git](https://aur.archlinux.org/packages/mopidy-git/)<sup><small>AUR</small></sup>. Be warned that is not a complete MPD [drop-in replacement](http://docs.mopidy.com/en/latest/ext/mpd/#limitations).

## Setup

MPD is able to run locally (per user settings), globally (settings apply to all users), and in multiple instances. The way of setting up mpd depends on the way it is intended to be used: a local configuration may prove more useful on a desktop system, for example.

In order for MPD to be able to play back audio, [ALSA](/index.php/ALSA "ALSA") or [OSS](/index.php/OSS "OSS") (optionally with [PulseAudio](/index.php/PulseAudio "PulseAudio")) needs to be setup and working.

MPD is configured in `mpd.conf`. The location of this file depends on how you want to run MPD (see the sections below). These are commonly used configuration options:

*   `pid_file` - The file where mpd stores its process ID
*   `db_file` - The music database
*   `state_file` - MPD's current state is noted here
*   `playlist_directory` - The folder where playlists are saved into
*   `music_directory` - The folder that MPD scans for music
*   `sticker_file` - The sticker database

### Global configuration

**Warning:** Users of PulseAudio with a global mpd have to implement a [workaround](/index.php/Music_Player_Daemon/Tips_and_tricks#Local_.28with_separate_mpd_user.29 "Music Player Daemon/Tips and tricks") in order to run mpd as its own user!

The default `/etc/mpd.conf` keeps the setup in `/var/lib/mpd` and uses _mpd_ as default user. However, `/var/lib/mpd` is owned by _root_ by default, we need to change this so _mpd_ can write here:

```
# chown -R mpd /var/lib/mpd

```

Edit `/etc/mpd.conf` and add a `music_directory` line with the path to your music directory:

```
music_directory "/path/to/music"

```

#### Music directory

MPD needs to have `+x` permissions on _all_ parent directories to the music collection and also read access to all directories containing music files. This conflicts with the default configuration of the user directory where many users store their music.

While there are several solutions to this problem one of these should be most practical:

*   [run MPD as user](#Local_configuration_.28per_user.29)
*   add the mpd user to your login group and grant group permission to your user directory:

```
 # gpasswd -a mpd <your login group>
 $ chmod 710 /home/<your home dir>

```

*   put your music collection to a different path (a) by moving it entirely, (b) with a bind mount or (c) with a [Btrfs subvolume](/index.php/Btrfs#Sub-volumes "Btrfs") (you should make this change persistent with an entry to `/etc/fstab` ).

The MPD config must contain only one music directory. If the music collection is contained under multiple directories, create symbolic links under the main music directory in `/var/lib/mpd`. Remember to set permissions accordingly on the directories being linked.

#### Start MPD

MPD can be controlled with `mpd.service` [using systemd](/index.php/Systemd#Using_units "Systemd"). The first startup can take some time as MPD will scan your music directory.

Test everything by starting a client application ([ncmpc](https://www.archlinux.org/packages/?name=ncmpc) is a light and easy to use client), and play some music!

##### Socket activation

If the `mpd.socket` unit (provided by [mpd](https://www.archlinux.org/packages/?name=mpd)) is enabled while `mpd.service` is disabled, systemd will not start mpd immediately, but it will listen on the appropriate sockets. When an mpd client attempts to connect on one of those sockets, systemd will start `mpd.service` and transparently hand over control of those ports to the mpd process.

If you prefer to listen on different UNIX sockets or network ports (even multiple sockets of each type), or if you prefer not to listen on network ports at all, [edit](/index.php/Systemd#Editing_provided_units "Systemd") the `mpd.socket` unit appropriately **and** modify `/etc/mpd.conf` to match the configuration (see `man 5 mpd.conf` for details).

#### Configure audio

To change the volume for mpd independent from other programs, uncomment or add this switch in mpd.conf:

 `/etc/mpd.conf` 

```
mixer_type			"software"

```

Users of [ALSA](/index.php/ALSA "ALSA") will want to have the following device definition, which allows software volume control in the MPD client to control the volume separately from other applications.

 `/etc/mpd.conf` 

```
audio_output {
        type            "alsa"
        name            "My Sound Card"
        mixer_type      "software"      # optional
}
```

Users of [PulseAudio](/index.php/PulseAudio "PulseAudio") will need to make the following modification:

 `/etc/mpd.conf` 

```
audio_output {
        type            "pulse"
        name            "pulse audio"
}
```

PulseAudio supports multiple advanced operations, e.g. transferring the audio to a different machine. For advanced configuration with MPD see [Music Player Daemon Community Wiki](http://mpd.wikia.com/wiki/PulseAudio).

#### Changing user

Changing the group that MPD runs as may result in errors like `output: Failed to open "My ALSA Device"`, `[alsa]: Failed to open ALSA device "default": No such file or directory` or `player_thread: problems opening audio device while playing "Song Name.mp3"`.

This is because the MPD users need to be part of the _audio_ group to access sound devices under `/dev/snd/`. To fix it add user make the MPD user part of the _audio_ group:

```
# gpasswd -a **mpd** audio

```

#### Timeline of MPD startup

To depict when MPD drops its superuser privileges and assumes those of the user set in the configuration, the timeline of a normal MPD startup is listed here:

1.  Since MPD is started as root by systemd, it first reads the `/etc/mpd.conf` file.
2.  MPD reads the user variable in the `/etc/mpd.conf` file, and changes from root to this user.
3.  MPD then reads the contents of the `/etc/mpd.conf` file and configures itself accordingly.

Notice that MPD changes the running user from root to the one named in the `/etc/mpd.conf` file. This way, uses of `~` in the configuration file point correctly to the home user's directory, and not root's directory. It may be worthwhile to change all uses of `~` to `/home/username` to avoid any confusion over this aspect of MPD's behavior.

### Local configuration (per user)

MPD can be configured per user (rather than the typical method of configuring MPD globally). Running MPD as a normal user has the benefits of:

*   A single directory `~/.config/mpd/` (or any other directory under `$HOME`) that will contain all the MPD configuration files.
*   Easier to avoid unforeseen read/write permission errors.

Good practice is to create a single directory for the required files and playlists. It can be any directory for which you have read and write access, e.g. `~/.config/mpd/` or `~/.mpd/`. This section assumes it is `~/.config/mpd/`, which corresponds to the default value of `$XDG_CONFIG_HOME` (part of [XDG Base Directory Specification](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html)).

MPD searches for a config file in `$XDG_CONFIG_HOME/mpd/mpd.conf` and then `~/.mpdconf`. It is also possible to pass other path as command line argument.

Copy the example configuration file to desired location, for example:

```
$ cp /usr/share/doc/mpd/mpdconf.example ~/.config/mpd/mpd.conf

```

Edit `~/.config/mpd/mpd.conf` and specify the required files:

 `~/.config/mpd/mpd.conf` 

```
# Required files
db_file            "~/.config/mpd/database"
log_file           "~/.config/mpd/log"

# Optional
music_directory    "~/Music"
playlist_directory "~/.config/mpd/playlists"
pid_file           "~/.config/mpd/pid"
state_file         "~/.config/mpd/state"
sticker_file       "~/.config/mpd/sticker.sql"

```

Create all the files and directories as configured above:

```
$ mkdir ~/.config/mpd/playlists
$ touch ~/.config/mpd/{database,log,pid,state,sticker.sql}

```

When the paths of required files are configured, MPD can be started. To specify custom location of the configuration file:

```
$ mpd _config_file_

```

#### Autostart on tty login

To start MPD on login add the following to `~/.profile` (or another [autostart file](/index.php/Autostarting#Shells "Autostarting")):

```
# MPD daemon start (if no other user instance exists)
[ ! -s ~/.config/mpd/pid ] && mpd

```

#### Autostart in X

If you use a [desktop environment](/index.php/Desktop_environment "Desktop environment"), place the following file in `~/.config/autostart/`:

 `~/.config/autostart/mpd.desktop` 

```
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=Music Player Daemon
Comment=Server for playing audio files
Exec=mpd
StartupNotify=false
Terminal=false
Hidden=false
X-GNOME-Autostart-enabled=false

```

If you do not use a DE, place the line from [#Autostart on tty login](#Autostart_on_tty_login) in your [autostart file](/index.php/Autostarting#Graphical "Autostarting").

#### Autostart with systemd

**Note:** It is assumed that you already have systemd user-session manager running (which should be default). See the [systemd/User](/index.php/Systemd/User "Systemd/User") page for details.

The package [mpd](https://www.archlinux.org/packages/?name=mpd) provides user service file in `/usr/lib/systemd/user/mpd.service`. The configuration file is expected to exist either in `~/.mpdconf` or `~/.config/mpd/mpd.conf`, see [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") if you would like to use different path. The process is not started as root, so you should not use the `user` and `group` variables in the MPD configuration file, the process already has user permissions and therefore it is not necessary to change them further.

All you have to do is enable and start the `mpd` [user service](/index.php/Systemd/User#User_Services "Systemd/User").

**Note:**

*   [mpd](https://www.archlinux.org/packages/?name=mpd) provides also system service file in `/usr/lib/systemd/system/mpd.service`, but as the process is started as root, it does not read the user configuration file and falls back to `/etc/mpd.conf`. [Global configuration](#Global_configuration) is described in other section.
*   Make sure to disable every other method of starting mpd you used before.

#### Scripted configuration

You can use a [script](http://dl.53280.de/mpdsetup.sh) to create the proper directory structure, configuration files and prompt for the location of the user's Music directory.

#### Scripted configuration for bit perfect playback

You can use a [bash script](http://lacocina.nl/audiophile-mpd) to also create a valid mpd configuration file which focusses on bit perfect audio playback. That is playback without any resampling or format conversion. It does this by setting audio output parameters to use a direct alsa hwardware address (like `hw:0,0`). The script detects and lists which playback interfaces alsa supports. When one interface is found it uses that one, if multiple are found it prompts the user which one to use. When not specified on the command line, it auto configures things like the music_directory and mpd's home directory by using freedesktop.org XDG configuration.

### Multi-mpd setup

#### Running an icecast server

For a second MPD (e.g., with icecast output to share music over the network) using the same music and playlist as the one above, simply copy the above configuration file and make a new file (e.g., `/home/username/.mpd/config-icecast`), and only change the log_file, error_file, pid_file, and state_file parameters (e.g., `mpd-icecast.log`, `mpd-icecast.error`, and so on); using the same directory paths for the music and playlist directories would ensure that this second mpd would use the same music collection as the first one e.g., creating and editing a playlist under the first daemon would affect the second daemon as well. Users do not have to create the same playlists all over again for the second daemon. Call this second daemon the same way from `~/.xinitrc` above. (Just be sure to have a different port number, so as to not conflict with the first mpd daemon).

#### Satellite setup

The method above works, but at least in theory could lead to issues with the database, when both mpd instances try to write to the same database file. MPD has a [satellite mode](http://www.musicpd.org/doc/user/advanced_config.html#satellite) where one instance can receive the database from an already running mpd instance.

in your config-icecast add this, where host and port reflect your primary mpd server.

```
database {
    plugin "proxy"
    host "localhost"
    port "6600"
}

```

## Clients

A separate client is needed to control mpd. See a long list of clients at the [mpd wiki](http://mpd.wikia.com/wiki/Clients). Popular options are:

### Console

*   **mpc** — Command line user interface for MPD server

	[http://www.musicpd.org/clients/mpc/](http://www.musicpd.org/clients/mpc/) || [mpc](https://www.archlinux.org/packages/?name=mpc)

*   **ncmpc** — Ncurses client for mpd

	[http://www.musicpd.org/clients/ncmpc/](http://www.musicpd.org/clients/ncmpc/) || [ncmpc](https://www.archlinux.org/packages/?name=ncmpc)

*   **[ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")** — Almost exact clone of ncmpc with some new features written in C++ (tag editor, search engine)

	[http://ncmpcpp.rybczak.net/](http://ncmpcpp.rybczak.net/) || [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp)

*   **pms** — Highly configurable and accessible ncurses client

	[http://pms.sourceforge.net/](http://pms.sourceforge.net/) || [pmus](https://aur.archlinux.org/packages/pmus/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pmus)]</sup>

*   **vimpc** — Ncurses based MPD client with vi-like key bindings

	[http://sourceforge.net/projects/vimpc/](http://sourceforge.net/projects/vimpc/) || [vimpc](https://aur.archlinux.org/packages/vimpc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/vimpc)]</sup>

### Graphical

*   **Ario** — Very feature-rich GTK2 GUI client for mpd, inspired by Rhythmbox

	[http://ario-player.sourceforge.net/](http://ario-player.sourceforge.net/) || [ario](https://www.archlinux.org/packages/?name=ario)

*   **QmpdClient** — GUI client written with Qt 4.x

	[http://bitcheese.net/wiki/QMPDClient](http://bitcheese.net/wiki/QMPDClient) || [qmpdclient](https://www.archlinux.org/packages/?name=qmpdclient)

*   **Sonata** — Elegant Python GTK+ client

	[http://www.nongnu.org/sonata/](http://www.nongnu.org/sonata/) || [sonata](https://www.archlinux.org/packages/?name=sonata)

*   **gmpc** — GTK2 frontend for Music Player Daemon. It is designed to be lightweight and easy to use, while providing full access to all of MPD's features. Users are presented with several different methods to browse through their music. It can be extended by plugins, of which many are available.

	[http://gmpclient.org/](http://gmpclient.org/) || [gmpc](https://www.archlinux.org/packages/?name=gmpc)

*   **Cantata** — High-feature, Qt4, Qt5 or KDE4 client for MPD with very configurable interface

	[https://code.google.com/p/cantata/](https://code.google.com/p/cantata/) || [cantata](https://www.archlinux.org/packages/?name=cantata)

### Web

*   **Patchfork** — Web client for MPD written in PHP and Ajax

	[http://mpd.wikia.com/wiki/Client:Pitchfork](http://mpd.wikia.com/wiki/Client:Pitchfork) || [patchfork-git](https://aur.archlinux.org/packages/patchfork-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/patchfork-git)]</sup>.

## See also

*   [MPD Forum](http://forum.musicpd.org/)
*   [MPD User Manual](http://www.musicpd.org/doc/user/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Music_Player_Daemon "wikipedia:Music Player Daemon")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Music_Player_Daemon&oldid=417054](https://wiki.archlinux.org/index.php?title=Music_Player_Daemon&oldid=417054)"