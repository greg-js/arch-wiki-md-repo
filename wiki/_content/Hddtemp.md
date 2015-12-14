# Hddtemp

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [lm sensors](/index.php/Lm_sensors "Lm sensors")

[hddtemp](https://savannah.nongnu.org/projects/hddtemp/) is a small utility (with daemon) that gives the hard-drive temperature via S.M.A.R.T. (for drives supporting this feature).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Daemon](#Daemon)
*   [4 Monitors](#Monitors)
*   [5 Solid State Drives](#Solid_State_Drives)

## Installation

[Install](/index.php/Install "Install") [hddtemp](https://www.archlinux.org/packages/?name=hddtemp) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Hddtemp requires root privileges. The command `hddtemp` must be followed by at least one drive's location, with several directories separated by spaces:

```
# hddtemp /dev/sd_X1_ /dev/sd_X2_ ... /dev/sd_Xn_

```

## Daemon

Running the daemon allows to access the temperature via TCP/IP, to use for example with scripts.

The daemon is [controlled](/index.php/Systemd#Using_units "Systemd") by `hddtemp.service`.

**Note:** Arguments to `hddtemp` are directly given in `/usr/lib/systemd/system/hddtemp.service`. This is especially important with multiple disks, as the default configuration only monitors `/dev/sda`. Change `ExecStart` [to override](/index.php/Systemd#Editing_provided_units "Systemd") `hddtemp.service`:

*   Create a directory in `/etc/systemd/system`:

```
# mkdir /etc/systemd/system/hddtemp.service.d

```

*   Create `customexec.conf` inside and add the drives you want to monitor, e.g.:

 `/etc/systemd/system/hddtemp.service.d/customexec.conf` 

```
[Service]
ExecStart=
ExecStart=/usr/bin/hddtemp -dF /dev/sda /dev/sdb /dev/sdc
```

You can also the [auto-generate](https://github.com/AndyCrowd/auto-generate-configuration-files/blob/master/gen-customexec.conf-hddtemp.sh) script that detects with help of [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) all supported by [hddtemp](https://www.archlinux.org/packages/?name=hddtemp) hard-drivers and generating to the stdout the `customexec.conf` pattern file.

*   [Reload](/index.php/Reload "Reload") systemd's unit files.
*   [Restart](/index.php/Restart "Restart") the hddtemp service.

To get the temperature, connect to the daemon which listens on port 7634\. With [inetutils](https://www.archlinux.org/packages/?name=inetutils):

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

 `$ nc localhost 7634 |sed 's/|//m' | sed 's/||/ \n/g' | awk -F'|' '{print $1 " " $3 " " $4}'` 

```
/dev/sda 32 C 
/dev/sdb 36 C
```

Refer to the manpage for more information:

```
$ man hddtemp

```

## Monitors

Hddtemp can be integrated with [system monitors](/index.php/List_of_applications#System_monitoring "List of applications").

## Solid State Drives

Hddtemp usually reads field `194` from the smart data of the drive. In SSDs temperature information is usually stored in field `190`. To obtain this information, one can run:

```
$ smartctl -a /dev/sdX

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hddtemp&oldid=412096](https://wiki.archlinux.org/index.php?title=Hddtemp&oldid=412096)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")