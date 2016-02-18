Иногда возникают проблемы с яркостью. На многих машинах уже нет физического переключателя, а вместо него используются программные решения, которые не всегда работают как положено. Найдите работающий способ для вашего оборудования! Слишком яркие экраны могут привести к потере зрения!

There are many ways to adjust the screen backlight of a monitor, laptop or integrated panel (such as the iMac) using software, but depending on hardware and model, sometimes only some options are available. This article aims to summarize all possible ways to adjust the backlight.

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [2 ACPI](#ACPI)
    *   [2.1 Kernel command-line options](#Kernel_command-line_options)
    *   [2.2 Udev rule](#Udev_rule)
*   [3 Switching off the backlight](#Switching_off_the_backlight)
*   [4 systemd-backlight service](#systemd-backlight_service)
*   [5 Backlight utilities](#Backlight_utilities)
    *   [5.1 xbacklight](#xbacklight)
    *   [5.2 xcalib](#xcalib)
    *   [5.3 redshift](#redshift)
    *   [5.4 relight](#relight)
    *   [5.5 setpci (use with great care)](#setpci_.28use_with_great_care.29)
    *   [5.6 Calise](#Calise)
    *   [5.7 brightd](#brightd)
*   [6 KDE](#KDE)
*   [7 NVIDIA settings](#NVIDIA_settings)
*   [8 Backlight PWM modulation frequency (Intel i915 only)](#Backlight_PWM_modulation_frequency_.28Intel_i915_only.29)

## Обзор

Существует несколько способов контролировать яркость. В соответствии с этим обуждением [[1]](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/397617) и этой wiki страницей [[2]](https://wiki.ubuntu.com/Kernel/Debugging/Backlight), способы контроля делятся на следующие категории:

*   яркость управляется горячей клавишей, определённой производителем и нет интерфейса для того, чтобы ОС могла настраивать яркость
*   яркость управляется операционной системой:
    *   яркость можно контролировать через ACPI
    *   яркость можно контролировать через графический драйвер

All methods are exposed to the user through `/sys/class/backlight` and xrandr/xbacklight can choose one method to control brightness. It is still not very clear which one xbacklight prefers by default. *See [FS#27677](https://bugs.archlinux.org/task/27677) for xbacklight, if you get "No outputs have backlight property."* There is a temporary fix if xrandr/xbacklight does not choose the right directory in `/sys/class/backlight`: You can specify the one you want in xorg.conf by setting the "Backlight" option of the Device section to the name of that directory (see [https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741) at the bottom of the page for details).

*   brightness is controlled by HW register through setpci

## ACPI

The brightness of the screen backlight is adjusted by setting the power level of the backlight LEDs or cathodes. The power level can often be controlled using the ACPI kernel module for video. An interface to this module is provided via a folder in the sysfs at `/sys/class/backlight`.

The name of the folder depends on the graphics card model.

 `# ls /sys/class/backlight/` 
```
intel_backlight

```

This particular backlight is managed by an Intel graphics card. It is called `acpi_video0` on an ATI card. In the following example, acpi_video0 is used.

The directory contains the following files and folders:

```
actual_brightness  brightness         max_brightness     subsystem/    uevent             
bl_power           device/            power/             type

```

The maximum brightness can be found by reading from `max_brightness`, which is often 15.

 `/sys/class/backlight/acpi_video0/max_brightness` 
```
15

```

The brightness can be set by writing a number to `brightness`. It is not possible to go any higher than the maximum brightness.

```
# tee /sys/class/backlight/acpi_video0/brightness <<< 5

```

### Kernel command-line options

Sometimes, ACPI does not work well due to different motherboard implementations and ACPI quirks. This includes some laptops with dual graphics (e.g. Nvidia/Radeon dedicated GPU with Intel/AMD integrated GPU). On Nvidia Optimus laptops, the kernel parameter nomodeset can interfere with the ability to adjust the backlight. Additionally, ACPI sometimes register its own `acpi_video0` backlight even if one already exists (such as `intel_backlight`), which results in non working backlight keys. You can try adding the following kernel parameters in your [bootloader](/index.php/Bootloader "Bootloader") to stop ACPI from registering its own backlight interface if one already exists:

```
video.use_native_backlight=1

```

This is the default as of [linux](https://www.archlinux.org/packages/?name=linux) 3.16\. If that does not work, you can try to adjust the list of supported OS interfaces:

```
acpi_osi="!Windows 2012"

```

**Tip:** On an Asus notebooks you might also need to do: `# modprobe asus-nb-wmi` 

**Note:** Disabling legacy boot on Dell XPS13 breaks backlight support.

### Udev rule

If the ACPI interface is available, the backlight level can be set at boot using a udev rule.

 `/etc/udev/rules.d/81-backlight.rules` 
```
# Set backlight level to 8
SUBSYSTEM=="backlight", ACTION=="add", KERNEL=="acpi_video0", ATTR{brightness}="8"
```

The systemd-backlight service restores the previous backlight brightness level at boot, whereas this rule sets it to a fixed value. If you want to use this rule, it is necessary to mask the system-backlight service, as explained in [#systemd-backlight service](#systemd-backlight_service).

## Switching off the backlight

Switching off the backlight (for example when one locks the notebook) can be useful to conserve battery energy. Ideally the following command inside of a graphical session should work:

```
sleep 1 && xset dpms force off

```

The backlight should switch on again on mouse movement or keyboard input. If the previous command does not work, there is a chance that `vbetool` works. Note, however, that in this case the backlight must be manually activated again. The command is as follows:

```
vbetool dpms off

```

To activate the backlight again:

```
vbetool dpms on

```

For example, this can be put to use when closing the notebook lid as outlined in the entry for [Acipd](/index.php/Acpid#Laptop_Monitor_Power_Off "Acpid").

## systemd-backlight service

The [systemd](/index.php/Systemd "Systemd") package includes the service systemd-backlight@.service, which is enabled by default and "static". It saves the backlight brightness level at shutdown and restores it at boot. The service uses the ACPI method described in [Backlight#ACPI](/index.php/Backlight#ACPI "Backlight"), generating services for each folder found in `/sys/class/backlight/`. For example, if there is a folder named `acpi_video0`, it generates a service called `systemd-backlight@backlight:acpi_video0.service`. When using other methods of setting the backlight at boot, it is recommended to mask the service systemd-backlight@.service.

## Backlight utilities

### xbacklight

You can adjust the backlight through the xorg-server command `xbacklight`. The utility is provided by the [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) package in [extra].

A useful demonstration was posted by [gotbletu on YouTube](http://www.youtube.com/watch?v=_pi3iKMAJcY). He suggests the following commands to adjust the backlight:

*   brighten up:

```
xbacklight -inc 40

```

*   dim down:

```
xbacklight -dec 40

```

**Tip:** These commands can be bound to keyboard keys as described in [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

### xcalib

The package [xcalib](https://aur.archlinux.org/packages/xcalib/) ([upstream url](http://xcalib.sourceforge.net/)) is available in the [AUR](/index.php/AUR "AUR") and can be used to dim the screen. Again, the user gotbletu posted a demonstration on [Youtube](http://www.youtube.com/watch?v=A9xsvntT6i4). This program can correct gamma, invert colors and reduce contrast, the latter of which we use in this case:

*   dim down:

```
xcalib -co 40 -a

```

This program uses ICC technology to interact with X11 and while the screen is dimmed, you may find that the mouse cursor is just as bright as before.

### redshift

The program [Redshift](/index.php/Redshift_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Redshift (Русский)") in the official repositories uses `randr` to adjust the screen brightness depending on the time of day and your geographic position. It can also do RGB gamma corrections and set color temperatures. As with `xcalib`, this is very much a software solution and the look of the mouse cursor is unaffected. To execute a single quick adjustment of the brightness, try something like this:

```
redshift -o -l 0:0 -b 0.8 -t 6500:6500

```

**Tip:** If your longitude is west or your latitude is south, you should input it as negative.

Example for Berkeley, CA:

```
redshift-gtk -l 37.8717:-122.2728 

```

### relight

[relight](http://xyne.archlinux.ca/projects/relight) is available in [Xyne's repos](http://xyne.archlinux.ca/repos) and as package [relight](https://aur.archlinux.org/packages/relight/) in the [AUR](/index.php/AUR "AUR"). The package provides `relight.service`, a [systemd](/index.php/Systemd "Systemd") service to automatically restore previous backlight settings during reboot along using the ACPI method explained above, and *relight-menu*, a dialog-based menu for selecting and configuring backlights for different screens.

### setpci (use with great care)

It is possible to set the register of the graphic card to adjust the backlight. It means you adjust the backlight by manipulating the hardware directly, which can be risky and generally is not a good idea. Not all of the graphic cards support this method.

When using this method, you need to use `lspci` first to find out where your graphic card is.

```
# setpci -s 00:02.0 F4.B=0

```

### Calise

The software [calise](http://calise.sourceforge.net/wordpress/) can be found in AUR.

*   Stable version: [calise](https://aur.archlinux.org/packages/calise/)
*   Development version: [calise-git](https://aur.archlinux.org/packages/calise-git/)

It basically computes ambient brightness, and set screen's correct backlight, simply making captures from the webcam, for laptop without light sensor. For more information, calise has its own wiki: [Calise wiki](http://calise.sourceforge.net/mediawiki/index.php/Main_Page).

The main features of this program are that it is very precise, very light on resource usage, and with the daemon version (.service file for systemd users available too), it has practically no impact on battery life.

### brightd

Macbook-inspired [brightd](https://aur.archlinux.org/packages/brightd/) automatically dims (but does not put to standby) the screen when there is no user input for some time. A good companion of [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") so that the screen does not blank out in a sudden.

## KDE

[KDE](/index.php/KDE "KDE") users can adjust the backlight via *System Settings > Power Management > Energy Saving*. If you want to set backlight before kdm just put in /usr/share/config/kdm/Xsetup :

```
xbacklight -inc 10

```

## NVIDIA settings

Users of [NVIDIA's proprietary drivers](/index.php/NVIDIA "NVIDIA") users can change display brightness via the nvidia-settings utility under "X Server Color Correction." However, note that this has absolutely nothing to do with backlight (intensity), it merely adjusts the color output. (Reducing brightness this way is a power-inefficient last resort when all other options fail; increasing brightness spoils your color output completely, in a way similar to overexposed photos.)

## Backlight PWM modulation frequency (Intel i915 only)

Laptops with LED backlight are known to have screen flicker sometimes. The reason for this, is that it is hard enough to dim LEDs by limiting direct current flowing through. It is easier to control brightness by switching LEDs on and off fast enough.

However, frequency of the switching (so-called PWM modulation frequency) is not high enough actually, and some people may notice flicker either explicitly or by feeling headache and eyestrain.

If you have an Intel i915 GPU, then it may be possible to adjust PWM modulation frequency to eliminate flicker.

Install [intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools) from the official repositories. Get value of the register, that determines PWM modulation frequency

 `# intel_reg_read 0xC8254` 
```
0xC8254 : 0x12281228

```

The value returned represents period of PWM modulation. So to increase PWM modulation frequency, value of the register has to be reduced. For example, to double frequency from the previous listing, execute:

```
# intel_reg_write 0xC8254 0x09140914

```

You can use online calculator to calculate desired value [http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html](http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html)

Refer to dedicated topic for details [https://bbs.archlinux.org/viewtopic.php?pid=1245913](https://bbs.archlinux.org/viewtopic.php?pid=1245913)

If you are using the Intel GM45 chipset use address 0x61254 instead of 0xC8254.