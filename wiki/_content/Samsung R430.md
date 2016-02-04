# Samsung R430

This page aims to provide as much information as possible to make the Samsung R430 laptop work. There are many variations of the hardware of the unit, so if you had to do something not listed here, please add it.

## Contents

*   [1 Hardware Specification](#Hardware_Specification)
*   [2 Installation](#Installation)
*   [3 Audio](#Audio)
*   [4 Touchpad](#Touchpad)
*   [5 Wireless](#Wireless)
*   [6 Screen brightness](#Screen_brightness)
*   [7 Enable and disable featues](#Enable_and_disable_featues)

## Hardware Specification

*   **Video:** NVIDIA 310M
*   **WLAN:** Atheros AR9285
*   **CPU:** Intel Core 2 Duo T6600
*   **LAN:** Marvell 88E8040 PCI-E Ethernet
*   **Soundcard:** Realtek ALC269 (NVIDIA Chipset)

## Installation

Actual instalation works without trouble

## Audio

Works nicely

## Touchpad

It's supposed to be multitouch, and works that way in windows, but activating two-finger scroll doesn't do anything.

## Wireless

Works out of the box

## Screen brightness

To enable screen brightness, you need to install and activate the kernel module [nvidia-bl](https://aur.archlinux.org/packages/nvidia-bl/) from the AUR. It needs some options tweaked however, so edit **/etc/modprobe.d/modprobe.conf** to contain:

```
options nvidia-bl max_level=131071 shift=9

```

In different models or with different video cards this might not work, so I'll now explain how to get to those values.

max_level is a number one less than a power of 2\. to find the ideal one for your laptop just load it with a value (the default is 2047), like

```
 # modprobe nvidia-bl max_level=level

```

and, if it isn't bright enough, try with the next number, not without unloading the module first:

```
 # rmmod nvidia-bl

```

The shift parameter bit-shifts the brightness values, as to make it a sane number. The recomended is to make it so max_level is 256, so it can be calculated by adding one to the max_value (getting a power of two), then calculat[[ing the base 2 logarithm of that, and substracting 8 from the result.

finally, you have to load the module, to do this, just issue

```
 # modprobe nvidia-bl

```

To load it automatically at boot, add a `nvidia-bl.conf` file containing the line `nvidia-bl` to the directory `/etc/modules.d` as described in [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules").

The brightness level can then be set by writing the desired value to **/sys/class/backlight/nvidia_backlight/brightness**

## Enable and disable featues

To be able to activate and deactivate features such as the touchpad or the wireless card, you need to install the kernel module [easy-slow-down-manager](https://aur.archlinux.org/packages/easy-slow-down-manager/). It's very simple to use and the usage is described in **/usr/share/doc/easy-slow-down-manager/README**.

Obviously, like before, you need to load the module for it to work, either by using modprobe, like **modprobe easy-slow-down-manager** (might need a reboot to work for the first time), or adding a `easy-slow-down-manager.conf` file to `/etc/modules-load.d`.

To make managing the features of the notebook easier, you can install [samsung-tools](https://aur.archlinux.org/packages/samsung-tools/). Just install it and follow the instructions given by the install script.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samsung_R430&oldid=392651](https://wiki.archlinux.org/index.php?title=Samsung_R430&oldid=392651)"