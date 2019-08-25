This document describes how to install the CyberPower UPS daemon PowerPanel or alternatively the Network-UPS-Tools. The main advantage of using a CyberPower UPS is that it is cheap and it can communicate with your Linux box through either a RS-232 or USB serial connection. In the event of a prolonged power outage, should the CyberPower UPS lose most of its battery capacity, it can tell the Linux box to perform a safe shutdown.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Using PowerPanel](#Using_PowerPanel)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Running](#Running)
    *   [1.4 Customization](#Customization)
        *   [1.4.1 Desktop Notifications](#Desktop_Notifications)
*   [2 Using Network UPS Tools](#Using_Network_UPS_Tools)

## Using PowerPanel

### Installation

[Install](/index.php/Install "Install") the [powerpanel](https://aur.archlinux.org/packages/powerpanel/) package.

### Configuration

Edit `/etc/pwrstatd.conf`

Email notifications can be accomplished by editing `/etc/powerpanel/pwrstatd-powerfail.sh` and `/etc/powerpanel/pwrstatd-lowbatt.sh`

**Warning:** Make sure the path to the email script at the bottom of these scripts is correct. It should be `/etc/powerpanel/pwrstatd-email.sh`

### Running

[Start/enable](/index.php/Start/enable "Start/enable") `pwrstatd.service`.

Then run `# pwrstat -status`. You should get something like this:

```

The UPS information shows as following:

        Properties:
                Model Name...................  Value 1500E
                Firmware Number.............. BFF7104#7N5
                Rating Voltage............... 230 V
                Rating Power................. 900 Watt

        Current UPS status:
                State........................ Normal
                Power Supply by.............. Utility Power
                Utility Voltage.............. 230 V
                Output Voltage............... 230 V
                Battery Capacity............. 100 %
                Remaining Runtime............ 61 min.
                Load......................... 126 Watt(14 %)
                Line Interaction............. None
                Test Result.................. Unknown
                Last Power Event............. None

```

### Customization

You can check and change the current settings using the `pwrstat` command. (However, the command won't work unless the daemon is up and running.)

The service performs configurable actions in two different scenarios:

*   When external power has failed for at least a certain amount of time (60 seconds by default)
*   When battery power is low, as determined by either of two conditions:
    *   Battery capacity is less than a predetermined percentage (35% by default), *or*
    *   Remaining runtime (estimated from current power draw) is less than a predetermined number of seconds (300 seconds—that is, 5 minutes—by default)

To check the current settings, use `pwrstat -config`. For example:

 `$ pwrstat -config` 
```
Daemon Configuration:

Alarm .............................................. On
Hibernate .......................................... Off

Action for Power Failure:

	Delay time since Power failure ............. 60 sec.
	Run script command ......................... On
	Path of script command ..................... /etc/powerpanel/pwrstatd-powerfail.sh
	Duration of command running ................ 0 sec.
	Enable shutdown system ..................... Off

Action for Battery Low:

	Remaining runtime threshold ................ 300 sec.
	Battery capacity threshold ................. 35 %.
	Run script command ......................... On
	Path of command ............................ /etc/powerpanel/pwrstatd-lowbatt.sh
	Duration of command running ................ 0 sec.
	Enable shutdown system ..................... On
```

The `pwrstat` command also provides an interface for changing the settings. For example, to configure the UPS *not* to shut down automatically when there's a power failure but battery power is still high:

```
$ pwrstat -pwrfail -shutdown off

```

See `man pwrstat` or the [PDF user manual](https://dl4jz3rbrsfum.cloudfront.net/documents/CyberPower_UM_PPL.pdf) for more information on how to configure settings.

#### Desktop Notifications

You can modify the `pwrstatd-powerfail.sh` and `pwrstatd-lowbatt.sh` scripts to send [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications") when power fails or battery is low (respectively). For example, add the following line to either file:

 `sudo -u *your_username_here* DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/*your_userid_here*/bus notify-send "Warning: Utility power has failed. Now running on battery." --icon=battery-caution` 

Be sure to change *your_username_here* to your user name and *your_userid_here* to the numeric user ID of your user (use `ls /run/user/` to list possibilities if you're not sure).

## Using Network UPS Tools

If you do not wish to use PowerPanel, the [Network UPS Tools (NUT)](http://networkupstools.org/) is an alternative. Only one of these programs (PowerPanel or NUT) is required to monitor and shut the system down. You shouldn't use both as they might interfere with one another.

Use instructions from the Wiki page of [Network UPS Tools](/index.php/Network_UPS_Tools "Network UPS Tools").