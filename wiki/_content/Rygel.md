# Rygel

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Rygel is available in one of the Arch repos now. It also uses a different configuration format. (Discuss in [Talk:Rygel#](https://wiki.archlinux.org/index.php/Talk:Rygel))

[Rygel](https://live.gnome.org/Rygel) is a streaming media server compatible with many [DLNA](http://en.wikipedia.org/wiki/Digital_Living_Network_Alliance)/[UPnP](http://en.wikipedia.org/wiki/Universal_Plug_and_Play) clients including the Sony PlayStation 3, Microsoft Xbox 360, smart televisions, DLNA speakers and many smartphones. Rygel will automatically transcode media to a format compatible with the client device. It can also utilise published media hierarchies from external applications like [Rhythmbox](/index.php/Rhythmbox "Rhythmbox") and DVB Daemon through the D-Bus MediaServer specification. It is under active development and is a part of the [GNOME](/index.php/GNOME "GNOME") project.

## Installation

Install [rygel](https://www.archlinux.org/packages/?name=rygel) from the [gnome-extra](https://www.archlinux.org/groups/i686/gnome-extra/) repository.

## Configuration

After having installed Rygel on a GNOME environment, the "Share media" option will be available along the Sharing settings.

Rygel can be configured globally (`/etc/rygel.conf`) or per-user (`$HOME/.config/rygel.conf`). Some of the common configuration options include:

```
# Set it to 'false' if you want to disable transcoding support.
enable-transcoding=true

# Where video files should be saved if allow-upload is true.
# Defaults to @VIDEOS@, the standard videos folder (typically ${HOME}/Videos).
video-upload-folder=@VIDEOS@

# Where music files should be saved if allow-upload is true
# Defaults to @MUSIC@, the standard music folder (typically ${HOME}/Music).
music-upload-folder=@MUSIC@

# Where picture files should be saved if allow-upload is true
# Defaults to @PICTURES@, the standard picture folder (typically ${HOME}/Pictures).
picture-upload-folder=@PICTURES@

# Tracker's indexing options can be configured with tracker-preferences
[Tracker]
enabled=true
share-pictures=true
share-videos=true
share-music=true
strict-sharing=false
title=@REALNAME@'s media        # whatever name you choose

[MediaExport]
enabled=true
title=@REALNAME@'s media        # whatever name you choose
# List of URIs to export.
uris=@MUSIC@;@VIDEOS@;@PICTURES@
extract-metadata=true
monitor-changes=true            # watch the URIs above for new/changed media
virtual-folders=true

[Playbin]
enabled=true
title=Audio/Video playback on @HOSTNAME@        # whatever name you choose

```

More information on these and other configuration options can be found with `man rygel.conf`.

## Troubleshooting

When starting Rygel from the command line, there are several options that might help you troubleshoot any strange behaviour. Find out more about these options with `man rygel`.

`-g, --log-level=LIST`

Comma-separated list of of DOMAIN:LEVEL pairs. DOMAIN can be "*", "rygel" or the name of a plugin. Levels are 1 for critical, 2 for error, 3 for warning, 4 for info and 5 for debug.

`-d, --disable-plugin=PLUGIN`

Disable PLUGIN

`-t, --disable-transcoding`

Disable transcoding.

`-c, --config=CONFIG_FILE`

Load the specified config file instead of /etc/rygel.conf or $HOME/.config/rygel.conf

Retrieved from "[https://wiki.archlinux.org/index.php?title=Rygel&oldid=377003](https://wiki.archlinux.org/index.php?title=Rygel&oldid=377003)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Streaming](/index.php/Category:Streaming "Category:Streaming")
*   [GNOME](/index.php/Category:GNOME "Category:GNOME")