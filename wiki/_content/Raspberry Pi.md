# Raspberry Pi

From [Wikipedia](https://en.wikipedia.org/wiki/Raspberry_Pi "wikipedia:Raspberry Pi"):

	"_The Raspberry Pi is a series of credit card-sized single-board computers developed in the UK by the Raspberry Pi Foundation with the intention of promoting the teaching of basic computer science in schools._"

The original models, released in 2012, are based on the Broadcom SoC BCM2835 ([ARM11 architecture](https://en.wikipedia.org/wiki/ARM11 "wikipedia:ARM11")). The Raspberry Pi 2, released in 2015, is shipped with a BCM2836 SoC (quad-core [ARM Cortex-A7 architecture](https://en.wikipedia.org/wiki/ARM_Cortex-A7 "wikipedia:ARM Cortex-A7")).

## Contents

*   [1 Article preface](#Article_preface)
*   [2 System architecture](#System_architecture)
*   [3 SD card performance](#SD_card_performance)
    *   [3.1 Enable fsck on boot](#Enable_fsck_on_boot)
*   [4 Installing Arch Linux ARM](#Installing_Arch_Linux_ARM)
*   [5 Network](#Network)
    *   [5.1 Configure WLAN without ethernet](#Configure_WLAN_without_ethernet)
*   [6 Audio](#Audio)
    *   [6.1 Caveats for HDMI audio](#Caveats_for_HDMI_audio)
*   [7 Video](#Video)
    *   [7.1 HDMI / analog TV-Out](#HDMI_.2F_analog_TV-Out)
    *   [7.2 Caveats for analog TV-Out](#Caveats_for_analog_TV-Out)
    *   [7.3 X.org driver](#X.org_driver)
*   [8 Onboard hardware sensors](#Onboard_hardware_sensors)
    *   [8.1 Temperature](#Temperature)
    *   [8.2 Voltage](#Voltage)
    *   [8.3 Lightweight monitoring suite](#Lightweight_monitoring_suite)
*   [9 Overclocking/underclocking](#Overclocking.2Funderclocking)
*   [10 Serial console](#Serial_console)
*   [11 Raspberry Pi camera module](#Raspberry_Pi_camera_module)
*   [12 Hardware random number generator](#Hardware_random_number_generator)
*   [13 GPIO](#GPIO)
    *   [13.1 SPI](#SPI)
    *   [13.2 Python](#Python)
*   [14 I2C](#I2C)
*   [15 QEMU chroot](#QEMU_chroot)
*   [16 See also](#See_also)

## Article preface

This article is not meant to be an exhaustive setup guide and assumes that the reader has setup an Arch system before. Arch newbies are encouraged to read the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") if unsure how to perform standard tasks such as creating users, managing the system, etc.

**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org](http://archlinuxarm.org) not through posts to the official Arch Linux Forum. Any posts related to ARM specific issues will be promptly closed per the [Arch Linux distribution support ONLY](/index.php/Forum_etiquette#Arch_Linux_distribution_support_ONLY "Forum etiquette") policy.

## System architecture

The Raspberry Pi is an ARM-based device and therefore needs binaries compiled for this architecture. These binaries are provided by the [Arch Linux ARM project](http://archlinuxarm.org/about) which ports Arch Linux to ARM-based devices. They also have a separate community and forum on their website, while original forum does _not_ support ARM specific issues. With the introduction of the Raspberry Pi 2 the packages needed now depend on which architecture the devices has:

*   ARMv6 (BCM2835): Raspberry Pi Model A, A+, B, B+, Zero
*   ARMv7 (BCM2836): Raspberry Pi 2 (based on Model B+)

## SD card performance

System responsiveness, particularly during operations involving disk I/O such as updating the system, can be adversely affected by poor quality/slow SD media. This is characterized by [frequent, often extended pauses](http://archlinuxarm.org/forum/viewtopic.php?f=64&t=9467) as pacman writes out files to the file system. The pauses are not due to saturation of the RPi or RPi2 bus, but are likely the bottle-neck due to a slow SD (or micro SD) card. See the [Benchmarking#Flash media](/index.php/Benchmarking#Flash_media "Benchmarking") for more.

Performance and system responsiveness can be generally improved by making adjustments to the system configuration. See especially [Maximizing performance](/index.php/Maximizing_performance "Maximizing performance") and [SSD#Tips for minimizing disk reads/writes](/index.php/SSD#Tips_for_minimizing_disk_reads.2Fwrites "SSD").

### Enable fsck on boot

Follow [fsck#Boot time checking](/index.php/Fsck#Boot_time_checking "Fsck"). Remember that kernel parameters are specified in `/boot/cmdline.txt`.

## Installing Arch Linux ARM

See the [Arch Linux ARM Pi documentation](http://archlinuxarm.org/platforms/armv6/raspberry-pi) or [Arch Linux ARM Pi2 documentation](http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2).

## Network

The fresh install comes preconfigured to use the onboard NIC in dhcp mode via [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") which should allow access to an official installation through [Secure Shell](/index.php/Secure_Shell "Secure Shell"). The root user's password is "root" and it is highly recommended to change the password and optionally set up [SSH keys](/index.php/SSH_keys "SSH keys").

### Configure WLAN without ethernet

Users needing to establish a wireless internet connection will need to use a wireless daemon such as [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant"). Consult the [wireless section](/index.php/Beginners%27_guide#Wireless "Beginners' guide") of the Beginner's Guide for additional instruction.

## Audio

[alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) should supply the needed programs to use onboard sound. Default volume can be adjusted using `alsamixer`.

**Tip:** Ensure that the sole source "PCM" is not muted (denoted by `MM` if muted, press `M` to unmute).

Select an audio source for output:

```
$ amixer cset numid=3 _x_

```

Where `_x_` corresponds to:

*   0 for Auto
*   1 for Analog out
*   2 for HDMI

### Caveats for HDMI audio

Some applications require a setting in `/boot/config.txt` to force audio over HDMI:

```
hdmi_drive=2

```

## Video

### HDMI / analog TV-Out

With the default configuration, raspberry pi uses HDMI video if a [HDMI](https://en.wikipedia.org/wiki/HDMI "wikipedia:HDMI") monitor is connected. Otherwise, it uses analog TV-Out (also known as composite output or RCA)

To turn the HDMI or analog TV-Out on or off, have a look at

```
/opt/vc/bin/tvservice

```

Use the _-s_ parameter to check the status; the _-o_ parameter to turn the display off and _-p_ parameter to power on HDMI with preferred settings.

Adjustments are likely required to correct proper overscan/underscan and are easily achieved in `boot/config.txt` in which many tweaks are set. To fix, simply uncomment the corresponding lines and setup per the commented instructions:

```
# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
#overscan_left=16
overscan_right=8
overscan_top=-16
overscan_bottom=-16

```

Users wishing to use the analog video out should consult [this](https://raw.github.com/Evilpaul/RPi-config/master/config.txt) config file which contains options for non-NTSC outputs.

A reboot is needed for new settings to take effect.

### Caveats for analog TV-Out

Since Raspberry Pi 1 Model B+ and Raspberry Pi 2 Model B, the composite video socket was removed, with the replacement of composite signal through the 3.5mm video/audio jack. Some RCA cables do not follow the same standard as Raspberry Pi, in which case connect the red or white audio plug for video.[[1]](http://www.raspberrypi-spy.co.uk/2014/07/raspberry-pi-model-b-3-5mm-audiovideo-jack/)

### X.org driver

The X.org driver for Raspberry Pi can be [installed](/index.php/Installed "Installed") with the _xf86-video-fbdev_ or _xf86-video-fbturbo-git_ package.

## Onboard hardware sensors

### Temperature

Temperatures sensors can be queried with utils in the _raspberrypi-firmware-tools_ package. The RPi offers a sensor on the BCM2835 SoC (CPU/GPU):

 `$ /opt/vc/bin/vcgencmd measure_temp`  `temp=49.8'C` 

Alternatively, simply read from the file system:

 `$ cat /sys/class/thermal/thermal_zone0/temp`  `49768` 

For human readable output:

 `$ awk '{printf "%3.1f°C\n", $1/1000}' /sys/class/thermal/thermal_zone0/temp`  `54.1°C` 

### Voltage

Four different voltages can be monitored via `/opt/vc/bin/vcgencmd` as well:

```
$ /opt/vc/bin/vcgencmd measure_volts _<id>_

```

Where `_<id>_` is:

*   core for core voltage
*   sdram_c for sdram Core voltage
*   sdram_i for sdram I/O voltage
*   sdram_p for sdram PHY voltage

### Lightweight monitoring suite

[monitorix](https://aur.archlinux.org/packages/monitorix/)<sup><small>AUR</small></sup> has specific support for the RPi since v3.2.0\. Screenshots available [here](http://www.monitorix.org/screenshots.html).

## Overclocking/underclocking

The RPi can be overclocked by editing `/boot/config.txt`, for example:

```
arm_freq=800
arm_freq_min=100
core_freq=300
core_freq_min=75
sdram_freq=400
over_voltage=0

```

The optional `*_min` lines define the minimum frequency to be used for the given component. When the system is not under load, the frequencies will drop down to the minimum value. Consult the [Overclocking](http://elinux.org/RPiconfig#Overclocking) article on elinux for additional options and examples.

A reboot is needed for new settings to take effect.

The overclocked setting for CPU clock applies only when the governor throttles up the CPU, i.e. under load. To query the current frequency of the CPU:

```
$ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq

```

See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for details on scaling governors.

**Tip:** The following script will show all frequencies set on the RPi:

```
#/bin/bash
for src in arm core h264 isp v3d uart pwm emmc pixel vec hdmi dpi ; do
    echo -e "$src:\t$(/opt/vc/bin/vcgencmd  measure_clock $src)"
done

```

## Serial console

Edit the default `/boot/cmdline.txt`, change `loglevel` to `5` to see boot messages:

```
loglevel=5

```

If the default speed of 115200 does not work properly, try changing it to 38400:

```
console=ttyAMA0,38400 kgdboc=ttyAMA0,38400

```

Start getty service on the Pi

```
# systemctl start getty@ttyAMA0

```

Enable on boot

```
# systemctl enable getty@ttyAMA0.service

```

Creating the proper service link:

```
# ln -s /usr/lib/systemd/system/serial-getty@.service /etc/systemd/system/getty.target.wants/serial-getty@ttyAMA0.service

```

From a PC, connect:

```
# screen /dev/ttyUSB0 38400

```

## Raspberry Pi camera module

The commands for the camera module are included as part of the _raspberrypi-firmware-tools_ package - which is installed by default.

```
$ /opt/vc/bin/raspistill
$ /opt/vc/bin/raspivid

```

Append to `/boot/config.txt`:

```
gpu_mem=128
start_file=start_x.elf
fixup_file=fixup_x.dat

```

Optionally

```
disable_camera_led=1

```

The following is a common error:

```
mmal: mmal_vc_component_enable: failed to enable component: ENOSPC
mmal: camera component couldn't be enabled
mmal: main: Failed to create camera component
mmal: Failed to run camera app. Please check for firmware updates

```

which can be corrected by setting these values in `/boot/config.txt`:

```
cma_lwm=
cma_hwm=
cma_offline_start=

```

Another common error:

```
mmal: mmal_vc_component_create: failed to create component 'vc.ril.camera' (1:ENOMEM)
mmal: mmal_component_create_core: could not create component 'vc.ril.camera' (1)
mmal: Failed to create camera component
mmal: main: Failed to create camera component
mmal: Only 64M of gpu_mem is configured. Try running "sudo raspi-config" and ensure that "memory_split" has a value of 128 or greater

```

can be corrected by adding the following line into the `/etc/modprobe.d/blacklist.conf`:

```
blacklist i2c_bcm2708

```

In order to use standard applications (those that look for `/dev/video0`) the V4L2 driver must be loaded. This can be done automatically at boot by creating an autoload file such as the following.

 `/etc/modules-load.d/rpi-camera.conf`  `bcm2835-v4l2` 

## Hardware random number generator

Arch Linux ARM for the Raspberry Pi has the `bcm2708-rng` module set to load at boot (see [this](http://archlinuxarm.org/forum/viewtopic.php?f=31&t=4993#p27708)), but install the _rng-tools_ and tell the Hardware RNG Entropy Gatherer Daemon (_rngd_) where to find the hardware random number generator.

This can be done by editing `/etc/conf.d/rngd`:

```
RNGD_OPTS="-o /dev/random -r /dev/hwrng"

```

and enabling and [starting](/index.php/Start "Start") the _rngd_ service.

If [haveged](/index.php/Haveged "Haveged") is running, it should be stopped and disabled, as it might compete with _rngd_ and is only preferred when there is no hardware random number generator available.

Once completed, this change ensures that data from the hardware random number generator is fed into the kernel's entropy pool at `/dev/random`. To check the available entropy, run:

```
# cat /proc/sys/kernel/random/entropy_avail

```

The number it reports should be around 3000, whereas before setting up _rngd_ it would have been closer to 1000.

## GPIO

### SPI

To enable the `/dev/spidev*` devices, uncomment the following line:

 `/boot/config.txt`  `device_tree_param=spi=on` 

### Python

To be able to use the GPIO pins from Python, use the [RPi.GPIO](https://pypi.python.org/pypi/RPi.GPIO) library. Install either [python-raspberry-gpio](https://aur.archlinux.org/packages/python-raspberry-gpio/)<sup><small>AUR</small></sup> or [python2-raspberry-gpio](https://aur.archlinux.org/packages/python2-raspberry-gpio/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python2-raspberry-gpio)]</sup> from the [AUR](/index.php/AUR "AUR").

## I2C

Install _i2c-tools_ and _lm_sensors_ packages.

Configure the bootloader to enable the i2c hardware by appending `/boot/config.txt`:

```
 dtparam=i2c_arm=on

```

Configure the `i2c-dev` and `i2c-bcm2708` (if you did not blacklist it for the camera) modules to be loaded at boot:

 `/etc/modules-load.d/raspberrypi.conf` 

```
i2c-dev
i2c-bcm2708
```

Reboot the Raspberry Pi and issue the following command to get the hardware address:

```
 i2cdetect -y 0

```

Now we need to tell Linux to instantiate the device. Change the hardware address to the address found in the previous step with '0x' as prefix (e.g. 0x48) and choose a device name:

```
 echo <devicename> <hardware address> >/sys/class/i2c-adapter/i2c-0/new_device

```

Check the dmesg command for a new entry:

```
 i2c-0: new_device: Instantiated device ds1621 at 0x48

```

Finally, read the sensor output:

```
 sensors

```

## QEMU chroot

Sometimes it is easier to work directly on a disk image instead of the real Raspberry Pi. This can be achieved by mounting an SD card containing the RPi root partition and chrooting into it. From the chroot it should be possible to run _pacman_ and install more packages, compile large libraries etc. Since the executables are for the ARM architecture, the translation to x86 needs to be performed by [QEMU](/index.php/QEMU "QEMU").

**Note:** As of January 2016, [make](https://www.archlinux.org/packages/?name=make) won't run in QEMU for ARM so it is not possible to build packages this way. Follow the [guide on the Arch Linux ARM website](http://archlinuxarm.org/developers/distcc-cross-compiling) to build a cross-compiler if building ARM packages is needed.

Install [binfmt-support](https://aur.archlinux.org/packages/binfmt-support/)<sup><small>AUR</small></sup> and [qemu-user-static](https://aur.archlinux.org/packages/qemu-user-static/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

Make sure that the ARM to x86 translation is active:

```
# update-binfmts --importdir /var/lib/binfmts/ --import
# update-binfmts --display qemu-arm

```

If ARM to x86 translation is not active, enable it using update-binfmts:

```
# update-binfmts --enable qemu-arm

```

Mount the SD card to `mnt/` (the device name may be different).

```
# mkdir mnt
# mount /dev/mmcblk0p2 mnt

```

Copy the QEMU executable, which will handle the translation from ARM, to the SD card root:

```
# cp /usr/bin/qemu-arm-static mnt/usr/bin

```

Finally chroot into the SD card root as described in [Change root#Using chroot](/index.php/Change_root#Using_chroot "Change root"), keeping in mind that `qemu-arm-static` needs to be called in the `chroot` command i.e.:

```
# chroot /mnt/arch /usr/bin/qemu-arm-static /bin/bash

```

## See also

*   [RPi Config](http://elinux.org/RPiconfig) - Excellent source of info relating to under-the-hood tweaks.
*   [RPi vcgencmd usage](http://elinux.org/RPI_vcgencmd_usage) - Overview of firmware command vcgencmd.
*   [Arch Linux ARM on Raspberry PI](http://archpi.dabase.com/) - A FAQ style site with hints and tips for running Arch Linux on the RPi
*   [[2]](https://github.com/phortx/Raspberry-Pi-Setup-Guide) - A really opionionated guide how to setup a RPi with Arch Linux

Retrieved from "[https://wiki.archlinux.org/index.php?title=Raspberry_Pi&oldid=415133](https://wiki.archlinux.org/index.php?title=Raspberry_Pi&oldid=415133)"