See [Steam](/index.php/Steam "Steam") for the main article, and [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting") for generic troubleshooting.

**Note:** [Steam](/index.php/Steam "Steam") installs library dependencies of a game to a library directory, but some are missing at the moment. Report bugs involving missing libraries on Valve's bug tracker on their [GitHub page](https://github.com/ValveSoftware/steam-for-linux) before adding workarounds here, and then provide a link to the bug so it can be removed as the problems are fixed.

**Tip:** If a game fails to start, a possible reason is that it is missing required libraries. You can find out what libraries it requests by running `ldd *game_executable*`. `*game_executable*` is likely located somewhere in `~/.steam/root/steamapps/common/`. Please note that most of these "missing" libraries are actually already included with Steam, and do not need to be installed globally.

## Contents

*   [1 Common steps](#Common_steps)
    *   [1.1 Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH)
    *   [1.2 OpenSSL 1.0 setup](#OpenSSL_1.0_setup)
    *   [1.3 Adobe Air setup](#Adobe_Air_setup)
*   [2 Alien Isolation](#Alien_Isolation)
*   [3 Amnesia: The Dark Descent](#Amnesia:_The_Dark_Descent)
*   [4 And Yet It Moves](#And_Yet_It_Moves)
    *   [4.1 Game does not start](#Game_does_not_start)
*   [5 Anodyne](#Anodyne)
    *   [5.1 Play with a controller: joy2key configuration](#Play_with_a_controller:_joy2key_configuration)
*   [6 Aquaria](#Aquaria)
    *   [6.1 Mouse pointer gets stuck in one direction](#Mouse_pointer_gets_stuck_in_one_direction)
*   [7 ARK: Survival Evolved](#ARK:_Survival_Evolved)
    *   [7.1 Game does not start, displays text window with unreadable text](#Game_does_not_start.2C_displays_text_window_with_unreadable_text)
*   [8 Audiosurf 2](#Audiosurf_2)
*   [9 Binding of Isaac: Rebirth](#Binding_of_Isaac:_Rebirth)
    *   [9.1 No sound](#No_sound)
*   [10 The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales)
*   [11 The Book of Unwritten Tales: The Critter Chronicles](#The_Book_of_Unwritten_Tales:_The_Critter_Chronicles)
*   [12 Borderlands 2](#Borderlands_2)
    *   [12.1 Migrating saves from other platforms](#Migrating_saves_from_other_platforms)
    *   [12.2 Using Ctrl Key](#Using_Ctrl_Key)
    *   [12.3 Logging into SHiFT](#Logging_into_SHiFT)
    *   [12.4 Game crashes nearly instantly](#Game_crashes_nearly_instantly)
*   [13 Borderlands: The Pre-Sequel](#Borderlands:_The_Pre-Sequel)
    *   [13.1 Keyboard not working](#Keyboard_not_working)
    *   [13.2 Not starting via Steam](#Not_starting_via_Steam)
    *   [13.3 Game crashes nearly instantly](#Game_crashes_nearly_instantly_2)
*   [14 Cities in Motion 2](#Cities_in_Motion_2)
    *   [14.1 Dialog boxes fail to display properly](#Dialog_boxes_fail_to_display_properly)
*   [15 Cities Skylines](#Cities_Skylines)
    *   [15.1 Textures not rendering properly](#Textures_not_rendering_properly)
*   [16 Civilization V](#Civilization_V)
    *   [16.1 Stuttering sound with PulseAudio](#Stuttering_sound_with_PulseAudio)
*   [17 Civilization: Beyond earth](#Civilization:_Beyond_earth)
*   [18 Civilization VI](#Civilization_VI)
*   [19 Deus Ex: Mankind divided](#Deus_Ex:_Mankind_divided)
*   [20 The Clockwork Man](#The_Clockwork_Man)
*   [21 Company of Heroes 2](#Company_of_Heroes_2)
*   [22 Counter-Strike: Global Offensive (CS:GO)](#Counter-Strike:_Global_Offensive_.28CS:GO.29)
    *   [22.1 Game starts on the wrong screen](#Game_starts_on_the_wrong_screen)
    *   [22.2 Cannot reach bottom of the screen on menus](#Cannot_reach_bottom_of_the_screen_on_menus)
    *   [22.3 Sound is played slightly delayed](#Sound_is_played_slightly_delayed)
    *   [22.4 Mouse not working in-game](#Mouse_not_working_in-game)
    *   [22.5 Brightness slider not working](#Brightness_slider_not_working)
    *   [22.6 Microphone not working](#Microphone_not_working)
*   [23 Crusader Kings II](#Crusader_Kings_II)
    *   [23.1 Locations](#Locations)
    *   [23.2 No audio](#No_audio)
    *   [23.3 Oddly sized starting window](#Oddly_sized_starting_window)
*   [24 Death Road To Canada](#Death_Road_To_Canada)
    *   [24.1 No music](#No_music)
*   [25 Defender's Quest: Valley of the Forgotten](#Defender.27s_Quest:_Valley_of_the_Forgotten)
*   [26 Dirt](#Dirt)
*   [27 Divinity: Original Sin - Enhanced Edition](#Divinity:_Original_Sin_-_Enhanced_Edition)
    *   [27.1 Game doesn't start when using Bumblebee optirun or primusrun](#Game_doesn.27t_start_when_using_Bumblebee_optirun_or_primusrun)
*   [28 Don't Starve](#Don.27t_Starve)
    *   [28.1 No sound](#No_sound_2)
*   [29 Dota 2](#Dota_2)
    *   [29.1 In-game font is unreadable](#In-game_font_is_unreadable)
    *   [29.2 The game does not start](#The_game_does_not_start)
    *   [29.3 Game runs on the wrong screen](#Game_runs_on_the_wrong_screen)
    *   [29.4 Game does not start with libxcb-dri3 error message](#Game_does_not_start_with_libxcb-dri3_error_message)
    *   [29.5 Steam overlay](#Steam_overlay)
    *   [29.6 Chinese tips and player names not shown](#Chinese_tips_and_player_names_not_shown)
    *   [29.7 Chinese input method problem](#Chinese_input_method_problem)
*   [30 Drox Operative](#Drox_Operative)
*   [31 Dwarfs F2P](#Dwarfs_F2P)
    *   [31.1 Game does not start](#Game_does_not_start_2)
    *   [31.2 Game crashes](#Game_crashes)
*   [32 Dynamite Jack](#Dynamite_Jack)
    *   [32.1 Sound Issues](#Sound_Issues)
    *   [32.2 Game does not start](#Game_does_not_start_3)
*   [33 Euro Truck Simulator 2](#Euro_Truck_Simulator_2)
    *   [33.1 Shows only a black screen](#Shows_only_a_black_screen)
*   [34 Football Manager 2014](#Football_Manager_2014)
*   [35 FORCED](#FORCED)
*   [36 FTL: Faster than Light](#FTL:_Faster_than_Light)
    *   [36.1 Compatibility](#Compatibility)
    *   [36.2 Problems with open-source video driver](#Problems_with_open-source_video_driver)
*   [37 Game Dev Tycoon](#Game_Dev_Tycoon)
    *   [37.1 Game does not start](#Game_does_not_start_4)
*   [38 Garry's Mod](#Garry.27s_Mod)
    *   [38.1 Game does not start](#Game_does_not_start_5)
    *   [38.2 Opening some menus causes the game to crash](#Opening_some_menus_causes_the_game_to_crash)
    *   [38.3 Game crashes after attempting to join server](#Game_crashes_after_attempting_to_join_server)
*   [39 Gods will be watching](#Gods_will_be_watching)
*   [40 GRID Autosport](#GRID_Autosport)
    *   [40.1 Black screen when trying to play](#Black_screen_when_trying_to_play)
*   [41 Hack 'n' Slash](#Hack_.27n.27_Slash)
    *   [41.1 Crashes when trying to load a game](#Crashes_when_trying_to_load_a_game)
*   [42 Hacker Evolution](#Hacker_Evolution)
*   [43 Half-Life 2 and episodes](#Half-Life_2_and_episodes)
    *   [43.1 Cyrillic fonts problem](#Cyrillic_fonts_problem)
*   [44 Hammerwatch](#Hammerwatch)
    *   [44.1 The game does not start via Steam](#The_game_does_not_start_via_Steam)
    *   [44.2 No sound](#No_sound_3)
*   [45 Halo: Custom Edition](#Halo:_Custom_Edition)
*   [46 Harvest: Massive Encounter](#Harvest:_Massive_Encounter)
    *   [46.1 Compatibility](#Compatibility_2)
*   [47 Hatoful Boyfriend](#Hatoful_Boyfriend)
    *   [47.1 Japanese text invisible](#Japanese_text_invisible)
*   [48 Hyper Light Drifter](#Hyper_Light_Drifter)
    *   [48.1 The controller does not work](#The_controller_does_not_work)
    *   [48.2 Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found)
*   [49 The Impossible Game](#The_Impossible_Game)
*   [50 The Inner World](#The_Inner_World)
    *   [50.1 Bringing up the inventory or main menu](#Bringing_up_the_inventory_or_main_menu)
        *   [50.1.1 Cutscenes](#Cutscenes)
*   [51 Interloper](#Interloper)
    *   [51.1 Game does not start](#Game_does_not_start_6)
*   [52 Invisible Apartment](#Invisible_Apartment)
    *   [52.1 Game does not start](#Game_does_not_start_7)
*   [53 Joe Danger 2: The Movie](#Joe_Danger_2:_The_Movie)
    *   [53.1 Compatibility](#Compatibility_3)
*   [54 Kerbal Space Program](#Kerbal_Space_Program)
*   [55 Killing Floor](#Killing_Floor)
    *   [55.1 Cannot change screen resolution](#Cannot_change_screen_resolution)
    *   [55.2 Windowed mode](#Windowed_mode)
    *   [55.3 Stuttering sound](#Stuttering_sound)
*   [56 Lethal League](#Lethal_League)
*   [57 Life is Strange](#Life_is_Strange)
*   [58 Mark of the Ninja](#Mark_of_the_Ninja)
    *   [58.1 Bad sound](#Bad_sound)
*   [59 Metro: Last Light](#Metro:_Last_Light)
*   [60 Middle-earth: Shadow of Mordor](#Middle-earth:_Shadow_of_Mordor)
    *   [60.1 Floating heads](#Floating_heads)
*   [61 Multiwinia](#Multiwinia)
    *   [61.1 Crash on startup](#Crash_on_startup)
*   [62 Natural Selection 2](#Natural_Selection_2)
    *   [62.1 No Sound](#No_Sound_4)
*   [63 Nuclear Throne](#Nuclear_Throne)
    *   [63.1 Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found_2)
*   [64 Penumbra: Overture](#Penumbra:_Overture)
    *   [64.1 Windowed mode](#Windowed_mode_2)
*   [65 The Polynomial](#The_Polynomial)
    *   [65.1 Segfaults during program start on 64-bit systems](#Segfaults_during_program_start_on_64-bit_systems)
*   [66 Portal 2](#Portal_2)
    *   [66.1 Game does not start](#Game_does_not_start_8)
    *   [66.2 Resolution too low](#Resolution_too_low)
*   [67 Prison Architect](#Prison_Architect)
    *   [67.1 ALSA error when using PulseAudio](#ALSA_error_when_using_PulseAudio)
*   [68 Project Zomboid](#Project_Zomboid)
    *   [68.1 No sound](#No_sound_5)
*   [69 Redshirt](#Redshirt)
*   [70 Revenge of the Titans](#Revenge_of_the_Titans)
*   [71 Rock Boshers DX: Directors Cut](#Rock_Boshers_DX:_Directors_Cut)
*   [72 Saints Row IV](#Saints_Row_IV)
    *   [72.1 Game fails to launch after update to new Nvidia drivers](#Game_fails_to_launch_after_update_to_new_Nvidia_drivers)
    *   [72.2 Game causes GPU lockup with mesa drivers](#Game_causes_GPU_lockup_with_mesa_drivers)
*   [73 Serious Sam 3: BFE](#Serious_Sam_3:_BFE)
    *   [73.1 No audio](#No_audio_2)
*   [74 Space Pirates and Zombies](#Space_Pirates_and_Zombies)
    *   [74.1 No audio](#No_audio_3)
*   [75 Spacechem](#Spacechem)
    *   [75.1 Game crash](#Game_crash)
*   [76 Splice](#Splice)
*   [77 Star Wars Battlefront II](#Star_Wars_Battlefront_II)
*   [78 The Stanley Parable](#The_Stanley_Parable)
    *   [78.1 Game won't start](#Game_won.27t_start)
*   [79 Shadow Tactics: Blades of the Shogun](#Shadow_Tactics:_Blades_of_the_Shogun)
*   [80 Steel Storm: Burning Retribution](#Steel_Storm:_Burning_Retribution)
    *   [80.1 Start with black screen](#Start_with_black_screen)
    *   [80.2 No English fonts](#No_English_fonts)
*   [81 Stephen's Sausage Roll](#Stephen.27s_Sausage_Roll)
    *   [81.1 No sound](#No_sound_6)
*   [82 Superbrothers: Sword & Sworcery EP](#Superbrothers:_Sword_.26_Sworcery_EP)
*   [83 Tabletop Simulator](#Tabletop_Simulator)
    *   [83.1 CJK characters not showing in game](#CJK_characters_not_showing_in_game)
*   [84 Team Fortress 2](#Team_Fortress_2)
    *   [84.1 HRTF setup](#HRTF_setup)
    *   [84.2 Loading screen freeze](#Loading_screen_freeze)
    *   [84.3 No audio](#No_audio_4)
    *   [84.4 Slow loading textures](#Slow_loading_textures)
*   [85 Terraria](#Terraria)
*   [86 This War of Mine](#This_War_of_Mine)
    *   [86.1 Game does not start](#Game_does_not_start_9)
    *   [86.2 Sound glitches with Steam native](#Sound_glitches_with_Steam_native)
*   [87 Ticket to Ride](#Ticket_to_Ride)
*   [88 Tomb Raider](#Tomb_Raider)
    *   [88.1 Game immediately closes when running with steam-native](#Game_immediately_closes_when_running_with_steam-native)
    *   [88.2 Steam Controller not working in-game](#Steam_Controller_not_working_in-game)
*   [89 Towns / Towns Demo](#Towns_.2F_Towns_Demo)
*   [90 Transistor](#Transistor)
    *   [90.1 Crash on launch / FMOD binding crash / Audio issues](#Crash_on_launch_.2F_FMOD_binding_crash_.2F_Audio_issues)
*   [91 Transmissions: Element 120](#Transmissions:_Element_120)
    *   [91.1 Troubleshooting](#Troubleshooting)
*   [92 Trine 2](#Trine_2)
    *   [92.1 Colors](#Colors)
    *   [92.2 Sound](#Sound)
    *   [92.3 Resolution](#Resolution)
*   [93 Tropico 5](#Tropico_5)
    *   [93.1 Blank screen with sound only on startup](#Blank_screen_with_sound_only_on_startup)
*   [94 Unity of Command](#Unity_of_Command)
    *   [94.1 Squares](#Squares)
    *   [94.2 No audio](#No_audio_5)
*   [95 Unity3D](#Unity3D)
    *   [95.1 Locale settings](#Locale_settings)
    *   [95.2 Unity 5 sound problems](#Unity_5_sound_problems)
    *   [95.3 Game launching on wrong monitor in fullscreen mode](#Game_launching_on_wrong_monitor_in_fullscreen_mode)
*   [96 Unrest](#Unrest)
*   [97 War Thunder](#War_Thunder)
    *   [97.1 No audio](#No_audio_6)
    *   [97.2 Blank screen](#Blank_screen)
*   [98 Warhammer 40,000: Dawn of War II](#Warhammer_40.2C000:_Dawn_of_War_II)
*   [99 Witcher 2: Assassin of Kings](#Witcher_2:_Assassin_of_Kings)
    *   [99.1 Game does not start](#Game_does_not_start_10)
*   [100 Wizardry 6: Bane of the Cosmic Forge](#Wizardry_6:_Bane_of_the_Cosmic_Forge)
*   [101 World of Goo](#World_of_Goo)
    *   [101.1 Changing resolution](#Changing_resolution)
*   [102 XCOM](#XCOM)
    *   [102.1 Hangs on startup](#Hangs_on_startup)
    *   [102.2 Graphical glitches on Intel HD](#Graphical_glitches_on_Intel_HD)
*   [103 Tower Unite](#Tower_Unite)
    *   [103.1 Graphical Glitches](#Graphical_Glitches)

## Common steps

### Prepend /usr/lib to LD_LIBRARY_PATH

Add `LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH"` to your [launch options](/index.php/Steam#Launch_options "Steam").

### OpenSSL 1.0 setup

Some Steam games are built against OpenSSL 1.0\. [[1]](https://bugs.archlinux.org/task/53618)

Install [libopenssl-1.0-compat](https://aur.archlinux.org/packages/libopenssl-1.0-compat/) and add `LD_LIBRARY_PATH=/usr/lib/openssl-1.0-compat` to your [launch options](/index.php/Steam#Launch_options "Steam").

### Adobe Air setup

The package [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/) installs Adobe Air not in the place where the game expects it to be, fix this by creating the following symlink:

```
# ln -s "/opt/adobe-air-sdk/runtimes/air/linux/Adobe AIR" "/opt/Adobe AIR"

```

Adobe AIR requires you to accept its EULA:

```
$ mkdir -p ~/.appdata/Adobe/AIR
$ echo 2 > ~/.appdata/Adobe/AIR/eulaAccepted

```

## Alien Isolation

Symlink `/usr/lib/libpcre.so` to `*gamedir*/lib/x86_64/libpcre.so.3`, otherwise the game will fail to start.

## Amnesia: The Dark Descent

Dependencies:

*   [lib32-freealut](https://aur.archlinux.org/packages/lib32-freealut/)
*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxmu](https://www.archlinux.org/packages/?name=lib32-libxmu)
*   [lib32-sdl_ttf](https://www.archlinux.org/packages/?name=lib32-sdl_ttf)

## And Yet It Moves

Dependencies:

*   [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)
*   [lib32-libtheora](https://www.archlinux.org/packages/?name=lib32-libtheora)
*   [lib32-libtiff4](https://www.archlinux.org/packages/?name=lib32-libtiff4)

### Game does not start

When the game refuses to launch and prints one of the following error messages:

```
readlink: extra operand ‘Yet’
Try 'readlink --help' for more information.

```

or

```
This script must be run as a user with write priviledges to game directory

```

Open `*gamedir*/AndYetItMovesSteam.sh` and replace the line:

```
ayim_dir="$(dirname "$(readlink -f ${BASH_SOURCE[0]})")"

```

with:

```
ayim_dir="$(dirname "$(readlink -f "${BASH_SOURCE[0]}")")"

```

## Anodyne

Dependencies:

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/), follow [#Adobe Air setup](#Adobe_Air_setup)
*   [xterm](https://www.archlinux.org/packages/?name=xterm) (probably not required)

### Play with a controller: joy2key configuration

Configuration example to play [Anodyne](http://www.anodynegame.com/) with an XBox 360 Wireless Controller

```
COMMON
-dev /dev/input/js0
-X
-thresh -18000 18000 -18000 18000 -18000 18000 -18000 18000 -18000 18000 -18000 18000 -18000 18000 -18000 18000
-axis Left Right Up Down blank blank blank blank blank blank blank blank Left Right Up Down
-buttons c x Return

```

Save this to `~/.joy2keyrc` and start joy2key after you start Anodyne

```
joy2key -rcfile ~/.joy2keyrc

```

## Aquaria

### Mouse pointer gets stuck in one direction

If the mouse pointer gets stuck in one direction, make sure `*gamedir*/usersettings.xml` contains `<JoystickEnabled on="0" />`.

If that does not fix the issue, try unplugging any joysticks or joystick adapter devices you have plugged in.

## ARK: Survival Evolved

### Game does not start, displays text window with unreadable text

Add `MESA_GL_VERSION_OVERRIDE=4.0 MESA_GLSL_VERSION_OVERRIDE=400` to your [launch options](/index.php/Steam#Launch_options "Steam").

## Audiosurf 2

Requires [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

## Binding of Isaac: Rebirth

### No sound

**Note:** This also helps with Never Alone (Kisima Ingitchuna) and No Time to Explain.

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

Adjust the audio levels in the game options.

## The Book of Unwritten Tales

Dependencies:

*   [lib32-jasper](https://aur.archlinux.org/packages/lib32-jasper/)
*   [lib32-libxaw](https://aur.archlinux.org/packages/lib32-libxaw/)

If the game does not start, uncheck: *Properties > Enable Steam Community In-Game*.

The game is known to segfault when opening the settings and possibly during or before playing. A workaround from the [Steam discussions](http://steamcommunity.com/app/221410/discussions/3/846939071081758230/#p2) is to replace the game's `RenderSystem_GL.so` with one from Debian's repositories. To do that download [this deb file](https://launchpad.net/ubuntu/+archive/primary/+files/libogre-1.7.4_1.7.4-3_i386.deb), and extract it with [dpkg](https://aur.archlinux.org/packages/dpkg/):

```
$ dpkg -x libogre-*.deb outdir

```

Now replace `*gamedir*/lib/32/RenderSystem_GL.so` with the one extracted from the `.deb` package.

## The Book of Unwritten Tales: The Critter Chronicles

See [#The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales).

To prevent the game from crashing at the end credits, change the size of the credits image as described [here](http://steamcommunity.com/app/221830/discussions/0/828925849276110960/#c810921273836530791).

## Borderlands 2

### Migrating saves from other platforms

Borderlands 2 does not support cross-platform Steam Cloud syncing, you have to manually copy the files between platforms. Save locations can be found [here](https://pcgamingwiki.com/wiki/Borderlands_2#Game_data). Make sure your user can access the files.

### Using Ctrl Key

Borderlands 2 does not allow the `Ctrl` key to be used by default. The game seems to be accessing keycodes and not keysyms, therefore xmodmap has no affect. A workaround is using *setkeycodes* to map the Ctrl-scancode to some other key, as described in [Map scancodes to keycodes#Using setkeycodes](/index.php/Map_scancodes_to_keycodes#Using_setkeycodes "Map scancodes to keycodes"). I use `setkeycodes 0x1d 56` (as root) to map Ctrl to Alt before starting the game and `setkeycodes 0x1d 29` to restore the default.

### Logging into SHiFT

Out of the box you will not be able to log into SHiFT since the game expects certificates to be in `/usr/lib/ssl`, which is where Ubuntu stores them. Arch however uses `/etc/ssl`. To resolve the problem, add `SSL_CERT_DIR=/etc/ssl/certs` to your [launch options](/index.php/Steam#Launch_options "Steam").

### Game crashes nearly instantly

As of lib32-openal version 1.18.0-1, the game crashes instantly. The possible solutions are to downgrade lib32-openal to 1.17.2-1, or to start the game with `LD_PRELOAD='$HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libopenal.so.1'`.

## Borderlands: The Pre-Sequel

See [#Logging into SHiFT](#Logging_into_SHiFT).

### Keyboard not working

Using [dwm](/index.php/Dwm "Dwm"), no keyboard input seems to register.

### Not starting via Steam

If the game appears as *Running*, then syncs and closes when you launch it from Steam, try creating a `steam_appid.txt` in the game directory containing `261640`. This should resolve the issue and let you start the game directly from the game directory. If that does not work, try using the [steam-native-runtime](https://www.archlinux.org/packages/?name=steam-native-runtime).

### Game crashes nearly instantly

As of lib32-openal version 1.18.0-1, the game crashes instantly. The possible solutions are to downgrade lib32-openal to 1.17.2-1, or to start the game with `LD_PRELOAD='$HOME/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libopenal.so.1'`.

## Cities in Motion 2

### Dialog boxes fail to display properly

You will not be able to read or see anything, and you will have this in your logs:

```
Fontconfig error: "/etc/fonts/conf.d/10-scale-bitmap-fonts.conf", line 69: non-double matrix element
Fontconfig error: "/etc/fonts/conf.d/10-scale-bitmap-fonts.conf", line 69: wrong number of matrix elements

```

Workaround for the bug [FS#35039](https://bugs.archlinux.org/task/35039) is available [here](http://bpaste.net/show/167019/)  (replace `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`).

## Cities Skylines

### Textures not rendering properly

Add `UNITY_DISABLE_GRAPHICS_DRIVER_WORKAROUNDS=yes` to your [launch options](/index.php/Steam#Launch_options "Steam").

## Civilization V

You need to add `LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%` to your [launch options](/index.php/Steam#Launch_options "Steam").

[steam-for-linux issue #4379](https://github.com/ValveSoftware/steam-for-linux/issues/4379)

### Stuttering sound with PulseAudio

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting").

## Civilization: Beyond earth

If you are getting an instant crash/close upon launch, make sure you have the following 32-bit packages installed:

*   [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-intel-tbb](https://aur.archlinux.org/packages/lib32-intel-tbb/)

## Civilization VI

As with Civ V, you need to add `LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%` to your [launch options](/index.php/Steam#Launch_options "Steam").

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

## Deus Ex: Mankind divided

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

## The Clockwork Man

Requires [lib32-libidn](https://www.archlinux.org/packages/?name=lib32-libidn).

## Company of Heroes 2

Like with [#Alien Isolation](#Alien_Isolation) you need to symlink `/usr/lib/libpcre.so` to `*gamedir*/lib/*arch*/libpcre.so.3`, otherwise the game will fail to start.

## Counter-Strike: Global Offensive (CS:GO)

### Game starts on the wrong screen

[csgo-osx-linux issue #60](https://github.com/ValveSoftware/csgo-osx-linux/issues/60)

If it happens, go into fullscreen windowed or windowed mode and drag the window to the correct monitor. Then go back into fullscreen, the game should now be on the correct monitor.

### Cannot reach bottom of the screen on menus

[csgo-osx-linux issue #594](https://github.com/ValveSoftware/csgo-osx-linux/issues/594)

If you have a secondary monitor you might have a part of your lower screen you cannot reach in menus. If on Gnome you can try to open the overview (Super key) and drag the game to the other monitor and back.

If you are not on Gnome or dragging the window back and forth did not work you can try to [install](/index.php/Install "Install") [wmctrl](https://www.archlinux.org/packages/?name=wmctrl) and run this command, where X and Y is the offset of the window and H and W is the size.

```
wmctrl -r "Counter-Strike: Global Offensive - OpenGL" -e 0,X,Y,H,W

```

**Example**: SecondaryMonitor: on the left 2560x1600, GamingMonitor: on the right 2560x1440).

```
wmctrl -r "Counter-Strike: Global Offensive - OpenGL" -e 0,2560,0,1600,1200

```

Here X and Y is 0,2560 to move the window to the monitor on the right and H and W 1600,1200 is set to match the ingame resolution.

### Sound is played slightly delayed

[csgo-osx-linux issue #45](https://github.com/ValveSoftware/csgo-osx-linux/issues/45)

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting") for a possible solution.

### Mouse not working in-game

If your mouse works in the main menu but not in-game, add `SDL_VIDEO_X11_DGAMOUSE=0` to your [launch options](/index.php/Steam#Launch_options "Steam"). [[2]](https://bbs.archlinux.org/viewtopic.php?id=184905)

### Brightness slider not working

[Install](/index.php/Install "Install") [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and run `xrandr` to find out the name of your connected display output.

Edit `*gamedir*/csgo.sh` and add the following lines (adapt *output_name*):

```
**# gamma correction**
**xrandr --output *output_name* --gamma 1.6:1.6:1.6 # play with values if required**
STATUS=42
while [$STATUS -eq 42]; do
 ...
done
**# restore gamma**
**xrandr --output *output_name* --gamma 1:1:1**
exit $STATUS

```

### Microphone not working

[csgo-osx-linux issue #573](https://github.com/ValveSoftware/csgo-osx-linux/issues/573#issuecomment-174016722)

CS:GO uses the default PulseAudio sound device ignoring what is configured in Steam settings.

First find out the source name of your microphone (it should start with `alsa_input.`):

```
$ pacmd list-sources

```

Then set the default device (change the name accordingly):

```
$ pacmd set-default-source *device_name*

```

Also lower the microphone level to 60% otherwise you will get some nasty background noise and you will be difficult to understand (change the name accordingly):

```
$ pacmd set-source-volume *device_name* 0x6000

```

## Crusader Kings II

x86_64 dependencies:

*   [lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl)

### Locations

The game can be started directly without running Steam by executing `./ck2` in its directory.

Save files are stored in `~/.paradoxinteractive/Crusader Kings II/`. Before version 2.03 they were stored in `~/Documents/Paradox Interactive/Crusader Kings II/save games/`.

### No audio

SDL uses [PulseAudio](/index.php/PulseAudio "PulseAudio") by default, so to use it with [ALSA](/index.php/ALSA "ALSA") you need to set:

 `~/.pam_environment`  `SDL_AUDIODRIVER=alsa` 

### Oddly sized starting window

You can make full screen mode the default by setting `fullscreen=yes` in `~/.paradoxinteractive/Crusader Kings II/settings.txt`.

## Death Road To Canada

### No music

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

## Defender's Quest: Valley of the Forgotten

Dependencies:

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/), follow [#Adobe Air setup](#Adobe_Air_setup)
*   [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra)
*   [xterm](https://www.archlinux.org/packages/?name=xterm)

## Dirt

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

## Divinity: Original Sin - Enhanced Edition

### Game doesn't start when using Bumblebee optirun or primusrun

Edit `*gamedir*/runner.sh` to use primusrun:

```
LD_LIBRARY_PATH="." primusrun ./EoCApp

```

## Don't Starve

Dependencies:

*   [lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)

### No sound

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

In the game, go to the options and adjust the audio levels.

## Dota 2

Dependencies:

*   [libudev0](https://aur.archlinux.org/packages/libudev0/)
*   [libpng12](https://www.archlinux.org/packages/?name=libpng12)
*   [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn)

### In-game font is unreadable

Add `MESA_GL_VERSION_OVERRIDE=2.1` to your [launch options](/index.php/Steam#Launch_options "Steam").

### The game does not start

If you run the game from the terminal and, although no error is shown, try **disabling**: *Steam > Settings > In-Game > Enable Steam Community In-Game*.

Apparently the game [#The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales) has the same problem. It also describes a workaround that is untested in Dota 2.

### Game runs on the wrong screen

	[GitHub Dota 2 issue #11](https://github.com/ValveSoftware/Dota-2/issues/11)

### Game does not start with libxcb-dri3 error message

After a recent Mesa update, Dota 2 stopped working. The error message is:

```
SDL_GL_LoadLibrary(NULL) failed: Failed loading libGL.so.1: /usr/lib32/libxcb-dri3.so.0: undefined symbol: xcb_send_fd

```

See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

### Steam overlay

Steam distributes a copy of libxcb which is incompatible with the latest xorg libxcb. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting"), [[3]](https://github.com/ValveSoftware/steam-for-linux/issues/3199), [[4]](https://github.com/ValveSoftware/steam-for-linux/issues/3093).

### Chinese tips and player names not shown

The Chinese characters in tips and player names are displayed as block characters.

The problem is caused by the font packages: [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu), [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) and [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).

	[GitHub Steam issue #1688](https://github.com/ValveSoftware/Dota-2/issues/1688) 

### Chinese input method problem

Dota2 is not compatible with CJK IME(Input Method Editor/Enhancer), such as [Ibus](/index.php/Ibus "Ibus") and [Fcitx](/index.php/Fcitx "Fcitx"). Chinese characters cannot be typed in Dota2.

A possible solution is to replace `*gamedir*/dota 2 beta/bin/libSDL2-2.0.so.0` with a self-compiled *libSDL* that supports fcitx or ibus.

	[LibSDL+Ibus](https://forum.ubuntu.com.cn/viewtopic.php?f=34&t=460195)

	[LibSDL+Fcitx](https://forum.ubuntu.com.cn/viewtopic.php?f=34&t=466879)

	[LibSDL+Fcitx source](https://github.com/timxx/SDL-fcitx)

	[The solutions issue](https://github.com/ValveSoftware/Dota-2/issues/1650) 

## Drox Operative

If the game fails to start with "Couldn't find Database/database.dbl!", manually extract the assets. assets003.zip will overwrite some files from the previous files.

```
$ cd "~/.steam/root/steamapps/common/Drox Operative/Assets"
$ unzip assets00[123].zip

```

## Dwarfs F2P

Dependencies:

*   [lib32-libgdiplus](https://aur.archlinux.org/packages/lib32-libgdiplus/)

### Game does not start

There was a bug that stopped Steam from fetching all the needed files. It should be resolved, if you still bump into this problem, try verifying integrity of game cache from game properties, local files tab.

If the game still crashes at startup, edit `*gamedir*/Run.sh` and change

```
export LD_LIBRARY_PATH=.:${LD_LIBRARY_PATH}

```

to

```
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:.

```

**Note:** This file may be overwritten by updates or by verifying integrity of game cache. You may need to modify it again.

If these do not help, you may have outdated libraries in the game installation folder that are crashing the game on startup. Try removing the following files from the game directory:

```
libX11.so.6 libsteam.so libtier0_s.so libvstdlib_s.so steamclient.so

```

### Game crashes

In some cases, the game crashes about 2 minutes before the end of every arcade. This bug has been reported, but there's no known solution to it.

## Dynamite Jack

Requires [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl).

### Sound Issues

When running on 64-bit Arch Linux, there may be "pops and hisses" when running Dynamite Jack. This could be caused by not having `STEAM_RUNTIME=0` set. (However, even with `STEAM_RUNTIME=0` set, the game may still sometimes start with this issue. Exiting and restarting the game seems to make the problem go away.)

### Game does not start

If running steam with the `STEAM_RUNTIME=0`, Dynamite Jack may have a problem starting. Check the steam error messages for this message:

```
/home/$USER/.steam/root/steamapps/common/Dynamite Jack/bin/main: error while loading shared libraries: libSDL-1.2.so.0: cannot open shared object file: No such file or directory

```

Install [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl) from [multilib](/index.php/Multilib "Multilib") and Dynamite Jack should start up.

## Euro Truck Simulator 2

### Shows only a black screen

Select safe mode when the game starts up.

## Football Manager 2014

This game will not run when installed on an [XFS](/index.php/XFS "XFS") or reiserfs filesystem. Workaround is to install on an ext4 filesystem.

## FORCED

Requires [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu).

This game has 32-bit and 64-bit binaries. For some reason, Steam will launch the 32-bit binary even on 64-bit Arch Linux. When manually launching the 64-bit binary, the game starts, but cannot connect to Steam account, so you cannot play. So install 32-bits dependencies, and launch the game from Steam.

## FTL: Faster than Light

### Compatibility

After installation, FTL may fail to run due to a 'Text file busy' error (characterised in Steam by your portrait border going green then blue again). The easiest way to mend this is to just reboot your system. Upon logging back in FTL should run.

The Steam overlay in FTL does not function as it is not a 3D accelerated game. Because of this the desktop notifications will be visible. If playing in fullscreen, therefore, these notifications in some systems may steal focus and revert you back to windowed mode with no way of going back to fullscreen without relaunching. The binaries for FTL on Steam have no DRM and it is possible to run the game *without* Steam running, so in some cases that may be optimum - just ensure that you launch FTL via the launcher script in `~/.steam/root/steamapps/common/FTL Faster than Light/data/` rather than the FTL binary in the $arch directory.

### Problems with open-source video driver

FTL may fail to run if you are using an opensource driver for your video card. There are two solutions: install a proprietary video driver or delete (rename if you are unsure) the library "libstdc++.so.6" inside `~/.steam/root/steamapps/common/FTL Faster Than Light/data/amd64/lib`. This is if you are using a 64bit system. In case you are using a 32bit system you have to remove (rename) the same library located into `~/.steam/root/steamapps/common/FTL Faster Than Light/data/x86/lib`.

## Game Dev Tycoon

### Game does not start

You might get an error about missing `libudev.so.0`. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

## Garry's Mod

### Game does not start

When an error about a missing `client.so` appears, try the following:

```
$ cd ~/.steam/root/steamapps/common/GarrysMod/bin/
$ ln -s libawesomium-1-7.so.0 libawesomium-1-7.so.2
$ ln -s ../garrysmod/bin/client.so ./

```

If the error mentions a missing library for `libgcrypt.so.11`, install [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15).

### Opening some menus causes the game to crash

Most menus work fine, but ones with checkboxes (LAN multiplayer, mounted games list) do not work at all. This is a bug in the menu code.

If you prefer the default menu style and do not mind a hacky solution: [Simon311](https://github.com/Facepunch/garrysmod-issues/issues/86#issuecomment-30935491) has written code with instructions to fix it.

If you do not care for the default menu style and want a more stable but feature-incomplete solution, Facepunch developer [robotboy655](https://github.com/robotboy655/gmod-lua-menu) has written a new menu.

### Game crashes after attempting to join server

While in the process of joining a server, downloading resources, etc, the game seems to hang and after a while, perhaps during the "sending client info" portion the game crashes, usually without any error messages. Error does not give much information, however, the process for Garry's mod is killed.

This issue arises more often when joining servers with many addons like DarkRP servers specifically.

The problem seems to correlate with a weak GPU and the game is timing out from the server, so if the GPU is the problem, lowering the graphics settings to the minimum should fix the problem.

## Gods will be watching

Install [lib32-libopenssl-1.0-compat](https://aur.archlinux.org/packages/lib32-libopenssl-1.0-compat/) and add `LD_LIBRARY_PATH=/usr/lib32/openssl-1.0-compat` to your [launch options](/index.php/Steam#Launch_options "Steam").

## GRID Autosport

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

### Black screen when trying to play

Add `LC_ALL=C` to your [launch options](/index.php/Steam#Launch_options "Steam").

## Hack 'n' Slash

### Crashes when trying to load a game

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

## Hacker Evolution

Requires [lib32-sdl2_mixer](https://www.archlinux.org/packages/?name=lib32-sdl2_mixer).

## Half-Life 2 and episodes

### Cyrillic fonts problem

This problem can be solved by deleting "Helvetica" font.

## Hammerwatch

### The game does not start via Steam

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

### No sound

Hammerwatch opens with a popup: "Sound Error" -- "Could not initialize OpenAL, no sounds will be played. Try updating your OpenAL drivers."

OpenAL, which Hammerwatch uses, defaults to PulseAudio. To change that, add the following line to `/etc/openal/alsoft.conf`:

```
drivers=alsa,pulse

```

This way, Hammerwatch will use ALSA. This solution was found [here](https://stackoverflow.com/questions/9547396/what-does-al-lib-pulseaudio-c612-context-did-not-connect-access-denied-me).

## Halo: Custom Edition

Although not a Steam game, Halo: Custom Edition running under [Wine](/index.php/Wine "Wine") and/or PlayOnLinux has many audio problems. To mitigate this, install dsound via winetricks or PlayOnLinux. Then, set the in-game "Sound Quality" to medium. If you have installed the campaign extra, this also restores all video cut-scene audio.

## Harvest: Massive Encounter

Dependencies:

*   [lib32-sfml](https://aur.archlinux.org/packages/lib32-sfml/)
*   [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo)
*   [lib32-nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=lib32-nvidia-cg-toolkit)
*   [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)

### Compatibility

Game refuses to launch and throws you to library installer loop. Just edit `*gamedir*/run_harvest` and remove everything but:

```
#!/bin/bash
exec ./Harvest

```

## Hatoful Boyfriend

### Japanese text invisible

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

## Hyper Light Drifter

### The controller does not work

[Install](/index.php/Install "Install") [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2) and add `LD_PRELOAD=libSDL2.so` to your [launch options](/index.php/Steam#Launch_options "Steam").

See the following Steam Community discussions:

*   [Controller Issues](https://steamcommunity.com/app/257850/discussions/1/365163686036494421)
*   [Common Bugs + Known Issues](https://steamcommunity.com/app/257850/discussions/1/365163686045397160/)

It is suggested to run the *next_update* branch to get new fixes, there however currently is a libcurl segfault keeping it from starting without special workarounds.

### Missing libcurl.so.4 or version CURL_OPENSSL_3 not found

[Install](/index.php/Install "Install") [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat) and add `LD_PRELOAD=libcurl.so.3` to your [launch options](/index.php/Steam#Launch_options "Steam").

## The Impossible Game

Dependencies:

*   [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2)
*   [lib32-sdl2_image](https://www.archlinux.org/packages/?name=lib32-sdl2_image)

## The Inner World

Requires [java-commons-codec](https://aur.archlinux.org/packages/java-commons-codec/) for sound support.

### Bringing up the inventory or main menu

Hold the tab key.

#### Cutscenes

The game has cutscenes. It starts directly with a cutscene before you start the actual game in the backyard. To see these cutscenes you need to use Oracle's Java instead of the openjdk.

Install [jre](https://aur.archlinux.org/packages/jre/) from the [AUR](/index.php/AUR "AUR") and run:

```
# archlinux-java set java-8-jre/jre

```

Furthermore you need the package [ffmpeg-compat-55](https://aur.archlinux.org/packages/ffmpeg-compat-55/).

There seem to be problems with the Steam overlay. Try to run the game directly with `*gamedir*/TIW_start.sh`.

Note that cutscenes open in a new window. So pay attention to that and switch to the new window to enjoy the movies.

See the [Steam Forums](http://steamcommunity.com/app/251430/discussions/0/611701360817206606/#c611701360827509770) for details.

## Interloper

Requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib).

### Game does not start

The game can sometimes segfault due to an incompatibility with the Steam Runtime's `libasound.so.2`. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

## Invisible Apartment

Requires [qt5-multimedia](https://www.archlinux.org/packages/?name=qt5-multimedia).

### Game does not start

If the game does not run when you launch it via Steam, try to directly run `./ia1` in the game directory.

## Joe Danger 2: The Movie

Requires [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse).

### Compatibility

Game only worked after obtaining from the [Humble Bundle](https://www.humblebundle.com/‎) directly and [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) was installed.

## Kerbal Space Program

See [Kerbal Space Program](/index.php/Kerbal_Space_Program "Kerbal Space Program").

## Killing Floor

### Cannot change screen resolution

If trying to modify the resolution in-game crashes your desktop environment, edit `~/.killingfloor/System/KillingFloor.ini`:

```
[WinDrv.WindowsClient]
WindowedViewportX=*width*
WindowedViewportY=*height*
FullscreenViewportX=*width*
FullscreenViewportY=*height*
MenuViewportX=*width*
MenuViewportY=*height*

[SDLDrv.SDLClient]
WindowedViewportX=*width*
WindowedViewportY=*height*
FullscreenViewportX=*width*
FullscreenViewportY=*height*
MenuViewportX=*width*
MenuViewportY=*height*

```

### Windowed mode

Uncheck fullscreen in the options menu, and press `Ctrl+g` to stop mouse capturing.

### Stuttering sound

KillingFloor comes with its own OpenAL library `*gamedir*/System/openal.so`.

Back it up, [install](/index.php/Install "Install") [openal](https://www.archlinux.org/packages/?name=openal) or [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal) (if using a 64bit system).

Then symlink the installed system library (`/usr/lib32/libopenal.so.1` or `/usr/lib/libopenal.so.1`) to `openal.so`.

## Lethal League

Requires [lib32-glew1.10](https://www.archlinux.org/packages/?name=lib32-glew1.10).

## Life is Strange

Requires [lib32-librtmp0](https://www.archlinux.org/packages/?name=lib32-librtmp0).

## Mark of the Ninja

### Bad sound

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

## Metro: Last Light

The game does not allow you to change its resolution on a multi-monitor setup on GNOME with the AMD Catalyst drivers. A temporary workaround is to disable the side monitors. Jason over at [unencumbered by facts](http://unencumberedbyfacts.com/2013/11/20/multiple-monitor-gaming-on-linux/) managed to get it working with his multi-monitor setup using a single display server, he however is using Nvidia.

## Middle-earth: Shadow of Mordor

### Floating heads

Add `__GL_ShaderPortabilityWarnings=0` to your [launch options](/index.php/Steam#Launch_options "Steam").

## Multiwinia

Requires [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

### Crash on startup

If Multiwinia crashes on startup on X64 systems, force launching the 32-bit executable by replacing `*gamedir*/run_steam.sh` with the following script:

```
#!/bin/sh
./multiwinia.bin.x86

```

See [[5]](https://steamcommunity.com/app/1530/discussions/0/864969481950542663/#c558746995160431396).

## Natural Selection 2

Requires [lib32-speex](https://www.archlinux.org/packages/?name=lib32-speex).

### No Sound

If there is no sound in-game. Try installing [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl) and [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2).

If this fails, try setting the game's launch options in Steam to:

```
LD_LIBRARY_PATH="/usr/lib32:$LD_LIBRARY_PATH" %command%

```

## Nuclear Throne

### Missing libcurl.so.4 or version CURL_OPENSSL_3 not found

[Install](/index.php/Install "Install") [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat) and add `LD_PRELOAD=libcurl.so.3` to your [launch options](/index.php/Steam#Launch_options "Steam").

## Penumbra: Overture

Dependencies:

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-sdl_image](https://www.archlinux.org/packages/?name=lib32-sdl_image)
*   [lib32-sdl_ttf](https://www.archlinux.org/packages/?name=lib32-sdl_ttf)

### Windowed mode

There is no in-game option to change to the windowed mode, you will have to edit `~/.frictionalgames/Penumbra/Overture/settings.cfg` to activate it.

Find `FullScreen="true"` and change it to `FullScreen="false"`, after this the game should start in windowed mode.

## The Polynomial

Dependencies:

*   [ilmbase102-libs](https://aur.archlinux.org/packages/ilmbase102-libs/)
*   [openexr170-libs](https://aur.archlinux.org/packages/openexr170-libs/)

[Steam for Linux issue #2721](https://github.com/ValveSoftware/steam-for-linux/issues/2721)

### Segfaults during program start on 64-bit systems

The game segfaults during program start because of the `LD_LIBRARY_PATH` setting in the launcher script. Edit `*gamedir*/Polynomial64`, and comment out the `LD_LIBRARY_PATH` variable. Make sure to put the `./bin/Polynomial64 "$@"` command on a new line.

## Portal 2

### Game does not start

Several OpenGL-related errors (such as `PROBLEM: You appear to have OpenGL 1.4.0, but we need at least 2.0.0!` or `libGL error: driver pointer missing`) are caused by Portal 2 bundling an old libstdc++ file. This error is especially common with open source Radeon drivers (`radeonsi`). See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

A problem with libstdc can be fixed with:

```
LD_PRELOAD='/usr/$LIB/libstdc++.so.6' %command%

```

### Resolution too low

When the game starts with a resolution so low that you cannot reach the game settings, start the game in windowed mode by setting the launch option `-windowed`.

## Prison Architect

### ALSA error when using PulseAudio

The error:

`ALSA lib pcm_dmix.c:1018:(snd_pcm_dmix_open) unable to open slave`

was resolved by installing:

*   [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)

per [PulseAudio#ALSA](/index.php/PulseAudio#ALSA "PulseAudio").

## Project Zomboid

Requires [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk).

### No sound

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

In the game, go to the options and set all audio to the proper volume.

## Redshirt

Requires [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) if you use PulseAudio.

## Revenge of the Titans

Requires [libxtst](https://www.archlinux.org/packages/?name=libxtst) and [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst).

## Rock Boshers DX: Directors Cut

Requires [lib32-libcaca](https://www.archlinux.org/packages/?name=lib32-libcaca).

## Saints Row IV

### Game fails to launch after update to new Nvidia drivers

Set the launch options for Saints Row IV to:

 `LD_PRELOAD=$LD_PRELOAD:/usr/lib32/libGLX_nvidia.so %command%` 

### Game causes GPU lockup with mesa drivers

Saints Rows IV can cause a GPU lockup when trying to play on certain AMD hardware using open source drivers: [Bug 93475](https://bugs.freedesktop.org/show_bug.cgi?id=93475).

A workaround is to set the launch options to:

 `R600_DEBUG=nosb %command%` 

## Serious Sam 3: BFE

### No audio

Try running:

```
# mkdir -p /usr/lib/i386-linux-gnu/alsa-lib/
# ln -s /usr/lib32/alsa-lib/libasound_module_pcm_pulse.so /usr/lib/i386-linux-gnu/alsa-lib/

```

If that does not work, try tweaking `~/.alsoftrc` as proposed by the [Steam community](http://steamcommunity.com/app/221410/discussions/3/846940248238406974/) (Serious Sam 3: BFE uses OpenAL to output sound). If you are not using Pulse Audio, you may want to write the following configuration:

 `~/.alsoftrc` 
```
[general]
drivers = alsa
[alsa]
device = default
capture = default
mmap = true

```

## Space Pirates and Zombies

Requires [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

### No audio

Try running:

```
# mkdir -p /usr/lib/i386-linux-gnu/alsa-lib/
# ln -s /usr/lib32/alsa-lib/libasound_module_pcm_pulse.so /usr/lib/i386-linux-gnu/alsa-lib/

```

If that does not work, try tweaking `~/.alsoftrc` as proposed by the Steam community (Serious Sam 3: BFE uses OpenAL to output sound). If you are not using Pulse Audio, you may want to write the following configuration:

 `~/.alsoftrc` 
```
[general]
drivers = alsa
[alsa]
device = default
capture = default
mmap = true

```

## Spacechem

Dependencies:

*   [lib32-sdl_mixer](https://www.archlinux.org/packages/?name=lib32-sdl_mixer)
*   [lib32-sdl_image](https://www.archlinux.org/packages/?name=lib32-sdl_image)
*   [lib32-sqlite](https://www.archlinux.org/packages/?name=lib32-sqlite)

### Game crash

The shipped x86 version of Spacechem does not work on x64 with the game's own libSDL* files, and crashes with some strange output.

To solve this just remove the three files `libSDL-1.2.so.0`, `libSDL_image-1.2.so.0`, `libSDL_mixer-1.2.so.0` from the game directory.

## Splice

Requires [glu](https://www.archlinux.org/packages/?name=glu).

Splice comes with both x86 and x64 binaries. Steam does not have to be running to launch this game.

## Star Wars Battlefront II

Star Wars Battlefront 2's Steam version running under [Wine](/index.php/Wine "Wine") has a bug which causes it to take forever to load a game. The solution is to compile a custom Wine version with the patch from this [WineHQ bug comment](https://bugs.winehq.org/show_bug.cgi?id=29582#c31).

In order to use the patched wine version with PlayOnLinux, copy the completely patched and compiled wine-1.7.55 folder to `~/.PlayOnLinux/wine/linux-x86/`.

## The Stanley Parable

### Game won't start

As discussed in the Steam store page, remove `bin/libstdc++.so.6` from the game folder.

## Shadow Tactics: Blades of the Shogun

Dependencies:

*   [lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5)
*   [lib32-libxcursor](https://www.archlinux.org/packages/?name=lib32-libxcursor)
*   [lib32-libxrandr](https://www.archlinux.org/packages/?name=lib32-libxrandr)

## Steel Storm: Burning Retribution

### Start with black screen

The game tries to launch in 1024x768 resolution with fullscreen mode by default. It is impossible on some devices. (for example laptop Samsung Series9 with intel hd4000 video).

You can launch the game in windowed mode. To do this open game Properties in Steam, in General tab select "Set launch options..." and type "-window".

Now you can change the resolution in game.

### No English fonts

If you are using an Intel video card, disable S3TC in [driconf](https://www.archlinux.org/packages/?name=driconf).

## Stephen's Sausage Roll

### No sound

If using [native libraries](/index.php/Steam/Troubleshooting#Native_runtime "Steam/Troubleshooting") and [libpulse](https://www.archlinux.org/packages/?name=libpulse) is installed, Unity may try to use that library for sound and fail. To test if this is the problem, try removing [libpulse](https://www.archlinux.org/packages/?name=libpulse) or renaming the package files that are named `libpulse-simple*`. To see which [libpulse](https://www.archlinux.org/packages/?name=libpulse) files are relevant, run:

 `$ pacman -Qql libpulse | grep /usr/lib/libpulse-simple` 
```
/usr/lib/libpulse-simple.so
/usr/lib/libpulse-simple.so.0
/usr/lib/libpulse-simple.so.0.1.0
```

If renaming any of those files works for you, you can proceed with the following instructions (revert any renaming you just did). Browse to the game's directory:

```
$ cd "$HOME/.steam/root/steamapps/common/Stephen's Sausage Roll"

```

And create a sub-directory that we can use to hold 0-byte look-alike library files:

```
$ mkdir noload/

```

Use `touch` to create 0-byte versions of the above files that we want the dynamic linker to skip, e.g.:

```
$ touch noload/{libpulse-simple.so,libpulse-simple.so.0,libpulse-simple.so.0.1.0}

```

**Note:** Only a 0-byte `libpulse-simple.so.0` file may be required.

After you have created these 0-byte files, you can now attempt to run the game binary directly, telling the dynamic linker to use our 0-byte files:

```
$ LD_LIBRARY_PATH="noload/:$LD_LIBRARY_PATH" ./Sausage.x86_64

```

If everything works up to this point, you can amend the launch options in Steam to be:

```
LD_LIBRARY_PATH="noload/:$LD_LIBRARY_PATH" %command%

```

Again, this should work because Steam checks for a `noload/` directory relative to the game's directory. The dynamic linker should respect the `$LD_LIBRARY_PATH` variable and fail to load the necessary [libpulse](https://www.archlinux.org/packages/?name=libpulse) files. The game should then fallback to plain ALSA.

## Superbrothers: Sword & Sworcery EP

Dependencies:

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) if you use PulseAudio

The game bundles an outdated version of libstdc++ which prevents the game from starting. [[6]](http://steamcommunity.com/app/204060/discussions/0/364039785161291413) The following can be observed when you run Steam and S&S from the terminal:

```
libGL error: unable to load driver: i965_dri.so
libGL error: driver pointer missing
libGL error: failed to load driver: i965
libGL error: unable to load driver: i965_dri.so
libGL error: driver pointer missing
libGL error: failed to load driver: i965
libGL error: unable to load driver: swrast_dri.so
libGL error: failed to load driver: swrast

```

To solve this problem remove `*gamedir*/lib/libstdc++.so.6*`. After that the game will use the libstdc++ from Steam.

## Tabletop Simulator

### CJK characters not showing in game

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

## Team Fortress 2

Requires [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12).

### HRTF setup

Assuming HRTF (head-related transfer function) has been properly set up in the operating system, HRTF won't be enabled unless you disable the original processing. To do so, use

```
dsp_slow_cpu 1

```

For best results, also change the following:

```
snd_spatialize_roundrobin 1
dsp_enhance_stereo 0
snd_pitchquality 1

```

### Loading screen freeze

If you are a non-english (speaking) user, you have to enable "en_US.UTF-8" in the locale.gen! Generate a new locale after that.

### No audio

It happens if there is no PulseAudio in your system. If you want to use [ALSA](/index.php/ALSA "ALSA"), you need to launch Steam or the game directly with `SDL_AUDIODRIVER=alsa` (From [SteamCommunity](http://steamcommunity.com/app/221410/discussions/0/882966056462819091/#c882966056470753683)).

If it still does not work, you may also need to set the environment variable AUDIODEV. For instance `AUDIODEV=Live`. Use `aplay -l` to list the available sound cards.

### Slow loading textures

If you are using Chris' FPS Configs or any other FPS config, you may have set `mat_picmip` to `2`. This spawns multiple threads for texture loading, which may cause more jittering and lag on Linux, especially on alternative kernels. Try setting it to `-1`, the default.

## Terraria

See the KNOWN ISSUES & WORKAROUNDS​ section of the [release announcement](http://forums.terraria.org/index.php?threads/terraria-1-3-0-8-can-mac-linux-come-out-play.30287/).

## This War of Mine

### Game does not start

This happens because of an incompatibility with the newer version of `lib32-curl`. To fix the problem you need to remove `libcurl.so.4` from the game directory.

### Sound glitches with Steam native

The bundled `libOpenAL` might not work correctly, try symlinking `/usr/lib32/libopenal.so` to `*gamedir*/libOpenAL.so`.

## Ticket to Ride

Dependencies:

*   [lib32-gstreamer0.10-base](https://aur.archlinux.org/packages/lib32-gstreamer0.10-base/)
*   [lib32-pangox-compat](https://aur.archlinux.org/packages/lib32-pangox-compat/)

As lib32-gstreamer0.10-base is quite hard to build you can use [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repo for this package

## Tomb Raider

### Game immediately closes when running with steam-native

Tomb Raider has a very heavy amount of dependency on the Steam runtime, the easiest solution is to just run it using the runtime. You can do so by setting the following as the launch option:

 `~/.steam/root/ubuntu12_32/steam-runtime/run.sh %command%` 

### Steam Controller not working in-game

If your Steam Controller is correctly recognized and paired but still not working in-game try the following:

*   In Steam, non Big Screen, go to Settings -> Account -> Beta participation -> Change... and in the dropdown select box select Steam Beta Update
*   Restart Steam
*   Go to Big Screen and start Tomb Raider

Correctly recognized means you can control desktop mouse and Steam in Big Picture mode and the controller is shown in Big Picture settings

## Towns / Towns Demo

Requires [Java](/index.php/Java "Java").

## Transistor

### Crash on launch / FMOD binding crash / Audio issues

Try running steam with following command

```
LD_PRELOAD='/usr/lib/libstdc++.so.6:/usr/lib/libgcc_s.so.1:/usr/lib/libxcb.so.1:/usr/lib/libasound.so.2' steam

```

Alternatively, right click on Transistor, go to Properties => Set Launch Options... and enter

```
LD_PRELOAD='/usr/lib/libstdc++.so.6:/usr/lib/libgcc_s.so.1:/usr/lib/libxcb.so.1:/usr/lib/libasound.so.2' %command%

```

This will force Steam to do the fix whenever Transistor is started, but allows Steam to be launched normally.

Otherwise, run the game via shell and set up proper audio device for FMOD, as discussed in [[7]](https://steamcommunity.com/app/237930/discussions/2/620695877176333955/).

Also, check out this thread [[8]](https://steamcommunity.com/app/237930/discussions/2/492378265893557247/)

## Transmissions: Element 120

Dependencies:

*   [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)

### Troubleshooting

Make sure you have all libraries installed. Above the standard set required by Steam runtime, the game requires few additional ones. The typical error message that indicates that is

```
AppFramework : Unable to load module vguimatsurface.so!

```

To find missing dependencies go into the game directory and run:

```
LD_LIBRARY_PATH=bin ldd bin/vguimatsurface.so

```

Look for entries that say *not found*.

## Trine 2

Dependencies:

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxxf86vm](https://www.archlinux.org/packages/?name=lib32-libxxf86vm)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo)
*   [lib32-libdrm](https://www.archlinux.org/packages/?name=lib32-libdrm)

*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)
*   [lib32-libwrap](https://www.archlinux.org/packages/?name=lib32-libwrap)

### Colors

If colors are wrong with FOSS drivers (r600g at least), try to run the game in windowed mode, rendering will be corrected. ([bugreport](https://bugs.freedesktop.org/show_bug.cgi?id=60553))

### Sound

If sound plays choppy, try:

 `/etc/openal/alsoft.conf` 
```
drivers=pulse,alsa
frequency=48000

```

### Resolution

If the game resolution is wrong when using a dual monitor setup and you can't see the whole window edit `~/.frozenbyte/Trine2/options.txt` and change the options `ForceFullscreenWidth` and `ForceFullscreenHeight` to the resolution of your monitor on which you want to play the game.

## Tropico 5

### Blank screen with sound only on startup

Add `MESA_GL_VERSION_OVERRIDE=4.0 MESA_GLSL_VERSION_OVERRIDE=400` to your [launch options](/index.php/Steam#Launch_options "Steam").

## Unity of Command

Requires [lib32-pango](https://www.archlinux.org/packages/?name=lib32-pango).

### Squares

If squares are shown instead of text, try removing `*gamedir*/bin/libpangoft2-1.0.so.0`.

### No audio

If you get this error:

```
ALSA lib dlmisc.c:254:(snd1_dlobj_cache_get) Cannot open shared library /usr/lib/i386-linux-gnu/alsa-lib/libasound_module_pcm_pulse.so

```

Try running:

```
# mkdir -p /usr/lib/i386-linux-gnu/alsa-lib/
# ln -s /usr/lib32/alsa-lib/libasound_module_pcm_pulse.so /usr/lib/i386-linux-gnu/alsa-lib/

```

## Unity3D

Games based on the Unity3D engine, like *War For The Overworld* or *Pixel Piracy* may need the package [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) to understand that they run on Linux and work properly.

### Locale settings

Games made in C# often have a problem with some locales (e.g. Russian, German) because developers don't specify locale-agnostic number formatting. This can result in some game screens loading only partially, problems with online features or other bugs.

To work around this, set the game's launch options to `LC_ALL=C %command%`

Some of the affected games: *FORCED*, *Gone Home*, *Ichi*, *Nimble Quest*, *Syder Arcade*.

### Unity 5 sound problems

The sound system in Unity 5 changed and to be able to play games created with it you must most likely install and run [PulseAudio](/index.php/PulseAudio "PulseAudio").

Another solution is to disable the Steam runtime: in the launch options for the game, write this: `LD_LIBRARY_PATH="" %command%`

Another solution is to prevent Unity from trying to use pulseaudio using [pulsenomore](https://aur.archlinux.org/packages/pulsenomore/) package from the [AUR](/index.php/AUR "AUR"). Once it is installed, use the following as launch options :`/usr/bin/pulsenomore %command%`

Some of the affected games: *Kerbal Space Programm*, *SUPERHOT*, *ClusterTruck*

### Game launching on wrong monitor in fullscreen mode

Unity games that do not support monitor selection will most likely launch the game on a wrong monitor.

The problem is that Unity games write the default param `<pref name="UnitySelectMonitor" type="int">-1</pref>` to the game config file.

This will lead to the game launching on a non-primary monitor.

When changing to value into `<pref name="UnitySelectMonitor" type="int">**0**</pref>` for the according game, the game will start on the correct (primary) monitor.

A Unity game config file usually resides in `~/.config/unity3d/*CompanyName*/*ProductName*/prefs`.

Some of the affected games: *Cities: Skylines*, *Tablestop Simulator*, *Assault Android Cactus*, *Wasteland 2*, *Tyranny*.

Be aware that some games do not support setting that parameter, it will simply be ignored. This is the case for *Pillars of Eternity*, *Kentucky Route Zero*, *Sunless Sea*.

## Unrest

Requires [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth).

## War Thunder

### No audio

If there is no audio after launching the game, install [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

### Blank screen

If having a green or blank screen on startup, add `MESA_GL_VERSION_OVERRIDE=4.1COMPAT` to your [launch options](/index.php/Steam#Launch_options "Steam"). [[9]](https://forum.warthunder.com/index.php?/topic/267809-linux-potential-workaround-for-mesa-drivers-black-screen/) [[10]](http://forum.warthunder.com/index.php?search_term=0030709&app=core&module=search&do=search&fromMainBar=1&search_app=forums%3Aforum%3A920&sort_field=&sort_order=&search_in=posts)

## Warhammer 40,000: Dawn of War II

Dependencies:

*   [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib)
*   [librtmp0](https://www.archlinux.org/packages/?name=librtmp0)

The start script does not point to the right direction of `libasound.so.2`.

To fix it open `*gamedir*/DawnOfWar2.sh` and replace the following lines:

```
HAS_LSB_RELEASE=$(command -v lsb_release)
if [ -n "${HAS_LSB_RELEASE}" ] && [ "$(lsb_release -c | cut -f2)" = "trusty" ]; then
	LD_PRELOAD_ADDITIONS="/usr/lib/x86_64-linux-gnu/libasound.so.2:${LD_PRELOAD_ADDITIONS}"
fi 
```

with:

 `LD_PRELOAD_ADDITIONS="/usr/lib64/libasound.so.2:${LD_PRELOAD_ADDITIONS}"` 

## Witcher 2: Assassin of Kings

Dependencies:

*   [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls)
*   [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)
*   [lib32-sdl2_image](https://www.archlinux.org/packages/?name=lib32-sdl2_image)
*   [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2)

### Game does not start

If the game does not run, enable error messages:

```
$ cd "$HOME/.steam/root/steamapps/common/the witcher 2"
$ LIBGL_DEBUG=verbose ./witcher2

```

## Wizardry 6: Bane of the Cosmic Forge

Requires [DOSBox](/index.php/DOSBox "DOSBox").

To fix the crash at start, open `*gamedir*/dosbox_linux/launch_wizardry6.sh` and:

*   comment the line `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./libs`
*   change the beginning of the line starting with `exec ./dosbox` to `exec dosbox`

## World of Goo

### Changing resolution

To change the game resolution edit the *Graphics display* section in `*gamedir*/properties/config.txt`. For example:

```
<!-- Graphics display -->
<param name="screen_width" value="1680" />
<param name="screen_height" value="1050" />
<param name="color_depth" value="0" />
<param name="fullscreen" value="true" />
<param name="ui_inset" value="10" />

```

## XCOM

Dependencies:

*   [librtmp0](https://www.archlinux.org/packages/?name=librtmp0)
*   [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image) (required to enable keyboard functionality in-game)

### Hangs on startup

See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

If you are running a [hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics") system, try:

```
__GL_THREADED_OPTIMIZATIONS=0 primusrun %command%

```

### Graphical glitches on Intel HD

XCOM may not recognize the SDL2 shared libraries shipped with the Steam runtime. Check if the binary finds all required files and install missing packages if necessary ([sdl2](https://www.archlinux.org/packages/?name=sdl2) and [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image)).

 `ldd ~/.steam/root/steamapps/common/XCom-Enemy-Unknown/binaries/linux/game.x86_64 ` 

## Tower Unite

### Graphical Glitches

This is a known issue, and it occurs because the shaders had not been ported to Linux yet by the developers. To minimize glitches and make the game playable use

 `-opengl4` 

launch option, set Ocean Quality to "Potato" and Effects Quality to "Low" in game's settings.