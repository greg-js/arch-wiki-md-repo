<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
    *   [1.1 Relevant online resources](#Relevant_online_resources)
*   [2 Steam runtime](#Steam_runtime)
    *   [2.1 Steam native runtime](#Steam_native_runtime)
*   [3 Debugging shared libraries](#Debugging_shared_libraries)
    *   [3.1 Finding missing game libraries](#Finding_missing_game_libraries)
    *   [3.2 Finding missing runtime libraries](#Finding_missing_runtime_libraries)
*   [4 Debugging Steam](#Debugging_Steam)
*   [5 Runtime issues](#Runtime_issues)
    *   [5.1 Segmentation fault when disabling runtime](#Segmentation_fault_when_disabling_runtime)
    *   [5.2 'GLBCXX_3.X.XX' not found when using Bumblebee](#'GLBCXX_3.X.XX'_not_found_when_using_Bumblebee)
    *   [5.3 Game crashes immediately](#Game_crashes_immediately)
    *   [5.4 Version `CURL_OPENSSL_3` not found](#Version_`CURL_OPENSSL_3`_not_found)
*   [6 Audio issues](#Audio_issues)
    *   [6.1 Configure PulseAudio](#Configure_PulseAudio)
    *   [6.2 No audio or 756 Segmentation fault](#No_audio_or_756_Segmentation_fault)
    *   [6.3 FMOD sound engine](#FMOD_sound_engine)
    *   [6.4 PulseAudio & OpenAL: Audio streams can't be moved between devices](#PulseAudio_&_OpenAL:_Audio_streams_can't_be_moved_between_devices)
*   [7 Steam client issues](#Steam_client_issues)
    *   [7.1 Cannot add library folder because of missing execute permissions](#Cannot_add_library_folder_because_of_missing_execute_permissions)
    *   [7.2 Unusually slow download speed](#Unusually_slow_download_speed)
    *   [7.3 "Needs to be online" error](#"Needs_to_be_online"_error)
    *   [7.4 Steam forgets password](#Steam_forgets_password)
    *   [7.5 Preventing crash memory dumps](#Preventing_crash_memory_dumps)
    *   [7.6 Steam license problem with playing videos](#Steam_license_problem_with_playing_videos)
*   [8 In-home streaming issues](#In-home_streaming_issues)
    *   [8.1 In-home streaming does not work from archlinux host to archlinux guest](#In-home_streaming_does_not_work_from_archlinux_host_to_archlinux_guest)
    *   [8.2 Hardware decoding not available](#Hardware_decoding_not_available)
    *   [8.3 Big Picture Mode minimizes itself after losing focus](#Big_Picture_Mode_minimizes_itself_after_losing_focus)
*   [9 Other issues](#Other_issues)
    *   [9.1 Wrong ELF class](#Wrong_ELF_class)
    *   [9.2 Multiple monitors setup](#Multiple_monitors_setup)
    *   [9.3 Text is corrupt or missing](#Text_is_corrupt_or_missing)
    *   [9.4 SetLocale('en_US.UTF-8') fails at game startup](#SetLocale('en_US.UTF-8')_fails_at_game_startup)
    *   [9.5 Missing libc](#Missing_libc)
    *   [9.6 Games do not launch on older Intel hardware](#Games_do_not_launch_on_older_Intel_hardware)
    *   [9.7 Mesa: Game does not launch, complaining about OpenGL version supported by the card](#Mesa:_Game_does_not_launch,_complaining_about_OpenGL_version_supported_by_the_card)
    *   [9.8 2K games do not run on XFS partitions](#2K_games_do_not_run_on_XFS_partitions)
    *   [9.9 Steam controller not being detected correctly](#Steam_controller_not_being_detected_correctly)
    *   [9.10 Steam controller makes a game crash](#Steam_controller_makes_a_game_crash)
    *   [9.11 Steam hangs on "Installing breakpad exception handler..."](#Steam_hangs_on_"Installing_breakpad_exception_handler...")
    *   [9.12 Killing standalone compositors when launching games](#Killing_standalone_compositors_when_launching_games)
    *   [9.13 Symbol lookup error using DRI3](#Symbol_lookup_error_using_DRI3)
    *   [9.14 Launching games on Nvidia optimus laptops](#Launching_games_on_Nvidia_optimus_laptops)

## Introduction

1.  Make sure that you have followed [Steam#Installation](/index.php/Steam#Installation "Steam").
2.  If the Steam client / a game is not starting and/or you have error message about a library, read [#Steam runtime](#Steam_runtime) and see [#Debugging shared libraries](#Debugging_shared_libraries).
3.  If the issue is related to networking, make sure that you have forwarded the [required ports for Steam](https://support.steampowered.com/kb_article.php?ref=8571-GLVN-8711).
4.  If the issue is about a game, consult [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting").

### Relevant online resources

*   [Multimedia and Games / Arch Linux Forums](https://bbs.archlinux.org/viewforum.php?id=32)
*   [ValveSoftware/steam-for-linux](https://github.com/ValveSoftware/steam-for-linux) – Issue tracking for the Steam for Linux client
*   [Steam Community discussions of the game](https://steamcommunity.com/)
*   [Steam Support FAQ](https://help.steampowered.com/en/)

## Steam runtime

Steam for Linux ships with its own set of libraries called the [Steam runtime](https://github.com/ValveSoftware/steam-runtime). By default Steam launches all Steam Applications within the runtime environment. The Steam runtime is located at `~/.steam/root/ubuntu12_32/steam-runtime/`.

If you mix the Steam runtime libraries with system libraries you will run into binary incompatibility issues, see [steam-for-linux issue #4768](https://github.com/ValveSoftware/steam-for-linux/issues/4768). Binary incompatibility can lead to the Steam client and games not starting (manifesting as a crash, as hanging or silently returning), audio issues and various other problems.

The [steam](https://www.archlinux.org/packages/?name=steam) package offers three ways to launch Steam:

*   `steam-runtime` (alias `steam`), which overrides runtime libraries known to cause problems via the `LD_PRELOAD` [environment variable](/index.php/Environment_variable "Environment variable") (see [ld.so(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ld.so.8)).
*   `steam-native`, see [#Steam native runtime](#Steam_native_runtime)
*   `/usr/lib/steam/steam`, the default Steam launch script

As the Steam runtime libraries are older they can lack newer features, e.g. the OpenAL version of the Steam runtime lacks [HRTF](/index.php/Gaming#Binaural_Audio_with_OpenAL "Gaming") and surround71 support.

### Steam native runtime

**Warning:** Using the Steam native runtime is not recommended as it might break some games due to binary incompatibility and it might miss some libraries present in the Steam runtime.

The `steam-native` script launches Steam with the `STEAM_RUNTIME=0` environment variable making it ignore its runtime and only use system libraries.

The [steam-native-runtime](https://www.archlinux.org/packages/?name=steam-native-runtime) meta package depends on over 120 packages to pose a native replacement of the Steam runtime, some games may however still require additional packages. You can also use the Steam native runtime without [steam-native-runtime](https://www.archlinux.org/packages/?name=steam-native-runtime) by manually installing just the packages you need. See [#Finding missing runtime libraries](#Finding_missing_runtime_libraries).

## Debugging shared libraries

To see the shared libraries required by a program or a shared library run the `ldd` command on it, see [ldd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ldd.1). The `LD_LIBRARY_PATH` and `LD_PRELOAD` [environment variables](/index.php/Environment_variables "Environment variables") can alter which shared libraries are loaded, see [ld.so(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ld.so.8). To correctly debug a program or shared library it is therefore important that these environment variables in your debug environment match the environment you wish to debug.

If you figure out a missing library you can use [pacman](/index.php/Pacman "Pacman") or [pkgfile](/index.php/Pkgfile "Pkgfile") to search for packages that contain the missing library.

### Finding missing game libraries

If a game fails to start, a possible reason is that it is missing required libraries. You can find out what libraries it requests by running `ldd *game_executable*`. `*game_executable*` is likely located somewhere in `~/.steam/root/steamapps/common/`. Please note that most of these "missing" libraries are actually already included with Steam, and do not need to be installed globally.

### Finding missing runtime libraries

If individual games or Steam itself is failing to launch when using `steam-native` you are probably missing libraries. To find the required libraries run:

```
$ cd ~/.steam/root/ubuntu12_32
$ file * | grep ELF | cut -d: -f1 | LD_LIBRARY_PATH=. xargs ldd | grep 'not found' | sort | uniq

```

Alternatively, run Steam with `steam-runtime` and use the following command to see which non-system libraries Steam is using (not all of these are part of the Steam runtime):

```
$ for i in $(pgrep steam); do sed '/\.local/!d;s/.*  //g' /proc/$i/maps; done | sort | uniq

```

## Debugging Steam

The Steam launcher redirects its stdout and stderr to `/tmp/dumps/*USER*_stdout.txt`. This means you do not have to run Steam from the command-line to see that output.

It is possible to debug Steam to gain more information which could be useful to find out why something does not work.

You can set `DEBUGGER` environment variable with one of `gdb`, `cgdb`, `valgrind`, `callgrind`, `strace` and then start `steam`.

For example with [gdb](https://www.archlinux.org/packages/?name=gdb)

 `$ DEBUGGER=gdb steam` 

`gdb` will open, then type `run` which will start `steam` and once crash happens you can type `backtrace` to see call stack.

## Runtime issues

### Segmentation fault when disabling runtime

	[steam-for-linux issue #3863](https://github.com/ValveSoftware/steam-for-linux/issues/3863)

As per the bug report above, Steam crashes with the following error message when run with `STEAM_RUNTIME=0`:

```
/home/*USER*/.local/share/Steam/steam.sh: line 756: <variable numeric code> Segmentation fault (core dumped)

```

This happens because `steamclient.so` is linked to `libudev.so.0` ([lib32-libudev0](https://aur.archlinux.org/packages/lib32-libudev0/)) which conflicts with `libudev.so.1` ([lib32-systemd](https://www.archlinux.org/packages/?name=lib32-systemd)).

A proposed workaround is to copy Steam's packaged 32-bit versions of libusb and libgudev to `/usr/lib32`:

```
# cp ~/.steam/root/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libgudev* /usr/lib32
# cp ~/.steam/root/ubuntu12_32/steam-runtime/i386/lib/i386-linux-gnu/libusb* /usr/lib32

```

Notice that the workaround is necessary because the bug affects systems with lib32-libgudev and lib32-libusb installed.

Alternatively it has been successful to prioritize the loading of the libudev.so.1 (see [comment on the same issue](https://github.com/ValveSoftware/steam-for-linux/issues/3863#issuecomment-203929113)):

 `$ LD_PRELOAD=/usr/lib32/libudev.so.1 STEAM_RUNTIME=0 steam` 

### 'GLBCXX_3.X.XX' not found when using Bumblebee

This error is likely caused because Steam packages its own out of date `libstdc++.so.6`. See [#Steam runtime issues](#Steam_runtime_issues) about working around the bad library. See also [steam-for-linux issue 3773](https://github.com/ValveSoftware/steam-for-linux/issues/3773).

### Game crashes immediately

This is likely due to [#Steam runtime](#Steam_runtime) issues, see [#Debugging shared libraries](#Debugging_shared_libraries).

Disabling the in-game Steam Overlay in the game properties might help.

And finally, if those don't work, you should check Steam's output for any error from the game. You may encounter the following:

*   `munmap_chunk(): invalid pointer`
*   `free(): invalid pointer`

In these cases, try replacing the `libsteam_api.so` file from the problematic game with one of a game that works. This error usually happens for games that were not updated recently when Steam runtime is disabled. This error has been encountered with AYIM, Bastion and Monaco.

### Version `CURL_OPENSSL_3` not found

This is because [curl](https://www.archlinux.org/packages/?name=curl) alone is not compatible with previous versions. You need to install the compatibility libraries:

One of the following messages may show up:

```
# Nuclear Throne
./nuclearthrone: /usr/lib32/libcurl.so.4: version `CURL_OPENSSL_3' not found (required by ./nuclearthrone)

# Devil Daggers
./devildaggers: /usr/lib/libcurl.so.4: version `CURL_OPENSSL_3' not found (required by ./devildaggers)

```

You need to install either [libcurl-compat](https://www.archlinux.org/packages/?name=libcurl-compat) or [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat) and link the compatibility library manually:

```
# Nuclear Throne
$ ln -s /usr/lib32/libcurl-compat.so.4.4.0 "*LIBRARY*/steamapps/common/Nuclear Throne/lib/libcurl.so.4"

# Devil Daggers
$ ln -s /usr/lib/libcurl-compat.so.4.4.0 *LIBRARY*/steamapps/common/devildaggers/lib64/libcurl.so.4

```

## Audio issues

If the sections below do not address the issue, using the [#Steam native runtime](#Steam_native_runtime) might help.

### Configure PulseAudio

Games that explicitly depend on ALSA can break PulseAudio. Follow the directions for [PulseAudio#ALSA](/index.php/PulseAudio#ALSA "PulseAudio") to make these games use PulseAudio instead.

### No audio or 756 Segmentation fault

First [#Configure PulseAudio](#Configure_PulseAudio) and see if that resolves the issue. If you do not have audio in the videos which play within the Steam client, it is possible that the ALSA libraries packaged with Steam are not working.

Attempting to playback a video within the steam client results in an error similar to:

```
ALSA lib pcm_dmix.c:1018:(snd_pcm_dmix_open) unable to open slave

```

A workaround is to rename or delete the `alsa-lib` folder and the `libasound.so.*` files. They can be found at:

```
~/.steam/steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/

```

An alternative workaround is to add the `libasound.so.*` library to the `LD_PRELOAD` environment variable:

```
LD_PRELOAD='/usr/$LIB/libasound.so.2 '${LD_PRELOAD} steam

```

If audio still won't work, adding the Pulseaudio-libs to the `LD_PRELOAD` variable may help:

```
LD_PRELOAD='/usr/$LIB/libpulse.so.0 /usr/$LIB/libpulse-simple.so.0 '${LD_PRELOAD}

```

Be advised that their names may change over time. If so, it is necessary to take a look in

```
~/.steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu

```

and find the new libraries and their versions.

Bugs reports have been filed: [#3376](https://github.com/ValveSoftware/steam-for-linux/issues/3376) and [#3504](https://github.com/ValveSoftware/steam-for-linux/issues/3504)

### FMOD sound engine

The [FMOD](https://www.fmod.com/) audio middleware package is a bit buggy, and as a result games using it may have sound problems.

It usually occurs when an unused sound device is used as default for ALSA. See [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture").

	Affected games: Hotline Miami, Hotline Miami 2, Transistor

### PulseAudio & OpenAL: Audio streams can't be moved between devices

If you use [PulseAudio](/index.php/PulseAudio "PulseAudio") and cannot move an audio stream between sinks, it might be because recent OpenAL versions default to disallow audio streams from being moved. Try to add the following to your `~/.alsoftrc`:

```
[pulse]
allow-moves=true

```

## Steam client issues

### Cannot add library folder because of missing execute permissions

If you add another Steam library folder on another drive, you might get the error message:

```
New Steam library folder must be on a filesystem mounted with execute permissions

```

Make sure you are mounting the filesystem with the correct flags in your `/etc/fstab`, usually by adding `exec` to the list of mount parameter. The parameter must occur after any `user` or `users` parameter since these can imply `noexec`.

This error might also occur if your library folder does not contain a `steamapps` directory. Previous versions used `SteamApps` instead, so ensure the name is fully lowercase.

This error can also occur because of Steam runtime issues and may be fixed following the [#Finding missing runtime libraries](#Finding_missing_runtime_libraries) section.

### Unusually slow download speed

If your Steam apps (games, software…) download speed through the client is unusually slow, but browsing the Steam store and streaming videos is unaffected, installing a DNS cache program, such as [dnsmasq](/index.php/Dnsmasq "Dnsmasq") can help [[1]](https://steamcommunity.com/app/221410/discussions/2/616189106498372437/).

### "Needs to be online" error

If the Steam launcher refuses to start and you get an error saying: "*Fatal Error: Steam needs to be online to update*" while you are online, then there might be issues with name resolving.

Try to install [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns) or [lib32-nss](https://www.archlinux.org/packages/?name=lib32-nss).

### Steam forgets password

	Related: [steam-for-linux#5030](https://github.com/ValveSoftware/steam-for-linux/issues/5030)

Steam for Linux has a bug which causes it to forget the password of some users.

As a workaround, after logging in to Steam, run

```
$ chmod -w ~/.steam/registry.vdf

```

This will make the file read-only so Steam cannot modify it, and thus not log you out.

### Preventing crash memory dumps

Every time Steam crashes, it writes a memory dump to `/tmp/dumps/`. If Steam falls into a crash loop, the dump files can become quite large. When `/tmp` is mounted as [tmpfs](/index.php/Tmpfs "Tmpfs"), memory and swap file can be consumed needlessly.

To prevent this, link `/tmp/dumps/` to `/dev/null`:

```
# ln -s /dev/null /tmp/dumps

```

Or alternatively, create and modify permissions on `/tmp/dumps`. Then Steam will be unable to write dump files to the directory.

```
# mkdir /tmp/dumps
# chmod 600 /tmp/dumps

```

This also has the added benefit of Steam not uploading these dumps to Valve's servers.

### Steam license problem with playing videos

Steam uses [Google's Widevine DRM](https://en.wikipedia.org/wiki/Widevine "w:Widevine") for some videos. If it is not installed you will get the following error:

```
This video requires a license to play which cannot be retrieved. This may be a temporary network condition. Please restart the video to try again.

```

To solve this issue follow the [*Streaming Videos on Steam* support page](https://support.steampowered.com/kb_article.php?ref=8699-OASD-1871#15).

## In-home streaming issues

See [Steam#In-home streaming](/index.php/Steam#In-home_streaming "Steam").

### In-home streaming does not work from archlinux host to archlinux guest

Chances are you are missing [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra). Once you [install](/index.php/Install "Install") that, it should work as expected.

With that, Steam should no longer crash when trying to launch a game through in-home streaming.

### Hardware decoding not available

In-home streaming hardware decoding uses `vaapi`, but steam requires `libva1` where arch now defaults to `libva2`. This means the libva1 package set is required, including the `lib32` versions as well.

As a basic set, this is [libva1](https://www.archlinux.org/packages/?name=libva1) and [lib32-libva1](https://www.archlinux.org/packages/?name=lib32-libva1). Intel graphics users will also require both [libva1-intel-driver](https://www.archlinux.org/packages/?name=libva1-intel-driver) and [lib32-libva1-intel-driver](https://www.archlinux.org/packages/?name=lib32-libva1-intel-driver). For more information about vaapi see [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

It may also be necessary to remove the steam runtime version of libva, in order to force it to use system libraries. The current library in use can be found by using:

```
pgrep steam | xargs -I {} cat /proc/{}/maps | grep libva

```

If this shows locations in `~/.local/Share/steam` steam is still using it's packaged version of libva. This can be rectified by deleting the libva library files at `~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libva*`, so that steam falls back to the system libraries.

### Big Picture Mode minimizes itself after losing focus

This can occur when you play a game via in-home streaming or if you have a multi-monitor setup and move the mouse outside of BPM's window. To prevent this, set the following environment variable and restart Steam

```
export SDL_VIDEO_MINIMIZE_ON_FOCUS_LOSS=0

```

See also the [steam-for-linux issue 4769](https://github.com/ValveSoftware/steam-for-linux/issues/4769).

## Other issues

### Wrong ELF class

If you see this message in Steam's console output

```
ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.

```

you can safely ignore it. It is not really any error: Steam includes both 64- and 32-bit versions of some libraries and only one version will load successfully. This "error" is displayed even when Steam (and the in-game overlay) is working perfectly.

### Multiple monitors setup

A setup with multiple monitors may prevent games from starting. Try to disable all additional displays, and then run a game. You can enable them after the game successfully started.

Also you can try running Steam with this environment variable set:

```
export LD_LIBRARY_PATH=/usr/lib32/nvidia:/usr/lib/nvidia:$LD_LIBRARY_PATH

```

### Text is corrupt or missing

The Steam Support [instructions](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) for Windows seem to work on Linux also.

You can install them via the [steam-fonts](https://aur.archlinux.org/packages/steam-fonts/) package, or manually by downloading and [installing](/index.php/Fonts#Manual_installation "Fonts") [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip).

**Note:** When steam cannot find the Arial fonts, font-config likes to fall back onto the Helveticia bitmap font. Steam does not render this and possibly other bitmap fonts correctly, so either removing problem fonts or [disabling bitmap fonts](/index.php/Font_configuration#Disable_bitmap_fonts "Font configuration") will most likely fix the issue without installing the Arial or ArialBold fonts. The font being used in place of Arial can be found with the command `$ fc-match -v Arial` 

### SetLocale('en_US.UTF-8') fails at game startup

You need to generate the `en_US.UTF-8 UTF-8` locale. See [Locale#Generating locales](/index.php/Locale#Generating_locales "Locale").

### Missing libc

This could be due to a corrupt Steam executable. Check the output of:

```
$ ldd ~/.local/share/Steam/ubuntu12_32/steam

```

Should `ldd` claim that it is not a dynamic executable, then Steam likely corrupted the binary during an update. The following should fix the issue:

```
$ cd ~/.local/share/Steam/
$ ./steam.sh --reset

```

If it doesn't, try to delete the `~/.local/share/Steam/` directory and launch Steam again, telling it to reinstall itself.

This error message can also occur due to a bug in Steam which occurs when your `$HOME` directory ends in a slash (Valve GitHub [issue 3730](https://github.com/ValveSoftware/steam-for-linux/issues/3730)). This can be fixed by editing `/etc/passwd` and changing `/home/<username>/` to `home/<username>`, then logging out and in again. Afterwards, Steam should repair itself automatically.

### Games do not launch on older Intel hardware

	[source](https://steamcommunity.com/app/8930/discussions/1/540744299927655197/)

On older Intel hardware which doesn't support OpenGL 3, such as Intel GMA chips or Westmere CPUs, games may immediately crash when run. It appears as a `gameoverlayrenderer.so` error in `/tmp/dumps/mobile_stdout.txt`, but looking in `/tmp/gameoverlayrenderer.log` it shows a GLXBadFBConfig error.

This can be fixed, by forcing the game to use a later version of OpenGL than it wants. Add `MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140` to your [launch options](/index.php/Launch_option "Launch option").

### Mesa: Game does not launch, complaining about OpenGL version supported by the card

Some games are badly programmed, to use any OpenGL version above 3.0. With Mesa, an application has to request a specific core profile. If it doesn't make such a request, only OpenGL 3.0 and lower are available.

This can be fixed, by forcing the game to use a version of OpenGL it actually needs. Add `MESA_GL_VERSION_OVERRIDE=4.1 MESA_GLSL_VERSION_OVERRIDE=410` to your [launch options](/index.php/Launch_option "Launch option").

### 2K games do not run on XFS partitions

If you are running 2K games such as Civilization 5 on [XFS](/index.php/XFS "XFS") partitions, then the game may not start or run properly due to how the game loads files as it starts. [[3]](https://bbs.archlinux.org/viewtopic.php?id=185222)

### Steam controller not being detected correctly

See [Gamepad#Steam Controller](/index.php/Gamepad#Steam_Controller "Gamepad").

### Steam controller makes a game crash

See [Gamepad#Steam Controller makes a game crash or not recognized](/index.php/Gamepad#Steam_Controller_makes_a_game_crash_or_not_recognized "Gamepad").

### Steam hangs on "Installing breakpad exception handler..."

[BBS#177245](https://bbs.archlinux.org/viewtopic.php?id=177245)

You have an Nvidia GPU and Steam has the following output:

```
Running Steam on arch rolling 64-bit
STEAM_RUNTIME is enabled automatically
Installing breakpad exception handler for appid(steam)/version(0_client)

```

Then nothing else happens. Ensure you have the correct drivers installed as well as their 32-bit versions (the 64-bit and 32-bit variants have to have the same versions): see [NVIDIA#Installation](/index.php/NVIDIA#Installation "NVIDIA").

### Killing standalone compositors when launching games

Further to this, utilising the `%command%` switch, you can kill standalone compositors (such as Xcompmgr or [Compton](/index.php/Compton "Compton")) - which can cause lag and tearing in some games on some systems - and relaunch them after the game ends by adding the following to your game's launch options.

```
 killall compton && %command%; compton -b &

```

Replace `compton` in the above command with whatever your compositor is. You can also add -options to `%command%` or `compton`, of course.

Steam will latch on to any processes launched after `%command%` and your Steam status will show as in game. So in this example, we run the compositor through `nohup` so it is not attached to Steam (it will keep running if you close Steam) and follow it with an ampersand so that the line of commands ends, clearing your Steam status.

### Symbol lookup error using DRI3

Steam outputs this error and exits.

```
 symbol lookup error: /usr/lib/libxcb-dri3.so.0: undefined symbol: xcb_send_request_with_fds

```

To work around this, run Steam with `LIBGL_DRI3_DISABLE=1`, disabling DRI3 for Steam.

### Launching games on Nvidia optimus laptops

To be able to play games which require using Nvidia GPU (for example, Hitman 2016) on optimus enabled laptop, you should start game with *primusrun* prefix in launch options. Otherwise, game will not work.

Find the game in steam library, right click -> Properties -> SET LAUNCH OPTIONS. Change options to

`primusrun %command%`

Running steam with primusrum used to work. While steam has changed some behavior that now running steam with primusrun would not have effect on launching games. As a result, you need to set launch options for each game (and you do NOT have to run steam with primusrun).

For primusrun, VSYNC is enabled by default it could result in a mouse input delay lag, slightly decrease performance and in-game FPS might be locked to a refresh rate of a monitor/display. In order to disable VSYNC for primusrun default value of option vblank_mode needs to be overridden by environment variable.

`vblank_mode=0 primusrun %command%`

Same with optirun that uses primus as a bridge.

`vblank_mode=0 optirun -b primus %command%`

If that did not work try:

`LD_PRELOAD="libpthread.so.0 libGL.so.1" __GL_THREADED_OPTIMIZATIONS=1 optirun %command%`

For more details see [Bumblebee#Primusrun mouse delay (disable VSYNC)](/index.php/Bumblebee#Primusrun_mouse_delay_(disable_VSYNC) "Bumblebee").