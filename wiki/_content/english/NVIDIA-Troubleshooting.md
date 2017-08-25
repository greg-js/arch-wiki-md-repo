## Contents

*   [1 Corrupted screen: "Six screens" Problem](#Corrupted_screen:_.22Six_screens.22_Problem)
*   [2 '/dev/nvidia0' input/output error](#.27.2Fdev.2Fnvidia0.27_input.2Foutput_error)
*   [3 Crashing in general](#Crashing_in_general)
*   [4 Bad performance after installing a new driver version](#Bad_performance_after_installing_a_new_driver_version)
*   [5 Avoid screen tearing](#Avoid_screen_tearing)
    *   [5.1 Multi-monitor](#Multi-monitor)
    *   [5.2 Avoid screen tearing in KDE (KWin)](#Avoid_screen_tearing_in_KDE_.28KWin.29)
*   [6 Modprobe Error: "Could not insert 'nvidia': No such device" on linux >=4.8](#Modprobe_Error:_.22Could_not_insert_.27nvidia.27:_No_such_device.22_on_linux_.3E.3D4.8)
*   [7 Poor performance after resuming from suspend](#Poor_performance_after_resuming_from_suspend)
*   [8 CPU spikes with 400 series cards](#CPU_spikes_with_400_series_cards)
*   [9 Full system freeze or crashes when using Flash](#Full_system_freeze_or_crashes_when_using_Flash)
*   [10 Laptops: X hangs on login/out, worked around with Ctrl+Alt+Backspace](#Laptops:_X_hangs_on_login.2Fout.2C_worked_around_with_Ctrl.2BAlt.2BBackspace)
*   [11 Screen(s) found, but none have a usable configuration](#Screen.28s.29_found.2C_but_none_have_a_usable_configuration)
*   [12 Blackscreen at X startup / Machine poweroff at X shutdown](#Blackscreen_at_X_startup_.2F_Machine_poweroff_at_X_shutdown)
*   [13 Backlight is not turning off in some occasions](#Backlight_is_not_turning_off_in_some_occasions)
*   [14 Xorg fails to load or Red Screen of Death](#Xorg_fails_to_load_or_Red_Screen_of_Death)
*   [15 Black screen on systems with Intel integrated GPU](#Black_screen_on_systems_with_Intel_integrated_GPU)
*   [16 Black screen on systems with VIA integrated GPU](#Black_screen_on_systems_with_VIA_integrated_GPU)
*   [17 X fails with "no screens found" with Intel iGPU](#X_fails_with_.22no_screens_found.22_with_Intel_iGPU)
*   [18 Xorg fails during boot, but otherwise starts fine](#Xorg_fails_during_boot.2C_but_otherwise_starts_fine)
*   [19 xrandr BadMatch](#xrandr_BadMatch)
*   [20 Override EDID](#Override_EDID)
*   [21 Overclocking with nvidia-settings GUI not working](#Overclocking_with_nvidia-settings_GUI_not_working)

## Corrupted screen: "Six screens" Problem

For some users, using GeForce GT 100M's, the screen gets corrupted after X starts, divided into 6 sections with a resolution limited to 640x480. The same problem has been recently reported with Quadro 2000 and hi-res displays.

To solve this problem, enable the Validation Mode `NoTotalSizeCheck` in section `Device`:

```
Section "Device"
 ...
 Option "ModeValidation" "NoTotalSizeCheck"
 ...
EndSection

```

## '/dev/nvidia0' input/output error

This error can occur for several different reasons, and the most common solution given for this error is to check for group/file permissions, which in almost every case is *not* the problem. The NVIDIA documentation does not talk in detail on what you should do to correct this problem but there are a few things that have worked for some people. The problem can be a IRQ conflict with another device or bad routing by either the kernel or your BIOS.

First thing to try is to remove other video devices such as video capture cards and see if the problem goes away. If there are too many video processors on the same system it can lead into the kernel being unable to start them because of memory allocation problems with the video controller. In particular on systems with low video memory this can occur even if there is only one video processor. In such case you should find out the amount of your system's video memory (e.g. with `lspci -v`) and pass allocation parameters to the kernel, e.g. for a 32-bit kernel:

```
vmalloc=384M

```

If running a 64bit kernel, a driver defect can cause the NVIDIA module to fail initializing when IOMMU is on. Turning it off in the BIOS has been confirmed to work for some users. [[1]](http://www.nvnews.net/vbulletin/showthread.php?s=68bb2fabadcb53b10b286aa42d13c5bc&t=159335)[User:Clickthem#nvidia module](/index.php/User:Clickthem#nvidia_module "User:Clickthem")

Another thing to try is to change your BIOS IRQ routing from `Operating system controlled` to `BIOS controlled` or the other way around. The first one can be passed as a kernel parameter:

```
PCI=biosirq

```

The `noacpi` kernel parameter has also been suggested as a solution but since it disables ACPI completely it should be used with caution. Some hardware are easily damaged by overheating.

**Note:** The kernel parameters can be passed either through the kernel command line or the bootloader configuration file. See your bootloader Wiki page for more information.

## Crashing in general

*   Try disabling `RenderAccel` in xorg.conf.
*   If Xorg outputs an error about `"conflicting memory type"` or `"failed to allocate primary buffer: out of memory"`, or crashes with a "Signal 11" while using nvidia-96xx drivers, add `nopat` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").
*   If the NVIDIA compiler complains about different versions of GCC between the current one and the one used for compiling the kernel, add in `/etc/profile`:

```
export IGNORE_CC_MISMATCH=1

```

*   If Xorg is crashing , try disabling PAT. Pass the argument `nopat` to [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

More information about troubleshooting the driver can be found in the [NVIDIA forums.](https://forums.geforce.com/)

## Bad performance after installing a new driver version

If FPS have dropped in comparison with older drivers, check if direct rendering is enabled (`glxinfo` is included in [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)):

```
$ glxinfo | grep direct

```

If the command prints:

```
direct rendering: No

```

A possible solution could be to regress to the previously installed driver version and rebooting afterwards.

## Avoid screen tearing

**Note:** This has been reported to reduce the performance of some OpenGL applications and may produce issues in WebGL.

Tearing can be avoided by forcing a full composition pipeline, regardless of the compositor you are using. To test whether this option will work, run:

```
$ nvidia-settings --assign CurrentMetaMode="nvidia-auto-select +0+0 { ForceFullCompositionPipeline = On }"

```

Or click on the *Advanced* button that is available on the *X Server Display Configuration* menu option. Select either *Force Composition Pipeline* or *Force Full Composition Pipeline* and click on *Apply*.

In order to make the change permanent, it must be added to the `"Screen"` section of the [Xorg](/index.php/Xorg "Xorg") configuration file. When making this change, `TripleBuffering` should be enabled and `AllowIndirectGLXProtocol` should be disabled in the driver configuration as well. See example configuration below:

 `/etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
        Identifier "Nvidia Card"
        Driver     "nvidia"
        VendorName "NVIDIA Corporation"
        BoardName  "GeForce GTX 1050 Ti"
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    Option         "metamodes" "nvidia-auto-select +0+0 {ForceCompositionPipeline=On, ForceFullCompositionPipeline=On}"
    Option         "AllowIndirectGLXProtocol" "off"
    Option         "TripleBuffer" "on"
EndSection

```

If you do not have an Xorg configuration file, you can create one for your present hardware using `nvidia-xconfig` (see [NVIDIA#Automatic configuration](/index.php/NVIDIA#Automatic_configuration "NVIDIA")) and move it from `/etc/X11/xorg.conf` to the preferred location `/etc/X11/xorg.conf.d/20-nvidia.conf`.

**Note:** Many of the configuration options produced in `20-nvidia.conf` by using `nvidia-xconfig` are set automatically by the driver and are not needed. To only use this file for enabling composition pipeline, only the section `"Screen"` containing lines with values for `Identifier` and `Option` are necessary. Other sections may be removed from this file.

### Multi-monitor

For multi-monitor setup you will need to specify `ForceCompositionPipleline=On` for each display. For example:

```
$ nvidia-settings --assign CurrentMetaMode="DP-2: nvidia-auto-select +0+0 {ForceCompositionPipeline=On}, DP-4: nvidia-auto-select +3840+0 {ForceCompositionPipeline=On}"

```

Without doing this, the `nvidia-settings` command will disable your secondary display.

The above line is for two 3840x2160 monitors connected to DP-2 and DP-4\. You will need to read the correct `CurrentMetaMode` by exporting `xorg.conf` and append `ForceCompositionPipeline` to each of your displays. Setting `ForceCompositionPipeline` only affects the targeted display.

**Tip:** Multi monitor setups using different model monitors may have slightly different refresh rates. If vsync is enabled by the driver it will sync to only one of these refresh rates which can cause the appearance of screen tearing on incorrectly synced monitors. Select to sync the display device which is the primarily used monitor as others will not sync properly. This is configurable in `~/.nvidia-settings-rc` as `0/XVideoSyncToDisplayID=` or by installing [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) and using the graphical configuration options.

### Avoid screen tearing in KDE (KWin)

If `ForceFullCompositionPipeline` described above does not help:

 `/etc/profile.d/kwin.sh` 
```
export KWIN_TRIPLE_BUFFER=1

```

If you enable triple buffering make sure to enable `TripleBuffering` for the driver itself.

 `/etc/X11/xorg.conf or /etc/X11/xorg.conf.d/20-nvidia.conf` 
```
Section "Device"
    [...]
    Option         "TripleBuffer" "on"
    [...]
EndSection

```

Also make sure to select OpenGL >= 2.0 as rendering backend under *Systemsettings*, *Display and Monitor*, *Compositor*.

If the above does not help, then try this, however you could have huge performance loss in games since this option will put the GL threads to sleep:

 `/etc/profile.d/kwin.sh` 
```
export __GL_YIELD="USLEEP"

```

**Warning:** Do not have both of the above enabled at the same time [[2]](https://bugs.kde.org/show_bug.cgi?id=322060).

## Modprobe Error: "Could not insert 'nvidia': No such device" on linux >=4.8

With linux 4.8, one can get the following errors when trying to use the discrete card:

 `$ modprobe nvidia -vv` 
```
modprobe: INFO: custom logging function 0x409c10 registered
modprobe: INFO: Failed to insert module '/lib/modules/4.8.6-1-ARCH/extramodules/nvidia.ko.gz': No such device
modprobe: ERROR: could not insert 'nvidia': No such device
modprobe: INFO: context 0x24481e0 released
insmod /lib/modules/4.8.6-1-ARCH/extramodules/nvidia.ko.gz 

```
 `$ dmesg` 
```
...
NVRM: The NVIDIA GPU 0000:01:00.0 (PCI ID: 10de:139b)
NVRM: installed in this system is not supported by the 370.28
NVRM: NVIDIA Linux driver release.  Please see 'Appendix
NVRM: A - Supported NVIDIA GPU Products' in this release's
NVRM: README, available on the Linux driver download page
NVRM: at www.nvidia.com.
...

```

This problem is caused by bad commits pertaining to PCIe power management in the Linux Kernel (as documented in [this NVIDIA DevTalk thread](https://devtalk.nvidia.com/default/topic/971733/-370-28-with-kernel-4-8-on-gt-2015-machines-driver-claims-card-not-supported-if-nvidia-is-not-primary-card/)).

The workaround is to add `pcie_port_pm=off` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). Note that this disables PCIe power management for all devices.

## Poor performance after resuming from suspend

If you are getting poor performance after resuming from suspend, you need to register the nvidia kernel module with the ACPI subsystem. This can be done by [loading](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `nvidia` module with the `NVreg_RegisterForACPIEvents=1 NVreg_EnableMSI=1` options.

## CPU spikes with 400 series cards

If you are experiencing intermittent CPU spikes with a 400 series card, it may be caused by PowerMizer constantly changing the GPU's clock frequency. Switching PowerMizer's setting from Adaptive to Performance, add the following to the `Device` section of your Xorg configuration:

```
 Option "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"

```

## Full system freeze or crashes when using Flash

If you experience occasional full system freezes using [[[Flash]], a possible workaround is to disable Hardware Acceleration:

 `/etc/adobe/mms.cfg`  `EnableLinuxHWVideoDecode=0` 

Or, if you want to keep Hardware acceleration enabled but allowing a higher chance of screen tearing, you may try to before starting a browser:

```
export VDPAU_NVIDIA_NO_OVERLAY=1

```

## Laptops: X hangs on login/out, worked around with Ctrl+Alt+Backspace

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

## Screen(s) found, but none have a usable configuration

Sometimes NVIDIA and X have trouble finding the active screen. If your graphics card has multiple outputs try plugging your monitor into the other ones. On a laptop it may be because your graphics card has VGA/TV out. Xorg.0.log will provide more info.

Another thing to try is adding invalid `"ConnectedMonitor" Option` to `Section "Device"` to force Xorg throws error and shows you how correct it. [Here](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) more about ConnectedMonitor setting.

After re-run X see Xorg.0.log to get valid CRT-x,DFP-x,TV-x values.

`nvidia-xconfig --query-gpu-info` could be helpful.

## Blackscreen at X startup / Machine poweroff at X shutdown

If you have installed an update of Nvidia and your screen stays black after launching Xorg, or if shutting down Xorg causes a machine poweroff, try the below workarounds:

*   Use the `rcutree.rcu_idle_gp_delay=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

*   You can also try to add the `nvidia` module directly to your [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file.

*   If the screen still stays black with **both** the `rcutree.rcu_idle_gp_delay=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") and the `nvidia` module directly in the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") config file, try re-installing [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) in that order, and finally reload the driver:

```
# modprobe nvidia

```

## Backlight is not turning off in some occasions

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

## Xorg fails to load or Red Screen of Death

If you get a red screen and use GRUB, disable the GRUB framebuffer by editing `/etc/default/grub` and uncomment `GRUB_TERMINAL_OUTPUT=console`. For more information see [GRUB/Tips and tricks#Disable framebuffer](/index.php/GRUB/Tips_and_tricks#Disable_framebuffer "GRUB/Tips and tricks").

## Black screen on systems with Intel integrated GPU

If you have an Intel CPU with an integrated GPU (e.g. Intel HD 4000) and have installed the [nvidia](https://www.archlinux.org/packages/?name=nvidia) package, you may experience a black screen on boot, when changing virtual terminal, or when exiting an X session. This may be caused by a conflict between the graphics modules. This is solved by blacklisting the Intel GPU modules. Create the file `/etc/modprobe.d/blacklist.conf` and prevent the *i915* and *intel_agp* modules from loading on boot:

 `/etc/modprobe.d/blacklist.conf` 
```
install i915 /usr/bin/false
install intel_agp /usr/bin/false

```

## Black screen on systems with VIA integrated GPU

As above, blacklisting the *viafb* module may resolve conflicts with NVIDIA drivers:

 `/etc/modprobe.d/blacklist.conf` 
```
install viafb /usr/bin/false

```

## X fails with "no screens found" with Intel iGPU

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

## Xorg fails during boot, but otherwise starts fine

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

## xrandr BadMatch

If you are trying to configure a WQHD monitor such as DELL U2515H using [xrandr](/index.php/Xrandr "Xrandr") and `xrandr --addmode` gives you the error `X Error of failed request: BadMatch`, it might be because the proprietary NVIDIA driver clips the pixel clock maximum frequency of HDMI output to 225 MHz or lower. To set the monitor to maximum resolution you have to install [nouveau](/index.php/Nouveau "Nouveau") drivers. You can force nouveau to use a specific pixel clock frequency by setting `nouveau.hdmimhz=297` (or `330`) in your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

Alternatively, it may be that your monitor's EDID is incorrect. See [#Override EDID](#Override_EDID).

## Override EDID

**Note:** See [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") for more information.

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

Alternatively, it may be that your monitor's EDID is actually correct and the driver does not trust it. To force it to use the EDID anyway, set the `IgnoreEDIDChecksum` option for the X11 Device.

**Warning:** If the EDID is actually incorrect, ignoring the checksum could cause hardware damage. Only attempt this if you know for a fact that the monitor's mode is correctly detected in some case (e.g. different OS, different driver, different output).

```
Section "Device"
    Identifier "Device0"
    Driver "nvidia"
    Option "IgnoreEDIDChecksum" "*displayName*"
EndSection
```

where `*displayName*` is the name of the display device e.g. `DFP-4`. You can find the display device name in your Xorg log; it is *not* the same as the output name (e.g. `DVI-I-0`) that you would see in [Xrandr](/index.php/Xrandr "Xrandr") output.

## Overclocking with nvidia-settings GUI not working

Workaround is to use nvidia-settings CLI to query and set certain variables after enabling overclocking(as explained in [NVIDIA/Tips and tricks#Enabling overclocking](/index.php/NVIDIA/Tips_and_tricks#Enabling_overclocking "NVIDIA/Tips and tricks"). `man nvidia-settings` for more information.

Example to query all variables:

```
 nvidia-settings -q all

```

Example to set PowerMizerMode to prefer performance mode:

```
 nvidia-settings -a [gpu:0]/GPUPowerMizerMode=1

```

Example to set multiple variables at once(Overclock on performance level [3] by 50Mhz, overclock MemoryTransferRate by 50Mhz, Over Voltage by 100 microvolts)

```
 nvidia-setting -a GPUGraphicsClockOffset[3]=50 -a GPUMemoryTransferRateOffset[3]=50 -a GPUOverVoltageOffset=100

```