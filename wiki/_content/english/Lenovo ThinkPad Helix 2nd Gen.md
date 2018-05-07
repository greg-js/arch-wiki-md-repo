<caption>Hardware Information</caption>
| Form Factor | Tablet/Ultrabook Convertible (detachable keyboard dock) |
| Display | 11.6" 1920x1080 LCD with Capacitive and Pen Digitizers |
| CPU | Intel Core M-5Y10c or M-5Y71 |
| RAM | 4GiB or 8GiB DDR3L RAM |
| Storage | 128/256GB M.2 SSD |
| WiFi | Intel Dual Band Wireless-AC 7265 with Bluetooth 4.0 |
| Bluetooth | Intel Dual Band Wireless-AC 7265 |
| Camera | 5MP Rear and 2MP Front (also USB) |

This hardware is substantially different from the [Lenovo ThinkPad Helix 1st Gen](/index.php/Lenovo_ThinkPad_Helix "Lenovo ThinkPad Helix") and thus the solutions outlined there are not helpful. Note: the following was tested with the standard ThinkPad Ultrabook keyboard, not the Pro one.

## Contents

*   [1 Suspend & Resume](#Suspend_.26_Resume)
*   [2 Sensors](#Sensors)
*   [3 Touch Screen](#Touch_Screen)
*   [4 Graphics](#Graphics)
*   [5 Unresolved Issues](#Unresolved_Issues)

## Suspend & Resume

This device does not support suspend-to-RAM. It only supports suspend-to-idle (aka "freeze"). In order for this to work completely, you must update the BIOS to the latest version (1.99 works) using the disc image provided by Lenovo. If you do not do this, you may only be able to suspend-to-idle and resume while docked in the keyboard (detaching to tablet mode while suspended would prevent the device from resuming). With an updated BIOS, it appears the device can resume from suspend-to-idle under all conditions.

Older versions of the BIOS misreport the suspend capabilities, and thus the system will try to suspend to RAM. To verify this, run `cat /sys/power/mem_sleep`. If you see `mem` in the output, you are susceptible to this problem. If you are unable to update the RAM, you can force the system to use suspend-to-idle. Simply create the file `/etc/systemd/sleep.conf` containing:

 `/etc/systemd/sleep.conf` 
```
[Sleep]
SuspendState=freeze
```

On the most recent BIOS versions, this isn't necessary, since `/sys/power/mem_sleeep` will only contain `s2idle` and thus any attempt to suspend in any manner will default to suspend-to-idle.

## Sensors

A regression introduced in version 4.14 of the kernel prevents the sensors from being detected properly:

```
$ dmesg | grep sensor
[    2.664607] hid-sensor-hub 0018:2047:0855.0002: item 0 1 0 8 parsing failed
[    2.664615] hid-sensor-hub 0018:2047:0855.0002: parse failed
[    2.664620] hid-sensor-hub: probe of 0018:2047:0855.0002 failed with error -22

```

Until that is fixed, the functionality can be restored by compiling the kernel with the following patch (this could probably be simplified to just focus on this model; here we're simply reverting the full offending commit):

```
--- a/drivers/hid/hid-sensor-hub.c	2018-04-01 22:20:27.000000000 +0100
+++ b/drivers/hid/hid-sensor-hub.c	2017-09-03 21:56:17.000000000 +0100
@@ -579,6 +579,54 @@
 }
 EXPORT_SYMBOL_GPL(sensor_hub_device_close);

+static __u8 *sensor_hub_report_fixup(struct hid_device *hdev, __u8 *rdesc,
+		unsigned int *rsize)
+{
+	int index;
+	struct sensor_hub_data *sd =  hid_get_drvdata(hdev);
+	unsigned char report_block[] = {
+				0x0a,  0x16, 0x03, 0x15, 0x00, 0x25, 0x05};
+	unsigned char power_block[] = {
+				0x0a,  0x19, 0x03, 0x15, 0x00, 0x25, 0x05};
+
+	if (!(sd->quirks & HID_SENSOR_HUB_ENUM_QUIRK)) {
+		hid_dbg(hdev, "No Enum quirks
");
+		return rdesc;
+	}
+
+	/* Looks for power and report state usage id and force to 1 */
+	for (index = 0; index < *rsize; ++index) {
+		if (((*rsize - index) > sizeof(report_block)) &&
+			!memcmp(&rdesc[index], report_block,
+						sizeof(report_block))) {
+			rdesc[index + 4] = 0x01;
+			index += sizeof(report_block);
+		}
+		if (((*rsize - index) > sizeof(power_block)) &&
+			!memcmp(&rdesc[index], power_block,
+						sizeof(power_block))) {
+			rdesc[index + 4] = 0x01;
+			index += sizeof(power_block);
+		}
+	}
+
+	/* Checks if the report descriptor of Thinkpad Helix 2 has a logical
+	 * minimum for magnetic flux axis greater than the maximum */
+	if (hdev->product == USB_DEVICE_ID_TEXAS_INSTRUMENTS_LENOVO_YOGA &&
+		*rsize == 2558 && rdesc[913] == 0x17 && rdesc[914] == 0x40 &&
+		rdesc[915] == 0x81 && rdesc[916] == 0x08 &&
+		rdesc[917] == 0x00 && rdesc[918] == 0x27 &&
+		rdesc[921] == 0x07 && rdesc[922] == 0x00) {
+		/* Sets negative logical minimum for mag x, y and z */
+		rdesc[914] = rdesc[935] = rdesc[956] = 0xc0;
+		rdesc[915] = rdesc[936] = rdesc[957] = 0x7e;
+		rdesc[916] = rdesc[937] = rdesc[958] = 0xf7;
+		rdesc[917] = rdesc[938] = rdesc[959] = 0xff;
+	}
+
+	return rdesc;
+}
+
 static int sensor_hub_probe(struct hid_device *hdev,
 				const struct hid_device_id *id)
 {
@@ -730,6 +778,51 @@
 }

 static const struct hid_device_id sensor_hub_devices[] = {
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_INTEL_0,
+			USB_DEVICE_ID_INTEL_HID_SENSOR_0),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_INTEL_1,
+			USB_DEVICE_ID_INTEL_HID_SENSOR_0),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_INTEL_1,
+			USB_DEVICE_ID_INTEL_HID_SENSOR_1),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_MICROSOFT,
+			USB_DEVICE_ID_MS_SURFACE_PRO_2),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_MICROSOFT,
+			USB_DEVICE_ID_MS_TOUCH_COVER_2),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_MICROSOFT,
+			USB_DEVICE_ID_MS_TYPE_COVER_2),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_MICROSOFT,
+			0x07bd), /* Microsoft Surface 3 */
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_MICROCHIP,
+			0x0f01), /* MM7150 */
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_STM_0,
+			USB_DEVICE_ID_STM_HID_SENSOR),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_STM_0,
+			USB_DEVICE_ID_STM_HID_SENSOR_1),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_TEXAS_INSTRUMENTS,
+			USB_DEVICE_ID_TEXAS_INSTRUMENTS_LENOVO_YOGA),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_ITE,
+			USB_DEVICE_ID_ITE_LENOVO_YOGA),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_ITE,
+			USB_DEVICE_ID_ITE_LENOVO_YOGA2),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_ITE,
+			USB_DEVICE_ID_ITE_LENOVO_YOGA900),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
+	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, USB_VENDOR_ID_INTEL_0,
+			0x22D8),
+			.driver_data = HID_SENSOR_HUB_ENUM_QUIRK},
 	{ HID_DEVICE(HID_BUS_ANY, HID_GROUP_SENSOR_HUB, HID_ANY_ID,
 		     HID_ANY_ID) },
 	{ }
@@ -742,6 +835,7 @@
 	.probe = sensor_hub_probe,
 	.remove = sensor_hub_remove,
 	.raw_event = sensor_hub_raw_event,
+	.report_fixup = sensor_hub_report_fixup,
 #ifdef CONFIG_PM
 	.suspend = sensor_hub_suspend,
 	.resume = sensor_hub_resume,

```

In order to use the sensors (particularly the accelerometer and the ambient light sensor) in [GNOME](/index.php/GNOME "GNOME"), you should install the [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) package. There is presumably a quirk with this sensor hardware. The effect is that `iio-sensor-proxy` loads too early, requiring the service to be restarted before the sensors can be read properly. To fix this, edit the systemd unit so that it starts after GDM (`After=gdm.service`; see [Systemd#Editing_provided_units](/index.php/Systemd#Editing_provided_units "Systemd")).

If you are using [GNOME](/index.php/GNOME "GNOME"), a program called [tp-helix-orientation-lock](http://brandon.invergo.net/software/tp-helix-orientation-lock.html) enables the use of the "rotation lock" button on the Helix 2, as well as optionally automatically locking/unlocking the screen orientation when docking/undocking the tablet.

## Touch Screen

In order to enable multitouch, install [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) and [libwacom](https://www.archlinux.org/packages/?name=libwacom). By default, [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) handles multitouch, however it is limited to two-finger input. In order to allow true multitouch, you must disable this built-in support. Multitouch events will then be passed on to XServer. To test this, try running

```
$ xset "Wacom HID 501D Finger touch" Gesture off

```

To make it permanent, copy `/usr/share/X11/xorg.conf.d/70-wacom.conf` to `/etc/X11/xorg.conf.d/70-wacom.conf` and edit it so the input entries all contain `Option "Gesture" "Off"`.

## Graphics

Install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) for graphics acceleration.

## Unresolved Issues

*   The fingerprint reader is apparently not supported by any driver.
*   The speakers make popping sounds.