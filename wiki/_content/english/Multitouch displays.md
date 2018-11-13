Since Linux Kernel 3.2, multitouch devices are handled by the `hid-multitouch` module, see [Kernel modules](/index.php/Kernel_modules "Kernel modules").

## Contents

*   [1 Configuration (USB devices)](#Configuration_(USB_devices))
*   [2 Rotating the touch screen](#Rotating_the_touch_screen)
*   [3 Drivers](#Drivers)
    *   [3.1 eGalax](#eGalax)
        *   [3.1.1 Invert Y-axis](#Invert_Y-axis)
*   [4 Gestures](#Gestures)

## Configuration (USB devices)

Find the vendor ID (VID) and product ID (PID) for your touchscreen using `lsusb`:

 `$ lsusb` 
```
...
Bus 004 Device 002: ID 0eef:725e D-WAV Scientific Co., Ltd 
...

```

Here, VID=0eef (eGalax) and PID=725e. Now, get the MT_CLASS_* definitions from [[1]](http://lxr.free-electrons.com/source/drivers/hid/hid-multitouch.c). Currently vendor specific classes are available for 3M Cypress and eGalax. If none of this matches your device, you can try to experiment with the other MT_CLS_*. In this example

```
#define MT_CLS_EGALAX                           0x0103

```

You need to convert MT_CLS_* to decimal (In this case, 0x0103 is 259 in decimal).

After loading the `hid-multitouch`, see [Kernel modules](/index.php/Kernel_modules "Kernel modules"), you need to pass the devices' options with

```
# echo BUS VID PID MT_CLASS_* > /sys/module/hid_multitouch/drivers/hid\:hid-multitouch/new_id

```

In this example, the touchscreen is an USB device, so BUS=3 and the previous command looks like this:

```
# echo 3 0eef 725e 259 > /sys/module/hid_multitouch/drivers/hid\:hid-multitouch/new_id

```

Reboot. If the touchscreen is detected you should submit your devices' details (relevant `lsusb` line) to the [linux-input mailing list](http://vger.kernel.org/vger-lists.html#linux-input).

If the touchscreen is not working properly, you may need to install a specific driver for your touchscreen, see [#Drivers](#Drivers).

## Rotating the touch screen

Store and mark [[2]](https://gist.githubusercontent.com/anonymous/b5728d68bb8808454cb6/raw/1882d23b273fc1b341a8b7afa1f2649fceff4574/gistfile1.sh) executable (call the script to see its input options).

## Drivers

### eGalax

The driver for eGalax touchscreens is available from the [eGalax website](http://home.eeti.com.tw/drivers_Linux.html). Also, it is availbale as [xf86-input-egalax](https://aur.archlinux.org/packages/xf86-input-egalax/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

#### Invert Y-axis

If after installing the eGalax driver the Y-axis of the touchscreen is inverted, edit the file `/etc/eGTouchd.ini` an change the value of `Direction` from 0 to 2:

 `/etc/eGtouchd.ini` 
```
...
DetectRotation 0
**Direction 2**
Orientation 0
...
```

## Gestures

If you want gestures in your window manager, install [touchegg](https://aur.archlinux.org/packages/touchegg/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") and read its [docs](https://code.google.com/p/touchegg/wiki/Main).