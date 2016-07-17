There are several supported ODROID ARM boards available to consumers. This wiki page offers general configuration that should be applicable to them all. At this point, the content has been verified to work on the ODROID-C2 and ODROID-U3.

**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org](http://archlinuxarm.org) not through posts to the official Arch Linux Forum. Any posts related to ARM specific issues will be promptly closed per the [Code of conduct#Arch Linux distribution support *only*](/index.php/Code_of_conduct#Arch_Linux_distribution_support_.2Aonly.2A "Code of conduct") policy.

## Contents

*   [1 Installation](#Installation)
*   [2 CPU frequency scaling](#CPU_frequency_scaling)
    *   [2.1 Show online/offline cores](#Show_online.2Foffline_cores)
    *   [2.2 Read CPU temperature](#Read_CPU_temperature)
    *   [2.3 Read CPU frequency](#Read_CPU_frequency)
    *   [2.4 Read CPU governor](#Read_CPU_governor)
*   [3 LEDs](#LEDs)
    *   [3.1 Blue LED](#Blue_LED)
        *   [3.1.1 List available triggers](#List_available_triggers)
        *   [3.1.2 Temporary configuration](#Temporary_configuration)
        *   [3.1.3 Permanent configuration](#Permanent_configuration)
*   [4 CPU Fan](#CPU_Fan)
    *   [4.1 Fan Mode](#Fan_Mode)
    *   [4.2 Fan Speed (Manual Only)](#Fan_Speed_.28Manual_Only.29)
*   [5 See also](#See_also)

## Installation

See the installation instructions at the [Arch ARM](https://archlinuxarm.org) project page.

*   [ODROID-U2 (armv8)](https://archlinuxarm.org/platforms/armv8/amlogic/odroid-c2)
*   [ODROID-C1 (armv7)](https://archlinuxarm.org/platforms/armv7/amlogic/odroid-c1)
*   [ODROID-U2 (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-u2)
*   [ODROID-U3 (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-u3)

*   [ODROID-U3 (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-x)
*   [ODROID-X2 (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-x2)
*   [ODROID-XU (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu)
*   [ODROID-XU3 (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu3)
*   [ODROID-XU4 (armv7)](https://archlinuxarm.org/platforms/armv7/samsung/odroid-xu4)

## CPU frequency scaling

The [cpupower](https://www.archlinux.org/packages/?name=cpupower) package can be used to select alternative CPU governors for power savings. Edit `/etc/default/cpupower` and set the *governor=* line followed by [start](/index.php/Start "Start") cpupower.service.

### Show online/offline cores

If using the *hotplug* governor, idle cores are switched off to reduce power consumption and head generation.

```
lscpu |grep line

```

### Read CPU temperature

```
awk '{printf "%3.1f°C
", $1/1000}' /sys/class/thermal/thermal_zone0/temp

```

### Read CPU frequency

```
awk '{printf "%3.1f MHz
", $1/1000}' /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq

```

### Read CPU governor

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

```

## LEDs

The ODROID-U3 has two LEDs. A red power LED which is always on if power is supplied, and a blue LED which can be configured.

### Blue LED

By default, the blue LED is a heartbeat LED, which flashes when the kernel is running. This can be changed through the `/sys/class/leds/led1/trigger` interface.

#### List available triggers

 `# cat /sys/class/leds/led1/trigger`  `none mmc0 mmc1 timer oneshot [heartbeat] backlight gpio cpu0 cpu1 cpu2 cpu3 default-on transient` 

#### Temporary configuration

Replace `*TRIGGER*` with one of the available triggers. This setting will apply instantly, but be lost upon reboot.

 `# echo *TRIGGER* > /sys/class/leds/led1/trigger` 

#### Permanent configuration

Replace `*TRIGGER*` with one of the available triggers. This setting will apply upon reboot.

 `/etc/tmpfiles.d/leds.conf`  `w /sys/class/leds/led1/trigger - - - - *TRIGGER*` 

## CPU Fan

The optional CPU fan can be controlled via the `/sys/devices/platform/odroidu2-fan` interface.

### Fan Mode

 `# echo auto > /sys/devices/platform/odroidu2-fan/fan_mode`  `# echo manual > /sys/devices/platform/odroidu2-fan/fan_mode` 

### Fan Speed (Manual Only)

Values range from 0 (0%) to 255 (100%)

 `# echo 0 > /sys/devices/platform/odroidu2-fan/pwm_duty`  `# echo 255 > /sys/devices/platform/odroidu2-fan/pwm_duty` 

## See also

*   [Hardkernel Product Page](http://www.hardkernel.com/main/main.php)