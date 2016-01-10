# Urban Terror

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Urban Terror#](https://wiki.archlinux.org/index.php/Talk:Urban_Terror))

"_[Urban Terror](http://www.urbanterror.net)™ is a free multiplayer first person shooter, it can be described as a Hollywood tactical shooter; somewhat realism based, but the motto is "fun over realism". This results in a very unique, enjoyable and addictive game._" <small>[[1]](http://www.urbanterror.net)</small>

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Client](#Client)
        *   [1.1.1 Running Urban Terror in a second X server](#Running_Urban_Terror_in_a_second_X_server)
        *   [1.1.2 Running Urban Terror in a single X server](#Running_Urban_Terror_in_a_single_X_server)
*   [2 Mapping](#Mapping)
    *   [2.1 Prepare the game files](#Prepare_the_game_files)
        *   [2.1.1 Extract your pk3s (recommended, ~1GB free disk space required)](#Extract_your_pk3s_.28recommended.2C_.7E1GB_free_disk_space_required.29)
        *   [2.1.2 Or: Give GTKRadiant write access to the game folder (for single user machines)](#Or:_Give_GTKRadiant_write_access_to_the_game_folder_.28for_single_user_machines.29)
    *   [2.2 Install a level editor](#Install_a_level_editor)
        *   [2.2.1 ZeroRadiant (gtkradiant-svn)](#ZeroRadiant_.28gtkradiant-svn.29)
    *   [2.3 Test your map](#Test_your_map)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Fix urbanterror_ui.shader](#Fix_urbanterror_ui.shader)
    *   [3.2 Problems with libcurl](#Problems_with_libcurl)
    *   [3.3 no sound ??](#no_sound_.3F.3F)
*   [4 External links](#External_links)

## Installation

### Client

Urban Terror is now supported in the [official repositories](/index.php/Official_repositories "Official repositories"). Two packages should be [installed](/index.php/Pacman "Pacman"): [urbanterror](https://www.archlinux.org/packages/?name=urbanterror) and [urbanterror-data](https://www.archlinux.org/packages/?name=urbanterror-data).

#### Running Urban Terror in a second X server

You might want to run this game in an extra X server. To do that, create a new Bash script with that content and mark it as executable:

 `~/xstart/urbanterror.sh` 

```
#!/bin/bash 
DISPLAY=:1.0
xinit /usr/bin/urbanterror $* -- :1
```

Now you can use `Ctrl+Alt+F7` to get to your first X server with your normal desktop, and `Ctrl+Alt+F8` to go back to your game.

Because the second X server is only running the game and the first X server with all your programs is backgrounded, performance should increase. In addition, it is much more convenient to switch X servers while in game to access other resources, rather than having to exit the game completely or `Alt+Tab` out. Finally, it is useful if Urban Terror crashes. Simply `Ctrl+Alt+Backspace` on the second X server to kill that X and all processes on that desktop will terminate as well.

#### Running Urban Terror in a single X server

If you log out from any X sessions if already started up and execute the file from e.g. tty1 (`Ctrl+Alt+F1`) urbanterror is run on the first X Server (`Ctrl+Alt+F7`). All terminal output is printed to tty1\. This works for mostly every game not depending on a window manager.

## Mapping

How to create your own maps.

### Prepare the game files

There are **two ways,** use the second one if you are low on disk space.

#### Extract your pk3s (recommended, ~1GB free disk space required)

To get something to work with, you need to extract Urban Terror's pk3 files to a new folder:

```
install -d ~/urtmapping/q3ut4
cd ~/urtmapping/q3ut4

bsdtar -x -f /opt/urbanterror/q3ut4/zpak000_assets.pk3 --exclude maps
bsdtar -x -f /opt/urbanterror/q3ut4/zpak000.pk3

```

#### Or: Give GTKRadiant write access to the game folder (for single user machines)

GTKradiant creates a few own files inside game directory on creating a game profile. This means that you can own to the Urban Terror folder temporarily until these are created:

```
chown _yourusername_ -R /opt/urbanterror

```

Then start GTKRadiant and configure the game profile (see [below](#ZeroRadiant_.28gtkradiant-svn.29), just use `/opt/urbanterror` as path). Close it afterwards and restrict access again with:

```
chown root -R /opt/urbanterror

```

Please note, that your user will own the newly created files until they get deleted (which is just what we want in this case).

### Install a level editor

It might be possible to create Urban Terror maps with other level editors, such as [netradiant](http://dev.alientrap.org/wiki/7) for example. If you know how to do just that, please add it to the wiki.

#### ZeroRadiant (gtkradiant-svn)

Build and install both [gtkradiant-svn](https://aur.archlinux.org/packages.php?ID=31795) and [gtkradiant-gamepack-urt-svn](https://aur.archlinux.org/packages/gtkradiant-gamepack-urt-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gtkradiant-gamepack-urt-svn)]</sup> from the AUR.

Start gtkradiant by either typing its name in a terminal or clicking the new menu entry. You will see a dialog, choose _Urban Terror (standalone)_ in the drop-down list and `/home/you/urtmapping` as engine directory (_not_ q3ut4). Click OK in the next window and the editor should pop up.

[Here](http://daffy.nerius.com/radiant/#first-map) is a nice guide that explains how to create your first map as well as some Urban Terror specific things you need to watch out for.

### Test your map

Copy your compiled .bsp mapfile to `~/.urbanterror/q3ut4/maps` and run:

```
urbanterror +set fs_game iourtmap +set sv_pure 0 +map _ut4_yourmap_

```

## Troubleshooting

### Fix urbanterror_ui.shader

Open up `~/urtmapping/q3ut4/scripts/urbanterror_ui.shader` in your favorite editor and delete lines 29-55 (from /* to */), because gtkradiant will not recognize this part as a comment and would try to parse it.

### Problems with libcurl

UrbanTerror may complain that it cannot autodownload missing files because the cURL library could not be loaded, even though the cURL package is installed. UrbanTerror expects the shared library file to be called libcurl.so.3, but Arch Linux currently uses libcurl.so.4.

To remedy this, start UrbanTerror with an additional parameter from a terminal emulator:

```
urbanterror +cl_curllib libcurl.so.4

```

### no sound ??

maybe you are using alsa

```
export SDL_AUDIODRIVER=alsa 

```

or maybe you are using the wrong device

```
emacs .asoundrc   

```

maybe this will help..

```
cat /proc/asound/card*/id

```

## External links

[Urban Terror homepage](http://www.urbanterror.info)

[ZeroRadiant homepage](http://www.qeradiant.com/cgi-bin/trac.cgi/wiki/ZeroRadiant)

[UT-Forums: Level Design Linklist](http://forums.urbanterror.info/topic/141-level-design-links/)

[Debian + GTKRadiant + Urban Terror HOW-TO](http://daffy.nerius.com/radiant/)

[UT-Forums: Urban Terror GTKRadiant Tutorial](http://forums.urbanterror.info/topic/13539-complete-linux-gtkradiant-urt-mapping-how-to/page__hl__urtpack__fromsearch__1__s__0bed93b96b8f19a3707143f46acfb964) _Please note_ that the example from this guide has no light and Urban Terror will just display black walls.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Urban_Terror&oldid=414785](https://wiki.archlinux.org/index.php?title=Urban_Terror&oldid=414785)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")