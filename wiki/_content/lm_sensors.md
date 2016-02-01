# lm_sensors

Related articles

*   [hddtemp](/index.php/Hddtemp "Hddtemp")
*   [monitorix](/index.php/Monitorix "Monitorix")

[lm_sensors](http://lm-sensors.org/) (Linux monitoring sensors) is a free and open-source application that provides tools and drivers for monitoring temperatures, voltage, and fans. This document explains how to install, configure, and use lm_sensors.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
*   [3 Running sensors](#Running_sensors)
    *   [3.1 Reading SPD values from memory modules (optional)](#Reading_SPD_values_from_memory_modules_.28optional.29)
*   [4 Using Sensor Data](#Using_Sensor_Data)
    *   [4.1 Graphical Front-ends](#Graphical_Front-ends)
    *   [4.2 sensord](#sensord)
*   [5 Tips and Tricks](#Tips_and_Tricks)
    *   [5.1 Adjusting Values](#Adjusting_Values)
        *   [5.1.1 Example 1\. Adjusting Temperature Offsets](#Example_1._Adjusting_Temperature_Offsets)
        *   [5.1.2 Example 2\. Renaming Labels](#Example_2._Renaming_Labels)
        *   [5.1.3 Example 3\. Renumbering Cores for Multi-CPU Systems](#Example_3._Renumbering_Cores_for_Multi-CPU_Systems)
    *   [5.2 Automatic lm_sensors Deployment](#Automatic_lm_sensors_Deployment)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 K10Temp Module](#K10Temp_Module)
    *   [6.2 Sensors not working since Linux 2.6.31](#Sensors_not_working_since_Linux_2.6.31)
    *   [6.3 Gigabyte GA-J1900N-D3V](#Gigabyte_GA-J1900N-D3V)
    *   [6.4 Laptop Screen issues after running sensors-detect](#Laptop_Screen_issues_after_running_sensors-detect)

## Installation

[Install](/index.php/Install "Install") the [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) package.

## Setup

Use **sensors-detect** to detect and generate a list of kernel modules:

**Warning:** Do not use anything other than the default options (by just hitting `Enter`), unless you know exactly what you are doing. See [#Laptop Screen issues after running sensors-detect](#Laptop_Screen_issues_after_running_sensors-detect).

```
# sensors-detect

```

This will create the `/etc/conf.d/lm_sensors` configuration file which is used by the `sensors` daemon to automatically load kernel modules on boot. Users are asked to probe for various hardware. The "safe" answers are the defaults, so just hitting `Enter` to all the questions will generally not cause any problems.

When the detection is finished, a summary of the probes is presented.

Example:

 `# sensors-detect` 

```
This program will help you determine which kernel modules you need
to load to use lm_sensors most effectively. It is generally safe
and recommended to accept the default answers to all questions,
unless you know what you're doing.

Some south bridges, CPUs or memory controllers contain embedded sensors.
Do you want to scan for them? This is totally safe. (YES/no): 
Module cpuid loaded successfully.
Silicon Integrated Systems SIS5595...                       No
VIA VT82C686 Integrated Sensors...                          No
VIA VT8231 Integrated Sensors...                            No
AMD K8 thermal sensors...                                   No
AMD Family 10h thermal sensors...                           No

...

Now follows a summary of the probes I have just done.
Just press ENTER to continue: 

Driver `coretemp':
  * Chip `Intel digital thermal sensor' (confidence: 9)

Driver `lm90':
  * Bus `SMBus nForce2 adapter at 4d00'
    Busdriver `i2c_nforce2', I2C address 0x4c
    Chip `Winbond W83L771AWG/ASG' (confidence: 6)

Do you want to overwrite /etc/conf.d/lm_sensors? (YES/no): 
ln -s '/usr/lib/systemd/system/lm_sensors.service' '/etc/systemd/system/multi-user.target.wants/lm_sensors.service'
Unloading i2c-dev... OK
Unloading cpuid... OK

```

**Note:** A systemd service is automatically enabled if users answer **YES** when asked about generating `/etc/conf.d/lm_sensors`. Answering **YES** also automatically starts the service.

## Running sensors

Example running `sensors`:

 `$ sensors` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +35.0°C  (crit = +105.0°C)
Core 1:       +32.0°C  (crit = +105.0°C)

w83l771-i2c-0-4c
Adapter: SMBus nForce2 adapter at 4d00
temp1:        +28.0°C  (low  = -40.0°C, high = +70.0°C)
                       (crit = +85.0°C, hyst = +75.0°C)
temp2:        +37.4°C  (low  = -40.0°C, high = +70.0°C)
                       (crit = +110.0°C, hyst = +100.0°C)

```

### Reading SPD values from memory modules (optional)

To read the SPD timing values from memory modules, install [i2c-tools](https://www.archlinux.org/packages/?name=i2c-tools) from the [official repositories](/index.php/Official_repositories "Official repositories"). Once installed, load the `eeprom` [kernel module](/index.php/Kernel_module "Kernel module").

```
# modprobe eeprom

```

Finally, view memory information with `decode-dimms`.

Here is partial output from one machine:

 `# decode-dimms` 

```
Memory Serial Presence Detect Decoder
By Philip Edelbrock, Christian Zuckschwerdt, Burkart Lingner,
Jean Delvare, Trent Piepho and others

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0050
Guessing DIMM is in                             bank 1

---=== SPD EEPROM Information ===---
EEPROM CRC of bytes 0-116                       OK (0x583F)
# of bytes written to SDRAM EEPROM              176
Total number of bytes in EEPROM                 512
Fundamental Memory type                         DDR3 SDRAM
Module Type                                     UDIMM

---=== Memory Characteristics ===---
Fine time base                                  2.500 ps
Medium time base                                0.125 ns
Maximum module speed                            1066MHz (PC3-8533)
Size                                            2048 MB
Banks x Rows x Columns x Bits                   8 x 14 x 10 x 64
Ranks                                           2
SDRAM Device Width                              8 bits
tCL-tRCD-tRP-tRAS                               7-7-7-33
Supported CAS Latencies (tCL)                   8T, 7T, 6T, 5T

---=== Timing Parameters ===---
Minimum Write Recovery time (tWR)               15.000 ns
Minimum Row Active to Row Active Delay (tRRD)   7.500 ns
Minimum Active to Auto-Refresh Delay (tRC)      49.500 ns
Minimum Recovery Delay (tRFC)                   110.000 ns
Minimum Write to Read CMD Delay (tWTR)          7.500 ns
Minimum Read to Pre-charge CMD Delay (tRTP)     7.500 ns
Minimum Four Activate Window Delay (tFAW)       30.000 ns

---=== Optional Features ===---
Operable voltages                               1.5V
RZQ/6 supported?                                Yes
RZQ/7 supported?                                Yes
DLL-Off Mode supported?                         No
Operating temperature range                     0-85C
Refresh Rate in extended temp range             1X
Auto Self-Refresh?                              Yes
On-Die Thermal Sensor readout?                  No
Partial Array Self-Refresh?                     No
Thermal Sensor Accuracy                         Not implemented
SDRAM Device Type                               Standard Monolithic

---=== Physical Characteristics ===---
Module Height (mm)                              15
Module Thickness (mm)                           1 front, 1 back
Module Width (mm)                               133.5
Module Reference Card                           B

---=== Manufacturer Data ===---
Module Manufacturer                             Invalid
Manufacturing Location Code                     0x02
Part Number                                     OCZ3G1600LV2G     

...

```

## Using Sensor Data

### Graphical Front-ends

There are a variety of front-ends for sensors data.

*   [conky](/index.php/Conky "Conky") - Conky is an advanced, highly configurable system monitor for X based on torsmo
*   [xsensors](https://www.archlinux.org/packages/?name=xsensors) - X11 interface to lm_sensors

For specific [Desktop environments](/index.php/Desktop_environments "Desktop environments"):

*   [sensors-applet](https://www.archlinux.org/packages/?name=sensors-applet) - applet for the [GNOME](/index.php/GNOME "GNOME") Panel to display readings from hardware sensors, including CPU temperature, fan speeds and voltage readings.
*   [plasma5-applets-thermal-monitor-git](https://aur.archlinux.org/packages/plasma5-applets-thermal-monitor-git/)<sup><small>AUR</small></sup> - Is an example of the [widgets](/index.php/KDE#Widgets "KDE") available for [KDE](/index.php/KDE "KDE") desktop.
*   [sensors-lxpanel-plugin](https://aur.archlinux.org/packages/sensors-lxpanel-plugin/)<sup><small>AUR</small></sup> -- A lm_sensors plugin for the [LXDE](/index.php/LXDE "LXDE") panel. lxpanel also includes a simple 'Temperature Monitor' plugin.
*   [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin) - A lm_sensors plugin for the [Xfce](/index.php/Xfce "Xfce") panel

### sensord

There is an optional daemon called sensord (included with the [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) package) which can log data to a round robin database (rrd) and later visualize graphically. See the sensord man page for details.

## Tips and Tricks

### Adjusting Values

In some cases, the data displayed might be incorrect or users may wish to rename the output. Use cases include:

*   Incorrect temperature values due to a wrong offset (i.e. temps are reported 20 °C higher then actual).
*   Users wish to rename the output of some sensors.
*   The cores might be displayed in an incorrect order.

All of the above (and more) can be adjusted by overriding the package provides settings in `/etc/sensors3.conf` by creating `/etc/sensors.d/foo` wherein any number of tweaks will override the default values. It is recommended to rename 'foo' to the motherboard brand and model but this naming nomenclature is optional.

**Note:** Do not edit /etc/sensors3.conf directly since package updates will overwrite any changes thus losing them.

#### Example 1\. Adjusting Temperature Offsets

This is a real example on a Zotac ION-ITX-A-U motherboard. The coretemp values are off by 20 °C (too high) and are adjusted down to Intel specs.

 `$ sensors` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +57.0°C  (crit = +125.0°C)
Core 1:       +55.0°C  (crit = +125.0°C)
...

```

Run `sensors` with the `-u` switch to see what options are available for each physical chip (raw mode):

 `$ sensors -u` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:
  temp2_input: 57.000
  temp2_crit: 125.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 55.000
  temp3_crit: 125.000
  temp3_crit_alarm: 0.000
...

```

Create the following file overriding the default values:

 `/etc/sensors.d/Zotac-IONITX-A-U` 

```
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  compute temp2 @-20,@-20

  label temp3 "Core 1"
  compute temp3 @-20,@-20

```

Now invoking `sensors` shows the adjust values:

 `$ sensors` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +37.0°C  (crit = +105.0°C)
Core 1:       +35.0°C  (crit = +105.0°C)
...

```

#### Example 2\. Renaming Labels

This is a real example on an Asus A7M266\. The user wishes more verbose names for the temperature labels 'temp1' and 'temp2':

 `$ sensors` 

```
as99127f-i2c-0-2d
Adapter: SMBus Via Pro adapter at e800
...
temp1:        +35.0°C  (high =  +0.0°C, hyst = -128.0°C)
temp2:        +47.5°C  (high = +100.0°C, hyst = +75.0°C)
...

```

Create the following file to override the default values:

 `/etc/sensors.d/Asus_A7M266` 

```
chip "as99127f-*"
  label temp1 "Mobo Temp"
  label temp2 "CPU0 Temp"

```

Now invoking `sensors` shows the adjust values:

 `$ sensors` 

```
as99127f-i2c-0-2d
Adapter: SMBus Via Pro adapter at e800
...
Mobo Temp:        +35.0°C  (high =  +0.0°C, hyst = -128.0°C)
CPU0 Temp:        +47.5°C  (high = +100.0°C, hyst = +75.0°C)
...

```

#### Example 3\. Renumbering Cores for Multi-CPU Systems

This is a real example on an HP Z600 workstation with dual Xeons. The actual numbering of physical cores is incorrect: numbered 0, 1, 9, 10 which is repeated into the second CPU. Most users expect the core temperatures to report out in sequential order, i.e. 0,1,2,3,4,5,6,7.

 `$ sensors` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core 1:       +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core 9:       +66.0°C  (high = +85.0°C, crit = +95.0°C)
Core 10:      +66.0°C  (high = +85.0°C, crit = +95.0°C)

coretemp-isa-0004
Adapter: ISA adapter
Core 0:       +54.0°C  (high = +85.0°C, crit = +95.0°C)
Core 1:       +56.0°C  (high = +85.0°C, crit = +95.0°C)
Core 9:       +60.0°C  (high = +85.0°C, crit = +95.0°C)
Core 10:      +61.0°C  (high = +85.0°C, crit = +95.0°C)
...

```

Again, run `sensors` with the `-u` switch to see what options are available for each physical chip:

 `$ sensors -u coretemp-isa-0000` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:
  temp2_input: 61.000
  temp2_max: 85.000
  temp2_crit: 95.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 61.000
  temp3_max: 85.000
  temp3_crit: 95.000
  temp3_crit_alarm: 0.000
Core 9:
  temp11_input: 62.000
  temp11_max: 85.000
  temp11_crit: 95.000
Core 10:
  temp12_input: 63.000
  temp12_max: 85.000
  temp12_crit: 95.000

```

 `$ sensors -u coretemp-isa-0004` 

```
coretemp-isa-0004
Adapter: ISA adapter
Core 0:
  temp2_input: 53.000
  temp2_max: 85.000
  temp2_crit: 95.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 54.000
  temp3_max: 85.000
  temp3_crit: 95.000
  temp3_crit_alarm: 0.000
Core 9:
  temp11_input: 59.000
  temp11_max: 85.000
  temp11_crit: 95.000
Core 10:
  temp12_input: 59.000
  temp12_max: 85.000
  temp12_crit: 95.000
...

```

Create the following file overriding the default values:

 `/etc/sensors.d/HP_Z600` 

```
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  label temp3 "Core 1"
  label temp11 "Core 2"
  label temp12 "Core 3"

chip "coretemp-isa-0004"
  label temp2 "Core 4"
  label temp3 "Core 5"
  label temp11 "Core 6"
  label temp12 "Core 7"
```

Now invoking `sensors` shows the adjust values:

 `$ sensors` 

```
coretemp-isa-0000
Adapter: ISA adapter
Core0:        +64.0°C  (high = +85.0°C, crit = +95.0°C)
Core1:        +63.0°C  (high = +85.0°C, crit = +95.0°C)
Core2:        +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core3:        +66.0°C  (high = +85.0°C, crit = +95.0°C)

coretemp-isa-0004
Adapter: ISA adapter
Core4:        +53.0°C  (high = +85.0°C, crit = +95.0°C)
Core5:        +54.0°C  (high = +85.0°C, crit = +95.0°C)
Core6:        +59.0°C  (high = +85.0°C, crit = +95.0°C)
Core7:        +60.0°C  (high = +85.0°C, crit = +95.0°C)
...

```

### Automatic lm_sensors Deployment

If users wishing to deploy lm_sensors on multiple machines can use either of the following:

1\. Accept defaults to questions:

```
# sensors-detect --auto

```

2\. Override defaults and answer YES to all questions:

```
 # yes | sensors-detect

```

## Troubleshooting

### K10Temp Module

Some K10 processors have issues with their temperature sensor. From the kernel documentation (`linux-<version>/Documentation/hwmon/k10temp`):

NaN

NaN

On affected machines the module will report "unreliable CPU thermal sensor; monitoring disabled". Users which to force it can:

```
# rmmod k10temp
# modprobe k10temp force=1

```

Confirm that the sensor is in fact valid and reliable. If it is, can edit `/etc/modprobe.d/k10temp.conf` and add:

```
options k10temp force=1

```

This will allow the module to load at boot.

### Sensors not working since Linux 2.6.31

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** kernel 2.6 references (Discuss in [Talk:Lm sensors#kernel 2.6 workaround](https://wiki.archlinux.org/index.php/Talk:Lm_sensors#kernel_2.6_workaround))

A change in version 2.6.31 has made some sensors stop working. See [this FAQ entry](http://www.lm-sensors.org/wiki/FAQ/Chapter3#Mysensorshavestoppedworkinginkernel2.6.31) for a detailed explanation and for some example errors. To fix sensors, add the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_enforce_resources=lax

```

**Warning:** In some situations, this may be dangerous. Consult the FAQ for details.

Note that in most cases the information is still accessible via other modules (e.g. via ACPI modules) for the hardware in question. Many utilities and monitors (e.g. `/usr/bin/sensors`) can gather information from either source. Where possible, this is the preferred solution.

### Gigabyte GA-J1900N-D3V

The motherboard use the ITE IT8620E chip (useful also to read voltages, mainboard temp, fan speed). As of October 2014, lm_sensors has no driver support for chip ITE IT8620E [[1]](http://www.lm-sensors.org/wiki/Devices) [[2]](http://comments.gmane.org/gmane.linux.drivers.sensors/35168). lm_sensors developers had a report that the chip is somewhat compatible with the IT8728F for the hardware monitoring part.

You can load the module at runtime with modprobe:

```
$ modprobe it87 force_id=0x8728

```

Or you can [load the module](/index.php/Kernel_modules#Loading "Kernel modules") during boot process by creating the following two files:

 `/etc/modules-load.d/it87.conf`  `it87`  `/etc/modprobe.d/it87.conf`  `options it87 force_id=0x8603` 

Once the module is loaded you can use the _sensors_ tool to probe the chip.

Now you can also use [fancontrol](/index.php/Fancontrol "Fancontrol") to control the speedsteps of your case fan.

### Laptop Screen issues after running sensors-detect

This is caused by lm-sensors messing with the Vcom values of the screen while probing for sensors. It has been discussed and solved at the forums already: [https://bbs.archlinux.org/viewtopic.php?id=193048](https://bbs.archlinux.org/viewtopic.php?id=193048) However, make sure to read through the thread carefully before running any of the suggested commands.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lm_sensors&oldid=418626](https://wiki.archlinux.org/index.php?title=Lm_sensors&oldid=418626)"