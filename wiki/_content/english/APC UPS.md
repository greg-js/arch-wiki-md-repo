This document describes how to install the APC UPS daemon. The main advantage of using an APC UPS (for me) is that it can communicate with your Linux box through either a RS-232 or USB serial connection. In the event of a prolonged power outage, should the APC UPS lose most of its battery capacity, it can tell the Linux box to perform a safe shutdown.

## Contents

*   [1 Install the package](#Install_the_package)
*   [2 Configure APC UPS](#Configure_APC_UPS)
*   [3 Test](#Test)
*   [4 Hibernating instead of shutting down](#Hibernating_instead_of_shutting_down)
    *   [4.1 Create the hibernate script](#Create_the_hibernate_script)
    *   [4.2 Link the hibernate script for apcupsd to use it](#Link_the_hibernate_script_for_apcupsd_to_use_it)
    *   [4.3 Make apcupsd kill UPS power once the hibernate is done](#Make_apcupsd_kill_UPS_power_once_the_hibernate_is_done)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 The desktop environment will also sense the UPS if connected by USB cable](#The_desktop_environment_will_also_sense_the_UPS_if_connected_by_USB_cable)
*   [6 See also](#See_also)

## Install the package

[Install](/index.php/Install "Install") the [apcupsd](https://www.archlinux.org/packages/?name=apcupsd) package.

## Configure APC UPS

The main configuration file for the APC UPS daemon can be found here: `/etc/apcupsd/apcupsd.conf`

In the following example, the lines of text are changed to support a USB style cable:

Before:

```
UPSCABLE smart

UPSTYPE smartups

DEVICE /dev/ttyS0

```

After:

```
UPSCABLE usb

UPSTYPE usb

DEVICE /dev/usb/hiddev[[0-15]]

```

## Test

First, [enable](/index.php/Enable "Enable") and start the [systemd](/index.php/Systemd "Systemd") service, `apcupsd.service`.

Next, wait about a minute and confirm the daemon is running and properly monitoring the battery:

```
# apcaccess status
APC      : 001,033,0819
DATE     : Sat Mar 05 SOMETIME 2005
HOSTNAME : somehostname
RELEASE  : 3.10.16
VERSION  : 3.10.16 (04 November 2004) unknown
UPSNAME  : somehostname
CABLE    : USB Cable
MODEL    : Back-UPS ES 725
UPSMODE  : Stand Alone
STARTTIME: Sat Mar SOMETIME 2005
STATUS   : ONLINE
LINEV    : 119.0 Volts
LOADPCT  :  23.0 Percent Load Capacity
BCHARGE  : 100.0 Percent
TIMELEFT :  30.5 Minutes
MBATTCHG : 5 Percent
MINTIMEL : 3 Minutes
MAXTIME  : 0 Seconds
LOTRANS  : 088.0 Volts
HITRANS  : 138.0 Volts
ALARMDEL : Always
BATTV    : 13.5 Volts
NUMXFERS : 0
TONBATT  : 0 seconds
CUMONBATT: 0 seconds
XOFFBATT : N/A
STATFLAG : 0x02000008 Status Flag
MANDATE  : 2002-12-02
SERIALNO : QB0249360043
BATTDATE : 2000-00-00
NOMBATTV :  12.0
FIRMWARE : 02.n2.D USB FW:n2
APCMODEL : Back-UPS ES 725
END APC  : Sat SOMETIME 2005

```

To fully test your setup:

1.  Change `TIMEOUT` from `0` to `1` in the `/etc/apcupsd/apcupsd.conf` file.
2.  Remove wall power from the UPS.
3.  Observe that your Linux box powers down, in short order.
4.  Plug the UPS back into the wall.
5.  Power on your Linux box.
6.  Change `TIMEOUT` from `1` back to `0` in the `/etc/apcupsd/apcupsd.conf` file.

When everything is ok, all that's left to do is enable the `apcupsd` service.

## Hibernating instead of shutting down

You can make your system hibernate instead of shutting down. First, make sure the system hibernates cleanly. To set up hibernation, look [here](/index.php/Pm-utils "Pm-utils").

### Create the hibernate script

Create this in `/usr/local/bin/hibernate` as root:

```
#!/bin/bash
# Hibernate the system - designed to be called via symlink from /etc/apcupsd
# directory in case of apcupsd initiating a shutdown/reboot.  Can also be used
# interactively or from any script to cause a hibernate.

# Do the hibernate
/usr/bin/systemctl hibernate

# At this point system should be hibernated - when it comes back, we resume this script here

# On resume, tell controlling script (/etc/apcupsd/apccontrol) NOT to continue with default action (i.e. shutdown).
exit 99

```

Make it executable by running:

```
# chmod +x /usr/local/bin/hibernate

```

### Link the hibernate script for apcupsd to use it

Create a symbolic link from the `/etc/apcupsd` directory to the script. The result is the apcupd's apccontrol script, in this directory, will call the hibernate script instead of doing the default shutdown action for these operations.

```
# ln -s /usr/local/bin/hibernate /etc/apcupsd/doshutdown

```

If you are running apcupsd as a client to another machine running apcupsd as a server and want your machine to hibernate if the sever is shutdown or if communication to the server is lost then you may also wish to add:

```
# ln -s /usr/local/bin/hibernate /etc/apcupsd/remotedown

```

### Make apcupsd kill UPS power once the hibernate is done

Once the PC has hibernated successfully, it is common practice to switch off the UPS in order to conserve battery charge and prevent full battery drain. This can be achieved through a power suspend event in systemd.

Create `/usr/lib/systemd/system-sleep/ups-kill` and put the following contents in it:

```
#!/bin/bash

case $2 in

  # In the event the computer is hibernating.
  hibernate)
    case $1 in

       # Going into a hibernate state.
       pre)

         # See if this is a powerfail situation.
         if [ -f /etc/apcupsd/powerfail ]; then
           echo
           echo "ACPUPSD will now power off the UPS"
           echo
           /etc/apcupsd/apccontrol killpower
           echo
           echo "Please ensure that the UPS has powered off before rebooting"
           echo "Otherwise, the UPS may cut the power during the reboot!!!"
           echo
         fi
       ;;

       # Coming out of a hibernate state.
       post)

         # If there are remnants from a powerfail situation, remove them.
         if [ -f /etc/apcupsd/powerfail ]; then
           rm /etc/apcupsd/powerfail
         fi

	 # Restart the daemon; otherwise it may be unresponsive in a
         # second powerfailure situation.
	 systemctl restart apcupsd
       ;;
    esac
  ;;
esac

```

Make the script executable by doing:

```
# chmod +x /usr/lib/systemd/system-sleep/ups-kill

```

Now you can [test your setup](#Test).

## Troubleshooting

### The desktop environment will also sense the UPS if connected by USB cable

For example, the default KDE setting is to put the computer in sleep if it has been on UPS battery for more than 10 minutes and the mouse has not moved. On many computers this causes a crash. This can be changed from KDE System Settings->Power Management->On battery.

## See also

*   [Apcupsd home page](http://www.apcupsd.org/)
*   [Forcing hibernate](http://ubuntuforums.org/showthread.php?p=4302102)
*   [apcupsd manual](http://www.apcupsd.com/manual/manual.html#the-shutdown-sequence-and-its-discontents)