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
            *   [2.1.3.1 Crackling sound](#Crackling_sound)
    *   [2.2 Messages during console login](#Messages_during_console_login)
    *   [2.3 USB devices and sleep](#USB_devices_and_sleep)
        *   [2.3.1 Battery charging issues](#Battery_charging_issues)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Touchpad switch](#Touchpad_switch)
    *   [3.2 Full fan speed](#Full_fan_speed)
    *   [3.3 Disable GPU throotling](#Disable_GPU_throotling)
    *   [3.4 Special keys for window managers](#Special_keys_for_window_managers)

## Configuration

### Video

#### Drivers

Install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee"). Add the kernel parameter `rcutree.rcu_idle_gp_delay=1` to your bootloader configuration, so that *optirun* will not fail to start.

#### Brightness

`FN+F5` and `FN+F6` will not produce any output (will not work) untill you use the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_osi=` to your bootloader. It's indeed followed by a blank space.

### Audio

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

After installation, reboot the laptop to ensure all modules are loaded. Check if the fallback device is correctly set to *Build-in Audio Analog Stereo* with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol). See [PulseAudio/Troubleshooting#Fallback device is not respected](/index.php/PulseAudio/Troubleshooting#Fallback_device_is_not_respected "PulseAudio/Troubleshooting") for more information. Also check for muted devices:

```
$ alsamixer -c PCH

```

**Note:** [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) provides `alsamixer` and `amixer` shell programs.

### Keyboard

#### Brightness

Key mappings `FN+F3` and `FN+F4` might not work out of box with some [desktop environments](/index.php/Desktop_environments "Desktop environments"). To resolve, install [asus-kbd-backlight](https://aur.archlinux.org/packages/asus-kbd-backlight/) and load the module to control hotkeys:

```
# modprobe asus-nb-wmi

```

and [start and enable](/index.php/Enable "Enable") the `asus-kbd-backlight.service`.

Now you can take control over the keyboard backlight:

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

`Media` and `FN+F7` buttons are not mapped correctly. It is not necessary to remap `FN+F7` shortcut, because it works without any additional configuration.

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

Optionally, for `FN+F7` give some value on keycode 253.

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

Test with `xev` or try to bind something on media button. `FN+F7` should be controlled by hardware and switch display without any additional configuration. Also, if you are satisfied, put the command above to [Xinitrc](/index.php/Xinitrc "Xinitrc").

 `~/.xinitrc` 
```
{ sleep 10; xmodmap ~/.Xmodmap; } &

```

### Touchpad

Touchpad might not work as expected out of the box. To resolve, install [Touchpad Synaptics driver](/index.php/Touchpad_Synaptics#Installation "Touchpad Synaptics").

## Troubleshooting

### Audio

##### Dual boot

If you boot your laptop right after Windows to Linux, sound might only work through headphones jack, but not through speakers and subwoofer. The quick fix is to suspend your laptop and resume it back.

##### Bug

The internal speakers seems not to play any sound until volume is being increased significantly. This also occurs on Windows operation system as well as on Linux.

To fix this, please flash BIOS 206 as per description in [#Disable GPU throotling](#Disable_GPU_throotling) section.

#### Sound pops twice during shutdown and sleep

Create new file:

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

and one more:

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

Then [enable](/index.php/Enable "Enable") `beep-disable.service` and `beep-disable-wakeup.service` as root.

##### Crackling sound

Add `tsched=0` to pulseaudio config file as per instructions at [PulseAudio/Troubleshooting#Glitches, skips or crackling](/index.php/PulseAudio/Troubleshooting#Glitches.2C_skips_or_crackling "PulseAudio/Troubleshooting").

### Messages during console login

After booting up, when Linux asks you to enter your login and password, some messages might appear similar to these:

```
Nouveau E[    PBUS][0000:01:00.0] MIMO write of 0x00000002 FAULT at 0x4188ac [ IBUS]
Nouveau E[    DRM] Pointer to TMDS table invalid
Nouveau E[    DRM] Pointer to flat panel table invalid

```

After installing Intel with Nvidia graphics drivers, messages should dissappear.

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

## Tips and tricks

### Touchpad switch

The touchpad can be toggled using a `xinput` [script](/index.php/Touchpad_Synaptics#Software_toggle "Touchpad Synaptics").

### Full fan speed

**Note:** No solution yet how to slow it down. After the reboot everything is fine

This is very helpful if you are about to play a heavy game. Install package [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors), then follow [Lm_sensors#Setup](/index.php/Lm_sensors#Setup "Lm sensors") guide to set up sensors. Once you ready, just before every hard game run the following command:

```
# pwmconfig

```

If prompted, click `y` and after a few seconds you are done. Fan spins at full speed.

### Disable GPU throotling

If you have BIOS 208 installed and tried to play something heavy, you noticed that for a few seconds game runs for 60fps, but most of the time - 20-40fps. GPU performance is being reduced, so temperature can drop down and this is known as GPU throttling. This is strange behavior and even if temperature limit is set to 90c, GPU throttling occurs at 75c or even all the time.

To fix this, flash [bios 206](https://www.asus.com/support/Download/3/529/0/2/dad5aYI8mC6sfoNV/41/). If your BIOS version is newer than this, you must follow [this guide](http://forums.legitreviews.com/viewtopic.php?t=41080), which requires you to have Windows installed to your laptop.

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