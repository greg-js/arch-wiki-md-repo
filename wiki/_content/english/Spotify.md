[Spotify](https://www.spotify.com/) is a digital music service that gives you access to millions of songs. This Internet music service allows you to select any song in its database and stream for free.

Spotify also offers free users the ability to create playlist which can be shuffled, and set to repeat tracks. Content provided by Spotify comes in explicit versions as well as censored.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Third-party clients](#Third-party_clients)
    *   [1.2 Official Linux client](#Official_Linux_client)
    *   [1.3 Official Windows client through Wine](#Official_Windows_client_through_Wine)
*   [2 Tips & tricks](#Tips_.26_tricks)
    *   [2.1 Global media hotkeys](#Global_media_hotkeys)
        *   [2.1.1 MPRIS](#MPRIS)
            *   [2.1.1.1 Playerctl](#Playerctl)
            *   [2.1.1.2 D-Bus](#D-Bus)
        *   [2.1.2 xdotool](#xdotool)
    *   [2.2 Disable track notifications](#Disable_track_notifications)
    *   [2.3 Show track notifications](#Show_track_notifications)
    *   [2.4 Skip overplayed radio tracks](#Skip_overplayed_radio_tracks)
    *   [2.5 Mute commercials](#Mute_commercials)
        *   [2.5.1 blockify](#blockify)
        *   [2.5.2 spotblock](#spotblock)
        *   [2.5.3 Spotify-AdKiller](#Spotify-AdKiller)
    *   [2.6 Remote Control](#Remote_Control)
        *   [2.6.1 Send commands via SSH](#Send_commands_via_SSH)
        *   [2.6.2 Grab the Spotify window via SSH](#Grab_the_Spotify_window_via_SSH)
    *   [2.7 HiDPI Mode](#HiDPI_Mode)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Using search causes the whole interface to blink and then crash](#Using_search_causes_the_whole_interface_to_blink_and_then_crash)
    *   [3.2 Blinking images and improper rendering while using Spotify Linux with DWM](#Blinking_images_and_improper_rendering_while_using_Spotify_Linux_with_DWM)
    *   [3.3 Broken search, browsing or radio](#Broken_search.2C_browsing_or_radio)
    *   [3.4 SpotifyHelper.exe crashes (Windows client)](#SpotifyHelper.exe_crashes_.28Windows_client.29)
    *   [3.5 Wrong launcher icon (Windows client)](#Wrong_launcher_icon_.28Windows_client.29)
    *   [3.6 Deadlock GUI Thread](#Deadlock_GUI_Thread)
    *   [3.7 Pulseaudio](#Pulseaudio)
    *   [3.8 Spotify does not detect other devices on local network](#Spotify_does_not_detect_other_devices_on_local_network)
    *   [3.9 Search Bar text is invisible when using a dark theme](#Search_Bar_text_is_invisible_when_using_a_dark_theme)
    *   [3.10 Segmentation fault when playing a local file](#Segmentation_fault_when_playing_a_local_file)
*   [4 See also](#See_also)

## Installation

Choose which client you would prefer. The Linux client is receiving good reviews. However, if you are comfortable with wine and its configuration, you might want to choose the windows client. Please note that you do **not** need to install both. There is also the online player (requires [Flash](/index.php/Flash "Flash")) on [https://play.spotify.com/](https://play.spotify.com/).

### Third-party clients

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Able of streaming from Spotify with a premium account after activating (downloading) a plugin in the settings.

	[http://www.clementine-player.org/](http://www.clementine-player.org/) || [clementine](https://www.archlinux.org/packages/?name=clementine)

*   **Mopidy** — An alternative plug-in based implementation of [Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon") is able of streaming from Spotify with an extension.

	[https://www.mopidy.com/](https://www.mopidy.com/) || [mopidy](https://www.archlinux.org/packages/?name=mopidy)+ [mopidy-spotify](https://aur.archlinux.org/packages/mopidy-spotify/) or [despotify-svn](https://aur.archlinux.org/packages/despotify-svn/)

*   **Librespot** — An open source client library for Spotify. It enables applications to use Spotify's service (streaming), without using the official closed-source *libspotif*.

	[https://github.com/plietar/librespot](https://github.com/plietar/librespot) || [librespot-git](https://aur.archlinux.org/packages/librespot-git/) [librespot-alsa-git](https://aur.archlinux.org/packages/librespot-alsa-git/)

### Official Linux client

[Install](/index.php/Install "Install") it with the [spotify](https://aur.archlinux.org/packages/spotify/) package. If you wish to play local files you will need to install [zenity](https://www.archlinux.org/packages/?name=zenity) and [ffmpeg0.10](https://aur.archlinux.org/packages/ffmpeg0.10/) as well.

### Official Windows client through Wine

First, install [Wine](/index.php/Wine "Wine").

Obtaining Spotify can be done by registering for an account on their Website, the application does not offer in-app registration. Obtain the appliction from [https://www.spotify.com/nl/download/windows/](https://www.spotify.com/nl/download/windows/).

After you have registered and downloaded your copy of the installer you will need to run the application through Wine, depending on your setup you may be able to run the application by right clicking the file. If not terminal will work just fine, as long as you run the below command in the directory of your download.

```
$ wine SpotifySetup.exe

```

Once the application is successfully installed you may run Spotify by using one of the following commands in terminal, or in the ALT+F2 launcher:

If you use a x86_64 copy of Arch Linux, you will have to run it like this:

```
$ wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Spotify/spotify.exe

```

If you use a x86 copy of Arch Linux, you can use this command just fine:

```
$ wine ~/.wine/drive_c/Program\ Files/Spotify/spotify.exe

```

If you have any additional problems, I recommend setting the winecfg to Windows XP or Windows 7 emulation.

## Tips & tricks

### Global media hotkeys

The official Linux client has support for media keys like `XF86AudioPlay`, but out of the box they only work inside Spotify. We can use for example [xbindkeys](/index.php/Xbindkeys "Xbindkeys") to catch the global media keypresses, and then forward them to Spotify using one of the methods below. If you use xbindkeys, ensure that Spotify is restarted after installation and key configuration otherwise the key events will not be properly caught.

#### MPRIS

The Spotify client implements the [MPRIS2](https://specifications.freedesktop.org/mpris-spec/latest/) D-Bus interface which allows external control.

##### Playerctl

The [playerctl](https://aur.archlinux.org/packages/playerctl/) utility provides a command line tool to send commands to MPRIS clients. The only commands you will likely need to bind globally are `play-pause`, `next` and `previous`

```
$ playerctl play-pause
$ playerctl next
$ playerctl previous

```

Playerctl will send the command to the first player it finds, so this method will also work with others players such as [vlc](/index.php/Vlc "Vlc"). To ignore other players, pass `--player=spotify` as an argument.

##### D-Bus

An alternative to the above is to manually use [D-Bus](/index.php/D-Bus "D-Bus"), which should be available by default as it is a dependency of [systemd](/index.php/Systemd "Systemd").

To play or pause the current song in Spotify:

```
$ dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause

```

In order to bind this and the other commands to the media keys you need to install [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") and edit your .xbindkeysrc and add the following lines:

```
# Play/Pause
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.PlayPause"
XF86AudioPlay

# Next
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Next"
XF86AudioNext

# Previous
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Previous"
XF86AudioPrev

# Stop
"dbus-send --print-reply --dest=org.mpris.MediaPlayer2.spotify /org/mpris/MediaPlayer2 org.mpris.MediaPlayer2.Player.Stop"
XF86AudioStop

```

If the above commands do not work, try setting the dbus address:

```
 USER=`whoami`
 PROCESS=spotify
 PID=`pgrep -o -u $USER $PROCESS`
 ENVIRON=/proc/$PID/environ
 if [ -e $ENVIRON ]
 then
     export `grep -z DBUS_SESSION_BUS_ADDRESS $ENVIRON`
 else
     echo "Unable to set DBUS_SESSION_BUS_ADDRESS."
     exit 1
 fi

```

#### xdotool

With the help of `xdotool` it is possible to send your hotkeys to the application. The following script is an example of how to control Spotify from the outside:

```
#!/bin/sh

case $1 in
   "play")
       key="XF86AudioPlay"
       ;;
   "next")
       key="XF86AudioNext"
       ;;
   "prev")
       key="XF86AudioPrev"
       ;;
   *)
       echo "Usage: $0 play|next|prev"
       exit 1
        ;;
esac
xdotool key --window $(xdotool search --name "Spotify (Premium |Unlimited |Free )?- Linux Preview"|head -n1) $key
exit 0

```

Let us call it `musickeys.sh`. Make the script executable:

```
$ chmod +x musickeys.sh

```

By executing `./musickeys.sh play` you can now toggle playing a song. Now you can bind this script to any tool that catches keypresses, such as [xbindkeys](/index.php/Xbindkeys "Xbindkeys").

### Disable track notifications

**Note:** It is worth noting that if you have a [SpotCommander](https://aur.archlinux.org/packages/SpotCommander/) [Server](http://olejon.github.io/spotcommander/) running alongside Spotify, and you disable track notifications by following the instructions below, the [SpotCommander Client](https://play.google.com/store/apps/details?id=net.olejon.spotcommander&hl=en) running on your mobile device will display that “No Music is Playing” and will [fail to display track info](http://askubuntu.com/questions/472325/remove-spotify-pop-up-notification-when-a-song-starts/472329#472329) such as title, artist, album art, etc. Apart from that, the mobile client still works fine though, and is still able to skip, play, pause, control volume, etc.

After version 0.9.10, track change notifications were enabled by default. They can be quite intrusive. To disable them, add the following line to `~/.config/spotify/Users/<spotifylogin>-user/prefs`

```
 ui.track_notifications_enabled=false

```

It is also possible to launch spotify with the `--ui.track_notifications_enabled=false` option.

### Show track notifications

[playerctl](https://aur.archlinux.org/packages/playerctl/) provides a library you can use with [python-gobject](https://www.archlinux.org/packages/?name=python-gobject) and a notification daemon such as [dunst](https://www.archlinux.org/packages/?name=dunst) to show the artist and title in a notification when the track changes.

```
#!/usr/bin/env python3

from gi.repository import Playerctl, GLib
from subprocess import Popen

player = Playerctl.Player()

def on_track_change(player, e):
    track_info = '{artist} - {title}'.format(artist=player.get_artist(), title=player.get_title())
    Popen(['notify-send', track_info])

player.on('metadata', on_track_change)

GLib.MainLoop().run()

```

### Skip overplayed radio tracks

Another use of the [playerctl](https://aur.archlinux.org/packages/playerctl/) library is to skip tracks that are played too much on radio when you do not necessarily want to downvote these tracks because you may want to hear them again later on that station.

```
#!/usr/bin/env python3

from gi.repository import Playerctl, GLib

player = Playerctl.Player()

played_out = ['Zu Fuss', 'Walk And Talk', 'Neuland']

def on_track_change(player, e):
    if player.get_title() in played_out:
        player.next()

player.on('metadata', on_track_change)

GLib.MainLoop().run()

```

### Mute commercials

#### blockify

With [blockify](https://github.com/mikar/blockify) you can mute commercials. It is available in the [AUR](/index.php/AUR "AUR") as [blockify](https://aur.archlinux.org/packages/blockify/).

To have this start and run in the background every time Spotify starts you will need to automate this yourself:

```
#!/bin/sh

spotify=/usr/bin/spotify

if [[ -x $spotify && -x /usr/bin/blockify ]];
then
  blockify &
  block_pid=$!
  $spotify
  trap "kill -9 $block_pid" SIGINT SIGTERM EXIT
fi

```

By placing this script at `/usr/local/bin/spotify`, it gets preferred to `/usr/bin/spotify` everytime you start Spotify, so there's nothing else to change and updates won't break it.

#### spotblock

[spotblock](https://github.com/mahkoh/spotblock) ([spotblock-git](https://aur.archlinux.org/packages/spotblock-git/)) is a resource-efficient ad blocker that runs as a systemd daemon.

#### Spotify-AdKiller

[Spotify-AdKiller](https://github.com/SecUpwN/Spotify-AdKiller) ([spotify-adkiller-git](https://aur.archlinux.org/packages/spotify-adkiller-git/)) is another alternative to block Spotify ads.

### Remote Control

#### Send commands via SSH

If you set up ssh on the server, you can send controls from a client to a remote Spotify instance with

```
$ ssh user@host *yourcommand*

```

where *yourcommand* can be [spotifycmd](https://code.google.com/p/spotifycmd/) that you installed on the server, or a dbus script for the linux version, as described above.

#### Grab the Spotify window via SSH

Aside from grabbing the whole desktop with TeamViewer or VNC to remotely control your server, you can also only grab the Spotify Window from the server to your client.

To do that, you need to configure sshd on your server and install x11vnc on both server and client as well as tigervnc on the client. Then you can use these scripts to grab either the complete dektop or only the Spotify window, which essentially gets you GUI client-like behavior as with MPD.

```
#!/bin/bash
# vncget.sh

if [[ $1 == all ]];then
  ssh -f -t -L 5900:localhost:5900 user@host "x11vnc -q -display :0 -auth .Xauthority"
else
  ssh -f -t -L 5900:localhost:5900 user@host ".bin/vncgetspotify.sh"
fi

for i in {1..4}; do
  sleep 2
  if vncviewer localhost:0; then break; fi
done

```

```
#!/bin/bash
# vncgetspotify.sh

export DISPLAY=:0

id=$(wmctrl -lx | awk '/spotify.exe.Wine/ {print $1}')
[[ -z $id ]] && id=$(wmctrl -lx | awk '/spotify.Spotify/ {print $1}')

x11vnc -sid $id -display :0 -auth .Xauthority

```

You will need to copy the second script to ~/.bin/vncgetspotify.sh on the server and the first script to any place on your client.

Finally, to grab the spotify window, run on the client:

```
$ sh vncget.sh

```

or, for the whole desktop:

```
$ sh vncget.sh all

```

### HiDPI Mode

As the current Spotify build is not DPI aware, the amount to scale the interface by can be specified using the terminal command:

```
$ spotify --force-device-scale-factor=**X**

```

where X is the amount to scale the interface by, e.g 2.

This change can be added to the `spotify.desktop` file in order to apply the scaling when launching from the desktop.

To make sure the file does not get overwritten when the package is updated, copy it to you local applications folder:

```
$ cp /usr/share/applications/spotify.desktop ~/.local/share/applications/

```

Now edit `~/.local/share/applications/spotify.desktop` and add the `--force-device-scale-factor` option:

 `spotify.desktop` 
```
[Desktop Entry]
Name=Spotify
GenericName=Music Player
Comment=Spotify streaming music client
Icon=spotify-client
Exec=spotify **--force-device-scale-factor=2** %U
TryExec=spotify
Terminal=false
Type=Application
Categories=Audio;Music;Player;AudioVideo
MimeType=x-scheme-handler/spotify
```

You might need to relaunch your Desktop Manager, before these override changes will be effective.

## Troubleshooting

### Using search causes the whole interface to blink and then crash

Spotify is using an old version of Chromium Embedded Framework and hits a bug causing it to crash repeatedly when trying to use the search. This can be worked around by using the following command line option:

```
 --force-device-scale-factor=1.0000001

```

### Blinking images and improper rendering while using Spotify Linux with DWM

Start spotify as a floating window.

You can add this rule to the rules array in your `config.h`:

```
 { "Spotify",     NULL,       NULL,        2,         True,     -1 },

```

This will tell dwm to start spotify as a floating window associated with the tag "2" no matter what window mode you are in. Recompile and install dwm to apply your new settings.

### Broken search, browsing or radio

	Spotify [bug report](http://community.spotify.com/t5/Help-Desktop-Linux-Mac-and/Bug-Desktop-Linux-0-9-0-133-gd18ed589-Having-mixed-locale-breaks/td-p/418270) concerning non-english locales

If various tabs like browsing only show a blank screen, the search field doesn't seem to do anything or the radio page is broken (stuck when starting and unsresponsive to input) you might be using a custom locale.

Try setting the environment variable `LC_NUMERIC` to `en_US.utf8` before starting Spotify.

### SpotifyHelper.exe crashes (Windows client)

If SpotifyHelper.exe crashes when starting Spotify, disable the d3d9 library with `winecfg`. Go to the "Libraries" tab, choose "d3d9" and click Add. To disable it, click edit and select the "Disable" option.

### Wrong launcher icon (Windows client)

If the Spotify icon does not show up correctly in your launcher, add the following line to `~/.local/share/applications/wine/Programs/Spotify.desktop`:

```
StartupWMClass=spotify.exe

```

### Deadlock GUI Thread

Can occur under tiling window managers, such as Awesome, when double-clicking new song or playlist. Edit the file `~/.config/spotify/Users/[1-9]*-user/prefs` to add or change the following:

```
ui.track_notifications_enabled=false

```

Restart Spotify. Note that several causes appear to exist for this problem, and this particular fix only applies to select versions of Spotify client and Awesome, and it may be that additional root causes exist for the Debian and Ubuntu users reporting this issue. Observed with Spotify 0.9.17.1.g9b85d436 and Awesome 3.4.15.

**Note:** As of Spotify 1.0.17.75-2, `ui.track_notifications_enabled=false` seems to be ignored. On the other hand some, users report not experimenting the deadlock anymore as of Awesome 3.5.6\. Deadlocks could be caused by scripts called by Awesome, which rely on buggy spotify dbus properties. See [[1]](https://github.com/acrisci/playerctl/issues/20).

**Note:** This issue has multiple causes, so keep track of what you change while researching this. Update this section with additional scenarios and fixes.

### Pulseaudio

See [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting") and [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1393465#p1393465)

=== Album art and images are missing, show up as squares; with Quit spotify, then open spotify preferences `~/.config/spotify/prefs`

Change @https to @http:

```
 network.proxy.addr="your-proxy.com:80**@http**"
 network.proxy.mode=2

```

See original form post [here](http://community.spotify.com/t5/Help-Desktop-Linux-Mac-and/Mac-Windows-0-9-0-128-Apps-can-t-connect-anywhere-behind-proxy/m-p/448704#M52332).

**Note:** As of 1.0.17 it looks like replacing https with http as suggested above can result in no connectivity at all. If this happens an alternative solution is to set 'no proxy' in the GUI use [proxychains-ng](https://www.archlinux.org/packages/?name=proxychains-ng) to force all TCP connection coming from the app through a proxy. Even with HTTP proxies that reject connections on port 80 (and only work for port 443) this works reliably.

### Spotify does not detect other devices on local network

If a firewall is in place, open ports 57621 for UDP and TCP. If you use a variant of the [iptables](/index.php/Iptables "Iptables") [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall"), the following should do it:

```
iptables -A TCP -p tcp --dport 57621 -j ACCEPT -m comment --comment spotify
iptables -A UDP -p udp --dport 57621 -j ACCEPT -m comment --comment spotify

```

It is also possible to restrict the source and destination to the local network.

### Search Bar text is invisible when using a dark theme

The text in the search bar appears to be hardcoded to be white, making it invisible when using a dark Qt theme. To fix this, you'll need to make an override.

First create a css file somewhere your account has permission to read/write from (such as your home folder). Call it whatever you like (eg. **spotify-override.css**).

Open the newly created css file and add the following:

```
QLineEdit { color: #000 }

```

Save the file and exit. Next, you need to add the following to the end of your Spotify launcher (substitute the path with the actual path of your css file):

```
-stylesheet=/home/user/spotify-overide.css

```

So your full launch path should look something like this:

```
/usr/share/spotify/spotify-client/spotify -stylesheet=/home/user/spotify-override.css

```

### Segmentation fault when playing a local file

The cause of this problem is a missing dependency. For Pulseaudio users, installing [ffmpeg-compat-54](https://aur.archlinux.org/packages/ffmpeg-compat-54/) should fix it.

## See also

*   [playerctl](https://github.com/acrisci/playerctl): A command-line utility and library for controlling media players
*   [SpotCommander](/index.php/SpotCommander "SpotCommander"): A web based remote control for Spotify
*   [http://www.spotify.com/int/help/faq/wine/](http://www.spotify.com/int/help/faq/wine/)
*   [http://www.spotify.com/int/download/previews/](http://www.spotify.com/int/download/previews/)