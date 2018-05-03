Hybrid-graphics is a concept involving two graphics cards on same computer. The laptop manufacturers developed new technologies involving two graphic cards in an single computer, with different abilities and power consumptions. Hybrid-graphics is developed to support both high performance and power saving usages.

There are a variety of technologies and each manufacturer developed its own solution to this problem. This technology is well supported on Windows but it's still quite experimental with Linux distributions. Here we try to explain a little about each approach and models and some community solutions to the lack of GNU/Linux systems support.

## Contents

*   [1 First Generation Hybrid Model (Basic Switching)](#First_Generation_Hybrid_Model_.28Basic_Switching.29)
*   [2 Dynamic Switching Model](#Dynamic_Switching_Model)
    *   [2.1 Fully Power Down Discrete GPU](#Fully_Power_Down_Discrete_GPU)
        *   [2.1.1 Using bbswitch](#Using_bbswitch)
        *   [2.1.2 Using acpi_call](#Using_acpi_call)

## First Generation Hybrid Model (Basic Switching)

**Note:** Unless your notebook is from the last decade, it’s most likely using [dynamic switching](#Dynamic_Switching_Model).

The first generation of notebooks with hybrid graphics follow an approach that involves a two graphic card setup with a hardware multiplexer ([MUX](https://en.wikipedia.org/wiki/Multiplexer "wikipedia:Multiplexer")). It allows power save and low-end 3D rendering by using an Integrated Graphics Processor (IGP); or a major power consumption with 3D rendering performance using a Dedicated/Discrete Graphics Processor (DGP). This model makes the user choose (at boot time or at login time) within the two power/graphics profiles and is almost fixed through all the user session. The switch is done by a similar workflow:

*   Turn off the display
*   Turn on the DGP
*   Switch the multiplexer
*   Turn off the IGP
*   Turn the display on again

This switch is somewhat rough and adds some blinks and black screens in laptops that could do it "on the fly". Later approaches made the transition a little more user-friendly.

## Dynamic Switching Model

**Note:** This model is utilized by most manufacturers as of 2016.

Most of the new Hybrid-graphics technologies involve two graphic cards as the [basic switching](#First_Generation_Hybrid_Model_.28Basic_Switching.29) but now the DGP and IGP are plugged to a framebuffer and there is no hardware multiplexer. The IGP is always on and the DGP is switched on/off when there is a need in power-save or performance-rendering. In most cases there is no way to use *only* the DGP and all the switching and rendering is controlled by software. At startup, the Linux kernel starts using a video mode and setting up low-level graphic drivers which will be used by the applications. Most of the Linux distributions then use X.org to create a graphical environment. Finally, a few other softwares are launched, first a login manager and then a window manager, and so on. This hierarchical system has been designed to be used in most of cases on a single graphic card.

**Note:**
Read [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") and [Bumblebee](/index.php/Bumblebee "Bumblebee") for details about NVidia using hybrid graphics with NVidia’s proprietary driver.
Read [PRIME](/index.php/PRIME "PRIME") basically everything else (like AMD Radeon and NVidia GPUs with Nouveau driver).

### Fully Power Down Discrete GPU

You may want to turn off the high-performance graphics processor to save battery power.

#### Using bbswitch

With a NVidia GPU, this can be more safely done using [bbswitch](/index.php/Bbswitch "Bbswitch"), which consists of a kernel package that automatically and issues the correct ACPI calls to disable the discrete GPU when not needed, or automatically at boot.

#### Using acpi_call

Otherwise, and for GPUs not supported by bbswitch, the same can be done manually installing the [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) package.

**Tip:** For kernels not in the [Official repositories](/index.php/Official_repositories "Official repositories"), the [acpi_call-dkms](https://www.archlinux.org/packages/?name=acpi_call-dkms) is an alternative. See also [DKMS](/index.php/DKMS "DKMS").

Once installed load the kernel module:

```
# modprobe acpi_call

```

With the kernel module loaded run the following:

```
# /usr/share/acpi_call/examples/turn_off_gpu.sh

```

This script will go through all the known data buses and attempt to turn them off. You will get an output similar to the following:

```
Trying \_SB.PCI0.P0P1.VGA._OFF: failed
Trying \_SB.PCI0.P0P2.VGA._OFF: failed
Trying \_SB_.PCI0.OVGA.ATPX: failed
Trying \_SB_.PCI0.OVGA.XTPX: failed
Trying \_SB.PCI0.P0P3.PEGP._OFF: failed
Trying \_SB.PCI0.P0P2.PEGP._OFF: failed
Trying \_SB.PCI0.P0P1.PEGP._OFF: failed
Trying \_SB.PCI0.MXR0.MXM0._OFF: failed
Trying \_SB.PCI0.PEG1.GFX0._OFF: failed
Trying \_SB.PCI0.PEG0.GFX0.DOFF: failed
Trying \_SB.PCI0.PEG1.GFX0.DOFF: failed
**Trying \_SB.PCI0.PEG0.PEGP._OFF: works!**
Trying \_SB.PCI0.XVR0.Z01I.DGOF: failed
Trying \_SB.PCI0.PEGR.GFX0._OFF: failed
Trying \_SB.PCI0.PEG.VID._OFF: failed
Trying \_SB.PCI0.PEG0.VID._OFF: failed
Trying \_SB.PCI0.P0P2.DGPU._OFF: failed
Trying \_SB.PCI0.P0P4.DGPU.DOFF: failed
Trying \_SB.PCI0.IXVE.IGPU.DGOF: failed
Trying \_SB.PCI0.RP00.VGA._PS3: failed
Trying \_SB.PCI0.RP00.VGA.P3MO: failed
Trying \_SB.PCI0.GFX0.DSM._T_0: failed
Trying \_SB.PCI0.LPC.EC.PUBS._OFF: failed
Trying \_SB.PCI0.P0P2.NVID._OFF: failed
Trying \_SB.PCI0.P0P2.VGA.PX02: failed
Trying \_SB_.PCI0.PEGP.DGFX._OFF: failed
Trying \_SB_.PCI0.VGA.PX02: failed

```

See the "works"? This means the script found a bus which your GPU sits on and it has now turned off the chip. To confirm this, your battery time remaining should have increased.

Currently, the chip will turn back on with the next reboot. To get around this, add the kernel module to the array of modules to load at boot:

 `/etc/modules-load.d/acpi_call.conf` 
```
#Load 'acpi_call.ko' at boot.

acpi_call
```

To turn off the GPU at boot it is possible to use [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd").

 `/etc/tmpfiles.d/acpi_call.conf` 
```

w /proc/acpi/call - - - - *\\_SB.PCI0.PEG0.PEGP._OFF*
```

The above config will be loaded at boot by systemd. What it does is write the specific OFF signal to the `/proc/acpi/call` file. Obviously, replace the `\_SB.PCI0.PEG0.PEGP._OFF` with the one which works on your system (please note that you need to escape the backslash).

**Tip:** If you are experiencing trouble hibernating or suspending the system after disabling the GPU, try to enable it again by sending the corresponding acpi_call. See also [Suspend/resume service files](/index.php/Power_management#Suspend.2Fresume_service_files "Power management").