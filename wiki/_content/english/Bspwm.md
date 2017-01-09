*bspwm* is a tiling window manager that represents windows as the leaves of a full binary tree. It has support for [EWMH](http://standards.freedesktop.org/wm-spec/wm-spec-1.3.html) and multiple monitors, and is configured and controlled through messages.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Note for multi-monitor setups](#Note_for_multi-monitor_setups)
    *   [2.2 Rules](#Rules)
    *   [2.3 Panels](#Panels)
    *   [2.4 Scratchpad](#Scratchpad)
    *   [2.5 Different monitor configurations for different machines](#Different_monitor_configurations_for_different_machines)
    *   [2.6 Set up a desktop where all windows are floating](#Set_up_a_desktop_where_all_windows_are_floating)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Help! I get a blank screen and my keybindings don't work!](#Help.21_I_get_a_blank_screen_and_my_keybindings_don.27t_work.21)
    *   [3.2 Window box larger than the actual application!](#Window_box_larger_than_the_actual_application.21)
    *   [3.3 Problems with Java applications](#Problems_with_Java_applications)
    *   [3.4 Problems with keybindings using fish](#Problems_with_keybindings_using_fish)
    *   [3.5 Error messages "Could not grab key 43 with modfield 68" on start](#Error_messages_.22Could_not_grab_key_43_with_modfield_68.22_on_start)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [bspwm](https://www.archlinux.org/packages/?name=bspwm) and [sxhkd](https://www.archlinux.org/packages/?name=sxhkd), or the development versions: [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/) and [sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/). Sxhkd is a simple X hotkey daemon used to communicate with bspwm through `bspc` as well as launch your applications of choice.

To start bspwm on login, add the following to `~/.xinitrc` or `~/.xprofile` (depending on how you launch X/your display manager):

```
sxhkd &
exec bspwm

```

The first line should be omitted if you have a command for running sxhkd in your bspwmrc config file (it is this way in the example config).

## Configuration

Example configuration is found at `/usr/share/doc/bspwm/examples/` and on [GitHub](https://github.com/baskerville/bspwm/blob/master/examples/).

**Important:** Make sure your environment variable $XDG_CONFIG_HOME is set or your bspwmrc will not be found. This can be done by adding XDG_CONFIG_HOME="$HOME/.config" and export XDG_CONFIG_HOME to your ~/.profile.

Create `~/.config/bspwm/` and `~/.config/sxhkd/`, then copy `/usr/share/doc/bspwm/examples/bspwmrc` to `~/.config/bspwm/` and `/usr/share/doc/bspwm/examples/sxhkdrc` to `~/.config/sxhkd/`. Make bspwmrc executable with `chmod +x ~/.config/bspwm/bspwmrc`.

These two files are where you will be setting wm settings and keybindings, respectively. See [bspwm/Example configurations](/index.php/Bspwm/Example_configurations "Bspwm/Example configurations") for annotated examples.

Documentation for bspwm is found by running `man bspwm`.

There is also documentation for sxhkd found by running `man sxhkd`.

#### Note for multi-monitor setups

The example bspwmrc configures ten desktops on one monitor like this:

```
bspc monitor -d I II III IV V VI VII VIII IX X

```

You will need to change this line and add one for each monitor, similar to this:

```
bspc monitor DVI-I-1 -d I II III IV
bspc monitor DVI-I-2 -d V VI VII
bspc monitor DP-1 -d VIII IX X

```

You can use `xrandr -q` or `bspc query -M` to find the monitor names.

The total number of desktops were maintained at ten in the above example. This is so that each desktop can still be addressed with 'super + {1-9,0}' in the sxhkdrc.

### Rules

There are two ways to set window rules (as of [cd97a32](https://github.com/baskerville/bspwm/commit/cd97a3290aa8d36346deb706fa307f5f8faa2f34)).

The first is by using the built in rule command, as shown in the example bspwmrc:

```
bspc rule -a Gimp desktop=^8 follow=on state=floating
bspc rule -a Chromium desktop=^2
bspc rule -a mplayer2 state=floating
bspc rule -a Kupfer.py focus=on
bspc rule -a Screenkey manage=off

```

The second option is to use an external rule command. This is more complex, but can allow you to craft more complex window rules. See [these examples](https://github.com/baskerville/bspwm/tree/master/examples/external_rules) for a sample rule command.

If a particular window does not seem to be behaving according to your rules, check the class name of the program. This can be accomplished by running `xprop | grep WM_CLASS` to make sure you're using the proper string.

### Panels

An example panel for [lemonbar](https://aur.archlinux.org/packages/lemonbar/) is provided in the examples folder on the GitHub page. You might also get some insights from the [lemonbar](/index.php/Lemonbar "Lemonbar") wiki page. The panel will be executed by placing `panel &` in your bspwmrc. Check the opt-depends in the bspwm package for dependencies that may be required.

To display system information on your status bar you can use various system calls. This example will show you how to edit your `panel` to get the volume status on your BAR:

```
panel_volume()
{
        volStatus=$(amixer get Master | tail -n 1 | cut -d '[' -f 4 | sed 's/].*//g')
        volLevel=$(amixer get Master | tail -n 1 | cut -d '[' -f 2 | sed 's/%.*//g')
        # is alsa muted or not muted?
        if [ "$volStatus" == "on" ]
        then
                echo "%{Fyellowgreen} $volLevel %{F-}"
        else
                # If it is muted, make the font red
                echo "%{Findianred} $volLevel %{F-}"
        fi
}
```

Next, we will have to make sure it is called and piped to `$PANEL_FIFO`:

```
while true; do
echo "S" "$(panel_volume) $(panel_clock)" > "$PANEL_FIFO"
        sleep 1s
done &

```

### Scratchpad

You can emulate a dropdown terminal (like i3's scratchpad feature if you put a terminal in it) using bspwm's window flags. Append the following to the end of the bspwm config file (adapt to your own terminal emulator):

```
bspc rule -a scratchpad sticky=on state=floating hidden=on
st -c scratchpad -e ~/bin/scratch &

```

The sticky flag ensures that the window is always present on the current desktop. And `~/bin/scratch` is:

```
#!/usr/bin/sh
bspc query -N -n .floating > /tmp/scratchid
$SHELL

```

The hotkey for toggling the scratchpad should be bound to:

```
id=$(cat /tmp/scratchid);\
bspc node $id --flag hidden;bspc node -f $id

```

For a scratch-pad which can use any window type without pre-defined rules, see: [[1]](https://www.reddit.com/r/bspwm/comments/3xnwdf/i3_like_scratch_for_any_window_possible/cy6i585)

For a more sophisticated scratchpad script that supports many terminals out of the box and has flags for doing things like optionally starting a tmuxinator/tmux session, turning any window into a scratchpad on the fly, and automatically resizing a scratchpad to fit the current monitor see [tdrop-git](https://aur.archlinux.org/packages/tdrop-git/).

### Different monitor configurations for different machines

Since the `bspwmrc` is a shell script, it allows you to do things like these:

```
#! /bin/sh

 if [[ $(hostname) == 'myhost' ]]; then
     bspc monitor eDP1 -d I II III IV V VI VII VIII IX X
 elif [[ $(hostname) == 'otherhost' ]]; then
     bspc monitor VGA-0 -d I II III IV V
     bspc monitor VGA-1 -d VI VII VIII IX X
 elif [[ $(hostname) == 'yetanotherhost' ]]; then
     bspc monitor DVI-I-3 -d VI VII VIII IX X
     bspc monitor DVI-I-2 -d I II III IV V
 fi

```

### Set up a desktop where all windows are floating

Here is how to setup the desktop 3 to have only floating windows. It can be useful for Gimp or other apps with multiple windows.

Put this script somewhere in your $PATH and call it from .xinitrc or similar (with a & at the end):

```
#!/bin/bash

 # change the desktop number here
 FLOATING_DESKTOP_ID=$(bspc query -D -d '^3')

 bspc subscribe node_manage | while read -a msg ; do
    desk_id=${msg[2]}
    wid=${msg[3]}
    [ "$FLOATING_DESKTOP_ID" = "$desk_id" ] && bspc node "$wid" -t floating
 done

```

([source](https://github.com/baskerville/bspwm/issues/428#issuecomment-199985423))

## Troubleshooting

### Help! I get a blank screen and my keybindings don't work!

There are a few ways to debug this. First, a blank screen is good. That means bspwm is running.

I would confirm that your xinitrc looks something like

```
sxhkd &
exec bspwm

```

The ampersand is important. Next, try spawning a terminal in your xinitrc to see if its getting positioned properly. It should appear somewhat "centered" on the screen. To do this, use this .xinitrc:

```
sxhkd &
urxvt &
exec bspwm

```

If nothing shows up, that means you probably forgot to install urxvt. If it shows up but isn't centered or taking up most of your screen, that means BSPWM isn't getting started properly. Make sure that you've `chmod +x ~/.config/bspwm/bspwmrc` .

Next, type `pidof sxhkd` in that terminal you spawned. It should return a number. If it doesn't, that means sxhd isn't running. Try to be explicit and run `sxhkd -c ~/.config/sxhkd/sxhkdrc` . You could also try changing the Super key to something like Alt in your sxhkdrc and see if that helps. Another common problem is copying the text from the example files instead of physically copying the file over. Copying / pasting code usually leads to indentation issues which sxhkd can be sensitive to.

### Window box larger than the actual application!

This can happen if you are using GTK3 apps and usually for dialog windows. The fix is to create or add the below to a gtk3 theme file (~/.config/gtk-3.0/gtk.css).

```
.window-frame, .window-frame:backdrop {
  box-shadow: 0 0 0 black;
  border-style: none;
  margin: 0;
  border-radius: 0;
}

.titlebar {
  border-radius: 0;
}

```

(source: [Bspwm forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1404973#p1404973))

### Problems with Java applications

If you have problems, like Java application Windows not resizing, or menus immediately closing after you click, see [Java#Applications not resizing with WM, menus immediately closing](/index.php/Java#Applications_not_resizing_with_WM.2C_menus_immediately_closing "Java").

### Problems with keybindings using fish

If you use [fish](/index.php/Fish "Fish"), you will find that you are unable to switch desktops. This is because bspc's use of the ^ character is incompatible with fish. You can fix this by explicitly telling sxhkd to use bash to execute commands:

```
$ set -U SXHKD_SHELL /usr/bin/bash

```

Alternatively, the ^ character may be escaped with a backslash in your sxhkdrc file.

### Error messages "Could not grab key 43 with modfield 68" on start

Either you try to use the same key twice, or you start sxhkd twice. Check bspwmrc and `~/.profile` or `~/.bash_profile` for excessive commands starting sxhkd.

## See also

*   Mailing List: bspwm *at* librelist.com.
*   `#bspwm` - IRC channel at irc.freenode.net
*   [https://bbs.archlinux.org/viewtopic.php?id=149444](https://bbs.archlinux.org/viewtopic.php?id=149444) - Arch BBS thread
*   [https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) - GitHub project
*   [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies) - earsplit's "bspwm for dummies"
*   [https://github.com/smlb/dotfiles/wiki/Bspwm](https://github.com/smlb/dotfiles/wiki/Bspwm) - smlb's wiki