**Tip:** The `/usr/bin/steam` script redirects Steam's stdout and stderr to `/tmp/dumps/${USER}_stdout.txt`. This means you do not have to run Steam from a terminal emulator to see that output.

**Note:** In addition to being documented here, any bug/fix/error should be, if not already, reported on Valve's bug tracker on their [GitHub page](https://github.com/ValveSoftware/steam-for-linux).

## Contents

*   [1 Debugging Steam](#Debugging_Steam)
*   [2 Steam runtime issues](#Steam_runtime_issues)
    *   [2.1 Dynamic linker](#Dynamic_linker)
    *   [2.2 Native runtime](#Native_runtime)
        *   [2.2.1 Libraries for x86_64](#Libraries_for_x86_64)
*   [3 Multiple monitors setup](#Multiple_monitors_setup)
*   [4 Native runtime: steam.sh line 756 Segmentation fault](#Native_runtime:_steam.sh_line_756_Segmentation_fault)
*   [5 The close button only minimizes the window](#The_close_button_only_minimizes_the_window)
*   [6 Audio not working or 756 Segmentation fault](#Audio_not_working_or_756_Segmentation_fault)
*   [7 Text is corrupt or missing](#Text_is_corrupt_or_missing)
*   [8 SetLocale('en_US.UTF-8') fails at game startup](#SetLocale.28.27en_US.UTF-8.27.29_fails_at_game_startup)
*   [9 The game crashes immediately after start](#The_game_crashes_immediately_after_start)
*   [10 OpenGL not using direct rendering / Steam crashes Xorg](#OpenGL_not_using_direct_rendering_.2F_Steam_crashes_Xorg)
*   [11 No audio in certain games](#No_audio_in_certain_games)
    *   [11.1 FMOD sound engine](#FMOD_sound_engine)
*   [12 Missing libc](#Missing_libc)
*   [13 Missing libGL](#Missing_libGL)
*   [14 Games do not launch on older intel hardware](#Games_do_not_launch_on_older_intel_hardware)
*   [15 2k games do not run on xfs partitions](#2k_games_do_not_run_on_xfs_partitions)
*   [16 Unable to add library folder because of missing execute permissions](#Unable_to_add_library_folder_because_of_missing_execute_permissions)
*   [17 Steam controller not being detected correctly](#Steam_controller_not_being_detected_correctly)
*   [18 VERSION_ID: unbound variable](#VERSION_ID:_unbound_variable)
*   [19 Steam hangs on "Installing breakpad exception handler..."](#Steam_hangs_on_.22Installing_breakpad_exception_handler....22)
*   [20 'GLBCXX_3.X.XX' not found when using Bumblebee](#.27GLBCXX_3.X.XX.27_not_found_when_using_Bumblebee)
*   [21 Prevent Memory Dumps Consuming RAM](#Prevent_Memory_Dumps_Consuming_RAM)
*   [22 Killing standalone compositors when launching games](#Killing_standalone_compositors_when_launching_games)
*   [23 In Home Streaming does not work from archlinux host to archlinux guest](#In_Home_Streaming_does_not_work_from_archlinux_host_to_archlinux_guest)

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
libGL error: unable to load driver: some_driver_dri.so
libGL error: driver pointer missing
libGL error: failed to load driver: some_driver
libGL error: unable to load driver: swrast_dri.so
libGL error: failed to load driver: swrast
```

```
Failed to load libGL: undefined symbol: xcb_send_fd

```

```
ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.

```

```
OpenGL GLX context is not using direct rendering, which may cause performance problems.

```

```
Could not find required OpenGL entry point 'glGetError'! Either your video card is unsupported or your OpenGL driver needs to be updated.

```

**Note:** A misconfigured [firewall](/index.php/Firewall "Firewall") may cause Steam to fail as it can not connect to its servers. [[1]](https://support.steampowered.com/kb_article.php?ref=2198-AGHC-7226) Most games will crash if the Steam API fails to load.

See also [upstream issue #13](https://github.com/ValveSoftware/steam-runtime/issues/13), and these forum threads:

*   [https://bbs.archlinux.org/viewtopic.php?id=181171](https://bbs.archlinux.org/viewtopic.php?id=181171)
*   [https://bbs.archlinux.org/viewtopic.php?id=183141](https://bbs.archlinux.org/viewtopic.php?id=183141)

### Dynamic linker

The dynamic linker—see [ld.so(8)](http://man7.org/linux/man-pages/man8/ld.so.8.html)—can be used to force Steam to load the up-to-date system libraries via the `LD_PRELOAD` [environment variable](/index.php/Environment_variable "Environment variable"). For example:

```
LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1 /usr/$LIB/libgpg-error.so' /usr/bin/steam

```

**Note:** The `$LIB` above is **not** a variable, but a directive to the linker to pick the appropriate architecture for the library. The single quotes are required to prevent the shell from treating `$LIB` as a variable.

**Tip:** You can put this command in a wrapper script such as `/usr/local/bin/steam-preload`, appending `"$@"` to preserve command-line arguments. This script can be referred to in a [desktop file](/index.php/Desktop_file "Desktop file"), for example through `Exec=/usr/local/bin/steam-preload %U`.

### Native runtime

To force Steam to use only your system libraries, run it with

```
$ STEAM_RUNTIME=0 steam

```

This variable can also be set in a wrapper script or .desktop file, as with the [#Dynamic linker](#Dynamic_linker) solution. However, if you are missing any libraries from the Steam runtime, individual games or Steam itself may fail to launch. To find the required libraries run:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ file * | grep ELF | cut -d: -f1 | LD_LIBRARY_PATH=. xargs ldd | grep 'not found' | sort | uniq

```

**Note:** The libraries must be 32-bit, some of which are only available for x86_64 in the [AUR](/index.php/AUR "AUR").

Alternatively, while Steam is running, the following command will show which non-system libraries Steam is using (not all of these are part of the Steam runtime):

```
$ for i in $(pgrep steam); do sed '/\.local/!d;s/.*  //g' /proc/$i/maps; done | sort | uniq

```

#### Libraries for x86_64

The minimum required libraries needed on an x86_64 system are

*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-nss](https://www.archlinux.org/packages/?name=lib32-nss)
*   [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2)
*   [lib32-gtk3](https://www.archlinux.org/packages/?name=lib32-gtk3)
*   [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra)
*   [lib32-gconf](https://aur.archlinux.org/packages/lib32-gconf/)
*   [lib32-dbus-glib](https://aur.archlinux.org/packages/lib32-dbus-glib/)
*   [lib32-libnm-glib](https://aur.archlinux.org/packages/lib32-libnm-glib/)
*   [lib32-libudev0](https://aur.archlinux.org/packages/lib32-libudev0/)

Some games may require additional libraries in order to launch without the runtime. See [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting").

The meta-package [steam-libs](https://aur.archlinux.org/packages/steam-libs/) includes all of these libraries (as well as some game-specific libraries) as dependencies, to simplify the install process. You can also use the unofficial [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repository to install prebuilt versions of the AUR packages.

## Multiple monitors setup

Setup with multiple monitors can cause `ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.` error which will make game unable to start. If you stuck on this error and have multiple monitors, try to disable all additional displays, and then run a game. You can enable them after the game successfully started.

Also you can try this:

```
export LD_LIBRARY_PATH=/usr/lib32/nvidia:/usr/lib/nvidia:$LD_LIBRARY_PATH

```

and then run steam.

## Native runtime: steam.sh line 756 Segmentation fault

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

## The close button only minimizes the window

	Valve GitHub [issue 1025](https://github.com/ValveSoftware/steam-for-linux/issues/1025)

To close the Steam window (and remove it from the taskbar) when you press **x**, but keep Steam running in the tray, export the environment variable `STEAM_FRAME_FORCE_CLOSE=1`. See [Environment variables#Graphical applications](/index.php/Environment_variables#Graphical_applications "Environment variables").

Steam provides a script located at `/usr/bin/steam` that will be run when launching Steam; adding `export STEAM_FRAME_FORCE_CLOSE=1` to this file will export the environment variable for Steam on application launch.

## Audio not working or 756 Segmentation fault

First try to install [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) and if you run a x86_64 system [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins).

If you do not have audio in the videos which play within the Steam client, it is possible that the ALSA libs packaged with Steam are not working.

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

## Text is corrupt or missing

The Steam Support [instructions](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) for Windows seem to work on Linux also.

You can install them via the [steam-fonts](https://aur.archlinux.org/packages/steam-fonts/) package, or manually by downloading and [installing](/index.php/Fonts#Manual_installation "Fonts") [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip).

**Note:** When steam cannot find the Arial fonts, font-config likes to fall back onto the Helveticia bitmap font. Steam does not render this and possibly other bitmap fonts correctly, so either removing problem fonts or [disabling bitmap fonts](/index.php/Font_configuration#Disable_bitmap_fonts "Font configuration") will most likely fix the issue without installing the Arial or ArialBold fonts. The font being used in place of Arial can be found with the command `$ fc-match -v Arial` 

## SetLocale('en_US.UTF-8') fails at game startup

Uncomment `en_US.UTF-8 UTF-8` in `/etc/locale.gen` and then run `locale-gen` as root.

## The game crashes immediately after start

First, right-click on the game, choose Properties, and click the "Set Launch Options" button. In that text box put:

 `LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%` 

And try the game again. Some games work with this and some games don't.

Then if your game still crashes immediately, try disabling: *"Enable the Steam Overlay while in-game"* in game *Properties*.

And finally, if those don't work, you should check Steam's output for any error from the game. You may encounter the following:

*   munmap_chunk(): invalid pointer
*   free(): invalid pointer

In these particular cases, try replacing the libsteam_api.so file from the problematic game with one from a game that works fine. This error usually happens for games that were not updated recently when Steam runtime is disabled. This error has been encountered with at least AYIM, Bastion and Monaco.

## OpenGL not using direct rendering / Steam crashes Xorg

Sometimes presented with the error message "OpenGL GLX context is not using direct rendering, which may cause performance problems." [[2]](https://support.steampowered.com/kb_article.php?ref=9938-EYZB-7457)

If you still encounter this problem after addressing [#Steam runtime issues](#Steam_runtime_issues), you have probably not installed your 32-bit graphics driver correctly. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for which packages to install.

You can check/test if it is installed correctly by installing [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) and running the following command:

```
$ glxinfo32 | grep OpenGL.

```

## No audio in certain games

If there is no audio in certain games, and the suggestions provided in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") do not fix the problem, [#Native runtime](#Native_runtime) may provide a successful workaround. (See the note about "Steam Runtime issues" at the top of this section.)

### FMOD sound engine

While troubleshooting a sound issue, it became evident that the following games (as examples) use the 'FMOD' audio middleware package:

*   Hotline Miami
*   Hotline Miami 2
*   Transistor

This package is a bit buggy, and as a result while sound can appear to be working fine for the rest of your system, some games may still have problems.

It usually occurs when an unused sound device is used as default for ALSA. See [Advanced Linux Sound Architecture#Set the default sound card](/index.php/Advanced_Linux_Sound_Architecture#Set_the_default_sound_card "Advanced Linux Sound Architecture").

## Missing libc

Verify that [lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc) is installed.

This could also be due to a corrupt Steam executable. Check the output of:

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

If you get this error after reinstalling your Nvidia proprietary drivers, or switching from a version to another, [reinstall](/index.php/Reinstall "Reinstall") [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) and [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl).

## Games do not launch on older intel hardware

On older Intel hardware, if the game immediately crashes when run, it may be because your hardware does not directly support the latest OpenGL. It appears as a gameoverlayrenderer.so error in /tmp/dumps/mobile_stdout.txt, but looking in /tmp/gameoverlayrenderer.log it shows a GLXBadFBConfig error.

This can be fixed, however, by forcing the game to use a later version of OpenGL than it wants. Right click on the game, select Properties. Then, click "Set Launch Options" in the "General" tab and paste the following:

```
MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140 %command%

```

## 2k games do not run on xfs partitions

If you are running 2k games such as Civilization 5 on xfs partitions, then the game may not start or run properly due to how the game loads files as it starts. [[4]](https://bbs.archlinux.org/viewtopic.php?id=185222)

## Unable to add library folder because of missing execute permissions

If you add another steam library folder on another drive, you might receive the error message *"New Steam library folder must be on a filesystem mounted with execute permissions"*.

Make sure you are mounting the filesystem with the correct flags in your `/etc/fstab`, usually by adding `exec` to the list of mount parameter. The parameter must occur after any `user` or `users` parameter since these can imply `noexec`.

This error might also occur if you are readding a library folder and Steam is unable to find a contained `steamapps` folder. Previous versions used `SteamApps` instead, so ensure the name is fully lowercase.

## Steam controller not being detected correctly

See [Gamepad#Steam Controller](/index.php/Gamepad#Steam_Controller "Gamepad").

## VERSION_ID: unbound variable

In Steam's output, you may see the following line:

```
/home/user/.local/share/Steam/steam.sh: line 161: VERSION_ID: unbound variable

```

This is because steam.sh parses `/etc/os-release` and expects a VERSION_ID which Arch does not have. This error is unimportant but you can fix it by adding the following line to `/etc/os-release`:

```
VERSION_ID="2015.11.01"

```

## Steam hangs on "Installing breakpad exception handler..."

[BBS#177245](https://bbs.archlinux.org/viewtopic.php?id=177245)

Steam has the following output:

```
Running Steam on arch rolling 64-bit
STEAM_RUNTIME is enabled automatically
Installing breakpad exception handler for appid(steam)/version(0_client)

```

Then nothing else happens. This is likely related to mis-matched `lib32-nvidia-*` packages.

## 'GLBCXX_3.X.XX' not found when using Bumblebee

This error is likely caused because Steam packages its own out of date `libstdc++.so.6`. See [#Steam runtime issues](#Steam_runtime_issues) about working around the bad library. See also GitHub [issue 3773](https://github.com/ValveSoftware/steam-for-linux/issues/3773).

## Prevent Memory Dumps Consuming RAM

Every time steam crashes, it writes a memory dump to **/tmp/dumps/**. If Steam falls into a crash loop, and it often does, the dump files can start consuming considerable space. Since **/tmp** on Arch is mounted as tmpfs, memory and swap file can be consumed needlessly. To prevent this, you can make a symbolic link to **/dev/null** or create and modify permissions on **/tmp/dumps**. Then Steam will be unable to write dump files to the directory. This also has the added benefit of Steam not uploading these dumps to Valve's servers.

```
# ln -s /dev/null /tmp/dumps

```

or

```
# mkdir /tmp/dumps
# chmod 600 /tmp/dumps

```

## Killing standalone compositors when launching games

Further to this, utilising the `%command%` switch, you can kill standalone compositors (such as Xcompmgr or [Compton](/index.php/Compton "Compton")) - which can cause lag and tearing in some games on some systems - and relaunch them after the game ends by adding the following to your game's launch options.

```
 killall compton && %command%; compton -b &

```

Replace `compton` in the above command with whatever your compositor is. You can also add -options to `%command%` or `compton`, of course.

Steam will latch on to any processes launched after `%command%` and your Steam status will show as in game. So in this example, we run the compositor through `nohup` so it is not attached to Steam (it will keep running if you close Steam) and follow it with an ampersand so that the line of commands ends, clearing your Steam status.

## In Home Streaming does not work from archlinux host to archlinux guest

Chances are you are missing [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra). Once you [install](/index.php/Install "Install") that, it should work as expected.

With that, steam should no longer crash when trying to launch a game through in home streaming.