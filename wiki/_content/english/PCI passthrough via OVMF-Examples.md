As PCI passthrough is quite tricky to get right (both on the hardware and software configuration sides), this page presents **working, complete** VFIO setups. Feel free to look up users' scripts, BIOS/UEFI configuration, configuration files and specific hardware. If you have a problem, it might have been stumbled upon by other VFIO users and fixed in the examples below.

**Note:** If you've got VFIO working properly, please post your own setup according to the template on the bottom.

## Contents

*   [1 Users' setups](#Users.27_setups)
    *   [1.1 DragoonAethis: 6700K, GA-Z170X-UD3, GTX 1070](#DragoonAethis:_6700K.2C_GA-Z170X-UD3.2C_GTX_1070)
    *   [1.2 Manbearpig3130's Virtual Gaming Machine](#Manbearpig3130.27s_Virtual_Gaming_Machine)
*   [2 Adding your own setup](#Adding_your_own_setup)

## Users' setups

### DragoonAethis: 6700K, GA-Z170X-UD3, GTX 1070

Hardware:

*   **CPU**: Intel Core i7-6700K (using iGPU as the host GPU)
*   **Motherboard**: Gigabyte GA-Z170X-UD3 (Revision 1.0, BIOS/UEFI Version: F22)
*   **GPU**: MSI GeForce 1070 Gaming X (10Gbps)
*   **RAM**: 16GB DDR4 2400MHz

Configuration:

*   **Kernel**: Linux-ck (no ACS patch needed).
*   Using **libvirt**: XML domain, helper scripts, IOMMU groups, etc available in [my VFIO repository](https://github.com/DragoonAethis/VFIO).
*   **Guest OS**: Windows 8.1 Pro.
*   The entire HDD is passed to the VM as a raw device (formatted as a single NTFS partition).
*   HDMI audio is used, couldn't get audio output from QEMU to work properly. (Host uses ALSA only.)
*   Keyboard and mouse is passed to the guest VM and shared with the host with Synergy.
*   Bridged networking (with NetworkManager's and [this tutorial's](https://www.happyassassin.net/2014/07/23/bridged-networking-for-libvirt-with-networkmanager-2014-fedora-21/) help) is used. `bridge0` is created, `eth0` interface is bound to it. STP disabled, VirtIO NIC is configured in the VM and that VM is seen in the network just as any other computer (and is being assigned an IP address from the router itself, can communicate freely with other computers).

### Manbearpig3130's Virtual Gaming Machine

Hardware:

*   **CPU**: Intel Core i7-6850K
*   **Motherboard**: Gigabyte x99-Ultra Gaming-CF (Revision 1.0, BIOS/UEFI Version: F4)
*   **Host GPU**: AMD Radeon HD6950
*   **Guest GPU**: AMD R9 390
*   **RAM**: 32GB G-Skill Ripjaws DDR4 3333MHz

Configuration:

*   **Host Kernel**: Kernel version Linux 4.7.2-1 (No ACS patch).
*   Using **libvirt QEMU/KVM with OVMF**: link to domain XMLs/scripts/notes: [https://github.com/manbearpig3130/MBP-VT-d-gaming-machine](https://github.com/manbearpig3130/MBP-VT-d-gaming-machine)
*   **Host OS**: Arch Linux
*   **Guest OS**: Windows 10 Pro
*   2x 480GB SSDs set up in LVM striped mode formatted to ext4 are mounted in linux which contains the guest's qcow2 virtual VirtIO disk.
*   USB Host controller is passed through, giving most USB ports to the VM, leaving my USB 3.1 controller with attached USB hub for the host.
*   Motherboard has two NICs, one is passed into VM (Works after installing Killer NIC Driver).
*   To get HDMI audio working in windows I have to roll back the HDMI audio drivers from AMD back to the default Windows driver in device manager for some reason.
*   Sometimes doesn't boot properly, and have to restart the VM, sometimes a few times before it boots properly. I think it may have something to do with how Windows handles shutdown?
*   VM gets dedicated 16GB RAM via static hugepages.
*   CPU pinning increased performance considerably.
*   Windows boots straight into Steam big picture mode on it's primary display (43" Sony Bravia). Overall an awesome gaming machine that meets my gaming needs and lust for GNU/Linux at the same time.

## Adding your own setup

Add a new section with your nickname, CPU, motherboard and GPU models, then copy and paste this template to your section:

```
Hardware:
* '''CPU''': 
* '''Motherboard''': (Revision , BIOS/UEFI Version: )
* '''GPU''': 
* '''RAM''': 

Configuration:
* '''Kernel''': Kernel version (vanilla/CK/Zen/ACS-patched or not).
* Using '''libvirt/QEMU''': link to domain XMLs/scripts/notes (Git repo preferred).
* Issues you've encountered, special steps taken to make something work a bit better, etc.
* Describe your setup loosely here, so that when other wiki users are looking for something, they can easily skim through available setups.

```

Replace proper sections with your own data. Make sure to provide the exact motherboard model, revision (if possible - should be on both the motherboard itself and the box it came in) and BIOS/UEFI version you're using. Describe your exact software setup and add a link to your configuration files. (GitHub, GitLab, BitBucket, etc can host a public repository which you may update once in a while, but uploading them to pastebins is fine, too. **Don't** post the entire config file contents here.)