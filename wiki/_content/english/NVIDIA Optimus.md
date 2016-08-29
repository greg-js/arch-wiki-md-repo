NVIDIA Optimus is a technology that allows an Intel integrated GPU and discrete NVIDIA GPU to be built into and accessed by a laptop. Getting Optimus graphics to work on Arch Linux requires a few somewhat complicated steps, explained below. There are several methods available:

*   disabling one of the devices in BIOS, which may result in improved battery life if the NVIDIA device is disabled, but may not be available with all BIOSes and does not allow GPU switching

*   using the official Optimus support included with the proprietary NVIDIA driver, which offers the best NVIDIA performance but does not allow GPU switching and can be more buggy than the open-source driver

*   using the PRIME functionality of the open-source nouveau driver, which allows GPU switching but offers poor performance compared to the proprietary NVIDIA driver and does not currently implement any powersaving

*   using the third-party Bumblebee program to implement Optimus-like functionality, which offers GPU switching and powersaving but requires extra configuration

These options are explained in detail below.

## Contents

*   [1 Disabling switchable graphics](#Disabling_switchable_graphics)
*   [2 Using nvidia](#Using_nvidia)
    *   [2.1 Alternative configuration](#Alternative_configuration)
    *   [2.2 Display Managers](#Display_Managers)
        *   [2.2.1 LightDM](#LightDM)
        *   [2.2.2 SDDM](#SDDM)
        *   [2.2.3 GDM](#GDM)
        *   [2.2.4 KDM](#KDM)
    *   [2.3 Checking 3D](#Checking_3D)
    *   [2.4 Further Information](#Further_Information)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Tearing/Broken VSync](#Tearing.2FBroken_VSync)
    *   [3.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29)
    *   [3.3 Resolution, screen scan wrong. EDID errors in Xorg.log](#Resolution.2C_screen_scan_wrong._EDID_errors_in_Xorg.log)
    *   [3.4 NVIDIA provider in xrandr does not have the Source Output capability](#NVIDIA_provider_in_xrandr_does_not_have_the_Source_Output_capability)
*   [4 Using nouveau](#Using_nouveau)
*   [5 Using Bumblebee](#Using_Bumblebee)

## Disabling switchable graphics

If you only care to use a certain GPU without switching, check the options in your system's BIOS. There should be an option to disable one of the cards. Some laptops only allow disabling of the discrete card, or vice-versa, but it is worth checking if you only plan to use one of the cards. If you want to use both cards, or cannot disable the card you do not want, see the options below.

## Using nvidia

The [proprietary NVIDIA driver](/index.php/NVIDIA "NVIDIA") does not support dynamic switching like the nouveau driver (meaning it can only use the NVIDIA device). It also has notable screen-tearing issues that NVIDIA recognizes but has not fixed. However, it does allow use of the discrete GPU and has (as of October 2013) a marked edge in performance over the nouveau driver.

First, install [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl) and [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) from the official repositories.

Then, configure `xorg.conf`. You will need to know the PCI address of the NVIDIA card, which you can find by issuing

```
$ lspci | grep -E "VGA|3D"

```

The PCI address is the first 7 characters of the line that mentions NVIDIA. It will look something like `01:00.0`. In the `xorg.conf`, you will need to format it as `#:#:#`; e.g. `01:00.0` would be formatted as `1:0:0`.

**Note:** Since Xorg-server 1.17-1 [FS#43830](https://bugs.archlinux.org/task/43830) related to the `modesetting` module persists for Optimus configurations. A work-around for some systems is to set the `Option "AccelMethod"` to `"none"`, as in the configuration below. Other systems require it set to `"sna"`, see [#Alternative configuration](#Alternative_configuration).

**Note:** On some setups this setup breaks automatic detection of the values of the display by the nvidia driver through the EDID file. As a work-around see [#Resolution, screen scan wrong. EDID errors in Xorg.log](#Resolution.2C_screen_scan_wrong._EDID_errors_in_Xorg.log).

If X.Org X server version 1.17.2 or higher is installed ([[1]](http://us.download.nvidia.com/XFree86/Linux-x86/358.16/README/randr14.html))

 `/etc/X11/xorg.conf` 
```
Section "Module"
    Load "modesetting"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "<BusID for NVIDIA device here>"
    Option "AllowEmptyInitialConfiguration"
EndSection

```

For older X servers

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
    Identifier "layout"
    Screen 0 "nvidia"
    Inactive "intel"
EndSection

Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    **# Change BusID if necessary. Tips: (lspci | grep 3D) (Change 01:00.0 to 1:0:0)**
    **BusID "PCI:1:0:0"**
EndSection

Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    Option "AllowEmptyInitialConfiguration" "Yes"
EndSection

Section "Device"
    Identifier "intel"
    Driver "modesetting"
    **# Change BusID if necessary. Tips: (lspci | grep VGA) (Change 00:02.0 to 0:2:0)**
    **BusID "PCI:0:2:0"**
    Option "AccelMethod"  "none"
EndSection

Section "Screen"
    Identifier "intel"
    Device "intel"
EndSection

```

Next, add the following two lines to the beginning of your `~/.xinitrc`:

 `~/.xinitrc` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

Now reboot to load the drivers, and X should start.

If your display dpi is not correct add following line:

```
xrandr --dpi 96

```

If you get a black screen when starting X, make sure that there are no ampersands after the two `xrandr` commands in `~/.xinitrc`. If there are ampersands, it seems that the window manager can run before the `xrandr` commands finish executing, leading to a black screen.

If the black screen persists, see the [#Alternative configuration](#Alternative_configuration) below.

### Alternative configuration

If you experience Xorg-server crashes since release 1.17.1 with above configuration, modify the section for the Intel device in `/etc/X11/xorg.conf` as follows:

 `# nano /etc/X11/xorg.conf` 
```
Section "Device"
    Identifier  "intel"
    Driver      "modesetting"
    BusID       "PCI:0:2:0"
    Option      "AccelMethod"  "sna"
    #Option      "TearFree" "True"
    #Option      "Tiling" "True"
    #Option      "SwapbuffersWait" "True"
EndSection
```

As above, the `BusID` must match for the output of the *lspci* command. Search for the line with "VGA compatible controller", that contains something Intel. For example:

```
$ lspci |grep VGA
00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)

```

**Tip:** The three last commented out options may (without #) result in positive effects on the tearing, but exchange for some performance cost. Note the `TearFree` option may be used for `"sna"` acceleration only, see [Intel graphics](/index.php/Intel_graphics "Intel graphics"). You can use either `"sna"` or `"uxa"` in `"AccelMethod"` option. For further experimenting, a working `xorg.conf` from a Lenovo Ideapad Z50-70 59-432128 is here: [[2]](http://pastebin.com/tMtPz381).

If X starts but nothing appears on the screen, check if `/var/log/xorg.conf` contains a following line or similar:

 `/var/log/xorg.conf` 
```
[ 16112.937] (EE) Screen 1 deleted because of no matching config section.

```

If so, the problem may disappear when you change your ServerLayout section of `/etc/X11/xorg.conf`:

 `/etc/X11/xorg.conf` 
```
Section "ServerLayout"
    Identifier "layout"
    Screen **1** "nvidia"
    Inactive "intel"
EndSection

```

### Display Managers

If you are using a display manager then you will need to create or edit a display setup script for your display manager instead of using `~/.xinitrc`.

#### LightDM

For the [LightDM](/index.php/LightDM "LightDM") display manager:

 `/etc/lightdm/display_setup.sh` 
```
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

For the [SDDM](/index.php/SDDM "SDDM") display manager:

 `/usr/share/sddm/scripts/Xsetup` 
```
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

#### GDM

For the [GDM](/index.php/GDM "GDM") display manager create a new .desktop file:

 `/usr/share/gdm/greeter/autostart/display_setup.desktop` 
```
[Desktop Entry]
Type=Application
Name=Display setup
Exec=sh -c "xrandr --setprovideroutputsource modesetting NVIDIA-0; xrandr --auto"
NoDisplay=true
X-GNOME-AutoRestart=true

```

If it is not working, you must add a script to `/etc/X11/xinit/xinitrc.d` directory, as below:

 `/etc/X11/xinit/xinitrc.d/nvidia-optimus.sh` 
```
#!/bin/sh
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto

```

Then run:

```
# chmod +x /etc/X11/xinit/xinitrc.d/nvidia-optimus.sh

```

And make sure that GDM use [X as default backend](/index.php/GDM#Use_Xorg_backend "GDM").

#### KDM

For KDE's [KDM](/index.php/KDM "KDM"), add the xrandr lines into `/usr/share/config/kdm/Xsetup`.

### Checking 3D

You can check if the NVIDIA graphics are being used by installing [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) and running

```
$ glxinfo | grep NVIDIA

```

### Further Information

For more information, look at NVIDIA's official page on the topic [[3]](http://http.download.nvidia.com/XFree86/Linux-x86_64/340.32/README/randr14.html).

## Troubleshooting

### Tearing/Broken VSync

Unfortunately, this is an issue which currently has no solution, and is [known to NVIDIA](https://devtalk.nvidia.com/default/topic/775691/linux/vsync-issue-nvidia-prime-ux32vd-with-gt620-m-/).

### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

Add `rcutree.rcu_idle_gp_delay=1` to the kernel parameters. Original topic can be found [here](https://bbs.archlinux.org/viewtopic.php?id=169742).

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

### NVIDIA provider in xrandr does not have the Source Output capability

An example of this problem is the following:

```
$ xrand --listproviders
Provider 0: id: 0x261 cap: 0x0 crtcs: 4 outputs: 6 associated providers: 1 name:NVIDIA-0
Provider 1: id: 0x43 cap: 0xf, Source Output, Sink Output, Source Offload, Sink Offload crtcs: 3 outputs: 1 associated providers: 1 name:modesetting

```

This will prevent you from doing `xrandr --setprovideroutputsource X Y`. If this is the case for you, check if the `nvidia_drm` module is loaded. If not, and you have the [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) package installed, it might be blacklisting the nvidia modules and prevent all the modules from being loaded. In that case, try uninstalling [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) or manually load the `nvidia_drm` module.

## Using nouveau

The open-source [nouveau](/index.php/Nouveau "Nouveau") driver ([xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)) can dynamically switch with the Intel driver ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)) using a technology called PRIME. For more information, see the wiki article on [PRIME](/index.php/PRIME "PRIME").

## Using Bumblebee

If you wish to use Bumblebee, which will implement powersaving and some other useful features, see the wiki article on [Bumblebee](/index.php/Bumblebee "Bumblebee").