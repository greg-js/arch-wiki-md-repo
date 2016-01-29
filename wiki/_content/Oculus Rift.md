# Oculus Rift

The Oculus Rift is a virtual reality head-mounted display developed by [Oculus VR](http://www.oculusvr.com/).

## Contents

*   [1 Basic Setup](#Basic_Setup)
    *   [1.1 Hardware](#Hardware)
    *   [1.2 SDK](#SDK)
        *   [1.2.1 Package](#Package)
        *   [1.2.2 From official source](#From_official_source)
    *   [1.3 Video Mode](#Video_Mode)
        *   [1.3.1 xrandrift](#xrandrift)
        *   [1.3.2 Manually, using xrandr](#Manually.2C_using_xrandr)
*   [2 Working applications](#Working_applications)
    *   [2.1 Dolphin VR (Gamecube Emulator)](#Dolphin_VR_.28Gamecube_Emulator.29)
    *   [2.2 Oculus-wine-wrapper](#Oculus-wine-wrapper)
    *   [2.3 Unity games (in wine)](#Unity_games_.28in_wine.29)
    *   [2.4 Minecrift (Minecraft VR)](#Minecrift_.28Minecraft_VR.29)
    *   [2.5 JanusVR](#JanusVR)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Kernel log spamming by DK2 camera](#Kernel_log_spamming_by_DK2_camera)
    *   [3.2 Camera misbehaving after suspend/resume](#Camera_misbehaving_after_suspend.2Fresume)
    *   [3.3 Inaccurate latency readings for legacy applications](#Inaccurate_latency_readings_for_legacy_applications)

## Basic Setup

### Hardware

The Oculus Rift device connects via HDMI as a secondary display to your graphics card, as well as by USB in order to perform as a sensor. The [oculus-udev](https://aur.archlinux.org/packages/oculus-udev/)<sup><small>AUR</small></sup> package will setup proper [udev](/index.php/Udev "Udev") rules.

You also need to be in the `input` and `video` groups to have full permission, `plugdev` is no longer neccesary (as the mode is set to 0666).

### SDK

#### Package

The official Oculus Rift SDK is available on the AUR as [oculus-rift-sdk](https://aur.archlinux.org/packages/oculus-rift-sdk/)<sup><small>AUR</small></sup>, or a modified version with CMake build support and other features is available as [oculus-rift-sdk-jherico-git](https://aur.archlinux.org/packages/oculus-rift-sdk-jherico-git/)<sup><small>AUR</small></sup>.

This package will set up the `oculusd` daemon to run when you start an X session, so it should be running in the background after you've installed it and restarted X (or started it manually).

#### From official source

The SDK is available through the [Oculus VR Developer Center](https://developer.oculusvr.com/) after free registration.

Run a sanity check by compiling the SDK and running the WorldDemo:

```
$ tar zxvf ovr_sdk_linux_4.0.3.tar.gz
$ cd OculusSDK
$ make
$ ./Samples/OculusWorldDemo/Release/OculusWorldDemo_x86_64_Release

```

### Video Mode

For the Rift to function optimally, only certain video modes work very well. In addition, if you have a cloned video mode in which your ordinary monitor runs at a lower refresh rate, then often games will lock themselves to the lower refresh rate.

The Rift itself needs to be the primary monitor, or synchronization will not work properly.

**Note:** Having the display rotated adds an extra frame of latency, which makes it operate at the equivalent of Extended Mode on Windows. With the display unrotated, this extra frame of latency is removed and you get a much improved experience (equivalent of Direct Mode on Windows). Unfortunately only certain applications work correctly with this. You should test each to see if each application works correctly unrotated first.

#### xrandrift

A package exists on the AUR called [riftutilities-git](https://aur.archlinux.org/packages/riftutilities-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/riftutilities-git)]</sup> which contains (currently only) a script called `xrandrift`. It uses `xrandr` to determine suitable video modes (based on arguments passed) to run your rift, as well as trying to record your current video mode, and then switches back after the program exits.

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

Currently there are a handful of apps which work well on the Rift and Linux, with several of them being in the AUR.

### Dolphin VR (Gamecube Emulator)

[dolphin-emu-vr-git](https://aur.archlinux.org/packages/dolphin-emu-vr-git/)<sup><small>AUR</small></sup> is an emulator for Gamecube, with patches to allow it to have full headtracking stereoscopic rendering, as well as a number of customizations to make games work well out of the box in VR (for example, disabling culling functions to let you view the entire world).

**Note:** This application works correctly with Portrait (Direct) Mode, and should be run with the Rift un-rotated.

### Oculus-wine-wrapper

[oculus-wine-wrapper-git](https://aur.archlinux.org/packages/oculus-wine-wrapper-git/)<sup><small>AUR</small></sup> is a utility to patch up the differences between the Linux and Windows versions of the SDK when running Wine. It creates a shared memory context for the Wine application to use, letting the app access the native Oculus SDK. No installation of the SDK to the wineprefix appears to be neccesary.

### Unity games (in wine)

To get the best performance in Unity based games, ideally you should force them into OpenGL mode with the `-force-opengl`. However this is not currently possible with an unpatched wine, as the WGL context it tries to force has some differences from a typical GLX context, [as described here](http://wiki.unity3d.com/index.php/Running_Unity_on_Linux_through_Wine#.22-force-opengl.22_option_crashing_Unity_.28Experimental_fix.29). Using the [wine-unity3d-git](https://aur.archlinux.org/packages/wine-unity3d-git/)<sup><small>AUR</small></sup> package will allow you to run these games with native OpenGL, wrapped in the oculus-wine-wrapper layer, allowing you to play them with decent performance on your machine. Unfortunately they often try to change the video mode or mess with other settings, so supplying default screen settings may be neccesary. Additionally, since it's using native OpenGL, nvidia's __GL_THREADED_OPTIMIZATIONS may be Overall, your command should look something like

```
   env __GL_THREADED_OPTIMIZATIONS=1 oculus-wine-wrapper UnityGame.exe -screen-height 1080 -screen-width 1920 -popupwindow -force-opengl

```

### Minecrift (Minecraft VR)

Though Linux support should be in the main pipeline very soon, the project itself hasn't released an update which includes totally functioning Linux support, although it exists. A guide is available [here](https://www.reddit.com/r/oculus_linux/comments/2shnbk/minecrift_linuxmac_support_coming_soon_steps_to/) to run an existing Minecrift version with the very latest JRift (native java rift runtime) build.

Additionally, many users have reported much better performance with JRE8, rather than JRE7.

**Note:** This application works correctly with Portrait (Direct) Mode, and should be run with the Rift un-rotated. Unfortunately, as of 5/12/15 the ingame GUI will display as an elongated 9:16 rectangle, as opposed to staying at the screen ratio. This is usable but not ideal.

### JanusVR

"janusVR: an immersive, collaborative, multi-dimensional internet." JanusVR is an application that lets you explore 3D websites in a multiplayer experience. An AUR package is available: [janus-vr-browser-bin](https://aur.archlinux.org/packages/janus-vr-browser-bin/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/janus-vr-browser-bin)]</sup>

The AUR package does not automatically update when JanusVR does, but the application will tell you when a new version is available. Simply re-build the package when this happens.

**Note:** This application works correctly with Portrait (Direct) Mode (as of 42.3), and should be run with the Rift un-rotated.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Oculus_Rift&oldid=392510](https://wiki.archlinux.org/index.php?title=Oculus_Rift&oldid=392510)"