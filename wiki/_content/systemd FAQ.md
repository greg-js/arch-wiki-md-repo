# systemd FAQ

## Contents

*   [1 FAQ](#FAQ)
    *   [1.1 Why do I get log messages on my console?](#Why_do_I_get_log_messages_on_my_console.3F)
    *   [1.2 How do I change the default number of gettys?](#How_do_I_change_the_default_number_of_gettys.3F)
    *   [1.3 How do I get more verbose output during boot?](#How_do_I_get_more_verbose_output_during_boot.3F)
    *   [1.4 How do I avoid clearing the console after boot?](#How_do_I_avoid_clearing_the_console_after_boot.3F)
    *   [1.5 What kernel options are required for systemd?](#What_kernel_options_are_required_for_systemd.3F)
    *   [1.6 What other units does a unit depend on?](#What_other_units_does_a_unit_depend_on.3F)
    *   [1.7 My computer shuts down, but the power stays on](#My_computer_shuts_down.2C_but_the_power_stays_on)
    *   [1.8 After migrating to systemd, why won't my fakeRAID mount?](#After_migrating_to_systemd.2C_why_won.27t_my_fakeRAID_mount.3F)
    *   [1.9 How can I make a script start during the boot process?](#How_can_I_make_a_script_start_during_the_boot_process.3F)
    *   [1.10 Status of .service says "active (exited)" in green. (e.g. iptables)](#Status_of_.service_says_.22active_.28exited.29.22_in_green._.28e.g._iptables.29)
    *   [1.11 "Failed to issue method call: File exists" error](#.22Failed_to_issue_method_call:_File_exists.22_error)

## FAQ

For an up-to-date list of known issues, look at the upstream [TODO](https://github.com/systemd/systemd/blob/master/TODO).

### Why do I get log messages on my console?

You must set the kernel loglevel yourself. Historically, `/etc/rc.sysinit` did this for us and set dmesg loglevel to `3`, which was a reasonably quiet loglevel. Either add `loglevel=3` or `quiet` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### How do I change the default number of gettys?

Currently, only one getty is launched by default. If you switch to another tty, a getty will be launched there (socket-activation style). In other words, [Ctl] [Alt] [F2] will launch a new getty on tty2.

By default, the number of auto-activated gettys is capped at six. Thus [F7] through [F12] won't launch a getty.

If you want to change this behavior, then edit `/etc/systemd/logind.conf` and change the value of `NAutoVTs`. If you want all [F_x_] keys to start a getty, increase the value of NAutoVTs to 12\. If you are [forwarding journald to tty12](/index.php/Systemd#Forward_journald_to_.2Fdev.2Ftty12 "Systemd"), increase the value of NAutoVTs to 11 (thus leaving tty12 free).

You can also pre-activate gettys which will be running from boot.

To add another pre-activated getty, simply place another symlink for instantiating another getty in the `/etc/systemd/system/getty.target.wants/` directory:

```
# ln -sf /usr/lib/systemd/system/getty@.service /etc/systemd/system/getty.target.wants/getty@tty9.service
# systemctl start getty@tty9.service

```

To remove a getty, simply remove the getty symlinks you want to get rid of in the `/etc/systemd/system/getty.target.wants/` directory:

```
# rm /etc/systemd/system/getty.target.wants/getty@{tty5,tty6}.service
# systemctl stop getty@tty5.service getty@tty6.service

```

systemd does not use the `/etc/inittab` file.

### How do I get more verbose output during boot?

If you see no output at all in console after the initram message, this means you have the `quiet` parameter in your kernel line. It's best to remove it, at least the first time you boot with systemd, to see if everything is ok. Then, you will see a list `[ OK ]` in green or `[ FAILED ]` in red.

Any messages are logged to the system log and if you want to find out about the status of your system run `systemctl` (no root privileges required) or look at the boot/system log with `journalctl`.

### How do I avoid clearing the console after boot?

Create a directory called `/etc/systemd/system/getty@.service.d` and place `nodisallocate.conf` in there to [override](/index.php/Systemd#Editing_provided_units "Systemd") the `TTYVTDisallocate` option to `no`.

 `/etc/systemd/system/getty@.service.d/nodisallocate.conf` 

```
[Service]
TTYVTDisallocate=no
```

### What kernel options are required for systemd?

Kernels prior to 3.0 are unsupported.

If you use a custom kernel, you will need to make sure that systemd's options are selected.

If you are compiling a new kernel for use with an installed version of systemd, the required and recommended options are listed in the systemd README file `/usr/share/doc/systemd/README`.

If you are preparing to install a new version of systemd and are running a custom kernel, the most recent version of the file can be found in the [the systemd git](http://cgit.freedesktop.org/systemd/systemd/tree/README).

### What other units does a unit depend on?

For example, if you want to figure out which services a target like `multi-user.target` pulls in, use something like this:

 `$ systemctl show -p "Wants" multi-user.target`  `Wants=rc-local.service avahi-daemon.service rpcbind.service NetworkManager.service acpid.service dbus.service atd.service crond.service auditd.service ntpd.service udisks.service bluetooth.service org.cups.cupsd.service wpa_supplicant.service getty.target modem-manager.service portreserve.service abrtd.service yum-updatesd.service upowerd.service test-first.service pcscd.service rsyslog.service haldaemon.service remote-fs.target plymouth-quit.service systemd-update-utmp-runlevel.service sendmail.service lvm2-monitor.service cpuspeed.service udev-post.service mdmonitor.service iscsid.service livesys.service livesys-late.service irqbalance.service iscsi.service` 

Instead of `Wants` you might also try `WantedBy`, `Requires`, `RequiredBy`, `Conflicts`, `ConflictedBy`, `Before`, `After` for the respective types of dependencies and their inverse.

### My computer shuts down, but the power stays on

Use `systemctl poweroff` instead of `systemctl halt`.

### After migrating to systemd, why won't my fakeRAID mount?

Be sure you use:

```
# systemctl enable dmraid.service

```

### How can I make a script start during the boot process?

Create a new file in `/etc/systemd/system` (e.g. _myscript_.service) and add the following contents:

```
[Unit]
Description=My script

[Service]
ExecStart=/usr/bin/my-script

[Install]
WantedBy=multi-user.target 

```

Then:

```
# systemctl enable _myscript_.service

```

This example assumes you want your script to start up when the target multi-user is launched. Also do `chmod 755` to your script to enable execute permissions if you haven't done so already.

**Note:** In case you want to start a shell script, make sure you have `#!/bin/sh` in the first line of the script. Do **not** write something like `ExecStart=/bin/sh /path/to/script.sh` because that will not work.

### Status of .service says "active (exited)" in green. (e.g. iptables)

This is perfectly normal. In the case with iptables it is because there is no daemon to run, it is controlled in the kernel. Therefore, it exits after the rules have been loaded.

To check if your iptables rules have been loaded properly:

```
# iptables --list

```

### "Failed to issue method call: File exists" error

This happens when using `systemctl enable` and the symlink it tries to create in `/etc/systemd/system/` already exists. Typically this happens when switching from one display manager to another one (for instance GDM to KDM, which can be enabled with `gdm.service` and `kdm.service`, respectively) and the corresponding symlink `/etc/systemd/system/display-manager.service` already exists.

To solve this problem, either first disable the relevant display manager before enabling the new one, or use `systemctl -f enable` to overwrite an existing symlink.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Systemd_FAQ&oldid=418529](https://wiki.archlinux.org/index.php?title=Systemd_FAQ&oldid=418529)"