The LSM303DLH is a 3-axis accelerometer and magnetometer.

**Note:** As of kernel 3.13, it looks like this device is already recognized by the vanilla kernel. As an example, [this bash script](http://pastebin.com/742KTaS6), autostarted in the background, will perform automatic screen (and touchscreen) rotation for a Dell Inspiron 7347 convertible. This is just a working example, a proper method would also make use of the integrated gyroscope for faster reaction times.

## Contents

*   [1 Driver](#Driver)
*   [2 Accelerometer](#Accelerometer)
    *   [2.1 Instantiate the device](#Instantiate_the_device)
    *   [2.2 Enabling the device](#Enabling_the_device)
    *   [2.3 Reading the output of the device](#Reading_the_output_of_the_device)
*   [3 See also](#See_also)

## Driver

The official driver available is available at a [cached version of the manufacturer's website](http://webcache.googleusercontent.com/search?q=cache:iJTcx9sEDbUJ:www.st.com/jp/analog/product/250145.jsp+&cd=2&hl=en&ct=clnk). The driver is open source an it was released under the [GNU General Public License (v2)](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html). It compiles fine, and the accelerometer module can be loaded without problems:

 `dmesg` 
```
...
[  124.908804] lsm303dlh_acc_sysfs accelerometer driver: init
[  124.908876] i2c-core: driver [lsm303dlh_acc_sysfs] using legacy suspend method
[  124.908885] i2c-core: driver [lsm303dlh_acc_sysfs] using legacy resume method
```

The following error occurs when loading the magnetometer module:

 `dmesg` 
```
...
[ 2546.530196] lsm303dlh_mag_sysfs: Unknown symbol input_allocate_polled_device (err 0)
[ 2546.530271] lsm303dlh_mag_sysfs: Unknown symbol input_free_polled_device (err 0)
[ 2546.530425] lsm303dlh_mag_sysfs: Unknown symbol input_register_polled_device (err 0)
[ 2546.530550] lsm303dlh_mag_sysfs: Unknown symbol input_unregister_polled_device (err 0)
```

## Accelerometer

### Instantiate the device

Run the following command to instantiate the device:

```
# echo lsm303dlh_acc_sysfs 25 > /sys/bus/i2c/devices/i2c-2/new_device

```

Although, it seems to be a problem with the driver.

 `demesg` 
```
...
[  833.274769] lsm303dlh_acc_sysfs: probe start.
[  833.274781] lsm303dlh_acc_sysfs 2-0019: platform data is NULL. exiting.
**[  833.274790] lsm303dlh_acc_sysfs: Driver Init failed**
[  833.274813] i2c i2c-2: new_device: Instantiated device lsm303dlh_acc_sysfs at 0x19
```

### Enabling the device

### Reading the output of the device

## See also

*   Older version of the driver at [lklm.org](https://lkml.org/lkml/2010/12/1/3).
*   [Luke Ross' website](http://lukeross.name/dell/).
*   [yoga-laptop](https://github.com/pfps/yoga-laptop), an utility for Lenovo Ideapad Yoga laptops with information and scripts that can be adapted for devices with this accelerometer (Lenovo Thinkpad Yoga, Dell Inspiron 7347, ...)