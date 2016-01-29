# Acer Aspire V3-371

| **Device** | **Status** | **Modules** |
| Intel | Working, see notes | i915 |
| Ethernet | Working | r8169 |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working | uvcvideo |
| Card Reader | Working | rtsx_usb |
| Bluetooth | Working |

Information for the Acer Aspire V3-371 53L5 (Core i5-5200U, 4GiB RAM, 240GB SSD). Almost everything works right out of the box.

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Partitions](#Partitions)
    *   [1.2 Devices](#Devices)
*   [2 Configuration](#Configuration)
    *   [2.1 Disabling UEFI Secure Boot](#Disabling_UEFI_Secure_Boot)
    *   [2.2 Video](#Video)
    *   [2.3 Solid State Drive](#Solid_State_Drive)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Troubleshooting](#Troubleshooting)
        *   [2.5.1 Video](#Video_2)

# Hardware

## Partitions

 `# lsblk` 

```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0 223.6G  0 disk 
├─sda1   8:1    0   512M  0 part /boot
├─sda2   8:2    0    30G  0 part /
├─sda3   8:3    0     4G  0 part [SWAP]
└─sda4   8:4    0 189.1G  0 part /home

```

## Devices

 `# lspci` 

```
00:00.0 Host bridge: Intel Corporation Broadwell-U Host Bridge -OPI (rev 09)
00:02.0 VGA compatible controller: Intel Corporation Broadwell-U Integrated Graphics (rev 09)
00:03.0 Audio device: Intel Corporation Broadwell-U Audio Controller (rev 09)
00:14.0 USB controller: Intel Corporation Wildcat Point-LP USB xHCI Controller (rev 03)
00:16.0 Communication controller: Intel Corporation Wildcat Point-LP MEI Controller #1 (rev 03)
00:1b.0 Audio device: Intel Corporation Wildcat Point-LP High Definition Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation Wildcat Point-LP PCI Express Root Port #3 (rev e3)
00:1c.3 PCI bridge: Intel Corporation Wildcat Point-LP PCI Express Root Port #4 (rev e3)
00:1d.0 USB controller: Intel Corporation Wildcat Point-LP USB EHCI Controller (rev 03)
00:1f.0 ISA bridge: Intel Corporation Wildcat Point-LP LPC Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation Wildcat Point-LP SATA Controller [AHCI Mode] (rev 03)
00:1f.3 SMBus: Intel Corporation Wildcat Point-LP SMBus Controller (rev 03)
00:1f.6 Signal processing controller: Intel Corporation Wildcat Point-LP Thermal Management Controller (rev 03)
01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0c)
02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 48)

```

# Configuration

## Disabling UEFI Secure Boot

To disable Secure Boot, set the [supervisor password](https://acer.custhelp.com/app/answers/detail/a_id/29349/) in the BIOS settings. Then you should be able to boot Arch.

## Video

Install the xf86-video-intel package as shown [here](https://wiki.archlinux.org/index.php/Intel_graphics#Installation)

## Solid State Drive

[Enable TRIM by mount flag](https://wiki.archlinux.org/index.php/Solid_State_Drives#Enable_TRIM_by_mount_flag)

[Apply trim via periodic fstrim with systemd](https://wiki.archlinux.org/index.php/Solid_State_Drives#Apply_TRIM_via_periodic_fstrim)

[Switch from default CFQ scheduler to NOOP, for the whole system](https://wiki.archlinux.org/index.php/Solid_State_Drives#Kernel_parameter_.28for_a_single_device.29)

[Reduce Swappiness to 1](https://wiki.archlinux.org/index.php/Swap#Swappiness)

## Touchpad

Configure the touchpad as a ClickPad by editing the touchpad section in `/etc/X11/xorg.conf.d/50-synaptics.conf` as shown [here](https://wiki.archlinux.org/index.php/Touchpad_Synaptics#Buttonless_touchpads_.28aka_ClickPads.29)

## Troubleshooting

### Video

I experienced a [loss of h-sync when swiching TTYs](https://wiki.archlinux.org/index.php/Intel_graphics#Loss_of_horizontal_sync_when_switching_TTYs) and solved it as suggested by the wiki, by adding `i915.enable_ips=0` as a kernel parameter

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_V3-371&oldid=408270](https://wiki.archlinux.org/index.php?title=Acer_Aspire_V3-371&oldid=408270)"