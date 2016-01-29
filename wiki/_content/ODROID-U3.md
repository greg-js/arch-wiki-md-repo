# ODROID-U3

Related articles

*   [Installation guide](/index.php/Installation_guide "Installation guide")

From [Arch Linux ARM ODROID-U3 Page](http://archlinuxarm.org/platforms/armv7/samsung/odroid-u3):

NaN

**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org](http://archlinuxarm.org) not through posts to the official Arch Linux Forum. Any posts related to ARM specific issues will be promptly closed per the [Arch Linux Distribution Support ONLY](https://wiki.archlinux.org/index.php/Forum_etiquette#Arch_Linux_distribution_support_ONLY) policy.

## Contents

*   [1 Installation](#Installation)
*   [2 LEDs](#LEDs)
    *   [2.1 Blue LED](#Blue_LED)
        *   [2.1.1 List available triggers](#List_available_triggers)
        *   [2.1.2 Temporary configuration](#Temporary_configuration)
        *   [2.1.3 Permanent configuration](#Permanent_configuration)
*   [3 CPU Fan](#CPU_Fan)
    *   [3.1 Fan Mode](#Fan_Mode)
    *   [3.2 Fan Speed (Manual Only)](#Fan_Speed_.28Manual_Only.29)
    *   [3.3 Read CPU Temperature](#Read_CPU_Temperature)
*   [4 See also](#See_also)

## Installation

See the installation instructions at the [Arch Linux ARM ODROID-U3](http://archlinuxarm.org/platforms/armv7/samsung/odroid-u3) page.

## LEDs

The ODROID-U3 has two LEDs. A red power LED which is always on if power is supplied, and a blue LED which can be configured.

### Blue LED

By default, the blue LED is a heartbeat LED, which flashes when the kernel is running. This can be changed through the `/sys/class/leds/led1/trigger` interface.

#### List available triggers

 `# cat /sys/class/leds/led1/trigger`  `none mmc0 mmc1 timer oneshot [heartbeat] backlight gpio cpu0 cpu1 cpu2 cpu3 default-on transient` 

#### Temporary configuration

Replace `_TRIGGER_` with one of the available triggers. This setting will apply instantly, but be lost upon reboot.

 `# echo _TRIGGER_ > /sys/class/leds/led1/trigger` 

#### Permanent configuration

Replace `_TRIGGER_` with one of the available triggers. This setting will apply upon reboot.

 `/etc/tmpfiles.d/leds.conf`  `w /sys/class/leds/led1/trigger - - - - _TRIGGER_` 

## CPU Fan

The optional CPU fan can be controlled via the `/sys/devices/platform/odroidu2-fan` interface.

### Fan Mode

 `# echo auto > /sys/devices/platform/odroidu2-fan/fan_mode`  `# echo manual > /sys/devices/platform/odroidu2-fan/fan_mode` 

### Fan Speed (Manual Only)

Values range from 0 (0%) to 255 (100%)

 `# echo 0 > /sys/devices/platform/odroidu2-fan/pwm_duty`  `# echo 255 > /sys/devices/platform/odroidu2-fan/pwm_duty` 

### Read CPU Temperature

 `awk '{printf "%3.1f°C\n", $1/1000}' /sys/class/thermal/thermal_zone0/temp` 

## See also

*   [[1]](http://archlinuxarm.org/platforms/armv7/samsung/odroid-u3) - ODROID-U3 Arch Linux ARM Page
*   [[2]](http://www.hardkernel.com/main/products/prdt_info.php?g_code=g138745696275) - ODROID-U3 Hardkernel Product Page

Retrieved from "[https://wiki.archlinux.org/index.php?title=ODROID-U3&oldid=370330](https://wiki.archlinux.org/index.php?title=ODROID-U3&oldid=370330)"