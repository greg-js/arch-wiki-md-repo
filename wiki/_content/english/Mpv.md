Related articles

*   [MPlayer](/index.php/MPlayer "MPlayer")
*   [youtube-dl](/index.php/Youtube-dl "Youtube-dl")

[mpv](https://mpv.io/) is a media player based on [MPlayer](/index.php/MPlayer "MPlayer") and the now unmaintained *mplayer2*. It supports a wide variety of video file formats, audio and video codecs, and subtitle types. A comprehensive (although admittedly incomplete) list of differences between *mpv* and the aforementioned players can be found [here](https://github.com/mpv-player/mpv/blob/master/DOCS/mplayer-changes.rst).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Front ends](#Front_ends)
*   [2 Configuration](#Configuration)
    *   [2.1 General settings](#General_settings)
        *   [2.1.1 High quality configurations](#High_quality_configurations)
        *   [2.1.2 Custom profiles](#Custom_profiles)
    *   [2.2 Key bindings](#Key_bindings)
    *   [2.3 Additional configuration files](#Additional_configuration_files)
*   [3 Scripts](#Scripts)
    *   [3.1 JavaScript](#JavaScript)
    *   [3.2 Lua](#Lua)
        *   [3.2.1 mpv-stats](#mpv-stats)
        *   [3.2.2 mpv-webm](#mpv-webm)
    *   [3.3 C](#C)
        *   [3.3.1 mpv-mpris](#mpv-mpris)
*   [4 Vapoursynth](#Vapoursynth)
    *   [4.1 SVP 4 Linux (SmoothVideoProject)](#SVP_4_Linux_(SmoothVideoProject))
*   [5 Tips and Tricks](#Tips_and_Tricks)
    *   [5.1 Hardware video acceleration](#Hardware_video_acceleration)
    *   [5.2 Save position on quit](#Save_position_on_quit)
    *   [5.3 Volume is too low](#Volume_is_too_low)
    *   [5.4 Play a DVD](#Play_a_DVD)
    *   [5.5 Quickly cycle between aspect ratios](#Quickly_cycle_between_aspect_ratios)
    *   [5.6 Ignoring aspect ratio](#Ignoring_aspect_ratio)
    *   [5.7 Draw to the root window](#Draw_to_the_root_window)
    *   [5.8 Always show application window](#Always_show_application_window)
    *   [5.9 Disable video output](#Disable_video_output)
    *   [5.10 Restoring old OSC](#Restoring_old_OSC)
    *   [5.11 Use as a browser plugin](#Use_as_a_browser_plugin)
    *   [5.12 Improving mpv as a music player with Lua scripts](#Improving_mpv_as_a_music_player_with_Lua_scripts)
    *   [5.13 Twitch.tv streaming over mpv](#Twitch.tv_streaming_over_mpv)
    *   [5.14 youtube-dl and choosing formats](#youtube-dl_and_choosing_formats)
    *   [5.15 youtube-dl audio with search](#youtube-dl_audio_with_search)
    *   [5.16 Creating a single screenshot](#Creating_a_single_screenshot)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 General debugging](#General_debugging)
    *   [6.2 Fix jerky playback and tearing](#Fix_jerky_playback_and_tearing)
    *   [6.3 Problems with window compositors](#Problems_with_window_compositors)
    *   [6.4 No volume bar, cannot change volume](#No_volume_bar,_cannot_change_volume)
    *   [6.5 GNOME Blank screen (Wayland)](#GNOME_Blank_screen_(Wayland))
    *   [6.6 Use mpv with a compositor](#Use_mpv_with_a_compositor)

## Installation

[Install](/index.php/Install "Install") the [mpv](https://www.archlinux.org/packages/?name=mpv) package or [mpv-git](https://aur.archlinux.org/packages/mpv-git/) for the development version.

### Front ends

See [List of applications/Multimedia#mpv-based](/index.php/List_of_applications/Multimedia#mpv-based "List of applications/Multimedia").

## Configuration

*mpv* comes with good all-around defaults that should work well on computers with weaker/older video cards. However, if you have a computer with a more modern video card then *mpv* allows you to do a great deal of configuration to achieve better video quality (limited only by the power of your video card). To do this one only needs to create a few configuration files (they do not exist by default).

**Note:** Configuration files are read system-wide from `/etc/mpv` and per-user from `~/.config/mpv` (unless the [environment variable](/index.php/Environment_variable "Environment variable") `XDG_CONFIG_HOME` is set), where per-user settings override system-wide settings, all of which are overridden by the command line. User specific configuration is suggested since it may require some trial and error.

To help you get started *mpv* provides sample configuration files with default settings. Copy them to use as a starting point:

```
$ cp -r /usr/share/doc/mpv/ ~/.config/

```

`mpv.conf` contains the majority of *mpv'*s settings, `input.conf` contains key bindings. Read through both of them to get an idea of how they work and what options are available.

### General settings

Add the following settings to `~/.config/mpv/mpv.conf`.

#### High quality configurations

This loads high quality OpenGL options when using `vo=gpu` as video output (default). Most users can run these without any problems, but they are not enabled by default to avoid causing problems for the few users who cannot run them:

```
profile=gpu-hq

```

The `gpu-hq` profile defaults to the `spline36` scaling filter for mid quality and speed. For the best quality video output, the manual states that if your hardware can run it, `ewa_lanczossharp` is probably what you should use.

```
profile=gpu-hq
scale=ewa_lanczossharp
cscale=ewa_lanczossharp

```

These last three options are a little more complicated. The first option makes it so that if audio and video go out of sync then instead of dropping video frames it will resample the audio (a slight change in audio pitch is often less noticeable than dropped frames). The mpv wiki has an in depth article on it titled [Display Synchronization](https://github.com/mpv-player/mpv/wiki/Display-synchronization). The remaining two essentially make motion appear smoother on your display by changing the way that frames are shown so that the source framerate jives better with your display's refresh rate (not to be confused with SVP's technique which actually converts video to 60fps). The mpv wiki has an in depth article on it titled [Interpolation](https://github.com/mpv-player/mpv/wiki/Interpolation) though it is also commonly known as *smoothmotion*.

```
profile=gpu-hq
scale=ewa_lanczossharp
cscale=ewa_lanczossharp
video-sync=display-resample
interpolation
tscale=oversample

```

Beyond this there is still a lot you can do but things become more complicated, require more powerful video cards, and are in constant development. As a brief overview, it is possible to load special shaders that perform exotic scaling and sharpening techniques including some that actually use deep neural networks trained on images (for both real world and animated content). To learn more about this take a look around the [mpv wiki](https://github.com/mpv-player/mpv/wiki), particularly the [user shader's section](https://github.com/mpv-player/mpv/wiki/User-Scripts#user-shaders).

There are also plenty of other options you may find desirable as well. It is worthwhile taking a look at [mpv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpv.1). It is also helpful to run *mpv* from the command line to check for error messages about the config.

#### Custom profiles

In `mpv.conf` it is possible to create *profiles* which are essentially just "groups of options" with which you can:

*   Quickly switch between different configurations without having to rewrite the file.
*   Create special profiles for special content.
*   *nest* profiles so that you can make more complicated *profiles* out of simpler ones.

Creating a profile is easy. The area at the top of `mpv.conf` is called the top level, any options you write there will kick into effect once *mpv* is started. However, once you define a profile by writing its name in brackets then every option you write below it (until you define a new profile) is considered part of that profile. Here is an example `mpv.conf`:

```
profile=myprofile2        #Top level area, load myprofile2
ontop=yes                 #Always on top

[myprofile1]              #A simple profile, top level area ends here
profile-desc="a profile"  #Optional description for profile
fs=yes                    #Start in full screen

[myprofile2]              #Another simple profile
profile=gpu-hq            #A built in profile that comes with mpv
log-file=~~/log           #Sets a location for writing a log file, ~~/ translates to ~/.config/mpv

```

There are only two lines within the top level area and there are two separate profiles defined below it. When *mpv* starts it sees the first line, loads the options in `myprofile2` (which means it loads the options in `gpu-hq` and `log-file=~~/log`) finally it loads `ontop=yes` and finishes starting up. Note, `myprofile1` is never loaded because it is never called in the top level area.

Alternatively one could call *mpv* from the command line with:

```
$ mpv --profile=myprofile1 video.mkv

```

and it would ignore all options except the ones for `myprofile1`.

### Key bindings

Key bindings are fairly straightforward given the examples in `/usr/share/doc/mpv/input.conf` and the relevant section in the [manual](https://mpv.io/manual/master/#command-interface).

Add the following examples to `~/.config/mpv/input.conf`:

```
shift+s         screenshot each-frame
Shift+UP        seek  600
Shift+DOWN      seek -600
=               cycle video-unscaled
-               cycle-values window-scale 2 3 1 .5
WHEEL_UP        add volume 5
WHEEL_DOWN      add volume -5
WHEEL_LEFT      ignore
WHEEL_RIGHT     ignore
Alt+RIGHT       add video-rotate 90
Alt+LEFT        add video-rotate -90
Alt+-           add video-zoom -0.25
Alt+=           add video-zoom 0.25
Alt+j           add video-pan-x -0.05
Alt+l           add video-pan-x 0.05
Alt+i           add video-pan-y 0.05
Alt+k           add video-pan-y -0.05
Alt+BS          set video-zoom 0; set video-pan-x 0; set video-pan-y 0

```

For an attempt to reproduce MPC-HC key bindings in mpv, see [[1]](https://github.com/dragons4life/MPC-HC-config-for-MPV/blob/master/input.conf).

### Additional configuration files

In addition there are a few more configuration files and directories that can be created, among which:

*   `~/.config/mpv/script-opts/osc.conf` manages the [On Screen Controller](https://mpv.io/manual/master/#on-screen-controller).
*   `~/.config/mpv/scripts/*script-name*.lua` for Lua scripts. See [[2]](https://github.com/mpv-player/mpv/issues/3500#issuecomment-305646994) for an example.

See [https://mpv.io/manual/master/#files](https://mpv.io/manual/master/#files) for more.

## Scripts

*mpv* has a [large variety of scripts](https://github.com/mpv-player/mpv/wiki/User-Scripts) that extend the functionality of the player. To this end, it has internal bindings for both Lua and JavaScript (added recently).

Scripts are typically installed by putting them in the `~/.config/mpv/scripts/` directory (you may have to create it first). After that they will be automatically loaded when mpv starts (this behavior can be altered with other *mpv* options). Some scripts come with their own installation and configuration instructions, so make sure to have a look. In addition some scripts are old, broken, and unmaintained.

### JavaScript

Since JavaScript support is still fairly new, there is currently very little in the way of scripts, but [documentation exists](https://mpv.io/manual/master/#javascript) for anyone interested in making their own.

JavaScript support is not available in the [mpv](https://www.archlinux.org/packages/?name=mpv) build, but it is supported by some AUR packages e.g. [mpv-full](https://aur.archlinux.org/packages/mpv-full/) and [mpv-full-git](https://aur.archlinux.org/packages/mpv-full-git/).

### Lua

There are a lot of interesting Lua scripts for mpv. If you would like to make your own, the relevant documentation may be found [here](https://github.com/mpv-player/mpv/blob/master/DOCS/man/lua.rst).

#### mpv-stats

[mpv-stats](https://github.com/Argon-/mpv-stats/) (or simply *stats*) is a Lua script that outputs a lot of live statistics showing how well *mpv* is currently doing. It is very useful for making sure that your hardware can keep up with your configuration and for comparing different configurations. Since version [v0.28.0](https://github.com/mpv-player/mpv/releases/tag/v0.28.0), the script is built into [mpv](https://www.archlinux.org/packages/?name=mpv) and can be toggled on or off with the `i` or `I` keys (by default).

#### mpv-webm

[mpv-webm](https://github.com/ElegantMonkey/mpv-webm) (or simply *webm*) is a very easy to use Lua script that allows one to create WebM files while watching videos. It includes several features and does not have any extra dependencies (relies entirely on mpv).

### C

#### mpv-mpris

The C plugin [mpv-mpris](https://github.com/hoyon/mpv-mpris) allows other applications to integrate with *mpv* via the MPRIS protocol. For example, with mpv-mpris installed, [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) can automatically pause video playback in *mpv* when a phone call arrives.

Install [mpv-mpris](https://aur.archlinux.org/packages/mpv-mpris/) and follow the post-installation instructions displayed by Pacman.

## Vapoursynth

Vapoursynth is an alternative to AviSynth that can be used on Linux and allows for Video manipulation via python scripts. Vapoursynths python scripts can be used as video filters for *mpv*.

To use vapoursynth filters you have to install the [vapoursynth](https://www.archlinux.org/packages/?name=vapoursynth) package (or [vapoursynth-git](https://aur.archlinux.org/packages/vapoursynth-git/)) and compile *mpv* with the `--enable-vapoursynth` build flag.

This is easier to do by first installing Vapoursynth and then installing (or re-installing if it is already installed) [mpv-git](https://aur.archlinux.org/packages/mpv-git/). The configure script for [mpv-git](https://aur.archlinux.org/packages/mpv-git/) will auto-detect Vapoursynth (as long as it has already been installed) and it will automatically compile *mpv* with support for Vapoursynth without having to manually change any configure options or anything (this makes it very easy to update *mpv* as well).

### SVP 4 Linux (SmoothVideoProject)

[SmoothVideoProject SVP](https://www.svp-team.com/wiki/Main_Page) is a program that is primarily known for converting video to 60fps. It is free [as in beer] and full featured for 64bit Linux (costs money for Windows and OS X and is incompatible with 32bit Linux).

It has three main features and each one can be disabled/enabled as one chooses (you are not forced to use motion interpolation).

1.  [Motion interpolation](https://www.svp-team.com/wiki/Manual:FRC) ([youtube video](https://www.youtube.com/watch?v=Wjb6CSe4708)) - An algorithm that converts video to 60fps. This creates the somewhat controversial "soap opera effect" that some people love and others hate. Unfortunately the algorithm is not perfect and it also introduces more than its share of weird artifacts. The algorithm can be tuned (via a slider) for either performance or quality. It also has some artifact reduction settings that interpolate actual frames with the generated frames reducing the noticeability of the artifacts. The framerate detection can be set to automatic or manual (manual seems to resolve performance issues for some users).
2.  [Black bar lighting](https://www.svp-team.com/wiki/Manual:Outer_lighting) ([youtube video](https://www.youtube.com/watch?v=yTzTpW3kTBE)) - If the image has an aspect ratio that produces black bars on your display then SVP will illuminate the black bars with "lights" generated by the content on the screen. It has some amount of customization but the defaults are pretty close to optimal.
3.  [LED ambient lighting control](https://www.svp-team.com/wiki/Manual:SVPlight) ([youtube video](https://www.youtube.com/watch?v=UUM2n-8kIJ8)) - Has the ability to control LED ambient lighting attached to your television.

Once you have *mpv* compiled with Vapoursynth support it is fairly easy to get SVP working with *mpv*. Simply install [svp](https://aur.archlinux.org/packages/svp/), open the SVP program to let it assess your system performance (you may want to close other programs first so that it gets an accurate reading), and finally add the following *mpv* profile to your mpv.conf[[3]](https://www.svp-team.com/wiki/SVP:mpv):

 `mpv.conf` 
```
[svp]
input-ipc-server=/tmp/mpvsocket     # Receives input from SVP
hr-seek-framedrop=no                # Fixes audio desync
resume-playback=no                  # Not compatible with SVP

# Can fix stuttering in some cases, in other cases probably causes it. Try it if you experience stuttering.
#opengl-early-flush=yes
```

Then, in order to use SVP you must have the SVP program running in the background before opening the file using *mpv* with that profile. Either do:

```
$ mpv --profile=svp video.mkv

```

or set `profile=svp` in the top-level portion of the *mpv* [configuration](#Custom_profiles).

If you want to use hardware decoding then you must use a copy-back decoder since normal decoders are not compatible with Vapoursynth (choose a `hwdec` option that ends in `-copy`). For instance:

```
hwdec=auto-copy
hwdec-codecs=all

```

Either way, hardware decoding is discouraged by *mpv* developers and is not likely to make a significant difference in performance.

## Tips and Tricks

### Hardware video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

Hardware accelerated video decoding is available via `--hwdec=*API*` option. For list of all supported APIs and other required options see [relevant manual section](https://mpv.io/manual/stable/#options-hwdec).

Newer versions of mpv try to use `cuda`/`nvdec` as the API of choice for hardware acceleration on [NVIDIA](/index.php/NVIDIA "NVIDIA") cards when `--hwdec=auto`. If that method does not work for your card and you have a dual-GPU system, meaning that you cannot just set `--hwdec=vdpau`, you can make mpv fall back to `vdpau` by faking the cuda device: Set `cuda-decode-device=*value*` where `*value*` is the wrong index number for the card. (in most systems the correct number will be 0), e.g. `--cuda-decode-device=999`. See [mpv issue 6777](https://github.com/mpv-player/mpv/issues/6777).

For [Wayland](/index.php/Wayland "Wayland") use `--gpu-context=wayland` option. For list of other available GPU APIs see [manual](https://mpv.io/manual/stable/#options-gpu-context).

### Save position on quit

By default you can save the position and quit by pressing `Shift+q`. The shortcut can be changed by setting `quit_watch_later` in the key bindings configuration file.

To automatically save the current playback position on quit, start *mpv* with `--save-position-on-quit`, or add `save-position-on-quit` to the configuration file.

### Volume is too low

Set `volume-max=*value*` in your configuration file to a reasonable amount, such as `volume-max=150`, which then allows you to increase your volume up to 150%, which is more than twice as loud. Increasing your volume too high will result in clipping artefacts. Additionally (or alternatively), you can utilize [dynamic range compression](https://en.wikipedia.org/wiki/Dynamic_range_compression "wikipedia:Dynamic range compression") with `af=acompressor`.

### Play a DVD

To start the main stream of a video DVD, use the command:

```
$ mpv dvd://

```

Install [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss), to fix the error:

```
[dvdnav] Error getting next block from DVD 1 (Error reading from DVD.)

```

### Quickly cycle between aspect ratios

You can cycle between aspect ratios using `Shift+a`.

### Ignoring aspect ratio

You can ignore aspect ratio using `--keepaspect=*no*`. To make option permanent, add line `keepaspect=*no*` to configuration file.

### Draw to the root window

Run *mpv* with `--wid=0`. *mpv* will draw to the window with a window ID of 0.

### Always show application window

To show application window even for audio files when launching mpv from command line use `--force-window` option.

### Disable video output

To disable video output when launching from command line use `--vid=no` option, or its alias, `--no-video`.

### Restoring old OSC

Since version 0.21.0, *mpv* has replaced the on-screen controls by a bottombar. In case you want on-screen controls back, you can edit the *mpv* configuration [as described here](https://github.com/mpv-player/mpv/wiki/FAQ#i-want-the-old-osc-back).

### Use as a browser plugin

With the help of [mozplugger](https://aur.archlinux.org/packages/mozplugger/), *mpv* can be used in a supported browser to play video. See [Browser plugins#MozPlugger](/index.php/Browser_plugins#MozPlugger "Browser plugins") for configuration details. This coupled with a user script such as [ViewTube](http://isebaro.com/viewtube/?ln=en), allows you to use *mpv* in place of a site's integrated video player.

It may be needed to specify a valid user agent for HTTP streaming, e.g. `user-agent="Mozilla/5.0 (X11; Linux x86_64; rv:49.0) Gecko/20100101 Firefox/49.0"`.

[Browser plugins#Multimedia playback](/index.php/Browser_plugins#Multimedia_playback "Browser plugins") page shows other easy ways to watch videos.

### Improving mpv as a music player with Lua scripts

The development of *mpv'*s Lua scripts are documented in [DOCS/man/lua.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/lua.rst) and examples are shown in [TOOLS/lua](https://github.com/mpv-player/mpv/tree/master/TOOLS/lua) of the [mpv repository](https://github.com/mpv-player/mpv). [This blog post](https://web.archive.org/web/20160320001546/http://bamos.github.io/2014/07/05/mpv-lua-scripting/) introduces the [music.lua](https://github.com/bamos/dotfiles/blob/master/.mpv/scripts/music.lua) script, which shows how Lua scripts can be used to improve *mpv* as a music player.

### Twitch.tv streaming over mpv

If [youtube-dl](/index.php/Youtube-dl "Youtube-dl") is installed, *mpv* can directly open a Twitch livestream.

Alternatively, see [Streamlink#Twitch](/index.php/Streamlink#Twitch "Streamlink").

Another alternative based on Livestreamer is this Lua script: [https://gist.github.com/ChrisK2/8701184fe3ea7701c9cc](https://gist.github.com/ChrisK2/8701184fe3ea7701c9cc)

### youtube-dl and choosing formats

The default `--ytdl-format` is `bestvideo+bestaudio/best`. For youtube videos that have 4K resolutions available, this may mean that your device will struggle to decode 4K VP9 encoded video in software even if the attached monitor is much lower resolution.

Setting the right youtube-dl format selectors can fix this easily though. In the following configuration example, only videos with a vertical resolution of 1080 pixels or less will be considered.

```
ytdl-format="bestvideo[height<=?1080]+bestaudio/best"

```

If you wish to avoid a certain codec altogether because you cannot hardware-decode it, you can add this to the format selector. For example, we can additionally choose to ignore VP9 as follows:

```
ytdl-format="bestvideo[height<=?1080][vcodec!=vp9]+bestaudio/best"

```

If you prefer best quality open codecs (VP9 and Opus), use:

```
ytdl-format="((bestvideo[vcodec^=vp9]/bestvideo)+(bestaudio[acodec=opus]/bestaudio[acodec=vorbis]/bestaudio[acodec=aac]/bestaudio))/best"

```

### youtube-dl audio with search

To find and stream audio from your terminal emulator with `yta *search terms*` put the following function in your `.bashrc`:

```
function yta() {
    mpv --ytdl-format=bestaudio ytdl://ytsearch:"$*"
}

```

### Creating a single screenshot

An example of creating a single screenshot, by using a start time (`HH:MM:SS`):

```
$ mpv --no-audio --start=00:01:30 --frames=1 /path/to/video/file --o=/path/to/screenshot.png

```

Screenshots will be saved in /path/to/screenshot.png.

## Troubleshooting

### General debugging

If you are having trouble with *mpv'*s playback (or if it is flat out failing to run) then the first three things you should do are:

1.  Run *mpv* from the command line (the -v flag increases verbosity). If you are lucky there will be an error message there telling you what is wrong.
    `$ mpv -v video.mkv`
2.  Have *mpv* output a log file. The log file might be difficult to sift through but if something is broken you might see it there.
    `$ mpv -v --log-file=./log video.mkv`
3.  Run *mpv* without a configuration. If this runs well then the problem is somewhere in your configuration (perhaps your hardware cannot keep up with your settings).
    `$ mpv --no-config video.mkv`

If *mpv* runs but it just does not run well then a fourth thing that might be worth taking a look at is installing the [mpv-stats](#mpv-stats) script and using it to see exactly how it is performing.

### Fix jerky playback and tearing

*mpv* defaults to using the OpenGL video output device setting on hardware that supports it. In cases such as trying to play video back on a 4K display using a Intel HD4XXX series card or similar, you will find video playback unreliable, jerky to the point of stopping entirely at times and with major tearing when using any OpenGL output setting. If you experience any of these issues, using the XV ([Xorg](/index.php/Xorg "Xorg") only) video output device may help:

 `~/.config/mpv/mpv.conf`  `vo=xv` 
**Note:** This is the most compatible VO on X, but may be low-quality, and has issues with OSD and subtitle display.

It is possible to increase playback performance even more (especially on lower hardware), but this decreases the video quality dramatically in most cases.

The following [options](#Configuration) may be considered to increase the video playback performance:

 `~/.config/mpv/mpv.conf` 
```
vd-lavc-fast
vd-lavc-skiploopfilter=<skipvalue>
vd-lavc-skipframe=<skipvalue>
vd-lavc-framedrop=<skipvalue>
vd-lavc-threads=<threads>
```

### Problems with window compositors

Window compositors such as KWin or Mutter can cause trouble for playback smoothness. In such cases, it may help to set `x11-bypass-compositor=yes` to make *mpv* also disable window compositing when playing in windowed mode (if supported by the compositor).

With KWin compositing and hardware decoding, you may also want to set `x11-bypass-compositor=no` to keep compositing enabled in fullscreen, since reanabling compositing after leaving fullscreen may introduce stutter for a period of time.

### No volume bar, cannot change volume

Spin the mouse wheel over the volume icon.

### GNOME Blank screen (Wayland)

*mpv* may not suspend GNOME's Power Saving Settings if using Wayland resulting in screen saver turning off the monitor during video playback. A workaround is to add `gnome-session-inhibit` to the beginning of the `Exec=` line in `mpv.desktop`.

### Use mpv with a compositor

If you are using a compositor (e.g. in KDE Plasma 5) and find that composition is disabled (e.g. in Plasma this would make you unable to present windows or see window thumbnails in the default app switcher) when *mpv* is playing a video, try `x11-bypass-compositor=no`