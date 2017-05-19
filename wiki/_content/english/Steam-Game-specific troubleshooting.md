See [Steam](/index.php/Steam "Steam") for the main article, and [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting") for generic troubleshooting.

**Note:** [Steam](/index.php/Steam "Steam") installs library dependencies of a game to a library directory, but some are missing at the moment. Report bugs involving missing libraries on Valve's bug tracker on their [GitHub page](https://github.com/ValveSoftware/steam-for-linux) before adding workarounds here, and then provide a link to the bug so it can be removed as the problems are fixed.

**Tip:** If a game fails to start, a possible reason is that it is missing required libraries. You can find out what libraries it requests by running `ldd *game_executable*`. `*game_executable*` is likely located somewhere in `~/.steam/root/SteamApps/common/`. Please note that most of these "missing" libraries are actually already included with Steam, and do not need to be installed globally.

## Contents

*   [1 Common steps](#Common_steps)
    *   [1.1 Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH)
    *   [1.2 Adobe Air setup](#Adobe_Air_setup)
*   [2 Air Brawl](#Air_Brawl)
*   [3 Alien Isolation](#Alien_Isolation)
*   [4 Amnesia: The Dark Descent](#Amnesia:_The_Dark_Descent)
*   [5 And Yet It Moves](#And_Yet_It_Moves)
    *   [5.1 Compatibility](#Compatibility)
*   [6 Anodyne](#Anodyne)
*   [7 Aquaria](#Aquaria)
    *   [7.1 Mouse pointer gets stuck in one direction](#Mouse_pointer_gets_stuck_in_one_direction)
*   [8 ARK: Survival Evolved](#ARK:_Survival_Evolved)
    *   [8.1 Game does not start, displays text window with unreadable text](#Game_does_not_start.2C_displays_text_window_with_unreadable_text)
*   [9 Audiosurf 2](#Audiosurf_2)
*   [10 Binding of Isaac: Rebirth](#Binding_of_Isaac:_Rebirth)
    *   [10.1 No sound](#No_sound)
*   [11 The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales)
*   [12 The Book of Unwritten Tales: The Critter Chronicles](#The_Book_of_Unwritten_Tales:_The_Critter_Chronicles)
*   [13 Borderlands 2](#Borderlands_2)
    *   [13.1 Syncing save games](#Syncing_save_games)
    *   [13.2 Using Ctrl Key](#Using_Ctrl_Key)
    *   [13.3 Logging into SHiFT](#Logging_into_SHiFT)
*   [14 Borderlands: The Pre-Sequel](#Borderlands:_The_Pre-Sequel)
    *   [14.1 Keyboard not working](#Keyboard_not_working)
    *   [14.2 Not starting via Steam](#Not_starting_via_Steam)
*   [15 Cities in Motion 2](#Cities_in_Motion_2)
    *   [15.1 Dialog boxes fail to display properly](#Dialog_boxes_fail_to_display_properly)
*   [16 Cities Skylines](#Cities_Skylines)
    *   [16.1 Textures not rendering properly](#Textures_not_rendering_properly)
*   [17 Civilization V](#Civilization_V)
    *   [17.1 Stuttering sound with PulseAudio](#Stuttering_sound_with_PulseAudio)
    *   [17.2 Extra LD_PRELOAD variable](#Extra_LD_PRELOAD_variable)
*   [18 Civilization: Beyond earth](#Civilization:_Beyond_earth)
*   [19 Civilization VI](#Civilization_VI)
    *   [19.1 OpenSSL 1.0](#OpenSSL_1.0)
*   [20 Deus Ex: Mankind divided](#Deus_Ex:_Mankind_divided)
*   [21 The Clockwork Man](#The_Clockwork_Man)
*   [22 Company of Heroes 2](#Company_of_Heroes_2)
*   [23 Counter-Strike: Global Offensive (CS:GO)](#Counter-Strike:_Global_Offensive_.28CS:GO.29)
    *   [23.1 Game starts on the wrong screen](#Game_starts_on_the_wrong_screen)
    *   [23.2 Cannot reach bottom of the screen on menus](#Cannot_reach_bottom_of_the_screen_on_menus)
    *   [23.3 Sound is played slightly delayed](#Sound_is_played_slightly_delayed)
    *   [23.4 Unable to aim when in-game](#Unable_to_aim_when_in-game)
    *   [23.5 Brightness slider not working](#Brightness_slider_not_working)
    *   [23.6 Microphone not working](#Microphone_not_working)
*   [24 Crusader Kings II](#Crusader_Kings_II)
    *   [24.1 Tips and tricks](#Tips_and_tricks)
    *   [24.2 No audio](#No_audio)
    *   [24.3 Oddly sized starting window](#Oddly_sized_starting_window)
*   [25 Death Road To Canada](#Death_Road_To_Canada)
    *   [25.1 No music](#No_music)
*   [26 Defender's Quest: Valley of the Forgotten](#Defender.27s_Quest:_Valley_of_the_Forgotten)
*   [27 Dirt](#Dirt)
    *   [27.1 Fails to start](#Fails_to_start)
*   [28 Divinity: Original Sin - Enhanced Edition](#Divinity:_Original_Sin_-_Enhanced_Edition)
    *   [28.1 Game doesn't start when using Bumblebee optirun or primusrun](#Game_doesn.27t_start_when_using_Bumblebee_optirun_or_primusrun)
*   [29 Don't Starve](#Don.27t_Starve)
    *   [29.1 No sound](#No_sound_2)
*   [30 Dota 2](#Dota_2)
    *   [30.1 In-game font is unreadable](#In-game_font_is_unreadable)
    *   [30.2 The game does not start](#The_game_does_not_start)
    *   [30.3 Game runs on the wrong screen](#Game_runs_on_the_wrong_screen)
    *   [30.4 Game does not start with libxcb-dri3 error message](#Game_does_not_start_with_libxcb-dri3_error_message)
    *   [30.5 Steam overlay](#Steam_overlay)
    *   [30.6 Chinese Tips and player's name display problem](#Chinese_Tips_and_player.27s_name_display_problem)
    *   [30.7 Chinese input method problem](#Chinese_input_method_problem)
*   [31 Dwarfs F2P](#Dwarfs_F2P)
    *   [31.1 Game does not start](#Game_does_not_start)
    *   [31.2 Game crashes](#Game_crashes)
*   [32 Dynamite Jack](#Dynamite_Jack)
    *   [32.1 Sound Issues](#Sound_Issues)
    *   [32.2 Game does not start](#Game_does_not_start_2)
*   [33 Euro Truck Simulator 2](#Euro_Truck_Simulator_2)
    *   [33.1 Shows only a black screen](#Shows_only_a_black_screen)
*   [34 Football Manager 2014](#Football_Manager_2014)
*   [35 FORCED](#FORCED)
*   [36 FTL: Faster than Light](#FTL:_Faster_than_Light)
    *   [36.1 Compatibility](#Compatibility_2)
    *   [36.2 Problems with open-source video driver](#Problems_with_open-source_video_driver)
*   [37 Game Dev Tycoon](#Game_Dev_Tycoon)
    *   [37.1 Game does not start](#Game_does_not_start_3)
*   [38 Garry's Mod](#Garry.27s_Mod)
    *   [38.1 Game does not start](#Game_does_not_start_4)
    *   [38.2 Opening some menus causes the game to crash](#Opening_some_menus_causes_the_game_to_crash)
    *   [38.3 Game crashes after attempting to join server](#Game_crashes_after_attempting_to_join_server)
*   [39 GRID Autosport](#GRID_Autosport)
    *   [39.1 OpenSSL 1.0](#OpenSSL_1.0_2)
    *   [39.2 Game does not start (Black screen)](#Game_does_not_start_.28Black_screen.29)
*   [40 Hack 'n' Slash](#Hack_.27n.27_Slash)
    *   [40.1 Crashes when trying to load a game](#Crashes_when_trying_to_load_a_game)
*   [41 Hacker Evolution](#Hacker_Evolution)
*   [42 Half-Life 2 and episodes](#Half-Life_2_and_episodes)
    *   [42.1 Cyrillic fonts problem](#Cyrillic_fonts_problem)
*   [43 Hammerwatch](#Hammerwatch)
    *   [43.1 The game does not start via Steam](#The_game_does_not_start_via_Steam)
    *   [43.2 No sound](#No_sound_3)
*   [44 Halo: Custom Edition](#Halo:_Custom_Edition)
*   [45 Harvest: Massive Encounter](#Harvest:_Massive_Encounter)
    *   [45.1 Compatibility](#Compatibility_3)
*   [46 Hatoful Boyfriend](#Hatoful_Boyfriend)
    *   [46.1 Japanese text invisible](#Japanese_text_invisible)
*   [47 Hyper Light Drifter](#Hyper_Light_Drifter)
    *   [47.1 The controller does not work](#The_controller_does_not_work)
    *   [47.2 Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found)
*   [48 The Impossible Game](#The_Impossible_Game)
*   [49 The Inner World](#The_Inner_World)
    *   [49.1 Bringing up the inventory or main menu](#Bringing_up_the_inventory_or_main_menu)
        *   [49.1.1 Cutscenes](#Cutscenes)
*   [50 Interloper](#Interloper)
    *   [50.1 Game does not start](#Game_does_not_start_5)
*   [51 Invisible Apartment](#Invisible_Apartment)
    *   [51.1 Game does not start](#Game_does_not_start_6)
*   [52 Joe Danger 2: The Movie](#Joe_Danger_2:_The_Movie)
    *   [52.1 Compatibility](#Compatibility_4)
*   [53 Kerbal Space Program](#Kerbal_Space_Program)
*   [54 Killing Floor](#Killing_Floor)
    *   [54.1 Screen resolution](#Screen_resolution)
    *   [54.2 Windowed mode](#Windowed_mode)
    *   [54.3 Stuttering Sound](#Stuttering_Sound)
*   [55 Lethal League](#Lethal_League)
*   [56 Life is Strange](#Life_is_Strange)
*   [57 Mark of the Ninja](#Mark_of_the_Ninja)
    *   [57.1 Bad sound](#Bad_sound)
*   [58 Metro: Last Light](#Metro:_Last_Light)
*   [59 Middle-earth: Shadow of Mordor](#Middle-earth:_Shadow_of_Mordor)
    *   [59.1 Floating heads](#Floating_heads)
*   [60 Multiwinia](#Multiwinia)
    *   [60.1 Crash on startup](#Crash_on_startup)
*   [61 Natural Selection 2](#Natural_Selection_2)
    *   [61.1 No Sound](#No_Sound_4)
*   [62 Nuclear Throne](#Nuclear_Throne)
    *   [62.1 Missing libcurl.so.4 or version `CURL_OPENSSL_3' not found](#Missing_libcurl.so.4_or_version_.60CURL_OPENSSL_3.27_not_found)
*   [63 Penumbra: Overture](#Penumbra:_Overture)
    *   [63.1 Windowed mode](#Windowed_mode_2)
*   [64 The Polynomial](#The_Polynomial)
    *   [64.1 Segfaults during program start on 64-bit systems](#Segfaults_during_program_start_on_64-bit_systems)
*   [65 Portal 2](#Portal_2)
    *   [65.1 Game does not start](#Game_does_not_start_7)
    *   [65.2 Resolution too low](#Resolution_too_low)
*   [66 Prison Architect](#Prison_Architect)
    *   [66.1 ALSA error when using PulseAudio](#ALSA_error_when_using_PulseAudio)
*   [67 Project Zomboid](#Project_Zomboid)
    *   [67.1 No sound](#No_sound_5)
*   [68 Redshirt](#Redshirt)
*   [69 Revenge of the Titans](#Revenge_of_the_Titans)
*   [70 Rock Boshers DX: Directors Cut](#Rock_Boshers_DX:_Directors_Cut)
*   [71 Saints Row IV](#Saints_Row_IV)
    *   [71.1 Game fails to launch after update to new Nvidia drivers](#Game_fails_to_launch_after_update_to_new_Nvidia_drivers)
    *   [71.2 Game causes GPU lockup with mesa drivers](#Game_causes_GPU_lockup_with_mesa_drivers)
*   [72 Serious Sam 3: BFE](#Serious_Sam_3:_BFE)
    *   [72.1 No audio](#No_audio_2)
*   [73 Space Pirates and Zombies](#Space_Pirates_and_Zombies)
    *   [73.1 No audio](#No_audio_3)
*   [74 Spacechem](#Spacechem)
    *   [74.1 Game crash](#Game_crash)
*   [75 Splice](#Splice)
*   [76 Star Wars Battlefront II](#Star_Wars_Battlefront_II)
*   [77 The Stanley Parable](#The_Stanley_Parable)
    *   [77.1 Game won't start](#Game_won.27t_start)
*   [78 Shadow Tactics: Blades of the Shogun](#Shadow_Tactics:_Blades_of_the_Shogun)
*   [79 Steel Storm: Burning Retribution](#Steel_Storm:_Burning_Retribution)
    *   [79.1 Start with black screen](#Start_with_black_screen)
    *   [79.2 No English fonts](#No_English_fonts)
*   [80 Stephen's Sausage Roll](#Stephen.27s_Sausage_Roll)
    *   [80.1 No sound](#No_sound_6)
*   [81 Superbrothers: Sword & Sworcery EP](#Superbrothers:_Sword_.26_Sworcery_EP)
*   [82 Tabletop Simulator](#Tabletop_Simulator)
    *   [82.1 CJK characters not showing in game](#CJK_characters_not_showing_in_game)
*   [83 Team Fortress 2](#Team_Fortress_2)
    *   [83.1 Making HRTF work](#Making_HRTF_work)
    *   [83.2 Loading screen freeze](#Loading_screen_freeze)
    *   [83.3 No audio](#No_audio_4)
    *   [83.4 Slow loading textures](#Slow_loading_textures)
*   [84 Terraria](#Terraria)
*   [85 This War of Mine](#This_War_of_Mine)
    *   [85.1 Game does not start](#Game_does_not_start_8)
    *   [85.2 Sound glitches with Steam native](#Sound_glitches_with_Steam_native)
*   [86 Ticket to Ride](#Ticket_to_Ride)
*   [87 Tomb Raider](#Tomb_Raider)
    *   [87.1 Game immediately closes when running with steam-native](#Game_immediately_closes_when_running_with_steam-native)
    *   [87.2 Steam Controller not working in-game](#Steam_Controller_not_working_in-game)
*   [88 Towns / Towns Demo](#Towns_.2F_Towns_Demo)
*   [89 Transistor](#Transistor)
    *   [89.1 Crash on launch / FMOD binding crash / Audio issues](#Crash_on_launch_.2F_FMOD_binding_crash_.2F_Audio_issues)
*   [90 Transmissions: Element 120](#Transmissions:_Element_120)
    *   [90.1 Troubleshooting](#Troubleshooting)
*   [91 Trine 2](#Trine_2)
    *   [91.1 Colors](#Colors)
    *   [91.2 Sound](#Sound)
    *   [91.3 Resolution](#Resolution)
*   [92 Tropico 5](#Tropico_5)
    *   [92.1 Blank screen with sound only on startup](#Blank_screen_with_sound_only_on_startup)
*   [93 Unity of Command](#Unity_of_Command)
    *   [93.1 Squares](#Squares)
    *   [93.2 No audio](#No_audio_5)
*   [94 Unity3D](#Unity3D)
    *   [94.1 Locale settings](#Locale_settings)
    *   [94.2 Unity 5 sound problems](#Unity_5_sound_problems)
    *   [94.3 Game launching on wrong monitor in fullscreen mode](#Game_launching_on_wrong_monitor_in_fullscreen_mode)
*   [95 Unrest](#Unrest)
*   [96 War Thunder](#War_Thunder)
    *   [96.1 Blank screen](#Blank_screen)
*   [97 Warhammer 40,000: Dawn of War II](#Warhammer_40.2C000:_Dawn_of_War_II)
*   [98 Witcher 2: Assassin of Kings](#Witcher_2:_Assassin_of_Kings)
    *   [98.1 Game does not start](#Game_does_not_start_9)
*   [99 Wizardry 6: Bane of the Cosmic Forge](#Wizardry_6:_Bane_of_the_Cosmic_Forge)
*   [100 World of Goo](#World_of_Goo)
    *   [100.1 Changing resolution](#Changing_resolution)
*   [101 XCOM](#XCOM)
    *   [101.1 Hangs on startup](#Hangs_on_startup)
    *   [101.2 Graphical glitches on Intel HD](#Graphical_glitches_on_Intel_HD)

## Common steps

### Prepend /usr/lib to LD_LIBRARY_PATH

Right click on the game in your library, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

### Adobe Air setup

*   Package [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/) installs Adobe Air not in the place where the game expects it to be, fix this by creating a symlink (requires root permissions):

```
$ ln -s /opt/adobe-air-sdk/runtimes/air/linux/Adobe\ AIR /opt/Adobe\ AIR

```

*   Adobe AIR requires you to accept its EULA. You can do so using:

```
$ mkdir -p ~/.appdata/Adobe/AIR
$ echo 2 > ~/.appdata/Adobe/AIR/eulaAccepted

```

## Air Brawl

When some fonts are missing, [install](/index.php/Install "Install") [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts).

## Alien Isolation

You need to create the following symlink, otherwise the game will fail to start.

```
$ ln -s /usr/lib/libpcre.so  ~/.steam/steam/SteamApps/common/Alien\ Isolation/lib/x86_64/libpcre.so.3

```

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

### Compatibility

Game refuses to launch and one of the following messages can be observed on console

```
 readlink: extra operand ‘Yet’
 Try 'readlink --help' for more information.

```

OR

```
 This script must be run as a user with write priviledges to game directory

```

To fix this, use:

 `~/.steam/root/SteamApps/common/And Yet It Moves/AndYetItMovesSteam.sh` 
```
#ayim_dir="$(dirname "$(readlink -f ${BASH_SOURCE[0]})")"
ayim_dir="$(dirname "$(readlink -f "${BASH_SOURCE[0]}")")"

```

## Anodyne

Dependencies:

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/), follow [#Adobe Air setup](#Adobe_Air_setup)
*   [xterm](https://www.archlinux.org/packages/?name=xterm) (probably not required)

## Aquaria

### Mouse pointer gets stuck in one direction

If the mouse pointer gets stuck in any one direction, the game becomes unplayable. You may try:

 `~/.local/share/Steam/SteamApps/common/Aquaria/usersettings.xml` 
```
#<JoystickEnabled on=”1″ />
<JoystickEnabled on=”0″ />
```

If that does not fix the issue, unplug any joystick or joystick adapter devices you may have plugged in.

## ARK: Survival Evolved

### Game does not start, displays text window with unreadable text

Right click on the game's entry in your Steam library, click on `Properties`, then `SET LAUNCH OPTIONS`, and add this line:

 `MESA_GL_VERSION_OVERRIDE=4.0 MESA_GLSL_VERSION_OVERRIDE=400 %command%` 

## Audiosurf 2

Requires [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

## Binding of Isaac: Rebirth

### No sound

**Note:** This also helps with Never Alone (Kisima Ingitchuna) and No Time to Explain

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

In the game, go to the options and set all audio levels to the proper volume.

## The Book of Unwritten Tales

Dependencies:

*   [lib32-jasper](https://aur.archlinux.org/packages/lib32-jasper/)
*   [lib32-libxaw](https://aur.archlinux.org/packages/lib32-libxaw/)

If the game does not start, uncheck: *Properties > Enable Steam Community In-Game*.

The game may segfault upon clicking the Setting menu and possibly during or before gameplay. This is a known problem and you will unfortunately have to wait for a fix from the developer. A workaround (taken from the [Steam forums](http://steamcommunity.com/app/221410/discussions/3/846939071081758230/#p2)) is to replace the game's RenderSystem_GL.so with one from Debian's repositories. To do that download this [deb file](https://launchpad.net/ubuntu/+archive/primary/+files/libogre-1.7.4_1.7.4-3_i386.deb), extract it with [dpkg](https://aur.archlinux.org/packages/dpkg/):

```
$ dpkg -x libogre-*.deb outdir}}

```

and replace `~/.local/share/Steam/SteamApps/common/The Book of Unwritten Tales/lib/32/RenderSystem_GL.so` with the one that comes with the `.deb` package.

## The Book of Unwritten Tales: The Critter Chronicles

See [#The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales).

To prevent the game from crashing at the very end when the credits are shown, change the size of the credits image as described [here](http://steamcommunity.com/app/221830/discussions/0/828925849276110960/#c810921273836530791).

## Borderlands 2

### Syncing save games

Steam Cloud syncing does not (intentionally) work between platforms. With that said gave save files can be manually moved between systems. Save locations can be found here: [http://pcgamingwiki.com/wiki/Borderlands_2#Game_data](http://pcgamingwiki.com/wiki/Borderlands_2#Game_data). Once backed up to a FAT32 or other cross-compatible file-system thumbdrive (or the cloud), move the saved files to your GNU/Linux system, locate your saved file location, and move into the 17-digit long numeric file name. If previous saves on your GNU/Linux system can be deleted you can do so now. The key fix that I found was a need to change the ownership, group, and permissions. I used `chown steam:steam *` and then `chmod 0660 *` to get my moved saved files to work.

### Using Ctrl Key

Borderlands 2 does not allow the Ctrl key to be used by default. The game seems to be accessing keycodes and not keysyms, therefore xmodmap has no affect. A workaround is using *setkeycodes* to map the Ctrl-scancode to some other key, as described in [Map scancodes to keycodes#Using setkeycodes](/index.php/Map_scancodes_to_keycodes#Using_setkeycodes "Map scancodes to keycodes"). I use `setkeycodes 0x1d 56` (as root) to map Ctrl to Alt before starting the game and `setkeycodes 0x1d 29` to restore the default.

### Logging into SHiFT

The Linux version of Borderlands 2 expects to be run on Ubuntu, as that is the "officially" supported distro for Steam. As a result of this, when attempting to log in to SHiFT, it will fail, claiming the server is not available. Using strace, it can be seen that it fails to connect to the server because it cannot load SSL certificates from `/usr/lib/ssl`, which is the Ubuntu filesystem spec. Arch uses `/etc/ssl`. This can be fixed by symlinking `/etc/ssl` to `/usr/lib/ssl`, like so:

```
# ln -s /etc/ssl /usr/lib/ssl

```

To avoid symlinking an alternative to the above is to add the following to the launch options in Steam:

```
SSL_CERT_DIR="/etc/ssl/certs" %command%

```

Using one method or the other you will now be able to log into SHiFT to redeem SHiFT codes.

## Borderlands: The Pre-Sequel

Borderlands the Pre-Sequel (and maybe Borderlands 2) might not be able to connect to the Gearbox SHIFT-service, this is related to a wrong path to the available SSL certificates. This can be solved by creating a symbolic link from `/etc/ssl` to `/usr/lib/ssl`. See [this comment on the steam discussion forum](http://steamcommunity.com/app/49520/discussions/0/616189742722687689/#c616189742811551908).

As an alternative the following can be added to the launch options in Steam:

```
SSL_CERT_DIR="/etc/ssl/certs" %command%

```

### Keyboard not working

Using [dwm](/index.php/Dwm "Dwm"), no keyboard input seems to register with BL:TPQ. Switching to openbox helped solved the issue, no other fix could be found. It's either a specific dwm issue or tiling WMs in general.

### Not starting via Steam

The game may stop launching from Steam; on launch, game appears as 'Running', then syncs and closes.

Running Steam using [Steam-Native](https://www.archlinux.org/packages/multilib/x86_64/steam-native-runtime/) will allow the game to start correctly.

Alternatively create the missing `steam_appid.txt`:

```
$ echo 261640 > ~/.steam/steam/steamapps/common/BorderlandsPreSequel/steam_appid.txt

```

You can now start the game directly from the game directory, directly supplying any command line options you have configured under Set Launch Options.

Save the command in a [desktop entry](/index.php/Desktop_entry "Desktop entry") or script.

## Cities in Motion 2

### Dialog boxes fail to display properly

You will not be able to read or see anything, and you will have this in your logs:

```
Fontconfig error: "/etc/fonts/conf.d/10-scale-bitmap-fonts.conf", line 69: non-double matrix element
Fontconfig error: "/etc/fonts/conf.d/10-scale-bitmap-fonts.conf", line 69: wrong number of matrix elements

```

Workaround for the bug [FS#35039](https://bugs.archlinux.org/task/35039) is available [here](http://bpaste.net/show/167019/) (replace `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`).

## Cities Skylines

### Textures not rendering properly

In the Steam client set the following launch property for the game:

```
UNITY_DISABLE_GRAPHICS_DRIVER_WORKAROUNDS=yes %command%

```

## Civilization V

### Stuttering sound with PulseAudio

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting").

### Extra LD_PRELOAD variable

If the game seems to start and close, consider using the following as launch options for the game:

```
env LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%

```

[steam-for-linux issue #4379](https://github.com/ValveSoftware/steam-for-linux/issues/4379)

## Civilization: Beyond earth

If you are getting an instant crash/close upon launch, make sure you have the following 32-bit packages installed:

*   [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-intel-tbb](https://aur.archlinux.org/packages/lib32-intel-tbb/)

## Civilization VI

As with Civ V, you will need to modify the launch options, see [#Extra LD_PRELOAD variable](#Extra_LD_PRELOAD_variable).

### OpenSSL 1.0

Civ 6 is built against [openssl](https://www.archlinux.org/packages/?name=openssl) 1.0 exactly. If you have updated to openssl 1.1 or later Civ6 and some other steam games [will not work](https://bugs.archlinux.org/task/53618). To provide openssl 1.0 [install](/index.php/Install "Install") [libopenssl-1.0-compat](https://aur.archlinux.org/packages/libopenssl-1.0-compat/) and add the following launch options to Civ6

```
 LD_LIBRARY_PATH='/usr/lib/openssl-1.0-compat/' %command%

```

If your are already modifying the launch command with LD_PRELOAD then you can combine the commands

```
env LD_LIBRARY_PATH='/usr/lib/openssl-1.0-compat/' LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%

```

## Deus Ex: Mankind divided

Install [libopenssl-1.0-compat](https://aur.archlinux.org/packages/libopenssl-1.0-compat/) and follow the instructions for Civilization VI (above).

## The Clockwork Man

Requires [lib32-libidn](https://www.archlinux.org/packages/?name=lib32-libidn).

## Company of Heroes 2

Like with [#Alien Isolation](#Alien_Isolation) you need to create the following symlink, otherwise the game will fail to start.

```
$ ln -s /usr/lib/libpcre.so  ~/.steam/steam/SteamApps/common/Company\ of\ Heroes\ 2/lib/<ARCH>/libpcre.so.3

```

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

### Unable to aim when in-game

When you are unable to aim in-game but your mouse works in the GUI menus add this line to your `.bash_profile` and relogin [[1]](https://bbs.archlinux.org/viewtopic.php?id=184905):

```
export SDL_VIDEO_X11_DGAMOUSE=0

```

### Brightness slider not working

[Install](/index.php/Install "Install") [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and run `xrandr` to find out the name of your connected display output.

Edit `~/.steam/steam/steamapps/common/Counter-Strike\ Global\ Offensive/csgo.sh` and add the following lines (adapt *output_name*):

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

### Tips and tricks

Game is installed into `$HOME/Steam/SteamApps/common/Crusader Kings II`. Game can be started directly, without need of running Steam on background, using command `$HOME/Steam/SteamApps/common/Crusader Kings II/ck2`.

Saves are stored in `$HOME/Documents/Paradox Interactive/Crusader Kings II/save games/`. In the newest version (2.03), save-game files seem to be stored to `$HOME/.paradoxinteractive/Crusader Kings II/`. If your documents folder is empty, try looking there.

### No audio

SDL uses [PulseAudio](/index.php/PulseAudio "PulseAudio") by default, so to use it with [ALSA](/index.php/ALSA "ALSA") you need to set:

 `~/.pam_environment`  `SDL_AUDIODRIVER=alsa` 

### Oddly sized starting window

Enable full screen mode as the default. In `~/.paradoxinteractive/Crusader Kings II/settings.txt` set `fullscreen` to `yes`.

## Death Road To Canada

### No music

[#Prepend /usr/lib to LD_LIBRARY_PATH](#Prepend_.2Fusr.2Flib_to_LD_LIBRARY_PATH).

## Defender's Quest: Valley of the Forgotten

Dependencies:

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/), follow [#Adobe Air setup](#Adobe_Air_setup)
*   [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra)
*   [xterm](https://www.archlinux.org/packages/?name=xterm)

## Dirt

Requires [libopenssl-1.0-compat](https://aur.archlinux.org/packages/libopenssl-1.0-compat/).

### Fails to start

Dirt is built against [openssl](https://www.archlinux.org/packages/?name=openssl) 1.0 exactly. If you have updated to openssl 1.1 or later Dirt and some other steam games [will not work](https://bugs.archlinux.org/task/53618). To provide openssl 1.0 [install](/index.php/Install "Install") [libopenssl-1.0-compat](https://aur.archlinux.org/packages/libopenssl-1.0-compat/) then right click on Dirt on your game list, click on Properties, click on SET LAUNCH OPTIONS, then add this:

```
LD_PRELOAD='/usr/lib64/openssl-1.0-compat/libssl.so.1.0.0 /usr/lib64/openssl-1.0-compat/libcrypto.so.1.0.0' %command%

```

## Divinity: Original Sin - Enhanced Edition

### Game doesn't start when using Bumblebee optirun or primusrun

Edit `<path to library>/SteamApps/common/Divinity Original Sin Enhanced Edition/runner.sh` to have it use primusrun:

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

Start Steam (or Dota 2) with the environment variable:

```
MESA_GL_VERSION_OVERRIDE=2.1

```

### The game does not start

If you run the game from the terminal and, although no error is shown, try **disabling**: *Steam > Settings > In-Game > Enable Steam Community In-Game*.

Apparently the game [The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales) has the same problem. It also describes a workaround that is untested in Dota 2.

### Game runs on the wrong screen

	[GitHub Dota 2 issue #11](https://github.com/ValveSoftware/Dota-2/issues/11)

### Game does not start with libxcb-dri3 error message

After a recent Mesa update, Dota 2 stopped working. The error message is:

```
SDL_GL_LoadLibrary(NULL) failed: Failed loading libGL.so.1: /usr/lib32/libxcb-dri3.so.0: undefined symbol: xcb_send_fd

```

See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

### Steam overlay

Steam distributes a copy of libxcb which is incompatible with the latest xorg libxcb. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting"), [[2]](https://github.com/ValveSoftware/steam-for-linux/issues/3199), [[3]](https://github.com/ValveSoftware/steam-for-linux/issues/3093).

### Chinese Tips and player's name display problem

The Chinese characters in the Tips and player's name display block character.

The problem caused by some fonts package. It is known that the 'ttf-dejave', 'ttf-liberation' and 'ttf-ms-fonts' will cause the prolem, and the 'wqy-*', 'ttf-ubuntu-font-family', 'ttf-arphic-uming', 'ttf-linux-libertine' are safe. The other fonts family are not checked.

	[GitHub Steam issue #1688](https://github.com/ValveSoftware/Dota-2/issues/1688)

### Chinese input method problem

Dota2 is not compatible with CJK IME(Input Method Editor/Enhancer), such as Ibus and Fcitx. Chinese characters can't be typed in Dota2.[GitHub Steam issue 493](https://github.com/ValveSoftware/Dota-2/issues/493)

The possible solution

Compile the `libSDL` with fcitx or ibus support, then replace `Game Folder/dota 2 beta/bin/libSDL2-2.0.so.0` with your version.

	[LibSDL+Ibus](http://forum.ubuntu.org.cn/viewtopic.php?f=34&t=460195)

	[LibSDL+Fcitx](http://forum.ubuntu.org.cn/viewtopic.php?f=34&t=466879&sid=1664abac47d8f639ed9b7f3abf94c675)

	[LibSDL+Fcitx Source](https://github.com/timxx/SDL-fcitx)

	[The solutions issues](https://github.com/ValveSoftware/Dota-2/issues/1650)

## Dwarfs F2P

Dependencies:

*   [lib32-libgdiplus](https://aur.archlinux.org/packages/lib32-libgdiplus/)

### Game does not start

There was a bug that stopped Steam from fetching all the needed files. It should be resolved, if you still bump into this problem, try verifying integrity of game cache from game properties, local files tab.

If the game still crashes at startup, edit `~/.local/share/Steam/SteamApps/common/Dwarfs - F2P/Run.sh` and change

```
export LD_LIBRARY_PATH=.:${LD_LIBRARY_PATH}

```

to

```
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:.

```

**Note:** This file may be overwritten by updates or by verifying integrity of game cache. You may need to modify it again.

If these do not help, you may have outdated libraries in the game installation folder that are crashing the game on startup. Try moving/removing the following files out of `~/.local/share/Steam/SteamApps/common/Dwarfs - F2P/` to fix it:

```
libX11.so.6, libsteam.so libtier0_s.so, libvstdlib_s.so, steamclient.so

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
/home/$USER/.local/share/Steam/SteamApps/common/Dynamite Jack/bin/main: error while loading shared libraries: libSDL-1.2.so.0: cannot open shared object file: No such file or directory

```

Install [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl) from [multilib](/index.php/Multilib "Multilib") and Dynamite Jack should start up.

## Euro Truck Simulator 2

### Shows only a black screen

Select safe mode when the game starts up.

## Football Manager 2014

This game will not run when installed on an [XFS](/index.php/XFS "XFS") or reiserfs filesystem. Workaround is to install on an ext4 filesystem.

## FORCED

Requires [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu).

This game has 32-bit and 64-bit binaries. For unknown reason, steam will launch the 32-bit binary even on 64-bit Arch Linux. When manually launching the 64-bit binary, the game starts, but cannot connect to Steam account, so you cannot play. So install 32-bits dependencies, and launch the game from Steam.

## FTL: Faster than Light

### Compatibility

After installation, FTL may fail to run due to a 'Text file busy' error (characterised in Steam by your portrait border going green then blue again). The easiest way to mend this is to just reboot your system. Upon logging back in FTL should run.

The Steam overlay in FTL does not function as it is not a 3D accelerated game. Because of this the desktop notifications will be visible. If playing in fullscreen, therefore, these notifications in some systems may steal focus and revert you back to windowed mode with no way of going back to fullscreen without relaunching. The binaries for FTL on Steam have no DRM and it is possible to run the game *without* Steam running, so in some cases that may be optimum - just ensure that you launch FTL via the launcher script in `~/.steam/root/SteamApps/common/FTL Faster than Light/data/` rather than the FTL binary in the $arch directory.

### Problems with open-source video driver

FTL may fail to run if you are using an opensource driver for your video card. There are two solutions: install a proprietary video driver or delete (rename if you are unsure) the library "libstdc++.so.6" inside `~/.steam/root/SteamApps/common/FTL\ Faster\ Than\ Light/data/amd64/lib`. This is if you are using a 64bit system. In case you are using a 32bit system you have to remove (rename) the same library located into `~/.steam/root/SteamApps/common/FTL\ Faster\ Than\ Light/data/x86/lib`.

## Game Dev Tycoon

### Game does not start

You might get an error about missing `libudev.so.0`. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

## Garry's Mod

### Game does not start

Error about missing client.so might appear, solution:

```
 cd SteamLibrary/SteamApps/common/GarrysMod/bin/
 ln -s libawesomium-1-7.so.0 libawesomium-1-7.so.2
 ln -s ../garrysmod/bin/client.so ./

```

If the error mentions a missing library for libgcrypt.so.11, install [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15).

### Opening some menus causes the game to crash

Most menus work fine, but ones with checkboxes (LAN multiplayer, mounted games list) do not work at all. This is a bug in the menu code.

If you prefer the default menu style and do not mind a hacky solution: [Simon311](https://github.com/Facepunch/garrysmod-issues/issues/86#issuecomment-30935491) has written code with instructions to fix it.

If you do not care for the default menu style and want a more stable but feature-incomplete solution, Facepunch developer [robotboy655](https://github.com/robotboy655/gmod-lua-menu) has written a new menu.

### Game crashes after attempting to join server

While in the process of joining a server, downloading resources, etc, the game seems to hang and after a while, perhaps during the "sending client info" portion the game crashes, usually without any error messages. Error does not give much information, however, the process for Garry's mod is killed.

This issue arises more often when joining servers with many addons like DarkRP servers specifically.

The Problem seems to correlate with a weak GPU and the game is timing out from the server, so if the GPU is the problem, lowering the graphics settings to minimum fixes the problem until you can upgrade ;).

## GRID Autosport

### OpenSSL 1.0

GRID is built against [openssl](https://www.archlinux.org/packages/?name=openssl) 1.0 exactly. If you have updated to openssl 1.1 or later GRID and some other steam games [will not work](https://bugs.archlinux.org/task/53618). To provide openssl 1.0 [install](/index.php/Install "Install") [libopenssl-1.0-compat](https://aur.archlinux.org/packages/libopenssl-1.0-compat/) and add the following launch option:

```
"LD_LIBRARY_PATH='/usr/lib/openssl-1.0-compat/' %command%"

```

### Game does not start (Black screen)

Starting the launcher is successful, but starting the game fails with a black screen. Solution: Right click on the game in your game list, click on "Properties", click on "SET LAUNCH OPTIONS", then add:

```
"LC_ALL=C %command%"

```

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

Although not a steam game, Halo: Custom Edition running under WINE and/or PlayOnLinux has many audio problems. To mitigate this, install dsound via winetricks or PlayOnLinux. Then, set the in-game "Sound Quality" to medium. If you have installed the campaign extra, this also restores all video cut-scene audio.

## Harvest: Massive Encounter

Dependencies:

*   [lib32-sfml](https://aur.archlinux.org/packages/lib32-sfml/)
*   [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo)
*   [lib32-nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=lib32-nvidia-cg-toolkit)
*   [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)

### Compatibility

Game refuses to launch and throws you to library installer loop. Just edit `~/.steam/root/SteamApps/common/Harvest Massive Encounter/run_harvest` and remove everything but

```
 #!/bin/bash
 exec ./Harvest

```

## Hatoful Boyfriend

### Japanese text invisible

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

## Hyper Light Drifter

### The controller does not work

Install [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2) and change the game launch options in Steam to:

```
LD_PRELOAD=libSDL2.so %command%

```

```
**Note 01:** Follow this [discussion](https://steamcommunity.com/app/257850/discussions/1/365163686036494421/?ctp=14) for specifically the controller issues, and follow this [discussion](https://steamcommunity.com/app/257850/discussions/1/365163686045397160/) for general bugs including the controller problems.
Both are considered the "bug reports" since they don't have an issue tracking system other than the support forum on Steam.

```

```
**Note 02:** It is suggested to run the *next_update* branch to get the fixes that have recently dropped,
however there is a libcurl segfault currently keeping it from starting at all without special workarounds.

```

### Missing libcurl.so.4 or version CURL_OPENSSL_3 not found

[Install](/index.php/Install "Install") [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat).

Right click on the game's entry in your Steam library, click on `Properties`, then `SET LAUNCH OPTIONS`, and use the following:

```
LD_PRELOAD=libcurl.so.3 %command%

```

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

There seem to be problems with the Steam overlay. Try to run the game directly with `~/Steam/SteamApps/common/TheInnerWorld/TIW_start.sh`.

Note that cutscenes open in a new window. So pay attention to that and switch to the new window to enjoy the movies.

See the [Steam Forums](http://steamcommunity.com/app/251430/discussions/0/611701360817206606/#c611701360827509770) for details.

## Interloper

Requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib).

### Game does not start

The game can sometimes segfault due to an incompatibility with the Steam Runtime's libasound.so.2\. See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

## Invisible Apartment

Requires [qt5-multimedia](https://www.archlinux.org/packages/?name=qt5-multimedia).

### Game does not start

When the game does not run when you launch it via Steam try to run it directly:

```
./$HOME/.steam/steam/SteamApps/common/Invisible\ Apartment/ia1

```

## Joe Danger 2: The Movie

Requires [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse).

### Compatibility

Game only worked after obtaining from the [Humble Bundle](https://www.humblebundle.com/‎) directly and [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) was installed.

## Kerbal Space Program

See [Kerbal Space Program](/index.php/Kerbal_Space_Program "Kerbal Space Program").

## Killing Floor

### Screen resolution

Killing Floor runs pretty much from scratch, although you might have to change in-game resolution screen as the default one is **800x600** and a **4:3** screen format. If you try to modify screen resolution in-game, it might crash your desktop enviroment. To fix this, please set the desired resolution screen size by [editing](/index.php/Textedit "Textedit") `~/.killingfloor/System/KillingFloor.ini`.

 `~/.killingfloor/System/KillingFloor.ini` 
```
...

[WinDrv.WindowsClient]
WindowedViewportX=????
WindowedViewportY=????
FullscreenViewportX=????
FullscreenViewportY=????
MenuViewportX=???
MenuViewportY=???

...

[SDLDrv.SDLClient]
WindowedViewportX=????
WindowedViewportY=????
FullscreenViewportX=????
FullscreenViewportY=????
MenuViewportX=????
MenuViewportY=????

...

```

**Note:** Replace all the `????` with the corresponding numbers according the desired resolution. If you have an 1366x768 screen and want to use it at it's fullest, change all the Viewport fields to something like `ViewportX=1366` and `ViewportY=768` in the corresponding areas.

**Note:** The dots in the middle indicate that there are more fields in that .ini file. But for screen resolution troubleshooting, you do not need to modify anything else.

Save the file and restart the game, it should work now.

### Windowed mode

Uncheck fullscreen in the options menu, and use `Ctrl+g` to stop mouse capturing (that was non-obvious to discover..). This way you can easily minimize it and do other other things..and let your WM handle things.

### Stuttering Sound

KillingFloor comes with its own libopenal.so (called openal.so). To use system lib instead install [openal](https://www.archlinux.org/packages/?name=openal) or [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal) (if using 64bit system). Then go to `$HOME/Steam/SteamApps/common/KillingFloor/System`. and rename openal.so to openal.so.bak Then create symlink to /usr/lib32/libopenal.so.1 or /usr/lib/libopenal.so.1 called openal.so

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

Right click on `Middle-earth: Shadow of Mordor` on your game list, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
__GL_ShaderPortabilityWarnings=0 %command%

```

## Multiwinia

Requires [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

### Crash on startup

If Multiwinia crashes on startup on X64 systems, force launching the 32-bit executable by replacing `~/.local/share/Steam/steamapps/common/Multiwinia/run_steam.sh` with the following script:

```
#!/bin/sh
./multiwinia.bin.x86

```

See [[4]](https://steamcommunity.com/app/1530/discussions/0/864969481950542663/#c558746995160431396).

## Natural Selection 2

Requires [lib32-speex](https://www.archlinux.org/packages/?name=lib32-speex).

### No Sound

If there is no sound in-game. Try installing [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl) and [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2).

If this fails, try setting the game's launch options in Steam to:

```
LD_LIBRARY_PATH="/usr/lib32:$LD_LIBRARY_PATH" %command%

```

## Nuclear Throne

### Missing libcurl.so.4 or version `CURL_OPENSSL_3' not found

Install [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat).

Right click on the game's entry in your Steam library, click on `Properties`, then `SET LAUNCH OPTIONS`, and use the following:

```
 LD_PRELOAD=libcurl.so.3 %command%

```

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

The game segfaults during program start because of the `LD_LIBRARY_PATH` setting in the launcher script. Edit `~/.local/share/Steam/SteamApps/common/ThePolynomial/Polynomial64`, and comment out the `LD_LIBRARY_PATH` variable. Make sure to put the `./bin/Polynomial64 "$@"` command on a new line.

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

To solve this just remove or move the three files `libSDL-1.2.so.0`, `libSDL_image-1.2.so.0`, `libSDL_mixer-1.2.so.0` from `~/.steam/root/SteamApps/common/SpaceChem`

## Splice

Requires [glu](https://www.archlinux.org/packages/?name=glu).

Splice comes with both x86 and x64 binaries. Steam does not have to be running to launch this game.

## Star Wars Battlefront II

Star wars battlefront 2's steam version running under [Wine](/index.php/Wine "Wine") has a bug which causes it to take forever to load a game. The solution is to compile a custom wine version with the patch from this [WINEHQ bug page](https://bugs.winehq.org/show_bug.cgi?id=29582) Instructions are at the bottom of the page.

**Note:** The required patch is called "updated patchset (GetForgroundWindow hack + posix semaphores) rebased onto wine-1.7.55".

In order to use the patched wine version with PlayOnLinux, copy the completely patched and compiled wine-1.7.55 folder to `~/.PlayOnLinux/wine/linux-x86/`.

## The Stanley Parable

### Game won't start

As discussed in Steam's store page, remove `libstdc++.so.6` from the game folder. For example:

```
$ rm ~/.local/share/Steam/steamapps/common/The\ Stanley\ Parable/bin/libstdc++.so.6

```

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

If you use Intel video card, just disable S3TC in DriConf.

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
$ cd "$HOME/.local/share/Steam/steamapps/common/Stephen's Sausage Roll"

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

[The game bundles with an outdated version of libstdc++](http://steamcommunity.com/app/204060/discussions/0/364039785161291413/) which prevents the game from starting. The following can be observed when you run Steam and S&S from the terminal:

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

To solve this problem remove the bunlded libstdc++ using:

```
$ rm "$HOME/.steam/steam/steamapps/common/Superbrothers Sword & Sworcery EP/lib/libstdc++.so.6*"

```

After that the game will use the libstdc++ from Steam.

## Tabletop Simulator

### CJK characters not showing in game

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

## Team Fortress 2

Requires [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12).

### Making HRTF work

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

This happens because of an incompatibility with the newer version of `lib32-curl`. To fix the problem you need to remove the bundled `libcurl.so.4`

```
$ rm "$HOME/.local/share/Steam/steamapps/common/This War of Mine/libcurl.so.4"

```

### Sound glitches with Steam native

The bundled `libOpenAL` might not work correctly, try the following:

```
$ ln -sf /usr/lib32/libopenal.so ~/.local/share/Steam/steamapps/common/This\ War\ of\ Mine/libOpenAL.so

```

## Ticket to Ride

Dependencies:

*   [lib32-gstreamer0.10-base](https://aur.archlinux.org/packages/lib32-gstreamer0.10-base/)
*   [lib32-pangox-compat](https://aur.archlinux.org/packages/lib32-pangox-compat/)

As lib32-gstreamer0.10-base is quite hard to build you can use [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repo for this package

## Tomb Raider

### Game immediately closes when running with steam-native

Tomb Raider has a very heavy amount of dependency on the Steam runtime, the easiest solution is to just run it using the runtime. You can do so by setting the following as the launch option:

 `/home/[your username]/.local/share/Steam/ubuntu12_32/steam-runtime/run.sh %command%` 

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

Otherwise, run the game via shell and set up proper audio device for FMOD, as discussed in [[5]](https://steamcommunity.com/app/237930/discussions/2/620695877176333955/).

Also, check out this thread [[6]](https://steamcommunity.com/app/237930/discussions/2/492378265893557247/)

## Transmissions: Element 120

Dependencies:

*   [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)

### Troubleshooting

Make sure you have all libraries installed. Above the standard set required by Steam runtime, the game requires few additional ones. The typical error message that indicates that is

```
AppFramework : Unable to load module vguimatsurface.so!

```

To show which dependencies are satisfied, go to the folder in which you installed the game (`SteamLibrary/steamapps/common/Transmissions Element 120`) and execute:

```
LD_LIBRARY_PATH=bin ldd bin/vguimatsurface.so

```

look for entries that say `not found`

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

Right click on the game's entry in your Steam library, click on `Properties`, then `SET LAUNCH OPTIONS`, and add this line:

 `MESA_GL_VERSION_OVERRIDE=4.0 MESA_GLSL_VERSION_OVERRIDE=400 %command%` 

## Unity of Command

Requires [lib32-pango](https://www.archlinux.org/packages/?name=lib32-pango).

### Squares

If squares are shown instead of text, try removing `$HOME/Steam/SteamApps/common/Unity of Command/bin/libpangoft2-1.0.so.0`.

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

The sound system in Unity 5 changed and to be able to play games created with it you must most likely install and run [PulseAudio](/index.php/PulseAudio "PulseAudio"). Another solution is to disable the Steam runtime: in the launch options for the game, write this: `LD_LIBRARY_PATH="" %command%`

### Game launching on wrong monitor in fullscreen mode

Unity games that do not support monitor selection will most likely launch the game on a wrong monitor.

The problem is that Unity games write the default param `<pref name="UnitySelectMonitor" type="int">-1</pref>` to the game config file.

This will lead to the game launching on a non-primary monitor.

When changing to value into `<pref name="UnitySelectMonitor" type="int">**0**</pref>` for the according game, the game will start on the correct (primary) monitor.

A Unity game config file usually resides in `~/.config/unity3d/[CompanyName]/[ProductName]/prefs`.

Some of the affected games: *Cities: Skylines*, *Tablestop Simulator*, *Assault Android Cactus*, *Wasteland 2*, *Tyranny*.

Be aware that some games do not support setting that parameter, it will simply be ignored. This is the case for *Pillars of Eternity*, *Kentucky Route Zero*, *Sunless Sea*.

## Unrest

Requires [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth).

## War Thunder

### Blank screen

If having a green or blank screen at game start, set the `MESA_GL_VERSION_OVERRIDE=4.1COMPAT` [environment variable](/index.php/Environment_variable "Environment variable"). [[7]](https://forum.warthunder.com/index.php?/topic/267809-linux-potential-workaround-for-mesa-drivers-black-screen/) [[8]](http://forum.warthunder.com/index.php?search_term=0030709&app=core&module=search&do=search&fromMainBar=1&search_app=forums%3Aforum%3A920&sort_field=&sort_order=&search_in=posts)

## Warhammer 40,000: Dawn of War II

Dependencies:

*   [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib)
*   [librtmp0](https://www.archlinux.org/packages/?name=librtmp0)

The start script does not point to the right direction of `libasound.so.2`.

To fix it open `$HOME/.steam/steam/steamapps/common/Dawn of War 2/DawnOfWar2.sh` and replace the following lines:

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
$ cd "$HOME/.local/share/Steam/SteamApps/common/the witcher 2"
$ LIBGL_DEBUG=verbose ./witcher2

```

## Wizardry 6: Bane of the Cosmic Forge

Requires [DOSBox](/index.php/DOSBox "DOSBox").

To fix the crash at start, open `~/.local/share/Steam/SteamApps/common/Wizardry6/dosbox_linux/launch_wizardry6.sh` and:

*   comment the line `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./libs`
*   change the beginning of the line starting with `exec ./dosbox` to `exec dosbox`

## World of Goo

### Changing resolution

*   To change the game resolution edit the section "Graphics display" in the configuration file `$HOME/Steam/SteamApps/common/World of Goo/properties/config.txt`. For example, see below:

```
 <param name="screen_width" value="1680" />
 <param name="screen_height" value="1050" />
 <param name="color_depth" value="0" />
 <param name="fullscreen" value="true" />
 <param name="ui_inset" value="10" />

```

## XCOM

Dependencies:

*   [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image) (Required to enable keyboard functionality in-game)
*   [librtmp0](https://www.archlinux.org/packages/?name=librtmp0) (Required to run the game)

### Hangs on startup

See [Steam/Troubleshooting#Steam runtime issues](/index.php/Steam/Troubleshooting#Steam_runtime_issues "Steam/Troubleshooting").

If you are running a hybrid graphic system, try

```
__GL_THREADED_OPTIMIZATIONS=0 primusrun %command%

```

### Graphical glitches on Intel HD

XCOM may not recognize the SDL2 shared libraries shipped with the Steam runtime. Check if the binary finds all required files and install missing packages if necessary ([sdl2](https://www.archlinux.org/packages/?name=sdl2) and [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image)).

 `ldd ~/.local/share/Steam/steamapps/common/XCom-Enemy-Unknown/binaries/linux/game.x86_64 `