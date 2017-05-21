As PCI passthrough is quite tricky to get right (both on the hardware and software configuration sides), this page presents **working, complete** VFIO setups. Feel free to look up users' scripts, BIOS/UEFI configuration, configuration files and specific hardware. If you have a problem, it might have been stumbled upon by other VFIO users and fixed in the examples below.

**Note:** If you've got VFIO working properly, please post your own setup according to the template on the bottom.

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