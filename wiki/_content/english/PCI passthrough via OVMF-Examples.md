As PCI passthrough is quite tricky to get right (both on the hardware and software configuration sides), this page presents **working, complete** VFIO setups. Feel free to look up users' scripts, BIOS/UEFI configuration, configuration files and specific hardware. If you have a problem, it might have been stumbled upon by other VFIO users and fixed in the examples below.

**Note:** If you have got VFIO working properly, please post your own setup according to the template on the bottom.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Users' setups](#Users'_setups)
    *   [1.1 mstrthealias: Intel 7800X / X299, GTX 1070](#mstrthealias:_Intel_7800X_/_X299,_GTX_1070)
    *   [1.2 DragoonAethis: 6700K, GA-Z170X-UD3, GTX 1070](#DragoonAethis:_6700K,_GA-Z170X-UD3,_GTX_1070)
    *   [1.3 Manbearpig3130's Virtual Gaming Machine](#Manbearpig3130's_Virtual_Gaming_Machine)
    *   [1.4 Bretos' Virtual Gaming Setup](#Bretos'_Virtual_Gaming_Setup)
    *   [1.5 Skeen's Virtual Gaming Rack Machine](#Skeen's_Virtual_Gaming_Rack_Machine)
    *   [1.6 droserasprout poor man's setup](#droserasprout_poor_man's_setup)
    *   [1.7 prauat: 2xIntel(R) Xeon(R) CPU E5-2609 v4, 2xGigabyte GeForce GTX 1060 6GB G1 Gaming, Intel S2600CWTR](#prauat:_2xIntel(R)_Xeon(R)_CPU_E5-2609_v4,_2xGigabyte_GeForce_GTX_1060_6GB_G1_Gaming,_Intel_S2600CWTR)
    *   [1.8 Dinkonin's virtual gaming/work setup](#Dinkonin's_virtual_gaming/work_setup)
    *   [1.9 pauledd's unexeptional setup](#pauledd's_unexeptional_setup)
    *   [1.10 hkk's Windows gaming machine (6700K, 1070, 16GB)](#hkk's_Windows_gaming_machine_(6700K,_1070,_16GB))
    *   [1.11 sitilge's treachery](#sitilge's_treachery)
    *   [1.12 chestm007's hackery](#chestm007's_hackery)
    *   [1.13 Eduxstad's Infidelity](#Eduxstad's_Infidelity)
    *   [1.14 Pi's vr-vm](#Pi's_vr-vm)
    *   [1.15 coghex's gaming box](#coghex's_gaming_box)
    *   [1.16 Roobre's VFIO setup](#Roobre's_VFIO_setup)
    *   [1.17 laenco's VFIO setup](#laenco's_VFIO_setup)
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
*   **Motherboard**: Gigabyte GA-Z170X-UD3 (Revision 1.0, BIOS/UEFI Version: F23d)
*   **GPU**: MSI GeForce 1070 Gaming X (10Gbps)
*   **RAM**: 16GB DDR4 2400MHz

Configuration:

*   **Kernel**: "Vanilla" Linux (no ACS patch needed).
*   Using **libvirt**: XML domain, helper scripts, IOMMU groups, etc available in [my VFIO repository](https://github.com/DragoonAethis/VFIO).
*   **Guest OS**: Windows 8.1 Pro.
*   The entire HDD is passed to the VM as a raw device (formatted as a single NTFS partition).
*   USB keyboard and mouse are passed to the guest VM and shared with the host with Synergy.
*   Virtualized audio: PulseAudio -> local Unix socket. Previously, I've had a bit more complex setup in which PA on the host was configured to accept TCP connections, and the envvars required for QEMU to use PA were pointed at the PA server running on 127.0.0.1\. This way it was not required to change the QEMU user (exact details in the repo), but introduced other minor issues I've resolved later.
*   Bridged networking (with NetworkManager's and [this tutorial's](https://www.happyassassin.net/2014/07/23/bridged-networking-for-libvirt-with-networkmanager-2014-fedora-21/) help) is used. `bridge0` is created, `eth0` interface is bound to it. STP disabled, VirtIO NIC is configured in the VM and that VM is seen in the network just as any other computer (and is being assigned an IP address from the router itself, can communicate freely with other computers).
*   For some reason, enabling intel_iommu=on on the kernel cmdline without CSM support enabled in UEFI causes a black screen on boot. Enable it (Windows 8/10 features need to be enabled to show "CSM Support", selecting "Other OS" hides that).

### Manbearpig3130's Virtual Gaming Machine

Hardware:

*   **CPU**: Intel Core i7-6850K 3.6GHz
*   **Motherboard**: Gigabyte x99-Ultra Gaming (Revision 1.0, BIOS/UEFI Version: F4)
*   **Host GPU**: AMD Radeon HD6950 1GB
*   **Guest GPU**: AMD R9 390 8GB
*   **RAM**: 32GB G-Skill Ripjaws DDR4 runing at 3200MHz

Configuration:

*   **Host Kernel**: Kernel version Linux 4.7.2-1.
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
*   I sometimes have to reinstall the AMD drivers in Windows to get HDMI audio working properly, or roll back to Windows HDMI driver. I normally use a USB headset which works fine anyway.

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
*   Synergy is not perfect and will not entirely work in some games.
*   No boot screen. Display is turning on only when Windows is up and ready to go.

### sitilge's treachery

Full info: [https://git.sitilge.id.lv/sitilge/dotfiles](https://git.sitilge.id.lv/sitilge/dotfiles)

Hardware:

*   **CPU**: Intel Core i5 6600K
*   **Motherboard**: Asus Z170i
*   **GPU**: Gigabyte Radeon RX460 OC 2GB
*   **Storage**: Samsung 850 EVO 500GB
*   **RAM**: Corsair 16GB DDR4
*   **Mouse, Keyboard**: Logitech M90, Vortex Pok3r

Host Configuration:

*   **Kernel**: linux-vfio
*   **Packages**: qemu-git, virtio-win, ovmf

Guest Configuration:

*   **OS**: Windows 10 Pro
*   **CPU**: host
*   **Motherboard**: host
*   **GPU**: passthrough
*   **Storage**: 64GB
*   **RAM**: 8GB
*   **Mouse, Keyboard**: passthrough

Notes:

*   You can easy simlink the config files using `stow -t / boot mkinitcpio` and then `mkinitcpio -p linux-vfio`.
*   `-smp cores=4` - guest might utilize only one core otherwise.
*   `-soundhw ac97` - I'm passing mobo audio thus ac97\. Download, unzip and install the Realtek AC97 drivers within a guest.
*   Use virtio drivers for both block devices and network. For example, the ping went down from 250 to 50.
*   Mouse and keyboard passthrough solved the terrible lag problem which was present in emulation mode.
*   Make sure virtualization is supported and enabled in your firmware (UEFI). The option was hidden in a submenu in my case.
*   As trivial as it sounds, check your cables.
*   Be patient - it took more than 10 minutes for the guest to recognize the GPU.

### chestm007's hackery

Hardware:

*   **CPU**: Ryzen 7 1800x
*   **Motherboard**: Asus ROG Crosshair VI (Revision 1, BIOS/UEFI Version: 3502)
*   **GPU**: Asus ROG RX480oc 8GB
*   **RAM**: 32gb Ripjaws 2400mhz

Configuration:

*   **Kernel**: 4.16.12-1-ARCH.
*   Using **libvirt/QEMU**: libvirtd (libvirt) 4.3.0, QEMU emulator version 2.12.0,

Notes:

*   using ic6 audio - works fine for me.
*   have a working looking-glass setup, however cant get spice to pass through keyboard and mouse, currently using a mixture of synergy and a dedicated screen as a workaround

### Eduxstad's Infidelity

Hardware:

*   **CPU**: Ryzen 2600X @ 3.7 GHZ
*   **Motherboard**: ASUS PRIME B350-PLUS(BIOS/UEFI Version: 4011)
*   **GPU1 (Guest)**: MSI 390 8GB @ Stock
*   **GPU2 (Host)**: XFX 550 4GB @ Stock
*   **RAM**: 2 x 8GB (16GB) @ 3000 HZ
*   **Guest OS**: Windows 8.1 Embedded Pro

Configuration:

*   **Kernel**: 4.17.3-1-ARCH (vanilla).
*   Using **libvirt/QEMU**: libvirt/virt-manager ([https://github.com/eduxstad/vfio-config](https://github.com/eduxstad/vfio-config)).
*   Look in the repository for complete documentation of extra steps taken
*   Overview: VM managed using virt-manager, using looking glass for primary io and built in spice display server as backup. Passing vm audio back to pulseaudio. Using hugepages for RAM. SCSI Drivers installed for hardware drive support.

### Pi's vr-vm

Hardware:

*   **CPU**: i7-8700k @ 4.8 GHz
*   **Motherboard**: MSI Gaming Pro Carbon (BIOS/UEFI Version: A.40/5.12)
*   **GPU**: Palit RTX 2080 Ti
*   **RAM**: 4x8GB G.Skill DDR4 @ 3000 MHz

Configuration:

*   Kernel: latest mainline (rc if available)
    *   custom built with ZFS, WireGuard
    *   *CONFIG_PREEMPT_VOLUNTARY=y* to work around QEMU bug with long guest boot times
*   Startup scripts/additional info: [https://github.com/PiMaker/Win10-VFIO](https://github.com/PiMaker/Win10-VFIO)
*   Issues encountered:
    *   PUBG would not launch at all
        *   Solution: Enable the HyperV clock with <timer name='hypervclock' present='yes'/> and disable hpet with <timer name='hpet' present='no'/>
    *   VR would start to stutter badly after about 20-30 minutes of playtime (this one took me about 2 weeks to finally figure out :-)
        *   Solution:
            *   Enable invariant tsc passthrough with <feature policy='require' name='invtsc'/> (required even if using host-passthrough!)
            *   Enable MSI for the GPU (using tool from [here](https://forums.guru3d.com/threads/windows-line-based-vs-message-signaled-based-interrupts-msi-tool.378044/))
            *   Enable vAPIC and synic in the HyperV configuration
            *   Manually move all IRQs to host cores using qemu_fifo.sh script from my GitHub repo above
*   Overview: SteamVR-capable gaming and workstation rig, passing through NVIDIA GPU and onboard USB-controller (leaving an additional ASMedia USB port to the host). 22 GB hugepages memory, 10 of 12 cores (with SMT) passed through. Audio working via Scream ([https://github.com/duncanthrax/scream](https://github.com/duncanthrax/scream)) - with IVSHMEM, surprisingly low latency and no stutters.

### coghex's gaming box

Hardware:

*   **CPU**: i7-8700k @ 4.8 GHZ
*   **Motherboard**: GIGABYTE Z370 AORUS Gaming 7 rev1.0 (BIOS/UEFI Version: F7)
*   **GPU1**: GIGABYTE GV-N108TAORUSX WB-11GD AORUS GeForce GTX 1080 Ti Waterforce WB Xtreme Edition 11G @ ~2Ghz
*   **GPU2**: ZOTAC GeForce GT 710 1G @ stock
*   **RAM**: 4 x 8GB (32GB) Corsair Dominator Platinum @ 3600 HZ (XMP)

Configuration:

*   **Kernel**: linux 4.17.6-2-vfio-ck
*   vfio aur mixed PKGBUILD with ck aur, the only ck patch that would not mix was the 8th gen quirks patch, so i left it out
*   options: intel_iommu=on iommu=pt rd.driver.pre=vfio-pci pcie_acs_override=downstream nowatchdog
*   im running the clock at 100Hz, the people running it at 1000 with the ck kernel should know that the MuQSS scheduler works the same regardless of this speed and 1000 will just add more useless interrupts.
*   Using **libvirt/QEMU**: [https://github.com/coghex/hoest](https://github.com/coghex/hoest)
*   There were no issues until i added a usb card to passthrough to the windows guest, now my kernel throws a usb-hid error or two sometimes when i boot.
*   The whole system runs off of two M2 nvme drives in software RAID0 with mdadm to try and make it as fast as possible, this works great in my linux host, rsync and dd taking no time at all, but in windows 10 these drives are not running at the same native speeds, they have the same fast sequential rw speeds, but the random read writes across the disk are much slower. for video games this meant long load times. i solved this by getting an 480G intel optane drive and passing it though to the VM. installing games on this drive makes the textures load faster, and removes QEMU overhead. I highly recommend.
*   the ACS patch is needed on this motherboard if you want to use two graphics cards at once in seperate IOMMU groups. GPU2 is for a chrome OS VM that I use as the system's browser.
*   none of the proprietary gigabyte software works, in fact, it blue screens my windows and installs itself as a startup program, forever locking me out. avoid at all costs, MSI Afterburner can control the overclocking, the LEDs, however, will stay in an RGB cycle.
*   if anyone else uses this exact motherboard, there are two internal USB IOMMU groups, even with the ACS patch. one will include the usb labeled "USB 3.1", and the other will include all the other USBs. this means if you want more than just a keyboard and mouse, you will need either a usb hub to plug into the 3.1 slot and passthrough, or a PCIE USB bus, i went with the latter. this works great with the oculus rift.
*   my CPU performance was enhanced most when i switched from linux-zen with CPU pinning to the custom kernel with 100Hz clock and installed irqbalance and ananicy. letting the MuQSS scheduler bounce around the virtual cpus as threads seems to increase my responsiveness drastically but decrease my overall performance slightly. this may be because i am running 4-5 VMs at once, i imagine on a machine designed to just run windows, CPU pinning would be unquestionably faster.
*   one last thing is the audio, i spent far too much time trying to figure out the stuttering choppy sound that i see around the web in relation to vfio. for me, the solution was using pulseaudio with pulseeffects from the aur. pulseeffects is an effects program that will handle the correct levels and create an audio buffer, mixing everything how i like. then, go into advance speaker properties in windows 10 and set the format to 44100Hz. this solved it for me

### Roobre's VFIO setup

Hardware:

*   **CPU**: Intel(R) Core(TM) i5-6600K CPU @ 3.50GHz (OC'ed to 4.50)
*   **Motherboard**: ASUS ROG MAXIMUS VIII GENE, v3801
*   **GPU**: EVGA GTX 1080Ti
*   **RAM**: 32GB DDR4 2400 (2x Ballistix)

Configuration:

*   **Kernel**: Latest -ARCH or -zen (4.17.10-1-zen at the time of writing)
*   Using **libvirt/QEMU**: libvirt 4.5.0-1, qemu 2.12.0-2\. Config: [https://gist.github.com/roobre/d2d20cc638c5030f360b500000da0f88](https://gist.github.com/roobre/d2d20cc638c5030f360b500000da0f88)
*   **ZFS** volumes passed as raw devices for hard drives.
*   **VirtIO all the things!** Download drivers from [https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/)

Issues:

*   Pulseaudio never worked good (too much crackling), so I ended up passing-through an USB 3.1 PCI controller and connecting an USB audio card to it. That card is then connected to one of my MoBo's inputs, and echoed using pulseaudio's `loopback` module.

*   Synergy works really great. On some games (ones who take control of the mouse pointer, e.g. first-person), you need to lock the mouse cursor to the VM window to avoid issues (camera moving too fast).

*   Do not forget to add the needed snippet for the nvidia driver to run ([PCI passthrough via OVMF#"Error 43: Driver failed to load" on Nvidia GPUs passed to Windows VMs](/index.php/PCI_passthrough_via_OVMF#"Error_43:_Driver_failed_to_load"_on_Nvidia_GPUs_passed_to_Windows_VMs "PCI passthrough via OVMF"))

### laenco's VFIO setup

Hardware:

*   **CPU**: Ryzen 9 3950X @ 4.15Ghz all-cores via PBO
*   **Motherboard**: Asus ROG STRIX X470-F GAMING (BIOS/UEFI Version: 5406)
*   **GPU1 (Guest)**: Palit GeForce GTX 1080 8GB @ Stock
*   **GPU2 (Host)**: MSI RX 570 8GB @ Stock
*   **RAM**: 4 x 16GB (64GB) @ 3333 MHz

Configuration:

*   **Guest OS**: Windows 10 Pro
*   **Kernel**: 5.4.13-arch1-1-gc (-ck is also good). No ACS patch.
*   Using vanilla **QEMU 4.2.0**
*   AMD Ryzen currently (2020.01.20) got bugged with smp threads option - VM stuck on start.
*   Got classic Nvidia error 43 - classically fixed. But also added some cpu flags which are set automatically with kvm=on found here [https://github.com/qemu/qemu/blob/master/target/i386/cpu.c#L4008](https://github.com/qemu/qemu/blob/master/target/i386/cpu.c#L4008)
*   As pure qemu have no option to pin cpu cores and self threads - using python script "cpu_affinity" - credits to [https://github.com/zegelin/qemu-affinity/](https://github.com/zegelin/qemu-affinity/) and also a copy in my repo. Requires debug-threads=on
*   Using dynamically allocated hugepages 2Mb
*   Hardly using VirtIO
*   Using hardware usb switch like Aten US224-AT and hdmi switch "many-to-one", which allow me to have one monitor, mouse, keyboard and some usb devices, and switch them by button between host and guest.
*   Repo with current major system config and script for VM could be found here [https://github.com/laenco/vfio-config](https://github.com/laenco/vfio-config)

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