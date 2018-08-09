From the [Redshift project web page](http://jonls.dk/redshift/):

	[Redshift](https://en.wikipedia.org/wiki/Redshift_(software) adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](http://justgetflux.com).

**Note:**

*   Redshift does not support [Wayland](/index.php/Wayland "Wayland") since it offers no way to adjust the color temperature. [[1]](https://github.com/jonls/redshift/issues/55)
*   [GNOME](/index.php/GNOME "GNOME") provides features like Redshift out-of-the-box and has [Wayland](/index.php/Wayland "Wayland") support. Enable the Night Light in Display settings.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Front ends](#Front_ends)
*   [2 Configuration](#Configuration)
    *   [2.1 Quick start](#Quick_start)
    *   [2.2 Autostart](#Autostart)
    *   [2.3 Automatic location based on GeoClue2](#Automatic_location_based_on_GeoClue2)
    *   [2.4 Automatic location based on GPS](#Automatic_location_based_on_GPS)
    *   [2.5 Use real screen brightness](#Use_real_screen_brightness)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screen 1 could not be found](#Screen_1_could_not_be_found)
    *   [3.2 Left/right clicking the tray icon doesn't work](#Left.2Fright_clicking_the_tray_icon_doesn.27t_work)
    *   [3.3 Redshift makes the screen quickly flicker between the set color value of the screen and the default color value](#Redshift_makes_the_screen_quickly_flicker_between_the_set_color_value_of_the_screen_and_the_default_color_value)
    *   [3.4 Redshift works fine when invoked as a command but fails when run as a systemd service](#Redshift_works_fine_when_invoked_as_a_command_but_fails_when_run_as_a_systemd_service)
    *   [3.5 Redshift temporarily resets using some wine apps that reset gamma values](#Redshift_temporarily_resets_using_some_wine_apps_that_reset_gamma_values)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [redshift](https://www.archlinux.org/packages/?name=redshift) package. Alternatively, install the [redshift-minimal](https://aur.archlinux.org/packages/redshift-minimal/) package, for a version with minimal dependencies.

### Front ends

The *redshift-gtk* command comes with the [redshift](https://www.archlinux.org/packages/?name=redshift) package and provides a system tray icon for controlling Redshift. See optional dependencies.

Alternatives are [redshiftgui-bin](https://aur.archlinux.org/packages/redshiftgui-bin/) (GTK) and [redshift-qt](https://aur.archlinux.org/packages/redshift-qt/), [redshiftconf](https://aur.archlinux.org/packages/redshiftconf/) or [plasma5-applets-redshift-control](https://www.archlinux.org/packages/?name=plasma5-applets-redshift-control) and [plasma5-applets-redshift-control-git](https://aur.archlinux.org/packages/plasma5-applets-redshift-control-git/) (Qt).

## Configuration

Redshift will at least need your location to start (unless `-O` is used), meaning the latitude and longitude of your location. Redshift employs several routines for obtaining your location. If none of them works (e.g. none of the used helper programs is installed), you need to enter your location manually.

Redshift reads the configuration file `~/.config/redshift/redshift.conf`, if it exists. However, Redshift does not create that configuration file, so you may want to create it manually. See [redshift.conf.sample](https://raw.githubusercontent.com/jonls/redshift/master/redshift.conf.sample).

**Note:** There seems to be a bug in Redshift that causes the transition option in the configuration file to not work as described: Instead of handling the transition between day and night it **only** changes the transition between application start-up and shutdown (and delay the latter as a consequence). See the [talk page](/index.php/Talk:Redshift#Day_and_night_transition "Talk:Redshift") and the [issue on the Redshift project page](https://github.com/jonls/redshift/issues/270) for more information.

### Quick start

To just get it up and running with a basic setup, issue:

```
$ redshift -l LAT:LON

```

where *LAT* is the latitude and *LON* is the longitude of your location.

**Tip:** You can get the coordinates of a place with [GeoNames.org](http://www.geonames.org/).

To instantly adjusts the color temperature of your screen use:

```
$ redshift -O TEMP

```

where *TEMP* is the desired color temperature (between 1000 and 25000).

### Autostart

There are several options to have redshift automatically started:

*   By using a [systemd](/index.php/Systemd "Systemd") [user unit](/index.php/Systemd#Using_units "Systemd"). Two services are provided: `redshift.service` or `redshift-gtk.service`. Activate only one of them depending on whether or not you want the system tray icon.
*   By adding a shell script with the contents `redshift &> /dev/null &` in `/etc/X11/xinit/xinitrc.d/`, and then make it executable with `chmod +x script_name.sh`.
*   By adding `pgrep redshift &> /dev/null || redshift &> /dev/null &` to `~/.xinitrc` if you are using `startx`
*   By right-clicking the system tray icon when Redshift-GTK or plasma5-applets-redshift-control is already launched and selecting 'Autostart'.
*   By using your preferred window manager or desktop environment's autostart methods. For example in i3, the following line could be added to the config file: `exec --no-startup-id redshift-gtk`. On other desktop environments, [Desktop entries](/index.php/Desktop_entries "Desktop entries") inside `~/.config/autostart` can be used.

**Note:** The Redshift services files contains `Restart=always` so the service will restart infinitely (see [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)).

### Automatic location based on GeoClue2

[Install](/index.php/Install "Install") [geoclue2](https://www.archlinux.org/packages/?name=geoclue2).

In order to allow access Redshift to use GeoClue, add the following lines to `/etc/geoclue/geoclue.conf`:

 `/etc/geoclue/geoclue.conf` 
```
[redshift]
allowed=true
system=false
users=
```

[Restart](/index.php/Restart "Restart") `redshift.service` and/or any other Redshift instance to apply the chances.

**Note:**

*   If using [GNOME](/index.php/GNOME "GNOME"), also toggle Location Services to "On" in "Settings -> Privacy"
*   Due possible bugs with geoclue2 and Redshift [[2]](https://github.com/jonls/redshift/issues/318), it may be required to use the `manual` location-provider instead, e.g. for Paris:

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
lat=48.853
lon=2.349
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

Redshift has a brightness adjustment setting, but it does not work the way most people might expect. In fact it is a fake brightness adjustment obtained by manipulating the gamma ramps, which means that it does not reduce the backlight of the screen. [[3]](http://jonls.dk/redshift/#known-bugs-and-limitations)

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

Make it executable:

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

Locate configuration-file "redshift.conf" in your distribution and change "screen 1" to "screen 0"

### Left/right clicking the tray icon doesn't work

Install [libappindicator-gtk3](https://www.archlinux.org/packages/?name=libappindicator-gtk3). See [[4]](https://github.com/jonls/redshift/issues/363) and [[5]](https://bugs.archlinux.org/task/49971)

### Redshift makes the screen quickly flicker between the set color value of the screen and the default color value

Make sure there aren't multiple instances of redshift running.

### Redshift works fine when invoked as a command but fails when run as a systemd service

The [systemd](/index.php/Systemd "Systemd") unit has a line in the `redshift.service` file that makes the service wait until the `display-manager.service` unit is started by a [display manager](/index.php/Display_manager "Display manager") before the unit will invoke `redshift`. If you do not use a display manager, [edit](/index.php/Edit "Edit") the `redshift.service` user service and delete the `After=display-manager.service` line. Run `systemctl --user daemon-reload` and the service should initialize properly.

### Redshift temporarily resets using some wine apps that reset gamma values

If you notice that using some wine apps, redshift seems to reset temporarily upon launch, or adjusting settings, or etc, then there is a useful registry key that seems to alleviate this. See [[6]](https://www.winehq.org/pipermail/wine-bugs/2015-January/403770.html) and [[7]](https://wiki.winehq.org/UsefulRegistryKeys). Set or create the string value

 `HKEY_CURRENT_USER\Software\Wine\X11 Driver`  `UseXVidMode="N"` using the registry editor, or import/set it otherwise.

## See also

*   [Redshift website](http://jonls.dk/redshift)
*   [Redshift on github](http://github.com/jonls/redshift)
*   **sct** — set color temperature

	[http://www.tedunangst.com/flak/post/sct-set-color-temperature](http://www.tedunangst.com/flak/post/sct-set-color-temperature) || [sct](https://aur.archlinux.org/packages/sct/)

*   [xflux-gui-git](https://aur.archlinux.org/packages/xflux-gui-git/)
*   [Wikipedia:Redshift_(software)](https://en.wikipedia.org/wiki/Redshift_(software) "wikipedia:Redshift (software)")