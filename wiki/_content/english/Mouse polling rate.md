If you have invested in a high resolution mouse, adjusting the USB polling rate is a common trick to utilize the added precision it brings. The polling rate (or report rate) determines how often the mouse sends information to your computer.

## Contents

*   [1 Polling rate and polling interval](#Polling_rate_and_polling_interval)
*   [2 Display polling rate](#Display_polling_rate)
*   [3 Display polling interval](#Display_polling_interval)
*   [4 USB device speed](#USB_device_speed)
*   [5 Set polling interval](#Set_polling_interval)
*   [6 See also](#See_also)

## Polling rate and polling interval

The polling rate of a device is measured in Hertz (Hz) and is determined by the polling interval. The polling interval is measured in milliseconds (ms) and equates to lag time.

The default polling interval is 10ms. However, USB controllers round the interval down to the nearest power of two. Thus, an interval setting of 10ms will actually use 8ms, 7ms will use 4ms, etc.

| Hz | 1000 | 500 | 250 | 125 |
| ms | 1 | 2 | 4 | 8 |

The table to the right shows the relation between polling rate Hertz and the corresponding interval milliseconds (rate = 1000 / interval).

If the polling rate is 125 Hz, the mouse position will be updated every 8 milliseconds. In situations where lag is critical—for example games—some users decrease the interval to as little as possible. However, this puts more load on the CPU, so care should be taken when adjusting this value.

## Display polling rate

The `evhz` tool can display the actual mouse refresh rate.

You can install it from [evhz-git](https://aur.archlinux.org/packages/evhz-git/) and execute as root:

```
# evhz

```

Now move the mouse continuously in large circles until the displayed `Average` stabilizes then press `Ctrl+c` to exit.

If the `Latest` value does not stabilize and switches between two values then the attempted polling rate is faster than the device is capable of, see [#USB device speed](#USB_device_speed).

Alternatively, Windows tools such as [DirectX mouserate checker](http://razerblueprints.net/index.php/View-document-details/18-DirectX-mouserate-checker.html) can be run using [Wine](/index.php/Wine "Wine").

## Display polling interval

**Note:** This only shows the polling interval requested by the device and not the actual interval being used. See [BBS](https://bbs.archlinux.org/viewtopic.php?pid=1607073#p1607073).

Device information including polling interval can be found in debugfs if it is mounted and you have root access.

First, find the Vendor and Product IDs of your device with:

 `$ lsusb` 
```
Bus 001 Device 002: ID **045e**:**0024** Microsoft Corp. Trackball Explorer
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
```

Then run the following as root with those IDs to display the debug information for that device:

 `# grep -B3 -A6 *045e*.**0024* /sys/kernel/debug/usb/devices` 
```
T:  Bus=01 Lev=01 Prnt=01 Port=01 Cnt=01 Dev#=  2 **Spd=1.5**  MxCh= 0
D:  Ver= 1.10 Cls=00(>ifc ) Sub=00 Prot=00 MxPS= 8 #Cfgs=  1
P:  Vendor=045e ProdID=0024 Rev= 1.21
S:  Manufacturer=Microsoft
S:  Product=Microsoft Trackball Explorer®
C:* #Ifs= 1 Cfg#= 1 Atr=a0 MxPwr=100mA
I:* If#= 0 Alt= 0 #EPs= 1 Cls=03(HID  ) Sub=01 Prot=02 Driver=usbhid
E:  Ad=81(I) Atr=03(Int.) MxPS=   4 **Ivl=10ms**
```

The `Ivl` is the polling interval; this device has requested 10ms (and actually reports every 8ms as explained in [#Polling rate and polling interval](#Polling_rate_and_polling_interval)). The `Spd` is the device speed explained in [#USB device speed](#USB_device_speed). For information about the other fields see the [kernel documentation](https://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/tree/Documentation/usb/proc_usb_info.txt).

If debugfs or root access are not available the polling interval can be shown with:

 `$ lsusb -vd *045e*:*0024* | grep bInterval`  `bInterval 10` 

## USB device speed

[USB](https://en.wikipedia.org/wiki/USB "wikipedia:USB") devices are designed to operate at a certain bitrate. Many pointing devices are "Low Speed" 1.5Mbit/s devices. The speed of a device can be shown as explained in [#Display polling interval](#Display_polling_interval).

"Low Speed" devices may not be capable of polling at intervals less than 8ms.

All USB hubs should be capable of at least "Full Speed" 12Mbit/s. The speed of the hub that the device is attached to can be shown with the following command with the same `Bus=xx` as the device:

 `# grep -B1 -A10 "Bus=*01* Lev=00" /sys/kernel/debug/usb/devices` 
```
T:  Bus=01 Lev=00 Prnt=00 Port=00 Cnt=00 Dev#=  1 **Spd=12**   MxCh= 2
B:  Alloc= 11/900 us ( 1%), #Int=  1, #Iso=  0
D:  Ver= 1.10 Cls=09(hub  ) Sub=00 Prot=00 MxPS=64 #Cfgs=  1
P:  Vendor=1d6b ProdID=0001 Rev= 4.01
S:  Manufacturer=Linux 4.1.18-1-lts uhci_hcd
S:  Product=UHCI Host Controller
S:  SerialNumber=0000:00:10.0
C:* #Ifs= 1 Cfg#= 1 Atr=e0 MxPwr=  0mA
I:* If#= 0 Alt= 0 #EPs= 1 Cls=09(hub  ) Sub=00 Prot=00 Driver=hub
E:  Ad=81(I) Atr=03(Int.) MxPS=   2 Ivl=255ms
```

The `Ivl` of the hub is independent of the device and does not affect the polling rate of the device.

## Set polling interval

To configure the polling rate use the `mousepoll` option of the `usbhid` [kernel module](/index.php/Kernel_module "Kernel module"). The default value is 0 which means the module uses the interval requested by the device(s).

The current value of the option can be verified with:

 `$ systool -m usbhid -A mousepoll` 
```
Module = "usbhid"
    mousepoll           = "0"
```

To change the configuration create the following file:

 `/etc/modprobe.d/usbhid.conf`  `options usbhid mousepoll=4` 

This example sets a polling rate of 250Hz.

To change the polling interval without rebooting

```
# modprobe -r usbhid && modprobe usbhid

```

**Warning:** If the second command fails you will be unable to use any USB mouse or keyboard and may have to reboot or ssh into your machine.

You may have to unplug the mouse and plug it back in for the change to take effect.

**Note:** As of May 2015 there is a kernel bug that under certain configurations prevents devices from reaching 1000hz (1ms) polling rate. See [BBS](https://bbs.archlinux.org/viewtopic.php?pid=1528109) and [Bug](https://bugzilla.kernel.org/show_bug.cgi?id=60586).

**Note:** If the usbhid module is included on your initramfs image you may need to add `/etc/modprobe.d/usbhid.conf` to the image also. See the note at [Kernel modules#Using files in /etc/modprobe.d/](/index.php/Kernel_modules#Using_files_in_.2Fetc.2Fmodprobe.d.2F "Kernel modules"). Alternatively, you can add `usbhid.mousepoll=X` to your kernel command line. See [Kernel modules#Using kernel command line](/index.php/Kernel_modules#Using_kernel_command_line "Kernel modules").

**Tip:** When using a smaller than default interval you may want to adjust the [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration") option [VelocityScale](http://xorg.freedesktop.org/wiki/Development/Documentation/PointerAcceleration/#VelocityScale) to match.

## See also

*   [CS:S Mouse Optimization Guide](http://www.overclock.net/computer-peripherals/173255-cs-s-mouse-optimization-guide.html) -- largely aimed at Windows users, though the same principles apply for Linux.