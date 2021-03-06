### Use a joystick/gamepad to control applications which accept keyboard commands

I use [joy2key](http://interreality.org/~tetron/technology/joy2key/) to work around issues with the Logitech Cordless RumblePad 2 "hat" (a.k.a. d-pad) in [XBMC](http://xbmc.org/).

XBMC 10.0 or probably a recent Arch update (SDL?) broke the joystick hat functionality for me. On XBMC startup, `xbmc.log` shows 0 hats and 6 - instead of 4 - axes:

```
17:00:36 T:3020363648 M:1703337984  NOTICE: Enabled Joystick: Logitech Logitech Cordless RumblePad 2
17:00:36 T:3020363648 M:1703337984  NOTICE: Details: Total Axis: 6 Total Hats: 0 Total Buttons: 12

```

My solution was to install [joy2key](https://aur.archlinux.org/packages/joy2key/) from the [AUR](/index.php/AUR "AUR"). Here is my config which could potentially save you hours of frustration or fun, depending on how you look at it:

```
#
# ~/.joy2keyrc
#

COMMON
-dev /dev/input/js0
-thresh -16383 16383 -16383 16383 -16383 16383 -16383 16383 -16383 16383 -16383 16383
#-autorepeat 5
#-deadzone 50

START xbmc
-X
# -axis <axis0min> <axis0max> <axis1min> <axis1max> ...
#       0 = left analog stick X-axis
#       1 = left analog stick Y-axis
#       2 = right analog stick X-axis
#       3 = right analog stick Y-axis
#       4 = hat (d-pad) X-axis
#       5 = hat (d-pad) Y-axis
#
# actions: Left/Right/Up/Down (arrow keys) - first letter capital!
#          plus/minus (ASCII characters) - lower case!
#          blank = special
# more info in /usr/include/X11/keysymdef.h
#
# .....0..........1.......2..........3..........4..........5......
#-axis Left Right Up Down minus plus plus minus Left Right Up Down
-axis blank blank blank blank blank blank blank blank Left Right Up Down

# EoF

```

joy2key needs to start **after** XBMC to be able to see its window. Here's my XBMC standalone system config:

```
#
# ~/.xinitrc
#

# Enable Ctrl+Alt+Bksp.
setxkbmap -option terminate:ctrl_alt_bksp &

# Start joy2key after XBMC has been detected running. (Function takes arguments, some optional.)
start_joy2key()
{
  for n in $(seq $4 || seq 5)
  do
    xwininfo -display :0 -name "$1" >/dev/null 2>&1 && joy2key "$1" -config "$2"
    sleep $3 || sleep 3
  done
}
# syntax: start_joy2key <window name> <config file> [wait # of sec between tries] [repeat # of times]
start_joy2key "XBMC Media Center" xbmc 3 5 &

# Start XBMC.
xbmc-standalone

# EoF

```

And here is my joy2key config section for controlling [Boxee-source](/index.php/Boxee-source "Boxee-source"):

```
START boxee
-X
-axis blank blank Page_Up Page_Down blank blank plus minus Left Right Up Down
# .......1.2......3......4.5....6.....7...........8............9.0.1.2
-buttons v Return Escape c Left Right bracketleft bracketright i z s h

```

Add this to `~/.xinitrc` below the XBMC section to alternate between launching XBMC and Boxee:

```
start_joy2key Boxee boxee 3 3 &
/opt/boxee/run-boxee-desktop

```

This gets respawned over and over from `/etc/inittab`:

```
x:5:respawn:/bin/su xbmc -l -c "/bin/bash --login -c /usr/bin/startx >/dev/null 2>&1"

```

References to the sources where I learned about this:

*   [[1]](http://hans.fugal.net/blog/2007/06/02/joystick-hat-in-x-plane-in-linux/) blog entry: *Joystick Hat in X-Plane in Linux*
*   [[2]](http://ubuntuforums.org/showthread.php?t=646564) Ubuntu forum post: *How to use joy2key for SIXAXIS joypad (or any really!)*
*   [[3]](http://wiki.xbmc.org/index.php?title=Installing_XBMC_for_Linux#Autostarting_XBMC) XBMC wiki: *Installing XBMC for Linux > Autostarting XBMC*