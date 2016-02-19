[Rygel](https://live.gnome.org/Rygel) is a streaming media server compatible with many [DLNA](http://en.wikipedia.org/wiki/Digital_Living_Network_Alliance)/[UPnP](http://en.wikipedia.org/wiki/Universal_Plug_and_Play) clients including the Sony PlayStation 3, Microsoft Xbox 360, smart televisions, DLNA speakers and many smartphones. Rygel will automatically transcode media to a format compatible with the client device. It can also utilise published media hierarchies from external applications like [Rhythmbox](/index.php/Rhythmbox "Rhythmbox") and DVB Daemon through the D-Bus MediaServer specification. It is under active development and is a part of the [GNOME](/index.php/GNOME "GNOME") project.

## Installation

Install the [rygel](https://www.archlinux.org/packages/?name=rygel) package.

## Configuration

After having installed Rygel on a GNOME environment, the "Share media" option will be available along the Sharing settings.

Rygel can be configured globally (`/etc/rygel.conf`) or per-user (`$HOME/.config/rygel.conf`). The default `/etc/rygel.conf` is well documented.

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