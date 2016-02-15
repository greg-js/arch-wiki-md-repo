Xbindkeys is a program that allows to bind commands to certain keys or key combinations on the keyboard. Xbindkeys works with multimedia keys and is window manager / DE independent, so if you switch much, xbindkeys is very handy.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Xbindkeysrc](#Xbindkeysrc)
    *   [2.2 GUI method](#GUI_method)
*   [3 Identifying keycodes](#Identifying_keycodes)
*   [4 Making changes permanent](#Making_changes_permanent)
*   [5 Simulating multimedia keys](#Simulating_multimedia_keys)
*   [6 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") Xbindkeys with the package [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys), available in the [official repositories](/index.php/Official_repositories "Official repositories").

For those who prefer a GUI, there is the [xbindkeys_config-gtk2](https://aur.archlinux.org/packages/xbindkeys_config-gtk2/) package in the [AUR](/index.php/AUR "AUR").

## Configuration

Create a file named `.xbindkeysrc` in your home directory:

```
$ touch ~/.xbindkeysrc

```

Alternatively, you can create a sample file (Note this includes some bindings such as `Ctrl+f`, which you may want to edit or remove):

```
$ xbindkeys -d > ~/.xbindkeysrc

```

Now you can either edit `~/.xbindkeysrc` to set keybindings, or you can do that with the GUI.

### Xbindkeysrc

The first line represents a command. The second contains the state (0x8) and keycode (32) as reported by `xev`. The third line contains the keysyms associated with the given keycodes. To use this output, copy either one of the last two lines to `~/.xbindkeysrc` and replace "(Scheme function)" with the command you wish to perform. Here is an example configuration file that binds Fn key combos on a laptop to [pamixer](https://www.archlinux.org/packages/?name=pamixer) commands that adjust sound volume. Note that pound (#) symbols can be used to create comments.

```
# Increase volume
"pamixer --increase 5"
   XF86AudioRaiseVolume

```

```
# Decrease volume
"pamixer --decrease 5"
   m:0x0 + c:122

```

or

```
"pamixer --decrease 5"
   XF86AudioLowerVolume

```

Alternatively, instead of [pamixer](https://www.archlinux.org/packages/?name=pamixer) it is also possible to use _pactl_ to control a running [PulseAudio](/index.php/PulseAudio "PulseAudio") and to change volume level (replace above _pamixer_ command with the following):

```
pactl set-sink-volume 0 +2%
pactl set-sink-volume 0 -2%
pactl set-sink-mute 0 toggle

```

Instead of setting forcefully sink number it is possible to use `@DEFAULT_SINK@`:

```
pactl set-sink-volume @DEFAULT_SINK@ +2%
pactl set-sink-volume @DEFAULT_SINK@ -2%
pactl set-sink-mute @DEFAULT_SINK@ toggle

```

Another possibility is to use amixer (part of the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package)

```
amixer -c 1 set Master 5+
amixer -c 1 set Master 5-
amixer -c 1 set Master toggle

```

**Tip:** After you made a change, execute `xbindkeys -p` to reload the configuration file and apply the changes.

### GUI method

If you installed the [xbindkeys_config](https://aur.archlinux.org/packages/xbindkeys_config/) package, just run:

```
$ xbindkeys_config

```

## Identifying keycodes

To find the keycodes for a particular key, enter the following command:

```
$ xbindkeys -k

```

A blank window will pop up. Press the key(s) to which you wish to assign a command and _xbindkeys_ will output a handy snippet that can be entered into `~/.xbindkeysrc`. For example, while the blank window is open, press `Alt+o` to get the following output (results may vary):

```
"(Scheme function)"
    m:0x8 + c:32
    Alt + o

```

**Tip:** Use `xbindkeys -mk` to keep the key prompt open for multiple keypresses. Press `q` to quit.

## Making changes permanent

Once you're done configuring your keys, edit your [xprofile](/index.php/Xprofile "Xprofile") or [xinitrc](/index.php/Xinitrc "Xinitrc") file (depending on your window manager) and place

```
xbindkeys

```

before the line that starts your window manager or DE.

## Simulating multimedia keys

The XF86Audio* and other multimedia keys [[1]](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols) are pretty-much well-recognized by the major DEs. For keyboards without such keys, you can simulate their effect with other keys

```
# Decrease volume on pressing Super-minus
"amixer set Master playback 1-"
   m:0x50 + c:20
   Mod2+Mod4 + minus

```

However, to actually call the keys themselves you can use tools like [xdotool](https://www.archlinux.org/packages/?name=xdotool) (from [official repositories](/index.php/Official_repositories "Official repositories")) and [xmacro](https://aur.archlinux.org/packages/xmacro/) (from the [AUR](/index.php/AUR "AUR")). Unfortunately since you'd already be holding down some modifier key (Super or Shift, for example), X will see the result as `Super-XF86AudioLowerVolume` which won't do anything useful. Here's a script based on _xmacro_ and _xmodmap_ from the [xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils) package for doing this[[2]](https://bbs.archlinux.org/viewtopic.php?pid=843395).

```
#!/bin/sh
echo 'KeyStrRelease Super_L KeyStrRelease minus' 
```

This works for calling XF86AudioLowerVolume once (assuming you are using `Super+minus`), but repeatedly calling it without releasing the Super key (like tapping on a volume button) does not work. If you would like it to work that way, add the following line to the bottom of the script.

```
echo 'KeyStrPress Super_L' | xmacroplay :0

```

With this modified script, if you press the key combination fast enough your Super_L key will remain 'on' till the next time you hit it, which may result in some interesting side-effects. Just tap it again to remove that state, or use the original script if you want things to 'just work' and do not mind not multi-tapping on volume up/down.

These instructions are valid for pretty much any one of the XF86 multimedia keys (important ones would be XF86AudioRaiseVolume, XF86AudioLowerVolume, XF86AudioPlay, XF86AudioPrev, XF86AudioNext).

## Troubleshooting

If, for any reason, a hotkey you _already_ set in `~/.xbindkeysrc` doesn't work, open up a terminal and type the following:

```
$ xbindkeys -n

```

By pressing the non-working key, you will be able to see any error _xbindkeys_ encounter (e.g: mistyped command/keycode,...).