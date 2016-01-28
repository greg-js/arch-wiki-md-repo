# hibernate-script

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [pm-utils](/index.php/Pm-utils "Pm-utils")
*   [Laptop](/index.php/Laptop "Laptop")

"Hibernating" or suspending to disk writes all the running processes to the disk (typically to the swap partition), then completely powers down the machine. This resembles suspending to RAM, but while a machine suspended to RAM still requires a small charge from a battery or power source, a hibernated machine does not and can remain hibernated indefinitely. This advantage comes at the cost of additional time needed to hibernate and to resume, since disks (especially HDD swap partitions) write and read slower than RAM.

This guide focuses on hibernate-script (see the [pm-utils](/index.php/Pm-utils "Pm-utils") page for the alternative), a frontend used with the [uswsusp](/index.php/Uswsusp "Uswsusp") ("userspace suspension") and [TuxOnIce](/index.php/TuxOnIce "TuxOnIce") (formerly known as suspend2) hibernate backends. Uswsusp generally works without requiring a patched kernel but should be used with initrd/initramfs. Tuxonice requires a modified kernel, but works without initrd/initramfs and also allows suspending to a swap file if a user does not have, or does not want to use, a swap partition.

## Contents

*   [1 Installation](#Installation)
*   [2 Backend setup](#Backend_setup)
    *   [2.1 Direct Run](#Direct_Run)
    *   [2.2 Setting the suspend method](#Setting_the_suspend_method)
*   [3 Hibernate tricks with the hibernate.script](#Hibernate_tricks_with_the_hibernate.script)
    *   [3.1 Editing /etc/hibernate/common.conf](#Editing_.2Fetc.2Fhibernate.2Fcommon.conf)
    *   [3.2 NVIDIA specific settings](#NVIDIA_specific_settings)
    *   [3.3 Suspending with fglrx](#Suspending_with_fglrx)
    *   [3.4 Dropping disk caches](#Dropping_disk_caches)
    *   [3.5 Specific settings for TuxOnIce](#Specific_settings_for_TuxOnIce)
*   [4 Combining suspend to disk with suspend to RAM](#Combining_suspend_to_disk_with_suspend_to_RAM)
*   [5 Take action based on events](#Take_action_based_on_events)
    *   [5.1 After pressing power button](#After_pressing_power_button)
    *   [5.2 After closing lid](#After_closing_lid)
*   [6 Different methods of suspending to RAM](#Different_methods_of_suspending_to_RAM)
    *   [6.1 The hibernate-script and suspension to RAM](#The_hibernate-script_and_suspension_to_RAM)
    *   [6.2 Sound](#Sound)
    *   [6.3 Automatic suspend and wakeup](#Automatic_suspend_and_wakeup)
    *   [6.4 Automatic suspend, the hard way](#Automatic_suspend.2C_the_hard_way)
    *   [6.5 Controlling wakeup](#Controlling_wakeup)

## Installation

You can install [hibernate-script](https://aur.archlinux.org/packages/hibernate-script/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/hibernate-script)]</sup> from the [AUR](/index.php/AUR "AUR").

## Backend setup

There is a dedicated pages which covers the installing and configuring of these backend:

*   Tuxonice method: [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")
*   Uswsusp method: [Uswsusp](/index.php/Uswsusp "Uswsusp")

### Direct Run

you can suspend to disk with the method with the following command.

Using uswsusp:

```
# hibernate -F /etc/hibernate/ususpend-disk.conf

```

Using TuxOnIce:

```
# hibernate -F /etc/hibernate/tuxonice.conf

```

### Setting the suspend method

Preferred suspend/hibernation method of hibernate-script can be set in the file `/etc/hibernate/hibernate.conf`. If you list several methods, the first one will be used. Note that _hibernate_ can also be used with [Suspend to RAM](/index.php/Suspend_to_RAM "Suspend to RAM") or vanilla uswsusp).

For Uswsusp use:

```
TryMethod ususpend-disk.conf

```

For TuxOnIce use:

```
TryMethod tuxonice.conf

```

## Hibernate tricks with the hibernate.script

This is a brief overview of the hibernate script. If you want to tweak it further, examine the `common.conf` and `suspend2.conf` files further and read the excellent and exhaustive man pages for hibernate and `hibernate.conf`.

### Editing /etc/hibernate/common.conf

The options in this file are used with any hibernation method (actually, the file is sourced by the configuration files of each method) and also by [Suspend to RAM](/index.php/Suspend_to_RAM "Suspend to RAM") when accomplished with the hibernate-script. This file is complex and well commented. The man page `hibernate.conf` describes adequately all the options. Here, we can only stress the most commonly useful parts.

Uncomment the lines for any filesystems that have the potential to change while your computer is suspended (for example shared partitions with windows like vfat or ntfs ones). They will be remounted upon resume. Otherwise you would risk corrupting the filesystems.

```
### filesystems
# Unmount /nfsshare /windows /mnt/sambaserver
# UnmountFSTypes smbfs nfs
# UnmountGraceTime 1
# Mount /windows

```

If you do not explicitly restore the volume levels, ALSA may have the sound channels muted after resuming. If this happens, look for:

```
### services

```

in `/etc/hibernate/common.conf` and change the line just below to:

```
RestartServices alsa

```

The alsa service will be stopped before suspension and restarted after resuming: the sound channels and volumes will be as before. You may want to restart other problematic services here.

A common issue is that some drivers do not support suspension, that is they do not work properly after a suspension cycle or even they prevent the system from suspending or resuming properly. In these cases (which should be reported - at least for modules in the vanilla kernel - to the suspend-devel@lists.sourceforge.net mailing list, so that they can be fixed upstream) you can unload the module before suspension and reload it after resuming: the hibernate-script can automatize this routine with the LoadModules and UnloadModules options. Actually, the hibernate-script already unloads some problematic modules, listed in `/etc/hibernate/blacklisted-modules`, so you can also add the modules in that file.

To re-connect to networks after rebooting, you may want to add:

```
OnSuspend 25 netcfg2 -a
OnResume 20 netcfg-auto-wireless <your-network-interface>

```

This will disconnect from all networks, then should automatically choose the correct one. If you use another way to connect to a network (such as netcfg2 <profile-name> then of-course, put that there instead.

One 'gotcha' to watch out for is the priority level you put on your user-commands, this won't work:

```
OnSuspend 5 netcfg -a

```

You'll need to set the priority as 05 instead. Its normally best to use something within the range of 20-50 for your user scripts.

If you need/want to eject all PcCards before suspending and reinsert them after resuming, change the _EjectCards_ setting in `common.conf`:

```
### pcmcia
EjectCards yes

```

This is necessary on some laptops, if the pccards stop working after resume.

Finally, the most problematic aspect is constituted by the video card: its status needs often to be restored after resuming. In other cases, it is necessary to switch from X to the console. The following options in `/etc/hibernate/common.conf` will probably fix these issues (whose symptom could be a frozen machine or only a black display after resuming):

```
### vbetool
#EnableVbetool yes
#RestoreVbeStateFrom /var/lib/vbetool/vbestate
#VbetoolPost yes
# RestoreVCSAData yes

```

```
### xhacks
#SwitchToTextMode yes
#UseDummyXServer yes
#DummyXServerConfig xorg-dummy.conf

```

You can uncomment one or many of them in order to see if the problem is solved. In order to use the first block of options, you need to install the vbetool package from the extra repository. Each of the option is documented in man `hibernate.conf`. Please note that it is very important to try all the different combinations of these options before than anything else, becaause the problems with the display are the most common source of troubles in a suspension cycle.

### NVIDIA specific settings

If you have an [NVIDIA](/index.php/NVIDIA "NVIDIA") graphics card and use a driver version >177, you need to add the following line to `/etc/hibernate/tuxonice.conf`:

```
ProcSetting extra_pages_allowance 7500

```

A value lower than 7500 might also work on certain systems, though 7500 should be a working default. Setting this option should allow you to hibernate and resume without any additional X hacks. You will also need to comment out the nvidia module in `/etc/hibernate/blacklisted-modules` for this to work.

The suggested value for extra_pages_allowance for driver versions <177 is 0:

```
ProcSetting extra_pages_allowance 0

```

This setting has also been reported to help with the binary ATI driver.

If you have an AGP Nvidia card and are using the binary driver, you might also have to add the following line to your `/etc/X11/xorg.conf`:

```
Option "NvAGP" "1"

```

### Suspending with fglrx

Following addition to `/etc/hibernate/suspend2.conf` is required:

```
# For fglrx
ProcSetting extra_pages_allowance 20000

```

### Dropping disk caches

<small>_From: [drop_caches introduction](http://www.linuxinsight.com/proc_sys_vm_drop_caches.html)_</small>

As a way to speed up suspending, you can free the memory used for disk caches so there will be less to write to the disk. Just add something like this to the `common.conf`:

```
OnSuspend 00 sync; echo 3 > /proc/sys/vm/drop_caches

```

### Specific settings for TuxOnIce

Specific settings for TuxOnIce are in `/etc/hibernate/tuxonice.conf`. Make sure that the following lines are uncommented and appropriately configured:

```
UseTuxOnIce   yes
Compressor    lzo

```

There are a number of additional settings and tweaks which you can set in `/etc/hibernate/tuxonice.conf` and `/etc/hibernate/common.conf`, more information about these can be found on the [TuxOnIce](http://www.tuxonice.net/HOWTO-4.html) website and on the [Suspend to Disk](/index.php/Suspend_to_Disk "Suspend to Disk") page of this wiki.

You can abort a suspend cycle if you press the escape key. If you press a capital R, you will force the system to reboot after hibernation.

If all goes well, you should be able to resume using the same GRUB menu selection. If you make that option the default for GRUB, you will always default to resuming if a resume image is available. It is recommended that you test the suspend/hibernate from a text console first and then once you have confirmed that it works try it from within X.

**Warning:** Never use a different kernel to resume than you used to suspend! If pacman updates your kernel, do not suspend before you have rebooted properly.

You can make this practice safer adding the hibernate-cleanup daemon to your DAEMONS array in `/etc/rc.conf`. This script will make sure that any stale image is deleted from your swap partition at boot time. This should make your system safe also in the case that you have chosen the mistaken kernel at the GRUB prompt. The hibernate-cleanup service is included in the hibernate-script package.

## Combining suspend to disk with suspend to RAM

If your motherboard or laptop supports [Suspend to RAM](/index.php/Suspend_to_RAM "Suspend to RAM"), you can combine it with suspend2\. This will result in the following behavior:

*   When you call hibernate, your system will suspend to disk and after that suspend to RAM instead of powering down.
*   When you turn your system back on, it will resume directly from RAM (which only takes a few seconds)
*   If your battery fails in the meantime (and the image in your memory is therefore lost), you will be able to resumes from disk.

This can be done both with uswsusp and with tuxonice.

With uswsusp, you should use s2both. You can also call s2both from the hibernate script (with all its richness of options), resorting to the `ususpend-both.conf` method. Please note that s2both works only if s2ram (see [Suspend to RAM](/index.php/Suspend_to_RAM "Suspend to RAM")) works in your system. There is no way to force it to work if your laptop model is not whitelisted in s2ram. See [Suspend to RAM](/index.php/Suspend_to_RAM "Suspend to RAM") for instructions about how to whitelist your laptop in the local copy of s2ram and how to report that your laptop suspend to ram properly so that it is whitelisted in the next uswsusp release.

To do it with tuxonice, edit `/etc/hibernate/suspend2.conf`:

```
## Powerdown method - 3 for suspend-to-RAM, 4 for ACPI S4 sleep, 5 for poweroff
PowerdownMethod 3

```

For this to work, your computer must be able to use suspend to RAM also without s2ram.

## Take action based on events

Tuning hibernate-script for context sensitive modal operation. You need to have [acpid](https://www.archlinux.org/packages/?name=acpid) installed.

### After pressing power button

Edit the following file `/etc/acpi/events/power`

```
# This is called when the user presses the power button
event=button/power (PWR.||PBTN)
# To Hibernate uncomment the following line
#action=hibernate 
# To Suspend uncomment the following line
#action=suspend

```

### After closing lid

Edit the following file `/etc/acpi/events/lid`

```
# This is called when the user closes the lid
event=button/lid
# To Hibernate uncomment the following line
#action=hibernate 
# To Suspend uncomment the following line
#action=suspend

```

You can also install [lidsleep](https://aur.archlinux.org/packages/lidsleep/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lidsleep)]</sup> which includes the file altered to use pm-utils and suspend to RAM.

Alternatively you can edit `/etc/acpi/actions/lm_lid.sh` this is the file that is executed when the lid state is changed

Example:

```
#!/bin/bash
# lid button pressed/released event handler
#laptop mode helps minimized hdd activity
test -x /usr/sbin/laptop_mode && /usr/sbin/laptop_mode auto
# get the -xauth variable so we can access the display
XAUTH="$( ps -C X f | sed -n 's/.*-auth \(.*\)/\1/p' )"
if [[ -z $XAUTH ]]; then
  # if XAUTH is blank try another way to get it 
  XAUTH="$( ps -C xinit f | sed -n 's/.*-auth \(.*\)serverauth.*/\1Xauthority/p' )"
fi
#Find out if the lid is open or closed
if grep -q open /proc/acpi/button/lid/LID/state; then
  # the screen is on, forces it to be on
  ACTION="on"
  XAUTHORITY=$XAUTH /usr/bin/xset -display :0.0 dpms force $ACTION
else
  # screen is off, forces off
  ACTION="off"
  XAUTHORITY=$XAUTH /usr/bin/xset -display :0.0 dpms force $ACTION
  # script waits for 10 minutes
  sleep 10m
  # checks to make sure screen is still closed
  if grep -q closed /proc/acpi/button/lid/LID/state; then
    # if it is, then it suspends to disk
    s2disk
  else
    # or it turns it back on
    XAUTHORITY=$XAUTH /usr/bin/xset -display :0.0 dpms force on
  fi
fi

```

The script turns the monitor off or on. But if the screen is left shut for 10 minutes, it will suspend to the disk automatically. `man sleep` for more info on the sleep command.

## Different methods of suspending to RAM

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** use "uswsusp" instead of "s2ram" to refer to [Uswsusp](/index.php/Uswsusp "Uswsusp"). (Discuss in [Talk:Hibernate-script#](https://wiki.archlinux.org/index.php/Talk:Hibernate-script))

There is an application, called `s2ram`, which contains a "whitelist" of known laptop models and, according to what has been reported by other owners of these laptops, tries to do the right things for that specific laptop. The whitelisted laptops can therefore use `s2ram` to suspend to RAM "out of the box". Non-whitelisted laptops need to try different command line options of `s2ram` in order to determine - by trial and error - the appropriate "tricks" needed to make suspend and resume work. Your experience, if reported to the `s2ram` developers, will contribute to whitelist your machine in the next release of `s2ram`.

However, `s2ram` is not the only resource: the hibernate-script, which is commonly used to accomplish [Suspend to Disk](/index.php/Suspend_to_Disk "Suspend to Disk") , supports also suspension to RAM and proposes some further tricks which could convince your machine to suspend to RAM and resume properly. Moreover, the hibernate-script can automatize other useful operations which you could want/need to do before suspension or after resuming from suspension to RAM.

Thus, the first part of this article will be devoted to `s2ram`. The second will discuss the use of the hibernate-script in suspension to RAM. In particular, we will see how the hibernate-script can be used to suspend to RAM your system just with the `s2ram`, but providing some additional tweakings. Finally, we will mention the possibility to suspend the machine both to RAM and to disk.

### The hibernate-script and suspension to RAM

The hibernate-script, developed in the field of the tuxonice project for suspend-to-disk method, can be used also to suspend your machine to RAM. Actually, you can also try to do this directly, performing the required operations before calling the ACPI S3 state. However, the `s2ram` seems to be the leading method nowadays and, through the named whitelist, should assure in the future that virtually any laptop can suspend to RAM without too much hassle. So, the actually best way to use the power of the hibernate-script for suspension to RAM is to use it to call `s2ram`.

You can edit `/etc/hibernate/hibernate.conf` to select `ususpend-ram.conf` as the default action called by:

```
# hibernate

```

Just put the following as the first uncommented line:

```
 TryMethod ususpend-ram.conf

```

However, may be that you want to use the hibernate-script primarily to suspend to disk. In that case you should resort to the ram-specific configuration file from the command line:

```
# hibernate -F /etc/hibernate/ususpend-ram.conf

```

Now you should configure the script. Please note that the options that you put in `/etc/hibernate/common.conf` will be used anytime you call hibernate (that is also for suspension to disk). On the contrary, the options in `/etc/hibernate/ususpend-ram.conf` will be used only when you suspend to RAM with the `s2ram` method.

The hibernate-script options are exhaustively described in the man page `hibernate.conf`.

First of all, may be that some module is preventing you from accomplishing a proper suspension cycle. In this case, list it in the UnloadModules: it will be unloaded before suspension and reloaded after resuming. Note that the hibernation script already does this for some blacklisted modules, whose list is `/etc/hibernate/blacklisted-modules`.

If you discover that a module is guilty, you should report this to the suspend-devel@lists.sourceforge.net, so that the bad behaviour of the module can be fixed.

May be also that your display is the guilty and that the tricks provided by `s2ram` are not enough. The hibernate-script has some further tricks:

The relevant block of options is the following:

```
### vbetool
#EnableVbetool yes
#RestoreVbeStateFrom /var/lib/vbetool/vbestate
#VbetoolPost yes
# RestoreVCSAData yes

```

```
### xhacks
#SwitchToTextMode yes
#UseDummyXServer yes
#DummyXServerConfig xorg-dummy.conf

```

However, most of these tricks are already attempted by `s2ram` and you should not duplicate the effort. Only three tricks in this section are specific to the script. The first is to uncomment both the following two lines:

```
EnableVbetool yes
RestoreVbeStateFrom /var/lib/vbetool/vbestate

```

Please note that, while `s2ram` uses an internal vbetool component, the hibernate-script relies on the vbetool package in the extra repo, so you should install it. Basically, this combination of options do something similar to the `--vbe_save` `s2ram` option, but, instead of restoring the state saved immediately before suspension, it restores a state manually saved by the user in the file /var/lib/vbetool/vbestate (or any other file you have chosen). You can try to save the state in a peculiar safe situation, like immediately after booting, or before any switching from X to console and back. You can save the state with the following command:

```
# vbetool vbestate save > /var/lib/vbetool/vbestate

```

The second peculiar trick (very often required!) is to uncomment the following line:

```
SwitchToTextMode yes

```

The script will switch from X to console before suspension and back to X after a successful resuming.

Finally, the UseDummyXServer trick uses a second XServer, with a minimal safe configuration only during the suspension cycle, restoring the full fledged X server only after a complete resume. This can be useful with cards with problematic proprietary drivers: the dummy xserver will use the standard vesa driver instead. Anyway, this last trick should be seldom useful nowadays, because also proprietary drivers seem to support suspension without too many problems.

The hibernate-script gives you many other useful possibilities (such as restarting services, unmounting partitions, ejecting pccards, and so on). Read about them in the man pages.

### Sound

If you do not explicitly restore the volume level, ALSA may have the sound channels muted after resuming. If this happens, you can edit `/etc/suspend.conf` by adding

```
RestartServices alsa

```

### Automatic suspend and wakeup

Once you have suspend to RAM working, you will probably want it to happend automatically e.g., when you close the laptop lid.

There are several ways to do this. The easiest is to use a high-level power management tool such as KDE's PowerDevil. Another is to create your own ACPI event handler scripts.

### Automatic suspend, the hard way

ACPI events are managed by configuration files in `/etc/acpi/events/`. (The laptop-mode-tools package contains some examples). A default configuration file called 'anything' is provided by the acpid package, which runs `/etc/acpi/handler.sh` on every event.

An simple event configuration file to manage the opening and closing of a laptop lid (that could be called `/etc/acpi/events/lid`) looks like this:

```
event=button[ /]lid
action=/etc/acpi/actions/lid_handler.sh %e

```

The first line specifies the names of the events applicable to this file with a regexp. You can get the names of events by enabling event logging in acpid and looking at `/var/log/acpid`.

The second line specifies an executable to be run when an applicable event occurs. The `%e` is a variable containing arguments that the event provides. It's a good idea to provide them to the program.

It's customary to put handling programs in `/etc/acpi/actions/`. A possible implementation of `lid_handler.sh` in the previous example could be:

```
#!/bin/sh
# check if the lid is open or closed, using the /proc file
if grep closed /proc/acpi/button/lid/LID/state >/dev/null ; then
    # if the lid is now closed, save the network state and suspend to RAM
    netcfg all-suspend
    pm-suspend
else
    # if the lid is now open, restore the network state.
    # (if we are running, a wakeup has already occured!)
    netcfg all-resume
fi

```

The same example, adapted for wicd instead of netcfg:

```
#!/bin/sh
# check if the lid is open or closed, using the /proc file
if grep closed /proc/acpi/button/lid/LID/state >/dev/null ; then
    # if the lid is now closed, save the network state and suspend to RAM
    /usr/lib/wicd/suspend.py
    pm-suspend
else
    # if the lid is now open, restore the network state.
    # (if we are running, a wakeup has already occured!)
    /usr/lib/wicd/autoconnect.py
fi

```

Remember to make it executable. With some basic knowledge of shell scripting, you have a lot of possibilities.

### Controlling wakeup

The ACPI events that trigger wakeup are controlled through the procfile /proc/acpi/wakeup. An example output is:

```
root@hex in /proc/acpi $ cat wakeup
Device  S-state   Status   Sysfs node
LID       S3    *enabled
PBTN      S4    *enabled
MBTN      S5     enabled
PCI0      S3     disabled  no-bus:pci0000:00
USB0      S0     disabled  pci:0000:00:1d.0
USB1      S0     disabled  pci:0000:00:1d.1
USB2      S0     disabled  pci:0000:00:1d.2
USB3      S0     disabled  pci:0000:00:1d.3
EHCI      S0     disabled  pci:0000:00:1d.7
AZAL      S3     disabled  pci:0000:00:1b.0
PCIE      S4     disabled  pci:0000:00:1e.0
RP01      S4     disabled  pci:0000:00:1c.0
RP02      S3     disabled
RP03      S3     disabled
RP04      S3     disabled  pci:0000:00:1c.3
RP05      S3     disabled
RP06      S3     disabled

```

To toggle whether an event will trigger a wakeup, pipe its name into the /proc/acpi/wakeup. (Note that every name in the file must have 4 letters, so if it is shorter e.g. LID, it needs be prepended with spaces). So to prevent opening the laptop lid from triggering a wakeup, you could do:

```
root@hex in /proc/acpi $ echo " LID" > wakeup
root@hex in /proc/acpi $ cat wakeup
Device  S-state   Status   Sysfs node
LID       S3    *disabled
PBTN      S4    *disabled
MBTN      S5     disabled
PCI0      S3     disabled  no-bus:pci0000:00
...

```

Another thing to note is that the PBTN and MBTN events were also toggle with the LID event. Sometimes events are linked, so that all of them will be enable and disabled in unison. Checking the 'dmesg' command can confirm this:

```
root@hex in /proc/acpi $ dmesg
...
ACPI: 'PBTN' and 'LID' have the same GPE, can't disable/enable one separately
ACPI: 'MBTN' and 'LID' have the same GPE, can't disable/enable one separately

```

This may not actually affect the other events. On a Dell Inspiron 6400, for example, the power button always triggers a wake up. Your mileage may vary.

None of this will persist between boots, so you might want to add the echo command to `/etc/rc.local` so it is executed on every boot:

```
# disable the laptop lid switch
echo " LID" > /proc/acpi/wakeup

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hibernate-script&oldid=392232](https://wiki.archlinux.org/index.php?title=Hibernate-script&oldid=392232)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Power management](/index.php/Category:Power_management "Category:Power management")

Hidden categories:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")