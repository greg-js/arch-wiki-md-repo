Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Mouse_acceleration](/index.php/Mouse_acceleration "Mouse acceleration")

[IMWheel](http://imwheel.sourceforge.net/) is a tool for tweaking mouse wheel behavior, on a per-program basis. It can map mousewheel input to keyboard input, increase mousewheel speed, and has support for modifier keys.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Getting the window class string](#Getting_the_window_class_string)
    *   [2.2 Edit your configuration file](#Edit_your_configuration_file)
    *   [2.3 Run IMWheel](#Run_IMWheel)
    *   [2.4 Run IMWheel on startup](#Run_IMWheel_on_startup)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Back/forward buttons not working](#Back/forward_buttons_not_working)

## Installation

[Install](/index.php/Install "Install") the [imwheel](https://www.archlinux.org/packages/?name=imwheel) package.

## Configuration

See [imwheel(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/imwheel.1).

IMWheel matches window class strings with regular expressions for deciding which windows to apply tweaks to.

### Getting the window class string

Run *xprop* to get the class string. The program will exit when a window is clicked.

```
xprop WM_CLASS | grep -o '"[^"]*"' | head -n 1

```

So for the document viewer *zathura*, this will return the following:

```
"zathura"

```

Note that for some applications, the above method is unreliable (e.g. Java) and will return the wrong identifier for the window. In that case, you can run the following:

```
 imwheel -d --debug --kill

```

This will run IMWheel in the foreground in debug mode so you can see what Window IDs it's receiving when you scroll. This is also useful for debugging the regex matchers in your config file.

### Edit your configuration file

Create or edit `~/.imwheelrc`. In this configuration file lines can be added for each program you want to tweak mousewheel behavior for. The following example will increase the mousewheel speed for the document viewer *zathura*:

```
# Speed up scrolling for the document viewer
"^zathura$"
    None, Up, Button4, 4
    None, Down, Button5, 4

```

`Up` and `Down` may be used in the place of `Button4` and `Button5` respectively for the mousewheel.

Matching all programs (using ".*") can cause unwanted behaviour in some programs; since IMWheel emulates multiple scroll actions for each one the user makes, programs that have actions bound to the mousewheel will perform those actions more times than expected.

For example, terminal emulators in which scrolling selects commands from the history will jump multiple items per scroll.

IMWheel catches modifier keys for monitored mouse buttons, for passing them further you need to explicitly configure it to do so. In example below `Left Control` used with mousewheel is passed to chromium for zoom function without multiplying:

```
# Speed up scrolling for chromium and pass unchanged for zoom
"^chromium$"
    None, Up, Button4, 4
    None, Down, Button5, 4
    Shift_L,   Up,   Shift_L|Button4, 4
    Shift_L,   Down, Shift_L|Button5, 4
    Control_L, Up,   Control_L|Button4
    Control_L, Down, Control_L|Button5

```

### Run IMWheel

Run IMWheel simply like so:

```
imwheel

```

The program will print its PID and run in the background.

### Run IMWheel on startup

To avoid starting IMWheel manually, you can run it as part of your systemd startup.

Example:

 `~/.config/systemd/user/imwheel.service` 
```
[Unit]
Description=IMWheel
Wants=display-manager.service
After=display-manager.service

[Service]
Type=simple
Environment=XAUTHORITY=%h/.Xauthority
ExecStart=/usr/bin/imwheel -d
ExecStop=/usr/bin/pkill imwheel
RemainAfterExit=yes

[Install]
WantedBy=graphical.target

```

After installing the above:

```
 systemctl --user daemon-reload
 systemctl --user enable --now imwheel
 journalctl --user --unit imwheel

```

## Troubleshooting

### Back/forward buttons not working

You may need to restrict IMWheel so only the scroll wheel is affected to prevent it from breaking other mouse input like the back/forward buttons. You can do this with the -b option.

```
 imwheel -b 45

```

[See also this answer.](https://askubuntu.com/questions/421645/imwheel-destroys-back-forth-navigation-buttons-from-my-mouse)