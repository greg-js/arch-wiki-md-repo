Related articles

*   [acpid](/index.php/Acpid "Acpid")
*   [systemd](/index.php/Systemd "Systemd")
*   [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")
*   [Laptop](/index.php/Laptop "Laptop")
*   [Powertop](/index.php/Powertop "Powertop")
*   [TLP](/index.php/TLP "TLP")

[Laptop Mode Tools](https://github.com/rickysarraf/laptop-mode-tools) is a laptop power saving package for Linux systems. It is the primary way to enable the Laptop Mode feature of the Linux kernel, which lets your hard drive spin down. In addition, it allows you to tweak a number of other power-related settings using a simple configuration file.

Combined with [acpid](/index.php/Acpid "Acpid") and [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling"), LMT provides most users with a complete notebook power management suite.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Hard disks](#Hard_disks)
        *   [2.1.1 Solid state drives](#Solid_state_drives)
    *   [2.2 CPU frequency](#CPU_frequency)
    *   [2.3 Device and bus](#Device_and_bus)
        *   [2.3.1 Intel SATA](#Intel_SATA)
        *   [2.3.2 USB autosuspend](#USB_autosuspend)
    *   [2.4 Display and graphics](#Display_and_graphics)
        *   [2.4.1 LCD brightness](#LCD_brightness)
            *   [2.4.1.1 ThinkPad T40/T42](#ThinkPad_T40/T42)
            *   [2.4.1.2 ThinkPad T60](#ThinkPad_T60)
        *   [2.4.2 Terminal blanking](#Terminal_blanking)
    *   [2.5 Networking](#Networking)
        *   [2.5.1 Ethernet](#Ethernet)
        *   [2.5.2 Wireless LAN](#Wireless_LAN)
    *   [2.6 Audio](#Audio)
        *   [2.6.1 AC97](#AC97)
        *   [2.6.2 Intel HDA](#Intel_HDA)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Laptop-mode-tools is not picking up events](#Laptop-mode-tools_is_not_picking_up_events)
    *   [3.2 USB Mouse sleeping after 5 seconds when on battery](#USB_Mouse_sleeping_after_5_seconds_when_on_battery)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/) package or the [laptop-mode-tools-git](https://aur.archlinux.org/packages/laptop-mode-tools-git/) package.

## Configuration

Configuration is handled through:

*   `/etc/laptop-mode/laptop-mode.conf` - primary configuration file.
*   `/etc/laptop-mode/conf.d/*` - dozens of feature-specific "modules".

Each module can be explicitly `enabled`, `disabled`, or set to `auto` by changing the `CONTROL_*` argument of any file in `conf.d/`. LMT will attempt enable any modules where `CONTROL_*` is set to `auto` if `ENABLE_AUTO_MODULES` is set in `/etc/laptop-mode/laptop-mode.conf`. There are two exceptions to the above rule: `auto-hibernate.conf` and `battery-level-polling.conf` use an `ENABLE_*` variable instead of `CONTROL_*`.

To quickly check which modules are enabled, disabled or auto, run:

```
$ grep -r '^\(CONTROL\|ENABLE\)_' /etc/laptop-mode/conf.d

```

Finally, [enable](/index.php/Enable "Enable") `laptop-mode.service`.

### Hard disks

For this you need to have *hdparm* and/or *sdparm* installed. See [Hdparm](/index.php/Hdparm "Hdparm").

Spinning down the hard drive through `hdparm -S` values saves power and makes everything a lot more quiet. By using the readahead function you can allow the drives to spin down more often even though you are using the computer. LMT can also establish `hdparm -B` values. The maximum hard drive power saving is 1 and the minimum is 254\. For example, set this value to 254 when on AC and 20 when on battery. If you find that normal activity hangs often while waiting for the disk to spin up, it might be a good idea to set it to a higher value (e.g. 128) which will make it spin down less often. `hdparm -S` and `hdparm -B` values are configured in `/etc/laptop-mode/laptop-mode.conf`.

**Warning:** Spinning down a hard drive too frequently can shorten its lifespan. Take care when choosing a proper value.

With the `CONTROL_MOUNT_OPTIONS` variable (default on), laptop-mode-tools automatically remounts your partitions, appending `commit=600,noatime` in the mount options. This keeps the journaling program jbd2 from accessing your disk every few seconds, instead the disk journal gets updated every 10 minutes.

**Warning:** With this setting you could lose up to 10 minutes of work. Also be sure not to use the `atime` mount option. Use `noatime` or `relatime` instead.

**Note:** `CONTROL_MOUNT_OPTIONS` should not be turned on with nilfs2 partitions. Refer to this thread on the forum: [https://bbs.archlinux.org/viewtopic.php?id=134656](https://bbs.archlinux.org/viewtopic.php?id=134656)

#### Solid state drives

From the [official, upstream FAQ](https://github.com/rickysarraf/laptop-mode-tools/wiki/FAQ#i-have-a-solid-state-disk-ssd-in-my-machine-should-i-enable-any-of-the-disk-related-parts-of-laptop-mode-tools-or-are-they-irrelevant):

**Question:** I have a solid-state disk (SSD) in my machine. Should I enable any of the disk-related parts of laptop-mode-tools, or are they irrelevant?

**Answer:** They may be relevant, because (a) laptop mode will reduce the number of writes, which improves the lifetime of an SSD, and (b) laptop mode makes writes bursty, which enables power saving mechanisms like ALPM to kick in. However, your mileage may vary depending on the specific hardware involved. For some hardware, you will get no gain at all, for some the gain may be substantial.

### CPU frequency

For this you need to have a CPU frequency driver installed. See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

```
# cpufreq.conf
# ThinkPad T40/T42/T60 Example
#
CONTROL_CPU_FREQUENCY=1
BATT_CPU_MAXFREQ=fastest
BATT_CPU_MINFREQ=slowest
BATT_CPU_GOVERNOR=ondemand
BATT_CPU_IGNORE_NICE_LOAD=1
LM_AC_CPU_MAXFREQ=fastest
LM_AC_CPU_MINFREQ=slowest
LM_AC_CPU_GOVERNOR=ondemand
LM_AC_CPU_IGNORE_NICE_LOAD=1
NOLM_AC_CPU_MAXFREQ=fastest
NOLM_AC_CPU_MINFREQ=slowest
NOLM_AC_CPU_GOVERNOR=ondemand
NOLM_AC_CPU_IGNORE_NICE_LOAD=0
CONTROL_CPU_THROTTLING=0

```

### Device and bus

#### Intel SATA

*   Enable the Intel SATA AHCI controller Aggressive Link Power Management feature to set the disk link into a very low power mode in the absence of disk IO.

```
# intel-sata-powermgmt.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_INTEL_SATA_POWER=1
BATT_ACTIVATE_SATA_POWER=1
LM_AC_ACTIVATE_SATA_POWER=1
NOLM_AC_ACTIVATE_SATA_POWER=0

```

**Note:** Review the well-documented `/etc/laptop-mode/conf.d/intel-sata-powermgmt.conf` file for additional configuration details.

#### USB autosuspend

**Tip:** USB autosuspend functionality has been moved from the *usb-autosuspend* module to the *runtime-pm* module. Make sure to replace usb-autosuspend with runtime-pm on /lib/udev/rules.d/99-laptop-mode.rules.

```
# runtime-pm.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_RUNTIME_AUTOSUSPEND=1
BATT_SUSPEND_RUNTIME=1
LM_AC_SUSPEND_RUNTIME=1
NOLM_AC_SUSPEND_RUNTIME=1
AUTOSUSPEND_TIMEOUT=2

```

**Note:** Review the `/etc/laptop-mode/conf.d/runtime-pm.conf` file for additional configuration details. If you have an USB tool you always use (like an USB mouse), blacklisting them would stop them from suspending.

### Display and graphics

#### LCD brightness

*   Available brightness values for certain laptops can be obtained by running following command:

```
$ cat /proc/acpi/video/VID/LCD/brightness

```

##### ThinkPad T40/T42

For [ThinkPad](https://en.wikipedia.org/wiki/ThinkPad "wikipedia:ThinkPad") T40/T42 notebooks, minimum and maximum brightness values can be obtained by running:

```
$ cat /sys/class/backlight/acpi_video0/brightness
$ cat /sys/class/backlight/acpi_video0/max_brightness

```

```
# lcd-brightness.conf
# ThinkPad T40/T42 Example
#
DEBUG=0
CONTROL_BRIGHTNESS=1
BATT_BRIGHTNESS_COMMAND="echo 0"
LM_AC_BRIGHTNESS_COMMAND="echo 7"
NOLM_AC_BRIGHTNESS_COMMAND="echo 7"
BRIGHTNESS_OUTPUT="/sys/class/backlight/thinkpad_screen/brightness"

```

##### ThinkPad T60

*   For [ThinkPad](https://en.wikipedia.org/wiki/ThinkPad "wikipedia:ThinkPad") T60 notebooks, minimum and maximum brightness values can be obtained by running:

```
$ cat /sys/class/backlight/thinkpad_screen/max_brightness
$ cat /sys/class/backlight/thinkpad_screen/brightness

```

```
# lcd-brightness.conf
# ThinkPad T60 Example
#
DEBUG=0
CONTROL_BRIGHTNESS=1
BATT_BRIGHTNESS_COMMAND="echo 0"
LM_AC_BRIGHTNESS_COMMAND="echo 7"
NOLM_AC_BRIGHTNESS_COMMAND="echo 7"
BRIGHTNESS_OUTPUT="/sys/class/backlight/acpi_video0/brightness"

```

**Note:** Review the well-documented `/etc/laptop-mode/conf.d/lcd-brightness.conf` file for additional configuration details.

#### Terminal blanking

```
# terminal-blanking.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_TERMINAL=1
TERMINALS="/dev/tty1"
BATT_TERMINAL_BLANK_MINUTES=1
BATT_TERMINAL_POWERDOWN_MINUTES=2
LM_AC_TERMINAL_BLANK_MINUTES=10
LM_AC_TERMINAL_POWERDOWN_MINUTES=10
NOLM_AC_TERMINAL_BLANK_MINUTES=10
NOLM_AC_TERMINAL_POWERDOWN_MINUTES=10

```

**Note:** Review the well-documented `/etc/laptop-mode/conf.d/terminal-blanking.conf` file for additional configuration details.

### Networking

#### Ethernet

```
# ethernet.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_ETHERNET=1
LM_AC_THROTTLE_ETHERNET=0
NOLM_AC_THROTTLE_ETHERNET=0
DISABLE_WAKEUP_ON_LAN=1
DISABLE_ETHERNET_ON_BATTERY=1
ETHERNET_DEVICES="eth0"

```

#### Wireless LAN

Wireless interface power management settings are hardware-dependent, and thus a bit trickier to configure. Depending on the wireless chipset, the settings are managed in one of the following three files:

1.  `/etc/laptop-mode/conf.d/wireless-power.conf` for a generic method of saving power (using "iwconfig wlan0 power on/off"). This applies to most chipsets (that is, anything but Intel chipsets listed below).
2.  `/etc/laptop-mode/conf.d/wireless-ipw-power.conf` for Intel chipsets driven by the old ipw driver. This apply to IPW3945, IPW2200 and IPW2100\. It currently (as of LMT 1.55-1) uses iwpriv for IPW3945, and a combination of iwconfig and iwpriv settings for IPW2100 and IPW220\. See `/usr/share/laptop-mode-tools/modules/wireless-ipw-power` for details. (note that the ipw3945 is not used anymore, see below)
3.  `/etc/laptop-mode/conf.d/wireless-iwl-power.conf` for Intel chipsets driven by modules iwl4965, iwl3945 and iwlagn (this latter supports chipsets 4965, 5100, 5300, 5350, 5150, 1000, and 6000)

Note that activating the three of them should not be much of a problem, since LMT detects the module used by the interface and acts accordingly.

The supported modules for each configuration file, indicated above, are taken directly from LMT. However, this seems to be a bit out-of-date, since the current 2.6.34 kernel does not provide the ipw3945 and iwl4965 modules anymore (3945 chipset uses iwl3945 instead, and 4965 uses the generic module iwlagn). This is only brought here for information, as this does not (or should not) affect the way LMT works.

There is a known issue with some chipsets running with the iwlagn module (namely, the 5300 chipset, and maybe others). On those chipsets, the following settings of `/etc/laptop-mode/conf.d/wireless-iwl-power.conf`:

```
IWL_AC_POWER
IWL_BATT_POWER

```

are ignored, because the `/sys/class/net/wlan*/device/power_level` file does not exist. Instead, the standard method (with "iwconfig wlan0 power on/off") is automatically used.

### Audio

#### AC97

```
# ac97-powersave.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_AC97_POWER=1

```

#### Intel HDA

```
# intel-hda-powersave.conf
# ThinkPad T40/T42/T60 Example
#
DEBUG=0
CONTROL_INTEL_HDA_POWER=1
BATT_INTEL_HDA_POWERSAVE=1
LM_AC_INTEL_HDA_POWERSAVE=1
NOLM_AC_INTEL_HDA_POWERSAVE=0
INTEL_HDA_DEVICE_TIMEOUT=10
INTEL_HDA_DEVICE_CONTROLLER=0

```

## Troubleshooting

### Laptop-mode-tools is not picking up events

Install [acpid](https://www.archlinux.org/packages/?name=acpid) and enable its [systemd](/index.php/Systemd "Systemd") service `acpid.service`.

If that does not help, go through the laptop-mode configuration files and make sure that the service you want to enable is set to 1\. Many services (including cpufreq control) are by default set to "auto", which may not enable them.

I have experienced issues with bluetooth not working if I boot up with battery, and I fixed it with disabling runtime-pm.

### USB Mouse sleeping after 5 seconds when on battery

First find the ID of you device (it should look like `046d:c534`):

```
$ lsusb

```

Put this value into the `AUTOSUSPEND_DEVID_BLACKLIST` variable in `/etc/laptop-mode/conf.d/runtime-pm.conf`, for example:

 `/etc/laptop-mode/conf.d/runtime-pm.conf` 
```
...
AUTOSUSPEND_DEVID_BLACKLIST="046d:c534"
...
```

Multiple IDs can be seperated with spaces.

**Note:** Don't forget to [restart](/index.php/Restart "Restart") the laptop-mode service. You might also need to reconnect the USB device.

## See also

*   [Laptop Mode Tools wiki](https://github.com/rickysarraf/laptop-mode-tools/wiki)
*   [FAQ](https://github.com/rickysarraf/laptop-mode-tools/wiki/FAQ)
*   [Mailing List](https://groups.google.com/forum/#!forum/laptop-mode-tools)