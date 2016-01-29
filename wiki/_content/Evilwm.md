# Evilwm

[evilwm](http://www.6809.org.uk/evilwm/) is a minimalist window manager for the X Window system. It's minimalist in that it omits unnecessary stuff like window decorations and icons. But it's very usable in that it provides good keyboard control with repositioning and maximize toggles, solid window drags, snap-to-border support, and virtual desktops. Its installed binary size is only 0.07 MB.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Starting evilwm](#Starting_evilwm)
    *   [2.2 Startup options](#Startup_options)
*   [3 Using evilwm](#Using_evilwm)
    *   [3.1 Keyboard controls](#Keyboard_controls)
    *   [3.2 Mouse controls](#Mouse_controls)
    *   [3.3 Virtual desktops](#Virtual_desktops)
*   [4 Tips & Tricks](#Tips_.26_Tricks)
    *   [4.1 Horizontal window maximize](#Horizontal_window_maximize)
    *   [4.2 Exit evilwm by ending a program](#Exit_evilwm_by_ending_a_program)
    *   [4.3 Resize windows using the keyboard](#Resize_windows_using_the_keyboard)
    *   [4.4 Keybindings](#Keybindings)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Lost focus bug fix](#Lost_focus_bug_fix)
    *   [5.2 evilwm doesn't start](#evilwm_doesn.27t_start)
*   [6 Links](#Links)

## Installation

[Install](/index.php/Install "Install") the [evilwm](https://aur.archlinux.org/packages/evilwm/)<sup><small>AUR</small></sup> package.

## Configuration

### Starting evilwm

To start evilwm (without any options) via _startx_, ensure your `~/.xinitrc` file contains:

```
exec evilwm

```

evilwm doesn't control the desktop background or mouse cursor, so you may want to also specify these in your `~/.xinitrc` file. For example, to provide a solid color background and use the left pointer of your current mouse theme:

```
xsetroot -solid \#3f3f3f
xsetroot -cursor_name left_ptr

```

For other options, please consult _man xsetroot_.

### Startup options

evilwm can read options via command line switches. Some examples:

*   `-fg <color>` (Frame color of currently active window)
*   `-bw <number>` (Width of window borders in pixels)
*   `-term <term>` (Specifies a program to run when spawming a new terminal; default is xterm)
*   `-snap <number>` (enables snap-to-border support and specifies the proximity in pixels to snap to)
*   `-mask1 <modifier>` (override the default Ctrl+Alt keyboard modifiers)
*   `-nosoliddrag` (draw a window outline while moving or resizing, rather than drawing the entire window)

A full list of the evilwm options can be found via `man evilwm`.

By default, evilwm draws a one pixel gold border around the currenly active window. An example of the use of switches to change this would be a `~/.xinitrc` file such as:

```
exec evilwm -snap 10 -bw 2 -fg red

```

This would enable

*   snapping to a border within 10 pixels,
*   a border width of 2 pixels,
*   red for the currently active window border.

From [http://www.6809.org.uk/evilwm/usage.shtml](http://www.6809.org.uk/evilwm/usage.shtml):

_evilwm will also read options, one per line, from a file called .evilwmrc in the user's home directory._ _Options listed in a configuration file should omit the leading dash. Options specified on the command line_ _override those found in the configuration file._

## Using evilwm

After starting evilwm you will see nothing but a mouse cursor and a black background (or other background if you specified it as above). To open a terminal, use the key combination Ctrl+Alt+Return. Programs can then be run from the terminal using _ProgramName&_.

### Keyboard controls

Using the keyboard combination of Ctrl+Alt plus a third key gives you these functions:

*   Return – spawns new terminal
*   Escape – Deletes current window
*   Insert – Lowers current window
*   H,J,K,L – Move window left, down, up, right 16 pixels
*   Y,U,B,N – Move window to top-left, top-right, bottom-left, bottom-right corner
*   I – Show information about current window
*   = – Maximize current window vertically (toggle)
*   X – Maximize current window full-screen (toggle)

### Mouse controls

By holding down the Alt key, you can perform these functions with the mouse:

*   Button 1 – Move window
*   Button 2 – Resize window
*   Button 3 – Lower window

### Virtual desktops

Using the keyboard combination of Ctrl+Alt plus a third key gives you these virtual desktop functions:

*   1-8 – Switch virtual desktop
*   left – Previous virtual desktop
*   right – Next virtual desktop
*   F – Fix or unfix current window

To move a window from one virtual desktop to another, fix it, switch desktop, then unfix it. Alt+Tab can also be used to cycle through windows on the current desktop.

## Tips & Tricks

### Horizontal window maximize

The key combination of Ctrl+Alt+= will maximize a window vertically. To maximize a window horizontally, use Ctrl+Alt+= to maximize it vertically, then Ctrl+Alt+X to maximize it horizontally (as opposed to just using Ctrl+Alt+X to maximize it full-screen).

### Exit evilwm by ending a program

By default, evilwm has no quit option. To exit, simply kill X with [Ctrl+Alt+Backspace](/index.php/Keyboard_configuration_in_Xorg#Terminating_Xorg_with_Ctrl.2BAlt.2BBackspace "Keyboard configuration in Xorg"). If you wish, you can exit evilwm by closing a specific program. Instead of using `exec evilwm` in your `~/.xinitrc` file, you can transfer exec to another program. Killing this program will then exit evilwm. For example:

```
$ cat ~/.xinitrc
#!/bin/sh

evilwm -snap 10 -bw 2 -fg red &
exec xclock

```

### Resize windows using the keyboard

Although not mentioned in the man-page, you can resize windows with the keyboard as well as the mouse. Using the same key-combinations for moving a window, just add the _Shift_ key to the mix to resize a window.

Ctrl+Alt+_Shift_:

```
H,J,K,L - Resize window smaller horizontally, larger vertically, smaller vertically, larger horizontally

```

### Keybindings

You can make life easier by using [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) to run commands in evilwm. See [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") for more details.

## Troubleshooting

### Lost focus bug fix

Some users suffer from a bug where evilwm loses focus after closing a window. This means that evilwm stops responding to keyboard shortcuts, and if no other window is open which the mouse can be moved over to regain focus evilwm becomes unusable and has to be restarted.

Right now the solution requires adding one line to the source code, recompiling evilwm and installing it manually (not via pacman). To fix the bug, get the source code from the official website, unpack it and open "client.c" with any text editor. Find the "remove_client" function and add the following to the very end of its definition (after the "LOG_DEBUG" call):

```
XSetInputFocus(dpy, PointerRoot, RevertToPointerRoot, CurrentTime);

```

and compile and install evilwm by running "make" and "make install" (the latter with root privileges).

The author of evilwm has been told both of this bug and this fix, but he has not yet released a new version of evilwm which incorporates this solution.

### evilwm doesn't start

(Sourced from the forums thread [here](https://bbs.archlinux.org/viewtopic.php?id=38671).)

When you run evilwm, xorg presents error messages in the log file and/or on the screen and exits. The messages may vary from system to system. Probably [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) or [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) is missing. Install either font to solve the problem.

## Links

*   [evilwm](http://www.6809.org.uk/evilwm/) - the official website of evilwm

Retrieved from "[https://wiki.archlinux.org/index.php?title=Evilwm&oldid=378498](https://wiki.archlinux.org/index.php?title=Evilwm&oldid=378498)"