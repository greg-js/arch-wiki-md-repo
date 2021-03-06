**Note:** This page refers to the 7590 revision of the XPS 15\. Most of it also applies to the Precision 5540.

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Hibernate) | Working |
| [Integrated Graphics](#Graphics) | Working |
| [Discrete Nvidia Graphics](#Graphics) | Modify |
| [Backlight](#Graphics) | Modify |
| [WiFi](#Networking) | Working |
| [Bluetooth](#Networking) | Working |
| [rfkill](#Networking) | Working |
| Audio | Working |
| [Touchpad](#Touchpad_and_Touchscreen) | Working |
| [Touchscreen](#Touchpad_and_Touchscreen) | Working |
| Webcam | Working |
| Card Reader | Working |
| Function/Multimedia Keys | Working |
| [Power Management](#Power_Management) | Working |
| [EFI firmware updates](#Firmware_Update) | Working |
| [Fingerprint reader](#Fingerprint_reader) | Not working |

Related articles

*   [Dell XPS 15](/index.php/Dell_XPS_15 "Dell XPS 15")
*   [Dell XPS 15 2-in-1 (9575)](/index.php/Dell_XPS_15_2-in-1_(9575) "Dell XPS 15 2-in-1 (9575)")
*   [Dell XPS 15 9550](/index.php/Dell_XPS_15_9550 "Dell XPS 15 9550")
*   [Dell XPS 15 9560](/index.php/Dell_XPS_15_9560 "Dell XPS 15 9560")
*   [Dell XPS 15 9570](/index.php/Dell_XPS_15_9570 "Dell XPS 15 9570")

This page contains recommendations for running Arch Linux on the Dell XPS 15 7590 (2019).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pre-Installation UEFI Settings](#Pre-Installation_UEFI_Settings)
*   [2 Power Management](#Power_Management)
    *   [2.1 Suspend](#Suspend)
    *   [2.2 Hibernate](#Hibernate)
    *   [2.3 Powertop](#Powertop)
*   [3 Thermal Management](#Thermal_Management)
*   [4 Graphics](#Graphics)
    *   [4.1 kernel modules](#kernel_modules)
    *   [4.2 NVIDIA Optimus](#NVIDIA_Optimus)
        *   [4.2.1 Manually loading/unloading NVIDIA module](#Manually_loading/unloading_NVIDIA_module)
        *   [4.2.2 Using nvidia-xrun](#Using_nvidia-xrun)
    *   [4.3 Backlight](#Backlight)
    *   [4.4 Backlight function keys](#Backlight_function_keys)
    *   [4.5 Backlight in Wayland](#Backlight_in_Wayland)
    *   [4.6 Backlight in Sway](#Backlight_in_Sway)
*   [5 Networking](#Networking)
    *   [5.1 WiFi](#WiFi)
*   [6 Touchpad and Touchscreen](#Touchpad_and_Touchscreen)
*   [7 Docks](#Docks)
*   [8 Firmware Update](#Firmware_Update)
    *   [8.1 UEFI](#UEFI)
*   [9 Tips and Tricks](#Tips_and_Tricks)
*   [10 Fingerprint reader](#Fingerprint_reader)

## Pre-Installation UEFI Settings

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

**Warning:** If you will be dual booting alongside an existing Windows installation, Windows will not boot if you just go ahead and make the switch to AHCI as described in the steps below. You must log into you Windows install both before and after that BIOS change [to set and then remove a safeboot flag](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/), respectively.

*   Under 'System Configuration', change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD.
*   Under 'Secure Boot', disable secure boot to allow Linux to boot.
*   Under 'POST Behaviour', change "Fastboot" to "Thorough". This prevents intermittent boot failures.

If you are using multiboot with an existing Windows installation, make sure that "fast startup" is disabled in Windows 8/10.

## Power Management

### Suspend

By default, the very inefficient s2idle suspend variant is incorrectly selected. This is probably due to the BIOS. The much more efficient deep variant should be selected instead:

```
 $ cat /sys/power/mem_sleep 
 [s2idle] deep
 $ echo deep|sudo tee /sys/power/mem_sleep
 $ cat /sys/power/mem_sleep 
 s2idle [deep]

```

To make the change permanent add `mem_sleep_default=deep` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

An easy way would be to add `mem_sleep_default=deep` to the `GRUB_CMDLINE_LINUX_DEFAULT` entry in /etc/default/grub:

```
 GRUB_CMDLINE_LINUX_DEFAULT="mem_sleep_default=deep"

```

Read more regarding the sleep variants on the kernel documentation [[1]](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html).

**Warning:** Some users have reported a problem where the CPUs get stuck in a high power state after resuming from S3 (deep) suspension [[2]](https://www.reddit.com/r/Dell/comments/91313h/xps_15_9570_c_state_bug_after_s3_sleep_and_modern/).

### Hibernate

### Powertop

## Thermal Management

Default thermal management is not very optimized (this is my experience with the i9 processor at least).

The laptop gets hot quite often and the fans run at high speed most of the time.

One solution I found is to use powertop to get a quieter system.

See [Powertop](/index.php/Powertop "Powertop") for details.

You may activate manual fans control with [i8kutils](https://launchpad.net/i8kutils). Install [i8kutils](https://aur.archlinux.org/packages/i8kutils/) and [dell-bios-fan-control-git](https://aur.archlinux.org/packages/dell-bios-fan-control-git/). Edit `/etc/i8kutils/i8kmon.conf` and enable services:

```
$ sudo systemctl daemon-reload
$ sudo modprobe dell-smm-hwmon
$ sudo modprobe i8k
$ sudo systemctl enable --now i8kmon.service
$ sudo systemctl enable --now dell-bios-fan-control.service

```

You may have to modify the modprobe options for `dell-smm-hwmon` to have the above work. See more at this reddit [thread](https://www.reddit.com/r/Dell/comments/9pdgid/configuring_the_xps_to_play_nice_with_linux/)

 `options dell-smm-hwmon ignore_dmi=1` 

## Graphics

### kernel modules

### NVIDIA Optimus

#### Manually loading/unloading NVIDIA module

**Note:** The section is about manually loading/unloading NVIDIA module without packages unsupported by the model like [bbswitch](https://www.archlinux.org/packages/?name=bbswitch). After manually loaded NVIDIA module you still won't be able to run anything that actually displays something though have the module loaded is a prerequisite to all the things that are related to using the discrete graphic card, since it is mainly related to how the X window system handles the graphic card. However, you would be able to do GPU-related calculations, such like using CUDA or OpenCL. For running programs that do have something to display without launching a new X session, use [bumblebee](https://www.archlinux.org/packages/?name=bumblebee), see [bumblebee](/index.php/Bumblebee "Bumblebee").

First disable the nouveau modules.

 `/etc/modprobe.d/blacklist.conf` 
```
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
blacklist nv

```

If the nouveau modules are already loaded, a reboot would be required.

**Warning:** Beware and check your X window system configuration before you reboot. If the discrete GPU is running the X server and you reboot the computer without further configurations on X window system, there could be problems in starting the X server and getting into a GUI.

Install [nvidia](https://www.archlinux.org/packages/?name=nvidia)

A script has been written to automate some tedious jobs, run

```
curl [https://raw.githubusercontent.com/noxultranonerit/SimpleScripts/master/nvidia_gpu](https://raw.githubusercontent.com/noxultranonerit/SimpleScripts/master/nvidia_gpu) -o gpucli
chmod +x gpucli

```

to download the script and make it executable. Next run

 `gpucli` 

and follow the instructions.

**Note:** One should investigate the script and learn what the script will do before using it.

When unloading the dGPU, a message saying `module unload failed, run nvidia-smi to check running process and kill them` may be printed. Most process can be killed with the method described, that is, with `kill PROCESS_PID`, or when it doesn't work, with `kill -9 PROCESS_PID`.

If you are loading the dGPU in a existing X session, the server would automatically handle the dGPU, leading to unloading failure. In this case you should add

 `/etc/X11/xorg.conf.d/01-noautogpu.conf` 
```
Section "ServerFlags"
	Option "AutoAddGPU" "off"
EndSection

```

Finally, create a service locking NVIDIA GPU on shutdown

 `/etc/systemd/system/disable-nvidia-on-shutdown.service` 
```
[Unit]
Description=Disables Nvidia GPU on OS shutdown

[Service]
Type=oneshot
RemainAfterExit=true
ExecStart=/bin/true
ExecStop=/bin/bash -c "mv /etc/modprobe.d/disable-nvidia.conf.disable /etc/modprobe.d/disable-nvidia.conf || true"

[Install]
WantedBy=multi-user.target
```

Reload systemd daemons and enable the `disable-nvidia-on-shutdown` service:

```
 sudo systemctl daemon-reload
 sudo systemctl enable disable-nvidia-on-shutdown.service

```

Note that the script aforementioned will not install the systemd service. If you do not want a systemd service installed, make sure to turn off the computer only after you have unloaded the dGPU, i.e. have run `gpucli --off` and a success message has been printed.

You will be able to run CUDA after `gpucli --on`.

#### Using nvidia-xrun

If you want to start a whole X-session with dGPU, install [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/) (not [nvidia-xrun-pm](https://aur.archlinux.org/packages/nvidia-xrun-pm/) or [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/)). Consult [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun").

### Backlight

If using a desktop environment with an OLED screen, you may notice the backlight does not function. Since on some models the screen is OLED (which do not have physical backlights), you may need to shim the ACPI backlight functions to update Xrandr's "--backlight" option. This is done by monitoring the acpi_video0 levels, and updating the xrandr brightness levels accordingly.

For this to work, you must first install [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) and [bc](https://www.archlinux.org/packages/?name=bc). Then, create the following file:

```
$ nano /usr/local/bin/xbacklightmon

```

```
#!/bin/sh
#use LC_NUMERIC if you are using an European LC, else printf will not work because it expects an comma instead of a decimal point
LC_NUMERIC="en_US.UTF-8"

#Exit with 1 if $DISPLAY env isn't set. Helps when using the start up script below
[ -z "$DISPLAY" ] && exit 1;

# modify this path to the location of your backlight class
path=/sys/class/backlight/intel_backlight

read -r max < "$path"/max_brightness

luminance() {
    read -r level < "$path"/actual_brightness
    factor=$((max))
    new_brightness="$(bc -l <<< "scale = 2; $level / $factor")"
    printf '%f
' $new_brightness
}

# support both intel and nvidia
DEVICE=eDP-1
if [ ! -z "$(xrandr -q --output $DEVICE 2>&1)" ]; then
  DEVICE=eDP-1-1
fi

xrandr --output $DEVICE --brightness "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    xrandr --output $DEVICE --brightness "$(luminance)"
done

```

Then make this file executable and owned by root:

```
$ chown root:root /usr/local/bin/xbacklightmon
$ chmod 755 /usr/local/bin/xbacklightmon

```

You may test this by running the file, and using the backlight keys to test if the brightness updates.

To run the script automatically on startup, create a xbacklightmon.service file containing the following:

```
$ mkdir -p $HOME/.config/systemd/user/
$ nano $HOME/.config/systemd/user/xbacklightmon.service

```

```
[Unit]
Description=Ugly fix to be able to control the brightness of OLED screens via keyboard brightness
After=multi-user.target

[Service]
Type=simple
ExecStart=/usr/local/bin/xbacklightmon
Restart=on-failure
RestartSec=1

[Install]
WantedBy=default.target

```

And to enable on startup

 `systemctl --user enable xbacklightmon.service` 

**Please note:** If you are using the xf86-video-intel driver, you will need to replace 'eDP-1' in the script above with 'eDP1' You also have to change the path to 'path=/sys/class/backlight/intel_backlight/' if you are using xf86-video-intel

### Backlight function keys

When using a LCD display device and in a desktop environment (KDE verified) the function key will be working out of the box for the DEs have their own key mapping. However, when in a window manager with modesetting driver (and also int the tty console), the backlight controlling function keys won't be working and will throw out errors like `ACPI BIOS Error, could not resolve symbol`.

Usually `/sys/class/backlight/intel_backlight` is symlinked to `/sys/device/pci00/0000:00:02.0/drm/card0/card0-eDP-1/`, and by changing the value of `backlight` file inside the directory the backlight level can be controlled, but the operation needs root previliege. Establishing a udev rule and accordingly a backlight control group will help, but these steps can be done easily with the package [light](https://www.archlinux.org/packages/?name=light).

Then a mapping of function key to the command, say, `light -A 3` and `light -U 3` would be in need. `XF86BrightnessDown` and `XF86BrightnessUp` won't be working. The mapping of the keys can be done with [acpid](https://www.archlinux.org/packages/?name=acpid). Install the package, then insert these lines to the `case "$1" in` block

 `/etc/acpi/handler.sh` 
```
video/brightnessup) light -A 3 ;;
video/brightnessdown) light -U 3 ;;

```

start and enable the service:

`systemctl enable acpid.service`, `systemctl start acpid.service`.

### Backlight in Wayland

The xrandr command does not work with Wayland. Instead you can use the [icc-brightness](https://www.archlinux.org/packages/?name=icc-brightness) tool to control the brightness.

You can find it here: [https://github.com/udifuchs/icc-brightness](https://github.com/udifuchs/icc-brightness)

### Backlight in Sway

For [sway](https://www.archlinux.org/packages/?name=sway) users you can use [redshift-wlr-gamma-control](https://aur.archlinux.org/packages/redshift-wlr-gamma-control/) to set the brightness. The following command sets the brightness to 75%.

```
redshift -o -b 0.75 -O 6500k -m wayland -l manual

```

This may also work for other window managers based on [wlroots](https://www.archlinux.org/packages/?name=wlroots).

## Networking

### WiFi

With kernel version 5.2.2 and linux-firmware 20190717.bf13a71-1, WiFi would be working out of the box.

With kernel versions lower than 5.2.0, WiFi will not be working out of the box, a manual installation of drivers in is required in order that the hardware can be recognized correctly. Connect to the internet via a cable or via USB tethering, then consult [this page](https://support.killernetworking.com/knowledge-base/killer-ax1650-in-debian-ubuntu-16-04/)

```
$ pacman -S git
$ git clone [https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git](https://git.kernel.org/pub/scm/linux/kernel/git/iwlwifi/backport-iwlwifi.git)
$ cd backport-iwlwifi
$ make defconfig-iwlwifi-public
$ make -j4
$ sudo make install

```

Additionally, you may need to ensure you have the latest iwlwifi firmware:

```
$ sudo git clone [https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git)
$ cd linux-firmware
$ sudo cp iwlwifi-* /lib/firmware/

```

It is basically same with Pacman -Syu and updating the Linux-firmware package, albeit the package version would be newer in the former case. Reboot.

Kernel versions 5.2.0 and 5.2.1 [have issues with getting the WiFi module working](https://bbs.archlinux.org/viewtopic.php?id=247705) . However, according to the same post, removing the file `/lib/firmware/iwlwifi-cc-a0-48.ucode` will help, which keeps the troublesome firmware verision 48 from being loaded and load the version 46 firmware instead.

## Touchpad and Touchscreen

## Docks

## Firmware Update

### UEFI

Firmware images can be found at [Dell support page](https://www.dell.com/support/home/us/en/04/product-support/product/xps-15-7590-laptop/drivers). Keeping an existing Windows system will make updates of BIOS much simpler. If a clean Arch Linux install is the case in order to install:

*   Download the desired firmware from section "Dell XPS 15 7590 System BIOS"
*   Save it in `/efi/EFI/Dell/Bios/` or `/boot/EFI/Dell/Bios/` (this path may vary, depending on your installation)
*   Reboot the system, and enter the boot menu by pressing repeatedly `F12` on Dell logo
*   Choose "Bios Flash Update"
*   Select the file previously saved, and start the process

The process will take about five minutes, during which the system will have some reboots and push fans at maximum speed. Finally the system will reboot normally.

## Tips and Tricks

## Fingerprint reader

It is a Goodix fingerprint reader.

The producer does not provide any Linux driver nor documentation to implement one.

Some effort is in slow progress to reverse engineer the windows drivers (see [[3]](https://gitlab.freedesktop.org/libfprint/libfprint/issues/189)).