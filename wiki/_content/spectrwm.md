# spectrwm

From [spectrwm website](http://spectrwm.org/):

NaN

Spectrwm is written in C and configured with a text configuration file. It was previously known as scrotwm.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Starting spectrwm](#Starting_spectrwm)
    *   [3.1 Starting spectrwm with XDM](#Starting_spectrwm_with_XDM)
    *   [3.2 Starting spectrwm with KDM](#Starting_spectrwm_with_KDM)
*   [4 Multiple monitors (Xinerama)](#Multiple_monitors_.28Xinerama.29)
*   [5 Statusbar configuration](#Statusbar_configuration)
    *   [5.1 Bash scripts](#Bash_scripts)
    *   [5.2 Conky](#Conky)
*   [6 Alternative status bar](#Alternative_status_bar)
*   [7 Screenshots](#Screenshots)
*   [8 Screen locking](#Screen_locking)
*   [9 Using spectrwm](#Using_spectrwm)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Help, I just logged in and all I see is a blank screen](#Help.2C_I_just_logged_in_and_all_I_see_is_a_blank_screen)
    *   [10.2 Why does my window open in a desktop other then the current active one?](#Why_does_my_window_open_in_a_desktop_other_then_the_current_active_one.3F)
*   [11 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [spectrwm](https://www.archlinux.org/packages/?name=spectrwm) package.

The modkey (the main key to issue commands with) is set to Mod4, which is usually the `Super` key.

There is also a screen lock key binding, which by default calls xlock from the [xlockmore](https://www.archlinux.org/packages/?name=xlockmore) package.

[xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) is also useful for screen saving and power management after an idle period, and screen locking.

See [Xdefaults](/index.php/Xdefaults "Xdefaults") for details of how to set up fonts, colours and other settings for [xterm](https://www.archlinux.org/packages/?name=xterm) and [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver). Run `xscreensaver-demo` to select the animation (or blank) and display power management (recommended).

## Configuration

_spectrwm_ first tries to open the user specific file, `~/.spectrwm.conf`. If that file is unavailable, it tries to open the global configuration file at `/etc/spectrwm.conf`.

Optionally, spectrwm can call `baraction.sh` (in the user's path), which should output a text status message to `stdout` for the status bar.

## Starting spectrwm

To start spectrwm via `startx` or the [SLiM](/index.php/SLiM "SLiM") login manager, append the following to `~/.xinitrc`:

```
exec spectrwm

```

### Starting spectrwm with XDM

For [XDM](/index.php/XDM "XDM"), create `~/.xsession` with the following contents:

```
# .xsession
# This file is sourced by xdm
spectrwm

```

Make sure `~/.xsession` is executable:

```
$ chmod a+x ~/.xsession

```

**Note:** If you do not create `~/.xsession`, then `~/.xinitrc` will be used, but you might want different settings depending on if you use `startx` or XDM. Remember to make `~/.xinitrc` executable, or XDM won't start, if you use that method.

**Tip:** For a nice simple Arch themed xdm, try [xdm-arch-theme](https://aur.archlinux.org/packages/xdm-arch-theme/)<sup><small>AUR</small></sup>.

### Starting spectrwm with KDM

For [KDM](/index.php/KDM "KDM"), make sure `/usr/share/xsessions` is listed in SessionDirs in `/usr/share/config/kdm/kdmrc` as described [here](/index.php/KDM#SessionsDirs "KDM"). SpectrWM will then be available as an option in the Session Type menu in KDM.

To start other tasks when the session is launched, for example to launch xscreensaver and set the background image, copy `/usr/share/config/kdm/Xsession` to a custom version as described [here](/index.php/KDM#Session "KDM"), and then edit it, for example like this:

```
case $session in
  "")
    exec xmessage -center -buttons OK:0 -default OK "Sorry, $DESKTOP_SESSION is no valid session."
    ;;
  failsafe)
    exec xterm -geometry 80x24-0-0
    ;;
  custom)
    exec $HOME/.xsession
    ;;
  default)
    exec /usr/bin/startkde
    ;;
  '''/usr/bin/spectrwm'''|otherwm''')'''
    '''feh --bg-scale /usr/share/wallpapers/Plasmalicious/contents/images/1280x1024.jpg'''
    '''xscreensaver -no-splash &'''
    '''eval exec "$session"'''
    ''';;'''
  *)
    eval exec "$session"
    ;;
esac

```

## Multiple monitors (Xinerama)

With a non-Xrandr multiple monitor setup create regions to split the total desktop area into one region per monitor:

```
region                = screen[1]:1280x1024+0+0
region                = screen[1]:1280x1024+1280+0

```

## Statusbar configuration

To enable the statusbar, uncomment these two items in `/etc/spectrwm.conf` (or `~/.spectrwm.conf`). By default they are commented out and the statusbar is disabled.

```
bar_action              = baraction.sh
bar_delay               = 5

```

### Bash scripts

To test the status bar, place the following simple `baraction.sh` in a `~/scripts` (or `~/bin`) directory which you have previously added to your $PATH in your [~/.bashrc](/index.php/Bashrc "Bashrc") file.

```
#!/bin/bash
# baraction.sh script for spectrwm status bar

SLEEP_SEC=5  # set bar_delay = 5 in /etc/spectrwm.conf
COUNT=0
#loops forever outputting a line every SLEEP_SEC secs
while :; do
	let COUNT=$COUNT+1
        echo -e "         Hello World! $COUNT"
        sleep $SLEEP_SEC
done

```

Press `Modkey+Q` to restart spectrwm and after a few seconds you should see the output in the status bar. If you have problems at this stage, make sure the script is executable, test it from the command line, and check the path/filename you specified in `bar_action`.

Here are some other ideas for status bar items: ethernet, email notification, disk space, mounts, now playing (mpc current).

The script may also show the date, in which case the built-in clock can be disabled:

```
clock_enabled     = 0

```

### Conky

Instead of a bash script, conky may be used. It should be used in non-graphical mode as shown below to output a text string to stdout which can be read in by spectrwm. First install conky. It is not necessary to install the cut-down "conky-cli" from AUR (although that would work too).

In `~/.spectrwm.conf` set

```
bar_action = conky

```

Then in each user's `~/.conkyrc` file place for example:

```
out_to_x no
out_to_console yes
update_interval 1.0
total_run_times 0
use_spacer none
TEXT
${time %R %a,%d-%#b-%y} |Mail:${new_mails} |Up:${uptime_short} |Temp:${acpitemp}C |Batt:${battery_short} |${addr wlan0} |RAM:$memperc% |CPU:${cpu}% | ${downspeedf wlan0}

```

## Alternative status bar

An alternative is to use [dzen2](/index.php/Dzen "Dzen") to create a status bar. This has the advantage that colors and even icons may be used, but the disadvantage that the bar is not integrated with spectrwm. So the current workspace number and layout and the bar-toggle keybinding are not available. The "region" option can be used to reserve the required screen space. For example to reserve 14 pixels at the top of the screen in spectrwm.conf change

```
bar_enabled             = 1
region                  = screen[1]:1024x768+0+0

```

to

```
bar_enabled             = 0
region                  = screen[1]:1024x754+0+14

```

(adjust for your screen resolution).

Then, for example using [i3status](/index.php/I3 "I3") to supply the information:

```
$ i3status | dzen2 -fn -*-terminus-medium-*-*-*-*-*-*-*-*-*-*-* &

```

Spectrwm's own bar can still be enabled and disabled with `Meta+b`.

## Screenshots

Spectrwm has the facility to execute a script called `screenshot.sh` with the keybindings

```
Meta+s       for a full screenshot
Meta+Shift+s for a screenshot of a single window

```

First install scrot Then copy the default script supplied in the spectrwm package to a location in your `$PATH`, for example:

```
$ cp /usr/share/spectrwm/screenshot.sh ~/bin

```

## Screen locking

By default the lock keybinding `Mod+Shift+Delete` executes _xlock_

```
program[lock]      = xlock

```

An alternative, if xscreensaver is already running, is to use

```
program[lock]      = xscreensaver-command -lock

```

## Using spectrwm

*   To save space, window title bars are not shown. Window borders are one pixel wide. The border changes colour to indicate focus.

*   Layouts are handled dynamically and can be changed on the fly. There are three standard layouts (stacking algorithms): vertical, horizontal and maximized (indicated in the status bar as [|], [-] and [ ])

*   There is the concept of a master area (a working area). Any window can be switched to become the master and will then be shown in the master area. The master area is the left (top) portion of the screen in vertical (horizontal) mode. The size of the master area can be adjusted with the keys. By default the master area holds one window, but this can be increased.

*   The area excluding the master area is called the stacking area. New windows are added to the stacking area. By default the stacking area has one column (row) in vertical (horizontal) mode, but his can be increased.

*   Windows may be moved to a floating layer -- i.e. removed from the tiling management. This is useful for programs which are not suitable for tiling.

Some of the most useful key bindings:

```
Meta+Shift+Return: open terminal
Meta+p: dmenu (then type the start of the program name and return)
Meta+1/2/3/4/5/6/7/8/9/0: select workspaces 1-10
Meta+Shift+1/2/3/4/5/6/7/8/9/0: move window to workspace 1-10
Meta+Right/Left: select next/previous workspace
Meta+Shift+Right/Left: select next/previous screen
Meta+Spacebar: cycle through layouts (vertical, horizontal, maximized)
Meta+j/k: cycle through windows forwards/backwards
Meta+Tab/Meta+Shft+Tab: same as Meta+j/k
Meta+Return: move current window to master area
Meta+h/l:  increase/decrease size of master area

```

Advanced stacking

```
Meta+,/. : increase/decrease the number of windows in master area (default is 1)
Meta+Shift+,/. : increase/decrease number of columns(rows) in stacking area in vertical(horizontal) mode (default is 1)
Meta+Shift+j/k: swap window position with next/previous window
Meta+t: float<->tile toggle

```

Mouse bindings

```
Mouseover: focus window
Meta+LeftClick+Drag: move window (and float it if tiled)
Meta+RightClick+Drag: resize floating window
Meta+Shift+RightClick+Drag: resize floating window keeping it centred

```

Other useful bindings

```
Meta+x: close window
Meta+Shift+x: kill window
Meta+b: hide/show status bar
Meta+q: restart spectrwm (reset desktops and reread spectrwm config without stopping running programs)
Meta+Shift+q: exit spectrwm

```

## Troubleshooting

### Help, I just logged in and all I see is a blank screen

Press `Shift+WinKey+Return` and an xterm will start. See `man spectrwm` for other default key bindings. Also check your configuration file.

### Why does my window open in a desktop other then the current active one?

Currently the PID of window is used to determine the desktop for new windows. To workaround this with terminals for example, you can often pass an argument to open the terminal in a new process.

## See also

*   [spectrwm](http://www.spectrwm.org) - spectrwm's official website

*   [dmenu](/index.php/Dmenu "Dmenu") - Simple application launcher from the developers of [dwm](/index.php/Dwm "Dwm")

*   #spectrwm at irc.freenode.net - (un)official IRC channel

*   [The scrotwm thread](https://bbs.archlinux.org/viewtopic.php?id=64645)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Spectrwm&oldid=415872](https://wiki.archlinux.org/index.php?title=Spectrwm&oldid=415872)"