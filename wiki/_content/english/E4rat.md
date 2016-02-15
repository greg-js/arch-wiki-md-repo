[e4rat](http://e4rat.sourceforge.net/) stands for e4 'reduced access time' (ext4 file system only) and is a project by Andreas Rid and Gundolf Kiefer. The [e4rat range of tools](http://e4rat.sourceforge.net/) are comprised of e4rat-collect, e4rat-realloc and e4rat-preload.

Current version is 0.2.3

## Contents

*   [1 Process](#Process)
    *   [1.1 Who benefits, who does not](#Who_benefits.2C_who_does_not)
*   [2 Installation](#Installation)
*   [3 Getting it to work](#Getting_it_to_work)
    *   [3.1 e4rat-collect](#e4rat-collect)
    *   [3.2 e4rat-realloc](#e4rat-realloc)
    *   [3.3 e4rat-preload](#e4rat-preload)
    *   [3.4 Alternative: e4rat-preload-lite](#Alternative:_e4rat-preload-lite)
*   [4 e4rat and init systems](#e4rat_and_init_systems)
*   [5 Bootchart](#Bootchart)
    *   [5.1 bootchart 0.9-9](#bootchart_0.9-9)
    *   [5.2 bootchart2](#bootchart2)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 startup.log is not created](#startup.log_is_not_created)
    *   [6.2 e4rat erroneously reports an ext2 files system](#e4rat_erroneously_reports_an_ext2_files_system)
    *   [6.3 /var/lib/e4rat/startup.log is not accessible](#.2Fvar.2Flib.2Fe4rat.2Fstartup.log_is_not_accessible)
    *   [6.4 Remove annoying message that mess up boot message](#Remove_annoying_message_that_mess_up_boot_message)
*   [7 See also](#See_also)

## Process

If you look at a classical [bootchart](/index.php/Bootchart "Bootchart") you will notice that neither disk nor CPU are utilized fully during the boot process. e4rat changes this to make full use of both disk and CPU during boot process and thus reduce boot time drastically. It consists of three stages:

*   **e4rat-collect** - collect files for a specified time (default 120 seconds but this can be adjusted)
*   **e4rat-realloc** - reallocate files
*   **e4rat-preload** - preload them

### Who benefits, who does not

e4rat has proven to be extremely effective for typical single user set-ups which boot straight into X, perhaps even with a number of programs open. If you have a server set-up and boot only into the CLI your boot time decrease may not be as drastic. Users of SSD drives do not benefit because there are no moving parts and thus (almost) no disk latency - [Ureadahead](/index.php/Ureadahead "Ureadahead") might be worth looking at.

**Note:** **(to ureadahead users)** The [official e4rat manual](http://e4rat.sourceforge.net/wiki/index.php/Main_Page#Ubuntu_and_ureadahead) states that ureadahead conflicts with e4rat. This may be true for Ubuntu but using e4rat in conjunction with ureadahead does work on Arch Linux, although it does not speed up the boot process any further.

It is always better to be safe than sorry. Just make backup if you cannot afford to lose data on your partition.

## Installation

Install [e4rat](https://aur.archlinux.org/packages/e4rat/) from the [AUR](/index.php/AUR "AUR").

**Note:**

*   In order to build it, you must first rebuild [audit](https://www.archlinux.org/packages/?name=audit) from the [ABS](/index.php/ABS "ABS") with `staticlibs` option explicitly enabled. Simply installing the default [audit](https://www.archlinux.org/packages/?name=audit) package will result in a build error.
*   Audit needs these options to be enabled in the kernel configuration (CONFIG_AUDIT) together with support for auditing system calls (CONFIG_AUDITSYSCALL) also see [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). Probably you will need `audit=1` to add to your kernel parameters.

## Getting it to work

Now for the nitty-gritty:

### e4rat-collect

To have e4rat collect a list of files you will need to append `init=/sbin/e4rat-collect` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). For example:

```
kernel /vmlinuz-linux root=/dev/disk/by-label/ARCH init=/sbin/e4rat-collect ro 5

```

This will only have to be done once so you may prefer to append this command on the grub command line itself.

Upon booting e4rat-collect will watch your system for a default of 120 seconds. So if you boot, log into X, open your favourite browser and email client all within 2 minutes, every one of those activities is logged. To change the default of 120 seconds edit `/etc/e4rat.conf`. To manually stop e4rat-collect type:

```
e4rat-collect -k

```

or

```
pkill e4rat-collect

```

Upon successful boot and after having waited the allotted time you should see the file `/var/lib/e4rat/startup.log`.

Do not forget to remove the e4rat-collect command from your [boot loader configuration file](/index.php/Boot_Loader#Configuration_files "Boot Loader") (not necessary if you inserted it on the grub command line).

### e4rat-realloc

Once _e4rat-collect_ has finished to run, log in as root and run:

```
e4rat-realloc /var/lib/e4rat/startup.log

```

This can take a while depending on how many files you have in your startup.log file. Switching to rescue mode with `systemctl isolate rescue` ([Systemd#Targets table](/index.php/Systemd#Targets_table "Systemd")) may allow for more inodes/blocks to be reallocated as some may not be free while in _multiuser.target_

**Note:** It may be worthwhile to repeat the reallocation step multiple times before exiting or rebooting in order to further reduce the fragmentation count. Simply re-run the command a few times to see if this is possible on the your setup. If so you'll see the count number reduced after a few runs. This is perfectly safe and shouldn't cause any issues with booting.

**Note:** Users using SysV-style [init](/index.php/Init "Init") systems must switch to runlevel 1 using `sudo init 1` prior to running `e4rat-realloc`

### e4rat-preload

Append `init=/sbin/e4rat-preload` permanently to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### Alternative: e4rat-preload-lite

An alternative preload binary has been developed by [jlindgren](https://bbs.archlinux.org/viewtopic.php?id=117776&p=1), it saves a few extra seconds from your boot time.

The savings come from

*   using pure C with no external library dependencies, which drops the number of linked .so files from 22 to 3

**Note:** Current [0.2.3] version of e4rat-preload is linked against 5 .so libraries, including libc, libm, libpthread ! So there is not much of a difference here.

*   preloading only the first 100 files (both inodes and file contents) before starting /sbin/init, then continuing to load the remaining files in parallel with the normal boot sequence.

You can install [e4rat-preload-lite](https://aur.archlinux.org/packages/e4rat-preload-lite/) from the [AUR](/index.php/AUR "AUR").

Append (or replace) `init=/usr/sbin/e4rat-preload-lite` permanently to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). Reboot and enjoy.

## e4rat and init systems

e4rat-collect defaults to replacing itself with `/sbin/init` upon completion. With the default `systemd` installation, this file is a symbolic link to `/lib/systemd/systemd`. If you need to specify another process with PID 1, such as `/usr/bin/busybox`, you can change this in `/etc/e4rat.conf` by setting the `init` parameter:

```
init /usr/bin/busybox

```

This allows to launch both `e4rat-preload` and `bootchart` in the same boot sequence.

## Bootchart

**Warning:** This has not worked for and is still in development - any suggestions welcome

You will see a noticeable improvement but nothing can beat a nice [Bootchart](/index.php/Bootchart "Bootchart"). Have it run before and after e4rat installation and gawk at the difference.

### bootchart 0.9-9

This version of [bootchart](/index.php/Bootchart "Bootchart") automatically stops logging as soon as a [display manager](/index.php/Display_manager "Display manager") comes up. Supposedly the following overrides that and continues logging but it does not work for me:

To continue logging adjust your `/etc/bootchartd.conf` as follows:

```
AUTO_STOP_LOGGER="no"

```

To stop it manually type:

```
# bootchartd stop

```

To run both e4rat-preload and bootchart append the following to your grub kernel line:

```
init=/sbin/bootchartd bootchart_init=/sbin/e4rat-preload

```

### bootchart2

To get [bootchart](/index.php/Bootchart "Bootchart")2 working together with e4rat edit `/sbin/bootchartd` and replace the line where it says

```
init="/sbin/init"

```

with

```
init="/sbin/e4rat-preload"

```

This will allow you to measure your boot time with the fine informations that Bootchart2 provides.

It's easy to set up when to stop bootchart2 (on opposite to bootchat) by editing its configuration file `/etc/bootchartd.conf`. Simply adjust the line

```
EXIT_PROC="kdm_greet xterm konsole gnome-terminal metacity mutter compiz ldm icewm-session enlightenment"

```

with any program you want Bootchart2 stop logging when it launches, or rather left it empty for logging to be stopped manually.

## Troubleshooting

If things do not work you may want to try the following.

### startup.log is not created

*   Disable auditd service
*   Check the following for any hints

```
dmesg | grep e4rat

```

*   Try to increase verbosity and loglevel to 31 in your `e4rat.conf`

### e4rat erroneously reports an ext2 files system

Add `rootfstype=ext4` to [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") from your bootloader.

### /var/lib/e4rat/startup.log is not accessible

This suggests that you have `/var` on a separate partition which is not yet mounted during boot. You need move your `startup.log` to an accessible partition (`/etc/e4rat/` is just fine) and adjust your `/etc/e4rat.conf` to reflect this change:

```
startup_log_file /etc/e4rat/startup.log

```

### Remove annoying message that mess up boot message

If you are annoyed by the e4rat-preload message during boot, decrease verbose to 1 in `/etc/e4rat.conf`

## See also

*   [Main discussion on the forum](https://bbs.archlinux.org/viewtopic.php?id=115976)
*   [Improved e4rat-preload - forum thread](https://bbs.archlinux.org/viewtopic.php?id=117776)