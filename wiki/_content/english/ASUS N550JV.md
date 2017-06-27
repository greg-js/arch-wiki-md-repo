| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| Nvidia | Working | nouveau *or* nvidia |
| Ethernet | Working | r8169 |
| Wireless | Working | ath9k |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working | linux-uvc |
| Card Reader | Working | rtsx_usb |
| Bluetooth | Working | btusb |

[ASUS N550JV](http://www.asus.com/Notebooks_Ultrabooks/N550JV/specifications/) - this article covers hardware specific configuration. All topics covered can be performed after an installation of Arch Linux has been finished and the machine rebooted into it.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Video](#Video)
        *   [1.1.1 Drivers](#Drivers)
        *   [1.1.2 Brightness](#Brightness)
    *   [1.2 Audio](#Audio)
    *   [1.3 Keyboard](#Keyboard)
        *   [1.3.1 Brightness](#Brightness_2)
        *   [1.3.2 Incorrectly mapped buttons](#Incorrectly_mapped_buttons)
    *   [1.4 Touchpad](#Touchpad)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Audio](#Audio_2)
        *   [2.1.1 Dual boot](#Dual_boot)
        *   [2.1.2 Bug](#Bug)
        *   [2.1.3 Sound pops twice during shutdown and sleep](#Sound_pops_twice_during_shutdown_and_sleep)
        *   [2.1.4 Crackling sound](#Crackling_sound)
    *   [2.2 Failed to initialize the NVIDIA GPU](#Failed_to_initialize_the_NVIDIA_GPU)
    *   [2.3 Messages during console login](#Messages_during_console_login)
    *   [2.4 USB devices and sleep](#USB_devices_and_sleep)
        *   [2.4.1 Battery charging issues](#Battery_charging_issues)
    *   [2.5 Card reader does not detect cards](#Card_reader_does_not_detect_cards)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Fan control](#Fan_control)
        *   [3.1.1 Dual fan method](#Dual_fan_method)
        *   [3.1.2 Single fan method](#Single_fan_method)
    *   [3.2 Enable full performance of GPU](#Enable_full_performance_of_GPU)
    *   [3.3 Special keys for window managers](#Special_keys_for_window_managers)

## Configuration

### Video

#### Drivers

Install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee").

#### Brightness

In order to be able to adjust the screen brightness using `Fn+F5` and `Fn+F6` you need to set the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_osi= ` (the space is required).

### Audio

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

After installation, reboot the laptop to ensure all modules are loaded. Check if the fallback device is correctly set to *Build-in Audio Analog Stereo* with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol). See [PulseAudio/Troubleshooting#Fallback device is not respected](/index.php/PulseAudio/Troubleshooting#Fallback_device_is_not_respected "PulseAudio/Troubleshooting") for more information. Also check for muted devices:

```
$ alsamixer -c PCH

```

**Note:** [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) provides `alsamixer` and `amixer` shell programs.

### Keyboard

#### Brightness

Key mappings `Fn+F3` and `Fn+F4` should work with most [desktop environments](/index.php/Desktop_environments "Desktop environments") out of the box. If not, install [asus-kbd-backlight](https://aur.archlinux.org/packages/asus-kbd-backlight/), load kernel module `asus-nb-wmi` to control hotkeys, then [start and enable](/index.php/Enable "Enable") the `asus-kbd-backlight.service`.

Now you can control the keyboard backlighting using:

```
$ asus-kbd-backlight up
$ asus-kbd-backlight down
$ asus-kbd-backlight max
$ asus-kbd-backlight off
$ asus-kbd-backlight night
$ asus-kbd-backlight 2
$ asus-kbd-backlight show

```

#### Incorrectly mapped buttons

`Media` and `Fn+F7` buttons are not mapped correctly. It is not necessary to remap `Fn+F7` shortcut, because it works without any additional configuration.

Install [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap), which provides app `xmodmap`. Generate a xmodmap config file if you haven't done it already:

```
$ xmodmap -pke > ~/.Xmodmap

```

Then open it and locate keycode 234:

 `~/.Xmodmap` 
```
...
keycode 233 = XF86MonBrightnessUp NoSymbol XF86MonBrightnessUp
**keycode 234 = XF86AudioMedia NoSymbol XF86AudioMedia**
keycode 235 = XF86Display NoSymbol XF86Display
...

```

Now move `XF86AudioMedia NoSymbol XF86AudioMedia` text on the empty keycode 248 and leave keycode 234 empty:

 `~/.Xmodmap` 
```
...
**keycode 234 =** 
...
...
...
keycode 247 =
**keycode 248 = XF86AudioMedia NoSymbol XF86AudioMedia**
keycode 249 =
...

```

Optionally, for `Fn+F7` give some value on keycode 253.

 `~/.Xmodmap` 
```
...
keycode 252 =
**keycode 253 = XF86Launch0 NoSymbol XF86Launch0**
keycode 254 =
...

```

The next step is apply changes:

```
$ xmodmap ~/.Xmodmap

```

Test with `xev` or try to bind something on media button. `Fn+F7` should be controlled by hardware and switch display without any additional configuration. Also, if you are satisfied, put the command above to [Xinitrc](/index.php/Xinitrc "Xinitrc").

 `~/.xinitrc` 
```
{ sleep 10; xmodmap ~/.Xmodmap; } &

```

### Touchpad

See [libinput](/index.php/Libinput "Libinput"). Unless you are having issues, try [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

## Troubleshooting

### Audio

#### Dual boot

If you boot your laptop right after Windows to Linux, sound might only work through headphones jack, but not through speakers and subwoofer. The quick fix is to suspend your laptop and resume it back.

#### Bug

The internal speakers seems not to play any sound until volume is being increased significantly. This also occurs on Windows operation system as well as on Linux.

#### Sound pops twice during shutdown and sleep

Create and [enable](/index.php/Enable "Enable") the following two services:

 `/etc/systemd/system/beep-disable.service` 
```
[Unit]
Description=Unloads audio module to prevent beep on shutdown
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'rmmod snd_hda_intel'

[Install]
WantedBy=shutdown.target suspend.target

```
 `/etc/systemd/system/beep-disable-wakeup.service` 
```
[Unit]
Description=Load sound module back on system resume
After=suspend.target
Wants=local-system-resume.service
Before=local-system-resume.service

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'modprobe snd_hda_intel'

[Install]
WantedBy=suspend.target

```

#### Crackling sound

Add `tsched=0` to pulseaudio config file as per instructions at [PulseAudio/Troubleshooting#Glitches, skips or crackling](/index.php/PulseAudio/Troubleshooting#Glitches.2C_skips_or_crackling "PulseAudio/Troubleshooting").

### Failed to initialize the NVIDIA GPU

If you receive error similar to this `Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)`, see [here](/index.php/NVIDIA_Optimus#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29 "NVIDIA Optimus").

### Messages during console login

After booting up, when Linux asks you to enter your login and password, some messages might appear similar to these:

```
Nouveau E[    PBUS][0000:01:00.0] MIMO write of 0x00000002 FAULT at 0x4188ac [ IBUS]
Nouveau E[    DRM] Pointer to TMDS table invalid
Nouveau E[    DRM] Pointer to flat panel table invalid

```

To resolve, refer to [#Drivers](#Drivers).

### USB devices and sleep

**Note:** You might experience USB devices (e.g. mouse) are not being turned on immediately after wake up. Current 4.9 kernel (and probably further versions) does not have this issue and below fix might not be required

Hibernate via systemd works out of the box when the swap space or file is correctly identified in the resume kernel parameter. However, even though the system suspends properly it will lock up when resuming. This is due to the USB controller not properly turning off on its own. Create two the following files as shown:

 `/etc/systemd/system/root-suspend.service` 
```
[Unit]
Description=Local system suspend actions
Before=sleep.target

[Service]
Type=oneshot
ExecStart=-/usr/bin/rmmod ehci_pci ; /usr/bin/rmmod ehci_hcd ; /usr/bin/rmmod xhci_pci ; /usr/bin/rmmod xhci_hcd

[Install]
WantedBy=sleep.target
```
 `/etc/systemd/system/root-resume.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target

[Service]
Type=oneshot
ExecStart=/usr/bin/modprobe ehci_hcd ; /usr/bin/modprobe ehci_pci ; /usr/bin/modprobe xhci_hcd ; /usr/bin/modprobe xhci_pci

[Install]
WantedBy=suspend.target

```

Then [enable](/index.php/Enable "Enable") `root-suspend.service` and `root-resume.service` as root.

#### Battery charging issues

This battery in this laptop can only be accessed by removing the bottom of the entire laptop, which requires removing 10 TORX-5 screws. That there appears to be a power issue related to the recharging USB port (the USB port with a lightning bolt) under Linux. When an externally powered device is plugged into the charging USB port and the system is power cycled, the battery indicator will begin flashing orange and the system no longer recognizes or charges the battery. One way to reset the charging circuit is to force shutdown by holding the power button for a few seconds. See [this thread at the Ubuntu forums](http://ubuntuforums.org/showthread.php?t=2176915&page=4&p=13035724#post13035724) for other possible solutions.

### Card reader does not detect cards

Due to unknown reasons, card reader does not detect cards. To resolve this, quickly pull out the card and insert it back for several times (leave inserted afterwards) and after few seconds card will be detected in your system.

## Tips and tricks

### Fan control

**Warning:** Stopping fans on high CPU/GPU load might cause serious damage to your notebook.

Below are the methods, which can be used to control both fans. Generally there are 2 advantages of fans control:

*   Save power (completely stopped fans - notes taking or viewing pictures on battery)
*   Prevent overheating (100% speed of both fans - you can play game longer on max performance until GPU throttling occurs)

#### Dual fan method

**Note:** CPU fan will be controlled by `asus-wmi` and `asus-nb-wmi` modules, therefore blacklisting them prevent FN+X keys from working. However, you don't need to do anything with these modules since `asus_fan` seem to work fine. You might only see false values using `sensors` command (e.g. `asus-isa-0000` will always display 2300 RPM).

Install [asus-fan-dkms-git](https://aur.archlinux.org/packages/asus-fan-dkms-git/). Load kernel module:

```
# modprobe asus_fan

```

**Note:** For unknown reasons this is likely going to fail (no asus_fan module found in your system). [Mkinitcpio#Image_creation_and_activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") and system reboot usually fixes this issue.

Check if you have any control over both fans:

```
# echo 255 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1          # Full CPU fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1            # CPU fan is stopped (Value: 0)
# echo 255 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1          # Full GFX fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1            # GFX fan is stopped (Value: 0)
# echo 2 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1_enable     # Change CPU fan mode to automatic
# echo 1 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1_enable     # Change CPU fan mode to manual
# echo 2 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2_enable     # Change GFX fan mode to automatic
# echo 1 > /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2_enable     # Change GFX fan mode to manual
# cat /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/temp1_input          # Display GFX temperature (will always be 0 when GFX is disabled/unused)

```

If everything works, you might want to load this kernel module on boot:

 `/etc/modules-load.d/asus_fan.conf` 
```
# Load asus_fan module on boot:
asus_fan

```

To be able to use [Fan speed control](/index.php/Fan_speed_control "Fan speed control") script, see [Fan speed control#There are no working fan sensors, all readings are 0](/index.php/Fan_speed_control#There_are_no_working_fan_sensors.2C_all_readings_are_0 "Fan speed control").

Here is a configuration file, which was tested and working fine on the Asus N550JV. However, it might need some tweaking:

 `/etc/fancontrol` 
```
INTERVAL=10
FCTEMPS=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1=/sys/devices/platform/coretemp.0/hwmon/hwmon[[:print:]]*/temp1_input /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/temp1_input
FCFANS=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/fan1_input /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/fan2_input
MINTEMP=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1=50 /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2=45
MAXTEMP=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1=80 /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2=90
MINSTART=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1=40 /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2=40
MINSTOP=/sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm1=10 /sys/devices/platform/asus_fan/hwmon/hwmon[[:print:]]*/pwm2=10

```

#### Single fan method

**Note:** The kernel modules for fan control are `asus-wmi` and `asus-nb-wmi`. Unfortunately, as seen in this [GitHub page](https://github.com/KastB/asus_wmi), you can only control the right side fan (designed for CPU cooling only). Left fan will always be controlled by system and you don't have any controls over it.

Below are the commands to control it (there is no need to replace the wildcard with anything, since the hwmon**X** will change after each boot):

```
# echo 255 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1           # Full fan speed (Value: 255)
# echo 0 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1             # Fan is stopped (Value: 0)
# echo 2 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[[:print:]]*/pwm1_enable     # Change fan mode to automatic
# echo 1 > /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1_enable      # Change fan mode to manual

```

To be able to use [Fan speed control](/index.php/Fan_speed_control "Fan speed control") script, see [Fan speed control#There are no working fan sensors, all readings are 0](/index.php/Fan_speed_control#There_are_no_working_fan_sensors.2C_all_readings_are_0 "Fan speed control").

Here is a configuration file, which was tested to work on the Asus N550JV. It however might need some tweaking:

 `/etc/fancontrol` 
```
INTERVAL=10
FCTEMPS=/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1=/sys/devices/platform/coretemp.0/hwmon/hwmon[[:print:]]*/temp1_input
FCFANS= /sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1=/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/fan1_input
MINTEMP=/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1=50
MAXTEMP=/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1=80
MINSTART=/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1=40
MINSTOP=/sys/devices/platform/asus-nb-wmi/hwmon/hwmon[[:print:]]*/pwm1=10

```

### Enable full performance of GPU

**Note:** This only applicable if you have BIOS 207 or BIOS 208 installed. BIOS 206 and earlier aren't affected.

If you have BIOS 208 or 207 installed and tried to play something heavy, you noticed that for a few seconds game runs for 60fps, but most of the time - 20-40fps. This is strange behavior, which happens on Windows as well as on Linux. Even if the temperature limit is set to 90c, GPU throttling occurs at 75c or even all the time (with a feeling that GPU only runs at 60-70% of it's full potential).

To fix this, flash [bios 206](https://www.asus.com/support/Download/3/529/0/2/dad5aYI8mC6sfoNV/41/). If your BIOS version is newer than this, you must follow [this guide](http://forums.legitreviews.com/viewtopic.php?t=41080), which requires you to have **Windows installed on this laptop**.

**Note:** If you get error while installing WinFlash that this is only supported on Asus notebooks - first you need to install [ATKACPI driver](http://www.asus.com/support/Download/3/588/0/1/41/).

### Special keys for window managers

If you prefer using a [Window manager](/index.php/Window_manager "Window manager") rather than a [Desktop environment](/index.php/Desktop_environment "Desktop environment"), most settings will not work out of the box, so you might need to manually bind every single `FN` button combination. How to bind, see [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

<caption>FN buttons output</caption>
| Buttons | Output |
| Media Button | XF86AudioMedia (xmodmap) |
| FN + F1 | XF86Sleep |
| FN + F2 | XF86WLAN |
| FN + F3 | XF86KbdBrightnessDown |
| FN + F4 | XF86KbdBrightnessUp |
| FN + F5 | XF86MonBrightnessDown |
| FN + F6 | XF86MonBrightnessUp |
| FN + F7 | XF86Launch0 (xmodmap) |
| FN + F8 | XF86Display |
| FN + F9 | XF86TouchpadToggle |
| FN + F10 | XF86AudioMute |
| FN + F11 | XF86AudioLowerVolume |
| FN + F12 | XF86AudioRaiseVolume |
| FN + C | XF86Launch1 |
| FN + V | XF86WebCam |
| FN + Space | XF86Launch6 |
| FN + NumEnter | XF86Calculator |
| FN + Left | XF86AudioPrev |
| FN + Right | XF86AudioNext |
| FN + Up | XF86AudioStop |
| FN + Down | XF86AudioPlay |
| FN + Delete | Insert |