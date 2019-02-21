[polybar](https://github.com/jaagr/polybar) is a fast and easy-to-use tool for creating status bars. It aims to be easily customizable, utilising many modules which enable a wide range of (editable) functionality, such as displaying workspaces, the date, or system volume. Polybar is especially useful for [Window managers](/index.php/Window_manager "Window manager") that have a limited or non-existent status bar, such as [awesome](/index.php/Awesome "Awesome") or [i3](/index.php/I3 "I3"). Polybar can also be used on full [Desktop environments](/index.php/Desktop_environment "Desktop environment") like [Plasma](/index.php/Plasma "Plasma").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Running Polybar](#Running_Polybar)
    *   [2.2 Sample Config](#Sample_Config)
    *   [2.3 Running with WM](#Running_with_WM)
        *   [2.3.1 bspwm](#bspwm)
        *   [2.3.2 i3](#i3)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Cannot open shared object file libjsoncpp.so](#Cannot_open_shared_object_file_libjsoncpp.so)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [polybar](https://aur.archlinux.org/packages/polybar/) package. The development version is [polybar-git](https://aur.archlinux.org/packages/polybar-git/).

## Configuration

Copy the configuration example from `/usr/share/doc/polybar/config` to `$XDG_CONFIG_HOME/polybar/config`

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

However you will probably want to run Polybar with your window manager's bootstrap routine. See [#Running with WM](#Running_with_WM)

#### Sample Config

A very basic polybar config may look like this:

```
[bar/mybar]
modules-right = date

[module/date]
type = internal/date
date = %Y-%m-%d%
```

It defines a bar named `mybar` with a module called `date`.

By default polybar will also install a sample configuration with many preconfigured modules in `/usr/share/doc/polybar/config`

**Note:** The sample config is not designed to work out of the box for everyone, you will need to modify it to match your setup

#### Running with WM

Create an [executable](/index.php/Executable "Executable") file containing the startup logic, for example `$HOME/.config/polybar/launch.sh`:

```
#!/bin/bash

# Terminate already running bar instances
killall -q polybar

# Wait until the processes have been shut down
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done

# Launch Polybar, using default config location ~/.config/polybar/config
polybar mybar &

echo "Polybar launched..."

```

This script will mean that restarting your WM will also restart Polybar.

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

## Troubleshooting

### Cannot open shared object file libjsoncpp.so

Attempt a reinstall as per [this](https://github.com/jaagr/polybar/issues/885) github issue.

Failing that, try installing jsoncpp from the official repositories:

 `pacman -S jsoncpp` 

## See also

*   [Polybar Github Wiki](https://github.com/jaagr/polybar/wiki/)