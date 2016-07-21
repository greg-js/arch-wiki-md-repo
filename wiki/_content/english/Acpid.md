[acpid2](http://acpid2.sourceforge.net/) is a flexible and extensible daemon for delivering [ACPI events](/index.php/ACPI_modules "ACPI modules"). When an event occurs, it executes programs to handle the event. These events are triggered by certain actions, such as:

*   Pressing special keys, including the Power/Sleep/Suspend button
*   Closing a notebook lid
*   (Un)Plugging an AC power adapter from a notebook
*   (Un)Plugging phone jack etc.

**Note:** [Desktop environments](/index.php/Desktop_environments "Desktop environments"), such as [GNOME](/index.php/GNOME "GNOME"), [systemd](/index.php/Power_management#ACPI_events "Power management") login manager and some [extra key handling](/index.php/Extra_keyboard_keys "Extra keyboard keys") daemons may implement own event handling schemes, independent of acpid. Running more than one system at the same time may lead to unexpected behaviour, such as suspending two times in a row after one sleep button press. You should be aware of this and only activate desirable handlers.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Alternative configuration](#Alternative_configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Example events](#Example_events)
    *   [3.2 Enabling volume control](#Enabling_volume_control)
    *   [3.3 Enabling backlight control](#Enabling_backlight_control)
    *   [3.4 Enabling Wi-Fi toggle](#Enabling_Wi-Fi_toggle)
    *   [3.5 Getting user name of the current display](#Getting_user_name_of_the_current_display)
        *   [3.5.1 Connect to acpid socket](#Connect_to_acpid_socket)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [acpid](https://www.archlinux.org/packages/?name=acpid) package. Then [start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") `acpid.service`.

## Configuration

[acpid](https://www.archlinux.org/packages/?name=acpid) comes with a number of predefined actions for triggered events, such as what should happen when you press the Power button on your machine. By default, these actions are defined in `/etc/acpi/handler.sh`, which is executed after any ACPI events are detected (as determined by `/etc/acpi/events/anything`).

The following is a brief example of one such action. In this case, when the Sleep button is pressed, acpid runs the command `echo -n mem >/sys/power/state` which *should* place the computer into a sleep (suspend) state:

```
button/sleep)
    case "$2" in
        SLPB) echo -n mem >/sys/power/state ;;
	 *)    logger "ACPI action undefined: $2" ;;
    esac
    ;;

```

Unfortunately, not every computer labels ACPI events in the same way. For example, the Sleep button may be identified on one machine as *SLPB* and on another as *SBTN*.

To determine how your buttons or `Fn` shortcuts are recognized, run the following command:

```
# journalctl -f

```

Now press the Power button and/or Sleep button (e.g. `Fn+Esc`) on your machine. The result should look something this:

```
logger: ACPI action undefined: PBTN
logger: ACPI action undefined: SBTN

```

If that does not work, run:

```
# acpi_listen

```

or with [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat):

```
$ netcat -U /var/run/acpid.socket

```

Then press the power button and you will see something like this:

```
button/power PBTN 00000000 00000b31

```

The output of `acpi_listen` is sent to `/etc/acpi/handler.sh` as $1, $2 , $3 & $4 parameters. Example:

```
$1 button/power
$2 PBTN
$3 00000000
$4 00000b31

```

As you might have noticed, the Sleep button in the sample output is actually recognized as *SBTN*, rather than the *SLPB* label specified in the default `/etc/acpi/handler.sh`. In order for Sleep function to work properly on this machine, we would need to replace *SLPB)* with *SBTN)*.

Using this information as a base, you can easily customize the `/etc/acpi/handler.sh` file to execute a variety of commands depending on which event is triggered. See the [Tips & Tricks](#Tips_.26_Tricks) section below for other commonly used commands.

### Alternative configuration

By default, all ACPI events are passed through the `/etc/acpi/handler.sh` script. This is due to the ruleset outlined in `/etc/acpi/events/anything`:

```
# Pass all events to our one handler script
event=.*
action=/etc/acpi/handler.sh %e

```

While this works just fine as it is, some users may prefer to define event rules and actions in their own self-contained scripts. The following is an example of how to use an individual event file and corresponding action script:

As root, create the following file:

 `/etc/acpi/events/sleep-button` 
```
event=button sleep.*
action=/etc/acpi/actions/sleep-button.sh %e
```

Now create the following file:

 `/etc/acpi/actions/sleep-button.sh` 
```
#!/bin/sh
case "$3" in
    SLPB) echo -n mem >/sys/power/state ;;
    *)    logger "ACPI action undefined: $3" ;;
esac
```

Finally, make the script executable:

```
# chmod +x /etc/acpi/actions/sleep-button.sh

```

Using this method, it is easy to create any number of individual event/action scripts.

## Tips and tricks

**Note:** Some of actions, described here, such as Wi-Fi toggle and backlight control, may already be managed directly by driver. You should consult documentation of corresponding kernel modules, when this is the case.

### Example events

The following are examples of events that can be used in the `/etc/acpi/handler.sh` script. These examples should be modified so that they apply your specific environment e.g. changing the event variable names interpreted by `acpi_listen`.

To set the laptop screen brightness when plugged in power or not (the numbers might need to be adjusted, see `/sys/class/backlight/acpi_video0/max_brightness`):

```
ac_adapter)
    case "$2" in
        AC*|AD*)
            case "$4" in
                00000000)
                    echo -n 50 > /sys/class/backlight/acpi_video0/brightness
                    ;;
                00000001)
                    echo -n 100 > /sys/class/backlight/acpi_video0/brightness
                    ;;
            esac

```

### Enabling volume control

Find out the acpi identity of the volume buttons (see above) and susbtitute it for the acpi events in the files below.

 `/etc/acpi/events/vol-d` 
```
event=button/volumedown
action=amixer set Master 5-
```
 `/etc/acpi/events/vol-m` 
```
event=button/mute
action=amixer set Master toggle
```
 `/etc/acpi/events/vol-u` 
```
event=button/volumeup
action=amixer set Master 5+
```

**Note:** These commands may not work as expected with PulseAudio. See [PulseAudio/Troubleshooting#Output stuck muted while Master is toggled](/index.php/PulseAudio/Troubleshooting#Output_stuck_muted_while_Master_is_toggled "PulseAudio/Troubleshooting").

**Tip:** Disable or bind the volume buttons in Xorg to prevent conflicts with other applications. See [Xmodmap](/index.php/Xmodmap "Xmodmap") for details.

See also [Fixing volume change in Linux](http://blog.lastlog.de/posts/fixing_volume_change_in_linux/).

### Enabling backlight control

Similar to volume control, acpid also enables you to control screen backlight. To achieve this you write some handler, like this:

 `/etc/acpi/handlers/bl` 
```
#!/bin/sh
bl_dev=/sys/class/backlight/acpi_video0
step=1

case $1 in
  -) echo $(($(< $bl_dev/brightness) - $step)) >$bl_dev/brightness;;
  +) echo $(($(< $bl_dev/brightness) + $step)) >$bl_dev/brightness;;
esac
```

and again, connect keys to ACPI events:

 `/etc/acpi/events/bl_d` 
```
event=video/brightnessdown
action=/etc/acpi/handlers/bl -
```
 `/etc/acpi/events/bl_u` 
```
event=video/brightnessup
action=/etc/acpi/handlers/bl +
```

### Enabling Wi-Fi toggle

You can also create a simple wireless-power switch by pressing the WLAN button. Example of event:

 `/etc/acpi/events/wlan` 
```
event=button/wlan
action=/etc/acpi/handlers/wlan
```

and its handler:

 `/etc/acpi/handlers/wlan` 
```
#!/bin/sh
rf=/sys/class/rfkill/rfkill0

case $(< $rf/state) in
  0) echo 1 >$rf/state;;
  1) echo 0 >$rf/state;;
esac
```

### Getting user name of the current display

To run commands dependening on [Xorg](/index.php/Xorg "Xorg"), defining the X display as well as the MIT magic cookie file (via XAUTHORITY) is required. Latter is a security credential providing read and write access to the X server, display, and any input devices (see `man xauth`).

See [[1]](https://gist.githubusercontent.com/AladW/de1c5676d93d05a5a0e1/raw/16e010ecda9f2328e1e22d4e02ac814ed27717b4/gistfile1.txt) for an example function when using [xinitrc](/index.php/Xinitrc "Xinitrc").

**Note:**

*   If the LCD backlight is not turned off when the lid is closed, you may do so manually by running `getXuser xset dpms force off` and `getXuser xset dpms force on` respectively on lid close and lid open events. Should the display be blanked, but the backlight left on, instead use [vbetool](https://www.archlinux.org/packages/?name=vbetool) with `vbetool dpms off` and `vbetool dpms on`. See also [XScreenSaver#DPMS settings](/index.php/XScreenSaver#DPMS_settings "XScreenSaver").
*   When using *who* or *w*, make sure `/run/utmp` is created at boot-time. See `man utmp` for details.

#### Connect to acpid socket

In addition to rule files, acpid accepts connections on a UNIX domain socket, by default `/var/run/acpid.socket`. User applications may connect to this socket.

```
#!/bin/bash
coproc acpi_listen
trap 'kill $COPROC_PID' EXIT

while read -u ${COPROC[0]} -a event; do
    *handler.sh* ${event[@]}
done

```

Where *handler.sh* can be a script similar to `/etc/acpi/handler.sh`.

## See also

*   [acpid homepage](http://acpid.sourceforge.net/)
*   [Gentoo wiki](http://www.gentoo-wiki.info/ACPI/Configuration)