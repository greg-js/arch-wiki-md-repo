[nvidia-xrun](https://github.com/Witko/nvidia-xrun) is a utility to run separate X with discrete nvidia graphics. This solution offers a bit more complicated procedure but offers a full GPU utilization(in terms of linux drivers).

## Contents

*   [1 installation](#installation)
*   [2 configuration](#configuration)
    *   [2.1 Setting the right bus id](#Setting_the_right_bus_id)
    *   [2.2 Automatically run window manager](#Automatically_run_window_manager)
    *   [2.3 Use bbswitch to manage nvidia](#Use_bbswitch_to_manage_nvidia)
*   [3 usage](#usage)
*   [4 Troubleshooting](#Troubleshooting)

## installation

[Install](/index.php/Install "Install"):

*   [nvidia](https://www.archlinux.org/packages/?name=nvidia)
*   [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)
*   [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun/) or [nvidia-xrun-git](https://aur.archlinux.org/packages/nvidia-xrun-git/)
*   a [Window manager](/index.php/Window_manager "Window manager"), such as [openbox](https://www.archlinux.org/packages/?name=openbox) it only for running applications，becasue running some applications (such as Steam) directly with nvidia-xrun does not work well, use some window manager like openbox will be better.

## configuration

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

When do not need to use nvidia , use bbswitch to turn off it , and run application which need nvidia , nvidia-xrun will automatically run window manager and wake up nvidia.

*   Load bbswitch module when boot

```
 # echo 'bbswitch ' > /etc/modules-load.d/bbswitch

```

*   Disable the nvidia on boot time.

```
 # echo 'options bbswitch load_state=0' > /etc/modprobe.d/bbswitch.conf 

```

*   Blacklisting nvidia modules

```
$ lsmod | grep nvidia | cut -d ' ' -f 1 > /tmp/nvidia
$ lsmod | grep  nouveau | cut -d ' ' -f 1 > > /tmp/nvidia
$ sort -n /tmp/nvidia | uniq >  /tmp/nvidia.conf
$ sed -i 's/^\w*$/blacklist &/g' /tmp/nvidia.conf
# cp /tmp/nvidia.conf /etc/modprobe.d/nvidia.conf

```

Reboot system , nvidia will be off , you can geet the status:

```
 $ cat /proc/acpi/bbswitch  

```

turn the card off, respectively on:

```
 # tee /proc/acpi/bbswitch <<<OFF
 # tee /proc/acpi/bbswitch <<<ON

```

more about bbswitch see [Bumblebee-Project/bbswitch](https://github.com/Bumblebee-Project/bbswitch)

## usage

1.  switch to free tty
2.  login
3.  run `nvidia-xrun [app]`

## Troubleshooting

Running Steam directly with nvidia-xrun does not work well, use some window manager like openbox will be better.