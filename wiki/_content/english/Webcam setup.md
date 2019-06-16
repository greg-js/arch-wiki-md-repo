This is a guide to setting up your webcam in Arch Linux.

Most probably your webcam will work out of the box. Permissions to access video devices (e.g. `/dev/video0`) are handled by [udev](/index.php/Udev "Udev"), there is no configuration necessary.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Loading](#Loading)
*   [2 Configuration](#Configuration)
    *   [2.1 Command Line](#Command_Line)
    *   [2.2 Persisting configuration changes](#Persisting_configuration_changes)
*   [3 Applications](#Applications)
    *   [3.1 xawtv](#xawtv)
    *   [3.2 VLC](#VLC)
    *   [3.3 MPlayer](#MPlayer)
    *   [3.4 mpv](#mpv)
    *   [3.5 FFmpeg](#FFmpeg)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 V4L1 support](#V4L1_support)
    *   [4.2 xawtv with nvidia card](#xawtv_with_nvidia_card)
    *   [4.3 Microsoft Lifecam Studio/Cinema](#Microsoft_Lifecam_Studio/Cinema)
    *   [4.4 Skype](#Skype)
    *   [4.5 Check bandwidth used by USB webcams](#Check_bandwidth_used_by_USB_webcams)

## Loading

Most recent webcams are UVC (*USB Video Class*) compliant and are supported by the generic *uvcvideo* kernel driver module. To check that your webcam is recognized, run *dmesg* just after you plug the webcam in. You should see something like this:

 `$ dmesg | tail` 
```
sn9c102: V4L2 driver for SN9C10x PC Camera Controllers v1:1.24a
usb 1-1: SN9C10[12] PC Camera Controller detected (vid/pid 0x0C45/0x600D)
usb 1-1: PAS106B image sensor detected
usb 1-1: Initialization succeeded
usb 1-1: V4L2 device registered as /dev/video0
usb 1-1: Optional device control through 'sysfs' interface ready
usbcore: registered new driver sn9c102
```

Some pre-UVC webcams are also supported via the *gspca* kernel driver module. See the [gspca devices](https://www.linuxtv.org/wiki/index.php/Gspca_devices) for a non-exhaustive list of supported devices under this framework.

Otherwise, if your webcam is not supported by the kernel's drivers, an external driver is necessary. The first step is to identify the name of the webcam, using for example `lsusb`. Then you can check [webcam devices](https://www.linuxtv.org/wiki/index.php/Webcam_devices) for information and resources about webcams. Once you find a driver compatible with the webcam, you have to add the corresponding [kernel module](/index.php/Kernel_module "Kernel module") in `/etc/modules-load.d/webcam.conf` so it will be loaded into the kernel during init stage bootstrapping.

**Note:** The Linux kernel to userspace API used to control webcams is named *Video4Linux2*, **v4l2** for short. All applications which support v4l2 will work with the kernel's drivers.

## Configuration

If you want to configure brightness, color and other webcam parameters (e.g. in the case when out-of-the-box colors are too bluish/reddish/greenish) you may use *Qt V4L2 Test Bench*. To run it, [install](/index.php/Install "Install") [v4l-utils](https://www.archlinux.org/packages/?name=v4l-utils) and launch `qv4l2`, and it will present you a list of configurable settings. Changing these settings will affect all applications.

### Command Line

[v4l-utils](https://www.archlinux.org/packages/?name=v4l-utils) also installs an equivalent command line tool, `v4l2-ctl`. To list all video devices:

```
$ v4l2-ctl --list-devices

```

To list the configurable settings of a video device:

```
$ v4l2-ctl -d /dev/video0 --list-ctrls

```

### Persisting configuration changes

Configuration made via V4L2 does not persist after the webcam is disconnected and reconnected. It's possible to use `v4l2-ctl` with [Udev](/index.php/Udev "Udev") rules in order to set some configuration each time a particular camera is connected.

For example, to set a default zoom setting on a particular Logitech webcam each time it is connected, add a [udev rule](/index.php/Udev#udev_rule_example "Udev") like this:

 `/etc/udev/rules.d/99-logitech-default-zoom.rules`  `SUBSYSTEM=="video4linux", KERNEL=="video[0-9]*", ATTRS{product}=="HD Pro Webcam C920", ATTRS{serial}=="BBBBFFFF", RUN="/usr/bin/v4l2-ctl -d $devnode --set-ctrl=zoom_absolute=170"` 

To find udev attributes like the product name and serial, see [Udev#List the attributes of a device](/index.php/Udev#List_the_attributes_of_a_device "Udev"). It also possible to [set a static name for a video device](/index.php/Udev#Setting_static_device_names "Udev")).

## Applications

See also [List of applications/Multimedia#Webcam](/index.php/List_of_applications/Multimedia#Webcam "List of applications/Multimedia").

### xawtv

This is a basic *Video4Linux2* device viewer, and although it is intended for use with TV tuner cards, it works well with webcams. It will display what your webcam sees in a window.

[Install](/index.php/Install "Install") [xawtv](https://www.archlinux.org/packages/?name=xawtv) and run it with:

```
$ xawtv -c /dev/video0

```

In case of error see [#xawtv with nvidia card](#xawtv_with_nvidia_card).

### VLC

[VLC](/index.php/VLC "VLC") can also be used to view and record your webcam. In VLC's "Media" menu, open the 'Capture Device...' dialog and enter the video and audio device files. Or from the command line, do:

```
$ vlc v4l2:// :input-slave=alsa:// :v4l-vdev="/dev/video0"

```

This will make VLC mirror your webcam.

*   To take stills, simply choose *Snapshot* in the *Video* menu.
*   To record the stream, add a `--sout` argument to the command line, e.g.

```
$ vlc v4l:// :v4l-vdev="/dev/video0" :v4l-adev="/dev/audio2" --sout "#transcode{vcodec=mp1v,vb=1024,scale=1,acodec=mpga,ab=192,channels=2}:duplicate{dst=std{access=file,mux=mpeg1,dst=/tmp/test.mpg}}"

```

(Obviously a bit overkill with regard to the bit rates but it is fine for testing purposes). Note that by default this will not display the video, in order to see what you are recording, you need to add the display as a destination to the argument (note that it will slow down the operation):

```
... :duplicate{**dst=display**,dst=std{access= ....

```

### MPlayer

To use [MPlayer](/index.php/MPlayer "MPlayer") to take snapshots from your webcam run this command from the terminal:

```
$ mplayer tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0 -fps 15 -vf screenshot

```

From here you have to press `s` to take the snapshot. The snapshot will be saved in the current folder as `shotXXXX.png`. If you want to record video continuous:

```
$ mencoder tv:// -tv driver=v4l2:width=640:height=480:device=/dev/video0:forceaudio:adevice=/dev/dsp -ovc lavc -oac mp3lame -lameopts cbr:br=64:mode=3 -o *filename*.avi

```

Press `Ctrl+c` to end the recording.

### mpv

To use [mpv](/index.php/Mpv "Mpv") to take snapshots from your webcam, run this command from the terminal:

```
$ mpv av://v4l2:/dev/video0

```

From here you have to press `s` to take the snapshot. The snapshot will be saved in your current folder as `mpv-shot*NNNN*.jpg`.

To use MJPEG as the pixelformat instead of the default, which in most cases is YUYV, you can run the following instead:

```
$ mpv --demuxer-lavf-format video4linux2 --demuxer-lavf-o-set input_format=mjpeg av://v4l2:/dev/video0

```

In some cases this can lead to drastic improvements in quality and performance (5FPS -> 30FPS for example).

### FFmpeg

See [FFmpeg#Recording webcam](/index.php/FFmpeg#Recording_webcam "FFmpeg").

## Troubleshooting

### V4L1 support

Version 2.6.27 of the Linux kernel dropped support for the legacy Video4Linux (1) API. Pixel format decoding has been pushed to user space, since Video4Linux version 2 does not support kernel space decoding. The libv4l library provides userland applications with pixel decoding services and will be used by most programs. Other compatibility layers are also available.

**If your device is created but your image looks strange (e.g. nearly completely green), you probably need this.**

If the application has V4L2 support but no pixelformat support then use the following command:

```
LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so application

```

If the application only supports the older version of V4L, use this command:

```
LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so application

```

**Tip:** You also might want to put a line like the following into `/etc/profile` or [xprofile](/index.php/Xprofile "Xprofile") so you do not have to type that long command all the time: `export LD_PRELOAD=/usr/lib/libv4l/v4l2convert.so` or `export LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so`

For 32-bit [multilib](/index.php/Multilib "Multilib") applications, install the [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils) package and replace `/usr/lib/libv4l/` by `/usr/lib32/libv4l/` in the above commands.

### xawtv with nvidia card

If you are using an nvidia graphic card, and get an error like

```
X Error of failed request:  XF86DGANoDirectVideoMode
 Major opcode of failed request:  139 (XFree86-DGA)
 Minor opcode of failed request:  1 (XF86DGAGetVideoLL)
 Serial number of failed request:  69
 Current serial number in output stream:  69

```

you should instead run it as `$ xawtv -nodga`

### Microsoft Lifecam Studio/Cinema

Under certain configurations, the Microsoft lifecam studio/cinema may request too much usb bandwidth and fail [see Uvcvideo FAQ](http://www.ideasonboard.org/uvc/#footnote-13). In this case, change the buffering by loading the `uvcvideo` driver with `quirks=0x80`. Add it to `/etc/modprobe.d/uvcvideo.conf` :

 `/etc/modprobe.d/uvcvideo.conf` 
```
## fix bandwidth issue for lifecam studio/cinema
options uvcvideo quirks=0x80
```

**Note:** If delays are visible in the logs, or the camera works periodically, this workaround should apply generally. Bigger values such as `quirks=0x100` are possible.

### Skype

When testing the webcam, note the following:

*   The echobot does not support videochat. Don't use it for testing your webcam.
*   Skype might recognize different video/camera devices (/dev/video*). These will be listed as something like "integrated camera..." in a dropdown menu in the camera settings. Try each camera and wait a few seconds, because it takes time to switch to a different camera.

### Check bandwidth used by USB webcams

When running multiple webcams on a single USB bus, they may saturate the bandwidth of the USB bus and not work properly. You can diagnose this with the *usbtop* tool from the [usbtop](https://aur.archlinux.org/packages/usbtop/) package.