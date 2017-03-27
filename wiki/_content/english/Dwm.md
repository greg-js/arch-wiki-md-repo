[dwm](http://dwm.suckless.org/) is a dynamic window manager for [Xorg](/index.php/Xorg "Xorg"). It manages windows in tiled, stacked, and full-screen layouts, as well as many others with the help of [optional patches](#Patches). Layouts can be applied dynamically, optimizing the environment for the application in use and the task being performed. dwm is extremely lightweight and fast, written in C and with a stated design goal of remaining under 2000 source lines of code. It provides [multihead](/index.php/Multihead "Multihead") support for [xrandr](/index.php/Xrandr "Xrandr") and Xinerama.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting dwm](#Starting_dwm)
*   [3 Configuration](#Configuration)
    *   [3.1 Customization](#Customization)
    *   [3.2 Patches](#Patches)
    *   [3.3 Status bar](#Status_bar)
    *   [3.4 Use pacman](#Use_pacman)
    *   [3.5 Applying changes](#Applying_changes)
*   [4 Basic usage](#Basic_usage)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 st keybindings conflict](#st_keybindings_conflict)
    *   [5.2 Statusbar configuration](#Statusbar_configuration)
        *   [5.2.1 Conky statusbar](#Conky_statusbar)
    *   [5.3 Restart dwm without logging out or closing programs](#Restart_dwm_without_logging_out_or_closing_programs)
    *   [5.4 Make the right Alt key work as if it were Mod4 (Windows Key)](#Make_the_right_Alt_key_work_as_if_it_were_Mod4_.28Windows_Key.29)
    *   [5.5 Space around font in dwm's bar](#Space_around_font_in_dwm.27s_bar)
    *   [5.6 Disable focus follows mouse behaviour](#Disable_focus_follows_mouse_behaviour)
    *   [5.7 Make some windows start floating](#Make_some_windows_start_floating)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Fixing misbehaving Java applications](#Fixing_misbehaving_Java_applications)
    *   [6.2 Fixing the extra topbar that does not disappear when changing resolution/monitors](#Fixing_the_extra_topbar_that_does_not_disappear_when_changing_resolution.2Fmonitors)
    *   [6.3 Fixing gaps around terminal windows](#Fixing_gaps_around_terminal_windows)
*   [7 See also](#See_also)

## Installation

**Note:** If dwm is not compiled from source, opportunities for customization are lost since dwm's configuration is performed by editing its source code. See [#Configuration](#Configuration) for more information.

[Install](/index.php/Install "Install") the [dwm](https://www.archlinux.org/packages/?name=dwm) package. Alternatively, make changes to the source code, then compile dwm using [ABS](/index.php/ABS "ABS") or the [dwm-git](https://aur.archlinux.org/packages/dwm-git/) package for the development version.

## Starting dwm

Select *Dwm* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

Alternatively, to start dwm with [startx](/index.php/Startx "Startx") append the following to `~/.xinitrc`:

```
exec dwm

```

## Configuration

### Customization

dwm is configured at compile-time by editing some of its source files, namely `config.h`. For detailed information on these settings see the included, well commented `config.def.h` as well as the [customisation section](http://dwm.suckless.org/customisation/) on the dwm website.

### Patches

The official website has a number of [patches](http://dwm.suckless.org/patches/) that can add extra functionality to dwm. These patches primarily make changes to the `dwm.c` file but also make changes to the `config.h` file where appropriate. For information on applying patches, see [Patching in ABS](/index.php/Patching_in_ABS "Patching in ABS").

### Status bar

See the [dwmstatus](http://dwm.suckless.org/dwmstatus/) section on the dwm website. Also see the [#Statusbar configuration](#Statusbar_configuration) section.

### Use pacman

You should [create a package](/index.php/Creating_packages "Creating packages") using a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") so that [pacman](/index.php/Pacman "Pacman") is aware of the package.

### Applying changes

After making any desired changes and installing the updated package, restart dwm in order to apply the changes.

## Basic usage

Consult the [dwm tutorial](http://dwm.suckless.org/tutorial) for information on basic dwm usage. Additionally see dwm(1).

## Tips and tricks

### st keybindings conflict

The default terminal for *dwm* is [st](/index.php/St "St"). Be default, *st* uses `Mod1+Ctrl+C` for copy, but *dwm* uses this same key combination to kill a program. You should change this shortcut in either *dwm* or *st* such that *st* is not killed when attempting to copy text.

### Statusbar configuration

**Note:** The following requires the [xorg-xsetroot](https://www.archlinux.org/packages/?name=xorg-xsetroot) package to be installed.

Dwm reads the name of the root window and redirects it to the statusbar. The root window is the window within which all other windows are drawn and arranged by the window manager. Like any other window, the root window has a title/name, but it is usually undefined because the root window always runs in the background.

The information that you want dwm to show in the statusbar should be defined with `xsetroot -name ""` command in `~/.xinitrc` or `~/.xprofile` (if you are using a [display manager](/index.php/Display_manager "Display manager")). For example:

 `xsetroot -name "Thanks for all the fish!"` 

Dynamically updated information should be put in a loop which is forked to background - see the example below:

```
# Statusbar loop
while true; do
   xsetroot -name "$( date +"%F %R" )"
   sleep 1m    # Update time every minute
done &

# Autostart section
pcmanfm & 

exec dwm

```

In this case the date is shown in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601 "wikipedia:ISO 8601") format and [PCManFM](/index.php/PCManFM "PCManFM") is launched at startup.

**Note:** It is not recommended to set the update interval equal to zero or remove the "sleep" line entirely since this will cause CPU usage to rise substantially (you can assess the effect with *top* and [powertop](/index.php/Powertop "Powertop")).

More examples of statusbars are included [on the suckless wiki](http://dwm.suckless.org/dwmstatus/).

#### Conky statusbar

[Conky](/index.php/Conky "Conky") can be printed to the statusbar with `xsetroot -name`:

```
(conky | while read LINE; do xsetroot -name "$LINE"; done) &
exec dwm

```

To do this, conky needs to be told to output text to the console only. The following is a sample conkyrc for a dual core CPU, displaying several usage statistics:

```
conky.config = {
out_to_console = true,
out_to_x = false,
background = false,
update_interval = 2,
total_run_times = 0,
use_spacer = 'none',
};
conky.text = [[
$mpd_smart :: ${cpu cpu1}% / ${cpu cpu2}%  ${loadavg 1} ${loadavg 2 3} :: ${acpitemp}c :: $memperc% ($mem) :: ${downspeed eth0}K/s ${upspeed eth0}K/s :: ${time %a %b %d %I:%M%P}
]];

```

For icons and color options, see [dzen](/index.php/Dzen "Dzen").

### Restart dwm without logging out or closing programs

For restarting dwm without logging out or closing applications, change or add a startup script so that it loads dwm in a *while* loop, see below:

```
while true; do
    # Log stderror to a file 
    dwm 2> ~/.dwm.log
    # No error logging
    #dwm >/dev/null 2>&1
done

```

dwm can now be restarted without destroying other X windows by pressing the usual Mod-Shift-Q combination.

It is a good idea to place the above startup script into a separate file, `~/bin/startdwm` for instance, and execute it through `~/.xinitrc`. From this point on, when you wish to end the X session, simply execute `killall xinit`, or bind it to a convenient key. Alternatively, you could setup your dwm session script so that it relaunches dwm only if the binary changes. This could be useful in the case where you change a setting or update the dwm code base.

```
# relaunch DWM if the binary changes, otherwise bail
csum=$(sha1sum $(which dwm))
new_csum=""
while true
do
    if [ "$csum" != "$new_csum" ]
    then
        csum=$new_csum
        dwm
    else
        exit 0
    fi
    new_csum=$(sha1sum $(which dwm))
    sleep 0.5
done
```

### Make the right Alt key work as if it were Mod4 (Windows Key)

When using Mod4 (the Super/Windows Key) as the `MODKEY`, it may be equally convenient to have the right Alt key (`Alt_R`) act as `Mod4`. This will allow you to perform otherwise awkward keystrokes one-handed, such as zooming with `Alt_R`+`Enter`.

First, find out which keycode is assigned to `Alt_R`:

```
xmodmap -pke | grep Alt_R

```

Then simply add the following to the startup script (e.g. `~/.xinitrc`), changing the keycode *113* if necessary to the result gathered by the previous `xmodmap` command:

```
xmodmap -e "keycode 113 = Super_L"  # reassign Alt_R to Super_L
xmodmap -e "remove mod1 = Super_L"  # make sure X keeps it out of the mod1 group

```

After doing so, any functions that are triggered by the `Super_L` key press will also be triggered by an `Alt_R` key press.

**Note:** There is a #define option in [config.h](#Customizing_config.h) which also allows you to switch the modkey

### Space around font in dwm's bar

By default, dwm's bar adds 2px around the size of the font. To change this, modify the following line in `dwm.c`:

 `bh = dc.h = dc.font.height + 2;` 

### Disable focus follows mouse behaviour

To disable focus follows mouse behaviour comment out the following line in definiton of struct handler in `dwm.c`

 `[EnterNotify] = enternotify,` 

Note that this change can cause some difficulties; the first click on an inactive window will only bring the focus to it. To interact with window contents (buttons, fields etc) you need to click again. Also, if you have several monitors, you may notice that the keyboard focus does not switch to another monitor activated by clicking.

### Make some windows start floating

For some windows, such as preferences dialogs, it does not make sense for these windows to be tiled - they should be free-floating instead. For example, to make Firefox's preferences dialog float, add the following to your rules array in `config.h`:

```
 { "Firefox",     NULL,       "Firefox Preferences",        1 << 8,         True,     -1 },

```

## Troubleshooting

### Fixing misbehaving Java applications

See [Java#Non-reparenting window managers](/index.php/Java#Non-reparenting_window_managers "Java") for a solution.

### Fixing the extra topbar that does not disappear when changing resolution/monitors

**Note:** this patch is intended for dwm-6.0 which is currently in the [official repositories](/index.php/Official_repositories "Official repositories"). The development version of dwm has already implemented this.

When resizing or connecting/disconnecting different monitors there may be a remnant of the topbar stuck on the screen which cannot be removed. To fix this bug, rebuild dwm with [this patch](http://ix.io/fea).

### Fixing gaps around terminal windows

If there are empty gaps of desktop space outside terminal windows, it is likely due to the terminal's font size. Either adjust the size until finding the ideal scale that closes the gap, or toggle `resizehints` to *False* in `config.h`:

```
static Bool resizehints = False; /* True means respect size hints in tiled resizals */

```

This will cause dwm to ignore resize requests from all client windows, not just terminals. The downside to this workaround is that some terminals may suffer redraw anomalies, such as ghost lines and premature line wraps, among others.

## See also

*   [dwm's official website](http://dwm.suckless.org/)
*   [Introduction to dwm video](http://www.youtube.com/watch?v=GQ5s6T25jCc)
*   [dmenu](/index.php/Dmenu "Dmenu") - Simple application launcher from the developers of dwm
*   The [dwm thread](https://bbs.archlinux.org/viewtopic.php?id=57549/) on the forums
*   [Hacking dwm thread](https://bbs.archlinux.org/viewtopic.php?id=92895/)
*   Check out the forums' [wallpaper thread](https://bbs.archlinux.org/viewtopic.php?id=57768/) for a selection of dwm wallpapers
*   [Show off your dwm configuration forum thread](https://bbs.archlinux.org/viewtopic.php?id=74599)