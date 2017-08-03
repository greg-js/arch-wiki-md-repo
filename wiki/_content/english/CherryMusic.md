[CherryMusic](http://www.fomori.org/cherrymusic/) is a web application that lets you remotely stream, browse and manage your music collection. It is intended to be an alternative to streaming services like Last.fm, Spotify and Grooveshark.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Optional dependencies](#Optional_dependencies)
*   [2 Configuration](#Configuration)
    *   [2.1 Quick start](#Quick_start)
    *   [2.2 Manual setup](#Manual_setup)
    *   [2.3 Fine tuning](#Fine_tuning)
*   [3 Tips & Tricks](#Tips_.26_Tricks)
    *   [3.1 Symlinks in "basedir"](#Symlinks_in_.22basedir.22)
    *   [3.2 Systemd service file](#Systemd_service_file)
    *   [3.3 Running in a GNU Screen session](#Running_in_a_GNU_Screen_session)
    *   [3.4 Manually adjust the search parameters of the search algorithm](#Manually_adjust_the_search_parameters_of_the_search_algorithm)
    *   [3.5 Bind CherryMusic to ports less than 1024 (without root access)](#Bind_CherryMusic_to_ports_less_than_1024_.28without_root_access.29)
*   [4 3rd Party Extensions](#3rd_Party_Extensions)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Missing module wsgiserver2 when using pip for installation](#Missing_module_wsgiserver2_when_using_pip_for_installation)
    *   [5.2 Deactivate flash blocker](#Deactivate_flash_blocker)
    *   [5.3 CherryMusic does not load on Android Chrome](#CherryMusic_does_not_load_on_Android_Chrome)
    *   [5.4 Track scrolling not working behind Nginx](#Track_scrolling_not_working_behind_Nginx)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cherrymusic](https://aur.archlinux.org/packages/cherrymusic/) package, or [cherrymusic-devel-git](https://aur.archlinux.org/packages/cherrymusic-devel-git/) for the development version.

### Optional dependencies

*   Live transcoding: [lame](https://www.archlinux.org/packages/?name=lame), [vorbis-tools](https://www.archlinux.org/packages/?name=vorbis-tools), [flac](https://www.archlinux.org/packages/?name=flac), [faad2](https://www.archlinux.org/packages/?name=faad2), [mpg123](https://www.archlinux.org/packages/?name=mpg123), [opus-tools](https://www.archlinux.org/packages/?name=opus-tools) or [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) (which replaces the aforementioned codecs plus adds WMA decoding)
*   Automatic image resizing on displayed cover art: [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)
*   Special character search terms: [python-unidecode](https://www.archlinux.org/packages/?name=python-unidecode)
*   GTK system tray icon: [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

## Configuration

### Quick start

To just get it up and running with a basic setup, issue:

```
 $ cherrymusic --setup --port 8080

```

and open the address "localhost:8080" in your browser (e.g. with [Firefox](/index.php/Firefox "Firefox")):

```
 $ firefox localhost:8080

```

This will let you configure the most important options from within the browser and you can set up the admin account.

If you want CherryMusic to run as a system service and to automatically start on boot, see [systemd service file](#Systemd_service_file).

### Manual setup

Start CherryMusic for the initial setup:

```
 $ cherrymusic

```

On first startup CherryMusic will create its data and configuration files in `~/.local/share/cherrymusic/` and `~/.config/cherrymusic/`, print a note to *stdout* and exit. Now, edit the configuration file in `~/.config/cherrymusic/cherrymusic.conf`and change the following lines to match your setup:

 `~/.config/cherrymusic/cherrymusic.conf` 
```
[...]
basedir = /path/to/your/music
[...]
port = 8080
[...]

```

Open the address [http://localhost:8080](http://localhost:8080) in your browser to create an admin account.

After logging in, populate the search database by clicking *Update Music Library* in the *Admin* panel.

If you want CherryMusic to run as a system service and to automatically start on boot, see [systemd service file](#Systemd_service_file).

There are many more options to configure, please see [this section](#Fine_tuning).

### Fine tuning

See the man pages `cherrymusic` and `cherrymusic.conf`.

## Tips & Tricks

### Symlinks in "basedir"

**Note:** This is only useful if your music is in different locations, e.g. on an internal hard drive **and** an external hard dirve.

Probably, the most modular and flexible way of populating CherryMusic's music directory (called "basedir") is to create a dedicated directory and only symlink all paths to your music collections into that directory, e.g.:

```
 $ mkdir ~/.local/share/cherrymusic/basedir
 $ ln -s /path/to/musicdir1 ~/.local/share/cherrymusic/basedir/musicdir1
 $ ln -s /path/to/musicdir2 ~/.local/share/cherrymusic/basedir/musicdir2

```

### Systemd service file

CherryMusic does not come with a daemon yet, but [both CherryMusic AUR packages](#Installation) provide a systemd service file. It can be [started](/index.php/Start "Start") as `cherrymusic@*user*.service`, where `*user*` is the user that should run CherryMusic (do not use root!).

### Running in a GNU Screen session

To keep CherryMusic running after logout, it can be run in a [GNU Screen](/index.php/GNU_Screen "GNU Screen") session.

```
$ screen -d -m -S cherrymusic cherrymusic

```

Since CherryMusic only writes the output to the GNU Screen session, there is nothing to control from within the session. It may be more convenient to use a [systemd service file](#Systemd_service_file). However, this may still be useful for debugging.

To run it in a GNU Screen session after boot, the following [systemd](/index.php/Systemd "Systemd") service file can also be created and used:

 `/etc/systemd/system/cherrymusic@.service` 
```
[Unit]
Description = CherryMusic server
Requires = network.target
After = network.target

[Service]
User = %I
Type = simple
ExecStart = /usr/bin/screen -d -m -S cherrymusic /usr/bin/cherrymusic
ExecStop = /usr/bin/screen -X -S cherrymusic quit
StandardOutput = null
PrivateTmp = true
Restart = always

[Install]
WantedBy = multi-user.target

```

To finally enable and start the service, see [systemd service file](#Systemd_service_file).

### Manually adjust the search parameters of the search algorithm

The search parameters of the search algorithm can be adjusted manually via the file `cherrymusicserver/tweak.py` within your CherryMusic installation.

**Warning:** Changing this file can potentially break CherryMusic's search function. Only proceed if you know what you are doing. It might also be a good idea to backup the file before editing.

### Bind CherryMusic to ports less than 1024 (without root access)

To bind CherryMusic (or any other application) to a port less than 1024 you normally need root access. However, you should **never run CherryMusic as root!** There are several ways around this:

*   Use a firewall ([iptables](/index.php/Iptables "Iptables") or similar) for a port redirect
*   Use [authbind](https://en.wikipedia.org/wiki/Authbind "wikipedia:Authbind")
*   Use [Capabilities](/index.php/Capabilities "Capabilities") (more exactly [setcap](/index.php/Capabilities#Other_programs_that_benefit_from_capabilities "Capabilities"))

For more information, see these references:

[https://serverfault.com/questions/268099/bind-to-ports-less-than-1024-without-root-access](https://serverfault.com/questions/268099/bind-to-ports-less-than-1024-without-root-access)
[https://www.debian-administration.org/article/386/Running_network_services_as_a_non-root_user](https://www.debian-administration.org/article/386/Running_network_services_as_a_non-root_user)
[https://stackoverflow.com/questions/413807/is-there-a-way-for-non-root-processes-to-bind-to-privileged-ports-1024-on-l](https://stackoverflow.com/questions/413807/is-there-a-way-for-non-root-processes-to-bind-to-privileged-ports-1024-on-l)

## 3rd Party Extensions

*   CherryMusic Control - A Playback control plugin for Firefox:
    [https://addons.mozilla.org/en-US/firefox/addon/cherrymusic-control](https://addons.mozilla.org/en-US/firefox/addon/cherrymusic-control)
    Which is also developed on github: [https://github.com/Sets88/cherrymusicctrl](https://github.com/Sets88/cherrymusicctrl)

## Troubleshooting

### Missing module wsgiserver2 when using pip for installation

If the error

```
ImportError: No module named wsgiserver2

```

occurs when starting CherryMusic, probably a broken CherryPy package from pip (versions `3.2.6` and `3.4.0` seem to be affected) is used. Here is a [description of the problem](http://alessiofanelli.com/cherrypy-pip-package-not-working-properly-frustration/). To fix this, uninstall CherryPy and reinstall:

```
$ pip uninstall cherrypy
$ pip install --no-use-wheel cherrypy

```

### Deactivate flash blocker

An active flash blocker can interfere with the web frontend. If you have trouble with things like track selection or playback, try whitelisting the server in your browser's flash blocker/plugin manager.

### CherryMusic does not load on Android Chrome

This might be due to AdBlock Plus being installed in the browser. CM does not feature any ads, so the problem is caused by this plug-in.

### Track scrolling not working behind Nginx

If track scrolling is not working in major desktop browsers behind Nginx and playback stops in the middle of the track and start over from the beginning, the Nginx module `ngx_http_proxy_module` [has to be configured](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_http_version).

Change the line `proxy_http_version 1.0;` to:

 `ngx_http_proxy_module` 
```
[...]
proxy_http_version 1.1;
[...]

```

## See also

*   [GitHub repository](https://github.com/devsnd/cherrymusic)
*   [https://github.com/devsnd/cherrymusic/wiki/Setup-guide](https://github.com/devsnd/cherrymusic/wiki/Setup-guide)
*   [http://fomori.org/blog/?p=687](http://fomori.org/blog/?p=687)
*   [CherryMusic website](http://www.fomori.org/cherrymusic/)