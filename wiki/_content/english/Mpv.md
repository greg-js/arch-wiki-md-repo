[mpv](http://mpv.io/) is a media player based on [MPlayer](/index.php/MPlayer "MPlayer") and MPlayer2\. It supports a wide variety of video file formats, audio and video codecs, and subtitle types. A comprehensive (although admittedly incomplete) list of differences between *mpv* and the aforementioned players can be found [here](https://github.com/mpv-player/mpv/blob/master/DOCS/mplayer-changes.rst).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Front ends](#Front_ends)
*   [2 Configuration](#Configuration)
    *   [2.1 An example input.conf file](#An_example_input.conf_file)
    *   [2.2 mpv and PulseAudio since 0.18.1](#mpv_and_PulseAudio_since_0.18.1)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 Hardware Decoding](#Hardware_Decoding)
    *   [3.2 High quality video output](#High_quality_video_output)
    *   [3.3 Automatically resuming from where you left off](#Automatically_resuming_from_where_you_left_off)
    *   [3.4 Volume is too low](#Volume_is_too_low)
    *   [3.5 Quickly cycle between multiple aspect ratio](#Quickly_cycle_between_multiple_aspect_ratio)
    *   [3.6 Drawing to a root window](#Drawing_to_a_root_window)
    *   [3.7 Always show GUI](#Always_show_GUI)
    *   [3.8 Restoring old OSC](#Restoring_old_OSC)
    *   [3.9 Use as a browser plugin](#Use_as_a_browser_plugin)
    *   [3.10 Improving mpv as a music player with Lua scripts](#Improving_mpv_as_a_music_player_with_Lua_scripts)
    *   [3.11 Twitch.tv streaming over mpv](#Twitch.tv_streaming_over_mpv)
    *   [3.12 youtube-dl and choosing formats](#youtube-dl_and_choosing_formats)
    *   [3.13 youtube-dl audio with search](#youtube-dl_audio_with_search)
    *   [3.14 Use mpv with a compositor](#Use_mpv_with_a_compositor)
*   [4 Vapoursynth](#Vapoursynth)
    *   [4.1 Debanding (flash3kyuu)](#Debanding_.28flash3kyuu.29)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Fix jerky playback and tearing](#Fix_jerky_playback_and_tearing)

## Installation

[Install](/index.php/Install "Install") the [mpv](https://www.archlinux.org/packages/?name=mpv) package from the [official repositories](/index.php/Official_repositories "Official repositories") or [mpv-git](https://aur.archlinux.org/packages/mpv-git/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

### Front ends

*mpv* provides an elegant User Interface called OSC which appears when moving the mouse. To ease casual users, other graphical interfaces exist:

*   **Baka MPlayer** — Free and open source, cross-platform, *libmpv* based multimedia player (Qt 5).

	[http://bakamplayer.u8sand.net/](http://bakamplayer.u8sand.net/) || [baka-mplayer](https://www.archlinux.org/packages/?name=baka-mplayer), [baka-mplayer-git](https://aur.archlinux.org/packages/baka-mplayer-git/)

*   **bomi** — Powerful and easy to use multimedia player (Qt 5).

	[https://bomi-player.github.io/](https://bomi-player.github.io/) || [bomi](https://aur.archlinux.org/packages/bomi/), [bomi-git](https://aur.archlinux.org/packages/bomi-git/)

*   **GNOME MPV** — A simple frontend for *mpv* (GTK+ 3).

	[http://gnome-mpv.github.io/](http://gnome-mpv.github.io/) || [gnome-mpv](https://aur.archlinux.org/packages/gnome-mpv/), [gnome-mpv-git](https://aur.archlinux.org/packages/gnome-mpv-git/)

*   **Media Player Classic Qute Theater** — A clone of [Media Player Classic](https://en.wikipedia.org/wiki/Media_Player_Classic "wikipedia:Media Player Classic") reimplimented in Qt.

	[https://github.com/cmdrkotori/mpc-qt](https://github.com/cmdrkotori/mpc-qt) || [mpc-qt-git](https://aur.archlinux.org/packages/mpc-qt-git/)

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Qt multimedia player with extra features (CSS themes, YouTube integration, etc.) (Qt 5).

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **xt7-player-mpv** — Qt/Gambas GUI to mpv with a rich set of configurable options including filters and drivers, ladspa plugins support as well as library/playlist managment, YouTube, online radios, podcasts, DVB-T and more.

	[https://github.com/kokoko3k/xt7-player-mpv](https://github.com/kokoko3k/xt7-player-mpv) || [xt7-player-mpv-git](https://aur.archlinux.org/packages/xt7-player-mpv-git/)

**Note:** CMPlayer/*bomi* packages provide *mpv* internally.

## Configuration

*mpv'*s configuration is read from the files `mpv.conf` ([example](https://raw.githubusercontent.com/mpv-player/mpv/master/etc/mpv.conf)) (settings), `input.conf` (key bindings), and `lua-settings/osc.conf` ([example](https://raw.githubusercontent.com/mpv-player/mpv/master/etc/input.conf)) (on screen display). For a full list of options, see the [mpv(1)](https://mpv.io/manual/master/) or the github docs [options.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/options.rst), [input.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/input.rst), and [osc.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/osc.rst).

If the [environment variable](/index.php/Environment_variable "Environment variable") `XDG_CONFIG_HOME` is not set, user configuration files will be read from the `~/.config/mpv` directory. System-wide configuration files are read from the `/etc/mpv` directory.

### An example input.conf file

Copying the following into `~/.config/mpv/input.conf` will add a number of useful keybindings to mpv such as rotating video 90 degrees, zooming and panning.

```
Alt+RIGHT add video-rotate 90
Alt+LEFT add video-rotate -90
Alt+- add video-zoom -0.25
Alt+= add video-zoom 0.25
Alt+j add video-pan-x -0.05
Alt+l add video-pan-x 0.05
Alt+i add video-pan-y 0.05
Alt+k add video-pan-y -0.05

```

### mpv and PulseAudio since 0.18.1

This entry only applies if you are using pulseaudio for mpv (`-ao=pulse` or `ao=pulse` in `mpv.conf`).

Add the following to your `~/.config/mpv/input.conf` to make volume changes work again from PulseAudio to mpv and vice versa:

```
/ add ao-volume -2
SHIFT+* add ao-volume 2

```

Change the above to whatever volume keys you use. The above is the default of MPV only handles by "softvol" and with those lines handled by PulseAudio.

## Tips and Tricks

### Hardware Decoding

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

Unlike *mplayer* and *mplayer2*, *mpv* has both VA-API and VDPAU support built-in. To enable it, run *mpv* with the `--hwdec='method'` option. You can find list of all available methods looking for `--hwdec=<api>` in [man page](/index.php/Man_page "Man page") [mpv(1)](https://mpv.io/manual/master/). To make this persistent, add the line `hwdec=*method*` to your configuration file.

When hardware decoding is used, the video output should generally be set to `opengl` or `opengl-hq` (or possibly `vdpau` if using `hwdec=vdpau`). In particular, `hwdec=vaapi` should be used with `vo=opengl` [[1]](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst) if possible.

If hardware decoding cannot be used, *mpv* will automatically fall back to software decoding.

By default, hardware decoding is enabled for codecs h264, vc1, wmv3, hevc, mpeg2video and vp9\. It is however possible to specify codecs (e.g. `--hwdec-codecs=h264,mpeg2video`) or allow all codecs (`hwdec-codecs=all`) to use hardware decoding.

### High quality video output

The `opengl-hq` profile is a high quality preset which use the OpenGL video driver and enables various options selected by the mpv developers. To make use of it, specify it in your configuration file.

 `~/.config/mpv/mpv.conf`  `profile=opengl-hq` 

This comes with a GLSL debanding filter by default, which may lead to bad performance for some users, and can reduce the visual quality of grainy content. You can disable it easily though.

 `~/.config/mpv/mpv.conf` 
```
profile=opengl-hq
deband=no
```

### Automatically resuming from where you left off

The default key to quit *mpv*, saving the video's current position and state, is `Shift+q`. This key can be changed by adding the `quit_watch_later` string in the key bindings configuration file.

To always automatically save the current playback position on quit, start *mpv* with a flag `--save-position-on-quit`. To make option permanent, add line `save-position-on-quit` to configuration file.

### Volume is too low

Set `volume-max=*value*` in your configuration file to a reasonable amount, such as `volume-max=600`. Additionally (or alternatively), you can utilize [dynamic range compression](https://en.wikipedia.org/wiki/Dynamic_range_compression "wikipedia:Dynamic range compression") with `af=drc`.

### Quickly cycle between multiple aspect ratio

You can cycle between aspect ratios using `Shift+a` from version 0.8.0 onwards.

### Drawing to a root window

Run *mpv* with `--wid=0`. This tells *mpv* to draw onto a window with a window ID of 0.

### Always show GUI

It may be useful to always show the GUI window, even for audio files, especially when *mpv* is not started from terminal. This can be done by using `--force-window` option.

### Restoring old OSC

Since version 0.21.0, mpv has replaced the on-screen controls by a bottombar. In case you want on-screen controls back, you can edit the mpv configuration [as described here](https://github.com/mpv-player/mpv/wiki/FAQ#i-want-the-old-osc-back).

### Use as a browser plugin

With the help of [mozplugger](https://aur.archlinux.org/packages/mozplugger/), *mpv* can be used in a supported browser to play video. See [Browser plugins#MozPlugger](/index.php/Browser_plugins#MozPlugger "Browser plugins") for configuration details. This coupled with a user script such as [ViewTube](http://isebaro.com/viewtube/?ln=en), allows you to use *mpv* in place of a site's integrated video player.

It may be needed to specify a valid user agent for HTTP streaming, e.g. `user-agent="Mozilla/5.0 (X11; Linux x86_64; rv:49.0) Gecko/20100101 Firefox/49.0"`.

[Browser plugins#Video players workarounds](/index.php/Browser_plugins#Video_players_workarounds "Browser plugins") page shows other easy ways to watch videos.

### Improving mpv as a music player with Lua scripts

The development of mpv's Lua scripts are documented in [DOCS/man/lua.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/lua.rst) and examples are shown in [TOOLS/lua](https://github.com/mpv-player/mpv/tree/master/TOOLS/lua) of the [mpv repository](https://github.com/mpv-player/mpv). [This blog post](https://web.archive.org/web/20160320001546/http://bamos.github.io/2014/07/05/mpv-lua-scripting/) introduces the [music.lua](https://github.com/bamos/dotfiles/blob/master/.mpv/scripts/music.lua) script, which shows how Lua scripts can be used to improve mpv as a music player.

### Twitch.tv streaming over mpv

If [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl) is installed, mpv can directly open a Twitch livestream.

Alternatively, [livestreamer](https://www.archlinux.org/packages/?name=livestreamer) can be used to stream Twitch. See [Livestreamer#Twitch](/index.php/Livestreamer#Twitch "Livestreamer").

Another alternative based on Livestreamer is this Lua script: [https://gist.github.com/ChrisK2/8701184fe3ea7701c9cc](https://gist.github.com/ChrisK2/8701184fe3ea7701c9cc)

### youtube-dl and choosing formats

The default `--ytdl-format` is `bestvideo+bestaudio/best`. For youtube videos that have 4K resolutions available, this may mean that your device will struggle to decode 4K VP9 encoded video in software even if the attached monitor is much lower resolution.

Setting the right youtube-dl format selectors can fix this easily though. In the following configuration example, only videos with a vertical resolution of 1080 pixels or less will be considered.

```
ytdl-format=bestvideo[height<=?1080]+bestaudio/best

```

If you wish to avoid a certain codec altogether because you cannot hardware-decode it, you can add this to the format selector. For example, we can additionally choose to ignore VP9 as follows:

```
ytdl-format=bestvideo[height<=?1080][vcodec!=vp9]+bestaudio/best

```

### youtube-dl audio with search

To find and play audio straight from your terminal with `mm "*search terms*"` put the following function in your `.bashrc`:

```
function mm() {
    mpv --no-video --ytdl-format=bestaudio ytdl://ytsearch10:"$@"
}

```

### Use mpv with a compositor

If you're using a compositor (e.g. in KDE Plasma 5) and find that composition is disabled (e.g. in Plasma this would make you unable to present windows or see window thumbnails in the default app switcher) when mpv is playing a video, try `x11-bypass-compositor=no`

## Vapoursynth

Vapoursynth is an alternative to AviSynth that can be used on Linux and allows for Video manipulation via python scripts. Vapoursynths python scripts can be used as video filters for *mpv*.

To use vapoursynth filters you have to install the [vapoursynth](https://www.archlinux.org/packages/?name=vapoursynth) package and compile *mpv* with the `--enable-vapoursynth` build flag.

### Debanding (flash3kyuu)

To use the `f3k_db` debanding filter install [vapoursynth-plugin-f3kdb](https://www.archlinux.org/packages/?name=vapoursynth-plugin-f3kdb) and write a python script that uses the *vapoursynth* extension.

The following sample script can be used to enable debanding in *mpv*.

```
import vapoursynth as vs
core = vs.get_core()

clip = video_in
clip = core.std.Trim(clip, first=0, length=500000)
clip = core.f3kdb.Deband(clip, grainy=0, grainc=0, output_depth=16)
clip.set_output()

```

Finally specify the python script in the config file or use a command line argument when executing mpv.

```
$ mpv --vf=vapoursynth=f3k_db.py <video_file>

```

## Troubleshooting

### Fix jerky playback and tearing

mpv defaults to using the opengl video output device setting on hardware that supports it. In cases such as trying to play video back on a 4K display using a Intel HD4XXX series card or similar, you will find video playback unreliable, jerky to the point of stopping entirely at times and with major tearing when using any opengl output setting. If you experience any of these issues, using the xv (XVideo) video output device may help.

 `~/.config/mpv/mpv.conf`  `vo=xv` 

It is possible to increase decoding performance (especially on lower hardware), but this may affect the video quality. See the [configuration section](/index.php/Mpv#Configuration "Mpv") for information about the available options.

The following options can be considered to increase video performance:

 `~/.config/mpv/mpv.conf` 
```
vd-lavc-fast
vd-lavc-skiploopfilter=<skipvalue>
vd-lavc-skipframe=<skipvalue>
vd-lavc-framedrop=<skipvalue>
vd-lavc-threads=<threads>
```