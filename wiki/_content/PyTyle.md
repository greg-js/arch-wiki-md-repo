# PyTyle

**[PyTyle](http://code.google.com/p/pytyle/)** is a tiling manager that works with EWMH-compliant window managers (like [Openbox](/index.php/Openbox "Openbox") and KWin) to provide functions for tiling windows. Both Xmonad and Musca have influenced the feature set.

## Contents

*   [1 Installation](#Installation)
*   [2 Execution](#Execution)
*   [3 Configuration](#Configuration)
*   [4 Gaps between terminals](#Gaps_between_terminals)

## Installation

PyTyle is currently not available from the Arch official repositories.

*   **PyTyle** — An automatic tiler that is compatible with Openbox Multihead.

	[https://sourceforge.net/projects/pytyle/](https://sourceforge.net/projects/pytyle/) || [pytyle](https://aur.archlinux.org/packages/pytyle/)

*   **PyTyle2** — Auto/manual on-demand tiling manager that fits in any EWMH compatible window manager.

	[https://code.google.com/p/pytyle/](https://code.google.com/p/pytyle/) || [pytyle2-hg](https://aur.archlinux.org/packages/pytyle2-hg/)

*   **PyTyle3** — An automatic tiler that is compatible with Openbox Multihead with faster action and lower memory footprint.

	[https://github.com/BurntSushi/pytyle3](https://github.com/BurntSushi/pytyle3) || [pytyle3-git](https://aur.archlinux.org/packages/pytyle3-git/)

**Note:** Any can be installed on the same system, although only one can be run at the same time.

## Execution

After installation, PyTyle can be run simply by entering this into the terminal:

```
pytyle

```

Alternatively, if you want to run PyTyle2 or PyTyle3, you would run

```
pytyle2

```

or

```
pytyle3

```

After that, simply press `Alt` + `A`(default keybind).

## Configuration

*   PyTyle2

After you have started PyTyle for the first time, a new configuration directory should appear in your `$XDG_CONFIG_HOME` directory (usually ~/.config/) called pytyle2\. Inside this directory is config.ini. All of the configuration options are stored there.

**Warning:** The options haven't really been documented yet, so your guess will have to do at the moment.

*   PyTyle3

You need to create pytyle3 directory in your `$XDG_CONFIG_HOME` directory and the configs in `/etc/xdg/pytyle3/` can be a base of your custom configuration. All these configuration are in Python2, it is easy to understand and to edit. But if you make any gramma error or something like that, it will cause pytyle3 fail to start with a backtrace.

## Gaps between terminals

Depending on your window manager, some gaps may appear between the windows when a terminal is launched. This is due to the imposed size of some terminal emulators. Using [Urxvt](/index.php/Urxvt "Urxvt"), install the patched package rxvt-unicode-noinc from the AUR. Using [Terminator](/index.php/Terminator "Terminator"), disable the "Window Geometry Hint" checkbox in the main options.

Retrieved from "[https://wiki.archlinux.org/index.php?title=PyTyle&oldid=392600](https://wiki.archlinux.org/index.php?title=PyTyle&oldid=392600)"