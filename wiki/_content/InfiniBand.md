# InfiniBand

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Numerous [Help:Style](/index.php/Help:Style "Help:Style") violations. (Discuss in [Talk:InfiniBand#](https://wiki.archlinux.org/index.php/Talk:InfiniBand))

This page explains how to set up, diagnose, and benchmark an InfiniBand network.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Overview](#Overview)
    *   [1.2 Affordable used equipment](#Affordable_used_equipment)
    *   [1.3 Bandwidth](#Bandwidth)
        *   [1.3.1 Signal transfer rates](#Signal_transfer_rates)
        *   [1.3.2 Effective throughput & multiple virtual lanes](#Effective_throughput_.26_multiple_virtual_lanes)
    *   [1.4 Latency](#Latency)
    *   [1.5 Backwards compatibility](#Backwards_compatibility)
    *   [1.6 Cables](#Cables)
*   [2 Terminology](#Terminology)
    *   [2.1 Hardware](#Hardware)
    *   [2.2 GUID](#GUID)
    *   [2.3 NEED ANOTHER NAME](#NEED_ANOTHER_NAME)
    *   [2.4 Software](#Software)
*   [3 Software installation](#Software_installation)
    *   [3.1 Upgrade firmware](#Upgrade_firmware)
        *   [3.1.1 For Mellanox](#For_Mellanox)
        *   [3.1.2 For Intel/QLogic](#For_Intel.2FQLogic)
    *   [3.2 Kernel modules](#Kernel_modules)
    *   [3.3 Subnet manager](#Subnet_manager)
        *   [3.3.1 For a software subnet manager, use opensm](#For_a_software_subnet_manager.2C_use_opensm)
    *   [3.4 TCP/IP over InfiniBand (IPoIB)](#TCP.2FIP_over_InfiniBand_.28IPoIB.29)
        *   [3.4.1 Connection mode](#Connection_mode)
        *   [3.4.2 MTU](#MTU)
        *   [3.4.3 Fine-tuning connection mode and MTU](#Fine-tuning_connection_mode_and_MTU)
    *   [3.5 iSCSI over InfiniBand](#iSCSI_over_InfiniBand)
        *   [3.5.1 ISCSI over IPoIB](#ISCSI_over_IPoIB)
*   [4 InfiniBand programs for diagnosing and benchmarking](#InfiniBand_programs_for_diagnosing_and_benchmarking)
    *   [4.1 ibstat - View a computer's InfiniBand GUIDs](#ibstat_-_View_a_computer.27s_InfiniBand_GUIDs)
    *   [4.2 ibhosts - View all hosts on InfiniBand network](#ibhosts_-_View_all_hosts_on_InfiniBand_network)
    *   [4.3 ibswitches - View all switches on InfiniBand network](#ibswitches_-_View_all_switches_on_InfiniBand_network)
    *   [4.4 iblinkinfo - View link information on InfiniBand network](#iblinkinfo_-_View_link_information_on_InfiniBand_network)
    *   [4.5 ibping - Ping another InfiniBand device](#ibping_-_Ping_another_InfiniBand_device)
    *   [4.6 ibdiagnet - Show diagnostic information for entire subnet](#ibdiagnet_-_Show_diagnostic_information_for_entire_subnet)
    *   [4.7 qperf - Measure performance over RDMA or TCP/IP](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP)
        *   [4.7.1 TCP/IP over IPoIB](#TCP.2FIP_over_IPoIB)
    *   [4.8 iperf - Measure performance over TCP/IP](#iperf_-_Measure_performance_over_TCP.2FIP)
*   [5 Common problems / FAQ](#Common_problems_.2F_FAQ)
    *   [5.1 Connection problems](#Connection_problems)
        *   [5.1.1 Link, physical state, and port state](#Link.2C_physical_state.2C_and_port_state)
        *   [5.1.2 getaddrinfo failed: Name or service not known](#getaddrinfo_failed:_Name_or_service_not_known)
    *   [5.2 Speed problems](#Speed_problems)
*   [6 Network segmentation](#Network_segmentation)
*   [7 How can I use libsdp for SDP (Sockets Direct Protocol)? =](#How_can_I_use_libsdp_for_SDP_.28Sockets_Direct_Protocol.29.3F_.3D)

## Introduction

### Overview

InfiniBand (abbreviated IB) is an alternative to Ethernet and Fibre Channel. InfiniBand provides high bandwidth and low latency. InfiniBand can transfer data directly to and from a storage device on one machine to userspace on another machine, bypassing and avoiding the overhead of a system call. InfiniBand adapters can handle the networking protocols, unlike Ethernet networking protocols which are ran on the CPU. This allows the OS's and CPU's to remain free while the high bandwidth transfers take place, which can be a real problem with 10Gb+ Ethernet.

InfiniBand hardware is made by Mellanox (which merged with Voltaire, and is heavily backed by Oracle) and Intel (which acquired QLogic's InfiniBand program.) InfiniBand is most often used by supercomputers, clusters, and data centers. IBM, HP, and Cray are also members of the InfiniBand Steering Committee. Facebook, Twitter, eBay, YouTube, and PayPal are examples of InfiniBand users.

InfiniBand software is developed under the [OpenFabrics Open Source Alliance](http://www.openfabrics.org)

### Affordable used equipment

With large businesses benefiting so much from jumping to newer versions, the maximum length limitations of passive InfiniBand cabling, the high cost of active InfiniBand cabling, and the more technically complex setup than Ethernet, the used InfiniBand market is heavily saturated, allowing used InfiniBand devices to affordably be used at home or smaller businesses for their internal networks.

### Bandwidth

#### Signal transfer rates

InfiniBand transfer rates now correspond to the maximum supported by PCI Express (abbreviated PCIe). It originally corresponded to PCI Extended (abbreviated PCI-X), which severely limited performance. It launched using SDR (Single Data Rate) with a signaling rate of 2.5Gb/s per lane (corresponding with PCI Express v1.0), and has added: DDR (Double Data Rate) at 5Gb/s (PCI Express v2.0); QDR (Quad Data Rate) at 10Gb/s (PCI Express 3.0); and FDR (Fourteen Data Rate) at 14.0625Gbps (PCI Express 4.0.) InfiniBand is now delivering EDR (Enhanced Data Rate) at 25Gb/s. Planned around 2017 will be HDR (High Data Rate) at 50Gb/s.

#### Effective throughput & multiple virtual lanes

Because SDR, DDR, and QDR versions use 8/10 encoding (8 bits of data takes 10 bits of signaling), effective throughput for these is lowered to 80%: SDR at 2Gb/s/lane; DDR at 4Gb/s/lane; and QDR at 8Gb/s/lane. Starting with FDR, InfiniBand uses 64/66 encoding, allowing a higher effective throughput to signaling rate ratio of 96.97%: FDR at 13.64Gb/s/lane; EDR at 24.24Gb/s/lane; and HDR at 48.48Gb/s/lane.

InfiniBand devices are capable of using multiple virtual lanes, most using 4X, but some using a slower 1X or faster 12X.

When using the common 4X lane devices, this effectively allows total effective throughputs of: SDR of 8Gb/s; DDR of 16Gb/s; QDR of 32Gb/s; FDR of 54.54Gb/s; EDR of 96.97Gb/s; and HDR of 193.94Gb/s.

### Latency

InfiniBand's latency is incredibly small: SDR (5us); DDR (2.5us); QDR (1.3us); FDR (0.7us); EDR (0.5us); and HDR (< 0.5us.) For comparison 10Gb Ethernet is more like 7.22us, ten times more than FDR's latency.

### Backwards compatibility

InfiniBand devices are almost always backwards compatible. Connections should be established at the lowest common denominator. A DDR adapter meant for a PCI Express 8x slot should work in a PCI Express 4x slot. (With half the bandwidth.)

### Cables

InfiniBand passive copper cables can be up to 7 meters using up to QDR, and 3 meters using FDR.

InfiniBand active fiber (optical) cables can be up to 300 meters using up to FDR. (Only 100 meters on FDR10, which is a variant not otherwise really discussed in this article.)

Mellanox MetroX devices exist which allow up to 80 kilometer (50 mile) connections. Latency increases by about 5us per kilometer.

An InfiniBand cable can be used to directly link two computers without a switch; InfiniBand cross-over cables do not exist.

## Terminology

### Hardware

Adapters, switches, routers, and bridges/gateways must be specifically made for InfiniBand.

NaN

### GUID

Like Ethernet MAC addresses, but a device has multiple GUID's. Assigned by the hardware manufacturer, and remains the same through reboots. 64-bit addresses (24-bit manufacturer prefix and 40-bit device identifier.) Given to adapters, switches, routers, and bridges/gateways.

NaN

### NEED ANOTHER NAME

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Give the section a proper heading. (Discuss in [Talk:InfiniBand#](https://wiki.archlinux.org/index.php/Talk:InfiniBand))

NaN

NaN

### Software

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** TODO. (Discuss in [Talk:InfiniBand#](https://wiki.archlinux.org/index.php/Talk:InfiniBand))

## Software installation

This article makes many references to the InfiniBand AUR packages. You can [obtain and install AUR packages any way you wish](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages).

### Upgrade firmware

Running the most recent firmware can give significant performance increases, and fix connectivity issues.

**Warning:** That being said, upgrade your firmware at your own risk! Whatever device you're flashing new firmware onto, there is always some risk of bricking the device.

#### For Mellanox

*   Install [mstflint](https://aur.archlinux.org/packages/mstflint/)<sup><small>AUR</small></sup>, with prerequisites: [libibumad](https://aur.archlinux.org/packages/libibumad/)<sup><small>AUR</small></sup>; [libibmad](https://aur.archlinux.org/packages/libibmad/)<sup><small>AUR</small></sup>.
*   Determine your adapter's PCI device ID (in this example, "05:00.0" is the adapter's PCI device ID)

 `$ lspci | grep Mellanox`  `**05:00.0** InfiniBand: Mellanox Technologies MT25418 [ConnectX VPI PCIe 2.0 2.5GT/s - IB DDR / 10GigE] (rev a0)` 

*   Determine what firmware version your adapter has, and your adapter's PSID (more specific than just a model number - specific to a compatible set of revisions)

 `# mstflint -d <adapter PCI device ID> query` 

```
...
FW Version:      **2.7.1000**
...
PSID:            **MT_04A0110002**
```

*   Check latest firmware version
    *   Visit [Mellanox's firmware download page](http://www.mellanox.com/page/firmware_download). (This guide incorporates this link's "firmware burning instructions", using its mstflint option.)
    *   Choose the category of device you have
    *   Locate your device's PSID on their list, that mstflint gave you
    *   Examine the Firmware Image filename to see if it's more recent than your adapter's FW Version. (i.e. If Mellanox lists for your PSID a file fw-25408-2_9_1000-MHGH28-XTC_A1.bin.zip, that's a 2.9.1000 FW Version.)
*   If there's a more recent version, download new firmware and burn it to your adapter

```
$ unzip <_firmware .bin.zip file name_>
# mstflint -d <_adapter PCI device ID_> -i <_firmware .bin file name_> burn

```

#### For Intel/QLogic

(Intel acquired QLogic's InfiniBand program)

... You figure it out, and update this wiki! Maybe start at [http://driverdownloads.qlogic.com/QLogicDriverDownloads_UI/Defaultnewsearch.aspx](http://driverdownloads.qlogic.com/QLogicDriverDownloads_UI/Defaultnewsearch.aspx) or [https://downloadcenter.intel.com/](https://downloadcenter.intel.com/)

### Kernel modules

Recent kernels have InfiniBand modules compiled in, and they just need to be loaded.

*   Install [rdma](https://aur.archlinux.org/packages/rdma/)<sup><small>AUR</small></sup>
    *   Its `/usr/lib/udev/rules.d/98-rdma.rules` attempts loading hardware kernel modules cxgb*, ib_*, mlx*, iw_*, be2net, and usnic*.
    *   Its `/usr/bin/rdma-init-kernel` (which is what `rdma.service` starts) loads kernel modules requested by `/etc/rdma.conf`.

<caption>/etc/rdma.conf supports these options</caption>
| Option | If yes, loads category | of these kernel modules |
| (Always) | Core | ib_core, ib_mad, ib_sa, and ib_addr |
| (Always) | Core user | ib_umad, ib_uverbs, ib_ucm, and rdma_ucm |
| (Always) | Core connection manager | iw_cm, ib_cm, and rdma_cm |
| IPOIB_LOAD=yes (default yes)* | Internet Protocol over InfiniBand | ib_ipoib |
| RDS_LOAD=yes (default no) | Reliable Datagram Service | rds, rds_tcp, and rds_rdma |
| SRP_LOAD=yes (default no) | SCSI Remote Protocol initiator | ib_srp |
| SRPT_LOAD=yes (default no) | SCSI Remote Protocol target | ib_srpt |
| ISER_LOAD=yes (default no) | iSCSI over RDMA initiator | ib_iser. |
| ISERT_LOAD=yes (default no) | iSCSI over RDMA target | ib_isert. |
| (if lhca devices) | IBM pSeries Adapters (rare) | ib_ehca |
| (if be2net module) | Emulex Adpaters (rare) | ocrdma |

NaN

*   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `rdma.service`

**Note:** [Due to how the kernel stacks are handled](https://bugzilla.redhat.com/show_bug.cgi?id=965829), changes to `/etc/rdma.conf` only take effect during boot, or upon a boot's first [start](/index.php/Start "Start") of `rdma.service`. Restarting `rdma.service` will have no effect.

### Subnet manager

Each InfiniBand network requires a subnet manager. (It is also possible to set up a redundant subnet manager.) Without one, your devices may show they have a link, but will never move past the state "Initializing" to "Active". A subnet manager often (typically every 5 or 30 seconds) checks the InfiniBand for new adapters, and adds them to the network's routing tables. If you have an InfiniBand switch with an embedded subnet manager, or you can use that, or you can keep it disabled and use a software subnet manager instead. Dedicated InfiniBand subnet manager devices also exist.

#### For a software subnet manager, use opensm

On one system:

*   [Install rdma for loading kernel modules](#Kernel_modules)
*   Install [opensm](https://aur.archlinux.org/packages/opensm/)<sup><small>AUR</small></sup>, with prerequisite [libibumad](https://aur.archlinux.org/packages/libibumad/)<sup><small>AUR</small></sup>.
*   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `opensm.service`.

All of your connected InfiniBand ports should now be in a (port) state of "Active", and a physical state of "LinkUp". You can check this by running [ibstat](#ibstat_-_View_a_computer.27s_InfiniBand_GUIDs) in [infiniband-diags](https://aur.archlinux.org/packages/infiniband-diags/)<sup><small>AUR</small></sup>:

 `$ ibstat` 

```
... (look at the ports shown you expect to be connected)
State: Active
Physical state: LinkUp
...
```

And/or by examining the `/sys` filesystem:

 `$ cat /sys/class/infiniband/_kernel_module_/ports/_port_number_/phys_state`  `5: LinkUp`  `$ cat /sys/class/infiniband/_kernel_module_/ports/_port_number_/state`  `4: ACTIVE` 

### TCP/IP over InfiniBand (IPoIB)

You can create a virtual Ethernet Adapter to be ran on an InfiniBand adapter. This is intended so programs that are designed to work with TCP/IP but not InfiniBand, can (indirectly) use InfiniBand networks. This is not intended to route internet traffic through your InfiniBand network. (Unless your internet connection is faster than your Ethernet devices are... Which means you're working with [Internet2](https://en.wikipedia.org/wiki/Internet2), **very** high performance supercomputers, clusters, or data centers, or you live in a handpicked area by [Google Fiber](https://fiber.google.com/about/) or [Comcast](http://www.pcmag.com/article2/0,2817,2479953,00.asp) offering a 2Gbps+ internet connection, which isn't available residentially anywhere as of mid 2015.)

There is a performance hit for programs using InfiniBand via TCP/IP rather than natively. Using IPoIB sends all traffic through the normal TCP stack, requires system calls, memory copies, and the network protocols are ran on the CPU rather than on the InfiniBand adapter.

*   [Install rdma for loading kernel modules](#Kernel_modules).
*   You should now have a network interface(s) (likely `ib_X_` like `ib0`), that you [can configure just like a traditional Ethernet adapter](/index.php/Network_configuration "Network configuration"). If you only have one subnet with point-to-point connections (perhaps with switches) with no gateways, for:
    *   [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"): (replacing the IP addresses as needed, to use a subnet that does not conflict with your existing private network IP addresses)

 `/etc/systemd/network/_interface_.network` 

```
[Match]
Name=_interface_

[Network]
Address=192.168.2.1/24
```

NaN

 `/etc/conf.d/net-conf-_interface_` 

```
address=192.168.2.1
netmask=24
broadcast=192.168.2.255
```

NaN

#### Connection mode

IPoIB can run in "datagram" (default), or "connected" mode. Connected mode [allows you to set a higher MTU](#Fine-tuning_MTU), but does increase TCP latency for short messages by about 5% more than datagram mode.

To see the current mode used:

```
$ cat /sys/class/net/_interface_/mode

```

#### MTU

In datagram mode, UD (Unreliable Datagram) transport is used, which typically forces the MTU to be 2044 bytes. (Technically to the IB L2 MTU - 4 bytes for the IPoIB encapsulation header, which is usually 2044 bytes.)

In connected mode, RC (Reliable Connected) transport is used, which allows a MTU up to the maximum IP packet size of 64K (65520 bytes is the exact maximum.)

To see your MTU:

```
$ ip link show _interface_

```

#### Fine-tuning connection mode and MTU

You only need `ipoibmodemtu` if you want to change the default connection mode and/or MTU.

*   [Install and set up TCP/IP over InfiniBand (IPoIB)](#TCP.2FIP_over_InfiniBand_.28IPoIB.29).
*   Install [ipoibmodemtu](https://aur.archlinux.org/packages/ipoibmodemtu/)<sup><small>AUR</small></sup>
*   Configure `ipoibmodemtu` through `/etc/ipoibmodemtu.conf`, which contains instructions on how to do so.
    *   It defaults to setting a single InfiniBand port `ib0` to `connected` mode and MTU `65520`.
*   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `ipoibmodemtu.service`

Different setups will see different results. Some people see a gigantic (double+) speed increase by usign `connected` mode and MTU `65520`, and a few see about the same or even worse speeds. Use [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) and/or [iperf](#iperf_-_Measure_performance_over_TCP.2FIP) to fine-tune your system.

Using the [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) examples given in this article, here are author's results on a SDR speed InfiniBand network (8 theoretical Gb/s) with various fine-tuning:

| Mode | MTU | MB/s | us latency |
| datagram | 2044 | 707 | 19.4 |
| connected | 2044 | 353 | 18.9 |
| connected | 65520 | 726 | 19.6 |

**Tip:** It's usually best to have an entire subnet using the same connection and MTU settings. Mixing and matching appears to work, but not optimally.

### iSCSI over InfiniBand

iSCSI allows storage devices and virtual storage devices to be used over a network. It differs from traditional file sharing (i.e. [Samba](/index.php/Samba "Samba") or [NFS](/index.php/NFS "NFS")) because iSCSI has the "guest" system view the shared device as its own block level device, rather than a traditionally mounted network shared folder. The disadvantage is iSCSI only allows one system to use each shared device at a time; trying to mount a shared device on the target ("host") system that is logged into by iSCSI by another system will fail. (A system using a shared deivce can certainly run traditional file sharing on top.) The advantages are that iSCSI allows speed, more control, and even a system's root filesystem to be located remotely (remote booting.)

There is a lot of overlap with the [ISCSI Target](/index.php/ISCSI_Target "ISCSI Target"), [ISCSI Initiator](/index.php/ISCSI_Initiator "ISCSI Initiator"), and [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot") articles, but the necessities will be discussed since much needs to be customized for usage over InfiniBand.

#### ISCSI over IPoIB

*   On all target ("host") and initiator ("guest") systems, [Install TCP/IP over InfiniBand](#TCP.2FIP_over_InfiniBand_.28IPoIB.29)

*   On the target ("host") system:
    *   Install [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/)<sup><small>AUR</small></sup> with prerequisites: [python-configshell-fb](https://aur.archlinux.org/packages/python-configshell-fb/)<sup><small>AUR</small></sup>; and [python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/)<sup><small>AUR</small></sup>.
    *   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `target.service`
    *   Setup your iSCSI targets. Run `targetcli`, which acts like a shell that presents its complex and not worth creating by hand `/etc/target/saveconfig.json` as a pseudo-filesystem.
        *   In any pseudo-directory, you can run `help` to see the commands available _in that pseudo-directory_. Or, `help _command_` (like `help create` for more detailed help.
        *   Run `ls` to see the entire pseudo-filesystem at and below the current pseudo-directory.
        *   Create a backstore (the device or virtual device you want to share)
            *   To share an actual block device, run: `cd /backstores/block`; and `create _name_ _dev_`.
            *   To share a file as a virtual block device, run: `cd /backstores/fileio`; and `create _name_ _file_`.
            *   To share a physical SCSI device as a pass-through, run: `cd /backstores/pscsi`; and `create _name_ _dev_`.
            *   To share a RAM disk, run: `cd /backstores/ramdisk`; and `create _name_ _size_`.
            *   Where: _name_ is for the backstore's name.
            *   Where _dev_ is the block device to share (i.e. /dev/sda, /dev/sda4, /dev/disk/by-id/_x_, or a LVM logical volume /dev/vg0/lv1).
            *   Where _file_ is the file to share (i.e. _/path/to/file_).
            *   Where _size_ is the size of the RAM disk to create (i.e. 512MB, 20GB.)
        *   Create an iqn (iSCSI Qualified Name) (the name other systems' configurations will see the storage as.)
            *   Run: `cd /iscsi`; and `create`. It will give you a _randomly_generated_target_name_, i.e. iqn.2003-01.org.linux-iscsi.hostname.x8664:sn.3d74b8d4020a.
        *   Set up the tpg (Target Portal Group), automatically created in the last step as tpg1.
            *   Create a lun (Logical Unit Number).
                *   Run: `cd _randomly_generated_target_name_/tpg1/luns`; and `create _storage_object_`. Where `_storage_object_` is a full path to an existing storage object, i.e. /backstores/block/_name_.
            *   Create an acl (Access Control List).
                *   Run: `cd ../acls`; and `create _wwn_`. Where `_wwn_` is the initiator ("guest") system's iqn (iSCSI Qualified Name), aka its (World Wide Name).
                    *   Get the `_wwn_` by running on the initiator ("guest") system, **not** this target ("host") system: (after installing on it [open-iscsi](https://www.archlinux.org/packages/?name=open-iscsi) or [open-iscsi-git](https://aur.archlinux.org/packages/open-iscsi-git/)<sup><small>AUR</small></sup>) `cat /etc/iscsi/initiatorname.iscsi`.
        *   Save and exit by running: `cd /`; `saveconfig`; and `exit`.

*   On the initiator ("guest") system:
    *   Install [open-iscsi](https://www.archlinux.org/packages/?name=open-iscsi), or [open-iscsi-git](https://aur.archlinux.org/packages/open-iscsi-git/)<sup><small>AUR</small></sup>.
    *   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") open-iscsi.service.
    *   At this point, if you need this initiator system's iqn (iSCSI Qualified Name), aka its wwn (World Wide Name), for setting up the target ("host") system's `luns` in `targetcli`, run: `cat /etc/iscsi/initiatorname.iscsi`.
    *   Discover online targets. Run `iscsiadm -m discovery -t sendtargets -p _portal_`, where _portal_ is an IP (v4 or v6) address or hostname.
    *   Login to discovered targets. Run `iscsiadm -m node -L all`.
    *   View which block device ID was given to each target logged into. Run `iscsiadm -m session -P 3`. The block device ID will be the last line in the tree for each target. `-P` is the print command, and its option is the verbosity level. Only verbosity level 3 lists the block device IDs.

Now, on the initiator ("guest") system, you should be able to use your new iSCSI-backed block device just like any other. i.e. `fdisk /dev/_block_device_id_`, `mkfs.btrfs /dev/_block_device_id_with_partition_number_`.

## InfiniBand programs for diagnosing and benchmarking

### ibstat - View a computer's InfiniBand GUIDs

ibstat will show you detailed information about each InfiniBand adapter in the computer it is ran on, including: model number; number of ports; firmware and hardware version; node, system image, and port GUIDs; and port state, physical state, rate, base lid, lmc, SM lid, capability mask, and link layer.

 `$ ibstat` 

```
CA 'mlx4_0'
        CA type: MT25418
        Number of ports: 2
        Firmware version: 2.9.1000
        Hardware version: a0
        Node GUID: 0x0002c90300002f78
        System image GUID: 0x0002c90300002f7b
        Port 1:
                State: Active
                Physical state: LinkUp
                Rate: 20
                Base lid: 3
                LMC: 0
                SM lid: 3
                Capability mask: 0x0251086a
                Port GUID: 0x0002c90300002f79
                Link layer: InfiniBand
        Port 2:
                State: Down
                Physical state: Polling
                Rate: 10
                Base lid: 0
                LMC: 0
                SM lid: 0
                Capability mask: 0x02510868
                Port GUID: 0x0002c90300002f7a
                Link layer: InfiniBand
```

This example shows a Mellanox Technologies (MT) adapter. Its PCI Device ID is reported (25418), rather than the model number of part number. It shows a state of "Active", which means is it properly connected to a subnet manager. It shows a physical state of "LinkUp", which means it has an electrical connection via cable, but is not necessarily properly connected to a subnet manager. It shows a total rate of 20 Gb/s (which for this card is from a 5.0 Gb/s signaling rate and 4 virtual lanes.) It shows the subnet manager assigned the port a lid of 3.

### ibhosts - View all hosts on InfiniBand network

ibhosts will show you the Node GUIDs, number of ports, and device names, for each host on the InfiniBand network.

 `# ibhosts` 

```
Ca      : 0x0002c90300002778 ports 2 "MT25408 ConnectX Mellanox Technologies"
Ca      : 0x0002c90300002f78 ports 2 "hostname mlx4_0"
```

### ibswitches - View all switches on InfiniBand network

ibswitches will show you the Node GUIDs, number of ports, and device names, for each switch on the InfiniBand network. If you are running with direct connections only, it will show nothing.

```
# ibswitches

```

### iblinkinfo - View link information on InfiniBand network

iblinkinfo will show you the device names, Port GUIDs, number of virtual lanes, [signal transfer rates](#Signal_transfer_rates), state, physical state, and what it is connected to.

 `# iblinkinfo` 

```
CA: MT25408 ConnectX Mellanox Technologies:
      0x0002c90300002779      4    1[  ] ==( 4X           5.0 Gbps Active/  LinkUp)==>       3    1[  ] "kvm mlx4_0" ( )
CA: hostname mlx4_0:
      0x0002c90300002f79      3    1[  ] ==( 4X           5.0 Gbps Active/  LinkUp)==>       4    1[  ] "MT25408 ConnectX Mellanox Technologies" ( )
```

This example shows two adapters directly connected with out a switch, using a 5.0 Gb/s [signal transfer rate](#Signal_transfer_rates), and 4 virtual lanes (4X).

### ibping - Ping another InfiniBand device

ibping will attempt pinging another InfiniBand GUID. ibping must be ran in server mode on one computer, and in client mode on another.

ibping must be ran in server mode on one computer.

```
# ibping -S

```

And in client mode on another. It is pinging a specific port, so it cannot take a CA name, or a Node or System GUID. It requires `-G` with a Port GUID, or `-L` with a Lid.

```
# ibping -G 0x0002c90300002779
-or-
# ibping -L 1
```

```
Pong from hostname.(none) (Lid 1): time 0.053 ms
Pong from hostname.(none) (Lid 1): time 0.074 ms
^C
--- hostname.(none) (Lid 4) ibping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1630 ms
rtt min/avg/max = 0.053/0.063/0.074 ms
```

If you're running IPoIB, you can use regular `ping` which pings through the TCP/IP stack. ibping uses InfiniBand interfaces, and does not use the TCP/IP stack.

### ibdiagnet - Show diagnostic information for entire subnet

ibdiagnet will show you potential problems on your subnet. You can run it without options. `-lw <1x|4x|12x>` specifies the expected link width (number of virtual lanes) for your computer's adapter, so it can check if it is running as intended. `-ls <2.5|5|10>` specifies the expected link speed (signaling rate) for your computer's adapter, so it can check if it is running as intended, but it does not yet support options faster than 10 for FDR+ devices. `-c <count>` overrides the default number of packets to be sent of 10.

 `# ibdiagnet -lw 4x -ls 5 -c 1000` 

```
Loading IBDIAGNET from: /usr/lib/ibdiagnet1.5.7
-W- Topology file is not specified.
    Reports regarding cluster links will use direct routes.
Loading IBDM from: /usr/lib/ibdm1.5.7
-I- Using port 1 as the local port.
-I- Discovering ... 2 nodes (0 Switches & 2 CA-s) discovered.

-I---------------------------------------------------
-I- Bad Guids/LIDs Info
-I---------------------------------------------------
-I- No bad Guids were found

-I---------------------------------------------------
-I- Links With Logical State = INIT
-I---------------------------------------------------
-I- No bad Links (with logical state = INIT) were found

-I---------------------------------------------------
-I- General Device Info
-I---------------------------------------------------

-I---------------------------------------------------
-I- PM Counters Info
-I---------------------------------------------------
-I- No illegal PM counters values were found

-I---------------------------------------------------
-I- Links With links width != 4x (as set by -lw option)
-I---------------------------------------------------
-I- No unmatched Links (with width != 4x) were found

-I---------------------------------------------------
-I- Links With links speed != 5 (as set by -ls option)
-I---------------------------------------------------
-I- No unmatched Links (with speed != 5) were found

-I---------------------------------------------------
-I- Fabric Partitions Report (see ibdiagnet.pkey for a full hosts list)
-I---------------------------------------------------
-I-    PKey:0x7fff Hosts:2 full:2 limited:0

-I---------------------------------------------------
-I- IPoIB Subnets Check
-I---------------------------------------------------
-I- Subnet: IPv4 PKey:0x7fff QKey:0x00000b1b MTU:2048Byte rate:10Gbps SL:0x00
-W- Suboptimal rate for group. Lowest member rate:20Gbps > group-rate:10Gbps

-I---------------------------------------------------
-I- Bad Links Info
-I- No bad link were found
-I---------------------------------------------------
----------------------------------------------------------------
-I- Stages Status Report:
    STAGE                                    Errors Warnings
    Bad GUIDs/LIDs Check                     0      0     
    Link State Active Check                  0      0     
    General Devices Info Report              0      0     
    Performance Counters Report              0      0     
    Specific Link Width Check                0      0     
    Specific Link Speed Check                0      0     
    Partitions Check                         0      0     
    IPoIB Subnets Check                      0      1     

Please see /tmp/ibdiagnet.log for complete log
----------------------------------------------------------------

-I- Done. Run time was 0 seconds.
```

### qperf - Measure performance over RDMA or TCP/IP

qperf can measure bandwidth and latency over RDMA (SDP, UDP, UD, and UC) or TCP/IP (including IPoIB)

qperf must be ran in server mode on one computer.

```
$ qperf

```

And in client mode on another. SERVERNODE can be a hostname, or for IPoIB a TCP/IP address. There are many tests. Some of the most useful are below.

```
$ qperf SERVERNODE [OPTIONS] TESTS

```

#### TCP/IP over IPoIB

 `$ qperf 192.168.2.2 tcp_bw tcp_lat` 

```
tcp_bw:
    bw  =  701 MB/sec
tcp_lat:
    latency  =  19.8 us
```

### iperf - Measure performance over TCP/IP

iperf is not an InfiniBand aware program, and is meant to test over TCP/IP or UDP. Even though [#qperf - Measure performance over TCP/IP or RDMA](#qperf_-_Measure_performance_over_TCP.2FIP_or_RDMA) can test your InfiniBand TCP/IP performace using IPoIB, iperf is still another program you can use.

iperf must be ran in server mode on one computer.

```
$ iperf3 -s

```

And in client mode on another.

 `$ iperf3 -c 192.168.2.2` 

```
[  4] local 192.168.2.1 port 20139 connected to 192.168.2.2 port 5201
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-1.00   sec   639 MBytes  5.36 Gbits/sec                  
...
[  4]   9.00-10.00  sec   638 MBytes  5.35 Gbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[  4]   0.00-10.00  sec  6.23 GBytes  5.35 Gbits/sec                  sender
[  4]   0.00-10.00  sec  6.23 GBytes  5.35 Gbits/sec                  receiver

iperf Done.
```

iperf shows Transfer in base 10 GB's, and Bandwidth in base 2 GB's. So, this example shows 6.23GB (base 10) in 10 seconds. That's 6.69GB (base 2) in 10 seconds. (6.23 * 2^30 / 10^9) That's 5.35 Gb/s (base 2), as shown by iperf. (6.23 * 2^30 / 10^9 * 8 / 10) That's 685 MB/s (base 2), which is roughly the speed that qperf reported. (6.23 * 2^30 / 10^9 * 8 / 10 * 1024 / 8)

## Common problems / FAQ

### Connection problems

#### Link, physical state, and port state

*   See if the InfiniBand hardware modules are recognized by the system.

 `$ dmesg | egrep -i "Mellanox|InfiniBand|QLogic|Voltaire" # If you have an Intel adapter, you'll have to use Intel here and look through a few lines if you have other Intel hardware` 

```
[    6.287556] mlx4_core: Mellanox ConnectX core driver v2.2-1 (Feb, 2014)
[    8.686257] <mlx4_ib> mlx4_ib_add: mlx4_ib: Mellanox ConnectX InfiniBand driver v2.2-1 (Feb 2014)
```

-and/or-

 `$ ls -l /sys/class/infiniband`  `mlx4_0 -> ../../devices/pci0000:00/0000:00:03.0/0000:05:00.0/infiniband/mlx4_0` 

If nothing is shown, your kernel isn't recognizing your adapter. This example shows approximately what you will see if you have a Mellanox ConnectX adapter, which uses the mlx4_0 kernel module.

*   Check the port and physical states. Either run [ibstat](#ibstat_-_View_a_computer.27s_InfiniBand_GUIDs), or examine the /sys filesystem.

 `$ ibstat`  `(look at the port shown you expect to be connected)` 

-and/or-

 `$ cat /sys/class/infiniband/<kernel module>/ports/<port number>/phys_state`  ` 5: LinkUp`  `$ cat /sys/class/infiniband/<kernel module>/ports/<port number>/state`  ` 4: ACTIVE` 

The physical state should be "LinkUp". If it isn't, your cable likely isn't plugged in, isn't connected to anything on the other end, or is defective. The (port) state should be "Active". If it's "Initializing" or "INIT", your [subnet manager](#Subnet_manager) doesn't exist, isn't running, or hasn't added the port to the network's routing tables.

*   Can you successfully [ibping](#ibping_-_Ping_another_InfiniBand_device) which uses InfiniBand directly, rather than IPoIB? Can you successfully `ping`, if you are running IPoIB?

*   Consider [upgrading firmware](#Upgrade_firmware).

#### getaddrinfo failed: Name or service not known

*   Run [ibhosts](#ibhosts_-_View_all_hosts_on_InfiniBand_network) to see the CA names at the end of each line in quotes.

### Speed problems

*   Start by double-checking your expectations.

How have you determined you have a speed problem? Are you using [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) or [iperf](#iperf_-_Measure_performance_over_TCP.2FIP), which both transmit data to and from memory rather than hard drives. Or, are you benchmarking actual file transfers, which relies on your hard drives? Unless you're running RAID to boost speed, even with the fastest SSD's available in mid 2015, a single hard drive (or sometimes even multiple ones) will be bottlenecking your InfiniBand transfer speeds. Are you using RDMA or TCP/IP via IPoIB? If so, [there is a performance hit](#TCP.2FIP_over_InfiniBand_.28IPoIB.29) for using IPoIB instead of RDMA.

*   Check your link speeds. Run [ibstat](#ibstat_-_View_a_computer.27s_InfiniBand_GUIDs), [iblinkinfo](#iblinkinfo_-_View_link_information_on_InfiniBand_network), or examine the /sys filesystem.

 `$ ibstat`  `(look at the Rate shown on the port you are using.)` 

-and/or-

 `# iblinkinfo`  `(look at the middle part formatted like "4X     5.0 Gbps")` 

-and/or-

 `$ cat /sys/class/infiniband/<kernel module>/ports/<port number>/rate`  `20 Gb/sec (4X DDR)` 

Does this match your expected [bandwidth and number of virtual lanes](#Bandwidth)?

*   Check diagnostic information for entire subnet. Run [#ibdiagnet - Show diagnostic information for entire subnet](#ibdiagnet_-_Show_diagnostic_information_for_entire_subnet). Make sure to use `-ls` with [the proper signaling rate, which is likely the advertised speed of your card divided by 4](#Bandwidth).

```
# ibdiagnet -lw <expected number of virtual lanes -ls <expected signaling rate> -c 1000

```

*   Consider [upgrading firmware](#Upgrade_firmware).

## Network segmentation

An InfiniBand subnet can be partitioned for different customers or applications, giving security and quality of service guarantees. Each partition is identified by a PKEY (Partition Key.)

## How can I use libsdp for SDP (Sockets Direct Protocol)? =

Use [librdmacm](https://aur.archlinux.org/packages/librdmacm/)<sup><small>AUR</small></sup> instead. (When it started, it was called rsockets.)

librdmacm (and formerly libsdp) use `LD_PRELOAD` to intercept non-Infiniband programs' socket calls, and transparently (to the program) send them over RDMA over InfiniBand. That is, it can dramatically speed up programs built for TCP/IP, more than you can achieve by using them with IPoIB. It avoids the need to change a program's source code to work with InfiniBand, and can even be used on programs without the user having the source code. It does not work on programs that statically linked in socket libraries.

libsdp was deprecated. The ib_sdp kernel module is no longer maintained or distributed.

Retrieved from "[https://wiki.archlinux.org/index.php?title=InfiniBand&oldid=414700](https://wiki.archlinux.org/index.php?title=InfiniBand&oldid=414700)"