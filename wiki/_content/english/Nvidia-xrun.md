[nvidia-xrun](https://github.com/Witko/nvidia-xrun) is a utility to run separate X with discrete nvidia graphics. This solution offers a bit more complicated procedure but offers a full GPU utilization(in terms of linux drivers).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setting the right bus id](#Setting_the_right_bus_id)
    *   [2.2 Automatically run window manager](#Automatically_run_window_manager)
    *   [2.3 Use bbswitch to manage nvidia](#Use_bbswitch_to_manage_nvidia)
*   [3 Usage](#Usage)
*   [4 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install"):

*   [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)
*   [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/), [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/), or [nvidia-xrun-pm](https://aur.archlinux.org/packages/nvidia-xrun-pm/) if bbswitch doesn't support your hardware (see [[1]](https://bbs.archlinux.org/viewtopic.php?id=238389))
*   a [Window manager](/index.php/Window_manager "Window manager"), such as [openbox](https://www.archlinux.org/packages/?name=openbox) if only for running applications，because running some applications (such as Steam) directly with *nvidia-xrun* does not work well, using a window manager like [openbox](/index.php/Openbox "Openbox") will work better.

## Configuration

### Setting the right bus id

Users who installed `nvidia-xrun` from the [AUR](/index.php/AUR "AUR") can skip this step, because the bus id has been automatically set in `/etc/X11/nvidia-xorg.conf`. However, if you installed it from [Github repo](https://github.com/Witko/nvidia-xrun), you might need to set the bus id manually.

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
nvidia-xrun

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

1.  switch to free tty
2.  login
3.  run `nvidia-xrun [app]`

## Troubleshooting

Running Steam directly with *nvidia-xrun* does not work well, usage via a window manager, like openbox, will be better.