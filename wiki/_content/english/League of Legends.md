[League of Legends](https://www.leagueoflegends.com) is a multiplayer online battle arena video game developed and published by [Riot Games](http://www.riotgames.com/) for Microsoft Windows and OS X. This page outlines working methods to get the Windows version of League of Legends working through [Wine](/index.php/Wine "Wine").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Lutris Method](#Lutris_Method)
    *   [1.2 PlayonLinux Method](#PlayonLinux_Method)
        *   [1.2.1 PlayOnLinux 5](#PlayOnLinux_5)
    *   [1.3 AUR Package](#AUR_Package)
    *   [1.4 Wine Method](#Wine_Method)
        *   [1.4.1 Create a 32-bit Wine PREFIX](#Create_a_32-bit_Wine_PREFIX)
        *   [1.4.2 Install the dependencies](#Install_the_dependencies)
        *   [1.4.3 Client installation](#Client_installation)
            *   [1.4.3.1 Using Windows installer](#Using_Windows_installer)
            *   [1.4.3.2 Using an existing copy of the game](#Using_an_existing_copy_of_the_game)
        *   [1.4.4 Run the game under Wine](#Run_the_game_under_Wine)
            *   [1.4.4.1 Use the League Client open beta](#Use_the_League_Client_open_beta)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Tips](#Tips)
    *   [2.2 Client update issues](#Client_update_issues)
        *   [2.2.1 first client update stuck on 47%](#first_client_update_stuck_on_47.25)
    *   [2.3 Connection issues](#Connection_issues)
        *   [2.3.1 Connection Error: connection failure unable to connect to the pvp.net server](#Connection_Error:_connection_failure_unable_to_connect_to_the_pvp.net_server)
        *   [2.3.2 Login server does not respond](#Login_server_does_not_respond)
    *   [2.4 Launcher issues](#Launcher_issues)
        *   [2.4.1 Launcher screen is black](#Launcher_screen_is_black)
        *   [2.4.2 In-game shop crash](#In-game_shop_crash)
        *   [2.4.3 Store Authentication Required](#Store_Authentication_Required)
        *   [2.4.4 Hang after champ select with AMD proprietary fglrx driver](#Hang_after_champ_select_with_AMD_proprietary_fglrx_driver)
        *   [2.4.5 Game failing to run after Champion Select screen](#Game_failing_to_run_after_Champion_Select_screen)
    *   [2.5 In-game issues](#In-game_issues)
        *   [2.5.1 Low FPS](#Low_FPS)
        *   [2.5.2 For d3dstream patched Wine](#For_d3dstream_patched_Wine)
    *   [2.6 PlayOnLinux Troubleshooting](#PlayOnLinux_Troubleshooting)

## Installation

### Lutris Method

**Tip:** The other methods are lot harder and/or buggy, probably not working at all in some cases. This one is easier and is reported to work on 4º of june 2017

1.  Install [lutris](https://aur.archlinux.org/packages/lutris/) from [AUR](/index.php/AUR "AUR")
2.  Install from [https://lutris.net/games/league-of-legends/](https://lutris.net/games/league-of-legends/)
3.  Once installed and logged in, in the top right gear of the client, check "low spec mode" and uncheck "close client during game"

	Here is an outdated video from the creator of the Lutris script that could be useful in case of doubt/trobleshooting [https://youtu.be/sWisCfj_fA0](https://youtu.be/sWisCfj_fA0)

### PlayonLinux Method

**Note:** The PlayOnLinux script is out of date and may not work. There is a [beta script](https://www.playonlinux.com/en/app-1135-League_Of_Legends.html#contributions) that is reported to work.

To install League of Legends using this method, [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) must be installed in the system. When you first run it, [PlayOnLinux](/index.php/Wine#PlayOnLinux.2FPlayOnMac "Wine") will install some necessary fonts. Afterwards, click Install, check the "testing box" and then search for "League of Legends". The rest is self-explanatory.

If the installer fails saying that DirectX cannot be installed, make sure you install these packages first:

*   [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)
*   [openal](https://www.archlinux.org/packages/?name=openal)
*   [freealut](https://www.archlinux.org/packages/?name=freealut)

#### PlayOnLinux 5

1.  Install [playonlinux5-git](https://aur.archlinux.org/packages/playonlinux5-git/)
2.  Open it and go to Apps -> Games -> "League of Legends BETA Client".
3.  Click install.
4.  Run the "League of Legends BETA Client" from Library.
5.  Upgrade to the BETA client.
6.  Wait for it to finish and close the launcher.
7.  Start the BETA client from the Library.

### AUR Package

**Note:** You may need to add your user to `games` group.

[leagueoflegends](https://aur.archlinux.org/packages/leagueoflegends/) from the [AUR](/index.php/AUR "AUR") is available to ease the installation of the game using the method used in the [#Wine Method](#Wine_Method) section. This package will download the game installer in `/opt/games/leagueoflegends` and configure the wine environment to run the game. Additionally, it creates a bash script and a `.desktop` file to launch the game.

Also you can use [leagueoflegends-git](https://aur.archlinux.org/packages/leagueoflegends-git/) do the same, but another way.

### Wine Method

**Note:** The guide is written mostly for x86_64 systems, if your architecture is i686, you can skip setting up the new Wine Prefix (Just use the default wine prefix instead: .wine). You can also ignore WINEARCH/WINEPREFIX parts of commands· And to you, "lib32-lcms2" would just be "lcms2"

#### Create a 32-bit Wine PREFIX

Install [wine](https://www.archlinux.org/packages/?name=wine) on your system and run:

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winecfg

```

to create a default 32-bit prefix at $HOME/.wine. If it asks to install something (like Wine Mono or Wine Gecko or some such) just always click install. After this make sure Windows Version is set to Windows XP.

#### Install the dependencies

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

#### Client installation

##### Using Windows installer

**Warning:** The Windows installer may not work on some systems.

Use the latest installer from riot games: [https://signup.na.leagueoflegends.com/en/signup/redownload](https://signup.na.leagueoflegends.com/en/signup/redownload) Now unpack it and execute it using msiexec

```
mkdir /tmp/lol_installer
WINEARCH=win32 WINEPREFIX=$HOME/.wine32 wine /PATH/TO/INSTALLER.exe /extract:Z:/tmp/lol_installer
WINEARCH=win32 WINEPREFIX=$HOME/.wine32 wine  msiexec /i /tmp/lol_installer/LoL.XXX.msi

```

Where XXX is the region of the installer.

Follow the steps indicated on the installer menu.

*Note for installing via installer: Uncheck the "Create desktop icon" and "Create start menu icon", it may causes the installer to hang. You can leave the "Run League of Legends" checkbox checked, it does not cause any issues*

##### Using an existing copy of the game

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

#### Run the game under Wine

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
# alias League_of_Legends='pushd $HOME/.wine32/drive_c/Riot\ Games/League\ of\ Legends/RADS/system/ && wine32 rads_user_kernel.exe run lol_launcher $(ls ../projects/lol_launcher/releases/) LoLLauncher.exe && popd'

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

##### Use the League Client open beta

If you want to try out the new League Client, click on the upgrade button on the patcher. You have to add three overrides to your libraries for the client to start.

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winecfg

```

Access the libraries tab, and add :

*   msvcp140 (Native, then builtin)
*   vcomp140 (Native, then builtin)
*   vcruntime140 (Native, then builtin)

Starting the client from the actual patcher seems to work, but you can also start it by improving the script above :

Bash script example: **/bin/leagueoflegends**

```
#!/bin/sh
#

case $1 in
    beta)
        pushd $HOME/.wine32/drive_c/Riot\ Games/League\ of\ Legends/
        WINEARCH=win32 WINEPREFIX=$HOME/.wine32 wine LeagueClient.exe
        ;;
    *)
        pushd $HOME/.wine32/drive_c/Riot\ Games/League\ of\ Legends/RADS/system/
        WINEARCH=win32 WINEPREFIX=$HOME/.wine32 wine rads_user_kernel.exe run lol_launcher $(ls ../projects/lol_launcher/releases/) LoLLauncher.exe
        ;;
esac
popd

```

And running the beta version by typing

```
# leagueoflegends beta

```

## Troubleshooting

### Tips

*   In case of flashing mini-map or exceedingly low FPS try disabling HUD animations in the in-game options for notable boost in performance.

*   On certain Intel cards, enabling vertical sync can lead to a big boost in performance.

*   If the terrain is too dark, one solution would be to install the proprietary drivers of your graphics card.

*   Disabling Anti-Aliasing, Vertical Synchronization and Frame Rate Cap in the in-game options may greatly improve performance for some cards.

*   If there is no in-game audio with usb sound cards, installing [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) may resolve it.

### Client update issues

##### first client update stuck on 47%

**(tried in the Lutris installation version)** I let the game updating the whole night while sleeping. By the time i woke up the client stuck in 47%. I just closed the game (and stoppped it from the Lutris GUI) and when I restarted, it worked like a charm (maybe I was just lucky) and this shouldn't be noted here, but who knows... in concrete: the advice here is just to be really patient and generous with the time, in wine that is usually required (in my case 8+ hours)

### Connection issues

#### Connection Error: connection failure unable to connect to the pvp.net server

Authentication and logging in works, however the connection then fails with the abovementioned error. One possible solution, according to [https://appdb.winehq.org/objectManager.php?sClass=version&iId=19141](https://appdb.winehq.org/objectManager.php?sClass=version&iId=19141) is disabling TCP timestamps:

```
# sysctl -w net.ipv4.tcp_timestamps=0

```

For a permanent solution:

```
# echo "net.ipv4.tcp_timestamps = 0" > /etc/sysctl.d/10-tcp-timestamps.conf

```

#### Login server does not respond

You need to properly configure **wininet** library:

```
# WINEARCH=win32 WINEPREFIX=$HOME/.wine32 winecfg

```

In the library tab, you need to edit the configuration of the **wininet** library to **Built-in then native**.

*   For further troubleshooting, go to [this thread](https://bbs.archlinux.org/viewtopic.php?id=183860).

Alternatively, you can disable the library by adding the following variable override to the launch command:

```
 WINEDLLOVERRIDES='wininet=b,n'

```

### Launcher issues

#### Launcher screen is black

Install the 32-bit graphics driver listed in the *OpenGL (Multilib)* column in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

#### In-game shop crash

Edit the file `Config/game.cfg` and add `x3d_platform=1` to `[General]` section.

```
[General]
x3d_platform=1

```

This option should switch to the OpenGL renderer.

**Warning:** This may cause some moderate to severe graphic bugs and blurry textures, depending on setup.

#### Store Authentication Required

If clicking "Browse the Store" causes a dialog box titled "Authentication Required" with the text "Please enter your username and password: Server store.XX#.lol.riotgame.com", do not enter your user/pass. Clicking OK leads to a screen filled with black text (highlight to confirm), and clicking Cancel probably gives some network timeout error.

A possible solution: After you log in, there is a home screen containing elements that link to youtube videos, patch notes, etc. In this home screen there are two or more elements that link to current sales within the in-game shop. If you click on one of those sales, for example, a skin that is on sale, it'll automatically authenticate and send you to the in-game shop, and as a result you won't get the session error and re-authentication bug.

Tip via [Play on Linux thread](https://www.playonlinux.com/en/app-1135-League_Of_Legends.html).

#### Hang after champ select with AMD proprietary fglrx driver

If you have the proprietary AMD fglrx driver installed, you should install trough winetricks the `directx9` package (Not d3dx_y)

#### Game failing to run after Champion Select screen

First you will want to find your hostname.

```
# cat /etc/hostname

```

Then you will want to make sure your /etc/hosts file uses your hostname over localhost, you can do this by opening /etc/hosts with an editor of your choice.

```
# nano /etc/hosts

```

Then replace all mentions of localhost with the hostname you got from the first command (this change requires a system restart, without this your game will fail after champion select with a "Bad Window" error)

### In-game issues

#### Low FPS

*   On Wine configuration, in staging tab, set CSMT option checked
*   In game settings, set max FPS to 60 and disable vertical sync

#### For d3dstream patched Wine

**Warning:** On some setups users may experience temporary game freezes during gameplay if using this patch, proceed with caution. If this happens to you, you may be better off using the official version of Wine as freezing is not tolerable in competitive games.

*   You need to add a registry key to Wine in order to apply the performance boost the patch offers, [read this](https://bbs.archlinux.org/viewtopic.php?pid=1321578#p1321578) for more information on how.

*   If you cannot access the launcher store running d3dstream patched wine, you can bypass the problem by running the game from the default 64-bit prefix with the below command, just remember to restart the game before you try to go for another match.

```
wine .wine32/drive_c/Riot\ Games/League\ of\ Legends/lol.launcher.exe

```

### PlayOnLinux Troubleshooting

*   **Bugsplat opening patcher:** To fix this you need to configure the PlayOnLinux's wine version by clicking the configure gear, change wine version to system from 1.9-LeagueOfLegends and if you have not done so already install [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap).

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