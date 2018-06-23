## Contents

*   [1 Introduction](#Introduction)
*   [2 Contributing](#Contributing)
*   [3 Common steps](#Common_steps)
    *   [3.1 OpenSSL 1.0 setup](#OpenSSL_1.0_setup)
    *   [3.2 Adobe Air setup](#Adobe_Air_setup)
    *   [3.3 Steam Link](#Steam_Link)
*   [4 Games](#Games)
    *   [4.1 Alien Isolation](#Alien_Isolation)
        *   [4.1.1 Missing libpcre.so.3](#Missing_libpcre.so.3)
    *   [4.2 Amnesia: The Dark Descent](#Amnesia:_The_Dark_Descent)
    *   [4.3 And Yet It Moves](#And_Yet_It_Moves)
        *   [4.3.1 Game does not start](#Game_does_not_start)
    *   [4.4 Anodyne](#Anodyne)
        *   [4.4.1 Play with a controller: joy2key configuration](#Play_with_a_controller:_joy2key_configuration)
    *   [4.5 Aquaria](#Aquaria)
        *   [4.5.1 Mouse pointer gets stuck in one direction](#Mouse_pointer_gets_stuck_in_one_direction)
    *   [4.6 ARK: Survival Evolved](#ARK:_Survival_Evolved)
        *   [4.6.1 Game does not start, displays text window with unreadable text](#Game_does_not_start.2C_displays_text_window_with_unreadable_text)
        *   [4.6.2 Gray water](#Gray_water)
        *   [4.6.3 Segmentation fault on startup](#Segmentation_fault_on_startup)
    *   [4.7 Audiosurf 2](#Audiosurf_2)
        *   [4.7.1 error. unable to load song <filename> ,came back with zero duration](#error._unable_to_load_song_.3Cfilename.3E_.2Ccame_back_with_zero_duration)
    *   [4.8 BADLAND: Game of the Year Edition](#BADLAND:_Game_of_the_Year_Edition)
    *   [4.9 Beat Cop](#Beat_Cop)
        *   [4.9.1 "BeatCop.x86_64" is not responding](#.22BeatCop.x86_64.22_is_not_responding)
    *   [4.10 Binding of Isaac: Rebirth](#Binding_of_Isaac:_Rebirth)
        *   [4.10.1 No sound](#No_sound)
    *   [4.11 BioShock Infinite](#BioShock_Infinite)
        *   [4.11.1 Game launching on wrong monitor in fullscreen mode](#Game_launching_on_wrong_monitor_in_fullscreen_mode)
    *   [4.12 BLACKHOLE](#BLACKHOLE)
    *   [4.13 Black Mesa](#Black_Mesa)
    *   [4.14 Block'hood](#Block.27hood)
        *   [4.14.1 White screen on startup](#White_screen_on_startup)
    *   [4.15 The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales)
    *   [4.16 BRAIN/OUT](#BRAIN.2FOUT)
    *   [4.17 The Book of Unwritten Tales: The Critter Chronicles](#The_Book_of_Unwritten_Tales:_The_Critter_Chronicles)
    *   [4.18 Borderlands 2](#Borderlands_2)
        *   [4.18.1 Migrating saves from other platforms](#Migrating_saves_from_other_platforms)
        *   [4.18.2 Using Ctrl Key](#Using_Ctrl_Key)
        *   [4.18.3 Logging into SHiFT](#Logging_into_SHiFT)
        *   [4.18.4 Game crashes nearly instantly](#Game_crashes_nearly_instantly)
    *   [4.19 Borderlands: The Pre-Sequel](#Borderlands:_The_Pre-Sequel)
        *   [4.19.1 Keyboard not working](#Keyboard_not_working)
        *   [4.19.2 Not starting via Steam](#Not_starting_via_Steam)
    *   [4.20 Cities in Motion 2](#Cities_in_Motion_2)
        *   [4.20.1 Dialog boxes fail to display properly](#Dialog_boxes_fail_to_display_properly)
    *   [4.21 Cities Skylines](#Cities_Skylines)
        *   [4.21.1 Textures not rendering properly](#Textures_not_rendering_properly)
    *   [4.22 Civilization V](#Civilization_V)
        *   [4.22.1 Stuttering sound with PulseAudio](#Stuttering_sound_with_PulseAudio)
        *   [4.22.2 Game crashes seconds after loading a map](#Game_crashes_seconds_after_loading_a_map)
        *   [4.22.3 Game crashes after intro video with "Unable to load texture (LoadingBaseGame.dds)"](#Game_crashes_after_intro_video_with_.22Unable_to_load_texture_.28LoadingBaseGame.dds.29.22)
    *   [4.23 Civilization: Beyond earth](#Civilization:_Beyond_earth)
        *   [4.23.1 Segfault after a few minutes](#Segfault_after_a_few_minutes)
    *   [4.24 Civilization VI](#Civilization_VI)
        *   [4.24.1 If Segfault Immediately on Start](#If_Segfault_Immediately_on_Start)
    *   [4.25 Deus Ex: Mankind divided](#Deus_Ex:_Mankind_divided)
    *   [4.26 The Clockwork Man](#The_Clockwork_Man)
    *   [4.27 Company of Heroes 2](#Company_of_Heroes_2)
        *   [4.27.1 Missing libpcre.so.3](#Missing_libpcre.so.3_2)
    *   [4.28 Cossacks 3](#Cossacks_3)
        *   [4.28.1 No sound](#No_sound_2)
        *   [4.28.2 Flashing screen with primus](#Flashing_screen_with_primus)
    *   [4.29 Counter-Strike: Global Offensive (CS:GO)](#Counter-Strike:_Global_Offensive_.28CS:GO.29)
        *   [4.29.1 Game starts on the wrong screen](#Game_starts_on_the_wrong_screen)
        *   [4.29.2 Cannot reach bottom of the screen on menus](#Cannot_reach_bottom_of_the_screen_on_menus)
        *   [4.29.3 Sound is played slightly delayed](#Sound_is_played_slightly_delayed)
        *   [4.29.4 Mouse not working in-game](#Mouse_not_working_in-game)
        *   [4.29.5 Brightness slider not working](#Brightness_slider_not_working)
        *   [4.29.6 Microphone not working](#Microphone_not_working)
        *   [4.29.7 Mouse is unrensponsive or moves slowly](#Mouse_is_unrensponsive_or_moves_slowly)
    *   [4.30 Creeper World 3: Arc Eternal](#Creeper_World_3:_Arc_Eternal)
        *   [4.30.1 Game does not start](#Game_does_not_start_2)
    *   [4.31 Crusader Kings II](#Crusader_Kings_II)
        *   [4.31.1 No audio](#No_audio)
        *   [4.31.2 Oddly sized starting window](#Oddly_sized_starting_window)
        *   [4.31.3 DLCs not detected](#DLCs_not_detected)
    *   [4.32 Crypt of the NecroDancer](#Crypt_of_the_NecroDancer)
        *   [4.32.1 Crashes after splash screen](#Crashes_after_splash_screen)
    *   [4.33 The Curious Expedition](#The_Curious_Expedition)
        *   [4.33.1 Game stuck on loading screen](#Game_stuck_on_loading_screen)
    *   [4.34 Death Road To Canada](#Death_Road_To_Canada)
        *   [4.34.1 No music](#No_music)
    *   [4.35 Defender's Quest: Valley of the Forgotten](#Defender.27s_Quest:_Valley_of_the_Forgotten)
    *   [4.36 Dirt](#Dirt)
    *   [4.37 Dirt Rally](#Dirt_Rally)
    *   [4.38 Divinity: Original Sin - Enhanced Edition](#Divinity:_Original_Sin_-_Enhanced_Edition)
        *   [4.38.1 Game does not start when using Bumblebee optirun or primusrun](#Game_does_not_start_when_using_Bumblebee_optirun_or_primusrun)
        *   [4.38.2 Game does not work with amdgpu](#Game_does_not_work_with_amdgpu)
    *   [4.39 Don't Starve](#Don.27t_Starve)
        *   [4.39.1 No sound](#No_sound_3)
    *   [4.40 Dota 2](#Dota_2)
        *   [4.40.1 In-game font is unreadable](#In-game_font_is_unreadable)
        *   [4.40.2 Error with libpangoft2](#Error_with_libpangoft2)
        *   [4.40.3 The game does not start](#The_game_does_not_start)
        *   [4.40.4 Game runs on the wrong screen](#Game_runs_on_the_wrong_screen)
        *   [4.40.5 Game does not start with libxcb-dri3 error message](#Game_does_not_start_with_libxcb-dri3_error_message)
        *   [4.40.6 Steam overlay](#Steam_overlay)
        *   [4.40.7 Chinese tips and player names not shown](#Chinese_tips_and_player_names_not_shown)
        *   [4.40.8 Chinese input method problem](#Chinese_input_method_problem)
    *   [4.41 Devil Daggers](#Devil_Daggers)
    *   [4.42 Drox Operative](#Drox_Operative)
    *   [4.43 Dwarfs F2P](#Dwarfs_F2P)
        *   [4.43.1 Game does not start](#Game_does_not_start_3)
        *   [4.43.2 Game crashes](#Game_crashes)
    *   [4.44 Dynamite Jack](#Dynamite_Jack)
        *   [4.44.1 Sound Issues](#Sound_Issues)
        *   [4.44.2 Game does not start](#Game_does_not_start_4)
    *   [4.45 Empire Total War](#Empire_Total_War)
        *   [4.45.1 Weird unreadable fonts](#Weird_unreadable_fonts)
    *   [4.46 Euro Truck Simulator 2](#Euro_Truck_Simulator_2)
        *   [4.46.1 Shows only a black screen](#Shows_only_a_black_screen)
    *   [4.47 Football Manager 2014](#Football_Manager_2014)
    *   [4.48 FORCED](#FORCED)
    *   [4.49 For the King](#For_the_King)
    *   [4.50 FTL: Faster than Light](#FTL:_Faster_than_Light)
        *   [4.50.1 Compatibility](#Compatibility)
        *   [4.50.2 Problems with open-source video driver](#Problems_with_open-source_video_driver)
    *   [4.51 Game Dev Tycoon](#Game_Dev_Tycoon)
        *   [4.51.1 Game does not start](#Game_does_not_start_5)
    *   [4.52 Garry's Mod](#Garry.27s_Mod)
        *   [4.52.1 Game does not start](#Game_does_not_start_6)
        *   [4.52.2 Opening some menus causes the game to crash](#Opening_some_menus_causes_the_game_to_crash)
        *   [4.52.3 Game crashes after attempting to join server](#Game_crashes_after_attempting_to_join_server)
    *   [4.53 Gods will be watching](#Gods_will_be_watching)
    *   [4.54 GRID Autosport](#GRID_Autosport)
        *   [4.54.1 Black screen when trying to play](#Black_screen_when_trying_to_play)
    *   [4.55 Hack 'n' Slash](#Hack_.27n.27_Slash)
        *   [4.55.1 Crashes when trying to load a game](#Crashes_when_trying_to_load_a_game)
    *   [4.56 Hacker Evolution](#Hacker_Evolution)
    *   [4.57 Half-Life 2 and episodes](#Half-Life_2_and_episodes)
        *   [4.57.1 Cyrillic fonts problem](#Cyrillic_fonts_problem)
    *   [4.58 Hammerwatch](#Hammerwatch)
        *   [4.58.1 The game does not start via Steam](#The_game_does_not_start_via_Steam)
        *   [4.58.2 No sound](#No_sound_4)
    *   [4.59 Harvest: Massive Encounter](#Harvest:_Massive_Encounter)
        *   [4.59.1 Compatibility](#Compatibility_2)
    *   [4.60 Hatoful Boyfriend](#Hatoful_Boyfriend)
        *   [4.60.1 Japanese text invisible](#Japanese_text_invisible)
    *   [4.61 HuniePop](#HuniePop)
        *   [4.61.1 Game crashes upon launch](#Game_crashes_upon_launch)
    *   [4.62 Hyper Light Drifter](#Hyper_Light_Drifter)
        *   [4.62.1 The controller does not work](#The_controller_does_not_work)
        *   [4.62.2 Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found)
    *   [4.63 The Impossible Game](#The_Impossible_Game)
    *   [4.64 The Inner World](#The_Inner_World)
        *   [4.64.1 Bringing up the inventory or main menu](#Bringing_up_the_inventory_or_main_menu)
            *   [4.64.1.1 Cutscenes](#Cutscenes)
    *   [4.65 Interloper](#Interloper)
        *   [4.65.1 Game does not start](#Game_does_not_start_7)
    *   [4.66 Invisible Apartment](#Invisible_Apartment)
        *   [4.66.1 Game does not start](#Game_does_not_start_8)
    *   [4.67 Joe Danger 2: The Movie](#Joe_Danger_2:_The_Movie)
        *   [4.67.1 Compatibility](#Compatibility_3)
    *   [4.68 Kerbal Space Program](#Kerbal_Space_Program)
    *   [4.69 Killing Floor](#Killing_Floor)
        *   [4.69.1 Cannot change screen resolution](#Cannot_change_screen_resolution)
        *   [4.69.2 Windowed mode](#Windowed_mode)
        *   [4.69.3 Stuttering sound](#Stuttering_sound)
    *   [4.70 Left for Dead 2](#Left_for_Dead_2)
        *   [4.70.1 Missing Chinese font](#Missing_Chinese_font)
    *   [4.71 Lethal League](#Lethal_League)
    *   [4.72 Life is Strange](#Life_is_Strange)
    *   [4.73 Little Racers STREET](#Little_Racers_STREET)
    *   [4.74 The Long Dark](#The_Long_Dark)
        *   [4.74.1 Game does not start](#Game_does_not_start_9)
        *   [4.74.2 Game starts, but some overlay text is missing and cutscenes shows black screen](#Game_starts.2C_but_some_overlay_text_is_missing_and_cutscenes_shows_black_screen)
        *   [4.74.3 Cutscenes are still black](#Cutscenes_are_still_black)
        *   [4.74.4 Cursor disappears](#Cursor_disappears)
    *   [4.75 Magicka 2](#Magicka_2)
        *   [4.75.1 Indefinitely stuck at start](#Indefinitely_stuck_at_start)
    *   [4.76 Mark of the Ninja](#Mark_of_the_Ninja)
        *   [4.76.1 Bad sound](#Bad_sound)
    *   [4.77 Metro: Last Light](#Metro:_Last_Light)
    *   [4.78 Metro: 2033 Redux](#Metro:_2033_Redux)
        *   [4.78.1 No sound](#No_sound_5)
    *   [4.79 No image](#No_image)
    *   [4.80 Middle-earth: Shadow of Mordor](#Middle-earth:_Shadow_of_Mordor)
        *   [4.80.1 Floating heads](#Floating_heads)
    *   [4.81 Mount & Blade: Warband](#Mount_.26_Blade:_Warband)
        *   [4.81.1 Segmentation fault (core dumped) with wayland](#Segmentation_fault_.28core_dumped.29_with_wayland)
        *   [4.81.2 DLC Chooser](#DLC_Chooser)
        *   [4.81.3 Crash on startup](#Crash_on_startup)
    *   [4.82 Multiwinia](#Multiwinia)
        *   [4.82.1 Crash on startup](#Crash_on_startup_2)
    *   [4.83 Natural Selection 2](#Natural_Selection_2)
    *   [4.84 Nuclear Throne](#Nuclear_Throne)
        *   [4.84.1 Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found_2)
    *   [4.85 Oxygen Not Included](#Oxygen_Not_Included)
        *   [4.85.1 World generation hangs](#World_generation_hangs)
    *   [4.86 Penumbra: Overture](#Penumbra:_Overture)
        *   [4.86.1 Windowed mode](#Windowed_mode_2)
    *   [4.87 The Polynomial](#The_Polynomial)
        *   [4.87.1 Segfaults during program start on 64-bit systems](#Segfaults_during_program_start_on_64-bit_systems)
    *   [4.88 Portal 2](#Portal_2)
        *   [4.88.1 Game does not start](#Game_does_not_start_10)
        *   [4.88.2 Resolution too low](#Resolution_too_low)
        *   [4.88.3 Missing non Latin font](#Missing_non_Latin_font)
    *   [4.89 Prison Architect](#Prison_Architect)
        *   [4.89.1 ALSA error when using PulseAudio](#ALSA_error_when_using_PulseAudio)
    *   [4.90 Project Zomboid](#Project_Zomboid)
        *   [4.90.1 No sound](#No_sound_6)
    *   [4.91 Pyre](#Pyre)
        *   [4.91.1 Game does not start](#Game_does_not_start_11)
    *   [4.92 Redshirt](#Redshirt)
    *   [4.93 Revenge of the Titans](#Revenge_of_the_Titans)
    *   [4.94 Risk of Rain](#Risk_of_Rain)
    *   [4.95 Rock Boshers DX: Directors Cut](#Rock_Boshers_DX:_Directors_Cut)
    *   [4.96 Saints Row IV](#Saints_Row_IV)
        *   [4.96.1 Game fails to launch after update to new Nvidia drivers](#Game_fails_to_launch_after_update_to_new_Nvidia_drivers)
        *   [4.96.2 Game causes GPU lockup with mesa drivers](#Game_causes_GPU_lockup_with_mesa_drivers)
    *   [4.97 Serious Sam 3: BFE](#Serious_Sam_3:_BFE)
        *   [4.97.1 No audio](#No_audio_2)
    *   [4.98 Slay the Spire](#Slay_the_Spire)
    *   [4.99 Songbringer](#Songbringer)
        *   [4.99.1 Launch error with Wayland](#Launch_error_with_Wayland)
    *   [4.100 Space Pirates and Zombies](#Space_Pirates_and_Zombies)
        *   [4.100.1 No audio](#No_audio_3)
    *   [4.101 Spacechem](#Spacechem)
        *   [4.101.1 Game crash](#Game_crash)
    *   [4.102 Splice](#Splice)
    *   [4.103 The Stanley Parable](#The_Stanley_Parable)
        *   [4.103.1 Game won't start](#Game_won.27t_start)
    *   [4.104 Shadow Tactics: Blades of the Shogun](#Shadow_Tactics:_Blades_of_the_Shogun)
    *   [4.105 Steel Storm: Burning Retribution](#Steel_Storm:_Burning_Retribution)
        *   [4.105.1 Start with black screen](#Start_with_black_screen)
    *   [4.106 Stellaris](#Stellaris)
        *   [4.106.1 No window opening, only sound](#No_window_opening.2C_only_sound)
    *   [4.107 Stephen's Sausage Roll](#Stephen.27s_Sausage_Roll)
        *   [4.107.1 No sound](#No_sound_7)
    *   [4.108 Superbrothers: Sword & Sworcery EP](#Superbrothers:_Sword_.26_Sworcery_EP)
    *   [4.109 System Shock 2](#System_Shock_2)
    *   [4.110 Tabletop Simulator](#Tabletop_Simulator)
        *   [4.110.1 CJK characters not showing in game](#CJK_characters_not_showing_in_game)
    *   [4.111 Team Fortress 2](#Team_Fortress_2)
        *   [4.111.1 HRTF setup](#HRTF_setup)
        *   [4.111.2 Loading screen freeze](#Loading_screen_freeze)
        *   [4.111.3 No audio](#No_audio_4)
        *   [4.111.4 Slow loading textures](#Slow_loading_textures)
    *   [4.112 Terraria](#Terraria)
    *   [4.113 This War of Mine](#This_War_of_Mine)
        *   [4.113.1 Game does not start](#Game_does_not_start_12)
        *   [4.113.2 Sound glitches with Steam native](#Sound_glitches_with_Steam_native)
    *   [4.114 Ticket to Ride](#Ticket_to_Ride)
    *   [4.115 The Tiny Bang Story](#The_Tiny_Bang_Story)
        *   [4.115.1 Missing libGLEW.so.1.6](#Missing_libGLEW.so.1.6)
    *   [4.116 Tomb Raider](#Tomb_Raider)
        *   [4.116.1 Game immediately closes when running with steam-native](#Game_immediately_closes_when_running_with_steam-native)
        *   [4.116.2 Steam Controller not working in-game](#Steam_Controller_not_working_in-game)
    *   [4.117 Torchlight 2](#Torchlight_2)
        *   [4.117.1 Libfreetype/libfontconfig Incompatibility](#Libfreetype.2Flibfontconfig_Incompatibility)
        *   [4.117.2 Locale incompatibility](#Locale_incompatibility)
    *   [4.118 Tower Unite](#Tower_Unite)
        *   [4.118.1 Graphical Glitches](#Graphical_Glitches)
    *   [4.119 Towns / Towns Demo](#Towns_.2F_Towns_Demo)
    *   [4.120 Transistor](#Transistor)
        *   [4.120.1 Crash on launch / FMOD binding crash / audio issues](#Crash_on_launch_.2F_FMOD_binding_crash_.2F_audio_issues)
    *   [4.121 Transmissions: Element 120](#Transmissions:_Element_120)
        *   [4.121.1 Troubleshooting](#Troubleshooting)
    *   [4.122 Trine 2](#Trine_2)
        *   [4.122.1 Colors](#Colors)
        *   [4.122.2 Sound](#Sound)
        *   [4.122.3 Resolution](#Resolution)
    *   [4.123 Tropico 5](#Tropico_5)
        *   [4.123.1 Blank screen with sound only on startup](#Blank_screen_with_sound_only_on_startup)
    *   [4.124 Unity of Command](#Unity_of_Command)
        *   [4.124.1 Squares](#Squares)
        *   [4.124.2 No audio](#No_audio_5)
    *   [4.125 Unity3D](#Unity3D)
        *   [4.125.1 Locale settings](#Locale_settings)
        *   [4.125.2 Unity 5 sound problems](#Unity_5_sound_problems)
        *   [4.125.3 Game launching on wrong monitor in fullscreen mode](#Game_launching_on_wrong_monitor_in_fullscreen_mode_2)
        *   [4.125.4 Chinese/Japanese/Korean display bug](#Chinese.2FJapanese.2FKorean_display_bug)
        *   [4.125.5 Game does not respond](#Game_does_not_respond)
    *   [4.126 Unrest](#Unrest)
    *   [4.127 Volgarr the Viking](#Volgarr_the_Viking)
    *   [4.128 War Thunder](#War_Thunder)
        *   [4.128.1 No audio](#No_audio_6)
        *   [4.128.2 Blank screen](#Blank_screen)
    *   [4.129 Warhammer 40,000: Dawn of War II](#Warhammer_40.2C000:_Dawn_of_War_II)
    *   [4.130 We Were Here](#We_Were_Here)
        *   [4.130.1 Stuck on black screen or logo on launch](#Stuck_on_black_screen_or_logo_on_launch)
    *   [4.131 Worms W.M.D](#Worms_W.M.D)
    *   [4.132 Witcher 2: Assassin of Kings](#Witcher_2:_Assassin_of_Kings)
        *   [4.132.1 Game does not start](#Game_does_not_start_13)
    *   [4.133 Wizardry 6: Bane of the Cosmic Forge](#Wizardry_6:_Bane_of_the_Cosmic_Forge)
    *   [4.134 World of Goo](#World_of_Goo)
        *   [4.134.1 Changing resolution](#Changing_resolution)
    *   [4.135 X3: Terran Conflict](#X3:_Terran_Conflict)
        *   [4.135.1 Game crashes on startup](#Game_crashes_on_startup)
    *   [4.136 XCOM](#XCOM)
        *   [4.136.1 Hangs on startup](#Hangs_on_startup)
        *   [4.136.2 Graphical glitches on Intel HD](#Graphical_glitches_on_Intel_HD)

## Introduction

See [Steam/Troubleshooting](/index.php/Steam/Troubleshooting "Steam/Troubleshooting") first.

This page assumes familiarity with the [Steam#Directory structure](/index.php/Steam#Directory_structure "Steam"), [Steam#Launch options](/index.php/Steam#Launch_options "Steam"), [environment variables](/index.php/Environment_variables "Environment variables"), the [Steam runtime](/index.php/Steam_runtime "Steam runtime") and [shared libraries](/index.php/Steam/Troubleshooting#Debugging_shared_libraries "Steam/Troubleshooting"). The `*GAME*` pseudo-variable is used to refer to a game's directory. When the text reads "*run the game with `FOO=bar`*" it is implied that you either update your launch options or run the game from the command-line with the environment variable.

## Contributing

*   Use "game directory" or the `*GAME*` pseudo-variable to refer to a game's directory.
*   Link bug reports and sources of workarounds.

## Common steps

### OpenSSL 1.0 setup

Some Steam games are built against OpenSSL 1.0\. ([FS#53618](https://bugs.archlinux.org/task/53618))

Install [lib32-openssl-1.0](https://www.archlinux.org/packages/?name=lib32-openssl-1.0) and run the game with `LD_LIBRARY_PATH=/usr/lib/openssl-1.0`.

### Adobe Air setup

The package [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/) installs Adobe Air not in the place where the game expects it to be, fix this by creating the following symlink:

```
# ln -s "/opt/adobe-air-sdk/runtimes/air/linux/Adobe AIR" "/opt/Adobe AIR"

```

Adobe AIR requires you to accept its EULA by creating the file `~/.appdata/Adobe/AIR/eulaAccepted` containing `2`.

### Steam Link

Currently Steam Link does not work with Wayland. You will only see a blank screen or even flickering when connecting to a Steam host running on Wayland. So you have to disable Wayland in /etc/gdm/custom.conf:

```
WaylandEnable=false

```

And reboot before trying again.

## Games

### Alien Isolation

#### Missing libpcre.so.3

```
$ ln -s /usr/lib/libpcre.so *GAME*/lib/x86_64

```

Append `./lib/x86_64` to your `LD_LIBRARY_PATH`.[[1]](https://steamcommunity.com/app/214490/discussions/0/154644705028020291/)

### Amnesia: The Dark Descent

Dependencies: [[2]](https://steamcommunity.com/app/221410/discussions/0/864957183198111387/)

*   [lib32-freealut](https://aur.archlinux.org/packages/lib32-freealut/)
*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxmu](https://www.archlinux.org/packages/?name=lib32-libxmu)
*   [lib32-sdl_ttf](https://www.archlinux.org/packages/?name=lib32-sdl_ttf)

### And Yet It Moves

Dependencies:

*   [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)
*   [lib32-libtheora](https://www.archlinux.org/packages/?name=lib32-libtheora)
*   [lib32-libtiff4](https://www.archlinux.org/packages/?name=lib32-libtiff4)

#### Game does not start

When the game refuses to launch and prints one of the following error messages:

```
readlink: extra operand ‘Yet’
Try 'readlink --help' for more information.

```

```
This script must be run as a user with write priviledges to game directory

```

Open `*GAME*/AndYetItMovesSteam.sh` and surround `${BASH_SOURCE[0]}` in the following line with double quotes.

```
ayim_dir="$(dirname "$(readlink -f ${BASH_SOURCE[0]})")"

```

### Anodyne

Dependencies:

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/), follow [#Adobe Air setup](#Adobe_Air_setup)
*   [xterm](https://www.archlinux.org/packages/?name=xterm) (probably not required)

#### Play with a controller: joy2key configuration

Configuration example to play Anodyne with an XBox 360 Wireless Controller

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

### Aquaria

#### Mouse pointer gets stuck in one direction

If the mouse pointer gets stuck in one direction, make sure `*GAME*/usersettings.xml` contains `<JoystickEnabled on="0" />`.

If that does not fix the issue, try unplugging any joysticks or joystick adapter devices you have plugged in.

### ARK: Survival Evolved

#### Game does not start, displays text window with unreadable text

Run the game with `MESA_GL_VERSION_OVERRIDE=4.0 MESA_GLSL_VERSION_OVERRIDE=400`.

#### Gray water

Download the TheCenter map and copy `Water_DepthBlur_MIC.uasset` from that map into TheIsland as described [here](https://www.gamingonlinux.com/articles/heres-a-way-to-fix-the-broken-water-in-ark-survival-evolved-on-linux.10530).

Ragnarok uses TheIsland's texture, so the same procedure fixes the issue on Ragnarok as well.

#### Segmentation fault on startup

Caused by the games packaged libopenal. Use system libopenal to solve the segfault by running the game with with `LD_PRELOAD=/usr/lib/libopenal.so.1`

### Audiosurf 2

#### error. unable to load song <filename> ,came back with zero duration

If you get this in your log, install [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

### BADLAND: Game of the Year Edition

Refer to [#Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found).

### Beat Cop

#### "BeatCop.x86_64" is not responding

Run `BeatCop.x86` instead of `BeatCop.x86_64`.

### Binding of Isaac: Rebirth

#### No sound

**Note:** This also helps with Never Alone (Kisima Ingitchuna) and No Time to Explain.

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

Adjust the audio levels in the game options.

### BioShock Infinite

#### Game launching on wrong monitor in fullscreen mode

Add the following launch option:

```
--eon_force_display=1

```

### BLACKHOLE

Refer to [#Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found).

### Black Mesa

Install [lib32-gperftools](https://aur.archlinux.org/packages/lib32-gperftools/) for 32bit version of libtcmalloc_minimal.so.4 which is needed [Source](https://steamcommunity.com/app/362890/discussions/1/340412628175324858/?ctp=7).

### Block'hood

#### White screen on startup

When launched the game may only display a white screen with no interface and no way to play the game. Add "-screen-fullscreen 0" to launch options.

### The Book of Unwritten Tales

Dependencies:

*   [lib32-jasper](https://aur.archlinux.org/packages/lib32-jasper/)
*   [lib32-libxaw](https://aur.archlinux.org/packages/lib32-libxaw/)

If the game does not start, uncheck: *Properties > Enable Steam Community In-Game*.

The game is known to segfault when opening the settings and possibly during or before playing. A workaround from the [Steam discussions](http://steamcommunity.com/app/221410/discussions/3/846939071081758230/#p2) is to replace the game's `RenderSystem_GL.so` with one from Debian's repositories. To do that download [this deb file](https://launchpad.net/ubuntu/+archive/primary/+files/libogre-1.7.4_1.7.4-3_i386.deb), and extract it with [dpkg](https://aur.archlinux.org/packages/dpkg/):

```
$ dpkg -x libogre-*.deb outdir

```

Now replace `*GAME*/lib/32/RenderSystem_GL.so` with the one extracted from the `.deb` package.

### BRAIN/OUT

If the game does not start with error message saying "invalid app configuration". Change directory to game folder:

```
$ cd ~/.steam/steam/steamapps/common/BrainOut/

```

Run game directly:

```
$ java -jar brainout-steam.jar

```

You need to have steam running in the background.

### The Book of Unwritten Tales: The Critter Chronicles

See [#The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales).

To prevent the game from crashing at the end credits, change the size of the credits image as described [here](http://steamcommunity.com/app/221830/discussions/0/828925849276110960/#c810921273836530791).

### Borderlands 2

#### Migrating saves from other platforms

Borderlands 2 does not support cross-platform Steam Cloud syncing, you have to manually copy the files between platforms. Save locations can be found [here](https://pcgamingwiki.com/wiki/Borderlands_2#Game_data). Make sure your user can access the files.

#### Using Ctrl Key

Borderlands 2 does not allow the `Ctrl` key to be used by default. The game seems to be accessing keycodes and not keysyms, therefore xmodmap has no affect. A workaround is using *setkeycodes* to map the Ctrl-scancode to some other key, as described in [Map scancodes to keycodes#Using setkeycodes](/index.php/Map_scancodes_to_keycodes#Using_setkeycodes "Map scancodes to keycodes"). I use `setkeycodes 0x1d 56` (as root) to map Ctrl to Alt before starting the game and `setkeycodes 0x1d 29` to restore the default.

#### Logging into SHiFT

Out of the box you will not be able to log into SHiFT since the game expects certificates to be in `/usr/lib/ssl`, which is where Ubuntu stores them. Arch however uses `/etc/ssl`. To resolve the problem, run the game with `SSL_CERT_DIR=/etc/ssl/certs`.

#### Game crashes nearly instantly

The game crashes in libopenal directly after launch.

Possible solution 0: Run the game with the `-nostartupmovies` flag. It no longer crashes in libopenal with a general protection error.

Possible solution 1: As of lib32-openal version 1.18.0-1, the game crashes instantly. The possible solutions are to downgrade lib32-openal to 1.17.2-1, or to start the game with `LD_PRELOAD='$HOME/.steam/root/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libopenal.so.1'`.

In case there are messages like this in the terminal:

```
[  671.617205] Borderlands2[2772]: segfault at 0 ip           (null) sp 00000000ff9a462c error 14 in Borderlands2[8048000+235a000]

```

The following change may help ([source](http://steamcommunity.com/app/49520/discussions/0/348292787746982160/)):

```
LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%

```

### Borderlands: The Pre-Sequel

See [#Borderlands 2](#Borderlands_2).

#### Keyboard not working

This can occur with certain window managers e.g. [dwm](/index.php/Dwm "Dwm"). Try a different [window manager](/index.php/Window_manager "Window manager").

#### Not starting via Steam

If the game appears as *Running*, then syncs and closes when you launch it from Steam, try creating a `steam_appid.txt` in the game directory containing `261640`. This should resolve the issue and let you start the game directly from the game directory. If that does not work, try using the [steam-native-runtime](https://www.archlinux.org/packages/?name=steam-native-runtime).

### Cities in Motion 2

#### Dialog boxes fail to display properly

You will not be able to read or see anything, and you will have this in your logs:

```
Fontconfig error: "/etc/fonts/conf.d/10-scale-bitmap-fonts.conf", line 69: non-double matrix element
Fontconfig error: "/etc/fonts/conf.d/10-scale-bitmap-fonts.conf", line 69: wrong number of matrix elements

```

Workaround for the bug [FS#35039](https://bugs.archlinux.org/task/35039) is available [here](http://bpaste.net/show/167019/)  (replace `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`).

### Cities Skylines

#### Textures not rendering properly

Run the game with `UNITY_DISABLE_GRAPHICS_DRIVER_WORKAROUNDS=yes`.

### Civilization V

Run the game with `LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6' %command%`.[[3]](https://github.com/ValveSoftware/steam-for-linux/issues/4379)

#### Stuttering sound with PulseAudio

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting").

#### Game crashes seconds after loading a map

If you have a CPU with more than 8 threads (such as AMD Ryzen), set `MaxSimultaneousThreads` to `16` in `config.ini` in game directory.[[4]](https://www.reddit.com/r/civ5/comments/5z77jr/game_crashes_randomly_on_linux_amd_ryzen/)

#### Game crashes after intro video with "Unable to load texture (LoadingBaseGame.dds)"

The issue is a result of the game calling some file in a case-insensitive manner.

The solution is either to install the game on a case-insensitive file system like VFAT, or on a mount point for [ciopfs](https://aur.archlinux.org/packages/ciopfs/).

### Civilization: Beyond earth

If you are getting an instant crash/close upon launch, make sure you have the following packages installed:

*   [lib32-intel-tbb](https://aur.archlinux.org/packages/lib32-intel-tbb/)
*   [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)

#### Segfault after a few minutes

Backtrace:

```
   #0  0x08b71d06 in FireGrafix::DynamicsLock<Graphics::BuildingSkinnedDataDynamicConsts>::DynamicsLock(Graphics::SurfaceSet**, FireGrafix::SurfaceSetPoolAllocator*, unsigned short) ()
   #1  0x08c25ffc in cvLandmarkVisSystem::cvLandmarkVisDynamicConstantUpdaterSS::HandleBuildingShaderSkinned(Graphics::FGXShaderPackageInstanceView*, FireGrafix::FGXModelNode*, FGXVector4*) ()
   #2  0x08c25f34 in cvLandmarkVisSystem::cvLandmarkVisDynamicConstantUpdaterSS::UpdateNode(Graphics::FGXShaderPackageInstanceView*, FireGrafix::FGXModelNode*, FGXVector4*) ()
   #3  0x08c25e2c in FireGrafix::FGXModelRenderByNodeSSExample_Shadow<cvLandmarkVisSystem::cvLandmarkVisDynamicConstantUpdaterSS, 2, FireGrafix::FGXModelRenderEndSuperclass>::RenderNode(unsigned int*, FireGrafix::FGX_SPIV_GENERIC*, FireGrafix::FGXModelNode*, FGXVector4*) ()
   #4  0x08c24ff5 in cvLandmarkVisSystem::LandmarkRenderJob::Execute(unsigned int) ()
   #5  0x093d26d9 in Platform::JobTask::execute() ()
   #6  0xf749f3c0 in ?? () from /usr/lib32/libtbb.so.2
   #7  0xf7497551 in ?? () from /usr/lib32/libtbb.so.2
   #8  0xf7495fc3 in ?? () from /usr/lib32/libtbb.so.2
   #9  0xf7491b7e in ?? () from /usr/lib32/libtbb.so.2
   #10 0xf7491db7 in ?? () from /usr/lib32/libtbb.so.2
   #11 0xf78f4346 in start_thread () from /usr/lib32/libpthread.so.0
   #12 0xf7716026 in clone () from /usr/lib32/libc.so.6

```

Segfault is caused by [lib32-intel-tbb](https://aur.archlinux.org/packages/lib32-intel-tbb/). To fix the issue:

1.  Download [libtbb2 deb-package](https://packages.ubuntu.com/trusty/i386/libtbb2/download) from one of the Ubuntu mirrors.
2.  Unpack `libtbb.so.2` from `libtbb2_4.2_20130725-1.1ubuntu1_i386.deb/data.tar.xz/usr/lib` into the game directory.
3.  Run the game with `LD_PRELOAD='./libtbb.so.2'`.

### Civilization VI

Either run with steam-native or `env LD_PRELOAD='./libcxxrt.so:/usr/$LIB/libstdc++.so.6'`. The latter will disable the Steam overlay.

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

#### If Segfault Immediately on Start

This is a strange corner case which happens infrequently at best (and the prerequisites for reproducing it are unknown), but the crash would look like this:

1.  Immediate segfault on start, before any windows get created
2.  The game creates `~/.local/share/aspyr-media/Sid Meier's Civilization VI/AppOptions.txt`
3.  The string `AppHost::BugSubmissionPackager::BugSubmissionPackager` appears inhttp://store.steampowered.com/app/310080/Hatoful_Boyfriend/ the backtrace output when running the game under [gdb](https://www.archlinux.org/packages/?name=gdb)
    1.  To run under [gdb](https://www.archlinux.org/packages/?name=gdb), first launch a shell and change into the game directory.
    2.  Then `echo 289070 > steam_appid.txt` *(otherwise the game won't launch outside of Steam itself)*
    3.  Then run something like `gdb -ex run -ex bt -ex quit --args ./Civ6 ./Civ6`
    4.  The relevant info towards the end of the output should look like this:

```
   Thread 3 "Civ6" received signal SIGSEGV, Segmentation fault.
   [Switching to Thread 0x7fffe5d06700 (LWP 12315)]
   0x000000000201121e in AppHost::BugSubmissionPackager::BugSubmissionPackager(unsigned long, String::BasicT<Platform::StaticHeapAllocator<5, 0>, (String::Encoding)4> const&, String::BasicT<Platform::StaticHeapAllocator<5, 0>, (String::Encoding)0> const&, AppHost::ModuleVersionInfo const&) ()
   #0  0x000000000201121e in AppHost::BugSubmissionPackager::BugSubmissionPackager(unsigned long, String::BasicT<Platform::StaticHeapAllocator<5, 0>, (String::Encoding)4> const&, String::BasicT<Platform::StaticHeapAllocator<5, 0>, (String::Encoding)0> const&, AppHost::ModuleVersionInfo const&) ()
   #1  0x000000000200c796 in AppHost::_INTERNAL::SetupFXSPlatform(AppHost::AppEnvironment const*, AppHost::AppOptions*)
       ()
   #2  0x000000000200fea0 in AppHost::RunApp(int, char**, AppHost::Application*) ()
   #3  0x000000000200f9bc in AppHost::RunApp(char*, AppHost::Application*) ()
   #4  0x0000000001112d98 in WinMain ()
   #5  0x00000000010bdab0 in ?? ()
   #6  0x00000000010bfb31 in ThreadHANDLE::ThreadProc(void*) ()
   #7  0x00007ffff473e08a in start_thread () from /usr/lib/libpthread.so.0
   #8  0x00007ffff38f747f in clone () from /usr/lib/libc.so.6

```

If all of that is the case for you, the fix is pretty simple. Edit `~/.local/share/aspyr-media/Sid Meier's Civilization VI/AppOptions.txt` and change the line reading `EnableBugCollection 1` to `EnableBugCollection 0`.

Presumably this fix will prevent any automated bug reports from reaching Aspyr, should you encounter crashes/bugs in the future, but it will at least let the game launch properly.

### Deus Ex: Mankind divided

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

Requires [librtmp0](https://www.archlinux.org/packages/?name=librtmp0).

Also if you use Bumblebee set your [launch options](/index.php/Launch_option "Launch option") to:

```
LD_PRELOAD="$LD_PRELOAD:libpthread.so.0:libGL.so.1" __GL_THREADED_OPTIMIZATIONS=1  optirun %command%

```

### The Clockwork Man

Requires [lib32-libidn](https://www.archlinux.org/packages/?name=lib32-libidn) (pulled in by [steam-native-runtime](https://www.archlinux.org/packages/?name=steam-native-runtime)).

### Company of Heroes 2

#### Missing libpcre.so.3

Like with [#Alien Isolation](#Alien_Isolation) you need to symlink `/usr/lib/libpcre.so` to `*GAME*/lib/*arch*/libpcre.so.3`, otherwise the game will fail to start.

### Cossacks 3

#### No sound

Use the steam-runtime, e.g. set the [launch options](https://support.steampowered.com/kb_article.php?ref=1040-JWMT-2947) to:

```
~/.steam/root/ubuntu12_32/steam-runtime/run.sh %command%

```

#### Flashing screen with primus

Set `PRIMUS_SYNC=2`in the launch options.

### Counter-Strike: Global Offensive (CS:GO)

#### Game starts on the wrong screen

[csgo-osx-linux issue #60](https://github.com/ValveSoftware/csgo-osx-linux/issues/60)

If it happens, go into fullscreen windowed or windowed mode and drag the window to the correct monitor. Then go back into fullscreen, the game should now be on the correct monitor.

#### Cannot reach bottom of the screen on menus

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

Here X and Y is 0,2560 to move the window to the monitor on the right and H and W 1600,1200 is set to match the in-game resolution.

#### Sound is played slightly delayed

[csgo-osx-linux issue #45](https://github.com/ValveSoftware/csgo-osx-linux/issues/45)

See [PulseAudio/Troubleshooting#Laggy sound](/index.php/PulseAudio/Troubleshooting#Laggy_sound "PulseAudio/Troubleshooting") for a possible solution.

#### Mouse not working in-game

If your mouse works in the main menu but not in-game, run the game with `SDL_VIDEO_X11_DGAMOUSE=0`. [[5]](https://bbs.archlinux.org/viewtopic.php?id=184905)

#### Brightness slider not working

[Install](/index.php/Install "Install") [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and run `xrandr` to find out the name of your connected display output.

Edit `*GAME*/csgo.sh` and add the following lines (adapt *output_name*):

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

#### Microphone not working

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

#### Mouse is unrensponsive or moves slowly

Set launch options to:

```
vblank_mode=0 %command%

```

Works with almost any other game.

### Creeper World 3: Arc Eternal

#### Game does not start

Search for Player.log (might be in ~/.config/unity3d/Knuckle Cracker LLC/Creeper World 3/ )

If it says somewhere in Player.log "FMOD failed to get number of drivers ... An error occured that wasn't supposed to. Contact support." Unity is probably having problem with some pulse audio libraries.

Fix that worked for me: Remove or rename all instances of libpulse-simple* files.

Places to look for them: /usr/lib /usr/lib32 ~/.steam/steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/ ~/.steam/steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/

### Crusader Kings II

x86_64 dependencies:

*   [lib32-openssl](https://www.archlinux.org/packages/?name=lib32-openssl)

#### No audio

SDL uses [PulseAudio](/index.php/PulseAudio "PulseAudio") by default, so to use it with [ALSA](/index.php/ALSA "ALSA") you need to set:

 `~/.pam_environment`  `SDL_AUDIODRIVER=alsa` 

#### Oddly sized starting window

You can make full screen mode the default by setting `fullscreen=yes` in `~/.paradoxinteractive/Crusader Kings II/settings.txt`.

#### DLCs not detected

If the DLC tab in the launcher is not selectable, rename the `DLC` directory in the game directory to `dlc`.

### Crypt of the NecroDancer

#### Crashes after splash screen

The following error occurs if launching Steam from the terminal.

```
FMOD ERROR: UpdateFMOD SystemUpdate: This command failed because System::init or System::setDriver was not called.

```

This error is solved by installing [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

### The Curious Expedition

#### Game stuck on loading screen

The Electron shipped with this game is too old for Arch Linux.

Install [electron](https://www.archlinux.org/packages/?name=electron) and run the game with `electron resources/app.asar`.

### Death Road To Canada

#### No music

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

### Defender's Quest: Valley of the Forgotten

Dependencies:

*   [adobe-air-sdk](https://aur.archlinux.org/packages/adobe-air-sdk/), follow [#Adobe Air setup](#Adobe_Air_setup)
*   [xterm](https://www.archlinux.org/packages/?name=xterm)
*   [lib32-libcanberra](https://www.archlinux.org/packages/?name=lib32-libcanberra)

### Dirt

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

### Dirt Rally

Prepend `lib/x86_64` to your `LD_LIBRARY_PATH`, otherwise the game will fail to start.

**Note:** The order of the paths is important. `$LD_LIBRARY_PATH` must be the last entry or it won't work.

### Divinity: Original Sin - Enhanced Edition

#### Game does not start when using Bumblebee optirun or primusrun

Edit `*GAME*/runner.sh` to use primusrun:

```
LD_LIBRARY_PATH="." primusrun ./EoCApp

```

#### Game does not work with amdgpu

It is a known bug and they have no intention of fixing it, see [the bug](https://bugs.freedesktop.org/show_bug.cgi?id=93551).

Workaround:

Get the following file: [https://bugs.freedesktop.org/attachment.cgi?id=125302](https://bugs.freedesktop.org/attachment.cgi?id=125302) and rename it to `shim.c`

Then execute

```
$ gcc -shared -fpic shim.c -o divhack.so

```

Next, start *steam* and open a console, change to the diviniti directory with

```
$ cd ~/.steam/steam/steamapps/common/Divinity Original Sin Enhanced Edition

```

Edit the contained `runner.sh` as follows:

```
export MESA_GL_VERSION_OVERRIDE=4.2
export MESA_GLSL_VERSION_OVERRIDE=420
export LD_PRELOAD=/path/to/divhack.so
export LD_LIBRARY_PATH="."
./EoCApp
```

Then just start the game. In case it still crashes on loading you may also need to add

 `export allow_glsl_extension_directive_midshader=true` 

### Don't Starve

Dependencies:

*   [lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)

#### No sound

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

In the game, go to the options and adjust the audio levels.

### Dota 2

Dependencies:

*   [libudev0](https://aur.archlinux.org/packages/libudev0/)
*   [libpng12](https://www.archlinux.org/packages/?name=libpng12)

#### In-game font is unreadable

Run the game with `MESA_GL_VERSION_OVERRIDE=2.1`.

#### Error with libpangoft2

1.  [Install](/index.php/Install "Install") the [pango](https://www.archlinux.org/packages/?name=pango) package.
2.  Remove `libpango-1.0.so` and `libpangoft2-1.0.so` in `*GAME*/game/bin/linuxsteamrt64`.
3.  If you are using Bumblebee add `LD_PRELOAD="libpthread.so.0 libGL.so.1" __GL_THREADED_OPTIMIZATIONS=1 optiru` to your [launch options](/index.php/Launch_option "Launch option").

#### The game does not start

If you run the game from the terminal and, although no error is shown, try disabling: *Steam > Settings > In-Game > Enable Steam Community In-Game*.

Apparently the game [#The Book of Unwritten Tales](#The_Book_of_Unwritten_Tales) has the same problem. It also describes a workaround that is untested in Dota 2.

#### Game runs on the wrong screen

	[GitHub Dota 2 issue #11](https://github.com/ValveSoftware/Dota-2/issues/11)

#### Game does not start with libxcb-dri3 error message

After a recent Mesa update, Dota 2 stopped working. The error message is:

```
SDL_GL_LoadLibrary(NULL) failed: Failed loading libGL.so.1: /usr/lib32/libxcb-dri3.so.0: undefined symbol: xcb_send_fd

```

#### Steam overlay

Steam distributes a copy of libxcb which is incompatible with the latest xorg libxcb. See [[6]](https://github.com/ValveSoftware/steam-for-linux/issues/3199), [[7]](https://github.com/ValveSoftware/steam-for-linux/issues/3093).

#### Chinese tips and player names not shown

The Chinese characters in tips and player names are displayed as block characters.

The problem is caused by the font packages: [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu), [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) and [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).

	[GitHub Steam issue #1688](https://github.com/ValveSoftware/Dota-2/issues/1688) 

#### Chinese input method problem

Dota2 is compatible with [IBus](/index.php/IBus "IBus") .

### Devil Daggers

Refer to [#Missing libcurl.so.4 or version CURL_OPENSSL_3 not found](#Missing_libcurl.so.4_or_version_CURL_OPENSSL_3_not_found).

### Drox Operative

If the game fails to start with "Couldn't find Database/database.dbl!", manually extract the assets. assets003.zip will overwrite some files from the previous files.

```
$ cd "~/.steam/root/steamapps/common/Drox Operative/Assets"
$ unzip assets00[123].zip

```

### Dwarfs F2P

Dependencies:

*   [lib32-libgdiplus](https://aur.archlinux.org/packages/lib32-libgdiplus/)

#### Game does not start

There was a bug that stopped Steam from fetching all the needed files. It should be resolved, if you still bump into this problem, try verifying integrity of game cache from game properties, local files tab.

If the game still crashes at startup, edit `*GAME*/Run.sh` and change

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

#### Game crashes

In some cases, the game crashes about 2 minutes before the end of every arcade. This bug has been reported, but there's no known solution to it.

### Dynamite Jack

Requires [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl).

#### Sound Issues

When running on 64-bit Arch Linux, there may be "pops and hisses" when running Dynamite Jack. This could be caused by not having `STEAM_RUNTIME=0` set. (However, even with `STEAM_RUNTIME=0` set, the game may still sometimes start with this issue. Exiting and restarting the game seems to make the problem go away.)

#### Game does not start

If running steam with the `STEAM_RUNTIME=0`, Dynamite Jack may have a problem starting. Check the steam error messages for this message:

```
/home/$USER/.steam/root/steamapps/common/Dynamite Jack/bin/main: error while loading shared libraries: libSDL-1.2.so.0: cannot open shared object file: No such file or directory

```

Install [lib32-sdl](https://www.archlinux.org/packages/?name=lib32-sdl) from [multilib](/index.php/Multilib "Multilib") and Dynamite Jack should start up.

### Empire Total War

#### Weird unreadable fonts

Open `~/.local/share/feral-interactive/Empire/preferences`, then find `UsePBOSurfaces` and change it from 1 to 0.

### Euro Truck Simulator 2

#### Shows only a black screen

Select safe mode when the game starts up.

### Football Manager 2014

This game will not run when installed on an [XFS](/index.php/XFS "XFS") or reiserfs filesystem. Workaround is to install on an ext4 filesystem.

### FORCED

Requires [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu).

This game has 32-bit and 64-bit binaries. For some reason, Steam will launch the 32-bit binary even on 64-bit Arch Linux. When manually launching the 64-bit binary, the game starts, but cannot connect to Steam account, so you cannot play. So install 32-bits dependencies, and launch the game from Steam.

### For the King

Starts with black page. Requires to be told to use the libSDL2 shipping with Steam

Add to Steam launch options for game.

LD_PRELOAD=~/.local/share/Steam/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libSDL2-2.0.so.0 %command%

### FTL: Faster than Light

#### Compatibility

After installation, FTL may fail to run due to a 'Text file busy' error (characterised in Steam by your portrait border going green then blue again). The easiest way to mend this is to just reboot your system. Upon logging back in FTL should run.

The Steam overlay in FTL does not function as it is not a 3D accelerated game. Because of this the desktop notifications will be visible. If playing in fullscreen, therefore, these notifications in some systems may steal focus and revert you back to windowed mode with no way of going back to fullscreen without relaunching. The binaries for FTL on Steam have no DRM and it is possible to run the game *without* Steam running, so in some cases that may be optimum - just ensure that you launch FTL via the launcher script in `*GAME*/data/` rather than the FTL binary in the $arch directory.

#### Problems with open-source video driver

FTL may fail to run if you are using an opensource driver for your video card. There are two solutions: install a proprietary video driver or delete (rename if you are unsure) the library "libstdc++.so.6" inside `*GAME*/data/amd64/lib`. This is if you are using a 64bit system. In case you are using a 32bit system you have to remove (rename) the same library located into `*GAME*/data/x86/lib`.

### Game Dev Tycoon

#### Game does not start

You might get an error about missing `libudev.so.0`.

Run the game with `LD_PRELOAD=/usr/lib/libudev.so.1`.

### Garry's Mod

#### Game does not start

When an error about a missing `client.so` appears, try the following:

```
$ cd ~/.steam/root/steamapps/common/GarrysMod/bin/
$ ln -s libawesomium-1-7.so.0 libawesomium-1-7.so.2
$ ln -s ../garrysmod/bin/client.so ./

```

If the error mentions a missing library for `libgcrypt.so.11`, install [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15).

#### Opening some menus causes the game to crash

Most menus work fine, but ones with checkboxes (LAN multiplayer, mounted games list) do not work at all. This is a bug in the menu code.

If you prefer the default menu style and do not mind a hacky solution: [Simon311](https://github.com/Facepunch/garrysmod-issues/issues/86#issuecomment-30935491) has written code with instructions to fix it.

If you do not care for the default menu style and want a more stable but feature-incomplete solution, Facepunch developer [robotboy655](https://github.com/robotboy655/gmod-lua-menu) has written a new menu.

#### Game crashes after attempting to join server

While in the process of joining a server, downloading resources, etc, the game seems to hang and after a while, perhaps during the "sending client info" portion the game crashes, usually without any error messages. Error does not give much information, however, the process for Garry's mod is killed.

This issue arises more often when joining servers with many addons like DarkRP servers specifically.

The problem seems to correlate with a weak GPU and the game is timing out from the server, so if the GPU is the problem, lowering the graphics settings to the minimum should fix the problem.

The problem seems to be related to RAM usage, once you hit around 2GB of RAM used, the game will crash. Servers with many addons have much more RAM usage, and lowering graphics settings to the minimum lowers RAM usage and mitigates crashes.

### Gods will be watching

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

### GRID Autosport

Follow [#OpenSSL 1.0 setup](#OpenSSL_1.0_setup).

#### Black screen when trying to play

Run the game with `LC_ALL=C`.

### Hack 'n' Slash

#### Crashes when trying to load a game

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

### Hacker Evolution

Requires [lib32-sdl2_mixer](https://www.archlinux.org/packages/?name=lib32-sdl2_mixer).

### Half-Life 2 and episodes

#### Cyrillic fonts problem

This problem can be solved by deleting "Helvetica" font.

### Hammerwatch

#### The game does not start via Steam

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

#### No sound

Hammerwatch opens with a popup: "Sound Error" -- "Could not initialize OpenAL, no sounds will be played. Try updating your OpenAL drivers."

OpenAL, which Hammerwatch uses, defaults to PulseAudio. To change that, add the following line to `/etc/openal/alsoft.conf`:

```
drivers=alsa,pulse

```

This way, Hammerwatch will use ALSA. This solution was found [here](https://stackoverflow.com/questions/9547396/what-does-al-lib-pulseaudio-c612-context-did-not-connect-access-denied-me).

### Harvest: Massive Encounter

Dependencies:

*   [lib32-sfml](https://aur.archlinux.org/packages/lib32-sfml/)
*   [lib32-libjpeg6-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg6-turbo)
*   [lib32-nvidia-cg-toolkit](https://www.archlinux.org/packages/?name=lib32-nvidia-cg-toolkit)
*   [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)

#### Compatibility

If the game refuses to launch and throws you into a library installer loop, run the `Harvest` executable instead of the `run_harvest` script.

### Hatoful Boyfriend

#### Japanese text invisible

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

### HuniePop

#### Game crashes upon launch

Install [lsb-release](https://www.archlinux.org/packages/?name=lsb-release).

### Hyper Light Drifter

#### The controller does not work

[Install](/index.php/Install "Install") [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2) and run the game with `LD_PRELOAD=libSDL2.so`.

See the following Steam Community discussions:

*   [Controller Issues](https://steamcommunity.com/app/257850/discussions/1/365163686036494421)
*   [Common Bugs + Known Issues](https://steamcommunity.com/app/257850/discussions/1/365163686045397160/)

It is suggested to run the *next_update* branch to get new fixes, there however currently is a libcurl segfault keeping it from starting without special workarounds.

#### Missing libcurl.so.4 or version CURL_OPENSSL_3 not found

[Install](/index.php/Install "Install") [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat) and run the game with `LD_PRELOAD=libcurl.so.3`.

### The Impossible Game

Dependencies:

*   [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2)
*   [lib32-sdl2_image](https://www.archlinux.org/packages/?name=lib32-sdl2_image)

### The Inner World

Requires [java-commons-codec](https://aur.archlinux.org/packages/java-commons-codec/) for sound support.

#### Bringing up the inventory or main menu

Hold the tab key.

##### Cutscenes

The game has cutscenes. It starts directly with a cutscene before you start the actual game in the backyard. To see these cutscenes you need to use Oracle's [Java](/index.php/Java "Java") instead of the OpenJDK.

Furthermore you need the package [ffmpeg-compat-55](https://aur.archlinux.org/packages/ffmpeg-compat-55/).

There seem to be problems with the Steam overlay. Try to run the game directly with `*GAME*/TIW_start.sh`.

Note that cutscenes open in a new window. So pay attention to that and switch to the new window to enjoy the movies.

See the [Steam Forums](http://steamcommunity.com/app/251430/discussions/0/611701360817206606/#c611701360827509770) for details.

### Interloper

Requires [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib).

#### Game does not start

The game can sometimes segfault due to an incompatibility with the Steam Runtime's `libasound.so.2`.

### Invisible Apartment

Requires [qt5-multimedia](https://www.archlinux.org/packages/?name=qt5-multimedia).

#### Game does not start

If the game does not run when you launch it via Steam, try to directly run `./ia1` in the game directory.

### Joe Danger 2: The Movie

Requires [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse).

#### Compatibility

Game only worked after obtaining from the [Humble Bundle](https://www.humblebundle.com/) directly and [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) was installed.

### Kerbal Space Program

See [Kerbal Space Program](/index.php/Kerbal_Space_Program "Kerbal Space Program").

### Killing Floor

#### Cannot change screen resolution

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

#### Windowed mode

Uncheck fullscreen in the options menu, and press `Ctrl+g` to stop mouse capturing.

#### Stuttering sound

KillingFloor comes with its own OpenAL library `*GAME*/System/openal.so`.

Back it up, [install](/index.php/Install "Install") [openal](https://www.archlinux.org/packages/?name=openal) or [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal) (if using a 64bit system).

Then symlink the installed system library (`/usr/lib32/libopenal.so.1` or `/usr/lib/libopenal.so.1`) to `openal.so`.

### Left for Dead 2

#### Missing Chinese font

L4D2 Requires [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei). Or add the following lines to `~/.config/fontconfig/fonts.conf`

```
        <match target="pattern">
               <test qual="any" name="family">
                       <string>WenQuanYi Zen Hei</string>
               </test>
               <edit name="family" mode="assign" binding="same">
                       <string>Source Han Sans CN</string>
               </edit>
       </match>

```

### Lethal League

Requires [lib32-glew1.10](https://www.archlinux.org/packages/?name=lib32-glew1.10).

### Life is Strange

Requires [librtmp0](https://www.archlinux.org/packages/?name=librtmp0), [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image).

### Little Racers STREET

Install [sdl2_mixer](https://www.archlinux.org/packages/?name=sdl2_mixer).

Move/backup `*GAME*/lib64/libSDL2_mixer-2.0.so.0`.

Symlink `/usr/lib/libSDL2_mixer-2.0.so.0` to `*GAME*/lib64/libSDL2_mixer-2.0.so.0`.

### The Long Dark

#### Game does not start

The 64-bit version fails to start. Either use the 32-bit version `tld.x86` in the game directory or start the 64-bit version like so:

```
LD_PRELOAD=~/.steam/root/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libSDL2-2.0.so.0 ./tld.x86_64

```

#### Game starts, but some overlay text is missing and cutscenes shows black screen

In addition to the command above, add the following to the Steam launch command:

```
-screen-fullscreen 0 -screen-width WIDTH_PIXELS -screen-height HEIGHT_PIXELS

```

For example, if you have a screen resolution of 1280x720 and are launching the x64 version from the terminal (within the directory which contains the binaries), the full command would be:

```
LD_PRELOAD=~/.steam/root/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libSDL2-2.0.so.0 ./tld.x86_64 -screen-fullscreen 0 -screen-width 1280 -screen-height 720

```

and from Steam, the complete game [launch options](/index.php/Launch_option "Launch option") would be:

```
LD_PRELOAD=~/.steam/root/ubuntu12_32/steam-runtime/amd64/usr/lib/x86_64-linux-gnu/libSDL2-2.0.so.0 %command% -screen-fullscreen 0 -screen-width 1280 -screen-height 720

```

#### Cutscenes are still black

Turn off Vertical Sync in the Display options, and/or set POST FX to Low in the Quality options, and/or turn global Quality options down a notch.

#### Cursor disappears

Go to Options > Controls, and set mouse locking to unlocked.

The options is visible only if you're navigating using your (invisible) mouse. It will not show up when navigating with a controller. One solution is to go to Options -> Controls with a controller before switching to the mouse and trying to blindly it the setting.

### Magicka 2

#### Indefinitely stuck at start

The game does not start if the output of the command "ip -s link" is longer than 4096 characters. That is because, in the function bitsquid::network_info(char*), where they query the networking information, they do not handle that case correctly. See [this picture](https://i.imgur.com/AOTLoTY.png) for reference. It was reported to upstream (Pieces Interactive) but Magicka 2 does not seem to be maintained anymore.

A dirty fix is to wrap your ip binary, as such:

```
#!/bin/bash
if [[ $@ == "-s link" ]]; then
    echo "<paste a smaller subset of the normal output>"
else
    /path/to/your/real/ip "$@"
fi

```

### Mark of the Ninja

#### Bad sound

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

### Metro: Last Light

The game does not allow you to change its resolution on a multi-monitor setup on GNOME with the AMD Catalyst drivers. A temporary workaround is to disable the side monitors. Jason over at [unencumbered by facts](http://unencumberedbyfacts.com/2013/11/20/multiple-monitor-gaming-on-linux/) managed to get it working with his multi-monitor setup using a single display server, he however is using Nvidia.

### Metro: 2033 Redux

#### No sound

The game does not properly support [PulseAudio](/index.php/PulseAudio "PulseAudio"), so you will have to use ALSA. Run the game with `SDL_AUDIODRIVER=alsa`. Create the file `~/.asoundrc`. Get your card/device number with `aplay -l`. Add the following to your `~/.asoundrc` (replace card and device no with the one you got from `aplay -l`)

```
pcm.!default { 
    type hw
    card 0
    device 0
}

ctl.!default {
    type hw
    card 0
    device 0 
}

```

Before starting the game make sure to kill PulseAudio with `pulseaudio -k`.

### No image

Try setting `r_fullscreen off` in `~/.local/share/Steam/steamapps/common/Metro 2033 Redux/user.cfg`.

### Middle-earth: Shadow of Mordor

#### Floating heads

Run the game with `__GL_ShaderPortabilityWarnings=0`.

### Mount & Blade: Warband

#### Segmentation fault (core dumped) with wayland

Use [Xorg](/index.php/Xorg "Xorg") instead.

#### DLC Chooser

Requires [lib32-nas](https://aur.archlinux.org/packages/lib32-nas/).

#### Crash on startup

Set launch options to:

```
LD_LIBRARY_PATH="." %command%

```

### Multiwinia

Requires [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

#### Crash on startup

If Multiwinia crashes on startup on X64 systems, force launching the 32-bit executable by replacing `*GAME*/run_steam.sh` with the following script:

```
#!/bin/sh
./multiwinia.bin.x86

```

See [[8]](https://steamcommunity.com/app/1530/discussions/0/864969481950542663/#c558746995160431396).

### Natural Selection 2

[sndio](https://www.archlinux.org/packages/?name=sndio) is required, furthermore, you must also execute

```
$ ln -s /usr/lib/libsndio.so x64/libsndio.so.6.1

```

within the root of the NS2 directory. This is because NS2 uses an older outdated version of sndio, but it is still compatible with the new version, thankfully.

For a more minimal solution, one can attempt to set the audio driver used through the environment variable `SDL_AUDIODRIVER`. For example, `SDL_AUDIODRIVER=sndio` or `SDL_AUDIODRIVER=alsa`.

The environment variable `SDL_VIDEODRIVER` must not be set to `wayland`. Try setting `SDL_VIDEODRIVER` to `x11` if it still does not work.

### Nuclear Throne

#### Missing libcurl.so.4 or version CURL_OPENSSL_3 not found

[Install](/index.php/Install "Install") [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat) and run the game with `LD_PRELOAD=libcurl.so.3`.

### Oxygen Not Included

#### World generation hangs

This problem occurs with locales that use comas instead of dots to separate decimals.

Set launch options in steam to `LANG=C %command%`.[[9]](http://steamcommunity.com/app/457140/discussions/3/1488866180617243731/#c1488866813753688864)

### Penumbra: Overture

Dependencies:

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libvorbis](https://www.archlinux.org/packages/?name=lib32-libvorbis)
*   [lib32-libxft](https://www.archlinux.org/packages/?name=lib32-libxft)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [lib32-sdl_image](https://www.archlinux.org/packages/?name=lib32-sdl_image)
*   [lib32-sdl_ttf](https://www.archlinux.org/packages/?name=lib32-sdl_ttf)

#### Windowed mode

There is no in-game option to change to the windowed mode, you will have to edit `~/.frictionalgames/Penumbra/Overture/settings.cfg` to activate it.

Find `FullScreen="true"` and change it to `FullScreen="false"`, after this the game should start in windowed mode.

### The Polynomial

Dependencies:

*   [ilmbase102-libs](https://aur.archlinux.org/packages/ilmbase102-libs/)
*   [openexr170-libs](https://aur.archlinux.org/packages/openexr170-libs/)

[Steam for Linux issue #2721](https://github.com/ValveSoftware/steam-for-linux/issues/2721)

#### Segfaults during program start on 64-bit systems

The game segfaults during program start because of the `LD_LIBRARY_PATH` setting in the launcher script. Edit `*GAME*/Polynomial64`, and comment out the `LD_LIBRARY_PATH` variable. Make sure to put the `./bin/Polynomial64 "$@"` command on a new line.

### Portal 2

#### Game does not start

Several OpenGL-related errors (such as `PROBLEM: You appear to have OpenGL 1.4.0, but we need at least 2.0.0!` or `libGL error: driver pointer missing`) are caused by Portal 2 bundling an old libstdc++ file. This error is especially common with open source Radeon drivers (`radeonsi`).

A problem with libstdc can be fixed by running the game with `LD_PRELOAD='/usr/$LIB/libstdc++.so.6'`.

#### Resolution too low

When the game starts with a resolution so low that you cannot reach the game settings, run the game in windowed mode using the `-windowed` flag.

#### Missing non Latin font

The phenomenon is no menu in Portal. Portal and Portal2 use Helvetica, add the following lines to `~/.config/fontconfig/fonts.conf`:

```
<match target="pattern">
    <test qual="any" name="family">
        <string>Helvetica</string>
    </test>
    <edit name="family" mode="assign" binding="same">
        <string>Source Han Sans CN</string>
    </edit>
</match>

```

You can replace "Source Han Sans CN" by your favoriate and existing font.

### Prison Architect

#### ALSA error when using PulseAudio

The error:

`ALSA lib pcm_dmix.c:1018:(snd_pcm_dmix_open) unable to open slave`

was resolved by installing:

*   [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)

per [PulseAudio#ALSA](/index.php/PulseAudio#ALSA "PulseAudio").

### Project Zomboid

Requires [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk).

#### No sound

Prepend `/usr/lib` to `LD_LIBRARY_PATH`.

In the game, go to the options and set all audio to the proper volume.

### Pyre

#### Game does not start

Remove `*GAME*/lib64/libSDL2-2.0.so.0`.

If this doesn't work, downgrade sdl2.

```
$ pacman -U [https://archive.archlinux.org/packages/s/sdl2/sdl2-2.0.6-2-x86_64.pkg.tar.xz](https://archive.archlinux.org/packages/s/sdl2/sdl2-2.0.6-2-x86_64.pkg.tar.xz)

```

Then add sdl2 to IgnorePkg in `/etc/pacman.conf`.

`IgnorePkg = sdl2`

### Redshirt

Requires [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) if you use PulseAudio.

### Revenge of the Titans

Requires [libxtst](https://www.archlinux.org/packages/?name=libxtst) and [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst).

### Risk of Rain

Requires [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat). Then symlink it with this command :

```
$ ln -s /usr/lib32/libcurl.so.3 *GAME*/lib/libcurl.so.4

```

### Rock Boshers DX: Directors Cut

Requires [lib32-libcaca](https://www.archlinux.org/packages/?name=lib32-libcaca).

### Saints Row IV

#### Game fails to launch after update to new Nvidia drivers

Run the game with `/usr/lib32/libGLX_nvidia.so` appended to the `LD_PRELOAD`.

#### Game causes GPU lockup with mesa drivers

Saints Rows IV can cause a GPU lockup when trying to play on certain AMD hardware using open source drivers: [Bug 93475](https://bugs.freedesktop.org/show_bug.cgi?id=93475).

A workaround is to run the game with `R600_DEBUG=nosb`.

### Serious Sam 3: BFE

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

### Slay the Spire

If the game does not start or crashes at startup, install [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

### Songbringer

#### Launch error with Wayland

Install [glfw-x11](https://www.archlinux.org/packages/?name=glfw-x11) and run the game with `LD_PRELOAD=/usr/lib/libglfw.so.3`.

### Space Pirates and Zombies

Requires [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

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

### Spacechem

Dependencies:

*   [lib32-sdl_mixer](https://www.archlinux.org/packages/?name=lib32-sdl_mixer)
*   [lib32-sdl_image](https://www.archlinux.org/packages/?name=lib32-sdl_image)
*   [lib32-sqlite](https://www.archlinux.org/packages/?name=lib32-sqlite)

#### Game crash

The shipped x86 version of Spacechem does not work on x64 with the game's own libSDL* files, and crashes with some strange output.

To solve this just remove the three files `libSDL-1.2.so.0`, `libSDL_image-1.2.so.0`, `libSDL_mixer-1.2.so.0` from the game directory.

### Splice

Requires [glu](https://www.archlinux.org/packages/?name=glu).

### The Stanley Parable

#### Game won't start

As discussed in the Steam store page, remove `bin/libstdc++.so.6` from the game folder.

### Shadow Tactics: Blades of the Shogun

Dependencies:

*   [lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5)
*   [lib32-libxcursor](https://www.archlinux.org/packages/?name=lib32-libxcursor)
*   [lib32-libxrandr](https://www.archlinux.org/packages/?name=lib32-libxrandr)

### Steel Storm: Burning Retribution

#### Start with black screen

The game by default tries to launch in fullscreen mode with a resolution of 1024x768, which doesn't work on some devices (for example the Samsung Series9 laptop with Intel hd4000 video).

Run the game in windowed mode by using the `-window` flag. Then change the resolution in-game.

### Stellaris

#### No window opening, only sound

Happens with some AMD GPU and mesa combination, set multi_sampling=0 in ~/.local/share/Paradox\ Interactive/Stellaris/settings.txt.

### Stephen's Sausage Roll

#### No sound

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

If everything works up to this point, prepend `noload/` to your `LD_LIBRARY_PATH`.

Again, this should work because Steam checks for a `noload/` directory relative to the game's directory. The dynamic linker should respect the `$LD_LIBRARY_PATH` variable and fail to load the necessary [libpulse](https://www.archlinux.org/packages/?name=libpulse) files. The game should then fallback to plain ALSA.

### Superbrothers: Sword & Sworcery EP

Dependencies:

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) if you use PulseAudio

The game bundles an outdated version of libstdc++ which prevents the game from starting. [[10]](http://steamcommunity.com/app/204060/discussions/0/364039785161291413) The following can be observed when you run Steam and S&S from the terminal:

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

To solve this problem remove `*GAME*/lib/libstdc++.so.6*`. After that the game will use the libstdc++ from Steam.

### System Shock 2

You get these errors when running it with the native client:

```
C:\windows\system32\winedevice.exe: symbol lookup error: /usr/lib32/libX11.so.6: undefined symbol: xcb_wait_for_reply64
C:\windows\system32\wineboot.exe: symbol lookup error: /usr/lib32/libX11.so.6: undefined symbol: xcb_wait_for_reply64

```

Just delete or rename the libxcb library it got shipped with:

```
mv /mnt/olhdd/steam/steamapps/common/SS2/lib/libxcb.so.1{,.old}
mv /mnt/olhdd/steam/steamapps/common/SS2/lib/libxcb.so.1.1.0{,.old}

```

### Tabletop Simulator

#### CJK characters not showing in game

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite).

### Team Fortress 2

Requires [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12).

#### HRTF setup

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

#### Loading screen freeze

If you are a non-English (speaking) user, you have to enable "en_US.UTF-8" in the locale.gen! Generate a new locale after that.

#### No audio

It happens if there is no PulseAudio in your system. If you want to use [ALSA](/index.php/ALSA "ALSA"), you need to launch Steam or the game directly with `SDL_AUDIODRIVER=alsa` (From [SteamCommunity](http://steamcommunity.com/app/221410/discussions/0/882966056462819091/#c882966056470753683)).

If it still does not work, you may also need to set the environment variable AUDIODEV. For instance `AUDIODEV=Live`. Use `aplay -l` to list the available sound cards.

#### Slow loading textures

If you are using Chris' FPS Configs or any other FPS config, you may have set `mat_picmip` to `2`. This spawns multiple threads for texture loading, which may cause more jittering and lag on Linux, especially on alternative kernels. Try setting it to `-1`, the default.

### Terraria

See the KNOWN ISSUES & WORKAROUNDS​ section of the [release announcement](http://forums.terraria.org/index.php?threads/terraria-1-3-0-8-can-mac-linux-come-out-play.30287/).

### This War of Mine

#### Game does not start

This happens because of an incompatibility with the newer version of `lib32-curl`. To fix the problem , set your [launch options](/index.php/Launch_option "Launch option") to:

```
 LD_PRELOAD=./libcurl.so.4 %command%

```

#### Sound glitches with Steam native

The bundled `libOpenAL` might not work correctly, try symlinking `/usr/lib32/libopenal.so` to `*GAME*/libOpenAL.so`.

### Ticket to Ride

Dependencies:

*   [lib32-gstreamer0.10-base](https://aur.archlinux.org/packages/lib32-gstreamer0.10-base/)
*   [lib32-pangox-compat](https://aur.archlinux.org/packages/lib32-pangox-compat/)

As lib32-gstreamer0.10-base is quite hard to build you can use [alucryd-multilib](/index.php/Unofficial_user_repositories#alucryd-multilib "Unofficial user repositories") repo for this package

### The Tiny Bang Story

#### Missing libGLEW.so.1.6

```
# ln -s /usr/lib32/libGLEW.so.1.10.0 /usr/lib32/libGLEW.so.1.6

```

### Tomb Raider

#### Game immediately closes when running with steam-native

Tomb Raider has a very heavy amount of dependency on the Steam runtime, the easiest solution is to just run it using the runtime.

#### Steam Controller not working in-game

If your Steam Controller is correctly recognized and paired but still not working in-game try the following:

*   In Steam, non Big Screen, go to *Settings > Account > Beta participation > Change...* and in the dropdown select box select Steam Beta Update
*   Restart Steam
*   Go to Big Screen and start Tomb Raider

Correctly recognized means you can control the desktop mouse and Steam in Big Picture mode and the controller is shown in the Big Picture settings.

### Torchlight 2

#### Libfreetype/libfontconfig Incompatibility

If you are experiencing issues with launching Torchlight 2, it could be due to using a newer libfontconfig than the game currently supports.

Right click the game in Steam, and set the following as it's launch option:

```
LD_PRELOAD=/usr/lib/libfreetype.so.6 %command%

```

then attempt launching the game.

Alternately, re-naming or deleting these 2 files will force it to use your system's libraries:

```
Torchlight 2/game/lib/libfreetype.so.6
Torchlight 2/game/lib64/libfreetype.so.6

```

#### Locale incompatibility

Some users report that Torchlight 2 does not work if you do not have en_US.UTF8 in your locale.

Double check you have generated the locale needed in [Steam Installation Requirements](/index.php/Steam#Installation "Steam").

### Tower Unite

#### Graphical Glitches

This is a known issue, and it occurs because the shaders had not been ported to Linux yet by the developers. To minimize glitches and make the game playable add `-opengl4` to your [launch options](/index.php/Launch_option "Launch option"), set Ocean Quality to "Potato" and Effects Quality to "Low" in the game settings.

### Towns / Towns Demo

Requires [Java](/index.php/Java "Java").

### Transistor

#### Crash on launch / FMOD binding crash / audio issues

Run the game with:

```
LD_PRELOAD='/usr/lib/libstdc++.so.6:/usr/lib/libgcc_s.so.1:/usr/lib/libxcb.so.1:/usr/lib/libasound.so.2'

```

Otherwise, run the game via shell and set up proper audio device for FMOD, as discussed in [[11]](https://steamcommunity.com/app/237930/discussions/2/620695877176333955/).

Also, check out this thread [[12]](https://steamcommunity.com/app/237930/discussions/2/492378265893557247/).

### Transmissions: Element 120

Dependencies:

*   [lib32-libgcrypt15](https://www.archlinux.org/packages/?name=lib32-libgcrypt15)
*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)

#### Troubleshooting

Make sure you have all libraries installed. Above the standard set required by Steam runtime, the game requires few additional ones. The typical error message that indicates that is

```
AppFramework : Unable to load module vguimatsurface.so!

```

To find missing dependencies go into the game directory and run:

```
LD_LIBRARY_PATH=bin ldd bin/vguimatsurface.so

```

Look for entries that say *not found*.

### Trine 2

Dependencies:

*   [lib32-glu](https://www.archlinux.org/packages/?name=lib32-glu)
*   [lib32-libxxf86vm](https://www.archlinux.org/packages/?name=lib32-libxxf86vm)
*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [xorg-xwininfo](https://www.archlinux.org/packages/?name=xorg-xwininfo)
*   [lib32-libdrm](https://www.archlinux.org/packages/?name=lib32-libdrm)

*   [lib32-libpng12](https://www.archlinux.org/packages/?name=lib32-libpng12)
*   [lib32-libwrap](https://www.archlinux.org/packages/?name=lib32-libwrap)

#### Colors

If colors are wrong with FOSS drivers (r600g at least), try to run the game in windowed mode, rendering will be corrected. ([bug report](https://bugs.freedesktop.org/show_bug.cgi?id=60553))

#### Sound

If sound plays choppy, try:

 `/etc/openal/alsoft.conf` 
```
drivers=pulse,alsa
frequency=48000

```

#### Resolution

If the game resolution is wrong when using a dual monitor setup and you can't see the whole window edit `~/.frozenbyte/Trine2/options.txt` and change the options `ForceFullscreenWidth` and `ForceFullscreenHeight` to the resolution of your monitor on which you want to play the game.

### Tropico 5

#### Blank screen with sound only on startup

Run the game with `MESA_GL_VERSION_OVERRIDE=4.0 MESA_GLSL_VERSION_OVERRIDE=400`.

### Unity of Command

Requires [lib32-pango](https://www.archlinux.org/packages/?name=lib32-pango).

#### Squares

If squares are shown instead of text, try removing `*GAME*/bin/libpangoft2-1.0.so.0`.

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

### Unity3D

Games based on the Unity3D engine, like *War For The Overworld* or *Pixel Piracy* may need the package [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) to understand that they run on Linux and work properly.

#### Locale settings

Games made in C# often have a problem with some locales (e.g. Russian, German) because developers don't specify locale-agnostic number formatting. This can result in some game screens loading only partially, problems with online features or other bugs.

To work around this, run the game with `LC_ALL=C`.

Affected games: *FORCED, Gone Home, Ichi, Nimble Quest, Syder Arcade*.

#### Unity 5 sound problems

The sound system in Unity 5 changed and to be able to play games created with it you must most likely install and run [PulseAudio](/index.php/PulseAudio "PulseAudio").

Another solution is to disable the Steam runtime: in the launch options for the game, write this: `LD_LIBRARY_PATH="" %command%`

Another solution is to prevent Unity from trying to use pulseaudio using [pulsenomore](https://aur.archlinux.org/packages/pulsenomore/) package from the [AUR](/index.php/AUR "AUR"). Once it is installed, use the following as launch options :`/usr/bin/pulsenomore %command%`

Affected games: *Kerbal Space Program, SUPERHOT, ClusterTruck*

#### Game launching on wrong monitor in fullscreen mode

Unity games that do not support monitor selection will most likely launch the game on a wrong monitor.

The problem is that Unity games write the default parameter `<pref name="UnitySelectMonitor" type="int">-1</pref>` to the game config file.

This will lead to the game launching on a non-primary monitor.

When changing to value into `<pref name="UnitySelectMonitor" type="int">**0**</pref>` for the according game, the game will start on the correct (primary) monitor.

A Unity game config file usually resides in `~/.config/unity3d/*CompanyName*/*ProductName*/prefs`.

Affected games: *Cities: Skylines, Tabletop Simulator, Assault Android Cactus, Wasteland 2, Tyranny, Beat Cop*.

Be aware that some games do not support setting that parameter, it will simply be ignored. This is the case for *Pillars of Eternity*, *Kentucky Route Zero*, *Sunless Sea*.

#### Chinese/Japanese/Korean display bug

Install [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) and [wqy-microhei-lite](https://www.archlinux.org/packages/?name=wqy-microhei-lite). Then

```
#fc-cache -fv

```

#### Game does not respond

Add the following line to your [launch options](/index.php/Launch_option "Launch option") :

```
SDL_DYNAMIC_API=/usr/lib/libSDL2-2.0.so %command%

```

### Unrest

Requires [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth).

### Volgarr the Viking

Delete the `lib` directory in the game directory to get rid of the libGL errors.

### War Thunder

#### No audio

If there is no audio after launching the game, install [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

#### Blank screen

If having a green or blank screen on startup, run the game with `MESA_GL_VERSION_OVERRIDE=4.1COMPAT`. [[13]](https://forum.warthunder.com/index.php?/topic/267809-linux-potential-workaround-for-mesa-drivers-black-screen/) [[14]](http://forum.warthunder.com/index.php?search_term=0030709&app=core&module=search&do=search&fromMainBar=1&search_app=forums%3Aforum%3A920&sort_field=&sort_order=&search_in=posts)

### Warhammer 40,000: Dawn of War II

Dependencies:

*   [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib)
*   [librtmp0](https://www.archlinux.org/packages/?name=librtmp0)

The start script does not point to the right direction of `libasound.so.2`.

To fix it open `*GAME*/DawnOfWar2.sh` and replace the following lines:

```
HAS_LSB_RELEASE=$(command -v lsb_release)
if [ -n "${HAS_LSB_RELEASE}" ] && [ "$(lsb_release -c | cut -f2)" = "trusty" ]; then
	LD_PRELOAD_ADDITIONS="/usr/lib/x86_64-linux-gnu/libasound.so.2:${LD_PRELOAD_ADDITIONS}"
fi 
```

with:

 `LD_PRELOAD_ADDITIONS="/usr/lib64/libasound.so.2:${LD_PRELOAD_ADDITIONS}"` 

### We Were Here

#### Stuck on black screen or logo on launch

Add `-screen-fullscreen 0` to launch options. [[15]](https://steamcommunity.com/app/582500/discussions/1/1470840994974091613/)

### Worms W.M.D

The game includes several workarounds in the `Run.sh` script, however these may not work and it is easy to get the game running without this script.

First, try running the game directly from its game directory using `Worms W.M.Dx64`. If you get a "No such file or directory" error about libcurl-gnutls, install [libcurl-gnutls](https://www.archlinux.org/packages/?name=libcurl-gnutls). If the game crashes after playing the intro movies, add the Steam Runtime dbus libraries to the game's library directory:

```
$ ln -s ~/.steam/steam/ubuntu12_32/steam-runtime/amd64/lib/x86_64-linux-gnu/*dbus* ~/.steam/steam/steamapps/common/WormsWMD/lib

```

Now the game should run using the default "Play Worms W.M.D" option. See also Steam community discussions [[16]](https://steamcommunity.com/app/327030/discussions/2/133257959065155871/) and [[17]](https://steamcommunity.com/app/327030/discussions/1/343785380902286766/).

On some systems there are terrain bugs where holes in terrain are not rendered properly and worms can fall through terrain unexpectedly. These bugs can make the game unplayable in many situations and there is no known fix for them.

### Witcher 2: Assassin of Kings

Dependencies:

*   [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls)
*   [lib32-libcurl-compat](https://www.archlinux.org/packages/?name=lib32-libcurl-compat)
*   [lib32-libcurl-gnutls](https://www.archlinux.org/packages/?name=lib32-libcurl-gnutls)
*   [lib32-sdl2_image](https://www.archlinux.org/packages/?name=lib32-sdl2_image)
*   [lib32-sdl2](https://www.archlinux.org/packages/?name=lib32-sdl2)

#### Game does not start

If the game does not run, enable error messages:

```
$ LIBGL_DEBUG=verbose ./witcher2

```

### Wizardry 6: Bane of the Cosmic Forge

Requires [DOSBox](/index.php/DOSBox "DOSBox").

To fix the crash at start, open `*GAME*/dosbox_linux/launch_wizardry6.sh` and:

1.  comment the line `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./libs`
2.  change the beginning of the line starting with `exec ./dosbox` to `exec dosbox`

### World of Goo

#### Changing resolution

To change the game resolution edit the *Graphics display* section in `*GAME*/properties/config.txt`. For example:

```
<!-- Graphics display -->
<param name="screen_width" value="1680" />
<param name="screen_height" value="1050" />
<param name="color_depth" value="0" />
<param name="fullscreen" value="true" />
<param name="ui_inset" value="10" />

```

### X3: Terran Conflict

#### Game crashes on startup

The game may crash on startup because it's linked to libz version 1.2.9, while the latest version of this library in Arch Linux is higher. The following message in the terminals appears in this case:

```
./X3TC_config: lib/libz.so.1: version 'ZLIB_1.2.9' not found (required by /usr/lib32/libpng16.so.16

```

Running the game with `LD_PRELOAD='/usr/lib32/libz.so.1.2.11'` may help.

### XCOM

Dependencies:

*   [librtmp0](https://www.archlinux.org/packages/?name=librtmp0)
*   [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image) (required to enable keyboard functionality in-game)

#### Hangs on startup

If you are running a [hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics") system, try:

```
__GL_THREADED_OPTIMIZATIONS=0 primusrun %command%

```

#### Graphical glitches on Intel HD

XCOM: Enemy Unknown may not recognize the SDL2 shared libraries shipped with the Steam runtime. Check if the binary finds all required files and install missing packages if necessary ([sdl2](https://www.archlinux.org/packages/?name=sdl2) and [sdl2_image](https://www.archlinux.org/packages/?name=sdl2_image)).

 `ldd binaries/linux/game.x86_64 `