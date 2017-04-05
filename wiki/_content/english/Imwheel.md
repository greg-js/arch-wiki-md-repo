*imwheel* is a tool for tweaking mouse wheel behavior, on a per-program basis. It can map mousewheel input to keyboard input, increase mousewheel speed, and has support for modifier keys.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Getting the window class string](#Getting_the_window_class_string)
    *   [2.2 Edit your configuration file](#Edit_your_configuration_file)
    *   [2.3 Run imwheel](#Run_imwheel)

## Installation

imwheel is available from [AUR](/index.php/AUR "AUR") [imwheel](https://aur.archlinux.org/packages/imwheel/) or directly from [The sourceforge page](http://imwheel.sourceforge.net/).

## Configuration

[The official HTML documentation (manpage)](http://imwheel.sourceforge.net/imwheel.1.html) is available in the official website.

imwheel matches window class strings with regular expressions for deciding which windows to apply tweaks to.

### Getting the window class string

Run *xprop* to get the class string. The program will exit when a window is clicked.

```
xprop WM_CLASS | grep -o '"[^"]*"' | head -n 1

```

So for the document viewer *zathura*, this will return the following:

```
"zathura"

```

### Edit your configuration file

Create or edit `~/.imwheelrc`. In this configuration file lines can be added for each program you want to tweak mousewheel behavior for. The following example will increase the mousewheel speed for the document viewer *zathura*:

```
# Speed up scrolling for the document viewer
"^zathura$"
    None, Up, Button4, 4
    None, Down, Button5, 4

```

`Up` and `Down` may be used in the place of `Button4` and `Button5` respectively for the mousewheel.

Matching all programs (using ".*") can cause unwanted behaviour in some programs; since imwheel emulates multiple scroll actions for each one the user makes, programs that have actions bound to the mousewheel will perform those actions more times than expected.

For example, terminal emulators in which scrolling selects commands from the history will jump multiple items per scroll.

imwheel catches modifier keys for monitored mouse buttons, for passing them further you need to explicitly configure it to do so. In example below `Left Control` used with mousewheel is passed to chromium for zoom function without multiplying:

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

### Run imwheel

Run imwheel simply like so:

```
imwheel

```

The program will print its PID and run in the background. You may wish to run imwheel in a startup script.