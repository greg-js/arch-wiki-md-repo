Related articles

*   [List of games](/index.php/List_of_games "List of games")
*   [Video game platform emulators](/index.php/Video_game_platform_emulators "Video game platform emulators")
*   [Xorg](/index.php/Xorg "Xorg")

This page contains information about running games and related system configuration tips.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Game environments](#Game_environments)
*   [2 Getting games](#Getting_games)
    *   [2.1 Digital distribution](#Digital_distribution)
*   [3 Running games](#Running_games)
    *   [3.1 Multi-screen setups](#Multi-screen_setups)
    *   [3.2 Keyboard grabbing](#Keyboard_grabbing)
    *   [3.3 Starting games in a separate X server](#Starting_games_in_a_separate_X_server)
    *   [3.4 Adjusting mouse detections](#Adjusting_mouse_detections)
    *   [3.5 Mouse focus in GNOME](#Mouse_focus_in_GNOME)
    *   [3.6 Binaural Audio with OpenAL](#Binaural_Audio_with_OpenAL)
    *   [3.7 Tuning PulseAudio](#Tuning_PulseAudio)
        *   [3.7.1 Enabling realtime priority and negative nice level](#Enabling_realtime_priority_and_negative_nice_level)
        *   [3.7.2 Using higher quality remixing for better sound](#Using_higher_quality_remixing_for_better_sound)
        *   [3.7.3 Matching hardware buffers to Pulse's buffering](#Matching_hardware_buffers_to_Pulse's_buffering)
    *   [3.8 Double check your CPU frequency scaling settings](#Double_check_your_CPU_frequency_scaling_settings)
*   [4 Remote gaming](#Remote_gaming)
*   [5 Improving performance](#Improving_performance)
    *   [5.1 Improving frame rates and responsiveness with scheduling policies](#Improving_frame_rates_and_responsiveness_with_scheduling_policies)
        *   [5.1.1 Policies](#Policies)
        *   [5.1.2 Nice levels](#Nice_levels)
        *   [5.1.3 Core affinity](#Core_affinity)
        *   [5.1.4 General case](#General_case)
        *   [5.1.5 Optimus, and other helping programs](#Optimus,_and_other_helping_programs)

## Game environments

Different environments exist to play games in Linux:

*   Native – games written for Linux.
*   Web – games running in a web browser
    *   HTML5 games use canvas and WebGL technologies and work in all modern browsers
    *   [Flash](/index.php/Flash "Flash")-based – you need to install the plugin to play.
*   Specialized environments (software emulators) – Required for running software designed for other architectures or systems. See [Video game platform emulators](/index.php/Video_game_platform_emulators "Video game platform emulators") for more details.
    *   [Wine](/index.php/Wine "Wine") – allows running of some Windows games, as well as a large amount of Windows software. Performance in Wine varies, the additional CPU overhead will cause slowdown in some games while in some cases games may run faster. Consult [Wine AppDB](http://appdb.winehq.org/) for game-specific compatibility information.
    *   [Crossover Games](http://www.codeweavers.com/) – members of the Codeweavers team are prime supporters of Wine. Using Crossover Games makes the installation & setting up of some games easier, more reliable & even possible, when compared to using other methods. Crossover is a paid commercial product, which also provides a [forum](http://www.codeweavers.com/support/forums/) where the developers are very much involved in the community.
    *   [DOSBox](/index.php/DOSBox "DOSBox") is a minimal virtual machine which runs a full DOS-compatible environment. It can be used to run classic DOS titles.
    *   [scummvm](https://www.archlinux.org/packages/?name=scummvm) is an all-in-one engine reimplementation of many classic point-and-click adventure games. A full list of compatible titles can be found on the [ScummVM website](http://scummvm.org).
    *   Similar to ScummVM, engine reimplementations and ports exist for specific titles, such as Doom.
*   Virtual machines can be used to install compatible operating systems (such as Windows). [VirtualBox](/index.php/VirtualBox "VirtualBox") has good 3D support. As an extension of this, if you have compatible hardware you can consider VGA passthrough to a Windows KVM guest, keyword is ["virtual function I/O" (VFIO)](https://www.kernel.org/doc/Documentation/vfio.txt), or [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF").

## Getting games

A good number are available in the [official repositories](/index.php/Official_repositories "Official repositories") / the [AUR](/index.php/AUR "AUR"), see [List of games](/index.php/List_of_games "List of games").

### Digital distribution

Just because games are available for Linux doesn't mean that they are native, they might be pre-packaged with Wine or DOSBox.

*   **[Steam](/index.php/Steam "Steam")** — Digital distribution and communications platform developed by Valve.

	[https://store.steampowered.com](https://store.steampowered.com) || [steam](https://www.archlinux.org/packages/?name=steam)

*   **[itch.io](https://en.wikipedia.org/wiki/itch.io "wikipedia:itch.io")** — Indie game store.

	[https://itch.io/](https://itch.io/) || [itch](https://aur.archlinux.org/packages/itch/)

*   [GOG.com](https://www.gog.com/games/linux)
    *   GOG.com officially only supports Ubuntu and Linux Mint.
    *   The [lgogdownloader](https://aur.archlinux.org/packages/lgogdownloader/) package can be used to download GOG titles from the command line.

## Running games

Certain games or game types may need special configuration to run or to run as expected. For the most part, games will work right out of the box in Arch Linux with possibly better performance than on other distributions due to compile time optimizations. However, some special setups may require a bit of configuration or scripting to make games run as smoothly as desired.

### Multi-screen setups

Running a multi-screen setup may lead to problems with fullscreen games. In such a case, [running a second X server](#Starting_games_in_a_separate_X_server) is one possible solution. Another solution may be found in the [NVIDIA article](/index.php/NVIDIA#Gaming_using_TwinView "NVIDIA") (may also apply to non-NVIDIA users).

### Keyboard grabbing

Many games grab the keyboard, noticeably preventing you from switching windows (also known as alt-tabbing).

Some SDL games (e.g. Guacamelee) let you disable grabbing by pressing `Ctrl-g`.

To disable keyboard grabbing at X11 level, install the [libx11-nokeyboardgrab](https://aur.archlinux.org/packages/libx11-nokeyboardgrab/) package.

**Note:** SDL is known to sometimes not be able to grab the input system. In such a case, it may succeed in grabbing it after a few seconds of waiting.

### Starting games in a separate X server

In some cases like those mentioned above, it may be necessary or desired to run a second X server. Running a second X server has multiple advantages such as better performance, the ability to "tab" out of your game by using `Ctrl+Alt+F7`/`Ctrl+Alt+F8`, no crashing your primary X session (which may have open work on) in case a game conflicts with the graphics driver. The new X server will be akin a remote access login for the ALSA, so your user need to be part of the `audio` group to be able to hear any sound.

To start a second X server (using the free first person shooter game [Xonotic](http://www.xonotic.org/) as an example) you can simply do:

```
$ xinit /usr/bin/xonotic-glx -- :1 vt$XDG_VTNR

```

This can further be spiced up by using a separate X configuration file:

```
$ xinit /usr/bin/xonotic-glx -- :1 -xf86config xorg-game.conf vt$XDG_VTNR

```

A good reason to provide an alternative *xorg.conf* here may be that your primary configuration makes use of NVIDIA's Twinview which would render your 3D games like Xonotic in the middle of your multiscreen setup, spanned across all screens. This is undesirable, thus starting a second X with an alternative config where the second screen is disabled is advised.

A game starting script making use of Openbox for your home directory or `/usr/local/bin` may look like this:

 `~/game.sh` 
```
if [ $# -ge 1 ]; then
        game="$(which $1)"
        openbox="$(which openbox)"
        tmpgame="/tmp/tmpgame.sh"
        DISPLAY=:1.0
        echo -e "${openbox} &
${game}" > ${tmpgame}
        echo "starting ${game}"
        xinit ${tmpgame} -- :1 -xf86config xorg-game.conf || exit 1
else
        echo "not a valid argument"
fi

```

So after a `chmod +x` you would be able to use this script like:

```
$ ~/game.sh xonotic-glx

```

### Adjusting mouse detections

For games that require exceptional amount of mouse skill, adjusting the [mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate") can help improve accuracy.

### Mouse focus in GNOME

The 'sloppy' and 'mouse' window-focusing modes in [GNOME](/index.php/GNOME "GNOME") are known to cause issues with a variety of games, causing a 'click-through' effect. Users can remedy this problem by switching the focus mode to 'click' (with a tool such as [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)), playing in a different desktop environment, or spawing their game in a separate X-session.

### Binaural Audio with OpenAL

For games using [OpenAL](https://en.wikipedia.org/wiki/OpenAL "wikipedia:OpenAL"), if you use headphones you may get much better positional audio using OpenAL's [HRTF](https://en.wikipedia.org/wiki/Head-related_transfer_function "wikipedia:Head-related transfer function") filters. To enable, run the following command:

```
echo "hrtf = true" >> ~/.alsoftrc

```

Alternatively, install [openal-hrtf](https://aur.archlinux.org/packages/openal-hrtf/) from the AUR, and edit the options in /etc/openal/alsoftrc.conf

For Source games, the ingame setting `dsp_slow_cpu` must be set to `1` to enable HRTF, otherwise the game will enable its own processing instead. You will also either need to set up Steam to use native runtime, or link its copy of openal.so to your own local copy. For completeness, also use the following options:

```
dsp_slow_cpu 1 # Disable in-game spatialiazation
snd_spatialize_roundrobin 1 # Disable spatialization 1.0*100% of sounds
dsp_enhance_stereo 0 # Disable DSP sound effects. You may want to leave this on, if you find it does not interfere with your perception of the sound effects.
snd_pitchquality 1 # Use high quality sounds

```

### Tuning PulseAudio

If you are using [PulseAudio](/index.php/PulseAudio "PulseAudio"), you may wish to tweak some default settings to make sure it is running optimally.

#### Enabling realtime priority and negative nice level

Pulseaudio is built to be run with realtime priority, being an audio daemon. However, because of security risks of it locking up the system, it is scheduled as a regular thread by default. To adjust this, first make sure you are in the `audio` group. Then, uncomment and edit the following lines in `/etc/pulse/daemon.conf`:

 `/etc/pulse/daemon.conf` 
```
high-priority = yes
nice-level = -11

realtime-scheduling = yes
realtime-priority = 5
```

and restart pulseaudio.

#### Using higher quality remixing for better sound

PulseAudio on Arch uses speex-float-0 by default to remix channels, which is considered a 'medium-low' quality remixing. If your system can handle the extra load, you may benefit from setting it to one of the following instead:

```
resample-method = speex-float-10

```

#### Matching hardware buffers to Pulse's buffering

Matching the buffers can reduce stuttering and increase performance marginally. See [here](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862) for more details.

### Double check your CPU frequency scaling settings

If your system is currently configured to properly insert its own cpu frequency scaling driver, the system sets the default governor to Ondemand. By default, this governor only adjusts the clock if the system is utilizing 95% of its CPU, and then only for a very short period of time. This saves power and reduces heat, but has a noticeable impact on performance. You can instead only have the system downclock when it is idle, by tuning the system governor. To do so, see [Cpufrequtils#Tuning the ondemand governor](/index.php/Cpufrequtils#Tuning_the_ondemand_governor "Cpufrequtils").

## Remote gaming

[Cloud gaming](https://en.wikipedia.org/wiki/Cloud_gaming "wikipedia:Cloud gaming") has gained a lot of popularity in the last few years, because of low client-side hardware requirements. The only important thing is stable internet connection (over the ethernet cable or 5 GHz WiFi recommended) with a minimum speed of 5–10 Mbit/s (depending on the video quality and framerate).

*   [Steam In-Home](/index.php/Steam#In-home_streaming "Steam") — Remotely play games on the LAN from host machine. Some users managed to get it working over the VPN.
*   [Parsec](https://ui.parsecgaming.com/) — Remotely play games either from your Windows host machine or rented (within an app) Windows cloud machine. It prioritizes direct connection to the host (great for VPN connections) and if it's not available, then connects via Parsec's servers. Can be installed as [parsec-bin](https://aur.archlinux.org/packages/parsec-bin/).
*   [LiquidSky](https://liquidsky.com/) — Remotely play games from rented (within an app) Windows cloud machine. Can be installed as [liquidsky](https://aur.archlinux.org/packages/liquidsky/).
*   [Shadow](https://shadow.tech/) — Remotely play games from rented (within an app) Windows cloud machine. Can be installed as [shadow-beta](https://aur.archlinux.org/packages/shadow-beta/).
*   [Vortex](https://vortex.gg/) — Remotely play games from their servers. No installation or configuration is required. Works in browser.
*   [Rainway](https://rainway.com/) — Remotely play games from your Windows host machine. Works in browser (Linux client is coming at around 2019 Q3).
*   [Moonlight](https://moonlight-stream.org/) — Remotely play games from your Windows host machine with Nvidia GPU. Can be installed as [moonlight](https://aur.archlinux.org/packages/moonlight/).
*   [Dixper](https://dixper.gg/) — Remotely play games from your Windows host machine. Works in browser.

Also there are other services where users have reported success getting it to work under Linux (via [Wine](/index.php/Wine "Wine") or [Steam](/index.php/Steam "Steam")'s proton):

*   [PS Now](https://www.playstation.com/en-gb/explore/playstation-now/ps-now-on-pc/) — Play PS4, PS3 and PS2 games on PC. Alternatively, you can use emulators (see [Video_game_platform_emulators](/index.php/Video_game_platform_emulators "Video game platform emulators")).
*   [PLAYKEY](https://playkey.net/) — Yet another cloud gaming service.

## Improving performance

See also main article: [Improving performance](/index.php/Improving_performance "Improving performance"). For Wine programs, see [Wine#Performance](/index.php/Wine#Performance "Wine").

### Improving frame rates and responsiveness with scheduling policies

Most games can benefit if given the correct scheduling policies for the kernel to prioritize the task. These policies should ideally be set per-thread by the application itself.

For programs which do not implement scheduling policies on their own, application known as [schedtool](https://www.archlinux.org/packages/?name=schedtool), and its associated daemon [schedtoold](https://aur.archlinux.org/packages/schedtoold/) can handle many of these tasks automatically.

To edit what programs relieve what policies, simply edit `/etc/schedtoold.conf` and add the program followed by the *schedtool* arguments desired.

#### Policies

`SCHED_ISO` (only implemented in BFS/MuQSSPDS schedulers found in -pf and -ck [kernels](/index.php/Kernel "Kernel")) – will not only allow the process to use a maximum of 80 percent of the CPU, but will attempt to reduce latency and stuttering wherever possible. Most if not all games will benefit from this:

```
bit.trip.runner -I

```

`SCHED_FIFO` provides an alternative, that can even work better. You should test to see if your applications run more smoothly with `SCHED_FIFO`, in which case by all means use it instead. Be warned though, as `SCHED_FIFO` runs the risk of starving the system! Use this in cases where -I is used below:

```
bit.trip.runner -F -p 15

```

#### Nice levels

Secondly, the nice level sets which tasks are processed first, in ascending order. A nice level of -4 is reccommended for most multimedia tasks, including games:

```
bit.trip.runner -n -4

```

#### Core affinity

There is some confusion in development as to whether the driver should be multithreading, or the program. In any case where they both attempt it, it causes drops in framerate and crashes. Examples of this include a number of modern games, and any Wine program which is running with [GLSL](https://en.wikipedia.org/wiki/OpenGL_Shading_Language "wikipedia:OpenGL Shading Language") enabled. To select a single core and allow only the driver to handle this process, simply use the `-a 0x*#*` flag, where *#* is the core number, e.g.:

```
bit.trip.runner -a 0x1

```

uses first core.

Some CPUs are hyperthreaded and have only 2 or 4 cores but show up as 4 or 8, and are best accounted for:

```
bit.trip.runner -a 0x5

```

which use virtual cores 0101, or 1 and 3.

#### General case

For most games which require high framerates and low latency, usage of all of these flags seems to work best. Affinity should be checked per-program, however, as most native games can understand the correct usage. For a general case:

```
bit.trip.runner -I -n -4
Amnesia.bin64 -I -n -4
hl2.exe -I -n -4 -a 0x1 #Wine with GLSL enabled

```

etc.

#### Optimus, and other helping programs

As a general rule, any other process which the game requires to operate should be reniced to a level above that of the game itself. Strangely, Wine has a problem known as *reverse scheduling*, it can often have benefits when the more important processes are set to a higher nice level. Wineserver also seems unconditionally to benefit from `SCHED_FIFO`, since rarely consumes the whole CPU and needs higher prioritization when possible.

```
optirun -I -n -5
wineserver -F -p 20 -n 19
steam.exe -I -n -5

```