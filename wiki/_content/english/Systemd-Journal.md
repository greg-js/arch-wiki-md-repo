See [systemd](/index.php/Systemd "Systemd") for the main article.

*systemd* has its own logging system called the journal; therefore, running a `syslog` daemon is no longer required. To read the log, use:

```
# journalctl

```

In Arch Linux, the directory `/var/log/journal/` is a part of the [systemd](https://www.archlinux.org/packages/?name=systemd) package, and the journal (when `Storage=` is set to `auto` in `/etc/systemd/journald.conf`) will write to `/var/log/journal/`. If that directory is deleted, *systemd* will **not** recreate it automatically and instead will write its logs to `/run/systemd/journal` in a nonpersistent way. However, the folder will be recreated if `Storage=persistent` is added to journald.conf and `systemd-journald.service` is [restarted](/index.php/Restart "Restart") (or the system is rebooted).

Systemd journal classifies messages by [Priority level](#Priority_level) and [Facility](#Facility). Logging classification corresponds to classic [Syslog](https://en.wikipedia.org/wiki/Syslog "wikipedia:Syslog") protocol ([RFC 5424](https://tools.ietf.org/html/rfc5424)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Priority level](#Priority_level)
*   [2 Facility](#Facility)
*   [3 Filtering output](#Filtering_output)
*   [4 Journal size limit](#Journal_size_limit)
*   [5 Clean journal files manually](#Clean_journal_files_manually)
*   [6 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
*   [7 Forward journald to /dev/tty12](#Forward_journald_to_/dev/tty12)
*   [8 Specify a different journal to view](#Specify_a_different_journal_to_view)

## Priority level

A syslog severity code (in systemd called priority) is used to mark the importance of a message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Value | Severity | Keyword | Description | Examples |
| 0 | Emergency | emerg | System is unusable | Severe Kernel BUG, [systemd dumped core](/index.php/Systemd-coredump "Systemd-coredump").
This level should not be used by applications. |
| 1 | Alert | alert | Should be corrected immediately | Vital subsystem goes out of work. Data loss.
`kernel: BUG: unable to handle kernel paging request at ffffc90403238ffc`. |
| 2 | Critical | crit | Critical conditions | Crashes, coredumps. Like familiar flash:
`systemd-coredump[25319]: Process 25310 (plugin-containe) of user 1000 dumped core`
Failure in the system primary application, like X11. |
| 3 | Error | err | Error conditions | Not severe error reported:
`kernel: usb 1-3: 3:1: cannot get freq at ep 0x84`,
`systemd[1]: Failed unmounting /var.`,
`libvirtd[1720]: internal error: Failed to initialize a valid firewall backend` |
| 4 | Warning | warning | May indicate that an error will occur if action is not taken. | A non-root file system has only 1GB free.
`org.freedesktop. Notifications[1860]: (process:5999): Gtk-WARNING **: Locale not supported by C library. Using the fallback 'C' locale`. |
| 5 | Notice | notice | Events that are unusual, but not error conditions. | `systemd[1]: var.mount: Directory /var to mount over is not empty, mounting anyway`,
`gcr-prompter[4997]: Gtk: GtkDialog mapped without a transient parent. This is discouraged` |
| 6 | Informational | info | Normal operational messages that require no action. | `lvm[585]: 7 logical volume(s) in volume group "archvg" now active` |
| 7 | Debug | debug | Information useful to developers for debugging the application. | `kdeinit5[1900]: powerdevil: Scheduling inhibition from ":1.14" "firefox" with cookie 13 and reason "screen"` |

These rules are recommendations, and the priority level of a given error is at the application developer's discretion. It is always possible that the error will be at a higher or lower level than expected.

## Facility

A syslog facility code is used to specify the type of program that is logging the message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Facility code | Keyword | Description | Info |
| 0 | kern | Kernel messages |
| 1 | user | User-level messages |
| 2 | mail | Mail system | Archaic POSIX still supported and sometimes used (for more [mail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mail.1)) |
| 3 | daemon | System daemons | All daemons, including systemd and its subsystems |
| 4 | auth | Security/authorization messages | Also watch for different facility 10 |
| 5 | syslog | Messages generated internally by syslogd | For syslogd implementations (not used by systemd, see facility 3) |
| 6 | lpr | Line printer subsystem (archaic subsystem) |
| 7 | news | Network news subsystem (archaic subsystem) |
| 8 | uucp | UUCP subsystem (archaic subsystem) |
| 9 | Clock daemon | systemd-timesyncd |
| 10 | authpriv | Security/authorization messages | Also watch for different facility 4 |
| 11 | ftp | FTP daemon |
| 12 | - | NTP subsystem |
| 13 | - | Log audit |
| 14 | - | Log alert |
| 15 | cron | Scheduling daemon |
| 16 | local0 | Local use 0 (local0) |
| 17 | local1 | Local use 1 (local1) |
| 18 | local2 | Local use 2 (local2) |
| 19 | local3 | Local use 3 (local3) |
| 20 | local4 | Local use 4 (local4) |
| 21 | local5 | Local use 5 (local5) |
| 22 | local6 | Local use 6 (local6) |
| 23 | local7 | Local use 7 (local7) |

Useful facilities to watch: 0, 1, 3, 4, 9, 10, 15.

## Filtering output

*journalctl* allows for the filtering of the output by specific fields. If there are many messages to display or filtering of large time span has to be done, the output of this command can be extensively delayed.

Examples:

*   Show all messages from this boot: `# journalctl -b` However, often one is interested in messages not from the current, but from the previous boot (e.g. if an unrecoverable system crash happened). This is possible through optional offset parameter of the `-b` flag: `journalctl -b -0` shows messages from the current boot, `journalctl -b -1` from the previous boot, `journalctl -b -2` from the second previous and so on – you can see the list of boots with their numbers by using `journalctl --list-boots`. See [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) for a full description; the semantics are more powerful than indicated here.
*   Show all messages from date (and optional time): `# journalctl --since="2012-10-30 18:17:16"` 
*   Show all messages since 20 minutes ago: `# journalctl --since "20 min ago"` 
*   Follow new messages: `# journalctl -f` 
*   Show all messages by a specific executable: `# journalctl /usr/lib/systemd/systemd` 
*   Show all messages by a specific process: `# journalctl _PID=1` 
*   Show all messages by a specific unit: `# journalctl -u man-db.service` 
*   Show kernel ring buffer: `# journalctl -k` 
*   Show only error, critical and alert priority messages: `# journalctl -p err..alert` You can use numeric log level too, like `journalctl -p 3..1`. If single number/log level is used, `journalctl -p 3`, then all higher priority log levels are also included (i.e. 0 to 3 in this case).
*   Show auth.log equivalent by filtering on syslog facility: `# journalctl SYSLOG_FACILITY=10` 
*   If the journal directory (by default located under `/var/log/journal`) contains a large amount of log data then `journalctl` can take several minutes to filter output. It can be sped up significantly by using `--file` option to force `journalctl` to look only into most recent journal: `# journalctl --file /var/log/journal/*/system.journal -f` 

See [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1), [systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7), or [Lennart Poettering's blog post](http://0pointer.de/blog/projects/journalctl.html) for details.

**Tip:** By default, *journalctl* truncates lines longer than screen width, but in some cases, it may be better to enable wrapping instead of truncating. This can be controlled by the `SYSTEMD_LESS` [environment variable](/index.php/Environment_variable "Environment variable"), which contains options passed to [less](/index.php/Core_utilities#Essentials "Core utilities") (the default pager) and defaults to `FRSXMK` (see [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) and [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) for details).

By omitting the `S` option, the output will be wrapped instead of truncated. For example, start *journalctl* as follows:

```
$ SYSTEMD_LESS=FRXMK journalctl

```
To set this behaviour as default, [export](/index.php/Environment_variables#Per_user "Environment variables") the variable from `~/.bashrc` or `~/.zshrc`.

**Tip:** While the journal is stored in a binary format, the content of stored messages is not modified. This means it is viewable with *strings*, for example for recovery in an environment which does not have *systemd* installed, e.g.: `$ strings /mnt/arch/var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i *message*` 

## Journal size limit

If the journal is persistent (non-volatile), its size limit is set to a default value of 10% of the size of the underlying file system but capped at 4 GiB. For example, with `/var/log/journal/` located on a 20 GiB partition, journal data may take up to 2 GiB. On a 50 GiB partition, it would max at 4 GiB.

The maximum size of the persistent journal can be controlled by uncommenting and changing the following:

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

It is also possible to use the drop-in snippets configuration override mechanism rather than editing the global configuration file. In this case, place the overrides under the `[Journal]` header:

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

[Restart](/index.php/Restart "Restart") the `systemd-journald.service` after changing this setting to apply the new limit.

See [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5) for more info.

## Clean journal files manually

Journal files can be globally removed from `/var/log/journal/` using *e.g.* `rm`, or can be trimmed according to various criteria using `journalctl`. For example:

*   Remove archived journal files until the disk space they use falls below 100M: `# journalctl --vacuum-size=100M` 
*   Make all journal files contain no data older than 2 weeks. `# journalctl --vacuum-time=2weeks` 

See [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) for more info.

## Journald in conjunction with syslog

Compatibility with a classic, non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") implementation can be provided by letting *systemd* forward all messages via the socket `/run/systemd/journal/syslog`. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)).

The default `journald.conf` for forwarding to the socket is `ForwardToSyslog=no` to avoid system overhead, because [rsyslog](/index.php/Rsyslog "Rsyslog") or [syslog-ng](/index.php/Syslog-ng "Syslog-ng") pull the messages from the journal by [itself](https://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

See [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") and [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), or [rsyslog](/index.php/Rsyslog "Rsyslog") respectively, for details on configuration.

## Forward journald to /dev/tty12

Create a [drop-in directory](/index.php/Systemd#Editing_provided_units "Systemd") `/etc/systemd/journald.conf.d` and create a `fw-tty12.conf` file in it:

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

Then [restart](/index.php/Restart "Restart") `systemd-journald.service`.

## Specify a different journal to view

There may be a need to check the logs of another system that is dead in the water, like booting from a live system to recover a production system. In such case, one can mount the disk in e.g. `/mnt`, and specify the journal path via `-D`/`--directory`, like so:

```
$ journalctl -D */mnt*/var/log/journal -xe

```