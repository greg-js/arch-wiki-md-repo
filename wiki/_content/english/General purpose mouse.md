GPM, short for General Purpose Mouse, is a daemon that provides mouse support for Linux virtual consoles.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 QEMU or VirtualBox](#QEMU_or_VirtualBox)
*   [3 See also](#See_also)

## Installation

**Warning:** [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) is no longer actively updated. If possible, use [libinput](/index.php/Libinput "Libinput").

[Install](/index.php/Install "Install") the [gpm](https://www.archlinux.org/packages/?name=gpm) package. For touchpad support on a laptop you may also need to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

## Configuration

The `-m` parameter precedes the declaration of the mouse to be used. The `-t` parameter precedes the type of mouse. To get a list of available types for the `-t` option, run `gpm` with `-t help`.

```
# gpm -m /dev/input/mice -t help

```

The [gpm](https://www.archlinux.org/packages/?name=gpm) package needs to be started with a few parameters. These parameters can be recorded by [creating](/index.php/Create "Create") the file `/etc/conf.d/gpm`, or used when running *gpm* directly. As of 2016, the `gpm.service` file for [systemd](/index.php/Systemd "Systemd") includes the parameters for a USB mice.

 `/usr/lib/systemd/system/gpm.service`  `ExecStart=/usr/bin/gpm -m /dev/input/mice -t imps2` 

Obviously, it should be edited, preferably in a [systemd friendly manner](/index.php/Systemd#Editing_provided_units "Systemd"), if there is another mice type, and the service is used.

*   For PS/2 mice, the parameters are:

```
-m /dev/psaux -t ps2

```

*   And IBM Trackpoints need:

```
-m /dev/input/mice -t ps2

```

**Note:** If the mouse has only 2 buttons, pass `-2` to `GPM_ARGS` and second button will perform the paste function.

Once a suitable configuration has been found, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `gpm.service`.

For more information see [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8).

### QEMU or VirtualBox

The default mouse emulated by QEMU and VirtualBox has severe problems in both *gpm* and x with positioning and clicking. The position becomes unsynchronized with the host, so there are areas that can't be hovered over without repeatedly exiting and re-entering the window. Clicks register in a different location than the cursor was showing at.

Both QEMU and VirtualBox solve this problem by providing emulation for a USB tablet, which gives absolute positioning. ([libvirt](https://www.archlinux.org/packages/?name=libvirt) uses this automatically.)

However, the *gpm* only knows how to use the emulated mouse in relative positioning mode, so these problems remain. Attempting to use other types via `-t` fail to get it working properly.

[gpm-vm](https://aur.archlinux.org/packages/gpm-vm/) includes a several year old [pull request](https://github.com/telmich/gpm/pull/23) to add USB tablet support for VirtualBox (which also works under QEMU) and modifies the `gpm.service` file to use it by default.

You may need to change which event is used. (Giving *gpm* the original `-m /dev/input/mice` will not work.) By default:

 `/etc/gpm-vm.conf`  `event="/dev/input/event2"` 

You can determine the event to use by installing [evtest](https://www.archlinux.org/packages/?name=evtest) and running:

 `# evtest` 
```
...
/dev/input/event2:      QEMU QEMU USB Tablet
...

```

If you need to give *gpm* additional options, you can set `additional_args` in `/etc/gpm-vm.conf`.

Once a suitable configuration has been found, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the `gpm.service`.

## See also

*   [Gentoo:GPM](https://wiki.gentoo.org/wiki/GPM "gentoo:GPM")