# Bumblebee

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")
*   [Nouveau](/index.php/Nouveau "Nouveau")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [Intel graphics](/index.php/Intel_graphics "Intel graphics")

From Bumblebee's [FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ):

"_Bumblebee is an effort to make NVIDIA Optimus enabled laptops work in GNU/Linux systems. Such feature involves two graphics cards with two different power consumption profiles plugged in a layered way sharing a single framebuffer._"

## Contents

*   [1 Bumblebee: Optimus for Linux](#Bumblebee:_Optimus_for_Linux)
*   [2 Installation](#Installation)
    *   [2.1 Installing Bumblebee with Intel/NVIDIA](#Installing_Bumblebee_with_Intel.2FNVIDIA)
    *   [2.2 Installing Bumblebee with Intel/Nouveau](#Installing_Bumblebee_with_Intel.2FNouveau)
*   [3 Usage](#Usage)
    *   [3.1 Test](#Test)
    *   [3.2 General usage](#General_usage)
*   [4 Configuration](#Configuration)
    *   [4.1 Optimizing speed](#Optimizing_speed)
        *   [4.1.1 Using VirtualGL as bridge](#Using_VirtualGL_as_bridge)
        *   [4.1.2 Primusrun](#Primusrun)
    *   [4.2 Power management](#Power_management)
        *   [4.2.1 Default power state of NVIDIA card using bbswitch](#Default_power_state_of_NVIDIA_card_using_bbswitch)
        *   [4.2.2 Enable NVIDIA card during shutdown](#Enable_NVIDIA_card_during_shutdown)
    *   [4.3 Multiple monitors](#Multiple_monitors)
        *   [4.3.1 Outputs wired to the Intel chip](#Outputs_wired_to_the_Intel_chip)
        *   [4.3.2 Output wired to the NVIDIA chip](#Output_wired_to_the_NVIDIA_chip)
            *   [4.3.2.1 Using intel-virtual-output](#Using_intel-virtual-output)
            *   [4.3.2.2 xf86-video-intel-virtual-crtc and hybrid-screenclone](#xf86-video-intel-virtual-crtc_and_hybrid-screenclone)
*   [5 Switch between discrete and integrated like Windows](#Switch_between_discrete_and_integrated_like_Windows)
*   [6 CUDA without Bumblebee](#CUDA_without_Bumblebee)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 [VGL] ERROR: Could not open display :8](#.5BVGL.5D_ERROR:_Could_not_open_display_:8)
    *   [7.2 Xlib: extension "GLX" missing on display ":0.0"](#Xlib:_extension_.22GLX.22_missing_on_display_.22:0.0.22)
    *   [7.3 [ERROR]Cannot access secondary GPU: No devices detected](#.5BERROR.5DCannot_access_secondary_GPU:_No_devices_detected)
        *   [7.3.1 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA.280.29:_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
        *   [7.3.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29)
        *   [7.3.3 Could not load GPU driver](#Could_not_load_GPU_driver)
        *   [7.3.4 NOUVEAU(0): [drm] failed to set drm interface version](#NOUVEAU.280.29:_.5Bdrm.5D_failed_to_set_drm_interface_version)
    *   [7.4 /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied](#.2Fdev.2Fdri.2Fcard0:_failed_to_set_DRM_interface_version_1.4:_Permission_denied)
    *   [7.5 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored](#ERROR:_ld.so:_object_.27libdlfaker.so.27_from_LD_PRELOAD_cannot_be_preloaded:_ignored)
    *   [7.6 Fatal IO error 11 (Resource temporarily unavailable) on X server](#Fatal_IO_error_11_.28Resource_temporarily_unavailable.29_on_X_server)
    *   [7.7 Video tearing](#Video_tearing)
    *   [7.8 Bumblebee cannot connect to socket](#Bumblebee_cannot_connect_to_socket)
    *   [7.9 Running X.org from console after login (rootless X.org)](#Running_X.org_from_console_after_login_.28rootless_X.org.29)
    *   [7.10 Primusrun mouse delay/disable VSYNC](#Primusrun_mouse_delay.2Fdisable_VSYNC)
    *   [7.11 Primus issues under compositing window managers](#Primus_issues_under_compositing_window_managers)
    *   [7.12 Problems with bumblebee after resuming from standby](#Problems_with_bumblebee_after_resuming_from_standby)
*   [8 See also](#See_also)

## Bumblebee: Optimus for Linux

[Optimus Technology](http://www.nvidia.com/object/optimus_technology.html) is an _[hybrid graphics](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics)_ implementation without a hardware multiplexer. The integrated GPU manages the display while the dedicated GPU manages the most demanding rendering and ships the work to the integrated GPU to be displayed. When the laptop is running on battery supply, the dedicated GPU is turned off to save power and prolong the battery life. It has also been tested successfully with desktop machines with Intel integrated graphics and an nVidia dedicated graphics card.

Bumblebee is a software implementation comprising of two parts:

*   Render programs off-screen on the dedicated video card and display it on the screen using the integrated video card. This bridge is provided by VirtualGL or primus (read further) and connects to a X server started for the discrete video card.
*   Disable the dedicated video card when it is not in use (see the [#Power management](#Power_management) section)

It tries to mimic the Optimus technology behavior; using the dedicated GPU for rendering when needed and power it down when not in use. The present releases only support rendering on-demand, automatically starting a program with the discrete video card based on workload is not implemented.

## Installation

Before installing Bumblebee, check your BIOS and activate Optimus (older laptops call it "switchable graphics") if possible (BIOS doesn't have to provide this option). If neither "Optimus" or "switchable" is in the bios, still make sure both gpu's will be enabled and that the integrated graphics (igfx) is initial display (primary display). The display should be connected to the onboard integrated graphics, not the discrete graphics card. If integrated graphics had previously been disabled and discrete graphics drivers installed, be sure to remove `/etc/X11/xorg.conf` or the conf file in `/etc/X11/xorg.conf.d` related to the discrete graphics card.

### Installing Bumblebee with Intel/NVIDIA

Install:

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - The main package providing the daemon and client programs.

**Note:** [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) depends on [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl) and provides all [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl), [nvidia-340xx-libgl](https://www.archlinux.org/packages/?name=nvidia-340xx-libgl) and [nvidia-304xx-libgl](https://www.archlinux.org/packages/?name=nvidia-304xx-libgl) to avoid dependency conflict between the respective libgl versions.

*   [mesa](https://www.archlinux.org/packages/?name=mesa) - An open-source implementation of the **OpenGL** specification.
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) - Intel driver.
*   [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [nvidia-340xx](https://www.archlinux.org/packages/?name=nvidia-340xx) or [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) - Install appropriate NVIDIA driver. For more information read [NVIDIA#Installing](/index.php/NVIDIA#Installing "NVIDIA").

For 32-bit ([Multilib](/index.php/Multilib "Multilib") must be enabled) applications support on 64-bit machines, install:

*   [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) - A render/display bridge for 32 bit applications.
*   [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) or [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) or [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) - match the version of the 64 bit package.
*   [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) and make sure that [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) is **not** installed

In order to use Bumblebee, it is necessary to add your regular _user_ to the `bumblebee` group:

```
# gpasswd -a _user_ bumblebee

```

Also [enable](/index.php/Enable "Enable") `bumblebeed.service`. Reboot your system and follow [#Usage](#Usage).

### Installing Bumblebee with Intel/Nouveau

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Bumblebee#](https://wiki.archlinux.org/index.php/Talk:Bumblebee))

**Note:** This method is deprecated and will most likely not work anymore. Use the nvidia module instead. If you want nouveau, use [PRIME](/index.php/PRIME "PRIME").

Install:

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) - experimental 3D acceleration driver.
*   [mesa](https://www.archlinux.org/packages/?name=mesa) - Mesa classic DRI with Gallium3D drivers and 3D graphics libraries.

**Note:** If, when using `primusrun` on a system with the nouveau driver, you are getting:

```
primus: fatal: failed to load any of the libraries: /usr/$LIB/nvidia/libGL.so.1 
/usr/$LIB/nvidia/libGL.so.1: Cannot open shared object file: No such file or directory

```

You should add the following in `/usr/bin/primus` after `PRIMUS_libGL`:

```
export PRIMUS_libGLa='/usr/$LIB/libGL.so.1'

```

If you want, create a new script (for example _primusnouveau_).

## Usage

### Test

Install [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) and use `glxgears` to test if if Bumblebee works with your Optimus system:

```
$ optirun glxgears -info

```

If it fails, try the following commands:

*   64 bit system:

```
$ optirun glxspheres64

```

*   32 bit system:

```
$ optirun glxspheres32

```

If the window with animation shows up - Optimus with Bumblebee is working.

**Note:** If `glxgears` failed, but `glxspheres_XX_` worked, always replace "`glxgears`" with "`glxspheres_XX_`" in all cases.

### General usage

```
$ optirun [options] _application_ [application-parameters]

```

For example, start Windows applications with Optimus:

```
$ optirun wine application.exe

```

For another example, open NVIDIA Settings panel with Optimus:

```
$ optirun -b none nvidia-settings -c :8

```

For a list of the options for `optirun`, view its manual page:

```
$ man optirun

```

## Configuration

You can configure the behaviour of Bumblebee to fit your needs. Fine tuning like speed optimization, power management and other stuff can be configured in `/etc/bumblebee/bumblebee.conf`

### Optimizing speed

#### Using VirtualGL as bridge

Bumblebee renders frames for your Optimus NVIDIA card in an invisible X Server with VirtualGL and transports them back to your visible X Server. Frames will be compressed before they are transported - this saves bandwidth and can be used for speed-up optimization of bumblebee:

To use an other compression method for a single application:

```
$ optirun -c _compress-method_ application

```

The method of compress will affect performance in the GPU/CPU usage. Compressed methods will mostly load the CPU. However, uncompressed methods will mostly load the GPU.

Compressed methods

*   `jpeg`
*   `rgb`
*   `yuv`

Uncompressed methods

*   `proxy`
*   `xv`

Here is a performance table tested with [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV") laptop and benchmark app [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/)<sup><small>AUR</small></sup>:

<table class="wikitable">

<tbody>

<tr>

<th>Command</th>

<th>FPS</th>

<th>Score</th>

<th>Min FPS</th>

<th>Max FPS</th>

</tr>

<tr>

<td>optirun unigine-heaven</td>

<td>25.0</td>

<td>630</td>

<td>16.4</td>

<td>36.1</td>

</tr>

<tr>

<td>optirun -c jpeg unigine-heaven</td>

<td>24.2</td>

<td>610</td>

<td>9.5</td>

<td>36.8</td>

</tr>

<tr>

<td>optirun -c rgb unigine-heaven</td>

<td>25.1</td>

<td>632</td>

<td>16.6</td>

<td>35.5</td>

</tr>

<tr>

<td>optirun -c yuv unigine-heaven</td>

<td>24.9</td>

<td>626</td>

<td>16.5</td>

<td>35.8</td>

</tr>

<tr>

<td>optirun -c proxy unigine-heaven</td>

<td>25.0</td>

<td>629</td>

<td>16.0</td>

<td>36.1</td>

</tr>

<tr>

<td>optirun -c xv unigine-heaven</td>

<td>22.9</td>

<td>577</td>

<td>15.4</td>

<td>32.2</td>

</tr>

</tbody>

</table>

**Note:** Lag spikes occurred when `jpeg` compression method was used.

To use a standard compression for all applications, set the `VGLTransport` to `_compress-method_` in `/etc/bumblebee/bumblebee.conf`:

 `/etc/bumblebee/bumblebee.conf` 

```
[...]
[optirun]
VGLTransport=proxy
[...]
```

You can also play with the way VirtualGL reads back the pixels from your graphic card. Setting `VGL_READBACK` environment variable to `pbo` should increase the performance. Compare these two:

```
# PBO should be faster.
VGL_READBACK=pbo optirun glxgears
# The default value is sync.
VGL_READBACK=sync optirun glxgears

```

**Note:** CPU frequency scaling will affect directly on render performance

#### Primusrun

**Note:** Since compositing hurts performance, invoking primus when a compositing WM is active is not recommended. See [#Primus issues under compositing window managers](#Primus_issues_under_compositing_window_managers).

`primusrun` (from package [primus](https://www.archlinux.org/packages/?name=primus)) is becoming the default choice, because it consumes less power and sometimes provides better performance than `optirun`/`virtualgl`. It may be run separately, but it does not accept options as `optirun` does. Setting `primus` as the bridge for `optirun` provides more flexibility.

For 32-bit applications support on 64-bit machines, install [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus) ([Multilib](/index.php/Multilib "Multilib") must be enabled).

Usage (run separately):

```
$ primusrun glxgears

```

Usage (as a bridge for `optirun`):

The default configuration sets `virtualgl` as the bridge. Override that on the command line:

```
$ optirun -b primus glxgears

```

Or, set `Bridge=primus` in `/etc/bumblebee/bumblebee.conf` and you won't have to specify it on the command line.

**Tip:** Refer to [#Primusrun mouse delay/disable VSYNC](#Primusrun_mouse_delay.2Fdisable_VSYNC) if you want to disable `VSYNC`. It can also remove mouse input delay lag and slightly increase the performance.

### Power management

The goal of the power management feature is to turn off the NVIDIA card when it is not used by Bumblebee any more. If [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) (or [bbswitch-dkms](https://aur.archlinux.org/packages/bbswitch-dkms/)<sup><small>AUR</small></sup>) is installed, it will be detected automatically when the Bumblebee daemon starts. No additional configuration is necessary. However, [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) is for [Optimus laptops only and will not work on desktop computers](https://bugs.launchpad.net/ubuntu/+source/bbswitch/+bug/1338404/comments/6). So, Bumblebee power management is not available for desktop computers, and there is no reason to install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) on a desktop. (Nevertheless, the other features of Bumblebee do work on some desktop computers.)

#### Default power state of NVIDIA card using bbswitch

The default behavior of bbswitch is to leave the card power state unchanged. `bumblebeed` does disable the card when started, so the following is only necessary if you use bbswitch without bumblebeed.

Set `load_state` and `unload_state` module options according to your needs (see [bbswitch documentation](https://github.com/Bumblebee-Project/bbswitch)).

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=1` 

#### Enable NVIDIA card during shutdown

The NVIDIA card may not correctly initialize during boot if the card was powered off when the system was last shutdown. One option is to set `TurnCardOffAtExit=false` in `/etc/bumblebee/bumblebee.conf`, however this will enable the card everytime you stop the Bumblebee daemon, even if done manually. To ensure that the NVIDIA card is always powered on during shutdown, add the following [systemd](/index.php/Systemd "Systemd") service (if using [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)):

 `/etc/systemd/system/nvidia-enable.service` 

```
[Unit]
Description=Enable NVIDIA card
DefaultDependencies=no

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'echo ON > /proc/acpi/bbswitch'

[Install]
WantedBy=shutdown.target
```

Then enable the service by running `systemctl enable nvidia-enable.service` at the root prompt.

### Multiple monitors

#### Outputs wired to the Intel chip

If the port (DisplayPort/HDMI/VGA) is wired to the Intel chip, you can set up multiple monitors with xorg.conf. Set them to use the Intel card, but Bumblebee can still use the NVIDIA card. One example configuration is below for two identical screens with 1080p resolution and using the HDMI out.

 `/etc/X11/xorg.conf` 

```
Section "Screen"
    Identifier     "Screen0"
    Device         "intelgpu0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Screen"
    Identifier     "Screen1"
    Device         "intelgpu1"
    Monitor        "Monitor1"
    DefaultDepth   24
    Option         "TwinView" "0"
    SubSection "Display"
        Depth          24
        Modes          "1980x1080_60.00"
    EndSubSection
EndSection

Section "Monitor"
    Identifier     "Monitor0"
    Option         "Enable" "true"
EndSection

Section "Monitor"
    Identifier     "Monitor1"
    Option         "Enable" "true"
EndSection

Section "Device"
    Identifier     "intelgpu0"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier     "intelgpu1"
    Driver         "intel"
    Option         "XvMC" "true"
    Option         "UseEvents" "true"
    Option         "AccelMethod" "UXA"
    BusID          "PCI:0:2:0"
EndSection

Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection
```

You need to probably change the BusID for both the Intel and the NVIDIA card.

 `$ lspci | grep VGA` 

```
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)

```

The BusID is 0:2:0

#### Output wired to the NVIDIA chip

On some notebooks, the digital Video Output (HDMI or DisplayPort) is hardwired to the NVIDIA chip. If you want to use all the displays on such a system simultaniously, you have to run 2 X Servers. The first will be using the Intel driver for the notebooks panel and a display connected on VGA. The second will be started through optirun on the NVIDIA card, and drives the digital display.

There are currently several instructions on the web how such a setup can be made to work. One can be found on the bumblebee [wiki page](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup). Another approach is described below.

##### Using intel-virtual-output

This method should obsolete the use of _xf86-video-intel-virtual-crtc_ and _hybrid-screenclone_. _intel-virtual-output_ is a tool provided in the _xf86-video-intel driver_ set, as of v2.99\. When run in a terminal, it will daemonize itself unless the `-f` switch is used. Once the tool is running, it activates Bumblebee (Bumblebee can be left as default install), and any displays attached will be automatically detected, and manageable via any desktop display manager such as xrandr or KDE Display.

**Note:** In `/etc/bumblebee/xorg.conf.nvidia` change the lines `UseEDID` and `Option "AutoAddDevices" "false"` to `"true"`, if you are having trouble with device resolution detection.

Commandline usage is as follows:

```
intel-virtual-output [OPTION]... [TARGET_DISPLAY]...
 -d <source display>  source display
 -f                   keep in foreground (do not detach from console and daemonize)
 -b                   start bumblebee
 -a                   connect to all local displays (e.g. :1, :2, etc)
 -S                   disable use of a singleton and launch a fresh intel-virtual-output process
 -v                   all verbose output, implies -f
 -V <category>        specific verbose output, implies -f
 -h                   this help

```

If no target displays are parsed on the commandline, _intel-virtual-output_ will attempt to connect to any local display and then start bumblebee.[[1]](http://cgit.freedesktop.org/xorg/driver/xf86-video-intel/tree/tools/)

The advantage of using _intel-virtual-output_ in foreground mode is that once the external display is disconected, _intel-virtual-output_ can then be killed and bumblebee will disable the nvidia chip. Games can be run on the external screen by first exporting the display `export DISPLAY=:8`, and then running the game with `optirun _game_bin_`, however, cursor and keyboard are not fully captured. Use `export DISPLAY=:0` to revert back to standard operation.

##### xf86-video-intel-virtual-crtc and hybrid-screenclone

This method uses a patched Intel driver, which is extended to have a VIRTUAL Display, and the program hybrid-screenclone which is used to copy the display over from the virtual display to a second X Server which is running on the NVIDIA card using Optirun. Credit goes to [Triple-head monitors on a Thinkpad T520](http://judsonsnotes.com/notes/index.php?option=com_content&view=article&id=673:triple-head-monitors-on-thinkpad-t520&catid=37:tech-notes&Itemid=59) <sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2014-10-03]</sup> which has a detailed explanation on how this is done on a Ubuntu system.

For simplicity, DP is used below to refer to the Digital Output (DisplayPort). The instructions should be the same if the notebook has a HDMI port instead.

*   Set system to use NVIDIA card exclusively, test DP/Monitor combination and generate xorg.nvidia.conf. This step is not required, but recommended if your system Bios has an option to switch the graphics into NVIDIA-only mode. To do this, first uninstall the bumblebee package and install just the NVIDIA driver. Then reboot, enter the Bios and switch the Graphics to NVIDIA-only. When back in Arch, connect you Monitor on DP and use startx to test if it is working in principle. Use Xorg -configure to generate an xorg.conf file for your NVIDIA card. This will come in handy further down below.

*   Reinstall bumlbebee and bbswitch, reboot and set the system Gfx back to Hybrid in the BIOS.
*   Install [xf86-video-intel-virtual-crtc](https://aur.archlinux.org/packages/xf86-video-intel-virtual-crtc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xf86-video-intel-virtual-crtc)]</sup>, and replace your xf86-video-intel package with it.
*   Install [screenclone-git](https://aur.archlinux.org/packages/screenclone-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/screenclone-git)]</sup>
*   Change these bumblebee.conf settings:

 `/etc/bumblebee/bumblebee.conf` 

```
KeepUnusedXServer=true
Driver=nvidia
```

**Note:** Leave the PMMethod set to "bumblebee". This is contrary to the instructions linked in the article above, but on arch this options needs to be left alone so that bbswitch module is automatically loaded

*   Copy the xorg.conf generated in Step 1 to `/etc/X11` (e.g. `/etc/X11/xorg.nvidia.conf`). In the [driver-nvidia] section of `bumblebee.conf`, change `XorgConfFile` to point to it.
*   Test if your `/etc/X11/xorg.nvidia.conf` is working with `startx -- -config /etc/X11/xorg.nvidia.conf`
*   In order for your DP Monitor to show up with the correct resolution in your VIRTUAL Display you might have to edit the Monitor section in your `/etc/X11/xorg.nvidia.conf`. Since this is extra work, you could try to continue with your auto-generated file. Come back to this step in the instructions if you find that the resolution of the VIRTUAL Display as shown by xrandr is not correct.
    *   First you have to generate a Modeline. You can use the tool [amlc](http://zi.fi/amlc/), which will genearte a Modeline if you input a few basic parameters.

Example: 24" 1920x1080 Monitor

start the tool with `amlc -c`

```
Monitor Identifier: Samsung 2494
Aspect Ratio: 2
physical size[cm]: 60
Ideal refresh rate, in Hz: 60
min HSync, kHz: 40
max HSync, kHz: 90
min VSync, Hz: 50
max VSync, Hz: 70
max pixel Clock, MHz: 400
```

This is the Monitor section which `amlc` generated for this input:

```
Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494
```

Change your `xorg.nvidia.conf` to include this Monitor section. You can also trim down your file so that it only contains ServerLayout, Monitor, Device and Screen sections. For reference, here is mine:

 `/etc/X11/xorg.nvidia.conf` 

```
Section "ServerLayout"
        Identifier     "X.org Nvidia DP"
        Screen      0  "Screen0" 0 0
        InputDevice    "Mouse0" "CorePointer"
        InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Monitor"
    Identifier     "Samsung 2494"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

Section "Device"
        Identifier  "DiscreteNvidia"
        Driver      "nvidia"
        BusID       "PCI:1:0:0"
EndSection

Section "Screen"
        Identifier "Screen0"
        Device     "DiscreteNvidia"
        Monitor    "Samsung 2494"
        SubSection "Display"
                Viewport   0 0
                Depth     24
        EndSubSection
EndSection

```

*   Plug in both external monitors and startx. Look at your `/var/log/Xorg.0.log`. Check that your VGA Monitor is detected with the correct Modes there. You should also see a VIRTUAL output with modes show up.
*   Run `xrandr` and three displays should be listed there, along with the supported modes.
*   If the listed Modelines for your VIRTUAL display doesn't have your Monitors native resolution, make note of the exact output name. For me that is `VIRTUAL1`. Then have a look again in the Xorg.0.log file. You should see a message: "Output VIRTUAL1 has no monitor section" there. We will change this by putting a file with the needed Monitor section into `/etc/X11/xorg.conf.d`. Exit and Restart X afterward.

 `/etc/X11/xorg.conf.d/20-monitor_samsung.conf` 

```
Section "Monitor"
    Identifier     "VIRTUAL1"
    ModelName      "Generated by Another Modeline Calculator"
    HorizSync      40-90
    VertRefresh    50-70
    DisplaySize    532 299  # Aspect ratio 1.778:1
    # Custom modes
    Modeline "1920x1080" 174.83 1920 2056 2248 2536 1080 1081 1084 1149             # 174.83 MHz,  68.94 kHz,  60.00 Hz
EndSection  # Samsung 2494

```

*   Turn the NVIDIA card on by running: `sudo tee /proc/acpi/bbswitch <<< ON`
*   Start another X server for the DisplayPort monitor: `sudo optirun true`
*   Check the log of the second X server in `/var/log/Xorg.8.log`
*   Run xrandr to set up the VIRTUAL display to be the right size and placement, eg.: `xrandr --output VGA1 --auto --rotate normal --pos 0x0 --output VIRTUAL1 --mode 1920x1080 --right-of VGA1 --output LVDS1 --auto --rotate normal --right-of VIRTUAL1`
*   Take note of the position of the VIRTUAL display in the list of Outputs as shown by xrandr. The counting starts from zero, i.e. if it is the third display shown, you would specify `-x 2` as parameter to `screenclone` (Note: This might not always be correct. If you see your internal laptop display cloned on the monitor, try `-x 2` anyway.)
*   Clone the contents of the VIRTUAL display onto the X server created by bumblebee, which is connected to the DisplayPort monitor via the NVIDIA chip:

`screenclone -d :8 -x 2`

Thats it, all three displays should be up and running now.

## Switch between discrete and integrated like Windows

In Windows, the way that Optimus works is NVIDIA has a whitelist of applications that require Optimus for, and you can add applications to this whitelist as needed. When you launch the application, it automatically decides which card to use.

To mimic this behavior in Linux, you can use [libgl-switcheroo-git](https://aur.archlinux.org/packages/libgl-switcheroo-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libgl-switcheroo-git)]</sup>. After installing, you can add the below in your .xprofile.

 `~/.xprofile` 

```
mkdir -p /tmp/libgl-switcheroo-$USER/fs
gtkglswitch &
libgl-switcheroo /tmp/libgl-switcheroo-$USER/fs &
```

To enable this, you must add the below to the shell that you intend to launch applications from (I simply added it to the .xprofile file)

```
export LD_LIBRARY_PATH=/tmp/libgl-switcheroo-$USER/fs/\$LIB${LD_LIBRARY_PATH+:}$LD_LIBRARY_PATH

```

Once this has all been done, every application you launch from this shell will pop up a GTK+ window asking which card you want to run it with (you can also add an application to the whitelist in the configuration). The configuration is located in `$XDG_CONFIG_HOME/libgl-switcheroo.conf`, usually `~/.config/libgl-switcheroo.conf`

**Note:** This tool acts by making a FUSE file system and then adding it into the dynamic library searching path, which may lead to slow speed or even segmentation faults when launching a software.

## CUDA without Bumblebee

You can use CUDA without bumblebee. All you need to do is ensure that the nvidia card is on:

```
 # tee /proc/acpi/bbswitch <<< ON

```

Now when you start a CUDA application it is going to automatically load all the necessary modules.

To turn off the nvidia card after using CUDA do:

```
 # rmmod nvidia_uvm
 # rmmod nvidia
 # tee /proc/acpi/bbswitch <<< OFF

```

## Troubleshooting

**Note:** Please report bugs at [Bumblebee-Project](https://github.com/Bumblebee-Project/Bumblebee)'s GitHub tracker as described in its [wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues).

### [VGL] ERROR: Could not open display :8

There is a known problem with some wine applications that fork and kill the parent process without keeping track of it (for example the free to play online game "Runes of Magic")

This is a known problem with VirtualGL. As of bumblebee 3.1, so long as you have it installed, you can use Primus as your render bridge:

```
$ optirun -b primus wine _windows program_.exe

```

If this does not work, an alternative walkaround for this problem is:

```
$ optirun bash
$ optirun wine _windows program_.exe

```

If using NVIDIA drivers a fix for this problem is to edit `/etc/bumblebee/xorg.conf.nvidia` and change Option `ConnectedMonitor` to `CRT-0`.

### Xlib: extension "GLX" missing on display ":0.0"

If you tried to install the NVIDIA driver from NVIDIA website, this is not going to work.

1\. Uninstall that driver in the similar way:

```
# ./NVIDIA-Linux-*.run --uninstall

```

2\. Remove generated by NVIDIA Xorg configuration file:

```
# rm /etc/X11/xorg.conf

```

3\. (Re)install the correct NVIDIA driver: [#Installing Bumblebee with Intel/NVIDIA](#Installing_Bumblebee_with_Intel.2FNVIDIA)

### [ERROR]Cannot access secondary GPU: No devices detected

In some instances, running `optirun` will return:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) No devices detected.
[ERROR]Aborting because fallback start is disabled.

```

In this case, you will need to move the file `/etc/X11/xorg.conf.d/20-intel.conf` to somewhere else, [restart](/index.php/Restart "Restart") the bumblebeed daemon and it should work. If you do need to change some features for the Intel module, a workaround is to merge `/etc/X11/xorg.conf.d/20-intel.conf` to `/etc/X11/xorg.conf`.

It could be also necessary to comment the driver line in `/etc/X11/xorg.conf.d/10-monitor.conf`.

If you're using the `nouveau` driver you could try switching to the `nvidia` driver.

You might need to define the NVIDIA card somewhere (e.g. file `/etc/X11/xorg.conf.d`), using the correct `BusID` according to `lspci` output:

```
Section "Device"
    Identifier "nvidiagpu1"
    Driver "nvidia"
    BusID "PCI:0:1:0"
EndSection

```

Observe that the format of `lspci` output is in HEX, while in xorg it is in decimals. So if the output of `lspci` is, for example, `0a:00.0` the `BusID` should be `PCI:10:0:0`.

#### NVIDIA(0): Failed to assign any connected display devices to X screen 0

If the console output is:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) NVIDIA(0): Failed to assign any connected display devices to X screen 0
[ERROR]Aborting because fallback start is disabled.

```

You can change this line in `/etc/bumblebee/xorg.conf.nvidia`:

```
Option "ConnectedMonitor" "DFP"

```

to:

```
Option "ConnectedMonitor" "CRT"

```

#### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

Add `rcutree.rcu_idle_gp_delay=1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") of the [bootloader](/index.php/Bootloader "Bootloader") configuration (see also the original [BBS post](https://bbs.archlinux.org/viewtopic.php?id=169742) for a configuration example).

#### Could not load GPU driver

If the console output is:

```
[ERROR]Cannot access secondary GPU - error: Could not load GPU driver

```

and if you try to load the nvidia module you get:

```
modprobe nvidia
modprobe: ERROR: could not insert 'nvidia': Exec format error

```

This could be because the nvidia driver is out of sync with the Linux kernel, for example if you installed the latest nvidia driver and haven't updated the kernel in a while. A full system update might resolve the issue. If the problem persists you should try manually compiling the nvidia packages against your current kernel, for example with [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) or by compiling [nvidia](https://www.archlinux.org/packages/?name=nvidia) from the [ABS](/index.php/ABS "ABS").

#### NOUVEAU(0): [drm] failed to set drm interface version

Consider switching to the official nvidia driver. As commented [here](https://github.com/Bumblebee-Project/Bumblebee/issues/438#issuecomment-22005923), nouveau driver has some issues with some cards and bumblebee.

### /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied

This could be worked around by appending following lines in `/etc/bumblebee/xorg.conf.nvidia` (see [here](https://github.com/Bumblebee-Project/Bumblebee/issues/580)):

```
Section "Screen"
    Identifier "Default Screen"
    Device "DiscreteNvidia"
EndSection

```

If you are using [iptables](/index.php/Iptables "Iptables") and receiving this error, it's possible you need to allow communication with localhost so that bumblebee can communicate properly.

```
iptables -A INPUT -i lo -j ACCEPT

```

### ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored

You probably want to start a 32-bit application with bumblebee on a 64-bit system. See the "For 32-bit..." section in [#Installation](#Installation). If the problem persists or if it is a 64-bit application, try using the [primus bridge](#Primusrun).

### Fatal IO error 11 (Resource temporarily unavailable) on X server

Change `KeepUnusedXServer` in `/etc/bumblebee/bumblebee.conf` from `false` to `true`. Your program forks into background and bumblebee don't know anything about it.

### Video tearing

Video tearing is a somewhat common problem on Bumblebee. To fix it, you need to enable vsync. It should be enabled by default on the Intel card, but verify that from Xorg logs. To check whether or not it is enabled for NVIDIA, run:

```
$ optirun nvidia-settings -c :8

```

`X Server XVideo Settings -> Sync to VBlank` and `OpenGL Settings -> Sync to VBlank` should both be enabled. The Intel card has in general less tearing, so use it for video playback. Especially use VA-API for video decoding (e.g. `mplayer-vaapi` and with `-vsync` parameter).

Refer to the [Intel](/index.php/Intel#Video_tearing "Intel") article on how to fix tearing on the Intel card.

If it is still not fixed, try to disable compositing from your desktop environment. Try also disabling triple buffering.

### Bumblebee cannot connect to socket

You might get something like:

```
$ optirun glxspheres64

```

or (for 32 bit):

 `$ optirun glxspheres32` 

```
[ 1648.179533] [ERROR]You've no permission to communicate with the Bumblebee daemon. Try adding yourself to the 'bumblebee' group
[ 1648.179628] [ERROR]Could not connect to bumblebee daemon - is it running?

```

If you are already in the `bumblebee` group (`$ groups | grep bumblebee`), you may try [removing the socket](https://bbs.archlinux.org/viewtopic.php?pid=1178729#p1178729) `/var/run/bumblebeed.socket`.

Another reason for this error could be that you haven't actually turned on both gpu's in your bios, and as a result, the Bumblebee daemon is in fact not running. Check the bios settings carefully and be sure intel graphics (integrated graphics - may be abbreviated in bios as something like igfx) has been enabled or set to auto, and that it's the primary gpu. Your display should be connected to the onboard integrated graphics, not the discrete graphics card.

If you mistakenly had the display connected to the discrete graphics card and intel graphics was disabled, you probably installed Bumblebee after first trying to run Nvidia alone. In this case, be sure to remove the /etc/X11/xorg.conf or .../20-nvidia... configuration files. If Xorg is instructed to use Nvidia in a conf file, X will fail.

### Running X.org from console after login (rootless X.org)

See [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

### Primusrun mouse delay/disable VSYNC

For `primusrun`, `VSYNC` is enabled by default and as a result, it could make mouse input delay lag or even slightly decrease performance. Test `primusrun` without `VSYNC`:

```
$ vblank_mode=0 primusrun glxgears

```

If you want to use it instead of `primusrun`, create new file:

 `/usr/bin/optiprime` 

```
#!/bin/sh
vblank_mode=0 primusrun "$@"

```

Make it executable:

```
# chmod +x /usr/bin/optiprime

```

Usage:

```
$ optiprime glxgears

```

In conclusion, it doesn't make significant performance improvement, but as mentioned above, it should remove mouse input delay lag.

<table class="wikitable">

<tbody>

<tr>

<th>Command</th>

<th>FPS</th>

<th>Score</th>

<th>Min FPS</th>

<th>Max FPS</th>

</tr>

<tr>

<td>optiprime unigine-heaven</td>

<td>31.5</td>

<td>793</td>

<td>22.3</td>

<td>54.8</td>

</tr>

<tr>

<td>primusrun unigine-heaven</td>

<td>31.4</td>

<td>792</td>

<td>18.7</td>

<td>54.2</td>

</tr>

</tbody>

</table>

_Tested with [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV") laptop and benchmark app [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/)<sup><small>AUR</small></sup>._

**Note:** To disable vertical synchronization system-wide, see [Intel graphics#Disable Vertical Synchronization (VSYNC)](/index.php/Intel_graphics#Disable_Vertical_Synchronization_.28VSYNC.29 "Intel graphics").

### Primus issues under compositing window managers

Since compositing hurts performance, invoking primus when a compositing WM is active is not recommended.[[2]](https://github.com/amonakov/primus#issues-under-compositing-wms) If you need to use primus with compositing and see flickering or bad performance, synchronizing primus' display thread with the application's rendering thread may help:

```
$ PRIMUS_SYNC=1 primusrun ...

```

This makes primus display the previously rendered frame.

### Problems with bumblebee after resuming from standby

In some systems, it can happens that the nvidia module is loaded after resuming from standby. The solution for this, is to install the [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) and [acpi](https://www.archlinux.org/packages/?name=acpi) package.

## See also

*   [Bumblebee project repository](http://www.bumblebee-project.org)
*   [Bumblebee project wiki](http://wiki.bumblebee-project.org/)
*   [Bumblebee project bbswitch repository](https://github.com/Bumblebee-Project/bbswitch)

Join us at #bumblebee at freenode.net.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bumblebee&oldid=414751](https://wiki.archlinux.org/index.php?title=Bumblebee&oldid=414751)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Graphics](/index.php/Category:Graphics "Category:Graphics")
*   [X server](/index.php/Category:X_server "Category:X server")