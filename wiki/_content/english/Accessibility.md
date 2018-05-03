Related articles

*   [TalkingArch](/index.php/TalkingArch "TalkingArch")

There are many different methods of providing accessibility to users that suffer from a physical or visual handicap. However, unless a [desktop environment](/index.php/Desktop_environment "Desktop environment") is used, the configuration might require some tinkering until one gets it right.

## Contents

*   [1 Desktop environments](#Desktop_environments)
*   [2 Independent to specific desktop environments](#Independent_to_specific_desktop_environments)
    *   [2.1 Operating the keyboard](#Operating_the_keyboard)
        *   [2.1.1 Sticky keys with systemd](#Sticky_keys_with_systemd)
        *   [2.1.2 Sticky keys with xserverrc](#Sticky_keys_with_xserverrc)
    *   [2.2 Operating the mouse](#Operating_the_mouse)
        *   [2.2.1 Button mapping](#Button_mapping)
        *   [2.2.2 Mouse keys](#Mouse_keys)
    *   [2.3 Visual assistance](#Visual_assistance)
        *   [2.3.1 Speech recognition](#Speech_recognition)
        *   [2.3.2 Console and Virtual Terminal Emulators](#Console_and_Virtual_Terminal_Emulators)
*   [3 Known issues](#Known_issues)

## Desktop environments

Most modern desktop environments ship with an extensive set of features, among which one can find a tool to configure the accessibility options with. Generally, these options can be found listed under those of 'accessibility', or under those of the corresponding input device (e.g. 'keyboard' and 'mouse'). For example, with [GNOME](https://help.gnome.org/users/gnome-help/stable/a11y.html.en) and [KDE](https://userbase.kde.org/Applications/Accessibility).

**Note:** When using the configuration tools of a desktop environment, be weary of possible conflicts with settings of desktop-environment-independent tools.

## Independent to specific desktop environments

The [Xorg](/index.php/Xorg "Xorg") server has features (accessx) for physical assistance by setting parameters via the [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension"). This section covers examples.

For speech recognition, see also [Text to speech](/index.php/Text_to_speech "Text to speech").

### Operating the keyboard

For Braille, see [Arch Linux for the blind](/index.php/Arch_Linux_for_the_blind "Arch Linux for the blind").

#### Sticky keys with systemd

In order to enable Sticky Keys in a TTY, you require to know the exact keycodes of the keys to be used. These can be found by a tool like [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) or [xkeycaps](https://www.archlinux.org/packages/?name=xkeycaps). Alternatively, you can inspect the output of *dumpkeys*, provided that the current keymap is correct.

For example, a Logitech Ultra-X will provide the following keycodes for the modifier keys:

```
LCtrl = 29
LShift = 42
LAlt = 56
RShift = 54
RCtrl = 97

```

Next, use *dumpkeys* to determine the range of the keycodes:

```
# dumpkeys | head -1
keymaps 0-63

```

Continue by creating a new file with a suitable name, e.g. "stickyKeys", and use your favourite editor to combine the previously-found information with the desired key function.

In case of the keycodes found earlier, you would get:

```
keymaps 0-63
keycode 29 = SCtrl
keycode 42 = SShift
keycode 56 = SAlt
keycode 54 = SShift
keycode 97 = SCtrl

```

Here, the letter "S" in front of a modifier key denotes that we want the sticky version of that key.

**Note:** The following step will change your key mapping in all TTYs. Ensure the correctness of your keycodes, or you might lose the ability to use certain important keys.

Load your new mapping by running the following command:

```
# loadkeys ./stickyKeys

```

If you are satisfied by the results, then move the file to a suitable directory. To have it [enabled](/index.php/Enable "Enable") on boot, see the following systemd unit:

 `/etc/systemd/system/loadkeys.service` 
```
[Unit]
Description="load custom keymap (sticky keys)"

[Service]
Type=oneshot
ExecStart=/usr/bin/loadkeys /path/to/stickyKeys
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target emergency.target rescue.target
```

#### Sticky keys with xserverrc

One method of enabling desktop environment-independent accessibility function is by passing it through X, given that it is build with XKB support. This can be done by setting parameters for the X server, as specified in its man page:

```
[+-]accessx [ timeout [ timeout_mask [ feedback [ options_mask ] ] ] ]
              enables(+) or disables(-) AccessX key sequences (Sticky Keys).

-ardelay milliseconds
              sets the autorepeat delay (length of time in milliseconds  that
              a key must be depressed before autorepeat starts).

-arinterval milliseconds
              sets  the  autorepeat  interval (length of time in milliseconds
              that should elapse between autorepeat-generated keystrokes).

```

These parameters must be placed in the file `~/.xserverrc`, which you may need to create.

For example, to enable Sticky Keys without timeout and without audible or visible feedback, the following can be used:

```
if [ -z "$XDG_VTNR" ]; then
  exec /usr/bin/X -nolisten tcp "$@" +accessx 0 0x1e 0 0xcef
else
  exec /usr/bin/X -nolisten tcp "$@" vt$XDG_VTNR +accessx 0 0x1e 0 0xcef
fi

```

Note that once X has started, e.g. by executing `startx`, it still requires you to press the shift key 5 times to enable Sticky Keys. Unfortunately, this is needed each time X starts. Alternatively, a script can be used to automate this process.

Similar to most implementations, Sticky Keys can be disabled by pressing a modifier key and any other key at the same time.

### Operating the mouse

#### Button mapping

By using *xmodmap*, you can map functions to mouse buttons independent of your graphical environment. For this, you need to know which physical button on your mouse is read as which number, which can be found by a tool such as [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev). Generally, the physical buttons of left, middle, and right are read as the first, second, and third button, respectively.

Once you have acquired these, continue by creating a configuration file on a suitable location, e.g. `~/.mouseconfig`. Next, open the file with your favourite editor, and write the keyword `pointer =` followed by an enumeration of the previously-found number of mouse buttons.

For example, a three button mouse with a scroll wheel is able to provide five physical actions: left, middle, and right click, as well as scroll up and scroll down. This can be mapped to the same functions by using the following line in the configuration file:

```
pointer = 1 2 3 4 5

```

Here, the location will tell the action required to perform an internal mouse-button function. For example, a mapping for left-handed people (left- and right button switched) might look like

```
pointer = 3 2 1 4 5

```

When you are done, you can test and inspect your mapping by running `xmodmap`:

```
$ xmodmap ~/.mouseconfig
$ xmodmap -pp

```

Once satisfied, you can enable it on start by placing the first line in `~/.xinitrc`.

#### Mouse keys

[Mouse keys](https://en.wikipedia.org/wiki/Mouse_keys "w:Mouse keys") is a Xorg feature (like StickyKeys) to use the keyboard (especially a numeric keypad) as a pointing device. It can replace a mouse, or work beside it. It is disabled by default. You can use

```
$ xset q | grep "Mouse Keys"

```

to see status. To enable it for a session:

```
$ setxkbmap -option keypad:pointerkeys

```

If you use a [xmodmap](/index.php/Xmodmap "Xmodmap") configuration, be aware *setxkbmap* resets it.

To enable Mouse keys permanently, add

```
Option "XkbOptions" "keypad:pointerkeys" 

```

to the keyboard configuration file. This will make the `Shift+NumLock` shortcut toggle mouse keys.

For more see [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg") and [X KeyBoard extension#Mouse control](/index.php/X_KeyBoard_extension#Mouse_control "X KeyBoard extension") for advanced configuration.

### Visual assistance

As with physical assistance, most modern desktop environments ship with an extensive set of features to tweak the visual aspects of your system. Generally, these options can be found listed under those of 'accessibility' or 'visual assistance'. Alternatively, useful options might be found in the settings of the individual applications.

#### Speech recognition

See [Speech recognition](/index.php/Speech_recognition "Speech recognition").

#### Console and Virtual Terminal Emulators

*   Edit `/etc/vconsole.conf`.
*   Edit `~/.Xresources`.

## Known issues

*   Configuration of input devices is not recognized by software that circumvents the software layer, e.g. [wine](/index.php/Wine "Wine"), [VirtualBox](/index.php/VirtualBox "VirtualBox"), and [QEMU](/index.php/QEMU "QEMU").