# Tablet PC

Here are some hints for getting Arch Linux working on your tablet PC. These instructions contain information for getting the stylus, stylus rotation, and screen rotation to work properly on a tablet PC.

## Contents

*   [1 Models](#Models)
*   [2 Stylus](#Stylus)
*   [3 Rotation](#Rotation)
    *   [3.1 XFCE: Stylus and screen rotation](#XFCE:_Stylus_and_screen_rotation)
    *   [3.2 Touchscreen rotation](#Touchscreen_rotation)
*   [4 Automatic rotation](#Automatic_rotation)
    *   [4.1 With a script](#With_a_script)
    *   [4.2 With systemd](#With_systemd)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 CellWriter](#CellWriter)
    *   [5.2 Easystroke](#Easystroke)
        *   [5.2.1 Launch CellWriter under pen](#Launch_CellWriter_under_pen)
        *   [5.2.2 Gestures for the Alphabet](#Gestures_for_the_Alphabet)
    *   [5.3 Xournal](#Xournal)
    *   [5.4 Disable gksu grab mode](#Disable_gksu_grab_mode)
    *   [5.5 Gnome-screensaver](#Gnome-screensaver)
    *   [5.6 GDM](#GDM)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Wacom Drivers](#Wacom_Drivers)
    *   [6.2 Screen Rotation](#Screen_Rotation)

## Models

Intel (x86) tablets that are known to work (well) with Arch:

*   [Samsung Series 7 Slate XE700T1A](/index.php/Samsung_Series_7_Slate_XE700T1A "Samsung Series 7 Slate XE700T1A")
*   [Microsoft Surface Pro 3](/index.php/Microsoft_Surface_Pro_3 "Microsoft Surface Pro 3")

## Stylus

First [install](/index.php/Install "Install") [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom).

Then add the following lines to the **ServerLayout** section of the [Xorg](/index.php/Xorg "Xorg") configuration file `/etc/X11/xorg.conf`:

```
InputDevice    "stylus" "SendCoreEvents"
InputDevice    "eraser" "SendCoreEvents"
InputDevice    "cursor" "SendCoreEvents"

```

As well as the following sections:

```
Section "InputDevice"
    Identifier     "stylus"
    Driver         "wacom"
    Option         "Device" "/dev/ttyS0"
    Option         "Type" "stylus"
    Option         "ForceDevice" "ISDV4"
    Option         "Button2" "3"
EndSection

Section "InputDevice"
    Identifier     "eraser"
    Driver         "wacom"
    Option         "Device" "/dev/ttyS0"
    Option         "Type" "eraser"
    Option         "ForceDevice" "ISDV4"
    Option         "Button2" "3"
EndSection

Section "InputDevice"
    Identifier     "cursor"
    Driver         "wacom"
    Option         "Device" "/dev/ttyS0"
    Option         "Type" "cursor"
    Option         "ForceDevice" "ISDV4"
EndSection

```

## Rotation

Unless you are running a very old Xserver, rotation capabilities (included in [xrandr](/index.php/Xrandr "Xrandr")) should already be on by default. If not, you can enable xrandr by adding the following option to the **Screen** section of the xorg.conf file.

```
Option         "RandRRotation" "on"

```

Save the file and restart the xserver for changes to take effect.

### XFCE: Stylus and screen rotation

The following script will rotate the display 90 degrees clockwise every time it is executed. It will also rotate the wacom pointer so that the stylus will still work.

 `rotate.sh` 

```
#!/bin/bash

case $(xfconf-query -c pointers -p /Wacom_ISDv4_90_Pen_stylus/Properties/Wacom_Rotation) in
    2)  # Currently top is rotated left, we should set it normal (0°)
          xrandr -o 0
          xfconf-query -c pointers -p /Wacom_ISDv4_90_Pen_stylus/Properties/Wacom_Rotation -s 0
          xfconf-query -c xsettings -p /Xft/RGBA -s rgb
          ;;
    0)  # Screen is not rotated, we should rotate it right (90°)
           xrandr -o 3
           xfconf-query -c pointers -p /Wacom_ISDv4_90_Pen_stylus/Properties/Wacom_Rotation -s 1
           xfconf-query -c xsettings -p /Xft/RGBA -s vbgr
           ;;
    1)    # Top of screen is rotated right, we should invert it (180°)
           xrandr -o 2
           xfconf-query -c pointers -p /Wacom_ISDv4_90_Pen_stylus/Properties/Wacom_Rotation -s 3
           xfconf-query -c xsettings -p /Xft/RGBA -s bgr
           ;;
    3)  # Screen is inverted, we should rotate it left (270°)
           xrandr -o 1
           xfconf-query -c pointers -p /Wacom_ISDv4_90_Pen_stylus/Properties/Wacom_Rotation -s 2
           xfconf-query -c xsettings -p /Xft/RGBA -s vrgb
           ;;
    *)
           echo "Unknown result from 'xfconf-query -c pointers -p /Wacom_ISDv4_90_Pen_stylus/Properties/Wacom_Rotation'" >&2
           exit 1
           ;;
esac

```

Save the file and make it executable:

```
chmod +x rotate.sh

```

You can create a link to it on your desktop or panel, or link it to a keyboard shortcut or special button on your tablet.

### Touchscreen rotation

[Grox](https://github.com/yourealwaysbe/grox) is a simple script for rotating a touchscreen absolutely or by relative increments. It only uses xrandr to query the current state, rather than XFCE-specific features.

## Automatic rotation

### With a script

The following python script was developed to automatic rotate the screen and the touchscreen. Furthermore, it disable the touchpad for inverted, right, and left orientation, and supports automatic detection of accelerometers, touchscreens, and touchpad devices.

It works for devices with an accelerometer communicating through the industrial I/O subsystem `/sys/bus/iio/devices/iio:deviceX`, where X is the number of the device. Usually, it is necessary to change the following parameters dpath, devicename, and touchpad.

See [rotate.py](https://gist.githubusercontent.com/ei-grad/4d9d23b1463a99d24a8d/raw/rotate.py).

### With systemd

See [iio-sensor-proxy](https://github.com/hadess/iio-sensor-proxy). [iio-sensor-proxy-git](https://aur.archlinux.org/packages/iio-sensor-proxy-git/)<sup><small>AUR</small></sup> is available in the AUR.

## Tips and tricks

### CellWriter

[CellWriter](http://risujin.org/cellwriter/) is a grid-entry natural handwriting input panel. As you write characters into the cells, your writing is instantly recognized at the character level. [cellwriter](https://www.archlinux.org/packages/?name=cellwriter) is available in community repository.

### Easystroke

[Easystroke](http://easystroke.sourceforge.net/) is a gesture recognition application, recognizing gestures by a variety of input devices, to include pen stylus, mouse, and touch. Gestures can be used to launch programs, enter text, emulate buttons and keys, and scroll. Easystroke is available in the AUR: [easystroke-git](https://aur.archlinux.org/packages/easystroke-git/)<sup><small>AUR</small></sup>.

#### Launch CellWriter under pen

One useful application of Easystroke is to use it to launch CellWriter right below your mouse pointer.

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Script dump, in-code comments (Discuss in [Talk:Tablet PC#](https://wiki.archlinux.org/index.php/Talk:Tablet_PC))

**Note:** This script requires the [xdotool](https://www.archlinux.org/packages/?name=xdotool) package, which is not installed by default.

```
#!/bin/bash
# Original author: mr_deimos (ubuntuforums.org). February 14, 2010
# Many bugs fixed and improvements made by Ben Wong.  October 20, 2010

# This script toggles the cellwriter letter recognizer window.
# If a cellwriter window is visible, it will be hidden.
# If cellwriter is not already running, this will create a new process.
# If coordinates are specified, the window pops up at those coordinates. 
# If coordinates are not specified, the window is toggled, but not moved.

# Implementation Note: this script is trickier than it should be
# because cellwriter does two stupid things. First, it has no
# --get-state option, so we can't tell if it is hidden or not. Second,
# both the notification area applet and the actual program window have
# the same window name in X, which means we can't simply use xwininfo
# to find out if it is showing or not. 
#
# (Of course, we wouldn't have to be doing this crazy script at all,
# if cellwriter had a --toggle-window option to toggle showing the
# keyboard, but that's another rant...)
#
# To work around the problem, we'll assume that if the window we got
# information about from xwininfo is smaller than 100 pixels wide, it
# must be an icon in the notification area. This may be the wrong
# assumption, but, oh well...

if [[ "$1" == "-v" || "$1" == "--verbose" ]]; then
    verbose=echo
    shift
else
    verbose=:
fi

if [[ "$1" && -z "$2"  ||  "$1" == "-h"  ||  "$1" == "--help" ]] ; then 
    cat >&2 <<EOF
$(basename $0): Toggle showing the cellwriter window, optionally moving it."

Usage:  $(basename $0) [x y]"
	Where x and y are the desired position of the cellwriter window."
	If x and y are omitted, the window is not moved."
EOF
    exit 1
fi

if [[ "$1" && "$2" ]]; then
    x=$[$1-20]			# Offset slightly so cursor will be in window 
    y=$[$2-30]
    [ $x -lt 0 ] && x=0		# Minimum value is zero
    [ $y -lt 0 ] && y=0
fi

if ! xwininfo -root >/dev/null; then
    echo "$(basename $0): Error: Could not connect to your X server." >&2
    exit 1
fi

# Try to obtain CellWriter's window id.
# We can't use "xwininfo -name" b/c that might find the notification icon. 
OLDIFS="$IFS"
IFS=$'\n'
for line in $(xwininfo -root -tree | grep CellWriter); do
    line=0x${line#*0x}		# Just to get rid of white space before 0x.
    $verbose -en "Checking: $line\t"
    if [[ $line =~ (0x[A-Fa-f0-9]+).*\)\ *([0-9]+)x([0-9]+) ]]; then
	id=${BASH_REMATCH[1]}
	width=${BASH_REMATCH[2]}
	height=${BASH_REMATCH[3]}
	if [[ $width -gt 100 ]]; then
	    $verbose "looks good."
	    CW_WIN_ID=$id
	    break;
	else
	    $verbose "too small, ignoring."
	fi
    else
	echo "BUG: The xwininfo regular expression in $0 is broken." >&2
    fi
done
IFS="$OLDIFS"

#Check if Cellwriter's window is visible
if [ "$CW_WIN_ID" ] ; then
    CW_MAP_STATE=`xwininfo -id "$CW_WIN_ID"|grep "Map State"|cut -f 2 -d :`
else
    $verbose "Can't find cellwriter window, checking for a running process..."
    if ! pgrep -x cellwriter >& /dev/null; then
	$verbose "No cellwriter process running, starting a new one."
	if [[ "$x" && "$y" ]]; then
	    cellwriter --show-window --window-x=$x --window-y=$y &
	else
	    cellwriter --show-window &
	fi
	exit 0
    else
	$verbose "Found a process, so the window has not been created yet."
	$verbose "Pretending the window is UnMapped."
	CW_MAP_STATE=IsUnMapped
    fi
fi

$verbose "Map state: $CW_MAP_STATE"

case "$CW_MAP_STATE" in

    *IsViewable*)		# Window is currently visible.
	$verbose "hiding window"
	cellwriter --hide-window &
	;;

    *IsUnMapped*)		# Window is currently hidden or non-existent.
	if [[ "$x" && "$y" && "$CW_WIN_ID" ]]; then
	    $verbose "moving window to $x $y"
	    xdotool windowmove $CW_WIN_ID $x $y
	fi
	$verbose "showing window"
	cellwriter --show-window &    # In bg in case cw is not already running
	;;

    *) 				# This will never happen...
	echo "BUG: cellwriter is neither viewable nor unmapped" >&2
	echo "BUG: ...which means this script, $0, is buggy." >&2
	exit 1
	;;
esac

exit 0

```

Save the script as **cellwriter.sh** in either `/usr/local/bin/` or `$HOME/bin`, and give it executable rights:

```
chmod +x cellwriter.sh

```

Then create a gesture in Easystroke tied to the following command:

```
cellwriter.sh $EASYSTROKE_X1 $EASYSTROKE_Y1

```

When you launch it (using the gesture you created), it will open right under your pen.

#### Gestures for the Alphabet

You can also use Easystroke to make gestures for the entire alphabet, replacing much of the need for CellWriter. To avoid having to make seperate gestures for the uppser-case letters, you can use the following [script](http://wwww.ubuntuforums.org/showthread.php?t=837032&page=5#49) to activate the shift key.

**Note:** This script requires the [xautomation](https://www.archlinux.org/packages/?name=xautomation) package, which is not installed by default.

```
#!/bin/bash
if [ -f /tmp/shift ]
then
  xte "keydown Shift_L" "key $1" "keyup Shift_L"
  rm -f /tmp/shift
else
  xte "key $1"
fi

```

Save the script as **keypress.sh** in either `/usr/local/bin/` or `$HOME/bin`, and give it executable rights:

```
chmod +x keypress.sh

```

Then create a gesture in Easystroke tied to the following command:

```
touch /tmp/shift

```

This will activate the shift key. To activate the letter keys, tie your gestures to the following command:

```
keypress.sh $LETTER

```

Replace `$LETTER` with the letter in the alphabet in question.

So, when you want to enter an upper-case letter, use your gesture for the shift key followed by the letter. If you want a lower-case letter, simply use your gesture for the letter.

### Xournal

[Xournal](http://xournal.sourceforge.net/) is an application for notetaking, sketching, and keeping a journal using a stylus. Xournal aims to provide superior graphical quality (subpixel resolution) and overall functionality. [xournal](https://www.archlinux.org/packages/?name=xournal) can be installed from the **extra** repository.

You can also extend the functionality of Xournal with patches, to enable things such as autosaving documents and inserting images. See [SourceForge](http://sourceforge.net/tracker/?group_id=163434&atid=827735) for links to all the available patches. To apply a patch, download the PKGBUILD for Xournal from the [ABS](/index.php/ABS "ABS"), and reference the article [Patching in ABS](/index.php/Patching_in_ABS "Patching in ABS").

### Disable gksu grab mode

**Warning:** This will make it possible for other X applications to listen to keyboard input events, thus making it impossible to shield from malicious applications which may be running, such as keyloggers, etc.

If you are using gksu/gksudo, you can authenticate with the stylus to enter the password by disabling grab mode. In a terminal, run the following command:

```
$ gksu-properties

```

Change the **Grab Mode** to _disable_.

### Gnome-screensaver

To unlock your gnome-screensaver using Cellwriter to enter your password, first start Gconf-editor:

```
$ gconf-editor

```

Under `/apps/gnome-screensaver`, set **embedded_keyboard_command** to _cellwriter --xid --keyboard-only_, and check the **embedded_keyboard_enabled** checkbox.

Alternatively, instead of using the graphical registry editor, you can simply type these into your command line:

```
$ gconftool-2 --set /apps/gnome-screensaver/embedded_keyboard_command "cellwriter --xid --keyboard-only" --type string
$ gconftool-2 --set /apps/gnome-screensaver/embedded_keyboard_enabled true --type boolean

```

If you are administrating a multi-user system and would like to set the system-wide default, you can do so by typing the following:

```
# gconftool-2 --direct --config-source xml:readwrite:/etc/gconf/gconf.xml.defaults --set /apps/gnome-screensaver/embedded_keyboard_command "cellwriter --xid --keyboard-only" --type string
# gconftool-2 --direct --config-source xml:readwrite:/etc/gconf/gconf.xml.defaults --set /apps/gnome-screensaver/embedded_keyboard_enabled true --type boolean

```

### GDM

You can also use CellWriter with GDM. First open `/etc/gdm/Init/Default` as root with a text editor. Then near the bottom of the file, add the lines in **bold** as shown:

```
fi
**cellwriter --keyboard-only &**
exit 0

```

You can add `--window-x` and `--window-y` to adjust the position of CellWriter accordingly. For example:

```
cellwriter --keyboard-only --window-x=512 --window-y=768 &

```

**Note:** You can only use CellWriter with a Plain style GDM.

To start a fully fledged CellWriter instance within the user session, you might want to terminate the instance started with the keyboard-only switch within the gdm context. Add something such as `killall cellwriter` to your newly created file `/etc/gdm/PostLogin/Default`.

**Note:** This works in a single-user setup, if you have a multi-user setup, you might want to develop and post your more elaborate solution.

## Troubleshooting

### Wacom Drivers

These commands are useful in troubleshooting:

```
wacdump -f tpc /dev/ttyS0
xidump -l
xidump -u stylus

```

If xidump shows that your tablet's max resolution is the same as screen resolution, then your wacom driver has rescaled your wacom coordinates to the X server's resolution. To fix this, try recompiling your linuxwacom driver with:

```
./configure --disable-quirk-tablet-rescale

```

### Screen Rotation

Some video drivers do not support rotation. To check if your driver supports rotation, check the output of `xrandr` for the list orientations:

```
normal left inverted right

```

**Note:** The following driver(s) are known not to support rotation: fglrx

Retrieved from "[https://wiki.archlinux.org/index.php?title=Tablet_PC&oldid=409330](https://wiki.archlinux.org/index.php?title=Tablet_PC&oldid=409330)"