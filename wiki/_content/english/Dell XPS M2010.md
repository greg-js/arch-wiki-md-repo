## Contents

*   [1 Introduction](#Introduction)
*   [2 Hardware (Needs configuration)](#Hardware_.28Needs_configuration.29)
    *   [2.1 Sound](#Sound)
        *   [2.1.1 Running the workaround automatically with systemd](#Running_the_workaround_automatically_with_systemd)
    *   [2.2 Temperature monitoring and fan control (i8k)](#Temperature_monitoring_and_fan_control_.28i8k.29)
*   [3 Hardware (Working)](#Hardware_.28Working.29)
    *   [3.1 Keyboard](#Keyboard)
    *   [3.2 Graphics](#Graphics)
    *   [3.3 Network](#Network)
*   [4 Hardware (Not working)](#Hardware_.28Not_working.29)
    *   [4.1 Webcam](#Webcam)
*   [5 Hardware (Untested)](#Hardware_.28Untested.29)

## Introduction

The XPS M2010 is a large 'mobile desktop' with an adjustable display, built-in speakers, and detachable bluetooth keyboard. For transportation, it may be folded and carried as a briefcase. (Adapted from [Wikipedia](http://en.wikipedia.org/wiki/Dell_XPS#XPS_M2010))

It also [made an appearance](http://www.starringthecomputer.com/appearance.html?f=647&c=324) in the 2008 Iron Man film.

## Hardware (Needs configuration)

### Sound

Internal speakers will not work out of the box. (See discussions on the [Linux Laptop Wiki](http://www.linlap.com/dell_xps_m2010), among other places.)

A workaround is described at [https://answers.yahoo.com/question/index?qid=20110813164454AAyeJJ5](https://answers.yahoo.com/question/index?qid=20110813164454AAyeJJ5). It looks like it was originally documented at [https://bugtrack.alsa-project.org/alsa-bug/view.php?id=3403](https://bugtrack.alsa-project.org/alsa-bug/view.php?id=3403) but the ALSA bug tracker has since been taken down.

For the record, the workaround involves running the following commands:

```
hda-verb /dev/snd/hwC0D0 0x1 set_gpio_data 5
hda-verb /dev/snd/hwC0D0 0x1 set_gpio_dir 5
hda-verb /dev/snd/hwC0D0 0x1 set_gpio_mask 5

```

Speaker output works as expected after this.

#### Running the workaround automatically with systemd

Using [systemd](/index.php/Systemd "Systemd"), it is possible to set up a script to run these commands automatically at boot.

First, create the relevant script and save it somewhere (e.g., in */usr/local/bin*):

 `/usr/local/bin/M2010-sound` 
```
#!/bin/sh
hda-verb /dev/snd/hwC0D0 0x1 set_gpio_data 5
hda-verb /dev/snd/hwC0D0 0x1 set_gpio_dir 5
hda-verb /dev/snd/hwC0D0 0x1 set_gpio_mask 5

```

Make it executable.

```
chmod 755 /usr/local/bin/M2010-sound

```

Create a new systemd unit (e.g., in */etc/systemd/system*) that calls your script:

 `/etc/systemd/system/M2010-sound.service` 
```
[Unit]
Description=M2010 Speaker Configuration
After=sound.target
Requires=sound.target

[Service]
ExecStart=/usr/local/bin/M2010-sound

[Install]
WantedBy=multi-user.target

```

Enable the new service.

```
systemctl enable M2010-sound

```

To test the workaround, either reboot or start the service immediately with `systemctl start M2010-sound`. However, note that running the commands a second time during the same session might cause the speakers to stop working; they should work again after a reboot.

### Temperature monitoring and fan control (i8k)

The `i8k` module appears to work for temperature monitoring and fan control, but it needs to be loaded explicitly.

First, create a new .conf file in `/etc/modules-load.d` specifying `i8k` as a module to load:

 `/etc/modules-load.d/i8k.conf` 
```
i8k

```

Next, specify the module load options in a .conf file in `/etc/modprobe.d`. The fan RPM values shown by default appear to be erroneous, so we change the `fan_mult` option here (see [https://bugs.launchpad.net/ubuntu/+source/sensors-applet/+bug/200449](https://bugs.launchpad.net/ubuntu/+source/sensors-applet/+bug/200449)):

 `/etc/modprobe.d/i8k.conf` 
```
options i8k force=1 fan_mult=1

```

The `i8k` module should now be loaded automatically at boot.

To make system-wide changes to the configuration for `i8kmon`, you can simply edit `/etc/i8kutils/i8kmon.conf` -- You do not need to create a configuration file anywhere else.

Note: Within `i8k`, the left value appears to control the right fan (GPU) while the right value appears to control the left fan (CPU) for the M2010.

## Hardware (Working)

### Keyboard

The M2010 bluetooth keyboard/touchpad works out of the box.

### Graphics

The ATI Mobility Radeon X1800 works with 3D acceleration using the `radeon` module.

Install `xf86-video-ati` using [pacman](/index.php/Pacman "Pacman").

### Network

Ethernet (Broadcom Corporation NetXtreme BCM5753 Gigabit Ethernet PCI Express) works out of the box with module `tg3`.

Wireless (Intel Corporation PRO/Wireless 4965 AG or AGN) works out of the box with module `iwl4965`.

## Hardware (Not working)

### Webcam

The webcam does not work out of the box (picture is garbled). [http://en.community.dell.com/support-forums/software-os/f/3525/t/18800012](http://en.community.dell.com/support-forums/software-os/f/3525/t/18800012) suggests that it is possible to get it to work; further testing is needed to get it up and running on more modern configurations.

## Hardware (Untested)

The following devices/functions were untested:

*   Other bluetooth devices
*   Card reader
*   Fan control (i8k)
*   Internal modem