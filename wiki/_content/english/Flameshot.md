[Flameshot](https://flameshot.js.org) is a program for taking screenshots. It has an interactive GUI with controls to select the desired capture region, move and resize the capture window, make edits with common drawing tools (pencil, line, rectangle, circle, blur, undo/redo), and choose the output destination (copy to clipboard, save to disk, upload to [Imgur](https://imgur.com), open with another program).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Sub-commands exit immediately with no output](#Sub-commands_exit_immediately_with_no_output)
        *   [2.1.1 Option 1: Use *dbus-launch*](#Option_1:_Use_dbus-launch)
        *   [2.1.2 Option 2: Run as background process](#Option_2:_Run_as_background_process)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [flameshot](https://www.archlinux.org/packages/?name=flameshot) package, or [flameshot-git](https://aur.archlinux.org/packages/flameshot-git/) for the development version.

## Troubleshooting

### Sub-commands exit immediately with no output

#### Option 1: Use *dbus-launch*

Some [X](/index.php/X "X") clients ([dwm](/index.php/Dwm "Dwm"), [i3](/index.php/I3 "I3"), [xmonad](/index.php/Xmonad "Xmonad"), possibly others) must be started with *dbus-launch* in order for Flameshot to start when using its sub-commands (e.g., `flameshot gui`, `flameshot config`).

For example, using [xinit](/index.php/Xinit "Xinit"):

 `~/.xinitrc` 
```
...

exec dbus-launch dwm
```

See [dbus-launch(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dbus-launch.1) for more information.

#### Option 2: Run as background process

Alternatively, you can start Flameshot as a background process at any time during your X session:

```
$ flameshot &

```

## See also

*   [Official website](https://flameshot.js.org)
*   Claims that using *dbus-launch* fixes sub-command problems: `[xmonad](https://github.com/lupoDharkael/flameshot/issues/168#issuecomment-377851744)`, `[i3](https://github.com/lupoDharkael/flameshot/issues/90#issuecomment-398322771)`