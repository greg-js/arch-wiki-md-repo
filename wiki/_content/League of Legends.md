# League of Legends

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Style problems, little overview - see [Help:Style](/index.php/Help:Style "Help:Style") (Discuss in [Talk:League of Legends#](https://wiki.archlinux.org/index.php/Talk:League_of_Legends))

There is currently only a Mac OS and a Windows version of LoL. This page outlines working methods to get the Windows League of Legends version working on your arch system through Wine.

**This guide was last tested with:**

_Arch Linux Kernel:_ **4.2.3-1-ARCH**

_Wine Version:_ **1.7.53**

_LoL Version:_ **5.20**

**Issues:**

*   Icons for runes in the launcher store do not appear
*   Right clicking friends in the friend list (to invite to a game) does not work (this issue can be circumvented by using the invite button in the lobby)
    *   [Another workaround](https://bugs.winehq.org/show_bug.cgi?id=35701#c5) to this issue is to mouse over your friend, press down right mouse button, press down left mouse button, release left mouse button, and then release right mouse button.
*   Lesser performance than running the game on windows
*   In a 64-bit Wine prefix the Patcher will be black (but pressing buttons will work) and launching a match will end up in a black screen.
*   The installer hangs when it should start the installation
*   The Basic Tutorial does not work.

## Contents

*   [1 PlayonLinux Method](#PlayonLinux_Method)
    *   [1.1 Troubleshooting](#Troubleshooting)
*   [2 Wine Method](#Wine_Method)
    *   [2.1 Create a 32-bit Wine PREFIX](#Create_a_32-bit_Wine_PREFIX)
    *   [2.2 Install the dependencies](#Install_the_dependencies)
    *   [2.3 Installation](#Installation)
        *   [2.3.1 Get your hands on an installed copy of the game](#Get_your_hands_on_an_installed_copy_of_the_game)
        *   [2.3.2 Compatibility Steps](#Compatibility_Steps)
    *   [2.4 Run the Game](#Run_the_Game)
*   [3 Troubleshooting/Tips](#Troubleshooting.2FTips)
    *   [3.1 For d3dstream patched Wine](#For_d3dstream_patched_Wine)
    *   [3.2 In-game shop crash](#In-game_shop_crash)
    *   [3.3 Connection Error: connection failure unable to connect to the pvp.net server](#Connection_Error:_connection_failure_unable_to_connect_to_the_pvp.net_server)
    *   [3.4 Hang after champ select with AMD proprietary fglrx driver](#Hang_after_champ_select_with_AMD_proprietary_fglrx_driver)

## PlayonLinux Method

This is the easiest method. Just install [playonlinux](https://www.archlinux.org/packages/?name=playonlinux).

After installation run from the command line

```
$ playonlinux

```

When you first run it, playonlinux will install some necessary fonts. Afterwards, click Install, check the "testing box" and then search for "League of Legends". The rest is self-explanatory.

### Troubleshooting

*   **Bugsplat opening patcher:** To fix this you need to configure the PlayOnLinux's wine version by clicking the configure gear, change wine version to system from 1.7-LeagueOfLegends and if you have not done so already install [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap).

*   **Adobe air missing:** To fix this you need to install [lib32-lcms2](https://www.archlinux.org/packages/?name=lib32-lcms2).

*   **The login server did not respond:**

PlayOnLinux seem to be missing a symlink from the generic version of [libgcrypt](https://www.archlinux.org/packages/?name=libgcrypt) to the specific version it ships. That can be fixed by finding the folders of the affected Wine versions and creating the links manually. Replace ARCH with either x86 or amd64, and VERSION with the Wine version you intend to fix.

```
$ cd ~/.PlayOnLinux/wine/linux-ARCH/VERSION/lib
$ ln -s libgcrypt.so.11.* libgcrypt.so.11
$ ln -s libgcrypt.so.11 libgcrypt.so

```

If you are still unable to login after setting up the above symlinks, [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls) may need to be manually installed or re-installed.

*   **No sounds:** install [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib) (for pulseaudio users: [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) and [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse))

*   **Store (for runes) is all black:** [install IE8](http://forums.eune.leagueoflegends.com/board/showthread.php?t=571456) in the PlayOnLinux components.

*   **Crash after champ select:** [install directx9](http://www.playonlinux.com/en/topic-11344-1.html) in the PlayOnLinux components.

## Wine Method

**Note:** The guide is written mostly for x86_64 systems, if your architecture is i686, you can skip setting up the new Wine Prefix (Just use the default wine prefix instead: .wine). You can also ignore WINEARCH/WINEPREFIX parts of commands· And to you, "lib32-lcms2" would just be "lcms2"

**Warning:** The installer does not currently seem to be working in Wine

### Create a 32-bit Wine PREFIX

**Tip:** There is an experimental higher d3d performance [patched version of wine](https://aur.archlinux.org/packages/wine-d3dstream-git/) available in AUR, the performance boost it offers requires adding a registry key with regedit in Wine. I see my framerate go from 160 to 240 with this feature enabled, that is a solid +50% increase in framerate. See more at the bottom of the page.

Install [wine](https://www.archlinux.org/packages/?name=wine) on your system and run:

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winecfg

```

to create a default 32-bit prefix at $HOME/.wine. If it asks to install something (like Wine Mono or Wine Gecko or some such) just always click install. After this make sure Windows Version is set to Windows XP.

### Install the dependencies

Install the required packages on your system:

*   [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib) (for pulseaudio users: [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) and [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse))
*   [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap)
*   [lib32-lcms2](https://www.archlinux.org/packages/?name=lib32-lcms2)
*   [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls)
*   [winetricks](https://www.archlinux.org/packages/?name=winetricks)

Install the following windows components using winetricks:

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winetricks d3dx9 vcrun2005 wininet corefonts adobeair ie8

```

If you run into problems installing adobeair, you need to make a little change in your Winecfg.

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winecfg

```

Access the libraries tab, find in the list of existing libraries (or add a new entry for it if it does not exist) **dnsapi**, click Edit... and configure it for "**Native then Builtin**"

### Installation

The installer is currently not working for me in Wine, but the command to execute it if you want to try would be the following:

```
# GC_DONT_GC=1 WINEARCH=win32 WINEPREFIX=$HOME/.wine32 wine /path/to/installer.exe

```

#### Get your hands on an installed copy of the game

There are several ways to do this, the Windows version (as long as it can run the Installer which probably requires Windows XP or newer) here are a few methods.

*   Get access to a physical Windows based machine, in your home or at your neighbors/friends place, bring a 8GB USB flash drive or external HDD with you and install the game on it. (If you do not have a 16GB flash drive you can use a smaller one and make a few round trips after installing the game on the HDD instead.)

*   Install a virtualization software (like Virtualbox or VMWare Player) and set up a Windows installation inside of it. Make sure it has a network connection, then install League of Legends on it, set up a shared folder between the VM and the host machine, and move the League of Legends installation into it, then from the Host system you can proceed to the next step and move the installation from the shared folder into your Wine Prefix.

*   If you already have a Dual-Boot setup, you can just install League of Legends onto the Windows installation, load the hard drive to Linux (requires [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g), may also require you to set the exec option in /etc/fstab for the drive) then proceed to the next step and symlink the folder from your Windows drive to your Wine Prefix.

*   See if the installer works with [playonlinux](https://www.archlinux.org/packages/?name=playonlinux). If it does then install it, move the folder from the playonlinux wineprefix to the wine32 prefix and uninstall playonlinux again (or keep it if you would like)

After you get your hands on the game, either move or symlink it to your wine32 prefix, using either of these commands (assuming you have a dual boot setup and your windows partition is mounted at /mnt/windows, or you have the game on a USB flash drive mounted at /media/removable):

```
# ln -s /mnt/windows/Riot\ Games/ $HOME/.wine32/drive_c/
# mv /media/removable/Riot\ Games/ $HOME/.wine32/drive_c/

```

#### Compatibility Steps

*   **Hostname** (Fixes the game failing to run after Champion Select screen)

First you will want to find your hostname.

```
# cat /etc/hostname

```

Then you will want to make sure your /etc/hosts file uses your hostname over localhost, you can do this by opening /etc/hosts with an editor of your choice.

```
# nano /etc/hosts

```

Then replace all mentions of localhost with the hostname you got from the first command (this change requires a system restart, without this your game will fail after champion select with a "Bad Window" error)

*   **Texture Patch** (Fixes in-game store crashing the game when it is opened)

You now need to patch away the mipmaps of the in-game shop icons. An alternative method is to patch [Wine itself](http://pastebin.com/xSNJjkMY).

A better method is edit the .../Config/Game.cfg and under the [General] section add "x3d_platform=1" along with the other options instead of patching either wine or the texture files. This works in wine 1.7.53.

Download

[LoL-Linux-Tools](https://github.com/A-Metaphysical-Drama/LoL-Linux-Tools/)

Extract the file to a location of your choosing, then edit config.py with an editor of your choice and set an absolute path.

```
lol_path = '/home/USERNAME/.wine32/drive_c/Riot Games/League of Legends/'

```

Then execute the patch with

```
# python2 lol_linux.py texture_patch

```

If all went well, you will see an output explaning what the patch is doing (unpacking a bunch of dds files from an archive, patching out the mipmaps in them, archiving them again, and then it will be done, this takes a few) And now your LoL client should finally be working!

**Warning:** If you use this Texture Patch rather than patching Wine itself for compatibility with the original store icons, you will need to apply the patch again every time the game is updated. This is because if Riot Games add new icons or change existing ones, they will not be compatible with Wine anymore.

You can create an alias in .bashrc to automate this process a bit.

```
alias lol-update='python2 $HOME/.lol_patch/lol_linux.py texture_patch'

```

The patch will only take long to finish the first time you run it, as it does not need to patch all of the files again, only the ones that are new or have changed.

### Run the Game

Create an alias to execute the 32-bit Wine installation (in ~/.bashrc) this is not really a required step, but just a good practice since you can use this to run other programs that play better with a 32-bit wine prefix than a 64-bit one.

```
# alias wine32='env WINEARCH=win32 WINEPREFIX="$HOME/.wine32" wine'

```

The above alias will work with winecfg, it will however not work with winetricks (to run winetricks you need to do it like done formerly in this guide)

Create a bash script or an alias with the following commands:

Bash script example: **/bin/leagueoflegends**

```
#!/bin/sh
pushd $HOME/.wine32/drive_c/Riot\ Games/League\ of\ Legends/RADS/system/
WINEARCH=win32 WINEPREFIX=$HOME/.wine32 wine rads_user_kernel.exe run lol_launcher $(ls ../projects/lol_launcher/releases/) LoLLauncher.exe
popd

```

Make sure to remember to make the file executable

```
# chmod +755 /bin/leagueoflegends

```

Alias example: **$HOME/.bashrc**

```
# alias League_of_Legends='popd $HOME/.wine32/drive_c/Riot\ Games/League\ of\ Legends/RADS/system/ && wine32 rads_user_kernel.exe run lol_launcher $(ls ../projects/lol_launcher/releases/) LoLLauncher.exe && pushd'

```

Shortcut example (if you made a bash script, this can be useful for example if you want to launch the game from steam): **/usr/share/applications/LeagueofLegends.desktop**

```
[Desktop Entry]
Name=League of Legends
Comment=Runs League of Legends through a 32-bit Wine installation.
Exec=/bin/leagueoflegends
Terminal=false
Type=Application
Icon=LoL_Icon.png
Categories=Wine;Game;

```

To be able to use an Icon for the application, you need to either convert the ***/RADS/system/lol.ico** to the png format (with imagemick or gimp), or download the icon separately and place it in the **~/.icons/** folder of your home directory. Here is a [48x48 icon](http://img.informer.com/icons/png/48/4719/4719180.png) you can download.

Run the bash script/alias/shortcut and you should be good to go!

To test if the game is working, create a custom Summoner's Rift match with one bot. If it loads and you do not crash upon opening the in-game store, you are golden! Congratulations!

## Troubleshooting/Tips

*   In case of flashing minimap or exceedingly low FPS try disabling HUD animations in the in-game options for notable boost in performance.

*   On certain intel cards, enabling vertical sync can lead to a big boost in performance.

*   If the launcher is all black, make sure you have a lib32 version of libgl installed [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)<sup><small>AUR</small></sup>/[lib32-catalyst-libgl](/index.php/AMD_Catalyst#Installing_from_the_unofficial_repository "AMD Catalyst")

*   If the terrain is too dark, one solution would be to install the proprietary drivers of your graphics card.

*   Disabling Anti-Aliasing, Vertical Synchronization and Frame Rate Cap in the in-game options may greatly improve performance for some cards.

*   If there is no ingame audio with usb sound cards, installing [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) may resolve it.

*   If the login server doesn't respond, you can try by removing wininet:

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winecfg

```

Access the libraries tab, find in the list of existing libraries **wininet**, click Remove...

*   For further troubleshooting, go to [this thread](https://bbs.archlinux.org/viewtopic.php?id=183860).

#### For d3dstream patched Wine

**Warning:** On some setups users may experience temporary game freezes during gameplay if using this patch, proceed with caution. If this happens to you, you may be better off using the official version of Wine as freezing is not tolerable in competitive games.

*   You need to add a registry key to Wine in order to apply the performance boost the patch offers, [read this](https://bbs.archlinux.org/viewtopic.php?pid=1321578#p1321578) for more information on how.

*   If you cannot access the launcher store running d3dstream patched wine, you can bypass the problem by running the game from the default 64-bit prefix with the below command, just remember to restart the game before you try to go for another match.

```
wine .wine32/drive_c/Riot\ Games/League\ of\ Legends/lol.launcher.exe

```

#### In-game shop crash

Edit the file `Config/game.cfg` and add `x3d_platform=1` to `[General]` section.

```
[General]
x3d_platform=1

```

This option should switch to the OpenGL renderer.

**Warning:** This may cause some moderate to severe graphic bugs and blurry textures, depending on setup.

#### Connection Error: connection failure unable to connect to the pvp.net server

Authentication and logging in works, however the connection then fails with the abovementioned error. One possible solution, according to [https://appdb.winehq.org/objectManager.php?sClass=version&iId=19141](https://appdb.winehq.org/objectManager.php?sClass=version&iId=19141) is disabling TCP timestamps:

```
# sysctl -w net.ipv4.tcp_timestamps=0

```

For a permanent solution:

```
# echo "net.ipv4.tcp_timestamps = 0" > /etc/sysctl.d/10-tcp-timestamps.conf

```

#### Hang after champ select with AMD proprietary fglrx driver

If you have the proprietary AMD fglrx driver installed, you should install trough winetricks the `directx9` package (Not d3dx_y)

Retrieved from "[https://wiki.archlinux.org/index.php?title=League_of_Legends&oldid=411663](https://wiki.archlinux.org/index.php?title=League_of_Legends&oldid=411663)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")
*   [Wine](/index.php/Category:Wine "Category:Wine")