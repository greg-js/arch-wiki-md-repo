See [Steam](/index.php/Steam "Steam") for the main article, and [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting") for generic troubleshooting.

**Note:** [Steam](/index.php/Steam "Steam") installs library dependencies of a game to a library directory, but some are missing at the moment. Report bugs involving missing libraries on Valve's bug tracker on their [GitHub page](https://github.com/ValveSoftware/steam-for-linux) before adding workarounds here, and then provide a link to the bug so it can be removed as the problems are fixed.

**Tip:** If a game fails to start, a possible reason is that it is missing required libraries. You can find out what libraries it requests by running `ldd *game_executable*`. `*game_executable*` is likely located somewhere in `~/.steam/root/SteamApps/common/`. Please note that most of these "missing" libraries are actually already included with Steam, and do not need to be installed globally.

## Contents

*   [1 Air Brawl](#Air_Brawl)
    *   [1.1 Dependencies](#Dependencies)
    *   [1.2 Menus are missing text/blacked out](#Menus_are_missing_text.2Fblacked_out)
*   [2 Amnesia: The Dark Descent](#Amnesia:_The_Dark_Descent)
    *   [2.1 Dependencies](#Dependencies_2)
*   [3 And Yet It Moves](#And_Yet_It_Moves)
    *   [3.1 Dependencies](#Dependencies_3)
    *   [3.2 Compatibility](#Compatibility)
*   [4 Anodyne](#Anodyne)
    *   [4.1 Dependencies](#Dependencies_4)
    *   [4.2 Compatibility](#Compatibility_2)
*   [5 Aquaria](#Aquaria)
    *   [5.1 Mouse pointer gets stuck in one direction](#Mouse_pointer_gets_stuck_in_one_direction)
*   [6 Audiosurf 2](#Audiosurf_2)
    *   [6.1 Dependencies](#Dependencies_5)
*   [7 Binding of Isaac: Rebirth](#Binding_of_Isaac:_Rebirth)
    *   [7.1 Troubleshooting](#Troubleshooting)
        *   [7.1.1 No sound](#No_sound)
*   [8 Borderlands 2](#Borderlands_2)
    *   [8.1 Syncing save games](#Syncing_save_games)
    *   [8.2 Using Ctrl Key](#Using_Ctrl_Key)
    *   [8.3 Logging into SHiFT](#Logging_into_SHiFT)
*   [9 Borderlands the Pre-Sequel](#Borderlands_the_Pre-Sequel)
*   [10 Cities in Motion 2](#Cities_in_Motion_2)
    *   [10.1 Dialog boxes fail to display properly](#Dialog_boxes_fail_to_display_properly)
*   [11 Cities Skylines](#Cities_Skylines)
    *   [11.1 Textures not rendering properly](#Textures_not_rendering_properly)
*   [12 Civilization V](#Civilization_V)
    *   [12.1 Stuttering sound with PulseAudio](#Stuttering_sound_with_PulseAudio)
*   [13 Counter-Strike: Global Offensive (CS:GO)](#Counter-Strike:_Global_Offensive_.28CS:GO.29)
    *   [13.1 Game runs on the wrong screen](#Game_runs_on_the_wrong_screen)
    *   [13.2 Cannot reach bottom of the screen on menues](#Cannot_reach_bottom_of_the_screen_on_menues)
    *   [13.3 Audio is not synced](#Audio_is_not_synced)
    *   [13.4 Unable to aim when in game](#Unable_to_aim_when_in_game)
    *   [13.5 Mouse Deadzone](#Mouse_Deadzone)
    *   [13.6 Low Performance on AMD card using Catalyst proprietary driver ( <= 15.7 )](#Low_Performance_on_AMD_card_using_Catalyst_proprietary_driver_.28_.3C.3D_15.7_.29)
    *   [13.7 Brightness slider not working](#Brightness_slider_not_working)
*   [14 Crusader Kings II](#Crusader_Kings_II)
    *   [14.1 Dependencies (x86_64)](#Dependencies_.28x86_64.29)
    *   [14.2 Tips and tricks](#Tips_and_tricks)
    *   [14.3 Troubleshooting](#Troubleshooting_2)
        *   [14.3.1 No audio](#No_audio)
        *   [14.3.2 Odd Sized Starting Window](#Odd_Sized_Starting_Window)
*   [15 Death Road To Canada](#Death_Road_To_Canada)
    *   [15.1 Troubleshooting](#Troubleshooting_3)
        *   [15.1.1 No music](#No_music)
*   [16 Defender's Quest: Valley of the Forgotten](#Defender.27s_Quest:_Valley_of_the_Forgotten)
    *   [16.1 Dependencies](#Dependencies_6)
    *   [16.2 Troubleshooting](#Troubleshooting_4)
        *   [16.2.1 Game does not start](#Game_does_not_start)
*   [17 Divinity: Original Sin Enhanced Edition](#Divinity:_Original_Sin_Enhanced_Edition)
    *   [17.1 Game doesn't start when using Bumblebee optirun or primusrun](#Game_doesn.27t_start_when_using_Bumblebee_optirun_or_primusrun)
*   [18 Don't Starve](#Don.27t_Starve)
    *   [18.1 Dependencies (x86_64)](#Dependencies_.28x86_64.29_2)
    *   [18.2 Troubleshooting](#Troubleshooting_5)
        *   [18.2.1 No sound](#No_sound_2)
*   [19 Dota 2](#Dota_2)
    *   [19.1 Dependencies (x86_64)](#Dependencies_.28x86_64.29_3)
    *   [19.2 Dependencies (Dota 2 reborn)](#Dependencies_.28Dota_2_reborn.29)
    *   [19.3 Troubleshooting](#Troubleshooting_6)
        *   [19.3.1 In-game font is unreadable](#In-game_font_is_unreadable)
        *   [19.3.2 Everything seems OK but the game doesn't start](#Everything_seems_OK_but_the_game_doesn.27t_start)
        *   [19.3.3 Game runs on the wrong screen](#Game_runs_on_the_wrong_screen_2)
        *   [19.3.4 Game does not start with libxcb-dri3 error message](#Game_does_not_start_with_libxcb-dri3_error_message)
        *   [19.3.5 Steam overlay](#Steam_overlay)
        *   [19.3.6 Chinese Tips and player's name display problem](#Chinese_Tips_and_player.27s_name_display_problem)
        *   [19.3.7 Chinese input method problem](#Chinese_input_method_problem)
*   [20 Dwarfs F2P](#Dwarfs_F2P)
    *   [20.1 Dependencies](#Dependencies_7)
    *   [20.2 Troubleshooting](#Troubleshooting_7)
        *   [20.2.1 Game does not start](#Game_does_not_start_2)
        *   [20.2.2 Game crashes](#Game_crashes)
*   [21 Dynamite Jack](#Dynamite_Jack)
    *   [21.1 Dependencies](#Dependencies_8)
    *   [21.2 Troubleshooting](#Troubleshooting_8)
        *   [21.2.1 Sound Issues](#Sound_Issues)
        *   [21.2.2 Game does not start](#Game_does_not_start_3)
*   [22 Football Manager 2014](#Football_Manager_2014)
*   [23 FORCED](#FORCED)
    *   [23.1 Dependencies](#Dependencies_9)
*   [24 FTL: Faster than Light](#FTL:_Faster_than_Light)
    *   [24.1 Dependencies](#Dependencies_10)
    *   [24.2 Compatibility](#Compatibility_3)
    *   [24.3 Problems with open-source video driver](#Problems_with_open-source_video_driver)
*   [25 Game Dev Tycoon](#Game_Dev_Tycoon)
    *   [25.1 Troubleshooting](#Troubleshooting_9)
        *   [25.1.1 Game does not start](#Game_does_not_start_4)
*   [26 Garry's Mod](#Garry.27s_Mod)
    *   [26.1 Troubleshooting](#Troubleshooting_10)
        *   [26.1.1 Game does not start](#Game_does_not_start_5)
        *   [26.1.2 Opening some menus causes the game to crash](#Opening_some_menus_causes_the_game_to_crash)
    *   [26.2 Game crashes after attempting to join server](#Game_crashes_after_attempting_to_join_server)
*   [27 Hack 'n' Slash](#Hack_.27n.27_Slash)
    *   [27.1 Troubleshooting](#Troubleshooting_11)
        *   [27.1.1 The game starts but craches when loading a new or saved game](#The_game_starts_but_craches_when_loading_a_new_or_saved_game)
*   [28 Hacker Evolution [Untold, Duality]](#Hacker_Evolution_.5BUntold.2C_Duality.5D)
    *   [28.1 Dependencies](#Dependencies_11)
*   [29 Half-Life 2 & episodes](#Half-Life_2_.26_episodes)
    *   [29.1 Cyrillic fonts problem](#Cyrillic_fonts_problem)
*   [30 Hammerwatch](#Hammerwatch)
    *   [30.1 Troubleshooting](#Troubleshooting_12)
        *   [30.1.1 The game not starting from Steam GUI](#The_game_not_starting_from_Steam_GUI)
        *   [30.1.2 No sound](#No_sound_3)
*   [31 Harvest: Massive Encounter](#Harvest:_Massive_Encounter)
    *   [31.1 Dependencies](#Dependencies_12)
    *   [31.2 Compatibility](#Compatibility_4)
*   [32 Hatoful Boyfriend](#Hatoful_Boyfriend)
    *   [32.1 Japanese text invisible](#Japanese_text_invisible)
*   [33 The inner world](#The_inner_world)
    *   [33.1 Bringing up the inventory or main menu](#Bringing_up_the_inventory_or_main_menu)
    *   [33.2 Dependencies](#Dependencies_13)
        *   [33.2.1 Sound support](#Sound_support)
        *   [33.2.2 Cutscenes](#Cutscenes)
*   [34 Interloper](#Interloper)
    *   [34.1 Dependencies](#Dependencies_14)
    *   [34.2 Game does not launch](#Game_does_not_launch)
*   [35 Invisible Apartment](#Invisible_Apartment)
    *   [35.1 Dependencies](#Dependencies_15)
    *   [35.2 Game does not run](#Game_does_not_run)
*   [36 Joe Danger 2: The Movie](#Joe_Danger_2:_The_Movie)
    *   [36.1 Dependencies](#Dependencies_16)
    *   [36.2 Compatibility](#Compatibility_5)
*   [37 Kerbal Space Program](#Kerbal_Space_Program)
    *   [37.1 Troubleshooting](#Troubleshooting_13)
    *   [37.2 Game never progresses past initial loading](#Game_never_progresses_past_initial_loading)
    *   [37.3 No text display](#No_text_display)
    *   [37.4 Graphics flickering when using primusrun](#Graphics_flickering_when_using_primusrun)
    *   [37.5 Game crashes when accessing settings or saves on 64 bit systems on Steam](#Game_crashes_when_accessing_settings_or_saves_on_64_bit_systems_on_Steam)
    *   [37.6 Locale settings](#Locale_settings)
    *   [37.7 No audio on 64-bit systems](#No_audio_on_64-bit_systems)
    *   [37.8 Black ingame textures](#Black_ingame_textures)
    *   [37.9 See also](#See_also)
*   [38 Killing Floor](#Killing_Floor)
    *   [38.1 Troubleshooting](#Troubleshooting_14)
        *   [38.1.1 Screen resolution](#Screen_resolution)
        *   [38.1.2 Windowed mode](#Windowed_mode)
        *   [38.1.3 Stuttering Sound](#Stuttering_Sound)
*   [39 Lethal League](#Lethal_League)
    *   [39.1 Dependencies](#Dependencies_17)
*   [40 Metro: Last Light](#Metro:_Last_Light)
    *   [40.1 Attempted fixes](#Attempted_fixes)
    *   [40.2 Hacky solution](#Hacky_solution)
    *   [40.3 Possible solutions](#Possible_solutions)
*   [41 Mark of the Ninja](#Mark_of_the_Ninja)
    *   [41.1 Troubleshooting](#Troubleshooting_15)
        *   [41.1.1 Bad sound](#Bad_sound)
*   [42 Middle-earth: Shadow of Mordor](#Middle-earth:_Shadow_of_Mordor)
    *   [42.1 Floating heads](#Floating_heads)
*   [43 Multiwinia](#Multiwinia)
    *   [43.1 Dependencies](#Dependencies_18)
    *   [43.2 Crash on startup](#Crash_on_startup)
*   [44 Natural Selection 2](#Natural_Selection_2)
    *   [44.1 No Sound](#No_Sound_4)
*   [45 Penumbra: Overture](#Penumbra:_Overture)
    *   [45.1 Dependencies](#Dependencies_19)
    *   [45.2 Troubleshooting](#Troubleshooting_16)
        *   [45.2.1 Windowed mode](#Windowed_mode_2)
*   [46 Portal 2](#Portal_2)
    *   [46.1 Troubleshooting](#Troubleshooting_17)
        *   [46.1.1 Game does not start](#Game_does_not_start_6)
*   [47 Prison Architect](#Prison_Architect)
    *   [47.1 Troubleshooting](#Troubleshooting_18)
        *   [47.1.1 ALSA error when using PulseAudio](#ALSA_error_when_using_PulseAudio)
*   [48 Project Zomboid](#Project_Zomboid)
    *   [48.1 Dependencies](#Dependencies_20)
    *   [48.2 No sound](#No_sound_5)
*   [49 Redshirt](#Redshirt)
    *   [49.1 Dependencies (x86_64)](#Dependencies_.28x86_64.29_4)
*   [50 Revenge of the Titans](#Revenge_of_the_Titans)
    *   [50.1 Dependencies](#Dependencies_21)
*   [51 Rock Boshers DX: Directors Cut](#Rock_Boshers_DX:_Directors_Cut)
    *   [51.1 Dependencies](#Dependencies_22)
*   [52 Serious Sam 3: BFE](#Serious_Sam_3:_BFE)
    *   [52.1 Dependencies](#Dependencies_23)
    *   [52.2 Troubleshooting](#Troubleshooting_19)
        *   [52.2.1 No audio](#No_audio_2)
*   [53 Sir, you are being hunted](#Sir.2C_you_are_being_hunted)
    *   [53.1 Dependencies](#Dependencies_24)
*   [54 Spacechem](#Spacechem)
    *   [54.1 Dependencies](#Dependencies_25)
    *   [54.2 Troubleshooting](#Troubleshooting_20)
        *   [54.2.1 Game crash](#Game_crash)
*   [55 Space Pirates and Zombies](#Space_Pirates_and_Zombies)
    *   [55.1 Dependencies](#Dependencies_26)
    *   [55.2 Troubleshooting](#Troubleshooting_21)
        *   [55.2.1 No audio](#No_audio_3)
*   [56 Splice](#Splice)
    *   [56.1 Dependencies](#Dependencies_27)
*   [57 Steel Storm: Burning Retribution](#Steel_Storm:_Burning_Retribution)
    *   [57.1 Troubleshooting](#Troubleshooting_22)
        *   [57.1.1 Start with black screen](#Start_with_black_screen)
        *   [57.1.2 No English fonts](#No_English_fonts)
*   [58 Stephen's Sausage Roll](#Stephen.27s_Sausage_Roll)
    *   [58.1 Troubleshooting](#Troubleshooting_23)
        *   [58.1.1 No sound](#No_sound_6)
*   [59 Strike Suite Zero](#Strike_Suite_Zero)
    *   [59.1 Dependencies](#Dependencies_28)
*   [60 Superbrothers: Sword & Sworcery EP](#Superbrothers:_Sword_.26_Sworcery_EP)
    *   [60.1 Dependencies](#Dependencies_29)
*   [61 Team Fortress 2](#Team_Fortress_2)
    *   [61.1 Dependencies](#Dependencies_30)
    *   [61.2 Making HRTF work](#Making_HRTF_work)
    *   [61.3 Troubleshooting](#Troubleshooting_24)
        *   [61.3.1 Loading screen freeze](#Loading_screen_freeze)
        *   [61.3.2 No audio](#No_audio_4)
        *   [61.3.3 Slow loading textures](#Slow_loading_textures)
        *   [61.3.4 NVIDIA drivers](#NVIDIA_drivers)
*   [62 Terraria](#Terraria)
*   [63 The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales)
    *   [63.1 Dependencies](#Dependencies_31)
*   [64 The Book of Unwritten Tales: The Critter Chronicles](#The_Book_of_Unwritten_Tales:_The_Critter_Chronicles)
*   [65 The Clockwork Man](#The_Clockwork_Man)
    *   [65.1 Dependencies](#Dependencies_32)
*   [66 The Polynomial](#The_Polynomial)
    *   [66.1 Dependencies](#Dependencies_33)
    *   [66.2 Troubleshooting](#Troubleshooting_25)
        *   [66.2.1 Segfaults during program start on 64-bit systems](#Segfaults_during_program_start_on_64-bit_systems)
*   [67 The Stanley Parable](#The_Stanley_Parable)
    *   [67.1 Troubleshooting](#Troubleshooting_26)
        *   [67.1.1 Game won't start](#Game_won.27t_start)
*   [68 This War of Mine](#This_War_of_Mine)
    *   [68.1 Troubleshooting](#Troubleshooting_27)
        *   [68.1.1 Game doesn't load](#Game_doesn.27t_load)
*   [69 Tomb Raider](#Tomb_Raider)
    *   [69.1 Troubleshooting](#Troubleshooting_28)
        *   [69.1.1 Game immediately closes when running with steam-native](#Game_immediately_closes_when_running_with_steam-native)
        *   [69.1.2 Steam Controller not working ingame while being correctly recognised* by Steam outside of the game](#Steam_Controller_not_working_ingame_while_being_correctly_recognised.2A_by_Steam_outside_of_the_game)
*   [70 Towns / Towns Demo](#Towns_.2F_Towns_Demo)
    *   [70.1 Crash on launch](#Crash_on_launch)
*   [71 Transistor](#Transistor)
    *   [71.1 Crash on launch / FMOD binding crash / Audio issues](#Crash_on_launch_.2F_FMOD_binding_crash_.2F_Audio_issues)
*   [72 Transmissions: Element 120](#Transmissions:_Element_120)
    *   [72.1 Troubleshooting](#Troubleshooting_29)
    *   [72.2 Dependencies](#Dependencies_34)
*   [73 Trine 2](#Trine_2)
    *   [73.1 Dependencies](#Dependencies_35)
    *   [73.2 Troubleshooting](#Troubleshooting_30)
*   [74 Unity3D](#Unity3D)
    *   [74.1 Locale Settings](#Locale_Settings_2)
    *   [74.2 Unity 5 sound problems](#Unity_5_sound_problems)
    *   [74.3 Game launching on wrong monitor in fullscreen mode](#Game_launching_on_wrong_monitor_in_fullscreen_mode)
*   [75 Unity of Command](#Unity_of_Command)
    *   [75.1 Dependencies](#Dependencies_36)
    *   [75.2 Troubleshooting](#Troubleshooting_31)
        *   [75.2.1 No audio](#No_audio_5)
*   [76 Unrest](#Unrest)
    *   [76.1 Dependencies](#Dependencies_37)
*   [77 War Thunder](#War_Thunder)
    *   [77.1 Troubleshooting](#Troubleshooting_32)
*   [78 Witcher 2: Assassin of Kings](#Witcher_2:_Assassin_of_Kings)
    *   [78.1 Dependencies](#Dependencies_38)
    *   [78.2 Troubleshooting](#Troubleshooting_33)
*   [79 Wizardry 6: Bane of the Cosmic Forge](#Wizardry_6:_Bane_of_the_Cosmic_Forge)
    *   [79.1 Dependencies](#Dependencies_39)
*   [80 World of Goo](#World_of_Goo)
    *   [80.1 Changing resolution](#Changing_resolution)
*   [81 Worms Reloaded](#Worms_Reloaded)
    *   [81.1 Dependencies](#Dependencies_40)
*   [82 XCOM](#XCOM)
    *   [82.1 Dependencies](#Dependencies_41)
    *   [82.2 Hangs on startup](#Hangs_on_startup)
    *   [82.3 Graphical glitches on Intel HD](#Graphical_glitches_on_Intel_HD)
*   [83 Saints Row IV](#Saints_Row_IV)
    *   [83.1 Game fails to launch after update to new Nvidia drivers](#Game_fails_to_launch_after_update_to_new_Nvidia_drivers)

## Air Brawl

### Dependencies

*   [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts)

### Menus are missing text/blacked out

Air Brawl seems to require some fonts that are missing, installing the package [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts) may fix it.

## Amnesia: The Dark Descent

### Dependencies

*   [lib32-freealut](https://aur.archlinux.org/packages/lib32-freealut/)
*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxmu](https://www.archlinux.org/packages/?name=lib32-libxmu)
*   [lib32-sdl_ttf](https://www.archlinux.org/packages/?name=lib32-sdl_ttf)

## And Yet It Moves

### Dependencies

*   [lib32-libtheora](https://www.archlinux.org/packages/?name=lib32-libtheora)
*   [lib32-libjpeg6](https://aur.archlinux.org/packages/lib32-libjpeg6/)
*   [lib32-libtiff4](https://aur.archlinux.org/packages/lib32-libtiff4/)
*   [lib32-libpng12](https://aur.archlinux.org/packages/lib32-libpng12/)

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

### Dependencies

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/)
*   [xterm](https://www.archlinux.org/packages/?name=xterm) (probably not actually required)

### Compatibility

Follow the same steps as [Defender's Quest](#Defender.27s_Quest:_Valley_of_the_Forgotten)

## Aquaria

### Mouse pointer gets stuck in one direction

If the mouse pointer gets stuck in any one direction, the game becomes unplayable. You may try:

 `~/.local/share/Steam/SteamApps/common/Aquaria/usersettings.xml` 
```
#<JoystickEnabled on=”1″ />
<JoystickEnabled on=”0″ />
```

If that does not fix the issue, unplug any joystick or joystick adapter devices you may have plugged in.

## Audiosurf 2

### Dependencies

*   [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)

## Binding of Isaac: Rebirth

### Troubleshooting

#### No sound

Right click on `Binding of Isaac: Rebirth` on your game list, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

In the game, go to the options and set all audio to the proper volume.

## Borderlands 2

### Syncing save games

Steam Cloud syncing does not (intentionally) work between platforms. With that said gave save files can be manually moved between systems. Save locations can be found here: [http://pcgamingwiki.com/wiki/Borderlands_2#Game_data](http://pcgamingwiki.com/wiki/Borderlands_2#Game_data). Once backed up to a FAT32 or other cross-compatible file-system thumbdrive (or the cloud), move the saved files to your GNU/Linux system, locate your saved file location, and move into the 17-digit long numeric file name. If previous saves on your GNU/Linux system can be deleted you can do so now. The key fix that I found was a need to change the ownership, group, and permissions. I used `chown steam:steam *` and then `chmod 0660 *` to get my moved saved files to work.

### Using Ctrl Key

Borderlands 2 does not allow the Ctrl key to be used by default. The game seems to be accessing keycodes and not keysyms, therefore xmodmap has no affect. A workaround is using *setkeycodes* to map the Ctrl-scancode to some other key, as described in [Map scancodes to keycodes#Using setkeycodes](/index.php/Map_scancodes_to_keycodes#Using_setkeycodes "Map scancodes to keycodes"). I use `setkeycodes 0x1d 56` (as root) to map Ctrl to Alt before starting the game and `setkeycodes 0x1d 29` to restore the default.

### Logging into SHiFT

The Linux version of Borderlands 2 expects to be run on Ubuntu, as that is the "officially" supported distro for Steam. As a result of this, when attempting to log in to SHiFT, it will fail, claiming the server is not available. Using strace, it can be seen that it fails to connect to the server because it cannot load SSL certificates from /usr/lib/ssl, which is the Ubuntu filesystem spec. Arch uses /etc/ssl. This can be fixed by symlinking /etc/ssl to /usr/lib/ssl, like so:

```
# ln -s /etc/ssl /usr/lib/ssl

```

To avoid symlinking an alternative to the above is to add the following to the launch options in Steam:

```
SSL_CERT_DIR="/etc/ssl/certs" %command%

```

Using one method or the other you will now be able to log into SHiFT to redeem SHiFT codes.

## Borderlands the Pre-Sequel

Borderlands the Pre-Sequel (and maybe Borderlands 2) might not be able to connect to the Gearbox SHIFT-service, this is related to a wrong path to the available SSL certificates. This can be solved by creating a symbolic link from `/etc/ssl` to `/usr/lib/ssl`. See [this comment on the steam discussion forum](http://steamcommunity.com/app/49520/discussions/0/616189742722687689/#c616189742811551908).

As an alternative the following can be added to the launch options in Steam:

```
SSL_CERT_DIR="/etc/ssl/certs" %command%

```

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

In Steam client set launch properties for game:

```
UNITY_DISABLE_GRAPHICS_DRIVER_WORKAROUNDS=yes %command%

```

## Civilization V

### Stuttering sound with PulseAudio

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting").

## Counter-Strike: Global Offensive (CS:GO)

### Game runs on the wrong screen

[GitHub Counter-Strike: Global Offensive issue #60](https://github.com/ValveSoftware/Counter-Strike-Global-Offensive/issues/60)

If it happens, you can fix it by going into fullscreen windowed or windowed mode and then dragging the game onto the correct monitor. After you go back in fullscreen, the game should be on the correct monitor.

### Cannot reach bottom of the screen on menues

[GitHub Counter-Strike: Global Offensive issue #594](https://github.com/ValveSoftware/Counter-Strike-Global-Offensive/issues/594)

If you have a secondary monitor you might have a part of your lower screen you cannot reach on menues. If on Gnome you can try to open the overview (Super key) and drag the game to the other monitor and back.

If you are not on Gnome or dragging the window back and forth did not work you can try to install and run this command, where X and Y is the offset of the window and H and W is the size.

```
wmctrl -r "Counter-Strike: Global Offensive - OpenGL" -e 0,X,Y,H,W

```

**Example**: SecondaryMonitor: on the left 2560x1600, GamingMonitor: on the right 2560x1440).

```
wmctrl -r "Counter-Strike: Global Offensive - OpenGL" -e 0,2560,0,1600,1200

```

Here X and Y is 0,2560 to move the window to the monitor on the right and H and W 1600,1200 is set to match the ingame resolution.

### Audio is not synced

[GitHub Counter-Strike: Global Offensive issue #45](https://github.com/ValveSoftware/Counter-Strike-Global-Offensive/issues/45)

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting") for a possible solution.

### Unable to aim when in game

Unable to aim when in game. However, the mouse cursor does works in GUI such as main menu, game menu, etc. Add this line to your `.bash_profile` and relogin:

```
export SDL_VIDEO_X11_DGAMOUSE=0

```

See also [[1]](https://bbs.archlinux.org/viewtopic.php?id=184905).

### Mouse Deadzone

Small mouse movements (less than under 5 pixels per second) does not register on X or an OpenGL games.

Solution[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1519944#p1519944):

```
sudo pacman -R x86-input-libinput libinput

```

### Low Performance on AMD card using Catalyst proprietary driver ( <= 15.7 )

Solution[[3]](http://www.phoronix.com/scan.php?page=article&item=amd-csgo-workaround&num=1):

```
cd ~/.steam/steam/steamapps/common/Counter-Strike\ Global\ Offensive
mv csgo_linux hl2_linux

```

Now edit csgo.sh

```
nano csgo.sh

```

and change

```
GAMEEXE=csgo_linux

```

to

```
GAMEEXE=hl2_linux

```

### Brightness slider not working

First, find out your current display output name (connected one):

```
xrandr | grep -v disconnected | grep connected

```

In my case, it's

```
**DFP9** connected

```

Edit csgo.sh

```
nano ~/.steam/steam/steamapps/common/Counter-Strike\ Global\ Offensive/csgo.sh

```

and add the following lines (change the OUTPUT_NAME to one you found with xrandr)

```
**# gamma correction**
**xrandr --output <OUTPUT_NAME> --gamma 1.6:1.6:1.6 # play with values if required**
STATUS=42
while [ $STATUS -eq 42 ]; do
 ...
done
**# restore gamma**
**xrandr --output <OUTPUT_NAME> --gamma 1:1:1**
exit $STATUS

```

## Crusader Kings II

### Dependencies (x86_64)

*   [lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl)

### Tips and tricks

Game is installed into `$HOME/Steam/SteamApps/common/Crusader Kings II`. Game can be started directly, without need of running Steam on background, using command `$HOME/Steam/SteamApps/common/Crusader Kings II/ck2`.

Saves are stored in `$HOME/Documents/Paradox Interactive/Crusader Kings II/save games/`. In the newest version (2.03), save-game files seem to be stored to `$HOME/.paradoxinteractive/Crusader Kings II/`. If your documents folder is empty, try looking there.

### Troubleshooting

#### No audio

The default audio driver used by Crusader Kings 2 is for [PulseAudio](/index.php/PulseAudio "PulseAudio"), so an override is necessary:

 `~/.pam_environment`  `SDL_AUDIODRIVER=alsa` 

#### Odd Sized Starting Window

Enable full screen mode as the default. In `~/.paradoxinteractive/Crusader Kings II/settings.txt` change fullscreen=no to fullscreen=yes.

## Death Road To Canada

### Troubleshooting

#### No music

Right click on `Death Road To Canada` on your game list, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

## Defender's Quest: Valley of the Forgotten

### Dependencies

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/)
*   [xterm](https://www.archlinux.org/packages/?name=xterm)
*   [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra)

### Troubleshooting

#### Game does not start

*   Package [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/) installs Adobe Air not in the place where the game expects it to be, fix this by creating a symlink (requires root permissions):

 `$ ln -s /opt/adobe-air-sdk/runtimes/air/linux/Adobe\ AIR /opt/Adobe\ AIR` 

*   Adobe AIR will want to check whether the EULA was accepted and fail in doing so. To fix it, issue the following commands (from under your user, not under root):

```
$ mkdir -p ~/.appdata/Adobe/AIR
$ echo 2 > ~/.appdata/Adobe/AIR/eulaAccepted
```

**Note:** By issuing these commands you're accepting Adobe Air's EULA.

## Divinity: Original Sin Enhanced Edition

### Game doesn't start when using Bumblebee optirun or primusrun

Edit `<path to library>/SteamApps/common/Divinity Original Sin Enhanced Edition/runner.sh` to have it use primusrun:

```
LD_LIBRARY_PATH="." primusrun ./EoCApp

```

## Don't Starve

### Dependencies (x86_64)

*   [lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin)
*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) (Looks like it fixes sound in some cases. See [this github issue](https://github.com/ValveSoftware/steam-for-linux/issues/2968) for details)
*   [lib32-libcurl-compat](https://aur.archlinux.org/packages/lib32-libcurl-compat/) (Requires further commands after installation as described [here](http://steamcommunity.com/app/219740/discussions/2/620700960796078576/#c611704730329482542))

### Troubleshooting

#### No sound

Right click on Don't Starve on your game list, click on Properties, click on SET LAUNCH OPTIONS, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

On the game, go to the option and set all audio to the proper volume.

## Dota 2

### Dependencies (x86_64)

*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) (if you use PulseAudio)
*   [lib32-fontconfig](https://www.archlinux.org/packages/?name=lib32-fontconfig)

### Dependencies (Dota 2 reborn)

*   [libpng12](https://www.archlinux.org/packages/?name=libpng12)
*   [libudev0](https://aur.archlinux.org/packages/libudev0/) or [libudev.so.0](https://aur.archlinux.org/packages/libudev.so.0/)

### Troubleshooting

#### In-game font is unreadable

Start Steam (or Dota 2) with the environment variable:

```
MESA_GL_VERSION_OVERRIDE=2.1

```

#### Everything seems OK but the game doesn't start

If you run the game from the terminal and, although no error is shown, try **disabling**: *Steam > Settings > In-Game > Enable Steam Community In-Game*. Apparently the game [The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales) has the same problem. It also describes a workaround that is untested in Dota 2.

#### Game runs on the wrong screen

	[GitHub Dota 2 issue #11](https://github.com/ValveSoftware/Dota-2/issues/11)

#### Game does not start with libxcb-dri3 error message

After a recent Mesa update, Dota 2 stopped working. The error message is:

```
SDL_GL_LoadLibrary(NULL) failed: Failed loading libGL.so.1: /usr/lib32/libxcb-dri3.so.0: undefined symbol: xcb_send_fd

```

Simply remove the bundled libxcb to force Steam to use the system-wide version. Restart Steam to apply.

```
$ find ~/.local/share/Steam -name 'libxcb*' -type f | grep -v installed | xargs rm

```

	[GitHub Steam issue #3204](https://github.com/ValveSoftware/steam-for-linux/issues/3204)

#### Steam overlay

Steam distributes a copy of libxcb which is incompatible with the latest xorg libxcb. If you're having issues with steam overlay and on recent xorg try removing the bundled lib.

```
 mv ~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libxcb.so.1 /tmp/libxcb.so.1.bak

```

See more information here:

	[[4]](https://github.com/ValveSoftware/steam-for-linux/issues/3199)

	[[5]](https://github.com/ValveSoftware/steam-for-linux/issues/3093)

#### Chinese Tips and player's name display problem

The Chinese characters in the Tips and player's name display block character.

The problem caused by some fonts package. It is known that the 'ttf-dejave', 'ttf-liberation' and 'ttf-ms-fonts' will cause the prolem, and the 'wqy-*', 'ttf-ubuntu-font-family', 'ttf-arphic-uming', 'ttf-linux-libertine' are safe. The other fonts family are not checked.

	[GitHub Steam issue #1688](https://github.com/ValveSoftware/Dota-2/issues/1688)

#### Chinese input method problem

Dota2 is not compatible with CJK IME(Input Method Editor/Enhancer), such as Ibus and Fcitx. Chinese characters can't be typed in Dota2.[GitHub Steam issue 493](https://github.com/ValveSoftware/Dota-2/issues/493)

The possible solution

Compile the `libSDL` with fcitx or ibus support, then replace `Game Folder/dota 2 beta/bin/libSDL2-2.0.so.0` with your version.

	[LibSDL+Ibus](http://forum.ubuntu.org.cn/viewtopic.php?f=34&t=460195)

	[LibSDL+Fcitx](http://forum.ubuntu.org.cn/viewtopic.php?f=34&t=466879&sid=1664abac47d8f639ed9b7f3abf94c675)

	[LibSDL+Fcitx Source](https://github.com/timxx/SDL-fcitx)

	[The solutions issues](https://github.com/ValveSoftware/Dota-2/issues/1650)

## Dwarfs F2P

### Dependencies

*   [lib32-libgdiplus](https://aur.archlinux.org/packages/lib32-libgdiplus/)

### Troubleshooting

#### Game does not start

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

#### Game crashes

In some cases, the game crashes about 2 minutes before the end of every arcade. This bug has been reported, but there's no known solution to it.

## Dynamite Jack

### Dependencies

*   [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl)

### Troubleshooting

#### Sound Issues

When running on 64-bit Arch Linux, there may be "pops and hisses" when running Dynamite Jack. This could be caused by not having `STEAM_RUNTIME=0` set. (However, even with `STEAM_RUNTIME=0` set, the game may still sometimes start with this issue. Exiting and restarting the game seems to make the problem go away.)

#### Game does not start

If running steam with the `STEAM_RUNTIME=0`, Dynamite Jack may have a problem starting. Check the steam error messages for this message:

```
/home/<USER>/.local/share/Steam/SteamApps/common/Dynamite Jack/bin/main: error while loading shared libraries: libSDL-1.2.so.0: cannot open shared object file: No such file or directory

```

Install [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl) from [multilib](/index.php/Multilib "Multilib") and Dynamite Jack should start up.

## Football Manager 2014

This game will not run when installed on an XFS or reiserfs filesystem. Workaround is to install on an ext4 filesystem.

## FORCED

This game has 32-bit and 64-bit binaries. For unknown reason, steam will launch the 32-bit binary even on 64-bit Arch Linux. When manually launching the 64-bit binary, the game starts, but cannot connect to Steam account, so you cannot play. So install 32-bits dependencies, and launch the game from Steam.

### Dependencies

*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)
*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)

## FTL: Faster than Light

### Dependencies

Libraries are downloaded and and placed in the game's data directory for both architectures. As long as you run FTL by the launcher script (or via the shortcut in Steam) you should not need to download any further libraries.

### Compatibility

After installation, FTL may fail to run due to a 'Text file busy' error (characterised in Steam by your portrait border going green then blue again). The easiest way to mend this is to just reboot your system. Upon logging back in FTL should run.

The Steam overlay in FTL does not function as it is not a 3D accelerated game. Because of this the desktop notifications will be visible. If playing in fullscreen, therefore, these notifications in some systems may steal focus and revert you back to windowed mode with no way of going back to fullscreen without relaunching. The binaries for FTL on Steam have no DRM and it is possible to run the game *without* Steam running, so in some cases that may be optimum - just ensure that you launch FTL via the launcher script in `~/.steam/root/SteamApps/common/FTL Faster than Light/data/` rather than the FTL binary in the $arch directory.

### Problems with open-source video driver

FTL may fail to run if you are using an opensource driver for your video card. There are two solutions: install a proprietary video driver or delete (rename if you are unsure) the library "libstdc++.so.6" inside `~/.steam/root/SteamApps/common/FTL\ Faster\ Than\ Light/data/amd64/lib`. This is if you are using a 64bit system. In case you are using a 32bit system you have to remove (rename) the same library located into `~/.steam/root/SteamApps/common/FTL\ Faster\ Than\ Light/data/x86/lib`.

## Game Dev Tycoon

### Troubleshooting

#### Game does not start

Error about missing libudev.so.0 might appear, solution:

```
 # ln -s /lib/libudev.so /lib/libudev.so.0

```

## Garry's Mod

### Troubleshooting

#### Game does not start

Error about missing client.so might appear, solution:

```
 cd SteamLibrary/SteamApps/common/GarrysMod/bin/
 ln -s libawesomium-1-7.so.0 libawesomium-1-7.so.2
 ln -s ../garrysmod/bin/client.so ./

```

#### Opening some menus causes the game to crash

Most menus work fine, but ones with checkboxes (LAN multiplayer, mounted games list) do not work at all. This is a bug in the menu code.

If you prefer the default menu style and do not mind a hacky solution: [Simon311](https://github.com/Facepunch/garrysmod-issues/issues/86#issuecomment-30935491) has written code with instructions to fix it.

If you do not care for the default menu style and want a more stable but feature-incomplete solution, Facepunch developer [robotboy655](https://github.com/robotboy655/gmod-lua-menu) has written a new menu.

### Game crashes after attempting to join server

While in the process of joining a server, downloading resources, etc, the game seems to hang and after a while, perhaps during the "sending client info" portion the game crashes, usually without any error messages. Error does not give much information, however, the process for Garry's mod is killed.

This issue arises more often when joining servers with many addons like DarkRP servers specifically.

The Problem seems to correlate with a weak GPU and the game is timing out from the server, so if the GPU is the problem, lowering the graphics settings to minimum fixes the problem until you can upgrade ;).

## Hack 'n' Slash

### Troubleshooting

#### The game starts but craches when loading a new or saved game

This seems to be the same issue as with Hammerwatch. Right click on Hack 'n' Slash on your game list, click on Properties, click on SET LAUNCH OPTIONS, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

## Hacker Evolution [Untold, Duality]

### Dependencies

*   [lib32-sdl2_mixer](https://aur.archlinux.org/packages/lib32-sdl2_mixer/)

## Half-Life 2 & episodes

### Cyrillic fonts problem

This problem can be solved by deleting "Helvetica" font.

## Hammerwatch

### Troubleshooting

#### The game not starting from Steam GUI

Right click on Hammerwatch on your game list, click on Properties, click on SET LAUNCH OPTIONS, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

#### No sound

Hammerwatch opens with a popup: "Sound Error" -- "Could not initialize OpenAL, no sounds will be played. Try updating your OpenAL drivers."

OpenAL, which Hammerwatch uses, defaults to PulseAudio. To change that, add the following line to `/etc/openal/alsoft.conf`:

```
drivers=alsa,pulse

```

This way, Hammerwatch will use ALSA. This solution was found [here](https://stackoverflow.com/questions/9547396/what-does-al-lib-pulseaudio-c612-context-did-not-connect-access-denied-me).

## Harvest: Massive Encounter

### Dependencies

*   [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=lib32-nvidia-cg-toolkit)
*   [lib32-libjpeg6](https://aur.archlinux.org/packages/lib32-libjpeg6/)
*   [lib32-sfml](https://aur.archlinux.org/packages/lib32-sfml/)

### Compatibility

Game refuses to launch and throws you to library installer loop. Just edit `~/.steam/root/SteamApps/common/Harvest Massive Encounter/run_harvest` and remove everything but

```
 #!/bin/bash
 exec ./Harvest

```

## Hatoful Boyfriend

### Japanese text invisible

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

## The inner world

### Bringing up the inventory or main menu

Hold the <tab> key.

### Dependencies

#### Sound support

Install [java-commons-codec](https://aur.archlinux.org/packages/java-commons-codec/) from the [AUR](/index.php/AUR "AUR") to get sound support.

#### Cutscenes

The game has cutscenes. It starts directly with a cutscene before you start the actual game in the backyard. To see these cutscenes you need to use Oracle's Java instead of the openjdk.

Install [jre](https://aur.archlinux.org/packages/jre/) from the [AUR](/index.php/AUR "AUR") and run

```
archlinux-java set java-8-jre/jre

```

as root. Furthermore you need the package ffmpeg-compat. Currently this package is in the community repository.

There seem to be problems with Steam Overlay. Try to run the game directly with ~/Steam/SteamApps/common/TheInnerWorld/TIW_start.sh

Note that cutscenes open in a new window. So pay attention to that and switch to the new window to enjoy the movies.

See the [Steam Forums](http://steamcommunity.com/app/251430/discussions/0/611701360817206606/#c611701360827509770) for details.

## Interloper

### Dependencies

*   [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib)

### Game does not launch

Game can sometimes segfault due to an incompatibility with the Steam Runtime's libasound.so.2\. Delete the bad library:

```
 rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libasound.so.2

```

## Invisible Apartment

### Dependencies

*   [qt5-multimedia](https://www.archlinux.org/packages/?name=qt5-multimedia)

### Game does not run

Game does not run if you try to launch it via Steam, but you can run it directly if you run the following in terminal

```
 /home/<username>/.steam/steam/SteamApps/common/Invisible\ Apartment/ia1

```

where for <username> you put your Linux username.

## Joe Danger 2: The Movie

### Dependencies

*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)
*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

### Compatibility

Game only worked after obtaining from the [Humble Bundle](https://www.humblebundle.com/‎) directly and [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) was installed.

## [Kerbal Space Program](/index.php/Kerbal_Space_Program "Kerbal Space Program")

### Troubleshooting

### Game never progresses past initial loading

To fix this, set:

```
LC_ALL=C

```

### No text display

The game requires Arial and Arial Black fonts, provided by the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) package.

Another alternative is to try to install the [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) package. This worked using KSP 0.90.0 on x86_64 Arch Linux.

### Graphics flickering when using primusrun

Run with PRIMUS_SYNC=2 (but you will get reduced frame rate this way)

### Game crashes when accessing settings or saves on 64 bit systems on Steam

In the properties for Kerbal Space program, set a launch option of:

```
LC_ALL=C %command%_64

```

### Locale settings

See [https://bugs.kerbalspaceprogram.com/issues/504](https://bugs.kerbalspaceprogram.com/issues/504) if you have troubles with building Ships.

### No audio on 64-bit systems

Run the 64-bit executable.

Steam launches the KSP.x86 executable vs. the KSP.x86_64 executable. Navigate to:

```
/home/$USER/.local/share/Steam/SteamApps/common/Kerbal\ Space\ Program/ 

```

Launch with:

```
./KSP.x86_64

```

Or you can simply right click on "Kerbal Space Program" in your game list, click *Properties*, click *SET LAUNCH OPTIONS*, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" LC_ALL=C %command%_64

```

### Black ingame textures

Disable "Edge Highlighting (PPFX)" in graphics settings ingame.

### See also

*   [Kerbal Space Program](/index.php/Kerbal_Space_Program "Kerbal Space Program")
*   [http://forum.kerbalspaceprogram.com/showthread.php/24529-The-Linux-compatibility-thread](http://forum.kerbalspaceprogram.com/showthread.php/24529-The-Linux-compatibility-thread)!

## Killing Floor

### Troubleshooting

#### Screen resolution

Killing Floor runs pretty much from scratch, although you might have to change in-game resolution screen as the default one is **800x600** and a **4:3** screen format. If you try to modify screen resolution in-game, it might crash your desktop enviroment. To fix this, please set the desired resolution screen size by modifing your `~/.killingfloor/System/KillingFloor.ini` with your prefered editor.

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

#### Windowed mode

Uncheck fullscreen in the options menu, and use `Ctrl+g` to stop mouse capturing (that was non-obvious to discover..). This way you can easily minimize it and do other other things..and let your WM handle things.

#### Stuttering Sound

KillingFloor comes with its own libopenal.so (called openal.so). To use system lib instead install [openal](https://www.archlinux.org/packages/?name=openal) or [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal) (if using 64bit system). Then go to `$HOME/Steam/SteamApps/common/KillingFloor/System`. and rename openal.so to openal.so.bak Then create symlink to /usr/lib32/libopenal.so.1 or /usr/lib/libopenal.so.1 called openal.so

## Lethal League

### Dependencies

*   [lib32-glew1.10](https://aur.archlinux.org/packages/lib32-glew1.10/)

## Metro: Last Light

This game is not allowing to change its resolution on a multimonitor setup on GNOME with Catalyst drivers.

### Attempted fixes

Various changes to the games config file was tried without success. `wmctrl` was not able to force the games resolution.

### Hacky solution

Disabled the side monitors.

### Possible solutions

Jason over at [unencumbered by fact](http://unencumberedbyfacts.com/2013/11/20/multiple-monitor-gaming-on-linux/) is using Nvidia drivers on his multimonitor setup. However he notes he is using a single display server setup. This is being explored.

## Mark of the Ninja

### Troubleshooting

#### Bad sound

Right click on `Mark of the Ninja` on your game list, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

## Middle-earth: Shadow of Mordor

### Floating heads

Right click on `Middle-earth: Shadow of Mordor` on your game list, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
__GL_ShaderPortabilityWarnings=0 %command%

```

## Multiwinia

### Dependencies

*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)

### Crash on startup

If Multiwinia crashes on startup on X64 systems, force launching the 32-bit executable by replacing `~/.local/share/Steam/steamapps/common/Multiwinia/run_steam.sh` with the following script:

```
#!/bin/sh
./multiwinia.bin.x86	

```

See [[6]](https://steamcommunity.com/app/1530/discussions/0/864969481950542663/#c558746995160431396).

## Natural Selection 2

Game mostly works out of the box.

### No Sound

If there is no sound in-game. Try installing [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl), [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2), and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

If this fails, try setting the game's launch options in Steam to:

```
LD_LIBRARY_PATH="/usr/lib32:$LD_LIBRARY_PATH" %command%

```

## Penumbra: Overture

### Dependencies

(Taken from [penumbra-collection](https://aur.archlinux.org/packages/penumbra-collection/) and [penumbra-overture-ep1-demo](https://aur.archlinux.org/packages/penumbra-overture-ep1-demo/))

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-sdl_ttf](https://www.archlinux.org/packages/?name=lib32-sdl_ttf)
*   [lib32-sdl_image](https://www.archlinux.org/packages/?name=lib32-sdl_image)

### Troubleshooting

#### Windowed mode

There is no in-game option to change to the windowed mode, you will have to edit `~/.frictionalgames/Penumbra/Overture/settings.cfg` to activate it. Find `FullScreen="true"` and change it to `FullScreen="false"`, after this the game should start in windowed mode.

## Portal 2

### Troubleshooting

#### Game does not start

Several OpenGL-related errors (such as `PROBLEM: You appear to have OpenGL 1.4.0, but we need at least 2.0.0!` or `libGL error: driver pointer missing`) are caused by Portal 2 bundling an old libstdc++ file. This error is especially common with open source Radeon drivers (`radeonsi`).

To remedy this, make Portal 2 use the system-wide file by setting the launch options to `LD_PRELOAD='/usr/$LIB/libstdc++.so.6' %command%`.

More details and background info available [here.](https://wirejungle.wordpress.com/2015/01/09/how-to-fix-broken-steam-linux-client-with-radeon-graphics-driver-workaround/)

## Prison Architect

### Troubleshooting

#### ALSA error when using PulseAudio

The error: `ALSA lib pcm_dmix.c:1018:(snd_pcm_dmix_open) unable to open slave` was resolved by installing:

*   [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)
*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)

per [PulseAudio#ALSA](/index.php/PulseAudio#ALSA "PulseAudio")

## Project Zomboid

### Dependencies

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk)

### No sound

Right click on `Project Zomboid` on your game list, click on `Properties`, click on `SET LAUNCH OPTIONS`, then add this:

```
LD_LIBRARY_PATH="/usr/lib:$LD_LIBRARY_PATH" %command%

```

In the game, go to the options and set all audio to the proper volume.

## Redshirt

### Dependencies (x86_64)

*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) (if you use PulseAudio)

## Revenge of the Titans

### Dependencies

*   [libxtst](https://www.archlinux.org/packages/?name=libxtst) and [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst)

## Rock Boshers DX: Directors Cut

### Dependencies

*   [lib32-libcaca](https://www.archlinux.org/packages/?name=lib32-libcaca)

## Serious Sam 3: BFE

### Dependencies

*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

### Troubleshooting

#### No audio

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

## Sir, you are being hunted

### Dependencies

*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

## Spacechem

### Dependencies

*   [lib32-sqlite](https://www.archlinux.org/packages/?name=lib32-sqlite)
*   [lib32-sdl_image](https://www.archlinux.org/packages/?name=lib32-sdl_image)
*   [lib32-sdl_mixer](https://aur.archlinux.org/packages/lib32-sdl_mixer/)

### Troubleshooting

#### Game crash

The shipped x86 version of Spacechem does not work on x64 with the game's own libSDL* files, and crashes with some strange output.

To solve this just remove or move the three files `libSDL-1.2.so.0`, `libSDL_image-1.2.so.0`, `libSDL_mixer-1.2.so.0` from `~/.steam/root/SteamApps/common/SpaceChem`

## Space Pirates and Zombies

### Dependencies

*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)

### Troubleshooting

#### No audio

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

## Splice

Splice comes with both x86 and x64 binaries. Steam does not have to be running to launch this game.

### Dependencies

*   [glu](https://www.archlinux.org/packages/?name=glu)

## Steel Storm: Burning Retribution

### Troubleshooting

#### Start with black screen

The game tries to launch in 1024x768 resolution with fullscreen mode by default. It is impossible on some devices. (for example laptop Samsung Series9 with intel hd4000 video).

You can launch the game in windowed mode. To do this open game Properties in Steam, in General tab select "Set launch options..." and type "-window".

Now you can change the resolution in game.

#### No English fonts

If you use Intel video card, just disable S3TC in DriConf.

## Stephen's Sausage Roll

### Troubleshooting

#### No sound

If [libpulse](https://www.archlinux.org/packages/?name=libpulse) is installed, Unity may try to use that library for sound and fail. To test if this is the problem, try removing [libpulse](https://www.archlinux.org/packages/?name=libpulse) or renaming the package files that are named `libpulse-simple*`. To see which [libpulse](https://www.archlinux.org/packages/?name=libpulse) files are relevant, run:

 `$ pacman -Ql libpulse | awk '{print $2}' | grep /usr/lib/libpulse-simple` 
```
/usr/lib/libpulse-simple.so
/usr/lib/libpulse-simple.so.0
/usr/lib/libpulse-simple.so.0.1.0
```

If renaming any of those files works for you, you can proceed with the following instructions (don't forget to revert any renaming you just did!). Browse to the game's directory:

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

**Note:** I only had to create a 0-byte `libpulse-simple.so.0` file for the following trick to work.

After you have created these 0-byte files, you can now attempt to run the game binary directly, telling the dynamic linker to use our 0-byte files:

```
$ LD_LIBRARY_PATH="noload/:$LD_LIBRARY_PATH" ./Sausage.x86_64

```

Hopefully you now have sound!

If everything works up to this point, you can amend the launch options in Steam to be:

```
LD_LIBRARY_PATH="noload/:$LD_LIBRARY_PATH" %command%

```

Again, this should work because Steam checks for a `noload/` directory relative to the game's directory. The dynamic linker should respect the `$LD_LIBRARY_PATH` variable and fail to load the necessary [libpulse](https://www.archlinux.org/packages/?name=libpulse) files. The game should then fallback to plain ALSA.

## Strike Suite Zero

### Dependencies

*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

## Superbrothers: Sword & Sworcery EP

### Dependencies

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) (if you use PulseAudio)

## Team Fortress 2

### Dependencies

*   [lib32-libpng12](https://aur.archlinux.org/packages/lib32-libpng12/)

### Making HRTF work

Assuming HRTF has been set up properly in the operating system, hrtf won't be enabled unless you disable the original processing. To do so, use

```
   dsp_slow_cpu 1

```

For best results, also change the following:

```
   snd_spatialize_roundrobin 1
   dsp_enhance_stereo 0
   snd_pitchquality 1

```

### Troubleshooting

#### Loading screen freeze

If you are a non-english (speaking) user, you have to enable "en_US.UTF-8" in the locale.gen! Generate a new locale after that.

#### No audio

It happens if there is no PulseAudio in your system. If you want to use [ALSA](/index.php/ALSA "ALSA"), you need to launch Steam or the game directly with `SDL_AUDIODRIVER=alsa` (From [SteamCommunity](http://steamcommunity.com/app/221410/discussions/0/882966056462819091/#c882966056470753683)).

If it still does not work, you may also need to set the environment variable AUDIODEV. For instance `AUDIODEV=Live`. Use `aplay -l` to list the available sound cards.

#### Slow loading textures

If you are using Chris' FPS Configs or any other FPS config, you may have set `mat_picmip` to `2`. This spawns multiple threads for texture loading, which may cause more jittering and lag on Linux, especially on alternative kernels. Try setting it to `-1`, the default.

#### NVIDIA drivers

**Note:** This is fixed in [nvidia](https://www.archlinux.org/packages/?name=nvidia) 361.42-1

Some modern [NVIDIA](/index.php/NVIDIA "NVIDIA") drivers do not seem to go well with Team Fortress 2\. If you have some startup error complaining that a GL function is not available, you can fix this by putting your driver in compatibility mode. To do this, you need to change the launch options to:

```
   __GLVND_DISALLOW_PATCHING=1 %command%

```

## Terraria

See the KNOWN ISSUES & WORKAROUNDS​ section of the [release announcement](http://forums.terraria.org/index.php?threads/terraria-1-3-0-8-can-mac-linux-come-out-play.30287/).

## The Book of Unwritten Tales

If the game does not start, uncheck: *Properties > Enable Steam Community In-Game*.

The game may segfault upon clicking the Setting menu and possibly during or before gameplay. This is a known problem and you will unfortunately have to wait for a fix from the developer. A workaround (taken from the [Steam forums](http://steamcommunity.com/app/221410/discussions/3/846939071081758230/#p2)) is to replace the game's RenderSystem_GL.so with one from Debian's repositories. To do that download this [deb file](https://launchpad.net/ubuntu/+archive/primary/+files/libogre-1.7.4_1.7.4-3_i386.deb), extract it (with `[dpkg](https://aur.archlinux.org/packages/dpkg/) -x libogre-*.deb outdir`) and replace `~/.local/share/Steam/SteamApps/common/The Book of Unwritten Tales/lib/32/RenderSystem_GL.so` with the one that comes with the `.deb` package.

### Dependencies

*   [lib32-libxaw](https://aur.archlinux.org/packages/lib32-libxaw/)
*   [lib32-jasper](https://aur.archlinux.org/packages/lib32-jasper/)

## The Book of Unwritten Tales: The Critter Chronicles

Because it's based on the same engine, the things that apply to *The Book of Unwritten Tales* also apply for this game.

To prevent the game from crashing at the very end when the credits are shown, change the size of the credits image as described here: [http://steamcommunity.com/app/221830/discussions/0/828925849276110960/#c810921273836530791](http://steamcommunity.com/app/221830/discussions/0/828925849276110960/#c810921273836530791)

## The Clockwork Man

### Dependencies

*   [lib32-libidn](https://www.archlinux.org/packages/?name=lib32-libidn)

## The Polynomial

### Dependencies

*   [ilmbase102-libs](https://aur.archlinux.org/packages/ilmbase102-libs/)
*   [openexr170-libs](https://aur.archlinux.org/packages/openexr170-libs/)

[Steam for Linux issue #2721](https://github.com/ValveSoftware/steam-for-linux/issues/2721)

### Troubleshooting

#### Segfaults during program start on 64-bit systems

The game segfaults during program start because of the `LD_LIBRARY_PATH` setting in the launcher script. Edit `~/.local/share/Steam/SteamApps/common/ThePolynomial/Polynomial64`, and comment out the `LD_LIBRARY_PATH` variable. Make sure to put the `./bin/Polynomial64 "$@"` command on a new line.

## The Stanley Parable

### Troubleshooting

#### Game won't start

as discussed in steam's store page, remove `libstdc++.so.6` from the game folder. For example::

```
rm ~/.local/share/Steam/steamapps/common/The\ Stanley\ Parable/bin/libstdc++.so.6

```

## This War of Mine

### Troubleshooting

#### Game doesn't load

This happens because of a incompatibility of the newer version of `lib32-glibc`. To Fix the problem you need to download the version 2.20-6 of the lib, you can download it [here](http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/multilib-testing/os/x86_64/lib32-glibc-2.20-6-x86_64.pkg.tar.xz), then extract the:

```
   libc.so.6
   libc-2.20.so
   libpthread.so.0
   libpthread-2.20.so
   libresolv-2.20.so
   libresolv.so.2 
   librt.so.1
   librt-2.20.so

```

located in the archive and put on the main game folder: `~/.local/share/Steam/steamapps/common/This War of Mine/`

## Tomb Raider

### Troubleshooting

#### Game immediately closes when running with steam-native

Tomb Raider has a very heavy amount of dependency on the Steam runtime, the easiest solution is to just run it using the runtime. You can do so by setting the following as the launch option:

 `/home/[your username]/.local/share/Steam/ubuntu12_32/steam-runtime/run.sh %command%` 

#### Steam Controller not working ingame while being correctly recognised* by Steam outside of the game

If your Steam Controller is correctly recognised and paired but it still does not work in game then you can do the following:

*   In Steam, non Big Screen, go to Settings -> Account -> Beta participation -> Change... and in the dropdown select box select Steam Beta Update

*   Restart Steam

*   Go to Big Screen and start Tomb Raider

∗Correctly recognised means you can control desktop mouse and Steam in Big Picture mode and the controller is shown in Big Picture settings

## Towns / Towns Demo

### Crash on launch

Ensure you have [Java](/index.php/Java "Java") installed.

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

Otherwise, run the game via shell and set up proper audio device for FMOD, as discussed there [[7]](https://steamcommunity.com/app/237930/discussions/2/620695877176333955/).

Also, check out this thread [[8]](https://steamcommunity.com/app/237930/discussions/2/492378265893557247/)

## Transmissions: Element 120

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

### Dependencies

*   [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)

## Trine 2

### Dependencies

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxxf86vm](https://www.archlinux.org/packages/?name=lib32-libxxf86vm)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo)
*   [lib32-libdrm](https://www.archlinux.org/packages/?name=lib32-libdrm)

### Troubleshooting

*   If colors are wrong with FOSS drivers (r600g at least), try to run the game in windowed mode, rendering will be corrected. ([bugreport](https://bugs.freedesktop.org/show_bug.cgi?id=60553))
*   If sound plays choppy, try:

 `/etc/openal/alsoft.conf` 
```
drivers=pulse,alsa
frequency=48000

```

*   If the game resolution is wrong when using a dual monitor setup and you can't see the whole window edit `~/.frozenbyte/Trine2/options.txt` and change the options `ForceFullscreenWidth` and `ForceFullscreenHeight` to the resolution of your monitor on which you want to play the game.

## Unity3D

Games based on the Unity3D engine, like *War For The Overworld* or *Pixel Piracy* may need the package [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) to understand that they run on Linux and work properly.

### Locale Settings

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

Some of the affected games: *Cities: Skylines*, *Tablestop Simulator*, *Assault Android Cactus*, *Wasteland 2*.

Be aware that some games do not support setting that parameter, it will simply be ignored. This is the case for *Pillars of Eternity*, *Kentucky Route Zero*, *Sunless Sea*.

## Unity of Command

### Dependencies

*   [lib32-pango](https://www.archlinux.org/packages/?name=lib32-pango)
*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

### Troubleshooting

*   If squares are shown instead of text, try removing `$HOME/Steam/SteamApps/common/Unity of Command/bin/libpangoft2-1.0.so.0`.

#### No audio

If you get this error:

```
ALSA lib dlmisc.c:254:(snd1_dlobj_cache_get) Cannot open shared library /usr/lib/i386-linux-gnu/alsa-lib/libasound_module_pcm_pulse.so

```

Try running:

```
# mkdir -p /usr/lib/i386-linux-gnu/alsa-lib/
# ln -s /usr/lib32/alsa-lib/libasound_module_pcm_pulse.so /usr/lib/i386-linux-gnu/alsa-lib/

```

## Unrest

### Dependencies

*   [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth)

## War Thunder

### Troubleshooting

If having a green or blank screen at game start, set the `MESA_GL_VERSION_OVERRIDE=4.1COMPAT` [environment variable](/index.php/Environment_variable "Environment variable"). [[9]](https://forum.warthunder.com/index.php?/topic/267809-linux-potential-workaround-for-mesa-drivers-black-screen/) [[10]](http://forum.warthunder.com/index.php?search_term=0030709&app=core&module=search&do=search&fromMainBar=1&search_app=forums%3Aforum%3A920&sort_field=&sort_order=&search_in=posts)

## Witcher 2: Assassin of Kings

### Dependencies

*   [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2)
*   [lib32-libcurl-compat](https://aur.archlinux.org/packages/lib32-libcurl-compat/)
*   [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls)

*   [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2)
*   [lib32-sdl2_image](https://aur.archlinux.org/packages/lib32-sdl2_image/)
*   [lib32-libcurl-gnutls](https://aur.archlinux.org/packages/lib32-libcurl-gnutls/)

### Troubleshooting

If the game does not run, enable error messages:

```
cd "${HOME}/.local/share/Steam/SteamApps/common/the witcher 2"
LIBGL_DEBUG=verbose ./witcher2

```

## Wizardry 6: Bane of the Cosmic Forge

### Dependencies

*   [dosbox](https://www.archlinux.org/packages/?name=dosbox)

To fix the crash at start, edit `~/.local/share/Steam/SteamApps/common/Wizardry6/dosbox_linux/launch_wizardry6.sh` and change

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./libs
exec ./dosbox -conf dosbox_wiz6.conf -conf dosbox_wiz6_launch_linux.conf -noconsole "$@"

```

to

```
#export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./libs
exec dosbox -conf dosbox_wiz6.conf -conf dosbox_wiz6_launch_linux.conf -noconsole "$@"

```

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

## Worms Reloaded

### Dependencies

*   [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

## XCOM

### Dependencies

*   [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image)

### Hangs on startup

Steam ships its own versions of some libraries, and they sometimes are too old to work with archlinux system libraries. Removing the library supplied by Steam means Steam has to use the newer arch-specific version. [[11]](https://bbs.archlinux.org/viewtopic.php?pid=1428375#p1428375).

```
rm ~.local/share/Steam/ubuntu12_32/steam-runtime/amd64/lib/x86_64-linux-gnu/libgcc_s.so.1
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libstdc++.so.6
```

If you are running a hybrid graphic system, try

```
__GL_THREADED_OPTIMIZATIONS=0 primusrun %command%

```

### Graphical glitches on Intel HD

XCOM may not recognize sdl2 shared libraries shipped with Steam runtime. Check if binary finds all required files and install missing packages if necessary ([sdl2](https://www.archlinux.org/packages/?name=sdl2) and [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image)).

 `ldd ~/.local/share/Steam/steamapps/common/XCom-Enemy-Unknown/binaries/linux/game.x86_64 ` 

## Saints Row IV

### Game fails to launch after update to new Nvidia drivers

Set the launch options for Saints Row IV to:

 `LD_PRELOAD=$LD_PRELOAD:/usr/lib32/libGLX_nvidia.so %command%`