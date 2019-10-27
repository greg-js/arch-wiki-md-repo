From the [Redshift project web page](http://jonls.dk/redshift/):

	[Redshift](https://en.wikipedia.org/wiki/Redshift_(software) adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](http://justgetflux.com).

**Note:** Redshift does not support [Wayland](/index.php/Wayland "Wayland") since it offers no way to adjust the color temperature [[1]](https://github.com/jonls/redshift/issues/55). See [Wayland#Gamma](/index.php/Wayland#Gamma "Wayland") for more.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Front ends](#Front_ends)
*   [2 Usage](#Usage)
    *   [2.1 Quick start](#Quick_start)
    *   [2.2 Autostart](#Autostart)
*   [3 Configuration](#Configuration)
    *   [3.1 Automatic location based on GeoClue2](#Automatic_location_based_on_GeoClue2)
    *   [3.2 Automatic location based on GPS](#Automatic_location_based_on_GPS)
    *   [3.3 Use real screen brightness](#Use_real_screen_brightness)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Screen 1 could not be found](#Screen_1_could_not_be_found)
    *   [4.2 Left/right clicking the tray icon does not work](#Left/right_clicking_the_tray_icon_does_not_work)
    *   [4.3 Redshift makes the screen quickly flicker between the set color value of the screen and the default color value](#Redshift_makes_the_screen_quickly_flicker_between_the_set_color_value_of_the_screen_and_the_default_color_value)
    *   [4.4 Redshift works fine when invoked as a command but fails when run as a systemd service](#Redshift_works_fine_when_invoked_as_a_command_but_fails_when_run_as_a_systemd_service)
    *   [4.5 Redshift temporarily resets using some wine apps that reset gamma values](#Redshift_temporarily_resets_using_some_wine_apps_that_reset_gamma_values)
    *   [4.6 Redshift GDBus.Error:org.freedesktop.DBus.Error.AccessDenied on start](#Redshift_GDBus.Error:org.freedesktop.DBus.Error.AccessDenied_on_start)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [redshift](https://www.archlinux.org/packages/?name=redshift) package. Alternatively, install the [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/) package, for a version with minimal dependencies.

### Front ends

The *redshift-gtk* command comes with the [redshift](https://www.archlinux.org/packages/?name=redshift) package and provides a system tray icon for controlling Redshift. See optional dependencies.

Alternatives are [redshiftgui-bin](https://aur.archlinux.org/packages/redshiftgui-bin/) (GTK) and [redshift-qt](https://aur.archlinux.org/packages/redshift-qt/), [redshiftconf](https://aur.archlinux.org/packages/redshiftconf/) or [plasma5-applets-redshift-control](https://www.archlinux.org/packages/?name=plasma5-applets-redshift-control) and [plasma5-applets-redshift-control-git](https://aur.archlinux.org/packages/plasma5-applets-redshift-control-git/) (Qt).

## Usage

Redshift will at least need your location to start (unless `-O` is used), meaning the latitude and longitude of your location. Redshift employs several routines for obtaining your location. If none of them works (e.g. none of the used helper programs is installed), you need to enter your location manually.

### Quick start

To just get it up and running with a basic setup, issue:

```
$ redshift -l *LATITUDE*:*LONGITUDE*

```

where *LATITUDE* is the latitude and *LONGITUDE* is the longitude of your location.

**Tip:** You can get the coordinates of a place with [GeoNames.org](http://www.geonames.org/).

To instantly adjusts the color temperature of your screen use:

```
$ redshift -P -O *TEMPERATURE*

```

where *TEMPERATURE* is the desired [color temperature](https://en.wikipedia.org/wiki/Color_temperature "wikipedia:Color temperature") (between `1000` and `25000`).

### Autostart

There are several options to have Redshift automatically started:

*   By right-clicking the system tray icon and selecting *Autostart* when *redshift-gtk* or *plasma5-applets-redshift-control* is already launched.
*   By placing a Redshift [desktop entry](/index.php/Desktop_entry "Desktop entry") in `~/.config/autostart/` or by adding `redshift` to your window manager or desktop environment's [autostarting](/index.php/Autostarting "Autostarting") method.
*   By using [systemd/User](/index.php/Systemd/User "Systemd/User"). Two services are provided: `redshift.service` and `redshift-gtk.service`. Activate only one of them depending on whether or not you want the system tray icon.

**Note:**

*   The Redshift service files contain `Restart=always` so they will restart infinitely. See [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5).
*   When using a systemd user service, [Xorg](/index.php/Xorg "Xorg") must be started before execution of the service, which is not the case without a [display manager](/index.php/Display_manager "Display manager"). Otherwise you will get `RANDR Query Version' returned error -1` and `Initialization of randr failed`.

## Configuration

Redshift reads the configuration file `~/.config/redshift/redshift.conf` [[2]](https://github.com/jonls/redshift/releases/tag/v1.12) if it exists. However, Redshift does not create that configuration file, so you may want to create it manually. See [redshift.conf.sample](https://raw.githubusercontent.com/jonls/redshift/master/redshift.conf.sample).

### Automatic location based on GeoClue2

First check if GeoClue2 backend is operating properly by running `$ /usr/lib/geoclue-2.0/demos/where-am-i`. At this time default Archlinux API key for Mozilla services reaches limit (see [SO post](https://unix.stackexchange.com/questions/495333/geoclue2-insists-that-permission-is-forbidden) and [bugreport](https://bugs.archlinux.org/task/61494)) and Wi-Fi location banned. As workaround it's suggested to change API key to 'geoclue'.

 `/etc/geoclue/geoclue.conf`  `url=[https://location.services.mozilla.com/v1/geolocate?key=geoclue](https://location.services.mozilla.com/v1/geolocate?key=geoclue)` 

In order to allow access Redshift to use GeoClue2, add the following lines to `/etc/geoclue/geoclue.conf`:

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

[Restart](/index.php/Restart "Restart") `redshift.service` and/or any other Redshift instance to apply the changes.

**Note:**

*   This workaround is not needed with Geoclue2 version 2.5.0 and above.
*   If using [GNOME](/index.php/GNOME "GNOME"), also toggle Location Services to "On" in *Settings > Privacy*.
*   Due possible bugs with geoclue2 and Redshift [[3]](https://github.com/jonls/redshift/issues/318), it may be required to use the `manual` location-provider instead, e.g. for Paris:

 `~/.config/redshift/redshift.conf` 
```
[redshift]
...
; Set the location-provider: 'geoclue2', 'manual'
; type 'redshift -l list' to see possible values.
; The location provider settings are in a different section.
location-provider=manual

...

; Keep in mind that longitudes west of Greenwich (e.g. the Americas)
; are negative numbers.
[manual]
lat=82.50
lon=-62.34
```

*   If using [i3wm](/index.php/I3wm "I3wm") or similar, you will also need to enable the geoclue agent on startup. As well as `systemctl --user enable redshift-gtk` or `redshift` user service.

 `~/.i3/config` 
```
...
exec --no-startup-id /usr/lib/geoclue-2.0/demos/agent
...
```

### Automatic location based on GPS

You can also use [gpsd](https://www.archlinux.org/packages/?name=gpsd) to automatically determine your [GPS](/index.php/GPS "GPS") location and use it as an input for Redshift. Create the following script and pass `$lat` and `$lon` to `redshift -l $lat;$lon`:

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

### Use real screen brightness

Redshift has a brightness adjustment setting, but it does not work the way most people might expect. In fact it is a fake brightness adjustment obtained by manipulating the gamma ramps, which means that it does not reduce the backlight of the screen. [[4]](http://jonls.dk/redshift/#known-bugs-and-limitations)

Changing screen backlight is possible with redshift hooks and [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) and [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) but, please see [Backlight#xbacklight](/index.php/Backlight#xbacklight "Backlight") as there are some limitations and you may have to find another method of controlling the backlight depending on your hardware.

You need to create a file in `~/.config/redshift/hooks` and make it executable. You can use and edit the following example:

```
$ mkdir -p ~/.config/redshift/hooks

```

Create and adjust the following script:

 `~/.config/redshift/hooks/brightness.sh` 
```
#!/bin/sh

# Set brightness via xbrightness when redshift status changes

# Set brightness values for each status.
# Range from 1 to 100 is valid
brightness_day=100
brightness_transition=50
brightness_night=10
# Set fade time for changes to one minute
fade_time=60000

if [ "$1" = period-changed ]; then
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
fi
```

Make it [executable](/index.php/Executable "Executable"):

```
$ chmod +x ~/.config/redshift/hooks/brightness.sh

```

[Restart](/index.php/Restart "Restart") the `redshift.service` to apply changes.

Check the service status as it should **not** contain the following message:

```
redshift[..]: No outputs have backlight property

```

## Troubleshooting

### Screen 1 could not be found

Locate configuration-file "redshift.conf" in your distribution and change "screen 1" to "screen 0".

### Left/right clicking the tray icon does not work

Install [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3). See [redshift issue 363](https://github.com/jonls/redshift/issues/363) and [FS#49971](https://bugs.archlinux.org/task/49971).

### Redshift makes the screen quickly flicker between the set color value of the screen and the default color value

Make sure there are not multiple instances of redshift running.

### Redshift works fine when invoked as a command but fails when run as a systemd service

The [systemd](/index.php/Systemd "Systemd") unit has a line in the `redshift.service` file that makes the service wait until the `display-manager.service` unit is started by a [display manager](/index.php/Display_manager "Display manager") before the unit will invoke `redshift`. If you do not use a display manager, [edit](/index.php/Edit "Edit") the `redshift.service` user service and delete the `After=display-manager.service` line. Run `systemctl --user daemon-reload` and the service should initialize properly.

### Redshift temporarily resets using some wine apps that reset gamma values

If you notice that using some wine apps, redshift seems to reset temporarily upon launch, or adjusting settings, or etc, then there is a useful registry key that seems to alleviate this. See [[5]](https://www.winehq.org/pipermail/wine-bugs/2015-January/403770.html) and [[6]](https://wiki.winehq.org/UsefulRegistryKeys). Set or create the string value

 `HKEY_CURRENT_USER\Software\Wine\X11 Driver`  `UseXVidMode="N"` 

using the registry editor, or import/set it otherwise.

### Redshift GDBus.Error:org.freedesktop.DBus.Error.AccessDenied on start

If running `$ redshift` and you are getting:

 `$ redshift` 
```
Trying location provider `geoclue2'...
Using provider `geoclue2'.
Unable to start GeoClue client: GDBus.Error:org.freedesktop.DBus.Error.AccessDenied: 'redshift' disallowed, no agent for UID 1000.
Unable to connect to GeoClue.
Unable to get location from provider.

```

or running `$ redshift-gtk` and getting the similar error:

 `$ redshift-gtk` 
```
Failed to run Redshift
Trying location provider `geoclue2'...
Unable to start GeoClue client:
GDBus.Error:org.freedesktop.DBus.Error.AccessDenied:
'redshift' disallowed, no agent for UID 1000.
Unable to connect to GeoClue.
Unable to get location from provider.

```

You can create a [systemd](/index.php/Systemd "Systemd") unit file in `~/.config/systemd/user/geoclue-agent.service` with the following config:

 `~/.config/systemd/user/geoclue-agent.service` 
```
[Unit]
Description=redshift needs to get a (geo)clue

[Service]
ExecStart=/usr/lib/geoclue-2.0/demos/agent

[Install]
WantedBy=default.target
```

Start and enable the service with systemctl: `$ systemctl --user enable --now geoclue-agent.service` and try running redshift again.

If you still get the same error, it may be because of geoclue being locked down to a few programs by default. Try adding the following lines to `/etc/geoclue/geoclue.conf` (see [redshift issue 158](https://github.com/jonls/redshift/issues/158#issuecomment-71329118) and [FS#40360](https://bugs.archlinux.org/task/40360)) and run `$ redshift` again:

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
*   [Wikipedia:Redshift (software)](https://en.wikipedia.org/wiki/Redshift_(software) "wikipedia:Redshift (software)")
*   Similar software: [[7]](https://github.com/jumper149/blugon) [blugon](https://aur.archlinux.org/packages/blugon/), [xflux-gui-git](https://aur.archlinux.org/packages/xflux-gui-git/)