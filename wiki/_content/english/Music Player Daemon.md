Related articles

*   [MPD/Tips and Tricks](/index.php/MPD/Tips_and_Tricks "MPD/Tips and Tricks")
*   [MPD/Troubleshooting](/index.php/MPD/Troubleshooting "MPD/Troubleshooting")

**[MPD](http://www.musicpd.org/)** (music player daemon) is an audio player that has a server-client architecture. It plays audio files, organizes playlists and maintains a music database, all while using very few resources. In order to interface with it, a separate [client](#Clients) is needed.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Per-user configuration](#Per-user_configuration)
        *   [2.1.1 Configure the location of files and directories](#Configure_the_location_of_files_and_directories)
        *   [2.1.2 Audio configuration](#Audio_configuration)
        *   [2.1.3 Autostart with systemd](#Autostart_with_systemd)
        *   [2.1.4 Autostart on tty login](#Autostart_on_tty_login)
        *   [2.1.5 Scripted configuration](#Scripted_configuration)
    *   [2.2 System-wide configuration](#System-wide_configuration)
        *   [2.2.1 Music directory](#Music_directory)
        *   [2.2.2 Start with systemd](#Start_with_systemd)
            *   [2.2.2.1 Socket activation](#Socket_activation)
        *   [2.2.3 User id startup workflow](#User_id_startup_workflow)
    *   [2.3 Multi-MPD setup](#Multi-MPD_setup)
        *   [2.3.1 Running an icecast server](#Running_an_icecast_server)
        *   [2.3.2 Satellite setup](#Satellite_setup)
*   [3 Clients](#Clients)
    *   [3.1 Console](#Console)
    *   [3.2 Graphical](#Graphical)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mpd](https://www.archlinux.org/packages/?name=mpd) package, or [mpd-git](https://aur.archlinux.org/packages/mpd-git/) for the development version.

## Configuration

MPD is able to run in [#Per-user configuration](#Per-user_configuration) or [#System-wide configuration](#System-wide_configuration) mode (settings apply to all users). Also it is possible to run multiple instances of MPD in a [#Multi-MPD setup](#Multi-MPD_setup). The way of setting up MPD depends on the way it is intended to be used: a local per-user configuration is easier to setup and may prove more adapted on a desktop system.

In order for MPD to be able to playback audio, [ALSA](/index.php/ALSA "ALSA"), optionally with [PulseAudio](/index.php/PulseAudio "PulseAudio"), must be setup and working. The [#Audio configuration](#Audio_configuration) section thereafter describes the parameters needed for *ALSA* or *PulseAudio*.

MPD is configured in the file [mpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpd.conf.5) which can be located in various paths depending on the setup chosen (system-wide or per-user). In short, the two common locations used are:

1.  `~/.config/mpd/mpd.conf` in per-user configuration mode, this is the first location searched,
2.  `/etc/mpd.conf` in system-wide configuration.

For indication, some of the most commonly used configuration options are listed thereafter:

*   `pid_file` - The file where MPD stores its process ID
*   `db_file` - The music database
*   `state_file` - MPD's current state is noted here
*   `playlist_directory` - The folder where playlists are saved into
*   `music_directory` - The folder that MPD scans for music
*   `sticker_file` - The sticker database

### Per-user configuration

MPD can be configured per-user. Running it as a normal user has the benefits of:

*   Regrouping into one single directory `~/.config/mpd/` (or any other directory under `$HOME`) all the MPD configuration files.
*   Avoiding unforeseen directory and file permission errors.

#### Configure the location of files and directories

In user mode, the configuration is read from `$XDG_CONFIG_HOME/mpd/mpd.conf`. We will assume here `$XDG_CONFIG_HOME` equals `~/.config` which is the recommended [XDG base directory specification](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html).

To build the user configuration, the [MPD configuration example](https://raw.githubusercontent.com/MusicPlayerDaemon/MPD/master/doc/mpdconf.example) included in the package is a good starting point, copy it using the following lines:

```
$ mkdir ~/.config/mpd
$ cp /usr/share/doc/mpd/mpdconf.example ~/.config/mpd/mpd.conf

```

A good practice is to use this newly created `~/.config/mpd/` directory to store, together with the configuration file, other MPD related files like the database or the playlists. The user must have read write access to this directory.

Then edit the configuration file in order to specify the required and optional files and directories:

 `~/.config/mpd/mpd.conf` 
```
# Recommended location for database
db_file            "~/.config/mpd/database"

# Logs to systemd journal
log_file           "syslog"

# The music directory is by default the XDG directory, uncomment to amend and choose a different directory
#music_directory    "~/music"

# Uncomment to refresh the database whenever files in the music_directory are changed
#auto_update "yes"

# Uncomment to enable the functionalities
#playlist_directory "~/.config/mpd/playlists"
#pid_file           "~/.config/mpd/pid"
#state_file         "~/.config/mpd/state"
#sticker_file       "~/.config/mpd/sticker.sql"

```

If playlists are enabled in the configuration, the specified playlist directory must be created:

```
$ mkdir ~/.config/mpd/playlists

```

MPD can now be started (an optional custom location for the configuration file can be specified):

```
$ mpd *[config_file]*

```

In order to build the database file, *MPD* must scan into the `music_directory` defined above. A MPD client is required to request this task, for example with [mpc](https://www.archlinux.org/packages/?name=mpc) the command is:

```
$ mpc update

```

or alternatively one can set the option `auto_update` to `"yes"` in the configuration to refresh the database whenever files are changed in `music_directory`.

#### Audio configuration

If [ALSA](/index.php/ALSA "ALSA") is used, **autodetection** of the default device should work out of the box without any particular setting. If not, the syntax for ALSA audio output definition is provided thereafter; the required `name` parameter specifies a unique name for the audio output. The exact device as displayed using `aplay --list-pcm` from the package [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) can optionally be indicated with the `device` option.

 `~/.config/mpd/mpd.conf` 
```
audio_output {
        type          "alsa"
        name          "*ALSA sound card*"
        # Optional
        #device        "*iec958:CARD=Intel,DEV=0*"
        #mixer_control "PCM"
}
```

Users of [PulseAudio](/index.php/PulseAudio "PulseAudio") will need to make the following modification:

 `~/.config/mpd/mpd.conf` 
```
audio_output {
        type            "pulse"
        name            "*pulse audio*"
}
```

User will also have to edit `/etc/pulse/client.conf` and change the `autospawn` option to `yes` in order to allow the MPD user to use PulseAudio. It will be necessary to restart PulseAudio after making this modification.

#### Autostart with systemd

The [mpd](https://www.archlinux.org/packages/?name=mpd) package provides a [user service](/index.php/Systemd/User "Systemd/User") file. The service starts the process as user, there is no need to change permission nor use the `user` and `group` variables in the MPD configuration file.

[start/enable](/index.php/Start/enable "Start/enable") the user unit `mpd.service` (i.e. with the `--user` flag).

**Note:** The configuration file is read from `~/.config/mpd/mpd.conf`, see [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") if you would like to indicate a custom configuration file path.

#### Autostart on tty login

To start MPD on login add the following to `~/.profile` or another [autostart file](/index.php/Autostarting "Autostarting"):

```
# MPD daemon start (if no other user instance exists)
[ ! -s ~/.config/mpd/pid ] && mpd

```

#### Scripted configuration

The following tool provides assistance for MPD configuration:

*   **[mpd-configure](http://lacocina.nl/audiophile-mpd)** — Create a MPD configuration optimized for [bit perfect](https://www.musicpd.org/doc/user/advanced_usage.html#bit_perfect) audio playback, without any resampling or conversion, using the ALSA interface hardware address (hw:x,y)

	[https://github.com/ronalde/mpd-configure](https://github.com/ronalde/mpd-configure) || no package

### System-wide configuration

**Note:** Users of PulseAudio with a system-wide MPD configuration have to implement a [workaround](/index.php/Music_Player_Daemon/Tips_and_tricks#Local_(with_separate_mpd_user) "Music Player Daemon/Tips and tricks") in order to run MPD as its own user!

The default `/etc/mpd.conf` keeps the setup in `/var/lib/mpd` which is assigned to user as well as primary group MPD.

#### Music directory

The music directory is defined by the option `music_directory` in the configuration file `/etc/mpd.conf`.

MPD needs to have execute permission on *all* parent directories of the music collection and also read access to all directories containing music files. This may conflict with the default configuration of the user directory, like `~/Music`, where the music is stored.

While there are several solutions to this issue, one of these should be most practical:

*   Switch to the [#Per-user configuration](#Per-user_configuration) mode instead
*   Add the `mpd` user to the user's group and grant group execute permission to the user directory. This way the `mpd` user has permission to open the user directory:

```
# gpasswd -a mpd *user_group*
$ chmod 710 /home/*user_directory*

```

*   Store the music collection in a different path, either:
    *   by moving it entirely,
    *   with a bind mount,
    *   or with [Btrfs#Subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") (you should make this change persistent with an entry to `/etc/fstab` ).

The MPD configuration file must define only one music directory. If the music collection is contained under multiple directories, create symbolic links under the main music directory in `/var/lib/mpd`. Remember to set permissions accordingly on the directories being linked.

#### Start with systemd

MPD can be controlled with `mpd.service` [using systemd](/index.php/Systemd#Using_units "Systemd"). The first startup can take some time as MPD will scan your music directory.

Test everything by starting a client application ([ncmpc](https://www.archlinux.org/packages/?name=ncmpc) is a light and easy to use client), and play some music!

##### Socket activation

[mpd](https://www.archlinux.org/packages/?name=mpd) provides a `mpd.socket` unit. If `mpd.socket` is enabled (and `mpd.service` is disabled), systemd will not start MPD immediately, it will just listen to the appropriate sockets. Then, whenever an MPD client attempts to connect to one of these sockets, systemd will start `mpd.service` and transparently hand over control of these ports to the MPD process.

If you prefer to listen to different UNIX sockets or network ports (even multiple sockets of each type), or if you prefer not to listen to network ports at all, [edit](/index.php/Edit "Edit") the `mpd.socket` unit appropriately **and** modify `/etc/mpd.conf` to match the configuration (see [mpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpd.conf.5) for details).

#### User id startup workflow

MPD should never run as *root*, you may use the `user` option in the configuration to make MPD change its user id after initialization. Do not use this option if you start MPD as an unprivileged user. To describe how MPD drops its superuser privileges and switch to those of the user set in the configuration, the steps of a normal MPD startup are listed thereafter:

1.  Since MPD is started as *root* by systemd, it first reads the `/etc/mpd.conf` file.
2.  MPD reads the `user` variable in the configuration, and changes from *root* to this user.
3.  MPD then reads the rest of the configuration file and configures itself accordingly. Uses of `~` in the configuration file points to the home user's directory, and not root's directory.

### Multi-MPD setup

#### Running an icecast server

For a second MPD (e.g., with icecast output to share music over the network) using the same music and playlist as the one above, simply copy the above configuration file and make a new file (e.g., `/home/username/.mpd/config-icecast`), and only change the log_file, error_file, pid_file, and state_file parameters (e.g., `mpd-icecast.log`, `mpd-icecast.error`, and so on); using the same directory paths for the music and playlist directories would ensure that this second MPD would use the same music collection as the first one e.g., creating and editing a playlist under the first daemon would affect the second daemon as well. Users do not have to create the same playlists all over again for the second daemon. Call this second daemon the same way from `~/.xinitrc` above. (Just be sure to have a different port number, so as to not conflict with the first MPD daemon).

#### Satellite setup

The method above works, but at least in theory could lead to issues with the database, when both MPD instances try to write to the same database file. MPD has a [satellite mode](http://www.musicpd.org/doc/user/advanced_config.html#satellite) where one instance can receive the database from an already running MPD instance.

in your config-icecast add this, where host and port reflect your primary MPD server.

```
database {
    plugin "proxy"
    host "localhost"
    port "6600"
}

```

## Clients

A separate client is needed to control MPD. See a long list of clients at the [mpd website](https://www.musicpd.org/clients/). Popular options are:

### Console

*   **clerk** — MPD client using [Rofi](/index.php/Rofi "Rofi").

	[https://github.com/carnager/clerk](https://github.com/carnager/clerk) || [clerk-git](https://aur.archlinux.org/packages/clerk-git/)

*   **FMUI** — Console user interface created with [fzf](/index.php/Fzf "Fzf") and mpc.

	[https://github.com/seebye/fmui](https://github.com/seebye/fmui) || [fmui-git](https://aur.archlinux.org/packages/fmui-git/)

*   **mpc** — Command line user interface for MPD server.

	[http://www.musicpd.org/clients/mpc/](http://www.musicpd.org/clients/mpc/) || [mpc](https://www.archlinux.org/packages/?name=mpc)

*   **ncmpc** — Ncurses client for MPD.

	[http://www.musicpd.org/clients/ncmpc/](http://www.musicpd.org/clients/ncmpc/) || [ncmpc](https://www.archlinux.org/packages/?name=ncmpc)

*   **[ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")** — Almost exact clone of ncmpc with some new features written in C++ (tag editor, search engine).

	[http://ncmpcpp.rybczak.net/](http://ncmpcpp.rybczak.net/) || [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp)

*   **ncmpy** — Curses-based MPD client written in Python.

	[http://ncmpcpp.rybczak.net/](http://ncmpcpp.rybczak.net/) || [ncmpy](https://aur.archlinux.org/packages/ncmpy/)

*   **nncmpp** — Yet another MPD client. It is in effect a simplified TUI version of Sonata.

	[http://ncmpcpp.rybczak.net/](http://ncmpcpp.rybczak.net/) || [nncmpp-git](https://aur.archlinux.org/packages/nncmpp-git/)

*   **pms** — Highly configurable and accessible ncurses client written in Go.

	[https://ambientsound.github.io/pms/](https://ambientsound.github.io/pms/) || [pmus-git](https://aur.archlinux.org/packages/pmus-git/)

*   **vimpc** — Ncurses based MPD client with vi-like key bindings.

	[https://github.com/boysetsfrog/vimpc](https://github.com/boysetsfrog/vimpc) || [vimpc-git](https://aur.archlinux.org/packages/vimpc-git/)

### Graphical

*   **Ario** — Very feature-rich GTK3 GUI client for MPD, inspired by [Rhythmbox](/index.php/Rhythmbox "Rhythmbox").

	[http://ario-player.sourceforge.net/](http://ario-player.sourceforge.net/) || [ario](https://www.archlinux.org/packages/?name=ario)

*   **Cantata** — High-feature, Qt4, Qt5 or KDE client for MPD with very configurable interface.

	[https://github.com/CDrummond/cantata](https://github.com/CDrummond/cantata) || [cantata](https://www.archlinux.org/packages/?name=cantata)

*   **GMPC** — Gnome Music Player Client. GTK+ frontend for MPD. It is designed to be lightweight and easy to use, while providing full access to all of MPD's features. Users are presented with several different methods to browse through their music. It can be extended by plugins, of which many are available.

	[http://gmpclient.org/](http://gmpclient.org/) || [gmpc](https://www.archlinux.org/packages/?name=gmpc)

*   **pymp'd** — A GTK+ front end client for the music playing daemon MPD.

	[http://pympd.sourceforge.net](http://pympd.sourceforge.net) || [pympd](https://www.archlinux.org/packages/?name=pympd)

*   **QMPDClient** — Qt4 GUI client.

	[http://bitcheese.net/wiki/QMPDClient](http://bitcheese.net/wiki/QMPDClient) || [qmpdclient](https://www.archlinux.org/packages/?name=qmpdclient)

*   **Quimup** — Simple Qt5 frontend for MPD written in C++.

	[https://sourceforge.net/projects/quimup/](https://sourceforge.net/projects/quimup/) || [quimup](https://aur.archlinux.org/packages/quimup/)

*   **RompЯ** — Web client for MPD.

	[https://fatg3erman.github.io/RompR/](https://fatg3erman.github.io/RompR/) || [rompr](https://aur.archlinux.org/packages/rompr/)

*   **SkyMPC** — Simple MPD client, powered by Qt5.

	[https://github.com/soramimi/SkyMPC](https://github.com/soramimi/SkyMPC) || [skympc-git](https://aur.archlinux.org/packages/skympc-git/)

*   **Sonata** — Elegant Python GTK+ client.

	[http://www.nongnu.org/sonata/](http://www.nongnu.org/sonata/) || [sonata](https://www.archlinux.org/packages/?name=sonata)

*   **Xfce MPD Panel Plugin** — MPD plugin for [Xfce](/index.php/Xfce "Xfce")4 panel.

	[http://goodies.xfce.org/projects/panel-plugins/xfce4-mpc-plugin](http://goodies.xfce.org/projects/panel-plugins/xfce4-mpc-plugin) || [xfce4-mpc-plugin](https://www.archlinux.org/packages/?name=xfce4-mpc-plugin)

*   **Xfmpc** — Graphical GTK+ MPD client focusing on low footprint.

	[http://goodies.xfce.org/projects/applications/xfmpc](http://goodies.xfce.org/projects/applications/xfmpc) || [xfmpc](https://www.archlinux.org/packages/?name=xfmpc)

*   **ympd** — Standalone MPD Web GUI written in C, utilizing Websockets and Bootstrap/JS.

	[https://ympd.org/](https://ympd.org/) || [ympd](https://aur.archlinux.org/packages/ympd/)

## See also

*   [MPD Forum](http://forum.musicpd.org/)
*   [MPD User Manual](http://www.musicpd.org/doc/user/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Music_Player_Daemon "wikipedia:Music Player Daemon")
*   [GitHub repository](https://github.com/MusicPlayerDaemon/MPD)
*   [mopidy](https://www.archlinux.org/packages/?name=mopidy) is an alternative to MPD written in Python. Note it is not a complete MPD replacement, its advantage is that it has plug-ins for playing music from cloud services like Spotify, SoundCloud, and Google Play Music. However, the project is not that active and some of its plugins are not maintained.