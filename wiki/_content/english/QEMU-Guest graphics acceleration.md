Related articles

*   [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF")
*   [QEMU](/index.php/QEMU "QEMU")
*   [KVM](/index.php/KVM "KVM")

There are multiple methods for virtual machine (VM) graphics display which yield greatly accelerated or near-bare metal performance.

## Contents

*   [1 Methods for QEMU guest graphics acceleration](#Methods_for_QEMU_guest_graphics_acceleration)
    *   [1.1 QXL video driver and SPICE client for display](#QXL_video_driver_and_SPICE_client_for_display)
    *   [1.2 PCI GPU passthrough](#PCI_GPU_passthrough)
        *   [1.2.1 PCI VGA/GPU passthrough via OVMF](#PCI_VGA.2FGPU_passthrough_via_OVMF)
        *   [1.2.2 Looking Glass](#Looking_Glass)
    *   [1.3 Fully virtualized GPU support via Intel-specific iGVT-g extension](#Fully_virtualized_GPU_support_via_Intel-specific_iGVT-g_extension)
    *   [1.4 Virgil3d virtio-gpu paravirtualized device driver](#Virgil3d_virtio-gpu_paravirtualized_device_driver)

## Methods for QEMU guest graphics acceleration

### QXL video driver and SPICE client for display

[QXL/SPICE](/index.php/QEMU#qxl "QEMU") is a high-performance display method. However, it is not designed to offer near-bare metal performance.

### PCI GPU passthrough

#### PCI VGA/GPU passthrough via OVMF

[PCI passthrough](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF") currently seems to be the most popular method for optimal performance. [This forum thread](https://bbs.archlinux.org/viewtopic.php?id=162768&p=1) (now closed) may be of interest for problem solving.

#### Looking Glass

There is a fairly recent passthrough method called [Looking Glass](https://looking-glass.hostfission.com/). See [this guide to getting started](https://forum.level1techs.com/t/looking-glass-guides-help-and-support/122387) which provides some problem solving and user support. Looking Glass uses DXGI (MS DirectX Graphics Infrastructure) to pass complete frames captured from the VM's passed-through video card via shared memory to the host system where they are read (scraped) by a display client running on the bare-metal host.

### Fully virtualized GPU support via Intel-specific iGVT-g extension

[iGVT-g](/index.php/Intel_graphics#Intel_GVT-g_Graphics_Virtualization_Support "Intel graphics") is limited to Intel graphics on [recent Intel CPUs](https://github.com/intel/gvt-linux/wiki/GVTg_Setup_Guide) (starting with 5th generation Intel Core(TM) processors). For more information, see [this Reddit thread for use on an Arch host system](https://www.reddit.com/r/VFIO/comments/8h352p/guide_running_windows_via_qemukvm_and_intel_gvtg/).

### Virgil3d virtio-gpu paravirtualized device driver

[Virgil3d](https://virgil3d.github.io/) virtio-gpu is a paravirtualized 3d accelerated graphics driver, similar to [non-graphics virtio drivers](/index.php/QEMU#Installing_virtio_drivers "QEMU") (see [virtio driver information](https://www.linux-kvm.org/page/Virtio) and [virtio Windows guest drivers](https://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers)). For Linux guests, [virtio-gpu](/index.php/QEMU#virtio "QEMU") is fairly mature, having been available since Linux kernel version 4.4 and QEMU version 2.6\. See [this Reddit Arch thread](https://www.reddit.com/r/archlinux/comments/7nmceg/kvmqemu_with_virtiogpu_virgl_support_enabled/) and [Gerd Hoffmann's blog for using this with libvirt and spice](https://www.kraxel.org/blog/2016/09/using-virtio-gpu-with-libvirt-and-spice/).

For Windows guests, there is very little information on [VirtIO-gpu OpenGL drivers](https://studiopixl.com/2017-08-27/3d-acceleration-using-virtio.html). [A project summary](https://gist.github.com/Keenuts/199184f9a6d7a68d9a62cf0011147c0b), [the DOD (Windows kernel) driver](https://gitlab.com/spice/win32/virtio-gpu-wddm-dod) and [the ICD (Windows userland) driver](https://github.com/Keenuts/virtio-gpu-win-icd) are available. In addition, see [this Phoronix article](https://www.phoronix.com/scan.php?page=news_item&px=QEMU-3D-Windows-Guests) and its comments.