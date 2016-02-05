# Monit

[Monit](https://mmonit.com/monit/), not to be confused to [M/Monit](https://mmonit.com/), is an AGPL3.0 licensed system and process monitoring tool. Monit can automatically restart crashed services, display temperatures from standard hardware (through [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) and hard drives from [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) for example). Service alerts can be sent based on a wide criteria including a single occurrence or occurrences over a period of time. It can be accessed directly through the command line or ran as a web app using its integrated HTTP(S) server. This allows quick and streamlined snapshot of a given systems status.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Configuration syntax](#Configuration_syntax)
*   [3 Configuration examples](#Configuration_examples)
    *   [3.1 Mailserver declaration](#Mailserver_declaration)
    *   [3.2 Email notification format](#Email_notification_format)
    *   [3.3 CPU, memory and swap utilization](#CPU.2C_memory_and_swap_utilization)
    *   [3.4 Filesystem(s) usage](#Filesystem.28s.29_usage)
    *   [3.5 Process monitoring](#Process_monitoring)
    *   [3.6 Hard drive health and temperature using scripts](#Hard_drive_health_and_temperature_using_scripts)
        *   [3.6.1 Temperature](#Temperature)
        *   [3.6.2 SMART health status](#SMART_health_status)
*   [4 Alert recipients: global or subsystem based](#Alert_recipients:_global_or_subsystem_based)
    *   [4.1 Global alerts](#Global_alerts)
    *   [4.2 Subsystem alerts](#Subsystem_alerts)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [monit](https://www.archlinux.org/packages/?name=monit) package and any software for optional testing such as [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) or [smartmontools](https://www.archlinux.org/packages/?name=smartmontools). Once you have completed the configuration, be sure to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `monit` service.

## Configuration

Monit keeps a main configuration file as `/etc/monitrc`. You can choose to edit this file but if you wish to run scripts (such as to get hard drive temperatures or health status) you should uncomment the last directive of `include /etc/monit.d/*`, save `/etc/monitrc` and create `/etc/monit.d/`.

**Note:** Monit requires the `/etc/monitrc` file (and potentially files stored in `/etc/monit.d`) to have `0700` permissions. Failure to comply will result in Monit failing to start.

### Configuration syntax

Monit utilizes a configuration syntax that makes it very easy to read; essentially `check WHAT` followed by `if THING condition THEN action` format. Any occurrence of `if`, `and`, `with(in)`, `has`, `us(ing|e)`, `on(ly)`, `then`, `for`, `of` in the configuration file is for human readability only and are completely ignored by Monit.

## Configuration examples

### Mailserver declaration

```
set mailserver smtp.myserver.com port 587
        username "MyUser" password "MyPassW0rd"
using tlsv12
```

### Email notification format

```
set mail-format {
      from: Monit@MyServer
   subject: $SERVICE $EVENT at $DATE
   message: Monit $ACTION $SERVICE at $DATE on $HOST: $DESCRIPTION.
} 
```

**Note:** The above variables such as `$SERVICE` are _not_ generic examples but are _specific_ variable names which Monit replaces with what the alert is, on what system, etc.

### CPU, memory and swap utilization

```
check system $HOST
    if loadavg (15min) > 15 for 5 times within 15 cycles then alert
    if memory usage > 80% for 4 cycles then alert
    if swap usage > 20% for 4 cycles then alert
```

### Filesystem(s) usage

```
check filesystem rootfs with path /
    if space usage > 90% then alert

check filesystem NFS with path /mnt/nfs_share
    if space usage > 90% then alert
```

### Process monitoring

```
check process sshd with pidfile /var/run/sshd.pid
   start program  "systemctl start sshd"
   stop program  "systemctl stop sshd"
   if failed port 22 protocol ssh then restart
```

```
check process smbd with pidfile /run/samba/smbd.pid
   group samba
   start program = "/etc/init.d/samba start"
   stop  program = "/etc/init.d/samba stop"
   if failed host 192.168.1.250 port 139 type TCP  then restart
   depends on smbd_bin

check file smbd_bin with path /usr/sbin/smbd
   group samba
   if failed permission 755 then unmonitor
   if failed uid root then unmonitor
   if failed gid root then unmonitor
```

**Note:** For the above [samba](https://www.archlinux.org/packages/?name=samba) example, the first block has `depends on smbd_bin`, this makes the _testing_ of Samba require the actual `smbd` process

### Hard drive health and temperature using scripts

#### Temperature

Create the file `/etc/monit.d/scripts/hdtemp.sh` as well as the `/etc/monit.d/scripts` folder if necessary.

 `/etc/monit.d/scripts/hdtemp.sh` 

```
 #!/bin/sh
 HDDTP=`/usr/sbin/smartctl -a /dev/sd${1} | grep Temp | awk -F " " '{printf "%d",$10}'`
 #echo $HDDTP # for debug only
 exit $HDDTP
```

 `monitrc or /etc/monit.d/*.monit file` 

```
check program SSD-A-Temp with path "/etc/monit.d/scripts/hdtemp.sh a"
    every 5 cycles
    if status > 40 then alert
    group health

check program HDD-B-Temp with path "/etc/monit.d/scripts/hdtemp.sh b"
    every 5 cycles
    if status > 40 then alert
    group health
```

In this example, the `/etc/monit.d/scripts/hdtemp.sh` script assumes your drive path is `/dev/sdX` where `X` is filled in by the letter at the end of the `check` declaration. A similar method is used for the SMART health status in the next example.

#### SMART health status

 `/etc/monit.d/scripts/hdhealth.sh` 

```
 #!/bin/sh
 STATUS=`/usr/sbin/smartctl -H /dev/sd${1} | grep overall-health | awk 'match($0,"result:"){print substr($0,RSTART+8,6)}'`
 if [ "$STATUS" = "PASSED" ] 
 then
     # 1 implies PASSED
     TP=1
 else 
     # 2 implies FAILED
     TP=2
 fi
 #echo $TP # for debug only
 exit $TP
```

 `monitrc or /etc/monit.d/*.monit file` 

```
check program SSD-A-Health with path "/etc/monit.d/scripts/hdhealth.sh a"
    every 120 cycles
    if status != 1 then alert
    group health

check program HDD-B-Health with path "/etc/monit.d/scripts/hdhealth.sh b"
    every 120 cycles
    if status != 1 then alert
    group health
```

**Tip:** The `group` declaration will cause Monit to display all assigned checks with the same group name (in this case samba) together.

## Alert recipients: global or subsystem based

Alerts can be set globally, where a given user / email address is alerted for any `alert` condition; or you can set an alert recipient for each type of check (eg network alerts go to recipient A; process alerts go to recipient B). You can set as many global or subsystem recipients as you like, just make multiple declarations.

### Global alerts

Global alerts are set **outside** of any subsystem checks; for ease of reading they should be set in the same location as the mailserver declaration.

```
SET ALERT email@domain

```

### Subsystem alerts

Subsystem alerts are set very similarly to global alerts except they lack the `SET` flag.

```
ALERT email@domain

```

## See also

*   [Official Documentation](https://mmonit.com/monit/documentation/monit.html)
*   [Monit Wiki configuration examples](https://mmonit.com/wiki/Monit/ConfigurationExamples)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Monit&oldid=419103](https://wiki.archlinux.org/index.php?title=Monit&oldid=419103)"