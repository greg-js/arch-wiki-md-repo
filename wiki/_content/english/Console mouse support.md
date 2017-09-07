GPM, short for General Purpose Mouse, is a daemon that provides mouse support for Linux virtual consoles.

## Installation

[Install](/index.php/Install "Install") the [gpm](https://www.archlinux.org/packages/?name=gpm) package. For touchpad support on a laptop you may also need to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

## Configuration

The `-m` parameter precedes the declaration of the mouse to be used. The `-t` parameter precedes the type of mouse. To get a list of available types for the `-t` option, run `gpm` with `-t help`.

```
# gpm -m /dev/input/mice -t help

```

The [gpm](https://www.archlinux.org/packages/?name=gpm) package needs to be started with a few parameters. These parameters can be added in the file `/etc/conf.d/gpm`, or used when running *gpm* directly. As of 2016, the `gpm.service` file for [systemd](/index.php/Systemd "Systemd") includes the parameters for a USB mice. Obviously, it should be edited if there is another mice type, and the file is used.

*   For PS/2 mice, replace the existing line with:

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

*   Whereas USB mice should use:

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

*   And IBM Trackpoints need:

```
GPM_ARGS="-m /dev/input/mice -t ps2"

```

**Note:** If the mouse has only 2 buttons, pass `-2` to `GPM_ARGS` and second button will perform the paste function.

Once a suitable configuration has been found, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `gpm.service`.

For more information see [gpm(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8).