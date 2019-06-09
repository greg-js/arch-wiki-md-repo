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
            *   [1.2.1.2 Using RAMFB display](#Using_RAMFB_display)
        *   [1.2.2 Display vGPU output](#Display_vGPU_output)
            *   [1.2.2.1 Output using SPICE with MESA EGL](#Output_using_SPICE_with_MESA_EGL)
            *   [1.2.2.2 Output using SPICE with NVIDIA EGL or VNC](#Output_using_SPICE_with_NVIDIA_EGL_or_VNC)
            *   [1.2.2.3 Disable all output](#Disable_all_output)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Missing mdev_supported_types directory](#Missing_mdev_supported_types_directory)
*   [3 See also](#See_also)

## Configuration

You'll have to create a virtual GPU (vGPU) first, then assign it to your VM. The guest with a vGPU sees it as a "regular" GPU - just install the latest native drivers. (The vGPU actually does need specialized drivers to work correctly, but all the required changes are present in the latest upstream Linux/Windows drivers.)

You'll need to:

*   Use at least Linux 4.16 and [QEMU](/index.php/QEMU "QEMU") 2.12.
*   Enable kernel modules `kvmgt vfio-iommu-type1 vfio-mdev`.
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

First it is needed to add the following device inside the VM <devices> tag.

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

Replacing GVT_GUID with the above generated UUID.

#### Getting vGPU display contents

In order to retrieve the contents from the vGPU there are 2 possible ways

##### Using DMA-BUF display

**Warning:** Acording to this [issue](https://github.com/intel/gvt-linux/issues/20), this method will not work using OVMF for now.

First, modify the libvirt configuration

 `$ virsh edit [vmname]` 
```
<domain type='kvm'>

```

to

 `$ virsh edit [vmname]` 
```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>

```

Now we add those lines to your configuration right before the closing </domain> tag:

 `$ virsh edit [vmname]` 
```
...
 <qemu:commandline>
       <qemu:arg value='-set'/>
       <qemu:arg value='device.hostdev0.x-igd-opregion=on'/>
 </qemu:commandline>
...

```

##### Using RAMFB display

This can be combined with the above DMA-BUF in order to also display initial VGA initialization.

First, modify the libvirt configuration

 `$ virsh edit [vmname]` 
```
<domain type='kvm'>

```

to

 `$ virsh edit [vmname]` 
```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>

```

Now we add those lines to your configuration right before the closing </domain> tag:

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

## See also

*   [Official GVT-g Setup Guide](https://github.com/intel/gvt-linux/wiki/GVTg_Setup_Guide)
*   [Official GVT-g DMA-BUF User Guide](https://github.com/intel/gvt-linux/wiki/Dma_Buf_User_Guide).
*   [Running Windows via QEMU/KVM and Intel GVT-g](https://www.reddit.com/r/VFIO/comments/8h352p/guide_running_windows_via_qemukvm_and_intel_gvtg/)