Fancontrol, part of [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors), can be used to control the speed and sound of CPU/case fans. This article covers configuration/setup of the utility.

For some Dell laptops, an alternative is [i8kutils](#i8kutils).

## Contents

*   [1 Sensor driver](#Sensor_driver)
    *   [1.1 lm-sensors](#lm-sensors)
        *   [1.1.1 Increasing fan_div](#Increasing_fan_div)
*   [2 Configuration](#Configuration)
    *   [2.1 Tweaking](#Tweaking)
*   [3 fancontrol](#fancontrol)
*   [4 i8kutils](#i8kutils)
    *   [4.1 Dependencies](#Dependencies)
    *   [4.2 Configuration](#Configuration_2)
    *   [4.3 Disable BIOS fan speed control](#Disable_BIOS_fan_speed_control)
    *   [4.4 Installation as a service](#Installation_as_a_service)

## Sensor driver

Support for newer motherboards may not yet be in the Linux kernel. Check the official [lm-sensors devices](http://www.lm-sensors.org/wiki/Devices) table to see if experimental drivers are available for such motherboards.

It is recommended not to use `lm_sensors.service` to load the needed modules for fancontrol. Instead, manually place them in `/etc/modules-load.d/load_these.conf` since the order in which these modules are loaded dictate the order in which the needed symlinks for hwmon get created. In other words, using the `lm_sensors.service` causes inconsistencies boot-to-boot which will render the configuration file for fan control worthless for a consistency point of view. To avoid this problem:

In `/etc/conf.d/lm_sensors` you find the modules. If not there, run as root `sensors-detect` accepting the defaults. In the `modules-load.d` file place one module name per line. Specifying them like this will create a reproducible order. Another alternative is to use absolute device names in the configuration file.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1415552#p1415552)

### lm-sensors

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

#### Increasing fan_div

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

Once sensors is properly configured, run `pwmconfig` to test and configure speed control. Follow the instructions in `pwmconfig` to set up basic speeds. The default configuration options should create a new file, `/etc/fancontrol`.

### Tweaking

**Warning:** Some of the steps outlined below describe how to tweak fan speeds. Before doing this be sure to have a low CPU load.

**Note:** On several systems, the included script may report errors as it trys to calibrate fans to the respective PWM. Users may safely ignore these errors. The problem is that the script does not wait long enough before ramping up or down the PWM.

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

There are also two settings fancontrol needs to verify the configuration file is still up to date. The lines start with the setting name and a equality sign, followed by groups of hwmon-class-device=setting, seperated by spaces. You need to specify each setting for each hwmon class device you use anywhere in the config, or fancontrol will not work.

*   `DEVPATH`: Sets the physical device. You can determine this by executing the command

```
readlink -f /sys/class/hwmon/*hwmon-device*/device | sed -e 's/^\/sys\///'

```

*   `DEVNAME`: Sets the name of the device. Try:

```
$ sed -e 's/[[:space:]=]/_/g' /sys/class/hwmon/*hwmon-device*/device/name

```

**Tip:** Use `MAXPWM` and `MINPWM` options that limit fan speed range. See fancontrol manual page for details.

**Tip:** Not only the `DEVPATH` may change on reboot due to different timing of module loading, but also e.g. the temperature sensor paths (hwmon0/device/temp1_input becomes hwmon0/temp1_input). This usually happens on a kernel update. Check the system log to find out which is the troublemaker:
```
# systemctl status fancontrol.service

```
and correct your config file accordingly.

## fancontrol

Try to run *fancontrol*:

```
# /usr/bin/fancontrol

```

A properly configured setup will not error out and will take control of system fans. Users should hear system fans slowing shortly after executing this command.

To make *fancontrol* start automatically on every boot, [enable](/index.php/Enable "Enable") `fancontrol.service`.

**Note:** Upon upgrading/changing the kernel, running fancontrol may result in an error regarding changed device paths. This issue may be fixed by running `sensors-detect` and restarting the system.

## i8kutils

[i8kutils](https://aur.archlinux.org/packages/i8kutils/) provides an alternative method of controlling the fan speed on some Dell Inspiron and Latitude laptops. It makes use of the `/proc/i8k` interface provided by the `dell_smm_hwmon` driver (formerly `i8k`). Results will vary depending on the exact model of laptop.

### Dependencies

[tcl](https://www.archlinux.org/packages/?name=tcl) must be installed in order to run `i8kmon` as a background service (using the `--daemon` option). To run the X11 desktop applet, [tk](https://www.archlinux.org/packages/?name=tk) is required as well.

### Configuration

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

### Disable BIOS fan speed control

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

### Installation as a service

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