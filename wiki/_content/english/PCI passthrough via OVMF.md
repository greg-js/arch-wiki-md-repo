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
    *   [3.3 Gotchas](#Gotchas_2)
        *   [3.3.1 Tainting your boot GPU](#Tainting_your_boot_GPU)
*   [4 Installation](#Installation)
*   [5 Setting up libvirt](#Setting_up_libvirt)
*   [6 User-level access to devices](#User-level_access_to_devices)
*   [7 QEMU permissions](#QEMU_permissions)
*   [8 QEMU commands](#QEMU_commands)
*   [9 Create and configure VM for OVMF](#Create_and_configure_VM_for_OVMF)
*   [10 Complete example for QEMU (CLI-based) without libvirtd](#Complete_example_for_QEMU_.28CLI-based.29_without_libvirtd)
*   [11 Complete example for QEMU with libvirtd](#Complete_example_for_QEMU_with_libvirtd)
*   [12 Control VM via Synergy](#Control_VM_via_Synergy)
*   [13 Operating system](#Operating_system)
*   [14 Troubleshooting](#Troubleshooting)
    *   [14.1 "Error 43 : Driver failed to load" on Nvidia GPUs passed to Windows VMs](#.22Error_43_:_Driver_failed_to_load.22_on_Nvidia_GPUs_passed_to_Windows_VMs)
    *   [14.2 Dropped into uefi shell without boot errors](#Dropped_into_uefi_shell_without_boot_errors)
    *   [14.3 Unexpected crashes related to CPU exceptions](#Unexpected_crashes_related_to_CPU_exceptions)
*   [15 Additionnal information](#Additionnal_information)
    *   [15.1 ACS Override Patch](#ACS_Override_Patch)
*   [16 See also](#See_also)

## Prerequisites

A VGA Passthrough relies on a number of technologies that are not ubiquitous as of today and might not be available on your hardware. You will not be able to do this on your machine unless the following requirements are met :

*   Your CPU must support hardware virtualization (for kvm) and IOMMU (for the passthrough itself)
    *   [List of compatible Intel CPUs (Intel VT-x and Intel VT-d)](http://ark.intel.com/search/advanced?s=t&VTX=true&VTD=true)
    *   [List of compatible AMD CPUs (AMD-V and AMD-Vi)](http://support.amd.com/en-us/kb-articles/Pages/GPU120AMDRVICPUsHyperVWin8.aspx)
*   Your motherboard must also support IOMMU
    *   Both the chipset and the BIOS must support it. It is not always easy to tell at a glance whether or not this is the case, but there is a [fairly comprehensive list on the matter on the Xen wiki](http://wiki.xen.org/wiki/VTdHowTo) as well as [another one on Wikipedia](https://en.wikipedia.org/wiki/List_of_IOMMU-supporting_hardware "wikipedia:List of IOMMU-supporting hardware").
*   Your guest GPU ROM must support UEFI
    *   If you can find [any ROM in this list](https://www.techpowerup.com/vgabios/) that applies to your specific GPU and is said to support UEFI, you are generally in the clear. If not, you might want to try anyway if you have a recent GPU.

You will probably want to have a spare monitor (the GPU will not display anything if there is no screen plugged it and using a VNC or Spice connection will not help your performance), as well as a mouse and a keyboard you can pass to your VM. If anything goes wrong, you will at least have a way to control your host machine this way.

## Setting up IOMMU

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

The following command will allow you to see how your various PCI devices are mapped to IOMMU groups. If it does not return anything, you either have not enabled IOMMU support properly or your hardware does not support it.

 `$ for iommu_group in $(find /sys/kernel/iommu_groups/ -maxdepth 1 -mindepth 1 -type d); do echo "IOMMU group $(basename "$iommu_group")"; for device in $(ls -1 "$iommu_group"/devices/); do echo -n $'\t'; lspci -nns "$device"; done; done` 
```
IOMMU group 0
	00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v2/Ivy Bridge DRAM Controller [8086:0158] (rev 09)
IOMMU group 1
	00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port [8086:0151] (rev 09)
IOMMU group 2
	00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller [8086:0e31] (rev 04)
IOMMU group 4
	00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 [8086:0e2d] (rev 04)
IOMMU group 5
	00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller [8086:0e20] (rev 04)
IOMMU group 10
	00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 [8086:0e26] (rev 04)
IOMMU group 13
	06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)
```

An IOMMU group is the smallest set of physical devices that can be passed to a virtual machine. For instance, in the example above, both the GPU in 06:00.0 and its audio controller in 6:00.1 belong to IOMMU group 13 and can only be passed be passed together. The frontal USB controller, however, has its own group (group 2) which is separate from both the USB expansion controller (group 10) and the rear USB controller (group 4), meaning that any of them could be passed to a VM without affecting the others.

### Gotchas

#### Plugging your guest GPU in an unisolated CPU-based PCIe slot

Not all PCI-E slots are the same. Most motherboards have PCIe slots provided by both the CPU and the PCH. Depending on your CPU, it is possible that your processor-based PCIe slot does not support isolation properly, in which case the PCI slot itself will be appear to be grouped with the device that is connected to it.

```
IOMMU group 1
	00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port (rev 09)
	01:00.0 VGA compatible controller: NVIDIA Corporation GM107 [GeForce GTX 750] (rev a2)
	01:00.1 Audio device: NVIDIA Corporation Device 0fbc (rev a1)
```

This is fine so long as only your guest GPU is included in here, such as above. Depending on what is plugged in your other PCIe slots and whether they are allocated to your CPU or your PCH, you may find yourself with additional devices within the same group, which would force you to pass those as well. If you are ok with passing everything that is in there to your VM, you are free to continue. Otherwise, you will either need to try and plug your GPU in your other PCIe slots (if you have any) and see if those provide isolation from the rest or to install the ACS override patch, which comes with its own drawbacks.

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
IOMMU group 13
	06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)
```

You can then add those vendor-device ID pairs to the default parameters passed to vfio-pci whenever it is inserted into the kernel.

 `/etc/modprobe.d/vfio.conf`  `options vfio-pci ids=10de:13c2,10de:0fbb` 

This, however, does not guarantee that vfio-pci will be loaded before other graphics drivers. To ensure that, we need to statically bind it in the kernel image by adding it anywhere in the MODULES list in mkinitpcio.conf, alongside with its dependencies.

**Note:** If you also have another driver loaded this way for [early modesetting](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") (such as "nouveau", "radeon", "amdgpu", "i915", etc.), all of the following VFIO modules must preceed it.
 `/etc/mkinitcpio.conf`  `MODULES="... vfio vfio_iommu_type1 vfio_pci vfio_virqfd ..."` 

Remember to regenerate your initramfs.

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
IOMMU group 13
	06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)
```

Most linux distros (including Arch Linux) have pci-stub built statically within the kernel image. If for any reason it needs to be loaded as a module in your case, you will need to bind it yourself using whatever tool your distro provides for this, such as `mkinitpcio` for Arch.

 `/etc/mkinitcpio.conf`  `MODULES="... pci-stub ..."` 

Remember to regenerate your initramfs.

 `# mkinitcpio -p linux` 
**Note:** If you are using a non-standard kernel, such as `linux-vfio`, replace `linux` with whichever kernel you intend to use.

Add the relevant PCI device IDs to the kernel command line:

 `/etc/mkinitcpio.conf` 
```
...
GRUB_CMDLINE_LINUX_DEFAULT="... pci-stub.ids=10de:13c2,10de:0fbb ..."
...
```

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

### Gotchas

#### Tainting your boot GPU

If you are passing through your boot GPU and you cannot change it, make sure you also add `video=efifb:off` to your kernel command line so nothing gets sent to it before vfio-pci gets to bind with it.

## Installation

[Install](/index.php/Install "Install") [qemu](https://www.archlinux.org/packages/?name=qemu) and [rpmextract](https://www.archlinux.org/packages/?name=rpmextract). Consider installing [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) if you need the kernel with the patches.

Install edk2.git-ovmf-x64 from [Gerd Hoffman's repository](https://www.kraxel.org/repos/jenkins/edk2/).

Extract that archive to /usr:

```
# rpmextract.sh edk2.git-ovmf-x64-0-20150223.b877.ga8577b3.noarch.rpm
# cp -R ./usr/share/* /usr/share
```

Ensure /usr/share/edk2.git/ovmf-x64 contains these files:

 `$ ls -l /usr/share/edk2.git/ovmf-x64/*pure*.fd` 
```
/usr/share/edk2.git/ovmf-x64/OVMF-pure-efi.fd
/usr/share/edk2.git/ovmf-x64/OVMF_VARS-pure-efi.fd
/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd
```

This will be the BIOS that the VM will use. Non-UEFI users may need to use i440fx without OVMF, and the i915 vga arbiter patch for Intel graphics as host, see this forum thread. For users that do have a UEFI compatible motherboard but a UEFI incompatible graphics card, look at this post.

## Setting up libvirt

See [Polkit#Bypass password prompt](/index.php/Polkit#Bypass_password_prompt "Polkit") to bypass the password prompt, install [libvirt](https://www.archlinux.org/packages/?name=libvirt), then [enable](/index.php/Enable "Enable") and start `libvirtd.service`.

Start *virt-manager* and configure the hypervisor. Virtmanager should connect to the qemu session.

## User-level access to devices

Create udev rules to give user-access to devices (hdd and gpu):

 `/etc/udev/rules.d/10-qemu-hw-users.rules` 
```
KERNEL=="sda[3-6]", OWNER="YOUR_USER", GROUP="YOUR_GROUP"
KERNEL=="YOUR_VFIO_GROUPS", SUBSYSTEM=="vfio", OWNER="YOUR_USER", GROUP="YOUR_USER"
```

This should allow you to set qemu user and group to something a little safer than root:root in /etc/libvirtd/qemu.conf

## QEMU permissions

Give QEMU access to hardware (there may be safer ways of doing this):

 `/etc/libvirt/qemu.conf` 
```
...
user = "root"
group = "root"
clear_emulator_capabilities = 0
```

QEMU also needs acces to VFIO files. Include every numbered file in /dev/vfio:

```
ls -1 /dev/vfio

```
 `/etc/libvirt/qemu.conf` 
```
...
cgroup_device_acl = [
    "/dev/null", "/dev/full", "/dev/zero",
    "/dev/random", "/dev/urandom",
    "/dev/ptmx", "/dev/kvm", "/dev/kqemu",
    "/dev/rtc","/dev/hpet", "/dev/vfio/vfio",
    "/dev/vfio/1"
]
...
```

Referenced from [firewing1's webpage](http://www.firewing1.com/howtos/fedora-20/create-gaming-virtual-machine-using-vfio-pci-passthrough-kvm).

## QEMU commands

This is the command to run QEMU with VGA Passthrough:

```
cp /usr/share/edk2.git/ovmf-x64/OVMF_VARS-pure-efi.fd /tmp/my_vars.fd
qemu-system-x86_64 \
  -enable-kvm \
  -m 2048 \
  -cpu host,kvm=off \
  -vga none \
  -device vfio-pci,host=01:00.0 \
  -drive if=pflash,format=raw,readonly,file=/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd \
  -drive if=pflash,format=raw,file=/tmp/my_vars.fd

```

`-enable KVM` - enables KVM for your system, using AMD-VI/VT-D for hardware virtualisation.

`-m [number]` - sets the amount of memory the VM should have.

`-cpu host, kvm=off` - emulate the host's exact CPU. `kvm=off` is used for NVIDIA cards to stop it detecting a hypervisor and therefore exiting with an error.

`-vga none` - disables the built in graphics card emulation.

`-device vfio-pci,host=01:00.0 \` - PCI location of graphics card(s) you are using for VGA passthrough.

`-drive if=flash,format=raw,readonly,file=/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd` BIOS location.

For more commands see [QEMU](/index.php/QEMU "QEMU").

## Create and configure VM for OVMF

[Alex Williamson's blog](http://vfio.blogspot.com/2014/08/primary-graphics-assignment-without-vga.html)

Use virsh to edit the VM with these changes:

 `<domain type='kvm'>` 
```
<os>
 <loader readonly='yes' type='pflash'>/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd</loader>
 <nvram template='/usr/share/edk2.git/ovmf-x64/OVMF_VARS-pure-efi.fd'/>
</os>
```

A guide from: [Alex Williamson's blog - using virt-manager](http://vfio.blogspot.com/2014/08/primary-graphics-assignment-without-vga.html) can also be used, but in order to make virt-manager discover UEFI on your system, you need to tell your QEMU where to look for ovmf first. Edit your `/etc/libvirt/qemu.conf` appending this at the end of it:

```
nvram = [
  "/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd:/usr/share/edk2.git/ovmf-x64/OVMF_VARS-pure-efi.fd",
]

```

then restart libvirtd,

```
systemctl restart libvirtd.service

```

and you are good to go.

## Complete example for QEMU (CLI-based) without libvirtd

This script starts Samba and Synergy, runs the VM and closes everything after the VM is shut down. Note that this method does **not** require libvirtd to be running or configured, although the second statement has not been verified.

```
#!/bin/bash

echo "Starting Samba"
sudo systemctl start smbd.service
sudo systemctl start nmbd.service

echo "Starting Synergy"
/usr/bin/synergys --daemon --config /etc/synergy.conf

# This is probably not neccesary, except when updating the OVMF bios
# echo "Removing old OVMF variables"
# rm -v ./Windows_ovmf_vars_x64.bin
# echo "Copying new OVMF variables"
# cp -v /usr/share/ovmf/x64/ovmf_vars_x64.bin ./Windows_ovmf_vars_x64.bin

echo "Exporting PulseAudio driver"
export QEMU_AUDIO_DRV="pa"

echo "Starting VM"
sudo \
    qemu-system-x86_64 \
        -serial none \
        -parallel none \
        -nodefaults \
        -nodefconfig \
        -enable-kvm \
        -name Windows \
        -cpu host,kvm=off,check \
        -smp sockets=1,cores=4,threads=2 \
        -m 12288 \
        -soundhw hda \
        -device ich9-usb-uhci3,id=uhci \
        -device usb-ehci,id=ehci \
        -device nec-usb-xhci,id=xhci \
        -drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/ovmf_code_x64.bin \
        -drive if=pflash,format=raw,file=./Windows_ovmf_vars_x64.bin \
        -rtc base=localtime \
        -boot order=c \
        -net nic,vlan=0,macaddr=52:54:00:00:00:01,model=virtio,name=net0 \
        -net bridge,vlan=0,name=bridge0,br=br0 \
        -drive if=virtio,id=drive0,file=./Windows.img,format=raw,cache=none,aio=native \
        -nographic \
        -device vfio-pci,host=04:00.0,addr=09.0,multifunction=on \
        -device vfio-pci,host=04:00.1,addr=09.1

# For GPU sound
# add ",multifunction=on" to GPU
# -device vfio-pci,host=04:00.1,addr=09.1

# Standard VGA
# Remove "-nographic \" and "-device vfio-pci" lines
# -vga std

# Install
# In addination to the steps "Standard VGA", add or change these options
# -boot order=d \
# -device ide-cd,drive=drive-cd-disk1,id=cd-disk1,unit=0,bus=ide.0 \
# -drive file=/run/media/melvin/primarydata/Data/OS/Windows_10.img,if=none,id=drive-cd-disk1,media=cdrom \
# -device ide-cd,drive=drive-cd-disk2,id=cd-disk2,unit=0,bus=ide.1 \
# -drive file=/run/media/melvin/primarydata/Data/OS/virtio-win-0.1.109.iso,if=none,id=drive-cd-disk2,media=cdrom \

echo "VM closed"

echo "Stopping Synergy"
pkill synergys

echo "Stopping Samba"
sudo systemctl stop smbd.service
sudo systemctl stop nmbd.service

```

For more information regarding this example see [this email at Red Hat's vfio-users list](https://www.redhat.com/archives/vfio-users/2015-August/msg00020.html).

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

## Control VM via Synergy

[Synergy](http://synergy-project.org/) lets you easily share a single mouse and keyboard between multiple computers (even with different operating systems) without the need for special hardware. It is intended for users with multiple computers on their desk since each system uses its own monitor(s). See [Synergy](/index.php/Synergy "Synergy") arch wiki page for more information.

To control the VM using Synergy, first [install](/index.php/Install "Install") the [synergy](https://www.archlinux.org/packages/?name=synergy) package.

Additionally, ensure that you are not passing your keyboard or mouse through to the VM, as the Synergy server will be running on the host and thus need access to those devices.

Create the synergy server config.

 `/etc/synergy.conf` 
```
# Example config
section: screens
	vm:
		halfDuplexCapsLock = false
		halfDuplexNumLock = false
		halfDuplexScrollLock = false
		xtestIsXineramaUnaware = false
		switchCorners = none 
		switchCornerSize = 0
	host:
		halfDuplexCapsLock = false
		halfDuplexNumLock = false
		halfDuplexScrollLock = false
		xtestIsXineramaUnaware = false
		switchCorners = none 
		switchCornerSize = 0
end

section: aliases
	vm:
	        10.0.2.15 # default for vm
	host:
		10.0.2.2  # default for host
end

section: links
	vm:
		right = host
	host:
		left = vm
end

section: options
	relativeMouseMoves = false
	screenSaverSync = true
	win32KeepForeground = false
	switchCorners = none 
	switchCornerSize = 0
end
```

Replace `vm` and `host` with the hostnames of your Virtual Machine and host OS respectively.

Add `altgr = alt` in the section screens/vm if your Alt Gr key dose not work properly.

Before you start qemu or within your startup script:

```
$ /usr/bin/synergys --daemon --config /etc/synergy.conf

```

Now download and configure synergy as a client on the Virtual Machine. Exact configurations depend on the virtual OS. However, if you are running QEMU in User Networking Mode (default), the default IP of the host is `10.0.2.2`.

If while playing a game and the mouse behaves wonky or is too sensitive, change the `relativeMouseMoves = false` line in the `options` section to `relativeMouseMoves = true` and while playing a game, press the `Scroll Lock` key to lock your mouse to the VM.

## Operating system

Depending on your operating system, you may find that it may refuse to boot after a certain point. To work around this, simply replace `-vga none` to `-vga qxl`, install your operating system, check Device Manager and see if your graphics card has PCI device id equal to your actual GPU and install the graphics card driver, and then change it back to `-vga none`.

## Troubleshooting

### "Error 43 : Driver failed to load" on Nvidia GPUs passed to Windows VMs

Since version 337.88, Nvidia drivers on Windows check if an hypervisor is running and fail if it detects one, which results in an Error 43 in the Windows device manager. Starting with QEMU 2.5.0, the vendor_id for the hypervisor can be spoofed, which is enough to fool the Nvidia drivers into loading anyway. All one must do is add `hv_vendor_id=whatever` to the cpu parameters in their QEMU command line.

Since libvirt has not yet caught up with this new feature, libvirt users will instead have to create a dummy script that will insert that option in the QEMU command line at launch and set it as their emulator.

 `/usr/local/qemu-kvm-vga` 
```
#!/bin/sh
exec /usr/bin/qemu-system-x86_64 \
$(echo "$@" | sed 's|hv_time|hv_time,hv_vendor_id=whatever|g')
```
 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<emulator>/usr/local/qemu-kvm-vga</emulator>
...
```

Users with older versions of QEMU will instead have to disable a few hypervisor extensions, which can degrade performance substentially. If this is what you want to do, do the following replacement in your libvirt domain config file.

 `EDITOR=nano virsh edit myPciPassthroughVm` 
```
...
<hyperv>
	<relaxed state='on'/>
	<vapic state='on'/>
	<spinlocks state='on' retries='8191'/>
</hyperv>
...
<clock offset='localtime'>
	<timer name='hypervclock' present='yes'/>
</clock>
...
```

```
...
<hyperv>
	<relaxed state='off'/>
	<vapic state='off'/>
	<spinlocks state='off'/>
</hyperv>
...
<clock offset='localtime'>
	<timer name='hypervclock' present='no'/>
</clock>
...
<features>
	<kvm>
	<hidden state='on'/>
	</kvm>
</features>
...
```

### Dropped into uefi shell without boot errors

If you are dropped into a uefi shell and do not have any "boot failed" errors you may have an invalid uefi boot media. Try using an alternative linux/windows uefi boot media to determine if you have an invalid media.

### Unexpected crashes related to CPU exceptions

In some cases, kvm may react strangely to certain CPU operations, such as GeForce Experience complaining about an unsupported CPU being present or some game crashing for unknown reasons. A number of those issues can be solved by passing the `ignore_msrs=1` option to the KVM module, which will ignore unimplemented MSRs instead of returning an error value.

 `/etc/modprobe.d/kvm.conf` 
```
...
options kvm ignore_msrs=1
...
```

**Warning:** While this is normally safe and some applications might not work without this, silently ignoring unknown MSR accesses could potentially break other software within the VM or other VMs.

## Additionnal information

### ACS Override Patch

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

## See also

*   [Discussion on Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=162768) | [Archived link](https://archive.is/kZYMt)
*   [User contributed hardware compatibility list](https://docs.google.com/spreadsheet/ccc?key=0Aryg5nO-kBebdFozaW9tUWdVd2VHM0lvck95TUlpMlE)
*   [Example script from https://www.youtube.com/watch?v=37D2bRsthfI](http://pastebin.com/rcnUZCv7)
*   [Complete tutorial for PCI passthrough](http://vfio.blogspot.com/)