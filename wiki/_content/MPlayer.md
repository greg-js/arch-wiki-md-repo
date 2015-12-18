# MPlayer

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [mpv](/index.php/Mpv "Mpv")

**MPlayer** is a popular movie player for GNU/Linux. It has support for most video and audio formats and is thus highly versatile, even if it is mostly used for viewing videos.

## Contents

*   [1 Installation](#Installation)
*   [2 Frontends/GUIs](#Frontends.2FGUIs)
*   [3 Browser integration](#Browser_integration)
    *   [3.1 Firefox](#Firefox)
    *   [3.2 Konqueror](#Konqueror)
    *   [3.3 Chromium](#Chromium)
*   [4 Configuration](#Configuration)
    *   [4.1 Key bindings](#Key_bindings)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Automatic resuming from where you left off](#Automatic_resuming_from_where_you_left_off)
    *   [5.2 Enabling VDPAU](#Enabling_VDPAU)
        *   [5.2.1 Using a configuration file](#Using_a_configuration_file)
        *   [5.2.2 Using a wrapper script](#Using_a_wrapper_script)
    *   [5.3 Enabling VA-API](#Enabling_VA-API)
    *   [5.4 Translucent video with Radeon cards and Composite enabled](#Translucent_video_with_Radeon_cards_and_Composite_enabled)
    *   [5.5 Watching streamed video](#Watching_streamed_video)
        *   [5.5.1 DVD playing](#DVD_playing)
        *   [5.5.2 DVB-T Streaming](#DVB-T_Streaming)
    *   [5.6 JACK support](#JACK_support)
    *   [5.7 Advanced Subtitles](#Advanced_Subtitles)
    *   [5.8 Internet radio](#Internet_radio)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 MPlayer fails to open files with spaces](#MPlayer_fails_to_open_files_with_spaces)
    *   [6.2 MPlayer has black or strange colored font for OSD and Subtitles](#MPlayer_has_black_or_strange_colored_font_for_OSD_and_Subtitles)
    *   [6.3 SMPlayer: No video issue](#SMPlayer:_No_video_issue)
    *   [6.4 SMPlayer: fail to resume playback after pause](#SMPlayer:_fail_to_resume_playback_after_pause)
    *   [6.5 SMPlayer: no video when using transparency in GNOME](#SMPlayer:_no_video_when_using_transparency_in_GNOME)
    *   [6.6 SMPlayer: OSD font too big / subtitle text too small](#SMPlayer:_OSD_font_too_big_.2F_subtitle_text_too_small)
    *   [6.7 Mplayer shows question marks for some characters on subtitle](#Mplayer_shows_question_marks_for_some_characters_on_subtitle)
    *   [6.8 Choppy audio CD playback](#Choppy_audio_CD_playback)
*   [7 See also](#See_also)

## Installation

Various flavours of MPlayer can be [installed](/index.php/Pacman "Pacman") from the [official repositories](/index.php/Official_repositories "Official repositories") or from the [AUR](/index.php/AUR "AUR"):

*   ****MPlayer**** — Official package

[https://mplayerhq.hu/](https://mplayerhq.hu/) || [mplayer](https://www.archlinux.org/packages/?name=mplayer)

Notable variants are:

*   **MPlayer-VAAPI** — VAAPI-enabled version

[http://gitorious.org/vaapi/mplayer](http://gitorious.org/vaapi/mplayer) || [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)<sup><small>AUR</small></sup>

*   **MPlayer-svn** — Development version

|| [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/)<sup><small>AUR</small></sup>

*   **MPlayer2** — Fork of MPlayer

[http://www.mplayer2.org/](http://www.mplayer2.org/) || [mplayer2](https://aur.archlinux.org/packages/mplayer2/)<sup><small>AUR</small></sup> [mplayer2-git](https://aur.archlinux.org/packages/mplayer2-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mplayer2-git)]</sup>

**Note:** _mplayer2_ development seems to be ceased in favour of [mpv](/index.php/Mpv "Mpv"), which is focused on speed and quality of development, though this breaks compatibility with old hardware and software. Be aware of its [differences](https://github.com/mpv-player/mpv/blob/master/DOCS/man/changes.rst) if you want to use it.

## Frontends/GUIs

*   **Deepin Media Player** — Rich GTK2/Python interface for the Deepin desktop.

[http://www.linuxdeepin.com/](http://www.linuxdeepin.com/) || [deepin-media-player](https://aur.archlinux.org/packages/deepin-media-player/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/deepin-media-player)]</sup>

*   **GNOME MPlayer** — Simple GTK+-based GUI for MPlayer.

[http://kdekorte.googlepages.com/gnomemplayer](http://kdekorte.googlepages.com/gnomemplayer) || [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **KPlayer** — Multimedia player for KDE4 using mplayer as a backend.

[http://kplayer.sourceforge.net/](http://kplayer.sourceforge.net/) || [kplayer](https://aur.archlinux.org/packages/kplayer/)<sup><small>AUR</small></sup>

*   **KMPlayer** — Video player plugin for Konqueror and basic MPlayer/Xine/ffmpeg/ffserver/VDR frontend for KDE.

[http://kmplayer.kde.org/](http://kmplayer.kde.org/) || [kmplayer](https://aur.archlinux.org/packages/kmplayer/)<sup><small>AUR</small></sup>

*   **Rosa Media Player** — Multimedia player based on SMPlayer with clean and elegant UI.

[http://www.rosalab.com/](http://www.rosalab.com/) || [rosa-media-player](https://aur.archlinux.org/packages/rosa-media-player/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rosa-media-player)]</sup>

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Qt multimedia player with extra features (CSS themes, YouTube integration, etc.).

[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **Xt7-Player** — Graphical user interface for MPlayer written in Gambas, with a huge list of features.

[http://xt7-player.sourceforge.net/xt7forum/](http://xt7-player.sourceforge.net/xt7forum/) || [xt7-player](https://aur.archlinux.org/packages/xt7-player/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xt7-player)]</sup>

## Browser integration

If you want to let MPlayer control video viewing in your favorite web browser, install one of the following plugins for your browser.

### Firefox

A browser plugin is available in the official repositories with the [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer) package.

**Note:** It depends on [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer), which provides a complete frontend to MPlayer.

### Konqueror

A plugin for Konqueror can be found in the [AUR](/index.php/AUR "AUR") with the [kmplayer](https://aur.archlinux.org/packages/kmplayer/)<sup><small>AUR</small></sup> package.

**Note:** [kmplayer](https://aur.archlinux.org/packages/kmplayer/)<sup><small>AUR</small></sup> also provides a complete frontend to MPlayer.

### Chromium

The [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer) plugin for Firefox also works in [Chromium](/index.php/Chromium "Chromium").

## Configuration

System-wide configuration files are located in the `/etc/mplayer/`, whereas the user-local settings are stored in `~/.mplayer/` directory. The default files in the `/etc/mplayer/` are:

*   `codecs.conf` - Contains configuration of codecs.
*   `example.conf` - Is an example of mplayer.conf, which is not automatically created after installation.
*   `input.conf` - Contains configuration of a hotkeys.

In the `~/.mplayer/` by default created a file with a name _config_.

See also: [Example MPlayer configuration file](http://mplayerhq.hu/DOCS/man/en/mplayer.1.html#CONFIGURATION%20FILES), `man mplayer`.

### Key bindings

System key bindings are configured via `/etc/mplayer/input.conf`. Personal key bindings are stored in `~/.mplayer/input.conf`. For a complete list of keyboard shortcuts look at `man mplayer`.

See also: [XF86 keyboard symbols](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols)

## Tips and tricks

### Automatic resuming from where you left off

To get this behavior, you can install the [mplayer-resumer](https://aur.archlinux.org/packages/mplayer-resumer/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR"). The package contains a Perl wrapper script for MPlayer which will allow you to autoresume playback from the point it was last stopped.

To use it, simply call the wrapper script in place of MPlayer:

```
$ mplayer-resumer _options_ _path/to/file_

```

If this script is restarted within a short amount of time after closing MPayer (default 5 seconds) then it will delete the file used to keep track of the videos resume position, effectively starting the video from the beginning.

If the video file to be played is on a read-only filesystem, or otherwise lives in a location that cannot be written to, resume will fail. This is because the current implementation uses a file parallel to the video file to store the timecode.

### Enabling VDPAU

For a complete list of NVIDIA VDPAU capable hardware, see [this table](http://en.wikipedia.org/wiki/PureVideo#Table_of_PureVideo_.28HD.29_GPUs). Ensure the [nvidia](https://www.archlinux.org/packages/?name=nvidia) driver is installed and consider one of the following two methods to automatically enable VDPAU for playback.

For an Intel or (AMD with [Catalyst](/index.php/Catalyst "Catalyst")) video card, you can use [libvdpau-va-gl](https://www.archlinux.org/packages/?name=libvdpau-va-gl) — VAAPI backend for VDPAU. For AMD you should also install [xvba-video](https://aur.archlinux.org/packages/xvba-video/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xvba-video)]</sup>. To use it, create:

 `/etc/profile.d/vdpau_vaapi.sh` 

```
#!/bin/sh
export VDPAU_DRIVER=va_gl

```

and make it executable:

```
# chmod +x /etc/profile.d/vdpau_vaapi.sh

```

and reboot or relogin.

[The open source driver for AMD video cards](/index.php/ATI#Enabling_video_acceleration "ATI") provides VDPAU.

#### Using a configuration file

Append the following to either the system-wide (`/etc/mplayer/mplayer.conf`) or user-specific (`~/.mplayer/config`) configuration files:

```
vo=vdpau,
vc=ffh264vdpau,ffmpeg12vdpau,ffodivxvdpau,ffwmv3vdpau,ffvc1vdpau,

```

**Note:**

*   The trailing commas are important! They tell MPlayer to fall back on other drivers and codecs should the specified ones not be found.
*   `-vo` option selects VDPAU video output driver, `-vc` option selects VDPAU video codecs.

**Warning:** The `ffodivxvdpau` codec is only supported by the most recent series of NVIDIA hardware. Consider omitting it based on your specific hardware. See [the NVIDIA page](/index.php/NVIDIA#Pure_Video_HD_.28VDPAU.2FVAAPI.29 "NVIDIA") for more information.

#### Using a wrapper script

The [AUR](/index.php/AUR "AUR") contains a trivial Bash script called [mplayer-vdpau-auto](https://aur.archlinux.org/packages/mplayer-vdpau-auto/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mplayer-vdpau-auto)]</sup> that detects which video codec to use and when to use VDPAU as the video output.

Another simple wrapper is [mplayer-vdpau-shell-git](https://aur.archlinux.org/packages/mplayer-vdpau-shell-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mplayer-vdpau-shell-git)]</sup>, which can recover from a VDPAU FATAL error. This wrapper uses the "-include" option to include a VDPAU configuration, so it will ignore any VDPAU specific settings in your `~/.mplayer/config` file.

### Enabling VA-API

This requires [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)<sup><small>AUR</small></sup> from the AUR.

 `$ mplayer -vo vaapi -va vaapi _foobar.mpeg_` 

*   **-vo** - Select vaapi video output driver
*   **-va** - Select vaapi video decoder driver

MPlayer based players:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): To enable hardware acceleration: _Edit > Preferences > Player_, then set Video Output to `vaapi`.
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): To enable hardware acceleration: _Options > Preferences > General > Video_, then set Output driver to `vaapi`.

### Translucent video with Radeon cards and Composite enabled

To get translucent video output in X you have to enable textured video in MPlayer:

```
$ mplayer -vo xv:adaptor=1 _file_

```

Or add the following line to `~/.mplayer/config`:

```
vo=xv:adaptor=1

```

You can use `xvinfo` to check which video modes your graphic card supports.

### Watching streamed video

If you want to play a video stream (e.g an `ASX` link) use:

```
$ mplayer -playlist link-to-stream.asx

```

The `-playlist` option is necessary because these streams are actually playlists and cannot be played without it.

#### DVD playing

To play a DVD with MPlayer:

```
$ mplayer dvd://_N_

```

where _N_ is the desired title number. Start at 1 and work up if unsure. To start at a specific chapter use the '-chapter' flag. For example, adding '-chapter 5' to the command starts the dvd playing at chapter five of the title.

Mplayer checks `/dev/dvd` by default. Tell it to use `/dev/sr0` with the `dvd-device` option at the command line, or the `dvd-device` variable in `~/.mplayer/config`.

To play a DVD image file:

```
$ mplayer -dvd-device movie.iso dvd://_N_

```

To enable the DVD menu use:

```
$ mplayer dvdnav://

```

**Note:** You use arrow keys to navigate and the `Enter` key to choose.

To enable mouse support in DVD menus use:

```
$ mplayer -mouse-movements dvdnav://

```

To find the audio language, start MPlayer with the `-v` switch to output audio IDs. An audio track is selected with `-aid _audio_id_`. Set a default audio language by editing `~/.mplayer/config` and adding the line `alang=en` for English.

With MPlayer, the DVD could be set to a low volume. To increase the maximum volume to 400%, use `softvol=yes` and `softvol-max=400`. The startup volume defaults to 100% of software volume and the global mixer levels will remain untouched. Using the `9` and `0` keys, volume can be adjusted between 0 and 400 percent.

```
alang=en
softvol=yes
softvol-max=400

```

#### DVB-T Streaming

See [DVB-T](/index.php/DVB-T "DVB-T") for more info.

### JACK support

To have MPlayer audio output directed to [JACK](/index.php/JACK "JACK") as its default behavior, edit `~/.mplayer/config` and add:

```
ao=jack

```

If you do not have JACK running all the time, you can have MPlayer output to JACK on an as-needed basis by invoking MPlayer from the command line as such:

```
$ mplayer -ao jack _path/to/file_

```

### Advanced Subtitles

In order to get Advanced SubStation Alpha (ass) or SubStation Alpha (ssa) formatted subtitles to display properly you need to either edit `~/.mplayer/config` and add:

```
ass=true

```

or add -ass to the command line:

```
$ mplayer -ass _path/to/subtitledVideo.mkv_

```

One possible indication of needing to enable this flag is if you get numbers appearing with your subtitles. This is caused by the positioning information being interpreted as something to be displayed. Mplayer will also complain about subtitles being either too long or having too many lines.

Enabling `ass` also enables any embedded fonts. As per the note in the mplayer's man adding `embeddedfonts=true` is unneeded if [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) is version 2.4.2 or newer. Fontconfig will also be used to select which font to use when there are no embedded fonts. This may result in a different font being used than the OSD subtitle renderer.

### Internet radio

Here is an example of a script for an easy start/stop of playing a predefined radio station. [[1]](http://www.linuxforums.org/forum/miscellaneous/199396-mplayer-flash.html#post941062)

```
#!/bin/bash
XX="X"$1;
PLAYIT='mplayer  -loop 0 -playlist http://*.*.*.*:8000/listen.pls';

if [ "$XX" == "Xstop" ]; then
  killall mplayer;
else
  if [ 'EX' == 'EX'"$(pidof mplayer)" ]; then
    if [ "$UID" -ne 0 ]; then 
      nohup $PLAYIT &> /dev/null & disown;
    else 
      echo The "root" user is not allowed to run this script.
    fi
  else
    echo mplayer is already running by user: $(ps -eo user,comm | grep -i "mplayer"$ | sed 's/ mplayer/,/m') | sed "s/ ,$/./m";
  fi
fi

```

For more details on a running mplayer instance:

```
$ ps -eo pcpu,pid,user,comm | grep -i "mplayer"$ | sed  "s/ mplayer$//m"

```

## Troubleshooting

### MPlayer fails to open files with spaces

MPlayer can fail to open a file with spaces (e.g. 'The Movie') by saying that it could not open the file `file:///_The%20Movie_` (where all spaces are converted to `%20`). This can be fixed by editing `/usr/share/applications/mplayer.desktop` to changing the following line from:

```
Exec=mplayer %U

```

to:

```
Exec=mplayer "%F"

```

If you use a frontend/GUI for MPlayer, enter its name in `Exec=gui_name "%F"`.

### MPlayer has black or strange colored font for OSD and Subtitles

There appears to be an issue with OSD and Subtitle colors when using vdpau output, which mplayer may be using by default. You can get around this issue by using xv instead of vdpau:

As a command line option:

```
mplayer -vo xv

```

Adding the following line to your `~/.mplayer/config` file:

```
vo=xv

```

See the original [forums thread](https://bbs.archlinux.org/viewtopic.php?pid=1379141) for details.

### SMPlayer: No video issue

SMPlayer may have trouble opening some `MP4` (and probably `FLV`) videos. If it plays only audio without any video, a possible fix is to add the following lines to your `~/.mplayer/config` file:

```
[extension.mp4]
demuxer=mov

```

If problem persists after doing so, it is because SMPlayer is keeping settings for that specific file. Deleting the settings for all the files that SMPlayer is keeping will solve this problem:

```
$ rm -rf ~/.config/smplayer/file_settings

```

### SMPlayer: fail to resume playback after pause

SMPlayer might stop playing a video after pausing it if your audio output driver is incorrectly set. You can fix this by specifically setting your audio driver. For example, if you use PulseAudio, this can be done by starting MPlayer with the `-ao pulse` argument or by adding the following to your `~/.mplayer/config` file:

```
ao=pulse

```

You can also change this from SMPlayer by going to _Options > Preferences > General > Audio_ and setting the _Output Driver_ option to _pulse_.

### SMPlayer: no video when using transparency in GNOME

This problem may arise under GNOME when using Compiz to provide transparency: SMPlayer starts with a transparent screen with audio playing, but no video. To fix this, create (as root) a file with the contents:

 `/usr/local/bin/smplayer.helper` 

```
export XLIB_SKIP_ARGB_VISUALS=1
exec smplayer.real "$@"

```

Then do the following:

```
# chmod 755 /usr/local/bin/smplayer.helper
# ln -sf /usr/local/bin/smplayer.helper /usr/local/bin/smplayer

```

### SMPlayer: OSD font too big / subtitle text too small

Since SMPlayer 0.8.2.1 (with MPlayer2 20121128-1), the ratio of the subtitle font to the OSD font is very strange. This can result in the OSD text filling the whole screen while the subtitles are very small and unreadable. This problem can be solved by adding:

```
-subfont-osd-scale 2

```

or to the extra options passed to MPlayer from SMPlayer. These options are found in _Options > Preferences > Advanced > Options for MPlayer_. This can also be achieved by adding the following line to `~/.mplayer/config`:

```
subfont-osd-scale=2

```

### Mplayer shows question marks for some characters on subtitle

If the codepage of the subtitles is utf8, try using:

```
-subcp utf8

```

You can find the codepage of the subtitles with:

```
file subtitles.srt

```

See [mplayer-shows-question-marks-for-some-characters-on-subtitle](http://www.linuxquestions.org/questions/slackware-14/mplayer-shows-question-marks-for-some-characters-on-subtitle-works-fine-on-xine-906077/).

### Choppy audio CD playback

CDDA playback may be interrupted every few seconds as the CDROM spins down the CD. To get around this you need to cache or buffer in advance using the `-cache` option:

```
mplayer cdda://:1 -cache 1024

```

The `:1` is to lower the CDROM speed for a constant spin and less noise.

## See also

*   [Official MPlayer website](http://www.mplayerhq.hu/)
*   [Official MPlayer2 website](http://www.mplayer2.org/)
*   [MPlayer FAQ](http://wiki.multimedia.cx/index.php?title=MPlayer_FAQ)
*   [MPlayer notes](https://www.youtube.com/watch?v=n4Ul_A0VBVI)
*   [MPlayer tips](https://help.ubuntu.com/community/MPlayerTips)
*   [How to configure MPlayer](http://how-to.wikia.com/wiki/How_to_configure_MPlayer)
*   [playerctl](https://github.com/acrisci/playerctl): A command-line utility and library for controlling media players

Retrieved from "[https://wiki.archlinux.org/index.php?title=MPlayer&oldid=412708](https://wiki.archlinux.org/index.php?title=MPlayer&oldid=412708)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")