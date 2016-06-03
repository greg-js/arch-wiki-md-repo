This wiki page documents the configuration and troubleshooting specific to the Alienware13 laptop.

See the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") for installation instructions.

## Contents

*   [1 Getting Linux to boot](#Getting_Linux_to_boot)
*   [2 Touchpad](#Touchpad)
*   [3 Wifi](#Wifi)
*   [4 Switchable graphics](#Switchable_graphics)
*   [5 Keyboard Lights](#Keyboard_Lights)

## Getting Linux to boot

First of all we must create a [bootable usb](/index.php/USB_flash_installation_media "USB flash installation media"), after that we must reboot the computer and press F12 button while the bios is loading to access to the boot menu, from there we select the USB and boot from there.

The first issue that we can find is that the distribution not boots and gets stuck into a nouveau loop or a black screen; if this happens we must change the kernel parameters to get ArchLinux to boot; in my case I erase all the default parameters and put only "nomodeset" with only this parameter I was able to get ArchLinux to boot.

Note than this might not be necessary as the kernel is being continuously developed and updated.

From now on we must have ArchLinux booted and we only have to install it normally

## Touchpad

After we install a graphic interface we can appreciate that the touchpad of the computer is not working, so the easy fix is to blacklist "i2c_hid".

```
 echo "blacklist i2c_hid" | sudo tee -a /etc/modprobe.d/blacklist.conf

```

See more about [blacklisting](/index.php/Blacklisting "Blacklisting").

## Wifi

At the moment of writing this, the wifi network of the Alienware13 is a Atheros Qualcomm Killer N1525, which is not configured by the default installation

```
 $lspci
 ...
 01:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 20)
 02:00.0 Ethernet controller: Qualcomm Atheros Killer E220x Gigabit Ethernet Controller (rev 10)
 ...

```

Here is the [ubuntu bug](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1383184)

Fortunately for us they have a patch that is able to get it to work (Tested on 4.2.5-1)

```
 git clone [https://github.com/sumdog/ath10k-firmware](https://github.com/sumdog/ath10k-firmware)
 sudo cp -a ath10k-firmware/ath10k/QCA6174 /lib/firmware/ath10k/QCA6174
 echo "options ath10k_core skip_otp=y" | sudo tee -a /etc/modprobe.d/ath10k.conf

```

So we copy the QCA6174 files to a folder into our /lib/firmware called ath10k (create if not exists) and we write "options ath10k_core skip_otp=y" to the file /etc/modprobe.d/ath10k.conf (also create if not exists).

After a reboot we should be able to see wireless networks (It's compatible with the new standard wifi-ac reaching speeds of 200Mb/s in a 200Mb/s Internet connection)

## Switchable graphics

To have switchable graphics working we must use the [bumblebee](/index.php/Bumblebee "Bumblebee") utility that is able to turn on and off our dedicated graphics card ondemand and without having to restart the computer or reopening session.

```
 sudo pacman -S bumblebee mesa xf86-video-intel lib32-virtualgl lib32-nvidia-utils dkms bbswitch lib32-mesa-libgl nvidia primus mesa-demos
 sudo gpasswd -a $USER bumblebee
 sudo systemctl enable bumblebeed.service
 sudo systemctl enable dkms

```

```
 nano /etc/modprobe.d/bbswitch.conf
   # Make sure that this line is present
   options bbswitch load_state=0 unload_state=1

```

After a reboot we should have the dedicated graphics card off. We can check it by doing this:

```
 optirun --status

   Bumblebee status: Ready (3.2.1). X inactive. Discrete video card is on.

```

And we can make use of it by calling primusrun or optirun before the program we want to run; for example:

```
 $ glxspheres64
 Polygons in scene: 62464 (61 spheres * 1024 polys/spheres)
 Visual ID of window: 0x99
 Context is Direct
 OpenGL Renderer: Mesa DRI Intel(R) HD Graphics 5500 (Broadwell GT2) 
 60.004917 frames/sec - 28.911809 Mpixels/sec
 ...

 $ primusrun glxspheres64
 Polygons in scene: 62464 (61 spheres * 1024 polys/spheres)
 Visual ID of window: 0x99
 Context is Direct
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

There plenty of programs like pyAlienFX or Alienware-kbl and none of these worked for me but there's a github project that consists on sending data to the usb using libusb that worked fine.

```
 git clone [https://github.com/snooze6/hack-alienfx](https://github.com/snooze6/hack-alienfx)
 make all

```

If we have some kind of compilation error that says that FILE is not defined or something like this we can edit /usr/include/readline/rltypedefs.h and add the stdio.h include:

```
 nano /usr/include/readline/rltypedefs.h
   # Add
   #include <stdio.h>

```

And now it must compile fine

Once it's compiled we can do this:

```
 sudo ./run seq/snooze
 # Some lights in the keyboard now

```

So this program basically reads a file that has a theme coded in it and send this data to the usb changing keyboard lights.

To register this as a command and can use this program without being root we can do the next:

```
 sudo cp run /bin/
 sudo mkdir /usr/fx
 sudo cp seq/* /usr/fx
 sudo sudo chmod 4755 /bin/fx
 cp lights.sh /usr/bin/lights
 chmod +x /usr/bin/lights

```

So we can do simply

```
 lights
 lights on
 lights off

```

Controlling the keyboard from the terminal.

We can simply add this commands to the energy admin or the startup to make keyboard lights change automatically