If you have invested in a high resolution mouse, adjusting the USB polling rate is a common trick to utilise the added precision it brings. The polling rate (or report rate) determines how often the mouse sends information to your computer. Measured in Hertz (Hz), this setting equates to lag time (in *ms*).

By default, the USB polling rate is set at 125 Hz. The table below represents combinations of *Hz* values and their corresponding delay time:

| Hz | ms |
| 1000 | 1 |
| 500 | 2 |
| 250 | 4 |
| 125 | 8 |
| 100 | 10 |

If the polling rate is set at 125 Hz, the mouse cursor can only be updated every 8 milliseconds. In situations where lag is critical (for example games), it is useful to decrease this value to as little as possible. Increasing the polling interval will improve precision at the trade-off of using more CPU resources, therefore care should be taken when adjusting this value.

**Warning:** As of May 2015 there is a kernel bug that under certain configurations prevents the system from reaching 1000hz (1ms) polling rate. See [BBS](https://bbs.archlinux.org/viewtopic.php?pid=1528109) and [Bug](https://bugzilla.kernel.org/show_bug.cgi?id=60586).

## Contents

*   [1 Setting the polling rate](#Setting_the_polling_rate)
*   [2 Displaying current mouse rate](#Displaying_current_mouse_rate)
*   [3 Displaying device polling rate](#Displaying_device_polling_rate)
*   [4 Further Reading](#Further_Reading)

## Setting the polling rate

Here we are using the `usbhid` module of the kernel to set a custom "mousepoll" rate. Add the following line according to [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

 `/etc/modprobe.d/modprobe.conf`  `options usbhid mousepoll=[polling interval]` 

The `[polling interval]` is a number in *ms* from the table above. For example, to set a polling rate of 500Hz:

```
options usbhid mousepoll=2

```

To change the polling rate without rebooting

```
# modprobe -r usbhid && modprobe usbhid

```

**Warning:** Make sure that both commands execute otherwise you will be unable to use the mouse and keyboard and will have to reboot or ssh into your machine.

Then unplug and replug your mouse.

**Note:** If you use the **usbinput** and **udev** hooks in your initramfs, usbhid will be included on the image and you'll need to add `/etc/modprobe.d/modprobe.conf` to the FILES entry in `/etc/mkinitcpio.conf`. Remember to regenerate your image after changing the config. Without doing this, the module will be inserted during early userspace without the polling option. Alternatively, you can add usbhid.mousepoll=X to your kernel command line.

## Displaying current mouse rate

A tool exists (named *evhz*) that can display the current mouse refresh rate -- useful when checking that your customized polling settings have been applied.

You can install it from [AUR](/index.php/AUR "AUR") [evhz-git](https://aur.archlinux.org/packages/evhz-git/) or compile it yourself:

Save [evhz.c](https://github.com/ian-kelling/evhz/raw/master/evhz.c) ([its github page](https://github.com/ian-kelling/evhz))

Compile it with:

```
$ gcc -o evhz evhz.c

```

Then execute as root:

```
# ./evhz

```

Alternatively, Windows tools such as [DirectX mouserate checker](http://razerblueprints.net/index.php/View-document-details/18-DirectX-mouserate-checker.html) can be run using WINE.

## Displaying device polling rate

Device information including polling rates can be found in debugfs if it is mounted and you have root access.

First, identify the Bus and Device number of your device with:

```
$ lsusb

```

Then print out the file as root and find the corresponding bus and device output:

```
# cat /sys/kernel/debug/usb/devices

```

The `Ivl` field indicates the polling interval, thus 1/Ivl is the polling rate. For example, `Ivl=1ms` would be a 1000Hz polling rate.

## Further Reading

*   [CS:S Mouse Optimization Guide](http://www.overclock.net/computer-peripherals/173255-cs-s-mouse-optimization-guide.html) -- largely aimed at Windows users, though the same principles apply for Linux.