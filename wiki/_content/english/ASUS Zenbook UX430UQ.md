[ASUS Zenbook UX430UQ](https://www.asus.com/us/Laptops/ASUS-ZenBook-UX430UQ/) - this article covers hardware specific configuration. All topics covered can be performed after an installation of Arch Linux has been finished and the machine rebooted into it.

For general instructions see [Laptop](/index.php/Laptop "Laptop") and comparable models from the summary page [Laptop/Asus](/index.php/Laptop/Asus "Laptop/Asus") and [Category:ASUS](/index.php/Category:ASUS "Category:ASUS").

## Contents

*   [1 Video](#Video)
*   [2 Audio](#Audio)
*   [3 Keyboard backlight](#Keyboard_backlight)
*   [4 Touchpad](#Touchpad)
*   [5 Fan](#Fan)
*   [6 Battery & performance](#Battery_.26_performance)
*   [7 TSC_DEADLINE message during boot](#TSC_DEADLINE_message_during_boot)

## Video

Install [bumblebee along with Nvidia and Intel drivers](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee").

**Note:** Nvidia GPU does not work after laptop is suspended and waked up. Temporary fix is to reboot system. Permanent fix is unknown.

## Audio

Install [PulseAudio](/index.php/PulseAudio "PulseAudio").

After installation, reboot the laptop to ensure all modules are loaded. Check if the fallback device is correctly set to *Build-in Audio Analog Stereo* with [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol). See [PulseAudio/Troubleshooting#Fallback device is not respected](/index.php/PulseAudio/Troubleshooting#Fallback_device_is_not_respected "PulseAudio/Troubleshooting") for more information. Also check for muted devices:

```
$ alsamixer -c PCH

```

**Note:** [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) provides `alsamixer` and `amixer` shell programs.

## Keyboard backlight

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

## Touchpad

See [libinput](/index.php/Libinput "Libinput").

## Fan

See [Fan_speed_control](/index.php/Fan_speed_control "Fan speed control"). There is a single fan in this notebook, designed to cool down both CPU and GPU. On both Windows and Linux it spins all the time, even if CPU is not in use after long time. None of methods in [Fan_speed_control#Asus_laptops](/index.php/Fan_speed_control#Asus_laptops "Fan speed control") helps, but [Fan_speed_control#NBFC](/index.php/Fan_speed_control#NBFC "Fan speed control") works fantastically (if you face any issues, ensure you update your BIOS).

**Tip:** There is no [NBFC](https://github.com/hirschmann/nbfc/tree/master/Configs) profile for this laptop, but **Asus Zenbook UX410UQ** works perfectly.

## Battery & performance

As advertised by Asus, this laptop's battery lasts up to 9 hours on battery. On Linux, it is likely to last the way shorter, but with some tweaks you can go beyond 9 hours on battery:

*   [ASUS_Zenbook_UX430UQ#Fan](/index.php/ASUS_Zenbook_UX430UQ#Fan "ASUS Zenbook UX430UQ") - Fan is completely stopped when CPU is not in use or in low workload.
*   [Power_management](/index.php/Power_management "Power management") - General power management tweaks.
*   [Improving_performance#Watchdogs](/index.php/Improving_performance#Watchdogs "Improving performance") - Watchdogs are not needed for non-server, especially portable devices like this.

It is also worth noting that [Btrfs](/index.php/Btrfs "Btrfs") file system with LZO compression algorithm increases read/write performance, but also "increases" your SSD space. Also 7th generation Intel processors have high performance of ZLIB compression/decompression, so using this algorithm is likely to save even more space on SSD while keeping nearly the same performance as LZO.

## TSC_DEADLINE message during boot

During boot you might notice message `TSC_DEADLINE disabled due to Erra...`. See [Intel microcode](/index.php/Microcode "Microcode") for solution.