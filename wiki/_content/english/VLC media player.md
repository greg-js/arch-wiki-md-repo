From the project [home page](https://www.videolan.org/vlc/):

	VLC is a free and open source cross-platform multimedia player and framework that plays most multimedia files as well as DVD, Audio CD, VCD, and various streaming protocols.

## Contents

*   [1 Installation](#Installation)
*   [2 Language](#Language)
*   [3 Skins](#Skins)
*   [4 Web interface](#Web_interface)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Twitch.tv streaming over VLC](#Twitch.tv_streaming_over_VLC)
    *   [5.2 Playing streamed content from a local DLNA server](#Playing_streamed_content_from_a_local_DLNA_server)
    *   [5.3 Control using hotkeys or cli](#Control_using_hotkeys_or_cli)
    *   [5.4 Preventing multiple instances](#Preventing_multiple_instances)
    *   [5.5 Hardware video acceleration](#Hardware_video_acceleration)
    *   [5.6 systemd service](#systemd_service)
    *   [5.7 Chromecast support](#Chromecast_support)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Video broken or other issue after upgrade](#Video_broken_or_other_issue_after_upgrade)
    *   [6.2 Segmentation fault](#Segmentation_fault)
    *   [6.3 Missing icons in dropdown menus](#Missing_icons_in_dropdown_menus)
    *   [6.4 Failed to open VDPAU backend](#Failed_to_open_VDPAU_backend)
    *   [6.5 No playback via SFTP of media files names containing spaces](#No_playback_via_SFTP_of_media_files_names_containing_spaces)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [vlc](https://www.archlinux.org/packages/?name=vlc) package.

Notable variants are:

*   [vlc-git](https://aur.archlinux.org/packages/vlc-git/) - Development branch.
*   [vlc-nox](https://aur.archlinux.org/packages/vlc-nox/) - Without X support.

## Language

VLC does not offer an option to change language in its *Preferences* menu. But you can use the *LANGUAGE=* prefix. For instance, modify the `/usr/share/applications/vlc.desktop` line:

```
Exec=/usr/bin/vlc %U

```

to:

```
Exec=LANGUAGE=fr /usr/bin/vlc %U

```

to switch VLC interface to French.

## Skins

VLC can be "skinned" for a different look and feel. You can get skins at the [skins website](https://www.videolan.org/vlc/skins.php).

To install a skin download it and move it to `~/.local/share/vlc/skins2/`.

Open up VLC, click *Tools > Preferences*. When the preferences window opens up you should be in the "Interface" tab

Choose the "Use custom skin" radio button, and select the downloaded skin.

Restart VLC for the change to take effect.

## Web interface

Run VLC with the parameter `--extraintf=http` to use both the desktop and web interface. The `--http-host` parameter specifies the address to, which is `localhost` by default. To set a password, use `--http-password`, otherwise VLC will not allow you to log in.

```
# vlc --extraintf=http --http-host 0.0.0.0 --http-port 8080 --http-password 'yourpasswordhere'

```

Or you can enable this feature in the UI by navigating to *View > Add Interface > Web Interface*.

VLC defaults to port 8080: [http://127.0.0.1:8080](http://127.0.0.1:8080)

Edit `/usr/share/vlc/lua/http/.hosts` to allow remote connections. You will need to restart VLC in order for changes to take effect.

## Tips and tricks

### Twitch.tv streaming over VLC

See [Streamlink#Twitch](/index.php/Streamlink#Twitch "Streamlink").

### Playing streamed content from a local DLNA server

If you find that trying to play uPNP/DLNA content (by going to *View > Playlist > Local Network > Universal Plug'n'Play*), that vlc fails to see the DLNA server on the local network, then make sure that the firewall is not blocking port 1900 UDP. It is essential that this port is open in order to play local uPNP/DLNA content.

### Control using hotkeys or cli

Install [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat).

Get script at: [http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035](http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035)

Follow instructions in script to setup a socket for VLC.

Either run the script from the command line or register the script with keyboard shortcuts through your desktop.

Alternatively, you can use dbus-send [as discussed here](https://theelitist.github.io/control-vlc-media-player-through-d-bus) to interact with VLC:

```
$ dbus-send --print-reply --session --dest=org.mpris.MediaPlayer2.vlc /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause

```

### Preventing multiple instances

The default settings for VLC is to open a new instance of the program for each file that is opened. This can be annoying if you are using VLC for something like playing your music collection. You can disable this in *Tools > Preferences > Interface > Instances > Allow only one instance*. Optionally, tick *Enqueue files when in one instance mode* which keeps current file playing and adds any newly opened files to the current playlist.

### Hardware video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

VLC automatically tries to use an available API, but you can override it by going to *Tools > Preferences > Input & Codecs* and choosing the suitable option under *Hardware-accelerated decoding*, e.g. `Video Acceleration (VA) API` for VA-API or `Video Decode and Presentation API for Unix (VDPAU)` for VDPAU.

### systemd service

VLC's web interface can be started from systemd. First, you need to create a default user:

```
# useradd -c "VLC daemon" -d / -G audio -M -p \! -r -s /usr/bin/nologin -U vlcd

```

Now create the systemd service file:

 `/etc/systemd/system/vlc.service` 
```
[Unit]
Description=VideoOnLAN Service
After=network.target

[Service]
Type=forking
User=vlcd
ExecStart=/usr/bin/vlc --daemon --syslog -I http --http-port 8090 --http-password *password* 
Restart=on-abort

[Install]
WantedBy=multi-user.target

```

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `vlc.service`. Log in to http://*yourmachine*:8090/ with no username and with the password you put in the service file.

### Chromecast support

Starting with 3.0 release (*Vetinari* branch), VLC can stream to chromecast devices on the same wireless network.

Install packages:

*   [libmicrodns](https://www.archlinux.org/packages/?name=libmicrodns) - VLC can find the chromecast device and it shows up in *Playback > Renderer* menu
*   [protobuf](https://www.archlinux.org/packages/?name=protobuf) - enables streaming to the selected device in *Playback > Renderer* menu

## Troubleshooting

### Video broken or other issue after upgrade

Now and then VLC will have some issues with configuration even in minor releases. Before making bug reports, remove or rename your configuration located at `~/.config/vlc` and confirm whether the issue is still there.

If using a ffmpeg variant from the AUR, be sure that you have upgraded it as well. Pacman will not upgrade it when necessary and a mismatch will break VLC.

### Segmentation fault

When starting VLC you can get a segfault, and ruling out general factors such as [Microcode](/index.php/Microcode "Microcode"), a possible workaround to this is running the following:

```
# /usr/lib/vlc/vlc-cache-gen /usr/lib/vlc/plugins

```

Then reinstall VLC.

If that does not work, VLC has a segfault issue with `plugins.dat` (see [FS#57777](https://bugs.archlinux.org/task/57777)), simply remove the file:

```
# rm /usr/lib/vlc/plugins/plugins.dat

```

### Missing icons in dropdown menus

This can happen under XFCE, there will be no more icons in dropdown menus, like the PCI card icon.

Execute these commands to reactivate these icons:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true

```

### Failed to open VDPAU backend

See [Hardware video acceleration#Failed to open VDPAU backend](/index.php/Hardware_video_acceleration#Failed_to_open_VDPAU_backend "Hardware video acceleration").

Since your system probably does not support VDPAU you should tell VLC to use VA-API instead, see [#Hardware video acceleration](#Hardware_video_acceleration).

### No playback via SFTP of media files names containing spaces

If VLC does not play any videos or audio files over SFTP make sure you have [sshfs](https://www.archlinux.org/packages/?name=sshfs) installed.

If it refuses to play any media files containing spaces via SFTP and always asks for authentication change the Exec line in the `vlc.desktop` file to:

```
Exec=/usr/bin/vlc --started-from-file %F

```

See [[1]](https://bugs.launchpad.net/ubuntu/+source/vlc/+bug/239431/comments/11).

## See also

*   [Wikipedia article](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")
*   [List of applications#Multimedia](/index.php/List_of_applications#Multimedia "List of applications")
*   [VLC homepage](https://www.videolan.org/vlc/)
*   [playerctl](https://github.com/acrisci/playerctl): A command-line utility and library for controlling media players
*   [Control VLC via a browser](https://wiki.videolan.org/Control_VLC_via_a_browser)