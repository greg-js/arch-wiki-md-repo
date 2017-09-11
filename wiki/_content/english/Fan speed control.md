Related articles

*   [Lm_sensors](/index.php/Lm_sensors "Lm sensors")

Fan control can bring various benefits to your system, such as quieter working system and power saving by completely stopping fans on low CPU load.

**Warning:** Configuring or completely stopping fans on high system load might result in permanently damaged hardware. You have been warned!

## Contents

*   [1 Overview](#Overview)
*   [2 Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29)
    *   [2.1 lm-sensors](#lm-sensors)
        *   [2.1.1 Increasing fan_div](#Increasing_fan_div)
    *   [2.2 Configuration](#Configuration)
        *   [2.2.1 Tweaking](#Tweaking)
    *   [2.3 fancontrol](#fancontrol)
*   [3 NBFC](#NBFC)
    *   [3.1 Installation](#Installation)
    *   [3.2 Configuration](#Configuration_2)
*   [4 Dell laptops](#Dell_laptops)
    *   [4.1 Installation](#Installation_2)
    *   [4.2 Configuration](#Configuration_3)
    *   [4.3 Disable BIOS fan speed control](#Disable_BIOS_fan_speed_control)
    *   [4.4 Installation as a service](#Installation_as_a_service)
*   [5 ThinkPad laptops](#ThinkPad_laptops)
    *   [5.1 Installation](#Installation_3)
    *   [5.2 Running](#Running)
    *   [5.3 Old packages which have gone missing](#Old_packages_which_have_gone_missing)
*   [6 Asus laptops](#Asus_laptops)
    *   [6.1 Kernel modules overview](#Kernel_modules_overview)
    *   [6.2 asus-nb-wmi](#asus-nb-wmi)
    *   [6.3 asus_fan](#asus_fan)
    *   [6.4 Generate config file with pmwconfig](#Generate_config_file_with_pmwconfig)

# Overview

**Note:** Laptop users should be aware about how cooling system works in their hardware. Some laptops have single fan for both CPU and GPU and cools both at the same time. Some laptops have two fans for CPU and GPU, but the first fan cools down CPU and GPU at the same time, while the other one cools CPU only. By using [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29) tool, you might need to monitor highest temperature of both CPU and GPU, which cannot be achieved with [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29) without modifications to `fancontrol` script. [Here](https://github.com/daringer/asus-fan/issues/47#issue-232063547) is some more information about this topic.

There are multiple working solutions for fan control for both desktops and notebooks. Depending on your needs:

*   [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29) - General tool to configure fan speeds. Most suitable for desktops.
*   [NoteBook Fan Control (NBFC)](#NBFC) - Cross-platform solution for laptop fan control. Supports wide variety of laptops, including the latest ones.
*   [Dell laptops](#Dell_laptops) - Alternative fan control daemon for some Dell laptops.
*   [ThinkPad laptops](#ThinkPad_laptops) - Fan configuration for some ThinkPad laptops.
*   [Asus laptops](#Asus_laptops) - Configure some Asus laptops for [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29) or manual control.

# Fancontrol (lm-sensors)

`fancontrol` is a part of [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors), which can be used to control the speed of CPU/case fans.

Support for newer motherboards may not yet be in the Linux kernel. Check the official [lm-sensors devices](https://hwmon.wiki.kernel.org/device_support_status) table to see if experimental drivers are available for such motherboards.

It is recommended not to use `lm_sensors.service` to load the needed modules for fancontrol. Instead, manually place them in `/etc/modules-load.d/load_these.conf` since the order in which these modules are loaded dictate the order in which the needed symlinks for hwmon get created. In other words, using the `lm_sensors.service` causes inconsistencies boot-to-boot which will render the configuration file for fan control worthless for a consistency point of view. To avoid this problem:

In `/etc/conf.d/lm_sensors` you find the modules. If not there, run as root `sensors-detect` accepting the defaults. In the `modules-load.d` file place one module name per line. Specifying them like this will create a reproducible order. Another alternative is to use absolute device names in the configuration file.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1415552#p1415552)

## lm-sensors

Set up [lm_sensors](/index.php/Lm_sensors "Lm sensors").

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:      +29.0°C  (high = +76.0°C, crit = +100.0°C)  

[...]

it8718-isa-0290
Adapter: ISA adapter
Vcc:         +1.14 V  (min =  +0.00 V, max =  +4.08 V)   
VTT:         +2.08 V  (min =  +0.00 V, max =  +4.08 V)   
+3.3V:       +3.33 V  (min =  +0.00 V, max =  +4.08 V)   
NB Vcore:    +0.03 V  (min =  +0.00 V, max =  +4.08 V)   
VDRAM:       +2.13 V  (min =  +0.00 V, max =  +4.08 V)   
fan1:        690 RPM  (min =   10 RPM)
temp1:       +37.5°C  (low  = +129.5°C, high = +129.5°C)  sensor = thermistor
temp2:       +25.0°C  (low  = +127.0°C, high = +127.0°C)  sensor = thermal diode
```

If the output does not display an RPM value for the CPU fan, one may need to increase the fan divisor. If fan speed is shown and higher than 0, skip the next step.

### Increasing fan_div

The first line of the sensors output is the chipset used by the motherboard for readings of temperatures and voltages.

Create a file in `/etc/sensors.d/`:

 `/etc/sensors.d/fan-speed-control.conf` 
```
chip "*coretemp-isa-**"
set fan*X*_div 4
```

Replacing *coretemp-isa-* with name of the chipset and *X* with the number of the CPU fan to change.

Save the file, and run as root:

```
# sensors -s

```

which will reload the configuration files.

Run `sensors` again, and check if there is an RPM readout. If not, increase the divisor to 8, 16, or 32\. YMMV!

## Configuration

**Note:** Advanced users may want to skip this section and write `/etc/fancontrol` on their own, which also saves them from hearing all of the fans at full speed.

Once sensors are properly configured, use `pwmconfig` to test and configure fan speed control. The default configuration options should create `/etc/fancontrol` configuration file:

```
# pwmconfig

```

### Tweaking

**Note:** On several systems, the included script may report errors as it tries to calibrate fans to the respective pulse-width modulation (PWM). Users may safely ignore these errors. The problem is that the script does not wait long enough before ramping up or down the PWM.

Users wishing more more control may need to tweak the generated configuration. Here is a sample configuration file:

```
INTERVAL=10
DEVPATH=hwmon0=devices/platform/coretemp.0 hwmon2=devices/platform/w83627ehf.656
DEVNAME=hwmon0=coretemp hwmon2=w83627dhg
FCTEMPS=hwmon0/device/pwm1=hwmon0/device/temp1_input
FCFANS= hwmon0/device/pwm1=hwmon0/device/fan1_input
MINTEMP=hwmon0/device/pwm1=20
MAXTEMP=hwmon0/device/pwm1=55
MINSTART=hwmon0/device/pwm1=150
MINSTOP=hwmon0/device/pwm1=105

```

*   `INTERVAL`: how often the daemon should poll CPU temps and adjust fan speeds. INTERVAL is in seconds.

The rest of the configuration file is split into (at least) two values per configuration option. Each configuration option first points to a PWM device which is written to which sets the fan speed. The second "field" is the actual value to set. This allows monitoring and controlling multiple fans and temperatures.

*   `FCTEMPS`: The temperature input device to read for CPU temperature. The above example corresponds to `/sys/class/hwmon/hwmon0/device/temp1_input`.
*   `FCFANS`: The current fan speed, which can be read (like the temperature) in `/sys/class/hwmon/hwmon0/device/fan1_input`
*   `MINTEMP`: The temperature (°C) at which to **SHUT OFF** the CPU fan. Efficient CPUs often will not need a fan while idling. Be sure to set this to a temperature that *you know is safe*. Setting this to 0 is not recommended and may ruin your hardware!
*   `MAXTEMP`: The temperature (°C) at which to spin the fan at its *MAXIMUM* speed. This should be probably be set to perhaps 10 or 20 degrees (°C) below your CPU's critical/shutdown temperature. Setting it closer to MINTEMP will result in higher fan speeds overall.
*   `MINSTOP`: The PWM value at which your fan stops spinning. Each fan is a little different. Power tweakers can `echo` different values (between 0 and 255) to `/sys/class/hwmon/hwmon0/device/pwm1` and then watch the CPU fan. When the CPU fan stops, use this value.
*   `MINSTART`: The PWM value at which your fan starts to spin again. This is often a higher value than MINSTOP as more voltage is required to overcome inertia.

There are also two settings fancontrol needs to verify the configuration file is still up to date. The lines start with the setting name and an equality sign, followed by groups of hwmon-class-device=setting, separated by spaces. You need to specify each setting for each hwmon class device you use anywhere in the config, or fancontrol will not work.

*   `DEVPATH`: Sets the physical device. You can determine this by executing the command

```
readlink -f /sys/class/hwmon/*[your-hwmon-device]*/device | sed -e 's/^\/sys\///'

```

*   `DEVNAME`: Sets the name of the device. Try:

```
$ sed -e 's/[[:space:]=]/_/g' /sys/class/hwmon/*[your-hwmon-device]*/device/name

```

**Tip:** Use `MAXPWM` and `MINPWM` options that limit fan speed range. See fancontrol manual page for details.

**Tip:** Not only the `DEVPATH` may change on reboot due to different timing of module loading, but also e.g. the temperature sensor paths (hwmon0/device/temp1_input becomes hwmon0/temp1_input). This usually happens on a kernel update. Check the system log to find out which is the troublemaker:
```
# systemctl status fancontrol.service

```
and correct your config file accordingly.

## fancontrol

**Note:** Upon upgrading/changing the kernel, running `fancontrol` may result in an error regarding changed device paths. This issue may be fixed by running `sensors-detect` again and restarting the system.

Try to run *fancontrol*:

```
# /usr/bin/fancontrol

```

A properly configured setup will not error out and will take control of system fans. Users should hear system fans slowing shortly after executing this command.

To enable starting *fancontrol* automatically on every boot, [enable](/index.php/Enable "Enable") `fancontrol.service`.

For an unofficial GUI [install](/index.php/Install "Install") [fancontrol-gui](https://aur.archlinux.org/packages/fancontrol-gui/) or [fancontrol-kcm](https://aur.archlinux.org/packages/fancontrol-kcm/).

# NBFC

NBFC is a cross-platform fan control solution for notebooks. It comes with a powerful configuration system, which allows to adjust it to many different notebook models, including some of the latest ones.

## Installation

NBFC can be installed as [nbfc-beta](https://aur.archlinux.org/packages/nbfc-beta/). Also start & enable `nbfc.service`.

## Configuration

NBFC comes with pre-made profiles. You can find them in `/opt/nbfc/Configs/` directory.

**Tip:** Profiles are being updated more frequently in [NBFC git repository](https://github.com/hirschmann/nbfc/tree/master/Configs) rather than together with releases. You may want to download some profiles directly to `/opt/nbfc/Configs/`.

Check if there is anything NBFC can recommend:

```
$ nbfc config -r

```

If there is at least one model, try to apply this profile and see how fan speeds are being handled. For example:

```
$ nbfc config -a "Asus Zenbook UX430UA"

```

If there are no recommended models, go to [NBFC git repository](https://github.com/hirschmann/nbfc/tree/master/Configs) and check if there are any similar models available from the same manufacturer. If there is - download directly to `/opt/nbfc/Configs/` directory. For example, on **Asus Zenbook UX430UQ**, the configuration **Asus Zenbook UX430UA** did not work well (fans completelly stopped all the time), but **Asus Zenbook UX410UQ** worked fantastically.

Run `nbfc` to see all options. More information is available at [first steps](https://github.com/hirschmann/nbfc/wiki/First-steps#linux) from NBFC GIT wiki.

# Dell laptops

`i8kutils` is a daemon to configure fan speed according to CPU temperatures on some Dell Inspiron and Latitude laptops. It uses of the `/proc/i8k` interface provided by the `dell_smm_hwmon` driver (formerly `i8k`). Results will vary depending on the exact model of laptop.

## Installation

[i8kutils](https://aur.archlinux.org/packages/i8kutils/) is the main package to control fan speed. Additionally, you might want to install these:

*   [tcl](https://www.archlinux.org/packages/?name=tcl) - must be installed in order to run `i8kmon` as a background service (using the `--daemon` option).
*   [tk](https://www.archlinux.org/packages/?name=tk) - must be installed together with [tcl](https://www.archlinux.org/packages/?name=tcl) to run as X11 desktop applet.

## Configuration

By default, `i8kmon` only monitors the CPU temperature and fan speed passively. To enable its fan speed control, either run it with the `--auto` option or enable the option permanently in `/etc/i8kutils/i8kmon.conf`:

```
set config(auto)       1

```

The temperature points at which the fan changes speed can be adjusted in the same configuration file. Only three fans speeds are supported (high, low, and off). Look for a section similar to the following:

```
set config(0)  {{0 0}  -1  55  -1  55}
set config(1)  {{1 1}  45  75  45  75}
set config(2)  {{2 2}  65 128  65 128}

```

This example starts the fan at low speed when the CPU temperature reaches 55 °C, switching to high speed at 75 °C. The fan will switch back to low speed once the temperature drops to 65 °C, and turns off completely at 45 °C.

## Disable BIOS fan speed control

It may be necessary to turn off control of the fan speed by the BIOS to prevent it from "fighting" with `i8kmon`. On some laptops, this can be done using the `smm` utility. **This utility is extremely dangerous as it writes directly to an I/O port to invoke the processor's [System Management Mode](https://en.wikipedia.org/wiki/System_Management_Mode "wikipedia:System Management Mode"). Use it at your own risk.**

`smm` must be compiled and installed manually. On a 64-bit system, [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) is required. Locate the file `smm.c` in the `i8kutils` source and compile it:

```
$ gcc -m32 -o smm smm.c

```

To disable BIOS fan speed control, run (as root):

```
# ./smm 30a3

```

To enable it again:

```
# ./smm 31a3

```

**Note:** This method may disable other power management features of the BIOS as well, such as notifying Linux when the power button is pressed.

## Installation as a service

`i8kmon` can be started automatically as a [systemd](/index.php/Systemd "Systemd") service using a unit file similar to the following:

 `/etc/systemd/system/i8kmon.service` 
```
[Unit]
Description=i8kmon

[Service]
#ExecStartPre=/usr/bin/smm 30a3  # uncomment to disable BIOS fan control
#ExecStopPost=/usr/bin/smm 31a3  # ... and re-enable it afterwards
ExecStart=/usr/bin/i8kmon -d
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

# ThinkPad laptops

By default, the embedded controller (EC) regulates fan speed. If it's too conservative/loud for your taste, you might want a daemon to take over control. But this is risky: you take responsibility for temperature control. Excessive temperatures can damage or shorten the lifespan of components in your laptop.

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

# Asus laptops

This topic will cover drivers configuration on Asus laptops **for [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29)**. If possible, use [#NBFC](#NBFC).

## Kernel modules overview

*   [#asus-nb-wmi](#asus-nb-wmi) is a kernel module, which is included in mainstream Linux kernel and is loaded automatically in Asus laptops. It will only allow to control a single fan and if there is a second fan - you will not have any controls over it. Blacklisting this module will prevent keyboard backlight to work.
*   [#asus_fan](#asus_fan) is a kernel module, which allows to control both fans on some older Asus laptops. Does not work with the most recent models.

In configuration files, we are going to use full paths to sysfs files (e.g. `/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1`). This is because hwmon**1** might change to any other number after reboot. [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29) is written in [Bash](/index.php/Bash "Bash"), so using these paths in configuration file is completely acceptable. You can find complete `/etc/fancontrol` configuration file examples at [ASUS_N550JV#Fan_control](/index.php/ASUS_N550JV#Fan_control "ASUS N550JV").

## asus-nb-wmi

Kernel module `asus-nb-wmi` is already included in Linux kernel and should already be loaded to your kernel.

Below are the commands to control it. Check if you have any controls over your fan:

```
# echo 255 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1           # Full fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1             # Fan is stopped (Value: 0)
# echo 2 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[[:print:]]*/pwm1_enable     # Change fan mode to automatic
# echo 1 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1_enable      # Change fan mode to manual

```

If you were able to modify fan speed with above commands, then continue with [#Generate_config_file_with_pmwconfig](#Generate_config_file_with_pmwconfig).

## asus_fan

Install [asus-fan-dkms-git](https://aur.archlinux.org/packages/asus-fan-dkms-git/). Load kernel module:

```
# modprobe asus_fan

```

**Note:** For unknown reasons this is likely going to fail (no asus_fan module found in your system). [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") and system reboot usually fix this issue.

Check if you have any control over both fans:

```
# echo 255 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1          # Full CPU fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1            # CPU fan is stopped (Value: 0)
# echo 255 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1          # Full GFX fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1            # GFX fan is stopped (Value: 0)
# echo 2 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1_enable     # Change CPU fan mode to automatic
# echo 1 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1_enable     # Change CPU fan mode to manual
# echo 2 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2_enable     # Change GFX fan mode to automatic
# echo 1 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2_enable     # Change GFX fan mode to manual
# cat /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/temp1_input          # Display GFX temperature (will always be 0 when GFX is disabled/unused)

```

If everything works, you might want to load this kernel module on boot:

 `/etc/modules-load.d/asus_fan.conf` 
```
# Load asus_fan module on boot:
asus_fan

```

Continue with [#Generate_config_file_with_pmwconfig](#Generate_config_file_with_pmwconfig).

## Generate config file with pmwconfig

If you get an error `There are no working fan sensors, all readings are 0` while generating config file with `pwmconfig`, open first console and execute:

```
# watch -n 1 "echo 2 > /sys/devices/platform/**<kernel_module>**/hwmon/hwmon[[:print:]]*/pwm**1**_enable"

```

If you use `asus_fan` kernel module and have 2nd fan, in second console:

```
# watch -n 1 "echo 2 > /sys/devices/platform/**<kernel_module>**/hwmon/hwmon[[:print:]]*/pwm**2**_enable"

```

And finally, in the third console:

```
# pwmconfig

```

Once you are done and the configuration file is generated, you should stop the first and second consoles. Continue with [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29). After config file is generated, you might need to manually replace PWM values with full sysfs paths as they are used in these steps, because hwmon number values might change after reboot.