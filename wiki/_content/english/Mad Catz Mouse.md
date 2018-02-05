Mad Catz produces a series of gaming mice, for example the Saitek Cyborg R.A.T.3 Mouse (7 buttons USB wired) or the R.A.T9 (7 buttons USB wireless). The mice do not work properly in X without some reconfiguration. This article explains how to make it work with any desktop manager.

## Contents

*   [1 Installation](#Installation)
*   [2 Issues](#Issues)
*   [3 The Disable Button Solution](#The_Disable_Button_Solution)
*   [4 RAT7 or RAT9 Partial Fix](#RAT7_or_RAT9_Partial_Fix)
*   [5 Manual Button Mapping Fix](#Manual_Button_Mapping_Fix)
*   [6 R.A.T. configuration software](#R.A.T._configuration_software)
*   [7 See also](#See_also)

## Installation

No driver installation is required. The mouse should be detected at boot or whenever it is hot-plugged.

**Note:** On some systems the *MatchProduct* string may vary, therefore, you can use the command `xinput list`

## Issues

After being plugged, the mouse will seems to work, but you may experience different issues :

*   You cannot move windows around when grabbing the window's title bar. (happens with [Openbox](/index.php/Openbox "Openbox") and other [Window manager](/index.php/Window_manager "Window manager"))
*   You cannot click on buttons.
*   You cannot get the focus on windows.
*   You cannot open menus, even with keyboard shortcuts.
*   Display does not refresh (using [Xcompmgr](/index.php/Xcompmgr "Xcompmgr"))
*   Closing certain windows restores functionality until the mouse locks into a new window.

## The Disable Button Solution

The issues are caused by an interaction between R.A.T Mode button and the X Server. To restore proper function, the 'Mode' button must be disabled, as follows:

With root privileges, create and edit the file **`/etc/X11/xorg.conf.d/50-vmmouse.conf`** (see [xorg](/index.php/Xorg "Xorg")).

Add the following content :

```
Section "InputDevice"
    Identifier     "Mouse0"
    Driver         "evdev"
    Option         "Name" "Saitek Cyborg R.A.T.3 Mouse"
    Option         "Vendor" "06a3"
    Option         "Product" "0ccc"
    Option         "Protocol" "auto"
    Option         "Device" "/dev/input/event4"
    Option         "Emulate3Buttons" "no"
    Option         "Buttons" "7"
    Option         "ZAxisMapping" "4 5"
    Option         "ButtonMapping" "1 2 3 4 5 6 7 0 0 0 0 0 0 0"
    Option         "Resolution" "3200"
EndSection

```

After restarting your X server, the mouse should be fully functional, including the two lateral buttons. If not, or if you need more informations about configuring gaming mice, see [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

## RAT7 or RAT9 Partial Fix

This is the configuration file that will get your R.A.T. 7 or R.A.T. 9 mouse working properly under linux.

*   Does not fix the change-profile button for RAT9, this profile needs more adjustment or just do not push it.

`/etc/X11/xorg.conf.d/910-rat.conf`:

```
Section "InputClass"
 Identifier "Mouse Remap"
 MatchProduct "Mad Catz Mad Catz M.M.O.7 Mouse"
 MatchIsPointer "true"
 MatchDevicePath "/dev/input/event*"
 Option "Buttons" "24"
 Option "ButtonMapping" "1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24"
 Option "AutoReleaseButtons" "13 14 15"
 Option "ZAxisMapping" "4 5 6 7"
EndSection

```

You can define different keystrokes applied to each mouse button by defining them in `~/.xbindkeysrc` eg.:

```
# pressing mouse button 7 sends keystroke: 2
"xvkbd  -text 2"
       m:0x0 + b:7
# pressing mouse button 8 sends keystroke: Space
"xvkbd  -text "\[SPACE]""
       m:0x0 + b:8
# pressing mouse button 9 sends keystroke: F8
"xvkbd  -text "\[F8]""
       m:0x0 + b:9
# pressing mouse button 10 sends keystroke: CursorLeft
"xvkbd  -text "\[Left]""
       m:0x0 + b:10
# pressing mouse button 11 sends keystroke: Shift+F2
"xvkbd  -text "\[Shift]\[F2]""
       m:0x0 + b:11

```

A very good article on setting up the Mad Catz M.M.O.7 mouse with Linux is written [here](https://delightlylinux.wordpress.com/2013/07/29/using-the-mad-catz-m-m-o-7-with-linux-mint-and-ubuntu/).

## Manual Button Mapping Fix

Please note that there are two different versions of the R.A.T.3 mouse which are **Saitek** and **Madcatz**, this must be input correctly into the "MatchProduct" or you will run into the same issues.

First find out the ID and the Name of the mouse :

```
xinput list | grep "id"

```

In you should see your mouse labeled as "Madcatz Mad Catz R.A.T.3 Mouse" or "Saitek Cyborg R.A.T.3 Mouse". Note the device id number and then input the following command :

```
xinput query-state ID

```

(Where ID corresponds to the ID number of your mouse)

Note which 'mode' color is currently active (red/blue/purple) and which button numbers correspond to the current 'mode' by being either **"up"** or **"down"**. Change the mouse 'mode' and and retype the above command, noting which buttons change state to match the 'mode'.

Example:

```
U = up
D = down
                        U U U U U D D U U D D D  U  U 
Option "ButtonMapping" "1 2 3 4 5 0 0 8 9 0 0 0 13 14"

```

Where buttons 10, 11, and 12 have been identified as 'mode' buttons, so they can be disabled by with zeros.

When you have identified which button numbers correspond to the mouse 'Modes', you should be able to edit your xorg.conf file and disable them by inserting a zero in the appropriate point in the button sequence. Open in your chosen editor:

```
/etc/X11/xorg.conf   or
/etc/X11/xorg.conf.d/50-vmmouse.conf

```

Create a block that overwrites the mode buttons as follows:

MadCatz R.A.T.3:

```
# RAT3 mouse
Section "InputClass"
 Identifier "Mouse Remap"
 MatchProduct "Madcatz Mad Catz R.A.T.3 Mouse"
 MatchDevicePath "/dev/input/event*"
 Option "ButtonMapping" "1 2 3 4 5 6 7 8 9 0 0 0 13 14 15 16 17 18"
EndSection

```

This configuration worked for me on my old Saitek Cyborg R.A.T.3:

```
# RAT3 mouse
Section "InputClass"
 Identifier "Mouse Remap"
 MatchProduct "Saitek Cyborg R.A.T.3 Mouse"
 MatchDevicePath "/dev/input/event*"
 Option "ButtonMapping" "1 2 3 4 5 0 0 8 9 0 0 0 13 14"
EndSection

```

This works for a Mad Catz R.A.T.TE:

```
Section "InputClass"
   Identifier     "Mouse Remap"
   MatchProduct   "Mad Catz Mad Catz R.A.T.TE"
   MatchDevicePath "/dev/input/event*"
   Option         "ButtonMapping" " 1 2 3 4 5 6 7 8 9 10 11 12 0 0 0"
   Option        "ZAxisMapping" "4 5 6 7"
EndSection

```

This configuration worked for a Mad Catz R.A.T.5: Create the file **/etc/X11/xorg.conf.d/rat5.conf** with the following content (source: [[1]](http://www.bpaulin.net/articles/linux/2014/05/16/mad-catz-rat5-avec-linux/)):

```
Section "InputClass"
   Identifier "Mad Catz R.A.T. 5"
   MatchProduct "Mad Catz Mad Catz R.A.T.5 Mouse"
   MatchDevicePath "/dev/input/event*"
   Option "Buttons" "21"
   Option "ButtonMapping" "1 2 3 4 5 0 0 9 8 7 6 10 0 0 0 0 0 0 0 0 0"
   Option "ZAxisMapping" "4 5 11 10"
   Option "AutoReleaseButtons" "13 14 15"
EndSection

```

To work correctly, it is important to that you identify the correct "ButtonMapping" and "MatchProduct" for your specific mouse.

For any any modifications to xorg.conf take effect, X must be restarted.

## R.A.T. configuration software

Saitek/Mad Catz does not provide any official configuration software for Linux.

There is however open an source project which allows you to configure DPI settings for each and mode [here](https://github.com/MayeulC/Saitek).

It might however require some tweaking for certain R.A.T. mice, such as adding your mouse ID to the list of supported IDs.

## See also

*   [http://ubuntuforums.org/showthread.php?t=2126385](http://ubuntuforums.org/showthread.php?t=2126385)
*   [http://askubuntu.com/questions/92546/cyborg-r-a-t-3-gaming-mouse-stops-working-after-a-while-and-or-misbehaves](http://askubuntu.com/questions/92546/cyborg-r-a-t-3-gaming-mouse-stops-working-after-a-while-and-or-misbehaves)