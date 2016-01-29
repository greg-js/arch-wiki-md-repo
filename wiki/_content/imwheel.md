# imwheel

Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Mouse_acceleration](/index.php/Mouse_acceleration "Mouse acceleration")

_imwheel_ is a tool for tweaking mouse wheel behavior, on a per-program basis. It can map mousewheel input to keyboard input, increase mousewheel speed, and has support for modifier keys.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Getting the window class string](#Getting_the_window_class_string)
    *   [2.2 Edit your configuration file](#Edit_your_configuration_file)
    *   [2.3 Run imwheel](#Run_imwheel)

## Installation

imwheel is available from [AUR](/index.php/AUR "AUR") [imwheel](https://aur.archlinux.org/packages/imwheel/)<sup><small>AUR</small></sup> or directly from [The sourceforge page](http://imwheel.sourceforge.net/).

## Configuration

[The official HTML documentation (manpage)](http://imwheel.sourceforge.net/imwheel.1.html) is available in the official website.

imwheel matches window class strings with regular expressions for deciding which windows to apply tweaks to.

### Getting the window class string

Run _xprop_ to get the class string. The program will exit when a window is clicked.

```
xprop WM_CLASS | grep -o '"[^"]*"' | head -n 1

```

So for the document viewer _zathura_, this will return the following:

```
"zathura"

```

### Edit your configuration file

Create or edit `~/.imwheelrc`. In this configuration file lines can be added for each program you want to tweak mousewheel behavior for. The following example will increase the mousewheel speed for the document viewer _zathura_:

```
# Speed up scrolling for the document viewer
"^zathura$"
    None, Up, Button4, 4
    None, Down, Button5, 4

```

### Run imwheel

Run imwheel simply like so:

```
imwheel

```

The program will print its PID and run in the background. You may wish to run imwheel in a startup script.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Imwheel&oldid=411757](https://wiki.archlinux.org/index.php?title=Imwheel&oldid=411757)"