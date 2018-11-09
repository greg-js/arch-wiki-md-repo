Related articles

*   [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate")
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [sysctl](/index.php/Sysctl "Sysctl")
*   [udev](/index.php/Udev "Udev")

[Power management](https://en.wikipedia.org/wiki/Power_management "wikipedia:Power management") is a feature that turns off the power or switches system's components to a low-power state when inactive.

In Arch Linux, power management consists of two main parts:

1.  Configuration of the Linux kernel, which interacts with the hardware.
    *   [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters")
    *   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
    *   [udev](/index.php/Udev "Udev") rules
2.  Configuration of userspace tools, which interact with the kernel and react to its events. Many userspace tools also allow to modify kernel configuration in a "user-friendly" way. See [#Userspace tools](#Userspace_tools) for the options.

## Contents

*   [1 Userspace tools](#Userspace_tools)
    *   [1.1 Console](#Console)
    *   [1.2 Graphical](#Graphical)
*   [2 Power management with systemd](#Power_management_with_systemd)
    *   [2.1 ACPI events](#ACPI_events)
        *   [2.1.1 Power managers](#Power_managers)
        *   [2.1.2 xss-lock](#xss-lock)
    *   [2.2 Suspend and hibernate](#Suspend_and_hibernate)
        *   [2.2.1 Hybrid-sleep on suspend or hibernation request](#Hybrid-sleep_on_suspend_or_hibernation_request)
    *   [2.3 Sleep hooks](#Sleep_hooks)
        *   [2.3.1 Suspend/resume service files](#Suspend.2Fresume_service_files)
        *   [2.3.2 Combined Suspend/resume service file](#Combined_Suspend.2Fresume_service_file)
        *   [2.3.3 Hooks in /usr/lib/systemd/system-sleep](#Hooks_in_.2Fusr.2Flib.2Fsystemd.2Fsystem-sleep)
    *   [2.4 Troubleshooting](#Troubleshooting)
        *   [2.4.1 Delayed lid switch action](#Delayed_lid_switch_action)
        *   [2.4.2 Suspend from corresponding laptop Fn key not working](#Suspend_from_corresponding_laptop_Fn_key_not_working)
*   [3 Power saving](#Power_saving)
    *   [3.1 Processors with HWP (Hardware P-state) support](#Processors_with_HWP_.28Hardware_P-state.29_support)
    *   [3.2 Audio](#Audio)
    *   [3.3 Backlight](#Backlight)
    *   [3.4 Bluetooth](#Bluetooth)
    *   [3.5 Web camera](#Web_camera)
    *   [3.6 Kernel parameters](#Kernel_parameters)
        *   [3.6.1 Disabling NMI watchdog](#Disabling_NMI_watchdog)
        *   [3.6.2 Writeback Time](#Writeback_Time)
        *   [3.6.3 Laptop Mode](#Laptop_Mode)
    *   [3.7 Network interfaces](#Network_interfaces)
        *   [3.7.1 Intel wireless cards (iwlwifi)](#Intel_wireless_cards_.28iwlwifi.29)
    *   [3.8 Bus power management](#Bus_power_management)
        *   [3.8.1 Active State Power Management](#Active_State_Power_Management)
        *   [3.8.2 PCI Runtime Power Management](#PCI_Runtime_Power_Management)
        *   [3.8.3 USB autosuspend](#USB_autosuspend)
        *   [3.8.4 SATA Active Link Power Management](#SATA_Active_Link_Power_Management)
    *   [3.9 Hard disk drive](#Hard_disk_drive)
    *   [3.10 CD-ROM or DVD drive](#CD-ROM_or_DVD_drive)
*   [4 Tools and scripts](#Tools_and_scripts)
    *   [4.1 Using a script and an udev rule](#Using_a_script_and_an_udev_rule)
    *   [4.2 Print power settings](#Print_power_settings)
*   [5 See also](#See_also)

## Userspace tools

Using these tools can replace setting a lot of settings by hand. Only run **one** of these tools to avoid possible conflicts as they all work more or less similarly. Have a look at the [power management category](/index.php/Category:Power_management "Category:Power management") to get an overview on what power management options exist in Arch Linux.

These are the more popular scripts and tools designed to help power saving:

### Console

*   **[acpid](/index.php/Acpid "Acpid")** — A daemon for delivering ACPI power management events with netlink support.

	[http://sourceforge.net/projects/acpid2/](http://sourceforge.net/projects/acpid2/) || [acpid](https://www.archlinux.org/packages/?name=acpid)

*   **[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")** — Utility to configure laptop power saving settings, considered by many to be the de facto utility for power saving though may take a bit of configuration.

	[https://github.com/rickysarraf/laptop-mode-tools](https://github.com/rickysarraf/laptop-mode-tools) || [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/)

*   **[powertop](/index.php/Powertop "Powertop")** — A tool to diagnose issues with power consumption and power management to help set power saving settings.

	[https://01.org/powertop/](https://01.org/powertop/) || [powertop](https://www.archlinux.org/packages/?name=powertop)

*   **[systemd](/index.php/Systemd "Systemd")** — A system and service manager.

	[https://freedesktop.org/wiki/Software/systemd/](https://freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[TLP](/index.php/TLP "TLP")** — Advanced power management for Linux.

	[http://linrunner.de/tlp](http://linrunner.de/tlp) || [tlp](https://www.archlinux.org/packages/?name=tlp)

### Graphical

*   **batterymon-clone** — Simple battery monitor tray icon.

	[https://github.com/jareksed/batterymon-clone](https://github.com/jareksed/batterymon-clone) || [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/)

*   **cbatticon** — Lightweight and fast battery icon that sits in your system tray.

	[https://github.com/valr/cbatticon](https://github.com/valr/cbatticon) || [cbatticon](https://www.archlinux.org/packages/?name=cbatticon)

*   **GNOME Power Statistics** — System power information and statistics for GNOME.

	[https://gitlab.gnome.org/GNOME/gnome-power-manager](https://gitlab.gnome.org/GNOME/gnome-power-manager) || [gnome-power-manager](https://www.archlinux.org/packages/?name=gnome-power-manager)

*   **KDE Power Devil** — Power management module for Plasma.

	[https://userbase.kde.org/Power_Devil](https://userbase.kde.org/Power_Devil) || [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) [powerdevil-light](https://aur.archlinux.org/packages/powerdevil-light/)

*   **LXQt Power Management** — Power management module for LXQt.

	[https://github.com/lxqt/lxqt-powermanagement](https://github.com/lxqt/lxqt-powermanagement) || [lxqt-powermanagement](https://www.archlinux.org/packages/?name=lxqt-powermanagement)

*   **MATE Power Management** — Power management tool for MATE.

	[https://github.com/mate-desktop/mate-power-manager](https://github.com/mate-desktop/mate-power-manager) || [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager)

*   **MATE Power Statistics** — System power information and statistics for MATE.

	[https://github.com/mate-desktop/mate-power-manager](https://github.com/mate-desktop/mate-power-manager) || [mate-power-manager](https://www.archlinux.org/packages/?name=mate-power-manager)

*   **Xfce Power Manager** — Power manager for Xfce.

	[https://docs.xfce.org/xfce/xfce4-power-manager/start](https://docs.xfce.org/xfce/xfce4-power-manager/start) || [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager)

*   **vattery** — Battery monitoring application written in Vala that will display the status of a laptop battery in a system tray.

	[http://www.jezra.net/projects/vattery](http://www.jezra.net/projects/vattery) || [vattery](https://aur.archlinux.org/packages/vattery/)

## Power management with systemd

### ACPI events

*systemd* handles some power-related [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") events, whose actions can be configured in `/etc/systemd/logind.conf` or `/etc/systemd/logind.conf.d/*.conf` — see [logind.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5). On systems with no dedicated power manager, this may replace the [acpid](/index.php/Acpid "Acpid") daemon which is usually used to react to these ACPI events.

The specified action for each event can be one of `ignore`, `poweroff`, `reboot`, `halt`, `suspend`, `hibernate`, `hybrid-sleep`, `suspend-then-hibernate`, `lock` or `kexec`. In case of hibernation and suspension, they must be properly [set up](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate"). If an event is not configured, *systemd* will use a default action.

| Event handler | Description | Default action |
| `HandlePowerKey` | Triggered when the power key/button is pressed. | `poweroff` |
| `HandleSuspendKey` | Triggered when the suspend key/button is pressed. | `suspend` |
| `HandleHibernateKey` | Triggered when the hibernate key/button is pressed. | `hibernate` |
| `HandleLidSwitch` | Triggered when the lid is closed, except in the cases below. | `suspend` |
| `HandleLidSwitchDocked` | Triggered when the lid is closed if the system is inserted in a docking station, or more than one display is connected. | `ignore` |
| `HandleLidSwitchExternalPower` | Triggered when the lid is closed if the system is connected to external power. | action set for `HandleLidSwitch` |

To apply any changes, [restart](/index.php/Restart "Restart") `systemd-logind.service` (be warned that this will terminate all login sessions that might still be open).

**Note:** *systemd* cannot handle AC and Battery ACPI events, so if you use [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") or other similar tools [acpid](/index.php/Acpid "Acpid") is still required.

#### Power managers

Some [desktop environments](/index.php/Desktop_environment "Desktop environment") include power managers which [inhibit](http://www.freedesktop.org/wiki/Software/systemd/inhibit/) (temporarily turn off) some or all of the *systemd* ACPI settings. If such a power manager is running, then the actions for ACPI events can be configured in the power manager alone. Changes to `/etc/systemd/logind.conf` or `/etc/systemd/logind.conf.d/*.conf` need be made only if you wish to configure behaviour for a particular event that is not inhibited by the power manager.

Note that if the power manager does not inhibit *systemd* for the appropriate events you can end up with a situation where *systemd* suspends your system and then when the system is woken up the other power manager suspends it again. As of December 2016, the power managers of [KDE](/index.php/KDE "KDE"), [GNOME](/index.php/GNOME "GNOME"), [Xfce](/index.php/Xfce "Xfce") and [MATE](/index.php/MATE "MATE") issue the necessary *inhibited* commands. If the *inhibited* commands are not being issued, such as when using [acpid](/index.php/Acpid "Acpid") or others to handle ACPI events, set the `Handle` options to `ignore`. See also [systemd-inhibit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-inhibit.1).

#### xss-lock

[xss-lock](https://www.archlinux.org/packages/?name=xss-lock) subscribes to the systemd-events `suspend`, `hibernate`, `lock-session`, and `unlock-session` with appropriate actions (run locker and wait for user to unlock or kill locker). *xss-lock* also reacts to [DPMS](/index.php/DPMS "DPMS") events and runs or kills the locker in response.

Start xss-lock in your [autostart](/index.php/Autostart "Autostart"), for example

```
xss-lock -- i3lock -n -i *background_image.png* &

```

### Suspend and hibernate

*systemd* provides commands to suspend to RAM or hibernate using the kernel's native suspend/resume functionality. There are also mechanisms to add hooks to customize pre- and post-suspend actions.

`systemctl suspend` should work out of the box, for `systemctl hibernate` to work on your system you need to follow the instructions at [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate").

There are also two modes combining suspend and hibernate:

*   `systemctl hybrid-sleep` suspends the system both to RAM and disk, so a complete power loss does not result in lost data. This mode is also called [suspend to both](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate").
*   `systemctl suspend-then-hibernate` initially suspends the system to RAM and if it is not interrupted within the delay specified by `HibernateDelaySec` in [systemd-sleep.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.conf.5), then the system will be woken using an RTC alarm and hibernated.

**Note:** *systemd* can also use other suspend backends (such as [Uswsusp](/index.php/Uswsusp "Uswsusp")), in addition to the default *kernel* backend, in order to put the computer to sleep or hibernate. See [Uswsusp#With systemd](/index.php/Uswsusp#With_systemd "Uswsusp") for an example.

#### Hybrid-sleep on suspend or hibernation request

It is possible to configure systemd to always do a *hybrid-sleep* even on a *suspend* or *hibernation* request.

The default *suspend* and *hibernation* action can be configured in the `/etc/systemd/sleep.conf` file. To set both actions to *hybrid-sleep*:

 `/etc/systemd/sleep.conf` 
```
[Sleep]
# suspend=hybrid-sleep
SuspendMode=suspend
SuspendState=disk
# hibernate=hybrid-sleep
HibernateMode=suspend
HibernateState=disk
```

See the [sleep.conf.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.conf.d.5) manual page for details and the [linux kernel documentation on power states](https://www.kernel.org/doc/html/latest/admin-guide/pm/sleep-states.html#basic-sysfs-interfaces-for-system-suspend-and-hibernation).

### Sleep hooks

#### Suspend/resume service files

Service files can be hooked into *suspend.target*, *hibernate.target*, *sleep.target*, *hybrid-sleep.target* and *suspend-then-hibernate.target* to execute actions before or after suspend/hibernate. Separate files should be created for user actions and root/system actions. [Enable](/index.php/Enable "Enable") the `suspend@*user*` and `resume@*user*` services to have them started at boot. Examples:

 `/etc/systemd/system/suspend@.service` 
```
[Unit]
Description=User suspend actions
Before=sleep.target

[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStartPre= -/usr/bin/pkill -u %u unison ; /usr/local/bin/music.sh stop
ExecStart=/usr/bin/sflock
ExecStartPost=/usr/bin/sleep 1

[Install]
WantedBy=sleep.target

```
 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStart=/usr/local/bin/ssh-connect.sh

[Install]
WantedBy=suspend.target

```

**Note:** As screen lockers may return before the screen is "locked", the screen may flash on resuming from suspend. Adding a small delay via `ExecStartPost=/usr/bin/sleep 1` helps prevent this.

For root/system actions ([enable](/index.php/Enable "Enable") the `root-resume` and `root-suspend` services to have them started at boot):

 `/etc/systemd/system/root-resume.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target

[Service]
Type=simple
ExecStart=/usr/bin/systemctl restart mnt-media.automount

[Install]
WantedBy=suspend.target

```
 `/etc/systemd/system/root-suspend.service` 
```
[Unit]
Description=Local system suspend actions
Before=sleep.target

[Service]
Type=simple
ExecStart=-/usr/bin/pkill sshfs

[Install]
WantedBy=sleep.target

```

A couple of handy hints about these service files (more in [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)):

*   If `Type=oneshot` then you can use multiple `ExecStart=` lines. Otherwise only one `ExecStart` line is allowed. You can add more commands with either `ExecStartPre` or by separating commands with a semicolon (see the first example above; note the spaces before and after the semicolon, as they are *required*).
*   A command prefixed with `-` will cause a non-zero exit status to be ignored and treated as a successful command.
*   The best place to find errors when troubleshooting these service files is of course with [journalctl](/index.php/Journalctl "Journalctl").

#### Combined Suspend/resume service file

With the combined suspend/resume service file, a single hook does all the work for different phases (sleep/resume) and for different targets (suspend/hibernate/hybrid-sleep).

Example and explanation:

 `/etc/systemd/system/wicd-sleep.service` 
```
[Unit]
Description=Wicd sleep hook
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=-/usr/share/wicd/daemon/suspend.py
ExecStop=-/usr/share/wicd/daemon/autoconnect.py

[Install]
WantedBy=sleep.target

```

*   `RemainAfterExit=yes`: After started, the service is considered active until it is explicitly stopped.
*   `StopWhenUnneeded=yes`: When active, the service will be stopped if no other active service requires it. In this specific example, it will be stopped after *sleep.target* is stopped.
*   Because *sleep.target* is pulled in by *suspend.target*, *hibernate.target* and *hybrid-sleep.target* and because *sleep.target* itself is a *StopWhenUnneeded* service, the hook is guaranteed to start/stop properly for different tasks.

#### Hooks in /usr/lib/systemd/system-sleep

*systemd* runs all executables in `/usr/lib/systemd/system-sleep/`, passing two arguments to each of them:

*   Argument 1: either `pre` or `post`, depending on whether the machine is going to sleep or waking up
*   Argument 2: `suspend`, `hibernate` or `hybrid-sleep`, depending on which is being invoked

*systemd* will run these scripts concurrently and not one after another.

The output of any custom script will be logged by *systemd-suspend.service*, *systemd-hibernate.service* or *systemd-hybrid-sleep.service*. You can see its output in *systemd*'s [journal](/index.php/Systemd#Journal "Systemd"):

```
# journalctl -b -u systemd-suspend.service

```

**Note:** You can also use *sleep.target*, *suspend.target*, *hibernate.target* or *hybrid-sleep.target* to hook units into the sleep state logic instead of using custom scripts.

An example of a custom sleep script:

 `/usr/lib/systemd/system-sleep/example.sh` 
```
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "Going to $2..."
    ;;
  post/*)
    echo "Waking up from $2..."
    ;;
esac

```

Do not forget to make your script executable:

```
# chmod a+x /usr/lib/systemd/system-sleep/example.sh

```

See [systemd.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7) and [systemd-sleep(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8) for more details.

### Troubleshooting

#### Delayed lid switch action

When performing lid switches in short succession, *logind* will delay the suspend action for up to 90s to detect possible docks. [[1]](http://lists.freedesktop.org/archives/systemd-devel/2015-January/027131.html) This delay was made configurable with systemd v220:[[2]](https://github.com/systemd/systemd/commit/9d10cbee89ca7f82d29b9cb27bef11e23e3803ba)

 `/etc/systemd/logind.conf` 
```
...
HoldoffTimeoutSec=30s
...
</nowiki>
```

#### Suspend from corresponding laptop Fn key not working

If, regardless of the setting in logind.conf, the sleep button does not work (pressing it does not even produce a message in syslog), then logind is probably not watching the keyboard device. [[3]](http://lists.freedesktop.org/archives/systemd-devel/2015-February/028325.html) Do:

```
# journalctl --grep="Watching system buttons"

```

You might see something like this:

```
May 25 21:28:19 vmarch.lan systemd-logind[210]: Watching system buttons on /dev/input/event2 (Power Button)
May 25 21:28:19 vmarch.lan systemd-logind[210]: Watching system buttons on /dev/input/event3 (Sleep Button)
May 25 21:28:19 vmarch.lan systemd-logind[210]: Watching system buttons on /dev/input/event4 (Video Bus)

```

Notice no keyboard device. Now obtain ATTRS{name} for the parent keyboard device [[4]](http://systemd-devel.freedesktop.narkive.com/Rbi3rjNN/patch-1-2-logind-add-support-for-tps65217-power-button) :

 `# udevadm info -a /dev/input/by-path/*-kbd` 
```
...
KERNEL=="event0"
...
ATTRS{name}=="AT Translated Set 2 keyboard"
```

Now write a custom udev rule to add the "power-switch" tag:

 `/etc/udev/rules.d/70-power-switch-my.rules` 
```
ACTION=="remove", GOTO="power_switch_my_end"
SUBSYSTEM=="input", KERNEL=="event*", ATTRS{name}=="AT Translated Set 2 keyboard", TAG+="power-switch"
LABEL="power_switch_my_end"

```

Restart services and reload rules:

```
# systemctl restart systemd-udevd.service
# udevadm trigger
# systemctl restart systemd-logind.service

```

Now you should see `Watching system buttons on /dev/input/event0` in syslog.

## Power saving

**Note:** See [Laptop#Power management](/index.php/Laptop#Power_management "Laptop") for power management specific to laptops, such as battery monitoring.

This section is a reference for creating custom scripts and power saving settings such as by udev rules. Make sure that the settings are not managed by some [other utility](#Userspace_tools) to avoid conflicts.

Almost all of the features listed here are worth using whether or not the computer is on AC or battery power. Most have negligible performance impact and are just not enabled by default because of commonly broken hardware/drivers. Reducing power usage means reducing heat, which can even lead to higher performance on a modern Intel or AMD CPU, thanks to [dynamic overclocking](https://en.wikipedia.org/wiki/Intel_Turbo_Boost "wikipedia:Intel Turbo Boost").

### Processors with HWP (Hardware P-state) support

The available energy preferences of a HWP supported processor are `default performance balance_performance balance_power power`.

This can be validated by `$ cat /sys/devices/system/cpu/cpufreq/policy?/energy_performance_available_preferences`

To conserve more energy, you can config by creating the following file:

 `/etc/tmpfiles.d/energy_performance_preference.conf` 
```
w /sys/devices/system/cpu/cpufreq/policy?/energy_performance_preference - - - - balance_power

```

See the [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) and [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) man pages for details.

### Audio

By default, audio power saving is turned off by most drivers. It can be enabled by setting the `power_save` parameter; a time (in seconds) to go into idle mode. To idle the audio card after one second, create the following file for Intel soundcards.

 `/etc/modprobe.d/audio_powersave.conf`  `options snd_hda_intel power_save=1` 

Alternatively, use the following for ac97:

```
options snd_ac97_codec power_save=1

```

**Note:**

*   To retrieve the manufacturer and the corresponding kernel driver which is used for your sound card, run `lspci -k`.
*   Toggling the audio card's power state can cause a popping sound or noticeable latency on some broken hardware.

It is also possible to further reduce the audio power requirements by disabling the HDMI audio output, which can done by [blacklisting](/index.php/Blacklisting "Blacklisting") the appropriate kernel modules (e.g. `snd_hda_codec_hdmi` in case of Intel hardware).

### Backlight

See [Backlight](/index.php/Backlight "Backlight").

### Bluetooth

To disable bluetooth completely, [blacklist](/index.php/Blacklist "Blacklist") the `btusb` and `bluetooth` modules.

To turn off bluetooth only temporarily, use *rfkill*:

```
# rfkill block bluetooth

```

Or with udev rule:

 `/etc/udev/rules.d/50-bluetooth.rules` 
```
# disable bluetooth
SUBSYSTEM=="rfkill", ATTR{type}=="bluetooth", ATTR{state}="0"

```

### Web camera

If you will not use integrated web camera then [blacklist](/index.php/Blacklist "Blacklist") the `uvcvideo` module.

### Kernel parameters

This section uses configs in `/etc/sysctl.d/`, which is *"a drop-in directory for kernel sysctl parameters."* See [The New Configuration Files](http://0pointer.de/blog/projects/the-new-configuration-files) and more specifically [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5) for more information.

#### Disabling NMI watchdog

The [NMI](https://en.wikipedia.org/wiki/Non-maskable_interrupt "wikipedia:Non-maskable interrupt") watchdog is a debugging feature to catch hardware hangs that cause a kernel panic. On some systems it can generate a lot of interrupts, causing a noticeable increase in power usage:

 `/etc/sysctl.d/disable_watchdog.conf`  `kernel.nmi_watchdog = 0` 

or add `nmi_watchdog=0` to the [kernel line](/index.php/Kernel_line "Kernel line") to disable it completely from early boot.

#### Writeback Time

Increasing the virtual memory dirty writeback time helps to aggregate disk I/O together, thus reducing spanned disk writes, and increasing power saving. To set the value to 60 seconds (default is 5 seconds):

 `/etc/sysctl.d/dirty.conf`  `vm.dirty_writeback_centisecs = 6000` 

To do the same for journal commits on supported filesystems (e.g. ext4, btrfs...), use `commit=60` as a option in [fstab](/index.php/Fstab "Fstab").

Note that this value is modified as a side effect of the Laptop Mode setting below. See also [sysctl#Virtual memory](/index.php/Sysctl#Virtual_memory "Sysctl") for other parameters affecting I/O performance and power saving.

#### Laptop Mode

See the [kernel documentation](https://www.kernel.org/doc/Documentation/laptops/laptop-mode.txt) on the laptop mode 'knob.' *"A sensible value for the knob is 5 seconds."*

 `/etc/sysctl.d/laptop.conf`  `vm.laptop_mode = 5` 
**Note:** This setting is mainly relevant to spinning-disk drives.

### Network interfaces

[Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") can be a useful feature, but if you are not making use of it then it is simply draining extra power waiting for a magic packet while in suspend. You can adapt a [udev rule](/index.php/Wake-on-LAN#udev "Wake-on-LAN") to disable the feature for all Ethernet interfaces.

To enable powersaving with [iw](https://www.archlinux.org/packages/?name=iw) on all wireless interfaces:

 `/etc/udev/rules.d/70-wifi-powersave.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wlan*", RUN+="/usr/bin/iw dev %k set power_save on"` 

In this example, `%k` is a specifier for the kernel name of the matched device. For example, if it finds that the rule is applicable to `wlan0`, the `%k` specifier will be replaced with `wlan0`. To apply the rules to only a particular interface, just replace the pattern `wlan*` and specifier `%k` with the desired interface name. For more information, see [Writing udev rules](http://www.reactivated.net/writing_udev_rules.html).

**Note:** In this case, the name of the configuration file is important. Due to the introduction of [persistent device names](/index.php/Network_configuration#Change_interface_name "Network configuration") via `80-net-setup-link.rules` in systemd, it is important that the network powersave rules are named lexicographically before `80-net-setup-link.rules` so that they are applied before the devices are named e.g. `enp2s0`. However, be advised that commands ran with `RUN` are executed **after** all rules have been processed -- in which case the naming of the rules file is irrelevant and the persistent device names should be used (the persistent device name can be referenced by replacing `%k` with `$name`).

#### Intel wireless cards (iwlwifi)

Additional power saving functions of Intel wireless cards with `iwlwifi` driver can be enabled by passing the correct parameters to the kernel module. Making it persistent can be achieved by adding the line below to `/etc/modprobe.d/iwlwifi.conf` file:

```
options iwlwifi power_save=1 d0i3_disable=0 uapsd_disable=0
options iwldvm force_cam=0

```

Keep in mind that these power saving options are experimental and can cause an unstable system.

### Bus power management

#### Active State Power Management

If the computer is believed not to support [ASPM](https://en.wikipedia.org/wiki/Active_State_Power_Management "wikipedia:Active State Power Management") it will be disabled on boot:

```
# lspci -vv | grep 'ASPM.*abled;'

```

ASPM is handled by the BIOS, if ASPM is disabled it will be because [ref](http://wireless.kernel.org/en/users/Documentation/ASPM):

1.  The BIOS disabled it for some reason (for conflicts?).
2.  PCIE requires ASPM but L0s are optional (so L0s might be disabled and only L1 enabled).
3.  The BIOS might not have been programmed for it.
4.  The BIOS is buggy.

If believing the computer has support for ASPM it can be forced on for the kernel to handle with the `pcie_aspm=force` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

**Warning:**

*   Forcing on ASPM can cause a freeze/panic, so make sure you have a way to undo the option if it does not work.
*   On systems that do not support it forcing on ASPM can even increase power consumption.
*   This forces ASPM in kernel while it can still remain disabled in hardware and not work. To check whether this is the case the `dmesg | grep ASPM` command can be used and if that is the case, hardware-specific Wiki article should be consulted.

To adjust to `powersave` do (the following command will not work unless enabled):

```
# echo powersave > /sys/module/pcie_aspm/parameters/policy

```

By default it looks like this:

 `$ cat /sys/module/pcie_aspm/parameters/policy` 
```
[default] performance powersave

```

#### PCI Runtime Power Management

 `/etc/udev/rules.d/pci_pm.rules`  `SUBSYSTEM=="pci", ATTR{power/control}="auto"` 

The rule above powers all unused devices down, but some devices will not wake up again. To allow runtime power management only for devices that are known to work, use simple matching against vendor and device IDs (use `lspci -nn` to get these values):

 `/etc/udev/rules.d/pci_pm.rules` 
```
# whitelist for pci autosuspend
SUBSYSTEM=="pci", ATTR{vendor}=="0x1234", ATTR{device}=="0x1234", ATTR{power/control}="auto"

```

Alternatively, to blacklist devices that are not working with PCI runtime power management and enable it for all other devices:

 `/etc/udev/rules.d/pci_pm.rules` 
```
# blacklist for pci runtime power management
SUBSYSTEM=="pci", ATTR{vendor}=="0x1234", ATTR{device}=="0x1234", ATTR{power/control}:="on"

SUBSYSTEM=="pci", ATTR{power/control}="auto"

```

#### USB autosuspend

The Linux kernel can automatically suspend USB devices when they are not in use. This can sometimes save quite a bit of power, however some USB devices are not compatible with USB power saving and start to misbehave (common for USB mice/keyboards). [udev](/index.php/Udev "Udev") rules based on whitelist or blacklist filtering can help to mitigate the problem.

The most simple and likely useless example is enabling autosuspend for all USB devices:

 `/etc/udev/rules.d/50-usb_power_save.rules` 
```
ACTION=="add", SUBSYSTEM=="usb", TEST=="power/control", ATTR{power/control}="auto"

```

To allow autosuspend only for devices that are known to work, use simple matching against vendor and product IDs (use *lsusb* to get these values):

 `/etc/udev/rules.d/50-usb_power_save.rules` 
```
# whitelist for usb autosuspend
ACTION=="add", SUBSYSTEM=="usb", TEST=="power/control", ATTR{idVendor}=="05c6", ATTR{idProduct}=="9205", ATTR{power/control}="auto"

```

Alternatively, to blacklist devices that are not working with USB autosuspend and enable it for all other devices:

 `/etc/udev/rules.d/50-usb_power_save.rules` 
```
# blacklist for usb autosuspend
ACTION=="add", SUBSYSTEM=="usb", ATTR{idVendor}=="05c6", ATTR{idProduct}=="9205", GOTO="power_usb_rules_end"

ACTION=="add", SUBSYSTEM=="usb", TEST=="power/control", ATTR{power/control}="auto"
LABEL="power_usb_rules_end"

```

The default autosuspend idle delay time is controlled by the `autosuspend` parameter of the `usbcore` [kernel module](/index.php/Kernel_module "Kernel module"). To set the delay to 5 seconds instead of the default 2 seconds:

 `/etc/modprobe.d/usb-autosuspend.conf` 
```
options usbcore autosuspend=5

```

Similarly to `power/control`, the delay time can be fine-tuned per device by setting the `power/autosuspend` attribute.

See the [Linux kernel documentation](https://www.kernel.org/doc/Documentation/usb/power-management.txt) for more information on USB power management.

#### SATA Active Link Power Management

**Warning:** SATA Active Link Power Management can lead to data loss on some devices. Do not enable this setting unless you have frequent backups.

Since Linux 4.15 there is a [new setting](https://hansdegoede.livejournal.com/18412.html) called `med_power_with_dipm` that matches the behaviour of Windows IRST driver settings and should not cause data loss with recent SSD/HDD drives. The power saving can be significant, ranging [from 1.0 to 1.5 Watts (when idle)](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=ebb82e3c79d2a956366d0848304a53648bd6350b). It will become a default setting for Intel based laptops in Linux 4.16 [[5]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=ebb82e3c79d2a956366d0848304a53648bd6350b).

The current setting can be read from `/sys/class/scsi_host/host*/link_power_management_policy` as follows:

```
# cat /sys/class/scsi_host/host*/link_power_management_policy

```

<caption>Available ALPM settings</caption>
| Setting | Description | Power saving |
| max_performance | current default | None |
| medium_power | - | ~1.0 Watts |
| med_power_with_dipm | recommended setting | ~1.5 Watts |
| min_power | **WARNING: possible data loss** | ~1.5 Watts |

 `/etc/udev/rules.d/hd_power_save.rules`  `ACTION=="add", SUBSYSTEM=="scsi_host", KERNEL=="host*", ATTR{link_power_management_policy}="med_power_with_dipm"` 
**Note:** This adds latency when accessing a drive that has been idle, so it is one of the few settings that may be worth toggling based on whether you are on AC power.

### Hard disk drive

See [hdparm#Power management configuration](/index.php/Hdparm#Power_management_configuration "Hdparm") for drive parameters that can be set.

Power saving is not effective when too many programs are frequently writing to the disk. Tracking all programs, and how and when they write to disk is the way to limit disk usage. Use [iotop](https://www.archlinux.org/packages/?name=iotop) to see which programs use the disk frequently. See [Improving performance#Storage devices](/index.php/Improving_performance#Storage_devices "Improving performance") for other tips.

Also little things like setting the [noatime](/index.php/Fstab#atime_options "Fstab") option can help. If enough RAM is available, consider disabling or limiting [swappiness](/index.php/Swappiness "Swappiness") as it has the possibility to limit a good number of disk writes.

### CD-ROM or DVD drive

See [Udisks#Devices do not remain unmounted (udisks)](/index.php/Udisks#Devices_do_not_remain_unmounted_.28udisks.29 "Udisks").

## Tools and scripts

### Using a script and an udev rule

Since systemd users can suspend and hibernate through `systemctl suspend` or `systemctl hibernate` and handle acpi events with `/etc/systemd/logind.conf`, it might be interesting to remove *pm-utils* and [acpid](/index.php/Acpid "Acpid"). There is just one thing systemd cannot do (as of systemd-204): power management depending on whether the system is running on AC or battery. To fill this gap, you can create a single [udev](/index.php/Udev "Udev") rule that runs a script when the AC adapter is plugged and unplugged:

 `/etc/udev/rules.d/powersave.rules` 
```
SUBSYSTEM=="power_supply", ATTR{online}=="0", RUN+="/path/to/your/script true"
SUBSYSTEM=="power_supply", ATTR{online}=="1", RUN+="/path/to/your/script false"

```

**Note:** You can use the same script that *pm-powersave* uses. You just have to make it executable and place it somewhere else (for example `/usr/local/bin/`).

Examples of powersave scripts:

*   [ftw](https://github.com/supplantr/ftw), package: [ftw-git](https://aur.archlinux.org/packages/ftw-git/)
*   [powersave](https://github.com/Unia/powersave)
*   [throttle](https://github.com/quequotion/pantheon-bzr-qq/blob/master/EXTRAS/indicator-powersave/throttle), from [indicator-powersave](https://aur.archlinux.org/packages/indicator-powersave/)

The above udev rule should work as expected, but if your power settings are not updated after a suspend or hibernate cycle, you should add a script in `/usr/lib/systemd/system-sleep/` with the following contents:

 `/usr/lib/systemd/system-sleep/00powersave` 
```
#!/bin/sh

case $1 in
    pre) /path/to/your/script false ;;
    post)       
	if cat /sys/class/power_supply/AC0/online | grep 0 > /dev/null 2>&1
	then
    		/path/to/your/script true	
	else
    		/path/to/your/script false
	fi
    ;;
esac
exit 0

```

Do not forget to make it executable!

**Note:** Be aware that AC0 may be different for your laptop, change it if that is the case.

### Print power settings

This script prints power settings and a variety of other properties for USB and PCI devices. Note that root permissions are needed to see all settings.

```
#!/bin/bash

for i in $(find /sys/devices -name "bMaxPower")
do
	busdir=${i%/*}
	busnum=$(<$busdir/busnum)
	devnum=$(<$busdir/devnum)
	title=$(lsusb -s $busnum:$devnum)

	printf "

+++ %s
  -%s
" "$title" "$busdir"

	for ff in $(find $busdir/power -type f ! -empty 2>/dev/null)
	do
		v=$(cat $ff 2>/dev/null|tr -d "
")
		[[ ${#v} -gt 0 ]] && echo -e " ${ff##*/}=$v";
		v=;
	done | sort -g;
done;

printf "

+++ %s
" "Kernel Modules"
for mod in $(lspci -k | sed -n '/in use:/s,^.*: ,,p' | sort -u)
do
	echo "+ $mod";
	systool -v -m $mod 2> /dev/null | sed -n "/Parameters:/,/^$/p";
done

```

## See also

*   [ThinkWiki:How to reduce power consumption](http://www.thinkwiki.org/wiki/How_to_reduce_power_consumption)
*   [How to get longer battery life on Linux](http://ivanvojtko.blogspot.sk/2016/04/how-to-get-longer-battery-life-on-linux.html)