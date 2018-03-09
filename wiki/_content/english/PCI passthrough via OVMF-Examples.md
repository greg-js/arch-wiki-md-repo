As PCI passthrough is quite tricky to get right (both on the hardware and software configuration sides), this page presents **working, complete** VFIO setups. Feel free to look up users' scripts, BIOS/UEFI configuration, configuration files and specific hardware. If you have a problem, it might have been stumbled upon by other VFIO users and fixed in the examples below.

**Note:** If you have got VFIO working properly, please post your own setup according to the template on the bottom.

## Contents

*   [1 Users' setups](#Users.27_setups)
    *   [1.1 mstrthealias: Intel 7800X / X299, GTX 1070](#mstrthealias:_Intel_7800X_.2F_X299.2C_GTX_1070)
    *   [1.2 DragoonAethis: 6700K, GA-Z170X-UD3, GTX 1070](#DragoonAethis:_6700K.2C_GA-Z170X-UD3.2C_GTX_1070)
    *   [1.3 Manbearpig3130's Virtual Gaming Machine](#Manbearpig3130.27s_Virtual_Gaming_Machine)
    *   [1.4 Bretos' Virtual Gaming Setup](#Bretos.27_Virtual_Gaming_Setup)
    *   [1.5 Skeen's Virtual Gaming Rack Machine](#Skeen.27s_Virtual_Gaming_Rack_Machine)
    *   [1.6 droserasprout poor man's setup](#droserasprout_poor_man.27s_setup)
    *   [1.7 prauat: 2xIntel(R) Xeon(R) CPU E5-2609 v4, 2xGigabyte GeForce GTX 1060 6GB G1 Gaming, Intel S2600CWTR](#prauat:_2xIntel.28R.29_Xeon.28R.29_CPU_E5-2609_v4.2C_2xGigabyte_GeForce_GTX_1060_6GB_G1_Gaming.2C_Intel_S2600CWTR)
    *   [1.8 Dinkonin's virtual gaming/work setup](#Dinkonin.27s_virtual_gaming.2Fwork_setup)
    *   [1.9 pauledd's unexeptional setup](#pauledd.27s_unexeptional_setup)
    *   [1.10 DragoonAethis: 6700K, GA-Z170X-UD3, GTX 1070](#DragoonAethis:_6700K.2C_GA-Z170X-UD3.2C_GTX_1070_2)
    *   [1.11 hkk's Windows gaming machine (6700K, 1070, 16GB)](#hkk.27s_Windows_gaming_machine_.286700K.2C_1070.2C_16GB.29)
*   [2 Adding your own setup](#Adding_your_own_setup)

## Users' setups

### mstrthealias: Intel 7800X / X299, GTX 1070

Hardware:

*   **CPU**: Intel(R) Core(TM) i7-7800X CPU
*   **Motherboard**: ASRock X299 Taichi (Revision: A, BIOS/UEFI Version: 1.60A)
*   **GPU**: Asus STRIX GTX 1070
*   **RAM**: 32GB DDR4

Configuration:

*   **Kernel**: Kernel version 4.14.8-1-skx (patched crystal_khz=24000).
    *   Custom patches:
        *   skylakex-crystal_khz-24000.patch (see below)
    *   Patches used from linux-ck:
        *   enable_additional_cpu_optimizations_for_gcc_v4.9+_kernel_v4.13+.patch
        *   0001-add-sysctl-to-disallow-unprivileged-CLONE_NEWUSER-by.patch
        *   0001-e1000e-Fix-e1000_check_for_copper_link_ich8lan-retur.patch
        *   0002-dccp-CVE-2017-8824-use-after-free-in-DCCP-code.patch
    *   Config:
        *   PREEMPT, NO_HZ_IDLE, 300HZ, MSKYLAKE
*   GitHub: Link TBD
*   Benchmarks: [https://imgur.com/a/hIfQD](https://imgur.com/a/hIfQD)
*   Using **libvirt/QEMU**: libvirt 3.10.0 / QEMU 2.11.0
*   Issues you have encountered, special steps taken to make something work a bit better, etc.
    *   Skylake-X default clock incorrect in 4.14.8 ([https://bugzilla.kernel.org/show_bug.cgi?id=197299](https://bugzilla.kernel.org/show_bug.cgi?id=197299))
        *   Was unable to resolve timing issue using adjtimex
        *   Patching kernel source to **crystal_khz = 24000** resolved timing/performance issues
    *   Enable 'Intel SpeedShift' in BIOS, installed **cpupower'**, set governor='performance'
        *   Verify: dmesg|grep HWP
            *   intel_pstate: HWP enabled
    *   Enable HT in BIOS
    *   Enable 'deadline' IO sceduler:
        *   echo 'ACTION=="add|change", KERNEL=="sd*[!0-9]|sr*", ATTR{queue/scheduler}="deadline"' >> /etc/udev/rules.d/60-schedulers.rules
    *   Bypass x2apic opt-out:
        *   GRUB_CMDLINE_LINUX="... intremap=no_x2apic_optout ..."
    *   Isolate cores for Windows VM:
        *   GRUB_CMDLINE_LINUX="... isolcpus=2-5,8-11 nohz_full=2-5,8-11 rcu_nocbs=2-5,8-11 ..."
    *   Use hugepages (2MB) for all VM memory allocation
    *   memoryBacking: <hugepages/><nosharepages/><locked/><access mode='private'/><allocation mode='immediate'/>
    *   Extracted rom from GPU; used for <rom file=../> config
    *   Using MSI for GPU and GPU Audio (configured in Windows registry; FPS seems same as using line-based interrupts)
*   Hardware setup
    *   PCIE1: NVIDIA GeForce GT 710B (for host)
    *   Onboard: ASRock XHCI 3.1 USB (for host)
    *   Onboard: Intel I219 NIC (bridged)
    *   PCIE3: Asus Xonar STX (passthrough to Win10)
    *   PCIE5: NVIDIA GeForce GTX 1070 (passthrough to Win10)
    *   M2_1: Samsung 960 EVO 500GB (passthrough to Win10)
    *   Onboard: Intel XHCI USB 3.0 (passthrough to Win10)
    *   Onboard: Intel HDA (passthrough to Win10)
    *   Onboard: Intel I211 NIC (passthrough to Win10)
    *   Onboard: ASRock AHCI SATA A1/A2 (passthrough to Linux)

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
*   USB keyboard and mouse are passed to the guest VM and shared with the host with Synergy.
*   Virtualized audio is working: PulseAudio on the host is configured to accept TCP connections, and the envvars required for QEMU to use PA are pointed at the PA server running on 127.0.0.1\. This way it's not required to change the QEMU user, everything works flawlessly. (Exact details in the repo.)
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
*   Issues you have encountered: AUDIO. Had to get USB audio adapter and pass it through.
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

Issues you have encountered:

*   Identifical GPUs; solved [using this section on the wiki](/index.php/PCI_passthrough_via_OVMF#Using_identical_guest_and_host_GPUs "PCI passthrough via OVMF"), but with the script from the [corresponding discussion page](/index.php/Talk:PCI_passthrough_via_OVMF#Using_identical_guest_and_host_GPUs_-_did_not_work_for_me. "Talk:PCI passthrough via OVMF"). Several adaptations for Debian were required too, but are not applicable for this forum.
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

### droserasprout poor man's setup

Hardware:

*   **CPU**: Intel Core i3-6100
*   **Motherboard**: ASRock H110M2 D3 (BIOS version 0603)
*   **Host GPU**: Intel HD 530
*   **Guest GPU**: Sapphire Radeon R7 360
*   **RAM**: Apacer 8Gb 75.C93DE.G040C, Kingston 4Gb 99U5401-011.A00LF

Configuration:

*   **Kernel**: linux-lts 4.9.67-1 (vanilla)
*   **Host OS**: Arch Linux
*   **Guest OS**: Windows 10 Pro 1709 (build 16299.98)
*   Using **libvirt/QEMU**: See my configs and IOMMU groups on [Github](https://github.com/droserasprout/win10-vfio-configs)
*   HDD partition is passed to the VM as a raw virtio device.
*   HD Audio is passed too. Works fine with both playing and recording, no latency issues or glitches. After VM is powered off host audio works fine too.
*   Guest's latency is slightly better when CPU cores are isolated for VM.
*   i2c-dev module added to bypass 'EDID signature' error when switching HDMI. Without it I had to switch video output before starting VM for some reason.
*   intremap=no_x2apic_optout kernel option added to bypass motherboard firmware falsely reporting x2APIC method is not supported. Seems to have a strong influence on the guest's latency.
*   Overall performance is pretty close to the native OS setup.

### prauat: 2xIntel(R) Xeon(R) CPU E5-2609 v4, 2xGigabyte GeForce GTX 1060 6GB G1 Gaming, Intel S2600CWTR

Hardware:

*   **CPU**:2xIntel(R) Xeon(R) CPU E5-2609 v4
*   **Motherboard**: Intel S2600CWTR(Revision ???, BIOS/UEFI Version: SE5C610.86B.01.01.0022.062820171903)
*   **GPU**: 2xGigabyte GeForce GTX 1060 6GB G1 Gaming [GeForce GTX 1060 6GB] (rev a1)
*   **RAM**: Samsung M393A2G40EB1-CPB 2133 MHz 64GB (4x16GB)

Configuration:

*   **Kernel**: Linux 4.14.15-1-ARCH #1 SMP PREEMPT
*   Using **libvirt/QEMU**: [https://github.com/prauat/passvm/blob/master/generic.xml](https://github.com/prauat/passvm/blob/master/generic.xml)
*   Most important:
*   When using nvidia driver hide virtualization to guest <kvm><hidden state='on'/></kvm>
*   Configuration works with Arch Linux guest os, still work in progress.

### Dinkonin's virtual gaming/work setup

Hardware:

*   **CPU**: Intel(R) Core(TM) i7-7700K CPU @ 4.60GHz
*   **Motherboard**: MSI Z270 GAMING PRO CARBON (MS-7A63) BIOS Version: 1.80
*   **GPU**: 1x Gigabyte GeForce GTX 1050 2GB (host), 1x MSI GeForce 1080 AERO 8GB(guest)
*   **RAM**: 32GB DDR4

Configuration:

*   **Kernel**: Kernel version linux 4.15.2-2-ARCH.
*   Using **libvirt/QEMU (patched from AUR) with OVMF**
*   Installed qemu-patched from AUR because of crackling/delayed sound with pulseaduio (still hear ocasional pops/clicks while gaming.
*   Patched video bios with [https://github.com/Matoking/NVIDIA-vBIOS-VFIO-Patcher](https://github.com/Matoking/NVIDIA-vBIOS-VFIO-Patcher), because of error:

```
vfio-pci 0000:01:00.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xffff

```

*   Single monitor setup, implemented full software KVM(for host and guest) described here: [https://rokups.github.io/#!pages/full-software-kvm-switch.md](https://rokups.github.io/#!pages/full-software-kvm-switch.md)

### pauledd's unexeptional setup

Hardware:

*   **CPU**: Intel Core i7 6700K
*   **Motherboard**: Gigabyte GA-Z170N-WIFI Retail (Revision 1.0 , BIOS/UEFI Version: F20)
*   **GPU**: 8GB Palit GeForce GTX 1070 Dual Aktiv PCIe 3.0 x16 (Retail)
*   **RAM**: 16GB G.Skill RipJaws V DDR4-3200 DIMM CL16 Dual Kit

Configuration:

*   **Kernel**: 4.15.2-gentoo
*   Using **libvirt/QEMU**: libvirt-4.0.0, qemu-2.11.1, [https://github.com/pauledd/GPU-Passthrough/blob/master/win10-2.xml](https://github.com/pauledd/GPU-Passthrough/blob/master/win10-2.xml) , using vfio kernel module
*   Had to dump VBIOS in at the host while GPU was normally attached (and drivers loaded) (see [https://stackoverflow.com/a/42441234](https://stackoverflow.com/a/42441234)), had to set CPU settings manually according to my cpu (host-passthrough, sockets 1, cores: 4, threads: 2 ) or some games will regularly crash, see my xml how to insert vbios, still have audio clicking/lag with pulseaudio but thats ok for me, no further patching etc.. works out of the box without any issues.
*   3DMark Results Time Spy Graphic Score: Native Windows 10: 5564 , GPU-Passthrough: 5541

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
*   USB keyboard and mouse are passed to the guest VM and shared with the host with Synergy.
*   Virtualized audio is working: PulseAudio on the host is configured to accept TCP connections, and the envvars required for QEMU to use PA are pointed at the PA server running on 127.0.0.1\. This way it's not required to change the QEMU user, everything works flawlessly. (Exact details in the repo.)
*   Bridged networking (with NetworkManager's and [this tutorial's](https://www.happyassassin.net/2014/07/23/bridged-networking-for-libvirt-with-networkmanager-2014-fedora-21/) help) is used. `bridge0` is created, `eth0` interface is bound to it. STP disabled, VirtIO NIC is configured in the VM and that VM is seen in the network just as any other computer (and is being assigned an IP address from the router itself, can communicate freely with other computers).

### hkk's Windows gaming machine (6700K, 1070, 16GB)

Hardware:

*   **CPU**: Intel Core i7-6700K 4.5GHz
*   **Motherboard**: AsRock Fatality Gaming K6 Z170 (rev. 1.05)
*   **Host GPU**: Intel GPU HD530 with 1GB shared memory
*   **Guest GPU**: Gigabyte GeForce GTX1070 G1 Gaming 8GB
*   **RAM**: 16GB G.Skill RipjawsV @ 3333 MHz CL14-15-15-31-2T [DDR4]

Configuration:

*   **Host Kernel**: Kernel version Linux 4.15.7-1-vfio (with ACS patch included).
*   Using **libvirt QEMU/KVM with OVMF**
*   **Host OS**: Arch Linux
*   **Guest OS**: Windows 10 Pro
*   128GB Intel 600p SSD splited into 3 partitions: 512MB for EFI, 30GB for / in Btrfs and other gigs for Windows 10 installed straight on SSD.
*   Two more HDDs for Windows. 1TB and 650GB
*   Passed specific devices like X360 and some of single USB ports.
*   One NIC behind NAT on VM machine.
*   VM gets dedicated 8GB RAM via static hugepages.
*   CPU pinning increased performance considerably and machine gets 4/4 cores of my 4/8 CPU
*   Windows boots on second screen with simple script which shutting down display with xrandr.
*   Using Synergy to share mouse and keyboard between systems.
*   **Quirks**:
*   Synergy isn't perfect and won't entirely work in some games.
*   No boot screen. Display is turning on only when Windows is up and ready to go.

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
* Issues you have encountered, special steps taken to make something work a bit better, etc.
* Describe your setup loosely here, so that when other wiki users are looking for something, they can easily skim through available setups.

```

Replace proper sections with your own data. Make sure to provide the exact motherboard model, revision (if possible - should be on both the motherboard itself and the box it came in) and BIOS/UEFI version you are using. Describe your exact software setup and add a link to your configuration files. (GitHub, GitLab, BitBucket, etc can host a public repository which you may update once in a while, but uploading them to pastebins is fine, too. **Do not** post the entire config file contents here.)