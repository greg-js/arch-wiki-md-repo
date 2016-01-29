# Exaile

[Exaile](http://www.exaile.org/) is a music manager and player for GTK+ written in Python. It incorporates automatic fetching of album art, lyrics fetching, Last.fm scrobbling, support for many portable media players, internet radio such as shoutcast, and tabbed playlists.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Enabling cover art, lyrics, and guitar tablature](#Enabling_cover_art.2C_lyrics.2C_and_guitar_tablature)
    *   [1.2 Playing audio CDs](#Playing_audio_CDs)
*   [2 Enabling multimedia keys irrespective of DE/WM](#Enabling_multimedia_keys_irrespective_of_DE.2FWM)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Progress bar stuck at 0:00](#Progress_bar_stuck_at_0:00)
    *   [3.2 "Playback error encountered! Configured audiosink bin0 is not working"](#.22Playback_error_encountered.21_Configured_audiosink_bin0_is_not_working.22)
    *   [3.3 "Last.fm Loved Tracks" plugin not working](#.22Last.fm_Loved_Tracks.22_plugin_not_working)
*   [4 Known issues](#Known_issues)
    *   [4.1 Playing from SMB share](#Playing_from_SMB_share)

## Installation

[Install](/index.php/Install "Install") [exaile](https://aur.archlinux.org/packages/exaile/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

If you use [ALSA](/index.php/ALSA "ALSA") and want to use alsasink instead of the default one, [install](/index.php/Install "Install") [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins) available in the [Official repositories](/index.php/Official_repositories "Official repositories"). This may solve problem if no sound is heard after installation and also when trying to play several sources simultaneously.

### Enabling cover art, lyrics, and guitar tablature

[gnome-python-extras](https://www.archlinux.org/packages/?name=gnome-python-extras) and [libgtkhtml](https://aur.archlinux.org/packages/libgtkhtml/)<sup><small>AUR</small></sup> are needed to enable the cover art, lyrics, guitar tablature, and wiki features of Exaile.

### Playing audio CDs

Exaile requires `python-cddb` to play audio cd's. The correct package for this is [cddb-py](https://www.archlinux.org/packages/?name=cddb-py).

## Enabling multimedia keys irrespective of DE/WM

First, run `xev` and retrieve the keycodes for the Previous, Next, Play, Stop, and Mute keys. Then create a textfile and add lines in the following format: `keycode 173 = XF86AudioPrev`. Replace the keycode (173) with your own keycode for the Previous key. Repeat the process for the other keys, substituting 'Prev' for 'Next', 'Play', 'Stop', and 'Mute'.

Then edit `~/.xinitrc` and add the line `xmodmap <file name>` prior to the 'exec' command (if there is one) for the DE/WM, where <file name> is the path to the text file created above.

Finally, in Exaile, go to _Edit > Preferences > Plugins_, and enable the XKeys plugin. After a restart, multimedia keys should work.

## Troubleshooting

### Progress bar stuck at 0:00

First, make sure there are no problems with your sound architecture ([ALSA](/index.php/ALSA "ALSA"), [OSS](/index.php/OSS "OSS"), etc.). And your _playback sink_ in Exaile is set correctly. Try setting it to automatic first.

If you're trying to listen to an MP3 file, try playing an audio file encoded in a different format, such as .ogg or .flac. If these play correctly then try installing [gstreamer0.10-ugly-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-ugly-plugins).

### "Playback error encountered! Configured audiosink bin0 is not working"

If you're getting a message like this, or "Configured audiosink bin1 is not working" (or with another number after 'bin'), it may be because Flash is blocking the use of ALSA by Exaile. You can fix this by running

```
killall npviewer.bin

```

In certain cases (such as if a YouTube video has finished playing), Flash may be blocking the use of ALSA even if an 'npviewer.bin' process is not running. In that case, refreshing the offending page while using a Flash blocking browser extension should fix the problem.

### "Last.fm Loved Tracks" plugin not working

When launched from console, Exaile emits a warning in the command line:

```
WARNING : Error while connecting to Last.fm network: 'module' object has no attribute 'LastFMNetwork'

```

You need to install the [python2-pylast](https://www.archlinux.org/packages/?name=python2-pylast) package from AUR.

## Known issues

### Playing from SMB share

Unfortunately, Exaile does **not** support smb protocol.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Exaile&oldid=412073](https://wiki.archlinux.org/index.php?title=Exaile&oldid=412073)"