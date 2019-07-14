Related articles

*   [Securely wipe disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk")

hdparm is a command line utility to set and view hardware parameters of [hard disk drives](https://en.wikipedia.org/wiki/Hard_disk_drive "wikipedia:Hard disk drive"). It can also be used as a simple [benchmarking](/index.php/Benchmarking "Benchmarking") tool.

**Warning:** Changing drive's default parameters can freeze the system or even irreversibly damage the drive.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Disk info](#Disk_info)
    *   [2.2 Benchmarking](#Benchmarking)
    *   [2.3 Power management configuration](#Power_management_configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Querying the status of the disk without waking it up](#Querying_the_status_of_the_disk_without_waking_it_up)
    *   [3.2 Persistent configuration using udev rule](#Persistent_configuration_using_udev_rule)
    *   [3.3 Reapplying configuration after wakeup](#Reapplying_configuration_after_wakeup)
    *   [3.4 Putting a drive to sleep directly after boot](#Putting_a_drive_to_sleep_directly_after_boot)
    *   [3.5 Working with unsupported hardware](#Working_with_unsupported_hardware)
    *   [3.6 Power management for Western Digital Green drives](#Power_management_for_Western_Digital_Green_drives)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 APM level reset after suspend](#APM_level_reset_after_suspend)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [hdparm](https://www.archlinux.org/packages/?name=hdparm) package. For use with SCSI devices, install the [sdparm](https://www.archlinux.org/packages/?name=sdparm) package.

## Usage

### Disk info

To get information about hard disks, run the following:

```
# hdparm -I /dev/sda

```

### Benchmarking

hdparm can be used for [Benchmarking#hdparm](/index.php/Benchmarking#hdparm "Benchmarking").

### Power management configuration

Modern hard drives support numerous power management features, the most common ones are summarized in the following table. See [hdparm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hdparm.8) for the complete list.

**Warning:** Overly aggressive power management can reduce the lifespan of hard drives due to frequent parking and spindowns.

| Parameter | Description |
| `-B` | Set the [Advanced Power Management](https://en.wikipedia.org/wiki/Advanced_Power_Management "wikipedia:Advanced Power Management") feature. Possible values are between 1 and 255, low values mean more aggressive power management and higher values mean better performance. Values from 1 to 127 permit spin-down, whereas values from 128 to 254 do not. A value of 255 completely disables the feature. |
| `-S` | Set the standby (spindown) timeout for the drive. The timeout specifies how long to wait in idle (with no disk activity) before turning off the motor to save power. The value of 0 disables spindown, the values from 1 to 240 specify multiples of 5 seconds and values from 241 to 251 specify multiples of 30 minutes. |
| `-M` | Set the [Automatic Acoustic Management](https://en.wikipedia.org/wiki/Automatic_Acoustic_Management "wikipedia:Automatic Acoustic Management") feature. Most modern hard disk drives have the ability to speed down the head movements to reduce their noise output. The possible value depends on the disk, some disks may not support this feature. |

To query current value, pass the parameter without a value. For example:

```
# hdparm -B /dev/sda

```

To apply different value, for example set APM to 127:

```
# hdparm -B 127 /dev/sda

```

## Tips and tricks

### Querying the status of the disk without waking it up

Invoking hdparm with the query option is known to wake-up some drives. In this case, consider `smartctl` provided by [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) to query the device which will not wake up a sleeping disk. For example:

 `# smartctl -i -n standby /dev/sda` 
```
smartctl 6.5 2016-05-07 r4318 [x86_64-linux-4.10.13-1-ARCH] (local build)
Copyright (C) 2002-16, Bruce Allen, Christian Franke, www.smartmontools.org

Device is in STANDBY mode, exit(2)

```

### Persistent configuration using udev rule

To make the setting persistent across reboot, one can use a [udev](/index.php/Udev "Udev") rule:

 `/etc/udev/rules.d/69-hdparm.rules`  `ACTION=="add", SUBSYSTEM=="block", KERNEL=="sda", RUN+="/usr/bin/hdparm -B 254 -S 0 /dev/sda"` 

Because a disk device can be assigned randomly to a changing `/dev/sd*X*`, the disk can also be identified by its serial as explained in [Udev#Identifying a disk by its serial](/index.php/Udev#Identifying_a_disk_by_its_serial "Udev").

Systems with multiple hard drives can apply the rule in a flexible way according to some criteria. For example, to apply power-saving settings to all rotational drives (hard disk with rotational head, excluding in particular [solid state drives](/index.php/Solid_state_drive "Solid state drive")), use the following rule:

 `/etc/udev/rules.d/69-hdparm.rules`  `ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", RUN+="/usr/bin/hdparm -B 127 /dev/%k"` 

### Reapplying configuration after wakeup

If the configuration is lost after system suspension/hibernation, it can be reapplied using [systemd-sleep](/index.php/Power_management#Hooks_in_/usr/lib/systemd/system-sleep "Power management").

Put a script into `/usr/lib/systemd/system-sleep` and make it executable:

 `/usr/lib/systemd/system-sleep/hdparm` 
```
#!/bin/sh

case $1 in post)
        /usr/bin/hdparm -B 254 -S 0 /dev/sda
        ;;
esac
```

### Putting a drive to sleep directly after boot

A device which is rarely needed can be put to sleep directly at the end of the boot process. This does not work with the above udev rule because it happens too early. In order to issue the command when the boot is completed, just create a [systemd](/index.php/Systemd "Systemd") service and [enable](/index.php/Enable "Enable") it:

 `/etc/systemd/system/hdparm.service` 
```
[Unit]
Description=hdparm sleep

[Service]
Type=oneshot
ExecStart=/usr/bin/hdparm -q -S 120 -y /dev/sdb

[Install]
WantedBy=multi-user.target
```

### Working with unsupported hardware

Some drives do not support spin down via hdparm. A diagnostic error message similar to the following is a good indication this is the case:

 `# hdparm -S 240 /dev/sda` 
```
/dev/sda:
setting standby to 240 (20 minutes)
HDIO_DRIVE_CMD(setidle) failed: Invalid argument

```

For some other drives, the hdparm command is acknowledged but the drive do not respect the parameters (either APM or spin down timer). This was observed with a Toshiba P300 (model HDWD120) HDD.

Such drives can be spun down using [hd-idle](https://www.archlinux.org/packages/?name=hd-idle) which ships with a [systemd](/index.php/Systemd "Systemd") service. One need to edit `/etc/conf.d/hd-idle` and the `HD_IDLE_OPTS` value, then [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `hd-idle.service`.

Example using a 10 min idle time for `/dev/sda` and a 1 min idle time for `/dev/disk/by-uuid/01CF0AC9AA5EAF70`:

```
HD_IDLE_OPTS="-i 0 -a /dev/sda -i 600 -a /dev/disk/by-uuid/01CF0AC9AA5EAF70 -i 60"

```

the leading `-i 0` parameter indicates that hd-idle is disabled on other drives.

### Power management for Western Digital Green drives

*Western Digital Green* hard drives have a special *idle3* timer which controls how long the drive waits before positioning its heads in their park position and entering a low power consumption state. The factory default is aggressively set to 8 seconds, which can result in thousands of head load/unload cycles in a short period of time and eventually premature failure, not to mention the performance impact of the drive often having to wake-up before doing routine I/O. Western Digital issued a [statement](http://wdc.custhelp.com/app/answers/detail/a_id/5357), claiming that Linux is not optimized for low power storage devices and advising to reduce logging frequency. There are different ways to amend the *idle3* state:

1.  Western Digital supplies a DOS utility *wdidle3.exe* for [download](https://support.wdc.com/downloads.aspx?p=113) for tweaking this setting. This utility is designed to upgrade only the firmware of the following hard drives: WD1000FYPS, WD7500AYPS, WD7501AYPS but is known to be able to change the *idle3* timer of other Green models as well.
2.  hdparm features a reverse-engineered implementation behind the `-J` flag, which is not as complete as the original official program, even though it seems to work on at least a few drives. A setting of 30 seconds is recommended for Linux use. Specify a value of zero (0) to disable the WD idle3 timer completely (NOT RECOMMENDED!): `# hdparm -J 30 --please-destroy-my-drive /dev/sda` See [#Persistent configuration using udev rule](#Persistent_configuration_using_udev_rule) to automatically use this parameter on supported hard drives.
3.  Another unofficial utility is provided by the [idle3-tools](https://www.archlinux.org/packages/?name=idle3-tools) package. A raw `*idle3*` value is passed as a parameter of the *idle3ctl* command. The correspondence between this value and the timeout in seconds is provided in the bottom table within [idle3ctl(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/idle3ctl.8). The following command sets the timer to 5 min: `# idle3ctl -s 138 /dev/sdc` this one completely disables the timer: `# idle3ctl -d /dev/sdc` 

**Note:**

*   A full power cycle is required for any change to take effect regardless of which program above is used. It means the drive needs to be powered OFF and then ON, a simple reboot does not suffice.
*   Some Western Digital Green drives are also known to have a different interpretation of hparm's standby timeout parameter, `-S 1` resulting in a 10 min timer rather than 5 sec.
*   The power consumption of a Green drive is typically around 5.3W during read/write, 4.7W in idle mode and 0.7W in standby mode.

## Troubleshooting

### APM level reset after suspend

The APM level may get reset after a suspend requiring it to be re-executed after each resume. This can be automated with the following [systemd](/index.php/Systemd "Systemd") unit (adapted from a [forum thread](https://bbs.archlinux.org/viewtopic.php?id=151640)):

 `/etc/systemd/system/apm.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target hybrid-sleep.target hibernate.target

[Service]
Type=simple
ExecStart=/usr/bin/hdparm -B 254 /dev/sda

[Install]
WantedBy=sleep.target
```

**Note:** The `sleep.target` is pulled by all `suspend`, `hybrid-sleep` and `hibernate` targets, but it finishes starting up *before* the system is suspended, so the three targets have to be specified explicitly. See [[1]](https://wiki.archlinux.org/index.php?title=Talk:Hdparm&oldid=440457#Troubleshooting_APM_settings_after_suspend.2C_hibernate_or_hybrid-sleep).

Alternatively, create a [hook in /usr/lib/systemd/system-sleep](/index.php/Power_management#Hooks_in_/usr/lib/systemd/system-sleep "Power management").

## See also

*   [https://sourceforge.net/projects/hdparm/](https://sourceforge.net/projects/hdparm/) - hdparm on SourceForge