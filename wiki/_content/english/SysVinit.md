**Warning:** Arch Linux only has official support for [systemd](/index.php/Systemd "Systemd"). [[1]](https://www.archlinux.org/news/end-of-initscripts-support/) When using SysVinit, please mention so in support requests.

On systems based on SysVinit, **init** is the first process that is executed once the Linux kernel loads. The default init program used by the kernel is `/sbin/init` provided by [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) (by default on new installs, see [systemd](/index.php/Systemd "Systemd")) or [sysvinit](https://aur.archlinux.org/packages/sysvinit/). The word **init** will always refer to sysvinit in this article.

**inittab** is the startup configuration file for init located in `/etc`. It contains directions for init on what programs and scripts to run when entering a specific runlevel.

Although a SysVinit-based Arch system does use init, most of the work is delegated to the [#Main Boot Scripts](#Main_Boot_Scripts). This article concentrates on init and inittab.

## Contents

*   [1 Installation](#Installation)
*   [2 Overview of init and inittab](#Overview_of_init_and_inittab)
*   [3 Switching runlevel](#Switching_runlevel)
    *   [3.1 Through bootloader](#Through_bootloader)
    *   [3.2 After boot up](#After_boot_up)
*   [4 inittab](#inittab)
    *   [4.1 Default Runlevel](#Default_Runlevel)
    *   [4.2 Main Boot Scripts](#Main_Boot_Scripts)
    *   [4.3 Single User Boot](#Single_User_Boot)
    *   [4.4 Gettys and Login](#Gettys_and_Login)
    *   [4.5 Ctrl+Alt+Del](#Ctrl.2BAlt.2BDel)
    *   [4.6 X Programs](#X_Programs)
    *   [4.7 Power-Sensing Scripts](#Power-Sensing_Scripts)
    *   [4.8 Custom Keyboard Request](#Custom_Keyboard_Request)
        *   [4.8.1 Trigger the kbrequest](#Trigger_the_kbrequest)
*   [5 Writing rc.d scripts](#Writing_rc.d_scripts)
    *   [5.1 Guideline](#Guideline)
    *   [5.2 Available functions](#Available_functions)
    *   [5.3 Example](#Example)
*   [6 Runlevels](#Runlevels)
    *   [6.1 Comparison to systemd targets](#Comparison_to_systemd_targets)
    *   [6.2 List of initscripts runlevels](#List_of_initscripts_runlevels)
    *   [6.3 Runlevel invocation](#Runlevel_invocation)
    *   [6.4 Adding runlevels](#Adding_runlevels)
        *   [6.4.1 First method](#First_method)
        *   [6.4.2 Another way, without adding any symlink](#Another_way.2C_without_adding_any_symlink)
    *   [6.5 Other distributions](#Other_distributions)
*   [7 See also](#See_also)

## Installation

Install [sysvinit](https://aur.archlinux.org/packages/sysvinit/) [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/) from the [AUR](/index.php/AUR "AUR"). This step will remove [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat), and you will use sysvinit on reboot. To restore [systemd](/index.php/Systemd "Systemd"), append `init=/usr/lib/systemd/systemd` to the [kernel command line](/index.php/Kernel_command_line "Kernel command line").

A snapshot of init scripts as packaged in Arch Linux before [migration to systemd](https://www.archlinux.org/news/end-of-initscripts-support/) is available at [arch-rcscripts](https://bitbucket.org/TZ86/arch-rcscripts/src/3e83aeed6c68c6252b8db1428c10a717bc9e05ff/community/?at=master). For support with newer packages, see [#Writing rc.d scripts](#Writing_rc.d_scripts).

See [Init#Configuration](/index.php/Init#Configuration "Init") for generic configuration steps.

## Overview of init and inittab

init is always process 1 and, other than managing some swap space, is the parent process to **all** other processes. You can get an idea of where init lies in the process hierarchy of your system with `pstree`:

 `$ pstree -Ap` 
```
init(1)-+-acpid(3432)
        |-crond(3423)
        |-dbus-daemon(3469)
        |-gpm(3485)
        |-mylogin(3536)
        |-ngetty(3535)---login(3954)---zsh(4043)---pstree(4326)
        |-polkitd(4033)---{polkitd}(4035)
        |-syslog-ng(3413)---syslog-ng(3414)
        `-udevd(643)-+-udevd(3194)
                     `-udevd(3218)

```

Besides usual initialization of system (as the name suggests), init also handles rebooting, shutdown and booting into recovery mode (single-user mode). To support these, inittab groups entries into different **runlevel**s. The runlevels Arch uses are 0 for halt, 1 (aliased as S) for single-user mode, 3 for normal booting (multi-user mode), 5 for X and 6 for reboot. Other distros may adopt other conventions, but the meanings of 0, 1 and 6 are universal.

Upon execution, init scans inittab and carry out appropriate actions. An entry in inittab takes the form

```
id:runlevels:action:process

```

Where `id` is a unique identifier for the entry (just a name, no real impact on init), and `runlevels` is a (not delimited) string of runlevels. If the runlevel init is entering appears in `runlevels`, `action` is carried out, executing `process` if appropriate. Some special `action`s would cause init to ignore `runlevels` and adopt a special matching method. More explanation follows in the next section.

See also `man 5 inittab` and `man 8 init`.

## Switching runlevel

### Through bootloader

To change the runlevel the system boots into, simply add the desired runlevel `n` to the respective bootloader's configuration line. A common application of this is [Start X at login#inittab](/index.php/Start_X_at_login#inittab "Start X at login"). To boot to the desired runlevel, add its number to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") (e.g. `3` for runlevel 3).

The run-level was appended to the end so the kernel knows what run-level to start with. To use another init program (e.g. [systemd](/index.php/Systemd "Systemd")), add `init=/bin/systemd` or similar.

**Note:** If using some init other than sysvinit, the runlevel parameter might be ignored.

### After boot up

After the system has booted up, you may issue `telinit n` to inform init to change the runlevel to `n`. init then reads inittab and "diffs" runlevel n and current runlevel - killing processes not present in the new runlevel and carrying out actions not present in the old runlevel. Processes present in both runlevels are left untouched. The killing procedure is actually a little complex; again, technical details can be found in the init manpage.

init doesn't watch inittab. You need to call `telinit` explicitly to apply modifications to inittab. The command `telinit q` causes init to re-examine inittab but not switch runlevel.

## inittab

In this section we examine common entries in inittab, in the same order as they appear in the default inittab used by Arch. After that there are a few examples to help you create your own inittab entry.

**Warning:** Always test a modified `/etc/inittab` with `telinit q` before you reboot, or a small syntax error can prevent your system from booting.

### Default Runlevel

The default runlevel is 3\. Uncomment or add this if you prefer to boot into runlevel 5 (which is used for X conventionally) by default:

```
id:5:initdefault:

```

### Main Boot Scripts

These are the main Arch init scripts.

```
rc::sysinit:/etc/rc.sysinit
rs:S1:wait:/etc/rc.single
rm:2345:wait:/etc/rc.multi
rh:06:wait:/etc/rc.shutdown

```

### Single User Boot

Sometimes your kernel may fail to boot up all the way, due to a corrupted or dead hard drive or filesystem, missing key files, etc. In that case your init image may automatically enter into **single-user mode** which only allows root login and uses `/sbin/sulogin` instead of `/sbin/login` to control the login process. You can also boot into single-user mode by appending the letter `S` to your kernel command line in your [GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), or [syslinux](/index.php/Syslinux "Syslinux") configuration. If you would like something other than sulogin to run, specify it here.

```
su:S:wait:/sbin/sulogin -p

```

### Gettys and Login

These are crucial entries that run the [gettys](/index.php/Getty "Getty") on your terminals. Most default configurations will have several gettys running on ttys1-6 which is what pops up on your screen with the login prompt. Also see openvt, chvt, stty, and ioctl.

```
c1:234:respawn:/sbin/agetty 9600 tty1 xterm-color
c5:5:respawn:/sbin/agetty 57600 tty2 xterm-256color

```

### Ctrl+Alt+Del

When the special key sequence `Ctrl+Alt+Del` is pressed, this determines what to do.

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

```

### X Programs

If you are not afraid to debug, you can figure out how to start all sorts of programs from inittab. One useful type of program is to start your login manager when the runlevel is 5, multi-user-x-mode. In the following example you can see how to start [SLiM](/index.php/SLiM "SLiM") when entering runlevel 5.

```
x:5:respawn:/usr/bin/slim >/dev/null 2>&1
#x:5:respawn:/usr/bin/xdm -nodaemon -confi /etc/X11/xdm/archlinux/xdm-config

```

### Power-Sensing Scripts

Init can communicate with your UPS device and execute processes based on the status of the UPS. Here are some examples:

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

```

### Custom Keyboard Request

The following line adds a custom function for when a special key sequence is pressed. You can modify this special key sequence to be anything you like, similar to a `Ctrl+Alt+Del`.

```
kb::kbrequest:/usr/bin/wall "Keyboard Request -- edit /etc/inittab to customize"

```

#### Trigger the kbrequest

You can trigger the special key sequence **kbrequest** by sending the WINCH signal to the init process (1) as root (via sudo). In this example, the command:

```
kill -WINCH 1

```

Causes `wall` to write to all ttys:

```
Broadcast message from root@askapachehost (console) (Wed Oct 27 14:02:26 2010):
Keyboard Request -- edit /etc/inittab to customize

```

## Writing rc.d scripts

Initscripts uses rc.d scripts to used to control the starting, stopping and restarting of [daemons](/index.php/Daemons "Daemons").

### Guideline

*   Source `/etc/rc.conf`, `/etc/rc.d/functions`, and optionally `/etc/conf.d/DAEMON_NAME`.
*   Arguments and other daemon options should be placed in `/etc/conf.d/DAEMON_NAME`. This is done to separate configuration from logic and to keep a consistent style among daemon scripts.
*   Use functions in `/etc/rc.d/functions` instead of duplicating their functionality.
*   Include at least start, stop and restart as arguments to the script.

### Available functions

*   There are some functions provided by `/etc/rc.d/functions`:
    *   `stat_busy "*message*"`: set status *busy* for printed message (e.g. Starting daemon [BUSY])
    *   `stat_done`: set status *done* (e.g. Starting daemon [DONE])
    *   `stat_fail`: set status *failed* (e.g. Starting daemon [FAILED])
    *   `get_pid *program*`: get PID of the program
    *   `ck_pidfile *PID-file* *program*`: check whether PID-file is still valid for the program (e.g. ck_pidfile /var/run/daemon.pid daemon || rm -f /var/run/daemon.pid)
    *   `[add|rm]_daemon *program*`: add/remove program to running daemons (stored in `/run/daemons/`)

Full list of functions is much longer and most possibilities (like way to control whether or not non-root users can launch daemon) are still undocumented and can be learned only from `/etc/rc.d/functions` source. See also `man rc.d`.

### Example

The following is an example for *crond*. Look in `/etc/rc.d` for greater variety.

The configuration file:

 `/etc/conf.d/crond`  `ARGS="-S -l info"` 

The actual script:

 `/etc/rc.d/crond` 
```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

DAEMON=crond
ARGS=

[ -r /etc/conf.d/$DAEMON ] && . /etc/conf.d/$DAEMON

PID=$(get_pid $DAEMON)

case "$1" in
 start)
   stat_busy "Starting $DAEMON"
   [ -z "$PID" ] && $DAEMON $ARGS &>/dev/null
   if [ $? = 0 ]; then
     add_daemon $DAEMON
     stat_done
   else
     stat_fail
     exit 1
   fi
   ;;
 stop)
   stat_busy "Stopping $DAEMON"
   [ -n "$PID" ] && kill $PID &>/dev/null
   if [ $? = 0 ]; then
     rm_daemon $DAEMON
     stat_done
   else
     stat_fail
     exit 1
   fi
   ;;
 restart)
   $0 stop
   sleep 1
   $0 start
   ;;
 *)
   echo "usage: $0 {start|stop|restart}"  
esac

```

## Runlevels

**Note:** [systemd](/index.php/Systemd "Systemd") is used by default, which uses targets (see `man systemd.target`) rather than runlevels.

From the [init](http://unixhelp.ed.ac.uk/CGI/man-cgi?init+8) man page:

	*A runlevel is a software configuration of the system which allows only a selected group of processes to exist. The processes spawned by init for each of these runlevels are defined in the /etc/inittab file.*

If something goes wrong with your Arch setup in such way that you are completely helpless when the system boots up, you may need this.

For example, if you use some deffective display drivers, the system may freeze when the X server starts. If you have a display manager in your startup daemons list, you need to take full control of your system before that daemon starts.

And how do you do that?

What you need is called "booting to another runlevel". This basically determines in what state the system will be when the boot sequence terminates. Normally you finish in the multi-user mode with all daemons started (=runlevel 3).

### Comparison to systemd targets

| systemd Target | SysV Runlevel | Notes |
| runlevel0.target, poweroff.target | 0 | Shut down the system. |
| runlevel1.target, rescue.target | 1, s, single | Single user mode. |
| runlevel2.target, runlevel4.target, multi-user.target | 2, 4 | User-defined/Site-specific runlevels. By default, identical to 3. |
| runlevel3.target, multi-user.target | 3 | Multi-user, non-graphical. Users can usually login via multiple consoles or via the network. |
| runlevel5.target, graphical.target | 5 | Multi-user, graphical. Usually has all the services of runlevel 3 plus a graphical login. |
| runlevel6.target, reboot.target | 6 | Reboot |
| emergency.target | emergency | Emergency shell |

### List of initscripts runlevels

And what are the possible runlevels?

*   1: Single user (maintainance mode): You want to use this one if you have problems.
*   3: Multi user: Normal mode
*   5: Multi user with X11: The same as 3 but with X11 loaded in virtual terminal 8 by default
*   0: Halt
*   6: Reboot
*   2, 4: Not used

Take a look to `/etc/inittab` to see how it works.

### Runlevel invocation

You specify what runlevel you would like to enter on the kernel commandline. You just have to pass the number of the desired runlevel as an option on that commandline, so it may look like this if you are in trouble and you want to use single user mode (only the last number is important here)

```
kernel /vmlinuz-linux ... root=/dev/sda2 ro **1**

```

And yes, in a case when you can not boot, you will have to append the runlevel number to the the kernel command line in the boot manager during bootup.

### Adding runlevels

#### First method

Throughout this page, 4 will be used for an example since it is not used by default in Arch. To create another runlevel:

```
cd /etc
cp rc.multi rc.multi4
sed -i "s/DAEMONS/DAEMONS4/g" /etc/rc.multi4

```

The execution of sed will change `/etc/rc.multi4` to look at the new DAEMONS array that will be defined in a couple of steps.

Next, we will add our new `/etc/rc.multi4` script to `/etc/[inittab](/index.php/Inittab "Inittab")` by changing this line:

```
rm:2345:wait:/etc/rc.multi

```

to:

```
rm:235:wait:/etc/rc.multi
ra:4:wait:/etc/rc.multi4

```

You can also add a new line to `/etc/inittab` to execute another script or program to do anything you would like.

Example: Log into X as a single user for a special purpose:

```
xa:4:respawn:/bin/su - $USER -c "/usr/bin/startx"

```

The next step will be to add a new DAEMONS array to your `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` file, call it `DAEMONS4=(...)` and populate this array with any daemons you would like to run for the new runlevel.

The `/etc/rc.conf` gives the suggestion to put a `!` in front of daemons you want to disable. How this is handled in the default `/etc/rc.multi`, is that anything prefaced with the `!` is skipped. A downside to this is if you use the above method to define a different set of daemons for your new runlevel (i.e, want to stop some, keep others going, and/or start new ones) any daemon prefaced with `!` will not be stopped when switching to or from your new runlevel. The following `/etc/rc.multi` changes this behavior.

Example:

 `/etc/rc.multi` 
```
 #!/bin/bash
 #
 # /etc/rc.multi
 #

 . /etc/rc.conf
 . /etc/rc.d/functions

 run_hook multi_start

 # Load sysctl variables if sysctl.conf is present
 [ -r /etc/sysctl.conf ] && /sbin/sysctl -q -p &>/dev/null

 # Start daemons
 # _remember to change DAEMONS in next line for the file /etc/rc.multi4
 for daemon in "${DAEMONS[@]}"; do
         if [ "$daemon" = "${daemon#!}" ]; then
                 # check to see if daemon is running.
                 ck_daemon $daemon
                 if [ $? -eq 1 ]; then
                         # daemon is running, skip it.
                         status_started
                 else
                         # daemon is not running, start it.
                         if [ "$daemon" = "${daemon#@}" ]; then
                                 start_daemon $daemon
                         else
                                 start_daemon_bkgd ${daemon:1}
                         fi
                 fi
         else
                 # check previous runlevel. if it's N, then we've just booted
                 #   and do not need to stop any daemons. otherwise, stop daemons
                 #   when runlevel changes as requested in DAEMONS array.
                 if [ `/sbin/runlevel | cut -d ' ' -f 1` != "N" ] ; then
                         ck_daemon ${daemon:1}
                         if [ $? -eq 1 ] ; then
                                  # daemon is running, let's stop it.
                                  stop_daemon ${daemon:1}
                         fi
                 fi
         fi
 done

 if [ -x /etc/rc.local ]; then
         /etc/rc.local
 fi

 run_hook multi_end

 # vim: set ts=2 noet:

```

Here is what this does:

```
DAEMONS=(syslog-ng network netfs sshd alsa !jack !gpm)      # runlevel 3
DAEMONS4=(syslog-ng network netfs !sshd alsa jack gpm)      # runlevel 4

```

In runlevel 3, jack and gpm are disabled, and in runlevel 4 sshd is not needed, but jack and gpm are. The above `/etc/rc.multi` script will scan the daemons array and check for:

```
1) if a daemon is running (without `!`). if it is, skip it. if not, start it.
2) if a daemon is disabled (`!`), stop it. (this is skipped on boot-up)
3) it still honors starting daemons in the background (`@`)

```

In the above example, when going from runlevel 3 to runlevel 4, syslog-ng, network, netfs, and alsa are checked and found to be running so they'll be skipped. sshd will be disabled then jack and gpm will be started. And when going from runlevel 4 to runlevel 3, syslog-ng, network, netfs, and alsa are still running, so will be skipped again, but jack and gpm will be stopped, while sshd will be started again.

In summary:

```
1) copy `/etc/rc.multi` to `/etc/rc.multi4`
2) add DAEMONS4 to the end of your `/etc/rc.conf` and add daemons to it
2) be sure to change `/etc/rc.multi4` by changing DAEMONS to DAEMONS4
3) edit `/etc/inittab` to add the runlevel and take appropriate actions

```

If you do use the above `/etc/rc.multi`, proper operation is for it to be both your main `/etc/rc.multi` and your new `/etc/rc.multi4` to ensure that all daemons are processed as you desire. It will not break your system to have two different versions of `/etc/rc.multi`.

While your new runlevel setup should not be written over by any system updates, it is always handy to have backups on hand in the event that something unforeseen happens.

#### Another way, without adding any symlink

With a simple modification on `/etc/rc.multi`, runlevels can be simply added by adding a new DAEMONS line in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`.

Here is the patch:

```
--- rc.multi	2008-06-22 23:58:29.000000000 +0200
+++ rc.multi.new	2008-06-23 00:14:05.000000000 +0200
@@ -11,8 +11,25 @@
 # Load sysctl variables if sysctl.conf is present
 [ -r /etc/sysctl.conf ] && /sbin/sysctl -q -p &>/dev/null

+# Load the appropriate DAEMONS array according to runlevel specified in the kernel boot cmdline
+RUNLEVEL=""
+FINAL_DAEMONS=()
+ 
+for param in `cat /proc/cmdline`; do
+  param_rl=`echo $param | grep ^runlevel`
+  if [ ! "$param_rl" = "" ]; then
+    RUNLEVEL=`echo $param_rl | sed -r -e "s#runlevel=(.+)#\1#"`
+  fi
+done;
+
+if [ "${RUNLEVEL}" = "" ]; then
+	eval FINAL_DAEMONS=(${DAEMONS[@]})
+else
+	eval FINAL_DAEMONS=(\${DAEMONS_${RUNLEVEL}[@]})
+	if [ "${#FINAL_DAEMONS[@]}" = "0" ]; then
+		eval FINAL_DAEMONS=(${DAEMONS[@]})
+	fi	
+fi
+
 # Start daemons
-for daemon in "${DAEMONS[@]}"; do
+for daemon in "${FINAL_DAEMONS[@]}"; do
 	if [ "$daemon" = "${daemon#!}" ]; then
 		if [ "$daemon" = "${daemon#@}" ]; then
 			/etc/rc.d/$daemon start

```

Now, to add a runlevel, add a new array in `/etc/rc.conf` (in this example I named it `FOO`):

```
DAEMONS_FOO=( ...whatever... )

```

and to run the system with this runlevel, simply add `runlevel=FOO` to your boot arguments in [LILO](/index.php/LILO "LILO") or [GRUB](/index.php/GRUB "GRUB").

### Other distributions

Runlevels exist in all Linux distributions and while runlevel 1 is usually single-user "emergency mode", 0 means halt and 6 mean reboot, the meaning of other runlevels varies from one distribution to another.

## See also

*   [Wikipedia: Init](https://en.wikipedia.org/wiki/Init "wikipedia:Init")
*   [Linux Knowledge Base and Tutorial. Run Levels.](http://www.linux-tutorial.info/modules.php?name=MContent&pageid=65)
*   [Linux.com. Introduction to runlevels and inittab](http://www.linux.com/articles/114107)
*   [Linux.com. An introduction to services, runlevels, and rc.d scripts.](http://www.linux.com/news/enterprise/systems-management/8116-an-introduction-to-services-runlevels-and-rcd-scripts)