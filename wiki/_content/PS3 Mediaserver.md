# PS3 Mediaserver

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Mentions rc.d scripts. (Discuss in [Talk:PS3 Mediaserver#](https://wiki.archlinux.org/index.php/Talk:PS3_Mediaserver))

Server implemented in java. Has very good default transcoding profiles for several clients, but lacks good information for headless servers.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Run as a daemon](#Run_as_a_daemon)
    *   [3.1 SysVinit](#SysVinit)
    *   [3.2 systemd](#systemd)
*   [4 Indexing](#Indexing)

## Installation

**Note:** Because of the dependency [tsmuxer](https://aur.archlinux.org/packages/tsmuxer/)<sup><small>AUR</small></sup> having extra 32-bit dependencies, you will need to enable the [multilib](/index.php/Multilib "Multilib") repository if you have a 64-bit system.

Install [pms](https://aur.archlinux.org/packages/pms/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR").

## Configuration

The default install location is /opt/pms and the config file is at /opt/pms/PMS.conf, there are comments describing what each option is for.

If running headless on a server

 `Operating Mode`  `minimized = true` 

If you do not want your entire filesystem to be shown

 `Media Locations` 

```
folders = /directory.you.want.shared/,/another.directory

```

If you run into issues with the wrong audio track playing (example: English desired)

 `Audio language priority` 

```
mencoder_audiolangs = eng,und

```

Example of english subtitles desired, no subtitles by default on English programs

 `Subtitle language priority` 

```
mencoder_sublangs = loc,eng,und

```

A list with all options can be found [here](http://ps3mediaserver.org/forum/viewtopic.php?f=3&t=254&hilit=pms.conf#p15283).

## Run as a daemon

### SysVinit

Use the following modified daemon script (originally from pms-svn).

 `/etc/rc.d/pms` 

```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions
. /etc/conf.d/pms

PID=`cat /var/run/pms.pid 2> /dev/null`
[ -z "$PID" ] && PID=`ps -Ao pid,command | grep java | grep pms.jar | awk '{print $1}'`

case "$1" in
	start)
		stat_busy "Starting PS3 Media Server"
		if [ -z "$PID" ]; then
			if [ -n "$PMS_USER" ]; then
				su -s '/bin/sh' $PMS_USER -c "/usr/bin/ps3mediaserver &>> /var/log/pms.log" &
			else
				/usr/bin/ps3mediaserver &>> /var/log/pms.log &
			fi
			PID=$!
			if [ $? -gt 0 ]; then
				stat_fail
			else
				echo $PID > /var/run/pms.pid
				add_daemon pms
				stat_done
			fi
		fi
		;;
	stop)
		stat_busy "Stopping PS3 Media Server"
		[ ! -z "$PID" ]  && kill $PID &> /dev/null
		while ps -p $PID &> /dev/null; do sleep 1; done
		if [ $? -gt 0 ]; then
			stat_fail
		else
			rm /var/run/pms.pid 2> /dev/null
			rm_daemon pms
			stat_done
		fi
		;;
	restart)
		$0 stop
		sleep 1
		$0 start
		;;
	*)
		echo "usage: $0 {start|stop|restart}"
		;;
esac
exit 0

```

```
# /etc/rc.d/pms start

```

*   (optionally) watch the output with 'tail -f /var/log/pms.log' or 'tail -f /opt/pms/debug.log' for any problems.

### systemd

The package ships a systemd unit file by default now (since 1.71.0-2). However, upon bootup the service [will not execute properly](http://www.ps3mediaserver.org/forum/viewtopic.php?f=3&t=17992). This can be resolved by adding a timeout before the service starts the involved script. One only has to edit the file as follows by adding the "ExecStartPre" line.

 `/usr/lib/systemd/system/pms@.service` 

```
[Unit]
Description=PS3 Media Server
After=syslog.target network.target rpcbind.service

[Service]
User=%i
Group=users
WorkingDirectory=/opt/pms/
Type=simple
ExecStartPre=/usr/bin/sleep 16
ExecStart=/opt/pms/PMS.sh

[Install]
WantedBy=multi-user.target
```

After the addition just run:

```
# systemctl daemon-reload
# systemctl start pms@<username> # to start once
# systemctl enable pms@<username> # automatically start at boot
# journalctl -u pms@<username> # to debug the logfiles

```

## Indexing

This should be done automagically upon starting the service, but if it does not, this is how to do it manually:

*   Browse the logs to see at what ip-address and port pms has started the built-in webservice
*   Use your web browser to go to: http://<ip-address-of-your-server>:5001/console/home and click on 'index files and folders'
*   After the indexing has ended, you are done.

Retrieved from "[https://wiki.archlinux.org/index.php?title=PS3_Mediaserver&oldid=418352](https://wiki.archlinux.org/index.php?title=PS3_Mediaserver&oldid=418352)"