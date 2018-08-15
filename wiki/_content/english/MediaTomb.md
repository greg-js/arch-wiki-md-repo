Related articles

*   [Streaming media](/index.php/Streaming_media "Streaming media")

**Note:** MediaTomb is unmaintained, users may wish to checkout [Gerbera](https://gerbera.io/) ([gerbera](https://aur.archlinux.org/packages/gerbera/)), which is build upon MediaTomb 12.1.

From [MediaTomb - Free UPnP MediaServer](http://mediatomb.cc/):

	*MediaTomb is an open source (GPL) UPnP MediaServer with a nice web user interface, it allows you to stream your digital media through your home network and listen to/watch it on a variety of UPnP compatible devices.*

MediaTomb enables users to stream digital media to UPnP compatible devices like the PlayStation 3 (the Xbox 360 is not yet supported). Several alternatives exist, such as [FUPPES](http://sourceforge.net/projects/fuppes), [ps3mediaserver](http://code.google.com/p/ps3mediaserver/), and uShare. One of MediaTomb's distinguishing features is the ability to customize the server layout based on extracted metadata (scriptable virtual containers); MediaTomb is highly flexible.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Hiding full paths from media players](#Hiding_full_paths_from_media_players)
    *   [3.2 Playstation 3 Support](#Playstation_3_Support)
    *   [3.3 Samsung TV Support](#Samsung_TV_Support)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Mediatomb doesn't provide content even though it is added in the webfrontend](#Mediatomb_doesn.27t_provide_content_even_though_it_is_added_in_the_webfrontend)
    *   [4.2 The Client loses connection after 30 Minutes](#The_Client_loses_connection_after_30_Minutes)
    *   [4.3 Problems with discovery](#Problems_with_discovery)

## Installation

MediaTomb is available in the [AUR](/index.php/AUR "AUR") via [mediatomb](https://aur.archlinux.org/packages/mediatomb/).

The latest development version is also available in the [AUR](/index.php/AUR "AUR") via [mediatomb-git](https://aur.archlinux.org/packages/mediatomb-git/).

Mediatomb can use its own database, or your local [MariaDB](/index.php/MariaDB "MariaDB") server. For more information about the [MariaDB](/index.php/MariaDB "MariaDB") integration visit the [Documentation](http://mediatomb.cc/pages/documentation#id2855459).

## Configuration

**Warning:** The current version of MediaTomb has a serious bug: The `-i` command-line option to bind to a specific IP address does not work. Bug reported in 2010 to [Debian](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=693301) and [Upstream](http://sourceforge.net/p/mediatomb/bugs/76). The webserver remains accessible on all interfaces, creating a security problem if running on a publicly accessible host.

The default settings may be sufficient for many users, though changes are required for PlayStation 3 support. MediaTomb may be configured and run per-user or as a system-wide daemon. Following installation, either run

```
$ mediatomb

```

to start MediaTomb as the current user and generate a default configuration in `~/.mediatomb/config.xml`, or [start/enable](/index.php/Start/enable "Start/enable") `mediatomb.service` to start the MediaTomb daemon and generate a default configuration in `/var/lib/mediatomb/.mediatomb/config.xml`.

If you want to use the [MariaDB](/index.php/MariaDB "MariaDB") database backend, you can alternatively [start/enable](/index.php/Start/enable "Start/enable") `mediatomb-mariadb.service` which will ensure that [MariaDB](/index.php/MariaDB "MariaDB") is up and running before MediaTomb is.

## Usage

The daemon listens on port `50500` by default. To access the web interface and begin importing media, navigate to [http://127.0.0.1:50500/](http://127.0.0.1:50500/) in your favorite browser (JavaScript required).

If running per-user instances of MediaTomb, the default port is `49152`. However, it is possible that the port will change upon server restart. The URL for the web interface is output during startup. Users may also specify the port manually:

```
$ mediatomb -p 50500

```

### Hiding full paths from media players

By default, full directory paths will be shown on devices when they are browsing through folders.

For example, if you add the directory `/media/my_media/video_data/videos/movies`, anyone connecting will have to navigate to the 'movies' directory from the root.

To hide all of that and only show the directory added, you can change the import script.

For example, this script will automatically truncate the whole directory structure specified in the variable video_root. Any directories added directly under the video root path will show up on UPnP devices starting from the that folder rather than `/`.

```
function addVideo(obj)
{
   var video_root = "/media/main_core/Server_Core_Folder/FTP_Services/Media/";

   var absolute_path = obj.location;

   var relative_path = absolute_path;

   if(absolute_path.indexOf(video_root) == 0)
      relative_path = absolute_path.replace(video_root, "")

  var chain = new Array();

  var pathSplit = relative_path.split("/");

  for(var i = 0; i < pathSplit.length - 1; i++) 
      chain.push(pathSplit[i]);

  addCdsObject(obj, createContainerChain(chain));
}

```

To also hide the default PC Directory folder from UPnP device directory listings, add the following directly under the server node of your `config.xml` file.

```
<pc-directory upnp-hide="yes"/>

```

### Playstation 3 Support

The following notes assume MediaTomb is running as a system-wide daemon. For a per-user install, the locations of the configuration file will be different (see above).

For PlayStation 3 support, users must set `<protocolInfo extend="yes"/>`. An "avi" mimetype mapping should also be uncommented for DivX support.

 `/var/lib/mediatomb/.mediatomb/config.xml` 
```
...

<protocolInfo extend="yes"/>

...

<map from="avi" to="video/divx"/>

...
```

When importing media to the database, MediaTomb will create a virtual container layout as defined by the `<virtual-layout type="...">` option. That is, media will be organized according to metadata (album, artist, etc.) through creation of virtual database objects. If your media is already organized on the file system, you may disable this feature to significantly improve import performance:

 `/var/lib/mediatomb/.mediatomb/config.xml` 
```
...

<virtual-layout type="disabled"/>

...
```

Users may customize the import script to fine-tune the virtual layout. The [Scripting](http://mediatomb.cc/dokuwiki/scripting:scripting) section of the MediaTomb wiki provides several examples. Starting with the built-in script available at `/usr/share/mediatomb/js/import.js`:

```
$ cp /usr/share/mediatomb/js/import.js /var/lib/mediatomb/.mediatomb/

```

... and edit `/var/lib/mediatomb/.mediatomb/import.js` as desired. To utilize the customized script, users must set `<virtual-layout type="js">` and specify the script's location.

 `/var/lib/mediatomb/.mediatomb/config.xml` 
```
...

<virtual-layout type="js">
  <import-script>/var/lib/mediatomb/.mediatomb/import.js</import-script>
</virtual-layout>

...
```

You may have to specify an interface before MediaTomb will be recognized:

 `/var/lib/mediatomb/.mediatomb/config.xml` 
```
<server>
...
  <interface>eth0</interface>
...
</server>

```

... replacing eth0 with the interface you connect on.

After configuring MediaTomb to your liking, [restart](/index.php/Restart "Restart") `mediatomb.service`.

### Samsung TV Support

For Samsung TV support users should install [mediatomb-samsung-tv](https://aur.archlinux.org/packages/mediatomb-samsung-tv/) from the [AUR](/index.php/AUR "AUR"), which it's the same as the [mediatomb](https://aur.archlinux.org/packages/mediatomb/) package with a few more patches. Note that the TV must have [DLNA](https://en.wikipedia.org/wiki/Digital_Living_Network_Alliance "wikipedia:Digital Living Network Alliance") support. Also the server and the TV should be connected to the same network.

The following note assume MediaTomb is running as a system-wide daemon. For a per-user install, the locations of the configuration file will be different (see above).

Some models require changes in config.xml. Users should edit the `<custom-http-headers>` section and add two entries in the `<mappings>` section for better compatibility.

 `/var/lib/mediatomb/.mediatomb/config.xml` 
```
...

<custom-http-headers>
   <add header="transferMode.dlna.org: Streaming"/>
   <add header="contentFeatures.dlna.org: DLNA.ORG_OP=01;DLNA.ORG_CI=0;DLNA.ORG_FLAGS=017000 00000000000000000000000000"/>
</custom-http-headers>

...

<map from="avi" to="video/mpeg"/>
<map from="mkv" to="video/mpeg"/>

...
```

## Troubleshooting

### Mediatomb doesn't provide content even though it is added in the webfrontend

Be aware of the fact that the user Mediatomb runs under, has to have read rights on the files that are added to be able to provide them.

So if Mediatomb runs under the user 'mediatomb' the (video-)files either have to be owned by the user 'mediatomb' and need to be readable or the files and the user 'mediatomb' have to belong to the same group with the file being readable ('mediatomb' has to be in the group to which the file belongs (the file then needs the read rights for the group to be set)).

### The Client loses connection after 30 Minutes

Apparently this is related to SSNP message only being sent once which results in the Client dropping its connection in 30 minutes since it thinks the server is gone.

In the `config.xml` add the alive tag:

```
<alive>180</alive>

```

Default is `180`. See [http://mediatomb.cc/pages/documentation#id2856362](http://mediatomb.cc/pages/documentation#id2856362).

### Problems with discovery

If you experience problem with discovery of MediaTomb service on your device, make sure that it binds to interfaces other than 'lo' - check in /etc/default/mediatomb