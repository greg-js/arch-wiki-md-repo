The Oculus Rift is a virtual reality head-mounted display developed by [Oculus VR](http://www.oculusvr.com/).

## Contents

*   [1 Basic Setup](#Basic_Setup)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 SDK](#SDK)
    *   [1.3 Video Mode](#Video_Mode)
        *   [1.3.1 xrandrift](#xrandrift)
        *   [1.3.2 Manually, using xrandr](#Manually.2C_using_xrandr)
*   [2 Working applications](#Working_applications)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Kernel log spamming by DK2 camera](#Kernel_log_spamming_by_DK2_camera)
    *   [3.2 Camera misbehaving after suspend/resume](#Camera_misbehaving_after_suspend.2Fresume)
    *   [3.3 Inaccurate latency readings for legacy applications](#Inaccurate_latency_readings_for_legacy_applications)

## Basic Setup

### Hardware

The Oculus Rift device connects via HDMI as a secondary display to your graphics card, as well as by USB in order to perform as a sensor. The [oculus-udev](https://aur.archlinux.org/packages/oculus-udev/) package will setup proper [udev](/index.php/Udev "Udev") rules.

You also need to be in the `input` and `video` groups to have full permission, `plugdev` is no longer neccesary (as the mode is set to 0666).

### SDK

The official Oculus Rift SDK is available on the AUR as [oculus-rift-sdk](https://aur.archlinux.org/packages/oculus-rift-sdk/), or a modified version with CMake build support and other features is available as [oculus-rift-sdk-jherico-git](https://aur.archlinux.org/packages/oculus-rift-sdk-jherico-git/).

This package will set up the `oculusd` daemon to run when you start an X session, so it should be running in the background after you've installed it and restarted X (or started it manually).

### Video Mode

For the Rift to function optimally, only certain video modes work very well. In addition, if you have a cloned video mode in which your ordinary monitor runs at a lower refresh rate, then often games will lock themselves to the lower refresh rate.

The Rift itself needs to be the primary monitor, or synchronization will not work properly.

**Note:** Having the display rotated adds an extra frame of latency, which makes it operate at the equivalent of Extended Mode on Windows. With the display unrotated, this extra frame of latency is removed and you get a much improved experience (equivalent of Direct Mode on Windows). Unfortunately only certain applications work correctly with this. You should test each to see if each application works correctly unrotated first.

#### xrandrift

A package exists on the AUR called [riftutilities-git](https://aur.archlinux.org/packages/riftutilities-git/) which contains (currently only) a script called `xrandrift`. It uses `xrandr` to determine suitable video modes (based on arguments passed) to run your rift, as well as trying to record your current video mode, and then switches back after the program exits.

For best latency (for applications which support it), run the programs like so:

```
   xrandrift OculusWorldDemo

```

**Note:** You may experience tearing due to the selected video mode being too big to fit on the same framebuffer as your device. If you see an odd vertical tearing in the Rift, try running with `-o` instead.

For Source games, such as Team Fortress 2 (in properties, set launch options):

```
   xrandrift -e -p %command% -freq 75

```

For games which only run properly at 60Hz:

```
   xrandrift -s -p OculusWorldDemo

```

#### Manually, using xrandr

Say our primary monitor is DVI-I-2, and DVI-I-3 is the Rift, and that 1152x864 is the highest mode that supports 75Hz. To use this:

```
 xrandr --output DVI-I-3 --primary --rotate left --mode 1080x1920 --rate 75 --auto --output DVI-I-2 --mode 1152x864 --rate 75 --auto --same-as DVI-I-3 --scale-from 1920x1080

```

Although the Rift SDK reccomends not rotating the secondary display, not doing so seems to cause issues with a number of programs. This command will set the primary monitor to have a scaled version of the entire display. If you prefer panning, change `--scale-from` to `--panning`.

```
 xrandr --output DVI-I-3 --primary --rotate left --mode 1080x1920 --rate 60 --auto --output DVI-I-2 --mode 1920x1080 --rate 60 --auto --same-as DVI-I-3 --scale-from 1920x1080

```

The above video modes can have some havoc on your display if you simply use xrandr --auto, as it'll still try to scale something. Use this to return to one monitor:

```
 xrandr --output DVI-I-2 --primary --auto --rotate normal --panning 1920x1080 --scale 1x1 --output DVI-I-3 --off

```

## Working applications

See [Virtual Reality#Compatibility matrix](/index.php/Virtual_Reality#Compatibility_matrix "Virtual Reality").

## Troubleshooting

### Kernel log spamming by DK2 camera

If you're receiving an enormous amount of messages in the kernel log that look like this:

```
   xhci_hcd 0000:04:00.0: WARN Successful completion on short TX: needs XHCI_TRUST_TX_LENGTH quirk?

```

this is because the Oculus DK2 Camera has some issues on USB 3.0/Hybrid 2.0/3.0 ports. Try plugging it into a USB 2.0 port.

### Camera misbehaving after suspend/resume

If you try to suspend/resume and then use the Rift, the camera will have issues giving positional tracking data, and any VR program you run will have issues with positional tracking. If you try to kill the `ovrd` process, it will simply lock up and become defunct until the parent process (your window manager) is killed. A temporary workaround is to simply unplug and replug the DK2 camera after resuming, which seems to resolve the issue.

### Inaccurate latency readings for legacy applications

For some reason, it seems that using `ovrd > 0.5.0` with applications compiled against 0.4.4 and below gives a latency reading of many millions of milliseconds (most likely a signed/unsigned change). This means timewarp is always clamped at maximum, and gives a 'swimming' view when using legacy applications. There isn't an ideal fix for this yet, although it is possible to install an old version of the SDK and use that instead.