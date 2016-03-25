This article covers installing and configuring [NVIDIA](http://www.nvidia.com)'s *proprietary* graphic card driver. For information about the open-source drivers, see [Nouveau](/index.php/Nouveau "Nouveau"). If you have a laptop with hybrid Intel/NVIDIA graphics, see [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") instead.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Unsupported drivers](#Unsupported_drivers)
    *   [1.2 Alternate install: custom kernel](#Alternate_install:_custom_kernel)
        *   [1.2.1 Automatic re-compilation of the NVIDIA module with kernel update](#Automatic_re-compilation_of_the_NVIDIA_module_with_kernel_update)
    *   [1.3 Pure Video HD (VDPAU/VAAPI)](#Pure_Video_HD_.28VDPAU.2FVAAPI.29)
    *   [1.4 Hardware accelerated video decoding with XvMC](#Hardware_accelerated_video_decoding_with_XvMC)
*   [2 Configuration](#Configuration)
    *   [2.1 Minimal configuration](#Minimal_configuration)
    *   [2.2 Automatic configuration](#Automatic_configuration)
    *   [2.3 NVIDIA Settings](#NVIDIA_Settings)
    *   [2.4 Multiple monitors](#Multiple_monitors)
        *   [2.4.1 Using NVIDIA Settings](#Using_NVIDIA_Settings)
        *   [2.4.2 ConnectedMonitor](#ConnectedMonitor)
        *   [2.4.3 TwinView](#TwinView)
            *   [2.4.3.1 Manual CLI configuration with xrandr](#Manual_CLI_configuration_with_xrandr)
            *   [2.4.3.2 Vertical sync using TwinView](#Vertical_sync_using_TwinView)
            *   [2.4.3.3 Gaming using TwinView](#Gaming_using_TwinView)
        *   [2.4.4 Mosaic mode](#Mosaic_mode)
            *   [2.4.4.1 Base Mosaic](#Base_Mosaic)
            *   [2.4.4.2 SLI Mosaic](#SLI_Mosaic)
    *   [2.5 Driver persistence](#Driver_persistence)
*   [3 See also](#See_also)

## Installation

**Warning:** Avoid installing the NVIDIA driver through the package provided from the NVIDIA website. Installation through [pacman](/index.php/Pacman "Pacman") allows upgrading the driver together with the rest of the system.

These instructions are for those using the stock [linux](https://www.archlinux.org/packages/?name=linux) or [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) packages. For custom kernel setup, skip to the [next](#Alternate_install:_custom_kernel) subsection.

1\. If you do not know what graphics card you have, find out by issuing:

	 `$ lspci -k | grep -A 2 -E "(VGA|3D)"` 

2\. Determine the necessary driver version for your card by:

*   finding the code name (e.g. NV50, NVC0, etc.) on [nouveau wiki's code names page](http://nouveau.freedesktop.org/wiki/CodeNames)
*   looking up the name in NVIDIA's [legacy card list](http://www.nvidia.com/object/IO_32667.html): if your card is not there you can use the latest driver
*   visiting NVIDIA's [driver download site](http://www.nvidia.com/Download/index.aspx)

3\. Install the appropriate driver for your card:

*   For GeForce 400 series cards and newer [NVCx and newer], [install](/index.php/Install "Install") the [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [nvidia-lts](https://www.archlinux.org/packages/?name=nvidia-lts) package along with [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl). (The very latest GPU models, may require the [nvidia-beta](https://aur.archlinux.org/packages/nvidia-beta/) package, as stable drivers may not support the newly introduced features).
*   For GeForce 8000/9000, ION and 100-300 series cards [NV5x, NV8x, NV9x and NVAx] from around 2006-2010, [install](/index.php/Install "Install") the [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) or [nvidia-340xx-lts](https://www.archlinux.org/packages/?name=nvidia-340xx-lts) package along with [nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=nvidia-340xx-libgl).
*   For GeForce 6000/7000 series cards [NV4x and NV6x] from around 2004-2006, [install](/index.php/Install "Install") the [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) or [nvidia-304xx-lts](https://www.archlinux.org/packages/?name=nvidia-304xx-lts) package along with [nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=nvidia-304xx-libgl).

*   For even older cards, have a look at [#Unsupported drivers](#Unsupported_drivers).

4\. If you are on 64-bit and also need 32-bit OpenGL support, you must also install the equivalent *lib32* package from the [multilib](/index.php/Multilib "Multilib") repository (e.g. [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl), [lib32-nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-libgl) or [lib32-nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-libgl)).

5\. Reboot. The [nvidia](https://www.archlinux.org/packages/?name=nvidia) package contains a file which blacklists the *nouveau* module, so rebooting is necessary.

Once the driver has been installed, continue to [#Configuration](#Configuration).

### Unsupported drivers

If you have a GeForce 5 FX series card or older, Nvidia no longer supports drivers for your card. This means that these drivers [do not support the current Xorg version](http://nvidia.custhelp.com/app/answers/detail/a_id/3142/). It thus might be easier if you use the [nouveau](/index.php/Nouveau "Nouveau") driver, which supports the old cards with the current Xorg.

However, Nvidia's legacy drivers are still available and might provide better 3D performance/stability if you are willing to downgrade Xorg:

*   For GeForce 5 FX series cards [NV30-NV36], install the [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/) package. Last supported Xorg version is 1.15.
*   For GeForce 2/3/4 MX/Ti series cards [NV11, NV17-NV28], install the [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/) package. Last supported Xorg version is 1.12.

**Tip:** The legacy nvidia-96xx-dkms and nvidia-173xx-dkms drivers can also be installed from the unofficial [[city] repository](http://pkgbuild.com/~bgyorgy/city.html). (It is strongly advised that you do not skip any dependencies restriction when installing from here)

### Alternate install: custom kernel

**Tip:** You must build a custom [nvidia](https://www.archlinux.org/packages/?name=nvidia) package to use it with a custom kernel, so it is a good idea to be familiar with the following topics:

*   [ABS](/index.php/ABS "ABS")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [Creating packages](/index.php/Creating_packages "Creating packages")

Follow the [How to use ABS](/index.php/ABS#How_to_use_ABS "ABS") instructions to create a build directory for the `nvidia` package. Then, before building with [makepkg](/index.php/Makepkg "Makepkg"), you must edit `nvidia.install` and `PKGBUILD` so that they contain the right kernel version variables.

While running the custom kernel, get the appropriate kernel and local version names:

```
$ uname -r

```

and make sure the corresponding kernel header package, which was built during kernel compilation, is installed as well. Next:

1.  In nvidia.install, replace the `EXTRAMODULES='extramodules-3.4-ARCH'` variable with the custom kernel version, such as `EXTRAMODULES='extramodules-3.4.4'` or `EXTRAMODULES='extramodules-3.4.4-custom'` depending on what the kernel's version is and the local version's text/numbers. Do this for all instances of the version number within this file.
2.  In PKGBUILD, change the `_extramodules=extramodules-3.4-ARCH` variable to match the appropriate version, as above.
3.  If there are multiple kernels installed in parallel (such as a custom kernel alongside the default -ARCH kernel), change the `pkgname=nvidia` variable in the PKGBUILD to a unique identifier, such as nvidia-344 or nvidia-custom. This will allow both kernels to use the nvidia module, since the custom nvidia module has a different package name and will not overwrite the original. You will also need to comment the line in `package()` that blacklists the nouveau module in `/usr/lib/modprobe.d/nvidia.conf` (no need to do it again).

Then build and install the package as usual.

#### Automatic re-compilation of the NVIDIA module with kernel update

This is possible with [DKMS](/index.php/DKMS "DKMS"). Install the [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) package (or a specific branch such as [nvidia-340xx-dkms](https://www.archlinux.org/packages/?name=nvidia-340xx-dkms)). The [dkms](https://www.archlinux.org/packages/?name=dkms) package doesn't use [Systemd](/index.php/Systemd "Systemd") anymore, it uses pacman/alpm hooks. See [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman") for more information. See [Dynamic Kernel Module Support#Usage](/index.php/Dynamic_Kernel_Module_Support#Usage "Dynamic Kernel Module Support") for more information on how to use [DKMS](/index.php/DKMS "DKMS").

### Pure Video HD (VDPAU/VAAPI)

At least a video card with second generation [PureVideo HD](https://en.wikipedia.org/wiki/Nvidia_PureVideo#Table_of_GPUs_containing_a_PureVideo_SIP_block "wikipedia:Nvidia PureVideo") is required to use [VDPAU](/index.php/VDPAU "VDPAU") and [VA-API](/index.php/VA-API "VA-API").

### Hardware accelerated video decoding with XvMC

Accelerated decoding of MPEG-1 and MPEG-2 videos via [XvMC](/index.php/XvMC "XvMC") are supported on GeForce4, GeForce 5 FX, GeForce 6 and GeForce 7 series cards. See [XvMC](/index.php/XvMC "XvMC") for detail.

## Configuration

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

**Tip:** If upgrading from nouveau make sure to remove `nouveau` from `/etc/mkinitcpio.conf`. See [Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers), if switching between the open and proprietary drivers often.

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

### NVIDIA Settings

The [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) tool lets you configure many options using a GUI. Run `nvidia-settings` as root, configure as you wish, and then save the configuration to `/etc/X11/xorg.conf.d/` as usual.

Alternatively, you can run the GUI as a normal user and save the settings to `~/.nvidia-settings-rc`. Then you can load the settings using `$ nvidia-settings --load-config-only` (for example in your [xinitrc](/index.php/Xinitrc "Xinitrc")).

**Tip:** If your X server is crashing on startup, it may be because the GUI-generated settings are corrupt. Try deleting the generated file and starting from scratch.

### Multiple monitors

	*See [Multihead](/index.php/Multihead "Multihead") for more general information*

#### Using NVIDIA Settings

The [nvidia-settings](#NVIDIA_Settings) tool can configure multiple monitors.

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
export __VDPAU_NVIDIA_SYNC_DISPLAY_DEVICE=DFP-0

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

### Driver persistence

Since version 319, Nvidia has changed the way driver persistence works, it now has a daemon that is to be run at boot. See the [Driver Persistence](http://docs.nvidia.com/deploy/driver-persistence/index.html) section of the Nvidia documentation for more details.

To start the persistence daemon at boot, [enable](/index.php/Enable "Enable") the `nvidia-persistenced.service`. For manual usage see the [upstream documentation](http://docs.nvidia.com/deploy/driver-persistence/index.html#usage).

## See also

*   [NVIDIA User forums](https://forums.geforce.com/)
*   [Official README for NVIDIA drivers, all on one text page. Most Recent Driver Version as of September 7, 2015: 355.11.](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt)
*   [README Appendix B. X Config Options, 355.11 (direct link)](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html)