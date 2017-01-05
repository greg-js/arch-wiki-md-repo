This article documents configuration and troubleshooting specific to the Alienware 13 laptop.

See the [Installation guide](/index.php/Installation_guide "Installation guide") for general installation instructions.

## Contents

*   [1 Getting Linux to boot](#Getting_Linux_to_boot)
*   [2 Touchpad](#Touchpad)
*   [3 Wireless](#Wireless)
*   [4 Switchable graphics](#Switchable_graphics)
*   [5 Keyboard Lights](#Keyboard_Lights)

## Getting Linux to boot

First of all we must create a [bootable usb](/index.php/USB_flash_installation_media "USB flash installation media"), after that we must reboot the computer and press `F12` button while the bios is loading to access to the boot menu, from there we select the USB and boot from there.

The first issue that we can find is that the distribution does not boot but gets stuck into a nouveau loop or a black screen. If this happens, we must change the kernel parameters to get ArchLinux to boot. Try to erase all default parameters and use only `nomodeset`.

## Touchpad

If the touchpad does not work, try to unload the `i2c_hid` module:

```
# modprobe -r i2c_hid

```

and restart the graphical environment. If that helps, consider [blacklisting](/index.php/Blacklist "Blacklist") the module.

## Wireless

At the moment of writing this, the wifi network of the Alienware13 is a Atheros Qualcomm Killer N1525, which is not configured by the default installation.

```
$ lspci
...
01:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 20)
02:00.0 Ethernet controller: Qualcomm Atheros Killer E220x Gigabit Ethernet Controller (rev 10)
...

```

Here is the [ubuntu bug](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1383184).

Fortunately, the enclosed patch is able to get it to work. It was tested on Kernel 4.2.5-1 as follows:

```
$ git clone [https://github.com/sumdog/ath10k-firmware](https://github.com/sumdog/ath10k-firmware)
# cp -a ath10k-firmware/ath10k/QCA6174 /lib/firmware/ath10k/QCA6174
# echo "options ath10k_core skip_otp=y" | tee -a /etc/modprobe.d/ath10k.conf

```

After a reboot, wireless should work, including wifi-ac speeds.

## Switchable graphics

To have switchable graphics see [bumblebee](/index.php/Bumblebee "Bumblebee") instructions. The utility is able to turn on and off the dedicated graphics card ondemand and without having to restart the computer or reopening session.

At the time of writing the Nvidia graphic chip was not yet recognised by the Nouveau driver, so you need to follow [Installing Bumblebee with Intel and NVIDIA](/index.php/Bumblebee#Installing_Bumblebee_with_Intel.2FNVIDIA "Bumblebee") for the functionality for now.

The following (with dependencies) was installed for the example machine:

```
# pacman -S bumblebee xf86-video-intel dkms bbswitch nvidia primus mesa-demos

```

After finishing setup and a reboot, the dedicated graphics card should be off. To check:

```
$ optirun --status
Bumblebee status: Ready (3.2.1). X inactive. Discrete video card is on.

```

And we can make use of it by calling *primusrun* or *optirun* before the program we want to run; for example:

```
$ glxspheres64
...
OpenGL Renderer: Mesa DRI Intel(R) HD Graphics 5500 (Broadwell GT2) 
60.004917 frames/sec - 28.911809 Mpixels/sec
...

$ primusrun glxspheres64
...
OpenGL Renderer: GeForce GTX 860M/PCIe/SSE2
61.130011 frames/sec - 68.221092 Mpixels/sec
...

```

With this we have the graphics card working ondemand

## Keyboard Lights

To get access to the keyboard lights they can be controlling by sending data to the correct usb.

```
 $ lsusb
 ...
 Bus 002 Device 003: ID 187c:0527 Alienware Corporation 
 ...

```

There plenty of programs like pyAlienFX or [Alienware-KBL](https://rafael.senties-martinelli.com/software/alienware-kbl) and none of these worked for me, but there is a github project that consists on sending data to USB using `libusb` that worked fine.

```
 git clone [https://github.com/snooze6/hack-alienfx](https://github.com/snooze6/hack-alienfx)
 make all

```

In case of a compilation error similar to `"FILE is not defined"`, try adding a `stdio.h include` to the following:

 `/usr/include/readline/rltypedefs.h` 
```
# Add
#include <stdio.h>
```

And try compilation again.

Once it is compiled, test by running:

```
 # ./run seq/snooze

```

and keyboard lights should work.

To register it as a command and can use this program without being root we can do the next:

```
 # cp run /usr/local/bin/
 # mkdir /usr/local/fx
 # cp seq/* /usr/local/fx
 # chmod 4755 /bin/fx
 # cp lights.sh /usr/local/bin/lights
 # chmod +x /usr/local/bin/lights

```

Now it should trigger by executing:

```
 $ lights
 $ lights on
 $ lights off

```

from a console.

We can simply add the commands to the energy admin or the startup to make keyboard lights change automatically.