# Lenovo ThinkPad X200

The Lenovo ThinkPad X200 is a high-quality laptop featuring a 12.1" widescreen WXGA display, an Intel Core 2 Duo processor (2.26 - 2.66GHz), an Intel Graphics Media Accelerator 4500MHD and up to 8GB of RAM whilst still maintaining impressive battery life.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Wireless](#Wireless)
    *   [1.2 TrackPoint](#TrackPoint)
    *   [1.3 Fingerprint Reader](#Fingerprint_Reader)
    *   [1.4 Disable bluetooth at boot](#Disable_bluetooth_at_boot)
    *   [1.5 Hard Disk shock protection](#Hard_Disk_shock_protection)
    *   [1.6 Mute button](#Mute_button)
    *   [1.7 Screen calibration](#Screen_calibration)
    *   [1.8 Loading the correct ICC colour profile](#Loading_the_correct_ICC_colour_profile)
    *   [1.9 Screen rotation](#Screen_rotation)
    *   [1.10 Screen auto-rotation](#Screen_auto-rotation)
    *   [1.11 Power consumption and fan control](#Power_consumption_and_fan_control)
    *   [1.12 Suspend to RAM / hibernate](#Suspend_to_RAM_.2F_hibernate)
    *   [1.13 BIOS WiFi-Whitelist Removal](#BIOS_WiFi-Whitelist_Removal)
    *   [1.14 Coreboot / Libreboot](#Coreboot_.2F_Libreboot)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 failed to execute '/usr/sbin/inputattach'](#failed_to_execute_.27.2Fusr.2Fsbin.2Finputattach.27)
    *   [2.2 System feels unresponsive](#System_feels_unresponsive)
    *   [2.3 Backlight fails to activate after system resume](#Backlight_fails_to_activate_after_system_resume)
    *   [2.4 PM device: Resume from hibernation error: Failed to restore -19](#PM_device:_Resume_from_hibernation_error:_Failed_to_restore_-19)
    *   [2.5 mei_me 0000:00:03.0: suspend](#mei_me_0000:00:03.0:_suspend)
    *   [2.6 pciehp 0000:00:1c.1:pcie04: Cannot add device at 0000:03:00](#pciehp_0000:00:1c.1:pcie04:_Cannot_add_device_at_0000:03:00)
    *   [2.7 Uhhuh. NMI received for unknown reason 30.](#Uhhuh._NMI_received_for_unknown_reason_30.)
    *   [2.8 High pitched noises](#High_pitched_noises)
*   [3 See also](#See_also)

## Configuration

### Wireless

The ThinkPad X200 has a Intel PRO/Wireless 5100/5300 AGN wireless adapter, supported by [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

If connectivity problems such as a slow connection or aborts are experienced, especially when connected to a [WPA2 Enterprise](/index.php/WPA2_Enterprise "WPA2 Enterprise") network, then try to load the iwlwifi module with the options `11n_disable=1`, `11n_disable=2`, `swcrypto=1`, `bt_coex_active=0`. There is no clear recommendation which of these options to be used as for some users `11n_disable=1` already solves the problem sufficiently, for others `bt_coex_active=0`. See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") for more detailed instructions.

### TrackPoint

See [TrackPoint](/index.php/TrackPoint "TrackPoint").

### Fingerprint Reader

The fingerprint reader that is found in the X200/X200T is not supported.

See [fprint](/index.php/Fprint "Fprint") for more information.

### Disable bluetooth at boot

See [Power saving#Bluetooth](/index.php/Power_saving#Bluetooth "Power saving").

### Hard Disk shock protection

The ThinkPad X200 comes with an integrated 2-axis accelerometer providing the possibility of parking the hard drive's disk heads preventing from data loss due to heavy shocks. See [HDAPS](/index.php/HDAPS "HDAPS") for details. It may be necessary to set correct [invert parameter](/index.php/HDAPS#Invert_module_parameter "HDAPS").

### Mute button

If the mute button on the keyboard is not working, then be sure to add acpi_osi="Linux" to the boot parameter in /etc/default/grub.

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi=Linux"

```

### Screen calibration

If the stylus happens to be working very imprecisely, the screen may be in need of calibration. Installing [xinput_calibrator](https://aur.archlinux.org/packages/xinput_calibrator/)<sup><small>AUR</small></sup> and running the following command will begin the calibration process.

```
# xinput_calibrator --device "Serial Wacom Tablet WACf004 stylus"

```

To save the calibration settings, create a config file at `/etc/X11/xorg.conf.d/99-calibration.conf` with the settings provided by xinput_calibrator.

### Loading the correct ICC colour profile

Download [x200.icc](https://github.com/yuvadm/dotfiles/raw/x200s/.color/icc/x200.icc) and move it to `~/.color/icc`. Load the profile with [xcalib](https://aur.archlinux.org/packages/xcalib/)<sup><small>AUR</small></sup> as follows:

```
$ /usr/bin/xcalib -d :0 ~/.color/icc/x200.icc

```

### Screen rotation

**Note:** Commands like [xmodmap](/index.php/Xmodmap "Xmodmap"), xev, showkey, dmesg, setkeycodes can help you. See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") for details.

The screen rotation hardware button does not work by default. To enable it, the button must first be assigned to a freekey code. To find a free keycode for use, try using the command `xmodmap -pke | less`.

Keycodes can be mapped to hardware buttons during the boot process via a [systemd](/index.php/Systemd "Systemd") config file such as the one shown below.

 `/etc/systemd/system/setkeycodes.service` 

```
[Unit]
Description=Assign each hardware button to a free keycode on boot

[Service]
Type=oneshot
ExecStart=/usr/bin/setkeycodes 0x67 184 0x6c 185 0x68 186 0x66 187

[Install]
WantedBy=multi-user.target
```

After successfully mapping a keycode to a hardware button, it can then be utilized with a script similar to the one below.

 `/usr/local/bin/screen_rotation.sh` 

```
#!/bin/sh

# Find the line in "xrandr -q --verbose" output that contains current screen orientation and "strip" out current orientation.
rotation="$(xrandr -q --verbose | grep 'connected' | egrep -o  '\) (normal|left|inverted|right) \(' | egrep -o '(normal|left|inverted|right)')"

# Using current screen orientation proceed to rotate screen and input tools.
case "$rotation" in
    normal)
    # rotate to the left
    xrandr -o left
    xsetwacom set "Serial Wacom Tablet WACf004 stylus" rotate ccw
    xsetwacom set "Serial Wacom Tablet WACf004 eraser" rotate ccw
    ;;
    left)
    # rotate to normal
    xrandr -o normal
    xsetwacom set "Serial Wacom Tablet WACf004 stylus" rotate none
    xsetwacom set "Serial Wacom Tablet WACf004 eraser" rotate none
    ;;
esac

```

The assignment of the keycode to the script depends on the currently installed desktop environment. For [GNOME](/index.php/GNOME "GNOME"), the assignment can be easily done in the custom shortcuts section of the Keyboard preferences.

If you are using another desktop environment (such as [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE"), [Fluxbox](/index.php/Fluxbox "Fluxbox"), etc) you can always use the program [xbindkeys](/index.php/Xbindkeys "Xbindkeys").

### Screen auto-rotation

Screen auto-rotation does not work by default. Installing the [HDAPS](/index.php/HDAPS "HDAPS") package will allow for the utilization of the ThinkPad X200's integrated 2-axis accelerometer.

After installing HDAPS, the following configuration file may be created to automate screen rotation:

```
#!/bin/bash

# (To have the exact names of these devices you should type the command : xsetwacom --list devices )
stylus="Serial Wacom Tablet stylus" 
eraser="Serial Wacom Tablet eraser"

function rotate {
    if [ $# -lt 1 ]; then  # error ...
	exit 1 
    fi

    case "$1" in
        up)
            nextRotate="none"
            nextOrient="normal" ;;
        down)
            nextRotate="half"
            nextOrient="inverted" ;;
	right)
            nextRotate="ccw"
            nextOrient="left" ;;
	left)
            nextRotate="cw"
            nextOrient="right";;
    esac

    # Rotate the screen      
    xrandr -o $nextOrient

    # Rotate the tablet                      
    xsetwacom set "$stylus" Rotate $nextRotate
    xsetwacom set "$eraser" Rotate $nextRotate
}

while true; do
    # 1) We extract data about the actual position
    position=$(cat /sys/devices/platform/hdaps/position)
    x=$(echo $position | sed -n "s/(\([-0-9]*\),\([-0-9]*\).*)/\1/p") # most of time contained in [350,650]
    y=$(echo $position | sed -n "s/(\([-0-9]*\),\([-0-9]*\).*)/\2/p") # most of time contained in [-650,-350]

    # 2) We work out the x value (= left and right inclination) (always between 
    if [ $x -lt 400 ]; then
	rotate left
    elif [ $x -gt 600 ]; then
	rotate right
    fi

    # 3) We work out the y value (= front and back inclination)
    if [ $y -gt -400 ]; then
	rotate down
    elif [ $y -lt -600 ]; then
	rotate up
    fi

    # 4) wait before checking the value again
    sleep 0.5
done

```

This script may be executed during startup to further automate the screen rotation process. See [Autostarting](/index.php/Autostarting "Autostarting") for more information on startup automation.

### Power consumption and fan control

**Note:** There is a useful [blog post](http://orschiro.blogspot.com/2013/06/linux-powersaving-measures.html) describing possible measures to reduce power consumption of a X200T to almost 7 Watt.

To set up an efficient power saving environment, install the [tlp](https://www.archlinux.org/packages/?name=tlp) package. A detailed guide how to implement a simplistic power saving environment based upon TLP can be found [here](http://www.robert.orzanna.de/simplistic-powersaving-with-systemd-service-files-and-udev-rules/).

Fan-control software can be used to further reduce power consumption. The [tpfanco-svn](https://aur.archlinux.org/packages/tpfanco-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tpfanco-svn)]</sup> package from AUR provides a simplistic GTK GUI for setting up fan activation thresholds based upon the X200's multiple hardware sensors.

Investigate [Powertop](/index.php/Powertop "Powertop") and the [powerstat-git](https://aur.archlinux.org/packages/powerstat-git/)<sup><small>AUR</small></sup> package from AUR for more information on measuring actual power consumption.

See [Power saving](/index.php/Power_saving "Power saving") for additional tips.

### Suspend to RAM / hibernate

Suspend to ram and hibernation is fully supported. See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate") for more information.

### BIOS WiFi-Whitelist Removal

**Warning:** Modifying the system's firmware can be rewarding but it is also very dangerous. Proceed with caution.

Like most ThinkPads, the X200(s) / X200T has an [FCC enforced whitelist](http://support.lenovo.com/us/en/documents/migr-43693) for wireless cards. This means if a third party wireless card is installed via Mini PCIe or PCMCIA slot, the system will not boot. However, there are many individuals who modify and distribute whitelist-free BIOS updates online.

The whitelist-free BIOS for the X200(s) can be found [here](http://forums.mydigitallife.info/threads/5866-LENOVO-(IBM)-Bioses-especially-Thinkpad/page501) and the whitelist-free BIOS for the X200T can be found [here](http://forums.mydigitallife.info/threads/20223-Remove-whitelist-check-add-ID-s-to-break-hardware-restrictions-mod-requests/page338).

Make sure the BIOS version the system is running matches the cracked version being distributed.

For more information about BIOS flashing and system firmware, please see [Flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux "Flashing BIOS from Linux").

### Coreboot / Libreboot

**Warning:** Modifying the system's firmware can be rewarding but it is also very dangerous. Proceed with caution.

[Coreboot](http://coreboot.org/) is a fast and flexible open source firmware solution to replace the system BIOS. The ThinkPad X200 is [fully supported](https://www.fsf.org/news/libreboot-x200-laptop-now-fsf-certified-to-respect-your-freedom) by Coreboot and good documentation can be found at the Libreboot project's official [website](http://libreboot.org/). The X200s and X200 Tablet are also partially supported per the [Libreboot X200 documentation](http://www.libreboot.org/docs/hcl/x200.html#x200s).

For more information on the Libreboot project, see Gluglug's official [website](http://www.gluglug.org.uk/).

## Troubleshooting

### failed to execute '/usr/sbin/inputattach'

If you see the above error in your logs, copy `/usr/lib/udev/rules.d/70-wacom.rules` to `/etc/udev/rules.d/70-wacom.rules` and comment out SUBSYSTEM of inputattach.

### System feels unresponsive

If your system feels unresponsive and lagging, you can try creating a file called `/etc/modprobe.d/drm_kms.conf`:

```
options drm_kms_helper poll=N

```

### Backlight fails to activate after system resume

On rare occasions the backlight may not activate after resuming. See [Problem with display remaining black after resume](http://www.thinkwiki.org/wiki/Problem_with_display_remaining_black_after_resume) for possible workarounds.

### PM device: Resume from hibernation error: Failed to restore -19

This is likely to be related to the tpm_tis and tpm modules not being properly unloaded before hibernation. These modules are required by the device listed in the error as 00:0a:

```
# dmesg | grep 00:0a
[    0.377877] pnp 00:0a: Plug and Play ACPI device, IDs PNP0c31 (active)
[   10.746742] tpm_tis 00:0a: 1.2 TPM (device-id 0x1020, rev-id 6)
[   10.746751] tpm_tis 00:0a: Intel iTPM workaround enabled
[   10.866734] tpm_tis 00:0a: TPM is disabled/deactivated (0x6)

```

To unload the module create the following executable file called `/usr/lib/systemd/system-sleep/tpm.sh`, assuming the use of the systemd hibernation procedure:

```
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "Going to $2..."
    modprobe -r tpm
    modprobe -r tpm_tis
    ;;
  post/*)
    echo "Waking up from $2..."
    modprobe tpm
    modprobe tpm_tis
    ;;
esac

```

### mei_me 0000:00:03.0: suspend

If you are seeing this error, a workaround is to blacklist the `mei` and `mei_me` modules. More information can be found [here](https://bbs.archlinux.org/viewtopic.php?pid=1314282#p1314282).

### pciehp 0000:00:1c.1:pcie04: Cannot add device at 0000:03:00

See [#mei_me 0000:00:03.0: suspend](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X200&action=submit#mei_me_0000:00:03.0:_suspend).

### Uhhuh. NMI received for unknown reason 30.

The Thinkpad X200 is known to report the following error on resume from hibernation or suspension:

```
Uhhuh. NMI received for unknown reason 30.
Dazed and confused, but trying to continue
Do you have a strange power saving mode enabled?

```

In this case you can disable the high precision event timer (HPET) by adding "nohpet" to your [GRUB](/index.php/GRUB "GRUB") kernel parameter line.

### High pitched noises

The X200(s) is prone to high pitched, low volume noises originating from the CPU, usually in low power scenarios. One proved solution to this is to disable CPU power control in the BIOS.

High pitched noises may also be emitted from the display's inverter board on CCFL models. This is normal behavior and may or may not be present depending on how much energy the installed display draws.

For more information see [[1]](http://www.thinkwiki.org/wiki/Problem_with_high_pitch_noises).

## See also

*   Thinkwiki: [X200 Overview](http://www.thinkwiki.org/wiki/Category:X200)
*   ThinkWiki: [How to reduce power consumption](http://www.thinkwiki.org/wiki/How_to_reduce_power_consumption)
*   [Example installation procedure for X200s](https://gist.github.com/yuvadm/52b3f350293a96501478)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X200&oldid=392341](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X200&oldid=392341)"