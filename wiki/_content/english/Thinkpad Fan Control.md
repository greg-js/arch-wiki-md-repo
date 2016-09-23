By default, the EC regulates fan speed. If it's too conservative/loud for your taste, you might want a daemon to take over control. But this is risky: you take responsibility for temperature control. Excessive temperatures can damage or shorten the lifespan of components in your laptop.

From the [http://www.thinkwiki.org/wiki/How_to_control_fan_speed](http://www.thinkwiki.org/wiki/How_to_control_fan_speed):

	*Fan control operations are disabled by default for safety reasons. To enable fan control, the module parameter fan_control=1 must be given to thinkpad-acpi.*

Current fan control daemons available in the [AUR](/index.php/AUR "AUR") are [simpfand-git](https://aur.archlinux.org/packages/simpfand-git/) and [thinkfan](https://aur.archlinux.org/packages/thinkfan/).

## Installation

Install [thinkfan](https://aur.archlinux.org/packages/thinkfan/). Then have a look at the files:

```
# pacman -Ql thinkfan

```

Note that the thinkfan package installs /usr/lib/modprobe.d/thinkpad_acpi.conf, which contains

```
options thinkpad_acpi fan_control=1

```

So fan control is enabled by default.

```
$ su
# modprobe thinkpad_acpi
# cat /proc/acpi/ibm/fan

```

You should see that the fan level is "auto" by default, but you can echo a level command to the same file to control the fan speed manually. The thinkfan daemon will do this automatically.

You will need to copy one of the example config files (e.g. /usr/share/doc/thinkfan/examples/thinkfan.conf.simple) to /etc/thinkfan.conf, and modify to taste. This file specifies which sensors to read, and which interface to use to control the fan. Some systems have /proc/acpi/ibm/fan available; on others, you will need to specify something like

```
hwmon /sys/devices/virtual/thermal/thermal_zone0/temp

```

to use generic hwmon sensors instead of thinkpad-specific ones.

## Running

You can test your configuration first by running thinkfan manually (as root):

```
# thinkfan -n

```

and see how it reacts to the load level of whatever other programs you have running.

When you have it configured correctly, the thinkfan daemon can be started by running (as root):

```
# systemctl start thinkfan

```

or by automatically loading it on system startup:

```
# systemctl enable thinkfan

```

## Old packages which have gone missing

[tpfand](https://aur.archlinux.org/packages/tpfand/) and a version that doesn't require [HAL](/index.php/HAL "HAL") [tpfand-no-hal](https://aur.archlinux.org/packages/tpfand-no-hal/) are not actively developed anymore, and no longer available. An additional GTK+ frontend was provided in the [tpfan-admin](https://aur.archlinux.org/packages/tpfan-admin/) package in the [AUR](/index.php/AUR "AUR") which enables the monitoring of temperatures as well as the graphical adjustment of trigger points.

Due to tpfand not beeing actively developed anymore, there was a fork called tpfanco (which in fact uses the same names for the executables as tpfand): [tpfanco-svn](https://aur.archlinux.org/packages/tpfanco-svn/).

The configuration file for tpfand (same for tpfanco) was `/etc/tpfand.conf`.

Additionally, the [tpfand-profiles](https://aur.archlinux.org/packages/tpfand-profiles/) package in the [AUR](/index.php/AUR "AUR") provided the latest fan profiles for various thinkpad models.