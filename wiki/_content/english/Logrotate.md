Related articles

*   [Cron](/index.php/Cron "Cron")
*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")

From [https://github.com/logrotate/logrotate](https://github.com/logrotate/logrotate):

	*The logrotate utility is designed to simplify the administration of log files on a system which generates a lot of log files. Logrotate allows for the automatic rotation compression, removal and mailing of log files. Logrotate can be set to handle a log file daily, weekly, monthly or when the log file gets to a certain size.*

By default, logrotate's *rotation* consists of renaming existing log files with a numerical suffix, then recreating the original *empty* log file. For example, `/var/log/syslog.log` is renamed `/var/log/syslog.log.1`. If `/var/log/syslog.log.1` already exists from a previous rotation, it is first renamed `/var/log/syslog.log.2`. (The number of backlogs to keep can be configured.)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 exim log not rotated](#exim_log_not_rotated)
    *   [3.2 Check logrotate status](#Check_logrotate_status)
    *   [3.3 Skipping log because parent directory has insecure permission](#Skipping_log_because_parent_directory_has_insecure_permission)
*   [4 See also](#See_also)

## Installation

Logrotate can be installed with the [logrotate](https://www.archlinux.org/packages/?name=logrotate) package. It is installed by default as it is member of the [base](https://www.archlinux.org/groups/x86_64/base/) group.

By default, logrotate runs daily using a [systemd timer](/index.php/Systemd/Timers "Systemd/Timers"): `logrotate.timer`.

## Configuration

The primary configuration file for logrotate which sets default parameters is `/etc/logrotate.conf`; additional application-specific configuration files are included from the `/etc/logrotate.d` directory. Values set in application-specific configuration files override those same parameters in the primary configuration file.

To verify if logrotate works correctly run the following command which will produce debug output:

```
logrotate -d

```

To test your logrotate script, for example your nginx logrotate script in */etc/logrotate.d* directory, use:

```
logrotate -f -v /etc/logrotate.d/nginx

```

## Troubleshooting

### exim log not rotated

If you have set the `olddir` variable in `/etc/logrotate.conf`, you will get a message such as:

`error: failed to rename /var/log/exim/mainlog to /var/log/old/mainlog.1: Permission denied`

To fix this, add the user `exim` to the group `log`. Then change the group of the `olddir`, usually `/var/log/old`, to `log` instead of the default `root`.

### Check logrotate status

Run `cat /var/lib/logrotate.status` to see which logrotate files were rotated.

```
"/var/log/mysql/query.log" 2016-3-20-5:0:0
"/var/log/samba/samba-smbd.log" 2016-3-21-5:0:0
"/var/log/httpd/access_log" 2016-3-20-5:0:0

```

### Skipping log because parent directory has insecure permission

Set in the config which user and which group has to job `/etc/logrotate.d/job` to be run with:

```
file-to-be-rotated {
    su user group
    rotate 4
}

```

## See also

*   [Logrotate on Gentoo Linux Wiki](http://wiki.gentoo.org/wiki/Logrotate)
*   [logrotate(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/logrotate.8) manual page