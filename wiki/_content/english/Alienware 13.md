This article documents configuration and troubleshooting specific to the Alienware 13 laptop.

See the [Installation guide](/index.php/Installation_guide "Installation guide") for general installation instructions.

## Contents

*   [1 Getting Linux to boot](#Getting_Linux_to_boot)
*   [2 Touchpad](#Touchpad)
*   [3 Wireless](#Wireless)
*   [4 Switchable graphics](#Switchable_graphics)
*   [5 Keyboard lights](#Keyboard_lights)
*   [6 Intel powersaving options](#Intel_powersaving_options)
*   [7 OLED screen brightness](#OLED_screen_brightness)
*   [8 OLED screen doesn't light up after resume](#OLED_screen_doesn't_light_up_after_resume)
*   [9 Switching Windows from RAID to AHCI mode](#Switching_Windows_from_RAID_to_AHCI_mode)
*   [10 HDMI/Mini-DP audio](#HDMI/Mini-DP_audio)
*   [11 R1 freezes on suspend/hibernate](#R1_freezes_on_suspend/hibernate)

## Getting Linux to boot

First of all we must create a [bootable usb](/index.php/USB_flash_installation_media "USB flash installation media"), after that we must reboot the computer and press `F12` button while the bios is loading to access to the boot menu, from there we select the USB and boot from there.

The first issue that we can find is that the distribution does not boot but gets stuck into a nouveau loop or a black screen. If this happens, we must change the kernel parameters to get ArchLinux to boot. Try to erase all default parameters and use only `nomodeset`.

The Kaby lake R3 suffers from a X lockup when either trying to start X or running `lspci` when the discrete GPU is off. There are [kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=156341) and [bumblebee bug](https://github.com/Bumblebee-Project/Bumblebee/issues/764) open to track this issue. In the meantime you can add the following to your kernel commandline at boot: `acpi_osi=! acpi_osi="Windows 2009"`

## Touchpad

If the touchpad does not work, try to unload the `i2c_hid` module:

```
# modprobe -r i2c_hid

```

and restart the graphical environment. If that helps, consider [blacklisting](/index.php/Blacklist "Blacklist") the module.

## Wireless

At the moment of writing this, the wifi network of the Alienware13 is a Atheros Qualcomm Killer N1525, which is not configured by the default installation.

```
$ lspci
...
01:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 20)
02:00.0 Ethernet controller: Qualcomm Atheros Killer E220x Gigabit Ethernet Controller (rev 10)
...

```

Here is the [ubuntu bug](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1383184).

Fortunately, the enclosed patch is able to get it to work. It was tested on Kernel 4.2.5-1 as follows:

```
$ git clone [https://github.com/sumdog/ath10k-firmware](https://github.com/sumdog/ath10k-firmware)
# cp -a ath10k-firmware/ath10k/QCA6174 /lib/firmware/ath10k/QCA6174
# echo "options ath10k_core skip_otp=y" | tee -a /etc/modprobe.d/ath10k.conf

```

After a reboot, wireless should work, including wifi-ac speeds.

For Alienware 13 R3, the wifi works out of box. The following kernel error seems to be harmless.

```
3c:00.0 Ethernet controller: Qualcomm Atheros Killer E2400 Gigabit Ethernet Controller (rev 10)
3d:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

```
[    3.420857] ath10k_pci 0000:3d:00.0: could not fetch firmware file 'ath10k/QCA6174/hw3.0/firmware-5.bin': -2

```

## Switchable graphics

To have switchable graphics see [bumblebee](/index.php/Bumblebee "Bumblebee") instructions. The utility is able to turn on and off the dedicated graphics card ondemand and without having to restart the computer or reopening session.

It is to be noted that some alienware laptop (AlienWare 13 R3) shows this [issue](/index.php/Bumblebee#Lockup_issue_.28lspci_hangs.29 "Bumblebee") where lspci / startx / any command hangs and freeze the system when probing inactive discrete nvidia gpu.

## Keyboard lights

To get access to the keyboard lights they can be controlling by sending data to the correct usb.

```
 $ lsusb
 ...
 Bus 002 Device 003: ID 187c:0527 Alienware Corporation 
 ...

```

There plenty of programs like pyAlienFX or [Alienware-KBL](https://github.com/rsm-gh/alienware-kbl) and none of these worked for me, but there is a github project that consists on sending data to USB using `libusb` that worked fine.

```
 git clone [https://github.com/snooze6/hack-alienfx](https://github.com/snooze6/hack-alienfx)
 make all

```

In case of a compilation error similar to `"FILE is not defined"`, try adding a `stdio.h include` to the following:

 `/usr/include/readline/rltypedefs.h` 
```
# Add
#include <stdio.h>
```

And try compilation again.

Once it is compiled, test by running:

```
 # ./run seq/snooze

```

and keyboard lights should work.

To register it as a command and can use this program without being root we can do the next:

```
 # cp run /usr/local/bin/
 # mkdir /usr/local/fx
 # cp seq/* /usr/local/fx
 # chmod 4755 /bin/fx
 # cp lights.sh /usr/local/bin/lights
 # chmod +x /usr/local/bin/lights

```

Now it should trigger by executing:

```
 $ lights
 $ lights on
 $ lights off

```

from a console.

We can simply add the commands to the energy admin or the startup to make keyboard lights change automatically.

## Intel powersaving options

In order to get the most out of your battery life it is recommended to use additional powersaving options. The following should be save to use.

```
 # cat /etc/modprobe.d/i915.conf 
 options i915 enable_rc6=1 enable_fbc=1 enable_guc_loading=1 enable_guc_submission=1 enable_psr=1

```

Refer to [Intel graphics#RC6 sleep modes (enable_rc6)](/index.php/Intel_graphics#RC6_sleep_modes_(enable_rc6) "Intel graphics") and [Dell XPS 13 (9360)#Module-based Powersaving Options](/index.php/Dell_XPS_13_(9360)#Module-based_Powersaving_Options "Dell XPS 13 (9360)") for additional information on each of them.

## OLED screen brightness

With gnome, the brightness control keys toggles the on-screen display, but it doesn't change the brightness level. The screen blanking feature also doesn't work. The following command can be used to set the brightness to 50%.

```
xrandr --output eDP1 --brightness .5

```

Until brightness control is supported by the kernel, we can use the following script to read off the brightness values from sysfs and apply xrandr brightness reduction to it:

```
$ cat /usr/local/bin/xbacklightmon 

```

```
#!/bin/sh

path=/sys/class/backlight/acpi_video0

luminance() {
    read -r level < "$path"/actual_brightness
    factor=$((max))
    new_brightness="$(bc -l <<< "scale = 2; $level / $factor")"
    printf '%f
' $new_brightness
}

read -r max < "$path"/max_brightness

xrandr --output eDP-1 --brightness "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    xrandr --output eDP-1 --brightness "$(luminance)"
done

```

Make it executable and add it to your DE's autostart and you are set. We use inotifywait to know when the value is modified so we don't busy wait but are still responsive.

## OLED screen doesn't light up after resume

Sometimes when you sleep the computer and resume it, the OLED screen will flicker but not actually light up again. To fix this use the following xrandr command:

```
$ cat /usr/local/bin/resmon 
#!/bin/sh
xrandr -d :0.0 --output eDP-1 --off && xrandr -d :0.0 --output eDP-1 --auto

```

I have added it to a script so that I can easily run it if the monitor is off after resume: You can add it to a keyboard shortcut, or use run command, whichever is easier.

## Switching Windows from RAID to AHCI mode

The stock installation of Windows is in RAID mode which makes linux unable to see the NVME disks. However once installed in RAID mode, Windows refuses to boot when the disk is in AHCI mode. You can however fix that by following those steps:

1.  Right-click the Windows Start Menu. **Choose Command Prompt (Admin).**
    *   If you don’t see Command Prompt listed, it’s because you have already been updated to a later version of Windows. If so, use this method instead to get to the Command Prompt:
        1.  Click the Start Button and type cmd
        2.  Right-click the result and select **Run as administrator**
2.  Type this command and press ENTER: **bcdedit /set {current} safeboot minimal**
    *   If this command does not work for you, try **bcdedit /set safeboot minimal**
3.  Restart the computer and enter BIOS Setup (the key to press varies between systems).
4.  Change the SATA Operation mode to AHCI from either IDE or RAID (again, the language varies).
5.  Save changes and exit Setup and Windows will automatically boot to Safe Mode.
6.  Right-click the Windows Start Menu once more. Choose **Command Prompt (Admin)**.
7.  Type this command and press ENTER: **bcdedit /deletevalue {current} safeboot**
    *   If you had to try the alternate command above, you will likely need to do so here also: **bcdedit /deletevalue safeboot**
8.  Reboot once more and Windows will automatically start with AHCI drivers enabled.

Source: [[1]](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/)

## HDMI/Mini-DP audio

The HDMI and the mini-DP are connected to the nvidia card, which means that in order for them to play audio you need to route it through the sound card attached to the nvidia device. However by default the GPU has its audio disabled for whatever reason. To enable it follow [NVIDIA/Troubleshooting#No audio over HDMI](/index.php/NVIDIA/Troubleshooting#No_audio_over_HDMI "NVIDIA/Troubleshooting")

## R1 freezes on suspend/hibernate

Due to firmware crashes with the ath10 wifi driver on R1 you may encounter system freezes upon suspend/hibernate. A workaround would be to unload the ath10 module before going down and load it back upon wake up. Put this in /usr/lib/systemd/system-sleep/suspend.sh and make it executable:

```
#!/bin/bash
if [ "${1}" == "pre" ]; then
   rmmod ath10k_pci ath10k_core
   sleep 1
elif [ "${1}" == "post" ]; then
   modprobe ath10k_pci
fi

```

Don't forget to

```
systemctl daemon reload

```

after that.

Note that the nouveau driver also can be the source of problems with suspend, so if the above doesn't help, try to either blacklist it or install the non-free nvidia driver to replace it.