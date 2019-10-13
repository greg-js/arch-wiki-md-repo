Related articles

*   [Lm_sensors](/index.php/Lm_sensors "Lm sensors")

**翻译状态：** 本文是英文页面 [Fan speed control](/index.php/Fan_speed_control "Fan speed control") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Fan+speed+control&diff=0&oldid=466874)可以查看翻译后英文页面的改动。

Fancontrol, 是[lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors)的一部分，可以被用于控制CPU以及其他风扇的转速。本文阐述了如何安装，配置它。

对于一些戴尔笔记本，可以由[i8kutils](#i8kutils)代替。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 传感器驱动](#传感器驱动)
    *   [1.1 lm-sensors](#lm-sensors)
        *   [1.1.1 增加 fan_div](#增加_fan_div)
*   [2 Configuration](#Configuration)
    *   [2.1 Tweaking](#Tweaking)
*   [3 fancontrol](#fancontrol)
*   [4 i8kutils](#i8kutils)
    *   [4.1 Dependencies](#Dependencies)
    *   [4.2 Configuration](#Configuration_2)
    *   [4.3 Disable BIOS fan speed control](#Disable_BIOS_fan_speed_control)
    *   [4.4 Installation as a service](#Installation_as_a_service)

## 传感器驱动

许多较新主板的传感器仍然未受到Kernel内建驱动的支持，检查一下表格 [lm-sensors devices](https://hwmon.wiki.kernel.org/device_support_status) 来确认驱动支持情况。

我们不建议使用`lm_sensors.service` 来加载驱动模块，请手动将配置文件放入`/etc/modules-load.d/load_these.conf`，使用 `lm_sensors.service` 可能导致设备地址在每次启动时变化。 在 `/etc/conf.d/lm_sensors` 你可以找到模块， 如果没有，请以root运行`sensors-detect`使用默认设置。 在`modules-load.d`一行行地加入。参见[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1415552#p1415552)

### lm-sensors

设置 [lm_sensors](/index.php/Lm_sensors "Lm sensors")。

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

如果不能正确地显示风扇转速，你可能需要增加风扇参数。

#### 增加 fan_div

Sensors输出的第一行是被主板用来读取温度和电压的chipset。

在 `/etc/sensors.d/`中创建文件:

 `/etc/sensors.d/fan-speed-control.conf` 
```
chip "*coretemp-isa-**"
set fan*X*_div 4
```

把*coretemp-isa-*替换为chipset的名称，并把`X`改成CPU风扇的编号。

保存文件，并以root身份运行:

```
# sensors -s

```

那将会重载配置文件。

再次运行 `sensors` ，看一下有没有读出RPM的值。如果没有，把`_div`后面的数增加到8, 16, 或32。重复尝试！

## Configuration

**Note:** Advanced users may want to skip this section and write `/etc/fancontrol` on their own, which also saves them from hearing all of the fans at full speed.

Once sensors is properly configured, run `pwmconfig` to test and configure speed control. Follow the instructions in `pwmconfig` to set up basic speeds. The default configuration options should create a new file, `/etc/fancontrol`.

### Tweaking

**Warning:** Some of the steps outlined below describe how to tweak fan speeds. Before doing this be sure to have a low CPU load.

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