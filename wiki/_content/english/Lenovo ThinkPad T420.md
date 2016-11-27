This article covers the installation and configuration of Arch Linux on a Lenovo T420 laptop.

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware](#Hardware)
    *   [2.1 Fingerprint reader](#Fingerprint_reader)
    *   [2.2 Some Media keys](#Some_Media_keys)
    *   [2.3 Untested](#Untested)
*   [3 Laptop Settings](#Laptop_Settings)
    *   [3.1 ACPI](#ACPI)
    *   [3.2 Tp_smapi](#Tp_smapi)
    *   [3.3 CPU frequency scaling](#CPU_frequency_scaling)
    *   [3.4 Fans](#Fans)
    *   [3.5 Laptop Mode Tools](#Laptop_Mode_Tools)
    *   [3.6 NVIDIA Optimus](#NVIDIA_Optimus)
    *   [3.7 Optional kernel boot arguments](#Optional_kernel_boot_arguments)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Media Keys](#Media_Keys)
    *   [4.2 Rebind Forward and Back keys](#Rebind_Forward_and_Back_keys)
    *   [4.3 Turn touchpad on and off](#Turn_touchpad_on_and_off)
    *   [4.4 Volume up/down not changing volume](#Volume_up.2Fdown_not_changing_volume)
    *   [4.5 Shutdown on battery](#Shutdown_on_battery)
    *   [4.6 Hang on reboot](#Hang_on_reboot)
*   [5 See also](#See_also)

## Installation

This laptop supports [UEFI](/index.php/UEFI "UEFI") as well as the traditional BIOS.

There are no issues with installing Arch Linux with the latest [Archiso](https://www.archlinux.org/download/).

The rest of the installation process can be followed with the [Installation guide](/index.php/Installation_guide "Installation guide").

## Hardware

All hardware works out of the box except the following:

### Fingerprint reader

Fingerprint reader works great with fprint and PAM (installation of fingerprint-gui recommended).

See [Fprint#Setup fingerprint-gui](/index.php/Fprint#Setup_fingerprint-gui "Fprint") for more information.

### Some Media keys

*   See [Media Keys](#Media_Keys)

### Untested

*   Firewire

## Laptop Settings

### ACPI

[ACPI](/index.php/ACPI_modules "ACPI modules") is well supported here. No obvious troubleshoots.

### Tp_smapi

Unfortunately, [tp_smapi](/index.php/Tp_smapi "Tp smapi") is only partially supported on the Thinkpad T420\. A number of features work since version 0.41\. For example, the hard drive protection mechanism [HDAPS](/index.php/HDAPS "HDAPS") now works well. See the linked wiki entry.

Some features like setting the starting threshold for charging the battery do not yet work. To control the battery charging thresholds, install the Perl script [tpacpi-bat](https://aur.archlinux.org/packages/tpacpi-bat/) from the [AUR](/index.php/AUR "AUR").

Insert the `acpi_call` kernel module by running

```
modprobe acpi_call

```

Manually set the thresholds by calling

```
/usr/bin/perl /usr/bin/tpacpi-bat -v -s SP 0 80 
/usr/bin/perl /usr/bin/tpacpi-bat -v -s ST 0 40

```

The example values 40 and 80 given here represent the percentage of full battery capacity remaining. Adjust them to your own needs. You may also want to write a simple `set-battery.service` and enable it to set them at startup. While these values should be permanent, they will be reset any time the battery is removed.

```
[Unit]
Description=Set battery capacity

[Service]
Type=oneshot
ExecStart=/usr/bin/perl /usr/bin/tpacpi-bat -v -s SP 0 80
ExecStart=/usr/bin/perl /usr/bin/tpacpi-bat -v -s ST 0 40

[Install]
WantedBy=multi-user.target

```

Also, if you are dual booting with Windows, you can still control the battery charging thresholds with Lenovo's Power Manager which communicates directly to the battery controller.

When using systemd, you may want to blacklist the tp_smapi module if your systemd-modules-load.service fails, as new ThinkPads handle everything over acpi.

### CPU frequency scaling

[CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") is fully supported with all of the available processor models with this laptop.

### Fans

Install the package [thinkfan](https://aur.archlinux.org/packages/thinkfan/). It will automatically create the necessary acpi configuration file in `/usr/lib/modprobe.d/thinkpad_acpi.conf`.

Copy the example sensor settings file from "/usr/share/doc/thinkfan/examples/thinkfan.conf.simple" to "/etc/thinkfan.conf".

 `# cp /usr/share/doc/thinkfan/examples/thinkfan.conf.simple /etc/thinkfan.conf` 

Aftwards replace the default `hwmon` in the settings file `/etc/thinkfan.conf` with the following:

 `/etc/thinkfan.conf`  `hwmon /sys/devices/virtual/thermal/thermal_zone0/temp` 

Alternatively, sensors can be generated using following command. Add `hwmon` before the sensor lines.

 `find /sys/devices -type f -name "temp*_input"` 

In the same configuration file replace the default fan level settings with your needs (the last lines of the file). Useful values are

```
(0,	0,	42)
(1,	40,	47)
(2,	45,	52)
(3,	50,	57)
(4,	55,	62)
(5,	60,	67)
(6,	65,	72)
(7,	70,	77)
(127,	75,	32767)
```

Finally [enable](/index.php/Enable "Enable") the **thinkfan** service.

 `# systemctl enable thinkfan` 

### Laptop Mode Tools

No significant issues were found using [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools").

Possible bug with [#Shutdown on battery](#Shutdown_on_battery).

The package [tlp](https://www.archlinux.org/packages/?name=tlp) is an alternative tool that can replace [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/).

### NVIDIA Optimus

[Bumblebee](/index.php/Bumblebee "Bumblebee") works as intended on models with NVIDIA Optimus

### Optional kernel boot arguments

Using the following kernel boot parameters [reduces battery drain](http://www.phoronix.com/scan.php?page=article&item=intel_i915_power&num=1%7C):

```
i915.i915_enable_rc6=1
i915.i915_enable_fbc=1
i915.lvds_downclock=1 
i915.semaphores=1

```

## Troubleshooting

### Media Keys

Media keys that (should) work out of the box:

*   Wireless On/Off
*   Backlight Brightness settings
*   Thinklight
*   Mute
*   Microphone mute

Media Keys that Do Not work out of the box:

*   [Volume keys](#Volume_up.2Fdown_not_changing_volume) (Works out-of-the-box in [GNOME](/index.php/GNOME "GNOME"))

You must find a workaround and bind the keys yourself for the rest of them.

[xbindkeys](/index.php/Xbindkeys "Xbindkeys") and [xbindkeys_config-gtk2](https://aur.archlinux.org/packages/xbindkeys_config-gtk2/) can be a solution for media keys that are not working. This solution also allows you to rebind the ThinkVantage button and certain FN layer shortcuts (the blue logos on the keyboard).

### Rebind Forward and Back keys

Keys forward and back (next to cursor keys) can be easily remapped to PageDown/PageUp.

[Install](/index.php/Install "Install") xmodmap with the package [xorg-server-utils](https://www.archlinux.org/packages/?name=xorg-server-utils)

Create a `~/.Xmodmap` file with content:

```
keysym XF86Back = Page_Up
keysym XF86Forward = Page_Down

```

Add this line to your `~/.xinitrc` to make it work:

```
xmodmap ~/.Xmodmap

```

You can also re-map AudioPrev (`Fn+Left`) and AudioNext (`Fn+Right`) to Home/End:

```
keysym XF86AudioNext = End
keysym XF86AudioPrev = Home

```

**Note:**

*   You have to log out for the changes to take effect.
*   The keys should work out of the box, at least on [KDE](/index.php/KDE "KDE").

### Turn touchpad on and off

For some, the (`Fn+F8`) key does not switch the touchpad on and off. See [Touchpad Synaptics#Software toggle](/index.php/Touchpad_Synaptics#Software_toggle "Touchpad Synaptics") for a workaround.

### Volume up/down not changing volume

See [Xbindkeys](/index.php/Xbindkeys "Xbindkeys").

### Shutdown on battery

Some users have reported that the T420 was rebooting on shutdown on battery power. There have been quite a few attempts to fix this. Three are detailed here.

One way is to disable the module `ehci_hcd`. See [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules") for more information.

Or try disable Laptop-mode. Add `!laptop-mode` to the `DAEMONS` array in `/etc/rc.conf`:

```
DAEMONS=(...!laptop-mode...)

```

[This forum post](https://bbs.archlinux.org/viewtopic.php?pid=1106437#p1106437) details another way to have your computer not reboot on shutdown. Turning off the `laptop-mode` daemon causes battery life to suffer, so when on the move and in need of a simple way to shutdown, this seems to work better.

### Hang on reboot

This is a problem on many laptops and can be fixed by [blacklisting](/index.php/Blacklisting "Blacklisting") the `e1000e` kernel module.

## See also

*   [Lenovo ThinkPad T420s](/index.php/Lenovo_ThinkPad_T420s "Lenovo ThinkPad T420s")
*   [Arch Linux on ThinkPad T420i](http://sysphere.org/~anrxc/j/articles/thinkpad-t420/index.html)