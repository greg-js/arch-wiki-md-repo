Virtual reality is the process of simulating an environment for a user, using a variety of peripherals, head mounted displays or CAVEs, and trackers. Instead of showing you a static viewpoint from a screen, it renders your viewpoint relative to where you are standing, on a head-attached or projected surface, to give an effect identical to your own eyes.

A number of peripherals have been released or are about to be released recently which have brought affordable, extremely immersive virtual reality to everyone. Most of these peripherals have full or partial Linux support, and many have AUR packages.

## Contents

*   [1 Compatibility matrix](#Compatibility_matrix)
*   [2 Peripherals and toolkits](#Peripherals_and_toolkits)
    *   [2.1 Oculus Rift](#Oculus_Rift)
    *   [2.2 OpenVR](#OpenVR)
        *   [2.2.1 Setting up](#Setting_up)
        *   [2.2.2 Troubleshooting](#Troubleshooting)
            *   [2.2.2.1 Configuration or startup errors](#Configuration_or_startup_errors)
    *   [2.3 OSVR](#OSVR)
        *   [2.3.1 Setting up](#Setting_up_2)
    *   [2.4 Leap Motion](#Leap_Motion)
        *   [2.4.1 Setting up](#Setting_up_3)
    *   [2.5 OpenHMD](#OpenHMD)
        *   [2.5.1 Installation](#Installation)
*   [3 Supported software](#Supported_software)
    *   [3.1 Dolphin (original VR fork)](#Dolphin_.28original_VR_fork.29)
    *   [3.2 Dolphin (official OSVR support)](#Dolphin_.28official_OSVR_support.29)
    *   [3.3 Games/Programs in Wine](#Games.2FPrograms_in_Wine)
        *   [3.3.1 Unity games](#Unity_games)
    *   [3.4 Minecrift (Minecraft VR)](#Minecrift_.28Minecraft_VR.29)
    *   [3.5 JanusVR](#JanusVR)
        *   [3.5.1 Leap Motion support](#Leap_Motion_support)
*   [4 Other notes](#Other_notes)
    *   [4.1 Enable OpenAL's binaural sound support](#Enable_OpenAL.27s_binaural_sound_support)

## Compatibility matrix

**Legend:**

*   Green: natively supported
*   Yellow: support via toolkit or partial support
*   Red: broken support
*   Uncolored: unknown/unfinished/planned support

 Oculus Rift | OSVR | OpenVR | Leap Motion | Razer Hydra |
| Dolphin (original VR fork) | Partially complete |
| Dolphin (official OSVR support) | Via OSVR | Via OSVR | Via OSVR |
| Minecrift (Minecraft VR) | (Planned) Via OSVR-SteamVR | (Planned) | (Planned) Via OSVR |
| Janus VR | Via OSVR |
| Team Fortress 2 | Via OpenVR | Via OSVR-SteamVR | Support broken and fixed seemingly at random | Via OSVR | Via OSVR |
| Half Life 2 | Displays one black eye, one solid color eye | Via OSVR-SteamVR | Displays one black eye, one solid color eye | Via OSVR | Via OSVR |
| VRUI VR Toolkit and demos |
| 4089: The Ghost Within | Via OpenVR | Via OSVR-SteamVR | Broken until Valve fixes the compositor on Linux | Via OSVR | Via OSVR |
| Games/Programs in Wine | On OVRSDK versions <=0.5.0.0, with [oculus-wine-wrapper-git](https://aur.archlinux.org/packages/oculus-wine-wrapper-git/) and [wine-unity3d-git](https://aur.archlinux.org/packages/wine-unity3d-git/) | Trackers work perfectly. Unity demos without Render Manager 'work' but are buggy, ones using the Render Manager display a white or black screen. |

## Peripherals and toolkits

### Oculus Rift

See [Oculus Rift](/index.php/Oculus_Rift "Oculus Rift").

### OpenVR

OpenVR is an effort by Valve to create an open API for VR development. Unfortunately, while the API is open, the actual default implementation (SteamVR) is not. Fortunately, OSVR (another, more open toolkit with support for a much wider variety of products via plugins) can work as an alternative OpenVR implementation via the OSVR-SteamVR plugin, letting you use any OSVR compatible peripherals with OpenVR compatible games and programs.

#### Setting up

Install [Steam](/index.php/Steam "Steam"), and from it install SteamVR from the tools menu.

#### Troubleshooting

##### Configuration or startup errors

SteamVR/OpenVR create a config directory ~/.openvr that can get misconfigured over the various versions. Delete that directory and completely uninstall/reinstall SteamVR.

It can also apparently have trouble accessing the Rift under some configurations. An alternative is to use the OSVR-SteamVR driver and the OSVR-Oculus-Rift plugin.

### OSVR

OSVR is a joint effort by Sensics, Inc (a long standing VR company) and Razer to create a completely or nearly completely open software API for VR, in which end developers only need to hook their individual headsets into a few functions in order to get first-rate support. It supports the widest variety of peripherals, as well as having extremely flexible config via the JSON config files.

It also provides a plugin which allows it to act as an OpenVR implementation, letting you use it to play OpenVR/SteamVR games with any peripherals it supports.

#### Setting up

Install [osvr-core-git](https://aur.archlinux.org/packages/osvr-core-git/), and whatever plugins are neccesary to support your individual device. Currently available external plugins include:

[osvr-oculus-rift-git](https://aur.archlinux.org/packages/osvr-oculus-rift-git/)

[osvr-leap-motion-git](https://aur.archlinux.org/packages/osvr-leap-motion-git/)

If wish to use OSVR with SteamVR/OpenVR games and applications, install [osvr-steamvr-git](https://aur.archlinux.org/packages/osvr-steamvr-git/) and symlink the driver to your SteamVR installation.

Run the OSVR server and leave it running in the background, by calling it with

```
   osvr_server /usr/share/osvrcore/sample-configs/your_device_config.json

```

You may wish to customize the configuration to suit your individual needs.

To test that your installation is working and your trackers are available, install [osvr-tracker-viewer-git](https://aur.archlinux.org/packages/osvr-tracker-viewer-git/) and run `OSVRTrackerView`. You should see a set of axis for each tracker OSVR can pick up. If you do not, run `osvr_print_tree` to see what trackers are available or if there is a configuration issue.

### Leap Motion

The Leap Motion is an incredibly affordable hand tracker which can easily be mounted on the faceplate of an HMD to allow you to interact with virtual objects. Unfortunately, the latest Orion software is not available for Linux while it is awaiting porting, so the currently available tracking is functional but excessively buggy. As such, it is only really suitable on Linux for social interaction, but seeing as it costs less than 1/10th what an HMD or equivalent tracking system, it is still a fairly useful device.

#### Setting up

Install [leap-motion-driver](https://aur.archlinux.org/packages/leap-motion-driver/), [osvr-leap-motion-git](https://aur.archlinux.org/packages/osvr-leap-motion-git/) and optionally [leap-motion-sdk](https://aur.archlinux.org/packages/leap-motion-sdk/).

To configure, enable and start `leapd.service` and run `LeapControlPanel`. To test that tracking works, run the `Playground` demo included with the installation.

### OpenHMD

[OpenHMD](http://www.openhmd.net/) aims to provide a Free and Open Source API and drivers for immersive technology, such as head mounted displays with built in head tracking. The aim is to implement support for as many devices as possible in a portable, cross-platform package.

OpenHMD supports a wide range of devices such as Oculus Rift, HTC Vive, Sony PSVR, Deepoon E2 and others.

Bindings for .NET, Java, Perl, Python and Rust are available from third-parties.

#### Installation

Install [openhmd-git](https://aur.archlinux.org/packages/openhmd-git/).

## Supported software

Currently there are a handful of apps which work well on the Rift and Linux, with several of them being in the AUR.

### Dolphin (original VR fork)

[dolphin-emu-vr-git](https://aur.archlinux.org/packages/dolphin-emu-vr-git/) is an emulator for Gamecube, with patches to allow it to have full headtracking stereoscopic rendering, as well as a number of customizations to make games work well out of the box in VR (for example, disabling culling functions to let you view the entire world).

Support has for the most part been discontinued, in light of the Dolphin project beginning to officially support OSVR upstream.

**Note:** When using this application with the Rift, it works correctly with Portrait (Direct) Mode, and should be run with the Rift un-rotated to minimize latency.

### Dolphin (official OSVR support)

The Dolphin project has begun to work on adding support for VR officially using OSVR, available through the package [dolphin-emu-osvr-git](https://aur.archlinux.org/packages/dolphin-emu-osvr-git/). It can even use OSVR's path tree inputs as controller inputs, such that you can use a pinch or sixaxis controller input as a wiimote input. Support is limited in places however, as the fork is not as far along as the original Oculus-only fork was.

### Games/Programs in Wine

A number of applications have some level of compatibility when using Wine, but often require some level of tweaks to make them function as expected.

[oculus-wine-wrapper-git](https://aur.archlinux.org/packages/oculus-wine-wrapper-git/) is a utility to patch up the differences between the Linux and Windows versions of the Oculus SDK when running Wine. It creates a shared memory context for the Wine application to use, letting the app access the native Oculus SDK. No installation of the SDK to the wineprefix appears to be necessary.

#### Unity games

To get the best performance in Unity based games, ideally you should force them into OpenGL mode with the `-force-opengl`. However this is not currently possible with an unpatched wine, as the WGL context it tries to force has some differences from a typical GLX context, [as described here](http://wiki.unity3d.com/index.php/Running_Unity_on_Linux_through_Wine#.22-force-opengl.22_option_crashing_Unity_.28Experimental_fix.29). Using the [wine-unity3d-git](https://aur.archlinux.org/packages/wine-unity3d-git/) package will allow you to run these games with native OpenGL, allowing you to play them with decent performance on your machine. Unfortunately they often try to change the video mode or mess with other settings, so supplying default screen settings may be neccesary. Additionally, since it is using native OpenGL, nvidia's __GL_THREADED_OPTIMIZATIONS may give a significant performance gain. Overall, the command should look something like this:

```
   env __GL_THREADED_OPTIMIZATIONS=1 wine UnityGame.exe -screen-height 1080 -screen-width 1920 -popupwindow -force-opengl

```

Or when using [oculus-wine-wrapper-git](https://aur.archlinux.org/packages/oculus-wine-wrapper-git/):

```
   env __GL_THREADED_OPTIMIZATIONS=1 oculus-wine-wrapper UnityGame.exe -screen-height 1080 -screen-width 1920 -popupwindow -force-opengl

```

### Minecrift (Minecraft VR)

A guide is available [here](https://www.reddit.com/r/oculus_linux/comments/2shnbk/minecrift_linuxmac_support_coming_soon_steps_to/) to run an existing Minecrift version with the very latest JRift (native java rift runtime) build. You will likely want to install an older version when using the Rift, as JRift has been updated continuously to match the Oculus SDK.

Additionally, many users have reported much better performance with JRE8, rather than JRE7.

**Note:** When using the Rift, this application works correctly with Portrait (Direct) Mode, and should be run with the Rift un-rotated. Unfortunately, as of 5/12/15 the ingame GUI will display as an elongated 9:16 rectangle, as opposed to staying at the screen ratio. This is usable but not ideal.

### JanusVR

"janusVR: an immersive, collaborative, multi-dimensional internet." JanusVR is an application that lets you explore 3D websites in a multiplayer experience. An AUR package is available: [janusvr](https://aur.archlinux.org/packages/janusvr/)

The AUR package does not automatically update when JanusVR does, but the application will tell you when a new version is available. Simply re-build the package when this happens.

**Note:** This application works correctly with Portrait (Direct) Mode (as of 42.3), and should be run with the Rift un-rotated.

#### Leap Motion support

The Leap Motion allows you to be more expressive with gesture input, seen by other people within the world. You will want to mount your Leap to the front of your HMD and ensure that you are using the default avatar.

## Other notes

### Enable OpenAL's binaural sound support

See [Gaming#Binaural Audio with OpenAL](/index.php/Gaming#Binaural_Audio_with_OpenAL "Gaming").