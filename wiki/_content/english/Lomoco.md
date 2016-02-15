Lomoco is a small program for some Logitech mice, for configuring resolution and other settings.

**Note:** Not all Logitech mice need lomoco, some of them already have the right settings out-of-the-box and other are still not supported!

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Finding mouse information](#Finding_mouse_information)
    *   [2.2 Testing the configuration](#Testing_the_configuration)
    *   [2.3 Making the configuration persistent](#Making_the_configuration_persistent)

## Installation

[Install](/index.php/Install "Install") the [lomoco](https://www.archlinux.org/packages/?name=lomoco) package.

## Configuration

### Finding mouse information

To list all lomoco supported mice found on your system:

```
$ lomoco -s

```

Here an output as example:

 `lomoco -s` 

```
004.002: 046d:c01b MX310 Optical Mouse (M-BP86) Caps: RES 
004.001: 1d6b:0001 Not a Logitech device
001.001: 1d6b:0002 Not a Logitech device
002.001: 1d6b:0002 Not a Logitech device
003.001: 1d6b:0001 Not a Logitech device
```

We found a supported mouse; we know that this mouse supports 800 cpi (this information can be found on the box or on the page dedicated to this mouse on the logitech site) but without configuration its resolution is at 400 cpi, you can see the current settings with:

```
# lomoco -i

```

### Testing the configuration

Let's set its resolution to 800 cpi with:

```
# lomoco -8

```

or with:

```
# lomoco --800

```

If your mouse support a different resolution or other settings read

```
$ lomoco --help

```

for other info.

The mouse is now configured this is ouput of "lomoco -i" after changing cpi.

 `lomoco -i` 

```
004.002: 046d:c01b MX310 Optical Mouse (M-BP86) Caps: RES 
	Resolution (RES): **800 cpi**
	USB Mouse Polling Interval:  10ms
```

**Note:** The mouse is now configured but these settings are not persistent and will be reset on the next reboot; read the next section for making them persistent.

### Making the configuration persistent

Just edit /etc/udev/lomoco_mouse.conf with the desired options, here an example for this mouse:

 `/etc/udev/lomoco_mouse.conf` 

```
# Possible Resolutions Are: 400 800 1200 1600 2000
LOGITECH_MOUSE_RESOLUTION="800"

# SmartScroll/Cruise Control (SMS command set): yes or no
#LOGITECH_MOUSE_SMS="no"
```