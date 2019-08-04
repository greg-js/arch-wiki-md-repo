Related articles

*   [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF")
*   [QEMU](/index.php/QEMU "QEMU")
*   [Intel graphics](/index.php/Intel_graphics "Intel graphics")

[Intel GVT-g](https://github.com/intel/gvt-linux/wiki/GVTg_Setup_Guide) is a technology that provides mediated device passthrough for Intel GPUs (Broadwell and newer). It can be used to virtualize the GPU for multiple guest VMs, effectively providing near-native graphics performance in the VM and still letting your host use the virtualized GPU normally. This is useful if you want accelerated graphics in Windows VMs running on ultrabooks without dedicated GPUs for [full device passthrough](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF"). (Similar technologies exist for NVIDIA and AMD GPUs, but they're available only in the "professional" GPU lines like Quadro, Radeon Pro and so on.)

There is also a variant of this technology called GVT-d - it is essentially Intel's name for full device passthrough with the vfio-pci driver. With GVT-d, the host cannot use the virtualized GPU.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Using QEMU CLI](#Using_QEMU_CLI)
    *   [1.2 Using libvirt](#Using_libvirt)
        *   [1.2.1 Getting vGPU display contents](#Getting_vGPU_display_contents)
            *   [1.2.1.1 Using DMA-BUF display](#Using_DMA-BUF_display)
                *   [1.2.1.1.1 Using DMA-BUF with UEFI/OVMF](#Using_DMA-BUF_with_UEFI/OVMF)
            *   [1.2.1.2 Using RAMFB display](#Using_RAMFB_display)
        *   [1.2.2 Display vGPU output](#Display_vGPU_output)
            *   [1.2.2.1 Output using SPICE with MESA EGL](#Output_using_SPICE_with_MESA_EGL)
            *   [1.2.2.2 Output using SPICE with NVIDIA EGL or VNC](#Output_using_SPICE_with_NVIDIA_EGL_or_VNC)
            *   [1.2.2.3 Disable all output](#Disable_all_output)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Missing mdev_supported_types directory](#Missing_mdev_supported_types_directory)
    *   [2.2 Windows hanging with bad memory error](#Windows_hanging_with_bad_memory_error)
*   [3 See also](#See_also)

## Configuration

You'll have to create a virtual GPU (vGPU) first, then assign it to your VM. The guest with a vGPU sees it as a "regular" GPU - just install the latest native drivers. (The vGPU actually does need specialized drivers to work correctly, but all the required changes are present in the latest upstream Linux/Windows drivers.)

You'll need to:

*   Use at least Linux 4.16 and [QEMU](/index.php/QEMU "QEMU") 2.12.
*   [Enable](/index.php/Mkinitcpio#MODULES "Mkinitcpio") kernel modules `kvmgt vfio-iommu-type1 vfio-mdev`.
*   Add `i915.enable_gvt=1` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to enable GPU virtualization.
*   Find the PCI address and domain number of your GPU (`$GVT_PCI` and `$GVT_DOM` in commands below), as it resides in `/sys/bus/pci/devices`. It looks like this: `0000:00:02.0` - you can look it up by running `lspci -D -nn`, looking for `VGA compatible controller: Intel Corporation HD Graphics ...` and noting down the address on the left.
*   Generate the vGPU GUID (`$GVT_GUID` in commands below) which you'll use to create and assign the vGPU. A single virtual GPU can be assigned only to a single VM - create as many GUIDs as you want vGPUs. (You can do so by running `uuidgen`.)

After rebooting with the `i915.enable_gvt=1` flag, you should be able to create vGPUs - there are multiple vGPU types you can create, which mainly differ in the amount of resources dedicated to that vGPU. You can look up what types are available in your system (and `cat description` inside of each type to discover what it's capable of) like this:

```
# ls /sys/devices/pci${GVT_DOM}/$GVT_PCI/mdev_supported_types
i915-GVTg_V5_1  # Video memory: <512MB, 2048MB>, resolution: up to 1920x1200
i915-GVTg_V5_2  # Video memory: <256MB, 1024MB>, resolution: up to 1920x1200
i915-GVTg_V5_4  # Video memory: <128MB, 512MB>, resolution: up to 1920x1200
i915-GVTg_V5_8  # Video memory: <64MB, 384MB>, resolution: up to 1024x768

```

Pick a type you want to use - we'll refer to it as `$GVT_TYPE` below. Use the GUID you've created to create a vGPU with a chosen type:

```
# echo "$GVT_GUID" > "/sys/devices/pci${GVT_DOM}/$GVT_PCI/mdev_supported_types/$GVT_TYPE/create"

```

You can repeat this as many times as you want with different GUIDs. All created vGPUs will land in `/sys/bus/pci/devices/$GVT_PCI/` - if you'd like to remove a vGPU, you can do:

```
# echo 1 > /sys/bus/pci/devices/$GVT_PCI/$GVT_GUID/remove

```

### Using QEMU CLI

To create a VM with the virtualized GPU, add this parameter to the QEMU command line:

```
-device vfio-pci,sysfsdev=/sys/bus/pci/devices/$GVT_PCI/$GVT_GUID,rombar=0

```

### Using libvirt

With libvirt, add the following device to the `<devices>` element of the VM definition:

 `$ virsh edit [vmname]` 
```
...
    <hostdev mode='subsystem' type='mdev' managed='no' model='vfio-pci' display='off'>
      <source>
        <address uuid='**GVT_GUID'**/>
      </source>
    </hostdev>
...
```

Replace **GVT_GUID** with the UUID of your vGPU.

#### Getting vGPU display contents

There are several possible ways to retrieve the display contents from the vGPU.

##### Using DMA-BUF display

**Warning:** According to this [issue](https://github.com/intel/gvt-linux/issues/20), this method will not work with UEFI guests using (unmodified) OVMF. See below for patches/workarounds.

First, modify the XML schema of the VM definition so that we can use QEMU-specific elements later, changing

 `$ virsh edit [vmname]` 
```
<domain type='kvm'>

```

to

 `$ virsh edit [vmname]` 
```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>

```

Then add this configuration to the end of the `<domain>` element, i. e. insert this text right above the closing `</domain>` tag:

 `$ virsh edit [vmname]` 
```
...
  <qemu:commandline>
    <qemu:arg value='-set'/>
    <qemu:arg value='device.hostdev0.x-igd-opregion=on'/>
 </qemu:commandline>
...

```

###### Using DMA-BUF with UEFI/OVMF

As stated above, DMA-BUF display will not work with UEFI-based guests using (unmodified) OVMF because it won't create the necessary ACPI OpRegion exposed via QEMU's nonstandard fw_cfg interface. See [this OVMF bug](https://bugzilla.tianocore.org/show_bug.cgi?id=935) for details of this issue.

According to [this GitHub comment](https://github.com/intel/gvt-linux/issues/23#issuecomment-468125999), the OVMF bug report suggests several solutions to the problem. It is possible to:

*   [patch](https://bugzilla.tianocore.org/attachment.cgi?id=165) OVMF ([details](https://bugzilla.tianocore.org/show_bug.cgi?id=935#c4)) to add an Intel-specific quirk (most straightforward but non-upstreamable solution);
*   [patch](https://bugzilla.tianocore.org/attachment.cgi?id=168) the host kernel ([details](https://bugzilla.tianocore.org/show_bug.cgi?id=935#c12)) to automatically provide an option ROM for the vGPU containing basically the same code but in option ROM format;
*   [extract the OpROM](http://120.25.59.132:3000/vbios_gvt_uefi.rom) from the kernel patch ([source](https://www.reddit.com/r/VFIO/comments/av736o/creating_a_clover_bios_nonuefi_install_for_qemu/ehdz6mf/)) and feed it to QEMU as an override.

We will go with the last option because it does not involve patching anything. (Note: if the link goes down, the OpROM can be extracted from the kernel patch by hand.)

Download `vbios_gvt_uefi.rom` and place it somewhere world-accessible (we will use `/` to make an example). Then edit the VM definition, appending this configuration to the `<qemu:commandline>` element we added earlier:

 `$ virsh edit [vmname]` 
```
...
    <qemu:arg value='-set'/>
    <qemu:arg value='device.hostdev0.romfile=**/vbios_gvt_uefi.rom**'/>
...

```

##### Using RAMFB display

This can be combined with the above DMA-BUF configuration in order to also display everything that happens before the guest Intel driver is loaded (i. e. POST, the firmware interface and the guest initialization).

First, modify the XML schema of the VM definition so that we can use QEMU-specific elements later, changing

 `$ virsh edit [vmname]` 
```
<domain type='kvm'>

```

to

 `$ virsh edit [vmname]` 
```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>

```

Then add this configuration to the end of the `<domain>` element, i. e. insert this text right above the closing `</domain>` tag:

 `$ virsh edit [vmname]` 
```
...
 <qemu:commandline>
    <qemu:arg value='-set'/>
    <qemu:arg value='device.hostdev0.ramfb=on'/>
    <qemu:arg value='-set'/>
    <qemu:arg value='device.hostdev0.driver=vfio-pci-nohotplug'/>
 </qemu:commandline>
...

```

#### Display vGPU output

Due to an [issue](https://gitlab.freedesktop.org/spice/spice-gtk/issues/100) with spice-gtk the configuration is different depending of the SPICE client EGL implementation.

##### Output using SPICE with MESA EGL

```
$ virsh edit [vmname]

```

1.  Ensure the above added <hostdev> device have the display attribute set to 'on'.
2.  Remove all <graphics> and <video> devices.
3.  Add the following devices:

 `$ virsh edit [vmname]` 
```
...
    <graphics type='spice'>
      <listen type='none'/>
      <gl enable='yes'/>
    </graphics>
    <video>
      <model type='none'/>
    </video>
...

```

The are an optional attribute rendernode in gl tag to allow specify the renderer, example:

```
     <gl enable='yes' rendernode='/dev/dri/by-path/pci-0000:00:02.0-render'/>

```

##### Output using SPICE with NVIDIA EGL or VNC

```
$ virsh edit [vmname]

```

1.  Ensure the above added <hostdev> device have the display attribute set to 'on'.
2.  Remove all <graphics> and <video> devices.
3.  Add the following devices:

 `$ virsh edit [vmname]` 
```
...
    <graphics type='spice' autoport='yes'>
      <listen type='address'/>
    </graphics>
    <graphics type='egl-headless'/>
    <video>
      <model type='none'/>
    </video>
...

```

The <graphics type='spice'> type can be changed to 'vnc' to use VNC instead.

Also there are an *optional* tag <gl> inside <graphics type='egl-headless'> tag to force a specific renderer, do not put inside the 'spice' graphics due the mentioned bug, example:

```
   <graphics type='egl-headless'>
     <gl rendernode='/dev/dri/by-path/pci-0000:00:02.0-render'/>
   </graphics>

```

##### Disable all output

To ensure no emulated GPU is added one can edit the VM configuration and do the following changes:

```
$ virsh edit [vmname]

```

1.  Remove all <graphics> devices.
2.  Change the <video> device to be type 'none'.
3.  Ensure the above added <hostdev> device have the display attribute set to 'off'.

Then the only way to see the display output would be using a software server like RDP, VNC or Looking Glass. To see more details in [using Looking Glass to stream guest screen to the host](/index.php/PCI_passthrough_via_OVMF#Using_Looking_Glass_to_stream_guest_screen_to_the_host "PCI passthrough via OVMF").

## Troubleshooting

### Missing mdev_supported_types directory

If you have followed instructions and added `i915.enable_gvt=1` kernel parameter, but there is still no `/sys/bus/pci/devices/0000:02:00.0/mdev_supported_types` directory, probably your hardware is not supported. Check dmesg log for this message:

 `$ dmesg | grep -i gvt `  `[    4.227468] [drm] Unsupported device. GVT-g is disabled` 

If that is the case, you may want to check upstream for support plans. For example, for the "Coffee Lake" (CFL) platform support, see [https://github.com/intel/gvt-linux/issues/53](https://github.com/intel/gvt-linux/issues/53)

### Windows hanging with bad memory error

If Windows is hanging due to a Bad Memory error look for more details via dmesg. If the logs show something like rlimit memory exceeded, you may need to increase the max memory linux allows qemu to allocate. Assuming you are in the group kvm, adding the following to /etc/security/limits.conf and restarting the PC fixed the errors for me.

```
   # qemu kvm, need high memlock to allocate mem for vga-passthrough
   @kvm	hard	memlock	8388608
   @kvm	soft	memlock	8388608

```

## See also

*   [Official GVT-g Setup Guide](https://github.com/intel/gvt-linux/wiki/GVTg_Setup_Guide)
*   [Official GVT-g DMA-BUF User Guide](https://github.com/intel/gvt-linux/wiki/Dma_Buf_User_Guide).
*   [Running Windows via QEMU/KVM and Intel GVT-g](https://www.reddit.com/r/VFIO/comments/8h352p/guide_running_windows_via_qemukvm_and_intel_gvtg/)
*   [Blog post about using GVT](https://blog.bepbep.co/posts/gvt/)