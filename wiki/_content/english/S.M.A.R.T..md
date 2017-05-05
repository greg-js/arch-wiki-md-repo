S.M.A.R.T. (Self-Monitoring, Analysis, and Reporting Technology) is a supplementary component built into many modern storage devices through which devices monitor, store, and analyze the health of their operation. Statistics are collected (temperature, number of reallocated sectors, seek errors...) which software can use to measure the health of a device, predict possible device failure, and provide notifications on unsafe values.

## Contents

*   [1 Smartmontools](#Smartmontools)
    *   [1.1 smartctl](#smartctl)
        *   [1.1.1 Run a test](#Run_a_test)
        *   [1.1.2 View test results](#View_test_results)
    *   [1.2 smartd](#smartd)
        *   [1.2.1 daemon management](#daemon_management)
        *   [1.2.2 Define the devices to monitor](#Define_the_devices_to_monitor)
        *   [1.2.3 Email potential problems](#Email_potential_problems)
        *   [1.2.4 Power management](#Power_management)
        *   [1.2.5 Schedule self-tests](#Schedule_self-tests)
        *   [1.2.6 Alert on temperature changes](#Alert_on_temperature_changes)
        *   [1.2.7 Complete smartd.conf example](#Complete_smartd.conf_example)
*   [2 GUI Applications](#GUI_Applications)
*   [3 See also](#See_also)

## Smartmontools

The smartmontools package contains two utility programs for analyzing and monitoring storage devices: `smartctl` and `smartd`. [Install](/index.php/Install "Install") the [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) package to use these tools.

SMART support must be available and enabled on each storage device to effectively use these tools. You can use [#smartctl](#smartctl) to check for and enable SMART support. That done, you can manually [#Run a test](#Run_a_test) and [#View test results](#View_test_results), or you can use [#smartd](#smartd) to automatically run tests and email notifications.

### smartctl

smartctl is a command-line tool that "controls the Self-Monitoring, Analysis and Reporting Technology (SMART) system built into most ATA/SATA and SCSI/SAS hard drives and solid-state drives."

The `-i`/`--info` option prints a variety of information about a device, including whether SMART is available and enabled:

```
# smartctl --info /dev/sda | grep 'SMART support is:'
SMART support is: Available - device has SMART capability.
SMART support is: Enabled

```

If SMART is available but not enabled, you can enable it:

```
# smartctl --smart=on /dev/<device>

```

You may need to specify a device type. For example, specifying `--device=ata` tells smartctl that the device type is ATA, and this prevents smartctl from issuing SCSI commands to that device.

#### Run a test

There are three types of self-tests that a device can execute (all are safe to user data):

*   Short (runs tests that have a high probability of detecting device problems)
*   Extended (or Long; a short check with complete disk surface examination)
*   Conveyance (identifies if damage incurred during transportation of the device)

The `-c`/`--capabilities` flag prints which tests a device supports and the approximate execution time of each test. For example:

```
# smartctl -c /dev/sda
[…]
Short self-test routine
recommended polling time:        (   1) minutes.
Extended self-test routine
recommended polling time:        (  74) minutes.
Conveyance self-test routine
recommended polling time:        (   2) minutes.
[…]

```

Use `-t`/`--test=<test_name>` flag to run a test:

```
# smartctl -t short /dev/<device>
# smartctl -t long /dev/<device>
# smartctl -t conveyance /dev/<device>

```

#### View test results

You can view a device's overall health with the `-H` flag. "If the device reports failing health status, this means either that the device has already failed, or that it is predicting its own failure within the next 24 hours. If this happens […] get your data off the disk and to someplace safe as soon as you can."

```
# smartctl -H /dev/<device>

```

You can also view a list of recent test results and detailed information about a device:

```
# smartctl -l selftest /dev/<device>
# smartctl -a /dev/<device>

```

### smartd

The smartd daemon monitors SMART statuses and emits notifications when something goes wrong. It can be managed with systemd and configured using the `/etc/smartd.conf` configuration file. The configuration file syntax is esoteric, and this wiki page provides only a quick reference. For more complete information, read the examples and comments within the configuration file, or read [smartd.conf(5)](https://www.smartmontools.org/browser/trunk/smartmontools/smartd.conf.5.in).

#### daemon management

To start the daemon, check its status, make it auto-start on system boot and read recent log file entries, simply [start/enable](/index.php/Start/enable "Start/enable") the `smartd.service` systemd unit.

smartd respects all the usual systemctl and journalctl commands. For more information on using systemctl and journalctl, see [Systemd#Using units](/index.php/Systemd#Using_units "Systemd") and [Systemd#Journal](/index.php/Systemd#Journal "Systemd").

#### Define the devices to monitor

To monitor for all possible SMART errors on all disks:

 `/etc/smartd.conf`  `DEVICESCAN -a` 

To monitor for all possible SMART errors on `/dev/sda` and `/dev/sdb`, and ignore all other devices:

 `/etc/smartd.conf` 
```
/dev/sda -a
/dev/sdb -a

```

To monitor for all possible SMART errors on externally connected disks (USB-backup disks spring to mind) it is prudent to tell SMARTd the UUID of the device since the /dev/sdX of the drive might change during a reboot.

First, you will have to get the UUID of the disk to monitor: `ls -lah /dev/disk/by-uuid/` now look for the disk you want to Monitor

 `ls -lah /dev/disk/by-uuid/` 
```
lrwxrwxrwx 1 root root   9 Nov  5 22:41 820cdd8a-866a-444d-833c-1edb0f4becac -> ../../sde
lrwxrwxrwx 1 root root  10 Nov  5 22:41 b51b87f3-425e-4fe7-883f-f4ff1689189e -> ../../sdf2
lrwxrwxrwx 1 root root   9 Nov  5 22:42 ea2199dd-8f9f-4065-a7ba-71bde11a462c -> ../../sda
lrwxrwxrwx 1 root root  10 Nov  5 22:41 fe9e886a-8031-439f-a909-ad06c494fadb -> ../../sdf1

```

I know that my USB disk attached to /dev/sde during boot. Now to tell SMARTd to monitor that disk simply use the `/dev/disk/by-uuid/` path.

 `/etc/smartd.conf` 
```
/dev/disk/by-uuid/820cdd8a-866a-444d-833c-1edb0f4becac -a

```

Now your USB disk will be monitored even if the /dev/sdX path changes during reboot.

#### Email potential problems

To have an email sent when a failure or new error occurs, use the `-m` option:

 `/etc/smartd.conf`  `DEVICESCAN -m address@domain.com` 

To be able to send the email externally (i.e. not to the root mail account) a MTA (Mail Transport Agent) or a MUA (Mail User Agent) will need to be installed and configured. Common MTAs are [Msmtp](/index.php/Msmtp "Msmtp") and [SSMTP](/index.php/SSMTP "SSMTP"). Common MTUs are sendmail and [Postfix](/index.php/Postfix "Postfix"). It is enough to simply configure [S-nail](/index.php/S-nail "S-nail") if you do not want anything else, but you will need to follow [these instructions](//dominicm.com/configure-email-notifications-on-arch-linux/).

The `-M test` option causes a test email to be sent each time the smartd daemon starts:

 `/etc/smartd.conf`  `DEVICESCAN -m address@domain.com -M test` 

E-Mail can take quite a long time to be delivered, but when your hard drive fails you want to be informed immediately to take the appropriate actions. Hence you should rather define a script to be executed instead of only emailing the problem:

 `/etc/smartd.conf`  `DEVICESCAN -m address@domain.com -M exec /usr/local/bin/smartdnotify` 

To send an e-mail and a system notification, put something like this into `/usr/local/bin/smartdnotify`:

```
#! /bin/sh

# Send mail
echo "$SMARTD_MESSAGE" | mail -s "$SMARTD_FAILTYPE" "$SMARTD_ADDRESS"

# Notify user
wall "$SMARTD_MESSAGE"

```

If you are running a desktop environment, you might also prefer having a popup to appear on your desktop. In this case, you can use this script (replace `*X_user*` and `*X_userid*` with the user and userid running X respectively) :

 `/usr/local/bin/smartdnotify` 
```
#!/bin/sh

sudo -u *X_user* DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/*X_userid*/bus notify-send "S.M.A.R.T Error ($SMARTD_FAILTYPE)" "$SMARTD_MESSAGE" --icon=dialog-warning
```

This requires [libnotify](https://www.archlinux.org/packages/?name=libnotify) and a compatible desktop environment. See [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications") for more details.

#### Power management

If you use a computer under control of power management, you should instruct smartd how to handle disks in low power mode. Usually, in response to SMART commands issued by smartd, the disk platters are spun up. So if this option is not used, then a disk which is in a low-power mode may be spun up and put into a higher-power mode when it is periodically polled by smartd.

 `/etc/smartd.conf`  `DEVICESCAN -n standby,15,q` 

More info on [smartmontools wiki](http://www.smartmontools.org/wiki/Powermode).

On some devices the -n does not work. You get the following error message in syslog:

 `journalctl -u smartd` 
```
CHECK POWER MODE: incomplete response, ATA output registers missing
Device: /dev/sdb [SAT], no ATA CHECK POWER STATUS support, ignoring -n Directive

```

As an alternative you can user -i option of smartd. It controls how often smartd spins the disks up to check their status. Default is 30 minutes. To change it create and edit `/etc/default/smartmontools`.

 `/etc/default/smartmontools`  `SMARTD_ARGS="-i 21600"  Check status every 21600 seconds (3 hours)` 

For more info see [smartd(8)](https://www.smartmontools.org/browser/trunk/smartmontools/smartd.8.in).

#### Schedule self-tests

smartd can tell disks to perform self-tests on a schedule. The following `/etc/smartd.conf` configuration will start a short self-test every day between 2-3am, and an extended self test weekly on Saturdays between 3-4am:

 `/etc/smartd.conf`  `DEVICESCAN -s (S/../.././02|L/../../6/03)` 

#### Alert on temperature changes

smartd can track disk temperatures and alert if they rise too quickly or hit a high limit. The following will log changes of 4 degrees or more, log when temp reaches 35 degrees, and log/email a warning when temp reaches 40:

 `/etc/smartd.conf`  `DEVICESCAN -W 4,35,40` 
**Tip:** You can determine the current disk temperature with the command `smartctl -A /dev/<device> | grep Temperature_Celsius`

**Tip:** If you have some disks that run a lot hotter/cooler than others, remove `DEVICESCAN` and define a separate configuration for each device with appropriate temperature settings.

#### Complete smartd.conf example

Putting together all of the above gives the following example configuration:

*   `DEVICESCAN` (smartd scans for disks and monitors all it finds)
*   `-a` (monitor all attributes)
*   `-o on` (enable automatic online data collection)
*   `-S on` (enable automatic attribute autosave)
*   `-n standby,q` (do not check if disk is in standby, and suppress log message to that effect so as not to cause a write to disk)
*   `-s ...` (schedule short and long self-tests)
*   `-W ...` (monitor temperature)
*   `-m ...` (mail alerts)

 `/etc/smartd.conf`  `DEVICESCAN -a -o on -S on -n standby,q -s (S/../.././02|L/../../6/03) -W 4,35,40 -m <username or email>` 

## GUI Applications

*   **Gsmartcontrol** — A GNOME frontend for the smartctl hard disk drive health inspection tool

	[http://gsmartcontrol.sourceforge.net](http://gsmartcontrol.sourceforge.net) || [gsmartcontrol](https://www.archlinux.org/packages/?name=gsmartcontrol) or [gsmartcontrol-svn](https://aur.archlinux.org/packages/gsmartcontrol-svn/)

## See also

*   [Smartmontools Homepage](https://www.smartmontools.org/)
*   [Smartmontools on Ubuntu Wiki](https://help.ubuntu.com/community/Smartmontools)
*   [Gentoo: smartmontools](https://wiki.gentoo.org/wiki/smartmontools "gentoo:smartmontools")