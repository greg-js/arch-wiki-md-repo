Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [ConsoleKit](/index.php/ConsoleKit "ConsoleKit")

**Warning:** Arch Linux only has official support for [systemd](/index.php/Systemd "Systemd"). [[1]](https://lists.archlinux.org/pipermail/arch-general/2015-July/039460.html) When using a different init system, please mention so in support requests.

[Init](https://en.wikipedia.org/wiki/Init "wikipedia:Init") is the first process started during system boot. It is a daemon process that continues running until the system is shut down. Init is the direct or indirect ancestor of all other processes, and automatically adopts all orphaned processes. It is started by the kernel using a hard-coded filename; if the kernel is unable to start it, panic will result. Init is typically assigned [process identifier](https://en.wikipedia.org/wiki/process_identifier "wikipedia:process identifier") 1.

The init *scripts* (or *rc*) are launched by the init process to guarantee basic functionality on system start and shutdown. This includes (un)mounting of [file systems](/index.php/File_system "File system") and launching of [daemons](/index.php/Daemons "Daemons"). A *service manager* takes this one step further by providing active control over launched processes, or [process supervision](https://en.wikipedia.org/wiki/Process_Supervision "wikipedia:Process Supervision"). An example is to monitor for crashes and restart processes accordingly.

These components combine to the init *system*. Some inits include the service manager in the init process, or have init scripts in close relation to them. These inits are below referred to as *integrated*, though entries in different categories may explicitly depend on each other.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Inits (integrated)](#Inits_(integrated))
*   [2 Inits](#Inits)
*   [3 Init scripts](#Init_scripts)
*   [4 Service managers](#Service_managers)
*   [5 Configuration](#Configuration)
    *   [5.1 Migrate running services](#Migrate_running_services)
    *   [5.2 logind](#logind)
    *   [5.3 Scheduled tasks](#Scheduled_tasks)
    *   [5.4 Dbus](#Dbus)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 systemd-nspawn](#systemd-nspawn)
    *   [6.2 Replacing udev](#Replacing_udev)
*   [7 See also](#See_also)

## Inits (integrated)

*   **anopa** — Init system built around the s6 supervision suite.

	[https://jjacky.com/anopa/](https://jjacky.com/anopa/) || [anopa](https://aur.archlinux.org/packages/anopa/)

*   **GNU Shepherd** — Init system written in [Guile](https://www.gnu.org/software/guile/).

	[https://www.gnu.org/software/shepherd/](https://www.gnu.org/software/shepherd/) || [shepherd](https://aur.archlinux.org/packages/shepherd/)

*   **[OpenRC](/index.php/OpenRC "OpenRC")** — Dependency-based init system.

	[http://www.gentoo.org/proj/en/base/openrc/](http://www.gentoo.org/proj/en/base/openrc/) || [openrc](https://aur.archlinux.org/packages/openrc/) [openrc-arch-services-git](https://aur.archlinux.org/packages/openrc-arch-services-git/)

*   **[systemd](/index.php/Systemd "Systemd")** — Dependency-based init system with aggressive parallelization, process supervision using cgroups, and the ability to depend on a given mount point or dbus service.

	[https://freedesktop.org/wiki/Software/systemd/](https://freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

## Inits

*   **[BusyBox](/index.php/BusyBox "BusyBox")** — Utilities for rescue and embedded systems.

	[http://busybox.net/](http://busybox.net/) || [busybox](https://www.archlinux.org/packages/?name=busybox)

*   **ninit** — Fork from [minit](http://www.fefe.de/minit/)

	[http://riemann.fmi.uni-sofia.bg/ninit/](http://riemann.fmi.uni-sofia.bg/ninit/) || [ninit](https://aur.archlinux.org/packages/ninit/)

*   **sinit** — Simple init initially based on Rich Felker’s minimal init.

	[http://core.suckless.org/sinit](http://core.suckless.org/sinit) || [sinit](https://aur.archlinux.org/packages/sinit/)

*   **[SysVinit](/index.php/SysVinit "SysVinit")** — Traditional System V init.

	[http://savannah.nongnu.org/projects/sysvinit](http://savannah.nongnu.org/projects/sysvinit) || [sysvinit](https://aur.archlinux.org/packages/sysvinit/)

## Init scripts

*   **initscripts-fork** — Maintained fork of SysVinit scripts in Arch Linux.

	[https://bitbucket.org/TZ86/initscripts-fork/overview](https://bitbucket.org/TZ86/initscripts-fork/overview) || [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/)

*   **minirc** — Minimal init script designed for BusyBox.

	[https://github.com/hut/minirc/](https://github.com/hut/minirc/) || [minirc-git](https://aur.archlinux.org/packages/minirc-git/)

*   **spark-rc** — A simple rc script to kickstart your system.

	[https://gitlab.com/fbt/spark-rc](https://gitlab.com/fbt/spark-rc) || [spark-rc](https://aur.archlinux.org/packages/spark-rc/)

## Service managers

*   **daemontools** — Collection of tools for managing UNIX services.

	[http://cr.yp.to/daemontools.html](http://cr.yp.to/daemontools.html) || [daemontools](https://aur.archlinux.org/packages/daemontools/)

*   **[Monit](/index.php/Monit "Monit")** — Monit is a process supervision tool for Unix and Linux. With monit, system status can be viewed directly from the command line, or via the native HTTP(S) web server.

	[http://mmonit.com/monit/](http://mmonit.com/monit/) || [monit](https://www.archlinux.org/packages/?name=monit)

*   **perp** — Persistent process (service) supervisor and management framework for UNIX.

	[http://b0llix.net/perp/](http://b0llix.net/perp/) || [perp](https://aur.archlinux.org/packages/perp/)

*   **[runit](/index.php/Runit "Runit")** — UNIX init scheme with service supervision, a replacement for SysVinit, and other init schemes.

	[http://smarden.org/runit/](http://smarden.org/runit/) || [runit](https://aur.archlinux.org/packages/runit/)

*   **s6** — Small suite of programs for UNIX, designed to allow service supervision in the line of daemontools and runit.

	[http://skarnet.org/software/s6/](http://skarnet.org/software/s6/) || [s6](https://aur.archlinux.org/packages/s6/)

## Configuration

### Migrate running services

To run daemons under the new init, save a list of running daemons:

```
$ systemctl list-units --state=running "*.service" > daemons.list

```

and configure the [#Init scripts](#Init_scripts) accordingly. See also [[2]](http://unix.stackexchange.com/questions/175380/how-to-list-all-running-daemons).

**Note:** [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8), [kernel modules](/index.php/Kernel_modules "Kernel modules") and [sysctl](/index.php/Sysctl "Sysctl") may also need configuration.

### logind

[logind](https://www.freedesktop.org/wiki/Software/systemd/logind/) requires *systemd* to be the init process. [[3]](https://www.freedesktop.org/wiki/Software/systemd/InterfacePortabilityAndStabilityChart/) As such, [local sessions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") and other functionality is not available.

**Tip:** A standalone version of *logind* is available as [elogind-git](https://aur.archlinux.org/packages/elogind-git/) [[4]](https://lists.gnu.org/archive/html/guix-devel/2015-04/msg00352.html)

	Device permissions

Add users to respective [user groups](/index.php/User_group "User group") for device access and reboot. Current group membership should first be checked with `id *user*`.

```
# usermod -a -G video,audio,power,disk,storage,optical,lp,scanner *user*

```

See also [Users and groups#Pre-systemd groups](/index.php/Users_and_groups#Pre-systemd_groups "Users and groups"). To create group rules for use with [Polkit](/index.php/Polkit "Polkit"), see [Polkit#Bypass password prompt](/index.php/Polkit#Bypass_password_prompt "Polkit").

	Rootless X (1.16)

As `Xorg.wrap` does not check if logind is active [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=86975#c5), [root rights for Xorg](/index.php/Xorg#Rootless_Xorg "Xorg") need be enabled manually:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = yes` 

	Power management

See [pm-utils](https://aur.archlinux.org/packages/pm-utils/) and [acpid](/index.php/Acpid "Acpid") to replace [Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Scheduled tasks

Arch uses [timer](/index.php/Systemd#Timers "Systemd") files instead of [cron](/index.php/Cron "Cron") by default. See [archlinux-cronjobs](https://github.com/notfoss/archlinux-cronjobs) for basic cron jobs.

### Dbus

User instances of *dbus-daemon* are launched by [systemd/User](/index.php/Systemd/User "Systemd/User") [[7]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/). When requiring IPC between desktop applications, restore `30-dbus.sh`:

 `/etc/X11/xinit/xinitrc.d/30-dbus.sh` 
```
#!/bin/bash

# launches a session dbus instance
if [ -z "${DBUS_SESSION_BUS_ADDRESS-}" ] && type dbus-launch >/dev/null; then
  eval $(dbus-launch --sh-syntax --exit-with-session)
fi
```

## Tips and tricks

### systemd-nspawn

[systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") is a tool for systemd systems. Since Linux 2.6.19 it is however possible to run systemd on a non-systemd system by using PID namespace. For it, the kernel needs to be configured with `CONFIG_PID_NS` and `CONFIG_NAMESPACES`).

The PID namespace creates a new hierarchy of processes starting with PID 1\. In addition to this, systemd requires a chrooted root filesystem to be mounted. Hence, you have to at least make a bind mount, because otherwise some services will fail with

```
"Failed at step NAMESPACE spawning" due to "Invalid operation" 

```

as systemd tries to remount the root with `private` option.

To setup a chroot with a new PID namespace you can use jchroot.[[8]](http://vincent.bernat.im/en/blog/2011-jchroot-isolation.html) [[9]](https://github.com/vincentbernat/jchroot). Make sure not to mount `/proc` inside the new root before chrooting, otherwise systemd will detect the chroot environment. You can mount it later once systemd is running.

### Replacing udev

**Warning:** Replacing udev is not required as *systemd-udev* is functional without *systemd* as PID 1\. Some replacements such as *eudev* can also not coexist with [systemd](https://www.archlinux.org/packages/?name=systemd)—ensure an alternative init is booted **prior** to their installation.

*   **eudev** — eudev is a fork of udev started by the Gentoo project. It is primarily designed and tested with OpenRC.

	[https://wiki.gentoo.org/wiki/Eudev](https://wiki.gentoo.org/wiki/Eudev) || [eudev](https://aur.archlinux.org/packages/eudev/) [eudev-git](https://aur.archlinux.org/packages/eudev-git/)

*   **mdev** — Device manager for usage in embedded systems.

	[https://git.busybox.net/busybox/plain/docs/mdev.txt](https://git.busybox.net/busybox/plain/docs/mdev.txt) || [busybox](https://www.archlinux.org/packages/?name=busybox)

*   **vdev** — A virtual device manager for unix.

	[https://github.com/jcnelson/vdev.git](https://github.com/jcnelson/vdev.git) || [vdev-git](https://aur.archlinux.org/packages/vdev-git/)

*   **smdev** — smdev is a simple program to manage device nodes. It is mostly compatible with mdev but doesn't have all of its features.

	[http://git.suckless.org/smdev/](http://git.suckless.org/smdev/) || [smdev-git](https://aur.archlinux.org/packages/smdev-git/)

## See also

*   [Debian init system debate](https://wiki.debian.org/Debate/initsystem)
*   [How to run s6-svscan as process 1](http://skarnet.org/software/s6/s6-svscan-1.html)
*   [Replace systemd with busybox + minirc](https://bbs.archlinux.org/viewtopic.php?id=162606&p=1)
*   [Experiments of Manjaro](http://www.troubleshooters.com/linux/init/manjaro_experiments.htm)
*   [Init vs. runsv](https://busybox.net/~vda/init_vs_runsv.html)
*   [Demystifying the init system](https://felipec.wordpress.com/2013/11/04/init/)
*   [A history of modern init systems (1992-2015)](http://blog.darknedgy.net/technology/2015/09/05/0/)
*   [Comparison of init systems (gentoo wiki)](https://wiki.gentoo.org/wiki/Comparison_of_init_systems)