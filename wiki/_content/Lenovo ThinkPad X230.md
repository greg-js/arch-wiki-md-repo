# Lenovo ThinkPad X230

[Lenovo ThinkPad X230](http://www.lenovo.com/hk/en/productcatalog/pdf/X230-datasheet.pdf)

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Screen](#Screen)
    *   [1.3 Touchpad](#Touchpad)
    *   [1.4 Backlight control keys](#Backlight_control_keys)
    *   [1.5 Suspend to ram](#Suspend_to_ram)
        *   [1.5.1 Suspend to ram fails](#Suspend_to_ram_fails)
    *   [1.6 Microphone](#Microphone)
*   [2 Power Saving](#Power_Saving)
    *   [2.1 TLP](#TLP)
*   [3 Not Working](#Not_Working)
*   [4 See also](#See_also)

## Configuration

### Kernel

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
BINARIES="badblocks"
FILES="/etc/modprobe.d/modprobe.conf"
HOOKS="base udev autodetect block filesystems keyboard fsck"

```

 `/etc/modprobe.d/modprobe.conf` 

```
options i915 enable_rc6=1 enable_fbc=1 lvds_downclock=1
options iwlwifi 11n_disable=1

```

The `badblocks` binary helps fix logical bad blocks if detected by fsck during system startup. The first line in modprobe.conf file enables different Intel HD power saving options. To see what each of the parameters does, issue the command `modinfo i915`. The second line disables the wifi N mode as the Intel wireless driver suffers connection loss due to possible bugs. You can comment out this line if you want to transfer data at wireless N speeds.

After saving the above files, make sure to regenerate your init ram image by the command `mkinitcpio -p linux`, and follow the steps in [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

**Note:** Using **enable_rc6=1** will enable basic power saving with first stage of [C-state 6](http://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface#Processor_states) [(sleeping state)](http://software.intel.com/en-us/blogs/2013/06/03/intel-xeon-phi-coprocessor-power-management-part-2a-core-c-states-the-details). The stages vary by the depth of sleep, that can be attained by setting the value of **enable_rc6** between 1 to 7 in ascending order as can be seen in its documentation with **modinfo i915** command shown above.

**Warning:** Keep in mind that c-state power saving always comes at performance sacrifice and setting a higher value can cause a jittery display or some other unexplained and unexpected misbehavior with i915 so you may want to experiment with different values to find out what suits your needs.

### Screen

X230 has IPS screen with 125.37 DPI. Refer to [HiDPI](/index.php/HiDPI "HiDPI") page for more information.

### Touchpad

The original configuration renders the touchpad quite useless, as it behaves very jumpily. [[Ubuntu Bugtracker](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-input-synaptics/+bug/1042069/comments/5)] offers a solution for this issue. Add the following

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 

```
Section "InputClass"
        Identifier "touchpad"
        MatchProduct "SynPS/2 Synaptics TouchPad"
        # MatchTag "lenovo_x230_all"
        Driver "synaptics"
        # fix touchpad resolution
        Option "VertResolution" "100"
        Option "HorizResolution" "65"
        # disable synaptics driver pointer acceleration
        Option "MinSpeed" "1"
        Option "MaxSpeed" "1"
        # tweak the X-server pointer acceleration
        Option "AccelerationProfile" "2"
        Option "AdaptiveDeceleration" "16"
        Option "ConstantDeceleration" "16"
        Option "VelocityScale" "20"
        Option "AccelerationNumerator" "30"
        Option "AccelerationDenominator" "10"
        Option "AccelerationThreshold" "10"
	# Disable two fingers right mouse click
	Option "TapButton2" "0"
        Option "HorizHysteresis" "100"
        Option "VertHysteresis" "100"
EndSection

```

Setting e.g. the motion-acceleration value in dconf to 2.8 works nicely.

### Backlight control keys

**Note:** On most X230 models, backlight works by default without any issues. Use below only in case of any problems.

Due to an issue with the firmware of several ThinkPads the backlight control keys (fn + F8/F9 on the X230) don't work correctly. Setting the brightness via e.g. the GNOME power control panel or altering the brightness value in sysfs is possible.

The issue can be temporarily and partially [http://www.example.com](http://www.example.com) link titlefixed in adding the acpi_osi="!Windows 2012" [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). The fix is partial in that only 8 steps are accessible via the keys. See [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=51231) for details.

### Suspend to ram

There is an issue with system shutdown with power saving tools that cannot distinguish sys devices. You will need to add to the systemd shutdown trigger on this machine or else you'll get a system reboot when you shutdown the machine. Put this in /etc/rc.local.shutdown and update and enable its service, if not already.

 `/etc/rc.local.shutdown` 

```
#!/bin/bash
# /etc/rc.local.shutdown: Local shutdown script.
# A script to act as a workaround for the bug in the runtime power management module, which causes thinkpad laptops to restart after shutting down. 
# Bus list for the runtime power management module.
buslist="pci i2c"
for bus in $buslist; do                                                             
  for i in /sys/bus/$bus/devices/*/power/control; do                              
    echo on > $i
  done
done

```

 `/usr/lib/systemd/system/rc-local-shutdown.service` 

```
[Unit]
Description=/etc/rc.local.shutdown Compatibility
ConditionFileIsExecutable=/etc/rc.local.shutdown
DefaultDependencies=no
After=rc-local.service basic.target
Before=shutdown.target

[Service]
Type=oneshot
ExecStart=/etc/rc.local.shutdown
StandardInput=tty
RemainAfterExit=yes

```

#### Suspend to ram fails

As of kernel 3.10 and 3.11 suspend may fail because the kernel tries to switch off the onboard ethernet device twice (see [http://forums.fedoraforum.org/archive/index.php/t-293457.html](http://forums.fedoraforum.org/archive/index.php/t-293457.html)).

A workaround is to unload the driver manually and reload it on wake.

 `/usr/lib/systemd/system-sleep/e1000e-probe.sh` 

```
#!/bin/bash
# /usr/lib/systemd/system-sleep/e1000e-probe.sh
# handles e1000e driver suspend problems:
#	pci_pm_suspend(): e1000_suspend+0x0/0x20 [e1000e] returns -2
#	dpm_run_callback(): pci_pm_suspend+0x0/0x150 returns -2
#	PM: Device 0000:00:19.0 failed to suspend async: error -2
#	PM: Some devices failed to suspend

case "$1" in
   "pre") rmmod e1000e
   ;;
   "post") modprobe e1000e
   ;;
esac

```

### Microphone

If the built-in microphone is not detected when using PulseAudio, the steps here may fix the issue: [PulseAudio/Troubleshooting#Microphone not detected by PulseAudio](/index.php/PulseAudio/Troubleshooting#Microphone_not_detected_by_PulseAudio "PulseAudio/Troubleshooting").

## Power Saving

Follow the main article: [Power saving](/index.php/Power_saving "Power saving")

Power saving [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") in addition to graphics card power saving, are shown below. `acpi_backlight=vendor` loads the vendor specific [Backlight#ACPI](/index.php/Backlight#ACPI "Backlight") driver (i.e. thinkpad_acpi) so the brightness keys (Fn + F8 and Fn + F9) work correctly.

Note that the `acpi_backlight=vendor` kernel option also works with the standard Arch kernel (currently 3.7.10-1) and has the additional bonus that (Fn + spacebar) controls the keyboard lighting.

### TLP

Users of [TLP](/index.php/TLP "TLP") need to pay attention to a hardware bug according to which it is recommended to only use either the upper or lower charging threshold. The following configuration is recommended by the developer of TLP.[[1](http://thinkpad-forum.de/threads/184510-elementary-OS-Thinkpad-X230-einrichten?p=1865345&viewfull=1#post1865345)]

 `/etc/default/tlp` 

```
START_CHARGE_THRESH_BAT0=67
STOP_CHARGE_THRESH_BAT0=100

```

## Not Working

*   Microphone on-off key does not work out of the box

## See also

*   [A Hacker's Ongoing Review for Lenovo ThinkPad X230](https://gist.github.com/bassu/8478346)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X230&oldid=412581](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X230&oldid=412581)"