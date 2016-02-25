If you have invested in a high resolution mouse, adjusting the USB polling rate is a common trick to utilize the added precision it brings. The polling rate (or report rate) determines how often the mouse sends information to your computer.

## Contents

*   [1 Polling rate and polling interval](#Polling_rate_and_polling_interval)
*   [2 Set polling interval](#Set_polling_interval)
*   [3 Display polling rate](#Display_polling_rate)
*   [4 Display polling interval](#Display_polling_interval)
*   [5 See also](#See_also)

## Polling rate and polling interval

The polling rate of a device is measured in Hertz (Hz) and is determined by the polling interval. The polling interval is measured in milliseconds (ms) and equates to lag time.

The default polling interval is 10ms. However, USB controllers round the interval down to the nearest power of two. Thus, an interval setting of 10ms will actually use 8ms, 7ms will use 4ms, etc.

The table below shows the relation between polling rate Hertz and the corresponding interval milliseconds (rate = 1000 / interval):

| Hz | ms |
| 1000 | 1 |
| 500 | 2 |
| 250 | 4 |
| 125 | 8 |

If the polling rate is 125 Hz, the mouse position will be updated every 8 milliseconds. In situations where lag is critical—for example games—some users decrease the interval to as little as possible. However, this puts more load on the CPU, so care should be taken when adjusting this value.

## Set polling interval

Here we are using the `usbhid` module of the kernel to set a custom "mousepoll" interval. Add the following line according to [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

 `/etc/modprobe.d/usbhid.conf`  `options usbhid mousepoll=[polling interval]` 

The `[polling interval]` is a number in *ms* from the table above. For example, to set a polling rate of 500Hz:

```
options usbhid mousepoll=2

```

To change the polling interval without rebooting

```
# modprobe -r usbhid && modprobe usbhid

```

**Warning:** If the second command fails you will be unable to use any USB mouse or keyboard and may have to reboot or ssh into your machine.

Then unplug and replug your mouse.

**Note:** As of May 2015 there is a kernel bug that under certain configurations prevents devices from reaching 1000hz (1ms) polling rate. See [BBS](https://bbs.archlinux.org/viewtopic.php?pid=1528109) and [Bug](https://bugzilla.kernel.org/show_bug.cgi?id=60586).

**Note:** If the usbhid module is included on your initramfs image you may need to add `/etc/modprobe.d/usbhid.conf` to the image also. See the note at [Kernel modules#Using files in /etc/modprobe.d/](/index.php/Kernel_modules#Using_files_in_.2Fetc.2Fmodprobe.d.2F "Kernel modules"). Alternatively, you can add `usbhid.mousepoll=X` to your kernel command line. See [Kernel modules#Using kernel command line](/index.php/Kernel_modules#Using_kernel_command_line "Kernel modules").

## Display polling rate

The `evhz` tool can display the actual mouse refresh rate.

You can install it from [evhz-git](https://aur.archlinux.org/packages/evhz-git/)

Then execute as root:

```
# evhz

```

Now move the mouse continuously in large circles until the displayed average stabilizes then press `Ctrl+c` to exit.

Alternatively, Windows tools such as [DirectX mouserate checker](http://razerblueprints.net/index.php/View-document-details/18-DirectX-mouserate-checker.html) can be run using WINE.

## Display polling interval

**Note:** This only shows the polling interval requested by the device and not the actual interval being used. See [BBS](https://bbs.archlinux.org/viewtopic.php?pid=1607073#p1607073).

Device information including polling interval can be found in debugfs if it is mounted and you have root access.

First, identify the Bus and Device number of your device with:

```
$ lsusb

```

Then print out the file as root and find the corresponding bus and device output:

```
# cat /sys/kernel/debug/usb/devices

```

The `Ivl` field indicates the polling interval, thus 1000/Ivl is the polling rate. For example, `Ivl=2ms` would be a 500Hz polling rate.

## See also

*   [CS:S Mouse Optimization Guide](http://www.overclock.net/computer-peripherals/173255-cs-s-mouse-optimization-guide.html) -- largely aimed at Windows users, though the same principles apply for Linux.