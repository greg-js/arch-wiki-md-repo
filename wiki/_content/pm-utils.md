# pm-utils

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Uswsusp](/index.php/Uswsusp "Uswsusp")
*   [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Need to address pm-utils relevance compared to systemd's suspend functions (Discuss in [Talk:Pm-utils#](https://wiki.archlinux.org/index.php/Talk:Pm-utils))

**Warning:** Hibernating with Pm-utils and then updating systemd is reported to corrupt files: [https://bbs.archlinux.org/viewtopic.php?pid=1423442](https://bbs.archlinux.org/viewtopic.php?pid=1423442)

**pm-utils** is a suspend and powerstate setting framework. It is designed to replace such scripts as those provided by the `powersave` package.

pm-utils is a collection of shell scripts that wrap the kernel mode suspend/resume with the various hacks. These hacks are needed to work around bugs in drivers and subsystems that are not yet aware of suspend. It is easily extensible by putting custom hooks into a directory, which can either be done by the system administrator or those hooks can be part of a package, especially if this package needs special attention during a system suspend or power state transition.

A lesser known feature is one that mimics toggling done by [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools").

Used in conjunction with the [cpupower](/index.php/Cpupower "Cpupower") package, notebook (and desktop) owners are provided with a complete power management suite.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing alternative suspend backend (optional)](#Installing_alternative_suspend_backend_.28optional.29)
*   [2 Basic configuration](#Basic_configuration)
    *   [2.1 Standby/suspend to RAM](#Standby.2Fsuspend_to_RAM)
    *   [2.2 Hibernation (suspend2disk)](#Hibernation_.28suspend2disk.29)
    *   [2.3 Suspend/hibernate as regular user](#Suspend.2Fhibernate_as_regular_user)
        *   [2.3.1 User permission method](#User_permission_method)
    *   [2.4 Power saving](#Power_saving)
        *   [2.4.1 Change brightness depending on AC state](#Change_brightness_depending_on_AC_state)
    *   [2.5 Suspend on idle/inactivity](#Suspend_on_idle.2Finactivity)
    *   [2.6 Using Swap file instead of regular swap partition](#Using_Swap_file_instead_of_regular_swap_partition)
*   [3 Advanced configuration](#Advanced_configuration)
    *   [3.1 Available variables for use in config files](#Available_variables_for_use_in_config_files)
    *   [3.2 Disabling a hook](#Disabling_a_hook)
        *   [3.2.1 Alternative method](#Alternative_method)
    *   [3.3 Creating your own hooks](#Creating_your_own_hooks)
*   [4 How it works](#How_it_works)
    *   [4.1 Pm-suspend internals](#Pm-suspend_internals)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Segmentation faults](#Segmentation_faults)
    *   [5.2 Reboot instead of resume from suspend](#Reboot_instead_of_resume_from_suspend)
    *   [5.3 Resume from suspend shuts down instead of wake up](#Resume_from_suspend_shuts_down_instead_of_wake_up)
    *   [5.4 Blank screen when waking from suspend](#Blank_screen_when_waking_from_suspend)
    *   [5.5 VirtualBox problems](#VirtualBox_problems)
    *   [5.6 Hibernate with missing swap partition](#Hibernate_with_missing_swap_partition)
    *   [5.7 Black screen with unblinking cursor when trying to suspend](#Black_screen_with_unblinking_cursor_when_trying_to_suspend)
    *   [5.8 Blank screen issue](#Blank_screen_issue)
    *   [5.9 Unable to resume with 64 bit OS](#Unable_to_resume_with_64_bit_OS)
    *   [5.10 Black screen when waking from hibernate with radeon driver](#Black_screen_when_waking_from_hibernate_with_radeon_driver)
    *   [5.11 Computer does not turn off when hibernating](#Computer_does_not_turn_off_when_hibernating)
    *   [5.12 Display not powering on after suspension (radeon)](#Display_not_powering_on_after_suspension_.28radeon.29)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Having the HD power management level automatically set again on resume](#Having_the_HD_power_management_level_automatically_set_again_on_resume)
    *   [6.2 Restarting the mouse](#Restarting_the_mouse)
    *   [6.3 Add sleep modes to Openbox menu](#Add_sleep_modes_to_Openbox_menu)
    *   [6.4 Handling "sleep" and "power" buttons](#Handling_.22sleep.22_and_.22power.22_buttons)
    *   [6.5 Locking the screen saver on hibernate or suspend](#Locking_the_screen_saver_on_hibernate_or_suspend)
    *   [6.6 Disabling hibernation via polkit](#Disabling_hibernation_via_polkit)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") the [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) package which is available in the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:**

*   If you run into issues when resuming video, it might be necessary to also install [vbetool](https://www.archlinux.org/packages/?name=vbetool) from the [official repositories](/index.php/Official_repositories "Official repositories").
*   If you are starting from a clean install, make sure that you have [acpi](https://www.archlinux.org/packages/?name=acpi) installed.

Run `pm-suspend`, `pm-suspend-hybrid` or `pm-hibernate` as root to trigger suspend manually. The suspend scripts write log to `/var/log/pm-suspend.log`.

### Installing alternative suspend backend (optional)

The Arch Linux package ships with support for the following backends: `kernel`, `tuxonice` and `uswsusp` which can be seen from command:

```
pacman -Ql pm-utils | grep module.d

```

Suspend backend is specified by the `SLEEP_MODULE` configuration variable in `/etc/pm/config.d` and defaults to the `kernel` backend. To use the alternative suspend backends the respective packages need to be installed. Both of these are available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   uswsusp - [uswsusp-git](https://aur.archlinux.org/packages/uswsusp-git/)<sup><small>AUR</small></sup>
*   tuxonice - [linux-ice](https://aur.archlinux.org/packages/linux-ice/)<sup><small>AUR</small></sup> / [linux-pf](/index.php/Linux-pf "Linux-pf")

Furthermore, [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) ships with its own video quirks database in `/usr/lib/pm-utils/video-quirks/`.

## Basic configuration

### Standby/suspend to RAM

In the ideal case, running `pm-suspend` as root should initiate suspend to memory, meaning that all running state will be preserved in RAM and all components other than RAM will be shut down to conserve power. Pressing the power button should initiate a resume from this state.

**Note:** It is always recommended to put your network drivers in SUSPENDED_MODULES because most wireless drivers are known to cause issues after standby. Intel's iwlwifi, Atheros' ath5k and Realtek's r8* drivers were all reported to have issues after resume on the forums. Iwlwifi even drops to 1Mbps connection if it is not reloaded after resume.

In some cases, it is possible that running `pm-suspend` causes hangs or other issues. This may be due to specific "misbehaving" modules. If you know which modules could cause such issues, adding a `SUSPEND_MODULES` config to `/etc/pm/config.d/modules` of the form:

```
SUSPEND_MODULES="uhci_hd button ehci_hd iwlwifi"

```

should cause these modules to be specifically unloaded before suspend and reloaded after resume.

To configure invoking `pm-suspend` automatically on power events like laptop lid close, please refer to [Acpid](/index.php/Acpid "Acpid").

### Hibernation (suspend2disk)

You need to follow instructions in [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate") in order to set up hibernation.

Alternatively, if you do not use the `kernel` backend, see [Uswsusp#Configuration](/index.php/Uswsusp#Configuration "Uswsusp") or [TuxOnIce#Setting up the bootloader](/index.php/TuxOnIce#Setting_up_the_bootloader "TuxOnIce").

### Suspend/hibernate as regular user

Three methods are available to suspend without the need for a root password: using [Udev](/index.php/Udev "Udev"), using UPower, and giving the user the appropriate permissions with [visudo](/index.php/Sudo "Sudo").

#### User permission method

Because the [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) scripts must be run as root, you may want to make the scripts accessible to normal users by running sudo without the root password. To do so, edit the `/etc/sudoers` file with `visudo` as root. For more information, see [sudo](/index.php/Sudo "Sudo").

Add the following lines, replacing `_username_` with your own user name, then save and exit `visudo`:

```
_username_  ALL = NOPASSWD: /usr/sbin/pm-hibernate
_username_  ALL = NOPASSWD: /usr/sbin/pm-suspend

```

Or you can enable it for a group, using the following lines, replacing `_group_`:

```
%_group_   ALL = NOPASSWD: /usr/sbin/pm-hibernate
%_group_   ALL = NOPASSWD: /usr/sbin/pm-suspend

```

**Note:** These must come after any user privilege specifications, e.g., `username ALL=(ALL) ALL`, or they will not work.

You can now run the scripts without a password by simply running:

```
$ sudo pm-hibernate

```

or:

```
$ sudo pm-suspend

```

Also, add yourself to the `power` [group](/index.php/Group "Group") so that way using things like applets to do suspend will work. If you do not do this, when you try to use suspend though things like [GNOME](/index.php/GNOME "GNOME")'s shutdown applet, your computer will just play a very annoying loud triple beep and lock the screen.

```
# gpasswd -a _username_ power

```

You should now be able to use your [Desktop environment](/index.php/Desktop_environment "Desktop environment")'s power management tools to automatically suspend or hibernate when doing things like closing the laptop lid, running low on battery power, etc.

### Power saving

pm-utils supports running commands depending on whether the system is connected to the AC adapter or not; therefore, a script has to be created inside the folder `/etc/pm/power.d/`. An example of such a script can be found in the [crunchbang forum](http://crunchbanglinux.org/forums/post/110148/#p110148). Be aware that upower must be running in order to detect changing AC states [(see more information)](https://bbs.archlinux.org/viewtopic.php?id=132125).

#### Change brightness depending on AC state

One possible example looks as follows and changes brightness according to the AC state. Create a file called `/etc/pm/power.d/00-brightness` with the following content and change the path to the brightness setting as well as the value written into the file with echo according to your system.

```
#!/bin/bash

case $1 in
    true)
        echo "Enable screen power saving"
        echo 5 > /sys/class/backlight/acpi_video0/device/backlight/acpi_video0/brightness
    ;;
    false)
        echo "Disable screen power saving"
        echo 14 > /sys/class/backlight/acpi_video0/device/backlight/acpi_video0/brightness
    ;;
esac

```

### Suspend on idle/inactivity

One method relies on xautolock program. Add following: `xautolock -time 30 -locker "sudo pm-suspend" -detectsleep &` to `~/.xinitrc`. This implies that `pm-suspend` is called after 30 minutes of inactivity.

### Using Swap file instead of regular swap partition

If you want use swap file instead of regular swap partition, see [Swap File](/index.php/Swap#Swap_file "Swap").

## Advanced configuration

The main configuration file is `/usr/lib/pm-utils/defaults`. You _should not edit this file_, since after a package update it might be overwritten with the default settings. Put your config file into `/etc/pm/config.d/` instead. You can just put a simple text file with

```
SUSPEND_MODULES="button uhci_hcd"

```

named `modules` or `config` into `/etc/pm/config.d` and it will override the settings in the system-wide configuration file.

### Available variables for use in config files

SUSPEND_MODULES="button"

the list of modules to be unloaded before suspend

SLEEP_MODULE="tuxonice uswsusp kernel"

the default sleep/wake systems to try

HIBERNATE_MODE="shutdown"

forces the system to shut down rather than reboot

### Disabling a hook

If a hook is run which you do not like or which you think is not useful or even harmful, we would appreciate a bug report for that. You can however easily disable hooks by just creating an empty file corresponding to the hook in `/etc/pm/sleep.d/`. Say you want to disable the hook `/usr/lib/pm-utils/sleep.d/45pcmcia`, you can do this easily by calling

```
# touch /etc/pm/sleep.d/45pcmcia

```

Do not set the executable bit on that dummy-hook.

Note: Make sure you create the dummy files in the appropriate directory. For example if you are trying to disable hooks in /usr/lib/pm-utils/power.d, you will need to place the dummy file in /etc/pm/power.d.

#### Alternative method

Create a file in `/etc/pm/config.d` with the modules you want to blacklist in the `HOOK_BLACKLIST` variable. For example, to manage power saving yourself, use:

```
HOOK_BLACKLIST="hal-cd-polling intel-audio-powersave journal-commit laptop-mode pcie_aspm readahead sata_alpm sched-powersave xfs_buffer wireless"

```

### Creating your own hooks

**Note:** If you are using systemd, then these hooks located in sleep.d will probably not work. In these cases you want to consider using [sleep hooks](/index.php/Power_management#Sleep_hooks "Power management") of systemd.

If you want to do something specific to your setup during suspend or hibernate, then you can easily put your own hook into `/etc/pm/sleep.d`. The hooks in this directory will be called in alphabetic order during suspend (that is the reason their names all start with 2 digits, to make the ordering explicit) and in the reverse order during resume. The general convention to be followed on number ordering is:.

00 - 49

User and most package supplied hooks. If a hook assumes that all of the usual services and userspace infrastructure is still running, it should be here.

50 - 74

Service handling hooks. Hooks that start or stop a service belong in this range. At or before 50, hooks can assume that all services are still enabled.

75 - 89

Module and non-core hardware handling. If a hook needs to load/unload a module, or if it needs to place non-video hardware that would otherwise break suspend or hibernate into a safe state, it belongs in this range. At or before 75, hooks can assume all modules are still loaded.

90 - 99

Reserved for critical suspend hooks.

I am showing a pretty useless demonstration hook here, that will just put some informative lines into your log file:

```
#!/bin/bash
case $1 in
    hibernate)
        echo "Hey guy, we are going to suspend to disk!"
    ;;
    suspend)
        echo "Oh, this time we are doing a suspend to RAM. Cool!"
    ;;
    thaw)
        echo "Oh, suspend to disk is over, we are resuming..."
    ;;
    resume)
        echo "Hey, the suspend to RAM seems to be over..."
    ;;
    *)  echo "Somebody is calling me totally wrong."
    ;;
esac

```

Put this into `/etc/pm/sleep.d/66dummy`, do a `chmod +x /etc/pm/sleep.d/66dummy` and it will spew some useless lines during suspend and resume.

**Warning:** All the hooks run as root. This means that you need to be careful when creating temporary files, check that the `PATH` environment variable is set correctly, etc. to avoid security problems.

## How it works

The concept is quite easy: the main script (`pm-action`, called via symlinks as either `pm-suspend`, `pm-hibernate` or `pm-suspend-hybrid`) executes so-called "hooks", executable scripts, in the alphabetical sorted order with the parameter `suspend` (suspend to RAM) or `hibernate` (suspend to disk). Once all hooks are done, it puts the machine to sleep. After the machine has woken up again, all those hooks are executed in reverse order with the parameter `resume` (resume from RAM) or `thaw` (resume from disk). The hooks perform various tasks, such as preparing the bootloader, stopping the Bluetooth subsystem, or unloading of critical modules.

Both `pm-suspend` and `pm-hibernate` are usually called from [Udev](/index.php/Udev "Udev"), initiated by desktop applets like [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager) or `kpowersave`.

**Note:** `suspend-hybrid` is a placeholder right now -- it is not completely implemented.

There is also the possibility to set the machine into high-power and low-power mode, the command `pm-powersave` is used with an additional parameter of `true` or `false`. It works basically the same as the suspend framework.

The hooks for suspend are placed in

`/usr/lib/pm-utils/sleep.d`

distribution / package provided hooks

`/etc/pm/sleep.d`

hooks added by the system administrator

The hooks for the power state are placed in

`/usr/lib/pm-utils/power.d`

distribution / package provided hooks

`/etc/pm/power.d`

hooks added by the system administrator

Hooks in `/etc/pm/` take precedence over those in `/usr/lib/pm-utils/`, so the system administrator can override the defaults provided by the distribution.

### Pm-suspend internals

This outlines the internal actions when `pm-suspend` is run, describing how `pm-utils` gracefully falls back onto the kernel method if the requirements of other methods are not met.

```
$ pm-suspend

```

The first step is set-up preliminary variables and source parent scripts:

```
export STASHNAME=pm-suspend
export METHOD="$(echo ${0##*pm-} |tr - _)"
. "/usr/lib/pm-utils/pm-functions"

```

The variable `METHOD` is extracted from the executable name, _suspend_ from `pm-suspend` and _hibernate_ from `pm-hibernate`.

The location of runtime configuration parameters is defined in `/usr/lib/pm-utils/pm-functions` as _PM_UTILS_RUNDIR="/var/run/pm-utils"_ and _STORAGEDIR="${PM_UTILS_RUNDIR}/${STASHNAME}/storage"_. Therefore _STORAGEDIR="/var/run/pm-utils/pm-suspend/storage"_; this is where `pm-suspend` will cache its configuration. Disabled hooks are stored as plain text files with the hook name prefixed by "_disable_hook:_". Configuration parameters are appended to the _parameters_ file:

 `$  ls -lah /var/run/pm-utils/pm-suspend/storage/` 

```
-rw-r--r-- 1 root root  20 May 19 09:57 disable_hook:99video
-rw-r--r-- 1 root root   0 May 19 02:59 parameters
-rw-r--r-- 1 root root 247 May 19 02:59 parameters.rm
-rw-r--r-- 1 root root   9 May 19 02:59 state:cpu0_governor
-rw-r--r-- 1 root root   9 May 19 02:59 state:cpu1_governor

```

Then `pm-functions` will source the files located in `/etc/pm/config.d/` in addition to `/usr/lib/pm-utils/defaults`. Upon returning, `pm-functions` will proceed to source the files specified by **$SLEEP_METHOD** as `/usr/lib/pm-utils/module.d/$SLEEP_METHOD[...]` if they exist:

```
for mod in $SLEEP_MODULE; do
    mod="${PM_UTILS_LIBDIR}/module.d/${mod}"
    [ -f "$mod" ] || continue
    . "$mod"
done

```

Otherwise, if **$SLEEP_MODULE** is empty, `do_suspend()` will be set to the kernel backend as described above:

```
if [ -z "$SUSPEND_MODULE" ]; then
    if grep -q mem /sys/power/state; then
       SUSPEND_MODULE="kernel"
       do_suspend() { echo -n "mem" >/sys/power/state; }
    elif [ -c /dev/pmu ] && pm-pmu --check; then
       SUSPEND_MODULE="kernel"
       do_suspend() { pm-pmu --suspend; }
    elif grep -q standby /sys/power/state; then
       SUSPEND_MODULE="kernel"
       do_suspend() { echo -n "standby" >/sys/power/state; }
    fi
fi

```

Assuming **$SLEEP_MODULE** is not empty and `uswsusp` is specified, `/usr/lib/pm-utils/module.d/uswsusp` is executed. This script checks several requirements (these are the requirements for being able to use uswsusp):

*   [ -z $SUSPEND_MODULE ]
*   command_exists s2ram
*   grep -q mem /sys/power/state || ( [ -c /dev/pmu ] && pm-pmu --check; );

If these requirements are met, do_suspend() is defined as:

```
do_suspend()
{
   uswsusp_get_quirks
   s2ram --force $OPTS
}

```

Most importantly, the `uswsusp` module runs:

```
add_before_hooks uswsusp_hooks
add_module_help uswsusp_help

```

The first function, _add_before_hook_ disables the **pm-utils** hooks **99video** since this functionality is subsumed by **s2ram**. The second function, _add_module_help_, adds uswsusp-module-specific help, which in essence replaces the help function provided by **99video**.

Back to `pm-suspend`:

```
command_exists "check_$METHOD" && command_exists "do_$METHOD"
"check_$METHOD"

```

This verifies that the _check_suspend_ and _do_suspend_ methods have been defined. The _check_suspend_ method simply verifies that $SUSPEND_MODULE is not empty:

```
check_suspend() { [ -n "$SUSPEND_MODULE" ]; }

```

Lastly, `pm-suspend` must run all hooks that have not been disabled, sync file-system buffers, and run _do_suspend_:

```
if run_hooks sleep "$ACTION $METHOD"; then
    # Sleep only if we know how and if a hook did not inhibit us.
    log "$(date): performing $METHOD"
    sync
    "do_$METHOD" || r=128
    log "$(date): Awake."

```

The method _run_hooks_ is a wrapper for __run_hooks_, which the case of `pm-suspend` is called as _run_hooks sleep "suspend suspend"_. Given that:

```
PARAMETERS="${STORAGEDIR}/parameters"
PM_UTILS_LIBDIR="/usr/lib/pm-utils"
PM_UTILS_ETCDIR="/etc/pm"

```

The method __run_hooks_, will for each hook in _"${PM_UTILS_LIBDIR}/$1.d"_ and _"${PM_UTILS_ETCDIR}/$1.d"_, check that sleep has not been inhibited and update the runtime parameters stored in _$PARAMETERS_ before running each hook via _run_hook $hook $2_. In the case of Suspend-to-RAM, all the hooks in _{/usr/lib/pm-utils/sleep.d/,/etc/pm/sleep.d/}_ will be enumerated, and _run_hook_ will be passed the parameters _$hook_ and "_suspend suspend_". The method _run_hook_ uses the _hook_ok_ function to verify that the hook has not been disabled before executing the hook with the "_suspend suspend_" parameters.

## Troubleshooting

If suspend or hibernate did not work correctly, you will probably find some information in the log file `/var/log/pm-suspend.log`. For example, which hooks were run and what the output of them was should be in that log file.

Also, check the output of the `pm-is-supported` command. This command (with the `--hibernate` or `--suspend` flag) will do some sanity checking and report any errors it finds in your configuration. It will not detect all possible errors, but may still be useful.

### Segmentation faults

If you experience segmentation faults that might result in an unresponsive system and missing keys then try to set the UUID in the resume-path in `/boot/grub/menu.lst` as explained [above](#Hibernation_.28suspend2disk.29).

### Reboot instead of resume from suspend

This problem started when saving NVS area during suspend was introduced (in 2.6.35-rc4) ([mailing list post](http://www.spinics.net/lists/linux-acpi/msg29521.html)). However, it is known that this mechanism does not work on all machines, so the kernel developers allow the user to disable it with the help of the `acpi_sleep=nonvs` kernel command line option (see [kernel parameters](/index.php/Kernel_parameters "Kernel parameters")).

### Resume from suspend shuts down instead of wake up

On an Acer Aspire AS3810TG, resuming from suspend shuts down the computer instead of waking it up. If you experience a similar issue, try passing the parameter `i8042.reset=1` to your kernel. In [GRUB](/index.php/GRUB "GRUB"), the line in `/boot/grub/grub.cfg` should be something like this:

```
linux /vmlinuz-linux root=/dev/vg00/root resume=/dev/vg00/swap i8042.reset=1 ro

```

Although I have not tested this, you could also set this parameter live without having to restart by doing:

```
# sysctl -e -w i8042.reset=1

```

### Blank screen when waking from suspend

Some laptops (e.g. Dell Inspiron Mini 1018) will just show a black screen with no backlight after resuming from suspend. If this happens to you, try going into the BIOS of the laptop and disabling Intel SpeedStep if it is present.

You could also try, without disabling SpeedStep, creating a quirk in `/etc/pm/sleep.d/` with this content (requires [vbetool](https://www.archlinux.org/packages/?name=vbetool)):

```
#!/bin/sh
#
case "$1" in
    suspend)
    ;;
    resume)
        sleep 5
        vbetool dpms off
        vbetool dpms on
    ;;
    *) exit $NA
    ;;
esac

```

save it as you want but with a `00` in front of the name so this is called last when resuming; remember to `chmod +x` the script. Try adjusting the `sleep` time if the other commands are called too soon, or if it works well, you can also try removing that line.

Some other laptops (e.g. Toshiba Portégé R830) will just show a black screen with no backlight after resuming from suspend, with fans blowing at top speed. If this is what you're seeing, try going into the BIOS and disable the VT-d virtualization setting by switching to "VT-x only".

### VirtualBox problems

The VirtualBox kernel modules cause `pm-suspend` and `pm-hibernate` to fail on some laptops. (See [this discussion](https://bbs.archlinux.org/viewtopic.php?id=123354)). Instead of suspending or hibernating, the system freezes and indicator LEDs blink (the suspend indicator in the case of ThinkPads and the Caps Lock and Scroll Lock indicators in the case of the MSI Wind U100). The `pm-suspend` and `pm-hibernate` logs appear normal.

The problem can be fixed by removing the modules before suspension or hibernation and reloading them afterwards. That can be accomplished through a script:

```
#!/bin/sh

rmmod vboxdrv
pm-hibernate
modprobe vboxdrv
```

**Note:** Some users reported that it is sufficient to rebuild the kernel module by running `vboxbuild` as root.

### Hibernate with missing swap partition

If you try to hibernate without an active swap partition, your system will look like it is going into hibernate, and then immediately resume again. There are no error messages warning you that there is no swap partition, even when verbose logging is activated, so this problem can be very hard to debug. On my system, the swap partition was somehow corrupted and deactivated, so this may happen even if you set up a swap partition during install. If hibernate displays this behaviour, make sure that you actually have a swap partition that is being used as such. The output of the `blkid` command should look e.g. like

 `# blkid` 

```
/dev/sda1: UUID="00000-000-000-0000000" TYPE="ext2" 
/dev/sda2: UUID="00000-000-000-0000000" TYPE="ext4"
/dev/sda3: UUID="00000-000-000-0000000" TYPE="ext4"
/dev/sda4: UUID="00000-000-000-0000000" TYPE="swap"
```

with one of the lines having `"swap"` as the type. If this is not the case, consult [Swap#Swap partition](/index.php/Swap#Swap_partition "Swap") for instructions on re-creating/activating the swap partition.

### Black screen with unblinking cursor when trying to suspend

If you get a black screen with unblinking cursor when trying to do

```
$ sudo pm-suspend

```

have a look at `/var/log/pm-suspend.log` and search for "ehci" or "xhci". Some of the names you could find may be "ehci_hd", "xhci_hd" or "ehci_hcd".

Then as root create the file `/etc/pm/config.d/modules` and include this code with the exact name of the ehci or xhci module you found. For example:

```
SUSPEND_MODULES="ehci_hcd"

```

Suspend should now be working.

### Blank screen issue

Some users have reported having issues with their laptops not resuming after a suspend or hibernate. This is due to the `autodetect` hook in "HOOKS" array of the `/etc/mkinitcpio.conf` file. This can be disabled using the same method for adding the `resume` hook. Just remove `autodetect` from the list and follow the steps to build the new image. See [Resume Hook](#Mkinitcpio_Resume_Hook) for more details on building the new image.

**Note:** If you are using [plymouth](/index.php/Plymouth "Plymouth") it may be an other reason to this issue. Adding `resume` before `plymouth` in "HOOKS" array of the `/etc/mkinitcpio.conf` file should fix this.

### Unable to resume with 64 bit OS

Certain motherboards/BIOS combinations (specifically known are some Zotac ITX boards, perhaps others) will not resume properly from suspend if any 64 bit operating system is installed. The solution is the enter your BIOS setup and Disable the "Memory Remapping Hole" in your DRAM configuration page. This will probably fix the suspend to RAM problem but will probably result in your OS not detecting all of your RAM.

### Black screen when waking from hibernate with radeon driver

When using the radeon driver and having `radeon` in the `HOOKS` array of the `/etc/mkinitcpio.conf` resuming from hibernation results in the screen being black, however everything else working (testable by keeping a console open with a command to execute and starting the execution after resuming). This seems to be related to using `radeon.dpm=1` (default since kernel 3.13) as the power management method in radeon.

Removing `radeon` from the HOOKS array (and rebuiling the initrd) fixes this problem. (See [here](https://bugs.freedesktop.org/show_bug.cgi?id=72716).)

### Computer does not turn off when hibernating

It is possible that after Linux hibernates and has written the data to disk, the computer does not power off properly. If it is then forcefully powered off and later restarted, resuming will work fine.

This can easily be fixed by making an executable file named `/etc/pm/config.d/hibernate_mode` which contains the single line: `HIBERNATE_MODE="shutdown"` . After that pm-hibernate should properly shut down the computer.

### Display not powering on after suspension (radeon)

If you get a blank display after suspension with radeon gpu, try to create `/etc/pm/config.d/radeon`, and add the following:

 `/etc/pm/config.d/radeon` 

```
QUIRK_S3_BIOS="true"
QUIRK_S3_MODE="true"
```

## Tips and tricks

### Having the HD power management level automatically set again on resume

Do it like this:

 `/etc/pm/sleep.d/50-hdparm_pm` 

```
 #!/bin/dash

 if [ -n "$1" ] && ([ "$1" = "resume" ] || [ "$1" = "thaw" ]); then
 	hdparm -B 254 /dev/sda > /dev/null
 fi

```

Then run:

```
# chmod +x /etc/pm/sleep.d/50-hdparm_pm

```

If the above [Bash](/index.php/Bash "Bash") script fails the work, the following may work instead:

 `/etc/pm/sleep.d/50-hdparm_pm` 

```
 #!/bin/sh

 . "${PM_FUNCTIONS}"
 case "$1" in
        thaw|resume)
                sleep 6
                hdparm -B 254 /dev/sda
                ;;
        *)
                ;;
 esac
 exit $NA

```

Lower `-B` switch values may be effective. See [hdparm](/index.php/Hdparm "Hdparm").

### Restarting the mouse

On some laptops the mouse will hang after an otherwise successful suspend. One way to remedy this is to force a re-initialization of the PS/2 driver (here `i8042`) through a hook in `/etc/pm/hooks` (see [hooks](#Creating_your_own_hooks))

```
#!/bin/sh
echo -n "i8042" > /sys/bus/platform/drivers/i8042/unbind
echo -n "i8042" > /sys/bus/platform/drivers/i8042/bind

```

### Add sleep modes to Openbox menu

Openbox users can add the new scripts as additional shutdown options within the Openbox menu by adding the items to a new or existing sub-menu in `~/.config/openbox/menu.xml`, for example:

```
<menu id="64" label="Shutdown">
	<item label="Lock"> <action name="Execute"> <execute>xscreensaver-command -lock</execute> </action> </item>
	<item label="Logout"> <action name="Exit"/> </item>
	<item label="Reboot"> <action name="Execute"> <execute>sudo shutdown -r now</execute> </action> </item>
	<item label="Poweroff"> <action name="Execute"> <execute>sudo shutdown -h now </execute> </action> </item>
	**<item label="Hibernate"> <action name="Execute"> <execute>sudo pm-hibernate</execute> </action> </item>**
	**<item label="Suspend"> <action name="Execute"> <execute>sudo pm-suspend</execute> </action> </item>**
</menu>

```

### Handling "sleep" and "power" buttons

"Sleep" and "power" buttons are handled by `acpid` in `/etc/acpi/handler.sh` (see "button/power" and "power/sleep" entries). You may want to substitute the default actions with calls to `pm-suspend` and `pm-hibernate`.

Please note that [systemd](/index.php/Power_management#ACPI_events "Power management") handles power events on its own and does not use pm-utils or any scripts from `/etc/pm/*`.

### Locking the screen saver on hibernate or suspend

You may wish to run a screen locking utility when the system suspends (so that a password is required after waking up). This can be done by adding a script to the `/etc/pm/sleep.d` folder. Make sure the script is executable (chmod 755) and owned by `root:root`.

A simple example script is:

 `/etc/pm/sleep.d/00screensaver-lock` 

```
 #!/bin/sh
 #
 # 00screensaver-lock: lock workstation on hibernate or suspend

 username= # add username here; i.e.: username=foobar
 userhome=/home/$username
 export XAUTHORITY="$userhome/.Xauthority"
 export DISPLAY=":0"

  case "$1" in
    hibernate|suspend)
       su $username -c "/usr/bin/slimlock" & # or any other such as /usr/bin/xscreensaver-command -lock
    ;;
    thaw|resume)
    ;;
    *) exit $NA
    ;;
 esac
```

Replace `/usr/bin/slimlock` with the path to your screen locking utility of choice.

If you do not wish to hard-code your username (e.g., if you have multiple users), then it is necessary to determine the current X11 username and display number. For systems using [systemd](/index.php/Systemd "Systemd"), you can use [xuserrun](https://github.com/rephorm/xuserrun) and the following sleep.d script (be sure to modify the path to xuserrun and your desired screen locker):

 `/etc/pm/sleep.d/00screensaver-lock` 

```
#!/bin/sh
#
# 00screensaver-lock: lock workstation on hibernate or suspend

 case "$1" in
   hibernate|suspend)
      /path/to/xuserrun /usr/bin/slimlock & # or any other such as /usr/bin/xscreensaver-command -lock
   ;;
   thaw|resume)
   ;;
   *) exit $NA
   ;;
esac

```

If you have problems using xuserrun, you can instead try having loginctl do this directly. This script will lock all active sessions before going into hibernation:

 `/etc/pm/sleep.d/00screensaver-lock` 

```
#!/bin/sh
#
# 00screensaver-lock: lock workstation on hibernate or suspend

 case "$1" in
   hibernate|suspend)
      loginctl lock-sessions
   ;;
   thaw|resume)
   ;;
   *) exit $NA
   ;;
esac

```

### Disabling hibernation via polkit

In order to disable hibernation, create a new file in /etc/polkit-1/ called 99-disable-hibernate.rules. Then add the following lines:

 `99-disable-hibernate.rules` 

```
polkit.addRule(function(action, subject) {
   if ((action.id == "org.freedesktop.login1.hibernate")) {
      return polkit.Result.NO;
   }
});

polkit.addRule(function(action, subject) {
   if ((action.id == "org.freedesktop.login1.hibernate-multiple-sessions")) {
      return polkit.Result.NO;
   }
});

```

If you're using KDE, log off once and the hibernation option should be gone.

## See also

*   [OpenSUSE Wiki](http://en.opensuse.org/SDB:Pm-utils) - The article from where this was originally sourced (Licensed under GPL)
*   [Understanding Suspend](https://wiki.ubuntu.com/UnderstandingSuspend) - Ubuntu article explaining how suspending to RAM works
*   [PM Debugging](http://www.mjmwired.net/kernel/Documentation/power/basic-pm-debugging.txt#178) - Basic PM debugging
*   [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") - CPU Frequency Scaling and CPU Power schemes
*   [Acpid](/index.php/Acpid "Acpid") - daemon for delivering ACPI events
*   [Hibernate after sleep](http://superuser.com/questions/298672/linuxhow-to-hibernate-after-a-period-of-sleep) - An example of a custom pm-utils hook where hibernation is triggered after a period of time in suspension

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pm-utils&oldid=410957](https://wiki.archlinux.org/index.php?title=Pm-utils&oldid=410957)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Power management](/index.php/Category:Power_management "Category:Power management")