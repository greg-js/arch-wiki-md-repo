From the [redshift project web page](http://jonls.dk/redshift/):

	Redshift adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](http://justgetflux.com)....

The project is developed on [GitHub](https://github.com/jonls/redshift).

**Note:** At the moment, Redshift [only works](https://github.com/jonls/redshift/issues/55) with [Xorg](/index.php/Xorg "Xorg") – [Wayland](/index.php/Wayland "Wayland") is not supported yet, see [Redshift#If you are on Wayland](/index.php/Redshift#If_you_are_on_Wayland "Redshift").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Desktop environments](#Desktop_environments)
    *   [1.2 Autostart](#Autostart)
*   [2 Configuration](#Configuration)
    *   [2.1 Quick start](#Quick_start)
    *   [2.2 Automatic location based on GPS](#Automatic_location_based_on_GPS)
    *   [2.3 Manual setup](#Manual_setup)
    *   [2.4 Use real screen brightness](#Use_real_screen_brightness)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screen 1 could not be found](#Screen_1_could_not_be_found)
    *   [3.2 redshift-gtk will not start](#redshift-gtk_will_not_start)
    *   [3.3 Failed to run Redshift due to geoclue2](#Failed_to_run_Redshift_due_to_geoclue2)
    *   [3.4 If you can't get redshift to autostart in i3](#If_you_can.27t_get_redshift_to_autostart_in_i3)
    *   [3.5 If you are on Wayland](#If_you_are_on_Wayland)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [redshift](https://www.archlinux.org/packages/?name=redshift) package. Alternatively, install the [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/) package, for a version with minimal dependencies.

### Desktop environments

For desktop environments, the `redshift-gtk` command is installed with the [redshift](https://www.archlinux.org/packages/?name=redshift) package. `redshift-gtk` provides a system tray icon for controlling redshift and requires these three packages to work: [python-gobject](https://www.archlinux.org/packages/?name=python-gobject), [python-xdg](https://www.archlinux.org/packages/?name=python-xdg), and [librsvg](https://www.archlinux.org/packages/?name=librsvg); all of them are listed as optional dependencies of the main [redshift](https://www.archlinux.org/packages/?name=redshift) package. [KDE](/index.php/KDE "KDE") users can use the [plasma5-applets-redshift-control-git](https://aur.archlinux.org/packages/plasma5-applets-redshift-control-git/).

### Autostart

There are several options to have redshift automatically started:

*   By launching redshift with a script under `/etc/X11/xinit/xinitrc.d/`.
*   By using the provided [systemd service unit files](/index.php/Systemd#Using_units "Systemd"). Be careful: the service can only be started in user mode, see [systemd/User#Basic setup](/index.php/Systemd/User#Basic_setup "Systemd/User"). Two service files are provided: `/usr/lib/systemd/user/redshift.service` and `/usr/lib/systemd/user/redshift-gtk.service`. Activate only one of them depending on whether or not you want the system tray icon. The `DISPLAY` environment variable needs to be configured. See [systemd/User#DISPLAY and XAUTHORITY](/index.php/Systemd/User#DISPLAY_and_XAUTHORITY "Systemd/User").
*   By right-clicking the system tray icon when redshift-gtk or plasma5-applets-redshift-control is already launched and selecting 'Autostart'.

**Note:** The redshift services files contains `Restart=always` so the service will restart infinitely (see `man systemd.service`)

## Configuration

Redshift will at least need your location to start, meaning the latitude and longitude of your location. Redshift employs several routines for obtaining your location. If none of them works (e.g. none of the used helper programs is installed), you need to enter your location manually: For most places/cities an easy way is to look up the wikipedia page of that place and get the location from there (search the page for "coordinates").

### Quick start

**Tip:** [Latlong.net](http://www.latlong.net/) provides a service getting the Latitude and Longitude coordinates.

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
; Set the day and night screen temperatures (Neutral is 6500K)
temp-day=5700
temp-night=3500

; Enable/Disable a smooth transition between day and night
; 0 will cause a direct change from day to night screen temperature.
; 1 will gradually increase or decrease the screen temperature.
transition=1

; Set the screen brightness. Default is 1.0.
;brightness=0.9
; It is also possible to use different settings for day and night
; since version 1.8.
;brightness-day=0.7
;brightness-night=0.4
; Set the screen gamma (for all colors, or each color channel
; individually)
gamma=0.8
;gamma=0.8:0.7:0.8
; This can also be set individually for day and night since
; version 1.10.
;gamma-day=0.8:0.7:0.8
;gamma-night=0.6

; Set the location-provider: 'geoclue2' or 'manual'
; type 'redshift -l list' to see possible values.
; The location provider settings are in a different section.
location-provider=manual

; Set the adjustment-method: 'randr', 'vidmode'
; type 'redshift -m list' to see all possible values.
; 'randr' is the preferred method, 'vidmode' is an older API.
; but works in some cases when 'randr' does not.
; The adjustment method settings are in a different section.
adjustment-method=randr

; Configuration of the location-provider:
; type 'redshift -l PROVIDER:help' to see the settings.
; ex: 'redshift -l manual:help'
; Keep in mind that longitudes west of Greenwich (e.g. the Americas)
; are negative numbers.
[manual]
lat=48.1
lon=11.6

; Configuration of the adjustment-method
; type 'redshift -m METHOD:help' to see the settings.
; ex: 'redshift -m randr:help'
; In this example, randr is configured to adjust screen 1.
; Note that the numbering starts from 0, so this is actually the
; second screen. If this option is not specified, Redshift will try
; to adjust _all_ screens.
[randr]
screen=1
```

### Use real screen brightness

Redshift has a brightness adjustment setting, but it does not work the way most people might expect. In fact it is a fake brightness adjustment obtained by manipulating the gamma ramps, which means that it does not reduce the backlight of the screen. [[1]](http://jonls.dk/redshift/#known-bugs-and-limitations)

Changing screen backlight is possible with redshift hooks and [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr). You need to create a file in `~/.config/redshift/hooks` and make it executable. You can use and edit this example.

 `~/.config/redshift/hooks/brightness.sh` 
```
#!/bin/sh

# Set brightness via xbrightness when redshift status changes

# Set brightness values for each status.
# Range from 1 to 100 is valid
brightness_day="100"
brightness_transition="50"
brightness_night="10"
# Set fade time for changes to one minute
fade_time=60000

case $1 in
	period-changed)
		case $3 in
			night)
				xbacklight -set $brightness_night -time $fade_time
				;;
			transition)
				xbacklight -set $brightness_transition -time $fade_time
				;;
			daytime)
				xbacklight -set $brightness_day -time $fade_time
				;;
		esac
		;;
esac
```

## Troubleshooting

### Screen 1 could not be found

Locate configuration-file "redshift.conf" in your distribution and change "screen 1" to "screen 0"

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

**Note:** Prior to apply the method below, close redshift-gtk and restart the geoclue service. Sometimes the location service fails due to e.g. connection established after the location service.

If using Gnome, you can also toggle Location Services to "On" in "Settings -> Privacy"

By default, the geoclue2 configuration files does not allow Redshift access. In order to allow access, add the following lines to `/etc/geoclue/geoclue.conf`

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

### If you can't get redshift to autostart in i3

You can add this to your i3 config file.

```
   exec --no-startup-id redshift-gtk

```

### If you are on Wayland

At the moment running redshift has no effect under Wayland, because gamma correction is not available there[[2]](https://github.com/jonls/redshift/issues/260). There is an open feature request on their issue tracker.[[3]](https://github.com/jonls/redshift/issues/55)

## See also

*   [Redshift website](http://jonls.dk/redshift)
*   [Redshift on github](http://github.com/jonls/redshift)
*   **sct** — set color temperature

	[https://aur.archlinux.org/packages/sct/](https://aur.archlinux.org/packages/sct/) || [sct](https://aur.archlinux.org/packages/sct/)