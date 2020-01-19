Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 (7390)](/index.php/Dell_XPS_13_(7390) "Dell XPS 13 (7390)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The New Dell XPS 13 2-in-1 (7390) is the model released in mid 2019 in most territories and is the second iteration of the Dell XPS 13 2-in-1 series, including an updated 10th generation Intel Ice Lake processor with Iris Plus integrated graphics. It can be used like a tablet when folding the display 180 degrees backwards and includes a enlarged 16:10 FHD+ or UHD touchscreen which should work out of the box. This includes support for Wacom pen technology (tested with the "Wacom Bamboo Ink Plus").

As of kernel 5.4.6.arch3-1, no modifications (in particular regarding LPSS and WiFi) are necessary for the installation and normal operations.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Additional features](#Additional_features)
    *   [1.1 Automatic screen rotation under Gnome and Wayland](#Automatic_screen_rotation_under_Gnome_and_Wayland)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Intermittent display blackouts](#Intermittent_display_blackouts)
    *   [2.2 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.3 Camera](#Camera)

## Additional features

### Automatic screen rotation under Gnome and Wayland

Install the [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) package. The screen will now automatically rotate and keyboard input will be disabled in tablet mode.

## Troubleshooting

### Intermittent display blackouts

Issues with the screen going black for a second on certain audio events have been resolved with kernel 5.4.12-arch1\. You might need to update the kernel if you installed from older installation media.

### Fingerprint Reader

There are currently no drivers available for the fingerprint reader. More information:

[[1]](https://gitlab.freedesktop.org/libfprint/libfprint/issues?scope=all&utf8=%E2%9C%93&state=opened&search=goodix) libfprint issues adressing Goodix devices

[[2]](https://github.com/goodix) Older Goodix drivers

### Camera

There are currently no drivers available for the camera. More information:

[[3]](https://wiki.ubuntu.com/Dell/XPS/XPS-13-7390-2-in-1) Ubuntu Wiki page on the XPS 13 2-in-1.

[[4]](https://github.com/intel/intel-camera-drivers/tree/master/drivers/media) IPU4 drivers that may be ported to the current kernel, needs a lot of work.

[[5]](https://github.com/endeavour/DellXps7390-2in1-Manjaro-Linux-Fixes/issues/6#issuecomment-552025852) Maybe IPU3 is enough?

[[6]](https://github.com/torvalds/linux/tree/5613970af3f5f8372c596b138bd64f3918513515/drivers/staging/media/ipu3) IPU3 driver in staging, needs some work.