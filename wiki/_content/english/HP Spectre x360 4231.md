Arch Linux is currently running successfully on this laptop with only minor issues after certain customization. The screen natively runs at 2560x1440\. Regular console is still ok compared to bricks running at 3200x1800\. Although you should keep in mind Gnome does only support whole numbers as a scaling factor. With this a scaling of 1 is hard to read while a scaling of 2 is for the blind. See tweaks for a work around.

## Contents

*   [1 Hardware info](#Hardware_info)
    *   [1.1 hardware options](#hardware_options)
    *   [1.2 lspci on a 4231](#lspci_on_a_4231)
*   [2 Tweaks](#Tweaks)
    *   [2.1 brightness / backlight](#brightness_.2F_backlight)
    *   [2.2 Gnome scaling](#Gnome_scaling)
    *   [2.3 video driver](#video_driver)
*   [3 Issues](#Issues)
    *   [3.1 Wifi](#Wifi)
    *   [3.2 Bluetooth](#Bluetooth)

### Hardware info

#### hardware options

The HP Spectre x360 is shipped for some years already. While the overall look & feel of the brick hasn't changed, some hardware configuration changed a lot. It is important to keep in mind that the article focuses on the year 2016 model packed with Intel Iris graphics. The main hardware components are

*   Intel i7 Skylake 6560U with Intel Iris 540 graphics (compared to i7 6500 with Intel HD 520 graphics on a 4100)
*   OLED touch screen running at 2560x1440 (compared to LED 1920x1080 on a 4100)
*   500 GB M.2 SDD
*   8 GB RAM

#### lspci on a 4231

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 09)
00:02.0 VGA compatible controller: Intel Corporation Skylake Integrated Graphics (rev 0a)
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.1 PCI bridge: Intel Corporation Device 9d11 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Multimedia audio controller: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)
02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 61)
03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)

```

### Tweaks

#### brightness / backlight

`/sys/class/backlight/intel_backlight` exists but is not working as of kernel 4.6 and 4.7rc6\. Proposed kernel parameters (such as `acpi_os`) do not remedy the issue. It may be helpful to know that OLED displays by their nature do not have backlight. xrandr offers some neat feature to change brightness of your screen. Depending on your driver (modesetting driver included in Xorg or xf86-video-intel, see [Intel graphics](/index.php/Intel_graphics "Intel graphics")) your screen is named eDP-1 or eDP1\. Use `xrandr` to determine the correct name if in doubt. The following statement changes brightness to 50%.

```
$ xrandr --output eDP1 --brightness .5

```

While this may probably work on non-OLED displays as well, it won't reduce power consumption on non-OLED displays at all. Without in-depth tests and measurements done, it seems like lowering brightness from the default 100% to something more regular 50% extends battery life by some hours.
Since the hotkeys are performing updates on `/sys/class/backlight/intel_backlight` you may use `inotify` to enable brightness adjustment using the hotkeys (see [Backlight#sysfs_modified_but_no_brightness_change](/index.php/Backlight#sysfs_modified_but_no_brightness_change "Backlight")). The following script does the job:

```
#!/bin/sh

path=/sys/class/backlight/intel_backlight

luminance() {
    read -r level < "$path"/actual_brightness
    bc <<< "scale=10;$level/$max"
}

read -r max < "$path"/max_brightness
xrandr --output eDP1 --brightness "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    echo $(luminance)
    xrandr --output eDP1 --brightness "$(luminance)"
done

```

The script requires package `bc` to actually calculate the brightness factor. If you store the script at `/usr/share/bin/brightness` (see [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy")), you may use the following file at `~/.config/autostart/brightness.desktop` to run the script at login to gnome:

```
[Desktop Entry]
Name=brightness
GenericName=brightness
Comment=adjust brightness using hotkeys 
Exec=/usr/local/bin/brightness
Terminal=false
Type=Application
X-GNOME-Autostart-enabled=true

```

While all this fixes brightness issues on the brick quite well, there are still some issues to be solved:

*   Chromium and some other programs reset brightness to 100% upon their first start since reboot.
*   Hotkeys aren't working prior to login.

#### Gnome scaling

Gnome by default assumes a scaling factor of 2 since the screen resolution at y-axis is greater than 1200 [[1](https://wiki.gnome.org/HowDoI/HiDpi)]. With this, at first glance all controls are quite over sized. xrandr offers some nice workaround:

```
xrandr --output eDP1 --scale 1.25x1.25

```

#### video driver

### Issues

#### Wifi

#### Bluetooth