Razer Blade is Razer's line of gaming laptops. There is currently a 12" model (Razer Blade Stealth), 14" model (Razer Blade), and a 17" model (Razer Blade Pro). Due to the proprietary SBUI trackpad on the 17" model, it will be extremely difficult to get it to work without extensive USB protocol reversing.

## Contents

*   [1 2016 version (Razer Blade & Razer Blade Stealth)](#2016_version_.28Razer_Blade_.26_Razer_Blade_Stealth.29)
    *   [1.1 Touchpad](#Touchpad)
    *   [1.2 Touchscreen](#Touchscreen)
    *   [1.3 Graphics Drivers](#Graphics_Drivers)
    *   [1.4 Hybrid graphics](#Hybrid_graphics)
    *   [1.5 Suspend Loop](#Suspend_Loop)
        *   [1.5.1 GRUB](#GRUB)
    *   [1.6 Tweaking](#Tweaking)
    *   [1.7 Audio](#Audio)
    *   [1.8 Webcam](#Webcam)
    *   [1.9 Keyboard](#Keyboard)
*   [2 2014 version](#2014_version)
    *   [2.1 Problems](#Problems)
    *   [2.2 Possible trackpad solution](#Possible_trackpad_solution)
*   [3 2013 version](#2013_version)
    *   [3.1 What works](#What_works)
    *   [3.2 Problems](#Problems_2)
    *   [3.3 Possible trackpad solution](#Possible_trackpad_solution_2)

# 2016 version (Razer Blade & Razer Blade Stealth)

The normal installation process works in general with the exceptions enumerated below.

## Touchpad

[Install](/index.php/Install "Install") the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package: this is also the only one that will enable natural scrolling. See [Libinput](/index.php/Libinput "Libinput") for more information on this driver.

Alternatively, if you prefer using the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") driver, [install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

If you have issues with the touchpad not working after resuming from sleep, restarting the module i2c_hid seems to work.

## Touchscreen

While the touchscreen will provide basic functionality out of the box, it is best to use [touchegg](https://aur.archlinux.org/packages/touchegg/) to configure multitouch gestures. These include two-finger scrolling, right-click, etc.

## Graphics Drivers

The graphics card works OK with the standard intel drivers which you can [install](/index.php/Install "Install") with the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. See [Intel graphics](/index.php/Intel_graphics "Intel graphics") for more information on installation and configuration.

Issues with screen flickering seem to be resolved by changing *AccelMethod* to *uxa* as described in the [SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics") section.

```
# cat >/etc/X11/xorg.conf.d/20-intel.conf 
Section "Device"
  Identifier  "Intel Graphics"
  Driver      "intel"
  Option      "AccelMethod"  "uxa"
  #Option      "AccelMethod"  "sna"
EndSection

```

If you experience screen tearing while scrolling add the following line to the conf above: `Option "TearFree" "true"` and set the "AccelMethod" to "sna" and comment out "uxa"

If you have an Intel Kaby Lake chip [wikipedia:Kaby_Lake](https://en.wikipedia.org/wiki/Kaby_Lake "wikipedia:Kaby Lake"), and the issue is not fixed with the conf above, add to `i915.enable_rc6=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Hybrid graphics

If the discrete Nvidia GPU is switched off before starting Xorg or Wayland, then the system freezes. The only possible solution is to manually disable/enable the discrete card after starting the graphical session. However there is a ACPI DSDT fix available which fixes this problem. Check the [repository](https://github.com/m4ng0squ4sh/razer_blade_14_2016_acpi_dsdt) for more information.

## Suspend Loop

Suspending (Close laptop lid) does not seem to work with a basic installation. The lid state transitions from "open" to "closed" correctly the first time (and the system suspends), but after resuming from suspend by opening the lid, the lid state does not change back to "open". This results in the laptop entering a suspend loop because systemd monitors the lid state, sees that the lid is closed, and suspends the system.

A [bug](https://bugzilla.kernel.org/show_bug.cgi?id=187271) was filed against the kernel ACPI driver in November 2016\. It contains a fair amount of documentation on the issue along with a workaround which seems to solve the problem.

To work around the issue, add the following to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
button.lid_init_state=open

```

This will instruct the acpi driver to generate an extra open event when waking from suspend which will keep the system up.

You can check that the setting was acknowledged:

```
# cat /sys/module/button/parameters/lid_init_state
open

```

And also view all boot parameters:

```
$ cat /proc/cmdline 
initrd=\initramfs-linux.img ... button.lid_init_state=open

```

### GRUB

For example, to make changes permanent on [GRUB](/index.php/GRUB "GRUB") systems, edit `# /etc/default/grub` and append `button.lid_init_state=open` to the `GRUB_CMDLINE_LINUX_DEFAULT` line. After the change, the line might look like this (mileage may vary depending on the kernel params already set):

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet button.lid_init_state=open"

```

Then automatically re-generate the grub.cfg file with:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

## Tweaking

If you are using [GNOME](/index.php/GNOME "GNOME"), the *gnome-tweak-tool* can be used to adjust the window and font scaling. A font scale of *1.25* puts the font sizes closer to how they are displayed by default in Windows 10.

If you are using an external monitor that is not [HiDPI](/index.php/HiDPI "HiDPI"), you can use *xrandr* to alter the scaling of the external monitor using the instructions for [Multiple Displays](/index.php/HiDPI#Multiple_displays "HiDPI"). You may have better results though running [GNOME](/index.php/GNOME "GNOME") on [Wayland](/index.php/Wayland "Wayland"). When installed, clicking the gear icon in [GDM](/index.php/GDM "GDM") will allow you to select *Gnome On Wayland* and will default to that in the future.

## Audio

On the latest 'KabyLake' Intel CPU, if you also have a dual-boot with Windows, you might experience some audio issues when booting to Windows and restarting on Linux. The problem is no sound from the speakers and some cracking noises on the headphones - especially when using the touchpad -. No official solution has been posted yet, but a quick hack is to completely shut down the computer (so power off, not restart).

## Webcam

Setting the uvcvideo option "quirks=128" appears to let the webcam work at 720p30, thus enabling [Google Hangouts](https://hangouts.google.com) support. [cheese](https://www.archlinux.org/packages/?name=cheese) works after changing resolution to 720p and relaunching. Multiplying the quirk by a power of 2+ further improves video quality to a point. "quirks=512" seems to work best for one user.

 `/etc/modprobe.d/uvcvideo.conf` 
```
## fix issue with built-in webcam
options uvcvideo quirks=512
```

## Keyboard

The [openrazer-meta](https://aur.archlinux.org/packages/openrazer-meta/) package enables backlight control capabilities (including effects) and macro controls. You may use [polychromatic](https://aur.archlinux.org/packages/polychromatic/) or [razercommander-git](https://aur.archlinux.org/packages/razercommander-git/) for a GUI to set the keyboard options.

For more information on OpenRazer, see the [Razer peripherals#OpenRazer](/index.php/Razer_peripherals#OpenRazer "Razer peripherals")

# 2014 version

## Problems

[Source](http://forum.notebookreview.com/razer/751074-2014-razer-blade-14-linux.html)

*   touchpad (multitouch, although this may be a kernel bug that has since been fixed)
*   keys to increase/decrease screen illumination not working
*   keys to increase/decrease keyboard illumination not working

## Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone [https://github.com/aduggan/hid-rmi.git](https://github.com/aduggan/hid-rmi.git) -b rb14 # and then install it
depmod -a

```

Then [install](/index.php/Install "Install") the [synaptics](https://www.archlinux.org/packages/?name=synaptics) package.

Feature still not working: pinch to zoom, 3rd mouse button.

# 2013 version

## What works

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356)

*   Wireless
*   Switchable graphics
*   Bluetooth
*   Keyboard light (HW controlled)
*   UEFI boot
*   Trackpad (only on Linux 4.0+ **without** libinput-based X.Org input driver (xf86-input-libinput) thanks to [Andrew Duggan's work](http://git.kernel.org/cgit/linux/kernel/git/jikos/hid.git/log/drivers/hid/hid-rmi.c?h=for-3.20/rmi)).

## Problems

[Source](http://forum.notebookreview.com/razer/729380-razer-blade-pro-under-linux.html)

*   SwitchBlade UI does not work due to lack of drivers.
*   ~~Trackpad scrolling does not work.~~

## Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a

```

Then [install](/index.php/Install "Install") the [synaptics](https://www.archlinux.org/packages/?name=synaptics) packages.

Feature still not working: pinch to zoom, 3rd mouse button