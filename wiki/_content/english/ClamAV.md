[Clam AntiVirus](http://www.clamav.net) is an open source (GPL) anti-virus toolkit for UNIX. It provides a number of utilities including a flexible and scalable multi-threaded daemon, a command line scanner and advanced tool for automatic database updates. Because ClamAV's main use is on file/mail servers for Windows desktops it primarily detects Windows viruses and malware.

## Contents

*   [1 Installation](#Installation)
*   [2 Updating database](#Updating_database)
*   [3 Starting the daemon](#Starting_the_daemon)
*   [4 Testing the software](#Testing_the_software)
*   [5 Adding more databases/signatures repositories](#Adding_more_databases.2Fsignatures_repositories)
*   [6 Scan for viruses](#Scan_for_viruses)
*   [7 Using the milter](#Using_the_milter)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Error: Clamd was NOT notified](#Error:_Clamd_was_NOT_notified)
    *   [8.2 Error: No supported database files found](#Error:_No_supported_database_files_found)
    *   [8.3 Error: Can't create temporary directory](#Error:_Can.27t_create_temporary_directory)

## Installation

ClamAV can be [installed](/index.php/Install "Install") with package [clamav](https://www.archlinux.org/packages/?name=clamav).

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

The virus definition updater service is called `freshclamd.service`. Consider starting it and enabling it to start at boot so that the virus definitions are kept recent.

## Starting the daemon

Consider updating the database before starting the service for the first time or you will run into troubles/errors which will prevent ClamAV to start correctly.

The service is called `clamd.service`. [Start](/index.php/Start "Start") it or [enable](/index.php/Enable "Enable") it to start at boot. You will need to run `freshclam` prior to starting the service.

## Testing the software

In order to make sure ClamAV and the definitions are installed correctly, scan the [EICAR test file](http://www.eicar.org/86-0-Intended-use.html) (a harmless signature with no virus code) with clamscan.

```
$ curl [http://www.eicar.org/download/eicar.com.txt](http://www.eicar.org/download/eicar.com.txt) | clamscan -

```

The output **must** include:

```
stdin: Eicar-Test-Signature FOUND

```

Otherwise; read the Troubleshooting part or ask for help in the [Arch Forums](https://bbs.archlinux.org/).

## Adding more databases/signatures repositories

ClamAV can use databases/signature from other repositories or security vendors.

To add the most important ones in a single step install [clamav-unofficial-sigs](https://aur.archlinux.org/packages/clamav-unofficial-sigs/) and configure it in `/etc/clamav-unofficial-sigs/user.conf`.

This will add signatures/databases from e.g. MalwarePatrol, SecuriteInfo, Yara, Linux Malware Detect,...

## Scan for viruses

`clamscan` can be used to scan certain files, home directory, or an entire system:

```
$ clamscan myfile
$ clamscan --recursive --infected /home # or -r -i
$ clamscan --recursive --infected --exclude-dir='^/sys|^/dev' /

```

If you would like `clamscan` to remove the infected file add to the command the `--remove` option, or you can use `--move=/dir` to quarantine them.

You may also want `clamscan` to scan larger files. In this case, append the options `--max-filesize=4000M` and `--max-scansize=4000M` to the command. '4000M' is the largest possible value, and may be lowered as necessary.

Using the `-l /path/to/file` option will print the `clamscan` logs to a text file for locating reported infections.

## Using the milter

Copy `/etc/clamav/clamav-milter.conf.sample` to `/etc/clamav/clamav-milter.conf` and adjust it to your needs. For example:

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

Save the file and [restart the daemon](/index.php/Daemons "Daemons")

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