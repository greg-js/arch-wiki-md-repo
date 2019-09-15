*tp_smapi* is a set of kernel modules that retrieves information from and conveys commands to the hardware of many ThinkPad laptops before [Ivy Bridge processors](#Supported_laptops).

This information is presented through the `/sys/devices/platform/smapi` filesystem. Much like the `/proc` filesystem, you can read and write information to these files to get information about and send commands to the hardware. tp_smapi is highly recommended if you're using a supported ThinkPad laptop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Supported laptops](#Supported_laptops)
*   [2 Installation](#Installation)
*   [3 Features](#Features)
    *   [3.1 Control battery charging](#Control_battery_charging)
        *   [3.1.1 General way](#General_way)
        *   [3.1.2 Check whether settings were accepted](#Check_whether_settings_were_accepted)
    *   [3.2 Protect the hard disk from drops](#Protect_the_hard_disk_from_drops)
*   [4 Workaround for partially supported laptops](#Workaround_for_partially_supported_laptops)
    *   [4.1 1st option, custom script](#1st_option,_custom_script)
    *   [4.2 2nd option, tpacpi-bat](#2nd_option,_tpacpi-bat)
    *   [4.3 3rd option, in kernel](#3rd_option,_in_kernel)
*   [5 See also](#See_also)

## Supported laptops

First check whether your laptop is supported. Thinkwiki has a comprehensive [list of all supported Thinkpads.](http://www.thinkwiki.org/wiki/Tp_smapi#Model-specific_status) In case your TP does not support stop_threshold but only start_threshold please go here [#Workaround for partially supported laptops](#Workaround_for_partially_supported_laptops) for a decent workaround.

If you are installing on a recent Thinkpad that has an Ivy Bridge processor or later (any of the `*30`, `*40` or `*50` models), tp_smapi will not work. Use [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) or [tpacpi-bat-git](https://aur.archlinux.org/packages/tpacpi-bat-git/).

## Installation

[Install](/index.php/Install "Install") the [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) package. For the custom [linux-ck](/index.php/Linux-ck "Linux-ck") kernel there is [tp_smapi-ck](https://aur.archlinux.org/packages/tp_smapi-ck/) in the [AUR](/index.php/AUR "AUR").

It provides you 3 [Kernel modules](/index.php/Kernel_modules "Kernel modules"):

| tp_smapi | ThinkPad SMAPI Support |
| hdaps | IBM Hard Drive Active Protection System ([HDAPS](/index.php/HDAPS "HDAPS")) driver |
| thinkpad_ec | ThinkPad embedded controller hardware access (tp_smapi and hdaps both depend on it) |

After a reboot, tp_smapi and its dependencies will get autoloaded and the sysfs-interface under `/sys/devices/platform/smapi` should be fully functional.

## Features

Here are a couple of useful things you can do using tp_smapi.

### Control battery charging

It's bad for most laptop batteries to hold a full charge for long periods of time. [[1]](http://www.thinkwiki.org/wiki/Maintenance#Battery_treatment) You should try to keep your battery in the 40-80% charged range, unless you need the battery life for extended periods of time.

#### General way

tp_smapi lets you control the start and stop charging threshold to do just that. Run these commands to set these to good values:

```
echo 40 > /sys/devices/platform/smapi/BAT0/start_charge_thresh
echo 80 > /sys/devices/platform/smapi/BAT0/stop_charge_thresh

```

This will cause the battery to begin charging when it falls below 40% charge and stop charging once it exceeds 80% charge. This will extend the lifetime of your battery.

Note that when you remove and re-insert the battery, these thresholds may be reset to their default values. To work around this, create a script to set these values, and make this script run both at startup and when a battery is inserted. More specific instructions follow.

Create a script `/usr/sbin/set_battery_thresholds`:

```
#!/bin/sh
# set the battery charging thresholds to extend battery lifespan
echo ${2:-40} > /sys/devices/platform/smapi/BAT${1:-0}/start_charge_thresh
echo ${3:-80} > /sys/devices/platform/smapi/BAT${1:-0}/stop_charge_thresh

```

Make it [executable](/index.php/Executable "Executable"). With this script to set a battery threshold is very simple, just type (if set_bat_thresh is the name of the script):

```
set_battery_thresholds 0 96 100

```

Or run it with no arguments to default to BAT0, and thresholds of 40% and 80%.

Let [systemd](/index.php/Systemd "Systemd") execute the script at startup (Using rc.local from initscripts is deprecated). Thus, create `/etc/systemd/system/tp_smapi_set_battery_thresholds.service`:

```
[Unit]
Description=Set Battery Charge Thresholds by tp_smapi

[Service]
Type=oneshot
ExecStart=/usr/sbin/set_battery_thresholds
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Enable it in systemd:

```
# systemctl enable tp_smapi_set_battery_thresholds.service

```

You can also make it run when a battery is inserted. This requires that [acpid](/index.php/Acpid "Acpid") is installed and running. Edit `/etc/acpi/handler.sh`:

```
#... other ACPI stuff
battery)
  case "$2" in
    BAT0)
      case "$4" in
        00000000)
        ;;
        00000001)
        **/usr/sbin/set_battery_thresholds**
        ;;
#... more ACPI stuff

```

#### Check whether settings were accepted

To check whether your settings were accepted check the output of the following:

```
cat /sys/devices/platform/smapi/BAT0/start_charge_thresh
cat /sys/devices/platform/smapi/BAT0/stop_charge_thresh

```

### Protect the hard disk from drops

tp_smapi includes a driver to read the accelerometer in your laptop to detect drops and other events that could cause damage to your hard drive. See the [HDAPS](/index.php/HDAPS "HDAPS") page for more information on this useful feature.

## Workaround for partially supported laptops

For partially supported laptops you can still gain control over your battery. First check what is actually supported:

```
cat /sys/devices/platform/smapi/BAT0/start_charge_thresh
cat /sys/devices/platform/smapi/BAT0/stop_charge_thresh

```

If start-charge_thresh is supported but not stop_charge_thresh but you still want to have your computer stop charging your battery you might have other options.

Note: None of the first two options works on T42p. The third one works on E540.

### 1st option, custom script

*   create the script `/usr/sbin/set_battery_thresholds` as above
*   copy the original `/etc/acpi/handler.sh` to `/etc/acpi/handler.sh.start`
*   edit `/etc/acpi/handler.sh` as above and copy it to `/etc/acpi/handler.sh.stop`

Now copy the following script, make it executable, adjust the values to your liking and run it every couple of minutes as a root cron.

```
#!/bin/bash

CURRENTCHARGE=$(acpitool -b | cut -d, -f2 | cut -d. -f1 | cut -b2-)

if [ $CURRENTCHARGE -gt 80 ]; then
    cp /etc/acpi/handler.sh.stop /etc/acpi/handler.sh
    echo 99 > /sys/devices/platform/smapi/BAT0/start_charge_thresh
    exit 0
fi
if [ $CURRENTCHARGE -lt 60 ]; then
    cp /etc/acpi/handler.sh.start /etc/acpi/handler.sh    
      echo 0 > /sys/devices/platform/smapi/BAT0/start_charge_thresh
    exit 0 
fi

exit 0

```

### 2nd option, tpacpi-bat

To control the battery charging thresholds, install the Perl script [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) or [tpacpi-bat-git](https://aur.archlinux.org/packages/tpacpi-bat-git/) from the AUR.

Manually set the thresholds by calling

```
tpacpi-bat -v -s startThreshold 0 40
tpacpi-bat -v -s stopThreshold 0 80

```

The example values 40 and 80 given here are in percent of the full battery capacity. Adjust them to your own needs. You may also want to add these lines to /etc/rc.local to set the at startup.

The manual setting of thresholds via the command `tpacpi-bat` is not permanent. To set the thresholds permanently, edit the start and end thresholds accordingly in `/etc/conf.d/tpacpi`.

**Note:** See tpacpi-bat help for the list of commands: `perl /usr/lib/perl5/vendor_perl/tpacpi-bat -h`.

### 3rd option, in kernel

Kernel 4.17 added the option to adjust battery charging thresholds for ThinkPads directly.

```
echo 60 > /sys/class/power_supply/BAT0/charge_stop_threshold
echo 40 > /sys/class/power_supply/BAT0/charge_start_threshold

```

Note that if you try to display the values, you'll get only the last one set (start in the example), with 128 added to it. This is a known issue, but the true value is really set, as you can see from battery behaviour. Other interesting parameters can be found under `/sys/class/power_supply/BAT0/`.

## See also

*   [tp_smapi on ThinkWiki](http://www.thinkwiki.org/wiki/Tp_smapi)