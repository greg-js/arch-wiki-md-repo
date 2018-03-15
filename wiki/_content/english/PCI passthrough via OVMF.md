The Open Virtual Machine Firmware ([OVMF](https://github.com/tianocore/tianocore.github.io/wiki/OVMF)) is a project to enable UEFI support for virtual machines. Starting with Linux 3.9 and recent versions of QEMU, it is now possible to passthrough a graphics card, offering the VM native graphics performance which is useful for graphic-intensive tasks.

Provided you have a desktop computer with a spare GPU you can dedicate to the host (be it an integrated GPU or an old OEM card, the brands do not even need to match) and that your hardware supports it (see [#Prerequisites](#Prerequisites)), it is possible to have a VM of any OS with its own dedicated GPU and near-native performance. For more information on techniques see the background [presentation (pdf)](https://www.linux-kvm.org/images/b/b3/01x09b-VFIOandYou-small.pdf).

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
        *   [5.4.1 CPU pinning with isolcpus](#CPU_pinning_with_isolcpus)
    *   [5.5 Improving performance on AMD CPUs](#Improving_performance_on_AMD_CPUs)
    *   [5.6 Further Tuning](#Further_Tuning)
*   [6 Special procedures](#Special_procedures)
    *   [6.1 Using identical guest and host GPUs](#Using_identical_guest_and_host_GPUs)
        *   [6.1.1 Script variants](#Script_variants)
            *   [6.1.1.1 Passthrough all GPUs but the boot GPU](#Passthrough_all_GPUs_but_the_boot_GPU)
            *   [6.1.1.2 Passthrough selected GPU](#Passthrough_selected_GPU)
        *   [6.1.2 Script installation](#Script_installation)
    *   [6.2 Passing the boot GPU to the guest](#Passing_the_boot_GPU_to_the_guest)
    *   [6.3 Using Looking Glass to stream guest screen to the host](#Using_Looking_Glass_to_stream_guest_screen_to_the_host)
        *   [6.3.1 Adding IVSHMEM Device to VM](#Adding_IVSHMEM_Device_to_VM)
        *   [6.3.2 Installing the IVSHMEM Host to Windows guest](#Installing_the_IVSHMEM_Host_to_Windows_guest)
        *   [6.3.3 Getting a client](#Getting_a_client)
    *   [6.4 Bypassing the IOMMU groups (ACS override patch)](#Bypassing_the_IOMMU_groups_.28ACS_override_patch.29)
*   [7 Plain QEMU without libvirt](#Plain_QEMU_without_libvirt)
*   [8 Passing though other devices](#Passing_though_other_devices)
    *   [8.1 USB controller](#USB_controller)
    *   [8.2 Passing VM audio to host via PulseAudio](#Passing_VM_audio_to_host_via_PulseAudio)
    *   [8.3 Physical Disk/Partition](#Physical_Disk.2FPartition)
    *   [8.4 Gotchas](#Gotchas_3)
        *   [8.4.1 Passing through a device that does not support resetting](#Passing_through_a_device_that_does_not_support_resetting)
*   [9 Complete setups and examples](#Complete_setups_and_examples)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 "Error 43: Driver failed to load" on Nvidia GPUs passed to Windows VMs](#.22Error_43:_Driver_failed_to_load.22_on_Nvidia_GPUs_passed_to_Windows_VMs)
        *   [10.1.1 "BAR 3: cannot reserve [mem]" error in dmesg after starting VM](#.22BAR_3:_cannot_reserve_.5Bmem.5D.22_error_in_dmesg_after_starting_VM)
    *   [10.2 UEFI (OVMF) Compatability in VBIOS](#UEFI_.28OVMF.29_Compatability_in_VBIOS)
    *   [10.3 Slowed down audio pumped through HDMI on the video card](#Slowed_down_audio_pumped_through_HDMI_on_the_video_card)
    *   [10.4 No HDMI audio output on host when intel_iommu is enabled](#No_HDMI_audio_output_on_host_when_intel_iommu_is_enabled)
    *   [10.5 X doesn't start after enabling vfio_pci](#X_doesn.27t_start_after_enabling_vfio_pci)
    *   [10.6 Chromium ignores integrated graphics for acceleration](#Chromium_ignores_integrated_graphics_for_acceleration)
    *   [10.7 VM only uses one core](#VM_only_uses_one_core)
    *   [10.8 Passthrough seems to work but no output is displayed](#Passthrough_seems_to_work_but_no_output_is_displayed)
    *   [10.9 virt-manager has permission issues](#virt-manager_has_permission_issues)
*   [11 See also](#See_also)

## Prerequisites

A VGA Passthrough relies on a number of technologies that are not ubiquitous as of today and might not be available on your hardware. You will not be able to do this on your machine unless the following requirements are met :

*   Your CPU must support hardware virtualization (for kvm) and IOMMU (for the passthrough itself)
    *   [List of compatible Intel CPUs (Intel VT-x and Intel VT-d)](https://ark.intel.com/Search/FeatureFilter?productType=processors&VTD=true)
    *   All AMD CPUs from the Bulldozer generation and up (including Zen) should be compatible.
        *   CPUs from the K10 generation (2007) do not have an IOMMU, so you **need** to have a motherboard with a [890FX](https://support.amd.com/TechDocs/43403.pdf#page=18) or [990FX](https://support.amd.com/TechDocs/48691.pdf#page=21) chipset to make it work, as those have their own IOMMU.
*   Your motherboard must also support IOMMU
    *   Both the chipset and the BIOS must support it. It is not always easy to tell at a glance whether or not this is the case, but there is a fairly comprehensive list on the matter on the [Xen wiki](https://wiki.xen.org/wiki/VTd_HowTo) as well as [Wikipedia:List of IOMMU-supporting hardware](https://en.wikipedia.org/wiki/List_of_IOMMU-supporting_hardware "wikipedia:List of IOMMU-supporting hardware").
*   Your guest GPU ROM must support UEFI.
    *   If you can find [any ROM in this list](https://www.techpowerup.com/vgabios/) that applies to your specific GPU and is said to support UEFI, you are generally in the clear. All GPUs from 2012 and later should support this, as Microsoft made UEFI a requirement for devices to be marketed as compatible with Windows 8.

You will probably want to have a spare monitor or one with multiple input ports connected to different GPUs (the passthrough GPU will not display anything if there is no screen plugged in and using a VNC or Spice connection will not help your performance), as well as a mouse and a keyboard you can pass to your VM. If anything goes wrong, you will at least have a way to control your host machine this way.

## Setting up IOMMU

**Note:** IOMMU is a generic name for Intel VT-d and AMD-Vi.

Using IOMMU opens to features like PCI passthrough and memory protection from faulty or malicious devices, see [wikipedia:Input-output memory management unit#Advantages](https://en.wikipedia.org/wiki/Input-output_memory_management_unit#Advantages "wikipedia:Input-output memory management unit") and [Memory Management (computer programming): Could you explain IOMMU in plain English?](https://www.quora.com/Memory-Management-computer-programming/Could-you-explain-IOMMU-in-plain-English).

### Enabling IOMMU

Ensure that AMD-Vi/Intel VT-d is support by the CPU and enabled in the BIOS settings. Both normally show up alongside other CPU features (meaning they could be in an overclocking-related menu) either with their actual names ("VT-d" or "AMD-Vi") or in more ambiguous terms such as "Virtualization technology", which may or may not be explained in the manual.

Enable IOMMU support by setting the correct [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") depending on the type of CPU in use:

*   For Intel CPUs (VT-d) set `intel_iommu=on`
*   For AMD CPUs (AMD-Vi) set `amd_iommu=on`

You should also [append](/index.php/Append "Append") the `iommu=pt` parameter. This will prevent Linux from touching devices which cannot be passed through.

After rebooting, check dmesg to confirm that IOMMU has been correctly enabled:

 `dmesg | grep -e DMAR -e IOMMU` 
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

This is fine so long as only your guest GPU is included in here, such as above. Depending on what is plugged in your other PCIe slots and whether they are allocated to your CPU or your PCH, you may find yourself with additional devices within the same group, which would force you to pass those as well. If you are ok with passing everything that is in there to your VM, you are free to continue. Otherwise, you will either need to try and plug your GPU in your other PCIe slots (if you have any) and see if those provide isolation from the rest or to install the ACS override patch, which comes with its own drawbacks. See [#Bypassing the IOMMU groups (ACS override patch)](#Bypassing_the_IOMMU_groups_.28ACS_override_patch.29) for more information.

**Note:** If they are grouped with other devices in this manner, pci root ports and bridges should neither be bound to vfio at boot, nor be added to the VM.

## Isolating the GPU

In order to assign a device to a virtual machine, this device and all those sharing the same IOMMU group must have their driver replaced by a stub driver or a VFIO driver in order to prevent the host machine from interacting with them. In the case of most devices, this can be done on the fly right before the VM starts.

However, due to their size and complexity, GPU drivers do not tend to support dynamic rebinding very well, so you cannot just have some GPU you use on the host be transparently passed to a VM without having both drivers conflict with each other. Because of this, it is generally advised to bind those placeholder drivers manually before starting the VM, in order to stop other drivers from attempting to claim it.

The following section details how to configure a GPU so those placeholder drivers are bound early during the boot process, which makes said device inactive until a VM claims it or the driver is switched back. This is the prefered method, considering it has less caveats than switching drivers once the system is fully online.

**Warning:** Once you reboot after this procedure, whatever GPU you have configured will no longer be usable on the host until you reverse the manipulation. Make sure the GPU you intend to use on the host is properly configured before doing this.

### Using vfio-pci

Starting with Linux 4.1, the kernel includes vfio-pci. This is a VFIO driver, meaning it fulfills the same role as pci-stub, but it can also control devices to an extent, such as by switching them into their D3 state when they are not in use. If your system supports it, which you can try by running the following command, you should use it. If it returns an error, use pci-stub instead.

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

**Note:** You cannot specify which device to isolate using vendor-device ID pairs if the host GPU and the guest GPU share the same pair (i.e : if both are the same model). If this is your case, read [#Using identical guest and host GPUs](#Using_identical_guest_and_host_GPUs) instead.

You can then add those vendor-device ID pairs to the default parameters passed to vfio-pci whenever it is inserted into the kernel.

 `/etc/modprobe.d/vfio.conf`  `options vfio-pci ids=10de:13c2,10de:0fbb` 
**Note:** If, as noted in [#Plugging your guest GPU in an unisolated CPU-based PCIe slot](#Plugging_your_guest_GPU_in_an_unisolated_CPU-based_PCIe_slot), your pci root port is part of your IOMMU group, you **must not** pass its ID to `vfio-pci`, as it needs to remain attached to the host to function properly. Any other device within that group, however, should be left for `vfio-pci` to bind with.

This, however, does not guarantee that vfio-pci will be loaded before other graphics drivers. To ensure that, we need to statically bind it in the kernel image alongside with its dependencies. That means adding, in this order, `vfio`, `vfio_iommu_type1`, `vfio_pci` and `vfio_virqfd` to [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"):

 `/etc/mkinitcpio.conf`  `MODULES=(... vfio vfio_iommu_type1 vfio_pci vfio_virqfd ...)` 
**Note:** If you also have another driver loaded this way for [early modesetting](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") (such as `nouveau`, `radeon`, `amdgpu`, `i915`, etc.), all of the aforementioned VFIO modules must precede it.

Also, ensure that the modconf hook is included in the HOOKS list of `mkinitcpio.conf`:

 `/etc/mkinitcpio.conf`  `HOOKS=(... modconf ...)` 

Since new modules have been added to the initramfs configuration, you must [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs"). Should you change the IDs of the devices in `/etc/modprobe.d/vfio.conf`, you will also have to regenerate it, as those parameters must be specified in the initramfs to be known during the early boot stages.

Reboot and verify that vfio-pci has loaded properly and that it is now bound to the right devices.

 `$ dmesg | grep -i vfio` 
```
[    0.329224] VFIO - User Level meta-driver version: 0.3
[    0.341372] vfio_pci: add [10de:13c2[ffff:ffff]] class 0x000000/00000000
[    0.354704] vfio_pci: add [10de:0fbb[ffff:ffff]] class 0x000000/00000000
[    2.061326] vfio-pci 0000:06:00.0: enabling device (0100 -> 0103)

```

It is not necessary for all devices (or even expected device) from `vfio.conf` to be in dmesg output. Sometimes a device does not appear in output at boot but actually is able to be visible and operatable in guest VM.

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

If your kernel does not support vfio-pci, you can use the pci-stub module instead, which is a dummy driver used to claim a device and prevent other drivers from using it.

Pci-stub normally targets PCI devices by ID, meaning you only need to specify the IDs of the devices you intend to passthrough. For the following IOMMU group, you would want to bind vfio-pci with `10de:13c2` and `10de:0fbb`, which will be used as example values for the rest of this section.

```
IOMMU group 13 06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
IOMMU group 13 06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)}}

```

**Note:** You cannot specify which device to isolate using vendor-device ID pairs if the host GPU and the guest GPU share the same pair (i.e : if both are the same model). If this is your case, read [#Using identical guest and host GPUs](#Using_identical_guest_and_host_GPUs) instead.

[linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) have pci-stub built as a module. You will need to add it to MODULES array in `mkinitpcio.conf`:

 `/etc/mkinitcpio.conf`  `MODULES=(... pci-stub ...)` 

If you did need to add this module to your kernel image configuration manually, you must also [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Add the relevant PCI device IDs to the `pci-stubs.ids` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), e.g. `pci-stub.ids=10de:13c2,10de:0fbb`.

**Note:** If, as noted in [#Plugging your guest GPU in an unisolated CPU-based PCIe slot](#Plugging_your_guest_GPU_in_an_unisolated_CPU-based_PCIe_slot), your pci root port is part of your IOMMU group, you **must not** pass its ID to `pci-stub`, as it needs to remain attached to the host to function properly. Any other device within that group, however, should be left for `pci-stub` to bind with.

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

After installing [qemu](https://www.archlinux.org/packages/?name=qemu), [libvirt](https://www.archlinux.org/packages/?name=libvirt), [ovmf](https://www.archlinux.org/packages/?name=ovmf), [firewalld](https://www.archlinux.org/packages/?name=firewalld), and [virt-manager](https://www.archlinux.org/packages/?name=virt-manager), add the path to your OVMF firmware image and runtime variables template to your libvirt config so `virt-install` or `virt-manager` can find those later on.

 `/etc/libvirt/qemu.conf` 
```
nvram = [
	"/usr/share/ovmf/x64/OVMF_CODE.fd:/usr/share/ovmf/x64/OVMF_VARS.fd"
]
```

You can now [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `libvirtd.service` and its logging component `virtlogd.socket`.

### Setting up the guest OS

The process of setting up a VM using `virt-manager` is mostly self-explanatory, as most of the process comes with fairly comprehensive on-screen instructions.

If using `virt-manager`, you have to add your user to the libvirt [group](/index.php/Group "Group") to ensure authentication.

However, you should pay special attention to the following steps :

*   When the VM creation wizard asks you to name your VM (final step before clicking "Finish"), check the "Customize before install" checkbox.
*   In the "Overview" section, [set your firmware to "UEFI"](https://i.imgur.com/73r2ctM.png). If the option is grayed out, make sure that you have correctly specified the location of your firmware in `/etc/libvirt/qemu.conf` and restart `libvirtd.service`.
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

**Note:** For certain users enabling CPU pinning may introduce stuttering and short hangs, especially with the MuQSS scheduler (present in linux-ck and linux-zen kernels). You might want to try disabling pinning first if you experience similar issues, which effectively trades maximum performance for responsiveness at all times.
 `$ virsh edit [vmname]` 
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

If your CPU supports hardware multitasking, also known as Hyper-threading on Intel chips, there are two ways you can go with your CPU pinning. That is, Hyper-threading is simply a very efficient way of running two threads on one CPU at any given time, so while it may give you 8 logical cores on what would otherwise be a quad-core CPU, if the physical core is overloaded, the logical core will not be of any use. One could pin their VM threads on 2 physical cores and their 2 respective threads, but any task overloading those two cores will not be helped by the extra two logical cores, since in the end you are only passing through two cores out of four, not four out of eight. What you should do knowing this depends on what you intend to do with your host while your VM is running.

This is the abridged content of `/proc/cpuinfo` on a quad-core machine with hyper-threading.

 `$ grep -e "processor" -e "core id" -e "^$" /proc/cpuinfo` 
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

If you do not intend to be doing any computation-heavy work on the host (or even anything at all) at the same time as you would on the VM, it would probably be better to pin your VM threads across all of your logical cores, so that the VM can fully take advantage of the spare CPU time on all your cores.

On the quad-core machine mentioned above, it would look like this :

 `$ virsh edit [vmname]` 
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

 `$ virsh edit [vmname]` 
```
...
<vcpu placement='static'>4</vcpu>
<cputune>
    <vcpupin vcpu='0' cpuset='2'/>
    <vcpupin vcpu='1' cpuset='6'/>
    <vcpupin vcpu='2' cpuset='3'/>
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

**Warning:** Static huge pages lock down the allocated amount of memory, making it unavailable for applications that are not configured to use them. Allocating 4GBs worth of huge pages on a machine with 8GBs of memory will only leave you with 4GBs of available memory on the host **even when the VM is not running**.

To allocate huge pages at boot, one must simply specify the desired amount on their kernel comand line with `hugepages=*x*`. For instance, reserving 1024 pages with `hugepages=1024` and the default size of 2048kB per huge page creates 2GBs worth of memory for the virtual machine to use.

If supported by CPU page size could be set manually. 1 GB huge page support could be verified by `grep pdpe1gb /proc/cpuinfo`. Setting 1 GB huge page size via kernel parameters : `default_hugepagesz=1G hugepagesz=1G hugepages=X transparent_hugepage=never`.

Also, since static huge pages can only be used by applications that specifically request it, you must add this section in your libvirt domain configuration to allow kvm to benefit from them :

 `$ virsh edit [vmname]` 
```
...
<memoryBacking>
	<hugepages/>
</memoryBacking>
...

```

### CPU frequency governor

Depending on the way your [CPU governor](/index.php/CPU_frequency_scaling "CPU frequency scaling") is configured, the VM threads may not hit the CPU load thresholds for the frequency to ramp up. Indeed, KVM cannot actually change the CPU frequency on its own, which can be a problem if it does not scale up with vCPU usage as it would result in underwhelming performance. An easy way to see if it behaves correctly is to check if the frequency reported by `watch lscpu` goes up when running a CPU-intensive task on the guest. If you are indeed experiencing stutter and the frequency does not go up to reach its reported maximum, it may be due to [cpu scaling being controlled by the host OS](https://lime-technology.com/forum/index.php?topic=46664.msg447678#msg447678). In this case, try setting all cores to maximum frequency to see if this improves performance. Note that if you are using a modern intel chip with the default pstate driver, cpupower commands will be [ineffective](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling"), so monitor `/proc/cpuinfo` to make sure your cpu is actually at max frequency.

### High DPC Latency

If you are experiencing high DPC and/or interrupt latency in your Guest VM, ensure you have [loaded the needed virtio kernel modules](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") on the host kernel. Loadable virtio kernel modules include: `virtio-pci`, `virtio-net`, `virtio-blk`, `virtio-balloon`, `virtio-ring` and `virtio`.

After loading one or more of these modules, `lsmod | grep virtio` executed on the host should not return empty.

#### CPU pinning with isolcpus

Alternatively, make sure that you have isolated CPUs properly. In this example, let us assume you are using CPUs 4-7. Use the kernel parameters `isolcpus nohz_full rcu_nocbs` to completely isolate the CPUs from the kernel.

 `sudo vim /etc/defaults/grub` 
```
...
GRUB_CMDLINE_LINUX="..your other params.. isolcpus=4-7 nohz_full=4-7 rcu_nocbs=4-7"
...

```

Then, run `qemu-system-x86_64` with taskset and chrt:

```
# chrt -r 1 taskset -c 4-7 qemu-system-x86_64 ...

```

The `chrt` command will ensure that the task scheduler will round-robin distribute work (otherwise it will all stay on the first cpu). For `taskset`, the CPU numbers can be comma- and/or dash-separated, like "0,1,2,3" or "0-4" or "1,7-8,10" etc.

See [this reddit comment](https://www.reddit.com/r/VFIO/comments/6vgtpx/high_dpc_latency_and_audio_stuttering_on_windows/dm0sfto/) for more info.

### Improving performance on AMD CPUs

Previously, Nested Page Tables (NPT) had to be disabled on AMD systems running KVM to improve GPU performance because of a [very old bug](https://sourceforge.net/p/kvm/bugs/230/), but the trade off was decreased CPU performance, including stuttering.

There is a [kernel patch](https://patchwork.kernel.org/patch/10027525/) that resolves this issue, which was accepted into kernel 4.14-stable and 4.9-stable. If you're running the official [linux](https://www.archlinux.org/packages/?name=linux) or [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel the patch has already been applied (make sure you're on the latest). If you're running another kernel you might need to manually patch yourself.

**Note:** Several Ryzen users (see [this Reddit thread](https://www.reddit.com/r/VFIO/comments/78i3jx/possible_fix_for_the_npt_issue_discussed_on_iommu/)) have tested the patch, and can confirm that it works, bringing GPU passthrough performance up to near native quality.

### Further Tuning

More specialized VM tuning tips are available at [Red Hat's Virtualization Tuning and Optimization Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html-single/Virtualization_Tuning_and_Optimization_Guide/index.html). This guide may be especially helpful if you are experiencing:

*   Moderate CPU load on the host during downloads/uploads from within the guest: See *Bridge Zero Copy Transmit* for a potential fix.
*   Guests capping out at certain network speeds during downloads/uploads despite virtio-net being used: See *Multi-queue virtio-net* for a potential fix.
*   Guests "stuttering" under high I/O, despite the same workload not affecting hosts to the same degree: See *Multi-queue virtio-scsi* for a potential fix.

## Special procedures

Certain setups require specific configuration tweaks in order to work properly. If you are having problems getting your host or your VM to work properly, see if your system matches one of the cases below and try adjusting your configuration accordingly.

### Using identical guest and host GPUs

Due to how both pci-stub and vfio-pci use your vendor and device id pair to identify which device they need to bind to at boot, if you have two GPUs sharing such an ID pair you will not be able to get your passthough driver to bind with just one of them. This sort of setup makes it necessary to use a script, so that whichever driver you are using is instead assigned by pci bus address using the `driver_override` mechanism.

#### Script variants

##### Passthrough all GPUs but the boot GPU

Here, we will make a script to bind vfio-pci to all GPUs but the boot gpu. Create the script `/usr/bin/vfio-pci-override.sh`:

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

##### Passthrough selected GPU

In this case we manually specify the GPU to bind.

```
#!/bin/sh

GROUP="0000:00:03.0"
DEVS="0000:03:00.0 0000:03:00.1 ."

if [ ! -z "$(ls -A /sys/class/iommu)" ]; then
	for DEV in $DEVS; do
		echo "vfio-pci" > /sys/bus/pci/devices/$GROUP/$DEV/driver_override
	done
fi

modprobe -i vfio-pci

```

#### Script installation

Create `/etc/modprobe.d/vfio.conf` with the following:

```
install vfio-pci /usr/bin/vfio-pci-override.sh

```

Edit `/etc/mkinitcpio.conf`

Remove any video drivers from MODULES, and add `vfio-pci`, and `vfio_iommu_type1`

```
MODULES=(ext4 vfat vfio-pci vfio_iommu_type1)

```

Add `/etc/modprobe.d/vfio.conf` and `/usr/bin/vfio-pci-override.sh` to FILES:

```
FILES=(/etc/modprobe.d/vfio.conf /usr/bin/vfio-pci-override.sh)

```

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") and reboot:

### Passing the boot GPU to the guest

The GPU marked as `boot_vga` is a special case when it comes to doing PCI passthroughs, since the BIOS needs to use it in order to display things like boot messages or the BIOS configuration menu. To do that, it makes [a copy of the VGA boot ROM which can then be freely modified](https://www.redhat.com/archives/vfio-users/2016-May/msg00224.html). This modified copy is the version the system gets to see, which the passthrough driver may reject as invalid. As such, it is generally recommended to change the boot GPU in the BIOS configuration so the host GPU is used instead or, if that's not possible, to swap the host and guest cards in the machine itself.

### Using Looking Glass to stream guest screen to the host

It is possible to make VM share the monitor, and optionally a keyboard and a mouse with a help of [Looking Glass](https://looking-glass.hostfission.com/).

#### Adding IVSHMEM Device to VM

Looking glass works by creating a shared memory buffer between a host and a guest. This is a lot faster than streaming frames via localhost, but requires additional setup.

With your VM turned off open the machine configuration

 `$ virsh edit [vmname]` 
```
...
<devices>
    ...
  <shmem name='looking-glass'>
    <model type='ivshmem-plain'/>
    <size unit='M'>32</size>
  </shmem>
</devices>
...

```

You should replace 32 with your own calculated value based on what resolution you are going to pass through. It can be calculated like this:

```
width x height x 4 x 2 = total bytes
total bytes / 1024 / 1024 = total megabytes + 2

```

For example, in case of 1920x1080

```
1920 x 1080 x 4 x 2 = 16,588,800 bytes
16,588,800 / 1024 / 1024 = 15.82 MB + 2 = 17.82

```

The result must be **rounded up** to the nearest power of two, and since 17.82 is bigger than 16 we should choose 32.

Next create a script to create a shared memory file.

 `/usr/local/bin/looking-glass-init.sh` 
```
#!/bin/sh

touch /dev/shm/looking-glass
chown **user**:kvm /dev/shm/looking-glass
chmod 660 /dev/shm/looking-glass
```

Replace user with your username.

Create a [systemd](/index.php/Systemd "Systemd") unit to execute this script during boot

 `/etc/systemd/system/looking-glass-init.service` 
```
[Unit]
Description=Create shared memory for looking glass

[Service]
Type=oneshot
ExecStart=/usr/local/bin/looking-glass-init.sh

[Install]
WantedBy=multi-user.target
```

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `looking-glass-init.service`

#### Installing the IVSHMEM Host to Windows guest

Currently Windows would not notify users about a new IVSHMEM device, it would silently install a dummy driver. To actually enable the device you have to go into device manager and update the driver for the device under the "System Devices" node for **"PCI standard RAM Controller"**. Download a signed driver [from issue 217](https://github.com/virtio-win/kvm-guest-drivers-windows/issues/217), as it is not yet available elsewhere.

Once the driver is installed you must download the latest [looking-glass-host](https://looking-glass.hostfission.com/downloads) from the looking glass website and start it on your guest. In order to run it you would also need to install Microsoft Visual C++ Redistributable from [Microsoft](https://www.visualstudio.com/downloads/) It is also possible to make it start automatically on VM boot by editing the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` registry and adding a path to the downloaded executable.

#### Getting a client

Looking glass client can be installed from AUR using [looking-glass](https://aur.archlinux.org/packages/looking-glass/) or [looking-glass-git](https://aur.archlinux.org/packages/looking-glass-git/) packages. You can start it once the VM is set up and running

```
$ looking-glass-client

```

If you don't want to use Spice to control the guest mouse and keyboard you can disable the Spice server

```
$ looking-glass-client -s

```

Refer to

```
$ looking-glass-client --help

```

for more info

### Bypassing the IOMMU groups (ACS override patch)

If you find your PCI devices grouped among others that you do not wish to pass through, you may be able to seperate them using Alex Williamson's ACS override patch. Make sure you understand [the potential risk](https://vfio.blogspot.com/2014/08/iommu-groups-inside-and-out.html) of doing so.

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

## Plain QEMU without libvirt

Instead of setting up a virtual machine with the help of libvirt, plain QEMU commands with custom parameters can be used for running the VM intended to be used with PCI passthrough. This is desirable for some use cases like scripted setups, where the flexibility for usage with other scripts is needed.

To achieve this after [#Setting up IOMMU](#Setting_up_IOMMU) and [#Isolating the GPU](#Isolating_the_GPU), follow the [QEMU](/index.php/QEMU "QEMU") article to setup the virtualized environment, [enable KVM](/index.php/QEMU#Enabling_KVM "QEMU") on it and use the flag `-device vfio-pci,host=07:00.0` replacing the identifier (07:00.0) with your actual device's ID that you used for the GPU isolation earlier.

For utilizing the OVMF firmware, make sure the [ovmf](https://www.archlinux.org/packages/?name=ovmf) package is installed, copy the UEFI variables from `/usr/share/ovmf/x64/OVMF_VARS.fd` to temporary location like `/tmp/MY_VARS.fd` and finally specify the OVMF paths by appending the following parameters to the QEMU command (order matters):

*   `-drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/OVMF_CODE.fd` for the actual OVMF firmware binary, note the readonly option
*   `-drive if=pflash,format=raw,file=/tmp/MY_VARS.fd` for the variables

**Note:** QEMU's default SeaBIOS can be used instead of OVMF, but it's not recommended as it can cause issues with passthrough setups.

It's recommended to study the QEMU article for ways to enhance the performance by using the [virtio drivers](/index.php/QEMU#Installing_virtio_drivers "QEMU") and other further configurations for the setup.

You also might have to use the `-cpu host,kvm=off` parameter to forward the host's CPU model info to the VM and fool the virtualization detection used by Nvidia's and possibly other manufacturers' device drivers trying to block the full hardware usage inside a virtualized system.

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

### Passing VM audio to host via PulseAudio

It is possible to route the virtual machine's audio to the host as an application using libvirt. This has the advantage of multiple audio streams being routable to one host output, and working with audio output devices that do not support passthrough. [PulseAudio](/index.php/PulseAudio "PulseAudio") is required for this to work.

First, remove the comment from the `#user = ""` line. Then add your username in the quotations. This tells QEMU which user's pulseaudio stream to route through.

 `/etc/libvirt/qemu.conf`  `user = "example"` 

Next, modify the libvirt configuration

 `$ virsh edit [vmname]` 
```
<domain type='kvm'>

```

to

 `$ virsh edit [vmname]` 
```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>

```

Then set the QEMU PulseAudio environment variables at the bottom of the libvirt xml file

 `$ virsh edit [vmname]` 
```
    </devices>
   </domain>

```

to

 `$ virsh edit [vmname]` 
```
    </devices>
      <qemu:commandline>
        <qemu:env name='QEMU_AUDIO_DRV' value='pa'/>
        <qemu:env name='QEMU_PA_SERVER' value='/run/user/1000/pulse/native'/>
      </qemu:commandline>
 </domain>

```

Change 1000 under the user directory to your user uid (which can be found by running the `id` command. Remember to save the file and exit it without ending the process before continuing, otherwise the changes will not register. If you get the message `Domain [vmname] XML configuration edited.` after exiting, it means that your changes have been applied.

[Restart](/index.php/Restart "Restart") `libvirtd.service` and [user service](/index.php/Systemd/User "Systemd/User") `pulseaudio.service`.

Virtual Machine audio will now be routed through the host as an application. The application [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) can be used to control the output device. Be aware that on Windows guests, this can cause audio crackling without [using Message-Signaled Interrupts.](#Slowed_down_audio_pumped_through_HDMI_on_the_video_card)

### Physical Disk/Partition

A whole disk or a partition may be used as a whole for improved I/O performance by adding an entry to XML

 `$ virsh edit [vmname]` 
```

<devices>
...
  <disk type='block' device='disk'>
    <driver name='qemu' type='raw' cache='none' io='native'/>
    <source dev='/dev/sdXX'/>
    <target dev='vda' bus='virtio'/>
    <address type='pci' domain='0x0000' bus='0x02' slot='0x0a' function='0x0'/>
  </disk>
...
</devices>

```

This would require a driver on Windows guests, refer to [#Setting up the guest OS](#Setting_up_the_guest_OS).

### Gotchas

#### Passing through a device that does not support resetting

When the VM shuts down, all devices used by the guest are deinitialized by its OS in preparation for shutdown. In this state, those devices are no longer functionnal and must then be power-cycled before they can resume normal operation. Linux can handle this power-cycling on its own, but when a device has no known reset methods, it remains in this disabled state and becomes unavailable. Since Libvirt and Qemu both expect all host PCI devices to be ready to reattach to the host before completely stopping the VM, when encountering a device that will not reset, they will hang in a "Shutting down" state where they will not be able to be restarted until the host system has been rebooted. It is therefore reccomanded to only pass through PCI devices which the kernel is able to reset, as evidenced by the presence of a `reset` file in the PCI device sysfs node, such as `/sys/bus/pci/devices/0000:00:1a.0/reset`.

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

## Complete setups and examples

If you have trouble configuring a certain mechanism in your setup, you might want to look up [complete passthrough setup examples](/index.php/PCI_passthrough_via_OVMF/Examples "PCI passthrough via OVMF/Examples"). A few users have described their setups and you might want to look up certain tricks from their configuration files.

## Troubleshooting

If your issue is not mentioned below, you may want to browse [QEMU#Troubleshooting](/index.php/QEMU#Troubleshooting "QEMU").

### "Error 43: Driver failed to load" on Nvidia GPUs passed to Windows VMs

**Note:**

*   This may also fix SYSTEM_THREAD_EXCEPTION_NOT_HANDLED boot crashes related to Nvidia drivers.
*   This may also fix problems under linux guests.

Since version 337.88, Nvidia drivers on Windows check if an hypervisor is running and fail if it detects one, which results in an Error 43 in the Windows device manager. Starting with QEMU 2.5.0 and libvirt 1.3.3, the vendor_id for the hypervisor can be spoofed, which is enough to fool the Nvidia drivers into loading anyway. All one must do is add `hv_vendor_id=whatever` to the cpu parameters in their QEMU command line, or by adding the following line to their libvirt domain configuration. It may help for the ID to be set to a 12-character alphanumeric (e.g. '123456789ab') as opposed to longer or shorter strings.

 `$ virsh edit [vmname]` 
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

Users with older versions of QEMU and/or libvirt will instead have to disable a few hypervisor extensions, which can degrade performance substantially. If this is what you want to do, do the following replacement in your libvirt domain config file.

 `$ virsh edit [vmname]` 
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

#### "BAR 3: cannot reserve [mem]" error in dmesg after starting VM

With respect to [this article](https://www.linuxquestions.org/questions/linux-kernel-70/kernel-fails-to-assign-memory-to-pcie-device-4175487043/):

If you still have code 43 check dmesg for memory reservation errors after starting up VM, if you have similar it could be the case:

```
vfio-pci 0000:09:00.0: BAR 3: cannot reserve [mem 0xf0000000-0xf1ffffff 64bit pref]

```

Find out a PCI Bridge your graphic card is connected to. This will give actual hierarchy of devices:

```
$ lspci -t

```

Before starting VM run following lines replacing IDs with actual from previous output.

```
# echo 1 > /sys/bus/pci/devices/0000\:00\:03.1/remove
# echo 1 > /sys/bus/pci/rescan

```

**Note:** Probably setting [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `video=efifb:off` is required as well. [Source](https://pve.proxmox.com/wiki/Pci_passthrough#BAR_3:_can.27t_reserve_.5Bmem.5D_error)

### UEFI (OVMF) Compatability in VBIOS

With respect to [this article](https://pve.proxmox.com/wiki/Pci_passthrough#How_to_known_if_card_is_UEFI_.28ovmf.29_compatible):

Error 43 can be caused by the GPU's VBIOS without UEFI support. To check whenever your VBIOS supports it, you will have to use `rom-parser`:

```
$ git clone [https://github.com/awilliam/rom-parser](https://github.com/awilliam/rom-parser)
$ cd rom-parser && make

```

Dump the GPU VBIOS:

```
# echo 1 > /sys/bus/pci/devices/0000:01:00.0/rom
# cat /sys/bus/pci/devices/0000:01:00.0/rom > /tmp/image.rom
# echo 0 > /sys/bus/pci/devices/0000:01:00.0/rom

```

And test it for compatibility:

 `$ ./rom-parser /tmp/image.rom` 
```
Valid ROM signature found @600h, PCIR offset 190h
	PCIR: type 0 (x86 PC-AT), vendor: 10de, device: 1184, class: 030000
	PCIR: revision 0, vendor revision: 1
Valid ROM signature found @fa00h, PCIR offset 1ch
	PCIR: type 3 (EFI), vendor: 10de, device: 1184, class: 030000
	PCIR: revision 3, vendor revision: 0
		EFI: Signature Valid, Subsystem: Boot, Machine: X64
	Last image

```

To be UEFI compatible, you need a "type 3 (EFI)" in the result. If it's not there, try updating your GPU VBIOS. GPU manufacturers often share VBIOS upgrades on their support pages. A large database of known compatible and working VBIOSes (along with their UEFI compatibility status!) is available on [TechPowerUp](https://www.techpowerup.com/vgabios/).

Updated VBIOS can be used in the VM without flashing. To load it in QEMU:

```
-device vfio-pci,host=07:00.0,......,romfile=/path/to/your/gpu/bios.bin \

```

And in libvirt:

```
<hostdev>
     ...
     <rom file='/path/to/your/gpu/bios.bin'/>
     ...
   </hostdev>
```

One should compare VBIOS versions between host and guest systems using [nvflash](https://www.techpowerup.com/download/nvidia-nvflash/) (Linux versions under *Show more versions*) or [GPU-Z](https://www.techpowerup.com/download/techpowerup-gpu-z/) (in Windows guest). To check the currently loaded VBIOS:

 `$ ./nvflash --version` 
```
...
Version               : 80.04.XX.00.97
...
UEFI Support          : No
UEFI Version          : N/A
UEFI Variant Id       : N/A ( Unknown )
UEFI Signer(s)        : Unsigned
...

```

And to check a given VBIOS file:

 `$ ./nvflash --version NV299MH.rom` 
```
...
Version               : 80.04.XX.00.95
...
UEFI Support          : Yes
UEFI Version          : 0x10022 (Jul  2 2013 @ 16377903 )
UEFI Variant Id       : 0x0000000000000004 ( GK1xx )
UEFI Signer(s)        : Microsoft Corporation UEFI CA 2011
...

```

If the external ROM did not work as it should in the guest, you will have to flash the newer VBIOS image to the GPU. In some cases it is possible to create your own VBIOS image with UEFI support using [GOPUpd](https://www.win-raid.com/t892f16-AMD-and-Nvidia-GOP-update-No-requests-DIY.html) tool, however this is risky and may result in GPU brick.

**Warning:** Failure during flashing may "brick" your GPU - recovery may be possible, but rarely easy and often requires additional hardware. **DO NOT** flash VBIOS images for other GPU models (different boards may use different VBIOSes, clocks, fan configuration). If it breaks, you get to keep all the pieces.

In order to avoid the irreparable damage to your graphics adapter it is necessary to unload the NVIDIA kernel driver first:

```
# modprobe -r nvidia_modeset nvidia 

```

Flashing the VBIOS can be done with:

```
# ./nvflash romfile.bin

```

**Warning:** **DO NOT** interrupt the flashing process, even if it looks like it's stuck. Flashing should take about a minute on most GPUs, but may take longer.

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

A `-` after `Enable` means MSI is supported, but not used by the VM, while a `+` says that the VM is using it.

The procedure to enable it is quite complex, instructions and an overview of the setting can be found [here](https://forums.guru3d.com/showthread.php?t=378044).

Other hints can be found on the [lime-technology's wiki](https://lime-technology.com/wiki/index.php/UnRAID_6/VM_Guest_Support#Enable_MSI_for_Interrupts_to_Fix_HDMI_Audio_Support), or on this article on [VFIO tips and tricks](https://vfio.blogspot.it/2014/09/vfio-interrupts-and-how-to-coax-windows.html).

Some tools named `MSI_util` or similar are available on the Internet, but they do not work on Windows 10 64bit.

In order to fix the issues enabling MSI on the 0 function of a nVidia card (`01:00.0 VGA compatible controller: NVIDIA Corporation GM206 [GeForce GTX 960] (rev a1) (prog-if 00 [VGA controller])`) was not enough; it will also be required to enable it on the other function (`01:00.1 Audio device: NVIDIA Corporation Device 0fba (rev a1)`) to fix the issue.

### No HDMI audio output on host when intel_iommu is enabled

If after enabling `intel_iommu` the HDMI output device of Intel GPU becomes unusable on the host then setting the option `igfx_off` (i.e. `intel_iommu=on,igfx_off`) might bring the audio back, please read `Graphics Problems?` in [Intel-IOMMU.txt](https://www.kernel.org/doc/Documentation/Intel-IOMMU.txt) for details about setting `igfx_off`.

### X doesn't start after enabling vfio_pci

This is related to the host GPU being detected as a secondary GPU, which causes X to fail/crash when it tries to load a driver for the guest GPU. To circumvent this, a Xorg configuration file specifying the BusID for the host GPU is required. The correct BusID can be acquired from lspci or the Xorg log. [Source →](https://www.redhat.com/archives/vfio-users/2016-August/msg00025.html)

 `/etc/X11/xorg.conf.d/10-intel.conf` 
```
Section "Device"
        Identifier "Intel GPU"
        Driver "modesetting"
        BusID  "PCI:0:2:0"
EndSection

```

### Chromium ignores integrated graphics for acceleration

Chromium and friends will try to detect as many GPUs as they can in the system and pick which one is preferred (usually discrete NVIDIA/AMD graphics). It tries to pick a GPU by looking at PCI devices, not OpenGL renderers available in the system - the result is that Chromium may ignore the integrated GPU available for rendering and try to use the dedicated GPU bound to the `vfio-pci` driver, and unusable on the host system, regardless of whenever a guest VM is running or not. This results in software rendering being used (leading to higher CPU load, which may also result in choppy video playback, scrolling and general un-smoothness).

This can be fixed by [explicitly telling Chromium which GPU you want to use](/index.php/Chromium/Tips_and_tricks#Forcing_specific_GPU "Chromium/Tips and tricks").

### VM only uses one core

For some users, even if IOMMU is enabled and the core count is set to more than 1, the VM still only uses one CPU core and thread. To solve this enable "Manually set CPU topology" in `virt-manager` and set it to the desirable amount of CPU sockets, cores and threads. Keep in mind that "Threads" refers to the thread count per CPU, not the total count.

### Passthrough seems to work but no output is displayed

Make sure if you are using virt-manager that UEFI firmware is selected for your virtual machine. Also, make sure you have passed the correct device to the VM.

### virt-manager has permission issues

If you are getting a permission error with virt-manager add the following to your `/etc/libvirt/qemu.conf`:

```
group="kvm"
user="*user*"

```

If that does not work make sure your user account is added to the kvm and libvirt [groups](/index.php/Groups "Groups").

## See also

*   [Discussion on Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=162768) | [Archived link](https://archive.is/kZYMt)
*   [User contributed hardware compatibility list](https://docs.google.com/spreadsheet/ccc?key=0Aryg5nO-kBebdFozaW9tUWdVd2VHM0lvck95TUlpMlE)
*   [Example script from https://www.youtube.com/watch?v=37D2bRsthfI](https://pastebin.com/rcnUZCv7)
*   [Complete tutorial for PCI passthrough](https://vfio.blogspot.com/)
*   [VFIO users mailing list](https://www.redhat.com/archives/vfio-users/)
*   [#vfio-users on freenode](https://webchat.freenode.net/?channels=vfio-users)
*   [YouTube: Level1Linux - GPU Passthrough for Virtualization with Ryzen](https://www.youtube.com/watch?v=aLeWg11ZBn0)