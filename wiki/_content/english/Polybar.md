[polybar](https://github.com/jaagr/polybar) is a fast and easy-to-use tool for creating status bars. It aims to be easily customizable, utilising many modules which enable a wide range of (editable) functionality, such as displaying workspaces, the date, or system volume. Polybar is especially useful for [Window Managers](/index.php/Window_Manager "Window Manager") that have a limited or non-existent status bar, such as [awesome](/index.php/Awesome "Awesome") or [i3](/index.php/I3 "I3"). Polybar can also be used on full [Desktop Environments](/index.php/Desktop_Environment "Desktop Environment") like [Plasma](/index.php/Plasma "Plasma").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Running Polybar](#Running_Polybar)
    *   [2.2 Running with WM](#Running_with_WM)
        *   [2.2.1 bspwm](#bspwm)
        *   [2.2.2 i3](#i3)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [polybar](https://aur.archlinux.org/packages/polybar/) package. The development version is [polybar-git](https://aur.archlinux.org/packages/polybar-git/).

## Configuration

#### Running Polybar

Polybar can be run with the following:

```
Usage: polybar [OPTION]... BAR

  -h, --help               Display this help and exit
  -v, --version            Display build details and exit
  -l, --log=LEVEL          Set the logging verbosity (default: WARNING)
                           LEVEL is one of: error, warning, info, trace
  -q, --quiet              Be quiet (will override -l)
  -c, --config=FILE        Path to the configuration file
  -r, --reload             Reload when the configuration has been modified
  -d, --dump=PARAM         Print value of PARAM in bar section and exit
  -m, --list-monitors      Print list of available monitors and exit
  -w, --print-wmname       Print the generated WM_NAME and exit
  -s, --stdout             Output data to stdout instead of drawing it to the X window
  -p, --png=FILE           Save png snapshot to FILE after running for 3 seconds

```

However you will probably want to run Polybar with your Window Managers bootstrap routine. See [#Running with WM](#Running_with_WM)

#### Running with WM

Create an [executable](/index.php/Executable "Executable") file containing the startup logic, for example `$HOME/.config/polybar/launch.sh`:

```
#!/bin/bash

# Terminate already running bar instances
killall -q polybar

# Wait until the processes have been shut down
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done

# Launch Polybar, using default config location ~/.config/polybar/config
polybar &

echo "Polybar launched..."

```

This script will mean that restarting your WM will also restart Polybar. You can add additional syntax here as well, such as:

```
MONITOR=HDMI-A-1 polybar &

```

This will display Polybar on the specified monitor, of which the name can be found out using the command `[xrandr](/index.php/Xrandr "Xrandr")`. You can also specify the position of Polybar:

```
polybar top &

```

###### bspwm

If using [bspwm](/index.php/Bspwm "Bspwm"), add the following to `bspwmrc`:

```
$HOME/.config/polybar/launch.sh

```

###### i3

If using [i3](/index.php/I3 "I3"), add the following to your configuration:

```
exec_always --no-startup-id $HOME/.config/polybar/launch.sh

```

## See also

*   [Polybar Github Wiki](https://github.com/jaagr/polybar/wiki/)