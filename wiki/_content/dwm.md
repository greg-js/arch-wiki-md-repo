# dwm

[dwm](http://dwm.suckless.org/) is a dynamic window manager for [Xorg](/index.php/Xorg "Xorg"). It manages windows in tiled, stacked, and full-screen layouts, as well as many others with the help of [optional patches](#Patches). Layouts can be applied dynamically, optimizing the environment for the application in use and the task being performed. dwm is extremely lightweight and fast, written in C and with a stated design goal of remaining under 2000 source lines of code. It provides [multihead](/index.php/Multihead "Multihead") support for [xrandr](/index.php/Xrandr "Xrandr") and Xinerama.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting dwm](#Starting_dwm)
*   [3 Configuration](#Configuration)
    *   [3.1 Patches](#Patches)
        *   [3.1.1 Window tiling patches](#Window_tiling_patches)
    *   [3.2 Customizing config.h](#Customizing_config.h)
        *   [3.2.1 Adding custom keybinds/shortcuts](#Adding_custom_keybinds.2Fshortcuts)
    *   [3.3 Customizing config.mk](#Customizing_config.mk)
    *   [3.4 Statusbar configuration](#Statusbar_configuration)
        *   [3.4.1 Examples of statusbar configuration](#Examples_of_statusbar_configuration)
        *   [3.4.2 Conky statusbar](#Conky_statusbar)
*   [4 Basic usage](#Basic_usage)
    *   [4.1 Using dmenu](#Using_dmenu)
    *   [4.2 Controlling windows](#Controlling_windows)
        *   [4.2.1 Giving another tag to a window](#Giving_another_tag_to_a_window)
        *   [4.2.2 Closing a window](#Closing_a_window)
        *   [4.2.3 Window layouts](#Window_layouts)
    *   [4.3 Exiting dwm](#Exiting_dwm)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Restart dwm without logging out or closing programs](#Restart_dwm_without_logging_out_or_closing_programs)
    *   [5.2 Make the right Alt key work as if it were Mod4 (Windows Key)](#Make_the_right_Alt_key_work_as_if_it_were_Mod4_.28Windows_Key.29)
    *   [5.3 Space around font in dwm's bar](#Space_around_font_in_dwm.27s_bar)
    *   [5.4 Disable focus follows mouse behaviour](#Disable_focus_follows_mouse_behaviour)
    *   [5.5 Make some windows start floating](#Make_some_windows_start_floating)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Fixing misbehaving Java applications](#Fixing_misbehaving_Java_applications)
    *   [6.2 Fixing the extra topbar that does not disappear when changing resolution/monitors](#Fixing_the_extra_topbar_that_does_not_disappear_when_changing_resolution.2Fmonitors)
    *   [6.3 Fixing gaps around terminal windows](#Fixing_gaps_around_terminal_windows)
*   [7 See also](#See_also)

## Installation

**Note:** If dwm is not compiled from source, opportunities for customization are lost since dwm's configuration is performed by editing its source code. See [#Configuration](#Configuration) for more information.

[Install](/index.php/Install "Install") the [dwm](https://www.archlinux.org/packages/?name=dwm) package. Alternatively, compile dwm from source using [ABS](/index.php/ABS "ABS") or the [dwm-git](https://aur.archlinux.org/packages/dwm-git/)<sup><small>AUR</small></sup> package (for the development version), making changes to the source code as desired. You may also want to install [dmenu](/index.php/Dmenu "Dmenu"), a fast and lightweight dynamic menu for [Xorg](/index.php/Xorg "Xorg").

## Starting dwm

Select _Dwm_ from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

Alternatively, to start dwm with `startx` or the [SLiM](/index.php/SLiM "SLiM") login manager, simply append the following to `~/.xinitrc`:

```
exec dwm

```

## Configuration

As mentioned in [#Installation](#Installation), dwm is configured at compile-time by editing some of its source files, namely `config.h` and `config.mk` and also `dwm.c`.

Once changes have been made, update the checksums in the PKGBUILD, see [PKGBUILD#Integrity](/index.php/PKGBUILD#Integrity "PKGBUILD"). Alternatively, you can skip integrity checks by calling _makepkg_ with the `--skipinteg` switch.

Then, compile and reinstall dwm:

```
$ makepkg -fi

```

Assuming the configuration changes were valid, the command above will compile dwm, build and reinstall the resulting package. If problems were encountered, review the output for specific information.

Finally, restart dwm in order to apply the changes.

**Tip:** To recompile easily, make an alias by putting `alias redwm='cd ~/dwm; updpkgsums; makepkg -fi --noconfirm; killall dwm'` in your `.bashrc` file.

### Patches

The official website has a number of [patches](http://dwm.suckless.org/patches/) that can add extra functionality to dwm. These patches primarily make changes to the `dwm.c` file but also make changes to the `config.h` file where appropriate. For information on applying patches, see [Patching in ABS](/index.php/Patching_in_ABS "Patching in ABS").

#### Window tiling patches

The [Bottom Stack](http://dwm.suckless.org/patches/bottom_stack) patch provides an additional tiling mode that splits the screen horizontally, as opposed to the default vertically oriented tiling mode. Similarly, bstack horizontal splits the tiles horizontally. The [gaplessgrid patch](http://dwm.suckless.org/patches/gapless_grid) allows windows to be tiled like a grid.

The default behaviour of dwm is to apply the currently selected layout for all tags. To have different layouts for different tags use the [pertag](http://dwm.suckless.org/patches/pertag) patch.

### Customizing config.h

The `config.h` file is where the general dwm preferences are stored. Most settings within the file should be self-explanatory. For detailed information on these settings, see the [dwm website](http://dwm.suckless.org/customisation/).

#### Adding custom keybinds/shortcuts

Two entries are needed in `config.h` to create custom keybinds. One under the `/* commands */` section, and another under the `static Key keys[] = {` section.

```
static const char *_keybindname_[]   = { "_command_", "_flags_", "_arguments_", NULL };

```

`_keybindname_` can be anything; `_command_`, `_flags_` and `_arguments_` can be anything but they have to be individually enclosed in `""`.

Some examples:

`{ MODKEY, XK__key_, spawn, {.v = _keybindname_ } }` would bind `Mod+_key_` to the command defined previously.

`{ MODKEY|ShiftMask, XK__key_, spawn, {.v = _keybindname_ } }` would bind `Mod+Shift+_key_` Use ControlMask for `Ctrl` key.

Single keys such as `Fn` or multimedia keys have to be bound with the hex codes obtainable from the program _xev_.

`{ 0, 0xff00, spawn, {.v = _keybindname_ } }` would bind foo key `0xff00` to `_keybindname_`.

See [Extra keyboard keys#Keycodes](/index.php/Extra_keyboard_keys#Keycodes "Extra keyboard keys") for information on finding keycodes.

### Customizing config.mk

**Warning:** Installing software directly from source without creating a package is **not recommended** as [pacman](/index.php/Pacman "Pacman") will not be able to track the installed files.

The `config.mk` file is included by Makefile. It allows you to configure how GNU _make_ is going to compile and install dwm.

If you are installing dwm directly from source, without creating a package first, then be sure to alter `config.mk` to set the correct prefixes:

Modify `PREFIX`:

```
PREFIX = /usr

```

The X11 include folder:

```
X11INC = /usr/include/X11

```

And the the X11 lib directory:

```
X11LIB = /usr/lib/X11

```

**Tip:** If you only wish to test configuration changes without affecting systemwide dwm, change `PREFIX` to a local directory such as `${HOME}/.local`. Note that if you are compiling using the [dwm](https://www.archlinux.org/packages/?name=dwm) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), you should change the `PREFIX` in the PKGBUILD instead as this will take precedence over `config.mk` - see the _package()_ function - and you should also change the `pkgname`.

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

**Note:** It is not recommended to set the update interval equal to zero or remove the "sleep" line entirely since this will cause CPU usage to rise substantially (you can assess the effect with _top_ and [powertop](/index.php/Powertop "Powertop")).

#### Examples of statusbar configuration

This example shows battery state (note that it depends on the [acpi](https://www.archlinux.org/packages/?name=acpi) package):

```
while true ; do
    xsetroot -name "$(acpi -b | awk 'sub(/,/,"") {print $3, $4}')"
    sleep 1m
done &
exec dwm

```

Below is another example that displays also the [ALSA](/index.php/ALSA "ALSA") volume and the battery state. The latter is displayed only when the system is off-line.

```
#set statusbar
 while true
 do
    if acpi -a | grep off-line > /dev/null; then
        xsetroot -name "Bat. $(awk 'sub(/,/,"") {print $3, $4}' <(acpi -b)) \
        | Vol. $(awk '/dB/ { gsub(/[\[\]]/,""); print $5}' <(amixer get Master)) \
        | $(date +"%a, %b %d %R")"
    else
        xsetroot -name "Vol. $(awk '/dB/ { gsub(/[\[\]]/,""); print $5}' <(amixer get Master)) \
        | $(date +"%a, %b %d %R")"
    fi
    sleep 1s   
 done &

```

Alternatively, you could create a script with variables for each type of data to be displayed - this should improve readability and maintainability. See the example below:

```
while true; do

# Power/Battery Status
if [ "$( cat /sys/class/power_supply/AC0/online )" -eq "1" ]; then
        DWM_BATTERY="AC";
        DWM_RENEW_INT=3;
else
        DWM_BATTERY=$(( `cat /sys/class/power_supply/BAT0/energy_now` * 100 / `cat /sys/class/power_supply/BAT0/energy_full` ));
        DWM_RENEW_INT=30;
fi;

# Wi-Fi eSSID
if [ "$( cat /sys/class/net/eth1/rfkill1/state )" -eq "1" ]; then
		  DWM_ESSID=$( /sbin/iwgetid -r ); 
else
		  DWM_ESSID="OFF";
fi;

# Keyboard layout
if [ "`xset -q | awk -F \" \" '/Group 2/ {print($4)}'`" = "on" ]; then 
		  DWM_LAYOUT="ru"; 
else 
		  DWM_LAYOUT="en"; 
fi; 

# Volume Level
DWM_VOL=$( amixer -c1 sget Master | awk -vORS=' ' '/Mono:/ {print($6$4)}' );

# Date and Time
DWM_CLOCK=$( date '+%e %b %Y %a | %k:%M' );

# Overall output command
DWM_STATUS="WiFi: [$DWM_ESSID] | Lang: [$DWM_LAYOUT] | Power: [$DWM_BATTERY] | Vol: $DWM_VOL | $DWM_CLOCK";
xsetroot -name "$DWM_STATUS";
sleep $DWM_RENEW_INT;

done &

```

Example output from the script above:

```
WiFi: [OFF] | Lang: [en] | Power: [96] | Vol: [on][31%]  | 10 Jan 2014 Fri | 23:01

```

**Note:** In the script above the "sleep" interval is adjusted automatically depending on whether your laptop is running on battery or not. For desktop computers without a battery, this section is not necessary.

#### Conky statusbar

[Conky](/index.php/Conky "Conky") can be printed to the statusbar with `xsetroot -name`:

```
(conky | while read LINE; do xsetroot -name "$LINE"; done) &
exec dwm

```

To do this, conky needs to be told to output text to the console only. The following is a sample conkyrc for a dual core CPU, displaying several usage statistics:

```
out_to_console yes
out_to_x no
background no
update_interval 2
total_run_times 0
use_spacer none

TEXT
$mpd_smart :: ${cpu cpu1}% / ${cpu cpu2}%  ${loadavg 1} ${loadavg 2 3} :: ${acpitemp}c :: $memperc% ($mem) :: ${downspeed eth0}K/s ${upspeed eth0}K/s :: ${time %a %b %d %I:%M%P}

```

For icons and color options, see [dzen](/index.php/Dzen "Dzen").

## Basic usage

Besides the following sections, also consult the [dwm tutorial](http://dwm.suckless.org/tutorial) for information on basic dwm usage.

### Using dmenu

To start [dmenu](/index.php/Dmenu "Dmenu"), press `Mod1` + `P` (`Mod1` should be the `Alt` key by default). This can be changed if you so desire. Then, simply type in the first few characters of the binary you wish to run until you see it along the top bar. Use your left and right arrow keys to navigate to the binary and press enter.

### Controlling windows

#### Giving another tag to a window

Changing a window's tag is simple. To do so, simply bring the window into focus by hovering over it with your cursor. Then press `Shift` + `Mod1` + `x`, where `x` is the number of the tag to which you want to move the window. `Mod1` is, by default, the `Alt` key.

#### Closing a window

To cleanly close a window using dwm, simply press `Shift` + `Mod1` + `c`.

#### Window layouts

By default, dwm will operate in tiled mode. This can be observed by new windows on the same tag growing smaller and smaller as new windows are opened. The windows will, together, take up the entire screen (except for the menu bar) at all times. There are, however, two other modes: floating and monocle. Floating mode should be familiar to users of non-tiling window managers; it allows users to rearrange windows as they please. Monocle mode will keep a single window visible at all times.

To switch to floating mode, simply press `Mod1` + `F`. `Mod1` is, by default, the `Alt` key. To check if you are in floating mode, you should see something like this next to the numbered tags in the top right corner of the screen: ><>.

To switch to monocole mode, press `Mod1` + `M`. To check if you are in monocle mode, you can see an M in square brackets (if no windows are open on that tag) or a number in square brackets (which corresponds with the number of windows open on that tag). Thus, a tag with no windows open would display this: [M], and a tag with 'n' windows open would display this: [n].

To return to tiled mode, press `Mod1` + `T`. You will see a symbol which looks like this: []= .

For using alternate window layouts, see [#Window tiling patches](#Window_tiling_patches).

### Exiting dwm

To cleanly exit dwm, press `Shift` + `Mod1` + `q`.

## Tips and tricks

### Restart dwm without logging out or closing programs

For restarting dwm without logging out or closing applications, change or add a startup script so that it loads dwm in a _while_ loop, see below:

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

Then simply add the following to the startup script (e.g. `~/.xinitrc`), changing the keycode _113_ if necessary to the result gathered by the previous `xmodmap` command:

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

As of JRE 6u20, Java applications may misbehave in dwm because dwm is not a known window manager for [Java](/index.php/Java "Java"). The misbehavior may include menus closing when the mouse is released and other minor issues. Firstly, install the [wmname](https://www.archlinux.org/packages/?name=wmname) package.

Now use _wmname_ to set a WM name that Java recognizes:

```
$ wmname LG3D

```

**Note:** This may cause some programs to behave oddly when tiled (specifically [Chromium](/index.php/Chromium "Chromium")).

This setting is not persistent so you may want to add this command to your `.xinitrc` or `.xprofile`.

Alternatively, it is also possible to change enable `export _JAVA_AWT_WM_NONREPARENTING=1` in `/etc/profile.d/jre.sh`

### Fixing the extra topbar that does not disappear when changing resolution/monitors

**Note:** this patch is intended for dwm-6.0 which is currently in the [official repositories](/index.php/Official_repositories "Official repositories"). The development version of dwm has already implemented this.

When resizing or connecting/disconnecting different monitors there may be a remnant of the topbar stuck on the screen which cannot be removed. To fix this bug, rebuild dwm with [this patch](http://ix.io/fea).

### Fixing gaps around terminal windows

If there are empty gaps of desktop space outside terminal windows, it is likely due to the terminal's font size. Either adjust the size until finding the ideal scale that closes the gap, or toggle `resizehints` to _False_ in `config.h`:

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
*   [dwm: Tags are not workspaces](http://wongdev.com/blog/dwm-tags-are-not-workspaces/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dwm&oldid=416147](https://wiki.archlinux.org/index.php?title=Dwm&oldid=416147)"