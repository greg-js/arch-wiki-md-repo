This article describes [Ethernet](https://en.wikipedia.org/wiki/Ethernet "wikipedia:Ethernet") specifics, general network configuration is covered in [Network configuration](/index.php/Network_configuration "Network configuration").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Device driver](#Device_driver)
    *   [1.1 Check the status](#Check_the_status)
    *   [1.2 Load the module](#Load_the_module)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 ifplugd for laptops](#ifplugd_for_laptops)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Swapping computers on the cable modem](#Swapping_computers_on_the_cable_modem)
    *   [3.2 Explicit Congestion Notification](#Explicit_Congestion_Notification)
    *   [3.3 Realtek no link / WOL problem](#Realtek_no_link_/_WOL_problem)
        *   [3.3.1 Enable the NIC directly in Linux](#Enable_the_NIC_directly_in_Linux)
        *   [3.3.2 Rollback/change Windows driver](#Rollback/change_Windows_driver)
        *   [3.3.3 Enable WOL in Windows driver](#Enable_WOL_in_Windows_driver)
        *   [3.3.4 Newer Realtek Linux driver](#Newer_Realtek_Linux_driver)
        *   [3.3.5 Enable LAN Boot ROM in BIOS/CMOS](#Enable_LAN_Boot_ROM_in_BIOS/CMOS)
    *   [3.4 No interface with Atheros chipsets](#No_interface_with_Atheros_chipsets)
    *   [3.5 Broadcom BCM57780](#Broadcom_BCM57780)
    *   [3.6 Realtek RTL8111/8168B](#Realtek_RTL8111/8168B)
    *   [3.7 Gigabyte Motherboard with Realtek 8111/8168/8411](#Gigabyte_Motherboard_with_Realtek_8111/8168/8411)

## Device driver

### Check the status

[udev](/index.php/Udev "Udev") should detect your [network interface controller](https://en.wikipedia.org/wiki/Network_interface_controller "wikipedia:Network interface controller") (NIC) and automatically load the necessary [kernel module](/index.php/Kernel_module "Kernel module") at startup. Check the "Ethernet controller" entry (or similar) from the `lspci -v` output. It should tell you which kernel module contains the driver for your network device. For example:

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

Next, check that the driver was loaded via `dmesg | grep *module_name*`. For example:

 `$ dmesg | grep atl1` 
```
...
atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Skip the next section if the driver was loaded successfully. Otherwise, you will need to know which module is needed for your particular model.

### Load the module

Search in the Internet for the right module/driver for the chipset. Some common modules are `8139too` for cards with a Realtek chipset, or `sis900` for cards with a SiS chipset. Once you know which module to use, try to [load it manually](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). If you get an error saying that the module was not found, it is possible that the driver is not included in Arch kernel. You may search the [AUR](/index.php/AUR "AUR") for the module name.

If udev is not detecting and loading the proper module automatically during bootup, see [Kernel module#Automatic module loading with systemd](/index.php/Kernel_module#Automatic_module_loading_with_systemd "Kernel module").

## Tips and tricks

### ifplugd for laptops

**Tip:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") provides the same feature out of the box.

[ifplugd](https://www.archlinux.org/packages/?name=ifplugd) is a daemon which will automatically configure your Ethernet device when a cable is plugged in and automatically unconfigure it if the cable is pulled. This is useful on laptops with onboard network adapters, since it will only configure the interface when a cable is really connected. Another use is when you just need to restart the network but do not want to restart the computer or do it from the shell.

By default it is configured to work for the `eth0` device. This and other settings like delays can be configured in `/etc/ifplugd/ifplugd.conf`.

**Note:** [netctl](/index.php/Netctl "Netctl") package includes `netctl-ifplugd@.service`, otherwise you can use `ifplugd@.service` from [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) package. For example, [enable](/index.php/Enable "Enable") `ifplugd@eth0.service`.

## Troubleshooting

### Swapping computers on the cable modem

Some cable ISPs (Vidéotron for example) have the cable modem configured to recognize only one client PC, by the MAC address of its network interface. Once the cable modem has learned the MAC address of the first PC or equipment that talks to it, it will not respond to another MAC address in any way. Thus if you swap one PC for another (or for a router), the new PC (or router) will not work with the cable modem, because the new PC (or router) has a MAC address different from the old one. To reset the cable modem so that it will recognise the new PC, you must power the cable modem off and on again. Once the cable modem has rebooted and gone fully online again (indicator lights settled down), reboot the newly connected PC so that it makes a DHCP request, or manually make it request a new DHCP lease.

If this method does not work, you will need to clone the MAC address of the original machine. See also [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

### Explicit Congestion Notification

[Explicit Congestion Notification](https://en.wikipedia.org/wiki/Explicit_Congestion_Notification "wikipedia:Explicit Congestion Notification") (ECN) may cause traffic problems with old/bad routers [[1]](https://bbs.archlinux.org/viewtopic.php?id=239892). As of [systemd 239](https://github.com/systemd/systemd/issues/9748), it is enabled for both ingoing and outgoing traffic.

To enable ECN only when requested by incoming connections (the reasonably safe, kernel default):

```
# sysctl net.ipv4.tcp_ecn=2

```

To disable ECN completely (to e.g. test whether ECN was causing problems):

```
# sysctl net.ipv4.tcp_ecn=0

```

See also the [kernel documentation](https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt).

### Realtek no link / WOL problem

Users with Realtek 8168 8169 8101 8111(C) based NICs (cards / and on-board) may notice a problem where the NIC seems to be disabled on boot and has no Link light. This can usually be found on a dual boot system where Windows is also installed. It seems that using the official Realtek drivers (dated anything after May 2007) under Windows is the cause. These newer drivers disable the Wake-On-LAN feature by disabling the NIC at Windows shutdown time, where it will remain disabled until the next time Windows boots. You will be able to notice if this problem is affecting you if the Link light remains off until Windows boots up; during Windows shutdown the Link light will switch off. Normal operation should be that the link light is always on as long as the system is on, even during POST. This problem will also affect other operating systems without newer drivers (eg. Live CDs). Here are a few fixes for this problem.

#### Enable the NIC directly in Linux

Follow [#Enabling and disabling network interfaces](#Enabling_and_disabling_network_interfaces) to enable the interface.

#### Rollback/change Windows driver

You can roll back your Windows NIC driver to the Microsoft provided one (if available), or roll back/install an official Realtek driver pre-dating May 2007 (may be on the CD that came with your hardware).

#### Enable WOL in Windows driver

Probably the best and the fastest fix is to change this setting in the Windows driver. This way it should be fixed system-wide and not only under Arch (eg. live CDs, other operating systems). In Windows, under Device Manager, find your Realtek network adapter and double-click it. Under the "Advanced" tab, change "Wake-on-LAN after shutdown" to "Enable".

In Windows XP (example):

```
Right click my computer and choose "Properties"
--> "Hardware" tab
  --> Device Manager
    --> Network Adapters
      --> "double click" Realtek ...
        --> Advanced tab
          --> Wake-On-Lan After Shutdown
            --> Enable

```

**Note:** Newer Realtek Windows drivers (tested with *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, dated 2009/01/22, available from GIGABYTE) may refer to this option slightly differently, like *Shutdown Wake-On-LAN > Enable*. It seems that switching it to `Disable` has no effect (you will notice the Link light still turns off upon Windows shutdown). One rather dirty workaround is to boot to Windows and just reset the system (perform an ungraceful restart/shutdown) thus not giving the Windows driver a chance to disable LAN. The Link light will remain on and the LAN adapter will remain accessible after POST - that is until you boot back to Windows and shut it down properly again.

#### Newer Realtek Linux driver

Any newer driver for these Realtek cards can be found for Linux on the realtek site (untested but believed to also solve the problem).

#### Enable LAN Boot ROM in BIOS/CMOS

It appears that setting *Integrated Peripherals > Onboard LAN Boot ROM > Enabled* in BIOS/CMOS reactivates the Realtek LAN chip on system boot-up, despite the Windows driver disabling it on OS shutdown.

**Note:** This was tested several times on a GIGABYTE GA-G31M-ES2L motherboard, BIOS version F8 released on 2009/02/05.

### No interface with Atheros chipsets

Users of some Atheros ethernet chips are reporting it does not work out-of-the-box (with installation media of February 2014). The working solution for this is to install [backports-patched](https://aur.archlinux.org/packages/backports-patched/).

### Broadcom BCM57780

This Broadcom chipset sometimes does not behave well unless you specify the order of the modules to be loaded. The modules are `broadcom` and `tg3`, the former needing to be loaded first.

These steps should help if your computer has this chipset:

*   Find your NIC in *lspci* output:

 `$ lspci | grep Ethernet` 
```
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

*   If your wired networking is not functioning in some way or another, unplug your cable then do the following:

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

*   Plug your network cable back in and check whether the module succeeded with:

```
$ dmesg | grep tg3

```

*   If this procedure solved the issue you can make it permanent by adding `broadcom` and `tg3` (in this order) to the `MODULES` array:

 `/etc/mkinitcpio.conf`  `MODULES=(.. broadcom tg3 ..)` 

*   [Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")
*   Alternatively, you can create an `/etc/modprobe.d/broadcom.conf`:

```
softdep tg3 pre: broadcom

```

**Note:** These methods may work for other chipsets, such as BCM57760.

### Realtek RTL8111/8168B

 `# lspci | grep Ethernet` 
```
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02)

```

The adapter should be recognized by the `r8169` module. However, with some chip revisions the connection may go off and on all the time. The alternative [r8168](https://www.archlinux.org/packages/?name=r8168) should be used for a reliable connection in this case. [Blacklist](/index.php/Blacklist "Blacklist") `r8169`, if [r8168](https://www.archlinux.org/packages/?name=r8168) is not automatically loaded by [udev](/index.php/Udev "Udev"), see [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules").

Another fault in the drivers for some revisions of this adapter is poor IPv6 support. [IPv6#Disable functionality](/index.php/IPv6#Disable_functionality "IPv6") can be helpful if you encounter issues such as hanging webpages and slow speeds.

### Gigabyte Motherboard with Realtek 8111/8168/8411

With motherboards such as the *Gigabyte GA-990FXA-UD3*, booting with [IOMMU](/index.php/PCI_passthrough_via_OVMF#Setting_up_IOMMU "PCI passthrough via OVMF") off (which can be the default) will cause the network interface to be unreliable, often failing to connect or connecting but allowing no throughput. This will apply to the onboard NIC and to any other pci-NIC in the box because the IOMMU setting affects the entire network interface on the board. Enabling IOMMU and booting with the install media will throw AMD I-10/xhci page faults for a second, but then boots normally, resulting in a fully functional onboard NIC (even with the r8169 module).

When configuring the boot process for your installation, add `iommu=soft` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to eliminate the error messages on boot and restore USB3.0 functionality.