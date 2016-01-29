# ASUS N551JM

| **Device** | **Status** | **Modules** |
| Intel | Working | i915 _and_ xf86-video-intel |
| Nvidia | Working | nouveau _or_ nvidia |
| Ethernet | Working | r8168 _or_ r8169 |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working | linux-uvc |
| Card Reader | Working | rtsx_pci |
| Bluetooth | Working | iwlwifi |

[ASUS N551JM](http://www.asus.com/Notebooks_Ultrabooks/N551JM/specifications/) - this article covers hardware specific configuration. All topics covered can be performed after an installation of Arch Linux has been finished and the machine rebooted into it. Also this article could be applicable for the ASUS N551JK model.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop"), for a predecessor with a similar configuration, see [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Video](#Video)
        *   [1.1.1 Display brightness](#Display_brightness)
    *   [1.2 Audio](#Audio)
    *   [1.3 Keyboard](#Keyboard)
        *   [1.3.1 Brightness](#Brightness)
    *   [1.4 Touchpad](#Touchpad)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 nouveau problems](#nouveau_problems)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 bbswitch](#bbswitch)
    *   [3.2 Touchpad switch](#Touchpad_switch)
    *   [3.3 Special keys for window managers](#Special_keys_for_window_managers)

## Configuration

### Video

Integrated Intel graphics works out of the box. For the hybrid graphics configuration, see [Bumblebee](/index.php/Bumblebee "Bumblebee").

You could install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee"). Add the kernel parameter `rcutree.rcu_idle_gp_delay=1` to your bootloader configuration, so that _optirun_ will not fail to start (not necessary with the current stock kernel).

#### Display brightness

`FN+F5` and `FN+F6` will not produce any output (will not work) until you use the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_osi=` to your bootloader. It's indeed followed by a blank space.

It might happen that display brightness adjustment will not work even when the kernel parameter is used. In this case, make sure you are still using kernel parameter `acpi_osi=` and load the `asus_nb_wmi` module with the following command:

```
# modprobe asus_nb_wmi

```

### Audio

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

To enable the internal microphone and the external subwoofer support, install [asus-n551-hda-fix](https://aur.archlinux.org/packages/asus-n551-hda-fix/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). This package installs the [pincfg patch](https://bugs.launchpad.net/ubuntu/+source/alsa-tools/+bug/1405691), and also enables the internal microphone by adding the _asus-mode8_ to the HDA driver options.

After installation, reboot the laptop to ensure all modules are loaded. Check if the fallback device is correctly set to _Build-in Audio Analog Stereo_ with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol). See [PulseAudio/Troubleshooting#Fallback device is not respected](/index.php/PulseAudio/Troubleshooting#Fallback_device_is_not_respected "PulseAudio/Troubleshooting") for more information. Also check for muted devices:

```
$ alsamixer -c PCH

```

**Note:** [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) provides `alsamixer` and `amixer` shell programs.

### Keyboard

Keyboard support is provided out of the box.

#### Brightness

In some cases, `FN+F3` and `FN+F4` might not work out of box with some [desktop environments](/index.php/Desktop_environments "Desktop environments"), so install [asus-kbd-backlight](https://aur.archlinux.org/packages/asus-kbd-backlight/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). Load the module to control hotkeys:

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

### Touchpad

Touchpad works out of the box with the default synaptics drivers. You can tweak its options using the default Xorg configuration files. For example:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 

```
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
	Option "MinSpeed" "1"
	Option "MaxSpeed" "2.5"

	Option "TapButton2" "2"
	Option "TapButton3" "0"

	Option "ClickFinger2" "2"
	Option "ClickFinger3" "0"

	Option "VertTwoFingerScroll" "1"
	Option "HorizTwoFingerScroll" "1"

	Option "VertScrollDelta" "60"
	Option "HorizScrollDelta" "60"

	Option "LockedDrags" "on"
	Option "LockedDragTimeout" "400"

	Option "CircularScrolling" "on"
	Option "CircScrollTrigger" "8"
EndSection
```

Rich multitouch gestures can be configured with [Touchegg](/index.php/Touchegg "Touchegg"). To use two-finger or three-finger gestures, you should disable the corresponding features in the Xorg config:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 

```
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"

        # ...

        # Two-finger gestures
	Option "TapButton2" "0"
	Option "ClickFinger2" "0"

        # Three-finger gestures
	Option "TapButton3" "0"
	Option "ClickFinger3" "0"

        # ...
EndSection
```

## Troubleshooting

### nouveau problems

Sometimes _nouveau_ driver produces a lot of garbage log lines during boot and even causes a kernel panic. This is a bug in the driver. You can workaround this by disabling _nouveau_:

 `/etc/modprobe.d/blacklist-nouveau.conf`  `blacklist nouveau` 

At the same time, you can install a proprietary [nvidia](https://www.archlinux.org/packages/?name=nvidia) dirver.

## Tips and tricks

### bbswitch

If you are using [Bumblebee](/index.php/Bumblebee "Bumblebee"), you can install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) package to manipulate the dedicated graphics card state. You can also [change the default state of the dedicated graphics card](/index.php/Bumblebee#Default_power_state_of_NVIDIA_card_using_bbswitch "Bumblebee").

### Touchpad switch

The touchpad can be toggled using a `xinput` [script](/index.php/Touchpad_Synaptics#Software_toggle "Touchpad Synaptics").

### Special keys for window managers

If you prefer using a [Window manager](/index.php/Window_manager "Window manager") rather than a [Desktop environment](/index.php/Desktop_environment "Desktop environment"), most settings will not work out of the box, so you might need to manually bind every single `FN` button combination. How to bind, see [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

You can see the list of the media keys here: [ASUS N550JV#Special keys for window managers](/index.php/ASUS_N550JV#Special_keys_for_window_managers "ASUS N550JV").

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_N551JM&oldid=390458](https://wiki.archlinux.org/index.php?title=ASUS_N551JM&oldid=390458)"