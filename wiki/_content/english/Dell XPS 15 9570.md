**Note:** This page far from completed. Some not mentioned items could be same as [XPS 15 9560](/index.php/XPS_15_9560 "XPS 15 9560"). Most of it also applies to the Precision 5530

| **Device/Functionality** | **Status** |
| [Suspend](#Suspend) | Working |
| [Hibernate](#Hibernate) | Working |
| [Integrated Graphics](#Graphics) | Working |
| [Discrete Nvidia Graphics](#Graphics) | Modify |
| [Wifi](#Wifi_and_Bluetooth) | Working |
| [Bluetooth](#Wifi_and_Bluetooth) | Working |
| [rfkill](#Wifi_and_Bluetooth) | Working |
| Audio | Working |
| [Touchpad](#Touchpad_and_Touchscreen) | Working |
| [Touchscreen](#Touchpad_and_Touchscreen) | Working |
| Webcam | Working |
| Card Reader | Working |
| Function/Multimedia Keys | Working |
| [Power Management](#Power_Management) | Working |
| [EFI firmware updates](#EFI_firmware_updates) | Working |
| [Fingerprint reader](#Fingerprint_reader) | Not working |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 UEFI](#UEFI)
*   [2 Power Management](#Power_Management)
    *   [2.1 Suspend](#Suspend)
    *   [2.2 Hibernate](#Hibernate)
    *   [2.3 Powertop](#Powertop)
*   [3 Graphics](#Graphics)
    *   [3.1 kernel modules](#kernel_modules)
    *   [3.2 NVIDIA Optimus](#NVIDIA_Optimus)
    *   [3.3 Troubleshooting](#Troubleshooting)
        *   [3.3.1 xbacklight](#xbacklight)
        *   [3.3.2 NVRM: Failed to enable MSI; falling back to PCIe virtual-wire interrupts](#NVRM:_Failed_to_enable_MSI;_falling_back_to_PCIe_virtual-wire_interrupts)
        *   [3.3.3 Built-in screen flickers or does not come on with Linux kernel 5.0.0 - 5.0.7](#Built-in_screen_flickers_or_does_not_come_on_with_Linux_kernel_5.0.0_-_5.0.7)
        *   [3.3.4 Lock-ups when resuming from suspend with nvidia module](#Lock-ups_when_resuming_from_suspend_with_nvidia_module)
*   [4 Wifi and Bluetooth](#Wifi_and_Bluetooth)
    *   [4.1 Troubleshooting](#Troubleshooting_2)
        *   [4.1.1 ath10k module crashes after suspend](#ath10k_module_crashes_after_suspend)
        *   [4.1.2 Bluetooth disappears (after suspend?)](#Bluetooth_disappears_(after_suspend?))
*   [5 Touchpad and Touchscreen](#Touchpad_and_Touchscreen)
*   [6 Thunderbolt docks](#Thunderbolt_docks)
    *   [6.1 TB16](#TB16)
*   [7 EFI firmware updates](#EFI_firmware_updates)
    *   [7.1 Fwupd](#Fwupd)
    *   [7.2 UEFI](#UEFI_2)
*   [8 Thermal management](#Thermal_management)
    *   [8.1 Diagnosis](#Diagnosis)
    *   [8.2 Undervolting](#Undervolting)
    *   [8.3 Repasting & padding](#Repasting_&_padding)
    *   [8.4 Results](#Results)
*   [9 Tips and Tricks](#Tips_and_Tricks)
    *   [9.1 Systemd doesn't wait for Network](#Systemd_doesn't_wait_for_Network)

## UEFI

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

*   Change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD. If dual booting with an existing Windows installation, Windows will not boot after the change but [this can be fixed without a reinstallation](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/).
*   Change Fastboot to "Thorough" in "POST Behaviour". This prevents intermittent boot failures.
*   Disable secure boot to allow Linux to boot.

Installation of Arch Linux can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more information.

## Power Management

### Suspend

By default, the very inefficient s2idle suspend variant is incorrectly selected. This is probably due to the BIOS. The much more efficient deep variant should be selected instead:

```
 $ cat /sys/power/mem_sleep 
 [s2idle] deep
 $ echo deep|sudo tee /sys/power/mem_sleep
 $ cat /sys/power/mem_sleep 
 s2idle [deep]

```

To make the change permanent add `mem_sleep_default=deep` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

An easy way would be to add `mem_sleep_default=deep` to the `GRUB_CMDLINE_LINUX_DEFAULT` entry in /etc/default/grub:

```
 GRUB_CMDLINE_LINUX_DEFAULT="mem_sleep_default=deep"

```

Read more regarding the sleep variants on the kernel documentation [[1]](https://www.kernel.org/doc/html/v4.18/admin-guide/pm/sleep-states.html).

**Warning:** Some users have reported a problem where the CPUs get stuck in a high power state after resuming from S3 (deep) suspension [[2]](https://www.reddit.com/r/Dell/comments/91313h/xps_15_9570_c_state_bug_after_s3_sleep_and_modern/).

### Hibernate

Works out of the Box see [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate")

### Powertop

`powertop` is very efficient to manage power consumption. Run `powertop --auto-tune` and compare the Watt consumption variation (battery must be unplugged). `powertop --auto-tune` can be run at every boot.

## Graphics

### kernel modules

The nouveau module is known to cause kernel panics and freezes on Dell XPS 15 9570.

One way to mitigate this would be by adding `nomodeset` to the kernel options. However it's better to completely disable it with the blacklist method (recommended):

 `/etc/modprobe.d/blacklist.conf` 
```
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
blacklist nv
```

### [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus")

The optimus configuration is a technology that allows an Intel integrated GPU and discrete NVIDIA GPU to be built into and accessed by a laptop. As the discret NVIDIA GPU card eats lots of power, we want to use the intergrated Intel card most of the time and activate/desactivate the NVIDIA GPU card only when required by a defined application. Due to a bug [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1794626#p1794626), the XPS 15 9570's secondary NVIDIA GPU cannot be powered down by [bbswitch](/index.php/Bbswitch "Bbswitch"). However, standard Linux power management is able to properly turn off the card when the driver is unloaded.

One solution [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1826641#p1826641) to this problem is to manually unload the NVIDIA module when not in use, which can be done as follows:

[Install](/index.php/Install "Install")

*   [nvidia](https://www.archlinux.org/packages/?name=nvidia) - Official NVIDIA drivers for Linux.
*   [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) - The main package providing the daemon and client programs.
*   [powertop](https://www.archlinux.org/packages/?name=powertop) - Tool to verify power consumption.
*   [unigine-valley](https://aur.archlinux.org/packages/unigine-valley/) - Graphic intensive application for testing

Make sure that [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) is uninstalled or at least disabled

`bumblebee` configuration, in the `[driver-nvidia]` section

 `/etc/bumblebee/bumblebee.conf` 
```
# *[driver-nvidia]* section
Driver=nvidia
PMMethod=none
```

Server X configuration for not auto adding gpu

 `/etc/X11/xorg.conf.d/01-noautogpu.conf` 
```
Section "ServerFlags"
	Option "AutoAddGPU" "off"
EndSection
```

`ipmi` modules are loaded together with `nvidia` and block its unloading. Create the two following files to disable them:

 `/etc/modprobe.d/disable-ipmi.conf` 
```
  install ipmi_msghandler /usr/bin/false
  install ipmi_devintf /usr/bin/false
```
 `/etc/modprobe.d/disable-nvidia.conf`  `install nvidia /bin/false` 

Now, add `nvidia` and `ipmi` in the modprobe.d blacklist to disable this functionality:

 `/etc/modprobe.d/blacklist.conf` 
```
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
blacklist nv
blacklist nvidia
blacklist nvidia-drm
blacklist nvidia-modeset
blacklist nvidia-uvm
blacklist ipmi_msghandler
blacklist ipmi_devintf
```

Create 2 GPU management scripts for enabling and disabling discret NVIDIA graphical card [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1826641#p1826641):

 `enablegpu.sh` 
```
#!/bin/sh
# allow to load nvidia module
mv /etc/modprobe.d/disable-nvidia.conf /etc/modprobe.d/disable-nvidia.conf.disable

# Remove NVIDIA card (currently in power/control = auto)
echo -n 1 > /sys/bus/pci/devices/0000\:01\:00.0/remove
sleep 1
# change PCIe power control
echo -n on > /sys/bus/pci/devices/0000\:00\:01.0/power/control
sleep 1
# rescan for NVIDIA card (defaults to power/control = on)
echo -n 1 > /sys/bus/pci/rescan
# someone said that modprobe nvidia is needed also to load nvidia, to check
# modprobe nvidia
```
 `disablegpu.sh` 
```
#!/bin/sh

modprobe -r nvidia_drm
modprobe -r nvidia_uvm
modprobe -r nvidia_modeset
modprobe -r nvidia

# Change NVIDIA card power control
echo -n auto > /sys/bus/pci/devices/0000\:01\:00.0/power/control
sleep 1
# change PCIe power control
echo -n auto > /sys/bus/pci/devices/0000\:00\:01.0/power/control
sleep 1

# Lock system form loading nvidia module
mv /etc/modprobe.d/disable-nvidia.conf.disable /etc/modprobe.d/disable-nvidia.conf
```

Create service locking NVIDIA GPU on shutdown A service which locks GPU on shutdown / restart when it is not disabled by `disablegpu.sh` script is necessary. Otherwise, on next boot `nvidia` will be loaded together with `ipmi` modules (even if blacklisted with `install` command) and it won't be possible to unload them then.

 `/etc/systemd/system/disable-nvidia-on-shutdown.service` 
```
[Unit]
Description=Disables Nvidia GPU on OS shutdown

[Service]
Type=oneshot
RemainAfterExit=true
ExecStart=/bin/true
ExecStop=/bin/bash -c "mv /etc/modprobe.d/disable-nvidia.conf.disable /etc/modprobe.d/disable-nvidia.conf || true"

[Install]
WantedBy=multi-user.target
```

Reload systemd daemons and enable the `disable-nvidia-on-shutdown` service:

```
 sudo systemctl daemon-reload
 sudo systemctl enable disable-nvidia-on-shutdown.service

```

Allow gpu to poweroff on boot

 `/etc/tmpfiles.d/nvidia_pm.conf`  `w /sys/bus/pci/devices/0000:01:00.0/power/control - - - - auto` 

Finally, check that everything is well configured:

1.  Reboot and verify that nvidia is not loaded by running:

    	 `lsmod | grep nvidia` 

    	Should not return anything

2.  Disconnect / unplug charger and verify the power consumption with powertop is around 5W on idle (Dell XPS 15 4570, powertop --auto-tune previously launched, FHD screen with no touchscreen)
3.  Enable GPU by using the enablegpu.sh script
4.  Check that the GPU is loaded by using:

    	 `nvidia-smi` 

5.  If good, launch unigine-valley with optirun:

    	 `optirun unigine-valley` 

    	unigine-valley needs a GPU to work. Should activate the fans quickly.

6.  Close all nvidia applications and disable gpu with the disablegpu.sh script
7.  Check again power consumption, it should have gone back to a similar value as before

### Troubleshooting

#### xbacklight

To get xbacklight working and not conflicting with NVIDIA optimus:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
	Identifier  "Intel Graphics"
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
EndSection

```

#### NVRM: Failed to enable MSI; falling back to PCIe virtual-wire interrupts

Sometimes it happens after suspend/resume. GPU could work fine without MSI. [[6]](http://us.download.nvidia.com/XFree86/Linux-x86/325.15/README/knownissues.html#msi_interrupts). You could disable MSI by adding the following in **/etc/modprobe.d/nvidia.conf**:

```
 options nvidia NVreg_EnableMSI=0

```

#### Built-in screen flickers or does not come on with Linux kernel 5.0.0 - 5.0.7

Some users reported that running Linux kernel 5.0.0 to 5.0.7 can cause the screen to flicker (or stay completely black) when booting up or running an X server, making the built-in display unusable (see *[[7]](https://bugs.archlinux.org/task/61964))

Currently, it seems that there are three possible workarounds :

*   [Downgrade](/index.php/Downgrade "Downgrade") to Linux 4.20.13.
*   Apply [Albert Astals Cid's patch](https://invent.kde.org/snippets/44) on Linux kernel 5.0.x (see [kernel Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")).
*   Install [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)
*   upgrade to Linux 5.0.8 or higher

#### Lock-ups when resuming from suspend with nvidia module

If your system locks up every time you resume from suspend with the following two lines in dmesg:

```
   [   42.447364] pci 0000:01:00.0: Refused to change power state, currently in D3
   [   46.896493] pci 0000:01:00.0: Refused to change power state, currently in D3

```

you need to do the following:

Into /etc/default/grub

```
   GRUB_CMDLINE_LINUX="nouveau.blacklist=0 acpi_osi=! acpi_osi=\"Windows 2015\" acpi_backlight=vendor mem_sleep_default=deep"

```

This solved the lock-ups for me. (internal nvidia bug number: 2589324, [dell resolution](https://www.dell.com/community/XPS/XPS-15-9570-with-Ubuntu-18-04-1-not-resuming-after-suspend/m-p/7305094#M28897))

## Wifi and Bluetooth

These work well out of the box but you might need to update the firmware for better stability. For bluetooth, make sure you have everything installed as per the [Bluetooth](/index.php/Bluetooth "Bluetooth") wiki page.

```
 $ lspci | grep Network
 3b:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

(please add a line here if you detect something different)

### Troubleshooting

#### ath10k module crashes after suspend

You may notice driver crashes after suspend/resume, which for the most part does not seem to impact the running system, with coredumps similar to:

```
kernel: WARNING: CPU: 6 PID: 27936 at drivers/net/wireless/ath/ath10k/mac.c:5746 ath10k_bss_info_changed+0xf96/0x1120 [ath10k_core]
kernel: Modules linked in: uhid algif_hash cmac rfcomm fuse ccm ipt_MASQUERADE nf_conntrack_netlink nfnetlink xfrm_user xfrm_algo iptable_nat nf_nat_ipv4>
kernel:  snd_hda_intel dcdbas x86_pkg_temp_thermal dell_smm_hwmon snd_hda_codec intel_powerclamp cfg80211 kvm_intel snd_hda_core input_leds snd_hwdep snd>
kernel:  vfio_mdev mdev vfio_iommu_type1 vfio kvm irqbypass intel_gtt i2c_algo_bit drm_kms_helper syscopyarea sysfillrect sysimgblt fb_sys_fops drm agpga>
kernel: CPU: 6 PID: 27936 Comm: kworker/u24:42 Tainted: G     U  W  OE     5.0.4-arch1-1-ARCH #1
kernel: Hardware name: Dell Inc. XPS 15 9570/0HWTMH, BIOS 1.8.1 02/01/2019
kernel: Workqueue: events_unbound async_run_entry_fn
kernel: RIP: 0010:ath10k_bss_info_changed+0xf96/0x1120 [ath10k_core]
kernel: Code: 24 8b 95 78 01 00 00 85 c0 0f 85 a7 00 00 00 89 d1 be 10 00 00 00 48 c7 c2 c0 b2 fa c0 4c 89 c7 e8 bf 68 00 00 e9 a5 f1 ff ff <0f> 0b 4c 89>
kernel: RSP: 0000:ffffb7a45422fcd0 EFLAGS: 00010282
kernel: RAX: 00000000fffffffe RBX: ffff98f6d44815a0 RCX: 0000000000000000
kernel: RDX: ffff98f6d4481938 RSI: ffffb7a45422fcf0 RDI: ffff98f6d81df418
kernel: RBP: ffff98f6d81df418 R08: 0000000000000001 R09: 0000000000000000
kernel: R10: 000000000000001f R11: 0000000000000000 R12: 0000000000000020
kernel: R13: ffff98f6d81df420 R14: ffff98f6d4482598 R15: ffff98f6d44815a0
kernel: FS:  0000000000000000(0000) GS:ffff98f6dc380000(0000) knlGS:0000000000000000
179 94%
kernel:  process_one_work+0x1eb/0x410
kernel:  worker_thread+0x2d/0x3d0
kernel:  ? process_one_work+0x410/0x410
kernel:  kthread+0x112/0x130
kernel:  ? kthread_park+0x80/0x80
kernel:  ret_from_fork+0x35/0x40
kernel: ---[ end trace 09ae3e174c178f98 ]---

```

Patched in some kernels and not others (which?), relevant links:

*   [BBS: Suspend issue with Dell XPS 9570](https://bbs.archlinux.org/viewtopic.php?pid=1824143) (related)
*   [buzbilla#201499: ath10k BUG on resume](https://bugzilla.kernel.org/show_bug.cgi?id=201499)

#### Bluetooth disappears (after suspend?)

Possibly related to the previous instability issue, sometimes the adapter seems to completely disappear. As reported [here](https://www.dell.com/community/XPS/XPS-15-9570-Bluetooth-disappearing/td-p/6192457) (thanks [w.v.w.](https://www.dell.com/community/user/viewprofilepage/user-id/3517956), you can likely fix this by manually upgrading the firmware (to something newer than what's in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware):

1\. Double check adapter (e.g. QCA6174, below)

```
 $ lspci | grep Network
 3b:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

2\. Confirm hardware and current firmware version (e.g. hw3.2, firmware RM.4.4.1.c3-00013-QCARMSWPZ-1, below)

```
 $ journalctl -b | grep ath10k | egrep 'firmware|qca'
 kernel: ath10k_pci 0000:3b:00.0: qca6174 hw3.2 target 0x05030000 chip_id 0x00340aff sub 1a56:1535
 kernel: ath10k_pci 0000:3b:00.0: firmware ver RM.4.4.1.c3-00013-QCARMSWPZ-1 api 6 features wowlan,ignore-otp,no-4addr-pad,raw-mode,mfp crc32 fc0096a8

```

3\. Follow the instructions at [https://wireless.wiki.kernel.org/en/users/Drivers/ath10k/firmware](https://wireless.wiki.kernel.org/en/users/Drivers/ath10k/firmware)

e.g. for the above adapter, download the latest firmware from [https://github.com/kvalo/ath10k-firmware/tree/master/QCA6174/hw3.0](https://github.com/kvalo/ath10k-firmware/tree/master/QCA6174/hw3.0) and

```
 $ cd /lib/firmware/ath10k/QCA6174/hw3.0
 $ sudo cp firmware-6.bin firmware-6.bin.bak
 $ sudo cp ~/Downloads/firmware-6.bin_RM.4.4.1.c3-00013-QCARMSWPZ-1 firmware-6.bin

```

Either `sudo rmmod ath10k_core ath10k_pci && sudo modprobe ath10k_pci` (may not work, check dmesg) or reboot.

## Touchpad and Touchscreen

Wacom touchscreen and Synaptics touchpad:

 `$ xinput` 
```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ SYNA2393:00 06CB:7A13 Touchpad            id=16   [slave  pointer  (2)]
⎜   ↳ Wacom HID 488F Finger                     id=15   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
[truncated]
```

Both are i2c devices:

 `$ udevadm info /dev/input/mouse3 # touchscreen` 
```
P: /devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-10/i2c-WCOM488F:00/0018:056A:488F.0006/input/input47/mouse3
N: input/mouse3
L: 0
E: DEVPATH=/devices/pci0000:00/0000:00:15.0/i2c_designware.0/i2c-10/i2c-WCOM488F:00/0018:056A:488F.0006/input/input47/mouse3
E: DEVNAME=/dev/input/mouse3
E: MAJOR=13
E: MINOR=35
E: SUBSYSTEM=input
E: USEC_INITIALIZED=5501073
E: ID_INPUT=1
E: ID_INPUT_TOUCHSCREEN=1
E: ID_PATH=pci-0000:00:15.0-platform-i2c_designware.0
E: ID_PATH_TAG=pci-0000_00_15_0-platform-i2c_designware_0
```
 `$ udevadm info /dev/input/mouse6 # touchpad` 
```
P: /devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-11/i2c-SYNA2393:00/0018:06CB:7A13.0007/input/input38/mouse6
N: input/mouse6
L: 0
S: input/by-path/pci-0000:00:15.1-platform-i2c_designware.1-mouse
E: DEVPATH=/devices/pci0000:00/0000:00:15.1/i2c_designware.1/i2c-11/i2c-SYNA2393:00/0018:06CB:7A13.0007/input/input38/mouse6
E: DEVNAME=/dev/input/mouse6
E: MAJOR=13
E: MINOR=38
E: SUBSYSTEM=input
E: USEC_INITIALIZED=4683741
E: ID_INPUT=1
E: ID_INPUT_TOUCHPAD=1
E: ID_SERIAL=noserial
E: ID_PATH=pci-0000:00:15.1-platform-i2c_designware.1
E: ID_PATH_TAG=pci-0000_00_15_1-platform-i2c_designware_1
E: DEVLINKS=/dev/input/by-path/pci-0000:00:15.1-platform-i2c_designware.1-mouse
```

## Thunderbolt docks

### TB16

TB16 works fine if either Thunderbolt security is disabled in the BIOS or using [bolt](https://www.archlinux.org/packages/?name=bolt) to temporarily authorize or permanently enroll Thunderbolt devices with Thunderbolt security activated. Various quirks are detailed on the [Dell TB16](/index.php/Dell_TB16 "Dell TB16") page.

## EFI firmware updates

They are 2 main ways to update efi firmware:

*   through running linux session with [Fwupd](/index.php/Fwupd "Fwupd")
*   through UEFI

### [Fwupd](/index.php/Fwupd "Fwupd")

```
 pacman -S fwupd

```

Then, look at:

```
 sudo fwupdmgr get-updates
 sudo fwupdmgr refresh
 sudo fwupdmgr update

```

### UEFI

Firmware images can be found at [Dell support page](https://www.dell.com/support/home/us/en/04/product-support/product/xps-15-9570-laptop/drivers) as `XPS_15_9570_X.Y.Z.exe` files. In order to install:

*   Download the desired firmware from section "Dell XPS 15 9570 System BIOS"
*   Save it in `/boot/EFI/Dell/Bios/` (this path may vary, depending on your installation)
*   Reboot the system, and enter the boot menu by pressing repeatedly `F12` on Dell logo
*   Choose "Bios Flash Update"
*   Select the file previously saved, and start the process

The process will take about five minutes, during which the system will have some reboots and push fans at maximum speed. Finally the system will reboot normally.

## Thermal management

Thermal design is poor in the 9570, primarily due to higher-end chips being used inside the original system design without compensating for extra heat. This impacts numerous areas:

1.  **Performance**: at higher temperatures, CPU cores are throttled down to avoid damage. At best your system will not run as fast as it can, and at worst (and quite commonly), slower than cheaper chips and with sluggish performance.
2.  **Battery life** is unnecessarily decreased.
3.  **System longevity**: running at constantly high temperatures will negatively impact equipment lifetime.
4.  **User discomfort**: uncomfortable heat and uncomfortable fan noise.

Fortunately these can all be improved significantly to get your system running powerfully and quietly.

### Diagnosis

You probably have a lot of dmesg output like this (for all CPUs), even with fairly light usage:

```
 kernel: CPU8: Package temperature above threshold, cpu clock throttled (total events = 8451)
 kernel: CPU8: Package temperature/speed normal

```

Use [lm_sensors](/index.php/Lm_sensors "Lm sensors") and do some [stress testing](/index.php/Stress_testing "Stress testing") (with `stress` and `mprime`) to see what's happening with CPU core temperatures and fanspeed under different loads.

### Undervolting

See [Undervolting CPU](/index.php/Undervolting_CPU "Undervolting CPU") on the wiki. Reduces heat and extends battery life.

Possible configurations for `/etc/intel-undervolt.conf`:

1.  i9-8950HK* (last updated 2019-03-30)

```
 undervolt 0 'CPU' -140
 undervolt 1 'GPU' -75

```

```
 * Tested extensively for moderate use.  Was not stress tested for > 24 hours.  Anecdotal reports of up to -200.

```

This has a more minor impact than repasting but is significantly easier to do.

### Repasting & padding

Significant improvements are possible by replacing the thermal grease used by Dell with better options available from Amazon, and adding some extra thermal padding. This might sound overwhelming but is well worth the effort, especially for newer CPUs. If you can't do this yourself consider finding a shop / technician who can do this for you. See the following article as the user comments below it for more info:

*   [UltraBookReview: How to Fix Throttling on the Dell XPS 15 9570 / 9560](https://www.ultrabookreview.com/14875-fix-throttling-xps-15/)
*   [Picture of 9570 VRMs](https://photos.google.com/share/AF1QipMv5n4GppVgSUNEuU-Ie9VOHd0sAFAe5U57l7vsOKuAiPZpLeZn1tSBYpmrNzpFpw/photo/AF1QipPi-eGtEStq0uF4Shle0FE_OgbEDeeNtuF0KqLR?key=Y0pJUEtYTmp5SUhteGEtTGlZa0p3cVFVT2dyNmtB) - from comments of the above article

### Results

According to the author of the UltraBookReview article above:

<q>Undervolting seems to reduce temps at max load by 7-10C, while repasting seems to reduce temps by between 4-10C depending on your original paste job and paste used.</q>

From [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1839474#p1839474), much lower/softer fan speeds were needed to maintain the same temperatures, and temperature was a few degrees lower under similar loads. Fans were on less often and for less time when they were. Throttling was less prevalent and less severe.

## Tips and Tricks

### Systemd doesn't wait for Network

Few months ago systemd added "after= .. .. network.target" in /usr/lib/systemd/system/systemd-user-sessions.service

This causes systemd to wait for network connection at boot, you can modify this file to remove network.target but it will be overwritten on systemd update. A better workaround is to add /etc/systemd/system/systemd-user-sessions.service with network.target removed.

 `/etc/systemd/system/systemd-user-sessions.service` 
```
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

[Unit]
Description=Permit User Sessions
Documentation=man:systemd-user-sessions.service(8)
After=remote-fs.target nss-user-lookup.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/lib/systemd/systemd-user-sessions start
ExecStop=/usr/lib/systemd/systemd-user-sessions stop
```