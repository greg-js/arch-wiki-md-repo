This article details the installation and configuration process of the ***Synaptics input driver*** for Synaptics (and ALPS) touchpads found on most notebooks.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Frequently used options](#Frequently_used_options)
    *   [2.2 Configuration on the fly](#Configuration_on_the_fly)
        *   [2.2.1 Console tools](#Console_tools)
        *   [2.2.2 Graphical tools](#Graphical_tools)
    *   [2.3 GNOME/Xfce4/Cinnamon](#GNOME.2FXfce4.2FCinnamon)
    *   [2.4 MATE](#MATE)
*   [3 Advanced configuration](#Advanced_configuration)
    *   [3.1 Using xinput to determine touchpad capabilities](#Using_xinput_to_determine_touchpad_capabilities)
    *   [3.2 Synclient](#Synclient)
    *   [3.3 evtest](#evtest)
    *   [3.4 xev](#xev)
    *   [3.5 Circular Scrolling](#Circular_Scrolling)
    *   [3.6 Natural scrolling](#Natural_scrolling)
    *   [3.7 Software toggle](#Software_toggle)
    *   [3.8 Disable trackpad while typing](#Disable_trackpad_while_typing)
        *   [3.8.1 Using the driver's automatic palm detection](#Using_the_driver.27s_automatic_palm_detection)
        *   [3.8.2 Using syndaemon](#Using_syndaemon)
    *   [3.9 Disable touchpad on mouse detection](#Disable_touchpad_on_mouse_detection)
        *   [3.9.1 Basic desktop](#Basic_desktop)
        *   [3.9.2 GDM](#GDM)
            *   [3.9.2.1 With syndeamon running](#With_syndeamon_running)
            *   [3.9.2.2 touchpad-state](#touchpad-state)
        *   [3.9.3 KDE](#KDE)
        *   [3.9.4 System with multiple X sessions](#System_with_multiple_X_sessions)
    *   [3.10 Buttonless touchpads (aka ClickPads)](#Buttonless_touchpads_.28aka_ClickPads.29)
        *   [3.10.1 Bottom edge correction](#Bottom_edge_correction)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Touchpad does not work after resuming from hibernate/suspend](#Touchpad_does_not_work_after_resuming_from_hibernate.2Fsuspend)
    *   [4.2 xorg.conf.d/50-synaptics.conf does not seem to apply under GNOME and MATE](#xorg.conf.d.2F50-synaptics.conf_does_not_seem_to_apply_under_GNOME_and_MATE)
    *   [4.3 The touchpad is not working, Xorg.0.log shows "Query no Synaptics: 6003C8"](#The_touchpad_is_not_working.2C_Xorg.0.log_shows_.22Query_no_Synaptics:_6003C8.22)
    *   [4.4 Touchpad detected as "PS/2 Generic Mouse" or "Logitech PS/2 mouse"](#Touchpad_detected_as_.22PS.2F2_Generic_Mouse.22_or_.22Logitech_PS.2F2_mouse.22)
        *   [4.4.1 Elantech touchpads](#Elantech_touchpads)
        *   [4.4.2 Laptops with touchscreen & touchpad](#Laptops_with_touchscreen_.26_touchpad)
    *   [4.5 Non-functional Synaptics special abilities (multi-tap, scrolling, etc.)](#Non-functional_Synaptics_special_abilities_.28multi-tap.2C_scrolling.2C_etc..29)
    *   [4.6 Cursor jump](#Cursor_jump)
    *   [4.7 Touchpad device is not located at /dev/input/*](#Touchpad_device_is_not_located_at_.2Fdev.2Finput.2F.2A)
    *   [4.8 Firefox and special touchpad events](#Firefox_and_special_touchpad_events)
        *   [4.8.1 Firefox 17.0 and later](#Firefox_17.0_and_later)
    *   [4.9 Opera: horizontal scrolling issues](#Opera:_horizontal_scrolling_issues)
    *   [4.10 Scrolling and multiple actions with Synaptics on LG laptops](#Scrolling_and_multiple_actions_with_Synaptics_on_LG_laptops)
    *   [4.11 Other external mouse issues](#Other_external_mouse_issues)
    *   [4.12 Touchpad synchronization issues](#Touchpad_synchronization_issues)
    *   [4.13 Xorg.log.0 shows SynPS/2 Synaptics touchpad can not grab event device, errno=16](#Xorg.log.0_shows_SynPS.2F2_Synaptics_touchpad_can_not_grab_event_device.2C_errno.3D16)
    *   [4.14 Synaptics loses multitouch detection after rebooting from Windows](#Synaptics_loses_multitouch_detection_after_rebooting_from_Windows)
    *   [4.15 Touchpad not recognized after shutdown from Arch](#Touchpad_not_recognized_after_shutdown_from_Arch)
    *   [4.16 Trackpoint and Clickpad](#Trackpoint_and_Clickpad)
    *   [4.17 ASUS Touchpads only recognised as PS/2 FocalTech emulated mouse](#ASUS_Touchpads_only_recognised_as_PS.2F2_FocalTech_emulated_mouse)
*   [5 See also](#See_also)

## Installation

The Synaptics driver can be [installed](/index.php/Installed "Installed") with the package [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

**Tip:** An alternative touchpad driver is [libinput](/index.php/Libinput "Libinput"). It implements a different approach to recognize and process multitouch features.

## Configuration

The primary method of configuration for the touchpad is through an [Xorg](/index.php/Xorg "Xorg") server configuration file. After installation of `xf86-input-synaptics`, a default configuration file is located at `/usr/share/X11/xorg.conf.d/50-synaptics.conf`. Users can copy this file to `/etc/X11/xorg.conf.d/` and edit it to configure the various driver options available. Refer to the `synaptics(4)` manual page for a complete list of available options. Machine-specific options can be discovered using [synclient](#Synclient).

### Frequently used options

The following lists options that many users may wish to configure. This example configuration file enables vertical, horizontal and circular scrolling as well as touchpad tap to click:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
        Option "TapButton1" "1"
        Option "TapButton2" "2"
        Option "TapButton3" "3"
        Option "VertEdgeScroll" "on"
        Option "VertTwoFingerScroll" "on"
        Option "HorizEdgeScroll" "on"
        Option "HorizTwoFingerScroll" "on"
        Option "CircularScrolling" "on"
        Option "CircScrollTrigger" "2"
        Option "EmulateTwoFingerMinZ" "40"
        Option "EmulateTwoFingerMinW" "8"
        Option "CoastingSpeed" "0"
        Option "FingerLow" "30"
        Option "FingerHigh" "50"
        Option "MaxTapTime" "125"
        ...
EndSection

```

	**TapButton1**

	(integer) configures which mouse-button is reported on a non-corner, one finger tap.

	**TapButton2**

	(integer) configures which mouse-button is reported on a non-corner, two finger tap

	**TapButton3**

	(integer) configures which mouse-button is reported on a non-corner, three finger tap

	**RBCornerButton**

	(integer) configures which mouse-button is reported on a right bottom corner, one finger tap (use `Option "RBCornerButton" "3"` to achieve Ubuntu style tap behaviour for right mouse button in lower right corner)

	**RTCornerButton**

	(integer) as above, but for top right corner, one finger tap.

	**VertEdgeScroll**

	(boolean) enables vertical scrolling while dragging across the right edge of the touch pad.

	**HorizEdgeScroll**

	(boolean) enables horizontal scrolling while dragging across the bottom edge of the touch pad.

	**VertTwoFingerScroll**

	(boolean) enables vertical scrolling using two fingers.

	**HorizTwoFingerScroll**

	(boolean) enables horizontal scrolling using two fingers.

	**EmulateTwoFingerMinZ/W**

	(integer) play with this value to set the precision of two finger scroll.

	**FingerLow**

	(integer) when finger pressure drops below this value, the driver counts it as a release.

	**FingerHigh**

	(integer) when finger pressure goes above this value, the driver counts it as a touch.

	**MaxTapTime**

	Determines how "crisp" a tap must be to be considered a real tap. Decrease the value to require a more crisp tap. Properly adjusting this parameter can reduce false positives when the hands hover over or lightly touch the pad.

	**VertScrollDelta** and **HorizScrollDelta**

	(integer) configures the speed of scrolling, it is a bit counter-intuitive because higher values produce greater precision and thus slower scrolling. Negative values cause natural scrolling like in OS X.

**Note:**

*   If you find that your hand frequently brushes your touchpad, causing the TapButton2 option to be triggered (which will more than likely paste from your clipboard), and you do not mind losing two-finger-tap functionality, set `TapButton2` to 0.
*   Recent versions include a "Coasting" feature, enabled by default, which may have the undesired effect of continuing almost any scrolling until the next tap or click, even if you are no longer touching the touchpad. This means that to scroll just a bit, you need to scroll (by using the edge, or a multitouch option) and then almost immediately tap the touchpad, otherwise scrolling will continue forever. If wish to avoid this, set `CoastingSpeed` to 0.
*   If your touchpad is too sensitive, use higher values for `FingerLow` and `FingerHigh` and vice versa. Remember that `FingerLow` should be smaller than `FingerHigh`

### Configuration on the fly

Next to the traditional method of configuration, the Synaptics driver also supports on the fly configuration. This means that users can set certain options through a software application, these options are applied immediately without needing a restart of Xorg. This is useful to test configuration options before you include them in the configuration file.

**Warning:** On-the-fly configuration is non-permanent and will not remain active through a reboot, suspend/resume, or restart of Xorg. This should only be used to test, fine-tune or script configuration features.

#### Console tools

*   **[Synclient](#Synclient) (Recommended)** — command line utility to configure and query Synaptics driver settings on a live system, the tool is developed by the synaptics driver maintainers and is provided with the synaptics driver

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics)

*   **[xinput](#Using_xinput_to_determine_touchpad_capabilities)** — small general-purpose CLI tool to configure devices

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput)

#### Graphical tools

*   **GPointing Device Settings** — provides graphical on the fly configuration for several pointing devices connected to the system, including your synaptics touch pad. This application replaces GSynaptics as the preferred tool for graphical touchpad configuration through the synaptics driver

	[https://wiki.gnome.org/Attic/GPointingDeviceSettings](https://wiki.gnome.org/Attic/GPointingDeviceSettings) || [gpointing-device-settings](https://www.archlinux.org/packages/?name=gpointing-device-settings)

*   **kcm-touchpad** — A new touchpad configuration tool for [KDE](/index.php/KDE "KDE"), provides a module under input devices in system settings. Released in February 2014, works under KDE SC 4.12+. It is to be considered a replacement for [synaptiks](https://aur.archlinux.org/packages/synaptiks/) and [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/).

	[https://projects.kde.org/projects/kde/workspace/kcm-touchpad/repository](https://projects.kde.org/projects/kde/workspace/kcm-touchpad/repository) || [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad)

### GNOME/Xfce4/Cinnamon

Users of [GNOME](/index.php/GNOME "GNOME") may have to edit its configuration as well, because in default it is set to disable tapping to click, horizontal scrolling and not to allow touchpad disabling while typing.

To change these settings in **GNOME 3** or **XFCE 4**:

1.  Open *System Settings*.
2.  Click *Mouse and Touchpad*.
3.  Change the settings on the *Touchpad* tab.

To change these settings in **Cinnamon**:

1.  Open *Cinnamon System Settings*.
2.  Click *Mouse and Touchpad*.
3.  Change the settings on the *Touchpad* tab.

GNOME settings daemon may override existing settings (for example ones set in `xorg.conf.d`) for which there is no equivalent in any of the graphical configuration utilities. It is possible to stop GNOME from touching mouse settings at all:

1.  Run `dconf-editor`
2.  Edit `/org/gnome/settings-daemon/plugins/mouse/` (or `/org/cinnamon/settings-daemon/plugins/mouse/` for cinnamon)
3.  Uncheck the **active** setting

It will now respect your system's existing synaptics configuration.

**Remember**: Since GNOME works on a user by user basis, when you run *dconf-editor* this should be done in your current user session. Repeat this procedure for each and every user you have for this computer.

### MATE

As with [GNOME](/index.php/GNOME "GNOME"), it is possible configure the way MATE handles the touchpad:

1.  Run `dconf-editor`
2.  Edit the keys in the `org.mate.peripherals-touchpad` folder.

To prevent Mate settings daemon from overriding existing settings, do as follows:

1.  Run `dconf-editor`
2.  Edit `org.mate.SettingsDaemon.plugins.mouse`
3.  Uncheck the **active** setting.

## Advanced configuration

### Using xinput to determine touchpad capabilities

Depending on your model, synaptic touchpads may have or lack capabilities. We can determine which capabilities your hardware supports by using `xinput`.

*   left, middle and right hardware buttons
*   two finger detection
*   three finger detection
*   configurable resolution

First, find the name of your touchpad:

```
$ xinput -list

```

You can now use `xinput` to find your touchpad's capabilities:

```
$ xinput list-props "SynPS/2 Synaptics TouchPad" | grep Capabilities

      Synaptics Capabilities (309):  1, 0, 1, 0, 0, 1, 1

```

From left to right, this shows:

*   (1) device has a physical left button
*   (0) device does not have a physical middle button
*   (1) device has a physical right button
*   (0) device does not support two-finger detection
*   (0) device does not support three-finger detection
*   (1) device can configure vertical resolution
*   (1) device can configure horizontal resolution

Use `xinput list-props "SynPS/2 Synaptics TouchPad"` to list all device properties.

### Synclient

Synclient can configure every option available to the user as documented in `$ man synaptics`. A full list of the current user settings can be brought up:

```
$ synclient -l

```

Every listed configuration option can be controlled through synclient, for example:

*   Enable palm detection: `$ synclient PalmDetect=1`
*   Configure button events (right button event for two finger tap here): `$ synclient TapButton2=3`
*   Disable the touchpad: `$ synclient TouchpadOff=1`

After you have successfully tried and tested your options through synclient, you can make these changes permanent by adding them to `/etc/X11/xorg.conf.d/50-synaptics.conf`.

### evtest

The tool [evtest](https://www.archlinux.org/packages/?name=evtest) can display pressure and placement on the touchpad in real-time, allowing further refinement of the default Synaptics settings. The evtest monitoring can be started with:

```
$ evtest /dev/input/event*X*

```

*X* denotes the touchpad's ID. It can be found by looking at the output of `cat /proc/bus/input/devices`.

evtest needs exclusive access to the device which means it cannot be run together with an X server instance. You can either kill the X server or run evtest from a different virtual terminal (e.g., by pressing `Ctrl+Alt+2`).

### xev

The tool [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) can display taps, clicks, pressure, placement and other measured parameters in real-time, allowing still further refinement of the default Synaptics settings. xev can be run in X and needs no specifics. using the "-event" parameter, it is possible to restrict the types of events that are reported.

### Circular Scrolling

Circular scrolling is a feature that Synaptics offers which closely resembles the behaviour of iPods. Instead of (or additional to) scrolling horizontally or vertically, you can scroll circularly. Some users find this faster and more precise. To enable circular scrolling, add the following options to the touchpad device section of `/etc/X11/xorg.conf.d/50-synaptics.conf`:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
    ...
    Option      "CircularScrolling"          "on"
    Option      "CircScrollTrigger"          "0"
    ...
EndSection

```

The option **CircScrollTrigger** may be one of the following values, determining which edge circular scrolling should start:

```
0    All Edges
1    Top Edge
2    Top Right Corner
3    Right Edge
4    Bottom Right Corner
5    Bottom Edge
6    Bottom Left Corner
7    Left Edge
8    Top Left Corner

```

Specifying something different from zero may be useful if you want to use circular scrolling in conjunction with horizontal and/or vertical scrolling. If you do so, the type of scrolling is determined by the edge you start from.

To scroll fast, draw small circles in the center of your touchpad. To scroll slowly and more precise, draw large circles.

### Natural scrolling

It is possible to enable natural scrolling through synaptics. Simply use negative values for `VertScrollDelta` and `HorizScrollDelta` like so:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
    ...
    Option      "VertScrollDelta"          "-111"
    Option      "HorizScrollDelta"         "-111"
    ...
EndSection

```

### Software toggle

You might want to turn the touchpad on and off with a simple button click or shortcut. This can be done by binding the following *xinput*-based script to a keyboard event as explained in [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg"):

 `/usr/local/bin/touchpad_toggle.sh` 
```
#!/bin/bash

declare -i ID
ID=`xinput list | grep -Eio 'touchpad\s*id\=[0-9]{1,2}' | grep -Eo '[0-9]{1,2}'`
declare -i STATE
STATE=`xinput list-props $ID|grep 'Device Enabled'|awk '{print $4}'`
if [ $STATE -eq 1 ]
then
    xinput disable $ID
    # echo "Touchpad disabled."
    # notify-send 'Touchpad' 'Disabled' -i /usr/share/icons/Adwaita/48x48/devices/input-touchpad.png
else
    xinput enable $ID
    # echo "Touchpad enabled."
    # notify-send 'Touchpad' 'Enabled' -i /usr/share/icons/Adwaita/48x48/devices/input-touchpad.png
fi

```

**Tip:** When using external monitors with [bumblebee](/index.php/Bumblebee "Bumblebee"), the touchpad can be configured on the second X server by prepending `DISPLAY=:8` to the command.

Alternatively, `synclient` can be used to toggle the touchpad. However, it can only turn off touch events but not physical clickpad button usage:

 `/usr/local/bin/touchpad.sh` 
```
#!/bin/bash

synclient TouchpadOff=$(synclient -l | grep -c 'TouchpadOff.*=.*0')

```

### Disable trackpad while typing

#### Using the driver's automatic palm detection

First of all you should test if it works properly for your trackpad and if the settings are accurate. Enable palm detection with

```
$ synclient PalmDetect=1

```

Then test the typing. You can tweak the detection by setting the minimum width for the touch to be considered a palm, for example

```
$ synclient PalmMinWidth=8

```

And you can tweak the minimum pressure required for the touch to be considered a palm, for example

```
$ synclient PalmMinZ=100

```

**Tip:** To help find the best values for palm detection, you can use [evtest](https://www.archlinux.org/packages/?name=evtest) to see the width and Z values reported during touchpad use.

Once you have found the correct settings, you can add them to your [config file](#Configuration):

```
Option "PalmDetect" "1"
Option "PalmMinWidth" "8"
Option "PalmMinZ" "100"

```

**Warning:** For some touchpads, an [issue](https://bugzilla.kernel.org/show_bug.cgi?id=77161) with the kernel can cause the palm width to always be reported as 0\. This breaks palm detection in a majority of cases. Pending an actual fix, you can [patch](https://gist.github.com/silverhammermba/a231c8156ecaa63c86f1) the synaptics package to use only Z for palm detection.

**Tip:** If you experience problems with consistent palm detection for your hardware, an alternative to try is [libinput](/index.php/Libinput "Libinput").

#### Using syndaemon

`syndaemon` monitors keyboard activity and disables the touchpad while typing. It has several options to control when the disabling occurs. View them with

```
$ syndaemon -h

```

For example, to disable tapping and scrolling for 2 seconds after each keypress (ignoring modifier keys like Ctrl), use

```
$ syndaemon -i 2 -t -k 

```

Once you have determined the options you like, you should use your login manager or [xinitrc](/index.php/Xinitrc "Xinitrc") to have it run automatically when X starts. The `-d` option will make it start in the background as a daemon.

### Disable touchpad on mouse detection

With the assistance of [udev](/index.php/Udev "Udev"), it is possible to automatically disable the touchpad if an external mouse has been plugged in. To achieve this, use one of the following rules.

#### Basic desktop

This is a basic rule generally for non-"desktop environment" sessions:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="add", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/synclient TouchpadOff=1"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="remove", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/*username*/.Xauthority", RUN+="/usr/bin/synclient TouchpadOff=0"
```

#### GDM

GDM usually stores the Xauthority files in `/var/run/gdm` in a randomly-named directory. You should find your actual path to the Xauthority file which can be done using `ps ax`. For some reason multiple authority files may appear for a user, so a rule like will be necessary:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="add", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print0 -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=1"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="remove", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print0 -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/usr/bin/synclient TouchpadOff=0"
```

Furthermore, you should validate that your udev script is running properly! You can check for the conditions using `udevadm monitor -p` which must be run as root.

##### With syndeamon running

`syndaemon` whether started by the [user](#Using_syndaemon) or the desktop environment can conflict with synclient and will need to be disabled. A rule like this will be needed:

 `/etc/udev/rules.d/01-touchpad.rules`  `SUBSYSTEM=="input", KERNEL=="mouse[0-9]", ACTION=="add", PROGRAM="/usr/bin/find /var/run/gdm -name *username* -print -quit", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="$result/database", RUN+="/bin/sh -c '/usr/bin/synclient TouchpadOff=1 ; sleep 1; /bin/killall syndaemon; '"` 

##### touchpad-state

An AUR package [touchpad-state-git](https://aur.archlinux.org/packages/touchpad-state-git/) has been created around the udev rules above. It includes a udev rule and script:

```
touchpad-state [--off] [--on]

```

#### KDE

If using KDE, the package [kcm-touchpad](https://www.archlinux.org/packages/?name=kcm-touchpad) can be set to disable the touchpad on mouse detection.

If using Plasma, the package [kcm-touchpad-frameworks](https://www.archlinux.org/packages/?name=kcm-touchpad-frameworks) can be used to manage the touchpad.

#### System with multiple X sessions

For an environment where multiple users are present, a slightly different approach is needed to detect the current users X environment. This script will help achieving this:

 `/usr/bin/mouse-pnp-event-handler.sh` 
```
#!/bin/sh
## $1 = "add" / "remove"
## $2 = %k from udev 

## Set TRACKPAD_NAME according to your configuration. 
## Check your trackpad name with: 
## find /sys/class/input/ -name mouse* -exec udevadm info -a {} \; | grep 'ATTRS{name}'
TRACKPAD_NAME="SynPS/2 Synaptics TouchPad"

USERLIST=$(w -h | cut -d' ' -f1 | sort | uniq)
MOUSELIST=$(find /sys/class/input/ -name mouse*)

for CUR_USER in ${USERLIST}; do
         CUR_USER_XAUTH="$(sudo -Hiu ${CUR_USER} env | grep -e "^HOME=" | cut -d'=' -f2)/.Xauthority"

        ## Can't find a way to get another users DISPLAY variable from an isolated root environment. Have to set it manually.
        #CUR_USER_DISPL="$(sudo -Hiu ${CUR_USER} env | grep -e "^DISPLAY=" | cut -d'=' -f2)"
        CUR_USER_DISPL=":0"

        export XAUTHORITY="${CUR_USER_XAUTH}"
        export DISPLAY="${CUR_USER_DISPL}"

        if [ -f "${CUR_USER_XAUTH}" ]; then
                case "$1" in
                        "add")
                                /usr/bin/synclient TouchpadOff=1
                                /usr/bin/logger "USB mouse plugged. Disabling touchpad for $CUR_USER. ($XAUTHORITY - $DISPLAY)"
                        ;;
                        "remove")
                                ## Only execute synclient if there are no external USB mice connected to the system.
                                EXT_MOUSE_FOUND="0"
                                for CUR_MOUSE in ${MOUSELIST}; do
                                        if [ "$(cat ${CUR_MOUSE}/device/name)" != "${TRACKPAD_NAME}" ]; then
                                                EXT_MOUSE_FOUND="1"
                                        fi
                                done
                                if [ "${EXT_MOUSE_FOUND}" == "0" ]; then
                                        /usr/bin/synclient TouchpadOff=0
                                        /usr/bin/logger "No additional external mice found. Enabling touchpad for $CUR_USER."
                                else
                                        logger "Additional external mice found. Won't enable touchpad yet for $CUR_USER."
                                fi
                        ;;
                esac
        fi
done

```

Update the `TRACKPAD_NAME` variable for your system configuration. Run `find /sys/class/input/ -name mouse* -exec udevadm info -a {} \; | grep 'ATTRS{name}'` to get a list of useful mice-names. Choose the one for your trackpad.

Then have udev run this script when USB mices are plugged in or out, with these udev rules:

 `/etc/udev/rules.d/01-touchpad.rules` 
```
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="add", RUN+="/usr/bin/mouse-pnp-event-handler.sh add %k"
SUBSYSTEM=="input", KERNEL=="mouse[0-9]*", ACTION=="remove", RUN+="/usr/bin/mouse-pnp-event-handler.sh remove %k"
```

### Buttonless touchpads (aka ClickPads)

Ever more laptops have a special kind of touchpad which has a single mouse button as part of the tracking plate, instead of external buttons. For example, the 2015 Dell XPS 13, HP series 4500 ProBooks, ThinkPad X220 and X1 ThinkPad series have this kind of a touchpad. By default, the whole button area is detected as a left button, so right and middle-click functions and click + drag will not work. It is possible to define two and three finger clicks as right and middle button clicks, and/or to define parts of the click pad surface as right and middle buttons. Note that although the driver registers multiple touches, it does not track individual fingers (as of version 1.7.1) which results in confusing behavior when using physical buttons of a clickpad for drag-and-drop and other gestures: you have to click with two or three fingers but then only move one of them while holding the button down with another. You can look into the [xf86-input-mtrack](https://aur.archlinux.org/packages/xf86-input-mtrack/) driver for better multitouch support.

Some desktop environments (KDE and GNOME at least) define sane and useful default configurations for clickpads, providing a right button at the bottom right of the pad, recognising two and three-finger clicks anywhere on the pad as right and middle clicks, and providing configuration options to define two and three-finger taps as right and middle clicks. If your desktop does not do this, or if you want more control, you can modify the touchpad section in `/etc/X11/xorg.conf.d/50-synaptics.conf` (or better, of your custom synaptics configuration file prefixed with a higher number). For example:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
        # Enable clickpad/multitouch support
        Option "ClickPad" "true"
        # Middle-button emulation is not supported
        Option "EmulateMidButtonTime" "0"
        # Define right soft button at the bottom
        Option "SoftButtonAreas"  "50% 0 82% 0 0 0 0 0"
EndSection

```

The format for the SoftButtonAreas option is (from `man 4 synaptics`):

 `RightButtonAreaLeft RightButtonAreaRight RightButtonAreaTop RightButtonAreaBottom  MiddleButtonAreaLeft MiddleButtonAreaRight MiddleButtonAreaTop MiddleButtonAreaBottom` 

The above "SoftButtonAreas" option is commonly found in documentation or synaptics packages, and it defines the right half of the bottom 18% of the touchpad as a right button. There is **no middle button** defined. If you want to define a middle button remember one key piece of information from the manual; **edge set to 0 extends to infinity in that direction.**

In the following example the right button will occupy the rightmost 40% of the button area and the middle button 20% of it in the center. The leftmost 40% remains as a left button (as does the rest of the clickpad):

```
...
Option     "SoftButtonAreas"  "60% 0 82% 0 40% 59% 82% 0"
...

```

You can use `synclient` to check the soft button areas:

 `$ synclient -l | grep -i ButtonArea` 
```
        RightButtonAreaLeft     = 3914
        RightButtonAreaRight    = 0
        RightButtonAreaTop      = 3918
        RightButtonAreaBottom   = 0
        MiddleButtonAreaLeft    = 3100
        MiddleButtonAreaRight   = 3873
        MiddleButtonAreaTop     = 3918
        MiddleButtonAreaBottom  = 0

```

If your buttons are not working, soft button areas are not changing, ensure you do not have a synaptics configuration file distributed by a package which is overriding your custom settings (ie. some AUR packages distribute configurations prefixed with very high numbers).

These settings cannot be modified on the fly with `synclient`, however, `xinput` works:

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Soft Button Areas" 4000 0 4063 0 3000 4000 4063 0

```

You cannot use percentages with this command, so look at `/var/log/Xorg.0.log` to figure out the touchpad x and y-axis ranges.

#### Bottom edge correction

In some cases, for example Toshiba Satellite P50, everything work out of the box except often your click are seen as mouse movement and the cursor will jump away just before registering the click. This can be easily solved running

```
$ synclient -l | grep BottomEdge

```

take the BottomEdge value and subtract a the wanted height of your button, then temporary apply with

```
$ synclient AreaBottomEdge=4000

```

when a good value has been found make it a fixed correction with

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
...
Option "AreaBottomEdge"         "4000"
...

```

**Note:** The area will not act as touchpad if the touch **begins** in that area, but it can still be used if the touch has originated outside.

## Troubleshooting

### Touchpad does not work after resuming from hibernate/suspend

Occasionally touchpads will fail to work when the computer resumes from sleep or hibernation. This can often be corrected without rebooting by

*   Switching to a console and back again,
*   entering sleep mode again, and resuming again, or
*   locating the correct kernel module, then removing it and inserting it again.

**Note:** You can use Ctrl-Alt-F1 through F8 to switch to a console without using the mouse.

```
modprobe -r psmouse #psmouse happens to be the kernel module for my touchpad (Alps DualPoint)
modprobe psmouse

```

Now switch back to the tty that X is running on. If you chose the right module, your touchpad should be working again.

### xorg.conf.d/50-synaptics.conf does not seem to apply under GNOME and MATE

[GNOME](/index.php/GNOME "GNOME") and [MATE](/index.php/MATE "MATE"), by default, will overwrite various options for your touch-pad. This includes configurable features for which there is no graphical configuration within GNOME's system control panel. This may cause it to appear that `/etc/X11/xorg.conf.d/50-synaptics.conf` is not applied. Please refer to the GNOME section in this article to prevent this behavior.

*   [#GNOME/Xfce4/Cinnamon](#GNOME.2FXfce4.2FCinnamon)

### The touchpad is not working, Xorg.0.log shows "Query no Synaptics: 6003C8"

Due to the way synaptics is currently set-up, 2 instances of the synaptics module are loaded. We can recognize this situation by opening the xorg log file (`/var/log/Xorg.0.log`) and noticing this:

 `/var/log/Xorg.0.log` 
```
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "evdev touchpad catchall"
 [ 9304.803] (**) SynPS/2 Synaptics TouchPad: Applying InputClass "touchpad catchall"

```

Notice how 2 differently named instances of the module are being loaded. In some cases, this causes the touchpad to become nonfunctional.

We can prevent this double loading by adding `MatchDevicePath "/dev/input/event*"` to our `/etc/X11/xorg.conf.d/50-synaptics.conf` file:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
    Identifier "touchpad catchall"
    Driver "synaptics"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
        Option "TapButton1" "1"
        Option "TapButton2" "2"
        Option "TapButton3" "3"
EndSection 

```

Restart X and check xorg logs again, the error should be gone and the touchpad should be functional.

related bugreport: [FS#20830](https://bugs.archlinux.org/task/20830)

related forum topics:

*   [https://bbs.archlinux.org/viewtopic.php?id=104769](https://bbs.archlinux.org/viewtopic.php?id=104769)
*   [https://bbs.archlinux.org/viewtopic.php?pid=825690](https://bbs.archlinux.org/viewtopic.php?pid=825690)

### Touchpad detected as "PS/2 Generic Mouse" or "Logitech PS/2 mouse"

This can be caused by a number of issues;

#### Elantech touchpads

This can happen with some laptops with an Elantech touchpad, for example the ASUS x53s. In this situation you need [psmouse-alps-driver](https://aur.archlinux.org/packages/psmouse-alps-driver/) package from [AUR](/index.php/AUR "AUR").

#### Laptops with touchscreen & touchpad

There also seems to be a problem with laptops which have both a touchscreen & a touchpad, such as the Dell XPS 12 or Dell XPS 13\. To fix this, you can [blacklist](/index.php/Blacklisting "Blacklisting") the `i2c_hid` driver, this does have the side-effect of disabling the touchscreen though.

This [seems to be a known problem](http://www.spinics.net/lists/linux-input/msg27768.html). Also see [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1419078).

Post kernel 3.15, having the module blacklisted may cause touchpad to stop working completely. Removing the blacklist should allow this to start working with limited functionality, see [FS#40921](https://bugs.archlinux.org/task/40921).

### Non-functional Synaptics special abilities (multi-tap, scrolling, etc.)

In some cases Synaptics touchpads only work partially. Features like two-finger scrolling or two-finger middle-click do not work even if properly enabled. This is probably related to the [The touchpad is not working](#The_touchpad_is_not_working.2C_Xorg.0.log_shows_.22Query_no_Synaptics:_6003C8.22) problem mentioned above. Fix is the same, prevent double module loading.

If preventing the module from loading twice does not solve your issue, try commenting out the toggle "MatchIsTouchpad" (which is now included by default in the synaptics config).

If clicking with either 2 or 3 fingers is interpreted as a right-click, so you cannot get a middle click either way regardless of configuration, this bug is probably the culprit: [https://bugs.freedesktop.org/show_bug.cgi?id=55365](https://bugs.freedesktop.org/show_bug.cgi?id=55365)

### Cursor jump

Some users have their cursor inexplicably *jump* around the screen. There currently no patch for this, but the developers are aware of the problem and are working on it.

Another posibility is that you are experiencing *IRQ losses* related to the i8042 controller (this device handles the keyboard and the touchpad of many laptops), so you have two posibilities here:

1\. rmmod && insmod the psmouse module. 2\. append i8042.nomux=1 to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") and reboot your machine.

### Touchpad device is not located at `/dev/input/*`

If that is the case, you can use this command to display information about your input devices:

```
$ cat /proc/bus/input/devices

```

Search for an input device which has the name "SynPS/2 Synaptics TouchPad". The "Handlers" section of the output specifies what device you need to specify.

**Example output:**

 `$ cat /proc/bus/input/devices` 
```
 I: Bus=0011 Vendor=0002 Product=0007 Version=0000
 N: Name="SynPS/2 Synaptics TouchPad"
 P: Phys=isa0060/serio4/input0
 S: Sysfs=/class/input/input1
 H: Handlers=mouse0 event1
 B: EV=b
 B: KEY=6420 0 7000f 0

```

In this case, the `Handlers` are `mouse0` and `event1`, so `/dev/input/mouse0` would be used.

### Firefox and special touchpad events

You can enable/disable some special events that Firefox handles upon tapping or scrolling certain parts of your touchpad by editing the settings of those actions. Type **about:config** in your Firefox address bar. To alter options, double-click on the line in question.

#### Firefox 17.0 and later

Horizontal scrolling will now by default scroll through pages and not through your history. To reenable Mac-style forward/backward with two-finger swiping, edit:

```
mousewheel.default.action.override_x = 2

```

You may encounter accidental forwards/backwards while scrolling vertically. To change Firefox's sensitivity to horizontal swipes, edit:

```
mousewheel.default.delta_multiplier_x

```

The optimum value will depend on your touchpad and how you use it, try starting with `10`. A negative value will reverse the swipe directions.

### Opera: horizontal scrolling issues

Same as above. To fix it, go to *Tools > Preferences > Advanced > Shortcuts*. Select "Opera Standard" mouse setup and click "Edit". In "Application" section:

*   assign key "Button 6" to command "Scroll left"
*   assign key "Button 7" to command "Scroll right"

### Scrolling and multiple actions with Synaptics on LG laptops

These problems seem to be occurring on several models of LG laptops. Symptoms include: when pressing Mouse Button 1, Synaptics interprets it as ScrollUP and a regular button 1 click; same goes for button 2.

The scrolling issue can be resolved by entering in `xorg.conf`:

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option "UpDownScrolling" "0"` 
**Note:** This will make Synaptics interpret one button push as three. There is a patch written by Oskar Sandberg[[1]](http://www.math.chalmers.se/~ossa/linux/lg_tx_express.html) that removes these clicks.

Apparently, when trying to compile this against the latest version of Synaptics it fails. The solution to this is using the GIT repository for Synaptics[[2]](http://web.telia.com/~u89404340/touchpad/synaptics/.git).

There is also a package build file in the AUR to automate this: [xf86-input-synaptics-lg](https://aur.archlinux.org/packages/xf86-input-synaptics-lg/).

To build the package after downloading the tarball and unpacking it, execute:

```
$ cd synaptics-git
$ makepkg

```

### Other external mouse issues

First, make sure your section describing the external mouse contains this line (or that the line looks like this):

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option     "Device" "/dev/input/mice"` 

If the "Device" line is different, change it to the above and try to restart X. If this does not solve your problem, make your **touchpad** is the CorePointer in the "Server Layout" section:

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "Touchpad" "CorePointer"` 

and make your external device "SendCoreEvents":

 `/etc/X11/xorg.conf.d/xorg.conf`  `InputDevice    "USB Mouse" "SendCoreEvents"` 

finally add this to your external device's section:

 `/etc/X11/xorg.conf.d/xorg.conf`  `Option      "SendCoreEvents"    "true"` 

If all of the above does not work for you, please check relevant bug trackers for possible bugs, or go through the forums to see if anyone has found a better solution.

### Touchpad synchronization issues

Sometimes the cursor may freeze for several seconds or start acting on its own for no apparent reason. This behavior is accompanied by records in `/var/log/messages.log`

 `/var/log/messages.log`  `psmouse.c: TouchPad at isa0060/serio1/input0 lost synchronization, throwing 3 bytes away` 

This problem has no general solution, but there are several possible workarounds.

*   If you use CPU frequency scaling, avoid using the "ondemand" governor and use the "performance" governor when possible, as the touchpad may lose sync when the CPU frequency changes.
*   Avoid using an ACPI battery monitor.
*   Attempt to load psmouse with "proto=imps" option. To do that, add this line to your `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf`  `options psmouse proto=imps` 

*   Try another desktop environment. Some users report that this problem only occurs when using XFCE or GNOME, for whatever reason

### Xorg.log.0 shows SynPS/2 Synaptics touchpad can not grab event device, errno=16

If you are using Xorg 7.4, you may get a warning like this from `/var/log/Xorg.0.log`, thais is because the driver will grab the event device for exclusive use when using the Linux 2.6 event protocol. When it fails, X will return this error message.

Grabbing the event device means that no other user space or kernel space program sees the touchpad events. This is desirable if the X config file includes `/dev/input/mice` as an input device, but is undesirable if you want to monitor the device from user space.

If you want to control it, add or modify the "GrabEventDevice" option in you touchpad section in `/etc/X11/xorg.conf.d/50-synaptics.conf`:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
...
Option "GrabEventDevice" "*boolean*"
...
```

This will come into effect when X is restarted, though you can also change it by using synclient. When changing this parameter with the synclient program, the change will not take effect until the Synaptics driver is disabled and re-enabled. This can be achieved by switching to a text console and then switching back to X.

### Synaptics loses multitouch detection after rebooting from Windows

Many drivers include a firmware that is loaded into flash memory when the computer boots. This firmware is not necessarily cleared upon shutdown, and is not always compatible with Linux drivers. The only way to clear the flash memory is to shutdown completely rather than using reboot. It is generally considered best practice to never use reboot when switching between operating systems.

### Touchpad not recognized after shutdown from Arch

Certain touchpads (elantech in particular) will fail to be recognized as a device of any sort after a standard shutdown from Arch linux. There are multiple possible solutions to this problem:

*   Boot into a Windows partition/install disk and shutdown from there.
*   Wait approximately 1 minute before turning on the computer after shutdown.
*   As discussed in [https://bugzilla.kernel.org/show_bug.cgi?id=81331#c186](https://bugzilla.kernel.org/show_bug.cgi?id=81331#c186) a patch has been merged into the stable kernel that provides a fix for Elantech touchpads. Gigabyte P34, P35v2 and X3 models are supported by default, for others (especially rebranded Gigabyte laptops, like XMG's) `i8042.kbdreset=1` can be set as kernel parameter.

### Trackpoint and Clickpad

Newer Thinkpads do not have physical buttons for their Trackpoint anymore and instead use the upper area of the Clickpad for buttons (Left, Middle, Right). Apart from the ergonomic viewpoint this works quite well with current Xorg. Unfortunately mouse wheel emulation using the middle button is not supported yet. Install [xf86-input-evdev-trackpoint](https://aur.archlinux.org/packages/xf86-input-evdev-trackpoint/) from the AUR for a patched and properly configured version if you intend to use the Trackpoint.

### ASUS Touchpads only recognised as PS/2 FocalTech emulated mouse

1.  Install the linux header for your kernel
2.  Install the focaltech-dkms from [https://github.com/hanipouspilot/focaltech-dkms](https://github.com/hanipouspilot/focaltech-dkms)
3.  Restart your computer
4.  Edit your settings in the "Mouse and Trackpad" settings.

## See also

*   [Synaptics touchpad driver](http://cgit.freedesktop.org/xorg/driver/xf86-input-synaptics/)
*   [Synaptics manual on x.org](http://www.x.org/archive/X11R7.5/doc/man/man4/synaptics.4.html)