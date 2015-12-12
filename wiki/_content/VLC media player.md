# VLC media player

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the project [home page](http://www.videolan.org/vlc/):

_VLC is a free and open source cross-platform multimedia player and framework that plays most multimedia files as well as DVD, Audio CD, VCD, and various streaming protocols._

## Contents

*   [1 Installation](#Installation)
*   [2 Language](#Language)
*   [3 Skins](#Skins)
*   [4 Web interface](#Web_interface)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 File association in GNOME](#File_association_in_GNOME)
    *   [5.2 Twitch.tv streaming over VLC](#Twitch.tv_streaming_over_VLC)
    *   [5.3 Playing streamed content from a local DLNA server](#Playing_streamed_content_from_a_local_DLNA_server)
    *   [5.4 Control using hotkeys or cli](#Control_using_hotkeys_or_cli)
    *   [5.5 Preventing multiple instances](#Preventing_multiple_instances)
    *   [5.6 Hardware acceleration support](#Hardware_acceleration_support)
    *   [5.7 systemd service](#systemd_service)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Video broken or other issue after upgrade](#Video_broken_or_other_issue_after_upgrade)
    *   [6.2 Segmentation fault](#Segmentation_fault)
    *   [6.3 Missing icons in dropdown menus](#Missing_icons_in_dropdown_menus)
    *   [6.4 Failed to open VDPAU backend](#Failed_to_open_VDPAU_backend)
    *   [6.5 No playback via SFTP of media files names containing spaces](#No_playback_via_SFTP_of_media_files_names_containing_spaces)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") [vlc](https://www.archlinux.org/packages/?name=vlc) from the [official repositories](/index.php/Official_repositories "Official repositories").

Notable variants are:

*   [vlc-git](https://aur.archlinux.org/packages/vlc-git/)<sup><small>AUR</small></sup> - Development branch.

If you want to play audio CDs, you should also install [libcddb](https://www.archlinux.org/packages/?name=libcddb).

## Language

It seems VLC does not offer an option to change language in its _Preferences_ menu. But you can use the _LANGUAGE=_ prefix. For instance, modify the `/usr/share/applications/vlc.desktop` line:

```
Exec=/usr/bin/vlc %U

```

to:

```
Exec=LANGUAGE=fr /usr/bin/vlc %U

```

to switch VLC interface to French.

## Skins

VLC can be "skinned" for a different look and feel. You can obtain new skins for VLC from [http://www.videolan.org/vlc/skins.php](http://www.videolan.org/vlc/skins.php).

Installation of skins is simple just download the skin you wish to use and copy it to:

```
~/.local/share/vlc/skins2

```

Open up VLC, click _Tools > Preferences_. When the preferences window opens up you should be in the "Interface" tab

Choose the "Use custom skin" radio button, and browse to the location of the downloaded skin.

Restart VLC for the change to take effect.

Note: You need to install [libtar](https://www.archlinux.org/packages/?name=libtar) from the [official repositories](/index.php/Official_repositories "Official repositories") to use the skinnable interface module.

## Web interface

Run VLC with the parameter `--extraintf=http` to use both the desktop and web interface. The `--http-host` parameter specifies the address to, which is `localhost` by default. To set a password, use `--http-password`, otherwise VLC will not allow you to log in.

```
# vlc --extraintf=http --http-host 0.0.0.0:8080 --http-password 'yourpasswordhere'

```

Or you can enable this feature in the UI by navigating to _View > Add Interface > Web Interface_.

VLC defaults to port 8080: [http://127.0.0.1:8080](http://127.0.0.1:8080)

Edit `/usr/share/vlc/lua/http/.hosts` to allow remote connections. You will need to restart VLC in order for changes to take effect.

## Tips and tricks

### File association in GNOME

Copy the system desktop file to the local one (local `.desktop` files supersede the global ones):

```
$ cp /usr/share/applications/vlc.desktop ~/.local/share/applications/

```

Define its mime types (known playback file type abilities) by doing:

```
sed -i 's|^Mimetype.*$|MimeType=video/dv;video/mpeg;video/x-mpeg;video/msvideo;video/quicktime;video/x-anim;video/x-avi;video/x-ms-asf;video/x-ms-wmv;video/x-msvideo;video/x-nsv;video/x-flc;video/x-fli;application/ogg;application/x-ogg;application/x-matroska;audio/x-mp3;audio/x-mpeg;audio/mpeg;audio/x-wav;audio/x-mpegurl;audio/x-scpls;audio/x-m4a;audio/x-ms-asf;audio/x-ms-asx;audio/x-ms-wax;application/vnd.rn-realmedia;audio/x-real-audio;audio/x-pn-realaudio;application/x-flac;audio/x-flac;application/x-shockwave-flash;misc/ultravox;audio/vnd.rn-realaudio;audio/x-pn-aiff;audio/x-pn-au;audio/x-pn-wav;audio/x-pn-windows-acm;image/vnd.rn-realpix;video/vnd.rn-realvideo;audio/x-pn-realaudio-plugin;application/x-extension-mp4;audio/mp4;video/mp4;video/mp4v-es;x-content/video-vcd;x-content/video-svcd;x-content/video-dvd;x-content/audio-cdda;x-content/audio-player;|' ~/.local/share/applications/vlc.desktop

```

Then in _System Settings > Details > Default Applications_ and on the _Video_ drop-down menu, select _Open VLC media player_.

### Twitch.tv streaming over VLC

See [Livestreamer#Twitch](/index.php/Livestreamer#Twitch "Livestreamer").

### Playing streamed content from a local DLNA server

If you find that trying to play uPNP/DLNA content (by going to _View > Playlist > Local Network > Universal Plug'n'Play_), that vlc fails to see the DLNA server on the local network, then make sure that the firewall is not blocking port 1900 UDP. It is essential that this port is open in order to play local uPNP/DLNA content.

### Control using hotkeys or cli

Install [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat).

Get script at: [http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035](http://crunchbang.org/forums/viewtopic.php?pid=112035%23p112035#p112035)

Follow instructions in script to setup a socket for VLC.

Either run the script from the command line or register the script with keyboard shortcuts through your desktop.

### Preventing multiple instances

The default settings for VLC is to open a new instance of the program for each file that is opened. This can be annoying if you are using VLC for something like playing your music collection. You can disable this in _Tools > Preferences > Interface > Instances > Allow only one instance_. Optionally. tick _Enqueue files when in one instance mode_ which keeps current file playing and adds any newly opened files to the current playlist.

### Hardware acceleration support

To enable hardware acceleration since version 2.1.x: _Tools > Preferences > Input & Codecs_, then choose under _Hardware-accelerated decoding_ the suitable item, e.g. `Video Acceleration (VA) API` or `Video Decode and Presentation API for Unix (VDPAU)`.

To enable hardware acceleration in previous versions: _Tools > Preferences > Input & Codecs_, then check `Use GPU accelerated decoding`.

### systemd service

**Note:** _cvlc_ is the _Console VLC Player_, or VLC without graphical interface.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** `nobody` is a valid user for daemons, should it still be changed? (Discuss in [Talk:VLC media player#](https://wiki.archlinux.org/index.php/Talk:VLC_media_player))

Change the `User=` parameter.

 `/etc/systemd/system/vlc.service` 

```
[Unit]
Description=VideoOnLAN Service
After=network.target

[Service]
Type=forking
User=nobody
ExecStart=/usr/bin/cvlc --intf=lua --lua-intf=http --daemon --http-port 8090
Restart=on-abort

[Install]
WantedBy=multi-user.target

```

## Troubleshooting

### Video broken or other issue after upgrade

Now and then VLC will have some issues with configuration even in minor releases. Before making bug reports, remove or rename your configuration located at `~/.config/vlc` and confirm whether the issue is still there.

If using a ffmpeg variant from the AUR, be sure that you have upgraded it as well. Pacman will not upgrade it when necessary and a mismatch will break VLC.

### Segmentation fault

When starting VLC you can get a segfault, and ruling out general factors such as [Microcode](/index.php/Microcode "Microcode"), a possible workaround to this is running the following:

```
 # /usr/lib/vlc/vlc-cache-gen -f usr/lib/vlc/plugins

```

Then reinstall VLC.

Another workaround can be reinstalling vlc within an `LD_PRELOAD` environment:

```
# LD_PRELOAD=/usr/lib/libgobject-2.0.so.0 pacman -S vlc

```

### Missing icons in dropdown menus

This can happen under XFCE, there will be no more icons in dropdown menus, like the or the PCI card icon.

Execute these commands to reactivate these icons:

```
$ gconftool-2 --type boolean --set /desktop/gnome/interface/buttons_have_icons true
$ gconftool-2 --type boolean --set /desktop/gnome/interface/menus_have_icons true
```

### Failed to open VDPAU backend

By changing some VLC preferences, you can fix the following message:

```
Failed to open VDPAU backend libvdpau_i965.so: cannot open shared object file: No such file or director

```

In _Tools_, _Preferences_, _Video_ tab (v2.2.0 menu) select "OpenGL video output (experimental)" for _Output_ and, in _Input/Codecs_, "VA-API video decoder via X11/DRM" (both are OK) in _Hardware-accelerated decoding_ (_Codecs_ group).[[1]](https://bugs.archlinux.org/task/44569)

### No playback via SFTP of media files names containing spaces

If vlc does not play any videos or audio files over SFTP first confirm you have sshfs installed.

If it refuses to play any media files containing spaces via SFTP and always asks for authentication change the line

```
Exec=/usr/bin/vlc --started-from-file %U

```

to

```
Exec=/usr/bin/vlc --started-from-file %F

```

in the vlc.desktop file. [[2]](https://bugs.launchpad.net/ubuntu/+source/vlc/+bug/239431/comments/11)

## See also

*   [List of applications#Multimedia](/index.php/List_of_applications#Multimedia "List of applications")
*   [VLC homepage](http://www.videolan.org/vlc/)
*   [playerctl](https://github.com/acrisci/playerctl): A command-line utility and library for controlling media players
*   [Control VLC via a browser](http://wiki.videolan.org/Control_VLC_via_a_browser)

Retrieved from "[https://wiki.archlinux.org/index.php?title=VLC_media_player&oldid=411509](https://wiki.archlinux.org/index.php?title=VLC_media_player&oldid=411509)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")