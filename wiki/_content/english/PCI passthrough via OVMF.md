The Open Virtual Machine Firmware ([OVMF](http://www.tianocore.org/ovmf/)) is a project to enable UEFI support for virtual machines. Starting with Linux 3.9 and recent versions of QEMU, it is now possible to passthrough a graphics card, offering the VM native graphics performance which is useful for graphic-intensive tasks.

Provided you have a desktop computer with a spare GPU you can dedicate to the host (be it an integrated GPU or an old OEM card, the brands do not even need to match) and that your hardware supports it (see [#Prerequisites](#Prerequisites)), it is possible to have a VM of any OS with its own dedicated GPU and near-native performance. For more information on techniques see the background [presentation (pdf)](http://www.linux-kvm.org/images/b/b3/01x09b-VFIOandYou-small.pdf).

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Setting up IOMMU](#Setting_up_IOMMU)
    *   [2.1 Enabling IOMMU](#Enabling_IOMMU)
    *   [2.2 Ensuring that the groups are valid](#Ensuring_that_the_groups_are_valid)
    *   [2.3 Gotchas](#Gotchas)
        *   [2.3.1 Plugging your guest GPU in an unisolated CPU-based PCIe slot](#Plugging_your_guest_GPU_in_an_unisolated_CPU-based_PCIe_slot)
*   [3 Isolating the GPU](#Isolating_the_GPU)
    *   [3.1 Using vfio-pci](#Using_vfio-pci)
    *   [3.2 Using pci-stub (legacy method, pre-4.1 kernels)](#Using_pci-stub_.28legacy_method.2C_pre-4.1_kernels.29)
*   [4 Setting up an OVMF-based guest VM](#Setting_up_an_OVMF-based_guest_VM)
    *   [4.1 Configuring libvirt](#Configuring_libvirt)
    *   [4.2 Setting up the guest OS](#Setting_up_the_guest_OS)
    *   [4.3 Attaching the PCI devices](#Attaching_the_PCI_devices)
    *   [4.4 Gotchas](#Gotchas_2)
        *   [4.4.1 Using a non-EFI image on an OVMF-based VM](#Using_a_non-EFI_image_on_an_OVMF-based_VM)
*   [5 Performance tuning](#Performance_tuning)
    *   [5.1 CPU pinning](#CPU_pinning)
        *   [5.1.1 The case of Hyper-threading](#The_case_of_Hyper-threading)
    *   [5.2 Static huge pages](#Static_huge_pages)
    *   [5.3 CPU frequency governor](#CPU_frequency_governor)
    *   [5.4 High DPC Latency](#High_DPC_Latency)
*   [6 Special procedures](#Special_procedures)
    *   [6.1 Using identical guest and host GPUs](#Using_identical_guest_and_host_GPUs)
    *   [6.2 Passing the boot GPU to the guest](#Passing_the_boot_GPU_to_the_guest)
    *   [6.3 Bypassing the IOMMU groups (ACS override patch)](#Bypassing_the_IOMMU_groups_.28ACS_override_patch.29)
*   [7 Complete example for QEMU (CLI-based) without libvirtd (can switch GPUs without reboot)](#Complete_example_for_QEMU_.28CLI-based.29_without_libvirtd_.28can_switch_GPUs_without_reboot.29)
*   [8 Complete example for QEMU with libvirtd](#Complete_example_for_QEMU_with_libvirtd)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 "Error 43 : Driver failed to load" on Nvidia GPUs passed to Windows VMs](#.22Error_43_:_Driver_failed_to_load.22_on_Nvidia_GPUs_passed_to_Windows_VMs)
    *   [9.2 Unexpected crashes related to CPU exceptions](#Unexpected_crashes_related_to_CPU_exceptions)
    *   [9.3 "System Thread Exception Not Handled" when booting on a Windows VM](#.22System_Thread_Exception_Not_Handled.22_when_booting_on_a_Windows_VM)
    *   [9.4 Slowed down audio pumped through HDMI on the video card](#Slowed_down_audio_pumped_through_HDMI_on_the_video_card)
*   [10 Passing though other devices](#Passing_though_other_devices)
    *   [10.1 USB controller](#USB_controller)
    *   [10.2 Gotchas](#Gotchas_3)
        *   [10.2.1 Passing through a device that does not support resetting](#Passing_through_a_device_that_does_not_support_resetting)
*   [11 Troubleshooting](#Troubleshooting_2)
    *   [11.1 No HDMI audio output on host when intel_iommu is enabled](#No_HDMI_audio_output_on_host_when_intel_iommu_is_enabled)
*   [12 See also](#See_also)

## Prerequisites

A VGA Passthrough relies on a number of technologies that are not ubiquitous as of today and might not be available on your hardware. You will not be able to do this on your machine unless the following requirements are met :

*   Your CPU must support hardware virtualization (for kvm) and IOMMU (for the passthrough itself)
    *   [List of compatible Intel CPUs (Intel VT-x and Intel VT-d)](http://ark.intel.com/search/advanced?s=t&VTX=true&VTD=true)
    *   [List of compatible AMD CPUs (AMD-V and AMD-Vi)](http://support.amd.com/en-us/kb-articles/Pages/GPU120AMDRVICPUsHyperVWin8.aspx)
*   Your motherboard must also support IOMMU
    *   Both the chipset and the BIOS must support it. It is not always easy to tell at a glance whether or not this is the case, but there is a [fairly comprehensive list on the matter on the Xen wiki](http://wiki.xen.org/wiki/VTdHowTo) as well as [another one on Wikipedia](https://en.wikipedia.org/wiki/List_of_IOMMU-supporting_hardware "wikipedia:List of IOMMU-supporting hardware").
*   Your guest GPU ROM must support UEFI
    *   If you can find [any ROM in this list](https://www.techpowerup.com/vgabios/) that applies to your specific GPU and is said to support UEFI, you are generally in the clear. All GPUs from 2012 and later should support this, as Microsoft made UEFI a requirement for devices to be marketed as compatible with Windows 8.

You will probably want to have a spare monitor (the GPU will not display anything if there is no screen plugged in and using a VNC or Spice connection will not help your performance), as well as a mouse and a keyboard you can pass to your VM. If anything goes wrong, you will at least have a way to control your host machine this way.

## Setting up IOMMU

IOMMU is a system specific IO mapping mechanism and can be used with most devices. IOMMU is a generic name for Intel VT-x/Intel and AMD AMD-V/AMD-Vi.

### Enabling IOMMU

Ensure that AMD-VI/VT-d is enabled in your BIOS settings. Both normally show up alongside other CPU features (meaning they could be in an overclocking-related menu) either with their actual names ("Vt-d" or "AMD-VI"), legacy names ("Vanderpool" for Vt-x, "Pacifica" for AMD-V) or in more ambiguous terms such as "Virtualization technology", which may or may not be explained in the manual.

You will also have to enable iommu support in the kernel itself through a [bootloader kernel option](/index.php/Kernel_parameters "Kernel parameters"). Depending on your type of CPU, use either `intel_iommu=on` for Intel CPUs (VT-d) or `amd_iommu=on` for AMD CPUs (AMD-Vi).

After rebooting, check dmesg to confirm that IOMMU has been correctly enabled:

 `dmesg|grep -e DMAR -e IOMMU` 
```
[    0.000000] ACPI: DMAR 0x00000000BDCB1CB0 0000B8 (v01 INTEL  BDW      00000001 INTL 00000001)
[    0.000000] Intel-IOMMU: enabled
[    0.028879] dmar: IOMMU 0: reg_base_addr fed90000 ver 1:0 cap c0000020660462 ecap f0101a
[    0.028883] dmar: IOMMU 1: reg_base_addr fed91000 ver 1:0 cap d2008c20660462 ecap f010da
[    0.028950] IOAPIC id 8 under DRHD base  0xfed91000 IOMMU 1
[    0.536212] DMAR: No ATSR found
[    0.536229] IOMMU 0 0xfed90000: using Queued invalidation
[    0.536230] IOMMU 1 0xfed91000: using Queued invalidation
[    0.536231] IOMMU: Setting RMRR:
[    0.536241] IOMMU: Setting identity map for device 0000:00:02.0 [0xbf000000 - 0xcf1fffff]
[    0.537490] IOMMU: Setting identity map for device 0000:00:14.0 [0xbdea8000 - 0xbdeb6fff]
[    0.537512] IOMMU: Setting identity map for device 0000:00:1a.0 [0xbdea8000 - 0xbdeb6fff]
[    0.537530] IOMMU: Setting identity map for device 0000:00:1d.0 [0xbdea8000 - 0xbdeb6fff]
[    0.537543] IOMMU: Prepare 0-16MiB unity mapping for LPC
[    0.537549] IOMMU: Setting identity map for device 0000:00:1f.0 [0x0 - 0xffffff]
[    2.182790] [drm] DMAR active, disabling use of stolen memory
```

### Ensuring that the groups are valid

The following script should allow you to see how your various PCI devices are mapped to IOMMU groups. If it does not return anything, you either have not enabled IOMMU support properly or your hardware does not support it.

```
#!/bin/bash
shopt -s nullglob
for d in /sys/kernel/iommu_groups/*/devices/*; do 
    n=${d#*/iommu_groups/*}; n=${n%%/*}
    printf 'IOMMU Group %s ' "$n"
    lspci -nns "${d##*/}"
done;

```

Example output:

```
IOMMU Group 0 00:00.0 Host bridge [0600]: Intel Corporation 2nd Generation Core Processor Family DRAM Controller [8086:0104] (rev 09)
IOMMU Group 1 00:16.0 Communication controller [0780]: Intel Corporation 6 Series/C200 Series Chipset Family MEI Controller #1 [8086:1c3a] (rev 04)
IOMMU Group 2 00:19.0 Ethernet controller [0200]: Intel Corporation 82579LM Gigabit Network Connection [8086:1502] (rev 04)
IOMMU Group 3 00:1a.0 USB controller [0c03]: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #2 [8086:1c2d] (rev  
...

```

An IOMMU group is the smallest set of physical devices that can be passed to a virtual machine. For instance, in the example above, both the GPU in 06:00.0 and its audio controller in 6:00.1 belong to IOMMU group 13 and can only be passed together. The frontal USB controller, however, has its own group (group 2) which is separate from both the USB expansion controller (group 10) and the rear USB controller (group 4), meaning that [any of them could be passed to a VM without affecting the others](#USB_controller).

### Gotchas

#### Plugging your guest GPU in an unisolated CPU-based PCIe slot

Not all PCI-E slots are the same. Most motherboards have PCIe slots provided by both the CPU and the PCH. Depending on your CPU, it is possible that your processor-based PCIe slot does not support isolation properly, in which case the PCI slot itself will be appear to be grouped with the device that is connected to it.

```
IOMMU Group 1 00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port (rev 09)
IOMMU Group 1 01:00.0 VGA compatible controller: NVIDIA Corporation GM107 [GeForce GTX 750] (rev a2)
IOMMU Group 1 01:00.1 Audio device: NVIDIA Corporation Device 0fbc (rev a1)

```

This is fine so long as only your guest GPU is included in here, such as above. Depending on what is plugged in your other PCIe slots and whether they are allocated to your CPU or your PCH, you may find yourself with additional devices within the same group, which would force you to pass those as well. If you are ok with passing everything that is in there to your VM, you are free to continue. Otherwise, you will either need to try and plug your GPU in your other PCIe slots (if you have any) and see if those provide isolation from the rest or to install the ACS override patch, which comes with its own drawbacks.

**Note:** If they are grouped with other devices in this manner, pci root ports and bridges should neither be bound to vfio at boot, nor be added to the VM.

## Isolating the GPU

Due to their size and complexity, GPU drivers do not tend to support dynamic rebinding very well, so you cannot just have some GPU you use on the host be transparently passed to a VM without consequences. It is generally preferable to bind them with a placeholder driver instead. This will stop other drivers from attempting to claim it, and will force the GPU to remain inactive while a VM is not running. There are two methods for doing this, but it is recommended to use vfio-pci if your kernel supports it.

**Warning:** Once you reboot after this procedure, whatever GPU you have configured will no longer be usable on the host until you reverse the manipulation. Make sure the GPU you intend to use on the host is properly configured before doing this.

### Using vfio-pci

Starting with Linux 4.1, the kernel includes vfio-pci, which is functionally similar to pci-stub with a few added bonuses, such as switching devices into their D3 state when they are not in use. If your system supports it, which you can try by running the following command, you should use it. If it returns en error, you will have to rely on pci-stub instead.

 `$ modinfo vfio-pci` 
```
filename:       /lib/modules/4.4.5-1-ARCH/kernel/drivers/vfio/pci/vfio-pci.ko.gz
description:    VFIO PCI - User Level meta-driver
author:         Alex Williamson <alex.williamson@redhat.com>
...
```

Vfio-pci normally targets PCI devices by ID, meaning you only need to specify the IDs of the devices you intend to passthrough. For the following IOMMU group, you would want to bind vfio-pci with `10de:13c2` and `10de:0fbb`, which will be used as example values for the rest of this section.

```
IOMMU Group 13 06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
IOMMU Group 13 06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)}}

```

**Note:** You cannot specify which device to isolate using vendor-device ID pairs if the host GPU and the guest GPU share the same pair (i.e : if both are the same model). If this is your case, read the [Special procedures](#Using_identical_guest_and_host_GPUs) section instead.

You can then add those vendor-device ID pairs to the default parameters passed to vfio-pci whenever it is inserted into the kernel.

 `/etc/modprobe.d/vfio.conf`  `options vfio-pci ids=10de:13c2,10de:0fbb` 
**Note:** If, as noted [here](#Plugging_your_guest_GPU_in_an_unisolated_CPU-based_PCIe_slot), your pci root port is part of your IOMMU group, you **must not** pass its ID to `vfio-pci`, as it needs to remain attached to the host to function properly. Any other device within that group, however, should be left for `vfio-pci` to bind with.

This, however, does not guarantee that vfio-pci will be loaded before other graphics drivers. To ensure that, we need to statically bind it in the kernel image by adding it anywhere in the MODULES list in mkinitpcio.conf, alongside with its dependencies.

**Note:** If you also have another driver loaded this way for [early modesetting](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") (such as "nouveau", "radeon", "amdgpu", "i915", etc.), all of the following VFIO modules must preceed it.
 `/etc/mkinitcpio.conf`  `MODULES="... vfio vfio_iommu_type1 vfio_pci vfio_virqfd ..."` 

Also, ensure that the modconf hook is included in the HOOKS list of mkinitcpio.conf:

 `/etc/mkinitcpio.conf`  `HOOKS="... modconf ..."` 

Since new modules have been added to the initramfs configuration, it must be regenerated. Should you change the IDs of the devices in `/etc/modprobe.d/vfio.conf`, you will also have to regenerate it, as those parameters must be specified in the initramfs to be known during the early boot stages.

 `# mkinitcpio -p linux` 
**Note:** If you are using a non-standard kernel, such as `linux-vfio`, replace `linux` with whichever kernel you intend to use.

Reboot and verify that vfio-pci has loaded properly and that it is now bound to the right devices.

 `$ dmesg | grep -i vfio ` 
```
[    0.329224] VFIO - User Level meta-driver version: 0.3
[    0.341372] vfio_pci: add [10de:13c2[ffff:ffff]] class 0x000000/00000000
[    0.354704] vfio_pci: add [10de:0fbb[ffff:ffff]] class 0x000000/00000000
[    2.061326] vfio-pci 0000:06:00.0: enabling device (0100 -> 0103)
```

It isn't necessary for all devices (or even expected device) from vfio.conf to be in dmesg output. Sometimes device doesn't appear in output at boot but actually is able to be visible and operatable in guest VM.

 `$ lspci -nnk -d 10de:13c2` 
```
06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	Kernel driver in use: vfio-pci
	Kernel modules: nouveau nvidia
```
 `$ lspci -nnk -d 10de:0fbb` 
```
06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)
	Kernel driver in use: vfio-pci
	Kernel modules: snd_hda_intel
```

### Using pci-stub (legacy method, pre-4.1 kernels)

If your kernel does not support vfio-pci, you can use the pci-stub module instead.

Pci-stub normally targets PCI devices by ID, meaning you only need to specify the IDs of the devices you intend to passthrough. For the following IOMMU group, you would want to bind vfio-pci with `10de:13c2` and `10de:0fbb`, which will be used as example values for the rest of this section.

```
IOMMU group 13 06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
IOMMU group 13 06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)}}

```

**Note:** You cannot specify which device to isolate using vendor-device ID pairs if the host GPU and the guest GPU share the same pair (i.e : if both are the same model). If this is your case, read the [Special procedures](#Using_identical_guest_and_host_GPUs) section instead.

Most linux distros (including Arch Linux) have pci-stub built statically within the kernel image. If for any reason it needs to be loaded as a module in your case, you will need to bind it yourself using whatever tool your distro provides for this, such as `mkinitpcio` for Arch.

 `/etc/mkinitcpio.conf`  `MODULES="... pci-stub ..."` 

If you did need to add this module to your kernel image configuration manually, you must also regenerate it.

 `# mkinitcpio -p linux` 
**Note:** If you are using a non-standard kernel, such as `linux-vfio`, replace `linux` with whichever kernel you intend to use.

Add the relevant PCI device IDs to the kernel command line:

 `/etc/default/grub` 
```
...
GRUB_CMDLINE_LINUX_DEFAULT="... pci-stub.ids=10de:13c2,10de:0fbb ..."
...
```

**Note:** If, as noted [here](#Plugging_your_guest_GPU_in_an_unisolated_CPU-based_PCIe_slot), your pci root port is part of your IOMMU group, you **must not** pass its ID to `pci-stub`, as it needs to remain attached to the host to function properly. Any other device within that group, however, should be left for `pci-stub` to bind with.

Reload the grub configuration:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

Check dmesg output for successful assignment of the device to pci-stub:

 `dmesg | grep pci-stub` 
```
[    2.390128] pci-stub: add 10DE:13C2 sub=FFFFFFFF:FFFFFFFF cls=00000000/00000000
[    2.390143] pci-stub 0000:06:00.0: claimed by stub
[    2.390150] pci-stub: add 10DE:0FBB sub=FFFFFFFF:FFFFFFFF cls=00000000/00000000
[    2.390159] pci-stub 0000:06:00.1: claimed by stub
```

## Setting up an OVMF-based guest VM

OVMF is an open-source UEFI firmware for QEMU virtual machines. While it's possible to use SeaBIOS to get similar results to an actual PCI passthough, the setup process is different and it is generally preferable to use the EFI method if your hardware supports it.

### Configuring libvirt

[Libvirt](/index.php/Libvirt "Libvirt") is a wrapper for a number of virtualization utilities that greatly simplifies the configuration and deployment process of virtual machines. In the case of KVM and QEMU, the frontend it provides allows us to avoid dealing with the permissions for QEMU and make it easier to add and remove various devices on a live VM. Its status as a wrapper, however, means that it might not always support all of the latest qemu features, which could end up requiring the use of a wrapper script to provide some extra arguments to QEMU.

After installing [qemu](https://www.archlinux.org/packages/?name=qemu), [libvirt](https://www.archlinux.org/packages/?name=libvirt), [ovmf-git](https://aur.archlinux.org/packages/ovmf-git/) and [virt-manager](https://www.archlinux.org/packages/?name=virt-manager), add the path to your OVMF firmware image and runtime variables template to your libvirt config so `virt-install` or `virt-manager` can find those later on.

 `/etc/libvirt/qemu.conf` 
```
nvram = [
	"/usr/share/ovmf/x64/ovmf_x64.bin:/usr/share/ovmf/x64/ovmf_vars_x64.bin"
]

```

You can now [enable](/index.php/Enable "Enable") and start `libvirtd` and its logging component.

```
# systemctl enable --now libvirtd
# systemctl enable virtlogd.socket
```

### Setting up the guest OS

The process of setting up a VM using `virt-manager` is mostly self explainatory, as most of the process comes with fairly comprehensive on-screen instructions. However, you should pay special attention to the following steps :

*   When the VM creation wizard asks you to name your VM, check the "Customize before install" checkbox.
*   In the "Overview" section, set your firmware to "UEFI". If the option is grayed out, make sure that you have correctly specified the location of your firmware in `/etc/libvirt/qemu.conf` and restart `libvirtd.service`.
*   In the "CPUs" section, change your CPU model to "host-passthrough". If it is not in the list, you will have to type it by hand. This will ensure that your CPU is detected properly, since it causes libvirt to expose your CPU capabilities exactly as they are instead of only those it recognizes (which is the preferred default behavior to make CPU behavior easier to reproduce). Without it, some applications may complain about your CPU being of an unknown model.
*   If you want to minimize IO overhead, go into "Add Hardware" and add a Controller for SCSI drives of the "VirtIO SCSI" model. You can then change the default IDE disk for a SCSI disk, which will bind to said controller.
    *   Windows VMs will not recognize those drives by default, so you need to download the ISO containing the drivers from [here](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/latest-virtio/) and add an IDE (or SATA for Windows 8.1 and newer) CD-ROM storage device linking to said ISO, otherwise you will not be able to get Windows to recognize it during the installation process. When prompted to select a disk to install windows on, load the drivers contained on the CD-ROM under *vioscsi*.

The rest of the installation process will take place as normal using a standard QXL video adapter running in a window. At this point, there is no need to install additional drivers for the rest of the virtual devices, since most of them will be removed later on. Once the guest OS is done installing, simply turn off the virtual machine.

### Attaching the PCI devices

With the installation done, it's now possible to edit the hardware details in libvirt and remove virtual integration devices, such as the spice channel and virtual display, the QXL video adapter, the emulated mouse and keyboard and the USB tablet device. Since that leaves you with no input devices, you may want to bind a few USB host devices to your VM as well, but remember to **leave at least one mouse and/or keyboard assigned to your host** in case something goes wrong with the guest. At this point, it also becomes possible to attach the PCI device that was isolated earlier; simply click on "Add Hardware" and select the PCI Host Devices you want to passthrough. If everything went well, the screen plugged into your GPU should show the OVMF splash screen and your VM should start up normally. From there, you can setup the drivers for the rest of your VM.

### Gotchas

#### Using a non-EFI image on an OVMF-based VM

The OVMF firmware does not support booting off non-EFI mediums. If the installation process drops you in a UEFI shell right after booting, you may have an invalid EFI boot media. Try using an alternate linux/windows image to determine if you have an invalid media.

## Performance tuning

Most use cases for PCI passthroughs relate to performance-intensive domains such as video games and GPU-accelerated tasks. While a PCI passthrough on its own is a step towards reaching native performance, there are still a few ajustments on the host and guest to get the most out of your VM.

### CPU pinning

The default behavior for KVM guests is to run operations coming from the guest as a number of threads representing virtual processors. Those threads are managed by the Linux scheduler like any other thread and are dispatched to any available CPU cores based on niceness and priority queues. Since switching between threads adds a bit of overhead (because context switching forces the core to change its cache between operations), this can noticeably harm performance on the guest. CPU pinning aims to resolve this as it overrides process scheduling and ensures that the VM threads will always run and only run on those specific cores. Here, for instance, the guest cores 0, 1, 2 and 3 are mapped to the host cores 4, 5, 6 and 7 respectively.

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<vcpu placement='static'>4</vcpu>
<cputune>
    <vcpupin vcpu='0' cpuset='4'/>
    <vcpupin vcpu='1' cpuset='5'/>
    <vcpupin vcpu='2' cpuset='6'/>
    <vcpupin vcpu='3' cpuset='7'/>
</cputune>
...
```

#### The case of Hyper-threading

If your CPU supports hardware multitasking, also known as Hyper-threading on Intel chips, there are two ways you can go with your CPU pinning. That is, Hyper-threading is simply a very efficient way of running two threads on one CPU at any given time, so while it may give you 8 logical cores on what would otherwise be a quad-core CPU, if the physical core is overloaded, the logical core won't be of any use. One could pin their VM threads on 2 physical cores and their 2 respective threads, but any task overloading those two cores won't be helped by the extra two logical cores, since in the end you're only passing through two cores out of four, not four out of eight. What you should do knowing this depends on what you intend to do with your host while your VM is running.

This is the abridged content of `/proc/cpuinfo` on a quad-core machine with hyper-threading.

 `$ cat /proc/cpuinfo | grep -e "processor" -e "core id" -e "^$"` 
```
processor	: 0
core id		: 0

processor	: 1
core id		: 1

processor	: 2
core id		: 2

processor	: 3
core id		: 3

processor	: 4
core id		: 0

processor	: 5
core id		: 1

processor	: 6
core id		: 2

processor	: 7
core id		: 3
```

If you don't intend to be doing any computation-heavy work on the host (or even anything at all) at the same time as you would on the VM, it would probably be better to pin your VM threads across all of your logical cores, so that the VM can fully take advantage of the spare CPU time on all your cores.

On the quad-core machine mentioned above, it would look like this :

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<vcpu placement='static'>4</vcpu>
<cputune>
    <vcpupin vcpu='0' cpuset='4'/>
    <vcpupin vcpu='1' cpuset='5'/>
    <vcpupin vcpu='2' cpuset='6'/>
    <vcpupin vcpu='3' cpuset='7'/>
</cputune>
...
<cpu mode='custom' match='exact'>
    ...
    <topology sockets='1' cores='4' threads='1'/>
    ...
</cpu>
...
```

If you would instead prefer to have the host and guest running intensive tasks at the same time, it would then be preferable to pin a limited amount of physical cores and their respective threads on the guest and leave the rest to the host to avoid the two competing for CPU time.

On the quad-core machine mentioned above, it would look like this :

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<vcpu placement='static'>4</vcpu>
<cputune>
    <vcpupin vcpu='0' cpuset='2'/>
    <vcpupin vcpu='1' cpuset='3'/>
    <vcpupin vcpu='2' cpuset='6'/>
    <vcpupin vcpu='3' cpuset='7'/>
</cputune>
...
<cpu mode='custom' match='exact'>
    ...
    <topology sockets='1' cores='2' threads='2'/>
    ...
</cpu>
...
```

### Static huge pages

When dealing with applications that require large amounts of memory, memory latency can become a problem since the more memory pages are being used, the more likely it is that this application will attempt to access information accross multiple memory "pages", which is the base unit for memory allocation. Resolving the actual address of the memory page takes multiple steps, and so CPUs normally cache information on recently used memory pages to make subsequent uses on the same pages faster. Applications using large amounts of memory run into a problem where, for instance, a virtual machine uses 4GB of memory divided into 4kB pages (which is the default size for normal pages), meaning that such cache misses can become extremely frequent and greatly increase memory latency. Huge pages exist to mitigate this issue by giving larger individual pages to those applications, increasing the odds that multiple operations will target the same page in succession. This is normally handeled with transparent huge pages, which dynamically manages hugepages to keep up with the demand.

On a VM with a PCI passthrough, however, it is **not possible** to benefit from transparent huge pages, as IOMMU requires that the guest's memory be allocated and pinned as soon as the VM starts. It is therefore required to allocate huge pages statically in order to benefit from them.

**Warning:** Do note that static huge pages lock down the allocated amount of memory, making it unavailable for applications that are not configured to use them. Allocating 4GBs worth of huge pages on a machine with 8GBs of memory will only leave you with 4GBs of available memory on the host **even when the VM is not running**.

To allocate huge pages at boot, one must simply specify the desired amount on their kernel comand line with `hugepages=x`. For instance, reserving 1024 pages with `hugepages=1024` and the default size of 2048kB per huge page creates 2GBs worth of memory for the virtual machine to use.

Also, since static huge pages can only be used by applications that specifically request it, you must add this section in your libvirt domain configuration to allow kvm to benefit from them :

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<memoryBacking>
	<hugepages/>
</memoryBacking>
...
```

### CPU frequency governor

Depending on the way your [CPU governor](/index.php/CPU_frequency_scaling "CPU frequency scaling") is configured, the VM threads may not hit the CPU load thresholds for the frequency to ramp up. Indeed, KVM cannot actually change the CPU frequency on its own, which can be a problem if the it does not scale up with vCPU usage as it would result in underwhelming performance. An easy way to see if it behaves correctly is to check if the frequency reported by `watch lscpu` goes up when running a CPU-intensive task on the guest. If you are indeed experiencing stutter and the frequency does not go up to reach its reported maximum, it may be due to [cpu scaling being controlled by the host OS](https://lime-technology.com/forum/index.php?topic=46664.msg447678#msg447678). In this case, try setting all cores to maximum frequency to see if this improves performance. Note that if you're using a modern intel chip with the default pstate driver, cpupower commands will be [ineffective](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling"), so monitor `/proc/cpuinfo` to make sure your cpu is actually at max frequency.

### High DPC Latency

If you are experiencing high DPC and/or interrupt latency in your Guest VM, ensure you have [loaded the needed virtio kernel modules](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") on the host kernel. Loadable virtio kernel modules include: `virtio-pci, virtio-net, virtio-blk, virtio-balloon, virtio-ring` and `virtio`.

After loading one or more of these modules, `lsmod | grep virtio` executed on the host should not return empty.

## Special procedures

Certain setups require specific configuration tweaks in order to work properly. If you're having problems getting your host or your VM to work properly, see if your system matches one of the cases below and try adjusting your configuration accordingly.

### Using identical guest and host GPUs

Due to how both pci-stub and vfio-pci use your vendor and device id pair to identify which device they need to bind to at boot, if you have two GPUs sharing such an ID pair you won't be able to get your passthough driver to bind with just one of them. This sort of setup makes it necessary to use a script, so that whichever driver you're using is instead assigned by pci bus address using the `driver_override` mechanism.

Here, we will make a script to bind vfio-pci to all GPUs but the boot gpu. Create the script "/sbin/vfio-pci-override.sh":

```
   #!/bin/sh

   for i in /sys/devices/pci*/*/boot_vga; do
           if [ $(cat "$i") -eq 0 ]; then
                   GPU="${i%/boot_vga}"
                   AUDIO="$(echo "$GPU" | sed -e "s/0$/1/")"
                   echo "vfio-pci" > "$GPU/driver_override"
                   if [ -d "$AUDIO" ]; then
                           echo "vfio-pci" > "$AUDIO/driver_override"
                   fi
           fi
   done

   modprobe -i vfio-pci

```

Create /etc/modprobe.d/vfio.conf with the following:

```
   install vfio-pci /sbin/vfio-pci-override.sh

```

Edit /etc/mkinitcpio.conf

Remove any video drivers from MODULES, and add vfio-pci, and vfio_iommu_type1

```
   MODULES="ext4 vfat vfio-pci vfio_iommu_type1"

```

Add "/etc/modprobe.d/vfio.conf" and "/sbin/vfio-pci-override.sh" to FILES:

```
   FILES="/etc/modprobe.d/vfio.conf /sbin/vfio-pci-override.sh"

```

Regenerate your initramfs, and reboot:

```
   mkinitcpio -p linux

```

### Passing the boot GPU to the guest

The GPU marked as `boot_vga` is a special case when it comes to doing PCI passthroughs, since the BIOS needs to use it in order to display things like boot messages or the BIOS configuration menu. To do that, it makes [a copy of the VGA boot ROM which can then be freely modified](https://www.redhat.com/archives/vfio-users/2016-May/msg00224.html). This modified copy is the version the system gets to see, which the passthrough driver may reject as invalid. As such, it is generally reccomanded to change the boot GPU in the BIOS configuration so the host GPU is used instead or, if that's not possible, to swap the host and guest cards in the machine itself.

### Bypassing the IOMMU groups (ACS override patch)

If you find your PCI devices grouped among others that you do not wish to pass through, you may be able to seperate them using Alex Williamson's ACS override patch. Make sure you understand [the potential risk](http://vfio.blogspot.com/2014/08/iommu-groups-inside-and-out.html) of doing so.

You will need a kernel with the patch applied. The easiest method to acquiring this is through the [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) package.

In addition, the ACS override patch needs to be enabled with kernel command line options. The patch file adds the following documentation:

```
       pcie_acs_override =
               [PCIE] Override missing PCIe ACS support for:
           downstream
               All downstream ports - full ACS capabilties
           multifunction
               All multifunction devices - multifunction ACS subset
           id:nnnn:nnnn
               Specfic device - full ACS capabilities
               Specified as vid:did (vendor/device ID) in hex

```

The option `pcie_acs_override=downstream` is typically sufficient.

After installation and configuration, reconfigure your [bootloader kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to load the new kernel with the `pcie_acs_override=` option enabled.

## Complete example for QEMU (CLI-based) without libvirtd (can switch GPUs without reboot)

This script starts Samba and Synergy, runs the VM and closes everything after the VM is shut down. Note that this method does **not** require libvirtd to be running or configured.

Since this was posted, the author continued working on scripts to ease the workflow of switching GPUs. All of said scripts can be found on the author's GitLab instance: [https://git.mel.vin/melvin/scripts/tree/master/qemu](https://git.mel.vin/melvin/scripts/tree/master/qemu).

With these new scripts, is it possible to switch GPUs without rebooting, only a restart of the X session is needed. This is all handled by a tiny shell script that runs in the tty. When you log in the tty, it will ask which card you would like to use if you autolaunch the shell script.

[vfio-users : Full set of (runtime) scripts for VFIO + Qemu CLI](https://www.redhat.com/archives/vfio-users/2016-May/msg00187.html)

[vfio-users : Example configuration with CLI Qemu (working VM => host audio)](https://www.redhat.com/archives/vfio-users/2015-August/msg00020.html)

The script below is the main QEMU launcher as of 2016-05-16, all other scripts can be found in the repo.

 `slightly edited from "windows.sh" 2016-05-16 : [https://git.mel.vin/melvin/scripts/tree/master/qemu](https://git.mel.vin/melvin/scripts/tree/master/qemu)` 
```
#!/bin/bash

if [[ $EUID -ne 0 ]]
then
	echo "This script must be run as root"
	exit 1
fi

echo "Starting Samba"
systemctl start smbd.service
systemctl start nmbd.service

echo "Starting VM"
export QEMU_AUDIO_DRV="pa"
qemu-system-x86_64 \
	-serial none \
	-parallel none \
	-nodefaults \
	-nodefconfig \
	-no-user-config \
	-enable-kvm \
	-name Windows \
	-cpu host,kvm=off,hv_vapic,hv_time,hv_relaxed,hv_spinlocks=0x1fff,hv_vendor_id=sugoidesu \
	-smp sockets=1,cores=4,threads=1 \
	-m 8192 \
	-mem-path /dev/hugepages \
	-mem-prealloc \
	-soundhw hda \
	-device ich9-usb-uhci3,id=uhci \
	-device usb-ehci,id=ehci \
	-device nec-usb-xhci,id=xhci \
	-machine pc,accel=kvm,kernel_irqchip=on,mem-merge=off \
	-drive if=pflash,format=raw,file=./Windows_ovmf_x64.bin \
	-rtc base=localtime,clock=host,driftfix=none \
	-boot order=c \
	-net nic,vlan=0,macaddr=52:54:00:00:00:01,model=virtio,name=net0 \
	-net bridge,vlan=0,name=bridge0,br=br0 \
	-drive if=virtio,id=drive0,file=./Windows.img,format=raw,cache=none,aio=native \
	-nographic \
	-device vfio-pci,host=04:00.0,addr=09.0,multifunction=on \
	-device vfio-pci,host=04:00.1,addr=09.1 \
	-usbdevice host:046d:c29b `# Logitech G27` &

#	-usbdevice host:054c:05c4 `# Sony DualShock 4` \
#	-usbdevice host:28de:1142 `# Steam Controller` \

sleep 5

while [[ $(pgrep -x -u root qemu-system-x86) ]]
do
	if [[ ! $(pgrep -x -u REGULAR_USER synergys) ]]
	then
		echo "Starting Synergy server"
		sudo -u REGULAR_USER /usr/bin/synergys --debug ERROR --no-daemon --enable-crypto --config /etc/synergy.conf &
	fi

	sleep 5
done

echo "VM stopped"

echo "Stopping Synergy server"
pkill -u REGULAR_USER synergys

echo "Stopping Samba"
systemctl stop smbd.service
systemctl stop nmbd.service

exit 0
```

## Complete example for QEMU with libvirtd

```
<domain type='kvm' xmlns:qemu='[http://libvirt.org/schemas/domain/qemu/1.0'](http://libvirt.org/schemas/domain/qemu/1.0')>
  <name>win7</name>
  <uuid>a3bf6450-d26b-4815-b564-b1c9b098a740</uuid>
  <memory unit='KiB'>8388608</memory>
  <currentMemory unit='KiB'>8388608</currentMemory>
  <vcpu placement='static'>8</vcpu>
  <os>
    <type arch='x86_64' machine='pc-i440fx-2.4'>hvm</type>
    <boot dev='hd'/>
    <bootmenu enable='yes'/>
  </os>
  <features>
    <acpi/>
    <kvm>
      <hidden state='on'/>
    </kvm>
  </features>
  <cpu mode='host-passthrough'>
    <topology sockets='1' cores='8' threads='1'/>
  </cpu>
  <clock offset='utc'/>
  <on_poweroff>destroy</on_poweroff>
  <on_reboot>restart</on_reboot>
  <on_crash>destroy</on_crash>
  <devices>
    <emulator>/usr/sbin/qemu-system-x86_64</emulator>
    <disk type='block' device='disk'>
      <driver name='qemu' type='raw' cache='none' io='native'/>
      <source dev='/dev/rootvg/win7'/>
      <target dev='vda' bus='virtio'/>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x04' function='0x0'/>
    </disk>
    <disk type='block' device='disk'>
      <driver name='qemu' type='raw' cache='none' io='native'/>
      <source dev='/dev/rootvg/windane'/>
      <target dev='vdb' bus='virtio'/>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x07' function='0x0'/>
    </disk>
    <disk type='block' device='cdrom'>
      <driver name='qemu' type='raw' cache='none' io='native'/>
      <target dev='hdb' bus='ide'/>
      <readonly/>
      <address type='drive' controller='0' bus='0' target='0' unit='1'/>
    </disk>
    <controller type='usb' index='0'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x01' function='0x2'/>
    </controller>
    <controller type='pci' index='0' model='pci-root'/>
    <controller type='ide' index='0'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x01' function='0x1'/>
    </controller>
    <controller type='sata' index='0'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x03' function='0x0'/>
    </controller>
    <interface type='network'>
      <mac address='52:54:00:fa:59:92'/>
      <source network='default'/>
      <model type='rtl8139'/>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x05' function='0x0'/>
    </interface>
    <input type='mouse' bus='ps2'/>
    <input type='keyboard' bus='ps2'/>
    <sound model='ac97'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x02' function='0x0'/>
    </sound>
    <memballoon model='virtio'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x06' function='0x0'/>
    </memballoon>
  </devices>
  <qemu:commandline>
    <qemu:arg value='-device'/>
    <qemu:arg value='vfio-pci,host=02:00.0,multifunction=on,x-vga=on'/>
    <qemu:arg value='-device'/>
    <qemu:arg value='vfio-pci,host=02:00.1'/>
    <qemu:env name='QEMU_PA_SAMPLES' value='1024'/>
    <qemu:env name='QEMU_AUDIO_DRV' value='pa'/>
    <qemu:env name='QEMU_PA_SERVER' value='/run/user/1000/pulse/native'/>
  </qemu:commandline>
</domain>

```

## Troubleshooting

### "Error 43 : Driver failed to load" on Nvidia GPUs passed to Windows VMs

**Note:** This may also fix SYSTEM_THREAD_EXCEPTION_NOT_HANDLED boot crashes related to Nvidia drivers

Since version 337.88, Nvidia drivers on Windows check if an hypervisor is running and fail if it detects one, which results in an Error 43 in the Windows device manager. Starting with QEMU 2.5.0 and libvirt 1.3.3, the vendor_id for the hypervisor can be spoofed, which is enough to fool the Nvidia drivers into loading anyway. All one must do is add `hv_vendor_id=whatever` to the cpu parameters in their QEMU command line, or by adding the following line to their libvirt domain configuration. It may help for the ID to be set to a 12-character alphanumeric (e.g. '123456789ab') as opposed to longer or shorter strings.

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...

<features>
	<hyperv>
		...
		<vendor_id state='on' value='whatever'/>
		...
	</hyperv>
	...
	<kvm>
	<hidden state='on'/>
	</kvm>
</features>
...

```

Users with older versions of QEMU and/or libvirt will instead have to disable a few hypervisor extensions, which can degrade performance substentially. If this is what you want to do, do the following replacement in your libvirt domain config file.

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<features>
	<hyperv>
		<relaxed state='on'/>
		<vapic state='on'/>
		<spinlocks state='on' retries='8191'/>
	</hyperv>
	...
</features>
...
<clock offset='localtime'>
	<timer name='hypervclock' present='yes'/>
</clock>
...
```

```
...

<clock offset='localtime'>
	<timer name='hypervclock' present='no'/>
</clock>
...
<features>
	<kvm>
	<hidden state='on'/>
	</kvm>
	...
	<hyperv>
		<relaxed state='off'/>
		<vapic state='off'/>
		<spinlocks state='off'/>
	</hyperv>
	...
</features>
...
```

### Unexpected crashes related to CPU exceptions

In some cases, kvm may react strangely to certain CPU operations, such as GeForce Experience complaining about an unsupported CPU being present or some game crashing for unknown reasons. A number of those issues can be solved by passing the `ignore_msrs=1` option to the KVM module, which will ignore unimplemented MSRs instead of returning an error value.

 `/etc/modprobe.d/kvm.conf` 
```
...
options kvm ignore_msrs=1
...
```

**Warning:** While this is normally safe and some applications might not work without this, silently ignoring unknown MSR accesses could potentially break other software within the VM or other VMs.

### "System Thread Exception Not Handled" when booting on a Windows VM

Windows 8 or Windows 10 guests may raise a generic compatibility exception at boot, namely "System Thread Exception Not Handled", which tends to be caused by legacy drivers acting strangely on real machines. On KVM machines this issue can generally be solved by setting the CPU model to `core2duo`.

### Slowed down audio pumped through HDMI on the video card

For some users VM's audio slows down/starts stuttering/becomes demonic after a while when it's pumped through HDMI on the video card. This usually also slows down graphics. A possible solution consists of enabling MSI (Message Signaled-Based Interrupts) instead of the default (Line-Based Interrupts).

In order to check whether MSI is supported or enabled, run the following command as root:

```
# lspci -vs $device | grep 'MSI:'

```

where `$device` is the card's address (e.g. `01:00.0`).

The output should be similar to:

```
Capabilities: [60] MSI: Enable**-** Count=1/1 Maskable- 64bit+

```

A `-` after `Enabled` means MSI is supported, but not used by the VM, while a `+` says that the VM is using it.

The procedure to enable it is quite complex, instructions and an overview of the setting can be found [here](http://forums.guru3d.com/showthread.php?t=378044).

Other hints can be found on the [lime-technology's wiki](http://lime-technology.com/wiki/index.php/UnRAID_6/VM_Guest_Support#Enable_MSI_for_Interrupts_to_Fix_HDMI_Audio_Support), or on this article on [VFIO tips and tricks](http://vfio.blogspot.it/2014/09/vfio-interrupts-and-how-to-coax-windows.html).

Some tools named `MSI_util` or similar are available on the Internet, but they didn't work for me on Windows 10 64bit.

In order to fix the issues enabling MSI on the 0 function of my nVidia card (`01:00.0 VGA compatible controller: NVIDIA Corporation GM206 [GeForce GTX 960] (rev a1) (prog-if 00 [VGA controller])`) was not enough; I also enabled it on the other function (`01:00.1 Audio device: NVIDIA Corporation Device 0fba (rev a1)`) and that seems to have fixed the issue.

## Passing though other devices

### USB controller

If your motherboard has multiple USB controllers mapped to multiple groups, it is possible to pass those instead of USB devices. Passing an actual controller over an individual USB device provides the following advantages :

*   If a device disconnects or changes ID over the course of an given operation (such as a phone undergoing an update), the VM will not suddenly stop seeing it.
*   Any USB port managed by this controller is directly handled by the VM and can have its devices unplugged, replugged and changed without having to notify the hypervisor.
*   Libvirt will not complain if one of the USB devices you usually pass to the guest is missing when starting the VM.

Unlike with GPUs, drivers for most USB controllers do not require any specific configuration to work on a VM and control can normally be passed back and forth between the host and guest systems with no side effects.

**Warning:** Make sure your USB controller supports resetting :[#Passing through a device that does not support resetting](#Passing_through_a_device_that_does_not_support_resetting)

You can find out which PCI devices correspond to which controller and how various ports and devices are assigned to each one of them using this command :

 `$ for usb_ctrl in $(find /sys/bus/usb/devices/usb* -maxdepth 0 -type l); do pci_path="$(dirname "$(realpath "${usb_ctrl}")")"; echo "Bus $(cat "${usb_ctrl}/busnum") --> $(basename $pci_path) (IOMMU group $(basename $(realpath $pci_path/iommu_group)))"; lsusb -s "$(cat "${usb_ctrl}/busnum"):"; echo; done` 
```
Bus 1 --> 0000:00:1a.0 (IOMMU group 4)
Bus 001 Device 004: ID 04f2:b217 Chicony Electronics Co., Ltd Lenovo Integrated Camera (0.3MP)
Bus 001 Device 007: ID 0a5c:21e6 Broadcom Corp. BCM20702 Bluetooth 4.0 [ThinkPad]
Bus 001 Device 008: ID 0781:5530 SanDisk Corp. Cruzer
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

Bus 2 --> 0000:00:1d.0 (IOMMU group 9)
Bus 002 Device 006: ID 0451:e012 Texas Instruments, Inc. TI-Nspire Calculator
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

This laptop has 3 USB ports managed by 2 USB controllers, each with their own IOMMU group. In this example, Bus 001 manages a single USB port (with a SanDisk USB pendrive plugged into it so it appears on the list), but also a number of internal devices, such as the internal webcam and the bluetooth card. Bus 002, on the other hand, does not apprear to manage anything except for the calculator that is plugged into it. The third port is empty, which is why it does not show up on the list, but is actually managed by Bus 002.

Once you have identified which controller manages which ports by plugging various devices into them and decided which one you want to passthrough, simply add it to the list of PCI host devices controlled by the VM in your guest configuration. No other configuration should be needed.

### Gotchas

#### Passing through a device that does not support resetting

When the VM shuts down, all devices used by the guest are deinitialized by its OS in preparation for shutdown. In this state, those devices are no longer functionnal and must then be power-cycled before they can resume normal operation. Linux can handle this power-cycling on its own, but when a device has no known reset methods, it remains in this disabled state and becomes unavailable. Since Libvirt and Qemu both expect all host PCI devices to be ready to reattach to the host before completely stopping the VM, when encountering a device that won't reset, they will hang in a "Shutting down" state where they will not be able to be restarted until the host system has been rebooted. It is therefore reccomanded to only pass through PCI devices which the kernel is able to reset, as evidenced by the presence of a `reset` file in the PCI device sysfs node, such as `/sys/bus/pci/devices/0000:00:1a.0/reset`.

The following bash command shows which devices can and cannot be reset.

 `for iommu_group in $(find /sys/kernel/iommu_groups/ -maxdepth 1 -mindepth 1 -type d);do echo "IOMMU group $(basename "$iommu_group")"; for device in $(\ls -1 "$iommu_group"/devices/); do if [[ -e "$iommu_group"/devices/"$device"/reset ]]; then echo -n "[RESET]"; fi; echo -n $'\t';lspci -nns "$device"; done; done` 
```
IOMMU group 0
	00:00.0 Host bridge [0600]: Intel Corporation Xeon E3-1200 v2/Ivy Bridge DRAM Controller [8086:0158] (rev 09)
IOMMU group 1
	00:01.0 PCI bridge [0604]: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port [8086:0151] (rev 09)
	01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GK208 [GeForce GT 720] [10de:1288] (rev a1)
	01:00.1 Audio device [0403]: NVIDIA Corporation GK208 HDMI/DP Audio Controller [10de:0e0f] (rev a1)
IOMMU group 2
	00:14.0 USB controller [0c03]: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller [8086:1e31] (rev 04)
IOMMU group 4
[RESET]	00:1a.0 USB controller [0c03]: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 [8086:1e2d] (rev 04)
IOMMU group 5
[RESET]	00:1b.0 Audio device [0403]: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller [8086:1e20] (rev 04)
IOMMU group 10
[RESET]	00:1d.0 USB controller [0c03]: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 [8086:1e26] (rev 04)
IOMMU group 13
	06:00.0 VGA compatible controller [0300]: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	06:00.1 Audio device [0403]: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)

```

This signals that the xHCI USB controller in 00:14.0 cannot be reset and will therefore stop the VM from shutting down properly, while the integrated sound card in 00:1b.0 and the other two controllers in 00:1a.0 and 00:1d.0 do not share this problem and can be passed without issue.

## Troubleshooting

### No HDMI audio output on host when intel_iommu is enabled

If after enabling `intel_iommu` the HDMI output device of Intel GPU becomes unusable on the host then setting the option `igfx_off` (i.e. `intel_iommu=on,igfx_off`) might bring the audio back, please read `Graphics Problems?` in [Intel-IOMMU.txt](https://www.kernel.org/doc/Documentation/Intel-IOMMU.txt) for details about setting `igfx_off`.

## See also

*   [Discussion on Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=162768) | [Archived link](https://archive.is/kZYMt)
*   [User contributed hardware compatibility list](https://docs.google.com/spreadsheet/ccc?key=0Aryg5nO-kBebdFozaW9tUWdVd2VHM0lvck95TUlpMlE)
*   [Example script from https://www.youtube.com/watch?v=37D2bRsthfI](http://pastebin.com/rcnUZCv7)
*   [Complete tutorial for PCI passthrough](http://vfio.blogspot.com/)
*   [VFIO users mailing list](https://www.redhat.com/archives/vfio-users/)
*   [#vfio-users on freenode](https://webchat.freenode.net/?channels=vfio-users)