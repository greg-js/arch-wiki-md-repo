# Redshift

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the [redshift project web page](http://jonls.dk/redshift/):

_Redshift adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](http://justgetflux.com) [...]._

The project is developed on [GitHub](https://github.com/jonls/redshift).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Desktop environments](#Desktop_environments)
    *   [1.2 Autostart](#Autostart)
*   [2 Configuration](#Configuration)
    *   [2.1 Quick start](#Quick_start)
    *   [2.2 Automatic location based on GPS](#Automatic_location_based_on_GPS)
    *   [2.3 Manual setup](#Manual_setup)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screen 1 could not be found](#Screen_1_could_not_be_found)
    *   [3.2 redshift-gtk will not start](#redshift-gtk_will_not_start)
    *   [3.3 Failed to run Redshift due to geoclue2](#Failed_to_run_Redshift_due_to_geoclue2)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [redshift](https://www.archlinux.org/packages/?name=redshift) package. Alternatively, install the [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/)<sup><small>AUR</small></sup> package, for a version with minimal dependencies.

### Desktop environments

For desktop environments, the `redshift-gtk` command is installed with the [redshift](https://www.archlinux.org/packages/?name=redshift) package. redshift-gtk provides a system tray icon for controlling redshift. redshift-gtk requires the [python-gobject](https://www.archlinux.org/packages/?name=python-gobject), [python-xdg](https://www.archlinux.org/packages/?name=python-xdg), and [librsvg](https://www.archlinux.org/packages/?name=librsvg) packages. [KDE](/index.php/KDE "KDE") users can use the [kdeplasma-applets-redshift](https://aur.archlinux.org/packages/kdeplasma-applets-redshift/)<sup><small>AUR</small></sup>. [plasma](https://www.archlinux.org/groups/x86_64/plasma/) users can use the [plasma5-applets-redshift-control-git](https://aur.archlinux.org/packages/plasma5-applets-redshift-control-git/)<sup><small>AUR</small></sup>.

### Autostart

There are two ways to have redshift automatically started:

*   By launching redshift on a script under /etc/X11/xinit/xinitrc.d/
*   Using the provided systemd service unit files (see [Systemd#Using units](/index.php/Systemd#Using_units "Systemd")). Two service files are provided, `/usr/lib/systemd/user/redshift.service` and `/usr/lib/systemd/user/redshift-gtk.service`: activate only one of them depending on whether or not you want the system tray icon. The `DISPLAY` environment variable needs to be configured, see [systemd/User#DISPLAY and XAUTHORITY](/index.php/Systemd/User#DISPLAY_and_XAUTHORITY "Systemd/User").
*   By right-clicking the system tray icon when redshift-gtk or plasma5-applets-redshift-control is already launched and selecting 'Autostart'.

**Note:** The redshift services files contains `Restart=always` so the service will restart infinitely (see `man systemd.service`)

## Configuration

Redshift will at least need your location to start, meaning the latitude and longitude of your location. Redshift employs several routines for obtaining your location. If none of them works (e.g. none of the used helper programs is installed), you need to enter your location manually: For most places/cities an easy way is to look up the wikipedia page of that place and get the location from there (search the page for "coordinates").

### Quick start

To just get it up and running with a basic setup, issue:

```
 $ redshift -l LAT:LON

```

where LAT is the latitude and LON is the longitude of your location.

### Automatic location based on GPS

You can also use [gpsd](https://www.archlinux.org/packages/?name=gpsd) to automatically determine your GPS location and use it as an input for Redshift. Create the following script and pass `$lat` and `$lon` to `redshift -l $lat;$lon`:

```
#!/bin/bash
date
#gpsdata=$( gpspipe -w -n 10 |   grep -m 1 lon )
gpsdata=$( gpspipe -w | grep -m 1 TPV )
lat=$( echo "$gpsdata"  | jsawk 'return this.lat' )
lon=$( echo "$gpsdata"  | jsawk 'return this.lon' )
alt=$( echo "$gpsdata"  | jsawk 'return this.alt' )
dt=$( echo "$gpsdata" | jsawk 'return this.time' )
echo "$dt"
echo "You are here: $lat, $lon at $alt"

```

For more information, see [this](https://bbs.archlinux.org/viewtopic.php?pid=1389735#p1389735) forums thread.

### Manual setup

Redshift reads the configuration file `~/.config/redshift.conf`, if it exists. However, Redshift does not create that configuration file, so you have to create it manually. Below is an example (copied from the [Redshift website](http://jonls.dk/redshift/)).

**Note:** There seems to be a bug in Redshift that causes the transition option in the configuration file to not work as described: Instead of handling the transition between day and night it **only** changes the transition between application start-up and shutdown (and delay the latter as a consequence). See the [talk page](/index.php/Talk:Redshift#Day_and_night_transition "Talk:Redshift") and the [issue on the Redshift project page](https://github.com/jonls/redshift/issues/270) for more information.

 `~/.config/redshift.conf` 

```
; Global settings for redshift
[redshift]
; Set the day and night screen temperatures
temp-day=5700
temp-night=3500

; Enable/Disable a smooth transition between day and night
; 0 will cause a direct change from day to night screen temperature. 
; 1 will gradually increase or decrease the screen temperature
transition=1

; Set the screen brightness. Default is 1.0
;brightness=0.9
; It is also possible to use different settings for day and night since version 1.8.
;brightness-day=0.7
;brightness-night=0.4
; Set the screen gamma (for all colors, or each color channel individually)
gamma=0.8
;gamma=0.8:0.7:0.8

; Set the location-provider: 'geoclue', 'gnome-clock', 'manual'
; type 'redshift -l list' to see possible values
; The location provider settings are in a different section.
location-provider=manual

; Set the adjustment-method: 'randr', 'vidmode'
; type 'redshift -m list' to see all possible values
; 'randr' is the preferred method, 'vidmode' is an older API
; but works in some cases when 'randr' does not.
; The adjustment method settings are in a different section.
adjustment-method=randr

; Configuration of the location-provider:
; type 'redshift -l PROVIDER:help' to see the settings
; e.g. 'redshift -l manual:help'
[manual]
lat=48.1
lon=11.6

; Configuration of the adjustment-method
; type 'redshift -m METHOD:help' to see the settings
; ex: 'redshift -m randr:help'
; In this example, randr is configured to adjust screen 1\. 
; Note that the numbering starts from 0, so this is actually the second screen.
[randr]
screen=1
```

## Troubleshooting

### Screen 1 could not be found

/home/username/.config, change Screen 1 to Screen 0, in redshift.conf

### redshift-gtk will not start

redshift-gtk requires optional dependencies to work correctly. To verify any missing dependencies, run `redshift-gtk` in the command line. Similar output to the following would be produced:

```
 Traceback (most recent call last):
   File "/usr/bin/redshift-gtk", line 26, in <module>
     from redshift_gtk.statusicon import run
   File "/usr/lib/python3.4/site-packages/redshift_gtk/statusicon.py", line 31, in <module>
     from gi.repository import Gtk, GLib
 ImportError: No module named 'gi.repository'

```

If this is the case, installing [python-gobject](https://www.archlinux.org/packages/?name=python-gobject), [python-xdg](https://www.archlinux.org/packages/?name=python-xdg), and [librsvg](https://www.archlinux.org/packages/?name=librsvg) packages solves this issue.

### Failed to run Redshift due to geoclue2

By default, the geoclue2 configuration files does not allow Redshift access. In order to allow access, add the following lines to `/etc/geoclue/geoclue.conf`

 `/etc/geoclue/geoclue.conf` 

```
[redshift]
allowed=true
system=false
users=
```

## See also

*   [Redshift website](http://jonls.dk/redshift)
*   [Redshift on github](http://github.com/jonls/redshift)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Redshift&oldid=411838](https://wiki.archlinux.org/index.php?title=Redshift&oldid=411838)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [X server](/index.php/Category:X_server "Category:X server")
*   [Graphics](/index.php/Category:Graphics "Category:Graphics")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")