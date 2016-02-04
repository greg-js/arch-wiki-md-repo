# NVIDIA

This article covers installing and configuring [NVIDIA](http://www.nvidia.com)'s _proprietary_ graphic card driver. For information about the open-source drivers, see [Nouveau](/index.php/Nouveau "Nouveau"). If you have a laptop with hybrid Intel/NVIDIA graphics, see [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") instead.

## Contents

*   [1 Installing](#Installing)
    *   [1.1 Unsupported drivers](#Unsupported_drivers)
    *   [1.2 Alternate install: custom kernel](#Alternate_install:_custom_kernel)
        *   [1.2.1 Automatic re-compilation of the NVIDIA module with kernel update](#Automatic_re-compilation_of_the_NVIDIA_module_with_kernel_update)
    *   [1.3 Pure Video HD (VDPAU/VAAPI)](#Pure_Video_HD_.28VDPAU.2FVAAPI.29)
*   [2 Configuring](#Configuring)
    *   [2.1 Minimal configuration](#Minimal_configuration)
    *   [2.2 Automatic configuration](#Automatic_configuration)
    *   [2.3 Multiple monitors](#Multiple_monitors)
        *   [2.3.1 Using NVIDIA Settings](#Using_NVIDIA_Settings)
        *   [2.3.2 ConnectedMonitor](#ConnectedMonitor)
        *   [2.3.3 TwinView](#TwinView)
            *   [2.3.3.1 Manual CLI configuration with xrandr](#Manual_CLI_configuration_with_xrandr)
        *   [2.3.4 Mosaic mode](#Mosaic_mode)
            *   [2.3.4.1 Base Mosaic](#Base_Mosaic)
            *   [2.3.4.2 SLI Mosaic](#SLI_Mosaic)
    *   [2.4 Driver Persistence](#Driver_Persistence)
*   [3 Tweaking](#Tweaking)
    *   [3.1 GUI: nvidia-settings](#GUI:_nvidia-settings)
    *   [3.2 Advanced: 20-nvidia.conf](#Advanced:_20-nvidia.conf)
        *   [3.2.1 Disabling the logo on startup](#Disabling_the_logo_on_startup)
        *   [3.2.2 Overriding monitor detection](#Overriding_monitor_detection)
        *   [3.2.3 Enabling brightness control](#Enabling_brightness_control)
        *   [3.2.4 Enabling SLI](#Enabling_SLI)
        *   [3.2.5 Enabling overclocking](#Enabling_overclocking)
            *   [3.2.5.1 Setting static 2D/3D clocks](#Setting_static_2D.2F3D_clocks)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Fixing terminal resolution](#Fixing_terminal_resolution)
    *   [4.2 Avoid screen tearing in KDE (KWin)](#Avoid_screen_tearing_in_KDE_.28KWin.29)
    *   [4.3 Hardware accelerated video decoding with XvMC](#Hardware_accelerated_video_decoding_with_XvMC)
    *   [4.4 Using TV-out](#Using_TV-out)
    *   [4.5 X with a TV (DFP) as the only display](#X_with_a_TV_.28DFP.29_as_the_only_display)
    *   [4.6 Check the power source](#Check_the_power_source)
    *   [4.7 Listening to ACPI events](#Listening_to_ACPI_events)
    *   [4.8 Displaying GPU temperature in the shell](#Displaying_GPU_temperature_in_the_shell)
        *   [4.8.1 Method 1 - nvidia-settings](#Method_1_-_nvidia-settings)
        *   [4.8.2 Method 2 - nvidia-smi](#Method_2_-_nvidia-smi)
        *   [4.8.3 Method 3 - nvclock](#Method_3_-_nvclock)
    *   [4.9 Set fan speed at login](#Set_fan_speed_at_login)
    *   [4.10 Order of install/deinstall for changing drivers](#Order_of_install.2Fdeinstall_for_changing_drivers)
    *   [4.11 Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers)
    *   [4.12 Avoid tearing with GeForce 500/600/700/900 series cards](#Avoid_tearing_with_GeForce_500.2F600.2F700.2F900_series_cards)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Gaming using TwinView](#Gaming_using_TwinView)
    *   [5.2 Vertical sync using TwinView](#Vertical_sync_using_TwinView)
    *   [5.3 Wayland (gdm) crashes after nvidia-libgl installation](#Wayland_.28gdm.29_crashes_after_nvidia-libgl_installation)
    *   [5.4 Corrupted screen: "Six screens" Problem](#Corrupted_screen:_.22Six_screens.22_Problem)
    *   [5.5 '/dev/nvidia0' input/output error](#.27.2Fdev.2Fnvidia0.27_input.2Foutput_error)
    *   [5.6 '/dev/nvidiactl' errors](#.27.2Fdev.2Fnvidiactl.27_errors)
    *   [5.7 32-bit applications do not start](#32-bit_applications_do_not_start)
    *   [5.8 Errors after updating the kernel](#Errors_after_updating_the_kernel)
    *   [5.9 Crashing in general](#Crashing_in_general)
    *   [5.10 Bad performance after installing a new driver version](#Bad_performance_after_installing_a_new_driver_version)
    *   [5.11 CPU spikes with 400 series cards](#CPU_spikes_with_400_series_cards)
    *   [5.12 Laptops: X hangs on login/out, worked around with Ctrl+Alt+Backspace](#Laptops:_X_hangs_on_login.2Fout.2C_worked_around_with_Ctrl.2BAlt.2BBackspace)
    *   [5.13 No screens found on a laptop/NVIDIA Optimus](#No_screens_found_on_a_laptop.2FNVIDIA_Optimus)
        *   [5.13.1 Possible Workaround](#Possible_Workaround)
    *   [5.14 Screen(s) found, but none have a usable configuration](#Screen.28s.29_found.2C_but_none_have_a_usable_configuration)
    *   [5.15 Blackscreen at X startup / Machine poweroff at X shutdown](#Blackscreen_at_X_startup_.2F_Machine_poweroff_at_X_shutdown)
    *   [5.16 Backlight is not turning off in some occasions](#Backlight_is_not_turning_off_in_some_occasions)
    *   [5.17 Blue tint on videos with Flash](#Blue_tint_on_videos_with_Flash)
    *   [5.18 Bleeding overlay with Flash](#Bleeding_overlay_with_Flash)
    *   [5.19 Full system freeze using Flash](#Full_system_freeze_using_Flash)
    *   [5.20 Xorg fails to load or Red Screen of Death](#Xorg_fails_to_load_or_Red_Screen_of_Death)
    *   [5.21 Black screen on systems with Intel integrated GPU](#Black_screen_on_systems_with_Intel_integrated_GPU)
    *   [5.22 Black screen on systems with VIA integrated GPU](#Black_screen_on_systems_with_VIA_integrated_GPU)
    *   [5.23 X fails with "no screens found" with Intel iGPU](#X_fails_with_.22no_screens_found.22_with_Intel_iGPU)
    *   [5.24 Xorg fails during boot, but otherwise starts fine](#Xorg_fails_during_boot.2C_but_otherwise_starts_fine)
    *   [5.25 Flash video players crashes](#Flash_video_players_crashes)
    *   [5.26 Override EDID](#Override_EDID)
    *   [5.27 Fix rendering lag (firefox, gedit, vim, tmux …)](#Fix_rendering_lag_.28firefox.2C_gedit.2C_vim.2C_tmux_.E2.80.A6.29)
    *   [5.28 Screen Tearing with Multiple Monitor Orientations](#Screen_Tearing_with_Multiple_Monitor_Orientations)
*   [6 See also](#See_also)

## Installing

**Warning:** Avoid installing the NVIDIA driver through the package provided from the NVIDIA website. Installation through [pacman](/index.php/Pacman "Pacman") allows upgrading the driver together with the rest of the system.

These instructions are for those using the stock [linux](https://www.archlinux.org/packages/?name=linux) or [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) packages. For custom kernel setup, skip to the [next](#Alternate_install:_custom_kernel) subsection.

1\. If you do not know what graphics card you have, find out by issuing:

	 `$ lspci -k | grep -A 2 -E "(VGA|3D)"` 

2\. Determine the necessary driver version for your card by:

*   finding the code name (e.g. NV50, NVC0, etc.) on [nouveau wiki's code names page](http://nouveau.freedesktop.org/wiki/CodeNames)
*   looking up the name in NVIDIA's [legacy card list](http://www.nvidia.com/object/IO_32667.html): if your card is not there you can use the latest driver
*   visiting NVIDIA's [driver download site](http://www.nvidia.com/Download/index.aspx)

3\. Install the appropriate driver for your card:

*   For GeForce 400 series cards and newer [NVCx and newer], [install](/index.php/Install "Install") the [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts) package along with [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl).
*   For GeForce 8000/9000, ION and 100-300 series cards [NV5x, NV8x, NV9x and NVAx] from around 2006-2010, [install](/index.php/Install "Install") the [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) or [nvidia-340xx-lts](https://www.archlinux.org/packages/?name=nvidia-340xx-lts) package along with [nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=nvidia-340xx-libgl).
*   For GeForce 6000/7000 series cards [NV4x and NV6x] from around 2004-2006, [install](/index.php/Install "Install") the [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) or [nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts) package along with [nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=nvidia-304xx-libgl).

*   For even older cards, have a look at [#Unsupported drivers](#Unsupported_drivers).
*   For the very latest GPU models, it may be required to [install](/index.php/Install "Install") the [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/) package, since the stable drivers may not support the newly introduced features.

4\. If you are on 64-bit and also need 32-bit OpenGL support, you must also install the equivalent _lib32_ package from the [multilib](/index.php/Multilib "Multilib") repository (e.g. [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl), [lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl) or [lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl)).

5\. Reboot. The [nvidia](https://www.archlinux.org/packages/?name=nvidia) package contains a file which blacklists the _nouveau_ module, so rebooting is necessary.

Once the driver has been installed, continue to [#Configuring](#Configuring).

### Unsupported drivers

If you have a GeForce 5 FX series card or older, Nvidia no longer supports drivers for your card. This means that these drivers [do not support the current Xorg version](http://nvidia.custhelp.com/app/answers/detail/a_id/3142/). It thus might be easier if you use the [nouveau](/index.php/Nouveau "Nouveau") driver, which supports the old cards with the current Xorg.

However, Nvidia's legacy drivers are still available and might provide better 3D performance/stability if you are willing to downgrade Xorg:

*   For GeForce 5 FX series cards [NV30-NV36], install the [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/) package. Last supported Xorg version is 1.15.
*   For GeForce 2/3/4 MX/Ti series cards [NV11, NV17-NV28], install the [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/) package. Last supported Xorg version is 1.12.

**Tip:** The legacy nvidia-96xx-dkms and nvidia-173xx-dkms drivers can also be installed from the unofficial [[city] repository](http://pkgbuild.com/~bgyorgy/city.html). (It is strongly advised that you do not skip any dependencies restriction when installing from here)

### Alternate install: custom kernel

First of all, it is good to know how the ABS works by reading some of the other articles about it:

*   Main article for [ABS](/index.php/ABS "ABS")
*   Article on [makepkg](/index.php/Makepkg "Makepkg")
*   Article on [Creating packages](/index.php/Creating_packages "Creating packages")

The following is a short tutorial for making a custom NVIDIA driver package using [ABS](/index.php/ABS "ABS"):

[Install](/index.php/Install "Install") the [abs](https://www.archlinux.org/packages/?name=abs) package and generate the tree with:

```
# abs

```

As a standard user, make a temporary directory for creating the new package:

```
$ mkdir -p ~/abs

```

Make a copy of the `nvidia` package directory:

```
$ cp -r /var/abs/extra/nvidia/ ~/abs/

```

Go into the temporary `nvidia` build directory:

```
$ cd ~/abs/nvidia

```

It is required to edit the files `nvidia.install` and `PKGBUILD` so that they contain the right kernel version variables.

While running the custom kernel, get the appropriate kernel and local version names:

```
$ uname -r

```

1.  In nvidia.install, replace the `EXTRAMODULES='extramodules-3.4-ARCH'` variable with the custom kernel version, such as `EXTRAMODULES='extramodules-3.4.4'` or `EXTRAMODULES='extramodules-3.4.4-custom'` depending on what the kernel's version is and the local version's text/numbers. Do this for all instances of the version number within this file.
2.  In PKGBUILD, change the `_extramodules=extramodules-3.4-ARCH` variable to match the appropriate version, as above.
3.  If there are multiple kernels installed in parallel (such as a custom kernel alongside the default -ARCH kernel), change the `pkgname=nvidia` variable in the PKGBUILD to a unique identifier, such as nvidia-344 or nvidia-custom. This will allow both kernels to use the nvidia module, since the custom nvidia module has a different package name and will not overwrite the original. You will also need to comment the line in `package()` that blacklists the nouveau module in `/usr/lib/modprobe.d/nvidia.conf` (no need to do it again).

Then do:

```
$ makepkg -ci

```

The `-c` operand tells makepkg to clean left over files after building the package, whereas `-i` specifies that makepkg should automatically run pacman to install the resulting package.

#### Automatic re-compilation of the NVIDIA module with kernel update

This is possible with [DKMS](/index.php/DKMS "DKMS"). Install the [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) package (or a specific branch such as [nvidia-340xx-dkms](https://www.archlinux.org/packages/?name=nvidia-340xx-dkms)) and make sure that the `dkms.service` systemd unit is enabled.

See [Dynamic Kernel Module Support#Usage](/index.php/Dynamic_Kernel_Module_Support#Usage "Dynamic Kernel Module Support") for more information on how to use DKMS.

### Pure Video HD (VDPAU/VAAPI)

At least a video card with second generation [PureVideo HD](https://en.wikipedia.org/wiki/Nvidia_PureVideo#Table_of_GPUs_containing_a_PureVideo_SIP_block "wikipedia:Nvidia PureVideo") is required to use [VDPAU](/index.php/VDPAU "VDPAU") and [VA-API](/index.php/VA-API "VA-API").

## Configuring

It is possible that after installing the driver it may not be needed to create an Xorg server configuration file. You can run [a test](/index.php/Xorg#Running "Xorg") to see if the Xorg server will function correctly without a configuration file. However, it may be required to create a configuration file (prefer `/etc/X11/xorg.conf.d/20-nvidia.conf` over `/etc/X11/xorg.conf`) in order to adjust various settings. This configuration can be generated by the NVIDIA Xorg configuration tool, or it can be created manually. If created manually, it can be a minimal configuration (in the sense that it will only pass the basic options to the [Xorg](/index.php/Xorg "Xorg") server), or it can include a number of settings that can bypass Xorg's auto-discovered or pre-configured options.

**Note:** Since 1.8.x Xorg uses separate configuration files in `/etc/X11/xorg.conf.d/` - check out [advanced configuration](#Advanced:_20-nvidia.conf) section.

### Minimal configuration

A basic configuration block in `20-nvidia.conf` (or deprecated in `xorg.conf`) would look like this:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 

```
Section "Device"
        Identifier "Nvidia Card"
        Driver "nvidia"
        VendorName "NVIDIA Corporation"
        Option "NoLogo" "true"
        #Option "UseEDID" "false"
        #Option "ConnectedMonitor" "DFP"
        # ...
EndSection

```

**Tip:** If upgrading from nouveau make sure to remove "`nouveau`" from `/etc/mkinitcpio.conf`. See [Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers), if switching between the open and proprietary drivers often.

### Automatic configuration

The NVIDIA package includes an automatic configuration tool to create an Xorg server configuration file (`xorg.conf`) and can be run by:

```
# nvidia-xconfig

```

This command will auto-detect and create (or edit, if already present) the `/etc/X11/xorg.conf` configuration according to present hardware.

If there are instances of DRI, ensure they are commented out:

```
#    Load        "dri"

```

Double check your `/etc/X11/xorg.conf` to make sure your default depth, horizontal sync, vertical refresh, and resolutions are acceptable.

**Warning:** That may still not work properly with Xorg-server 1.8

### Multiple monitors

	_See [Multihead](/index.php/Multihead "Multihead") for more general information_

#### Using NVIDIA Settings

You can use the `nvidia-settings` tool provided by [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) to configure your multi-monitor setup. With this method, you will use the proprietary software NVIDIA provides with their drivers. Simply run `nvidia-settings` as root, then configure as you wish, and then save the configuration to `/etc/X11/xorg.conf.d/10-monitor.conf`.

#### ConnectedMonitor

If the driver does not properly detect a second monitor, you can force it to do so with ConnectedMonitor.

 `/etc/X11/xorg.conf` 

```

Section "Monitor"
    Identifier     "Monitor1"
    VendorName     "Panasonic"
    ModelName      "Panasonic MICRON 2100Ex"
    HorizSync       30.0 - 121.0 # this monitor has incorrect EDID, hence Option "UseEDIDFreqs" "false"
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Monitor"
    Identifier     "Monitor2"
    VendorName     "Gateway"
    ModelName      "GatewayVX1120"
    HorizSync       30.0 - 121.0
    VertRefresh     50.0 - 160.0
    Option         "DPMS"
EndSection

Section "Device"
    Identifier     "Device1"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          0
EndSection

Section "Device"
    Identifier     "Device2"
    Driver         "nvidia"
    Option         "NoLogo"
    Option         "UseEDIDFreqs" "false"
    Option         "ConnectedMonitor" "CRT,CRT"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce 6200 LE"
    BusID          "PCI:3:0:0"
    Screen          1
EndSection

```

The duplicated device with `Screen` is how you get X to use two monitors on one card without `TwinView`. Note that `nvidia-settings` will strip out any `ConnectedMonitor` options you have added.

#### TwinView

You want only one big screen instead of two. Set the `TwinView` argument to `1`. This option should be used if you desire compositing. TwinView only works on a per card basis, when all participating monitors are connected to the same card.

```
Option "TwinView" "1"

```

Example configuration:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 

```
Section "ServerLayout"
    Identifier     "TwinLayout"
    Screen         0 "metaScreen" 0 0
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "Card0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"

    #refer to the link below for more information on each of the following options.
    Option         "HorizSync"          "DFP-0: 28-33; DFP-1 28-33"
    Option         "VertRefresh"        "DFP-0: 43-73; DFP-1 43-73"
    Option         "MetaModes"          "1920x1080, 1920x1080"
    Option         "ConnectedMonitor"   "DFP-0, DFP-1"
    Option         "MetaModeOrientation" "DFP-1 LeftOf DFP-0"
EndSection

Section "Screen"
    Identifier     "metaScreen"
    Device         "Card0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "True"
    SubSection "Display"
        Modes          "1920x1080"
    EndSubSection
EndSection

```

[Device option information](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/configtwinview.html).

If you have multiple cards that are SLI capable, it is possible to run more than one monitor attached to separate cards (for example: two cards in SLI with one monitor attached to each). The "MetaModes" option in conjunction with SLI Mosaic mode enables this. Below is a configuration which works for the aforementioned example and runs [GNOME](/index.php/GNOME "GNOME") flawlessly.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 

```
Section "Device"
        Identifier      "Card A"
        Driver          "nvidia"
        BusID           "PCI:1:00:0"
EndSection

Section "Device"
        Identifier      "Card B"
        Driver          "nvidia"
        BusID           "PCI:2:00:0"
EndSection

Section "Monitor"
        Identifier      "Right Monitor"
EndSection

Section "Monitor"
        Identifier      "Left Monitor"
EndSection

Section "Screen"
        Identifier      "Right Screen"
        Device          "Card A"
        Monitor         "Right Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "Screen"
        Identifier      "Left Screen"
        Device          "Card B"
        Monitor         "Left Monitor"
        DefaultDepth    24
        Option          "SLI" "Mosaic"
        Option          "Stereo" "0"
        Option          "BaseMosaic" "True"
        Option          "MetaModes" "GPU-0.DFP-0: 1920x1200+4480+0, GPU-1.DFP-0:1920x1200+0+0"
        SubSection      "Display"
                        Depth           24
        EndSubSection
EndSection

Section "ServerLayout"
        Identifier      "Default"
        Screen 0        "Right Screen" 0 0
        Option          "Xinerama" "0"
EndSection
```

##### Manual CLI configuration with xrandr

If the latest solutions do not work for you, you can use your window manager's _autostart_ implementation with [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

Some `xrandr` examples could be:

```
xrandr --output DVI-I-0 --auto --primary --left-of DVI-I-1

```

or:

```
xrandr --output DVI-I-1 --pos 1440x0 --mode 1440x900 --rate 75.0

```

When:

*   `--output` is used to indicate the "monitor" to which the options are set.
*   `DVI-I-1` is the name of the second monitor.
*   `--pos` is the position of the second monitor relative to the first.
*   `--mode` is the resolution of the second monitor.
*   `--rate` is the refresh rate (in Hz).

#### Mosaic mode

Mosaic mode is the only way to use more than 2 monitors across multiple graphics cards with compositing. Your window manager may or may not recognize the distinction between each monitor.

##### Base Mosaic

Base Mosaic mode works on any set of Geforce 8000 series or higher GPUs. It cannot be enabled from within the nvidia-setting GUI. You must either use the `nvidia-xconfig` command line program or edit `xorg.conf` by hand. Metamodes must be specified. The following is an example for four DFPs in a 2x2 configuration, each running at 1920x1024, with two DFPs connected to two cards:

```
$ nvidia-xconfig --base-mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

**Note:** While the documentation lists a 2x2 configuration of monitors, Nvidia has reduced that ability to just 3 monitors in Base Mosaic mode as of driver version 304\. More monitors are available with a Quadro card, but with standard consumer cards, it is limited to three. The explanation given for this reduction is "Feature parity with the Windows driver". As of September 2014, Windows has no restriction on the number of monitors, even on the same driver version. This is not a bug, this is entirely by design.

##### SLI Mosaic

If you have an SLI configuration and each GPU is a Quadro FX 5800, Quadro Fermi or newer then you can use SLI Mosaic mode. It can be enabled from within the nvidia-settings GUI or from the command line with:

```
$ nvidia-xconfig --sli=Mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

### Driver Persistence

Since version 319, Nvidia has changed the way driver persistence works, it now has a daemon that is to be run at boot. See the [Driver Persistence](http://docs.nvidia.com/deploy/driver-persistence/index.html) section of the Nvidia documentation for more details.

To start the persistence daemon at boot, [enable](/index.php/Enable "Enable") the `nvidia-persistenced.service`. For manual usage see the [upstream documentation](http://docs.nvidia.com/deploy/driver-persistence/index.html#usage).

## Tweaking

### GUI: nvidia-settings

The NVIDIA package includes the `nvidia-settings` program that allows adjustment of several additional settings.

For the settings to be loaded on login, run this command from the terminal:

```
$ nvidia-settings --load-config-only

```

The desktop environment's auto-startup method 'may' not work for loading nvidia-settings properly (KDE). To be sure that settings are really loaded put the command in ~/.xinitrc file (create if not present).

**Tip:** On rare occasions the `~/.nvidia-settings-rc` may become corrupt. If this happens, the Xorg server may crash and the file will have to be deleted to fix the problem.

### Advanced: 20-nvidia.conf

Edit `/etc/X11/xorg.conf.d/20-nvidia.conf`, and add the option to the correct section. The Xorg server will need to be restarted before any changes are applied.

See [NVIDIA Accelerated Linux Graphics Driver README and Installation Guide](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt) for additional details and options.

#### Disabling the logo on startup

Add the `"NoLogo"` option under section `Device`:

```
Option "NoLogo" "1"

```

#### Overriding monitor detection

The `"ConnectedMonitor"` option under section `Device` allows to override monitor detection when X server starts, which may save a significant amount of time at start up. The available options are: `"CRT"` for analog connections, `"DFP"` for digital monitors and `"TV"` for televisions.

The following statement forces the NVIDIA driver to bypass startup checks and recognize the monitor as DFP:

```
Option "ConnectedMonitor" "DFP"

```

**Note:** Use "CRT" for all analog 15 pin VGA connections, even if the display is a flat panel. "DFP" is intended for DVI, HDMI, or DisplayPort digital connections only.

#### Enabling brightness control

Add under section `Device`:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

If brightness control still does not work with this option, try installing [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) or [nvidiabl](https://aur.archlinux.org/packages/nvidiabl/).

#### Enabling SLI

**Warning:** As of May 7, 2011, you may experience sluggish video performance in GNOME 3 after enabling SLI.

Taken from the NVIDIA driver's [README](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) Appendix B: _This option controls the configuration of SLI rendering in supported configurations._ A "supported configuration" is a computer equipped with an SLI-Certified Motherboard and 2 or 3 SLI-Certified GeForce GPUs. See NVIDIA's [SLI Zone](http://www.slizone.com/page/home.html) for more information.

Find the first GPU's PCI Bus ID using `lspci`:

 `$ lspci | grep VGA` 

```
03:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)
05:00.0 VGA compatible controller: nVidia Corporation G92 [GeForce 8800 GTS 512] (rev a2)

```

Add the BusID (3 in the previous example) under section `Device`:

```
BusID "PCI:3:0:0"

```

**Note:** The format is important. The BusID value must be specified as `"PCI:<BusID>:0:0"`

Add the desired SLI rendering mode value under section `Screen`:

```
Option "SLI" "AA"

```

The following table presents the available rendering modes.

| Value | Behavior |
| 0, no, off, false, Single | Use only a single GPU when rendering. |
| 1, yes, on, true, Auto | Enable SLI and allow the driver to automatically select the appropriate rendering mode. |
| AFR | Enable SLI and use the alternate frame rendering mode. |
| SFR | Enable SLI and use the split frame rendering mode. |
| AA | Enable SLI and use SLI antialiasing. Use this in conjunction with full scene antialiasing to improve visual quality. |

Alternatively, you can use the `nvidia-xconfig` utility to insert these changes into `xorg.conf` with a single command:

```
# nvidia-xconfig --busid=PCI:3:0:0 --sli=AA

```

To verify that SLI mode is enabled from a shell:

 `$ nvidia-settings -q all | grep SLIMode` 

```
  Attribute 'SLIMode' (arch:0.0): AA 
    'SLIMode' is a string attribute.
    'SLIMode' is a read-only attribute.
    'SLIMode' can use the following target types: X Screen.

```

**Warning:** After enabling SLI, your system may become frozen/non-responsive upon starting xorg. It is advisable that you disable your display manager before restarting.

#### Enabling overclocking

**Warning:** Please note that overclocking may damage hardware and that no responsibility may be placed on the authors of this page due to any damage to any information technology equipment from operating products out of specifications set by the manufacturer.

Overclocking is controlled via _Coolbits_ option in the `Device` section, which enables various unsupported features:

```
Option "Coolbits" "_value_"

```

**Tip:** The _Coolbits_ option can be easily controlled with the _nvidia-xconfig_, which manipulates the Xorg configuration files: `# nvidia-xconfig --cool-bits=_value_` 

The _Coolbits_ value is the sum of its component bits in the binary numeral system. The component bits are:

*   `1` (bit 0) - Enables overclocking of older (pre-Fermi) cores on the _Clock Frequencies_ page in _nvidia-settings_.
*   `2` (bit 1) - When this bit is set, the driver will "attempt to initialize SLI when using GPUs with different amounts of video memory".
*   `4` (bit 2) - Enables manual configuration of GPU fan speed on the _Thermal Monitor_ page in _nvidia-settings_.
*   `8` (bit 3) - Enables overclocking on the _PowerMizer_ page in _nvidia-settings_. Available since version 337.12 for the Fermi architecture and newer.[[1]](http://www.phoronix.com/scan.php?px=MTY1OTM&page=news_item)
*   `16` (bit 4) - Enables overvoltage using _nvidia-settings_ CLI options. Available since version 346.16 for the Fermi architecture and newer.[[2]](http://www.phoronix.com/scan.php?page=news_item&px=MTg0MDI)

To enable multiple features, add the _Coolbits_ values together. For example, to enable overclocking and overvoltage of Fermi cores, set `Option "Coolbits" "24"`.

The documentation of _Coolbits_ can be found in `/usr/share/doc/nvidia/html/xconfigoptions.html`. Driver version 346.16 documentation on _Coolbits_ can be found online [here](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html).

**Note:** An alternative is to edit and reflash the GPU BIOS either under DOS (preferred), or within a Win32 environment by way of [nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/) and [NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/). The advantage of BIOS flashing is that not only can voltage limits be raised, but stability is generally improved over software overclocking methods such as Coolbits. [Fermi BIOS modification tutorial](http://ivanvojtko.blogspot.sk/2014/03/how-to-overclock-geforce-460gtx-fermi.html)

##### Setting static 2D/3D clocks

Set the following string in the `Device` section to enable PowerMizer at its maximum performance level (VSync will not work without this line):

```
Option "RegistryDwords" "PerfLevelSrc=0x2222"

```

## Tips and tricks

### Fixing terminal resolution

Transitioning from nouveau may cause your startup terminal to display at a lower resolution. For GRUB, see [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks") for details.

### Avoid screen tearing in KDE (KWin)

 `/etc/profile.d/kwin.sh` 

```
export __GL_YIELD="USLEEP"

```

Also if the above does not help, then try this:

 `/etc/profile.d/kwin.sh` 

```
export KWIN_TRIPLE_BUFFER=1

```

Do not have both of the above enabled at the same time. Also if you enable triple buffering make sure to enable TripleBuffering for the driver itself. Source: [https://bugs.kde.org/show_bug.cgi?id=322060](https://bugs.kde.org/show_bug.cgi?id=322060)

### Hardware accelerated video decoding with XvMC

Accelerated decoding of MPEG-1 and MPEG-2 videos via [XvMC](/index.php/XvMC "XvMC") are supported on GeForce4, GeForce 5 FX, GeForce 6 and GeForce 7 series cards. To use it, create a new file `/etc/X11/XvMCConfig` with the following content:

```
libXvMCNVIDIA_dynamic.so.1

```

See how to configure [supported software](/index.php/XvMC#Supported_software "XvMC").

### Using TV-out

A good article on the subject can be found [here](http://en.wikibooks.org/wiki/NVidia/TV-OUT).

### X with a TV (DFP) as the only display

The X server falls back to CRT-0 if no monitor is automatically detected. This can be a problem when using a DVI connected TV as the main display, and X is started while the TV is turned off or otherwise disconnected.

To force NVIDIA to use DFP, store a copy of the EDID somewhere in the filesystem so that X can parse the file instead of reading EDID from the TV/DFP.

To acquire the EDID, start nvidia-settings. It will show some information in tree format, ignore the rest of the settings for now and select the GPU (the corresponding entry should be titled "GPU-0" or similar), click the `DFP` section (again, `DFP-0` or similar), click on the `Acquire Edid` Button and store it somewhere, for example, `/etc/X11/dfp0.edid`.

If in the front-end mouse and keyboard are not attached, the EDID can be acquired using only the command line. Run an X server with enough verbosity to print out the EDID block:

```
$ startx -- -logverbose 6

```

After the X Server has finished initializing, close it and your log file will probably be in `/var/log/Xorg.0.log`. Extract the EDID block using nvidia-xconfig:

```
$ nvidia-xconfig --extract-edids-from-file=/var/log/Xorg.0.log --extract-edids-output-file=/etc/X11/dfp0.bin

```

Edit `xorg.conf` by adding to the `Device` section:

```
Option "ConnectedMonitor" "DFP"
Option "CustomEDID" "DFP-0:/etc/X11/dfp0.edid"

```

The `ConnectedMonitor` option forces the driver to recognize the DFP as if it were connected. The `CustomEDID` provides EDID data for the device, meaning that it will start up just as if the TV/DFP was connected during X the process.

This way, one can automatically start a display manager at boot time and still have a working and properly configured X screen by the time the TV gets powered on.

If the above changes did not work, in the `xorg.conf` under `Device` section you can try to remove the `Option "ConnectedMonitor" "DFP"` and add the following lines:

```
Option "ModeValidation" "NoDFPNativeResolutionCheck"
Option "ConnectedMonitor" "DFP-0"

```

The `NoDFPNativeResolutionCheck` prevents NVIDIA driver from disabling all the modes that do not fit in the native resolution.

### Check the power source

The NVIDIA X.org driver can also be used to detect the GPU's current source of power. To see the current power source, check the 'GPUPowerSource' read-only parameter (0 - AC, 1 - battery):

 `$ nvidia-settings -q GPUPowerSource -t`  `1` 

### Listening to ACPI events

NVIDIA drivers automatically try to connect to the [acpid](/index.php/Acpid "Acpid") daemon and listen to ACPI events such as battery power, docking, some hotkeys, etc. If connection fails, X.org will output the following warning:

 `~/.local/share/xorg/Xorg.0.log` 

```
NVIDIA(0): ACPI: failed to connect to the ACPI event daemon; the daemon
NVIDIA(0):     may not be running or the "AcpidSocketPath" X
NVIDIA(0):     configuration option may not be set correctly.  When the
NVIDIA(0):     ACPI event daemon is available, the NVIDIA X driver will
NVIDIA(0):     try to use it to receive ACPI event notifications.  For
NVIDIA(0):     details, please see the "ConnectToAcpid" and
NVIDIA(0):     "AcpidSocketPath" X configuration options in Appendix B: X
NVIDIA(0):     Config Options in the README.

```

While completely harmless, you may get rid of this message by disabling the `ConnectToAcpid` option in your `/etc/X11/xorg.conf.d/20-nvidia.conf`:

```
Section "Device"
  ...
  Driver "nvidia"
  Option "ConnectToAcpid" "0"
  ...
EndSection

```

If you are on laptop, it might be a good idea to install and enable the [acpid](/index.php/Acpid "Acpid") daemon instead.

### Displaying GPU temperature in the shell

#### Method 1 - nvidia-settings

**Note:** This method requires that you are using X. Use Method 2 or Method 3 if you are not. Also note that Method 3 currently does not not work with newer NVIDIA cards such as GeForce 200 series cards as well as embedded GPUs such as the Zotac IONITX's 8800GS.

To display the GPU temp in the shell, use `nvidia-settings` as follows:

```
$ nvidia-settings -q gpucoretemp

```

This will output something similar to the following:

```
Attribute 'GPUCoreTemp' (hostname:0.0): 41.
'GPUCoreTemp' is an integer attribute.
'GPUCoreTemp' is a read-only attribute.
'GPUCoreTemp' can use the following target types: X Screen, GPU.

```

The GPU temps of this board is 41 C.

In order to get just the temperature for use in utils such as `rrdtool` or `conky`, among others:

 `$ nvidia-settings -q gpucoretemp -t`  `41` 

#### Method 2 - nvidia-smi

Use nvidia-smi which can read temps directly from the GPU without the need to use X at all. This is important for a small group of users who do not have X running on their boxes, perhaps because the box is headless running server apps. To display the GPU temperature in the shell, use nvidia-smi as follows:

```
$ nvidia-smi

```

This should output something similar to the following:

 `$ nvidia-smi` 

```
Fri Jan  6 18:53:54 2012       
+------------------------------------------------------+                       
| NVIDIA-SMI 2.290.10   Driver Version: 290.10         |                       
|-------------------------------+----------------------+----------------------+
| Nb.  Name                     | Bus Id        Disp.  | Volatile ECC SB / DB |
| Fan   Temp   Power Usage /Cap | Memory Usage         | GPU Util. Compute M. |
|===============================+======================+======================|
| 0\.  GeForce 8500 GT           | 0000:01:00.0  N/A    |       N/A        N/A |
|  30%   62 C  N/A   N/A /  N/A |  17%   42MB /  255MB |  N/A      Default    |
|-------------------------------+----------------------+----------------------|
| Compute processes:                                               GPU Memory |
|  GPU  PID     Process name                                       Usage      |
|=============================================================================|
|  0\.           ERROR: Not Supported                                          |
+-----------------------------------------------------------------------------+

```

Only for temperature:

 `$ nvidia-smi -q -d TEMPERATURE` 

```

==============NVSMI LOG==============

Timestamp                           : Sun Apr 12 08:49:10 2015
Driver Version                      : 346.59

Attached GPUs                       : 1
GPU 0000:01:00.0
    Temperature
        GPU Current Temp            : 52 C
        GPU Shutdown Temp           : N/A
        GPU Slowdown Temp           : N/A

```

In order to get just the temperature for use in utils such as rrdtool or conky, among others:

 `$ nvidia-smi --query-gpu=temperature.gpu --format=csv,noheader,nounits`  `52` 

Reference: [http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli](http://www.question-defense.com/2010/03/22/gpu-linux-shell-temp-get-nvidia-gpu-temperatures-via-linux-cli).

#### Method 3 - nvclock

Use [nvclock](https://aur.archlinux.org/packages/nvclock/) which is available from the [AUR](/index.php/AUR "AUR").

**Note:** `nvclock` cannot access thermal sensors on newer NVIDIA cards such as Geforce 200 series cards.

There can be significant differences between the temperatures reported by nvclock and nvidia-settings/nv-control. According to [this post](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899) by the author (thunderbird) of nvclock, the nvclock values should be more accurate.

### Set fan speed at login

You can adjust the fan speed on your graphics card with _nvidia-settings'_ console interface. First ensure that your Xorg configuration sets the Coolbits option to `4`, `5` or `12` for fermi and above in your `Device` section to enable fan control.

```
Option "Coolbits" "4"

```

**Note:** GeForce 400/500 series cards cannot currently set fan speeds at login using this method. This method only allows for the setting of fan speeds within the current X session by way of nvidia-settings.

Place the following line in your [xinitrc](/index.php/Xinitrc "Xinitrc") file to adjust the fan when you launch Xorg. Replace `_n_` with the fan speed percentage you want to set.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=_n_"

```

You can also configure a second GPU by incrementing the GPU and fan number.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=_n_" \
                -a "[gpu:1]/GPUFanControlState=1" -a  [fan:1]/GPUCurrentFanSpeed=_n_" &

```

If you use a login manager such as GDM or KDM, you can create a desktop entry file to process this setting. Create `~/.config/autostart/nvidia-fan-speed.desktop` and place this text inside it. Again, change `_n_` to the speed percentage you want.

```
[Desktop Entry]
Type=Application
Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=_n_"
X-GNOME-Autostart-enabled=true
Name=nvidia-fan-speed

```

**Note:** Since the drivers version 349.16, `GPUCurrentFanSpeed` has to be replaced with `GPUTargetFanSpeed`.[[3]](https://devtalk.nvidia.com/default/topic/821563/linux/can-t-control-fan-speed-with-beta-driver-349-12/post/4526208/#4526208)

### Order of install/deinstall for changing drivers

Where the old driver is nvidiaO and the new driver is nvidiaN.

*   remove nvidiaO
*   install nvidia-libglN
*   install nvidiaN
*   install lib32-nvidia-libgl-N (if required)

### Switching between NVIDIA and nouveau drivers

If you need to switch between drivers, you may use the following script, run as root (say yes to all confirmations):

```
#!/bin/bash
BRANCH= # Enter a branch if needed, i.e. -340xx or -304xx
NVIDIA=nvidia${BRANCH} # If no branch entered above this would be "nvidia"
NOUVEAU=xf86-video-nouveau

# Replace -R with -Rs to if you want to remove the unneeded dependencies
if [ $(pacman -Qqs ^mesa-libgl$) ]; then
    pacman -S $NVIDIA ${NVIDIA}-libgl # Add lib32-${NVIDIA}-libgl and ${NVIDIA}-lts if needed
    # pacman -R $NOUVEAU
elif [ $(pacman -Qqs ^${NVIDIA}$) ]; then
    pacman -S --needed $NOUVEAU mesa-libgl # Add lib32-mesa-libgl if needed
    pacman -R $NVIDIA # Add ${NVIDIA}-lts if needed
fi

```

### Avoid tearing with GeForce 500/600/700/900 series cards

Tearing can be avoided by forcing a full composition pipeline, regardless of the compositor you are using. To test whether this option will work, type

```
nvidia-settings --assign CurrentMetaMode="nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

It has been reported to reduce the performance of some OpenGL applications, though.

In order to make the change permanent, you need to add the following line to the `"Screen"` section of your Xorg configuration file, for example `/etc/X11/xorg.conf.d/20-nvidia.conf`:

```
Option  "metamodes" "nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

If you do not have an Xorg configuration file, you can create one for your present hardware using `nvidia-xconfig` (see [#Automatic configuration](#Automatic_configuration)) and move it from `/etc/X11/xorg.conf` to the preferred location `/etc/X11/xorg.conf.d/20-nvidia.conf`.

## Troubleshooting

### Gaming using TwinView

In case you want to play fullscreen games when using TwinView, you will notice that games recognize the two screens as being one big screen. While this is technically correct (the virtual X screen really is the size of your screens combined), you probably do not want to play on both screens at the same time.

To correct this behavior for SDL, try:

```
export SDL_VIDEO_FULLSCREEN_HEAD=1

```

For OpenGL, add the appropriate Metamodes to your xorg.conf in section `Device` and restart X:

```
Option "Metamodes" "1680x1050,1680x1050; 1280x1024,1280x1024; 1680x1050,NULL; 1280x1024,NULL;"

```

Another method that may either work alone or in conjunction with those mentioned above is [starting games in a separate X server](/index.php/Gaming#Starting_games_in_a_separate_X_server "Gaming").

### Vertical sync using TwinView

If you are using TwinView and vertical sync (the "Sync to VBlank" option in **nvidia-settings**), you will notice that only one screen is being properly synced, unless you have two identical monitors. Although **nvidia-settings** does offer an option to change which screen is being synced (the "Sync to this display device" option), this does not always work. A solution is to add the following environment variables at startup, for example append in `/etc/profile`:

```
export __GL_SYNC_TO_VBLANK=1
export __GL_SYNC_DISPLAY_DEVICE=DFP-0
export __VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

```

You can change `DFP-0` with your preferred screen (`DFP-0` is the DVI port and `CRT-0` is the VGA port). You can find the identifier for your display from **nvidia-settings** in the "X Server XVideoSettings" section.

### Wayland (gdm) crashes after nvidia-libgl installation

On some Intel CPUs outdated microcode causes instability with Wayland when nvidia are installed, causing gdm to crash.

[Updating the microcode](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode") should solve this problem.

### Corrupted screen: "Six screens" Problem

For some users, using GeForce GT 100M's, the screen gets corrupted after X starts, divided into 6 sections with a resolution limited to 640x480. The same problem has been recently reported with Quadro 2000 and hi-res displays.

To solve this problem, enable the Validation Mode `NoTotalSizeCheck` in section `Device`:

```
Section "Device"
 ...
 Option "ModeValidation" "NoTotalSizeCheck"
 ...
EndSection

```

### '/dev/nvidia0' input/output error

This error can occur for several different reasons, and the most common solution given for this error is to check for group/file permissions, which in almost every case is _not_ the problem. The NVIDIA documentation does not talk in detail on what you should do to correct this problem but there are a few things that have worked for some people. The problem can be a IRQ conflict with another device or bad routing by either the kernel or your BIOS.

First thing to try is to remove other video devices such as video capture cards and see if the problem goes away. If there are too many video processors on the same system it can lead into the kernel being unable to start them because of memory allocation problems with the video controller. In particular on systems with low video memory this can occur even if there is only one video processor. In such case you should find out the amount of your system's video memory (e.g. with `lspci -v`) and pass allocation parameters to the kernel, e.g. for a 32-bit kernel:

```
vmalloc=384M

```

If running a 64bit kernel, a driver defect can cause the NVIDIA module to fail initializing when IOMMU is on. Turning it off in the BIOS has been confirmed to work for some users. [[4]](http://www.nvnews.net/vbulletin/showthread.php?s=68bb2fabadcb53b10b286aa42d13c5bc&t=159335)[User:Clickthem#nvidia module](/index.php/User:Clickthem#nvidia_module "User:Clickthem")

Another thing to try is to change your BIOS IRQ routing from `Operating system controlled` to `BIOS controlled` or the other way around. The first one can be passed as a kernel parameter:

```
PCI=biosirq

```

The `noacpi` kernel parameter has also been suggested as a solution but since it disables ACPI completely it should be used with caution. Some hardware are easily damaged by overheating.

**Note:** The kernel parameters can be passed either through the kernel command line or the bootloader configuration file. See your bootloader Wiki page for more information.

### '/dev/nvidiactl' errors

Trying to start an OpenGL application might result in errors such as:

```
Error: Could not open /dev/nvidiactl because the permissions are too
restrictive. Please see the `FREQUENTLY ASKED QUESTIONS` 
section of `/usr/share/doc/NVIDIA_GLX-1.0/README` 
for steps to correct.

```

Solve by adding the appropriate user to the `video` group and log in again:

```
# gpasswd -a username video

```

### 32-bit applications do not start

Under 64-bit systems, installing `lib32-nvidia-libgl` that corresponds to the same version installed for the 64-bit driver fixes the problem.

### Errors after updating the kernel

If a custom build of NVIDIA's module is used instead of the package from the _extra_ repository, a recompile is required every time the kernel is updated. Rebooting is generally recommended after updating kernel and graphic drivers.

### Crashing in general

*   Try disabling `RenderAccel` in xorg.conf.
*   If Xorg outputs an error about "conflicting memory type" or "failed to allocate primary buffer: out of memory", add `nopat` at the end of the `kernel` line in `/boot/grub/menu.lst`.
*   If the NVIDIA compiler complains about different versions of GCC between the current one and the one used for compiling the kernel, add in `/etc/profile`:

```
export IGNORE_CC_MISMATCH=1

```

*   If Xorg is crashing with a "Signal 11" while using nvidia-96xx drivers, try disabling PAT. Pass the argument `nopat` to [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

More information about troubleshooting the driver can be found in the [NVIDIA forums.](https://forums.geforce.com/)

### Bad performance after installing a new driver version

If FPS have dropped in comparison with older drivers, first check if direct rendering is turned on (glxinfo is included in [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)):

```
$ glxinfo | grep direct

```

If the command prints:

```
direct rendering: No

```

then that could be an indication for the sudden FPS drop.

A possible solution could be to regress to the previously installed driver version and rebooting afterwards.

### CPU spikes with 400 series cards

If you are experiencing intermittent CPU spikes with a 400 series card, it may be caused by PowerMizer constantly changing the GPU's clock frequency. Switching PowerMizer's setting from Adaptive to Performance, add the following to the `Device` section of your Xorg configuration:

```
 Option "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"

```

### Laptops: X hangs on login/out, worked around with Ctrl+Alt+Backspace

If, while using the legacy NVIDIA drivers, Xorg hangs on login and logout (particularly with an odd screen split into two black and white/gray pieces), but logging in is still possible via `Ctrl+Alt+Backspace` (or whatever the new "kill X" key binding is), try adding this in `/etc/modprobe.d/modprobe.conf`:

```
options nvidia NVreg_Mobile=1

```

One user had luck with this instead, but it makes performance drop significantly for others:

```
options nvidia NVreg_DeviceFileUID=0 NVreg_DeviceFileGID=33 NVreg_DeviceFileMode=0660 NVreg_SoftEDIDs=0 NVreg_Mobile=1

```

Note that `NVreg_Mobile` needs to be changed according to the laptop:

*   1 for Dell laptops.
*   2 for non-Compal Toshiba laptops.
*   3 for other laptops.
*   4 for Compal Toshiba laptops.
*   5 for Gateway laptops.

See [NVIDIA Driver's README: Appendix K](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt) for more information.

### No screens found on a laptop/NVIDIA Optimus

On a laptop, if the NVIDIA driver cannot find any screens, you may have an NVIDIA Optimus setup : an Intel chipset connected to the screen and the video outputs, and a NVIDIA card that does all the hard work and writes to the chipset's video memory.

Check if `$ lspci | grep VGA` outputs something similar to:

```
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df4 (rev a1)

```

NVIDIA drivers now offer Optimus support since 319.12 Beta [[[5]](http://www.nvidia.com/object/linux-display-amd64-319.12-driver.html)] with kernels above and including 3.9.

Another solution is to install the [Intel](/index.php/Intel "Intel") driver to handle the screens, then if you want 3D software you should run them through [Bumblebee](/index.php/Bumblebee "Bumblebee") to tell them to use the NVIDIA card.

#### Possible Workaround

Enter the BIOS and changed the default graphics setting from 'Optimus' to 'Discrete' and the install NVIDIA drivers (295.20-1 at time of writing) recognized the screens.

Steps:

1.  Enter BIOS.
2.  Find Graphics Settings (should be in tab _Config > Display_).
3.  Change 'Graphics Device' to 'Discrete Graphics' (Disables Intel integrated graphics).
4.  Change OS Detection for Nvidia Optimus to "Disabled".
5.  Save and exit.

Tested on a Lenovo W520 with a Quadro 1000M and Nvidia Optimus

### Screen(s) found, but none have a usable configuration

Sometimes NVIDIA and X have trouble finding the active screen. If your graphics card has multiple outputs try plugging your monitor into the other ones. On a laptop it may be because your graphics card has vga/tv outs. Xorg.0.log will provide more info.

Another thing to try is adding invalid `"ConnectedMonitor" Option` to `Section "Device"` to force Xorg throws error and shows you how correct it. [Here](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) more about ConnectedMonitor setting.

After re-run X see Xorg.0.log to get valid CRT-x,DFP-x,TV-x values.

`nvidia-xconfig --query-gpu-info` could be helpful.

### Blackscreen at X startup / Machine poweroff at X shutdown

If you have installed an update of Nvidia and your screen stays black after launching Xorg, or if shutting down Xorg causes a machine poweroff, try the below workarounds. Alternatively, use the [Nouveau](/index.php/Nouveau "Nouveau") driver.

*   Use the `rcutree.rcu_idle_gp_delay=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

*   You can also try to add the `nvidia` module directly to your [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file.

*   If the screen still stays black with **both** the `rcutree.rcu_idle_gp_delay=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") and the `nvidia` module directly in the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file, try re-installing [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl) in that order, and finally reload the driver:

```
# modprobe nvidia

```

### Backlight is not turning off in some occasions

By default, DPMS should turn off backlight with the timeouts set or by running xset. However, probably due to a bug in the proprietary Nvidia drivers the result is a blank screen with no powersaving whatsoever. To workaround it, until the bug has been fixed you can use the `vbetool` as root.

Install the [vbetool](https://www.archlinux.org/packages/?name=vbetool) package.

Turn off your screen on demand and then by pressing a random key backlight turns on again:

```
vbetool dpms off && read -n1; vbetool dpms on

```

Alternatively, xrandr is able to disable and re-enable monitor outputs without requiring root.

```
xrandr --output DP-1 --off; read -n1; xrandr --output DP-1 --auto

```

### Blue tint on videos with Flash

A problem with [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) versions 11.2.202.228-1 and 11.2.202.233-1 causes it to send the U/V panes in the incorrect order resulting in a blue tint on certain videos. There are a few potential fixes for this bug:

1.  Install the latest [libvdpau](https://www.archlinux.org/packages/?name=libvdpau).
2.  Patch `vdpau_trace.so` with [this makepkg](https://bbs.archlinux.org/viewtopic.php?pid=1078368#p1078368).
3.  Right click on a video, select "Settings..." and uncheck "Enable hardware acceleration". Reload the page for it to take affect. Note that this disables GPU acceleration.
4.  [Downgrade](/index.php/Downgrade "Downgrade") the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) package to version 11.1.102.63-1 at most.
5.  Use [google-chrome](https://aur.archlinux.org/packages/google-chrome/) with the new Pepper API [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/).
6.  Try one of the few Flash alternatives.

The merits of each are discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=137877).

### Bleeding overlay with Flash

This bug is due to the incorrect colour key being used by the [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) version 11.2.202.228-1 and causes the flash content to "leak" into other pages or solid black backgrounds. To avoid this problem simply install the latest [libvdpau](https://www.archlinux.org/packages/?name=libvdpau) or export `VDPAU_NVIDIA_NO_OVERLAY=1` within either your shell profile (E.g. `~/.bash_profile` or `~/.zprofile`) or `~/.xinitrc`

### Full system freeze using Flash

If you experience occasional full system freezes (only the mouse is moving) using flashplugin and get:

 `/var/log/errors.log` 

```
NVRM: Xid (0000:01:00): 31, Ch 00000007, engmask 00000120, intr 10000000

```

A possible workaround is to switch off Hardware Acceleration in Flash, setting

 `/etc/adobe/mms.cfg`  `EnableLinuxHWVideoDecode=0` 

Or, if you want to keep Hardware acceleration enabled, you may try to::

```
export VDPAU_NVIDIA_NO_OVERLAY=1

```

...before starting the browser. Note that this may introduce tearing.

### Xorg fails to load or Red Screen of Death

If you get a red screen and use GRUB disable the GRUB framebuffer by editing `/etc/default/grub` and uncomment GRUB_TERMINAL_OUTPUT. For more information see [GRUB/Tips and tricks#Disable framebuffer](/index.php/GRUB/Tips_and_tricks#Disable_framebuffer "GRUB/Tips and tricks").

### Black screen on systems with Intel integrated GPU

If you have an Intel CPU with an integrated GPU (e.g. Intel HD 4000) and have installed the [nvidia](https://www.archlinux.org/packages/?name=nvidia) package, you may experience a black screen on boot, when changing virtual terminal, or when exiting an X session. This may be caused by a conflict between the graphics modules. This is solved by blacklisting the Intel GPU modules. Create the file `/etc/modprobe.d/blacklist.conf` and prevent the _i915_ and _intel_agp_ modules from loading on boot:

 `/etc/modprobe.d/blacklist.conf` 

```
install i915 /usr/bin/false
install intel_agp /usr/bin/false

```

### Black screen on systems with VIA integrated GPU

As above, blacklisting the _viafb_ module may resolve conflicts with NVIDIA drivers:

 `/etc/modprobe.d/blacklist.conf` 

```
install viafb /usr/bin/false

```

### X fails with "no screens found" with Intel iGPU

Like above, if you have an Intel CPU with an integrated GPU and X fails to start with

```
[ 76.633] (EE) No devices detected.
[ 76.633] Fatal server error:
[ 76.633] no screens found

```

then you need to add your discrete card's BusID to your X configuration. Find it:

 `# lspci | grep VGA` 

```
00:02.0 VGA compatible controller: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor Graphics Controller (rev 09)
01:00.0 VGA compatible controller: NVIDIA Corporation GK107 [GeForce GTX 650] (rev a1)

```

then you fix it by adding it to the card's Device section in your X configuration. In my case:

 `/etc/X11/xorg.conf.d/10-nvidia.conf` 

```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BusID          "PCI:1:0:0"
EndSection

```

Note how `01:00.0` is written as `1:0:0`.

### Xorg fails during boot, but otherwise starts fine

On very fast booting systems, systemd may attempt to start the display manager before the NVIDIA driver has fully initialized. You will see a message like the following in your logs only when Xorg runs during boot.

 `/var/log/Xorg.0.log` 

```
[     1.807] (EE) NVIDIA(0): Failed to initialize the NVIDIA kernel module. Please see the
[     1.807] (EE) NVIDIA(0):     system's kernel log for additional error messages and
[     1.808] (EE) NVIDIA(0):     consult the NVIDIA README for details.
[     1.808] (EE) NVIDIA(0):  *** Aborting ***
```

In this case you will need to establish an ordering dependency from the display manager to the DRI device. First create device units for DRI devices by creating a new udev rules file.

 `/etc/udev/rules.d/99-systemd-dri-devices.rules`  `ACTION=="add", KERNEL=="card*", SUBSYSTEM=="drm", TAG+="systemd"` 

Then create dependencies from the display manager to the device(s).

 `/etc/systemd/system/display-manager.service.d/10-wait-for-dri-devices.conf` 

```
[Unit]
Wants=dev-dri-card0.device
After=dev-dri-card0.device
```

If you have additional cards needed for the desktop then list them in Wants and After seperated by spaces.

### Flash video players crashes

If you are getting frequent crashes of Flash video players, try to switch off Hardware Acceleration:

 `/etc/adobe/mms.cfg`  `EnableLinuxHWVideoDecode=0` 

(This problem appeared after installing the proprietary nvidia driver, and was fixed by changing this setting.)

### Override EDID

If your monitor is providing wrong EDID information, the nvidia-driver will pick a very small solution. Nvidia's driver options change, this guide refers to nvidia 346.47-11.

Aside from manually setting modelines in the xorg config, you have to allow non-edid modes and disable edid in the device section:

 `/etc/X11/xorg.conf.d/10-monitor.conf` 

```
Section "Monitor"
    Identifier     "Monitor0"
    VendorName     "Unknown"
    ModelName      "Unknown"
    HorizSync       30-94
    VertRefresh     56-76
    DisplaySize    518.4 324.0
    Option         "DPMS"
    # 1920x1200 59.95 Hz (CVT 2.30MA-R) hsync: 74.04 kHz; pclk: 154.00 MHz
    Modeline "1920x1200R"  154.00  1920 1968 2000 2080  1200 1203 1209 1235 +hsync -vsync
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    Option         "UseEdidFreqs" "FALSE"
    Option         "UseEDID" "FALSE"
    Option         "ModeValidation" "AllowNonEdidModes"
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    SubSection     "Display"
        Depth       24
        Modes      "1920x1200R"
    EndSubSection
EndSection
```

### Fix rendering lag (firefox, gedit, vim, tmux …)

```
nvidia-settings -a InitialPixmapPlacement=0

```

[https://bugzilla.gnome.org/show_bug.cgi?id=728464](https://bugzilla.gnome.org/show_bug.cgi?id=728464)

### Screen Tearing with Multiple Monitor Orientations

When running multiple monitors in different orientations (through [Xrandr](/index.php/Xrandr "Xrandr") settings) such as portrait and landscape simultaneously, you may notice screen tearing in one of the orientations/monitors. Unfortunately, this issue is fixed by setting all monitors to the same orientation via [Xrandr](/index.php/Xrandr "Xrandr") settings

## See also

*   [NVIDIA User forums](https://forums.geforce.com/)
*   [Official README for NVIDIA drivers, all on one text page. Most Recent Driver Version as of September 7, 2015: 355.11.](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt)
*   [README Appendix B. X Config Options, 355.11 (direct link)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=NVIDIA&oldid=417484](https://wiki.archlinux.org/index.php?title=NVIDIA&oldid=417484)"