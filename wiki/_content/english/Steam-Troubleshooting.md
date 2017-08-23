**Tip:** The Steam launcher redirects its stdout and stderr to `/tmp/dumps/*USER*_stdout.txt`. This means you do not have to run Steam from a terminal emulator to see that output.

**Note:** Bugs should be reported at Valve's [GitHub issue tracker](https://github.com/ValveSoftware/steam-for-linux).

## Contents

*   [1 Debugging Steam](#Debugging_Steam)
*   [2 Steam runtime issues](#Steam_runtime_issues)
    *   [2.1 Solutions](#Solutions)
    *   [2.2 Finding missing runtime libraries](#Finding_missing_runtime_libraries)
*   [3 Other runtime issues](#Other_runtime_issues)
    *   [3.1 Native runtime: steam.sh line 756 Segmentation fault](#Native_runtime:_steam.sh_line_756_Segmentation_fault)
    *   [3.2 OpenGL not using direct rendering / Steam crashes Xorg](#OpenGL_not_using_direct_rendering_.2F_Steam_crashes_Xorg)
    *   [3.3 'GLBCXX_3.X.XX' not found when using Bumblebee](#.27GLBCXX_3.X.XX.27_not_found_when_using_Bumblebee)
    *   [3.4 Games crash immediately](#Games_crash_immediately)
*   [4 Audio issues](#Audio_issues)
    *   [4.1 Configure PulseAudio](#Configure_PulseAudio)
    *   [4.2 No audio or 756 Segmentation fault](#No_audio_or_756_Segmentation_fault)
    *   [4.3 FMOD sound engine](#FMOD_sound_engine)
    *   [4.4 Audio streams can't be moved between devices](#Audio_streams_can.27t_be_moved_between_devices)
*   [5 In-home streaming issues](#In-home_streaming_issues)
    *   [5.1 In Home Streaming does not work from archlinux host to archlinux guest](#In_Home_Streaming_does_not_work_from_archlinux_host_to_archlinux_guest)
    *   [5.2 Hardware decoding not available](#Hardware_decoding_not_available)
    *   [5.3 BPM minimizes itself after losing focus](#BPM_minimizes_itself_after_losing_focus)
*   [6 Wrong ELF class](#Wrong_ELF_class)
*   [7 Multiple monitors setup](#Multiple_monitors_setup)
*   [8 Text is corrupt or missing](#Text_is_corrupt_or_missing)
*   [9 SetLocale('en_US.UTF-8') fails at game startup](#SetLocale.28.27en_US.UTF-8.27.29_fails_at_game_startup)
*   [10 Missing libc](#Missing_libc)
*   [11 Missing libGL](#Missing_libGL)
*   [12 Missing vgui2_s.so](#Missing_vgui2_s.so)
*   [13 Games do not launch on older Intel hardware](#Games_do_not_launch_on_older_Intel_hardware)
*   [14 2K games do not run on XFS partitions](#2K_games_do_not_run_on_XFS_partitions)
*   [15 Unable to add library folder because of missing execute permissions](#Unable_to_add_library_folder_because_of_missing_execute_permissions)
*   [16 Steam controller not being detected correctly](#Steam_controller_not_being_detected_correctly)
*   [17 Steam hangs on "Installing breakpad exception handler..."](#Steam_hangs_on_.22Installing_breakpad_exception_handler....22)
*   [18 Prevent memory dumps from consuming RAM](#Prevent_memory_dumps_from_consuming_RAM)
*   [19 Killing standalone compositors when launching games](#Killing_standalone_compositors_when_launching_games)
*   [20 Very slow app download speed](#Very_slow_app_download_speed)
*   [21 Symbol lookup error using dri3](#Symbol_lookup_error_using_dri3)
*   [22 Launching games on nvidia optimus laptops](#Launching_games_on_nvidia_optimus_laptops)

## Debugging Steam

It is possible to debug Steam to gain more information which could be useful to find out why something does not work.

You can set `DEBUGGER` environment variable with one of `gdb`, `cgdb`, `valgrind`, `callgrind`, `strace` and then start `steam`.

For example with [gdb](https://www.archlinux.org/packages/?name=gdb)

 `$ DEBUGGER=gdb steam` 

`gdb` will open, then type `run` which will start `steam` and once crash happens you can type `backtrace` to see call stack.

## Steam runtime issues

Steam installs its own older versions of some libraries collectively called the "Steam Runtime". These will often conflict with the libraries included in Arch Linux, and out-of-date libraries may be missing important features (Notably, the OpenAL version they ship lacks [HRTF](/index.php/Gaming#Binaural_Audio_with_OpenAL "Gaming") and surround71 support).

Some of the possible symptoms of this issue are the Steam client itself crashing or hanging, and/or various errors:

```
libGL error: unable to load driver: *some_driver_dri*.so
libGL error: driver pointer missing
libGL error: failed to load driver: *some_driver*
libGL error: unable to load driver: swrast_dri.so
libGL error: failed to load driver: swrast
```

```
Failed to load libGL: undefined symbol: xcb_send_fd

```

```
OpenGL GLX context is not using direct rendering, which may cause performance problems.

```

```
Could not find required OpenGL entry point 'glGetError'! Either your video card is unsupported or your OpenGL driver needs to be updated.

```

**Note:** A misconfigured [firewall](/index.php/Firewall "Firewall") may cause Steam to fail as it can not connect to its servers. [[1]](https://support.steampowered.com/kb_article.php?ref=2198-AGHC-7226) Most games will crash if the Steam API fails to load.

See also [upstream issue #4768](https://github.com/ValveSoftware/steam-for-linux/issues/4768), and these forum threads:

*   [https://bbs.archlinux.org/viewtopic.php?id=181171](https://bbs.archlinux.org/viewtopic.php?id=181171)
*   [https://bbs.archlinux.org/viewtopic.php?id=183141](https://bbs.archlinux.org/viewtopic.php?id=183141)

### Solutions

There are three ways to run Steam provided by the [steam](https://www.archlinux.org/packages/?name=steam) package:

```
$ steam-runtime

```

This is the command which is run when you run Steam via `/usr/bin/steam` or the "Steam" [desktop entry](/index.php/Desktop_entry "Desktop entry"). Runtime libraries which are known to cause problems are overriden via the `LD_PRELOAD` [environment variable](/index.php/Environment_variable "Environment variable") (see [ld.so(8)](http://man7.org/linux/man-pages/man8/ld.so.8.html)). If your system still has library conflicts with this command, you can make a copy of `/usr/bin/steam-runtime` and edit it to add additional workarounds.

```
$ steam-native

```

This is the command run by the "Steam (Native)" [desktop entry](/index.php/Desktop_entry "Desktop entry"). This version forces Steam to ignore its runtime and only use system libraries. You will probably need to install [steam-native-runtime](https://www.archlinux.org/packages/?name=steam-native-runtime) in order for Steam to run at all, though some games may require additional packages. See [#Finding missing runtime libraries](#Finding_missing_runtime_libraries) and [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting").

```
$ /usr/lib/steam/steam

```

This is the normal Steam launcher without any Arch-specific workarounds.

### Finding missing runtime libraries

If individual games or Steam itself is failing to launch when using `steam-native` you are probably missing libraries. To find the required libraries run:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ file * | grep ELF | cut -d: -f1 | LD_LIBRARY_PATH=. xargs ldd | grep 'not found' | sort | uniq

```

Alternatively, run Steam with its runtime (`/usr/bin/steam`) and use the following command to see which non-system libraries Steam is using (not all of these are part of the Steam runtime):

```
$ for i in $(pgrep steam); do sed '/\.local/!d;s/.*  //g' /proc/$i/maps; done | sort | uniq

```

If the above commands have no output and you have an NVIDIA video card, then you may need to explitly install [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils).

## Other runtime issues

### Native runtime: steam.sh line 756 Segmentation fault

	Valve GitHub [issue 3863](https://github.com/ValveSoftware/steam-for-linux/issues/3863)

As per the bug report above, Steam crashes with `/home/<username>/.local/share/Steam/steam.sh: line 756: <variable numeric code> Segmentation fault (core dumped)` when running with STEAM_RUNTIME=0.

This happens because steamclient.so is linked to libudev.so.0 ([lib32-libudev0](https://aur.archlinux.org/packages/lib32-libudev0/)) which conflicts with libudev.so.1 ([lib32-systemd](https://www.archlinux.org/packages/?name=lib32-systemd))

The only proposed workaround is copying Steam's packaged 32-bit versions of libusb and libgudev to /usr/lib32:

```
# cp $HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libgudev* /usr/lib32
# cp $HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/lib/i386-linux-gnu/libusb* /usr/lib32
```

Notice that the workaround is necessary because the bug affects systems with lib32-libgudev and lib32-libusb installed.

Alternatively it has been successful to prioritize the loading of the libudev.so.1 (see [comment on the same issue](https://github.com/ValveSoftware/steam-for-linux/issues/3863#issuecomment-203929113)):

 `$ LD_PRELOAD=/usr/lib32/libudev.so.1 STEAM_RUNTIME=0 steam` 

### OpenGL not using direct rendering / Steam crashes Xorg

Sometimes presented with the error message "OpenGL GLX context is not using direct rendering, which may cause performance problems." [[2]](https://support.steampowered.com/kb_article.php?ref=9938-EYZB-7457)

If you still encounter this problem after addressing [#Steam runtime issues](#Steam_runtime_issues), you have probably not installed your 32-bit graphics driver correctly. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for which packages to install.

You can check/test if it is installed correctly by installing [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) and running the following command:

```
$ glxinfo32 | grep OpenGL.

```

### 'GLBCXX_3.X.XX' not found when using Bumblebee

This error is likely caused because Steam packages its own out of date `libstdc++.so.6`. See [#Steam runtime issues](#Steam_runtime_issues) about working around the bad library. See also GitHub [issue 3773](https://github.com/ValveSoftware/steam-for-linux/issues/3773).

### Games crash immediately

This is likely due to [#Steam runtime issues](#Steam_runtime_issues). If those solutions do not work, try setting the following [launch options](/index.php/Steam#Launch_options "Steam"):

 `LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%` 

If it does not help try disabling: *Enable the Steam Overlay while in-game* in the game properties.

And finally, if those don't work, you should check Steam's output for any error from the game. You may encounter the following:

*   munmap_chunk(): invalid pointer
*   free(): invalid pointer

In these cases, try replacing the libsteam_api.so file from the problematic game with one of a game that works. This error usually happens for games that were not updated recently when Steam runtime is disabled. This error has been encountered with AYIM, Bastion and Monaco.

## Audio issues

Check [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") for issues with specific games. If the sections below do not address the issue, try running Steam with the native runtime (see [#Solutions](#Solutions)).

### Configure PulseAudio

Games that explicitly depend on ALSA can break PulseAudio. Follow the directions for [PulseAudio#ALSA](/index.php/PulseAudio#ALSA "PulseAudio") to make these games use PulseAudio instead.

### No audio or 756 Segmentation fault

First [#Configure PulseAudio](#Configure_PulseAudio) and see if that resolves the issue. If you do not have audio in the videos which play within the Steam client, it is possible that the ALSA libs packaged with Steam are not working.

Attempting to playback a video within the steam client results in an error similar to:

```
ALSA lib pcm_dmix.c:1018:(snd_pcm_dmix_open) unable to open slave

```

A workaround is to rename or delete the `alsa-lib` folder and the `libasound.so.*` files. They can be found at:

```
~/.steam/steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/

```

An alternative workaround is to add the `libasound.so.*` library to the **LD_PRELOAD** environment variable:

```
LD_PRELOAD='/usr/$LIB/libasound.so.2 '${LD_PRELOAD} steam

```

If audio still won't work, adding the Pulseaudio-libs to the **LD_PRELOAD** variable may help:

```
LD_PRELOAD='/usr/$LIB/libpulse.so.0 /usr/$LIB/libpulse-simple.so.0 '${LD_PRELOAD}

```

Be adviced that their names may change over time. If so, it is necessary to take a look in

```
~/.steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu

```

and find the new libs and their versions.

Bugs reports have been filed: [#3376](https://github.com/ValveSoftware/steam-for-linux/issues/3376) and [#3504](https://github.com/ValveSoftware/steam-for-linux/issues/3504)

### FMOD sound engine

While troubleshooting a sound issue, it became evident that the following games (as examples) use the 'FMOD' audio middleware package:

*   Hotline Miami
*   Hotline Miami 2
*   Transistor

This package is a bit buggy, and as a result while sound can appear to be working fine for the rest of your system, some games may still have problems.

It usually occurs when an unused sound device is used as default for ALSA. See [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture").

### Audio streams can't be moved between devices

If you use [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and attempt to move an audio stream between different sinks, there's a possibility that you won't be able to move the stream.

This is due to recent versions of OpenAL default to disallow pulse streams from being moved, create a ~/.alsoftrc with the contents

```
[pulse]
allow-moves=true

```

to remedy this fact

## In-home streaming issues

### In Home Streaming does not work from archlinux host to archlinux guest

Chances are you are missing [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra). Once you [install](/index.php/Install "Install") that, it should work as expected.

With that, steam should no longer crash when trying to launch a game through in home streaming.

### Hardware decoding not available

In-home streaming hardware decoding uses `vaapi`, so it needs to be installed (or wrapped around `vdpau`). See [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). Remember to install the `lib32` versions as well.

### BPM minimizes itself after losing focus

This can occur when you play a game via in-home streaming or if you have a multi-monitor setup and move the mouse outside of BPM's window. To prevent this, set the following environment variable and restart Steam

```
export SDL_VIDEO_MINIMIZE_ON_FOCUS_LOSS=0

```

See also the [github issue](https://github.com/ValveSoftware/steam-for-linux/issues/4769).

## Wrong ELF class

If you see this message in Steam's console output

```
ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.

```

you can safely ignore it. It is not really any error: Steam includes both 64- and 32-bit versions of some libraries and only one version will load successfully. This "error" is displayed even when Steam (and the in-game overlay) is working perfectly.

## Multiple monitors setup

A setup with multiple monitors may prevent games from starting. Try to disable all additional displays, and then run a game. You can enable them after the game successfully started.

Also you can try running Steam with this environment variable set:

```
export LD_LIBRARY_PATH=/usr/lib32/nvidia:/usr/lib/nvidia:$LD_LIBRARY_PATH

```

## Text is corrupt or missing

The Steam Support [instructions](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) for Windows seem to work on Linux also.

You can install them via the [steam-fonts](https://aur.archlinux.org/packages/steam-fonts/) package, or manually by downloading and [installing](/index.php/Fonts#Manual_installation "Fonts") [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip).

**Note:** When steam cannot find the Arial fonts, font-config likes to fall back onto the Helveticia bitmap font. Steam does not render this and possibly other bitmap fonts correctly, so either removing problem fonts or [disabling bitmap fonts](/index.php/Font_configuration#Disable_bitmap_fonts "Font configuration") will most likely fix the issue without installing the Arial or ArialBold fonts. The font being used in place of Arial can be found with the command `$ fc-match -v Arial` 

Specific games may have other font requirement. See [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting").

## SetLocale('en_US.UTF-8') fails at game startup

You need to generate the `en_US.UTF-8 UTF-8` locale. See [Locale#Generating locales](/index.php/Locale#Generating_locales "Locale").

## Missing libc

This could be due to a corrupt Steam executable. Check the output of:

```
$ ldd ~/.local/share/Steam/ubuntu12_32/steam

```

Should `ldd` claim that it is not a dynamic executable, then Steam likely corrupted the binary during an update. The following should fix the issue:

```
$ cd ~/.local/share/Steam/
$ ./steam.sh --reset

```

If it doesn't, try to delete the `~/.local/share/Steam/` directory and launch steam again, telling it to reinstall itself.

This error message can also occur due to a bug in steam which occurs when your `$HOME` directory ends in a slash (Valve GitHub [issue 3730](https://github.com/ValveSoftware/steam-for-linux/issues/3730)). This can be fixed by editing `/etc/passwd` and changing `/home/<username>/` to `home/<username>`, then logging out and in again. Afterwards, steam should repair itself automatically.

## Missing libGL

You may encounter this error when you launch Steam at first time.

```
You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1

```

Make sure you have installed the `lib32` version of all your video drivers as described in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

## Missing vgui2_s.so

Error on startup:

```
Could not load module 'vgui2_s.so'.
For more information visit [https://support.steampowered.com/kb_article.php?ref=9205-OZVN-0660](https://support.steampowered.com/kb_article.php?ref=9205-OZVN-0660)

```

Solution: install package `lib32-openal`

## Games do not launch on older Intel hardware

On older Intel hardware which doesn't support OpenGL 3, such as Intel GMA chips or Westmere CPUs, games may immediately crash when run. It appears as a gameoverlayrenderer.so error in /tmp/dumps/mobile_stdout.txt, but looking in /tmp/gameoverlayrenderer.log it shows a GLXBadFBConfig error.

This can be fixed, however, by forcing the game to use a later version of OpenGL than it wants. Right click on the game, select Properties. Then, click "Set Launch Options" in the "General" tab and paste the following:

```
MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140 %command%

```

## 2K games do not run on XFS partitions

If you are running 2K games such as Civilization 5 on [XFS](/index.php/XFS "XFS") partitions, then the game may not start or run properly due to how the game loads files as it starts. [[4]](https://bbs.archlinux.org/viewtopic.php?id=185222)

## Unable to add library folder because of missing execute permissions

If you add another steam library folder on another drive, you might receive the error message *"New Steam library folder must be on a filesystem mounted with execute permissions"*.

Make sure you are mounting the filesystem with the correct flags in your `/etc/fstab`, usually by adding `exec` to the list of mount parameter. The parameter must occur after any `user` or `users` parameter since these can imply `noexec`.

This error might also occur if you are readding a library folder and Steam is unable to find a contained `steamapps` folder. Previous versions used `SteamApps` instead, so ensure the name is fully lowercase.

This error can also occur because of steam runtime issues and may be fixed following the [#Dynamic linker](#Dynamic_linker) section.

## Steam controller not being detected correctly

See [Gamepad#Steam Controller](/index.php/Gamepad#Steam_Controller "Gamepad").

## Steam hangs on "Installing breakpad exception handler..."

[BBS#177245](https://bbs.archlinux.org/viewtopic.php?id=177245)

You have an NVIDIA GPU and Steam has the following output:

```
Running Steam on arch rolling 64-bit
STEAM_RUNTIME is enabled automatically
Installing breakpad exception handler for appid(steam)/version(0_client)

```

Then nothing else happens. Ensure you have the correct drivers installed as well as their 32-bit versions: see [NVIDIA#Installation](/index.php/NVIDIA#Installation "NVIDIA").

## Prevent memory dumps from consuming RAM

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

## Killing standalone compositors when launching games

Further to this, utilising the `%command%` switch, you can kill standalone compositors (such as Xcompmgr or [Compton](/index.php/Compton "Compton")) - which can cause lag and tearing in some games on some systems - and relaunch them after the game ends by adding the following to your game's launch options.

```
 killall compton && %command%; compton -b &

```

Replace `compton` in the above command with whatever your compositor is. You can also add -options to `%command%` or `compton`, of course.

Steam will latch on to any processes launched after `%command%` and your Steam status will show as in game. So in this example, we run the compositor through `nohup` so it is not attached to Steam (it will keep running if you close Steam) and follow it with an ampersand so that the line of commands ends, clearing your Steam status.

## Very slow app download speed

If your Steam apps (games, software…) download speed through the client is unusually slow, but browsing the Steam store and streaming videos is unaffected, installing a DNS cache program, such as [dnsmasq](/index.php/Dnsmasq "Dnsmasq") can help [[5]](https://steamcommunity.com/app/221410/discussions/2/616189106498372437/).

## Symbol lookup error using dri3

Steam outputs this error and exits.

```
 symbol lookup error: /usr/lib/libxcb-dri3.so.0: undefined symbol: xcb_send_request_with_fds

```

For steam to work, disable dri3 in xorg config file or as a workaround run steam with `LIBGL_DRI3_DISABLE=1`

```
 LIBGL_DRI3_DISABLE=1 steam

```

## Launching games on nvidia optimus laptops

To be able to play games which require using nvidia GPU (for example, Hitman 2016) on optimus enabled laptop, you should start steam with *primusrun* prefix. Otherwise, game will not work. Keep in mind, that issuing some command such as `primusrun steam` while steam is already running will not restart it. You should explicitly exit and then start steam via `primusrun steam` command or start game immediately after start, for example with `primusrun steam steam://rungameid/236870`. After steam was launched with primusrun prefix, you do not need to prefix your game with primusrun or optirun, because it does not matter.