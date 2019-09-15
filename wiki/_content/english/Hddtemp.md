Related articles

*   [lm sensors](/index.php/Lm_sensors "Lm sensors")
*   [Conky](/index.php/Conky "Conky")

[hddtemp](https://savannah.nongnu.org/projects/hddtemp/) is a small utility (with daemon) that gives the hard-drive temperature via [S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") (for drives supporting this feature).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Daemon](#Daemon)
    *   [3.1 Override default disk](#Override_default_disk)
*   [4 Monitors](#Monitors)
*   [5 Solid State Drives](#Solid_State_Drives)

## Installation

[Install](/index.php/Install "Install") the [hddtemp](https://www.archlinux.org/packages/?name=hddtemp) package.

## Usage

Hddtemp requires root privileges. The command `hddtemp` must be followed by at least one drive's location. You can list several drives separated by spaces:

```
# hddtemp /dev/disk/by-id/wwn-0x60015ee0000b237f /dev/sd*X2* ... /dev/sd*Xn*

```

**Note:** Block device naming under `/dev/`, like `/dev/sdX`, is inconsistent. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for information on using persistent device paths.

Further usage information is available in the manpage:

```
$ man hddtemp

```

## Daemon

Running the daemon allows access to the temperature information via TCP/IP as a regular user. This is useful for scripts and system monitors.

The daemon is [controlled](/index.php/Systemd#Using_units "Systemd") by `hddtemp.service`.

To get the temperature, connect to the daemon which listens on port 7634.

With [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
$ telnet localhost 7634

```

With [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat):

```
$ nc localhost 7634

```

Both outputs are similar to:

```
|/dev/sda|ST3500413AS|32|C||/dev/sdb|ST2000DM001-1CH164|36|C|

```

For a better looking statistic:

 `$ nc localhost 7634 |sed 's/|//m' | sed 's/||/ 
/g' | awk -F'|' '{print $1 " " $3 " " $4}'` 
```
/dev/sda 32 C 
/dev/sdb 36 C
```

### Override default disk

The default hddtemp daemon only monitors `/dev/sda`. If you have multiple disks, you need to [override](/index.php/Systemd#Editing_provided_units "Systemd") the default configuration to monitor them.

You will need to know which hard drives support monitoring. You can check with [smartmontools](https://www.archlinux.org/packages/?name=smartmontools).

First run this command which will open your default text editor:

```
# systemctl edit hddtemp.service

```

Add the following text:

 `/etc/systemd/system/hddtemp.service.d/<temp file>` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/hddtemp --daemon --foreground /dev/disk/by-id/wwn-0x60015ee0000b237f /dev/sdb --listen=127.0.0.1
```

Change the device names to the ones you want to monitor.

After editing, save the file and exit from editor. *systemd'* will apply changes and reload `hddtemp` service automatically.

You can also use the [auto-generate](https://github.com/AndyCrowd/auto-generate-configuration-files/blob/master/gen-customexec.conf-hddtemp.sh) script will detect supported hard drives using [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) and print to the stdout.

## Monitors

Hddtemp can be integrated with [system monitors](/index.php/List_of_applications#System_monitors "List of applications"). [Conky](/index.php/Conky "Conky") has built in support for hddtemp in daemon mode. You just need to add `$hddtemp °C` to your conky configuration file.

## Solid State Drives

Hddtemp usually reads field `194` from the smart data of the drive. In SSDs temperature information is usually stored in field `190`. To obtain this information, one can run:

```
$ smartctl --all /dev/sdX

```

or

```
$ hddtemp --debug /dev/sdX

```

where X is a character (e.g. a,b,c...) representing the drive. Use `lsblk` to check this.

Alternatively, add a new entry in `/usr/share/hddtemp/hddtemp.db`. For example:

```
$ echo '"Samsung SSD 840 EVO 250G B" 190 C "Samsung SSD 840 EVO 250GB"' >> /usr/share/hddtemp/hddtemp.db

```