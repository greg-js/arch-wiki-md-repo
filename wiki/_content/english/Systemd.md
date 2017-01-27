From the [project web page](http://freedesktop.org/wiki/Software/systemd):

	*systemd* is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system. systemd provides aggressive parallelization capabilities, uses socket and [D-Bus](/index.php/D-Bus "D-Bus") activation for starting services, offers on-demand starting of daemons, keeps track of processes using Linux [control groups](/index.php/Control_groups "Control groups"), maintains mount and automount points, and implements an elaborate transactional dependency-based service control logic. *systemd* supports SysV and LSB init scripts and works as a replacement for sysvinit. Other parts include a logging daemon, utilities to control basic system configuration like the hostname, date, locale, maintain a list of logged-in users and running containers and virtual machines, system accounts, runtime directories and settings, and daemons to manage simple network configuration, network time synchronization, log forwarding, and name resolution.

**Note:** For a detailed explanation as to why Arch has moved to *systemd*, see [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

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
        *   [2.3.2 Drop-in files](#Drop-in_files)
        *   [2.3.3 Examples](#Examples)
*   [3 Targets](#Targets)
    *   [3.1 Get current targets](#Get_current_targets)
    *   [3.2 Create custom target](#Create_custom_target)
    *   [3.3 Targets table](#Targets_table)
    *   [3.4 Change current target](#Change_current_target)
    *   [3.5 Change default target to boot into](#Change_default_target_to_boot_into)
*   [4 Temporary files](#Temporary_files)
*   [5 Timers](#Timers)
*   [6 Mounting](#Mounting)
*   [7 Journal](#Journal)
    *   [7.1 Priority level](#Priority_level)
    *   [7.2 Facility](#Facility)
    *   [7.3 Filtering output](#Filtering_output)
    *   [7.4 Journal size limit](#Journal_size_limit)
    *   [7.5 Clean journal files manually](#Clean_journal_files_manually)
    *   [7.6 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
    *   [7.7 Forward journald to /dev/tty12](#Forward_journald_to_.2Fdev.2Ftty12)
    *   [7.8 Specify a different journal to view](#Specify_a_different_journal_to_view)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Enable installed units by default](#Enable_installed_units_by_default)
    *   [8.2 Sandboxing application environments](#Sandboxing_application_environments)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Investigating systemd errors](#Investigating_systemd_errors)
    *   [9.2 Diagnosing boot problems](#Diagnosing_boot_problems)
    *   [9.3 Diagnosing problems with a specific service](#Diagnosing_problems_with_a_specific_service)
    *   [9.4 Shutdown/reboot takes terribly long](#Shutdown.2Freboot_takes_terribly_long)
    *   [9.5 Short lived processes do not seem to log any output](#Short_lived_processes_do_not_seem_to_log_any_output)
    *   [9.6 Boot time increasing over time](#Boot_time_increasing_over_time)
    *   [9.7 systemd-tmpfiles-setup.service fails to start at boot](#systemd-tmpfiles-setup.service_fails_to_start_at_boot)
    *   [9.8 systemctl enable fails for symlinks in /etc/systemd/system](#systemctl_enable_fails_for_symlinks_in_.2Fetc.2Fsystemd.2Fsystem)
    *   [9.9 dependent services are not started when starting a service manually](#dependent_services_are_not_started_when_starting_a_service_manually)
    *   [9.10 systemd version printed on boot is not the same as installed package version](#systemd_version_printed_on_boot_is_not_the_same_as_installed_package_version)
*   [10 See also](#See_also)

## Basic systemctl usage

The main command used to introspect and control *systemd* is *systemctl*. Some of its uses are examining the system state and managing the system and services. See `man systemctl` for more details.

**Tip:**

*   You can use all of the following *systemctl* commands with the `-H *user*@*host*` switch to control a *systemd* instance on a remote machine. This will use [SSH](/index.php/SSH "SSH") to connect to the remote *systemd* instance.
*   *systemadm* is the official graphical frontend for *systemctl* and is provided by the [systemd-ui](https://www.archlinux.org/packages/?name=systemd-ui) package.
*   [Plasma](/index.php/Plasma "Plasma") users can install [systemd-kcm](https://www.archlinux.org/packages/?name=systemd-kcm) as a graphical fronted for *systemctl*. After installing the module will be added under *System administration*.

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

Units can be, for example, services (*.service*), mount points (*.mount*), devices (*.device*) or sockets (*.socket*).

When using *systemctl*, you generally have to specify the complete name of the unit file, including its suffix, for example `sshd.socket`. There are however a few short forms when specifying the unit in the following *systemctl* commands:

*   If you do not specify the suffix, systemctl will assume *.service*. For example, `netctl` and `netctl.service` are equivalent.
*   Mount points will automatically be translated into the appropriate *.mount* unit. For example, specifying `/home` is equivalent to `home.mount`.
*   Similar to mount points, devices are automatically translated into the appropriate *.device* unit, therefore specifying `/dev/sda2` is equivalent to `dev-sda2.device`.

See `man systemd.unit` for details.

**Note:** Some unit names contain an `@` sign (e.g. `name@*string*.service`): this means that they are [instances](http://0pointer.de/blog/projects/instances.html) of a *template* unit, whose actual file name does not contain the `*string*` part (e.g. `name@.service`). `*string*` is called the *instance identifier*, and is similar to an argument that is passed to the template unit when called with the *systemctl* command: in the unit file it will substitute the `%i` specifier.

To be more accurate, *before* trying to instantiate the `name@.suffix` template unit, *systemd* will actually look for a unit with the exact `name@string.suffix` file name, although by convention such a "clash" happens rarely, i.e. most unit files containing an `@` sign are meant to be templates. Also, if a template unit is called without an instance identifier, it will just fail, since the `%i` specifier cannot be substituted.

**Tip:**

*   Most of the following commands also work if multiple units are specified, see `man systemctl` for more information.
*   The `--now` switch can be used in conjunction with `enable`, `disable`, and `mask` to respectively start, stop, or mask immediately the unit rather than after the next boot.
*   A package may offer units for different purposes. If you just installed a package, `pacman -Qql *package* | grep -Fe .service -e .socket` can be used to check and find them.

**Start** a unit immediately:

```
# systemctl start *unit*

```

**Stop** a unit immediately:

```
# systemctl stop *unit*

```

**Restart** a unit:

```
# systemctl restart *unit*

```

Ask a unit to **reload** its configuration:

```
# systemctl reload *unit*

```

Show the **status** of a unit, including whether it is running or not:

```
$ systemctl status *unit*

```

**Check** whether a unit is already enabled or not:

```
$ systemctl is-enabled *unit*

```

**Enable** a unit to be started on **bootup**:

```
# systemctl enable *unit*

```

**Disable** a unit to not start during bootup:

```
# systemctl disable *unit*

```

**Mask** a unit to make it impossible to start it:

```
# systemctl mask *unit*

```

**Unmask** a unit:

```
# systemctl unmask *unit*

```

Show the **manual page** associated with a unit (this has to be supported by the unit file):

```
$ systemctl help *unit*

```

Reload *systemd*, scanning for **new or changed units**:

```
# systemctl daemon-reload

```

### Power management

[polkit](/index.php/Polkit "Polkit") is necessary for power management as an unprivileged user. If you are in a local *systemd-logind* user session and no other session is active, the following commands will work without root privileges. If not (for example, because another user is logged into a tty), *systemd* will automatically ask you for the root password.

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

The syntax of *systemd'*s [unit files](http://www.freedesktop.org/software/systemd/man/systemd.unit.html) is inspired by XDG Desktop Entry Specification *.desktop* files, which are in turn inspired by Microsoft Windows *.ini* files. Unit files are loaded from two locations. From lowest to highest precedence they are:

*   `/usr/lib/systemd/system/`: units provided by installed packages
*   `/etc/systemd/system/`: units installed by the system administrator

**Note:**

*   The load paths are completely different when running *systemd* in [user mode](/index.php/Systemd/User#How_it_works "Systemd/User").
*   systemd unit names may only contain ASCII alphanumeric characters, underscores and periods. All other characters must be replaced by C-style "\x2d" escapes. See `man systemd.unit` and `man systemd-escape` for more information.

Look at the units installed by your packages for examples, as well as the [annotated example section](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples) of `man systemd.service`.

**Tip:** Comments prepended with `#` may be used in unit-files as well, but only in new lines. Do not use end-line comments after *systemd* parameters or the unit will fail to activate.

### Handling dependencies

With *systemd*, dependencies can be resolved by designing the unit files correctly. The most typical case is that the unit *A* requires the unit *B* to be running before *A* is started. In that case add `Requires=*B*` and `After=*B*` to the `[Unit]` section of *A*. If the dependency is optional, add `Wants=*B*` and `After=*B*` instead. Note that `Wants=` and `Requires=` do not imply `After=`, meaning that if `After=` is not specified, the two units will be started in parallel.

Dependencies are typically placed on services and not on targets. For example, `network.target` is pulled in by whatever service configures your network interfaces, therefore ordering your custom unit after it is sufficient since `network.target` is started anyway.

### Service types

There are several different start-up types to consider when writing a custom service file. This is set with the `Type=` parameter in the `[Service]` section:

*   `Type=simple` (default): *systemd* considers the service to be started up immediately. The process must not fork. Do not use this type if other services need to be ordered on this service, unless it is socket activated.
*   `Type=forking`: *systemd* considers the service started up once the process forks and the parent has exited. For classic daemons use this type unless you know that it is not necessary. You should specify `PIDFile=` as well so *systemd* can keep track of the main process.
*   `Type=oneshot`: this is useful for scripts that do a single job and then exit. You may want to set `RemainAfterExit=yes` as well so that *systemd* still considers the service as active after the process has exited.
*   `Type=notify`: identical to `Type=simple`, but with the stipulation that the daemon will send a signal to *systemd* when it is ready. The reference implementation for this notification is provided by *libsystemd-daemon.so*.
*   `Type=dbus`: the service is considered ready when the specified `BusName` appears on DBus's system bus.
*   `Type=idle`: *systemd* will delay execution of the service binary until all jobs are dispatched. Other than that behavior is very similar to `Type=simple`.

See the [systemd.service(5)](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=) man page for a more detailed explanation of the `Type` values.

### Editing provided units

To avoid conflicts with pacman, unit files provided by packages should not be directly edited. There are two safe ways to modify a unit without touching the original file: create a new unit file which overrides the original unit or create drop-in snippets which are applied on top of the original unit. For both methods, you must reload the unit afterwards to apply your changes. This can be done either by editing the unit with `systemctl edit` (which reloads the unit automatically) or by reloading all units with:

```
# systemctl daemon-reload

```

**Tip:**

*   You can use *systemd-delta* to see which unit files have been overridden or extended and what exactly has been changed.
*   Use `systemctl cat *unit*` to view the content of a unit file and all associated drop-in snippets.
*   Syntax highlighting for *systemd* unit files within [Vim](/index.php/Vim "Vim") can be enabled by installing [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd).

#### Replacement unit files

To replace the unit file `/usr/lib/systemd/system/*unit*`, create the file `/etc/systemd/system/*unit*` and reenable the unit to update the symlinks:

```
# systemctl reenable *unit*

```

Alternatively, run:

```
# systemctl edit --full *unit*

```

This opens `/etc/systemd/system/*unit*` in your editor (copying the installed version if it does not exist yet) and automatically reloads it when you finish editing.

**Note:** Pacman does not update the replacement unit files when the originals are updated, so this method can make system maintenance more difficult. For this reason the next approach is recommended.

#### Drop-in files

To create drop-in files for the unit file `/usr/lib/systemd/system/*unit*`, create the directory `/etc/systemd/system/*unit*.d/` and place *.conf* files there to override or add new options. *systemd* will parse these *.conf* files and apply them on top of the original unit.

The easiest way to do this is to run:

```
# systemctl edit *unit*

```

This opens the file `/etc/systemd/system/*unit*.d/override.conf` in your text editor (creating it if necessary) and automatically reloads the unit when you are done editing.

#### Examples

For example, if you simply want to add an additional dependency to a unit, you may create the following file:

 `/etc/systemd/system/*unit*.d/customdependency.conf` 
```
[Unit]
Requires=*new dependency*
After=*new dependency*
```

As another example, in order to replace the `ExecStart` directive for a unit that is not of type `oneshot`, create the following file:

 `/etc/systemd/system/*unit*.d/customexec.conf` 
```
[Service]
ExecStart=
ExecStart=*new command*
```

Note how `ExecStart` must be cleared before being re-assigned [[1]](https://bugzilla.redhat.com/show_bug.cgi?id=756787#c9). The same holds for every item that can be specified multiple times, e.g. `OnCalendar` for timers.

One more example to automatically restart a service:

 `/etc/systemd/system/*unit*.d/restart.conf` 
```
[Service]
Restart=always
RestartSec=30
```

## Targets

*systemd* uses *targets* which serve a similar purpose as runlevels but act a little different. Each *target* is named instead of numbered and is intended to serve a specific purpose with the possibility of having multiple ones active at the same time. Some *target*s are implemented by inheriting all of the services of another *target* and adding additional services to it. There are *systemd* *target*s that mimic the common SystemVinit runlevels so you can still switch *target*s using the familiar `telinit RUNLEVEL` command.

### Get current targets

The following should be used under *systemd* instead of running `runlevel`:

```
$ systemctl list-units --type=target

```

### Create custom target

The runlevels that held a defined meaning under sysvinit (i.e., 0, 1, 3, 5, and 6); have a 1:1 mapping with a specific *systemd* *target*. Unfortunately, there is no good way to do the same for the user-defined runlevels like 2 and 4\. If you make use of those it is suggested that you make a new named *systemd* *target* as `/etc/systemd/system/*your target*` that takes one of the existing runlevels as a base (you can look at `/usr/lib/systemd/system/graphical.target` as an example), make a directory `/etc/systemd/system/*your target*.wants`, and then symlink the additional services from `/usr/lib/systemd/system/` that you wish to enable.

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

In *systemd* targets are exposed via *target units*. You can change them like this:

```
# systemctl isolate graphical.target

```

This will only change the current target, and has no effect on the next boot. This is equivalent to commands such as `telinit 3` or `telinit 5` in Sysvinit.

### Change default target to boot into

The standard target is `default.target`, which is aliased by default to `graphical.target` (which roughly corresponds to the old runlevel 5). To change the default target at boot-time, append one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to your bootloader:

*   `systemd.unit=multi-user.target` (which roughly corresponds to the old runlevel 3),
*   `systemd.unit=rescue.target` (which roughly corresponds to the old runlevel 1).

Alternatively, you may leave the bootloader alone and change `default.target`. This can be done using *systemctl*:

```
# systemctl set-default multi-user.target

```

To be able to override the previously set `default.target`, use the force option:

```
# systemctl set-default -f multi-user.target

```

The effect of this command is output by *systemctl*; a symlink to the new default target is made at `/etc/systemd/system/default.target`.

## Temporary files

"*systemd-tmpfiles* creates, deletes and cleans up volatile and temporary files and directories." It reads configuration files in `/etc/tmpfiles.d/` and `/usr/lib/tmpfiles.d/` to discover which actions to perform. Configuration files in the former directory take precedence over those in the latter directory.

Configuration files are usually provided together with service files, and they are named in the style of `/usr/lib/tmpfiles.d/*program*.conf`. For example, the [Samba](/index.php/Samba "Samba") daemon expects the directory `/run/samba` to exist and to have the correct permissions. Therefore, the [samba](https://www.archlinux.org/packages/?name=samba) package ships with this configuration:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

Configuration files may also be used to write values into certain files on boot. For example, if you used `/etc/rc.local` to disable wakeup from USB devices with `echo USBE > /proc/acpi/wakeup`, you may use the following tmpfile instead:

 `/etc/tmpfiles.d/disable-usb-wake.conf`  `w /proc/acpi/wakeup - - - - USBE` 

See the `systemd-tmpfiles(8)` and `tmpfiles.d(5)` man pages for details.

**Note:** This method may not work to set options in `/sys` since the *systemd-tmpfiles-setup* service may run before the appropriate device modules is loaded. In this case you could check whether the module has a parameter for the option you want to set with `modinfo *module*` and set this option with a [config file in /etc/modprobe.d](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Otherwise you will have to write a [udev rule](/index.php/Udev#About_udev_rules "Udev") to set the appropriate attribute as soon as the device appears.

## Timers

A timer is a unit configuration file whose name ends with *.timer* and encodes information about a timer controlled and supervised by *systemd*, for timer-based activation. See [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

**Note:** Timers can replace *cron* functionality to a great extent. See [systemd/Timers#As a cron replacement](/index.php/Systemd/Timers#As_a_cron_replacement "Systemd/Timers").

## Mounting

Since systemd is a replacement for System V init, it is in charge of the mounts specified in `/etc/fstab`. In fact, it goes beyond the usual `fstab` capabilities, implementing special mount options prefixed with `x-systemd.`. See [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") for an example of *automounting* (mounting on-demand) using these extensions. See [[2]](https://www.freedesktop.org/software/systemd/man/systemd.mount.html#fstab) for the complete documentation of these extensions.

## Journal

*systemd* has its own logging system called the journal; therefore, running a `syslog` daemon is no longer required. To read the log, use:

```
# journalctl

```

In Arch Linux, the directory `/var/log/journal/` is a part of the [systemd](https://www.archlinux.org/packages/?name=systemd) package, and the journal (when `Storage=` is set to `auto` in `/etc/systemd/journald.conf`) will write to `/var/log/journal/`. If you or some program delete that directory, *systemd* will **not** recreate it automatically and instead will write its logs to `/run/systemd/journal` in a nonpersistent way. However, the folder will be recreated when you set `Storage=persistent` and run `systemctl restart systemd-journald` (or reboot).

Systemd journal classifies messages by [Priority level](#Priority_level) and [Facility](#Facility). Logging classification corresponds to classic [Syslog](https://en.wikipedia.org/wiki/Syslog "wikipedia:Syslog") protocol ([RFC 5424](https://tools.ietf.org/html/rfc5424)).

### Priority level

A syslog severity code (in systemd called priority) is used to mark the importance of a message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Value | Severity | Keyword | Description | Examples |
| 0 | Emergency | emerg | System is unusable | Severe Kernel BUG, systemd dumped core.
This level should not be used by applications. |
| 1 | Alert | alert | Should be corrected immediately | Vital subsystem goes out of work. Data loss.
`kernel: BUG: unable to handle kernel paging request at ffffc90403238ffc`. |
| 2 | Critical | crit | Critical conditions | Crashes, coredumps. Like familiar flash:
`systemd-coredump[25319]: Process 25310 (plugin-containe) of user 1000 dumped core`
Failure in the system primary application, like X11. |
| 3 | Error | err | Error conditions | Not severe error reported:
`kernel: usb 1-3: 3:1: cannot get freq at ep 0x84`,
`systemd[1]: Failed unmounting /var.`,
`libvirtd[1720]: internal error: Failed to initialize a valid firewall backend`). |
| 4 | Warning | warning | May indicate that an error will occur if action is not taken. | A non-root file system has only 1GB free.
`org.freedesktop. Notifications[1860]: (process:5999): Gtk-WARNING **: Locale not supported by C library. Using the fallback 'C' locale`. |
| 5 | Notice | notice | Events that are unusual, but not error conditions. | `systemd[1]: var.mount: Directory /var to mount over is not empty, mounting anyway`. `gcr-prompter[4997]: Gtk: GtkDialog mapped without a transient parent. This is discouraged`. |
| 6 | Informational | info | Normal operational messages that require no action. | `lvm[585]: 7 logical volume(s) in volume group "archvg" now active`. |
| 7 | Debug | debug | Information useful to developers for debugging the application. | `kdeinit5[1900]: powerdevil: Scheduling inhibition from ":1.14" "firefox" with cookie 13 and reason "screen"`. |

If issue you are looking for, was not found on according level, search it on couple of priority levels above and below. This rules are recommendations. Some errors considered a normal occasion for program so they marked low in priority by developer, and on the contrary, sometimes too many messages plaques too high priorities for them, but often it's an arguable situation. And often you really should solve an issue, also to understand architecture and adopt best practices.

Examples:

*   Info message: `pulseaudio[2047]: W: [pulseaudio] alsa-mixer.c: Volume element Master has 8 channels. That's too much! I can't handle that!` It is an warning or error by definition.
*   Plaguing alert message: `sudo[21711]:     user : a password is required ; TTY=pts/0 ; PWD=/home/user ; USER=root ; COMMAND=list /usr/bin/pacman --color auto -Sy` The [reason](https://bbs.archlinux.org/viewtopic.php?id=184455) - user was manually added to sudoers file, not to wheel group, which is arguably normal action, but sudo produced an alert on every occasion.

### Facility

A syslog facility code is used to specify the type of program that is logging the message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Facility code | Keyword | Description | Info |
| 0 | kern | kernel messages |
| 1 | user | user-level messages |
| 2 | mail | mail system | Archaic POSIX still supported and sometimes used system, for more `man mail`) |
| 3 | daemon | system daemons | All deamons, including systemd and its subsystems |
| 4 | auth | security/authorization messages | Also watch for different facility 10 |
| 5 | syslog | messages generated internally by syslogd | As it standartized for syslogd, not used by systemd (see facility 3) |
| 6 | lpr | line printer subsystem (archaic subsystem) |
| 7 | news | network news subsystem (archaic subsystem) |
| 8 | uucp | UUCP subsystem (archaic subsystem) |
| 9 | clock daemon | systemd-timesyncd |
| 10 | authpriv | security/authorization messages | Also watch for different facility 4 |
| 11 | ftp | FTP daemon |
| 12 | - | NTP subsystem |
| 13 | - | log audit |
| 14 | - | log alert |
| 15 | cron | scheduling daemon |
| 16 | local0 | local use 0 (local0) |
| 17 | local1 | local use 1 (local1) |
| 18 | local2 | local use 2 (local2) |
| 19 | local3 | local use 3 (local3) |
| 20 | local4 | local use 4 (local4) |
| 21 | local5 | local use 5 (local5) |
| 22 | local6 | local use 6 (local6) |
| 23 | local7 | local use 7 (local7) |

So, useful facilities to watch: 0,1,3,4,9,10,15.

### Filtering output

*journalctl* allows you to filter the output by specific fields. Be aware that if there are many messages to display or filtering of large time span has to be done, the output of this command can be delayed for quite some time.

**Tip:** While the journal is stored in a binary format, the content of stored messages is not modified. This means it is viewable with *strings*, for example for recovery in an environment which does not have *systemd* installed. Example command: `$ strings /mnt/arch/var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i *message*` 

Examples:

*   Show all messages from this boot: `# journalctl -b` However, often one is interested in messages not from the current, but from the previous boot (e.g. if an unrecoverable system crash happened). This is possible through optional offset parameter of the `-b` flag: `journalctl -b -0` shows messages from the current boot, `journalctl -b -1` from the previous boot, `journalctl -b -2` from the second previous and so on. See `man 1 journalctl` for full description, the semantics is much more powerful.
*   Show all messages from date (and optional time): `# journalctl --since="2012-10-30 18:17:16"` 
*   Show all messages since 20 minutes ago: `# journalctl --since "20 min ago"` 
*   Follow new messages: `# journalctl -f` 
*   Show all messages by a specific executable: `# journalctl /usr/lib/systemd/systemd` 
*   Show all messages by a specific process: `# journalctl _PID=1` 
*   Show all messages by a specific unit: `# journalctl -u netcfg` 
*   Show kernel ring buffer: `# journalctl -k` 
*   Show only error, critical, and alert priority messages `# journalctl -p err..alert` Numbers also can be used, `journalctl -p 3..1`. If single number/keyword used, `journalctl -p 3` - all higher priority levels also included.
*   Show auth.log equivalent by filtering on syslog facility: `# journalctl SYSLOG_FACILITY=10` 

See `man 1 journalctl`, `man 7 systemd.journal-fields`, or Lennart's [blog post](http://0pointer.de/blog/projects/journalctl.html) for details.

**Tip:** By default, *journalctl* truncates lines longer than screen width, but in some cases, it may be better to enable wrapping instead of truncating. This can be controlled by the `SYSTEMD_LESS` [environment variable](/index.php/Environment_variable "Environment variable"), which contains options passed to [less](/index.php/Core_utilities#less "Core utilities") (the default pager) and defaults to `FRSXMK` (see `man 1 less` and `man 1 journalctl` for details).

By omitting the `S` option, the output will be wrapped instead of truncated. For example, start *journalctl* as follows:

```
$ SYSTEMD_LESS=FRXMK journalctl

```
If you would like to set this behaviour as default, [export](/index.php/Environment_variables#Per_user "Environment variables") the variable from `~/.bashrc` or `~/.zshrc`.

### Journal size limit

If the journal is persistent (non-volatile), its size limit is set to a default value of 10% of the size of the underlying file system but capped to 4 GiB. For example, with `/var/log/journal/` located on a 20 GiB partition, journal data may take up to 2 GiB. On a 50 GiB partition, it would max at 4 GiB.

The maximum size of the persistent journal can be controlled by uncommenting and changing the following:

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

It is also possible to use the drop-in snippets configuration override mechanism rather than editing the global configuration file. In this case do not forget to place the overrides under the `[Journal]` header:

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

See `man journald.conf` for more info.

### Clean journal files manually

Journal files can be globally removed from `/var/log/journal/` using *e.g.* `rm`, or can be trimmed according to various criteria using `journalctl`. Examples:

*   Remove archived journal files until the disk space they use falls below 100M: `# journalctl --vacuum-size=100M` 
*   Make all journal files contain no data older than 2 weeks. `# journalctl --vacuum-time=2weeks` 

See `man journalctl` for more info.

### Journald in conjunction with syslog

Compatibility with a classic, non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") implementation can be provided by letting *systemd* forward all messages via the socket `/run/systemd/journal/syslog`. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)).

The default `journald.conf` for forwarding to the socket is `ForwardToSyslog=no` to avoid system overhead, because [rsyslog](/index.php/Rsyslog "Rsyslog") or [syslog-ng](/index.php/Syslog-ng "Syslog-ng") pull the messages from the journal by [itself](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

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
$ journalctl -D */mnt*/var/log/journal -xe

```

## Tips and tricks

### Enable installed units by default

Arch Linux ships with `/usr/lib/systemd/system-preset/99-default.preset` containing `disable *`. This causes *systemctl preset* to disable all units by default, such that when a new package is installed, the user must manually enable the unit.

If this behavior is not desired, simply create a symlink from `/etc/systemd/system-preset/99-default.preset` to `/dev/null` in order to override the configuration file. This will cause *systemctl preset* to enable all units that get installed—regardless of unit type—unless specified in another file in one *systemctl preset'*s configuration directories. User units are not affected. See the manpage for `systemd.preset` for more information.

**Note:** Enabling all units by default may cause problems with packages that contain two or more mutually exclusive units. *systemctl preset* is designed to be used by distributions and spins or system administrators. In the case where two conflicting units would be enabled, you should explicitly specify which one is to be disabled in a preset configuration file as specified in the manpage for `systemd.preset`.

### Sandboxing application environments

A unit file can be created as a sandbox to isolate applications and their processes within a hardened virtual environment. systemd leverages [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces"), white-/blacklisting of [Capabilities](/index.php/Capabilities "Capabilities"), and [control groups](/index.php/Cgroups "Cgroups") to container processes through an extensive [execution environment configuration](https://www.freedesktop.org/software/systemd/man/systemd.exec.html).

The enhancement of an existing systemd unit file with application sandboxing typically requires trial-and-error tests accompanied by the generous use of [strace](https://www.archlinux.org/packages/?name=strace), [stderr](https://en.wikipedia.org/wiki/Standard_streams#Standard_error_.28stderr.29 "wikipedia:Standard streams") and [journalctl](https://www.freedesktop.org/software/systemd/man/journalctl.html) error logging and output facilities. You may want to first search upstream documentation for already done tests to base trials on.

Some examples on how sandboxing with systemd can be deployed:

*   `CapabilityBoundingSet` defines a whitelisted set of allowed capabilities, but may also be used to blacklist a specific capability for a unit.
    *   The `CAP_SYS_ADM` capability, for example, which should be one of the [goals of a secure sandbox](https://lwn.net/Articles/486306/): `CapabilityBoundingSet=~ CAP_SYS_ADM`
*   [Unbound#Sandboxing](/index.php/Unbound#Sandboxing "Unbound") shows a full-scale example of systemd features for sandboxing.

## Troubleshooting

### Investigating systemd errors

As an example, we will investigate an error with `systemd-modules-load` service:

**1.** Lets find the *systemd* services which fail to start:

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

*systemd* has several options for diagnosing problems with the boot process. See [boot debugging](/index.php/Boot_debugging "Boot debugging") and the [systemd debugging documentation](http://freedesktop.org/wiki/Software/systemd/Debugging/).

### Diagnosing problems with a specific service

If some *systemd* service misbehaves and you want to get more information about what is going on, set the `SYSTEMD_LOG_LEVEL` [environment variable](/index.php/Environment_variable "Environment variable") to `debug`. For example, to run the *systemd-networkd* daemon in debug mode:

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

If the shutdown process takes a very long time (or seems to freeze) most likely a service not exiting is to blame. *systemd* waits some time for each service to exit before trying to kill it. To find out if you are affected, see [this article](http://freedesktop.org/wiki/Software/systemd/Debugging/#shutdowncompleteseventually).

### Short lived processes do not seem to log any output

If `journalctl -u foounit` does not show any output for a short lived service, look at the PID instead. For example, if `systemd-modules-load.service` fails, and `systemctl status systemd-modules-load` shows that it ran as PID 123, then you might be able to see output in the journal for that PID, i.e. `journalctl -b _PID=123`. Metadata fields for the journal such as `_SYSTEMD_UNIT` and `_COMM` are collected asynchronously and rely on the `/proc` directory for the process existing. Fixing this requires fixing the kernel to provide this data via a socket connection, similar to `SCM_CREDENTIALS`.

### Boot time increasing over time

After using `systemd-analyze` a number of users have noticed that their boot time has increased significantly in comparison with what it used to be. After using `systemd-analyze blame` [NetworkManager](/index.php/NetworkManager "NetworkManager") is being reported as taking an unusually large amount of time to start.

The problem for some users has been due to `/var/log/journal` becoming too large. This may have other impacts on performance, such as for `systemctl status` or `journalctl`. As such the solution is to remove every file within the folder (ideally making a backup of it somewhere, at least temporarily) and then setting a journal file size limit as described in [#Journal size limit](#Journal_size_limit).

### systemd-tmpfiles-setup.service fails to start at boot

Starting with systemd 219, `/usr/lib/tmpfiles.d/systemd.conf` specifies ACL attributes for directories under `/var/log/journal` and, therefore, requires ACL support to be enabled for the filesystem the journal resides on.

See [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") for instructions on how to enable ACL on the filesystem that houses `/var/log/journal`.

### systemctl enable fails for symlinks in /etc/systemd/system

If `/etc/systemd/system/*foo*.service` is a symlink and `systemctl enable *foo*.service` is run, it will fail with this error:

```
Failed to issue method call: No such file or directory

```

This is a [design choice](https://bugzilla.redhat.com/show_bug.cgi?id=955379#c14) of systemd. As a workaround, enabling by absolute path works:

```
# systemctl enable */absolute/path/foo*.service

```

### dependent services are not started when starting a service manually

One (in)famous example is `libvirtd.service` which needs the `virtlogd.socket` to function properly.

The dependencies in `/usr/lib/systemd/system/libvirtd.service` are defined as

```
[Install]
WantedBy=multi-user.target
Also=virtlockd.socket
Also=virtlogd.socket

```

This only defines the necessary/dependent sockets to be enabled services(i.e. as "autostart"), too - but does not start them whenever the DISABLED (= non-autostarting) service ist started manually e.g. by running `systemctl start libvirtd`

Thus the correct (?) way to manually start a service with dependent subservices once (instead of at each start of the system) probably is

```
systemctl enable ServiceWithSubservices
systemctl start ServiceWithSubservices
systemctl disable ServiceWithSubservices

```

### systemd version printed on boot is not the same as installed package version

You need to [regenerate your initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") and the versions should match.

**Tip:** A pacman hook can be used to automatically regenerate the initramfs every time [systemd](https://www.archlinux.org/packages/?name=systemd) is upgraded. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=215411) and [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman").

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
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in *The H Open* magazine.
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html)
*   [Status update](http://0pointer.de/blog/projects/systemd-update.html)
*   [Status update2](http://0pointer.de/blog/projects/systemd-update-2.html)
*   [Status update3](http://0pointer.de/blog/projects/systemd-update-3.html)
*   [Most recent summary](http://0pointer.de/blog/projects/why.html)
*   [Fedora's SysVinit to systemd cheatsheet](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)
*   [Gentoo Wiki systemd page](http://wiki.gentoo.org/wiki/Systemd)
*   [Emacs Syntax highlighting for Systemd files](/index.php/Emacs#Syntax_highlighting_for_systemd_Files "Emacs")
*   [digital ocean tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)