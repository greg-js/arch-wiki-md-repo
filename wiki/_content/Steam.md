# Steam

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Steam/Wine](/index.php/Steam/Wine "Steam/Wine")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")

From [Wikipedia](https://en.wikipedia.org/wiki/Steam_(software) "wikipedia:Steam (software)"):

_Steam is a digital distribution, digital rights management, multiplayer and communications platform developed by Valve Corporation. It is used to distribute games and related media online, from small independent developers to larger software houses._

[Steam](http://store.steampowered.com/about/) is best known as the platform needed to play Source Engine games (e.g. Half-Life 2, Counter-Strike). Today it offers many games from many other developers.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Steam](#Starting_Steam)
    *   [2.1 Big Picture Mode (with a Display Manager)](#Big_Picture_Mode_.28with_a_Display_Manager.29)
    *   [2.2 Silent Mode](#Silent_Mode)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Steam runtime issues](#Steam_runtime_issues)
    *   [3.2 Multiple monitors setup](#Multiple_monitors_setup)
    *   [3.3 Native runtime: steam.sh line 756 Segmentation fault](#Native_runtime:_steam.sh_line_756_Segmentation_fault)
    *   [3.4 The close button only minimizes the window](#The_close_button_only_minimizes_the_window)
    *   [3.5 Audio not working](#Audio_not_working)
    *   [3.6 Text is corrupt or missing](#Text_is_corrupt_or_missing)
    *   [3.7 SetLocale('en_US.UTF-8') fails at game startup](#SetLocale.28.27en_US.UTF-8.27.29_fails_at_game_startup)
    *   [3.8 The game crashes immediately after start](#The_game_crashes_immediately_after_start)
    *   [3.9 OpenGL not using direct rendering / Steam crashes Xorg](#OpenGL_not_using_direct_rendering_.2F_Steam_crashes_Xorg)
    *   [3.10 No audio in certain games](#No_audio_in_certain_games)
        *   [3.10.1 Some games use FMOD to obfuscate having to deal with Linux audio stack](#Some_games_use_FMOD_to_obfuscate_having_to_deal_with_Linux_audio_stack)
    *   [3.11 You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1](#You_are_missing_the_following_32-bit_libraries.2C_and_Steam_may_not_run:_libGL.so.1)
    *   [3.12 Games do not launch on older intel hardware](#Games_do_not_launch_on_older_intel_hardware)
    *   [3.13 Unable to add library folder because of missing execute permissions](#Unable_to_add_library_folder_because_of_missing_execute_permissions)
    *   [3.14 Steam controller not being detected correctly](#Steam_controller_not_being_detected_correctly)
    *   [3.15 Claims of missing 32-bit libc.so.6 even though lib32-glibc is installed](#Claims_of_missing_32-bit_libc.so.6_even_though_lib32-glibc_is_installed)
    *   [3.16 VERSION_ID: unbound variable](#VERSION_ID:_unbound_variable)
    *   [3.17 Steam hangs on "Installing breakpad exception handler..."](#Steam_hangs_on_.22Installing_breakpad_exception_handler....22)
*   [4 Launching games with custom commands, such as Bumblebee/Primus](#Launching_games_with_custom_commands.2C_such_as_Bumblebee.2FPrimus)
*   [5 Killing standalone compositors when launching games](#Killing_standalone_compositors_when_launching_games)
*   [6 Using native runtime](#Using_native_runtime)
*   [7 Skins for Steam](#Skins_for_Steam)
    *   [7.1 Steam skin manager](#Steam_skin_manager)
*   [8 Changing the Steam friends notification placement](#Changing_the_Steam_friends_notification_placement)
    *   [8.1 Use a skin](#Use_a_skin)
    *   [8.2 On The fly patch](#On_The_fly_patch)
*   [9 See also](#See_also)

## Installation

**Note:**

*   Arch Linux is **not** [officially supported](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366).
*   Because the Steam client is a 32-bit application, you will need to enable the [multilib](/index.php/Multilib "Multilib") repository if you have a 64-bit system. It may also make sense to install [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/) to provide some important multilib libraries.

To install Steam, [install](/index.php/Install "Install") the [steam](https://www.archlinux.org/packages/?name=steam) package. If you have a 64-bit system, enable the [multilib](/index.php/Multilib "Multilib") repository first.

Steam is not supported on this distribution. As such some fixes are needed on the users part to get things functioning properly:

*   Steam makes heavy usage of the Arial font. A decent Arial font to use is [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) or [the fonts provided by Steam](#Text_is_corrupt_or_missing). Asian languages require [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) to display properly.

*   **If you have a 64-bit system, you will need to install [the 32-bit version of your graphics driver](/index.php/Xorg#Driver_installation "Xorg") (the package in the _Multilib Package_ column) to run 32-bit games**.

*   If you have a 64-bit system, you will need to install [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) to enable sound in 32-bit games.

*   Several games have dependencies which may be missing from your system. If a game fails to launch (often without error messages) then make sure all of the libraries listed in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") are installed.

## Starting Steam

### Big Picture Mode (with a Display Manager)

To start Steam in Big Picture Mode from a Display Manager (such as LightDM), create a `/usr/share/xsessions/steam-big-picture.desktop` file with the following content:

 `/usr/share/xsessions/steam-big-picture.desktop` 

```
[Desktop Entry]
Name=Steam Big Picture Mode
Comment=Start Steam in Big Picture Mode
Exec=/usr/bin/steam -bigpicture
TryExec=/usr/bin/steam
Icon=
Type=Application
```

Alternatively, under Steam > Settings > Interface, check 'Start Steam in Big Picture Mode' and start Steam normally. This can behave slightly better with certain window managers than the command line option.

### Silent Mode

If your steam main window is showing at startup, you can add the `-silent` parameter to your startup command to hide the window:

```
/usr/bin/steam -silent %U

```

alternatively, you can edit the following desktop file, and manually add the parameter:

 `~/.config/autostart/steam.desktop` 

```
[Desktop Entry]
Name=Steam
Comment=Application for managing and playing games on Steam
Exec=/usr/bin/steam -silent %U
Icon=steam
Terminal=false
Type=Application
Categories=Network;FileTransfer;Game;
MimeType=x-scheme-handler/steam;
Actions=Store;Community;Library;Servers;Screenshots;News;Settings;BigPicture;Friends;
...
```

## Troubleshooting

**Note:** In addition to being documented here, any bug/fix/error should be, if not already, reported on Valve's bug tracker on their [GitHub page](https://github.com/ValveSoftware/steam-for-linux).

### Steam runtime issues

[Upstream GitHub issue tracker](https://github.com/ValveSoftware/steam-runtime/issues/13)

Steam ships with its own versions of some libraries (the "Steam Runtime") in an attempt to emulate the Ubuntu 12.04 environment in later versions of Ubuntu.

However, some core libraries included in the Steam Runtime will often conflict with the newer versions of other libraries included in Arch Linux (such as drivers, and specifically the open-source [ATI](/index.php/ATI "ATI") driver).

You can work around this by deleting the Steam Runtime versions of these libraries, forcing Steam to fall back to the up-to-date system versions (the ones installed by [pacman](/index.php/Pacman "Pacman")).

Note that Steam will frequently re-install these runtime libraries when Steam is updated, so until [ValveSoftware/steam-runtime#13](https://github.com/ValveSoftware/steam-runtime/issues/13) is resolved, whenever Steam updates, you should exit, remove the libraries, and restart it again.

Run this command to remove the runtime libraries known to cause issues on Arch Linux:

```
find ~/.steam/root/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" \) -print -delete

```

If the above command does not work, run the above command again, then run this command.

```
find ~/.local/share/Steam/ \( -name "libgcc_s.so*" -o -name "libstdc++.so*" -o -name "libxcb.so*" \) -print -delete

```

Alternatively you can run steam overriding those libraries.

```
LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' steam

```

If you wish to use this method in a .desktop shortcut, you can use this command in the **Exec=** field.

```
env LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' /usr/bin/steam %U

```

If you wish to restore the files that were deleted by the commands above, you can use the built-in steam reset functionality.

```
steam --reset

```

Examples of issues / error messages known to occur if these libraries are present:

*   `Failed to load libGL: undefined symbol: xcb_send_fd`
*   `ERROR: ld.so: object '~/.local/share/Steam/ubuntu12_32/gameoverlayrenderer.so' from LD_PRELOAD cannot be preloaded (wrong ELF class: ELFCLASS32): ignored.`
*   Problems with 64-bit games like XCOM
*   "OpenGL GLX context is not using direct rendering, which may cause performance problems." [(see below)](#OpenGL_not_using_direct_rendering_.2F_Steam_crashes_Xorg)
*   "Could not find required OpenGL entry point 'glGetError'! Either your video card is unsupported or your OpenGL driver needs to be updated."
*   The Steam client itself crashing

A misconfigured firewall may also show up as a runtime issue, because Steam silently fails whenever it can't connect to its servers, and most games just crash whenever the Steam API fails to load.

Forum threads:

*   [https://bbs.archlinux.org/viewtopic.php?id=181171](https://bbs.archlinux.org/viewtopic.php?id=181171)
*   [https://bbs.archlinux.org/viewtopic.php?id=183141](https://bbs.archlinux.org/viewtopic.php?id=183141)

See also [#Using native runtime](#Using_native_runtime) below.

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

### The close button only minimizes the window

Valve GitHub [issue 1025](https://github.com/ValveSoftware/steam-for-linux/issues/1025)

To close the Steam window (and remove it from the taskbar) when you press **x**, but keep Steam running in the tray, export the environment variable `STEAM_FRAME_FORCE_CLOSE=1`. See [Environment variables#Graphical applications](/index.php/Environment_variables#Graphical_applications "Environment variables").

Steam provides a script located at `/usr/bin/steam` that will be run when launching Steam; adding `export STEAM_FRAME_FORCE_CLOSE=1` to this file will export the environment variable for Steam on application launch.

### Audio not working

First try to install [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) and if you run a x86_64 system [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins).

If you do not have audio in the videos which play within the Steam client, it is possible that the ALSA libs packaged with Steam are not working.

If launching Steam from a terminal and attempting to playback a video within the steam client results in an error similar to the following:

```
ALSA lib pcm_dmix.c:1018:(snd_pcm_dmix_open) unable to open slave

```

There is a workaround which involves renaming or deleting some Steam Runtime folders and library files. The bugs have already been reported here: [#3376](https://github.com/ValveSoftware/steam-for-linux/issues/3376) and [#3504](https://github.com/ValveSoftware/steam-for-linux/issues/3504)

The solution is to rename or delete the `alsa-lib` folder and the `libasound.so.*` files. They can be found within `~/.steam/steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/` 

As an alternative, these `libasound.so.*` libraries can also be prepended to the **LD_PRELOAD** environment variable to fix this issue:

 `LD_PRELOAD="/usr/lib/libasound.so.2:/usr/lib32/libasound.so.2:${LD_PRELOAD}" steam` 

### Text is corrupt or missing

The Steam Support [instructions](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) for Windows seem to work on Linux also.

You can install them via the [steam-fonts](https://aur.archlinux.org/packages/steam-fonts/)<sup><small>AUR</small></sup> package, or manually by downloading and [installing](/index.php/Fonts#Manual_installation "Fonts") [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip).

**Note:** When steam cannot find the Arial fonts, font-config likes to fall back onto the Helveticia bitmap font. Steam does not render this and possibly other bitmap fonts correctly, so either removing problem fonts or [disabling bitmap fonts](/index.php/Font_configuration#Disable_bitmap_fonts "Font configuration") will most likely fix the issue without installing the Arial or ArialBold fonts. The font being used in place of Arial can be found with the command `$ fc-match -v Arial` 

### SetLocale('en_US.UTF-8') fails at game startup

Uncomment `en_US.UTF-8 UTF-8` in `/etc/locale.gen` and then run `locale-gen` as root.

### The game crashes immediately after start

If your game crashes immediately, try disabling: _"Enable the Steam Overlay while in-game"_ in game _Properties_.

### OpenGL not using direct rendering / Steam crashes Xorg

Sometimes presented with the error message "OpenGL GLX context is not using direct rendering, which may cause performance problems." [[1]](https://support.steampowered.com/kb_article.php?ref=9938-EYZB-7457)

If you still encounter this problem after addressing [#Steam runtime issues](#Steam_runtime_issues), you have probably not installed your 32-bit graphics driver correctly. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for which packages to install.

You can check/test if it is installed correctly by installing [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) and running the following command:

```
$ glxinfo32 | grep OpenGL.

```

### No audio in certain games

If there is no audio in certain games, and the suggestions provided in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") do not fix the problem, [#Using native runtime](#Using_native_runtime) may provide a successful workaround. (See the note about "Steam Runtime issues" at the top of this section.)

#### Some games use FMOD to obfuscate having to deal with Linux audio stack

While troubleshooting a sound issue, it became evident that the following games (as examples) use the 'FMOD' audio middleware package:

*   Hotline Miami
*   Hotline Miami 2
*   Transistor

This package is a bit buggy, and as a result while sound can appear to be working fine for the rest of your system, some games may still have problems.

It usually occurs when you have a default sound device set with ALSA, but you don't actually use that device, and have manually changed the device through other software, with me I had my default set as HDMI, but audio set through Steam/Gnome as S/PDIF.

To check what your default device is set as, use something like 'aplay' to output to your 'default' device, and see if you get sound, if you don't, your default is likely set to something that isn't even plugged in!

### You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1

You may encounter this error when you launch Steam at first time. Make sure you have installed the `lib32` version of all your video drivers as described in [#Installation](#Installation)

In some cases, if you get this error after reinstalling your Nvidia proprietary drivers, or switching from a version to another, [reinstall](/index.php/Reinstall "Reinstall") [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) and [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl).

### Games do not launch on older intel hardware

On older Intel hardware, if the game immediately crashes when run, it may be because your hardware does not directly support the latest OpenGL. It appears as a gameoverlayrenderer.so error in /tmp/dumps/mobile_stdout.txt, but looking in /tmp/gameoverlayrenderer.log it shows a GLXBadFBConfig error.

This can be fixed, however, by forcing the game to use a later version of OpenGL than it wants. Right click on the game, select Properties. Then, click "Set Launch Options" in the "General" tab and paste the following:

```
MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140 %command%

```

### Unable to add library folder because of missing execute permissions

If you add another steam library folder on another drive, you might receive the error message _"New Steam library folder must be on a filesystem mounted with execute permissions"_.

Make you sure you are mounting the filesystem with the correct flags in your `/etc/fstab`, usually by adding `exec` to the list of mount parameter. The parameter must occur after any `user` or `users` parameter since these can imply `noexec`.

This error might also occur if you are readding a library folder and Steam is unable to find a contained `steamapps` folder. Previous versions used `SteamApps` instead, so ensure the name is fully lowercase.

### Steam controller not being detected correctly

See [Gamepad#Steam Controller](/index.php/Gamepad#Steam_Controller "Gamepad").

### Claims of missing 32-bit libc.so.6 even though lib32-glibc is installed

The Steam launcher script checks the output of `ldd` to determine whether all required libraries are installed; however, this may fail due to reasons other than missing libraries, such as a corrupt Steam executable.

Check the output of the following:

```
$ ldd ~/.local/share/Steam/ubuntu12_32/steam

```

Should `ldd` claim that it is not a dynamic executable, then Steam likely corrupted the binary during an update. The following should fix the issue:

```
$ cd ~/.local/share/Steam/
$ ./steam.sh --reset

```

If it doesn't, try to delete the `~/.local/share/Steam/` directory and launch steam again, telling it to reinstall itself.

### VERSION_ID: unbound variable

When you launch steam via terminal, you can see the following line:

```
/home/user/.local/share/Steam/steam.sh: line 161: VERSION_ID: unbound variable

```

This is because steam.sh checks `/etc/os-release` for existance and if it exists, parses VERSION_ID variable, which is missing. To solve problem, you can just add the following line to `/etc/os-release`:

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

## Launching games with custom commands, such as Bumblebee/Primus

Steam has fortunately added support for launching games using your own custom command. To do so, navigate to the Library page, right click on the selected game, click Properties, and Set Launch Options. Steam replaces the tag `%command%` with the command it actually wishes to run. For example, to launch Team Fortress 2 with primusrun and at resolution 1920x1080, you would enter:

```
primusrun %command% -w 1920 -h 1080

```

On some systems optirun gives better performances than primusrun, however some games may crash shortly after the launch. This may be fixed preloading the correct version of libGL. Use:

```
locate libGL

```

to find out the available implementations. For a 64 bits game you may want to preload the nvidia 64 bits libGL, then use the launch command:

```
LD_PRELOAD=/usr/lib/nvidia/libGL.so optirun %command%

```

If you are running the [Linux-ck](/index.php/Linux-ck "Linux-ck") kernel, you may have some success in reducing overall latencies and improving performance by launching the game in SCHED_ISO (low latency, avoid choking CPU) via [schedtool](https://www.archlinux.org/packages/?name=schedtool)

```
# schedtool -I -e %command% _other arguments_

```

Also keep in mind that Steam [doesn't really care](http://i.imgur.com/oJcLDBi.png) what you want it to run. By setting `%command%` to an environment variable, you can have Steam run whatever you would like. For example, the Launch Option used in the image above:

```
IGNORE_ME=%command% glxgears

```

## Killing standalone compositors when launching games

Further to this, utilising the `%command%` switch, you can kill standalone compositors (such as Xcompmgr or [Compton](/index.php/Compton "Compton")) - which can cause lag and tearing in some games on some systems - and relaunch them after the game ends by adding the following to your game's launch options.

```
 killall compton && %command%; nohup compton &

```

Replace `compton` in the above command with whatever your compositor is. You can also add -options to `%command%` or `compton`, of course.

Steam will latch on to any processes launched after `%command%` and your Steam status will show as in game. So in this example, we run the compositor through `nohup` so it is not attached to Steam (it will keep running if you close Steam) and follow it with an ampersand so that the line of commands ends, clearing your Steam status.

## Using native runtime

Steam, by default, ships with a copy of every library it uses, packaged within itself, so that games can launch without issue. This can be a resource hog, and the slightly out-of-date libraries they package may be missing important features (Notably, the OpenAL version they ship lacks [HRTF](/index.php/Gaming#Binaural_Audio_with_OpenAL "Gaming") and surround71 support). To use your own system libraries, you can run Steam with:

```
$ STEAM_RUNTIME=0 steam

```

However, if you are missing any libraries Steam makes use of, this will fail to launch properly. An easy way to find the missing libraries is to run the following commands:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ LD_LIBRARY_PATH=".:${LD_LIBRARY_PATH}" ldd $(file *|sed '/ELF/!d;s/:.*//g')|grep 'not found'|sort|uniq

```

**Note:** The libraries will have to be 32-bit, which means you may have to download some from the AUR if on x86_64, such as NetworkManager.

Once you have done this, run steam again with `STEAM_RUNTIME=0 steam` and verify it is not loading anything outside of the handful of steam support libraries:

```
$ < /proc/$(pidof steam)/maps|sed '/\.local/!d;s/.*  //g'|sort|uniq

```

**Convenience repository**

The unofficial [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repository contains all libraries needed to run native steam on x86_64\. Please note that, for some reason, steam does not pick up sdl2 or libav* even if you have them installed. It will still use the ones it ships with.

All you need to install is the meta-package `steam-libs`, it will pull all the libs for you. Please report if there is any missing library, the maintainer already had some lib32 packages installed so a library may have been overlooked.

## Skins for Steam

**Note:** Using skins that are not up-to-date with the version of the Steam client may cause visual errors.

The Steam interface can be fully customized by copying its various interface files in its skins directory and modifying them.

An extensive list of skins can be found on [Steam's forums](http://forums.steampowered.com/forums/showthread.php?t=1161035).

### Steam skin manager

The process of applying a skin to Steam can be greatly simplified by installing the [steam-skin-manager](https://aur.archlinux.org/packages/steam-skin-manager/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/steam-skin-manager)]</sup> package. The package also comes with a hacked version of the Steam launcher which allows the window manager to draw its borders on the Steam window.

As a result, skins for Steam will come in two flavors, one with and one without window buttons. The skin manager will prompt you whether you use the hacked version or not, and will automatically apply the theme corresponding to your GTK+ theme if it is found. You can of course still apply another skin if you want.

The package ships with two themes for the default Ubuntu themes, Ambiance and Radiance.

## Changing the Steam friends notification placement

**Note:** A handful of games do not support this, for example this can not work with XCOM: Enemy Unknown.

### Use a skin

You can create a skin that does nothing but change the notification corner. First you need to create the directories:

```
 $ mkdir -p $HOME/Top-Right/resource
 $ cp -R $HOME/.steam/steam/resource/styles $HOME/Top-Right/resource/
 $ mv $HOME/Top-Right $HOME/.local/share/Steam/skins/
 $ cd .local/share/Steam/skins/
 $ cp -R Top-Right Top-Left && cp -R Top-Right Bottom-Right

```

Then modify the correct files. `Top-Right/resource/styles/gameoverlay.style` will change the corner for the in-game overlay whereas `steam.style` will change it for your desktop.

Now find the entry: `Notifications.PanelPosition` in whichever file you opened and change it to the appropriate value, for example for Top-Right:

```
 Notifications.PanelPosition     "TopRight"

```

This line will look the same in both files. Repeat the process for all the 3 variants (`Top-Right`, `Top-Left` and `Bottom-Left`) and adjust the corners for the desktop and in-game overlay to your satisfaction for each skin, then save the files.

To finish you will have to select the skin in Steam: _Settings > Interface_ and _<default skin>_ in the drop-down menu.

You can use these files across distributions and even between Windows and Linux (OS X has its own entry for the desktop notification placement)

### On The fly patch

This method is more compatible with future updates of Steams since the files in the skins above are updated as part of steam and as such if the original files change, the skin will not follow the graphics update to steam and will have to be re-created every time something like that happens. Doing things this way will also give you the ability to use per-game notification locations as you can run a patch changing the location of the notifications by specifying it in the launch options for games.

Steam updates the files we need to edit everytime it updates (which is everytime it is launched) so the most effective way to do this is patching the file after Steam has already been launched.

First you will need a patch:

 `$HOME/.steam/topright.patch` 

```
--- A/steam/resource/styles/gameoverlay.styles	2013-06-14 23:49:36.000000000 +0000
+++ B/steam/resource/styles/gameoverlay.styles	2014-07-08 23:13:15.255806000 +0000
@@ -7,7 +7,7 @@
 		mostly_black "0 0 0 240"
 		semi_black "0 0 0 128"
 		semi_gray "32 32 32 220"
-		Notifications.PanelPosition     "BottomRight"
+		Notifications.PanelPosition     "TopRight"
 	}

 	styles

```

**Note:** The patch file should have all above lines, including the newline at the end.

You can edit the entry and change it between "BottomRight"(default), "TopRight" "TopLeft" and "BottomLeft": the following will assume you used "TopRight" as in the original file.

Next create an alias in `$HOME/.bashrc`:

```
 alias steam_topright='pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd'

```

Log out and back in to refresh the aliases. Launch Steam and wait for it to fully load, then run the alias

```
 $ steam_topright

```

And most games you launch after this will have their notification in the upper right corner.

You can also duplicate the patch and make more aliases for the other corners if you do not want all games to use the same corner so you can switch back.

To automate the process you will need a script file as steam launch options cannot read your aliases. The location and name of the file could for example be **$HOME/.scripts/steam_topright.sh**, and assuming that is the path you used, it needs to be executable:

```
 $ chmod +755 $HOME/.scripts/steam_topright.sh

```

The contents of the file should be the following:

```
 #!/bin/sh
 pushd $HOME/.steam/ && patch -p1 -f -r - --no-backup-if-mismatch < topright.patch && popd

```

And the launch options should be something like the following.

```
 $HOME/.scripts/steam_topright.sh && %command%

```

There is another file in the same folder as **gameoverlay.style** folder called **steam.style** which has an entry with the exact same function as the file we patched and will change the notification corner for the desktop only (not in-game), but for editing this file to actually work it has to be set before steam is launched and the folder set to read-only so steam cannot re-write the file. Therefore the only two ways to modify that file is to make the directory read only so steam cannot change it when it is launched (can break updates) or making a skin like in method 1.

## See also

*   [https://wiki.gentoo.org/wiki/Steam](https://wiki.gentoo.org/wiki/Steam)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Steam&oldid=414877](https://wiki.archlinux.org/index.php?title=Steam&oldid=414877)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")