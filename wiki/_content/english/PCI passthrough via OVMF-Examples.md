As PCI passthrough is quite tricky to get right (both on the hardware and software configuration sides), this page presents **working, complete** VFIO setups. Feel free to look up users' scripts, BIOS/UEFI configuration, configuration files and specific hardware. If you have a problem, it might have been stumbled upon by other VFIO users and fixed in the examples below.

**Note:** If you've got VFIO working properly, please post your own setup according to the template on the bottom.

## Contents

*   [1 Users' setups](#Users.27_setups)
    *   [1.1 DragoonAethis: 6700K, GA-Z170X-UD3, GTX 1070](#DragoonAethis:_6700K.2C_GA-Z170X-UD3.2C_GTX_1070)
    *   [1.2 Manbearpig3130's Virtual Gaming Machine](#Manbearpig3130.27s_Virtual_Gaming_Machine)
    *   [1.3 Bretos' Virtual Gaming Setup](#Bretos.27_Virtual_Gaming_Setup)
    *   [1.4 Skeen's Virtual Gaming Rack Machine](#Skeen.27s_Virtual_Gaming_Rack_Machine)
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

*   **CPU**: Intel Core i7-6850K 3.6GHz
*   **Motherboard**: Gigabyte x99-Ultra Gaming (Revision 1.0, BIOS/UEFI Version: F4)
*   **Host GPU**: AMD Radeon HD6950 1GB
*   **Guest GPU**: AMD R9 390 8GB
*   **RAM**: 32GB G-Skill Ripjaws DDR4 runing at 3200MHz

Configuration:

*   **Host Kernel**: Kernel version Linux 4.7.2-1 (No ACS patch).
*   Using **libvirt QEMU/KVM with OVMF**: link to domain XMLs/scripts/notes: [https://github.com/manbearpig3130/MBP-VT-d-gaming-machine](https://github.com/manbearpig3130/MBP-VT-d-gaming-machine)
*   **Host OS**: Arch Linux
*   **Guest OS**: Windows 10 Pro
*   2x 480GB SSDs set up in LVM striped mode (with mdadm) formatted to ext4 are mounted in linux which contains the guest's qcow2 virtual VirtIO disk file.
*   USB Host controller is passed through, giving most USB ports to the VM, leaving my USB 3.1 controller with attached USB hub for the host.
*   Motherboard has two NICs, one is passed into VM (Works perfectly after installing Killer NIC Driver).
*   VM gets dedicated 16GB RAM via static hugepages.
*   CPU pinning increased performance considerably.
*   Windows boots straight into Steam big picture mode on primary display (43" Sony Bravia). Overall an awesome gaming machine that meets my gaming needs and lust for GNU/Linux at the same time.
*   **Quirks**:
*   I sometimes have to reinstall the AMD drivers in Windows to get HDMI audio working properly, or roll back to Windows HDMI driver.
*   I find that if I allow Windows to go through its shutdown procedure it has trouble booting again. To get around this I force off the machine in virtual machine manager gui.

### Bretos' Virtual Gaming Setup

Hardware:

*   **CPU**: Intel Core i7-7700k
*   **Motherboard**: Z270 GAMING M3 (MS-7A62)
*   **GPU**: ASUS GeForce GTX960
*   **RAM**: Kingston HyperX 3x8GB DDR4 2.4GHz
*   **Storage**: 2x Corsair MP500 m.2 240G SSDs in mdadm RAID0, 1x WD Black 1TB for storage. 100GB LVM volume as writeback cache for HDD

Configuration:

*   **Kernel**: vanilla
*   **Host OS**: Arch Linux
*   **Guest OS**: Windows 10 Pro
*   Using **libvirt/QEMU**: GitHub config repository: [[1]](https://github.com/Bretos/vfio)
*   Issues you've encountered: AUDIO. Had to get USB audio adapter and pass it through.
*   No issues other than audio. Works like a charm.

### Skeen's Virtual Gaming Rack Machine

Still work in progress.

Hardware:

*   **CPU**: AMD FX(tm)-8350
*   **Motherboard**: MSI 970A SLI Krait Edition (MS-7693) (Revision 5.0, BIOS/UEFI Version: 25.4)
*   **Host GPU**: ASUS GeForce GTX 480 1536MB
*   **Guest GPU**: ASUS GeForce GTX 480 1536MB
*   **RAM**: 2x8GB Kingston HyperX Fury White DDR3 1866MHz
*   **Storage**: 2x250GB Samsung EVO (MZ-75E250) set up in LVM striped mode (with mdadm), 2x1TB WD Blue (WDC_WD10SPCX) for storage. 250GB LVM volume as writeback cache for HDD.

Configuration:

*   **Host Kernel**: Linux 4.9.0-3 (No ACS)
*   **Host OS**: Debian Stretch
*   **Guest OS**: Windows 10 Home (10_1703_N, International Edition)
*   Using **libvirt QEMU/KVM with OVMF**: See [Github](https://github.com/Skeen/libvirt-gpu-passthrough)

Issues you've encountered:

*   Identifical GPUs; solved [using this section on the wiki](/index.php/PCI_passthrough_via_OVMF#Using_identical_guest_and_host_GPUs "PCI passthrough via OVMF"), but with the script from the [corresponding discussion page](/index.php/Talk:PCI_passthrough_via_OVMF#Using_identical_guest_and_host_GPUs_-_did_not_work_for_me. "Talk:PCI passthrough via OVMF"). Several adaptations for Debian were required too, but aren't applicable for this forum.
*   "Error 43: Driver failed to load";
    *   Spoofing vendor_id caused Windows to crash during boot-up.
    *   Linux VMs complain unable to find GPU from Grub2, and booted into blind-mode, but would still pick up the graphics card during the boot process, and would remain functional until VM reboot.
    *   Vendor_id spoofing turned out to work after solving the real problem (Missing UEFI compatability in VBIOS).
*   Missing UEFI (OVMF) compatability in VBIOS;
    *   Requested a GOP/UEFI compatible VBIOS upgrade from ASUS, but ASUS could neither understand the request, or provide the upgrade (The only thing supplied was standard support answers).
    *   No compatible VBIOS was found at [TechPowerUp](https://www.techpowerup.com/vgabios/).
    *   Finally solved by manually hacking GOP/UEFI support into the ROM, using [GOPupd](http://www.win-raid.com/t892f16-AMD-and-Nvidia-GOP-update-No-requests-DIY.html). Current rom was dumped within a Windows 10 VM using GPU-Z, then modified using GOPupd, pulled to Linux, and provided using the rom file parameter in the VM XML file.
*   VM only uses one core (even with mode=host-passthrough): solved [using this section on the wiki](/index.php/PCI_passthrough_via_OVMF#VM_only_uses_one_core "PCI passthrough via OVMF").

Quirks:

*   The GPU that is being passed through, [does not support resetting](/index.php/PCI_passthrough_via_OVMF#Passing_through_a_device_that_does_not_support_resetting "PCI passthrough via OVMF"), and thus doing a hard-reboot / shutdown of the VM locks the GPU.
    *   The VM cannot be started again unless the Host machine is rebooted.
        *   When doing a clean reboot / shutdown, allows the VM to start up as expected without reboot..
    *   Removing and rescanning the PCI device, does not change anything.
    *   No further attempts at powercycling the GPU from the host has been done (Yet).
*   [Passing VM audio to host via PulseAudio](/index.php/PCI_passthrough_via_OVMF#Passing_VM_audio_to_host_via_PulseAudio "PCI passthrough via OVMF") results in heavy crackling.
    *   Using [Message-Signaled Interrupts](/index.php/PCI_passthrough_via_OVMF#Slowed_down_audio_pumped_through_HDMI_on_the_video_card "PCI passthrough via OVMF") have not been attempted (Yet).

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