# hdparm

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Securely_wipe_disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk")

hdparm is a command line utility to set and view hardware parameters of [hard disk drives](https://en.wikipedia.org/wiki/Hard_disk_drive "wikipedia:Hard disk drive"). It can also be used as a simple [benchmarking](/index.php/Benchmarking "Benchmarking") tool.

**Warning:** Be careful, changing default parameters can damage the drive or freeze the system.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Disk info](#Disk_info)
    *   [2.2 Benchmarking](#Benchmarking)
        *   [2.2.1 Reading speed](#Reading_speed)
        *   [2.2.2 Writing speed](#Writing_speed)
    *   [2.3 Power management configuration](#Power_management_configuration)
        *   [2.3.1 Persistent configuration using udev rule](#Persistent_configuration_using_udev_rule)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 KDE => 4.4.4 and hdparm](#KDE_.3D.3E_4.4.4_and_hdparm)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 APM level reset after suspend](#APM_level_reset_after_suspend)

## Installation

[hdparm](https://www.archlinux.org/packages/?name=hdparm) can be installed from the [official repositories](/index.php/Official_repositories "Official repositories"). For use with SCSI devices, install [sdparm](https://www.archlinux.org/packages/?name=sdparm).

## Usage

### Disk info

To get information about your hard disk, run the following:

```
# hdparm -I /dev/sda

```

### Benchmarking

#### Reading speed

To measure how many MB/s your hard disk (SATA/IDE) can read, run the following:

```
# hdparm -t --direct /dev/sda

```

#### Writing speed

To measure how many MB/s your hard disk (SATA/IDE) can write, run the following:

```
$ sync;time bash -c "(dd if=/dev/zero of=bf bs=8k count=500000; sync)"

```

Do not forget to `Ctrl+c` and `rm bf` after that.

**Note:** `bf` is just the name of the output file that `dd` writes to.

**Tip:** See [dd-benchmark](https://romanrm.net/dd-benchmark) for an explanation on the requirement to `sync` and further related `dd` options.

### Power management configuration

Modern hard drives support numerous power management features, the most common ones are summarized in the following table. See `hdparm(8)` for the complete list.

**Warning:** Too aggressive power management can reduce the lifespan of your hard drive due to frequent parking and spindowns.

<table class="wikitable">

<tbody>

<tr>

<th>Parameter</th>

<th>Description</th>

</tr>

<tr>

<td>`-B`</td>

<td>Set the [Advanced Power Management](https://en.wikipedia.org/wiki/Advanced_Power_Management "wikipedia:Advanced Power Management") feature. Possible values are between 1 and 255, low values mean more aggressive power management and higher values mean better performance. Values from 1 to 127 permit spin-down, whereas values from 128 to 254 do not. A value of 255 completely disables the feature.</td>

</tr>

<tr>

<td>`-S`</td>

<td>Set the standby (spindown) timeout for the drive. The timeout specifies how long to wait in idle (with no disk activity) before turning off the motor to save power. The value of 0 disables spindown, the values from 1 to 240 specify multiples of 5 seconds and values from 241 to 251 specify multiples of 30 minutes.</td>

</tr>

<tr>

<td>`-M`</td>

<td>Set the [Automatic Acoustic Management](https://en.wikipedia.org/wiki/Automatic_Acoustic_Management "wikipedia:Automatic Acoustic Management") feature. Most modern hard disk drives have the ability to speed down the head movements to reduce their noise output. The possible value depends on the disk, some disks may not support this feature.</td>

</tr>

</tbody>

</table>

To query current value, pass the parameter without a value. For example:

```
# hdparm -B /dev/sda

```

To apply different value, for example set APM to 127:

```
# hdparm -B 127 /dev/sda

```

#### Persistent configuration using udev rule

To make the setting persistent, adapt the following [udev](/index.php/Udev "Udev") rule for your values:

 `/etc/udev/rules.d/50-hdparm.rules` 

```
ACTION=="add", SUBSYSTEM=="block", KERNEL=="sda", RUN+="/usr/bin/hdparm -B 254 -S 0 /dev/sda"

```

If you have more than one hard drive you could make the rule more flexible. For example, to apply power-saving settings for all external drives (assuming there is only one internal drive, `/dev/sda`):

 `/etc/udev/rules.d/50-hdparm.rules` 

```
ACTION=="add|change", KERNEL=="sd[b-z]", ATTR{queue/rotational}=="1", RUN+="/usr/bin/hdparm -B 127 -S 12 /dev/%k"

```

## Tips and tricks

### KDE => 4.4.4 and hdparm

To stop [KDE](/index.php/KDE "KDE") version 4.4.4 or greater from messing around with your (manually) configured hdparm values, enter the following and you should be done:

```
# touch /etc/pm/power.d/harddrive

```

## Troubleshooting

### APM level reset after suspend

The APM level may get reset after a suspend, so you will probably also have to re-execute the command after each resume. This can be automated with the following [systemd](/index.php/Systemd "Systemd") unit: (adapted from a [forum thread](https://bbs.archlinux.org/viewtopic.php?id=151640))

```
[Unit]
Description=Local system resume actions
After=sleep.target

[Service]
Type=simple
ExecStart=/usr/bin/hdparm -B 254 /dev/sda

[Install]
WantedBy=sleep.target

```

Or you could create `/usr/lib/systemd/system-sleep/hdparm_set`: [found here](https://bbs.archlinux.org/viewtopic.php?id=159233)

```
#!/bin/sh
hdparm -B 254 /dev/sda

```

And make it executable:

```
chmod +x /usr/lib/systemd/system-sleep/hdparm_set

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hdparm&oldid=365636](https://wiki.archlinux.org/index.php?title=Hdparm&oldid=365636)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")
*   [Storage](/index.php/Category:Storage "Category:Storage")