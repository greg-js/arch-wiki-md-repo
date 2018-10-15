Related articles

*   [Xmodmap](/index.php/Xmodmap "Xmodmap")
*   [Sxhkd](/index.php/Sxhkd "Sxhkd")
*   [Xorg#Automation](/index.php/Xorg#Automation "Xorg")

Xbindkeys is a program that allows to bind commands to certain keys or key combinations on the keyboard. Xbindkeys works with multimedia keys and is independent of the window manager and desktop environment.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Volume control](#Volume_control)
    *   [2.2 Backlight control](#Backlight_control)
    *   [2.3 GUI method](#GUI_method)
*   [3 Identifying keycodes](#Identifying_keycodes)
*   [4 Making changes permanent](#Making_changes_permanent)
*   [5 Simulating multimedia keys](#Simulating_multimedia_keys)
*   [6 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) package.

## Configuration

Create a blank `~/.xbindkeysrc`, or you can create a sample file (Note this includes some bindings such as `Ctrl+f`, which you may want to edit or remove):

```
$ xbindkeys -d > ~/.xbindkeysrc

```

Now you can either edit `~/.xbindkeysrc` to set keybindings, or you can do that with the [#GUI method](#GUI_method).

**Tip:** After you made a change, execute `xbindkeys --poll-rc` to reload the configuration file and apply the changes.

### Volume control

Here is an example configuration file that binds `Fn` key combos on a laptop to *pactl* commands that adjust sound volume. Note that pound (#) symbols can be used to create comments.

```
# Increase volume
"pactl set-sink-volume @DEFAULT_SINK@ +1000"
   XF86AudioRaiseVolume

```

```
# Decrease volume
"pactl set-sink-volume @DEFAULT_SINK@ -1000"
   XF86AudioLowerVolume

```

```
# Mute volume
"pactl set-sink-mute @DEFAULT_SINK@ toggle"
   XF86AudioMute

```

For alternative commands to control volume, see [PulseAudio#Keyboard volume control](/index.php/PulseAudio#Keyboard_volume_control "PulseAudio") or [ALSA#Keyboard volume control](/index.php/ALSA#Keyboard_volume_control "ALSA").

### Backlight control

Keybindings can also be defined in order to control the brightness of the screen.

```
# Increase backlight
"xbacklight -inc 10"
   XF86MonBrightnessUp

```

```
# Decrease backlight
"xbacklight -dec 10"
   XF86MonBrightnessDown

```

### GUI method

For graphical configuration [install](/index.php/Install "Install") the [xbindkeys_config-gtk2](https://aur.archlinux.org/packages/xbindkeys_config-gtk2/) package and run:

```
$ xbindkeys_config

```

## Identifying keycodes

To find the keycodes for a particular key, enter the following command:

```
$ xbindkeys --key

```

or the following to grab multiple keys:

```
$ xbindkeys --multikey

```

A blank window will pop up. Press the key(s) to which you wish to assign a command and *xbindkeys* will output a handy snippet that can be entered into `~/.xbindkeysrc`. For example, while the blank window is open, press `Alt+o` to get the following output (results may vary):

```
"(Scheme function)"
    m:0x8 + c:32
    Alt + o

```

1.  The first line represents a command.
2.  The second line contains the state (0x8) and keycode (32) as reported by the tool *xev*.
3.  The third line contains the keysyms associated with the given keycodes.

To use this output, copy either one of the last two lines to `~/.xbindkeysrc` and replace "(Scheme function)" with the command you wish to perform.

To identify mouse buttons, *xev* can be used, see [[1]](https://blog.hanschen.org/2009/10/13/mouse-shortcuts-with-xbindkeys/).

**Tip:** If the multikey mode is used, press `q` to quit the window.

**Note:** *xev* is provided within the [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) package, see [xev(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xev.1) for more information.

## Making changes permanent

Once you are done configuring your keys, edit your [xprofile](/index.php/Xprofile "Xprofile") or [xinitrc](/index.php/Xinitrc "Xinitrc") file (depending on your window manager) and place

```
xbindkeys

```

before the line that starts your window manager or DE.

## Simulating multimedia keys

The XF86Audio* and other multimedia keys [[2]](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols) are pretty-much well-recognized by the major DEs. For keyboards without such keys, you can simulate their effect with other keys

```
# Decrease volume on pressing Super-minus
"pactl set-sink-volume 0 -1000"
   m:0x50 + c:20
   Mod2+Mod4 + minus

```

However, to actually call the keys themselves you can use tools like [xdotool](https://www.archlinux.org/packages/?name=xdotool) and [xmacro](https://aur.archlinux.org/packages/xmacro/). Unfortunately since you would already be holding down some modifier key (Super or Shift, for example), X will see the result as `Super-XF86AudioLowerVolume` which will not do anything useful. Here is a script based on *xmacro* and *xmodmap* from the [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap) package for doing this[[3]](https://bbs.archlinux.org/viewtopic.php?pid=843395).

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

If, for any reason, a hotkey you *already* set in `~/.xbindkeysrc` does not work, open up a terminal and type the following:

```
$ xbindkeys -n

```

By pressing the non-working key, you will be able to see any error *xbindkeys* encounter (e.g: mistyped command/keycode,...).

If the command for a keybind works via the xdotool in command line, but not when activated by the hotkey try adding "+ Release" to the hotkey (Esp notable on gnome):

```
"xdotool key --clearmodifiers XF86AudioPlay"
    Mod2 + F7 + Release

```

This will make the `F7` key play/pause audio. Where the "xdotool" command would work in commandline, if the "+ Release" is removed it will fail with xbindkeys.