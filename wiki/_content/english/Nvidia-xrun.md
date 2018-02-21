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
*   [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/) or [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/)
*   a [Window manager](/index.php/Window_manager "Window manager"), such as [openbox](https://www.archlinux.org/packages/?name=openbox) it only for running applications，becasue running some applications (such as Steam) directly with nvidia-xrun does not work well, use some window manager like openbox will be better.

## Configuration

### Setting the right bus id

If you install nvidia-xrun from [AUR](/index.php/AUR "AUR"),you can skip this step,the bus id has been already setted in `/etc/X11/nvidia-xorg.conf`

If you down nvidia-xrun form [nvidia-xrun github repo],perhaps you should set the bus id.

check your display device's bus id

```
 $ lspci | grep NVIDIA

```

You will find your bus id.Usually the 1:0:0 bus is correct. If this is not your case(you can find out through lspci or bbswitch output mesages) you can create a conf script for example nano /etc/X11/nvidia-xorg.conf.d/30-nvidia.conf to set the proper bus id:

 `/etc/X11/nvidia-xorg.conf.d/30-nvidia.conf` 
```
Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:2:0:0"
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

For convenience you can create nano ~/.nvidia-xinitrc and put there your favourite window manager:

```
 openbox-session

```

With this you do not need to specify the app and you can simply run:

```
 nvidia-xrun

```

### Use bbswitch to manage nvidia

When the nvidia card is not needed, bbswitch can be used to turn it off. The nvidia-xrun script will automatically take care of running a window manager and waking up the nvidia card. To achieve that, you need to:

*   Load bbswitch module on boot

```
 # echo 'bbswitch ' > /etc/modules-load.d/bbswitch.conf

```

*   Disable the nvidia module on boot:

```
 # echo 'options bbswitch load_state=0 unload_state=1' > /etc/modprobe.d/bbswitch.conf 

```

After a reebot, the nvidia card will be off. This can bee seen by querying bbswitch's status:

```
 $ cat /proc/acpi/bbswitch  

```

To force the card to turn on/off respectively run:

```
 # tee /proc/acpi/bbswitch <<<OFF
 # tee /proc/acpi/bbswitch <<<ON

```

For more about bbswitch see [Bumblebee-Project/bbswitch](https://github.com/Bumblebee-Project/bbswitch)

## Usage

1.  switch to free tty
2.  login
3.  run `nvidia-xrun [app]`

## Troubleshooting

Running Steam directly with nvidia-xrun does not work well, use some window manager like openbox will be better.