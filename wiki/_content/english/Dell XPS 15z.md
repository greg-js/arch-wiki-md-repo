| Device | Status |
| Network | Works |
| Wireless | Works |
| Sound | Works |
| Bluetooth | Works |
| Touchpad | Works |
| Graphics | Modify |
| Screen | Modify |
| USB 3.0 | Not tested |
| Webcam | Works |
| Card Reader | Modify |
| System info | Not tested |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 System Settings](#System_Settings)
*   [2 System Setup](#System_Setup)
    *   [2.1 Hangs on boot](#Hangs_on_boot)
    *   [2.2 Graphics](#Graphics)
        *   [2.2.1 Using Bumblebee](#Using_Bumblebee)
        *   [2.2.2 Video Performance](#Video_Performance)
        *   [2.2.3 Boot time errors](#Boot_time_errors)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Touchpad and keyboard](#Touchpad_and_keyboard)
        *   [2.4.1 Keyboard is not working](#Keyboard_is_not_working)
    *   [2.5 Card Reader](#Card_Reader)

# System Settings

lspci

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation 2nd Generation Core Processor Family PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 6 Series Chipset Family High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 1 (rev b5)
00:1c.1 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 2 (rev b5)
00:1c.3 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 4 (rev b5)
00:1c.4 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 5 (rev b5)
00:1c.5 PCI bridge: Intel Corporation 6 Series Chipset Family PCI Express Root Port 6 (rev b5)
00:1d.0 USB Controller: Intel Corporation 6 Series Chipset Family USB Enhanced Host Controller #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM67 Express Chipset Family LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 6 Series Chipset Family 6 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 6 Series Chipset Family SMBus Controller (rev 05)
01:00.0 VGA compatible controller: nVidia Corporation Device 0df5 (rev ff)
03:00.0 Network controller: Intel Corporation Centrino Advanced-N 6230 (rev 34)
04:00.0 USB Controller: NEC Corporation uPD720200 USB 3.0 Host Controller (rev 04)
06:00.0 Ethernet controller: Atheros Communications Device 1083 (rev c0)

```

# System Setup

## Hangs on boot

Sometimes when booting the laptop with the default kernel it would hang at uevent detection. To prevent this from happening, append the following to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
nox2apic

```

## Graphics

Dell XPS 15z has two graphics processors installed, Intel integrated graphics and NVIDIA GeForce GT 525M. The NVIDIA card is using [Optimus](/index.php/Optimus "Optimus") technology.

See [Intel](/index.php/Intel "Intel") for details on using the Intel GPU.

### Using Bumblebee

Another way, which allows to use Optimus technology is [Bumblebee](/index.php/Bumblebee "Bumblebee").

### Video Performance

Using the Intel card without any modifications can result in poor video performance. A quick fix is to edit boot options of your [boot loader](/index.php/Boot_loader "Boot loader") and append the following to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
i915.semaphores=1

```

### Boot time errors

If you encounter boot time errors with Intel graphics, add the `i915` and `intel_agp` modules to `MODULES` in `/etc/mkinitcpio.conf`:

```
MODULES=(intel_agp i915)

```

Then regenerate the initramfs:

```
# mkinitcpio -p linux

```

## Bluetooth

See [Bluetooth](/index.php/Bluetooth "Bluetooth").

## Touchpad and keyboard

The touchpad is fully supported in kernels 3.9 and later. Make sure to install `xf86-input-synaptics` as well as a program such as synaptiks so that you can customize all of the features.

### Keyboard is not working

In case your keyboard is not working after installing Arch, or after upgrading older installation append the following to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi=noirq

```

As mentioned above, this problem shouldn't occur in new installations, although may in some cases of customized installs.

## Card Reader

To make the card reader function enter the following command:

```
# echo 1 > /sys/bus/pci/rescan

```

This will allow it to auto mount cards until the next reboot.