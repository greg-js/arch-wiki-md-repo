This page only contains information about running games and related system configuration tips. For lists of popular games for GNU/Linux see [List of games](/index.php/List_of_games "List of games").

## Contents

*   [1 Game environments](#Game_environments)
*   [2 Getting games](#Getting_games)
    *   [2.1 Native](#Native)
    *   [2.2 Digital distribution](#Digital_distribution)
    *   [2.3 Flash](#Flash)
    *   [2.4 Java](#Java)
    *   [2.5 Wine](#Wine)
*   [3 Running games](#Running_games)
    *   [3.1 Multi-screen setups](#Multi-screen_setups)
    *   [3.2 Keyboard grabbing](#Keyboard_grabbing)
    *   [3.3 Starting games in a separate X server](#Starting_games_in_a_separate_X_server)
    *   [3.4 Adjusting mouse detections](#Adjusting_mouse_detections)
    *   [3.5 Mouse focus in GNOME](#Mouse_focus_in_GNOME)
    *   [3.6 Binaural Audio with OpenAL](#Binaural_Audio_with_OpenAL)
    *   [3.7 Tuning Pulseaudio](#Tuning_Pulseaudio)
        *   [3.7.1 Enabling realtime priority and negative nice level](#Enabling_realtime_priority_and_negative_nice_level)
        *   [3.7.2 Using higher quality remixing for better sound](#Using_higher_quality_remixing_for_better_sound)
        *   [3.7.3 Matching hardware buffers to Pulse's buffering](#Matching_hardware_buffers_to_Pulse.27s_buffering)
    *   [3.8 Double check your CPU frequency scaling settings](#Double_check_your_CPU_frequency_scaling_settings)
*   [4 Improving framerates and responsiveness with scheduling policies](#Improving_framerates_and_responsiveness_with_scheduling_policies)
    *   [4.1 For Wine programs](#For_Wine_programs)
    *   [4.2 For everything else](#For_everything_else)
        *   [4.2.1 Policies](#Policies)
        *   [4.2.2 Nice levels](#Nice_levels)
        *   [4.2.3 Core affinity](#Core_affinity)
        *   [4.2.4 General case](#General_case)
        *   [4.2.5 Optimus, and other helping programs](#Optimus.2C_and_other_helping_programs)
*   [5 Using alternate kernels](#Using_alternate_kernels)
    *   [5.1 Using BFQ](#Using_BFQ)
*   [6 See also](#See_also)

## Game environments

Different environments exist to play games in Linux:

*   Native – Games written for Linux.
*   Browser – you need only browser and Internet connection to play these types of games.
    *   HTML5 games use canvas and WebGL technologies and work in all modern browsers but can be slow on weak machines.
    *   Plugin-based – you need to install plugin to play.
        *   [Java](/index.php/Java "Java") Webstart – used to install cross-platform games very easily.
        *   [Flash](/index.php/Flash "Flash") games are very common on the Web.
*   Specialized environments (software emulators) – – Required for running software designed for other architectures or systems, (Heed the copyright laws of your country!). Check the [list of emulators](/index.php/List_of_applications/Other#Emulators "List of applications/Other") for more details.
    *   [Wine](/index.php/Wine "Wine") – allows running of some Windows games, as well as a large amount of Windows software. Performance in Wine varies, the additional CPU overhead will cause slowdown in some games while in some cases games may run faster. Consult [Wine AppDB](http://appdb.winehq.org/) for game-specific compatibility information.
    *   [Crossover Games](http://www.codeweavers.com/) – members of the Codeweavers team are prime supporters of Wine. Using Crossover Games makes the installation & setting up of some games easier, more reliable & even possible, when compared to using other methods. Crossover is a paid commercial product, which also provides a [forum](http://www.codeweavers.com/support/forums/) where the developers are very much involved in the community.
    *   [DOSBox](/index.php/DOSBox "DOSBox") is a minimal virtual machine which runs a full DOS-compatible environment. It can be used to run classic DOS titles.
    *   [scummvm](https://www.archlinux.org/packages/?name=scummvm) is an all-in-one engine reimplementation of many classic point-and-click adventure games. A full list of compatible titles can be found on the [ScummVM website](http://scummvm.org).
    *   Similar to ScummVM, engine reimplementations exist for specific titles, such as Doom.
*   Virtual machines can be used to install compatible operating systems (such as Windows). [VirtualBox](/index.php/VirtualBox "VirtualBox") has good 3D support. As an extension of this, if you have compatible hardware you can consider VGA passthrough to a Windows KVM guest.

## Getting games

### Native

A good number are available in the [official repositories](/index.php/Official_repositories "Official repositories") or in the [AUR](/index.php/AUR "AUR"). [Loki](http://liflg.org/) provides installers for several games.

### Digital distribution

*   **[Desura](https://en.wikipedia.org/wiki/Desura "wikipedia:Desura")** — Digital distribution platform featuring indie games. It can be considered good source of games (if you do not care about security and bugs too much).

	[http://www.desura.com/](http://www.desura.com/) || [desura](https://aur.archlinux.org/packages/desura/)

*   **[Steam](/index.php/Steam "Steam")** — Famous digital distribution and communications platform developed by Valve. It has a large library with over 1000 Linux games. These include popular titles like Dota 2, Counter Strike: Global Offensive, Team Fortress 2, several AAA games, and lots of indie titles.

	[http://store.steampowered.com](http://store.steampowered.com) || [steam](https://www.archlinux.org/packages/?name=steam)

*   [Steam under Linux.](http://developer.valvesoftware.com/wiki/Steam_under_Linux)
*   [See linux-games catalog.](http://store.steampowered.com/browse/linux/)
*   Not all Steam titles are native, some are packaged to run using Wine.

*   The [Humble Store](https://www.humblebundle.com/store)

*   [itch.io](https://itch.io/)|[itch](https://aur.archlinux.org/packages/itch/)

*   [GOG.com](http://www.gog.com/games/linux)

*   The [lgogdownloader](https://aur.archlinux.org/packages/lgogdownloader/) package can be used to download GOG titles from the command line.
*   GOG.com only officially supports Ubuntu and Linux Mint. Bear this in mind if requesting support from them; you will not get a refund if you are having trouble running games on Arch.
*   Many GOG.com titles come pre-packaged with DOSBox, ScummVM or Wine.

### Flash

**Note:** The official Adobe Flash Player for Linux with NPAPI-based browsers is stuck at major version 11, whereas the current (as of August 25, 2015) major version is 18\. An up-to-date Adobe Flash Player is, however, obtainable on Linux with PPAPI-based browsers. Please see [wikipedia:Adobe Flash Player#Desktop platforms](https://en.wikipedia.org/wiki/Adobe_Flash_Player#Desktop_platforms "wikipedia:Adobe Flash Player") for more info. If you do not wish to install Chrome, however, there is an even more potent option to use the Windows version of Flash; see [http://community.linuxmint.com/tutorial/view/2028](http://community.linuxmint.com/tutorial/view/2028) for details.

Several huge Flash games portals exists, among them are:

*   [https://armorgames.com/](https://armorgames.com/)
*   [https://www.kongregate.com/](https://www.kongregate.com/)
*   [https://www.newgrounds.com/](https://www.newgrounds.com/)

### Java

*   Lots of games smaller than 4kb (some are real masterpieces of game design) can be found at [http://www.java4k.com](http://www.java4k.com).
*   [https://www.pogo.com/](https://www.pogo.com/) – biggest casual Java gaming portal
*   [The Java Game Tome](http://www.javagametome.com/) - huge database of primarily casual games

### Wine

*   Centralized source of information about running games (and other applications) in [Wine](/index.php/Wine "Wine") is [Wine AppDB](http://appdb.winehq.org/).
*   See also [Category:Wine](/index.php/Category:Wine "Category:Wine").

It is recommended (especially for beginners) to use [playonlinux](https://www.archlinux.org/packages/?name=playonlinux), which pulls all necessary dependencies during installation, automatically downloads Windows tools at first start-up to configure and set-up native windows applications to launch properly. For more information, see [Official Website](https://www.playonlinux.com/en/).

## Running games

Certain games or game types may need special configuration to run or to run as expected. For the most part, games will work right out of the box in Arch Linux with possibly better performance than on other distributions due to compile time optimizations. However, some special setups may require a bit of configuration or scripting to make games run as smoothly as desired.

### Multi-screen setups

Running a multi-screen setup may lead to problems with fullscreen games. In such a case, [running a second X server](#Starting_games_in_a_separate_X_server) is one possible solution. Another solution may be found in the [NVIDIA article](/index.php/NVIDIA#Gaming_using_TwinView "NVIDIA") (may also apply to non-NVIDIA users).

### Keyboard grabbing

Many games grab the keyboard, noticeably preventing you from switching windows (also known as alt-tabbing).

Some SDL games (e.g. Guacamelee) let you disable grabbing by pressing `Ctrl-g`.

You can also download [sdl-nokeyboardgrab](https://aur.archlinux.org/packages/sdl-nokeyboardgrab/) to gain the ability to use keyboard commands while in SDL games. If you wish to turn it up to 11, you can disable keyboard grabbing at X11 level using [libx11-nokeyboardgrab](https://aur.archlinux.org/packages/libx11-nokeyboardgrab/), or with more fine-grained control with [libx11-ldpreloadnograb](https://aur.archlinux.org/packages/libx11-ldpreloadnograb/) using the `LD_PRELOAD` environment variable to run applications with particular grab prevention. Wine/lib32 users should also look at the respective lib32 libraries.

**Note:** SDL is known to sometimes not be able to grab the input system. In such a case, it may succeed in grabbing it after a few seconds of waiting.

### Starting games in a separate X server

In some cases like those mentioned above, it may be necessary or desired to run a second X server. Running a second X server has multiple advantages such as better performance, the ability to "tab" out of your game by using `Ctrl+Alt+F7`/`Ctrl+Alt+F8`, no crashing your primary X session (which may have open work on) in case a game conflicts with the graphics driver. The new X server will be akin a remote access login for the ALSA, so your user need to be part of the `audio` group to be able to hear any sound.

To start a second X server (using [Xonotic](http://www.xonotic.org/) as an example) you can simply do:

```
$ xinit /usr/bin/xonotic-glx -- :1 vt$XDG_VTNR

```

This can further be spiced up by using a separate X configuration file:

```
$ xinit /usr/bin/xonotic-glx -- :1 -xf86config xorg-game.conf vt$XDG_VTNR

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

### Tuning Pulseaudio

If you are using [PulseAudio](/index.php/PulseAudio "PulseAudio"), you may wish to tweak some default settings to make sure it is running optimally.

#### Enabling realtime priority and negative nice level

Pulseaudio is built to be run with realtime priority, being an audio daemon. However, because of security risks of it locking up the system, it is scheduled as a regular thread by default. To adjust this, first make sure you are in the `audio` group. Then, uncomment and edit the following lines in `/etc/pulse/daemon.conf`:

```
high-priority = yes
nice-level = -11

```

```
realtime-scheduling = yes
realtime-priority = 5

```

and restart pulseaudio.

#### Using higher quality remixing for better sound

Pulseaudio on Arch uses speex-float-0 by default to remix channels, which is considered a 'medium-low' quality remixing. If your system can handle the extra load, you may benefit from setting it to one of the following instead:

```
resample-method = speex-float-10

```

#### Matching hardware buffers to Pulse's buffering

Matching the buffers can reduce stuttering and increase performance marginally. See [here](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862) for more details.

### Double check your CPU frequency scaling settings

If your system is currently configured to properly insert its own cpu frequency scaling driver, the system sets the default governor to Ondemand. By default, this governor only adjusts the clock if the system is utilizing 95% of its CPU, and then only for a very short period of time. This saves power and reduces heat, but has a noticeable impact on performance. You can instead only have the system downclock when it is idle, by tuning the system governor. To do so, see [Cpufrequtils#Improving on-demand performance](/index.php/Cpufrequtils#Improving_on-demand_performance "Cpufrequtils").

## Improving framerates and responsiveness with scheduling policies

Most every game can benefit if given the correct scheduling policies for the kernel to prioritize the task. However, without the help of a daemon, this rescheduling would have to be carried out manually or through the use of several daemons for each policy. These policies should ideally be set per-thread by the application itself, but not all developers implement these policies. There are several methods for getting them to work anyway:

### For Wine programs

[wine-rt](https://aur.archlinux.org/packages/wine-rt/) is a patched version of Wine that implements scheduling policies on a per-thread basis, using the equivalent of what the Windows developers had intended the threads to be run at. The default patch is more oriented towards professional audio users, and tends to be too heavy-handed of an approach for gaming. You may instead wish to use [this patch](http://pastebin.com/D9GBzBBv), which also includes nice levels and uses more than one policy decision. Be warned that it uses `SCHED_ISO`, which is only properly implemented on [Linux-ck](/index.php/Linux-ck "Linux-ck"), and will simply renice `THREAD_PRIORITY_ABOVE_NORMAL` threads if your system does not support it.

[wine-staging](https://www.archlinux.org/packages/?name=wine-staging) versions 1.9.5 and before incorporate the CSMT patchset which provides better performance for 3D accelerated games. The patchset has been disabled as of 1.9.6 pending an upstream update to the patch and incorporation into the main Wine source tree, so you will need to compile version 1.9.5 of wine-staging yourself if you wish to take advantage of this.

### For everything else

For programs which do not implement scheduling policies on their own, one tool known as **schedtool**, and its associated daemon [schedtoold](https://aur.archlinux.org/packages/schedtoold/) can handle many of these tasks automatically. To edit what programs relieve what policies, simply edit `/etc/schedtoold.conf` and add the program followed by the *schedtool* arguments desired.

#### Policies

First and foremost, setting the scheduling policy to `SCHED_ISO` will not only allow the process to use a maximum of 80 percent of the CPU, but will attempt to reduce latency and stuttering wherever possible. `SCHED_ISO` requires [Linux-ck](/index.php/Linux-ck "Linux-ck") to operate, as it has only been implemented in that kernel. [Linux-ck](/index.php/Linux-ck "Linux-ck") itself provides a hefty latency reduction, and should ideally be installed Most if not all games will benefit from this:

```
bit.trip.runner -I

```

For users not using [Linux-ck](/index.php/Linux-ck "Linux-ck"), `SCHED_FIFO` provides an alternative, that can even work better. You should test to see if your applications run more smoothly with `SCHED_FIFO`, in which case by all means use it instead. Be warned though, as `SCHED_FIFO` runs the risk of starving the system! Use this in cases where -I is used below:

```
bit.trip.runner -F -p 15

```

#### Nice levels

Secondly, the nice level sets which tasks are processed first, in ascending order. A nice level of -4 is reccommended for most multimedia tasks, including games:

```
bit.trip.runner -n -4

```

#### Core affinity

There is some confusion in development as to whether the driver should be multithreading, or the program. In any case where they both attempt it, it causes drops in framerate and crashes. Examples of this include a number of modern games, and any Wine program which is running without [GLSL](https://en.wikipedia.org/wiki/OpenGL_Shading_Language "wikipedia:OpenGL Shading Language") disabled. To select a single core and allow only the driver to handle this process, simply use the `-a 0x*#*` flag, where *#* is the core number, e.g.:

```
bit.trip.runner -a 0x1

```

uses first core. Some CPUs are hyperthreaded and have only 2 or 4 cores but show up as 4 or 8, and are best accounted for:

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

## Using alternate kernels

**Note:** Many users report inconsistant framerate and other performance hits when using [Linux-ck](/index.php/Linux-ck "Linux-ck"), even if the overall framerate is sometimes higher. You may wish to try using [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) if you just want BFQ.

The stock Arch kernel provides a very good baseline for general usage. However, if your system has less than 16 cores and is intended for use primarily as a workstation, you can sacrifice a small amount of throughput on batch workloads and gain a significant boost to interactivity by using [Linux-ck](/index.php/Linux-ck "Linux-ck"). If you prefer not to compile your own kernel, you can instead add [Repo-ck](/index.php/Repo-ck "Repo-ck") and use one of their kernels. Using a pre-optimized kernel will most definitely offset any loss of throughput that may have occurred as a result, so be sure to select the appropriate kernel for your architecture.

### Using BFQ

BFQ is an io-scheduler that comes as a feature of [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) and [Linux-ck](/index.php/Linux-ck "Linux-ck"), and is optimized to be much more simplistic, but provides better interactivity and throughput for non-server workloads. To enable, simply add the kernel parameter *elevator=bfq* to your [bootloader](/index.php/Bootloader "Bootloader"). It is important to note that although most guides recommend using either *noop* or *deadline* for SSDs for their raw throughput, they are actually detrimental to interactivity when more than one thread is attempting to access the device. It is best to use *bfq* unless you desperately need the throughput advantage.

## See also

*   [LinuxGames](http://www.linuxgames.com/) - News on linux games
*   [OSGameClones](http://osgameclones.com/) - List of open source game clones
*   [Free Gamer](http://freegamer.blogspot.com/) - Open source games blog
*   [FreeGameDev](http://forum.freegamedev.net/) - Free/open source game development community
*   [SIG/Games](https://fedoraproject.org/wiki/SIGs/Games#Gaming_News_sites) - OS/Linux gaming news sites and lists at Fedora's wiki
*   [live.linux-gamers](http://live.linux-gamers.net) - Arch-based live gaming distro
*   [Gaming on Linux](http://www.gamingonlinux.com/) - Active Linux gaming news and editorial source and community
*   [Unixgames](https://unixgames.org/) - Q&A service for Linux gamers.