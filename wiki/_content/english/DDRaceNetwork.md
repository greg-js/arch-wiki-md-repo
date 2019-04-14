**DDNet**, as it is popularly known, is a sidescrolling platform game, featuring weaponry and a cooperative gameplay, and is a mod of [Teeworlds](https://www.teeworlds.com). The game name comes from Dummy Drag Race Network, as it was based in DDRace.

From the official website [ddnet.tw](https://ddnet.tw):

	DDraceNetwork (DDNet) is an actively maintained version of DDRace, a Teeworlds modification with a unique cooperative gameplay. Help each other play through custom maps with up to 64 players, compete against the best in international tournaments, design your own maps, or run your own server. The official servers are located in Germany, Russia, USA, Canada, China, Chile, Brazil and South Africa. All ranks made on official servers are available worldwide and you can collect points!

You control a *tee*, a ball-shaped 2D character, using your keyboard and mouse to shoot, grapple hook and jump around to interact with other players and the environment in the map with the finish line as target.

The game works in a client–server model, where the user plays using a Client which connects to a local or remote Server. Since DDNet has official servers, you most likely will only start the Client and play online.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Optional skins](#Optional_skins)
    *   [1.2 Optional offline maps](#Optional_offline_maps)
*   [2 Play](#Play)
    *   [2.1 Gametypes](#Gametypes)
        *   [2.1.1 DDNet gametypes](#DDNet_gametypes)
        *   [2.1.2 Vanilla gametypes](#Vanilla_gametypes)
        *   [2.1.3 Blocker gametype](#Blocker_gametype)
        *   [2.1.4 FNG-like gametypes](#FNG-like_gametypes)
*   [3 Configuration](#Configuration)
    *   [3.1 File and directory for user settings](#File_and_directory_for_user_settings)
*   [4 Server](#Server)
    *   [4.1 MySQL support](#MySQL_support)
    *   [4.2 Setting up a server](#Setting_up_a_server)
*   [5 Extra tools](#Extra_tools)
    *   [5.1 config_retrieve](#config_retrieve)
    *   [5.2 config_store](#config_store)
    *   [5.3 confusables](#confusables)
    *   [5.4 crapnet](#crapnet)
    *   [5.5 dilate](#dilate)
    *   [5.6 dummy_map](#dummy_map)
    *   [5.7 fake_server](#fake_server)
    *   [5.8 map_diff](#map_diff)
    *   [5.9 map_extract](#map_extract)
    *   [5.10 map_replace_image](#map_replace_image)
    *   [5.11 map_resave](#map_resave)
    *   [5.12 packetgen](#packetgen)
    *   [5.13 tileset_borderadd](#tileset_borderadd)
    *   [5.14 tileset_borderfix](#tileset_borderfix)
    *   [5.15 tileset_borderrem](#tileset_borderrem)
    *   [5.16 tileset_borderset](#tileset_borderset)
    *   [5.17 uuid](#uuid)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Build failed, MYSQL_CPPCONN_INCLUDEDIR and MYSQL_CPPCONN_LIBRARY not found](#Build_failed,_MYSQL_CPPCONN_INCLUDEDIR_and_MYSQL_CPPCONN_LIBRARY_not_found)
    *   [6.2 Build failed, no such file boost/shared_ptr.hpp](#Build_failed,_no_such_file_boost/shared_ptr.hpp)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [ddnet](https://aur.archlinux.org/packages/ddnet/). Alternatively, you can install its development version [ddnet-git](https://aur.archlinux.org/packages/ddnet-git/).

### Optional skins

[Install](/index.php/Install "Install") [ddnet-skins](https://aur.archlinux.org/packages/ddnet-skins/).

This package provides all skins from [DDNet Skin Database](https://ddnet.tw/skins/) for your client, so you can choose between many skins to play with a fancy *tee* char. However, this will not affect anything in the gameplay.

These skins are installed in `/usr/share/ddnet/data/skins/`.

Please notice that other players will only see your chosen skin if they also have it installed and, in this case, they will see a default yellowish one. So, this may happen with the skins from this package or any other skin you modify or create yourself.

**Tip:** It is possible to create or modify skins and use for your char. If you do so, consider publishing it , so other users can use via DDNet Skin Database. For publishing skins, go to [this forum thread](https://forum.ddnet.tw/viewtopic.php?f=17&t=982)

**Warning:** This package brings around an additional RAM memory consumption of 120MB for the DDNet Client, so users playing in a computer with low RAM available might want to avoid it.

### Optional offline maps

[Install](/index.php/Install "Install") [ddnet-maps-git](https://aur.archlinux.org/packages/ddnet-maps-git/).

This package provides all playable maps from the [ddnet-maps repository](https://github.com/ddnet/ddnet-maps) with default configuration files for running an offline DDNet server. So, once installed, eases running a offline server.

**Note:** Client downloads maps automatically upon connection to, or map change of, a server instance. Therefore, it is optional.

Having these maps offline is beneficial for both client and server:

*   Clients will not need to download maps that are already installed by this package. Only new versions of installed maps (rarely happens) or new maps will be downloaded to the user directory (See [#File and directory for user settings](#File_and_directory_for_user_settings).
*   Servers can use the provided maps and configuration files to run without the server-administrator having to expend time creating configurations for them; see [#Server](#Server) for more info.

## Play

To play DDNet, run the command `$ DDNet` or run the `.desktop` file provided in the package (e.g. in GNOME, search for "ddnet" in its Activities Overview)

It is very straightforward – all user configuration (skin selection, video, controls etc.) can be done from the GUI of the DDNet Client.

No server setup is required; if you want to set up a local server, see [#Server](#Server).

Also, some extra tools – which you probably will not need – are available in `/usr/lib/ddnet/tools/`. See [#Extra tools](#Extra_tools).

### Gametypes

Gametypes (a.k.a game types or game modes) are different ways of playing Teeworlds-like games (DDNet included!), and different ways of exploring its resources (e.g. physics, weapons kill or just push other players, etc.).

In the main dashboard of DDNet Client, several server instances are listed (not only DDNet's), each one is launched with only one gametype. In order to play a gametype, you have to join the server instance that has the desired gametype (e.g. you want to play "ctf", you have to look for and join a "ctf" server instance)

See below a non-exhaustive list with name and an explanation of gametypes that can be found in DDNet official servers (although there are a lot more).

#### DDNet gametypes

These are the official DDNet gametypes, which DDNet maintains. That means these gametypes' maps are stored and made available in DDNet's maps repository. It also means that the Test Staff runs some test before the maps being added to the repository and published.

Some of these might require DDNet Client due to features (e.g. dummy *tee*, teaming, specific key bindings) that this client provides, but other could be played with other clients, like Teeworlds.

The goal of these maps, unless mentioned otherwise below, is to overcome obstacules and other difficulties of the map, while helping each other, in order to reach the finish line of map.

This set of gametypes consists of:

*   **novice** – The easiest collaborative maps can be found here. Newcomers should start here.
*   **moderate** – Moderate-level collaborative maps for more experienced users.
*   **brutal** – Hard collaborative maps for very experienced users.
*   **insane** – Insanely hard collaborative maps for insanely experienced users.
*   **solo** – Play alone the whole map, without any a dummy or any physical interaction with users (you can chat with other players, thought)
*   **ddmax** – Maps from DDracemaX, one of the first race mod and very popular one. This project discontinued, so DDNet adopted[[1]](https://forum.ddnet.tw/viewtopic.php?f=3&t=1253) its maps and made available in official servers. See [[2]](https://forum.ddnet.tw/viewtopic.php?f=3&t=1253&start=50#p13111) for info of this gametype.
*   **dummy** – Move your dummy to the finish line, collaboratively or solo depending on the map.
*   **oldschool** – Some old maps to make long-time players nostalgic.
*   **race** – Reach the finish line as fast as you can in a solo run.

**Note:** When looking at the server list of the client dashboard, you may notice that all DDNet server instances have Type column as *DDRace*, and the server instance's name will include the gametype listed above, e.g. "DDNet GER - DDmaX [DDRaceNetwork]"

#### Vanilla gametypes

The so-called *vanilla* gametypes are the first ones, and were created in Teeworlds, and which DDNet supports. This set of gametypes include:

*   **dm** (**d**eath**m**atch) – The goal is to kill as many other players as possible until a certain kill limit or a time limit is reached. Once one of the conditions is met, the match is over, and the winner is the player that accumulated the greatest number of kills.
*   **tdm** (**t**eam **d**eath**m**atch) – Same as Deathmatch above, except that the players are organized into two teams, with each team having its own kill count.
*   **ctf** (**c**apture **t**he **f**lag) – Two teams each have a flag (red for red team and blue for blue team) and the objective is to capture the other team's flag, located at the team's "base," and bring it safely back to their own base until reach a certain score or the time runs out. Kill the enemy to avoid having your flag captured or to get the flag back to your team's base.

#### Blocker gametype

**Note:** You'll find it with type *ddrace*, but the server title and map name can be easily identified as Blocker

**Blocker** has as only target to block other players, which means to fool around throwing into freeze areas. There is no score or time limit in this type of game, or at least it doesn't matter.

Please notice that while being a blocker is expected in the blocker gametype, the same does **not** apply to [#DDNet gametypes](#DDNet_gametypes) – in this last case it is rude and you most likely will be banned by vote of others.

#### FNG-like gametypes

Types noteworthy: **fng** (discontinued, incompatible), **openfng** ([thread](https://www.teeworlds.com/forum/viewtopic.php?id=7868)), **fng2** ([source](https://github.com/teeworldsmods/teeworlds-fng2)).

In this gametype, the players are divided in 2 teams and the target is to win by making more points. You will points by hitting the player with hammer or laser gun (the only weapons available), which will cause freeze, and to throwing into the spikes.

## Configuration

Configurations are stored in plain text files in the user's home directory and can be applied in the GUI options or in the embedded console. See more information below on this topic.

### File and directory for user settings

The directory `$HOME/.teeworlds/` stores user configuration, demos, screenshots downloaded maps and other user contents.

The config file `settings_ddnet.cfg` is where user's configuration is stored, in a simple text format in a proper syntax. This file is loaded by the Client on startup, and updated when exiting. Therefore, you're not required to set your settings manually in the config file. For all supported client settings, see [Client Settings](https://ddnet.tw/settingscommands/#client-settings).

The subdirectory `downloadedmaps/` will store maps downloaded in runtime by DDNet Client when connecting to server instances, if the maps are not available already.

**Tip:** With [ddnet-maps-git](https://aur.archlinux.org/packages/ddnet-maps-git/) installed, you avoid having to download maps while connecting to server instances

## Server

**Note:** These instructions are **not** required for playing DDNet; see [#Play](#Play).

Use these instructions if you want a local server in a [LAN](https://en.wikipedia.org/wiki/Local_area_network "w:Local area network") to play with friends, or due to high latency of Internet servers, or for testing.

### MySQL support

It is possible to use a MySQL or MariaDB instance to store races done in a DDNet Server. However, MySQL support is **not** enabled be default.

To enable MySQL support for [ddnet](https://aur.archlinux.org/packages/ddnet/) or [ddnet-git](https://aur.archlinux.org/packages/ddnet-git/), simply set the variable `_enable_mysql` with the value `1` in their PKGBUILD, and the proper dependencies will be added and proper flags will be enabled.

Case you are building DDNet by yourself, be sure to:

*   install the build dependency [boost](https://www.archlinux.org/packages/?name=boost) and the runtime dependencies [mariadb-libs](https://www.archlinux.org/packages/?name=mariadb-libs) and [mysql-connector-c++](https://aur.archlinux.org/packages/mysql-connector-c%2B%2B/);
*   append `-DMYSQL=ON` to the *cmake* command-line.

**Tip:** See [MariaDB](/index.php/MariaDB "MariaDB") for some post-installation instructions. Make sure to check in there, to avoid problems.

### Setting up a server

In order to have a server, you need DDNet installed, config file(s) and maps.

**1- Easy method:**

1.  install the package [ddnet-maps-git](https://aur.archlinux.org/packages/ddnet-maps-git/)
2.  start a server instance using the `.desktop` file provided in the package (e.g. in GNOME, search for "ddnet server" in its Activities Overview), or by running the command `$ DDNet-Server` 

The server instance should be available and visible for a Client in the LAN servers tab.

## Extra tools

This section list and describe some tools that, while most might not need them, could be useful for e.g. mappers. Some of these tools are developed by the DDNet development team, but other tools were inherited from Teeworlds when forking its source code in the beginning.

The tools below are provided in `/usr/lib/ddnet/tools/` by the DDNet packages.

### config_retrieve

```
$ /usr/lib/ddnet/tools/config_retrieve *mapfile.map*

```

Retrieves configuration embedded in DDNet map file and stores in a .cfg with same filename (e.g. "Kobra 4.map" returns "Kobra 4.cfg")

Available since DDNet version 9.0.

### config_store

```
$ /usr/lib/ddnet/tools/config_store *mapfile.map*

```

Stores configuration from a map's configuration file into the map file. Both configuration and map files must have the same filename in the same directory, otherwise the operation will fail.

Available since DDNet version 9.0.

**Note:** If there is no difference between the configuration to stored and the configuration embedded in the map, then operation will be cancelled with message `configs coincide, not updating map`.

### confusables

```
$ /usr/lib/ddnet/tools/confusables *string1* *string2*

```

Compare *string1* with *string2* and report if they are "confusable", i.e. if the characters are "equal" and could cause confusion. For this to work, the characters with accents or other things around them are considered the "confusable" with the base character. Therefore, *aa* and *aá* are confusable (*á* was considered as *a*), while *aa* and *ab* are not.

If they are confusable, it returns `not_confusable=0`, otherwise, returns `not_confusable=1`.

Available since DDNet version 10.3.5.

### crapnet

```
$ /usr/lib/ddnet/tools/crapnet

```

Tests connection by setting a client–server connection locally and running ping between them. Reports dropped packets with message `dropped packet` and successes with `cfg = *number*`, where *number* varies from 0 to 2.

### dilate

```
$ /usr/lib/ddnet/tools/dilate *imagefile1* [*imagefile2* ... ]

```

It is a graphical tool, mainly useful for mappers. It takes care of transparent areas to prevent black/white outlines around your images ingame, therefore avoiding blending and mipmap issues. See [Edge padding](http://wiki.polycount.com/wiki/Edge_padding) for more info.

**Note:** This works only in RGBA image files. So, it will not work for, for instance, in JPEG files.

### dummy_map

```
$ /usr/lib/ddnet/tools/dummy_map

```

Creates a dummy, small empty map to be used to start a server. See [[3]](https://github.com/ddnet/ddnet/blob/master/src/engine/shared/network_server.cpp#L371) for more info.

### fake_server

```
$ /usr/lib/ddnet/tools/fake_server

```

Creates a fake server for testing.

### map_diff

```
$ /usr/lib/ddnet/tools/map_diff *mapfile1.map* *mapfile2.map*

```

Compares two map files, reporting one of the follow:

*   no diff output (maps are the same)
*   `different layer numbers`, if one map has more layers than another
*   `different tile layers`, if the number of layers is the same, but at least one layer is different
*   lastly, the index and flags positions that differ.

If there is no difference between maps, returns 0; otherwise, returns 1.

### map_extract

```
$ /usr/lib/ddnet/tools/map_extract *mapfile.map* [*directory*]

```

Extracts content from *mapfile.map* into *directory*. If optional argument *directory* is not provided, extracts to the current directory.

### map_replace_image

```
$ /usr/lib/ddnet/tools/map_replace_image *mapfile1.map* *mapfile2.map* *imagename* *imagefile*

```

Replaces the image *imagename* currently inside the map filename *mapfile1.map* with the image filepath *imagefile*, and save into the map filename *mapfile2.map*.

**Note:**

*   Both map filenames must be relative to user default DDNet folder
*   New image filepath must be absolute or relative to the current position

### map_resave

```
$ /usr/lib/ddnet/tools/map_resave *mapfile.map* *imagefile*

```

Updates the map file *mapfile.map* with the provided file *imagefile*.

The error status 255 is returned if 1) a number of arguments different from 2 is provided, 2) if the *mapfile.map* is not valid, or 3) if *imagefile* is not a valid image file (e.g. it is a text file); otherwise, return 0.

### packetgen

```
$ /usr/lib/ddnet/tools/packetgen

```

Generates packets to localhost in default port (8303) to test communication with a local server instance.

### tileset_borderadd

```
$ /usr/lib/ddnet/tools/tileset_borderadd *tileset1* [*tileset2* ...]

```

It is a graphical tool, mainly useful for mappers. It fixes blending issues, similar to [#dilate], but only applies to tileset files. It expects as input tilesets with a size of 960x960 pixels with 60x60 tiles. After you apply the borderadd operation, the image will be 1024x1024 with 64x64 tiles with a 2px border.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### tileset_borderfix

```
$ /usr/lib/ddnet/tools/tileset_borderfix tileset1 [tileset2 ...]

```

Similarly to [#tileset_borderadd](#tileset_borderadd), it is a graphical tool, mainly useful for mappers, that fix blending issues by tilesets. However, this tool expects an input file with 1024x1024 pixels and does not produce output images as great as tileset_borderadd. e.g. it does not add 2px border.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### tileset_borderrem

```
$ /usr/lib/ddnet/tools/tileset_borderrem tileset1 [tileset2 ...]

```

This is a graphic tool, mainly useful for mappers. It does the inverse operation of [#tileset_borderadd](#tileset_borderadd) and [#tileset_borderset](#tileset_borderset), i.e. this remove border of tilesets.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### tileset_borderset

```
$ /usr/lib/ddnet/tools/tileset_borderset tileset1 [tileset2 ...]

```

This is a graphic tool, mainly useful for mappers. It does pretty much the same as [#tileset_borderadd](#tileset_borderadd) but expects 1024x1024 images instead of 960x960, and the border will be done in place. So each 60x60 tile should be placed inside a 64x64 tile.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### uuid

```
$ /usr/lib/ddnet/tools/uuid *name*

```

Prints uuid for the provided *name*.

The uuid system was implemented to be easily extended by independent authors without collisions, something that the old system – with increasing integers – did not allow. This works for engine and game messages, snapshot items and events.

Exits with error status 255 if *name* is not provided.

Available since DDNet 10.6.1

## Troubleshooting

### Build failed, MYSQL_CPPCONN_INCLUDEDIR and MYSQL_CPPCONN_LIBRARY not found

**Problem:**

Build fails and the following message is displayed:

```
CMake Error: The following variables are used in this project, but they are set to NOTFOUND.
Please set them or make sure they are set and tested correctly in the CMake files:
/build/ddnet/src/DDNet-11.1.9/MYSQL_CPPCONN_INCLUDEDIR
   used as include directory in directory /build/ddnet/src/DDNet-11.1.9
   [...]
   used as include directory in directory /build/ddnet/src/DDNet-11.1.9
MYSQL_CPPCONN_LIBRARY
    linked by target "DDNet-Server" in directory /build/ddnet/src/DDNet-11.1.9

-- Configuring incomplete, errors occurred!
See also "/build/ddnet/src/build/CMakeFiles/CMakeOutput.log".
See also "/build/ddnet/src/build/CMakeFiles/CMakeError.log".

```

**Solution:**

It means your *cmake* command-line has the `-DMYSQL=ON` flag set, you have [mariadb-libs](https://www.archlinux.org/packages/?name=mariadb-libs) package installed, but you are missing [mysql-connector-c++](https://aur.archlinux.org/packages/mysql-connector-c%2B%2B/).

Either install [mysql-connector-c++](https://aur.archlinux.org/packages/mysql-connector-c%2B%2B/) to build with MySQL support or remove `-DMYSQL=ON` (or set to off with `-DMYSQL=OFF`) to build without it.

### Build failed, no such file boost/shared_ptr.hpp

**Problem:**

Build fails and the following message is displayed:

```
[ 38%] Building CXX object CMakeFiles/DDNet-Server.dir/src/engine/server/server.cpp.o
In file included from /build/ddnet/src/DDNet-11.1.9/src/engine/server/sql_server.h:4,
                 from /build/ddnet/src/DDNet-11.1.9/src/engine/server/sql_connector.h:4,
                 from /build/ddnet/src/DDNet-11.1.9/src/engine/server/server.h:28,
                 from /build/ddnet/src/DDNet-11.1.9/src/engine/server/server.cpp:40:
/usr/include/mysql_connection.h:31:10: fatal error: boost/shared_ptr.hpp: No such file or directory
 #include <boost/shared_ptr.hpp>
          ^14:06, 19 June 2018 (UTC)14:06, 19 June 2018 (UTC)14:06, 19 June 2018 (UTC)14:06, 19 June 2018 (UTC)~
compilation terminated.
make[2]: *** [CMakeFiles/DDNet-Server.dir/build.make:116: CMakeFiles/DDNet-Server.dir/src/engine/server/server.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:281: CMakeFiles/DDNet-Server.dir/all] Error 2
make: *** [Makefile:152: all] Error 2

```

**Solution:**

It means your *cmake* command-line has the `-DMYSQL=ON` flag set, you have both [mariadb-libs](https://www.archlinux.org/packages/?name=mariadb-libs) and [mysql-connector-c++](https://aur.archlinux.org/packages/mysql-connector-c%2B%2B/) packages installed, but [boost](https://www.archlinux.org/packages/?name=boost) is missing.

Either install [boost](https://www.archlinux.org/packages/?name=boost) to build with MySQL support or remove `-DMYSQL=ON` (or set to off with `-DMYSQL=OFF`) to build without it.

## See also

*   [DDNet official website](https://ddnet.tw/)
*   [DDNet Forum](https://forum.ddnet.tw/)
*   [DDNet source code repository](https://github.com/ddnet/ddnet)
*   [The History of DDNet](https://forum.ddnet.tw/viewtopic.php?f=3&t=1824)
*   [Tutorials and other useful links](https://forum.ddnet.tw/viewtopic.php?f=35&t=2420)