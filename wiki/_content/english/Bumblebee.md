Related articles

*   [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")
*   [Nouveau](/index.php/Nouveau "Nouveau")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [Intel graphics](/index.php/Intel_graphics "Intel graphics")

From Bumblebee's [FAQ](https://github.com/Bumblebee-Project/Bumblebee/wiki/FAQ):

	Bumblebee is an effort to make NVIDIA Optimus enabled laptops work in GNU/Linux systems. Such feature involves two graphics cards with two different power consumption profiles plugged in a layered way sharing a single framebuffer.

## Contents

*   [1 Bumblebee: Optimus for Linux](#Bumblebee:_Optimus_for_Linux)
*   [2 Installation](#Installation)
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
        *   [4.2.3 Enable NVIDIA card after waking from suspend](#Enable_NVIDIA_card_after_waking_from_suspend)
    *   [4.3 Multiple monitors](#Multiple_monitors)
        *   [4.3.1 Outputs wired to the Intel chip](#Outputs_wired_to_the_Intel_chip)
        *   [4.3.2 Output wired to the NVIDIA chip](#Output_wired_to_the_NVIDIA_chip)
    *   [4.4 Multiple NVIDIA Graphics Cards](#Multiple_NVIDIA_Graphics_Cards)
*   [5 CUDA without Bumblebee](#CUDA_without_Bumblebee)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 [VGL] ERROR: Could not open display :8](#.5BVGL.5D_ERROR:_Could_not_open_display_:8)
    *   [6.2 Xlib: extension "GLX" missing on display ":0.0"](#Xlib:_extension_.22GLX.22_missing_on_display_.22:0.0.22)
    *   [6.3 [ERROR]Cannot access secondary GPU: No devices detected](#.5BERROR.5DCannot_access_secondary_GPU:_No_devices_detected)
        *   [6.3.1 NVIDIA(0): Failed to assign any connected display devices to X screen 0](#NVIDIA.280.29:_Failed_to_assign_any_connected_display_devices_to_X_screen_0)
        *   [6.3.2 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29)
        *   [6.3.3 Failed to initialize the NVIDIA GPU at PCI:1:0:0 (Bumblebee daemon reported: error: [XORG] (EE) NVIDIA(GPU-0))](#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28Bumblebee_daemon_reported:_error:_.5BXORG.5D_.28EE.29_NVIDIA.28GPU-0.29.29)
        *   [6.3.4 Could not load GPU driver](#Could_not_load_GPU_driver)
        *   [6.3.5 NOUVEAU(0): [drm] failed to set drm interface version](#NOUVEAU.280.29:_.5Bdrm.5D_failed_to_set_drm_interface_version)
    *   [6.4 [ERROR]Cannot access secondary GPU - error: X did not start properly](#.5BERROR.5DCannot_access_secondary_GPU_-_error:_X_did_not_start_properly)
    *   [6.5 /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied](#.2Fdev.2Fdri.2Fcard0:_failed_to_set_DRM_interface_version_1.4:_Permission_denied)
    *   [6.6 ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored](#ERROR:_ld.so:_object_.27libdlfaker.so.27_from_LD_PRELOAD_cannot_be_preloaded:_ignored)
    *   [6.7 Fatal IO error 11 (Resource temporarily unavailable) on X server](#Fatal_IO_error_11_.28Resource_temporarily_unavailable.29_on_X_server)
    *   [6.8 Video tearing](#Video_tearing)
    *   [6.9 Bumblebee cannot connect to socket](#Bumblebee_cannot_connect_to_socket)
    *   [6.10 Running X.org from console after login (rootless X.org)](#Running_X.org_from_console_after_login_.28rootless_X.org.29)
    *   [6.11 Using Primus causes a segmentation fault](#Using_Primus_causes_a_segmentation_fault)
    *   [6.12 Primusrun mouse delay (disable VSYNC)](#Primusrun_mouse_delay_.28disable_VSYNC.29)
    *   [6.13 Primus issues under compositing window managers](#Primus_issues_under_compositing_window_managers)
    *   [6.14 Problems with bumblebee after resuming from standby](#Problems_with_bumblebee_after_resuming_from_standby)
    *   [6.15 Optirun does not work, no debug output](#Optirun_does_not_work.2C_no_debug_output)
    *   [6.16 Broken power management with kernel 4.8](#Broken_power_management_with_kernel_4.8)
    *   [6.17 Lockup issue (lspci hangs)](#Lockup_issue_.28lspci_hangs.29)
    *   [6.18 Discrete card always on and acpi warnings](#Discrete_card_always_on_and_acpi_warnings)
    *   [6.19 Screen 0 deleted because of no matching config section](#Screen_0_deleted_because_of_no_matching_config_section)
    *   [6.20 Erratic, unpredictable behaviour](#Erratic.2C_unpredictable_behaviour)
    *   [6.21 Discrete card always on and nvidia driver cannot be unloaded](#Discrete_card_always_on_and_nvidia_driver_cannot_be_unloaded)
*   [7 See also](#See_also)

## Bumblebee: Optimus for Linux

[Optimus Technology](https://www.nvidia.com/object/optimus_technology.html) is a *[hybrid graphics](https://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics)* implementation without a hardware multiplexer. The integrated GPU manages the display while the dedicated GPU manages the most demanding rendering and ships the work to the integrated GPU to be displayed. When the laptop is running on battery supply, the dedicated GPU is turned off to save power and prolong the battery life. It has also been tested successfully with desktop machines with Intel integrated graphics and an nVidia dedicated graphics card.

Bumblebee is a software implementation comprising two parts:

*   Render programs off-screen on the dedicated video card and display it on the screen using the integrated video card. This bridge is provided by VirtualGL or primus (read further) and connects to a X server started for the discrete video card.
*   Disable the dedicated video card when it is not in use (see the [#Power management](#Power_management) section)

It tries to mimic the Optimus technology behavior; using the dedicated GPU for rendering when needed and power it down when not in use. The present releases only support rendering on-demand, automatically starting a program with the discrete video card based on workload is not implemented.

## Installation

Before installing Bumblebee, check your BIOS and activate Optimus (older laptops call it "switchable graphics") if possible (BIOS does not have to provide this option). If neither "Optimus" or "switchable" is in the bios, still make sure both gpu's will be enabled and that the integrated graphics (igfx) is initial display (primary display). The display should be connected to the onboard integrated graphics, not the discrete graphics card. If integrated graphics had previously been disabled and discrete graphics drivers installed, be sure to remove `/etc/X11/xorg.conf` or the conf file in `/etc/X11/xorg.conf.d` related to the discrete graphics card.

[Install](/index.php/Install "Install"):

*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - The main package providing the daemon and client programs.
*   [mesa](https://www.archlinux.org/packages/?name=mesa) - An open-source implementation of the **OpenGL** specification.
*   An appropriate version of the NVIDIA driver, see [NVIDIA#Installation](/index.php/NVIDIA#Installation "NVIDIA").
*   Optionally install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) - Intel [Xorg](/index.php/Xorg "Xorg") driver.

For 32-bit application support, enable the [multilib](/index.php/Multilib "Multilib") repository and install:

*   [lib32-virtualgl](https://www.archlinux.org/packages/?name=lib32-virtualgl) - A render/display bridge for 32 bit applications.
*   [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) or [lib32-nvidia-340xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-340xx-utils) (match the version of the regular NVIDIA driver).

In order to use Bumblebee, it is necessary to add your regular *user* to the `bumblebee` group:

```
# gpasswd -a *user* bumblebee

```

Also [enable](/index.php/Enable "Enable") `bumblebeed.service`. Reboot your system and follow [#Usage](#Usage).

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

If the window with animation shows up, Optimus with Bumblebee is working.

**Note:** If `glxgears` failed, but `glxspheres*XX*` worked, always replace "`glxgears`" with "`glxspheres*XX*`" in all cases.

### General usage

```
$ optirun [options] *application* [application-parameters]

```

For example, start Windows applications with Optimus:

```
$ optirun wine application.exe

```

For another example, open NVIDIA Settings panel with Optimus:

```
$ optirun -b none nvidia-settings -c :8

```

**Note:** A patched version of [nvdock](https://aur.archlinux.org/packages/nvdock/) is available in the package [nvdock-bumblebee](https://aur.archlinux.org/packages/nvdock-bumblebee/)

For a list of the options for `optirun`, view its manual page:

```
$ man optirun

```

## Configuration

You can configure the behaviour of Bumblebee to fit your needs. Fine tuning like speed optimization, power management and other stuff can be configured in `/etc/bumblebee/bumblebee.conf`

### Optimizing speed

#### Using VirtualGL as bridge

Bumblebee renders frames for your Optimus NVIDIA card in an invisible X Server with VirtualGL and transports them back to your visible X Server. Frames will be compressed before they are transported - this saves bandwidth and can be used for speed-up optimization of bumblebee:

To use another compression method for a single application:

```
$ optirun -c *compress-method* application

```

The method of compress will affect performance in the GPU/CPU usage. Compressed methods will mostly load the CPU. However, uncompressed methods will mostly load the GPU.

Compressed methods

*   `jpeg`
*   `rgb`
*   `yuv`

Uncompressed methods

*   `proxy`
*   `xv`

Here is a performance table tested with [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV") laptop and benchmark app [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/):

| Command | FPS | Score | Min FPS | Max FPS |
| optirun unigine-heaven | 25.0 | 630 | 16.4 | 36.1 |
| optirun -c jpeg unigine-heaven | 24.2 | 610 | 9.5 | 36.8 |
| optirun -c rgb unigine-heaven | 25.1 | 632 | 16.6 | 35.5 |
| optirun -c yuv unigine-heaven | 24.9 | 626 | 16.5 | 35.8 |
| optirun -c proxy unigine-heaven | 25.0 | 629 | 16.0 | 36.1 |
| optirun -c xv unigine-heaven | 22.9 | 577 | 15.4 | 32.2 |

**Note:** Lag spikes occurred when `jpeg` compression method was used.

To use a standard compression for all applications, set the `VGLTransport` to `*compress-method*` in `/etc/bumblebee/bumblebee.conf`:

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

For 32-bit applications support on 64-bit machines, install [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus) ([multilib](/index.php/Multilib "Multilib") must be enabled).

Usage (run separately):

```
$ primusrun glxgears

```

Usage (as a bridge for `optirun`):

The default configuration sets `virtualgl` as the bridge. Override that on the command line:

```
$ optirun -b primus glxgears

```

Or, set `Bridge=primus` in `/etc/bumblebee/bumblebee.conf` and you will not have to specify it on the command line.

**Tip:** Refer to [#Primusrun mouse delay (disable VSYNC)](#Primusrun_mouse_delay_.28disable_VSYNC.29) if you want to disable `VSYNC`. It can also remove mouse input delay lag and slightly increase the performance.

### Power management

The goal of the power management feature is to turn off the NVIDIA card when it is not used by Bumblebee any more. If [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) (for [linux](https://www.archlinux.org/packages/?name=linux)) or [bbswitch-dkms](https://www.archlinux.org/packages/?name=bbswitch-dkms) (for [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) or custom kernels) is installed, it will be detected automatically when the Bumblebee daemon starts. No additional configuration is necessary. However, [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) is for [Optimus laptops only and will not work on desktop computers](https://bugs.launchpad.net/ubuntu/+source/bbswitch/+bug/1338404/comments/6). So, Bumblebee power management is not available for desktop computers, and there is no reason to install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) on a desktop. (Nevertheless, the other features of Bumblebee do work on some desktop computers.)

#### Default power state of NVIDIA card using bbswitch

The default behavior of bbswitch is to leave the card power state unchanged. `bumblebeed` does disable the card when started, so the following is only necessary if you use bbswitch without bumblebeed.

Set `load_state` and `unload_state` module options according to your needs (see [bbswitch documentation](https://github.com/Bumblebee-Project/bbswitch)).

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=1` 

To run bbswitch without bumblebeed on system startup, do not forget to add `bbswitch` to `/etc/modules-load.d`.

#### Enable NVIDIA card during shutdown

On some laptops, the NVIDIA card may not correctly initialize during boot if the card was powered off when the system was last shutdown. Therefore the Bumblebee daemon will power on the GPU when stopping the daemon (e.g. on shutdown) due to the (default) setting `TurnCardOffAtExit=false` in `/etc/bumblebee/bumblebee.conf`. Note that this setting does not influence power state while the daemon is running, so if all `optirun` or `primusrun` programs have exited, the GPU will still be powered off.

When you stop the daemon manually, you might want to keep the card powered off while still powering it on on shutdown. To achieve the latter, add the following [systemd](/index.php/Systemd "Systemd") service (if using [bbswitch](https://www.archlinux.org/packages/?name=bbswitch)):

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

Then [enable](/index.php/Enable "Enable") the `nvidia-enable.service` unit.

#### Enable NVIDIA card after waking from suspend

The bumblebee daemon may fail to activate the graphics card after suspending. A possible fix involves setting [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) as the default method for power management in `/etc/bumblebee/bumblebee.conf`:

 `/etc/bumblebee/bumblebee.conf` 
```
[driver-nvidia]
PMMethod=bbswitch

[driver-nouveau]
PMMethod=bbswitch
```

**Note:** This fix seems to work only after rebooting the system. Restarting the bumblebee service is not enough.

If the above fix fails, try the following command:

```
# echo 1 > /sys/bus/pci/rescan

```

To rescan the PCI bus automatically after a suspend, create a script as described in [Power management#Hooks in /usr/lib/systemd/system-sleep](/index.php/Power_management#Hooks_in_.2Fusr.2Flib.2Fsystemd.2Fsystem-sleep "Power management").

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
        Modes          "1920x1080_60.00"
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
        Modes          "1920x1080_60.00"
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

On some notebooks, the digital Video Output (HDMI or DisplayPort) is hardwired to the NVIDIA chip. If you want to use all the displays on such a system simultaneously, the easiest solution is to use *intel-virtual-output*, a tool provided in the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver set, as of v2.99\. It will allow you to extend the existing X session onto other screens, leveraging virtual outputs to work with the discrete graphics card. Commandline usage is as follows:

 `$ intel-virtual-output [OPTION]... [TARGET_DISPLAY]...` 
```
-d <source display>  source display
-f                   keep in foreground (do not detach from console and daemonize)
-b                   start bumblebee
-a                   connect to all local displays (e.g. :1, :2, etc)
-S                   disable use of a singleton and launch a fresh intel-virtual-output process
-v                   all verbose output, implies -f
-V <category>        specific verbose output, implies -f
-h                   this help
```

If this command alone does not work, you can try running it with optirun to enable the discrete graphics and allow it to detect the outputs accordingly. This is known to be necessary on Lenovo's Legion Y720.

```
$ optirun intel-virtual-output

```

If no target displays are parsed on the commandline, *intel-virtual-output* will attempt to connect to any local display. The detected displays will be manageable via any desktop display manager such as xrandr or KDE Display. The tool will also start bumblebee (which may be left as default install). See the [Bumblebee wiki page](https://github.com/Bumblebee-Project/Bumblebee/wiki/Multi-monitor-setup) for more information.

When run in a terminal, *intel-virtual-output* will daemonize itself unless the `-f` switch is used. Games can be run on the external screen by first exporting the display `export DISPLAY=:8`, and then running the game with `optirun *game_bin*`, however, cursor and keyboard are not fully captured. Use `export DISPLAY=:0` to revert back to standard operation.

If *intel-virtual-output* does not detect displays, see [[1]](https://unix.stackexchange.com/questions/321151/do-not-manage-to-activate-hdmi-on-a-laptop-that-has-optimus-bumblebee) for further configuration to try. If the laptop screen is stretched and the cursor is misplaced while the external monitor shows only the cursor, try killing any running compositing managers.

**Note:** In `/etc/bumblebee/xorg.conf.nvidia` change the lines `Option "UseEDID" "false"` and `Option "AutoAddDevices" "false"` to `"true"`, and comment `Option "ConnectedMonitor"`. If you are having trouble with device resolution detection. You will also need to comment out the line `Option "UseDisplayDevices" "none"` in order to use the display connected to the NVIDIA GPU.

If you don't want to use intel-virtual-output, another option is to configure Bumblebee to leave the discrete GPU on and directly configure X to use both the screens, as it will be able to detect them.

As a last resort, you can run 2 X Servers. The first will be using the Intel driver for the notebook's screen. The second will be started through optirun on the NVIDIA card, to show on the external display. Make sure to disable any display/session manager before manually starting your desktop environment with optirun. Then, you can log in the integrated-graphics powered one.

### Multiple NVIDIA Graphics Cards

If you have multiple NVIDIA graphics cards (eg. when using an eGPU with a laptop with another built in NVIDIA graphics card), you need to make a minor edit to `/etc/bumblebee/xorg.conf.nvidia`. If this change is not made the daemon may default to using the internal NVIDIA card.

First, determine the BusID of the external card:

 `$ lspci | grep -E "VGA|3D"` 
```
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 530 (rev 06)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 960M] (rev a2)
0b:00.0 VGA compatible controller: NVIDIA Corporation GP104 [GeForce GTX 1070] (rev a1)

```

In this case, the BusID is `0b:00.0`.

Now edit `/etc/bumblebee/xorg.conf.nvidia` and add the following line to `Section "Device"`:

 `/etc/bumblebee/xorg.conf.nvidia` 
```
Section "Device"
    ...
    BusID "PCI:11:00:0"
    ...
EndSection

```

**Note:** Notice that the hex `0b` became a base10 `11`

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
$ optirun -b primus wine *windows program*.exe

```

If this does not work, an alternative walkaround for this problem is:

```
$ optirun bash
$ optirun wine *windows program*.exe

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

3\. (Re)install the correct NVIDIA driver: [#Installation](#Installation)

### [ERROR]Cannot access secondary GPU: No devices detected

In some instances, running `optirun` will return:

```
[ERROR]Cannot access secondary GPU - error: [XORG] (EE) No devices detected.
[ERROR]Aborting because fallback start is disabled.

```

In this case, you will need to move the file `/etc/X11/xorg.conf.d/20-intel.conf` to somewhere else, [restart](/index.php/Restart "Restart") the bumblebeed daemon and it should work. If you do need to change some features for the Intel module, a workaround is to merge `/etc/X11/xorg.conf.d/20-intel.conf` to `/etc/X11/xorg.conf`.

It could be also necessary to comment the driver line in `/etc/X11/xorg.conf.d/10-monitor.conf`.

If you are using the `nouveau` driver you could try switching to the `nvidia` driver.

You might need to define the NVIDIA card somewhere (e.g. file `/etc/bumblebee/xorg.conf.nvidia`), using the correct `BusID` according to `lspci` output:

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

After that, restart the Bumblebee service to apply these changes.

#### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (GPU fallen off the bus / RmInitAdapter failed!)

Add `rcutree.rcu_idle_gp_delay=1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") of the [bootloader](/index.php/Bootloader "Bootloader") configuration (see also the original [BBS post](https://bbs.archlinux.org/viewtopic.php?id=169742) for a configuration example).

#### Failed to initialize the NVIDIA GPU at PCI:1:0:0 (Bumblebee daemon reported: error: [XORG] (EE) NVIDIA(GPU-0))

You might encounter an issue when after resume from sleep, `primusrun` or `optirun` command does not work anymore. there are two ways to fix this issue - reboot your system or execute the following command:

```
# echo 1 > /sys/bus/pci/rescan

```

And try to test if `primusrun` or `optirun` works.

If the above command did not help, try finding your NVIDIA card's bus ID:

```
$ lspci | grep NVIDIA

```

For example, above command showed `01:00.0` so we use following commands with this bus ID:

```
# echo 1 > /sys/bus/pci/devices/0000:**01:00.0**/remove
# echo 1 > /sys/bus/pci/rescan

```

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

This could be because the nvidia driver is out of sync with the Linux kernel, for example if you installed the latest nvidia driver and have not updated the kernel in a while. A full system update might resolve the issue. If the problem persists you should try manually compiling the nvidia packages against your current kernel, for example with [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) or by compiling [nvidia](https://www.archlinux.org/packages/?name=nvidia) from the [ABS](/index.php/ABS "ABS").

#### NOUVEAU(0): [drm] failed to set drm interface version

Consider switching to the official nvidia driver. As commented [here](https://github.com/Bumblebee-Project/Bumblebee/issues/438#issuecomment-22005923), nouveau driver has some issues with some cards and bumblebee.

### [ERROR]Cannot access secondary GPU - error: X did not start properly

Set the `"AutoAddDevices"` option to `"true"` in `/etc/bumblebee/xorg.conf.nvidia` (see [here](https://github.com/Bumblebee-Project/Bumblebee/issues/88)):

```
Section "ServerLayout"
    Identifier  "Layout0"
    Option      "AutoAddDevices" "true"
    Option      "AutoAddGPU" "false"
EndSection

```

### /dev/dri/card0: failed to set DRM interface version 1.4: Permission denied

This could be worked around by appending following lines in `/etc/bumblebee/xorg.conf.nvidia` (see [here](https://github.com/Bumblebee-Project/Bumblebee/issues/580)):

```
Section "Screen"
    Identifier "Default Screen"
    Device "DiscreteNvidia"
EndSection

```

### ERROR: ld.so: object 'libdlfaker.so' from LD_PRELOAD cannot be preloaded: ignored

You probably want to start a 32-bit application with bumblebee on a 64-bit system. See the "For 32-bit..." section in [#Installation](#Installation). If the problem persists or if it is a 64-bit application, try using the [primus bridge](#Primusrun).

### Fatal IO error 11 (Resource temporarily unavailable) on X server

Change `KeepUnusedXServer` in `/etc/bumblebee/bumblebee.conf` from `false` to `true`. Your program forks into background and bumblebee do not know anything about it.

### Video tearing

Video tearing is a somewhat common problem on Bumblebee. To fix it, you need to enable vsync. It should be enabled by default on the Intel card, but verify that from Xorg logs. To check whether or not it is enabled for NVIDIA, make sure [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) is installed and run:

```
$ optirun nvidia-settings -c :8

```

`X Server XVideo Settings -> Sync to VBlank` and `OpenGL Settings -> Sync to VBlank` should both be enabled. The Intel card has in general less tearing, so use it for video playback. Especially use VA-API for video decoding (e.g. `mplayer-vaapi` and with `-vsync` parameter).

Refer to [Intel#Tear-free video](/index.php/Intel#Tear-free_video "Intel") on how to fix tearing on the Intel card.

If it is still not fixed, try to disable compositing from your desktop environment. Try also disabling triple buffering.

### Bumblebee cannot connect to socket

You might get something like:

```
$ optirun glxspheres64

```

or (for 32 bit):

 `$ optirun glxspheres32` 
```
[ 1648.179533] [ERROR]You have no permission to communicate with the Bumblebee daemon. Try adding yourself to the 'bumblebee' group
[ 1648.179628] [ERROR]Could not connect to bumblebee daemon - is it running?

```

If you are already in the `bumblebee` group (`$ groups | grep bumblebee`), you may try [removing the socket](https://bbs.archlinux.org/viewtopic.php?pid=1178729#p1178729) `/var/run/bumblebeed.socket`.

Another reason for this error could be that you have not actually turned on both gpu's in your bios, and as a result, the Bumblebee daemon is in fact not running. Check the bios settings carefully and be sure intel graphics (integrated graphics - may be abbreviated in bios as something like igfx) has been enabled or set to auto, and that it's the primary gpu. Your display should be connected to the onboard integrated graphics, not the discrete graphics card.

If you mistakenly had the display connected to the discrete graphics card and intel graphics was disabled, you probably installed Bumblebee after first trying to run Nvidia alone. In this case, be sure to remove the /etc/X11/xorg.conf or .../20-nvidia... configuration files. If Xorg is instructed to use Nvidia in a conf file, X will fail.

### Running X.org from console after login (rootless X.org)

See [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg").

### Using Primus causes a segmentation fault

In some instances, using primusrun instead of optirun will result in a segfault. This is caused by an issue in code auto-detecting faster upload method, see [FS#58933](https://bugs.archlinux.org/task/58933).

The workaround is skipping auto-detection by manually setting `PRIMUS_UPLOAD` [environment variable](/index.php/Environment_variable "Environment variable") to either 1 or 2, depending on which one is faster on your setup.

```
$ PRIMUS_UPLOAD=1 primusrun ...

```

### Primusrun mouse delay (disable VSYNC)

For `primusrun`, `VSYNC` is enabled by default and as a result, it could make mouse input delay lag or even slightly decrease performance. Test `primusrun` with `VSYNC` disabled:

```
$ vblank_mode=0 primusrun glxgears

```

If you are satisfied with the above setting, create an [alias](/index.php/Alias "Alias") (e.g. `alias primusrun="vblank_mode=0 primusrun"`).

Performance comparison:

| VSYNC enabled | FPS | Score | Min FPS | Max FPS |
| FALSE | 31.5 | 793 | 22.3 | 54.8 |
| TRUE | 31.4 | 792 | 18.7 | 54.2 |

*Tested with [ASUS N550JV](/index.php/ASUS_N550JV "ASUS N550JV") notebook and benchmark app [unigine-heaven](https://aur.archlinux.org/packages/unigine-heaven/).*

**Note:** To disable vertical synchronization system-wide, see [Intel graphics#Disable Vertical Synchronization (VSYNC)](/index.php/Intel_graphics#Disable_Vertical_Synchronization_.28VSYNC.29 "Intel graphics").

### Primus issues under compositing window managers

Since compositing hurts performance, invoking primus when a compositing WM is active is not recommended.[[2]](https://github.com/amonakov/primus#issues-under-compositing-wms) If you need to use primus with compositing and see flickering or bad performance, synchronizing primus' display thread with the application's rendering thread may help:

```
$ PRIMUS_SYNC=1 primusrun ...

```

This makes primus display the previously rendered frame.

### Problems with bumblebee after resuming from standby

In some systems, it can happens that the nvidia module is loaded after resuming from standby. One possible solution for this is to install the [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) and [acpi](https://www.archlinux.org/packages/?name=acpi) package.

### Optirun does not work, no debug output

Users are reporting that in some cases, even though Bumblebee was installed correctly, running

```
$ optirun glxgears -info

```

gives no output at all, and the glxgears window does not appear. Any programs that need 3d acceleration crashes:

```
$ optirun bash
$ glxgears
Segmentation fault (core dumped)

```

Apparently it is a bug of some versions of virtualgl. So a workaround is to [install](/index.php/Install "Install") [primus](https://www.archlinux.org/packages/?name=primus) and [lib32-primus](https://www.archlinux.org/packages/?name=lib32-primus) and use it instead:

```
$ primusrun glxspheres64
$ optirun -b primus glxspheres64

```

By default primus locks the framerate to the vrate of your monitor (usually 60 fps), if needed it can be unlocked by passing the `vblank_mode=0` environment variable.

```
$ vblank_mode=0 primusrun glxspheres64

```

Usually there is no need to display more frames han your monitor can handle, but you might want to for benchmarking or to have faster reactions in games (e.g., if a game need 3 frames to react to a mouse movement with `vblank_mode=0` the reaction will be as quick as your system can handle, without it will always need 1/20 of second).

You might want to edit `/etc/bumblebee/bumblebee.conf` to use the primus render as default. If after an update you want to check if the bug has been fixed just use `optirun -b virtualgl`.

See [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1643609) for more information.

### Broken power management with kernel 4.8

If you have a newer laptop (BIOS date 2015 or newer), then Linux 4.8 might break bbswitch ([bbswitch issue 140](https://github.com/Bumblebee-Project/bbswitch/issues/140)) since bbswitch does not support the newer, recommended power management method. As a result, the GPU may fail to power on, fail to power off or worse.

As a workaround, add `pcie_port_pm=off` to your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

Alternatively, if you are only interested in power saving (and perhaps use of external monitors), remove bbswitch and rely on [Nouveau](/index.php/Nouveau "Nouveau") runtime power-management (which supports the new method).

**Note:** Some tools such as `powertop --auto-tune` automatically enable power management on PCI devices, which leads to the same problem [[3]](https://github.com/Bumblebee-Project/bbswitch/issues/159). Use the same workaround or do not use the all-in-one tools.

### Lockup issue (lspci hangs)

See [NVIDIA Optimus#Lockup issue (lspci hangs)](/index.php/NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29 "NVIDIA Optimus")] for an issue that affects new laptops with a GTX 965M (or alike).

### Discrete card always on and acpi warnings

Add `acpi_osi=Linux` to your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). See [[4]](https://github.com/Bumblebee-Project/Bumblebee/issues/592) and [[5]](https://github.com/Bumblebee-Project/bbswitch/issues/112) for more information.

### Screen 0 deleted because of no matching config section

Modify the file xorg.conf.nvidia: First add `Screen 0 "nvidia"` to the section ServerLayout and then create a new section.

```
Section "Screen"
    Identifier     "nvidia"
    Device         "DiscreteNvidia"
EndSection

```

### Erratic, unpredictable behaviour

If Bumblebee starts/works in a random manner, check that you have set your [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") (details [here](https://github.com/Bumblebee-Project/Bumblebee/pull/939)).

### Discrete card always on and nvidia driver cannot be unloaded

Make sure `nvidia-persistenced.service` is disabled and not currently active. It is intended to keep the `nvidia` driver running at all times [[6]](https://us.download.nvidia.com/XFree86/Linux-x86_64/367.57/README/nvidia-persistenced.html), which prevents the card being turned off.

## See also

*   [Bumblebee project repository](https://www.bumblebee-project.org/)
*   [Bumblebee project wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki)
*   [Bumblebee project bbswitch repository](https://github.com/Bumblebee-Project/bbswitch)

Join us at #bumblebee at freenode.net.