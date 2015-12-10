# Logrotate

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Cron](/index.php/Cron "Cron")
*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")

From [https://fedorahosted.org/logrotate/](https://fedorahosted.org/logrotate/):

_The logrotate utility is designed to simplify the administration of log files on a system which generates a lot of log files. Logrotate allows for the automatic rotation compression, removal and mailing of log files. Logrotate can be set to handle a log file daily, weekly, monthly or when the log file gets to a certain size._

By default, logrotate's _rotation_ consists of renaming existing log files with a numerical suffix, then recreating the original _empty_ log file. For example, `/var/log/syslog.log` is renamed `/var/log/syslog.log.1`. If `/var/log/syslog.log.1` already exists from a previous rotation, it is first renamed `/var/log/syslog.log.2`. (The number of backlogs to keep can be configured.)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 logs not being rotated](#logs_not_being_rotated)
    *   [3.2 exim log not rotated](#exim_log_not_rotated)
*   [4 See also](#See_also)

## Installation

[logrotate](https://www.archlinux.org/packages/?name=logrotate) is available in the [official repositories](/index.php/Official_repositories "Official repositories") and is installed by default as a member of the [base](https://www.archlinux.org/groups/x86_64/base/) group.

[logrotate](https://www.archlinux.org/packages/?name=logrotate) no longer uses a daily [cron](/index.php/Cron "Cron") job. Instead, it uses a systemd timer: `systemctl status logrotate.timer`

## Configuration

The primary configuration file for logrotate is `/etc/logrotate.conf`; additional configuration files are included from the `/etc/logrotate.d` directory.

## Troubleshooting

### logs not being rotated

If you find that your logs aren't being rotated via the cronjob, one reason for that can be wrong `user` and `group` ownership. Both need to be `root`. To fix this either do:

```
# chown root:root /etc/logrotate.conf
# chown -R root:root /etc/logrotate.d

```

or, set the `su` variable to the user and group you desire in `/etc/logrotate.conf`.

### exim log not rotated

If you have set the `olddir` variable in `/etc/logrotate.conf`, you will get a message such as:

`error: failed to rename /var/log/exim/mainlog to /var/log/old/mainlog.1: Permission denied`

To fix this, add the user `exim` to the group `log`. Then change the group of the `olddir`, usually `/var/log/old`, to `log` instead of the default `root`.

## See also

*   [Logrotate on Gentoo Linux Wiki](http://wiki.gentoo.org/wiki/Logrotate)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Logrotate&oldid=381840](https://wiki.archlinux.org/index.php?title=Logrotate&oldid=381840)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services")
*   [Data compression and archiving](/index.php/Category:Data_compression_and_archiving "Category:Data compression and archiving")