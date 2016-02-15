This is a guide on how to do PCI VGA Passthrough on QEMU. Since kernel 3.9 and a change in QEMU, it is now possible to passthrough a graphics card, offering the VM native graphics performance which is useful when doing graphic-intensive tasks such as gaming. To do this, you need two graphics cards, one for the host and one for the VM; it is possible to use integrated graphics for the host. Your processor and motherboard also need to support AMD-VI/VT-D.

## Contents

*   [1 Installation](#Installation)
*   [2 Setting up libvirt](#Setting_up_libvirt)
*   [3 Enabling IOMMU](#Enabling_IOMMU)
*   [4 User-level access to devices](#User-level_access_to_devices)
*   [5 Isolating the GPU](#Isolating_the_GPU)
    *   [5.1 vfio-pci](#vfio-pci)
    *   [5.2 pci-stub](#pci-stub)
    *   [5.3 Blacklisting modules](#Blacklisting_modules)
    *   [5.4 Binding to VFIO](#Binding_to_VFIO)
*   [6 IOMMU groups](#IOMMU_groups)
    *   [6.1 ACS Override Patch](#ACS_Override_Patch)
*   [7 QEMU permissions](#QEMU_permissions)
*   [8 QEMU commands](#QEMU_commands)
*   [9 Create and configure VM for OVMF](#Create_and_configure_VM_for_OVMF)
*   [10 Complete example for QEMU (CLI-based) without libvirtd](#Complete_example_for_QEMU_.28CLI-based.29_without_libvirtd)
*   [11 Control VM via Synergy](#Control_VM_via_Synergy)
*   [12 Operating system](#Operating_system)
*   [13 Make Nvidia's GeForce Experience work](#Make_Nvidia.27s_GeForce_Experience_work)
*   [14 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [qemu](https://www.archlinux.org/packages/?name=qemu) and [rpmextract](https://www.archlinux.org/packages/?name=rpmextract). Consider installing [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) if you need the kernel with the patches.

Install edk2.git-ovmf-x64 from [Gerd Hoffman's repository](https://www.kraxel.org/repos/jenkins/edk2/).

Extract that archive to /usr:

```
# rpmextract.sh edk2.git-ovmf-x64-0-20150223.b877.ga8577b3.noarch.rpm
# cp -R ./usr/share/* /usr/share
```

Ensure /usr/share/edk2.git/ovmf-x64 contains these files:

 `$ ls /usr/share/edk2.git/ovmf-x64/*pure*.fd` 

```
/usr/share/edk2.git/ovmf-x64/OVMF-pure-efi.fd
/usr/share/edk2.git/ovmf-x64/OVMF_VARS-pure-efi.fd
/usr/share/edk2.git/ovmf-x64/OVMF_CODE-pure-efi.fd
```

This will be the BIOS that the VM will use. Non-UEFI users may need to use i440fx without OVMF, and the i915 vga arbiter patch for Intel graphics as host, see this forum thread. For users that do have a UEFI compatible motherboard but a UEFI incompatible graphics card, look at this post.

## Setting up libvirt

See [Polkit#Bypass password prompt](/index.php/Polkit#Bypass_password_prompt "Polkit") to bypass the password prompt, install [libvirt](https://www.archlinux.org/packages/?name=libvirt), then [enable](/index.php/Enable "Enable") and start `libvirtd.service`.

Start _virt-manager_ and configure the hypervisor. Virtmanager should connect to the qemu session.

## Enabling IOMMU

Ensure that AMD-VI/VT-D is enabled in your BIOS settings.

If your processor is Intel, add `intel_iommu=on` to your [bootloader kernel options](/index.php/Kernel_parameters "Kernel parameters"). Simlarly, if you have an AMD processor, add `amd_iommu=on`.

After rebooting, check dmesg to confirm IOMMU is enabled:

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

## User-level access to devices

Create udev rules to give user-access to devices (hdd and gpu):

 `/etc/udev/rules.d/10-qemu-hw-users.rules` 

```
KERNEL=="sda[3-6]", OWNER="YOUR_USER", GROUP="YOUR_GROUP"
KERNEL=="YOUR_VFIO_GROUPS", SUBSYSTEM=="vfio", OWNER="YOUR_USER", GROUP="YOUR_USER"
```

This should allow you to set qemu user and group to something a little safer than root:root in /etc/libvirtd/qemu.conf

## Isolating the GPU

Find your target card's PCI locations and device IDs:

 `lspci -nn|grep -iP "NVIDIA|Radeon"` 

```
01:00.0 VGA compatible controller [0300]: Advanced Micro Devices, Inc. [AMD/ATI] Cayman PRO [Radeon HD 6950] [1002:6719]
01:00.1 Audio device [0403]: Advanced Micro Devices, Inc. [AMD/ATI] Cayman/Antilles HDMI Audio [Radeon HD 6900 Series] [1002:aa80]
04:00.0 VGA compatible controller [0300]: NVIDIA Corporation G73 [GeForce 7600 GS] [10de:0392] (rev a1)
```

In this case, the three PCI device IDs we're after are `1002:6719 1002:aa80 10de:0392`, and their locations are `01:00.0 01:00.1 04:00.0`. Make note of any locations and device IDs you intend to pass through to the VM.

To allow the VM access to your passthrough'd devices, you'll need to claim it before the host drivers do. This can be achieved with either one of two kernel modules, `vfio-pci` or `pci-stub`.

vfio-pci is available in kernel v4.1+, and is the recommended option if your kernel supports it. You can check if this module is available by running:

```
$ modprobe vfio-pci

```

If there is no output, you're good to go. If instead you receive `modprobe: FATAL: Module vfio-pci not found`, use the guide further down for `pci-stub` instead.

### vfio-pci

Ensure the vfio-pci driver is loaded on bootup through `modprobe.d`. It is necessary to tell the vfio-pci driver which PCI devices to bind. If you were adding all three of the PCI devices listed above, your modprobe.d launch config would have the following contents:

 `/etc/modprobe.d/vfio.conf` 

```
options vfio-pci ids=1002:6719,1002:aa80,10de:0392

```

Next we'll want to ensure the kernel loads the necessary modules for vfio-pci when starting up:

 `/etc/mkinitcpio.conf` 

```
...
MODULES="vfio vfio_iommu_type1 vfio_pci vfio_virqfd"
...
```

Save the changes to the initial ramdisk environment:

```
# mkinitcpio -p linux

```

**Note:** If you're using a non-standard kernel, replace "linux" with whichever kernel you intend to use.

When using the 'base' hook in the initramfs, all modules specified in the MODULES array are loaded statically early in the boot process. The same behavior can be achieved with the 'systemd' hook by using the 'rd.modules-load' kernel parameter to specify modules that should be statically loaded early.

```
rd.modules-load=vfio-pci,...

```

Reboot and check dmesg output for successful assignment of the device(s) to vfio-pci:

 `dmesg | grep -i vfio` 

```
...
[    0.456472] VFIO - User Level meta-driver version: 0.3
[    0.470269] vfio_pci: add [10de:13c2[ffff:ffff]] class 0x000000/00000000
[    0.483631] vfio_pci: add [10de:0fbb[ffff:ffff]] class 0x000000/00000000
[    0.496998] vfio_pci: add [8086:8ca0[ffff:ffff]] class 0x000000/00000000
[    2.420184] vfio-pci 0000:0a:00.0: enabling device (0000 -> 0003)
[   38.590395] vfio_ecap_init: 0000:0a:00.0 hiding ecap 0x1e@0x258
[   38.590413] vfio_ecap_init: 0000:0a:00.0 hiding ecap 0x19@0x900
[   38.606881] vfio-pci 0000:0a:00.1: enabling device (0000 -> 0002)
[   38.620241] vfio-pci 0000:00:1b.0: enabling device (0000 -> 0002)
...
```

You can cross reference devices id's with `lspci -nn`'s output.

### pci-stub

If your kernel does not support vfio-pci, you can use the pci-stub module instead.

Add `pci-stub` to `/etc/mkinitcpio.conf`:

 `/etc/mkinitcpio.conf`  `MODULES="... pci-stub ..."` 

If it doesn't work, try adding it to /etc/modules-load.d/ as well:

```
$ echo "pci-stub" > sude tee /etc/modules-load.d/vfio.conf

```

Add the relevant PCI device IDs to the kernel command line:

 `/etc/mkinitcpio.conf` 

```
...
GRUB_CMDLINE_LINUX_DEFAULT="... pci-stub.ids=1002:6719,1002:aa80,10de:0392 ..."
...
```

If your graphics card has audio as a separated PCI device, it must be added as well:

```
pci-stub.ids=1002:6719,1002:aa80

```

Reload the grub configuration:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Check dmesg output for successful assignment of the device to pci-stub:

 `dmesg | grep pci-stub` 

```
...
[    2.390128] pci-stub: add 1002:6719 sub=FFFFFFFF:FFFFFFFF cls=00000000/00000000
[    2.390143] pci-stub 0000:01:00.0: claimed by stub
[    2.390150] pci-stub: add 1002:AA80 sub=FFFFFFFF:FFFFFFFF cls=00000000/00000000
[    2.390159] pci-stub 0000:01:00.1: claimed by stub
[    2.390150] pci-stub: add 1002:0392 sub=FFFFFFFF:FFFFFFFF cls=00000000/00000000
[    2.390159] pci-stub 0000:04:00.0: claimed by stub
...
```

### Blacklisting modules

Alternatively, if your host does not require the driver of the PCI device you intend to pass through (i.e. your host and VM are not using the same GPU vendor), you can blacklist `radeon` and `fglrx` for AMD GPUs, or `nouveau` and `nvidia` for NVIDIA GPus in `/etc/modprobe.d/blacklist.conf`.

Example, blacklisting the opensource radeon module:

 `/etc/modprobe.d/modprobe.conf`  `blacklist radeon` 

### Binding to VFIO

There are many methods to bind the card to vfio, here is one example:

*   [firewing1 webpage](http://www.firewing1.com/howtos/fedora-20/create-gaming-virtual-machine-using-vfio-pci-passthrough-kvm). Check the part after grub2-mkconfig.

## IOMMU groups

Only complete IOMMU groups can be attached to the guest VM. To see which groups each of your PCI devices are assigned to:

 `# find /sys/kernel/iommu_groups/ -type l` 

```
/sys/kernel/iommu_groups/0/devices/0000:00:00.0
/sys/kernel/iommu_groups/1/devices/0000:00:01.0
/sys/kernel/iommu_groups/1/devices/0000:01:00.0
/sys/kernel/iommu_groups/1/devices/0000:01:00.1
/sys/kernel/iommu_groups/2/devices/0000:00:02.0
/sys/kernel/iommu_groups/3/devices/0000:00:16.0
/sys/kernel/iommu_groups/4/devices/0000:00:1a.0
/sys/kernel/iommu_groups/5/devices/0000:00:1b.0
/sys/kernel/iommu_groups/6/devices/0000:00:1c.0
/sys/kernel/iommu_groups/7/devices/0000:00:1c.5
/sys/kernel/iommu_groups/8/devices/0000:00:1c.6
/sys/kernel/iommu_groups/9/devices/0000:00:1c.7
/sys/kernel/iommu_groups/9/devices/0000:05:00.0
/sys/kernel/iommu_groups/10/devices/0000:00:1d.0
/sys/kernel/iommu_groups/11/devices/0000:00:1f.0
/sys/kernel/iommu_groups/11/devices/0000:00:1f.2
/sys/kernel/iommu_groups/11/devices/0000:00:1f.3
/sys/kernel/iommu_groups/12/devices/0000:02:00.0
/sys/kernel/iommu_groups/12/devices/0000:02:00.1
/sys/kernel/iommu_groups/13/devices/0000:03:00.0
/sys/kernel/iommu_groups/14/devices/0000:04:00.0
```

### ACS Override Patch

If you find your PCI devices grouped among others that you don't wish to pass through, you may be able to seperate them using Alex Williamson's ACS override patch. Make sure you understand [the potential risk](http://vfio.blogspot.com/2014/08/iommu-groups-inside-and-out.html) of doing so.

You'll need a kernel with the patch applied. The easiest method to acquiring this is through the [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/) package.

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

For more commands see [QEMU.](https://wiki.archlinux.org/index.php/QEMU)

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

```
<hyperv>
 <relaxed state='off'/>
 <vapic state='off'/>
 <spinlocks state='off'/>
</hyperv>
```

```
<features>
 <kvm>
  <hidden state='on'/>
 </kvm>
</features>
```

```
<clock>
 <timer name='hypervclock' present='no'/>
</clock>
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

This script starts Samba and Synergy, runs the VM and closes everything after the VM is shut down. Note that this method does **not** require libvirtd to be running or configured, although the second statement hasn't been verified.

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

Add `altgr = alt` in the section screens/vm if your Alt Gr key dosen't work properly.

Before you start qemu or within your startup script:

```
$ /usr/bin/synergys --daemon --config /etc/synergy.conf

```

Now download and configure synergy as a client on the Virtual Machine. Exact configurations depend on the virtual OS. However, if you are running QEMU in User Networking Mode (default), the default IP of the host is `10.0.2.2`.

If while playing a game and the mouse behaves wonky or is too sensitive, change the `relativeMouseMoves = false` line in the `options` section to `relativeMouseMoves = true` and while playing a game, press the `Scroll Lock` key to lock your mouse to the VM.

## Operating system

Depending on your operating system, you may find that it may refuse to boot after a certain point. To work around this, simply replace `-vga none` to `-vga qxl`, install your operating system, check Device Manager and see if your graphics card has PCI device id equal to your actual GPU and install the graphics card driver, and then change it back to `-vga none`.

## Make Nvidia's GeForce Experience work

If GeForce Experience complains about an unsupported CPU being present and some features, e.g. game optimization, don't work, passing the `ignore_msrs=1` option to the KVM module will most likely solve the problem by ignoring accesses to unimplemented MSRs:

 `/etc/modprobe.d/kvm.conf` 

```
...
options kvm ignore_msrs=1
...
```

**Warning:** Silently ignoring unknown MSR accesses could potentially break other software within the VM or other VMs.

## See also

*   [Discussion on Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=162768) | [Archived link](https://archive.is/kZYMt)
*   [User contributed hardware compatibility list](https://docs.google.com/spreadsheet/ccc?key=0Aryg5nO-kBebdFozaW9tUWdVd2VHM0lvck95TUlpMlE)
*   [Example script from https://www.youtube.com/watch?v=37D2bRsthfI](http://pastebin.com/rcnUZCv7)
*   [Complete tutorial for PCI passthrough](http://vfio.blogspot.com/)