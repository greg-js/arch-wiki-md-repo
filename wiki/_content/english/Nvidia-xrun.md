[Nvidia-xrun](https://github.com/Witko/nvidia-xrun) is a utility to allow Nvidia optimus enabled laptops run [X server](/index.php/X_server "X server") with discrete nvidia graphics on demand. This solution offers full GPU utilization, compatibility and better performance than [Bumblebee](/index.php/Bumblebee "Bumblebee").

X server can only be used with integrated graphics or discrete Nvidia graphics, but not both, so user might want to switch to separate [virtual console](/index.php/Linux_console "Linux console") and start another X server using different graphics from what was used for the first X server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setting the right bus id](#Setting_the_right_bus_id)
    *   [2.2 Automatically run window manager](#Automatically_run_window_manager)
    *   [2.3 Use bbswitch to manage nvidia](#Use_bbswitch_to_manage_nvidia)
*   [3 Usage](#Usage)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 General issues](#General_issues)
    *   [4.2 Issues with Nvidia after removing Bumblebee](#Issues_with_Nvidia_after_removing_Bumblebee)

## Installation

[Install](/index.php/Install "Install"):

*   [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)
*   [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/), [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/), or [nvidia-xrun-pm](https://aur.archlinux.org/packages/nvidia-xrun-pm/) if bbswitch doesn't support your hardware (see [[1]](https://bbs.archlinux.org/viewtopic.php?id=238389))
*   a [Window manager](/index.php/Window_manager "Window manager"), such as [openbox](https://www.archlinux.org/packages/?name=openbox) if only for running applications，because running some applications (such as Steam) directly with *nvidia-xrun* does not work well, using a window manager like [openbox](/index.php/Openbox "Openbox") will work better.

## Configuration

### Setting the right bus id

**Note:** Users who installed `nvidia-xrun` from the [AUR](/index.php/AUR "AUR") can skip this step, because the bus id has been automatically set in `/etc/X11/nvidia-xorg.conf`.

Find your display device bus id:

```
 $ lspci | grep -i nvidia | awk '{print $1}'

```

It might return something similar to **`01:00.0`**. Then create a script (for example `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf`) to set the proper bus id:

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:**1:0:0**"
EndSection
```

Also this way you can adjust some nvidia settings if you encounter issues:

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Screen"
    Identifier "nvidia"
    Device "nvidia"
    #  Option "AllowEmptyInitialConfiguration" "Yes"
    #  Option "UseDisplayDevice" "none"
EndSection
```

### Automatically run window manager

For convenience you can create an `~/.nvidia-xinitrc` file with your favourite window manager:

```
openbox-session

```

With it you do not need to specify the app and can simply execute:

```
$ nvidia-xrun

```

### Use bbswitch to manage nvidia

When the nvidia card is not needed, *bbswitch* can be used to turn it off. The *nvidia-xrun* script will automatically take care of running a window manager and waking up the nvidia card. To achieve that, you need to:

*   Load bbswitch module on boot

```
 # echo 'bbswitch ' > /etc/modules-load.d/bbswitch.conf

```

*   Disable the nvidia module on boot:

```
 # echo 'options bbswitch load_state=0 unload_state=1' > /etc/modprobe.d/bbswitch.conf 

```

After a reboot, the nvidia card will be off. This can be seen by querying bbswitch's status:

```
 $ cat /proc/acpi/bbswitch  

```

To force the card to turn on/off respectively run:

```
 # tee /proc/acpi/bbswitch <<<OFF
 # tee /proc/acpi/bbswitch <<<ON

```

For more about bbswitch see [Bumblebee-Project/bbswitch](https://github.com/Bumblebee-Project/bbswitch).

## Usage

Once system boots, from virtual console login to your user and run `nvidia-xrun <application>`.

If above does not work, [switch](/index.php/Keyboard_shortcuts#Xorg_and_Wayland "Keyboard shortcuts") to unused virtual console and try again.

## Troubleshooting

### General issues

Running apps directly with `nvidia-xrun <application>` does not work well. Use window manager like [openbox](https://www.archlinux.org/packages/?name=openbox) and run apps from it.

### Issues with Nvidia after removing Bumblebee

See [#Use bbswitch to manage nvidia](#Use_bbswitch_to_manage_nvidia).

If Nvidia GPU still fails to switch off, or is somehow set to be default whenever you use or not `nvidia-xrun`, then you might likely need to blacklist specific modules (which were previously blacklisted by [Bumblebee](/index.php/Bumblebee "Bumblebee")). Create this file and restart your system:

 `/usr/lib/modprobe.d/nvidia-xrun.conf` 
```
blacklist nvidia
blacklist nvidia-drm
blacklist nvidia-modeset
blacklist nvidia-uv
blacklist nvidia_uvm
blacklist nouveau

```

Make sure DRM kernel mode setting is disabled see [NVIDIA#DRM kernel mode setting](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA")