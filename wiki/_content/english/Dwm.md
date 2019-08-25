Related articles

*   [dmenu](/index.php/Dmenu "Dmenu")
*   [wmii](/index.php/Wmii "Wmii")

[dwm](https://dwm.suckless.org/) is a dynamic window manager for [Xorg](/index.php/Xorg "Xorg"). It manages windows in tiled, stacked, and full-screen layouts, as well as many others with the help of optional patches. Layouts can be applied dynamically, optimizing the environment for the application in use and the task being performed. dwm is extremely lightweight and fast, written in C and with a stated design goal of remaining under 2000 source lines of code. It provides [multihead](/index.php/Multihead "Multihead") support for [xrandr](/index.php/Xrandr "Xrandr") and Xinerama.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Configuration](#Configuration)
*   [2 Starting](#Starting)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Statusbar configuration](#Statusbar_configuration)
        *   [4.1.1 Conky statusbar](#Conky_statusbar)
    *   [4.2 Restart dwm](#Restart_dwm)
    *   [4.3 Bind the right Alt key to Mod4](#Bind_the_right_Alt_key_to_Mod4)
    *   [4.4 Space around font in dwm's bar](#Space_around_font_in_dwm's_bar)
    *   [4.5 Disable focus follows mouse](#Disable_focus_follows_mouse)
    *   [4.6 Floating layout for some windows](#Floating_layout_for_some_windows)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Fixing misbehaving Java applications](#Fixing_misbehaving_Java_applications)
    *   [5.2 Fixing gaps around terminal windows](#Fixing_gaps_around_terminal_windows)
*   [6 Known issues](#Known_issues)
    *   [6.1 Crashes due to Emojis in some fonts](#Crashes_due_to_Emojis_in_some_fonts)
*   [7 See also](#See_also)

## Installation

dwm can be installed with [dwm](https://aur.archlinux.org/packages/dwm/) or [dwm-git](https://aur.archlinux.org/packages/dwm-git/). Make any required [#Configuration](#Configuration) changes **before** building and installing, see [makepkg](/index.php/Makepkg "Makepkg").

### Configuration

dwm is configured at compile-time by editing some of its source files, specifically `config.h`. For detailed information on these settings see the included, well-commented `config.def.h` as well as the [customisation section](https://dwm.suckless.org/customisation/) on the dwm website.

The official website has a number of [patches](http://dwm.suckless.org/patches/) that can add extra functionality to dwm. These patches primarily make changes to the `dwm.c` file but also make changes to the `config.h` file where appropriate. For information on applying patches, see the [Patching packages](/index.php/Patching_packages "Patching packages") article.

## Starting

Select *Dwm* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice. Alternatively, to start dwm with [startx](/index.php/Startx "Startx") append `exec dwm` to `~/.xinitrc` and prepend other programs to execute them as well, for example:

```
redshift -O3500; xset r rate 300 50; exec dwm

```

## Usage

See the [dwm tutorial](https://dwm.suckless.org/tutorial) for information on basic dwm usage.

## Tips and tricks

### Statusbar configuration

For more examples of status bars see [[1]](https://dwm.suckless.org/status_monitor/).

**Note:** The following requires the [xorg-xsetroot](https://www.archlinux.org/packages/?name=xorg-xsetroot) package to be installed.

dwm reads the name of the root window and redirects it to the statusbar. The root window is the window within which all other windows are drawn and arranged by the window manager. Like any other window, the root window has a title/name, but it is usually undefined because the root window always runs in the background.

The information that you want dwm to show in the statusbar should be defined with `xsetroot -name ""` command in `~/.xinitrc` or `~/.xprofile` (if you are using a [display manager](/index.php/Display_manager "Display manager")). For example:

 `xsetroot -name "Thanks for all the fish!"` 

Dynamically updated information should be put in a loop which is forked to background - see the example below:

```
# Statusbar loop
while true; do
   xsetroot -name "$( date +"%F %R" )"
   sleep 1m    # Update time every minute
done &

# Autostart section
pcmanfm & 

exec dwm

```

In this case the date is shown in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601 "wikipedia:ISO 8601") format and [PCManFM](/index.php/PCManFM "PCManFM") is launched at startup.

**Note:** It is not recommended to set the update interval equal to zero or remove the "sleep" line entirely since this will cause CPU usage to rise substantially (you can assess the effect with *top* and [powertop](/index.php/Powertop "Powertop")).

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

### Restart dwm

To restart dwm without logging out or closing applications, change or add a startup script so that it loads dwm in a *while* loop, for example:

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

### Bind the right Alt key to Mod4

When using Mod4 (the Super/Windows Key) as the `MODKEY`, it may be equally convenient to have the right `Alt` key (`Alt_R`) act as `Mod4`. This will allow you to perform otherwise awkward keystrokes one-handed, such as zooming with `Alt_R`+`Enter`.

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

**Note:** There is a `#define` option in [config.h](#Configuration) which also allows you to switch the modkey.

### Space around font in dwm's bar

By default, dwm's bar adds 2px around the size of the font. To change this, modify the following line in `dwm.c`:

 `bh = dc.h = dc.font.height + 2;` 

### Disable focus follows mouse

To disable focus follows mouse behaviour comment out the following line in definiton of struct handler in `dwm.c`

 `[EnterNotify] = enternotify,` 

Note that this change can cause some difficulties; the first click on an inactive window will only bring the focus to it. To interact with window contents (buttons, fields etc) you need to click again. Also, if you have several monitors, you may notice that the keyboard focus does not switch to another monitor activated by clicking.

### Floating layout for some windows

For some windows, such as preferences dialogs, it does not make sense for these windows to be tiled - they should be free-floating instead. For example, to make Firefox's preferences dialog float, add the following to your rules array in `config.h`:

```
 { "Firefox",     NULL,       "Firefox Preferences",        1 << 8,         True,     -1 },

```

## Troubleshooting

### Fixing misbehaving Java applications

Try setting `export _JAVA_AWT_WM_NONREPARENTING=1`. Also see the [Java](/index.php/Java#Non-reparenting_window_managers_.2F_Grey_window_.2F_Programs_not_drawing_properly "Java") page.

### Fixing gaps around terminal windows

If there are empty gaps of desktop space outside terminal windows, it is likely due to the terminal's font size. Either adjust the size until finding the ideal scale that closes the gap, or toggle `resizehints` to *0* in `config.h`.

This will cause dwm to ignore resize requests from all client windows, not just terminals. The downside to this workaround is that some terminals may suffer redraw anomalies, such as ghost lines and premature line wraps, among others.

Alternatively, if you use the [st](/index.php/St "St") terminal emulator, you can apply the [anysize](https://st.suckless.org/patches/anysize/) patch and recompile st.

## Known issues

### Crashes due to Emojis in some fonts

Emojis in title bars may cause dwm to crash with an error similar to the following:

```
dwm: fatal error: request code=140, error code=16
X Error of failed request: BadLength (poly request too large or internal Xlib length error)
  Major opcode of failed request: 140 (RENDER)
  Minor opcode of failed request: 20 (RenderAddGlyphs)
  Serial number of failed request: 4319
  Current serial number in output stream: 4331

```

This only occurs with some fonts, such as [noto-fonts-emoji](https://www.archlinux.org/packages/?name=noto-fonts-emoji) and [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont). See [[2]](https://lists.suckless.org/dev/1608/30245.html), [[3]](https://lists.suckless.org/dev/1610/30710.html), [[4]](https://bbs.archlinux.org/viewtopic.php?id=226928), and [[5]](https://www.reddit.com/r/archlinux/comments/703ayu/anyone_with_dwm_and_notofontsemoji/). To workaround this uninstall the problematic font or use a different font for dwm.

Alternatively see [[6]](https://lists.suckless.org/dev/1610/30720.html) for a possible fix.

## See also

*   [dwm's official website](https://dwm.suckless.org/)
*   [Introduction to dwm video](http://www.youtube.com/watch?v=GQ5s6T25jCc)
*   [dmenu](/index.php/Dmenu "Dmenu") - Simple application launcher from the developers of dwm
*   The [dwm thread](https://bbs.archlinux.org/viewtopic.php?id=57549/) on the forums
*   [Hacking dwm thread](https://bbs.archlinux.org/viewtopic.php?id=92895/)
*   Check out the forums' [wallpaper thread](https://bbs.archlinux.org/viewtopic.php?id=57768/) for a selection of dwm wallpapers
*   [Show off your dwm configuration forum thread](https://bbs.archlinux.org/viewtopic.php?id=74599)