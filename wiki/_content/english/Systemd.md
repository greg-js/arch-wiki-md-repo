Related articles

*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")
*   [systemd/Journal](/index.php/Systemd/Journal "Systemd/Journal")
*   [systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ")
*   [init](/index.php/Init "Init")
*   [Daemons](/index.php/Daemons "Daemons")
*   [udev](/index.php/Udev "Udev")
*   [Improving performance/Boot process](/index.php/Improving_performance/Boot_process "Improving performance/Boot process")
*   [Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown")

From the [project web page](https://freedesktop.org/wiki/Software/systemd/):

	*systemd* is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system. systemd provides aggressive parallelization capabilities, uses socket and [D-Bus](/index.php/D-Bus "D-Bus") activation for starting services, offers on-demand starting of daemons, keeps track of processes using Linux [control groups](/index.php/Control_groups "Control groups"), maintains mount and automount points, and implements an elaborate transactional dependency-based service control logic. *systemd* supports SysV and LSB init scripts and works as a replacement for sysvinit. Other parts include a logging daemon, utilities to control basic system configuration like the hostname, date, locale, maintain a list of logged-in users and running containers and virtual machines, system accounts, runtime directories and settings, and daemons to manage simple network configuration, network time synchronization, log forwarding, and name resolution.

**Note:** For a detailed explanation of why Arch moved to *systemd*, see [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
        *   [2.3.3 Revert to vendor version](#Revert_to_vendor_version)
        *   [2.3.4 Examples](#Examples)
*   [3 Targets](#Targets)
    *   [3.1 Get current targets](#Get_current_targets)
    *   [3.2 Create custom target](#Create_custom_target)
    *   [3.3 Mapping between SysV runlevels and systemd targets](#Mapping_between_SysV_runlevels_and_systemd_targets)
    *   [3.4 Change current target](#Change_current_target)
    *   [3.5 Change default target to boot into](#Change_default_target_to_boot_into)
    *   [3.6 Default target order](#Default_target_order)
*   [4 Temporary files](#Temporary_files)
*   [5 Timers](#Timers)
*   [6 Mounting](#Mounting)
    *   [6.1 GPT partition automounting](#GPT_partition_automounting)
*   [7 systemd-sysvcompat](#systemd-sysvcompat)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Running services after the network is up](#Running_services_after_the_network_is_up)
    *   [8.2 Enable installed units by default](#Enable_installed_units_by_default)
    *   [8.3 Sandboxing application environments](#Sandboxing_application_environments)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Investigating systemd errors](#Investigating_systemd_errors)
    *   [9.2 Diagnosing boot problems](#Diagnosing_boot_problems)
    *   [9.3 Diagnosing a service](#Diagnosing_a_service)
    *   [9.4 Shutdown/reboot takes terribly long](#Shutdown/reboot_takes_terribly_long)
    *   [9.5 Short lived processes do not seem to log any output](#Short_lived_processes_do_not_seem_to_log_any_output)
    *   [9.6 Boot time increasing over time](#Boot_time_increasing_over_time)
    *   [9.7 systemd-tmpfiles-setup.service fails to start at boot](#systemd-tmpfiles-setup.service_fails_to_start_at_boot)
    *   [9.8 systemd version printed on boot is not the same as installed package version](#systemd_version_printed_on_boot_is_not_the_same_as_installed_package_version)
    *   [9.9 Disable emergency mode on remote machine](#Disable_emergency_mode_on_remote_machine)
*   [10 See also](#See_also)

## Basic systemctl usage

The main command used to introspect and control *systemd* is *systemctl*. Some of its uses are examining the system state and managing the system and services. See [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) for more details.

**Tip:**

*   You can use all of the following *systemctl* commands with the `-H *user*@*host*` switch to control a *systemd* instance on a remote machine. This will use [SSH](/index.php/SSH "SSH") to connect to the remote *systemd* instance.
*   [Plasma](/index.php/Plasma "Plasma") users can install [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/) as a graphical frontend for *systemctl*. After installing the module will be added under *System administration*.

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

Show the [cgroup slice](/index.php/Cgroups "Cgroups"), memory and parent for a PID:

```
$ systemctl status *pid*

```

### Using units

Units can be, for example, services (*.service*), mount points (*.mount*), devices (*.device*) or sockets (*.socket*).

When using *systemctl*, you generally have to specify the complete name of the unit file, including its suffix, for example `sshd.socket`. There are however a few short forms when specifying the unit in the following *systemctl* commands:

*   If you do not specify the suffix, systemctl will assume *.service*. For example, `netctl` and `netctl.service` are equivalent.
*   Mount points will automatically be translated into the appropriate *.mount* unit. For example, specifying `/home` is equivalent to `home.mount`.
*   Similar to mount points, devices are automatically translated into the appropriate *.device* unit, therefore specifying `/dev/sda2` is equivalent to `dev-sda2.device`.

See [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) for details.

**Note:** Some unit names contain an `@` sign (e.g. `name@*string*.service`): this means that they are [instances](http://0pointer.de/blog/projects/instances.html) of a *template* unit, whose actual file name does not contain the `*string*` part (e.g. `name@.service`). `*string*` is called the *instance identifier*, and is similar to an argument that is passed to the template unit when called with the *systemctl* command: in the unit file it will substitute the `%i` specifier. To be more accurate, *before* trying to instantiate the `name@.suffix` template unit, *systemd* will actually look for a unit with the exact `name@string.suffix` file name, although by convention such a "clash" happens rarely, i.e. most unit files containing an `@` sign are meant to be templates. Also, if a template unit is called without an instance identifier, it will just fail, since the `%i` specifier cannot be substituted.

**Tip:**

*   Most of the following commands also work if multiple units are specified, see [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) for more information.
*   The `--now` switch can be used in conjunction with `enable`, `disable`, and `mask` to respectively start, stop, or mask the unit *immediately* rather than after rebooting.
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

**Enable** a unit to be started on **bootup** and **Start** immediately:

```
# systemctl enable --now *unit*

```

**Disable** a unit to not start during bootup:

```
# systemctl disable *unit*

```

**Mask** a unit to make it impossible to start it (both manually and as a dependency, which makes masking dangerous):

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

**Reload *systemd*** manager configuration, scanning for **new or changed units**:

**Note:** This does not ask the changed units to reload their own configurations. See `reload` example above.

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

The syntax of *systemd'*s [unit files](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) is inspired by XDG Desktop Entry Specification *.desktop* files, which are in turn inspired by Microsoft Windows *.ini* files. Unit files are loaded from multiple locations (to see the full list, run `systemctl show --property=UnitPath`), but the main ones are (listed from lowest to highest precedence):

*   `/usr/lib/systemd/system/`: units provided by installed packages
*   `/etc/systemd/system/`: units installed by the system administrator

**Note:**

*   The load paths are completely different when running *systemd* in [user mode](/index.php/Systemd/User#How_it_works "Systemd/User").
*   systemd unit names may only contain ASCII alphanumeric characters, underscores and periods. All other characters must be replaced by C-style "\x2d" escapes, or employ their predefined semantics ('@', '-'). See [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) and [systemd-escape(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-escape.1) for more information.

Look at the units installed by your packages for examples, as well as the [annotated example section](https://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples) of [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5).

**Tip:** Comments prepended with `#` may be used in unit-files as well, but only in new lines. Do not use end-line comments after *systemd* parameters or the unit will fail to activate.

### Handling dependencies

With *systemd*, dependencies can be resolved by designing the unit files correctly. The most typical case is that the unit *A* requires the unit *B* to be running before *A* is started. In that case add `Requires=*B*` and `After=*B*` to the `[Unit]` section of *A*. If the dependency is optional, add `Wants=*B*` and `After=*B*` instead. Note that `Wants=` and `Requires=` do not imply `After=`, meaning that if `After=` is not specified, the two units will be started in parallel.

Dependencies are typically placed on services and not on [#Targets](#Targets). For example, `network.target` is pulled in by whatever service configures your network interfaces, therefore ordering your custom unit after it is sufficient since `network.target` is started anyway.

### Service types

There are several different start-up types to consider when writing a custom service file. This is set with the `Type=` parameter in the `[Service]` section:

*   `Type=simple` (default): *systemd* considers the service to be started up immediately. The process must not fork. Do not use this type if other services need to be ordered on this service, unless it is socket activated.
*   `Type=forking`: *systemd* considers the service started up once the process forks and the parent has exited. For classic daemons use this type unless you know that it is not necessary. You should specify `PIDFile=` as well so *systemd* can keep track of the main process.
*   `Type=oneshot`: this is useful for scripts that do a single job and then exit. You may want to set `RemainAfterExit=yes` as well so that *systemd* still considers the service as active after the process has exited.
*   `Type=notify`: identical to `Type=simple`, but with the stipulation that the daemon will send a signal to *systemd* when it is ready. The reference implementation for this notification is provided by *libsystemd-daemon.so*.
*   `Type=dbus`: the service is considered ready when the specified `BusName` appears on DBus's system bus.
*   `Type=idle`: *systemd* will delay execution of the service binary until all jobs are dispatched. Other than that behavior is very similar to `Type=simple`.

See the [systemd.service(5)](https://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=) man page for a more detailed explanation of the `Type` values.

### Editing provided units

To avoid conflicts with pacman, unit files provided by packages should not be directly edited. There are two safe ways to modify a unit without touching the original file: create a new unit file which [overrides the original unit](#Replacement_unit_files) or create [drop-in snippets](#Drop-in_files) which are applied on top of the original unit. For both methods, you must reload the unit afterwards to apply your changes. This can be done either by editing the unit with `systemctl edit` (which reloads the unit automatically) or by reloading all units with:

```
# systemctl daemon-reload

```

**Tip:**

*   You can use *systemd-delta* to see which unit files have been overridden or extended and what exactly has been changed.
*   Use `systemctl cat *unit*` to view the content of a unit file and all associated drop-in snippets.

#### Replacement unit files

To replace the unit file `/usr/lib/systemd/system/*unit*`, create the file `/etc/systemd/system/*unit*` and *reenable* the unit to update the symlinks:

```
# systemctl reenable *unit*

```

Alternatively, run:

```
# systemctl edit --full *unit*

```

This opens `/etc/systemd/system/*unit*` in your editor (copying the installed version if it does not exist yet) and automatically reloads it when you finish editing.

**Note:** The replacement units will keep on being used even if Pacman updates the original units in the future. This method makes system maintenance more difficult and therefore the next approach is preferred.

#### Drop-in files

To create drop-in files for the unit file `/usr/lib/systemd/system/*unit*`, create the directory `/etc/systemd/system/*unit*.d/` and place *.conf* files there to override or add new options. *systemd* will parse and apply these files on top of the original unit.

The easiest way to do this is to run:

```
# systemctl edit *unit*

```

This opens the file `/etc/systemd/system/*unit*.d/override.conf` in your text editor (creating it if necessary) and automatically reloads the unit when you are done editing.

**Note:** Not all keys can be overridden with drop-in files. For example, for changing `Conflicts=` a replacement file [is necessary](https://lists.freedesktop.org/archives/systemd-devel/2017-June/038976.html).

#### Revert to vendor version

To revert any changes to a unit made using `systemctl edit` do:

```
# systemctl revert *unit*

```

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

*systemd* uses *targets* to group units together via dependencies and as standardized synchronization points. They serve a similar purpose as [runlevels](https://en.wikipedia.org/wiki/Runlevel "wikipedia:Runlevel") but act a little different. Each *target* is named instead of numbered and is intended to serve a specific purpose with the possibility of having multiple ones active at the same time. Some *target*s are implemented by inheriting all of the services of another *target* and adding additional services to it. There are *systemd* *target*s that mimic the common SystemVinit runlevels so you can still switch *target*s using the familiar `telinit RUNLEVEL` command.

### Get current targets

The following should be used under *systemd* instead of running `runlevel`:

```
$ systemctl list-units --type=target

```

### Create custom target

The runlevels that held a defined meaning under sysvinit (i.e., 0, 1, 3, 5, and 6); have a 1:1 mapping with a specific *systemd* *target*. Unfortunately, there is no good way to do the same for the user-defined runlevels like 2 and 4\. If you make use of those it is suggested that you make a new named *systemd* *target* as `/etc/systemd/system/*your target*` that takes one of the existing runlevels as a base (you can look at `/usr/lib/systemd/system/graphical.target` as an example), make a directory `/etc/systemd/system/*your target*.wants`, and then symlink the additional services from `/usr/lib/systemd/system/` that you wish to enable.

### Mapping between SysV runlevels and systemd targets

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

The standard target is `default.target`, which is a symlink to `graphical.target`. This roughly corresponds to the old runlevel 5.

To verify the current target with *systemctl*:

```
$ systemctl get-default

```

To change the default target to boot into, change the `default.target` symlink. With *systemctl*:

 `# systemctl set-default multi-user.target` 
```
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target -> /usr/lib/systemd/system/multi-user.target.
```

Alternatively, append one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to your bootloader:

*   `systemd.unit=multi-user.target` (which roughly corresponds to the old runlevel 3),
*   `systemd.unit=rescue.target` (which roughly corresponds to the old runlevel 1).

### Default target order

Systemd chooses the `default.target` according to the following order:

1.  Kernel parameter shown above
2.  Symlink of `/etc/systemd/system/default.target`
3.  Symlink of `/usr/lib/systemd/system/default.target`

## Temporary files

"*systemd-tmpfiles* creates, deletes and cleans up volatile and temporary files and directories." It reads configuration files in `/etc/tmpfiles.d/` and `/usr/lib/tmpfiles.d/` to discover which actions to perform. Configuration files in the former directory take precedence over those in the latter directory.

Configuration files are usually provided together with service files, and they are named in the style of `/usr/lib/tmpfiles.d/*program*.conf`. For example, the [Samba](/index.php/Samba "Samba") daemon expects the directory `/run/samba` to exist and to have the correct permissions. Therefore, the [samba](https://www.archlinux.org/packages/?name=samba) package ships with this configuration:

 `/usr/lib/tmpfiles.d/samba.conf` 
```
D /run/samba 0755 root root

```

Configuration files may also be used to write values into certain files on boot. For example, if you used `/etc/rc.local` to disable wakeup from USB devices with `echo USBE > /proc/acpi/wakeup`, you may use the following tmpfile instead:

 `/etc/tmpfiles.d/disable-usb-wake.conf` 
```
#    Path                  Mode UID  GID  Age Argument
w    /proc/acpi/wakeup     -    -    -    -   USBE

```

See the [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) and [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) man pages for details.

**Note:** This method may not work to set options in `/sys` since the *systemd-tmpfiles-setup* service may run before the appropriate device modules is loaded. In this case you could check whether the module has a parameter for the option you want to set with `modinfo *module*` and set this option with a [config file in /etc/modprobe.d](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Otherwise you will have to write a [udev rule](/index.php/Udev#About_udev_rules "Udev") to set the appropriate attribute as soon as the device appears.

## Timers

A timer is a unit configuration file whose name ends with *.timer* and encodes information about a timer controlled and supervised by *systemd*, for timer-based activation. See [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

**Note:** Timers can replace [cron](/index.php/Cron "Cron") functionality to a great extent. See [systemd/Timers#As a cron replacement](/index.php/Systemd/Timers#As_a_cron_replacement "Systemd/Timers").

## Mounting

*systemd* is in charge of mounting the partitions and filesystems specified in `/etc/fstab`. The [systemd-fstab-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-fstab-generator.8) translates all the entries in `/etc/fstab` into systemd units, this is performed at boot time and whenever the configuration of the system manager is reloaded.

*systemd* extends the usual [fstab](/index.php/Fstab "Fstab") capabilities and offers additional mount options. These affect the dependencies of the mount unit, they can for example ensure that a mount is performed only once the network is up or only once another partition is mounted. The full list of specific *systemd* mount options, typically prefixed with `x-systemd.`, is detailed in [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5#FSTAB).

An example of these mount options in the context of *automounting*, which means mounting only when the resource is required rather than automatically at boot time, is provided in [fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab").

### GPT partition automounting

On a [GPT](/index.php/GPT "GPT") partitioned disk [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) will mount partitions following the [Discoverable Partitions Specification](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/), thus they can be omitted from `fstab`.

The automounting for a partition can be disabled by changing the partition's [type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") or setting the partition attribute bit 63 "do not automount", see [gdisk#Prevent GPT partition automounting](/index.php/Gdisk#Prevent_GPT_partition_automounting "Gdisk").

## systemd-sysvcompat

[systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) (required by [base](https://www.archlinux.org/packages/?name=base)) primary role is to provide the traditional linux [init](/index.php/Init "Init") binary. For systemd controlled systems, `init` is just a symbolic link to its `systemd` executable.

In addition, it also provides 6 convenience short cuts that [SysVinit](/index.php/SysVinit "SysVinit") users might be used to. The convenience short cuts are [halt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/halt.8), [poweroff(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/poweroff.8), [reboot(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/reboot.8), [runlevel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/runlevel.8), [shutdown(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/shutdown.8), and [telinit(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/telinit.8). Each one of those 6 commands is a symbolic link to `systemctl`, and governed by systemd behavior. Therefore, the discussion at [#Power management](#Power_management) applies to `halt`, `poweroff`, `reboot` and `shutdown`. The discussion at [#Mapping between SysV runlevels and systemd targets](#Mapping_between_SysV_runlevels_and_systemd_targets) applies to `runlevel` and `telinit`.

Systemd based systems can give up those System V compatibility methods by using the `init=` [boot parameter](/index.php/Kernel_parameters#Parameter_list "Kernel parameters") (see, for example, [[solved] /bin/init is in systemd-sysvcompat ?](https://bbs.archlinux.org/viewtopic.php?id=233387)) and systemd native `systemctl` command arguments.

## Tips and tricks

### Running services after the network is up

To delay a service after the network is up, include the following dependencies in the *.service* file:

 `/etc/systemd/system/*foo*.service` 
```
[Unit]
...
**Wants=network-online.target**
**After=network-online.target**
...
```

The network wait service of the particular application that manages the network, must also be enabled so that `network-online.target` properly reflects the network status.

*   If using [NetworkManager](/index.php/NetworkManager "NetworkManager"), `NetworkManager-wait-online.service` is enabled together with `NetworkManager.service`. Check if this is the case with `systemctl is-enabled NetworkManager-wait-online.service`. If it is not enabled, then [reenable](/index.php/Enable "Enable") `NetworkManager.service`.
*   In the case of [netctl](/index.php/Netctl "Netctl"), [enable](/index.php/Enable "Enable") the `netctl-wait-online.service`.
*   If using [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), `systemd-networkd-wait-online.service` is enabled together with `systemd-networkd.service`. Check if this is the case with `systemctl is-enabled systemd-networkd-wait-online.service`.

For more detailed explanations see [Running services after the network is up](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) in the systemd wiki.

### Enable installed units by default

Arch Linux ships with `/usr/lib/systemd/system-preset/99-default.preset` containing `disable *`. This causes *systemctl preset* to disable all units by default, such that when a new package is installed, the user must manually enable the unit.

If this behavior is not desired, simply create a symlink from `/etc/systemd/system-preset/99-default.preset` to `/dev/null` in order to override the configuration file. This will cause *systemctl preset* to enable all units that get installed—regardless of unit type—unless specified in another file in one *systemctl preset'*s configuration directories. User units are not affected. See [systemd.preset(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.preset.5) for more information.

**Note:** Enabling all units by default may cause problems with packages that contain two or more mutually exclusive units. *systemctl preset* is designed to be used by distributions and spins or system administrators. In the case where two conflicting units would be enabled, you should explicitly specify which one is to be disabled in a preset configuration file as specified in the manpage for `systemd.preset`.

### Sandboxing application environments

A unit file can be created as a sandbox to isolate applications and their processes within a hardened virtual environment. systemd leverages [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces"), white-/blacklisting of [Capabilities](/index.php/Capabilities "Capabilities"), and [control groups](/index.php/Control_groups "Control groups") to container processes through an extensive [execution environment configuration](https://www.freedesktop.org/software/systemd/man/systemd.exec.html).

The enhancement of an existing systemd unit file with application sandboxing typically requires trial-and-error tests accompanied by the generous use of [strace](https://www.archlinux.org/packages/?name=strace), [stderr](https://en.wikipedia.org/wiki/Standard_streams#Standard_error_.28stderr.29 "wikipedia:Standard streams") and [journalctl](https://www.freedesktop.org/software/systemd/man/journalctl.html) error logging and output facilities. You may want to first search upstream documentation for already done tests to base trials on.

Some examples on how sandboxing with systemd can be deployed:

*   `CapabilityBoundingSet` defines a whitelisted set of allowed capabilities, but may also be used to blacklist a specific capability for a unit.
    *   The `CAP_SYS_ADM` capability, for example, which should be one of the [goals of a secure sandbox](https://lwn.net/Articles/486306/): `CapabilityBoundingSet=~ CAP_SYS_ADM`

## Troubleshooting

### Investigating systemd errors

As an example, we will investigate an error with `systemd-modules-load` service:

**1.** Lets find the *systemd* services which fail to start at boot time:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

Another way is to live log *systemd* messages:

```
$ journalctl -fp err

```

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
# systemctl start systemd-modules-load

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

### Diagnosing boot problems

*systemd* has several options for diagnosing problems with the boot process. See [boot debugging](/index.php/Boot_debugging "Boot debugging") for more general instructions and options to capture boot messages before *systemd* takes over the [boot process](/index.php/Boot_process "Boot process"). Also see the [systemd debugging documentation](https://freedesktop.org/wiki/Software/systemd/Debugging/).

### Diagnosing a service

If some *systemd* service misbehaves or you want to get more information about what is happening, set the `SYSTEMD_LOG_LEVEL` [environment variable](/index.php/Environment_variable "Environment variable") to `debug`. For example, to run the *systemd-networkd* daemon in debug mode:

Add a [drop-in file](#Drop-in_files) for the service adding the two lines:

```
[Service]
Environment=SYSTEMD_LOG_LEVEL=debug

```

Or equivalently, set the environment variable manually:

```
# SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

```

then [restart](/index.php/Restart "Restart") *systemd-networkd* and watch the journal for the service with the `-f`/`--follow` option.

### Shutdown/reboot takes terribly long

If the shutdown process takes a very long time (or seems to freeze) most likely a service not exiting is to blame. *systemd* waits some time for each service to exit before trying to kill it. To find out if you are affected, see [this article](https://freedesktop.org/wiki/Software/systemd/Debugging/#shutdowncompleteseventually).

### Short lived processes do not seem to log any output

If `journalctl -u foounit` does not show any output for a short lived service, look at the PID instead. For example, if `systemd-modules-load.service` fails, and `systemctl status systemd-modules-load` shows that it ran as PID 123, then you might be able to see output in the journal for that PID, i.e. `journalctl -b _PID=123`. Metadata fields for the journal such as `_SYSTEMD_UNIT` and `_COMM` are collected asynchronously and rely on the `/proc` directory for the process existing. Fixing this requires fixing the kernel to provide this data via a socket connection, similar to `SCM_CREDENTIALS`. In short, it is a [bug](https://github.com/systemd/systemd/issues/2913). Keep in mind that immediately failed services might not print anything to the journal as per design of systemd.

### Boot time increasing over time

After using `systemd-analyze` a number of users have noticed that their boot time has increased significantly in comparison with what it used to be. After using `systemd-analyze blame` [NetworkManager](/index.php/NetworkManager "NetworkManager") is being reported as taking an unusually large amount of time to start.

The problem for some users has been due to `/var/log/journal` becoming too large. This may have other impacts on performance, such as for `systemctl status` or `journalctl`. As such the solution is to remove every file within the folder (ideally making a backup of it somewhere, at least temporarily) and then setting a journal file size limit as described in [Systemd/Journal#Journal size limit](/index.php/Systemd/Journal#Journal_size_limit "Systemd/Journal").

### systemd-tmpfiles-setup.service fails to start at boot

Starting with systemd 219, `/usr/lib/tmpfiles.d/systemd.conf` specifies ACL attributes for directories under `/var/log/journal` and, therefore, requires ACL support to be enabled for the filesystem the journal resides on.

See [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") for instructions on how to enable ACL on the filesystem that houses `/var/log/journal`.

### systemd version printed on boot is not the same as installed package version

You need to [regenerate your initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") and the versions should match.

**Tip:** A pacman hook can be used to automatically regenerate the initramfs every time [systemd](https://www.archlinux.org/packages/?name=systemd) is upgraded. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=215411) and [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman").

### Disable emergency mode on remote machine

You may want to disable emergency mode on a remote machine, for example, a virtual machine hosted at Azure or Google Cloud. It is because if emergency mode is triggered, the machine will be blocked from connecting to network.

```
# systemctl mask emergency.service
# systemctl mask emergency.target

```

## See also

*   [Wikipedia:systemd](https://en.wikipedia.org/wiki/systemd "wikipedia:systemd")
*   [systemd Official web site](https://www.freedesktop.org/wiki/Software/systemd)
    *   [systemd optimizations](https://www.freedesktop.org/wiki/Software/systemd/Optimizations)
    *   [systemd FAQ](https://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
    *   [systemd Tips and tricks](https://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [Manual pages](https://www.freedesktop.org/software/systemd/man/)
*   Other distributions
    *   [Gentoo:Systemd](https://wiki.gentoo.org/wiki/Systemd "gentoo:Systemd")
    *   [Fedora:Systemd](https://fedoraproject.org/wiki/Systemd "fedora:Systemd")
    *   [Fedora:How to debug Systemd problems](https://fedoraproject.org/wiki/How_to_debug_Systemd_problems "fedora:How to debug Systemd problems")
    *   [Fedora:SysVinit to Systemd Cheatsheet](https://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet "fedora:SysVinit to Systemd Cheatsheet")
    *   [Debian:systemd](https://wiki.debian.org/systemd "debian:systemd")
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html), [update 1](http://0pointer.de/blog/projects/systemd-update.html), [update 2](http://0pointer.de/blog/projects/systemd-update-2.html), [update 3](http://0pointer.de/blog/projects/systemd-update-3.html), [summary](http://0pointer.de/blog/projects/why.html)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [How To Use Systemctl to Manage Systemd Services and Units](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)
*   [Session management with systemd-logind](https://dvdhrm.wordpress.com/2013/08/24/session-management-on-linux/)
*   [Emacs Syntax highlighting for Systemd files](/index.php/Emacs#Syntax_highlighting_for_systemd_Files "Emacs")
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in *The H Open* magazine.