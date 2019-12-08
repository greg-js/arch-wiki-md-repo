Related articles

*   [Bumblebee](/index.php/Bumblebee "Bumblebee")
*   [Nouveau](/index.php/Nouveau "Nouveau")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun")

[NVIDIA Optimus](https://en.wikipedia.org/wiki/NVIDIA_Optimus "wikipedia:NVIDIA Optimus") is a technology that allows an Intel integrated GPU and discrete NVIDIA GPU to be built into and accessed by a laptop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Available methods](#Available_methods)
*   [2 Use Intel graphics only](#Use_Intel_graphics_only)
*   [3 Use NVIDIA graphics only](#Use_NVIDIA_graphics_only)
    *   [3.1 Display managers](#Display_managers)
        *   [3.1.1 LightDM](#LightDM)
        *   [3.1.2 SDDM](#SDDM)
        *   [3.1.3 GDM](#GDM)
    *   [3.2 Checking 3D](#Checking_3D)
    *   [3.3 Further Information](#Further_Information)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Tearing/Broken VSync](#Tearing/Broken_VSync)
    *   [4.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_(GPU_fallen_off_the_bus_/_RmInitAdapter_failed!))
    *   [4.3 Resolution, screen scan wrong. EDID errors in Xorg.log](#Resolution,_screen_scan_wrong._EDID_errors_in_Xorg.log)
    *   [4.4 Wrong resolution without EDID errors](#Wrong_resolution_without_EDID_errors)
    *   [4.5 Lockup issue (lspci hangs)](#Lockup_issue_(lspci_hangs))
    *   [4.6 No screens found on a laptop/NVIDIA Optimus](#No_screens_found_on_a_laptop/NVIDIA_Optimus)
*   [5 Use switchable graphics](#Use_switchable_graphics)
    *   [5.1 Using PRIME render offload](#Using_PRIME_render_offload)
    *   [5.2 Using nouveau](#Using_nouveau)
    *   [5.3 Using Bumblebee](#Using_Bumblebee)
    *   [5.4 Using nvidia-xrun](#Using_nvidia-xrun)
    *   [5.5 Using optimus-manager](#Using_optimus-manager)
        *   [5.5.1 Installation](#Installation)
        *   [5.5.2 Usage](#Usage)

## Available methods

There are several methods available:

*   [#Use Intel graphics only](#Use_Intel_graphics_only) - saves power, because NVIDIA GPU will be completely powered off.
*   [#Use NVIDIA graphics only](#Use_NVIDIA_graphics_only) - gives more performance than Intel graphics, but drains more battery (which is not welcome for mobile devices). This utilizes the same underlying process as the [optimus-manager](#Using_optimus-manager) and [nvidia-xrun](#Using_nvidia-xrun) options, it should be utilized for troubleshooting and verifying general functionality, before opting for one of the more automated approaches.
*   Using both (use NVIDIA GPU when needed and keep it powered off to save power):
    *   [#Using PRIME render offload](#Using_PRIME_render_offload) - Official method supported by NVIDIA
    *   [#Using optimus-manager](#Using_optimus-manager) - switches graphics with a single command (logout and login required to take effect). It achieves maximum performance out of NVIDIA GPU and switches it off if not in use.
    *   [#Using nvidia-xrun](#Using_nvidia-xrun) - run separate X session on different TTY with NVIDIA graphics. It achieves maximum performance out of NVIDIA GPU and switches it off if not in use.
    *   [#Using Bumblebee](#Using_Bumblebee) - provides Windows-like functionality by allowing to run selected applications with NVIDIA graphics while using Intel graphics for everything else. Has significant performance issues.
    *   [#Using nouveau](#Using_nouveau) - offers poorer performance (compared to the proprietary NVIDIA driver) and may cause issues with sleep and hibernate. Does not work with latest NVIDIA GPUs.

**Note:** All of these options are mutually exclusive, if you test one approach and decide for another, you must ensure to revert any configuration changes done by following one approach before attempting another method, otherwise file conflicts and undefined behaviours may arise.

## Use Intel graphics only

If you only care to use a certain GPU without switching, check the options in your system's BIOS. There should be an option to disable one of the cards. Some laptops only allow disabling of the discrete card, or vice-versa, but it is worth checking if you only plan to use just one of the cards.

If your BIOS does not allow to disable Nvidia graphics, you can disable it from the Linux itself. See [Hybrid graphics#Fully Power Down Discrete GPU](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics").

## Use NVIDIA graphics only

The proprietary NVIDIA driver does not support dynamic switching like the nouveau driver (meaning it can only use the NVIDIA device). It also has notable screen-tearing issues that NVIDIA recognizes but has not fixed, unless you are using x.org > 1.19 and enable prime sync, see [[1]](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/). However, it does allow use of the discrete GPU and has (as of [January 2017](https://www.phoronix.com/scan.php?page=article&item=nouveau-410-blob&num=1)) a marked edge in performance over the nouveau driver.

First, [install](/index.php/Install "Install") the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver and [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr). Then, configure `xorg.conf`. You will need to know the PCI address of the NVIDIA card, which you can find by issuing

```
$ lspci | egrep 'VGA|3D'

```

The PCI address is the first 7 characters of the line that mentions NVIDIA. It will look something like `01:00.0`. In the `xorg.conf`, you will need to format it as `#:#:#` while converting hexadecimal numbers to decimal numbers; e.g. `01:00.0` would be formatted as `1:0:0`.

**Note:** On some setups this setup breaks automatic detection of the values of the display by the nvidia driver through the EDID file. As a work-around see [#Resolution, screen scan wrong. EDID errors in Xorg.log](#Resolution,_screen_scan_wrong._EDID_errors_in_Xorg.log).

If X.Org X server version 1.17.2 or higher is installed ([[2]](http://us.download.nvidia.com/XFree86/Linux-x86/358.16/README/randr14.html))

 `/etc/X11/xorg.conf` 
```
Section "Module"
    Load "modesetting"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:**<BusID for NVIDIA device here>**"
    Option "AllowEmptyInitialConfiguration"
EndSection

```

Next, add the following two lines to the beginning of your `~/.xinitrc`:

 `~/.xinitrc` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

Now reboot to load the drivers, and X should start.

If your display dpi is not correct add the following line:

```
xrandr --dpi 96

```

If you get a black screen when starting X, make sure that there are no ampersands after the two `xrandr` commands in `~/.xinitrc`. If there are ampersands, it seems that the window manager can run before the `xrandr` commands finish executing, leading to a black screen.

### Display managers

If you are using a display manager then you will need to create or edit a display setup script for your display manager instead of using `~/.xinitrc`.

#### LightDM

For the [LightDM](/index.php/LightDM "LightDM") display manager:

 `/etc/lightdm/display_setup.sh` 
```
#!/bin/sh
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

Make the script executable:

```
# chmod +x /etc/lightdm/display_setup.sh

```

Now configure lightdm to run the script by editing the `[Seat:*]` section in `/etc/lightdm/lightdm.conf`:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
display-setup-script=/etc/lightdm/display_setup.sh
```

Now reboot and your display manager should start.

#### SDDM

For the [SDDM](/index.php/SDDM "SDDM") display manager (SDDM is the default DM for [KDE](/index.php/KDE "KDE")):

 `/usr/share/sddm/scripts/Xsetup` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

#### GDM

For the [GDM](/index.php/GDM "GDM") display manager create two new .desktop files:

```
/usr/share/gdm/greeter/autostart/optimus.desktop
/etc/xdg/autostart/optimus.desktop
```

```
[Desktop Entry]
Type=Application
Name=Optimus
Exec=sh -c "xrandr --setprovideroutputsource modesetting NVIDIA-0; xrandr --auto"
NoDisplay=true
X-GNOME-Autostart-Phase=DisplayServer

```

Make sure that GDM use [X as default backend](/index.php/GDM#Use_Xorg_backend "GDM").

### Checking 3D

You can check if the NVIDIA graphics are being used by installing [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) and running

```
$ glxinfo | grep NVIDIA

```

### Further Information

For more information, look at NVIDIA's official page on the topic [[3]](http://us.download.nvidia.com/XFree86/Linux-x86/370.28/README/randr14.html).

## Troubleshooting

### Tearing/Broken VSync

This requires [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.19 or higher, [linux](https://www.archlinux.org/packages/?name=linux) kernel 4.5 or higher, and [nvidia](https://www.archlinux.org/packages/?name=nvidia) 370.23 or higher. Then enable [DRM kernel mode setting](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA"), which will in turn enable the PRIME synchronization and fix the tearing.

You can read the official [forum thread](https://devtalk.nvidia.com/default/topic/957814/linux/prime-and-prime-synchronization/) for details.

It has been [reported](https://bbs.archlinux.org/viewtopic.php?id=251032) that [linux](https://www.archlinux.org/packages/?name=linux) kernel 5.4 breaks PRIME synchronization.

### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

Add `rcutree.rcu_idle_gp_delay=1` to the kernel parameters. Original topic can be found in [[4]](https://github.com/Bumblebee-Project/Bumblebee/issues/455#issuecomment-22497464) and [[5]](https://bbs.archlinux.org/viewtopic.php?id=169742).

### Resolution, screen scan wrong. EDID errors in Xorg.log

This is due to the NVIDIA driver not detecting the EDID for the display. You need to manually specify the path to an EDID file or provide the same information in a similar way.

To provide the path to the EDID file edit the Device Section for the NVIDIA card in Xorg.conf, adding these lines and changing parts to reflect your own system:

 `/etc/X11/xorg.conf` 
```
Section "Device"
       	Option		"ConnectedMonitor" "CRT-0"
       	Option		"CustomEDID" "CRT-0:/sys/class/drm/card0-LVDS-1/edid"
	Option		"IgnoreEDID" "false"
	Option		"UseEDID" "true"
EndSection

```

If Xorg wont start try swapping out all references of CRT to DFB. card0 is the identifier for the intel card to which the display is connected via LVDS. The edid binary is in this directory. If the hardware arrangement is different, the value for CustomEDID might vary but yet this has to be confirmed. The path will start in any case with /sys/class/drm.

Alternatively you can generate your edid with tools like [read-edid](https://www.archlinux.org/packages/?name=read-edid) and point the driver to this file. Even modelines can be used, but then be sure to change "UseEDID" and "IgnoreEDID".

### Wrong resolution without EDID errors

Using *nvidia-xconfig*, incorrect information might be generated in Xorg.conf and in particular wrong monitor refresh rates that restruct the possible resolutions. Try commenting out the `HorizSync`/`VertRefresh` lines. If this helps, you can probably also remove everything else not mentioned in this article.

### Lockup issue (lspci hangs)

Symptoms: lspci hangs, system suspend fails, shutdown hangs, optirun hangs.

Applies to: newer laptops with GTX 965M or alike when bbswitch (e.g. via Bumblebee) or nouveau is in use.

When the dGPU power resource is turned on, it may fail to do so and hang in ACPI code ([kernel bug 156341](https://bugzilla.kernel.org/show_bug.cgi?id=156341)).

When using nouveau, disabling runtime power-management stops it from changing the power state, thus avoiding this issue. To disable runtime power-management, add `nouveau.runpm=0` to the kernel parameters.

For known model-specific workarounds, see [this issue](https://github.com/Bumblebee-Project/Bumblebee/issues/764#issuecomment-234494238). In other cases you can try to boot with `acpi_osi="!Windows 2015"` or `acpi_osi=! acpi_osi="Windows 2009"` added to your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). (Consider reporting your laptop to that issue.)

### No screens found on a laptop/NVIDIA Optimus

Check if `$ lspci | grep VGA` outputs something similar to:

```
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)

```

NVIDIA drivers now offer Optimus support since 319.12 Beta [[6]](http://www.nvidia.com/object/linux-display-amd64-319.12-driver.html) with kernels above and including 3.9.

Another solution is to install the [Intel](/index.php/Intel "Intel") driver to handle the screens, then if you want 3D software you should run them through [Bumblebee](/index.php/Bumblebee "Bumblebee") to tell them to use the NVIDIA card.

## Use switchable graphics

### Using PRIME render offload

This is the official NVIDIA method to support switchable graphics.

See [PRIME#PRIME render offload](/index.php/PRIME#PRIME_render_offload "PRIME") for details.

### Using nouveau

See [PRIME](/index.php/PRIME "PRIME") for graphics switching and [nouveau](/index.php/Nouveau "Nouveau") for open-source NVIDIA driver.

### Using Bumblebee

See [Bumblebee](/index.php/Bumblebee "Bumblebee").

### Using nvidia-xrun

See [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun").

### Using optimus-manager

[Optimus-manager](https://github.com/Askannz/optimus-manager) is one of the easiest solutions for graphics switching between NVIDIA and Intel with a single command. Graphical systray applet is also available.

#### Installation

Install the required [NVIDIA](/index.php/NVIDIA "NVIDIA") driver and [optimus-manager](https://aur.archlinux.org/packages/optimus-manager/). Optionally install [optimus-manager-qt](https://aur.archlinux.org/packages/optimus-manager-qt/) for system tray applet.

Also [start and enable](/index.php/Systemd#Using_units "Systemd") `optimus-manager.service`.

**Note:** By default, optimus-manager only changes which graphics driver is active; it does not automatically turn off the NVIDIA GPU when not in use. To enable power management, see the [upstream guide](https://github.com/Askannz/optimus-manager/wiki/A-guide--to-power-management-options). Configurations that include a Turing architecture (or newer) GPU and an Intel Coffee Lake (or newer) CPU can use power management features built into the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") driver; see [[7]](http://download.nvidia.com/XFree86/Linux-x86_64/435.17/README/dynamicpowermanagement.html) for setup instructions.

#### Usage

**Note:** Switching graphics will log you out automatically. Log in again to use selected graphics.

Use below commands to switch graphics:

```
$ optimus-manager --switch intel    # Use Intel graphics
$ optimus-manager --switch nvidia   # Use NVIDIA graphics
$ optimus-manager --switch hybrid   # Use hybrid graphics (Requires a patch to xorg-server)
$ optimus-manager --switch auto     # Switch to different graphics (from what is used now)

```

Also specify which graphics to use on boot:

```
$ optimus-manager --set-startup intel
$ optimus-manager --set-startup nvidia
$ optimus-manager --switch hybrid   # Use hybrid graphics (Requires a patch to xorg-server)

```

For more information and troubleshooting, see [upstream documentation](https://github.com/Askannz/optimus-manager/blob/master/README.md).