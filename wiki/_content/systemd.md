# systemd

From the [project web page](http://freedesktop.org/wiki/Software/systemd):

	_systemd_ is a system and service manager for Linux, compatible with SysV and LSB init scripts. systemd provides aggressive parallelization capabilities, uses socket and [D-Bus](/index.php/D-Bus "D-Bus") activation for starting services, offers on-demand starting of daemons, keeps track of processes using Linux [control groups](/index.php/Control_groups "Control groups"), supports snapshotting and restoring of the system state, maintains mount and automount points and implements an elaborate transactional dependency-based service control logic.

**Note:** For a detailed explanation as to why Arch has moved to _systemd_, see [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

## Contents

*   [1 Basic systemctl usage](#Basic_systemctl_usage)
    *   [1.1 Analyzing the system state](#Analyzing_the_system_state)
    *   [1.2 Using units](#Using_units)
    *   [1.3 Power management](#Power_management)
*   [2 Writing unit files](#Writing_unit_files)
    *   [2.1 Handling dependencies](#Handling_dependencies)
    *   [2.2 Service types](#Service_types)
    *   [2.3 Editing provided units](#Editing_provided_units)
        *   [2.3.1 Replacement unit files](#Replacement_unit_files)
        *   [2.3.2 Drop-in snippets](#Drop-in_snippets)
        *   [2.3.3 Examples](#Examples)
*   [3 Targets](#Targets)
    *   [3.1 Get current targets](#Get_current_targets)
    *   [3.2 Create custom target](#Create_custom_target)
    *   [3.3 Targets table](#Targets_table)
    *   [3.4 Change current target](#Change_current_target)
    *   [3.5 Change default target to boot into](#Change_default_target_to_boot_into)
*   [4 Temporary files](#Temporary_files)
*   [5 Timers](#Timers)
*   [6 Journal](#Journal)
    *   [6.1 Filtering output](#Filtering_output)
    *   [6.2 Journal size limit](#Journal_size_limit)
    *   [6.3 Clean journal files manually](#Clean_journal_files_manually)
    *   [6.4 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
    *   [6.5 Forward journald to /dev/tty12](#Forward_journald_to_.2Fdev.2Ftty12)
    *   [6.6 Specify a different journal to view](#Specify_a_different_journal_to_view)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Investigating systemd errors](#Investigating_systemd_errors)
    *   [7.2 Diagnosing boot problems](#Diagnosing_boot_problems)
    *   [7.3 Diagnosing problems with a specific service](#Diagnosing_problems_with_a_specific_service)
    *   [7.4 Shutdown/reboot takes terribly long](#Shutdown.2Freboot_takes_terribly_long)
    *   [7.5 Short lived processes do not seem to log any output](#Short_lived_processes_do_not_seem_to_log_any_output)
    *   [7.6 Disabling application crash dumps journaling](#Disabling_application_crash_dumps_journaling)
    *   [7.7 Boot time increasing over time](#Boot_time_increasing_over_time)
    *   [7.8 systemd-tmpfiles-setup.service fails to start at boot](#systemd-tmpfiles-setup.service_fails_to_start_at_boot)
    *   [7.9 systemctl enable fails for symlinks in /etc/systemd/system](#systemctl_enable_fails_for_symlinks_in_.2Fetc.2Fsystemd.2Fsystem)
*   [8 See also](#See_also)

## Basic systemctl usage

The main command used to introspect and control _systemd_ is _systemctl_. Some of its uses are examining the system state and managing the system and services. See `man systemctl` for more details.

**Tip:**

*   You can use all of the following _systemctl_ commands with the `-H _user_@_host_` switch to control a _systemd_ instance on a remote machine. This will use [SSH](/index.php/SSH "SSH") to connect to the remote _systemd_ instance.
*   _systemadm_ is the official graphical frontend for _systemctl_. It is provided by [systemd-ui](https://www.archlinux.org/packages/?name=systemd-ui) from the [official repositories](/index.php/Official_repositories "Official repositories") or by [systemd-ui-git](https://aur.archlinux.org/packages/systemd-ui-git/) from the [AUR](/index.php/AUR "AUR") for the development version.
*   [Plasma](/index.php/Plasma "Plasma") users can install [systemd-kcm](https://www.archlinux.org/packages/?name=systemd-kcm) as a graphical fronted for _systemctl_. After installing the module will be added under _System administration_.

### Analyzing the system state

Show **system status** using:

```
$ systemctl status

```

**List running** units:

```
$ systemctl

```

or:

```
$ systemctl list-units

```

**List failed** units:

```
$ systemctl --failed

```

The available unit files can be seen in `/usr/lib/systemd/system/` and `/etc/systemd/system/` (the latter takes precedence). **List installed** unit files with:

```
$ systemctl list-unit-files

```

### Using units

Units can be, for example, services (_.service_), mount points (_.mount_), devices (_.device_) or sockets (_.socket_).

When using _systemctl_, you generally have to specify the complete name of the unit file, including its suffix, for example `sshd.socket`. There are however a few short forms when specifying the unit in the following _systemctl_ commands:

*   If you do not specify the suffix, systemctl will assume _.service_. For example, `netctl` and `netctl.service` are equivalent.
*   Mount points will automatically be translated into the appropriate _.mount_ unit. For example, specifying `/home` is equivalent to `home.mount`.
*   Similar to mount points, devices are automatically translated into the appropriate _.device_ unit, therefore specifying `/dev/sda2` is equivalent to `dev-sda2.device`.

See `man systemd.unit` for details.

**Note:** Some unit names contain an `@` sign (e.g. `name@_string_.service`): this means that they are [instances](http://0pointer.de/blog/projects/instances.html) of a _template_ unit, whose actual file name does not contain the `_string_` part (e.g. `name@.service`). `_string_` is called the _instance identifier_, and is similar to an argument that is passed to the template unit when called with the _systemctl_ command: in the unit file it will substitute the `%i` specifier.

To be more accurate, _before_ trying to instantiate the `name@.suffix` template unit, _systemd_ will actually look for a unit with the exact `name@string.suffix` file name, although by convention such a "clash" happens rarely, i.e. most unit files containing an `@` sign are meant to be templates. Also, if a template unit is called without an instance identifier, it will just fail, since the `%i` specifier cannot be substituted.

**Tip:**

*   Most of the following commands also work if multiple units are specified, see `man systemctl` for more information.
*   Since [systemd 220](https://github.com/systemd/systemd/blob/master/NEWS#L323-L326), a `--now` switch can be used in conjunction with `enable`, `disable` and `mask` to respectively start, stop or mask immediately the unit rather than after the next boot.
*   A package may offer units for different purposes. If you just installed a package, `pacman -Qql _package_ | grep -Fe .service -e .socket` can be used to check and find them.

**Start** a unit immediately:

```
# systemctl start _unit_

```

**Stop** a unit immediately:

```
# systemctl stop _unit_

```

**Restart** a unit:

```
# systemctl restart _unit_

```

Ask a unit to **reload** its configuration:

```
# systemctl reload _unit_

```

Show the **status** of a unit, including whether it is running or not:

```
$ systemctl status _unit_

```

**Check** whether a unit is already enabled or not:

```
$ systemctl is-enabled _unit_

```

**Enable** a unit to be started on **bootup**:

```
# systemctl enable _unit_

```

**Disable** a unit to not start during bootup:

```
# systemctl disable _unit_

```

**Mask** a unit to make it impossible to start it:

```
# systemctl mask _unit_

```

**Unmask** a unit:

```
# systemctl unmask _unit_

```

Show the **manual page** associated with a unit (this has to be supported by the unit file):

```
$ systemctl help _unit_

```

Reload _systemd_, scanning for **new or changed units**:

```
# systemctl daemon-reload

```

### Power management

[polkit](/index.php/Polkit "Polkit") is necessary for power management as an unprivileged user. If you are in a local _systemd-logind_ user session and no other session is active, the following commands will work without root privileges. If not (for example, because another user is logged into a tty), _systemd_ will automatically ask you for the root password.

Shut down and reboot the system:

```
$ systemctl reboot

```

Shut down and power-off the system:

```
$ systemctl poweroff

```

Suspend the system:

```
$ systemctl suspend

```

Put the system into hibernation:

```
$ systemctl hibernate

```

Put the system into hybrid-sleep state (or suspend-to-both):

```
$ systemctl hybrid-sleep

```

## Writing unit files

The syntax of _systemd'_s [unit files](http://www.freedesktop.org/software/systemd/man/systemd.unit.html) is inspired by XDG Desktop Entry Specification _.desktop_ files, which are in turn inspired by Microsoft Windows _.ini_ files. Unit files are loaded from two locations. From lowest to highest precedence they are:

*   `/usr/lib/systemd/system/`: units provided by installed packages
*   `/etc/systemd/system/`: units installed by the system administrator

**Note:**

*   The load paths are completely different when running _systemd_ in [user mode](/index.php/Systemd/User#How_it_works "Systemd/User").
*   systemd unit names may only contain ASCII alphanumeric characters, underscores and periods. All other characters must be replaced by C-style "\x2d" escapes. See `man systemd.unit` and `man systemd-escape` for more information.

Look at the units installed by your packages for examples, as well as the [annotated example section](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples) of `man systemd.service`.

**Tip:** Comments prepended with `#` may be used in unit-files as well, but only in new lines. Do not use end-line comments after _systemd_ parameters or the unit will fail to activate.

### Handling dependencies

With _systemd_, dependencies can be resolved by designing the unit files correctly. The most typical case is that the unit _A_ requires the unit _B_ to be running before _A_ is started. In that case add `Requires=_B_` and `After=_B_` to the `[Unit]` section of _A_. If the dependency is optional, add `Wants=_B_` and `After=_B_` instead. Note that `Wants=` and `Requires=` do not imply `After=`, meaning that if `After=` is not specified, the two units will be started in parallel.

Dependencies are typically placed on services and not on targets. For example, `network.target` is pulled in by whatever service configures your network interfaces, therefore ordering your custom unit after it is sufficient since `network.target` is started anyway.

### Service types

There are several different start-up types to consider when writing a custom service file. This is set with the `Type=` parameter in the `[Service]` section:

*   `Type=simple` (default): _systemd_ considers the service to be started up immediately. The process must not fork. Do not use this type if other services need to be ordered on this service, unless it is socket activated.
*   `Type=forking`: _systemd_ considers the service started up once the process forks and the parent has exited. For classic daemons use this type unless you know that it is not necessary. You should specify `PIDFile=` as well so _systemd_ can keep track of the main process.
*   `Type=oneshot`: this is useful for scripts that do a single job and then exit. You may want to set `RemainAfterExit=yes` as well so that _systemd_ still considers the service as active after the process has exited.
*   `Type=notify`: identical to `Type=simple`, but with the stipulation that the daemon will send a signal to _systemd_ when it is ready. The reference implementation for this notification is provided by _libsystemd-daemon.so_.
*   `Type=dbus`: the service is considered ready when the specified `BusName` appears on DBus's system bus.
*   `Type=idle`: _systemd_ will delay execution of the service binary until all jobs are dispatched. Other than that behavior is very similar to `Type=simple`.

See the [systemd.service(5)](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=) man page for a more detailed explanation of the `Type` values.

### Editing provided units

To avoid conflicts with pacman, unit files provided by packages should not be directly edited. There are two safe ways to modify a unit without touching the original file: create a new unit file which overwrites the original unit or create drop-in snippets which are applied on top of the original unit. For both methods, you must reload the unit afterwards to apply your changes. This can be done either by editing the unit with `systemctl edit` (which reloads the unit automatically) or by reloading all units with:

```
# systemctl daemon-reload

```

**Tip:**

*   You can use _systemd-delta_ to see which unit files have been overridden or extended and what exactly has been changed.
*   Use `systemctl cat _unit_` to view the content of a unit file and all associated drop-in snippets.
*   Syntax highlighting for _systemd_ unit files within [Vim](/index.php/Vim "Vim") can be enabled by installing [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd).

#### Replacement unit files

To replace the unit file `/usr/lib/systemd/system/_unit_`, create the file `/etc/systemd/system/_unit_` and reenable the unit to update the symlinks:

```
# systemctl reenable _unit_

```

Alternatively, run:

```
# systemctl edit --full _unit_

```

This opens `/etc/systemd/system/_unit_` in your editor (copying the installed version if it does not exist yet) and automatically reloads it when you finish editing.

**Note:** Pacman does not update the replacement unit files when the originals are updated, so this method can make system maintenance more difficult. For this reason the next approach is recommended.

#### Drop-in snippets

To create drop-in snippets for the unit file `/usr/lib/systemd/system/_unit_`, create the directory `/etc/systemd/system/_unit_.d/` and place _.conf_ files there to override or add new options. _systemd_ will parse these _.conf_ files and apply them on top of the original unit.

The easiest way to do this is to run:

```
# systemctl edit _unit_

```

This opens the file `/etc/systemd/system/_unit_.d/override.conf` in your text editor (creating it if necessary) and automatically reloads the unit when you are done editing.

#### Examples

For example, if you simply want to add an additional dependency to a unit, you may create the following file:

 `/etc/systemd/system/_unit_.d/customdependency.conf` 

```
[Unit]
Requires=_new dependency_
After=_new dependency_
```

As another example, in order to replace the `ExecStart` directive for a unit that is not of type `oneshot`, create the following file:

 `/etc/systemd/system/_unit_.d/customexec.conf` 

```
[Service]
ExecStart=
ExecStart=_new command_
```

Note how `ExecStart` must be cleared before being re-assigned ([[1]](https://bugzilla.redhat.com/show_bug.cgi?id=756787#c9)).

One more example to automatically restart a service:

 `/etc/systemd/system/_unit_.d/restart.conf` 

```
[Service]
Restart=always
RestartSec=30
```

## Targets

_systemd_ uses _targets_ which serve a similar purpose as runlevels but act a little different. Each _target_ is named instead of numbered and is intended to serve a specific purpose with the possibility of having multiple ones active at the same time. Some _target_s are implemented by inheriting all of the services of another _target_ and adding additional services to it. There are _systemd_ _target_s that mimic the common SystemVinit runlevels so you can still switch _target_s using the familiar `telinit RUNLEVEL` command.

### Get current targets

The following should be used under _systemd_ instead of running `runlevel`:

```
$ systemctl list-units --type=target

```

### Create custom target

The runlevels that held a defined meaning under sysvinit (i.e., 0, 1, 3, 5, and 6); have a 1:1 mapping with a specific _systemd_ _target_. Unfortunately, there is no good way to do the same for the user-defined runlevels like 2 and 4\. If you make use of those it is suggested that you make a new named _systemd_ _target_ as `/etc/systemd/system/_your target_` that takes one of the existing runlevels as a base (you can look at `/usr/lib/systemd/system/graphical.target` as an example), make a directory `/etc/systemd/system/_your target_.wants`, and then symlink the additional services from `/usr/lib/systemd/system/` that you wish to enable.

### Targets table

| SysV Runlevel | systemd Target | Notes |
| 0 | runlevel0.target, poweroff.target | Halt the system. |
| 1, s, single | runlevel1.target, rescue.target | Single user mode. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | User-defined/Site-specific runlevels. By default, identical to 3. |
| 3 | runlevel3.target, multi-user.target | Multi-user, non-graphical. Users can usually login via multiple consoles or via the network. |
| 5 | runlevel5.target, graphical.target | Multi-user, graphical. Usually has all the services of runlevel 3 plus a graphical login. |
| 6 | runlevel6.target, reboot.target | Reboot |
| emergency | emergency.target | Emergency shell |

### Change current target

In _systemd_ targets are exposed via _target units_. You can change them like this:

```
# systemctl isolate graphical.target

```

This will only change the current target, and has no effect on the next boot. This is equivalent to commands such as `telinit 3` or `telinit 5` in Sysvinit.

### Change default target to boot into

The standard target is `default.target`, which is aliased by default to `graphical.target` (which roughly corresponds to the old runlevel 5). To change the default target at boot-time, append one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to your bootloader:

*   `systemd.unit=multi-user.target` (which roughly corresponds to the old runlevel 3),
*   `systemd.unit=rescue.target` (which roughly corresponds to the old runlevel 1).

Alternatively, you may leave the bootloader alone and change `default.target`. This can be done using _systemctl_:

```
# systemctl set-default multi-user.target

```

To be able to override the previously set `default.target`, use the force option:

```
# systemctl set-default -f multi-user.target

```

The effect of this command is output by _systemctl_; a symlink to the new default target is made at `/etc/systemd/system/default.target`.

## Temporary files

"_systemd-tmpfiles_ creates, deletes and cleans up volatile and temporary files and directories." It reads configuration files in `/etc/tmpfiles.d/` and `/usr/lib/tmpfiles.d/` to discover which actions to perform. Configuration files in the former directory take precedence over those in the latter directory.

Configuration files are usually provided together with service files, and they are named in the style of `/usr/lib/tmpfiles.d/_program_.conf`. For example, the [Samba](/index.php/Samba "Samba") daemon expects the directory `/run/samba` to exist and to have the correct permissions. Therefore, the [samba](https://www.archlinux.org/packages/?name=samba) package ships with this configuration:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

Configuration files may also be used to write values into certain files on boot. For example, if you used `/etc/rc.local` to disable wakeup from USB devices with `echo USBE > /proc/acpi/wakeup`, you may use the following tmpfile instead:

 `/etc/tmpfiles.d/disable-usb-wake.conf`  `w /proc/acpi/wakeup - - - - USBE` 

See the `systemd-tmpfiles(8)` and `tmpfiles.d(5)` man pages for details.

**Note:** This method may not work to set options in `/sys` since the _systemd-tmpfiles-setup_ service may run before the appropriate device modules is loaded. In this case you could check whether the module has a parameter for the option you want to set with `modinfo _module_` and set this option with a [config file in /etc/modprobe.d](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Otherwise you will have to write a [udev rule](/index.php/Udev#About_udev_rules "Udev") to set the appropriate attribute as soon as the device appears.

## Timers

A timer is a unit configuration file whose name ends with _.timer_ and encodes information about a timer controlled and supervised by _systemd_, for timer-based activation. See [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

**Note:** Timers can replace _cron_ functionality to a great extent. See [systemd/Timers#As a cron replacement](/index.php/Systemd/Timers#As_a_cron_replacement "Systemd/Timers").

## Journal

_systemd_ has its own logging system called the journal; therefore, running a `syslog` daemon is no longer required. To read the log, use:

```
# journalctl

```

In Arch Linux, the directory `/var/log/journal/` is a part of the [systemd](https://www.archlinux.org/packages/?name=systemd) package, and the journal (when `Storage=` is set to `auto` in `/etc/systemd/journald.conf`) will write to `/var/log/journal/`. If you or some program delete that directory, _systemd_ will **not** recreate it automatically and instead will write its logs to `/run/systemd/journal` in a nonpersistent way. However, the folder will be recreated when you set `Storage=persistent` and run `systemctl restart systemd-journald` (or reboot).

### Filtering output

_journalctl_ allows you to filter the output by specific fields. Be aware that if there are many messages to display or filtering of large time span has to be done, the output of this command can be delayed for quite some time.

**Tip:** While the journal is stored in a binary format, the content of stored messages is not modified. This means it is viewable with _strings_, for example for recovery in an environment which does not have _systemd_ installed. Example command: `$ strings /mnt/arch/var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i _message_` 

Examples:

*   Show all messages from this boot: `# journalctl -b` However, often one is interested in messages not from the current, but from the previous boot (e.g. if an unrecoverable system crash happened). This is possible through optional offset parameter of the `-b` flag: `journalctl -b -0` shows messages from the current boot, `journalctl -b -1` from the previous boot, `journalctl -b -2` from the second previous and so on. See `man 1 journalctl` for full description, the semantics is much more powerful.
*   Show all messages from date (and optional time): `# journalctl --since="2012-10-30 18:17:16"` 
*   Show all messages since 20 minutes ago: `# journalctl --since "20 min ago"` 
*   Follow new messages: `# journalctl -f` 
*   Show all messages by a specific executable: `# journalctl /usr/lib/systemd/systemd` 
*   Show all messages by a specific process: `# journalctl _PID=1` 
*   Show all messages by a specific unit: `# journalctl -u netcfg` 
*   Show kernel ring buffer: `# journalctl -k` 
*   Show auth.log equivalent by filtering on syslog facility: `# journalctl -f -l SYSLOG_FACILITY=10` 

See `man 1 journalctl`, `man 7 systemd.journal-fields`, or Lennart's [blog post](http://0pointer.de/blog/projects/journalctl.html) for details.

**Tip:** By default, _journalctl_ truncates lines longer than screen width, but in some cases, it may be better to enable wrapping instead of truncating. This can be controlled by the `SYSTEMD_LESS` [environment variable](/index.php/Environment_variable "Environment variable"), which contains options passed to [less](/index.php/Core_utilities#less "Core utilities") (the default pager) and defaults to `FRSXMK` (see `man 1 less` and `man 1 journalctl` for details).

By omitting the `S` option, the output will be wrapped instead of truncated. For example, start _journalctl_ as follows:

```
$ SYSTEMD_LESS=FRXMK journalctl

```

If you would like to set this behaviour as default, [export](/index.php/Environment_variables#Per_user "Environment variables") the variable from `~/.bashrc` or `~/.zshrc`.

### Journal size limit

If the journal is persistent (non-volatile), its size limit is set to a default value of 10% of the size of the respective file system. For example, with `/var/log/journal` located on a 50 GiB root partition this would lead to 5 GiB of journal data. The maximum size of the persistent journal can be controlled by uncommenting and changing the following:

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

Refer to `man journald.conf` for more info.

### Clean journal files manually

The journal files are located under `/var/log/journal`, `rm` will do the work. Or, use `journalctl`,

Examples:

*   Remove archived journal files until the disk space they use falls below 100M: `# journalctl --vacuum-size=100M` 
*   Make all journal files contain no data older than 2 weeks. `# journalctl --vacuum-time=2weeks` 

Refer to `man journalctl` for more info.

### Journald in conjunction with syslog

Compatibility with a classic, non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") implementation can be provided by letting _systemd_ forward all messages via the socket `/run/systemd/journal/syslog`. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)).

As of _systemd_ 216 the default `journald.conf` for forwarding to the socket was changed to `ForwardToSyslog=no` to avoid system overhead, because [rsyslog](/index.php/Rsyslog "Rsyslog") or [syslog-ng](/index.php/Syslog-ng "Syslog-ng") (since 3.6) pull the messages from the journal by [itself](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

See [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") and [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), or [rsyslog](/index.php/Rsyslog "Rsyslog") respectively, for details on configuration.

### Forward journald to /dev/tty12

Create a [drop-in directory](#Editing_provided_units) `/etc/systemd/journald.conf.d` and create a `fw-tty12.conf` file in it:

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 

```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

Then [restart](/index.php/Restart "Restart") systemd-journald.

### Specify a different journal to view

There may be a need to check the logs of another system that is dead in the water, like booting from a live system to recover a production system. In such case, one can mount the disk in e.g. `/mnt`, and specify the journal path via `-D`/`--directory`, like so:

```
$ journalctl -D _/mnt_/var/log/journal -xe

```

## Troubleshooting

### Investigating systemd errors

As an example, we will investigate an error with `systemd-modules-load` service:

**1.** Lets find the _systemd_ services which fail to start:

 `$ systemctl --failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

**2.** Ok, we found a problem with `systemd-modules-load` service. We want to know more:

 `$ systemctl status systemd-modules-load` 

```
systemd-modules-load.service - Load Kernel Modules
   Loaded: loaded (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **failed** (Result: exit-code) since So 2013-08-25 11:48:13 CEST; 32s ago
     Docs: man:systemd-modules-load.service(8).
           man:modules-load.d(5)
  Process: **15630** ExecStart=/usr/lib/systemd/systemd-modules-load (**code=exited, status=1/FAILURE**)
```

If the `Process ID` is not listed, just restart the failed service with `systemctl restart systemd-modules-load`

**3.** Now we have the process id (PID) to investigate this error in depth. Enter the following command with the current `Process ID` (here: 15630):

 `$ journalctl _PID=15630` 

```
-- Logs begin at Sa 2013-05-25 10:31:12 CEST, end at So 2013-08-25 11:51:17 CEST. --
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'blacklist usblp'**
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'install usblp /bin/false'**
```

**4.** We see that some of the kernel module configs have wrong settings. Therefore we have a look at these settings in `/etc/modules-load.d/`:

 `$ ls -Al /etc/modules-load.d/` 

```
...
-rw-r--r--   1 root root    79  1\. Dez 2012  blacklist.conf
-rw-r--r--   1 root root     1  2\. Mär 14:30 encrypt.conf
-rw-r--r--   1 root root     3  5\. Dez 2012  printing.conf
-rw-r--r--   1 root root     6 14\. Jul 11:01 realtek.conf
-rw-r--r--   1 root root    65  2\. Jun 23:01 virtualbox.conf
...

```

**5.** The `Failed to find module 'blacklist usblp'` error message might be related to a wrong setting inside of `blacklist.conf`. Lets deactivate it with inserting a trailing **#** before each option we found via step 3:

 `/etc/modules-load.d/blacklist.conf` 

```
**#** blacklist usblp
**#** install usblp /bin/false

```

**6.** Now, try to start `systemd-modules-load`:

```
$ systemctl start systemd-modules-load

```

If it was successful, this should not prompt anything. If you see any error, go back to step 3 and use the new PID for solving the errors left.

If everything is ok, you can verify that the service was started successfully with:

 `$ systemctl status systemd-modules-load` 

```
systemd-modules-load.service - Load Kernel Modules
   Loaded: **loaded** (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **active (exited)** since So 2013-08-25 12:22:31 CEST; 34s ago
     Docs: man:systemd-modules-load.service(8)
           man:modules-load.d(5)
 Process: 19005 ExecStart=/usr/lib/systemd/systemd-modules-load (code=exited, status=0/SUCCESS)
Aug 25 12:22:31 mypc systemd[1]: **Started Load Kernel Modules**.
```

Often you can solve these kind of problems like shown above. For further investigation look at [#Diagnosing boot problems](#Diagnosing_boot_problems).

### Diagnosing boot problems

_systemd_ has several options for diagnosing problems with the boot process. See [boot debugging](/index.php/Boot_debugging "Boot debugging") and the [systemd debugging documentation](http://freedesktop.org/wiki/Software/systemd/Debugging/).

### Diagnosing problems with a specific service

If some _systemd_ service misbehaves and you want to get more information about what is going on, set the `SYSTEMD_LOG_LEVEL` [environment variable](/index.php/Environment_variable "Environment variable") to `debug`. For example, to run the _systemd-networkd_ daemon in debug mode:

```
# systemctl stop systemd-networkd
# SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

```

Or, equivalently, modify the service file temporarily for gathering enough output. For example:

 `/usr/lib/systemd/system/systemd-networkd.service` 

```
[Service]
...
Environment=SYSTEMD_LOG_LEVEL=debug
....
```

If debug information is required long-term, add the variable the [regular](#Editing_provided_units) way.

### Shutdown/reboot takes terribly long

If the shutdown process takes a very long time (or seems to freeze) most likely a service not exiting is to blame. _systemd_ waits some time for each service to exit before trying to kill it. To find out if you are affected, see [this article](http://freedesktop.org/wiki/Software/systemd/Debugging/#shutdowncompleteseventually).

### Short lived processes do not seem to log any output

If `journalctl -u foounit` does not show any output for a short lived service, look at the PID instead. For example, if `systemd-modules-load.service` fails, and `systemctl status systemd-modules-load` shows that it ran as PID 123, then you might be able to see output in the journal for that PID, i.e. `journalctl -b _PID=123`. Metadata fields for the journal such as `_SYSTEMD_UNIT` and `_COMM` are collected asynchronously and rely on the `/proc` directory for the process existing. Fixing this requires fixing the kernel to provide this data via a socket connection, similar to `SCM_CREDENTIALS`.

### Disabling application crash dumps journaling

Edit the file `/etc/systemd/coredump.conf` by adding this line:

```
 Storage=none

```

and run:

```
# systemctl daemon-reload

```

to reload the configuration.

### Boot time increasing over time

After using `systemd-analyze` a number of users have noticed that their boot time has increased significantly in comparison with what it used to be. After using `systemd-analyze blame` [NetworkManager](/index.php/NetworkManager "NetworkManager") is being reported as taking an unusually large amount of time to start.

The problem for some users has been due to `/var/log/journal` becoming too large. This may have other impacts on performance, such as for `systemctl status` or `journalctl`. As such the solution is to remove every file within the folder (ideally making a backup of it somewhere, at least temporarily) and then setting a journal file size limit as described in [#Journal size limit](#Journal_size_limit).

### systemd-tmpfiles-setup.service fails to start at boot

Starting with systemd 219, `/usr/lib/tmpfiles.d/systemd.conf` specifies ACL attributes for directories under `/var/log/journal` and, therefore, requires ACL support to be enabled for the filesystem the journal resides on.

See [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") for instructions on how to enable ACL on the filesystem that houses `/var/log/journal`.

### systemctl enable fails for symlinks in /etc/systemd/system

If `/etc/systemd/system/_foo_.service` is a symlink and `systemctl enable _foo_.service` is run, it will fail with this error:

```
Failed to issue method call: No such file or directory

```

This is a [design choice](https://bugzilla.redhat.com/show_bug.cgi?id=955379#c14) of systemd. As a workaround, enabling by absolute path works:

```
# systemctl enable _/absolute/path/foo_.service

```

## See also

*   [Official web site](http://www.freedesktop.org/wiki/Software/systemd)
*   [Wikipedia article](https://en.wikipedia.org/wiki/systemd "wikipedia:systemd")
*   [Manual pages](http://0pointer.de/public/systemd-man/)
*   [systemd optimizations](http://freedesktop.org/wiki/Software/systemd/Optimizations)
*   [FAQ](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [Tips and tricks](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [About systemd on Fedora Project](http://fedoraproject.org/wiki/Systemd)
*   [How to debug systemd problems](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in _The H Open_ magazine.
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html)
*   [Status update](http://0pointer.de/blog/projects/systemd-update.html)
*   [Status update2](http://0pointer.de/blog/projects/systemd-update-2.html)
*   [Status update3](http://0pointer.de/blog/projects/systemd-update-3.html)
*   [Most recent summary](http://0pointer.de/blog/projects/why.html)
*   [Fedora's SysVinit to systemd cheatsheet](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)
*   [Gentoo Wiki systemd page](http://wiki.gentoo.org/wiki/Systemd)
*   [Emacs Syntax highlighting for Systemd files](/index.php/Emacs#Syntax_highlighting_for_systemd_Files "Emacs")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd&oldid=417725](https://wiki.archlinux.org/index.php?title=Systemd&oldid=417725)"