[DDNet](https://ddnet.tw) (abbreviation of *DDraceNetwork*) is an actively maintained modification of [Teeworlds](https://www.teeworlds.com) with a unique cooperative gameplay. Help each other play through custom maps with up to 64 players, compete against the best in international tournaments, design your own maps, or run your own server. Players' public ranks are made on serveral official servers are available worldwide.

It works in the client–server model, where the user plays using DDNet Client which connects to a local or remote DDNet Server. Since DDNet has official servers, you most likely will only start the Client and play online.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Optional packages](#Optional_packages)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 User settings](#User_settings)
*   [4 Server](#Server)
    *   [4.1 Setting up a server](#Setting_up_a_server)
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
    *   [5.12 map_version](#map_version)
    *   [5.13 packetgen](#packetgen)
    *   [5.14 tileset_borderadd](#tileset_borderadd)
    *   [5.15 tileset_borderfix](#tileset_borderfix)
    *   [5.16 tileset_borderrem](#tileset_borderrem)
    *   [5.17 tileset_borderset](#tileset_borderset)
    *   [5.18 uuid](#uuid)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [ddnet](https://aur.archlinux.org/packages/ddnet/) from [AUR](/index.php/AUR "AUR"). Alternatively, you install the development version [ddnet-git](https://aur.archlinux.org/packages/ddnet-git/) in same place.

### Optional packages

[ddnet-skins](https://aur.archlinux.org/packages/ddnet-skins/) – provides the whole [DDNet's skin database](https://ddnet.tw/skins/) (also available in a Git repository), allowing you to choose between 600 different skins for your character

[ddnet-maps-git](https://aur.archlinux.org/packages/ddnet-maps-git/) – provides all playable maps available in the [DDNet's maps repository](https://github.com/ddnet/ddnet-maps) with default configurations for running an offline DDNet server. Users interested in setting up a DDNet Server will probably want this package, but it's really not necessary for the DDNet Client.

## Usage

To play DDNet, run the command `$ DDNet` or run the `.desktop` file provided in the package (e.g. in GNOME, search for "ddnet" in its Activities Overview)

It is very straightforward – all user configuration (skin selection, video, controls etc.) can be done from the GUI of the DDNet Client.

No server setup is required; if you want to set up a local server, see [#Server](#Server).

Also, some extra tools – which you probably won't need – are available in `/usr/share/ddnet/tools/`. See [#Extra tools](#Extra_tools).

## Configuration

This section mention config files/directories and their use.

### User settings

The directory `$HOME/.teeworlds/` stores user configuration, demos, screenshots downloaded maps and other user contents.

The config file `settings_ddnet.cfg` is where user's configuration is stored, in a simple text format in a proper syntax. This file is loaded by the Client on startup, and updated when exiting. Therefore, you're not required to set your settings manually in the config file. For all supported client settings, see [Client Settings](https://ddnet.tw/settingscommands/#client-settings).

The subdirectory `downloadedmaps/` will store maps downloaded in runtime by DDNet Client when connecting to server instances, if the maps are not available already.

**Tip:** With [ddnet-maps-git](https://aur.archlinux.org/packages/ddnet-maps-git/) installed, you avoid having to download maps while connecting to server instances

## Server

**Note:** These instructions are **not** required for playing DDNet; see [#Usage](#Usage).

Use these instructions if you want a local server in a [LAN](https://en.wikipedia.org/wiki/Local_area_network "w:Local area network") to play with friends, or due to high latency of Internet servers, or for testing.

### Setting up a server

In order to have a server, you need DDNet installed, config file(s) and maps.

**1- Easy method:**

1.  install the package [ddnet-maps-git](https://aur.archlinux.org/packages/ddnet-maps-git/)
2.  start a server instance using the `.desktop` file provided in the package (e.g. in GNOME, search for "ddnet server" in its Activities Overview), or by running the command `$ DDNet-Server` 

The server instance should be available and visible for a Client in the LAN servers tab.

## Extra tools

The following tools are provided in `/usr/share/ddnet/tools/`:

### config_retrieve

```
$ /usr/share/ddnet/tools/config_retrieve *mapfile.map*

```

Retrieves configuration embedded in DDNet map file and stores in a .cfg with same filename (e.g. "Kobra 4.map" returns "Kobra 4.cfg")

Available since DDNet version 9.0.

### config_store

```
$ /usr/share/ddnet/tools/config_store *mapfile.map*

```

Stores configuration from a map's configuration file into the map file. Both configuration and map files must have the same filename in the same directory, otherwise the operation will fail.

Available since DDNet version 9.0.

**Note:** If there is no difference between the configuration to stored and the configuration embedded in the map, then operation will be cancelled with message `configs coincide, not updating map`.

### confusables

```
$ /usr/share/ddnet/tools/confusables *string1* *string2*

```

Compare *string1* with *string2* and report if they are "confusable", i.e. if the characters are "equal" and could cause confusion. For this to work, the characters with accents or other things around them are considered the "confusable" with the base character. Therefore, *aa* and *aá* are confusable (*á* was considered as *a*), while *aa* and *ab* are not.

If they confusable, returns `not_confusable=0`, otherwise, returns `not_confusable=1`.

Available since DDnet version 10.3.5.

### crapnet

```
$ /usr/share/ddnet/tools/crapnet

```

Tests connection by setting a client–server connection locally and running ping between them. Reports dropped packets with message `dropped packet` and successes with `cfg = *number*`, where *number* varies from 0 to 2.

### dilate

```
$ /usr/share/ddnet/tools/dilate *imagefile1* [*imagefile2* ... ]

```

It is a graphical tool, mainly useful for mappers. It takes care of transparent areas to prevent black/white outlines around your images ingame, therefore avoiding blending and mipmap issues. See [Edge padding](http://wiki.polycount.com/wiki/Edge_padding) for more info.

**Note:** This works only in RGBA image files. So, it won't work for, for instance, in JPEG files.

### dummy_map

```
$ /usr/share/ddnet/tools/dummy_map

```

Creates a dummy, small empty map to be used to start a server. See [[1]](https://github.com/ddnet/ddnet/blob/master/src/engine/shared/network_server.cpp#L371) for more info.

### fake_server

```
$ /usr/share/ddnet/tools/fake_server

```

Creates a fake server for testing.

### map_diff

```
$ /usr/share/ddnet/tools/map_diff *mapfile1.map* *mapfile2.map*

```

Compares two map files, reporting one of the follow:

*   no diff output (maps are the same)
*   `different layer numbers`, if one map has more layers than another
*   `different tile layers`, if the number of layers is the same, but at least one layer is different
*   lastly, the index and flags positions that differ.

If there is no difference between maps, returns 0; otherwise, returns 1.

### map_extract

```
$ /usr/share/ddnet/tools/map_extract *mapfile.map* [*directory*]

```

Extracts content from *mapfile.map* into *directory*. If optional argument *directory* is not provided, extracts to the current directory.

### map_replace_image

```
$ /usr/share/ddnet/tools/map_replace_image *mapfile1.map* *mapfile2.map* *imagename* *imagefile*

```

Replaces the image *imagename* currently inside the map filename *mapfile1.map* with the image filepath *imagefile*, and save into the map filename *mapfile2.map*.

**Note:**

*   both map filenames must be relative to user default ddnet folder
*   new image filepath must be absolute or relative to the current position

### map_resave

```
$ /usr/share/ddnet/tools/map_resave *mapfile.map* *imagefile*

```

Updates the map file *mapfile.map* with the provided file *imagefile*.

The error status 255 is returned if 1) a number of arguments different from 2 is provided, 2) if the *mapfile.map* is not valid, or 3) if *imagefile* is not a valid image file (e.g. it is a text file); otherwise, return 0.

### map_version

### packetgen

```
$ /usr/share/ddnet/tools/packetgen

```

Generates packets to localhost in default port (8303) to test communication with a local server instance.

### tileset_borderadd

```
$ /usr/share/ddnet/tools/tileset_borderadd *tileset1* [*tileset2* ...]

```

It is a graphical tool, mainly useful for mappers. It fixes blending issues, similar to [#dilate], but only applies to tileset files. It expects as input tilesets with a size of 960x960 pixels with 60x60 tiles. After you apply the borderadd operation, the image will be 1024x1024 with 64x64 tiles with a 2px border.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### tileset_borderfix

```
$ /usr/share/ddnet/tools/tileset_borderfix tileset1 [tileset2 ...]

```

Similarly to [#tileset_borderadd](#tileset_borderadd), it is a graphical tool, mainly useful for mappers, that fix blending issues by tilesets. However, this tool expects an input file with 1024x1024 pixels and does not produce output images as great as tileset_borderadd. e.g. it doesn't add 2px border.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### tileset_borderrem

```
$ /usr/share/ddnet/tools/tileset_borderrem tileset1 [tileset2 ...]

```

This is a graphic tool, mainly useful for mappers. It does the inverse operation of [#tileset_borderadd](#tileset_borderadd) and [#tileset_borderset](#tileset_borderset), i.e. this remove border of tilesets.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### tileset_borderset

```
$ /usr/share/ddnet/tools/tileset_borderset tileset1 [tileset2 ...]

```

This is a graphic tool, mainly useful for mappers. It does pretty much the same as [#tileset_borderadd](#tileset_borderadd) but expects 1024x1024 images instead of 960x960, and the border will be done in place. So each 60x60 tile should be placed inside a 64x64 tile.

Returns 255 with a usage message if less than 1 argument is provided, returns 1 if the image is not a RGBA image (i.e. invalid tileset file), and return 0 for success operation.

### uuid

```
$ /usr/share/ddnet/tools/uuid *name*

```

Prints uuid for the provided *name*.

The uuid system was implemented to be easily extended by independent authors without collisions, something that the old system – with increasing integers – did not allow. This works for engine and game messages, snapshot items and events.

Exits with error status 255 if *name* is not provided.

Available since DDNet 10.6.1

## See also

*   [DDNet website](https://ddnet.tw/)
*   [DDNet Forum](https://forum.ddnet.tw/)
*   [DDNet source code repository at GitHub](https://github.com/ddnet/ddnet)