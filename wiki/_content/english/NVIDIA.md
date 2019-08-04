Related articles

*   [NVIDIA/Tips and tricks](/index.php/NVIDIA/Tips_and_tricks "NVIDIA/Tips and tricks")
*   [NVIDIA/Troubleshooting](/index.php/NVIDIA/Troubleshooting "NVIDIA/Troubleshooting")
*   [Nouveau](/index.php/Nouveau "Nouveau")
*   [Bumblebee](/index.php/Bumblebee "Bumblebee")
*   [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")
*   [nvidia-xrun](/index.php/Nvidia-xrun "Nvidia-xrun")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Vulkan](/index.php/Vulkan "Vulkan")

This article covers the proprietary [NVIDIA](http://www.nvidia.com) graphics card driver. For the open-source driver, see [Nouveau](/index.php/Nouveau "Nouveau"). If you have a laptop with hybrid Intel/NVIDIA graphics, see [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") instead.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Unsupported drivers](#Unsupported_drivers)
    *   [1.2 Custom kernel](#Custom_kernel)
    *   [1.3 DRM kernel mode setting](#DRM_kernel_mode_setting)
        *   [1.3.1 Pacman hook](#Pacman_hook)
    *   [1.4 Hardware accelerated video decoding](#Hardware_accelerated_video_decoding)
        *   [1.4.1 NVDEC and VDPAU](#NVDEC_and_VDPAU)
        *   [1.4.2 XvMC](#XvMC)
*   [2 Configuration](#Configuration)
    *   [2.1 Minimal configuration](#Minimal_configuration)
    *   [2.2 Automatic configuration](#Automatic_configuration)
    *   [2.3 NVIDIA Settings](#NVIDIA_Settings)
    *   [2.4 Multiple GPUs/SLI](#Multiple_GPUs/SLI)
    *   [2.5 Multiple monitors](#Multiple_monitors)
        *   [2.5.1 Using NVIDIA Settings](#Using_NVIDIA_Settings)
        *   [2.5.2 ConnectedMonitor](#ConnectedMonitor)
        *   [2.5.3 TwinView](#TwinView)
            *   [2.5.3.1 Manual CLI configuration with xrandr](#Manual_CLI_configuration_with_xrandr)
            *   [2.5.3.2 Vertical sync using TwinView](#Vertical_sync_using_TwinView)
            *   [2.5.3.3 Gaming using TwinView](#Gaming_using_TwinView)
        *   [2.5.4 Mosaic mode](#Mosaic_mode)
            *   [2.5.4.1 Base Mosaic](#Base_Mosaic)
            *   [2.5.4.2 SLI Mosaic](#SLI_Mosaic)
    *   [2.6 Driver persistence](#Driver_persistence)
*   [3 See also](#See_also)

## Installation

**Warning:** Avoid installing the NVIDIA driver through the package provided from the NVIDIA website. Installation through [pacman](/index.php/Pacman "Pacman") allows upgrading the driver together with the rest of the system.

These instructions are for those using the stock [linux](https://www.archlinux.org/packages/?name=linux) or [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) packages. For custom kernel setup, skip to the [next](#Custom_kernel) subsection.

1\. If you do not know what graphics card you have, find out by issuing:

	 `$ lspci -k | grep -A 2 -E "(VGA|3D)"` 

2\. Determine the necessary driver version for your card by:

*   finding the code name (e.g. NV50, NVC0, etc.) on [Nouveau wiki's code names page](https://nouveau.freedesktop.org/wiki/CodeNames/)
*   looking up the name in NVIDIA's [legacy card list](https://www.nvidia.com/object/IO_32667.html): if your card is not there you can use the latest driver
*   visiting NVIDIA's [driver download site](https://www.nvidia.com/Download/index.aspx)

3\. Install the appropriate driver for your card:

*   For GeForce 600-900 and Quadro/Tesla/Tegra K-series cards and newer [NVE0, NV110 and NV130 family cards from around 2010-2019], [install](/index.php/Install "Install") the [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts) package.

*   If these packages do not work, [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/) may have a newer driver version that offers support.
*   There is also [nvidia-llb-dkms](https://aur.archlinux.org/packages/nvidia-llb-dkms/), which is built from Nvidia's [long lived branch](https://www.phoronix.com/scan.php?page=news_item&px=OTkxOA).

*   For GeForce 400/500 series cards [NVCx and NVDx] from around 2010-2011, [install](/index.php/Install "Install") the [nvidia-390xx](https://www.archlinux.org/packages/?name=nvidia-390xx) or [nvidia-390xx-lts](https://www.archlinux.org/packages/?name=nvidia-390xx-lts) package.

*   For even older cards (released in 2010 or earlier), have a look at [#Unsupported drivers](#Unsupported_drivers).

4\. For 32-bit application support, also install the corresponding *lib32* nvidia package from the [multilib](/index.php/Multilib "Multilib") repository (e.g. [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) or [lib32-nvidia-390xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-390xx-utils)).

5\. Reboot. The [nvidia](https://www.archlinux.org/packages/?name=nvidia) package contains a file which blacklists the *nouveau* module, so rebooting is necessary.

Once the driver has been installed, continue to [#Configuration](#Configuration).

### Unsupported drivers

If you have a GeForce 300 series card or older (released in 2010 or earlier), Nvidia no longer supports drivers for your card. This means that these drivers [do not support the current Xorg version](https://nvidia.custhelp.com/app/answers/detail/a_id/3142/). It thus might be easier if you use the [Nouveau](/index.php/Nouveau "Nouveau") driver, which supports the old cards with the current Xorg.

However, Nvidia's legacy drivers are still available and might provide better 3D performance/stability if you are willing to downgrade [Xorg](/index.php/Xorg "Xorg"):

*   For GeForce 8/9, ION and 100-300 series cards [NV5x, NV8x, NV9x and NVAx], [install](/index.php/Install "Install") the [nvidia-340xx-dkms](https://aur.archlinux.org/packages/nvidia-340xx-dkms/) package. (supports the latest Xorg but has [issues](https://lists.archlinux.org/pipermail/arch-dev-public/2019-May/029568.html) with Linux 5.0+)
*   For GeForce 6/7 series cards [NV4x and NV6x], [install](/index.php/Install "Install") the [nvidia-304xx-dkms](https://aur.archlinux.org/packages/nvidia-304xx-dkms/) package. Last supported Xorg version is 1.19.
*   For GeForce 5 FX series cards [NV30-NV36], install the [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/) package. Last supported Xorg version is 1.15.
*   For GeForce 2/3/4 MX/Ti series cards [NV11, NV17-NV28], install the [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/) package. Last supported Xorg version is 1.12.

### Custom kernel

If you are using a custom kernel, compilation of the Nvidia kernel modules can be automated with [DKMS](/index.php/DKMS "DKMS").

Install the [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) package (or a specific branch such as [nvidia-390xx-dkms](https://www.archlinux.org/packages/?name=nvidia-390xx-dkms)). The Nvidia module will be rebuilt after every Nvidia or kernel update thanks to the DKMS [pacman hook](/index.php/Pacman_hook "Pacman hook").

### DRM kernel mode setting

[nvidia](https://www.archlinux.org/packages/?name=nvidia) 364.16 adds support for DRM (Direct Rendering Manager) [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). To enable this feature, add the `nvidia-drm.modeset=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), and add `nvidia`, `nvidia_modeset`, `nvidia_uvm` and `nvidia_drm` to the initramfs according to [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio").

Do not forget to run [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") every time there is a [nvidia](https://www.archlinux.org/packages/?name=nvidia) driver update. See [#Pacman hook](#Pacman_hook) to automate these steps.

**Warning:** Enabling [KMS](/index.php/KMS "KMS") causes [GNOME](/index.php/GNOME "GNOME") to default to [Wayland](/index.php/Wayland "Wayland"), which currently suffers from very poor performance: [FS#53284](https://bugs.archlinux.org/task/53284). Use the *GNOME on Xorg* session instead.

**Note:** The NVIDIA driver does **not** provide an `fbdev` driver for the high-resolution console for the kernel compiled-in `vesafb` module. However, the kernel compiled-in `efifb` module supports a high-resolution console on EFI systems. This method requires GRUB and is described in [NVIDIA/Tips and tricks#Fixing terminal resolution](/index.php/NVIDIA/Tips_and_tricks#Fixing_terminal_resolution "NVIDIA/Tips and tricks").[[1]](https://forums.fedoraforum.org/showthread.php?t=306271)[[2]](https://www.reddit.com/r/archlinux/comments/4gwukx/nvidia_drivers_and_high_resolution_tty_possible/).

#### Pacman hook

To avoid the possibility of forgetting to update [initramfs](/index.php/Initramfs "Initramfs") after an NVIDIA driver upgrade, you may want to use a [pacman hook](/index.php/Pacman_hook "Pacman hook"):

 `/etc/pacman.d/hooks/nvidia.hook` 
```
[Trigger]
Operation=Install
Operation=Upgrade
Operation=Remove
Type=Package
Target=nvidia
Target=linux
# Change the linux part above and in the Exec line if a different kernel is used

[Action]
Description=Update Nvidia module in initcpio
Depends=mkinitcpio
When=PostTransaction
NeedsTargets
Exec=/bin/sh -c 'while read -r trg; do case $trg in linux) exit 0; esac; done; /usr/bin/mkinitcpio -P'
```

Make sure the `Target` package set in this hook is the one you've installed in steps above (e.g. `nvidia`, `nvidia-dkms`, `nvidia-lts` or `nvidia-ck-something`).

**Note:** The complication in the `Exec` line above is in order to avoid running `mkinitcpio` multiple times if both `nvidia` and `linux` get updated. In case this doesn't bother you, the `Target=linux` and `NeedsTargets` lines may be dropped, and the `Exec` line may be reduced to simply `Exec=/usr/bin/mkinitcpio -P`.

### Hardware accelerated video decoding

#### NVDEC and VDPAU

Accelerated video decoding with VDPAU is supported on GeForce 8 series cards and newer. Accelerated video decoding with NVDEC is supported on Fermi cards and newer. See [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration") for details.

#### XvMC

Accelerated decoding of MPEG-1 and MPEG-2 videos via [XvMC](/index.php/XvMC "XvMC") are supported on GeForce4, GeForce 5 FX, GeForce 6 and GeForce 7 series cards. See [XvMC](/index.php/XvMC "XvMC") for details.

## Configuration

The proprietary NVIDIA graphics card driver does not need any Xorg server configuration file. You can run [a test](/index.php/Xorg#Running "Xorg") to see if the Xorg server will function correctly without a configuration file. However, it may be required to create a configuration file (prefer `/etc/X11/xorg.conf.d/20-nvidia.conf` over `/etc/X11/xorg.conf`) in order to adjust various settings. This configuration can be generated by the NVIDIA Xorg configuration tool, or it can be created manually. If created manually, it can be a minimal configuration (in the sense that it will only pass the basic options to the [Xorg](/index.php/Xorg "Xorg") server), or it can include a number of settings that can bypass Xorg's auto-discovered or pre-configured options.

**Tip:** For more configuration options see [NVIDIA/Tips and tricks#Manual configuration](/index.php/NVIDIA/Tips_and_tricks#Manual_configuration "NVIDIA/Tips and tricks") and [NVIDIA/Troubleshooting](/index.php/NVIDIA/Troubleshooting "NVIDIA/Troubleshooting") section.

### Minimal configuration

A basic configuration block in `20-nvidia.conf` (or deprecated in `xorg.conf`) would look like this:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
        Identifier "Nvidia Card"
        Driver "nvidia"
        VendorName "NVIDIA Corporation"
        BoardName "GeForce GTX 1050 Ti"
EndSection

```

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

### NVIDIA Settings

The [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) tool lets you configure many options using either CLI or GUI. Running `nvidia-settings` without any options launches the GUI, for CLI options see [nvidia-settings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nvidia-settings.1).

You can run the CLI/GUI as a non-root user and save the settings to `~/.nvidia-settings-rc` or save it as [xorg.conf](/index.php/Xorg#Using_xorg.conf "Xorg") by using the option *Save to X configuration File* for a multi-user environment.

To load the `~/.nvidia-settings-rc` for the current user:

```
$ nvidia-settings --load-config-only

```

See [Autostarting](/index.php/Autostarting "Autostarting") to start this command on every boot.

**Note:** [Xorg](/index.php/Xorg "Xorg") may not start or crash on startup after saving `nvidia-settings` changes. Adjusting or deleting the generated `~/.nvidia-settings-rc` and/or [Xorg](/index.php/Xorg "Xorg") file(s) should recover normal startup.

### Multiple GPUs/SLI

If you're planning to use an SLI setup, you should check [NVIDIA/Tips and tricks#Enabling SLI](/index.php/NVIDIA/Tips_and_tricks#Enabling_SLI "NVIDIA/Tips and tricks") as manual configuration changes might be required for a working setup.

### Multiple monitors

See [Multihead](/index.php/Multihead "Multihead") for more general information.

#### Using NVIDIA Settings

The [nvidia-settings](#NVIDIA_Settings) tool can configure multiple monitors.

For CLI configuration, first get the `CurrentMetaMode` by running:

 `$ nvidia-settings -q CurrentMetaMode`  `Attribute 'CurrentMetaMode' (hostnmae:0.0): id=50, switchable=no, source=nv-control :: DPY-1: 2880x1620 @2880x1620 +0+0 {ViewPortIn=2880x1620, ViewPortOut=2880x1620+0+0}` 

Save everything after the `::` to the end of the attribute (in this case: `DPY-1: 2880x1620 @2880x1620 +0+0 {ViewPortIn=2880x1620, ViewPortOut=2880x1620+0+0}`) and use to reconfigure your displays with `nvidia-settings --assign "CurrentMetaMode=*your_meta_mode*"`.

**Tip:** You can create shell aliases for the different monitor and resolution configurations you use.

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

If the latest solutions do not work for you, you can use your window manager's *autostart* implementation with [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr).

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

##### Vertical sync using TwinView

If you are using TwinView and vertical sync (the "Sync to VBlank" option in **nvidia-settings**), you will notice that only one screen is being properly synced, unless you have two identical monitors. Although **nvidia-settings** does offer an option to change which screen is being synced (the "Sync to this display device" option), this does not always work. A solution is to add the following environment variables at startup, for example append in `/etc/profile`:

```
export __GL_SYNC_TO_VBLANK=1
export __GL_SYNC_DISPLAY_DEVICE=DFP-0
export VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

```

You can change `DFP-0` with your preferred screen (`DFP-0` is the DVI port and `CRT-0` is the VGA port). You can find the identifier for your display from **nvidia-settings** in the "X Server XVideoSettings" section.

##### Gaming using TwinView

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

#### Mosaic mode

Mosaic mode is the only way to use more than 2 monitors across multiple graphics cards with compositing. Your window manager may or may not recognize the distinction between each monitor. Mosaic mode requires a valid SLI configuration. Even if using Base mode without SLI, the GPUs must still be SLI capable/compatible.

##### Base Mosaic

Base Mosaic mode works on any set of Geforce 8000 series or higher GPUs. It cannot be enabled from within the nvidia-setting GUI. You must either use the `nvidia-xconfig` command line program or edit `xorg.conf` by hand. Metamodes must be specified. The following is an example for four DFPs in a 2x2 configuration, each running at 1920x1024, with two DFPs connected to two cards:

```
$ nvidia-xconfig --base-mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

**Note:** While the documentation lists a 2x2 configuration of monitors, [GeForce cards are artificially limited to 3 monitors](https://devtalk.nvidia.com/default/topic/579449/linux/basemosaic-v295-vs-v310-vs-v325-only-up-to-three-screens-/post/3954733/#3954733) in Base Mosaic mode. Quadro cards support more than 3 monitors. As of September 2014, the Windows driver has dropped this artificial restriction, but it remains in the Linux driver.

##### SLI Mosaic

If you have an SLI configuration and each GPU is a Quadro FX 5800, Quadro Fermi or newer then you can use SLI Mosaic mode. It can be enabled from within the nvidia-settings GUI or from the command line with:

```
$ nvidia-xconfig --sli=Mosaic --metamodes="GPU-0.DFP-0: 1920x1024+0+0, GPU-0.DFP-1: 1920x1024+1920+0, GPU-1.DFP-0: 1920x1024+0+1024, GPU-1.DFP-1: 1920x1024+1920+1024"

```

### Driver persistence

Nvidia has a daemon that can be optionally run at boot. In a standard single-GPU X desktop environment the persistence daemon is not needed and can actually create issues [[3]](https://devtalk.nvidia.com/default/topic/1044421/linux/nvidia-persistenced-causing-60-second-reboot-delays). See the [Driver Persistence](http://docs.nvidia.com/deploy/driver-persistence/index.html#persistence-daemon) section of the Nvidia documentation for more details.

To start the persistence daemon at boot, [enable](/index.php/Enable "Enable") the `nvidia-persistenced.service`. For manual usage see the [upstream documentation](http://docs.nvidia.com/deploy/driver-persistence/index.html#usage).

## See also

*   [NVIDIA User forums](https://forums.geforce.com/)
*   [Official README for NVIDIA drivers, all on one text page. Version 387.22 (2017-10-25)](http://download.nvidia.com/XFree86/Linux-x86/387.22/README/README.txt)
*   [README Appendix B. X Config Options, 387.22 (direct link)](http://download.nvidia.com/XFree86/Linux-x86/387.22/README/xconfigoptions.html)