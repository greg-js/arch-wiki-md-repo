Related articles

*   [Razer_peripherals](/index.php/Razer_peripherals "Razer peripherals")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")

Razer Blade is Razer's line of gaming laptops. There is currently a 12" model (Razer Blade Stealth), 14" model (Razer Blade), and a 17" model (Razer Blade Pro). Due to the proprietary SBUI trackpad on the 17" model, it will be extremely difficult to get it to work without extensive USB protocol reversing.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Touchpad](#Touchpad)
    *   [1.2 Touchscreen](#Touchscreen)
    *   [1.3 Graphics Drivers](#Graphics_Drivers)
    *   [1.4 Hybrid graphics](#Hybrid_graphics)
*   [2 Known issues](#Known_issues)
    *   [2.1 2013 version problems](#2013_version_problems)
    *   [2.2 Audio](#Audio)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Tweaking](#Tweaking)
    *   [3.2 Power management](#Power_management)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 2014 model issues](#2014_model_issues)
        *   [4.1.1 Possible trackpad solution](#Possible_trackpad_solution)
    *   [4.2 Webcam](#Webcam)
    *   [4.3 Keyboard](#Keyboard)
    *   [4.4 Infinite suspend loop](#Infinite_suspend_loop)
    *   [4.5 Suspend Loop](#Suspend_Loop)
    *   [4.6 Suspending](#Suspending)
    *   [4.7 Suspending stall issue](#Suspending_stall_issue)
    *   [4.8 Screen flickering / distorted / noise on 2017 stealth](#Screen_flickering_/_distorted_/_noise_on_2017_stealth)
        *   [4.8.1 Option 1: Change edp_vswing=2](#Option_1:_Change_edp_vswing=2)
        *   [4.8.2 Option 2: Use LTS Kernel With enable_rc6=0](#Option_2:_Use_LTS_Kernel_With_enable_rc6=0)
        *   [4.8.3 Option 3: Use intel_idle.max_cstate=1](#Option_3:_Use_intel_idle.max_cstate=1)
    *   [4.9 Possible trackpad solution for 2013 version](#Possible_trackpad_solution_for_2013_version)
    *   [4.10 pcieport PCIe Bus Error](#pcieport_PCIe_Bus_Error)
*   [5 2013 version](#2013_version)
    *   [5.1 What works](#What_works)
*   [6 See also](#See_also)

## Installation

Before uninstalling windows make sure to update the bios. It is easier to install the Razer drivers with windows. You can find updates on the [support page](https://support.razer.com/gaming-laptops/filter/family/0/type/laptops%7C) related to your model.

If you are for some reason unable to boot into windows to perform the update, there is still a [patch](https://github.com/jbdrthapa/razerblade15/blob/master/razerfiles/touchpad/translation_fix/pinctrl-intel-translation-fix.patch) that you an apply to your kernel build to get things working. However, this will unlikely be maintained due to the availability of the BIOS patch.

The normal installation process works in general with the exceptions enumerated below.

### Touchpad

[Install](/index.php/Install "Install") the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package: this is also the only one that will enable natural scrolling. See [Libinput](/index.php/Libinput "Libinput") for more information on this driver.

Alternatively, if you prefer using the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") driver, [install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

If you have issues with the touchpad not working after resuming from sleep, restarting the module i2c_hid seems to work.

In the 2013 version the touchpad works only on Linux 4.0+ **without** libinput-based X.Org input driver (xf86-input-libinput) thanks to [Andrew Duggan's work](http://git.kernel.org/cgit/linux/kernel/git/jikos/hid.git/log/drivers/hid/hid-rmi.c?h=for-3.20/rmi).

In the 2018 version the touchpad works with the vanilla kernel with [BIOS version 1.05](https://dl.razer.com/drivers/BladeC1/Razer%20Blade%2015%20%282018%29%20BIOS%20update%20v1.05.pdf).

In the 2019 version the touchpad works with the vanilla kernel and BIOS version 1.02.

### Touchscreen

While the touchscreen will provide basic functionality out of the box, it is best to use [touchegg](https://aur.archlinux.org/packages/touchegg/) to configure multitouch gestures. These include two-finger scrolling, right-click, etc.

### Graphics Drivers

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

### Hybrid graphics

If the discrete Nvidia GPU is switched off before starting Xorg or Wayland, then the system freezes. The only possible solution is to manually disable/enable the discrete card after starting the graphical session. However there is a ACPI DSDT fix available which fixes this problem. Check the [repository](https://github.com/m4ng0squ4sh/razer_blade_14_2016_acpi_dsdt) for more information.

## Known issues

The trackpad does not work with certain bios versions.

### 2013 version problems

[Source](http://forum.notebookreview.com/razer/729380-razer-blade-pro-under-linux.html)

*   SwitchBlade UI does not work due to lack of drivers.
*   ~~Trackpad scrolling does not work.~~

### Audio

On the latest 'KabyLake' Intel CPU, if you also have a dual-boot with Windows, you might experience some audio issues when booting to Windows and restarting on Linux. The problem is no sound from the speakers and some cracking noises on the headphones - especially when using the touchpad -. No official solution has been posted yet, but a quick hack is to completely shut down the computer (so power off, not restart).

## Tips and tricks

### Tweaking

If you are using [GNOME](/index.php/GNOME "GNOME"), the *gnome-tweak-tool* can be used to adjust the window and font scaling. A font scale of *1.25* puts the font sizes closer to how they are displayed by default in Windows 10.

If you are using an external monitor that is not [HiDPI](/index.php/HiDPI "HiDPI"), you can use *xrandr* to alter the scaling of the external monitor using the instructions for [Multiple Displays](/index.php/HiDPI#Multiple_displays "HiDPI"). You may have better results though running [GNOME](/index.php/GNOME "GNOME") on [Wayland](/index.php/Wayland "Wayland"). When installed, clicking the gear icon in [GDM](/index.php/GDM "GDM") will allow you to select *Gnome On Wayland* and will default to that in the future.

### Power management

[Configuration option 1](https://github.com/Askannz/optimus-manager/wiki/A-guide--to-power-management-options) is compatible if you use [optimus manager](/index.php/NVIDIA_Optimus#Using_optimus-manager "NVIDIA Optimus") to switch between intel and nvidia drivers.

## Troubleshooting

### 2014 model issues

[Source](http://forum.notebookreview.com/razer/751074-2014-razer-blade-14-linux.html)

*   touchpad (multitouch, although this may be a kernel bug that has since been fixed)
*   keys to increase/decrease screen illumination not working
*   keys to increase/decrease keyboard illumination not working

#### Possible trackpad solution

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone [https://github.com/aduggan/hid-rmi.git](https://github.com/aduggan/hid-rmi.git) -b rb14 # and then install it
depmod -a

```

Then [install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package.

Feature still not working: pinch to zoom, 3rd mouse button.

### Webcam

Setting the uvcvideo option "quirks=128" appears to let the webcam work at 720p30, thus enabling [Google Hangouts](https://hangouts.google.com) support. [cheese](https://www.archlinux.org/packages/?name=cheese) works after changing resolution to 720p and relaunching. Multiplying the quirk by a power of 2+ further improves video quality to a point. "quirks=512" seems to work best for one user.

 `/etc/modprobe.d/uvcvideo.conf` 
```
## fix issue with built-in webcam
options uvcvideo quirks=512
```

### Keyboard

The [openrazer-meta](https://aur.archlinux.org/packages/openrazer-meta/) package enables backlight control capabilities (including effects) and macro controls. You may use [polychromatic](https://aur.archlinux.org/packages/polychromatic/) or [razercommander-git](https://aur.archlinux.org/packages/razercommander-git/) for a GUI to set the keyboard options.

For more information on OpenRazer, see the [Razer peripherals#OpenRazer](/index.php/Razer_peripherals#OpenRazer "Razer peripherals")

### Infinite suspend loop

Add the following kernel param:

```
button.lid_init_state=open

```

to fix the suspend-resume-loop after closing the lid the first time after boot.

### Suspend Loop

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

### Suspending

Some users are reporting the laptop immediately waking up after suspending. It appears to be XHC (USB 3.0 chip) that is causing the wakeups.

You can fix this by running

```
   echo XHC | sudo tee /proc/acpi/wakeup

```

This will not persist on a restart though. To run this command on every startup, see [Systemd#Writing unit files](/index.php/Systemd#Writing_unit_files "Systemd").

### Suspending stall issue

If you have suspending stall issue, try to add a new file in `/etc/modprobe.d/` with the following contents:

```
blacklist i2c_nvidia_gpu

```

If you have an infinite suspend loop after the first time you close laptop's lid then try adding `button.lid_init_state=open` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1738818#p1738818)

### Screen flickering / distorted / noise on 2017 stealth

#### Option 1: Change edp_vswing=2

Add the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"):

```
i915.edp_vswing=2

```

Other fixes (changing xf86-video-intel settings like DRI and AccelMode do not seem to help)

#### Option 2: Use LTS Kernel With enable_rc6=0

If the above does not work try adding the following kernel param instead:

```
i915.enable_rc6=0

```

The parameter is not available in the latest kernels (e.g. "4.17.5-1") but the linux-lts kernel does (e.g. "4.14.54-1-lts"). This was the only thing I found that worked on my Razer Blade Stealth 13 with i7-8550U cpu.

#### Option 3: Use intel_idle.max_cstate=1

Instead of reverting to the LTS release, I was able to add the following kernel parameter:

```
intel_idle.max_cstate=1

```

This changes the power options for the kernel. This will increase power usage, as it keeps the processor on all the time. More information can be found here: [https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7](https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7) . I did not try any other cstates. It may be worth setting max_cstate as high as possible to reduce power usage. I have tested from 8 downward and the first one to work was "intel_idle.max_cstate=4"

### Possible trackpad solution for 2013 version

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356&p=2)

```
git clone https://github.com/aduggan/hid-rmi.git -b rb14 # and then install it
depmod -a

```

Then [install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) packages.

Feature still not working: pinch to zoom, 3rd mouse button

### pcieport PCIe Bus Error

You may see the following errors in dmesg:

```
kernel: pcieport 0000:00:1c.0: PCIe Bus Error: severity=Corrected, type=Data Link Layer, id=00e0(Transmitter ID)
kernel: pcieport 0000:00:1c.0:   device [8086:9d12] error status/mask=00001000/00002000
kernel: pcieport 0000:00:1c.0:    [12] Replay Timer Timeout

```

To fix this, add kernel param:

```
pci=nomsi

```

## 2013 version

### What works

[Source](https://bbs.archlinux.org/viewtopic.php?id=173356)

*   Wireless
*   Switchable graphics
*   Bluetooth
*   Keyboard light (HW controlled)
*   UEFI boot

## See also

*   [Wikipedia:List of Razer products#Laptops](https://en.wikipedia.org/wiki/List_of_Razer_products#Laptops "wikipedia:List of Razer products")
*   [The Linux Corner on Razer Insider](https://insider.razer.com/index.php?forums/linux/%7C)
*   [Systems Drivers](http://drivers.razersupport.com//index.php?_m=downloads&_a=view&parentcategoryid=350&nav=0%7CRazer)
*   [laptop support](https://support.razer.com/gaming-laptops/filter/family/0/type/laptops%7CRazer)