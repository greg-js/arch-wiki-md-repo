[Clam AntiVirus](https://www.clamav.net) is an open source (GPL) anti-virus toolkit for UNIX. It provides a number of utilities including a flexible and scalable multi-threaded daemon, a command line scanner and advanced tool for automatic database updates. Because ClamAV's main use is on file/mail servers for Windows desktops, it primarily detects Windows viruses and malware with its built-in signatures.

## Contents

*   [1 Installation](#Installation)
*   [2 Updating database](#Updating_database)
*   [3 Starting the daemon](#Starting_the_daemon)
*   [4 Testing the software](#Testing_the_software)
*   [5 Adding more databases/signatures repositories](#Adding_more_databases.2Fsignatures_repositories)
    *   [5.1 Set up clamav-unofficial-sigs](#Set_up_clamav-unofficial-sigs)
        *   [5.1.1 MalwarePatrol database](#MalwarePatrol_database)
*   [6 Scan for viruses](#Scan_for_viruses)
*   [7 Using the milter](#Using_the_milter)
*   [8 OnAccessScan](#OnAccessScan)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [9.2 Error: No supported database files found](#Error:_No_supported_database_files_found)
    *   [9.3 Error: Can't create temporary directory](#Error:_Can.27t_create_temporary_directory)
*   [10 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [clamav](https://www.archlinux.org/packages/?name=clamav) package. Also you can install:

*   [clamtk](https://www.archlinux.org/packages/?name=clamtk) , a GUI frontend for clamav.
*   addons
    *   [clamtk-gnome](https://aur.archlinux.org/packages/clamtk-gnome/) , a simple plugin for ClamTk to allow a right-click, context menu scan of files or folders in the Nautilus file manager.
    *   [thunar-sendto-clamtk](https://aur.archlinux.org/packages/thunar-sendto-clamtk/) , a simple plugin to allow a right-click, context menu scan of files or folders in Thunar.

## Updating database

Update the virus definitions with:

```
# freshclam

```

The database files are saved in:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd
/var/lib/clamav/bytecode.cvd

```

The virus definition updater service is called `clamav-freshclam.service`. Consider starting it and enabling it to start at boot so that the virus definitions are kept recent.

## Starting the daemon

Consider updating the database before starting the service for the first time or you will run into troubles/errors which will prevent ClamAV to start correctly.

The service is called `clamav-daemon.service`. [Start](/index.php/Start "Start") it or [enable](/index.php/Enable "Enable") it to start at boot. You will need to run `freshclam` prior to starting the service.

## Testing the software

In order to make sure ClamAV and the definitions are installed correctly, scan the [EICAR test file](https://www.eicar.org/86-0-Intended-use.html) (a harmless signature with no virus code) with clamscan.

```
$ curl [https://www.eicar.org/download/eicar.com.txt](https://www.eicar.org/download/eicar.com.txt) | clamscan -

```

The output **must** include:

```
stdin: Eicar-Test-Signature FOUND

```

Otherwise; read the Troubleshooting part or ask for help in the [Arch Forums](https://bbs.archlinux.org/).

## Adding more databases/signatures repositories

ClamAV can use databases/signature from other repositories or security vendors.

To add the most important ones in a single step, install [clamav-unofficial-sigs](https://aur.archlinux.org/packages/clamav-unofficial-sigs/) and configure it in `/etc/clamav-unofficial-sigs/user.conf`.

This will add signatures/databases from e.g. MalwarePatrol, SecuriteInfo, Yara, Linux Malware Detect, etc. For the full list of databases, [see the description of the GitHub repository](https://github.com/extremeshok/clamav-unofficial-sigs#description).

### Set up clamav-unofficial-sigs

First, edit the configuration in `/etc/clamav-unofficial-sigs/user.conf`, and change the following line:

```
# Uncomment the following line to enable the script
user_configuration_complete="yes"

```

To enable the unofficial signature service (which includes manpages, log rotation, and a cron job), run the following:

```
# clamav-unofficial-sigs.sh --install-all

```

Note that you still must have the `clamav-daemon` service running in order to have signature updates from ClamAV themselves.

This will refresh the signatures from the databases used in the clamav-unofficial-sigs script and extra ones as configured in each configuration file in the `/etc/clamav-unofficial-sigs` folder. To refresh signatures from these databases manually, run the following:

```
# clamav-unofficial-sigs.sh

```

To stop the cron job from running, delete this file: `/etc/cron.d/clamav-unofficial-sigs`.

#### MalwarePatrol database

If you would like to use the MalwarePatrol database, sign up for an account at [https://www.malwarepatrol.net/](https://www.malwarepatrol.net/).

In `/etc/clamav-unofficial-sigs/user.conf`, change the following to enable this functionality:

```
malwarepatrol_receipt_code="YOUR-RECEIPT-NUMBER" # enter your receipt number here
malwarepatrol_product_code="8" # Use 8 if you have a Free account or 15 if you are a Premium customer.
malwarepatrol_list="clamav_basic" # clamav_basic or clamav_ext
malwarepatrol_free="yes" # Set to yes if you have a Free account or no if you are a Premium customer.

```

Source: [https://www.malwarepatrol.net/clamav-configuration-guide/](https://www.malwarepatrol.net/clamav-configuration-guide/)

## Scan for viruses

`clamscan` can be used to scan certain files, home directories, or an entire system:

```
$ clamscan myfile
$ clamscan --recursive --infected /home # or -r -i
$ clamscan --recursive --infected --exclude-dir='^/sys|^/dev' /

```

If you would like `clamscan` to remove the infected file add to the command the `--remove` option, or you can use `--move=/dir` to quarantine them.

You may also want `clamscan` to scan larger files. In this case, append the options `--max-filesize=4000M` and `--max-scansize=4000M` to the command. '4000M' is the largest possible value, and may be lowered as necessary.

Using the `-l /path/to/file` option will print the `clamscan` logs to a text file for locating reported infections.

## Using the milter

Milter will scan your sendmail server for email containing virus. Copy `/etc/clamav/clamav-milter.conf.sample` to `/etc/clamav/clamav-milter.conf` and adjust it to your needs. For example:

 `/etc/clamav/clamav-milter.conf` 
```
MilterSocket /run/clamav/clamav-milter.sock
MilterSocketMode 660
FixStaleSocket yes
User clamav
PidFile /run/clamav/clamav-milter.pid
TemporaryDirectory /tmp
ClamdSocket unix:/var/lib/clamav/clamd.sock
LogSyslog yes
LogInfected Basic

```

Create `/etc/systemd/system/clamav-milter.service`:

 `/etc/systemd/system/clamav-milter.service` 
```
[Unit]
Description='ClamAV Milter'
After=clamd.service

[Service]
Type=forking
ExecStart=/usr/bin/clamav-milter --config-file /etc/clamav/clamav-milter.conf

[Install]
WantedBy=multi-user.target

```

Enable and start the service.

## OnAccessScan

On-access scanning requires the kernel to be compiled with the *fanotify* kernel module (kernel >= 3.8). Check if *fanotify* has been enabled before enabling on-access scanning.

```
$ cat /proc/config.gz | gunzip | grep FANOTIFY=y

```

On-access scanning will scan the file while reading, writing or executing it.

First, edit the `/etc/clamav/clamd.conf` configuration file by adding the following to the end of the file (you can also change the individual options):

 `/etc/clamav/clamd.conf` 
```
# Enables on-access scan, requires clamd service running
ScanOnAccess true

# Set the mount point where to recursively perform the scan,
# this could be every path or multiple path (one line for path)
OnAccessMountPath /usr
OnAccessMountPath /home/
OnAccessExcludePath /var/log/

# Flag fanotify to block any events on monitored files to perform the scan
OnAccessPrevention false

# Perform scans on newly created, moved, or renamed files
OnAccessExtraScanning true

# Check the UID from the event of fanotify
OnAccessExcludeUID 0

# Specify an action to perform when clamav detects a malicious file
# it is possible to specify an inline command too
VirusEvent /etc/clamav/detected.zsh

# WARNING: clamd should run as root
User root

```

Next, create the file `/etc/clamav/detected.sh` and add the following. This allows you to change/specify the debug message when a virus has been detected by clamd's on-access scanning service:

 `/etc/clamav/detected.sh` 
```
#!/bin/bash
PATH=/usr/bin

alert="Signature detected: $CLAM_VIRUSEVENT_VIRUSNAME in $CLAM_VIRUSEVENT_FILENAME"

# Send the alert to systemd logger if exist, othewise to /var/log
if [[ -z $(command -v systemd-cat) ]]; then
	echo "$(date) - $alert" >> /var/log/clamav/infected.log
else
	# as "emerg", this could cause your DE to show a visual alert. Happen in Plasma. but the next visual alert is much nicer
	echo "$alert" | /usr/bin/systemd-cat -t clamav -p emerg
fi

#send an alrt to all graphical user
XUSERS=($(who|awk '{print $1$NF}'|sort -u))

for XUSER in $XUSERS; do
    NAME=(${XUSER/(/ })
    DISPLAY=${NAME[1]/)/}
    DBUS_ADDRESS=unix:path=/run/user/$(id -u ${NAME[0]})/bus
    echo "run $NAME - $DISPLAY - $DBUS_ADDRESS -" >> /tmp/testlog 
    /usr/bin/sudo -u ${NAME[0]} DISPLAY=${DISPLAY} \
                       DBUS_SESSION_BUS_ADDRESS=${DBUS_ADDRESS} \
                       PATH=${PATH} \
                       /usr/bin/notify-send -i dialog-warning "clamAV" "$alert"
done

```

If you are using [AppArmor](/index.php/AppArmor "AppArmor"), it is also necessary to allow clamd to run as root:

```
# aa-complain clamd

```

Restart/start the service with `systemctl restart clamd.service`.

Source: [http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html](http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html)

## Troubleshooting

### Error: Clamd was NOT notified

If you get the following messages after running freshclam:

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Add a sock file for ClamAV:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Then, edit `/etc/clamav/clamd.conf` - uncomment this line:

```
LocalSocket /var/lib/clamav/clamd.sock

```

Save the file and [restart the daemon](/index.php/Daemons "Daemons") with `systemctl restart clamd.service`.

### Error: No supported database files found

If you get the next error when starting the daemon:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

This happens because of mismatch between `/etc/freshclam.conf` setting `DatabaseDirectory` and `/etc/clamd.conf` setting `DatabaseDirectory`. `/etc/freshclam.conf` pointing to `/var/lib/clamav`, but `/etc/clamd.conf` (default directory) pointing to `/usr/share/clamav`, or other directory. Edit in `/etc/clamd.conf` and replace with the same DatabaseDirectory like in `/etc/freshclam.conf`. After that clamav will start up succesfully.

### Error: Can't create temporary directory

If you get the following error, along with a 'HINT' containing a UID and a GID number:

```
# can't create temporary directory

```

Correct permissions:

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav

```

## See also

*   [Wikipedia:ClamAV](https://en.wikipedia.org/wiki/ClamAV "wikipedia:ClamAV")
*   [ClamSMTP](/index.php/ClamSMTP "ClamSMTP")