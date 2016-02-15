From the Thinkpad Fan Control website:

	_tp-fan monitors temperatures and controls fan speed of IBM/Lenovo ThinkPad notebooks. tp-fan is an open-source project released under the GPL v3._

	_The tpfand daemon controls the system fan in software. It can be used to make the notebook more quiet. However this will also result in higher system temperatures that may damage and/or shorten the lifespan of the computer. Since version 0.90 fan trigger temperatures can be configured separately for each temperature sensor._

	_This project also provides the tpfan-admin GTK+ frontend to monitor system temperature and adjust fan trigger temperatures._

	_Warning: This program may damage your notebook. The author does not take any responsibility for damages caused by the use of this program._

## Contents

*   [1 Installation](#Installation)
    *   [1.1 tpfand](#tpfand)
    *   [1.2 tpfanco](#tpfanco)
*   [2 Configuration](#Configuration)
    *   [2.1 Running](#Running)

## Installation

### tpfand

**Note:** tpfand is not actively developed anymore! There's a fork called tpfanco (see below).

The [tpfand](https://aur.archlinux.org/packages/tpfand/) daemon can be installed from the [AUR](/index.php/AUR "AUR"). Alternatively, a version that doesn't require [HAL](/index.php/HAL "HAL") is also available from the [AUR](/index.php/AUR "AUR"): [tpfand-no-hal](https://aur.archlinux.org/packages/tpfand-no-hal/)

An additional GTK+ frontend is provided in the [tpfan-admin](https://aur.archlinux.org/packages/tpfan-admin/) package in the [AUR](/index.php/AUR "AUR") which enables the monitoring of temperatures as well as the graphical adjustment of trigger points.

### tpfanco

Due to tpfand not beeing actively developed anymore, there's a fork called tpfanco (which in fact uses the same names for the executables as tpfand): [tpfanco-svn](https://aur.archlinux.org/packages/tpfanco-svn/). It may be used as a complete replacement for tpfand.

# Configuration

The configuration file for tpfand (same for tpfanco) is found in `/etc/tpfand.conf`. This file can be edited to adjust the fan trigger points to suit your needs.

Additionally, the [tpfand-profiles](https://aur.archlinux.org/packages/tpfand-profiles/) package in the [AUR](/index.php/AUR "AUR") gives the latest fan profiles for various thinkpad models.

## Running

The tpfand daemon can be started by running (as root):

```
# systemctl start tpfand

```

or by automatically loading it on system startup:

```
# systemctl enable tpfand

```