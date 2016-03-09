See [NVIDIA](/index.php/NVIDIA "NVIDIA") for the main article.

## Contents

*   [1 Fixing terminal resolution](#Fixing_terminal_resolution)
*   [2 Using TV-out](#Using_TV-out)
*   [3 X with a TV (DFP) as the only display](#X_with_a_TV_.28DFP.29_as_the_only_display)
*   [4 Check the power source](#Check_the_power_source)
*   [5 Listening to ACPI events](#Listening_to_ACPI_events)
*   [6 Displaying GPU temperature in the shell](#Displaying_GPU_temperature_in_the_shell)
    *   [6.1 Method 1 - nvidia-settings](#Method_1_-_nvidia-settings)
    *   [6.2 Method 2 - nvidia-smi](#Method_2_-_nvidia-smi)
    *   [6.3 Method 3 - nvclock](#Method_3_-_nvclock)
*   [7 Set fan speed at login](#Set_fan_speed_at_login)
*   [8 Switching between NVIDIA and nouveau drivers](#Switching_between_NVIDIA_and_nouveau_drivers)
*   [9 Avoid tearing with GeForce 500/600/700/900 series cards](#Avoid_tearing_with_GeForce_500.2F600.2F700.2F900_series_cards)
*   [10 Manual configuration](#Manual_configuration)
    *   [10.1 Disabling the logo on startup](#Disabling_the_logo_on_startup)
    *   [10.2 Overriding monitor detection](#Overriding_monitor_detection)
    *   [10.3 Enabling brightness control](#Enabling_brightness_control)
    *   [10.4 Enabling SLI](#Enabling_SLI)
    *   [10.5 Enabling overclocking](#Enabling_overclocking)
        *   [10.5.1 Setting static 2D/3D clocks](#Setting_static_2D.2F3D_clocks)

## Fixing terminal resolution

Transitioning from nouveau may cause your startup terminal to display at a lower resolution. For GRUB, see [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks") for details.

## Using TV-out

A good article on the subject can be found [here](http://en.wikibooks.org/wiki/NVidia/TV-OUT).

## X with a TV (DFP) as the only display

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

## Check the power source

The NVIDIA X.org driver can also be used to detect the GPU's current source of power. To see the current power source, check the 'GPUPowerSource' read-only parameter (0 - AC, 1 - battery):

 `$ nvidia-settings -q GPUPowerSource -t`  `1` 

## Listening to ACPI events

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

## Displaying GPU temperature in the shell

### Method 1 - nvidia-settings

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

### Method 2 - nvidia-smi

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

====NVSMI LOG====

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

### Method 3 - nvclock

Use [nvclock](https://aur.archlinux.org/packages/nvclock/) which is available from the [AUR](/index.php/AUR "AUR").

**Note:** `nvclock` cannot access thermal sensors on newer NVIDIA cards such as Geforce 200 series cards.

There can be significant differences between the temperatures reported by nvclock and nvidia-settings/nv-control. According to [this post](http://sourceforge.net/projects/nvclock/forums/forum/67426/topic/1906899) by the author (thunderbird) of nvclock, the nvclock values should be more accurate.

## Set fan speed at login

You can adjust the fan speed on your graphics card with *nvidia-settings'* console interface. First ensure that your Xorg configuration sets the Coolbits option to `4`, `5` or `12` for fermi and above in your `Device` section to enable fan control.

```
Option "Coolbits" "4"

```

**Note:** GeForce 400/500 series cards cannot currently set fan speeds at login using this method. This method only allows for the setting of fan speeds within the current X session by way of nvidia-settings.

Place the following line in your [xinitrc](/index.php/Xinitrc "Xinitrc") file to adjust the fan when you launch Xorg. Replace `*n*` with the fan speed percentage you want to set.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"

```

You can also configure a second GPU by incrementing the GPU and fan number.

```
nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*" \
                -a "[gpu:1]/GPUFanControlState=1" -a  [fan:1]/GPUCurrentFanSpeed=*n*" &

```

If you use a login manager such as GDM or KDM, you can create a desktop entry file to process this setting. Create `~/.config/autostart/nvidia-fan-speed.desktop` and place this text inside it. Again, change `*n*` to the speed percentage you want.

```
[Desktop Entry]
Type=Application
Exec=nvidia-settings -a "[gpu:0]/GPUFanControlState=1" -a "[fan:0]/GPUCurrentFanSpeed=*n*"
X-GNOME-Autostart-enabled=true
Name=nvidia-fan-speed

```

**Note:** Since the drivers version 349.16, `GPUCurrentFanSpeed` has to be replaced with `GPUTargetFanSpeed`.[[1]](https://devtalk.nvidia.com/default/topic/821563/linux/can-t-control-fan-speed-with-beta-driver-349-12/post/4526208/#4526208)

## Switching between NVIDIA and nouveau drivers

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

## Avoid tearing with GeForce 500/600/700/900 series cards

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

## Manual configuration

Several tweaks (which cannot be enabled [automatically](#Automatic_configuration) or with the [GUI](#NVIDIA_Settings)) can be performed by editing your [config](#Configuring) file. The Xorg server will need to be restarted before any changes are applied.

See [NVIDIA Accelerated Linux Graphics Driver README and Installation Guide](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/README.txt) for additional details and options.

### Disabling the logo on startup

Add the `"NoLogo"` option under section `Device`:

```
Option "NoLogo" "1"

```

### Overriding monitor detection

The `"ConnectedMonitor"` option under section `Device` allows to override monitor detection when X server starts, which may save a significant amount of time at start up. The available options are: `"CRT"` for analog connections, `"DFP"` for digital monitors and `"TV"` for televisions.

The following statement forces the NVIDIA driver to bypass startup checks and recognize the monitor as DFP:

```
Option "ConnectedMonitor" "DFP"

```

**Note:** Use "CRT" for all analog 15 pin VGA connections, even if the display is a flat panel. "DFP" is intended for DVI, HDMI, or DisplayPort digital connections only.

### Enabling brightness control

Add under section `Device`:

```
Option "RegistryDwords" "EnableBrightnessControl=1"

```

If brightness control still does not work with this option, try installing [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) or [nvidiabl](https://aur.archlinux.org/packages/nvidiabl/).

### Enabling SLI

**Warning:** As of May 7, 2011, you may experience sluggish video performance in GNOME 3 after enabling SLI.

Taken from the NVIDIA driver's [README](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html) Appendix B: *This option controls the configuration of SLI rendering in supported configurations.* A "supported configuration" is a computer equipped with an SLI-Certified Motherboard and 2 or 3 SLI-Certified GeForce GPUs. See NVIDIA's [SLI Zone](http://www.slizone.com/page/home.html) for more information.

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

### Enabling overclocking

**Warning:** Please note that overclocking may damage hardware and that no responsibility may be placed on the authors of this page due to any damage to any information technology equipment from operating products out of specifications set by the manufacturer.

Overclocking is controlled via *Coolbits* option in the `Device` section, which enables various unsupported features:

```
Option "Coolbits" "*value*"

```

**Tip:** The *Coolbits* option can be easily controlled with the *nvidia-xconfig*, which manipulates the Xorg configuration files: `# nvidia-xconfig --cool-bits=*value*` 

The *Coolbits* value is the sum of its component bits in the binary numeral system. The component bits are:

*   `1` (bit 0) - Enables overclocking of older (pre-Fermi) cores on the *Clock Frequencies* page in *nvidia-settings*.
*   `2` (bit 1) - When this bit is set, the driver will "attempt to initialize SLI when using GPUs with different amounts of video memory".
*   `4` (bit 2) - Enables manual configuration of GPU fan speed on the *Thermal Monitor* page in *nvidia-settings*.
*   `8` (bit 3) - Enables overclocking on the *PowerMizer* page in *nvidia-settings*. Available since version 337.12 for the Fermi architecture and newer.[[2]](http://www.phoronix.com/scan.php?px=MTY1OTM&page=news_item)
*   `16` (bit 4) - Enables overvoltage using *nvidia-settings* CLI options. Available since version 346.16 for the Fermi architecture and newer.[[3]](http://www.phoronix.com/scan.php?page=news_item&px=MTg0MDI)

To enable multiple features, add the *Coolbits* values together. For example, to enable overclocking and overvoltage of Fermi cores, set `Option "Coolbits" "24"`.

The documentation of *Coolbits* can be found in `/usr/share/doc/nvidia/html/xconfigoptions.html`. Driver version 346.16 documentation on *Coolbits* can be found online [here](ftp://download.nvidia.com/XFree86/Linux-x86/355.11/README/xconfigoptions.html).

**Note:** An alternative is to edit and reflash the GPU BIOS either under DOS (preferred), or within a Win32 environment by way of [nvflash](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,127/orderby,2/page,1/) and [NiBiTor 6.0](http://www.mvktech.net/component/option,com_remository/Itemid,26/func,select/id,135/orderby,2/page,1/). The advantage of BIOS flashing is that not only can voltage limits be raised, but stability is generally improved over software overclocking methods such as Coolbits. [Fermi BIOS modification tutorial](http://ivanvojtko.blogspot.sk/2014/03/how-to-overclock-geforce-460gtx-fermi.html)

#### Setting static 2D/3D clocks

Set the following string in the `Device` section to enable PowerMizer at its maximum performance level (VSync will not work without this line):

```
Option "RegistryDwords" "PerfLevelSrc=0x2222"

```