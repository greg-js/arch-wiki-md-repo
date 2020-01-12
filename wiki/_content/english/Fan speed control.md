Related articles

*   [Lm_sensors](/index.php/Lm_sensors "Lm sensors")
*   [Undervolting CPU](/index.php/Undervolting_CPU "Undervolting CPU")
*   [PHC](/index.php/PHC "PHC")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")

Fan control can bring various benefits to your system, such as quieter working system and power saving by completely stopping fans on low CPU load.

**Warning:** Configuring or completely stopping fans on high system load might result in permanently damaged hardware.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Fancontrol (lm-sensors)](#Fancontrol_(lm-sensors))
    *   [2.1 lm-sensors](#lm-sensors)
    *   [2.2 Configuration](#Configuration)
        *   [2.2.1 Tweaking](#Tweaking)
    *   [2.3 Running Fancontrol](#Running_Fancontrol)
*   [3 NBFC](#NBFC)
    *   [3.1 Installation](#Installation)
    *   [3.2 Configuration](#Configuration_2)
*   [4 Dell laptops](#Dell_laptops)
    *   [4.1 Installation](#Installation_2)
    *   [4.2 Configuration](#Configuration_3)
    *   [4.3 Installation as a service](#Installation_as_a_service)
    *   [4.4 BIOS overriding fan control](#BIOS_overriding_fan_control)
*   [5 ThinkPad laptops](#ThinkPad_laptops)
    *   [5.1 Installation](#Installation_3)
    *   [5.2 Running](#Running)
*   [6 Asus laptops](#Asus_laptops)
    *   [6.1 Kernel modules](#Kernel_modules)
        *   [6.1.1 asus-nb-wmi](#asus-nb-wmi)
        *   [6.1.2 asus_fan](#asus_fan)
    *   [6.2 Generate config file with pwmconfig](#Generate_config_file_with_pwmconfig)
*   [7 AMDGPU sysfs fan control](#AMDGPU_sysfs_fan_control)
    *   [7.1 Configuration of manual control](#Configuration_of_manual_control)
    *   [7.2 amdgpu-fan](#amdgpu-fan)
    *   [7.3 fancurve script](#fancurve_script)
        *   [7.3.1 Setting up fancurve script](#Setting_up_fancurve_script)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Increase the fan divisor for sensors](#Increase_the_fan_divisor_for_sensors)
    *   [8.2 Device Paths have Changed in /etc/fancontrol](#Device_Paths_have_Changed_in_/etc/fancontrol)
        *   [8.2.1 Solution](#Solution)
        *   [8.2.2 Alternative Solution: Absolute paths](#Alternative_Solution:_Absolute_paths)

## Overview

**Note:** Laptop users should be aware about how cooling system works in their hardware. Some laptops have single fan for both CPU and GPU and cools both at the same time. Some laptops have two fans for CPU and GPU, but the first fan cools down CPU and GPU at the same time, while the other one cools CPU only. In some cases, you will not be able to use [Fancontrol](#Fancontrol_(lm-sensors)) script due to incompatible cooling architecture (e.g. one fan for both GPU and CPU). [Here](https://github.com/daringer/asus-fan/issues/47#issue-232063547) is some more information about this topic.

There are multiple working solutions for fan control for both desktops and notebooks. Depending on your needs:

*   [Fancontrol (lm-sensors)](#Fancontrol_(lm-sensors)) - Script (written in Bash) to configure fan speeds. Most suitable for desktops and laptops, where fan controls are available via sysfs.
*   [NoteBook Fan Control (NBFC)](#NBFC) - Cross-platform solution for laptop fan control, written in C# and works under [Mono](/index.php/Mono "Mono") runtime. Most suitable for latest, unsupported by [Fancontrol](#Fancontrol_(lm-sensors)) laptops.
*   [Dell laptops](#Dell_laptops) - Alternative fan control daemon for some Dell laptops.
*   [ThinkPad laptops](#ThinkPad_laptops) - Fan configuration for some ThinkPad laptops.
*   [Asus laptops](#Asus_laptops) - Configure some Asus laptops for [Fancontrol](#Fancontrol_(lm-sensors)) or manual control.

## Fancontrol (lm-sensors)

`fancontrol` is a part of [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors), which can be used to control the speed of CPU/case fans.

Support for newer motherboards may not yet be in the Linux kernel. Check the official [lm-sensors devices](https://hwmon.wiki.kernel.org/device_support_status) table to see if experimental drivers are available for such motherboards.

### lm-sensors

The first thing to do is to run

```
# sensors-detect

```

This will detect all of the sensors present and they will be used for fancontrol. After that, run the following to check if it detected the sensors correctly:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:      +29.0°C  (high = +76.0°C, crit = +100.0°C)  
...
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

**Note:** If the output does not display an RPM value for the CPU fan, one may need to [#Increase the fan divisor for sensors](#Increase_the_fan_divisor_for_sensors). If the fan speed is shown and higher than 0, this is fine.

### Configuration

Once the sensors are properly configured, use `pwmconfig` to test and configure fan speed control. Following the guide should create /etc/fancontrol a customized configuration file. In the guide, the default answers are in parenthesis if you press enter without typing anything. Enter "y" for yes, "n" for no.

```
# pwmconfig

```

**Note:** Some users may experience issues when using /sys/class/hwmon/ paths for their configuration file. hwmon class device symlinks points to the absolute paths, and are used to group all of the hwmon sensors together into one folder for easier access. Sometimes, the order of the hwmon devices change from a reboot, causing fancontrol to stop working. Go to [#Device Paths have Changed in /etc/fancontrol](#Device_Paths_have_Changed_in_/etc/fancontrol) for more information on how to fix this.

#### Tweaking

Some users may want to manually tweak the config file after running pwmconfig, usually to fix something. For manually tweaking the `/etc/fancontrol` configuration file, see the [fancontrol(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fancontrol.8) manual page for the definitions of the variables.

Users will probably encounter the hwmon path issues as noted above in [#Fancontrol (lm-sensors)](#Fancontrol_(lm-sensors)). Look at [#Device Paths have Changed in /etc/fancontrol](#Device_Paths_have_Changed_in_/etc/fancontrol) for more information.

**Tip:** Use `MAXPWM` and `MINPWM` options that limit fan speed range. See the [fancontrol(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fancontrol.8) manual page for details.

**Note:** Temperature and fan sensor paths could change as well (usually on a kernel update) (e.g. `hwmon0/device/temp1_input` becomes `hwmon0/temp1_input`). Check the system log to find out which path is the troublemaker:
```
# systemctl status fancontrol.service 

```
and correct your config file accordingly.

### Running Fancontrol

Try to run *fancontrol*:

```
# fancontrol

```

A properly configured setup will not output errors and will take control of the system fans. Users should hear system fans starting shortly after executing this command.

To enable starting *fancontrol* automatically on every boot, [enable](/index.php/Enable "Enable") `fancontrol.service`:

```
# systemctl enable fancontrol.service

```

To start it in the background, run

```
# systemctl start fancontrol.service

```

For an unofficial GUI [install](/index.php/Install "Install") [fancontrol-gui](https://aur.archlinux.org/packages/fancontrol-gui/) or [fancontrol-kcm](https://aur.archlinux.org/packages/fancontrol-kcm/).

## NBFC

NBFC is a cross-platform fan control solution for notebooks. It comes with a powerful configuration system, which allows to adjust it to many different notebook models, including some of the latest ones.

### Installation

NBFC can be installed as [nbfc](https://aur.archlinux.org/packages/nbfc/) or [nbfc-git](https://aur.archlinux.org/packages/nbfc-git/). Also start and enable `nbfc.service`.

### Configuration

NBFC comes with pre-made profiles. You can find them in `/opt/nbfc/Configs/` directory. When applying them, use exact profile name without extension (e.g. `some profile.xml` becomes `"some profile"`).

Check if there is anything NBFC can recommend:

```
$ nbfc config -r

```

If there is at least one model, try to apply this profile and see how fan speeds are being handled. For example:

```
$ nbfc config -a "Asus Zenbook UX430UA"

```

**Note:** If you are getting `File Descriptor does not support writing`, delete `StagWare.Plugins.ECSysLinux.dll` [[1]](https://github.com/hirschmann/nbfc/issues/439) and [restart](/index.php/Restart "Restart") `nbfc.service`:
```
# mv /opt/nbfc/Plugins/StagWare.Plugins.ECSysLinux.dll /opt/nbfc/Plugins/StagWare.Plugins.ECSysLinux.dll.old

```

If above solution did not help, try appending `ec_sys.write_support=1` to [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

If there are no recommended models, go to [NBFC git repository](https://github.com/hirschmann/nbfc/tree/master/Configs) or `/opt/nbfc/Configs/` and check if there are any similar models available from the same manufacturer. For example, on **Asus Zenbook UX430UQ**, the configuration **Asus Zenbook UX430UA** did not work well (fans completelly stopped all the time), but **Asus Zenbook UX410UQ** worked fantastically.

Run `nbfc` to see all options. More information about configuration is available at [upstream wiki](https://github.com/hirschmann/nbfc/wiki/).

## Dell laptops

`i8kutils` is a daemon to configure fan speed according to CPU temperatures on some Dell Inspiron and Latitude laptops. It uses the `/proc/i8k` interface provided by the `dell_smm_hwmon` driver (formerly `i8k`). Results will vary depending on the exact model of laptop.

**Warning:** i8kutils BIOS system calls stop the kernel for a moment on some systems (confirmed on Dell 9560), this can lead to side effects like audio dropouts, see [https://bugzilla.kernel.org/show_bug.cgi?id=201097](https://bugzilla.kernel.org/show_bug.cgi?id=201097)

### Installation

[i8kutils](https://aur.archlinux.org/packages/i8kutils/) is the main package to control fan speed. Additionally, you might want to install these:

*   [acpi](https://www.archlinux.org/packages/?name=acpi) - must be installed to use `i8kmon`.
*   [tcl](https://www.archlinux.org/packages/?name=tcl) - must be installed in order to run `i8kmon` as a background service (using the `--daemon` option).
*   [tk](https://www.archlinux.org/packages/?name=tk) - must be installed together with [tcl](https://www.archlinux.org/packages/?name=tcl) to run as X11 desktop applet.
*   [dell-bios-fan-control-git](https://aur.archlinux.org/packages/dell-bios-fan-control-git/) - recommended if your BIOS overrides fan control

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

### Installation as a service

`i8kmon` can be started automatically as a [systemd](/index.php/Systemd "Systemd") service:

```
 # systemctl enable i8kmon
 # systemctl start i8kmon

```

### BIOS overriding fan control

Some newer laptops have BIOS fan control in place which will override the OS level fan control. To test if this the case, run `i8kmon` with verbose mode in a command line, make sure the CPU is idle, then see if the fan is turned off or turned down accordingly.

If the BIOS fan control is in place, you can try using [dell-bios-fan-control-git](https://aur.archlinux.org/packages/dell-bios-fan-control-git/):

**Warning:** turning off BIOS fan control could result in damage to your hardware. Make sure you have i8kmon properly set up beforehand, or leave the CPU idle while you test this program

To enable BIOS fan control:

```
 # dell-bios-fan-control 1

```

To disable BIOS fan control:

```
 # dell-bios-fan-control 0

```

To automatically disable BIOS fan control via [systemd](/index.php/Systemd "Systemd"):

```
 # systemctl enable dell-bios-fan-control
 # systemctl start dell-bios-fan-control

```

## ThinkPad laptops

Current fan control daemons available in the [AUR](/index.php/AUR "AUR") are [simpfand-git](https://aur.archlinux.org/packages/simpfand-git/) and [thinkfan](https://aur.archlinux.org/packages/thinkfan/) (recommended).

### Installation

Install [thinkfan](https://aur.archlinux.org/packages/thinkfan/) or [thinkfan-git](https://aur.archlinux.org/packages/thinkfan-git/). Optionally, but recommended, install [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors). Then have a look at the files:

```
# pacman -Ql thinkfan

```

Note that the thinkfan package installs `/usr/lib/modprobe.d/thinkpad_acpi.conf`, which contains

```
options thinkpad_acpi fan_control=1

```

So fan control is enabled by default. Alternatively, you can enable fan control as follows:

```
$ echo "options thinkpad_acpi fan_control=1" > /etc/modprobe.d/thinkfan.conf

```

Now, load the module:

```
$ su
# modprobe thinkpad_acpi
# cat /proc/acpi/ibm/fan

```

You should see that the fan level is "auto" by default, but you can echo a level command to the same file to control the fan speed manually. The thinkfan daemon will do this automatically.

Finally, enable the thinkfan systemd service:

```
$ systemctl enable thinkfan

```

To configure the temperature thresholds, you will need to copy one of the example config files (e.g. `/usr/share/doc/thinkfan/examples/thinkfan.conf.simple`) to `/etc/thinkfan.conf`, and modify to taste. This file specifies which sensors to read, and which interface to use to control the fan. Some systems have `/proc/acpi/ibm/fan` and `/proc/acpi/ibm/thermal` available; on others, you will need to specify something like:

```
hwmon /sys/devices/virtual/thermal/thermal_zone0/temp

```

to use generic hwmon sensors instead of thinkpad-specific ones.

### Running

You can test your configuration first by running thinkfan manually (as root):

```
# thinkfan -n

```

and see how it reacts to the load level of whatever other programs you have running.

When you have it configured correctly, [start/enable](/index.php/Start/enable "Start/enable") `thinkfan.service`.

## Asus laptops

This topic will cover drivers configuration on Asus laptops for [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29).

### Kernel modules

In configuration files, we are going to use full paths to sysfs files (e.g. `/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1`). This is because hwmon**1** might change to any other number after reboot. [Fancontrol (lm-sensors)](#Fancontrol_.28lm-sensors.29) is written in [Bash](/index.php/Bash "Bash"), so using these paths in configuration file is completely acceptable. You can find complete `/etc/fancontrol` configuration file examples at [ASUS N550JV#Fan control](/index.php/ASUS_N550JV#Fan_control "ASUS N550JV").

#### asus-nb-wmi

*asus-nb-wmi* is a kernel module, which is included in the Linux kernel and is loaded automatically on Asus laptops. It will only allow to control a single fan and if there is a second fan you will not have any controls over it. Note that blacklisting this module will prevent keyboard backlight to work.

Below are the commands to control it. Check if you have any controls over your fan:

```
# echo 255 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1           # Full fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1             # Fan is stopped (Value: 0)
# echo 2 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[[:print:]]*/pwm1_enable     # Change fan mode to automatic
# echo 1 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1_enable      # Change fan mode to manual

```

If you were able to modify fan speed with above commands, then continue with [#Generate config file with pwmconfig](#Generate_config_file_with_pwmconfig).

#### asus_fan

*asus_fan* is a kernel module, which allows to control both fans on some older Asus laptops. It does not work with the most recent models.

Install the [DKMS](/index.php/DKMS "DKMS") [asus-fan-dkms-git](https://aur.archlinux.org/packages/asus-fan-dkms-git/) [kernel module](/index.php/Kernel_module "Kernel module"), providing `asus_fan`:

```
# modprobe asus_fan

```

Check if you have any control over both fans:

```
# echo 255 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1          # Full CPU fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1            # CPU fan is stopped (Value: 0)
# echo 255 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2          # Full GFX fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2            # GFX fan is stopped (Value: 0)
# echo 2 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1_enable     # Change CPU fan mode to automatic
# echo 1 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1_enable     # Change CPU fan mode to manual
# echo 2 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2_enable     # Change GFX fan mode to automatic
# echo 1 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2_enable     # Change GFX fan mode to manual
# cat /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/temp1_input          # Display GFX temperature (will always be 0 when GFX is disabled/unused)

```

If everything works, you might want to load this kernel module [on boot](/index.php/Kernel_module#Automatic_module_loading_with_systemd "Kernel module"):

 `/etc/modules-load.d/asus_fan.conf` 
```
asus_fan

```

Continue with [#Generate config file with pwmconfig](#Generate_config_file_with_pwmconfig).

### Generate config file with pwmconfig

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

## AMDGPU sysfs fan control

[AMDGPU](/index.php/AMDGPU "AMDGPU") kernel driver offers fan control for graphics cards via hwmon in sysfs.

### Configuration of manual control

To switch to manual fan control from automatic, run

```
# echo "1" > /sys/class/drm/card0/device/hwmon/hwmon0/pwm1_enable

```

Set up fan speed to e.g. 50% (100% are 255 PWM cycles, thus calculate desired fan speed percentage by multiplying its value by 2.55):

```
# echo "128" > /sys/class/drm/card0/device/hwmon/hwmon0/pwm1

```

To reset to automatic fan control, run

```
# echo "2" > /sys/class/drm/card0/device/hwmon/hwmon0/pwm1_enable

```

**Warning:** Resetting fan speed to auto may not work due to a driver bug and instead a restart of the driver may be required as a workaround.

### amdgpu-fan

The [amdgpu-fan](https://aur.archlinux.org/packages/amdgpu-fan/) package is an automated fan controller for AMDGPU-enabled video cards written in Python. It uses a "speed-matrix" to match the frequency of the fans with the temperature of the GPU, for example:

```
speed_matrix:  # -[temp(*C), speed(0-100%)]
- [0, 0]
- [40, 30]
- [60, 50]
- [80, 100]
```

Once the package can be installed, it can be run as a service, so you can either run it for the current session:

```
# systemctl start amdgpu-fan.service

```

or executed at boot

```
# systemctl enable amdgpu-fan.service

```

### fancurve script

Not just fan controls are offered via hwmon in sysfs, but also GPU temperature reading:

```
cat /sys/class/drm/card0/device/hwmon/hwmon0/temp1_input

```

This outputs GPU temperature in °C + three zeroes, e.g. `33000` for 33°C.

The bash script [amdgpu-fancontrol](https://github.com/grmat/amdgpu-fancontrol) by grmat offers a fully automatic fan control by using the described sysfs hwmon functionality. It also allows to comfortably adjust the fancurve's temperature/PWM cycles assignments and a hysteresis by offering abstracted configuration fields at the top of the script.

**Tip:** In order to function correctly, the script needs at least three defined temperature/PWM cycles assignments.

For safety reasons, the script sets fan control again to auto when shutting down. This may cause spinning up of fans, which can be worked around at cost of security by setting `set_fanmode 1` in the section `function reset_on_fail`.

#### Setting up fancurve script

To start the script, it is recommend to do so via [systemd](/index.php/Systemd "Systemd") init system. This way the script's verbose output can be read via [journalctl](/index.php/Journalctl "Journalctl")/systemctl status. For this purpose, a .service configuration file is already included in the GitHub repository.

It may also be required to restart the script via a [root-resume.service](/index.php/Power_management#Sleep_hooks "Power management") after hibernation in order to make it automatically function properly again:

 `/etc/systemd/system/root-resume.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target

[Service]
Type=simple
ExecStart=/usr/bin/systemctl restart amdgpu-fancontrol.service

[Install]
WantedBy=suspend.target
```

## Troubleshooting

### Increase the fan divisor for sensors

If *sensors* does not output the CPU fan RPM, it may be necessary to change the fan divisor.

The first line of the *sensors* output is the chipset used by the motherboard for readings of temperatures and voltages.

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

### Device Paths have Changed in /etc/fancontrol

The enumerated hwmon symlinks located in /sys/class/hwmon/ might vary in order because the kernel modules do not load in a consistent order per boot. Because of this, it may cause fancontrol to not function correctly.

#### Solution

In `/etc/conf.d/lm_sensors`, there are 2 arrays that lists all of the modules detected when you execute `sensors-detect`. These get loaded in by fancontrol. If the file does not exist, run `sensors-detect` as root, accepting the defaults. Open (or create) `/etc/modules-load.d/modules.conf`. Get all of the modules listed from the 2 variables in {{ic|/etc/conf.d/lm_sensors/ and place them into the `/etc/modules-load.d/modules.conf` file, one module per line. Specifying them like this should make a defined order for the modules to load in, which should make the hwmon paths stay where they are and not change orders for every boot. If this doesnt work, I highly recommend finding another program to control your fans. If you cannot find any, then you could try using the alternative solution below.

#### Alternative Solution: Absolute paths

Using absolute file paths in fancontrol does not work by default, as its helper script `pwmconfig` is programmed to only use the hwmon paths to get the files. The way it does this is that it detects whether the hwmon path that is provided in its config file `/etc/fancontrol` did not change, and uses the variables `DEVNAME` and `DEVPATH` to determine such change. If your hwmon paths keep changing, this will prevent fancontrol from running no matter what you do. However, one can circumvent this problem. Open `/usr/bin/fancontrol`, and comment out this part of the script:

```
if ! ValidateDevices "$DEVPATH" "$DEVNAME"
 then
     echo "Configuration appears to be outdated, please run pwmconfig again" >&2
     exit 1
 fi

```

**Note:** Doing this may make fancontrol write into files you gave it in the config file, no matter what the file is. This can corrupt files if you provide the wrong path. Be sure that you are using the correct path for your files.

Another thing to note is that while doing this workaround, using `pwmconfig` to create your script again will overwrite all of your absolute paths that you have configured. Therefore, it is better to manually change the old paths to the new paths if it is needed instead of using pwmconfig.

Commenting this out should effectively ignore the hwmon validation checks. You can also ignore the variables `DEVNAME` and `DEVPATH` in the config file as well. After this, replace all of the hwmon paths in the other variables with its absolute path. To make it easier, rerun `pwmconfig` to refresh the hwmon devices. The hwmon paths in the config file should now point to the correct absolute paths. For each hwmon path, run the following command:

```
"#" is the enumeration of the hwmon path
$ readlink -f /sys/class/hwmon/hwmon#/device

```

This will give you the absolute path of the device.

For example, a /etc/fancontrol file lists FCTEMPS as this:

```
FCTEMPS=hwmon2/pwm1=hwmon3/temp1_input

```

Executing `readlink -f /sys/class/hwmon/hwmon3/device` can, for example, output `/sys/devices/platform/coretemp.0/`. `cd` into this directory. If you see a `/hwmon/hwmon#/` directory, you have to do this in your fancontrol config file to replace the hwmon# path. From the previous example:

```
# BEFORE
FCTEMPS=hwmon2/pwm1=hwmon3/temp1_input
# AFTER
FCTEMPS=hwmon2/pwm1=/sys/devices/platform/coretemp.0/hwmon/[[:print:]]*/temp1_input

```

Essentially, you must replace the hwmon path with the absolute path, concatenated with {{ic|/hwmon/[[:print:]]*/} so that bash can catch the random enumerated hwmon name.

If you do not see the `/hwmon/hwmon#/` directory, then you do not have to worry about this. This means that the temperature files are in the root of the device folder. Just replace `hwmon#/` with the absolute file path. For example:

```
#BEFORE
FCTEMPS=hwmon2/pwm1=hwmon3/temp1_input
#AFTER
FCTEMPS=hwmon2/pwm1=/sys/devices/platform/coretemp.0/temp1_input

```

After replacing all of paths, fancontrol should work fine.