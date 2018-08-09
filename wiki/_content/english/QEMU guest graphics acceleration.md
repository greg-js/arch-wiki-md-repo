Related articles

*   [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF")
*   [QEMU](/index.php/QEMU "QEMU")
*   [KVM](/index.php/KVM "KVM")

There are multiple methods for virtual machine (VM) graphics display which yield greatly accelerated or near-bare metal performance.

## Review of methods for qemu guest graphics acceleration

1.  QXL video driver and SPICE client for display
    *   [QXL](/index.php/QEMU#qxl "QEMU") is a high-performance display method. However, it is not designed to offer near-bare metal performance.
2.  PCI VGA/GPU passthrough via OVMF
    *   [PCI VGA passthrough](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF) currently seems to be the most popular method for optimal performance. [This forum thread](https://bbs.archlinux.org/viewtopic.php?id=162768&p=1) (now closed) may be of interest for problem solving.
    *   Looking Glass
        *   There is a fairly recent passthrough method called [Looking Glass](https://looking-glass.hostfission.com/). See [this guide to getting started](https://forum.level1techs.com/t/looking-glass-guides-help-and-support/122387) which provides some problem solving and user support. Looking Glass uses DXGI (MS DirectX Graphics Infrastructure) to pass complete frames captured from the VM's passed-through video card via shared memory to the host system where they are read (scraped) by a display client running on the bare-metal host.
3.  Fully virtualized GPU support for the VM via Intel-specific iGVT-g extension
    *   [iGVT-g](https://wiki.archlinux.org/index.php/intel_graphics#Intel_GVT-g_Graphics_Virtualization_Support) is restricted to Intel graphics (which could be seen as a performance limitation). For more information, see [this Reddit thread for use on an Arch host system](https://www.reddit.com/r/VFIO/comments/8h352p/guide_running_windows_via_qemukvm_and_intel_gvtg/).
4.  [Virgil3d](https://virgil3d.github.io/) para-virtualized virtio-gpu device
    *   For Linux guests, [virtio-vga/virtio-gpu](/index.php/QEMU#virtio "QEMU") is fairly mature, having been available since Linux kernel version 4.4\. See [this Reddit Arch thread](https://www.reddit.com/r/archlinux/comments/7nmceg/kvmqemu_with_virtiogpu_virgl_support_enabled/) and [Gerd Hoffman's blog for using this with libvirt and spice](https://www.kraxel.org/blog/2016/09/using-virtio-gpu-with-libvirt-and-spice/).
        Currently, there is very little information on [the VirtIO-gpu OpenGL drivers for Windows guests](https://studiopixl.com/2017-08-27/3d-acceleration-using-virtio.html). [A project summary](https://gist.github.com/Keenuts/199184f9a6d7a68d9a62cf0011147c0b), [the DOD (Windows kernel) driver](https://gitlab.com/spice/win32/virtio-gpu-wddm-dod) and [the ICD (Windows userland) driver](https://github.com/Keenuts/virtio-gpu-win-icd) are of interest. In addition, see [this Phoronix article](https://www.phoronix.com/scan.php?page=news_item&px=QEMU-3D-Windows-Guests) which includes comments.