See [Steam](/index.php/Steam "Steam") for the main article.

**Tip:** The `/usr/bin/steam` script redirects Steam's stdout and stderr to `/tmp/dumps/${USER}_stdout.txt`. This means you do not have to run Steam from a terminal emulator to see that output.

**Note:** In addition to being documented here, any bug/fix/error should be, if not already, reported on Valve's bug tracker on their [GitHub page](https://github.com/ValveSoftware/steam-for-linux).

## Contents

*   [1 Issues with nvidia 361.28](#Issues_with_nvidia_361.28)
*   [2 Steam runtime issues](#Steam_runtime_issues)
    *   [2.1 Possible symptoms](#Possible_symptoms)
    *   [2.2 Work arounds](#Work_arounds)
        *   [2.2.1 Using the dynamic linker](#Using_the_dynamic_linker)
        *   [2.2.2 Deleting the runtime libraries](#Deleting_the_runtime_libraries)
    *   [2.3 More information](#More_information)
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

### Issues with nvidia 361.28

A bug was introduced in nvidia 361.28 that prevents some games from launching with an error such as

 `"Missing basic OpenGL v1.0 -> v2.0 required OpenGL functionality."` 

You can update to 361.42 drivers

To workaround this until NVIDIA fixes this issue, use this line for the launch options for every game that fails:

 `__GLVND_DISALLOW_PATCHING=1 %command%` 

Alternatively, you can roll back to the 361.16 drivers

### Steam runtime issues

Steam installs its own older versions of some libraries collectively called the "Steam Runtime". These will often conflict with the libraries included in Arch Linux.

#### Possible symptoms

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
OpenGL GLX context is not using direct rendering, which may cause performance problems. [(see below)](#OpenGL_not_using_direct_rendering_.2F_Steam_crashes_Xorg)

```

```
Could not find required OpenGL entry point 'glGetError'! Either your video card is unsupported or your OpenGL driver needs to be updated.}}

```

**Note:** A misconfigured firewall may also show up as a runtime issue, because Steam silently fails whenever it can't connect to its servers, and most games just crash whenever the Steam API fails to load.

#### Work arounds

You can work around the issue by forcing Steam to use the up-to-date system versions (the ones installed by [pacman](/index.php/Pacman "Pacman")). There are two ways to do so.

##### Using the dynamic linker

The dynamic linker (`man 8 ld.so`) can be told to load specific libraries using the `LD_PRELOAD` [environment variable](/index.php/Environment_variable "Environment variable").

```
LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1 /usr/$LIB/libgpg-error.so' steam

```

If you wish to use this method in a .desktop shortcut, you can use this command in the **Exec=** field. In this case you need to enclose the command in `"` and prepend every `$` with `\\`.

```
Exec="env LD_PRELOAD='/usr/\\$LIB/libstdc++.so.6 /usr/\\$LIB/libgcc_s.so.1 /usr/\\$LIB/libxcb.so.1 /usr/\\$LIB/libgpg-error.so' /usr/bin/steam %U"

```

**Note:** The '$LIB' above is not a variable but a directive to the linker to pick the appropriate architecture for the library. The single quotes are required to prevent the shell from treating $LIB as a variable.

##### Deleting the runtime libraries

Run this command to delete the runtime libraries known to cause issues on Arch Linux:

```
find ~/.steam/root/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" -o -name "libgpg-error.so*" \) -print -delete

```

If the above command does not work, run the above command again, then run this command.

```
find ~/.local/share/Steam/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" -o -name "libgpg-error.so*" \) -print -delete

```

**Note:** Steam will frequently re-install these runtime libraries when Steam is updated, so until the issue is resolved: whenever Steam updates, you should exit, remove the libraries, and restart it again.

If you wish to restore the files that were deleted by the commands above, you can use the built-in steam reset functionality.

**Warning:** `--reset` also deletes your games (the AppCache).

```
steam --reset

```

#### More information

See also [upstream issue #13](https://github.com/ValveSoftware/steam-runtime/issues/13), [#Using native runtime](#Using_native_runtime), and these forum threads:

*   [https://bbs.archlinux.org/viewtopic.php?id=181171](https://bbs.archlinux.org/viewtopic.php?id=181171)
*   [https://bbs.archlinux.org/viewtopic.php?id=183141](https://bbs.archlinux.org/viewtopic.php?id=183141)

### Multiple monitors setup

Setup with multiple monitors can cause `ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.` error which will make game unable to start. If you stuck on this error and have multiple monitors, try to disable all additional displays, and then run a game. You can enable them after the game successfully started.

Also you can try this:

```
export LD_LIBRARY_PATH=/usr/lib32/nvidia:/usr/lib/nvidia:$LD_LIBRARY_PATH

```

and then run steam.

### Native runtime: steam.sh line 756 Segmentation fault

	Valve GitHub [issue 3863](https://github.com/ValveSoftware/steam-for-linux/issues/3863)

As per the bug report above, Steam crashes with `/home/<username>/.local/share/Steam/steam.sh: line 756: <variable numeric code> Segmentation fault (core dumped)` when running with STEAM_RUNTIME=0.

The only proposed workaround is copying Steam's packaged 32-bit versions of libusb and libgudev to /usr/lib32:

```
# cp $HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libgudev* /usr/lib32
# cp $HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/lib/i386-linux-gnu/libusb* /usr/lib32
```

Notice that the workaround is necessary because the bug affects systems with lib32-libgudev and lib32-libusb installed.

Alternatively it has been successful to prioritize the loading of the libudev.so.1 (see [comment on the same issue](https://github.com/ValveSoftware/steam-for-linux/issues/3863#issuecomment-203929113)):

 `$ LD_PRELOAD=/usr/lib32/libudev.so.1 STEAM_RUNTIME=0 steam` 

### The close button only minimizes the window

	Valve GitHub [issue 1025](https://github.com/ValveSoftware/steam-for-linux/issues/1025)

To close the Steam window (and remove it from the taskbar) when you press **x**, but keep Steam running in the tray, export the environment variable `STEAM_FRAME_FORCE_CLOSE=1`. See [Environment variables#Graphical applications](/index.php/Environment_variables#Graphical_applications "Environment variables").

Steam provides a script located at `/usr/bin/steam` that will be run when launching Steam; adding `export STEAM_FRAME_FORCE_CLOSE=1` to this file will export the environment variable for Steam on application launch.

### Audio not working or 756 Segmentation fault

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

Bugs reports have been filed: [#3376](https://github.com/ValveSoftware/steam-for-linux/issues/3376) and [#3504](https://github.com/ValveSoftware/steam-for-linux/issues/3504)

### Text is corrupt or missing

The Steam Support [instructions](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) for Windows seem to work on Linux also.

You can install them via the [steam-fonts](https://aur.archlinux.org/packages/steam-fonts/) package, or manually by downloading and [installing](/index.php/Fonts#Manual_installation "Fonts") [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip).

**Note:** When steam cannot find the Arial fonts, font-config likes to fall back onto the Helveticia bitmap font. Steam does not render this and possibly other bitmap fonts correctly, so either removing problem fonts or [disabling bitmap fonts](/index.php/Font_configuration#Disable_bitmap_fonts "Font configuration") will most likely fix the issue without installing the Arial or ArialBold fonts. The font being used in place of Arial can be found with the command `$ fc-match -v Arial` 

### SetLocale('en_US.UTF-8') fails at game startup

Uncomment `en_US.UTF-8 UTF-8` in `/etc/locale.gen` and then run `locale-gen` as root.

### The game crashes immediately after start

If your game crashes immediately, try disabling: *"Enable the Steam Overlay while in-game"* in game *Properties*.

If this doesn't work, you should check Steam's output for any error from the game. You may encounter the following:

*   munmap_chunk(): invalid pointer
*   free(): invalid pointer

In these particular cases, try replacing the libsteam_api.so file from the problematic game with one from a game that works fine. This error usually happens for games that were not updated recently when Steam runtime is disabled. This error has been encountered with at least AYIM, Bastion and Monaco.

### OpenGL not using direct rendering / Steam crashes Xorg

Sometimes presented with the error message "OpenGL GLX context is not using direct rendering, which may cause performance problems." [[1]](https://support.steampowered.com/kb_article.php?ref=9938-EYZB-7457)

If you still encounter this problem after addressing [#Steam runtime issues](#Steam_runtime_issues), you have probably not installed your 32-bit graphics driver correctly. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for which packages to install.

You can check/test if it is installed correctly by installing [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) and running the following command:

```
$ glxinfo32 | grep OpenGL.

```

### No audio in certain games

If there is no audio in certain games, and the suggestions provided in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") do not fix the problem, [#Using native runtime](#Using_native_runtime) may provide a successful workaround. (See the note about "Steam Runtime issues" at the top of this section.)

#### FMOD sound engine

While troubleshooting a sound issue, it became evident that the following games (as examples) use the 'FMOD' audio middleware package:

*   Hotline Miami
*   Hotline Miami 2
*   Transistor

This package is a bit buggy, and as a result while sound can appear to be working fine for the rest of your system, some games may still have problems.

It usually occurs when you have a default sound device set with ALSA, but you don't actually use that device, and have manually changed the device through other software, with me I had my default set as HDMI, but audio set through Steam/Gnome as S/PDIF.

To check what your default device is set as, use something like 'aplay' to output to your 'default' device, and see if you get sound, if you don't, your default is likely set to something that isn't even plugged in!

### Missing libc

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

### Missing libGL

You may encounter this error when you launch Steam at first time.

```
You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1

```

Make sure you have installed the `lib32` version of all your video drivers as described in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

If you get this error after reinstalling your Nvidia proprietary drivers, or switching from a version to another, [reinstall](/index.php/Reinstall "Reinstall") [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) and [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl).

### Games do not launch on older intel hardware

On older Intel hardware, if the game immediately crashes when run, it may be because your hardware does not directly support the latest OpenGL. It appears as a gameoverlayrenderer.so error in /tmp/dumps/mobile_stdout.txt, but looking in /tmp/gameoverlayrenderer.log it shows a GLXBadFBConfig error.

This can be fixed, however, by forcing the game to use a later version of OpenGL than it wants. Right click on the game, select Properties. Then, click "Set Launch Options" in the "General" tab and paste the following:

```
MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140 %command%

```

### 2k games do not run on xfs partitions

If you are running 2k games such as Civilization 5 on xfs partitions, then the game may not start or run properly due to how the game loads files as it starts. [[3]](https://bbs.archlinux.org/viewtopic.php?id=185222)

### Unable to add library folder because of missing execute permissions

If you add another steam library folder on another drive, you might receive the error message *"New Steam library folder must be on a filesystem mounted with execute permissions"*.

Make sure you are mounting the filesystem with the correct flags in your `/etc/fstab`, usually by adding `exec` to the list of mount parameter. The parameter must occur after any `user` or `users` parameter since these can imply `noexec`.

This error might also occur if you are readding a library folder and Steam is unable to find a contained `steamapps` folder. Previous versions used `SteamApps` instead, so ensure the name is fully lowercase.

### Steam controller not being detected correctly

See [Gamepad#Steam Controller](/index.php/Gamepad#Steam_Controller "Gamepad").

### VERSION_ID: unbound variable

In Steam's output, you may see the following line:

```
/home/user/.local/share/Steam/steam.sh: line 161: VERSION_ID: unbound variable

```

This is because steam.sh parses `/etc/os-release` and expects a VERSION_ID which Arch does not have. This error is unimportant but you can fix it by adding the following line to `/etc/os-release`:

```
VERSION_ID="2015.11.01"

```

### Steam hangs on "Installing breakpad exception handler..."

[BBS#177245](https://bbs.archlinux.org/viewtopic.php?id=177245)

Steam has the following output:

```
Running Steam on arch rolling 64-bit
STEAM_RUNTIME is enabled automatically
Installing breakpad exception handler for appid(steam)/version(0_client)

```

Then nothing else happens. This is likely related to mis-matched `lib32-nvidia-*` packages.

### 'GLBCXX_3.X.XX' not found when using Bumblebee

This error is likely caused because Steam packages its own out of date `libstdc++.so.6`. See [#Steam runtime issues](#Steam_runtime_issues) about working around the bad library. See also GitHub [issue 3773](https://github.com/ValveSoftware/steam-for-linux/issues/3773).