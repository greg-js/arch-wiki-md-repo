[Howdy](https://github.com/boltgolt/howdy) is a program that imitates Windows Hello on Linux. It uses a computer's IR sensors and camera to verify a user's face.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setup Howdy to start when needed](#Setup_Howdy_to_start_when_needed)
        *   [2.1.1 Example](#Example)
    *   [2.2 Add correct IR sensor](#Add_correct_IR_sensor)
    *   [2.3 Add face to Howdy](#Add_face_to_Howdy)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Testing your IR camera](#Testing_your_IR_camera)
    *   [3.2 Howdy does not seem to work](#Howdy_does_not_seem_to_work)
    *   [3.3 Errors recognizing an input device](#Errors_recognizing_an_input_device)
    *   [3.4 GStreamer warnings in shell](#GStreamer_warnings_in_shell)

## Installation

[Install](/index.php/Install "Install") the [howdy](https://aur.archlinux.org/packages/howdy/) package.

## Configuration

### Setup Howdy to start when needed

In order for Howdy to authenticate a user, a small change must be added to any [PAM](/index.php/PAM "PAM") configuration file where Howdy might want to be used. The following line must be added to any configuration file:

```
auth sufficient pam_python.so /lib/security/howdy/pam.py

```

#### Example

 `/etc/pam.d/sudo` 
```
# PAM-1.0
auth    sufficient pam_python.so /lib/security/howdy/pam.py
auth    include    system-auth
account include    system-auth
session include    system-auth
```

### Add correct IR sensor

Determine the correct `/dev/videoX` file connected to the IR sensor. This can be done through various programs such as [cheese](https://www.archlinux.org/packages/?name=cheese) and [fswebcam](https://aur.archlinux.org/packages/fswebcam/). Once the correct filename is found, edit `/lib/security/howdy/config.ini` using either your preferred editor or with `sudo howdy config`.

**Note:** [gedit](https://www.archlinux.org/packages/?name=gedit) must be installed for `sudo howdy config` to work.

### Add face to Howdy

In order to add a face model to Howdy, run `sudo howdy add`.

## Troubleshooting

### Testing your IR camera

It can be useful to first make verify that your IR camera functions correctly. A set of 10 jpg photos can be taken to test your device using the gstreamer package with the following command (replacing /dev/video0 with the location of your IR camera):

```
gst-launch-1.0 v4l2src device=/dev/video0 num-buffers=10 ! image/jpeg ! multifilesink location="frame-%02d.jpg"

```

### Howdy does not seem to work

Verify that Howdy is properly working by running `howdy test` as root. If that seems to work, check any PAM configuration files and verify they are working. Some programs, such as SDDM [[1]](https://github.com/sddm/sddm/issues/284), do not work properly with PAM, which may result in unexpected results.

### Errors recognizing an input device

Some IR sensors (for example of the Thinkpad T480) need to have the frame width and height defined in the configuration file:

```
frame_width = 400
frame_height = 400
```

The width and height of your sensor output: `v4l2-ctl --list-devices --all`.

### GStreamer warnings in shell

You might have howdy working but get warning like this in shell:

 `$sudo howdy test` 
```
[ WARN:0] global /build/opencv/src/opencv-4.1.1/modules/videoio/src/cap_gstreamer.cpp (1756) handleMessage OpenCV | GStreamer warning: Embedded video playback halted; module source reported: Could not read from resource.
[ WARN:0] global /build/opencv/src/opencv-4.1.1/modules/videoio/src/cap_gstreamer.cpp (886) open OpenCV | GStreamer warning: unable to start pipeline
[ WARN:0] global /build/opencv/src/opencv-4.1.1/modules/videoio/src/cap_gstreamer.cpp (480) isPipelinePlaying OpenCV | GStreamer warning: GStreamer: pipeline have not been created
...

```

This is caused by upstream [opencv](https://www.archlinux.org/packages/?name=opencv) package built with default warning level `LOG_LEVEL_WARNING = 3`. The cv::utils::logging API in C++ can set log level higher in order to hide lower level warning, but this API is not exposed into python-cv2 yet.

A temporary solution for this is adding an environment variable `OPENCV_LOG_LEVEL=ERROR` to your system per user or globally.

**Note:** This will make the warning disappear but might hide other potential problems