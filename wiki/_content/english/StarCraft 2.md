[StarCraft II](http://eu.battle.net/sc2/en/) is a real-time strategy game from Blizzard Entertainment released in 2010\. A native Linux version isn't available, but the game is fully playable using [Wine](/index.php/Wine "Wine").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Packages](#Packages)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Installing with the Blizzard App (former Battle.net App)](#Installing_with_the_Blizzard_App_.28former_Battle.net_App.29)
    *   [1.4 Installing from DVD](#Installing_from_DVD)
    *   [1.5 Playing StarCraft II](#Playing_StarCraft_II)
*   [2 Hints for Performance Tuning](#Hints_for_Performance_Tuning)
    *   [2.1 Unit Preloader](#Unit_Preloader)
*   [3 Hints for advanced hotkeys settings](#Hints_for_advanced_hotkeys_settings)
    *   [3.1 Preliminary](#Preliminary)
    *   [3.2 Rapid Fire Hotkey throughput](#Rapid_Fire_Hotkey_throughput)
    *   [3.3 Enable double-key Rapid Fire Hotkey behaviour](#Enable_double-key_Rapid_Fire_Hotkey_behaviour)
    *   [3.4 Enable CapsLock as a Rapid Fire Hotkey with xmodmap](#Enable_CapsLock_as_a_Rapid_Fire_Hotkey_with_xmodmap)
    *   [3.5 Use temporary XKB options](#Use_temporary_XKB_options)
    *   [3.6 Enable Scrollclick](#Enable_Scrollclick)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

#### Packages

You need to [install](/index.php/Install "Install") [wine](https://www.archlinux.org/packages/?name=wine), [lib32-libjpeg-turbo](https://www.archlinux.org/packages/?name=lib32-libjpeg-turbo), [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng), [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls) and [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap). If you are using [PulseAudio](/index.php/PulseAudio "PulseAudio"), install [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) available in [multilib](/index.php/Multilib "Multilib"). Optionally, instead of regular [wine](https://www.archlinux.org/packages/?name=wine), you might prefer [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) - [enabling CSMT via the Staging tab in winecfg](/index.php/Wine#CSMT_patch "Wine") may greatly improve performance, but is not required. You'll also need to use [winetricks](https://www.archlinux.org/packages/?name=winetricks) and install the following components (to use the Map Editor and avoid crashes on certain system configurations):

```
$ winetricks corefonts vcrun2005 vcrun2008 vcrun2015

```

#### Configuration

If you have a GPU which doesn't properly report the amount of memory available (older integrated or early AMD APUs), you'll need to tell Wine how much VRAM you have available. Open the Registry Editor:

```
$ regedit

```

Go to *HKEY_CURRENT_USER/Software/Wine/Direct3D* (right-click on Wine and New -> Key, *Direct3D*, Enter, if it doesn't exist) right-click on *Direct3D* (if such a key doesn't exist, right-click on *Wine*, New -> Key, *Direct3D*, OK), select New -> String Value, *VideoMemorySize*, which you should set to the amount of VRAM your GPU has, in MB (for example, "1024" or "2048"). If you're using an integrated GPU, try to preallocate a fair amount of RAM for your GPU in BIOS/UEFI Setup and use the same value here (512 is good enough for low-medium settings).

*   If the Battle.net App doesn't work, use a new Wine prefix.
*   **If you are asked to install Gecko, then click Install to do so.**
*   If the Battle.net App window is white, open *winecfg*, go to *Applications* and set *Windows Version* to "Windows XP". You may do so for Battle.net.exe only, as SC2 itself works fine with this being set to anything newer.

#### Installing with the Blizzard App (former Battle.net App)

Recent SC2 versions require the [Blizzard App](http://eu.battle.net/en/app/) to be installed, as it replaced the launchers for all Blizzard games. Furthermore, recent patches massively changed the file structure in their newer games - if you have a fast enough internet connection, it might be faster to download a new copy from the Blizzard App than trying to install the game from DVD. Simply install the app, select your region, log in with a Blizzard Account, then select StarCraft II on the left and click Install. You'll be able to select your game language and installation location. (Installing the game on a native Linux filesystem instead of NTFS might improve loading times.)

**Note:** You need to install [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls) in order to use the online-mode of the [Blizzard App](/index.php/Blizzard_App "Blizzard App").

#### Installing from DVD

**Note:** If you have a reasonable internet connection (10Mbps or better), redownload the game. Recent patches were massive and you'll literally spend more time waiting for the game to reconfigure and patch than just redownloading the whole game again. Furthermore, you can stream the game while playing.

*   Mount DVD/DVD Image, (unhide invisible data), for example:

```
$ mount -o ro,unhide,uid=1000 /dev/dvd /media/dvd (for the DVD)
$ mount -o loop,ro,unhide,uid=*your_id* *starcraft.iso* /media/dvd (for an image) 

```

*   Start the installer:

```
$ wine start /unix /media/dvd/Installer.exe

```

#### Playing StarCraft II

Launch the game from the Battle.net App. If the game crashes see troubleshooting section.

## Hints for Performance Tuning

*   `Ctrl+Alt+F` shows FPS.
*   Make sure that you are using the latest available graphics drivers. Nvidia drivers should be 256.35 or later (drivers in repositories are up to date).
*   Edit the variables.txt in your My Documents/Starcraft II/ following the guide [here](http://www.teamliquid.net/forum/viewmessage.php?topic_id=142046).
*   If you're using Intel HD Graphics 3000, you may have to set the VideoMemorySize to 128 (see the Configuration above). The game will complain about not enough VRAM otherwise.
*   If you have problems updating the game and see the following in the output:

```
Agent started on port #6882
Executing operation: disable_firewall applicationPath="C:\users\Public\Application Data\Battle.net\Agent\Agent.4432\Agent.exe" applicationName="Battle.net Update Agent"
AgentAsAdmin failed to add a firewall exception for 'C:\users\Public\Application Data\Battle.net\Agent\Agent.4432\Agent.exe'.
Registered Event: "shutdown event"
Registered Event: "database flush event"
PostTo succeeded status: 0 for url: http://enGB.patch.battle.net:1119/patch
Post Data:
<version program="Agnt"><record program="Bnet" component="Win" version="1" /><record program="Agnt" component="cdn" version="1" /><record program="Agnt" component="cfg" version="1" /><record program="Agnt" component="Win" version="1199" /></version>
DownloadTo failed error: 0 of article:  from:

DownloadTo failed error: 0 of article:  from:

DownloadTo failed error: 0 of article:  from:
```

Launch Agent.exe --nohttpauth:

```
$ killall Agent.exe && wine ~/.wine/drive_c/users/Public/AppData/Battle.net/Agent/Agent.exe --nohttpauth

```

You can now restart the Battle.net App. The updater should proceed smoothly.

#### Unit Preloader

SC2 never fully loads the game initially, but rather streams and loads required files on demand. Unit Preloader is a special map which forces SC2 to load **all** units, animations and effects, **causing high RAM usage**, but prevents loading the data (and massive framerate drops) during multiplayer matches. Open *Arcade* and search for *Unit Preloader*. There are 3 versions - start the one which corresponds to the game edition you'll want to play in multiplayer and wait for the Victory screen. All data will be preloaded until you exit the game to desktop.

## Hints for advanced hotkeys settings

#### Preliminary

Have a look at projects aiming at creating more ergonomic hotkeys for SCII:

*   [TheCore](http://www.teamliquid.net/forum/sc2-strategy/341878-thecore-advanced-keyboard-layout)
*   [TheCore Lite](https://github.com/bobo38/TheCoreLite)

Some other unmaintained options:

*   [Fleet Keys](http://www.teamliquid.net/forum/sc2-strategy/404476-fleet-keys-refined-hotkey-systems).
*   [DarkGrid](http://www.teamliquid.net/forum/sc2-strategy/257590-darkgrid-layout)

[Rapid Fire](http://www.teamliquid.net/forum/sc2-strategy/446530-rapid-fire-hotkey-trick) Hotkeys are implemented in those hotkeys settings.

#### Rapid Fire Hotkey throughput

[Xorg](/index.php/Xorg "Xorg") keyboard autorepeat can be modified. It may make sense to reduce delay before autorepeat starts (default=660 [ms]). Increasing a bit the repeat rate (default=25 [/s]) is a trade-off: speed vs accuracy.

To apply the settings:

```
$ xset r rate <delay_to_activate_in_ms> <nb_of_repeats_per_second>

```

**Tip:** `xset r rate` get X back to default autorepeat settings

**Tip:** `xset q` let you know the current X settings

#### Enable double-key Rapid Fire Hotkey behaviour

Fancy double-key Rapid Fire Trick are not possible by default for Linux. The [xkb_repeat](https://git.framasoft.org/bobo/xkb_repeat/tree/master) git project may help you unlock this behaviour, providing patches to recompile your X server.

**Warning:** This double key repeat usage for RapidFire inject is no longer possible since LoTV release

#### Enable CapsLock as a Rapid Fire Hotkey with xmodmap

TheCore and TheCore Lite hotkeys rely on CapsLock to be a rapid fire hotkey. This does not work by default under Linux. To make it work, CapsLock key could be remapped to another key with [xmodmap](/index.php/Xmodmap "Xmodmap"). Hereafter an example with "Backspace" character.

```
$ xmodmap -e "remove Lock = Caps_Lock" -e "keycode 66 = BackSpace"

```

The .SC2Hotkeys file would need to be modified, to take it into account to add "Backspace" as an alternate wherever CapsLock is used. You may consider tune your .SC2Hotkeys file with one of those command lines:

```
$ sed -i -e "s:CapsLock:Backspace:" <file>.SC2Hotkeys                         # replacement of CapsLock by BackSpace
$ sed -i -e "s:CapsLock:CapsLock,Backspace:" <file>.SC2Hotkeys                # easy command copy
$ sed -i -e "s:\([=,]\([=,]\)*CapsLock\):\1,\2Backspace:" <file>.SC2Hotkeys   # this one copies any modifier with CapsLock to equivalent with BackSpace

```

**Tip:** `xmodmap -e "add Lock = Caps_Lock" -e "keycode 66 = Caps_Lock"` to get back to default CapsLock behavior, once you exit the game

#### Use temporary XKB options

This tip could be used to perform some modifications:

*   map CapsLock to Backspace with `caps:backspace`
*   swap left Control and Alt keys with `ctrl:swap_lalt_lctl`

```
$ setxkbmap -option -option "$(localectl | grep Options | sed -e 's/.*Options:\s*//'),ctrl:swap_lalt_lctl,caps:backspace"

```

**Tip:** All possible options could be found looking in /usr/share/X11/xkb/rules/base.lst

**Tip:** to get back to the default XKB options, once you exit the game you can use the following code in a script

```
setxkbmap -option -option "$(localectl | grep Options | sed -e 's/.*Options:\s*//')"

```

#### Enable Scrollclick

Some scrollclick demo videos:

*   [infestor spawning infested terran](https://www.youtube.com/watch?v=7pQKnS1CPEQ)
*   [scrollclick applied to protoss](https://www.youtube.com/watch?v=9aPd8_9_vB4)

Using [Xmodmap](/index.php/Xmodmap#Reverse_scrolling "Xmodmap"), it possible to set your regular 3-buttons mouse with scroll wheel to practice scrollclick. First change scroll fonction to "forward mouse button" and "back mouse button":

```
$ xmodmap -e "pointer = 1 2 3 8 9 6 7 4 5"

```

Then add alternate key SCII hotkeys for:

*   Global=>Unit Management=>Choose Ability or AI target
*   Global=>Unit Management=>Smart Command

**Tip:** `xmodmap -e "pointer = default"` resets to default mouse functionality

**Warning:** scrollclick applications previously demoed could be better executed with RapidFire Key method

**Tip:** you may consider using this tip to use wheel for previous/next subgroup browsing

**Tip:** for more 5+ button, you may consider use `evrouter` to apply the same tip and map buttons to other usages

## Troubleshooting

*   You may want to start the game without the launcher: `cd ~/.wine/drive_c/Program\ Files/StarCraft\ II\Support` (or `Support64` for the 64-bit version) and `wine SC2Switcher.exe` - this might make debugging easier, but you may have to select your region in-game. Furthermore, if your game is not up-to-date, you'll be unable to log in, and no error message will be shown - simply start the Battle.net Launcher and let the game update completely.
*   If SC2 instacrashes, or crashes upon game start, try clicking on the Battle.net logo in the Launcher -> Settings -> Game Settings -> Check `Launch 32-bit client (instead of 64-bit)`, or **uncheck** it if it's already checked.
*   For some, in-game resolution changing does not work. Editing 'width=x' and 'height=y' in Variables.txt in My Documents/Starcraft II solves this issue. Replace x and y with the prefered resolution.
*   Should you experience graphics problems (no 3D background in menu, blue non-texturized units and other glitches), launch the game without Battle.net App (see above) like this: `force_s3tc_enable=true wine SC2Switcher.exe`. You can also add this option to the .desktop entry in ~/.local/share/applications/wine/Programs/StarCraft II, or edit your `~/.drirc` file to enable this setting permanently for all apps. Using [driconf](https://www.archlinux.org/packages/?name=driconf), you may just enable this setting with a simple GUI.

## See also

*   [StarCraft II](https://appdb.winehq.org/objectManager.php?sClass=application&iId=11123) (WineHQ AppDB)
*   [StarCraft II crashes because of ACCESS_VIOLATION before the loading screen](http://bugs.winehq.org/show_bug.cgi?id=23806) (WineHQ bug tracking database)
*   [World of Warcraft crashes upon login after 3.3.5 patch.](http://bugs.winehq.org/show_bug.cgi?id=23323) (WineHQ bug tracking database)
*   [starcraft2 crashing on loading](https://bbs.archlinux.org/viewtopic.php?id=101822) (Arch Linux forums)
*   [starcraft2 fails to update to patch 1.03](https://bbs.archlinux.org/viewtopic.php?id=103354) (Arch Linux forums)
*   [Patch News](http://eu.battle.net/sc2/en/forum/topic/283440977) (battle.net EU forums)