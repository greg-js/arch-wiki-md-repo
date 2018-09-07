Related articles

*   [mpv](/index.php/Mpv "Mpv")

[MPlayer](http://www.mplayerhq.hu/) is a popular movie player for GNU/Linux. It has support for most video and audio formats and is thus highly versatile, even if it is mostly used for viewing videos.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Frontends/GUIs](#Frontends.2FGUIs)
*   [2 Configuration](#Configuration)
    *   [2.1 Key bindings](#Key_bindings)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Automatic resuming from where you left off](#Automatic_resuming_from_where_you_left_off)
    *   [3.2 Hardware video acceleration](#Hardware_video_acceleration)
        *   [3.2.1 Enabling VDPAU](#Enabling_VDPAU)
        *   [3.2.2 Enabling VA-API](#Enabling_VA-API)
    *   [3.3 Translucent video with Radeon cards and Composite enabled](#Translucent_video_with_Radeon_cards_and_Composite_enabled)
    *   [3.4 Watching streamed video](#Watching_streamed_video)
        *   [3.4.1 DVD playing](#DVD_playing)
        *   [3.4.2 DVB-T Streaming](#DVB-T_Streaming)
    *   [3.5 JACK support](#JACK_support)
    *   [3.6 Advanced Subtitles](#Advanced_Subtitles)
    *   [3.7 Internet radio](#Internet_radio)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 MPlayer fails to open files with spaces](#MPlayer_fails_to_open_files_with_spaces)
    *   [4.2 MPlayer has black or strange colored font for OSD and Subtitles](#MPlayer_has_black_or_strange_colored_font_for_OSD_and_Subtitles)
    *   [4.3 SMPlayer: No video issue](#SMPlayer:_No_video_issue)
    *   [4.4 SMPlayer: fail to resume playback after pause](#SMPlayer:_fail_to_resume_playback_after_pause)
    *   [4.5 SMPlayer: no video when using transparency in GNOME](#SMPlayer:_no_video_when_using_transparency_in_GNOME)
    *   [4.6 SMPlayer: OSD font too big / subtitle text too small](#SMPlayer:_OSD_font_too_big_.2F_subtitle_text_too_small)
    *   [4.7 Mplayer shows question marks for some characters on subtitle](#Mplayer_shows_question_marks_for_some_characters_on_subtitle)
    *   [4.8 Choppy audio CD playback](#Choppy_audio_CD_playback)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mplayer](https://www.archlinux.org/packages/?name=mplayer) package, or [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/) for the development version.

Notable variants are:

*   **MPlayer-VAAPI** — VAAPI-enabled version

	[http://gitorious.org/vaapi/mplayer](http://gitorious.org/vaapi/mplayer) || [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)

*   **MPlayer2** — Fork of MPlayer

	[https://github.com/nezumisama/mplayer2](https://github.com/nezumisama/mplayer2) || [mplayer2](https://aur.archlinux.org/packages/mplayer2/)

**Note:** *mplayer2* development seems to be ceased in favour of [mpv](/index.php/Mpv "Mpv"), which is focused on speed and quality of development, though this breaks compatibility with old hardware and software. Be aware of its [differences](https://github.com/mpv-player/mpv/blob/master/DOCS/mplayer-changes.rst) if you want to use it.

### Frontends/GUIs

See [List of applications/Multimedia#MPlayer-based](/index.php/List_of_applications/Multimedia#MPlayer-based "List of applications/Multimedia").

## Configuration

System-wide configuration files are located in the `/etc/mplayer/`, whereas the user-local settings are stored in `~/.mplayer/` directory. The default files in the `/etc/mplayer/` are:

*   `codecs.conf` - Contains configuration of codecs.
*   `example.conf` - Is an example of mplayer.conf, which is not automatically created after installation.
*   `input.conf` - Contains configuration of a hotkeys.

A file `config` is created in the `~/.mplayer/` directory by default.

See also: [Example MPlayer configuration file](http://mplayerhq.hu/DOCS/man/en/mplayer.1.html#CONFIGURATION%20FILES), [mplayer(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1).

### Key bindings

System key bindings are configured via `/etc/mplayer/input.conf`. Personal key bindings are stored in `~/.mplayer/input.conf`. For a complete list of keyboard shortcuts look at [mplayer(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1).

See also: [XF86 keyboard symbols](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols)

## Tips and tricks

### Automatic resuming from where you left off

To get this behavior, you can install the [mplayer-resumer](https://aur.archlinux.org/packages/mplayer-resumer/) package from the [AUR](/index.php/AUR "AUR"). The package contains a Perl wrapper script for MPlayer which will allow you to autoresume playback from the point it was last stopped.

To use it, simply call the wrapper script in place of MPlayer:

```
$ mplayer-resumer *options* *path/to/file*

```

If this script is restarted within a short amount of time after closing MPayer (default 5 seconds) then it will delete the file used to keep track of the videos resume position, effectively starting the video from the beginning.

If the video file to be played is on a read-only filesystem, or otherwise lives in a location that cannot be written to, resume will fail. This is because the current implementation uses a file parallel to the video file to store the timecode.

### Hardware video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

#### Enabling VDPAU

Append the following to either the system-wide (`/etc/mplayer/mplayer.conf`) or user-specific (`~/.mplayer/config`) configuration files:

```
vo=vdpau,
vc=ffh264vdpau,ffmpeg12vdpau,ffodivxvdpau,ffwmv3vdpau,ffvc1vdpau,ffhevcvdpau

```

**Note:**

*   The trailing commas are important! They tell MPlayer to fall back on other drivers and codecs should the specified ones not be found.
*   `-vo` option selects VDPAU video output driver, `-vc` option selects VDPAU video codecs.

**Warning:** The `ffodivxvdpau` codec is only supported by the most recent series of NVIDIA hardware. Consider omitting it based on your specific hardware. See [NVIDIA#VDPAU](/index.php/NVIDIA#VDPAU "NVIDIA") for more information.

#### Enabling VA-API

This requires [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) from the AUR.

 `$ mplayer -vo vaapi -va vaapi *foobar.mpeg*` 

*   **-vo** - Select vaapi video output driver
*   **-va** - Select vaapi video decoder driver

MPlayer based players:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): To enable hardware acceleration: *Edit > Preferences > Player*, then set Video Output to `vaapi`.
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): To enable hardware acceleration: *Options > Preferences > General > Video*, then set Output driver to `vaapi`.

### Translucent video with Radeon cards and Composite enabled

To get translucent video output in X you have to enable textured video in MPlayer:

```
$ mplayer -vo xv:adaptor=1 *file*

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
$ mplayer dvd://*N*

```

where *N* is the desired title number. Start at 1 and work up if unsure. To start at a specific chapter use the '-chapter' flag. For example, adding '-chapter 5' to the command starts the dvd playing at chapter five of the title.

Mplayer checks `/dev/dvd` by default. Tell it to use `/dev/sr0` with the `dvd-device` option at the command line, or the `dvd-device` variable in `~/.mplayer/config`.

To play a DVD image file:

```
$ mplayer -dvd-device movie.iso dvd://*N*

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

To find the audio language, start MPlayer with the `-v` switch to output audio IDs. An audio track is selected with `-aid *audio_id*`. Set a default audio language by editing `~/.mplayer/config` and adding the line `alang=en` for English.

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
$ mplayer -ao jack *path/to/file*

```

### Advanced Subtitles

In order to get Advanced SubStation Alpha (ass) or SubStation Alpha (ssa) formatted subtitles to display properly you need to either edit `~/.mplayer/config` and add:

```
ass=true

```

or add -ass to the command line:

```
$ mplayer -ass *path/to/subtitledVideo.mkv*

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

MPlayer can fail to open a file with spaces (e.g. 'The Movie') by saying that it could not open the file `file:///*The%20Movie*` (where all spaces are converted to `%20`). This can be fixed by editing `/usr/share/applications/mplayer.desktop` to changing the following line from:

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

You can also change this from SMPlayer by going to *Options > Preferences > General > Audio* and setting the *Output Driver* option to *pulse*.

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

or to the extra options passed to MPlayer from SMPlayer. These options are found in *Options > Preferences > Advanced > Options for MPlayer*. This can also be achieved by adding the following line to `~/.mplayer/config`:

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

*   [MPlayer FAQ](https://wiki.multimedia.cx/index.php?title=MPlayer_FAQ)
*   [MPlayer tips](https://help.ubuntu.com/community/MPlayerTips)
*   [How to configure MPlayer](http://how-to.wikia.com/wiki/How_to_configure_MPlayer)
*   [playerctl](https://github.com/acrisci/playerctl): A command-line utility and library for controlling media players