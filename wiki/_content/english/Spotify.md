[Spotify](https://www.spotify.com/) is a digital music service that gives you access to millions of songs. This Internet music service allows you to select any song in its database and stream for free.

Spotify also offers free users the ability to create playlist which can be shuffled, and set to repeat tracks. Content provided by Spotify comes in explicit versions as well as censored.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Official Linux client](#Official_Linux_client)
    *   [1.2 Third-party clients](#Third-party_clients)
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
        *   [2.5.4 Hosts file](#Hosts_file)
    *   [2.6 Remote Control](#Remote_Control)
        *   [2.6.1 Send commands via SSH](#Send_commands_via_SSH)
        *   [2.6.2 Grab the Spotify window via SSH](#Grab_the_Spotify_window_via_SSH)
    *   [2.7 HiDPI Mode](#HiDPI_Mode)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Desktop Environment alerts (beeps) mutes Spotify](#Desktop_Environment_alerts_.28beeps.29_mutes_Spotify)
    *   [3.2 Using search causes the whole interface to blink and then crash](#Using_search_causes_the_whole_interface_to_blink_and_then_crash)
    *   [3.3 Blinking images and improper rendering while using Spotify Linux with DWM](#Blinking_images_and_improper_rendering_while_using_Spotify_Linux_with_DWM)
    *   [3.4 Broken search, browsing or radio](#Broken_search.2C_browsing_or_radio)
    *   [3.5 Deadlock GUI Thread](#Deadlock_GUI_Thread)
    *   [3.6 PulseAudio](#PulseAudio)
    *   [3.7 Album art and images are missing, show up as squares](#Album_art_and_images_are_missing.2C_show_up_as_squares)
    *   [3.8 Spotify does not detect other devices on local network](#Spotify_does_not_detect_other_devices_on_local_network)
    *   [3.9 Search Bar text is invisible when using a dark theme](#Search_Bar_text_is_invisible_when_using_a_dark_theme)
    *   [3.10 Can't play local files](#Can.27t_play_local_files)
    *   [3.11 Not respecting window manager rules](#Not_respecting_window_manager_rules)
    *   [3.12 GUI hangs while the music plays](#GUI_hangs_while_the_music_plays)
*   [4 See also](#See_also)

## Installation

Initially, Spotify was unavailable for Linux and the workaround was to run it under [Wine](/index.php/Wine "Wine"). However, [as of 2010](https://news.spotify.com/uk/2010/07/12/linux/), a native Linux client is available. Although it's officially unsupported, the Linux client is actively maintained and the developers have indicated that they will "try to make sure it keeps pace with its Mac and Windows siblings". [[1]](https://www.spotify.com/int/download/linux/) Alternatively, there is also also an [online player](https://open.spotify.com/).

### Official Linux client

[Install](/index.php/Install "Install") it with the [spotify](https://aur.archlinux.org/packages/spotify/) or [spotify-stable](https://aur.archlinux.org/packages/spotify-stable/) package. If you wish to play local files you will need to install [zenity](https://www.archlinux.org/packages/?name=zenity) and [ffmpeg-compat-54](https://aur.archlinux.org/packages/ffmpeg-compat-54/) as well.

### Third-party clients

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Able to stream from Spotify with a premium account after activating (downloading) a plugin in the settings.

	[https://www.clementine-player.org/](https://www.clementine-player.org/) || [clementine](https://www.archlinux.org/packages/?name=clementine)

*   **Mopidy** — An alternative plug-in based implementation of [Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon") is able to stream from Spotify with an extension.

	[https://www.mopidy.com/](https://www.mopidy.com/) || [mopidy](https://www.archlinux.org/packages/?name=mopidy)+ [mopidy-spotify](https://aur.archlinux.org/packages/mopidy-spotify/) or [despotify-svn](https://aur.archlinux.org/packages/despotify-svn/)

*   **Librespot** — An open source client library for Spotify. It enables applications to use Spotify's service (streaming), without using the official closed-source *libspotify*.

	[https://github.com/librespot-org/librespot](https://github.com/librespot-org/librespot) || [librespot-git](https://aur.archlinux.org/packages/librespot-git/)

*   **Tomahawk** — A Music Player App written in C++/Qt

	[https://www.tomahawk-player.org/](https://www.tomahawk-player.org/) || [tomahawk](https://aur.archlinux.org/packages/tomahawk/) [tomahawk-git](https://aur.archlinux.org/packages/tomahawk-git/) [tomahawk-qt5](https://aur.archlinux.org/packages/tomahawk-qt5/)

## Tips & tricks

### Global media hotkeys

**Tip:** Many [desktop environments](/index.php/Desktop_environments "Desktop environments") come with keyboard shortcuts which work with the Spotify client out of the box e.g. under [Cinnamon](/index.php/Cinnamon "Cinnamon") (Preferences -> Keyboard -> Shortcuts -> Sound and Media), several default bindings are set up to control the player, and these can easily be changed by pressing the preferred keys.

For environments in which controlling Spotify via the keyboard doesn't work automatically, the official Linux client has support for media keys like `XF86AudioPlay`. We can use for example [xbindkeys](/index.php/Xbindkeys "Xbindkeys") to catch the global media keypresses, and then forward them to Spotify using one of the methods below. If you use xbindkeys, ensure that Spotify is restarted after installation and key configuration otherwise the key events will not be properly caught.

#### MPRIS

The Spotify client implements the [MPRIS2](https://specifications.freedesktop.org/mpris-spec/latest/) D-Bus interface which allows external control.

##### Playerctl

The [playerctl](https://www.archlinux.org/packages/?name=playerctl) utility provides a command line tool to send commands to MPRIS clients. The only commands you will likely need to bind globally are `play-pause`, `next` and `previous`

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

[playerctl](https://www.archlinux.org/packages/?name=playerctl) provides a library you can use with [python-gobject](https://www.archlinux.org/packages/?name=python-gobject) and a notification daemon such as [dunst](https://www.archlinux.org/packages/?name=dunst) to show the artist and title in a notification when the track changes.

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

Another use of the [playerctl](https://www.archlinux.org/packages/?name=playerctl) library is to skip tracks that are played too much on radio when you do not necessarily want to downvote these tracks because you may want to hear them again later on that station.

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

#### Hosts file

You may also add the following lines to your hosts file to block ads in Spotify :

 `/etc/hosts` 
```
# Block spotify ads
127.0.0.1 media-match.com
127.0.0.1 adclick.g.doublecklick.net
127.0.0.1 www.googleadservices.com
127.0.0.1 open.spotify.com
127.0.0.1 pagead2.googlesyndication.com
127.0.0.1 desktop.spotify.com
127.0.0.1 googleads.g.doubleclick.net
127.0.0.1 pubads.g.doubleclick.net
127.0.0.1 audio2.spotify.com
127.0.0.1 www.omaze.com
127.0.0.1 omaze.com
127.0.0.1 bounceexchange.com
127.0.0.1 spclient.wg.spotify.com
127.0.0.1 securepubads.g.doubleclick.net

```

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

### Desktop Environment alerts (beeps) mutes Spotify

Comment out "module-role-cork" in pulse audio configuration file.

Open `/etc/pulse/default.pa` with your text editor and comment out:

```
load-module module-role-cork 

```

Or simply unload it with:

```
pactl unload-module module-role-cork

```

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

### Deadlock GUI Thread

Can occur under tiling window managers, such as Awesome, when double-clicking new song or playlist. Edit the file `~/.config/spotify/Users/[1-9]*-user/prefs` to add or change the following:

```
ui.track_notifications_enabled=false

```

Restart Spotify. Note that several causes appear to exist for this problem, and this particular fix only applies to select versions of Spotify client, i3 and Awesome, and it may be that additional root causes exist for the Debian and Ubuntu users reporting this issue. Observed with Spotify 0.9.17.1.g9b85d436 and Awesome 3.4.15 and i3-gaps 4.13-2 and Spotify 1.0.64.407.g9bd02c2d.

**Note:** As of Spotify 1.0.17.75-2, `ui.track_notifications_enabled=false` seems to be ignored. On the other hand, some users report not experiencing the deadlock anymore as of Awesome 3.5.6\. Deadlocks could be caused by scripts called by Awesome, which rely on buggy spotify dbus properties. See [[2]](https://github.com/acrisci/playerctl/issues/20).

**Note:** This issue has multiple causes, so keep track of what you change while researching this. Update this section with additional scenarios and fixes.

### PulseAudio

See [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting") and [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1393465#p1393465)

### Album art and images are missing, show up as squares

Quit spotify, then open spotify preferences `~/.config/spotify/prefs`

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

If you are using Spotify Connect to play music on a wireless speaker or AVR, your firewall needs to be configured for Spotify's mDNS lookup of those. Sadly, it uses a random unprivileged port [[4]](https://community.spotify.com/t5/Desktop-Linux-Windows-Web-Player/Spotify-Connect-and-iptables-netfilter/td-p/1235049) which makes these firewall rules rather nasty. Fortunately, you can restrict the rules to source port 1900 or 5353.

```
iptables -A UDP -p udp --sport 1900 --dport 1025:65535 -j ACCEPT -m comment --comment spotify
iptables -A UDP -p udp --sport 5353 --dport 1025:65535 -j ACCEPT -m comment --comment spotify

```

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

### Can't play local files

If you get a segmentation fault or error message when trying to play local files e.g.

```
   This song is not available. If you have the file on your computer you can import it.

```

- it's caused by a missing libavcodec dependency. For PulseAudio users, installing [ffmpeg-compat-54](https://aur.archlinux.org/packages/ffmpeg-compat-54/) should fix it. If you get PGP verification errors when you install it you might have to import the correct PGP key.

```
   $ gpg --keyserver pgp.mit.edu --recv-keys FCF986EA15E6E293A5644F10B4322F04D67658D8

```

### Not respecting window manager rules

Window manager that try to apply specific rules like starting it on a determined workspace or maximizing it on startup, has no effect, as Spotify doesn't set the *WM_CLASS* property before creating the window, violating the ICCCM specifications. One solution is to use [spotifywm](https://github.com/dasJ/spotifywm).

### GUI hangs while the music plays

Also the previous and next track buttons act with a delay of 10-40 seconds. Spotify by default tries to send notification about next track, if you don't have a notification-daemon installed, Spotify's GUI hangs.

The solution is to either disable notifications in the settings or to install a notification daemon from [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications").

## See also

*   [playerctl](https://github.com/acrisci/playerctl) — A command-line utility and library for controlling media players
*   [SpotCommander](/index.php/SpotCommander "SpotCommander") — A web based remote control for Spotify
*   [Spotify for Linux](http://www.spotify.com/int/download/previews/) — Spotify's homepage for the Linux client