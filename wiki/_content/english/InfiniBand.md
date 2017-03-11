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
    *   [2.3 Network Management](#Network_Management)
*   [3 Installation](#Installation)
    *   [3.1 Upgrade firmware](#Upgrade_firmware)
        *   [3.1.1 For Mellanox](#For_Mellanox)
        *   [3.1.2 For Intel/QLogic](#For_Intel.2FQLogic)
    *   [3.2 Kernel modules](#Kernel_modules)
    *   [3.3 Subnet manager](#Subnet_manager)
        *   [3.3.1 Software subnet manager](#Software_subnet_manager)
*   [4 TCP/IP (IPoIB)](#TCP.2FIP_.28IPoIB.29)
    *   [4.1 Connection mode](#Connection_mode)
    *   [4.2 MTU](#MTU)
    *   [4.3 Finetuning connection mode and MTU](#Finetuning_connection_mode_and_MTU)
*   [5 Remote data storage](#Remote_data_storage)
    *   [5.1 targetcli](#targetcli)
        *   [5.1.1 Installing and using](#Installing_and_using)
        *   [5.1.2 Create backstores](#Create_backstores)
    *   [5.2 iSCSI](#iSCSI)
        *   [5.2.1 Over IPoIB](#Over_IPoIB)
        *   [5.2.2 Over iSER](#Over_iSER)
            *   [5.2.2.1 Configuring iSER devices](#Configuring_iSER_devices)
*   [6 Network segmentation](#Network_segmentation)
*   [7 SDP (Sockets Direct Protocol)](#SDP_.28Sockets_Direct_Protocol.29)
*   [8 Diagnosing and benchmarking](#Diagnosing_and_benchmarking)
    *   [8.1 ibstat - View a computer's IB GUIDs](#ibstat_-_View_a_computer.27s_IB_GUIDs)
    *   [8.2 ibhosts - View all hosts on IB network](#ibhosts_-_View_all_hosts_on_IB_network)
    *   [8.3 ibswitches - View all switches on IB network](#ibswitches_-_View_all_switches_on_IB_network)
    *   [8.4 iblinkinfo - View link information on IB network](#iblinkinfo_-_View_link_information_on_IB_network)
    *   [8.5 ibping - Ping another IB device](#ibping_-_Ping_another_IB_device)
    *   [8.6 ibdiagnet - Show diagnostic information for entire subnet](#ibdiagnet_-_Show_diagnostic_information_for_entire_subnet)
    *   [8.7 qperf - Measure performance over RDMA or TCP/IP](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP)
        *   [8.7.1 TCP/IP over IPoIB](#TCP.2FIP_over_IPoIB)
    *   [8.8 iperf - Measure performance over TCP/IP](#iperf_-_Measure_performance_over_TCP.2FIP)
*   [9 Common problems / FAQ](#Common_problems_.2F_FAQ)
    *   [9.1 Connection problems](#Connection_problems)
        *   [9.1.1 Link, physical state and port state](#Link.2C_physical_state_and_port_state)
        *   [9.1.2 getaddrinfo failed: Name or service not known](#getaddrinfo_failed:_Name_or_service_not_known)
    *   [9.2 Speed problems](#Speed_problems)

## Introduction

### Overview

InfiniBand (abbreviated IB) is an alternative to Ethernet and Fibre Channel. IB provides high bandwidth and low latency. IB can transfer data directly to and from a storage device on one machine to userspace on another machine, bypassing and avoiding the overhead of a system call. IB adapters can handle the networking protocols, unlike Ethernet networking protocols which are ran on the CPU. This allows the OS's and CPU's to remain free while the high bandwidth transfers take place, which can be a real problem with 10Gb+ Ethernet.

IB hardware is made by Mellanox (which merged with Voltaire, and is heavily backed by Oracle) and Intel (which acquired QLogic's IB division in 2012). IB is most often used by supercomputers, clusters, and data centers. IBM, HP, and Cray are also members of the InfiniBand Steering Committee. Facebook, Twitter, eBay, YouTube, and PayPal are examples of IB users.

IB software is developed under the [OpenFabrics Open Source Alliance](https://www.openfabrics.org/)

### Affordable used equipment

With large businesses benefiting so much from jumping to newer versions, the maximum length limitations of passive IB cabling, the high cost of active IB cabling, and the more technically complex setup than Ethernet, the used IB market is heavily saturated, allowing used IB devices to affordably be used at home or smaller businesses for their internal networks.

### Bandwidth

#### Signal transfer rates

IB transfer rates now correspond to the maximum supported by PCI Express (abbreviated PCIe). It originally corresponded to PCI Extended (abbreviated PCI-X), which severely limited performance. It launched using SDR (Single Data Rate) with a signaling rate of 2.5Gb/s per lane (corresponding with PCI Express v1.0), and has added: DDR (Double Data Rate) at 5Gb/s (PCI Express v2.0); QDR (Quad Data Rate) at 10Gb/s (PCI Express 3.0); and FDR (Fourteen Data Rate) at 14.0625Gbps (PCI Express 4.0.) IB is now delivering EDR (Enhanced Data Rate) at 25Gb/s. Planned around 2017 will be HDR (High Data Rate) at 50Gb/s.

#### Effective throughput & multiple virtual lanes

Because SDR, DDR, and QDR versions use 8/10 encoding (8 bits of data takes 10 bits of signaling), effective throughput for these is lowered to 80%: SDR at 2Gb/s/lane; DDR at 4Gb/s/lane; and QDR at 8Gb/s/lane. Starting with FDR, IB uses 64/66 encoding, allowing a higher effective throughput to signaling rate ratio of 96.97%: FDR at 13.64Gb/s/lane; EDR at 24.24Gb/s/lane; and HDR at 48.48Gb/s/lane.

IB devices are capable of using multiple virtual lanes, most using 4X, but some using a slower 1X or faster 12X.

When using the common 4X lane devices, this effectively allows total effective throughputs of: SDR of 8Gb/s; DDR of 16Gb/s; QDR of 32Gb/s; FDR of 54.54Gb/s; EDR of 96.97Gb/s; and HDR of 193.94Gb/s.

### Latency

IB's latency is incredibly small: SDR (5us); DDR (2.5us); QDR (1.3us); FDR (0.7us); EDR (0.5us); and HDR (< 0.5us). For comparison 10Gb Ethernet is more like 7.22us, ten times more than FDR's latency.

### Backwards compatibility

IB devices are almost always backwards compatible. Connections should be established at the lowest common denominator. A DDR adapter meant for a PCI Express 8x slot should work in a PCI Express 4x slot (with half the bandwidth).

### Cables

IB passive copper cables can be up to 7 meters using up to QDR, and 3 meters using FDR.

IB active fiber (optical) cables can be up to 300 meters using up to FDR (only 100 meters on FDR10).

Mellanox MetroX devices exist which allow up to 80 kilometer connections. Latency increases by about 5us per kilometer.

An IB cable can be used to directly link two computers without a switch; IB cross-over cables do not exist.

## Terminology

### Hardware

Adapters, switches, routers, and bridges/gateways must be specifically made for IB.

	HCA (Host Channel Adapter)

	Like an Ethernet NIC (Network Interface Card). Connects the IB cable to the PCI Express bus, at the full speed of the bus if the proper generation of HCA is used. An end node on an IB network, executes transport-level functions, and supports the IB verbs interface.

	Switch

	Like an Ethernet NIC. Moves packets from one link to another on the same IB subnet.

	Router

	Like an Ethernet router. Moves packets between different IB subnets.

	Bridge/Gateway

	A standalone piece of hardware, or a computer performing this function. Bridges IB and Ethernet networks.

### GUID

Like Ethernet MAC addresses, but a device has multiple GUID's. Assigned by the hardware manufacturer, and remains the same through reboots. 64-bit addresses (24-bit manufacturer prefix and 40-bit device identifier). Given to adapters, switches, routers, and bridges/gateways.

	Node GUID

	Identifies the HCA, Switch, or Router

	Port GUID

	Identifies a port on a HCA, Switch, or Router (even a HCA often has multiple ports)

	System GUID

	Allows treating multiple GUIDs as one entity

	LID (Local IDentifier)

	16-bit addresses, assigned by the Subnet Manager when picked up by the Subnet Manager. Used for routing packets. Not persistent through reboots.

### Network Management

	SM (Subnet Manager)

	Actively manages an IB subnet. Can be implemented as a software program on a computer connected to the IB network, built in to an IB switch, or as a specialized IB device. Initializes and configures everything else on the subnet, including assigning LIDs (Local IDentifiers). Establishes traffic paths through the subnet. Isolates faults. Prevents unauthorized Subnet Managers. You can have multiple switches all on one subnet, under one Subnet Manager. You can have redundant Subnet Managers on one subnet, but only one can be active at a time.

	MAD (MAnagement Datagram)

	Standard message format for subnet manager to and from IB device communication, carried by a UD (Unreliable Datagram).

	UD (Unreliable Datagram)

## Installation

First install [rdma-core](https://aur.archlinux.org/packages/rdma-core/) which contains all core libraries and daemons.

### Upgrade firmware

Running the most recent firmware can give significant performance increases, and fix connectivity issues.

**Warning:** Be careful or the device may be bricked!

#### For Mellanox

*   Install [mstflint](https://aur.archlinux.org/packages/mstflint/)
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
    *   Visit [Mellanox's firmware download page](http://www.mellanox.com/page/firmware_download) (this guide incorporates this link's "firmware burning instructions", using its mstflint option)
    *   Choose the category of device you have
    *   Locate your device's PSID on their list, that mstflint gave you
    *   Examine the Firmware Image filename to see if it's more recent than your adapter's FW Version, i.e. `fw-25408-2_9_1000-MHGH28-XTC_A1.bin.zip`, is version `2.9.1000`
*   If there's a more recent version, download new firmware and burn it to your adapter

```
$ unzip <*firmware .bin.zip file name*>
# mstflint -d <*adapter PCI device ID*> -i <*firmware .bin file name*> burn

```

#### For Intel/QLogic

Search for the model number (or a substring) over at [Intel Download Center](https://downloadcenter.intel.com/) and follow the instructions. The downloaded software will probably need to be run from RHEL/CentOS or SUSE/OpenSUSE.

### Kernel modules

Edit `/etc/rdma/rdma.conf` to your liking and [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `rdma.service`.

**Note:** [Due to how the kernel stacks are handled](https://bugzilla.redhat.com/show_bug.cgi?id=965829), changes to `/etc/rdma/rdma.conf` only take effect max once every boot, when `rdma.service` is started for first time. Restarting `rdma.service` has no effect.

### Subnet manager

Each IB network requires at least one subnet manager. Without one, devices may show having a link, but will never change state from `Initializing` to `Active`. A subnet manager often (typically every 5 or 30 seconds) checks the network for new adapters and adds them to the routing tables. If you have an IB switch with an embedded subnet manager, you can use that, or you can keep it disabled and use a software subnet manager instead. Dedicated IB subnet manager devices also exist.

#### Software subnet manager

On one system:

*   Install [opensm](https://aur.archlinux.org/packages/opensm/)
*   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `opensm.service`

All of your connected IB ports should now be in a (port) state of `Active`, and a physical state of `LinkUp`. You can check this by running [ibstat](#ibstat_-_View_a_computer.27s_IB_GUIDs) from [infiniband-diags](https://aur.archlinux.org/packages/infiniband-diags/):

 `$ ibstat` 
```
... (look at the ports shown you expect to be connected)
State: Active
Physical state: LinkUp
...
```

Or by examining the `/sys` filesystem:

 `$ cat /sys/class/infiniband/*kernel_module*/ports/*port_number*/phys_state`  `5: LinkUp`  `$ cat /sys/class/infiniband/*kernel_module*/ports/*port_number*/state`  `4: ACTIVE` 

## TCP/IP (IPoIB)

You can create a virtual Ethernet Adapter that runs on the HCA. This is intended so programs designed to work with TCP/IP but not IB, can (indirectly) use IB networks. Performance is negatively affected due to sending all traffic through the normal TCP stack; requiring system calls, memory copies, and network protocols to run on the CPU rather than on the HCA.

Configure the IB interface(s) (e.g. `ib0`), [like traditional Ethernet adapters](/index.php/Network_configuration "Network configuration").

### Connection mode

IPoIB can run in datagram (default) or connected mode. Connected mode [allows you to set a higher MTU](#Finetuning_connection_mode_and_MTU), but does increase TCP latency for short messages by about 5% more than datagram mode.

To see the current mode used:

```
$ cat /sys/class/net/*interface*/mode

```

### MTU

In datagram mode, UD (Unreliable Datagram) transport is used, which typically forces the MTU to be 2044 bytes. Technically to the IB L2 MTU - 4 bytes for the IPoIB encapsulation header, which is usually 2044 bytes.

In connected mode, RC (Reliable Connected) transport is used, which allows a MTU up to the maximum IP packet size, 65520 bytes.

To see your MTU:

```
$ ip link show *interface*

```

### Finetuning connection mode and MTU

You only need `ipoibmodemtu` if you want to change the default connection mode and/or MTU.

*   [Install and set up TCP/IP over IB (IPoIB)](#TCP.2FIP_.28IPoIB.29)
*   Install [ipoibmodemtu](https://aur.archlinux.org/packages/ipoibmodemtu/)
*   Configure `ipoibmodemtu` through `/etc/ipoibmodemtu.conf`, which contains instructions on how to do so
    *   It defaults to setting a single IB port `ib0` to `connected` mode and MTU `65520`
*   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `ipoibmodemtu.service`

Different setups will see different results. Some people see a gigantic (double+) speed increase by usign `connected` mode and MTU `65520`, and a few see about the same or even worse speeds. Use [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) and [iperf](#iperf_-_Measure_performance_over_TCP.2FIP) to finetune your system.

Using the [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) examples given in this article, here are example results from an SDR network (8 theoretical Gb/s) with various finetuning:

| Mode | MTU | MB/s | us latency |
| datagram | 2044 | 707 | 19.4 |
| connected | 2044 | 353 | 18.9 |
| connected | 65520 | 726 | 19.6 |

**Tip:** Use the same connection and MTU settings for the entire subnet. Mixing and matching doesn't work optimally.

## Remote data storage

You can share physical or virtual devices from a target (host/server) to an initiator (guest/client) system over an IB network, using iSCSI, iSCSI with iSER, or SRP. These methods differ from traditional file sharing (i.e. [Samba](/index.php/Samba "Samba") or [NFS](/index.php/NFS "NFS")) because the initiator system views the shared device as its own block level device, rather than a traditionally mounted network shared folder. i.e. `fdisk /dev/*block_device_id*`, `mkfs.btrfs /dev/*block_device_id_with_partition_number*`

The disadvantage is only one system can use each shared device at a time; trying to mount a shared device on the target or another initiator system will fail (an initiator system can certainly run traditional file sharing on top).

The advantages are faster bandwidth, more control, and even having an initiator's root filesystem being physically located remotely (remote booting).

### targetcli

`targetcli` acts like a shell that presents its complex (and not worth creating by hand) `/etc/target/saveconfig.json` as a pseudo-filesystem.

#### Installing and using

On the target system:

*   Install [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/)
*   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `target.service`

In `targetcli`:

*   In any pseudo-directory, you can run `help` to see the commands available *in that pseudo-directory* or `help *command*` (like `help create`) for more detailed help
*   Tab-completion is also available for many commands
*   Run `ls` to see the entire pseudo-filesystem at and below the current pseudo-directory

#### Create backstores

In `targetcli`, setup a backstore for each device or virtual device to share:

*   To share an actual block device, run: `cd /backstores/block`; and `create *name* *dev*`
*   To share a file as a virtual block device, run: `cd /backstores/fileio`; and `create *name* *file*`
*   To share a physical SCSI device as a pass-through, run: `cd /backstores/pscsi`; and `create *name* *dev*`
*   To share a RAM disk, run: `cd /backstores/ramdisk`; and `create *name* *size*`
*   Where *name* is for the backstore's name
*   Where *dev* is the block device to share (i.e. `/dev/sda`, `/dev/sda4`, `/dev/disk/by-id/*XXX*`, or a LVM logical volume `/dev/vg0/lv1`)
*   Where *file* is the file to share (i.e. `/path/to/file`)
*   Where *size* is the size of the RAM disk to create (i.e. 512MB, 20GB)

### iSCSI

iSCSI allows storage devices and virtual storage devices to be used over a network. For IB networks, the storage can either work over IPoIB or iSER.

There is a lot of overlap with the [iSCSI Target](/index.php/ISCSI_Target "ISCSI Target"), [iSCSI Initiator](/index.php/ISCSI_Initiator "ISCSI Initiator"), and [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot") articles, but the necessities will be discussed since much needs to be customized for usage over IB.

#### Over IPoIB

Perform the target system instructions first, which will direct you when to temporarily switch over to the initiator system instructions.

*   On the target and initiator systems, [install TCP/IP over IB](#TCP.2FIP_.28IPoIB.29)

*   On the target system, for each device or virtual device you want to share, in `targetcli`:
    *   [Create a backstore](#Create_backstores)
    *   For each backstore, create an IQN (iSCSI Qualified Name) (the name other systems' configurations will see the storage as)
        *   Run: `cd /iscsi`; and `create`. It will give you a *randomly_generated_target_name*, i.e. `iqn.2003-01.org.linux-iscsi.hostname.x8664:sn.3d74b8d4020a`
        *   Set up the TPG (Target Portal Group), automatically created in the last step as tpg1
            *   Create a lun (Logical Unit Number)
                *   Run: `cd *randomly_generated_target_name*/tpg1/luns`; and `create *storage_object*`. Where `*storage_object*` is a full path to an existing storage object, i.e. `/backstores/block/*name*`
            *   Create an acl (Access Control List)
                *   Run: `cd ../acls`; and `create *wwn*`, where `*wwn*` is the initiator system's IQN (iSCSI Qualified Name), aka its (World Wide Name)
                    *   Get the `*wwn*` by running on the initiator system, **not** this target system: (after installing on it [open-iscsi](https://www.archlinux.org/packages/?name=open-iscsi)) `cat /etc/iscsi/initiatorname.iscsi`
    *   Save and exit by running: `cd /`; `saveconfig`; and `exit`

*   On the initiator system:
    *   Install [open-iscsi](https://www.archlinux.org/packages/?name=open-iscsi)
    *   [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `open-iscsi.service`
    *   At this point, if you need this initiator system's IQN (iSCSI Qualified Name), aka its wwn (World Wide Name), for setting up the target system's `luns`, run: `cat /etc/iscsi/initiatorname.iscsi`
    *   Discover online targets. Run `iscsiadm -m discovery -t sendtargets -p *portal*`, where *portal* is an IP (v4 or v6) address or hostname
    *   Login to discovered targets. Run `iscsiadm -m node -L all`
    *   View which block device ID was given to each target logged into. Run `iscsiadm -m session -P 3 | grep Attached`. The block device ID will be the last line in the tree for each target (`-P` is the print command, its option is the verbosity level, and only level 3 lists the block device IDs)

#### Over iSER

iSER (iSCSI Extensions for RDMA) takes advantage of IB's RDMA protocols, rather than using TCP/IP. It eliminates TCP/IP overhead, and provides higher bandwidth, zero copy time, lower latency, and lower CPU utilization.

##### Configuring iSER devices

Follow the [iSCSI Over IPoIB](#Over_IPoIB) instructions, with the following changes:

*   If you wish, instead of [installing IPoIB](#TCP.2FIP_.28IPoIB.29), you can just [install RDMA for loading kernel modules](#Kernel_modules)
*   On the target system, after everything else is setup, while still in `targetcli`, enable iSER on the target:
    *   Run `cd /iscsi/*iqn*/tpg1/portals/0.0.0.0:3260` for each *iqn* you want to have use iSER rather than IPoIB
        *   Where *iqn* is the randomly generated target name, i.e. `iqn.2003-01.org.linux-iscsi.hostname.x8664:sn.3d74b8d4020a`
    *   Run `enable_iser true`
    *   Save and exit by running: `cd /`; `saveconfig`; and `exit`
*   On the initiator system, when running `iscsiadm` to discover online targets and login to them, use the additional argument `-I iser`

## Network segmentation

An IB subnet can be partitioned for different customers or applications, giving security and quality of service guarantees. Each partition is identified by a PKEY (Partition Key).

## SDP (Sockets Direct Protocol)

Use `librdmacm` (successor to rsockets and libspd) and `LD_PRELOAD` to intercept non-IB programs' socket calls, and transparently (to the program) send them over IB via RDMA. Dramatically speeding up programs built for TCP/IP, much more than can be achieved by using IPoIB. It avoids the need to change the program's source code to work with IB and can even be used for closed source programs. It does not work for programs that statically link in socket libraries.

## Diagnosing and benchmarking

### ibstat - View a computer's IB GUIDs

ibstat will show you detailed information about each IB adapter in the computer it is ran on, including: model number; number of ports; firmware and hardware version; node, system image, and port GUIDs; and port state, physical state, rate, base lid, lmc, SM lid, capability mask, and link layer.

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

This example shows a Mellanox Technologies (MT) adapter. Its PCI Device ID is reported (25418), rather than the model number of part number. It shows a state of "Active", which means is it properly connected to a subnet manager. It shows a physical state of "LinkUp", which means it has an electrical connection via cable, but is not necessarily properly connected to a subnet manager. It shows a total rate of 20 Gb/s (which for this card is from a 5.0 Gb/s signaling rate and 4 virtual lanes). It shows the subnet manager assigned the port a lid of 3.

### ibhosts - View all hosts on IB network

ibhosts will show you the Node GUIDs, number of ports, and device names, for each host on the IB network.

 `# ibhosts` 
```
Ca      : 0x0002c90300002778 ports 2 "MT25408 ConnectX Mellanox Technologies"
Ca      : 0x0002c90300002f78 ports 2 "hostname mlx4_0"
```

### ibswitches - View all switches on IB network

ibswitches will show you the Node GUIDs, number of ports, and device names, for each switch on the IB network. If you are running with direct connections only, it will show nothing.

```
# ibswitches

```

### iblinkinfo - View link information on IB network

iblinkinfo will show you the device names, Port GUIDs, number of virtual lanes, [signal transfer rates](#Signal_transfer_rates), state, physical state, and what it is connected to.

 `# iblinkinfo` 
```
CA: MT25408 ConnectX Mellanox Technologies:
      0x0002c90300002779      4    1[  ] ==( 4X           5.0 Gbps Active/  LinkUp)==>       3    1[  ] "kvm mlx4_0" ( )
CA: hostname mlx4_0:
      0x0002c90300002f79      3    1[  ] ==( 4X           5.0 Gbps Active/  LinkUp)==>       4    1[  ] "MT25408 ConnectX Mellanox Technologies" ( )
```

This example shows two adapters directly connected with out a switch, using a 5.0 Gb/s [signal transfer rate](#Signal_transfer_rates), and 4 virtual lanes (4X).

### ibping - Ping another IB device

ibping will attempt pinging another IB GUID. ibping must be ran in server mode on one computer, and in client mode on another.

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

If you're running IPoIB, you can use regular `ping` which pings through the TCP/IP stack. ibping uses IB interfaces, and does not use the TCP/IP stack.

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

iperf is not an IB aware program, and is meant to test over TCP/IP or UDP. Even though [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) can test your IB TCP/IP performace using IPoIB, iperf is still another program you can use.

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

#### Link, physical state and port state

*   See if the IB hardware modules are recognized by the system.

 `$ dmesg | egrep -i "Mellanox|InfiniBand|QLogic|Voltaire" # If you have an Intel adapter, you'll have to use Intel here and look through a few lines if you have other Intel hardware` 
```
[    6.287556] mlx4_core: Mellanox ConnectX core driver v2.2-1 (Feb, 2014)
[    8.686257] <mlx4_ib> mlx4_ib_add: mlx4_ib: Mellanox ConnectX InfiniBand driver v2.2-1 (Feb 2014)
```
 `$ ls -l /sys/class/infiniband`  `mlx4_0 -> ../../devices/pci0000:00/0000:00:03.0/0000:05:00.0/infiniband/mlx4_0` 

If nothing is shown, your kernel isn't recognizing your adapter. This example shows approximately what you will see if you have a Mellanox ConnectX adapter, which uses the mlx4_0 kernel module.

*   Check the port and physical states. Either run [ibstat](#ibstat_-_View_a_computer.27s_IB_GUIDs) or examine `/sys`.

 `$ ibstat`  `(look at the port shown that you expect to be connected)` 

or

 `$ cat /sys/class/infiniband/<kernel module>/ports/<port number>/phys_state`  ` 5: LinkUp`  `$ cat /sys/class/infiniband/<kernel module>/ports/<port number>/state`  ` 4: ACTIVE` 

The physical state should be "LinkUp". If it isn't, your cable likely isn't plugged in, isn't connected to anything on the other end, or is defective. The (port) state should be "Active". If it's "Initializing" or "INIT", your [subnet manager](#Subnet_manager) doesn't exist, isn't running, or hasn't added the port to the network's routing tables.

*   Can you successfully [ibping](#ibping_-_Ping_another_IB_device) which uses IB directly, rather than IPoIB? Can you successfully `ping`, if you are running IPoIB?

*   Consider [upgrading firmware](#Upgrade_firmware).

#### getaddrinfo failed: Name or service not known

*   Run [ibhosts](#ibhosts_-_View_all_hosts_on_IB_network) to see the CA names at the end of each line in quotes.

### Speed problems

*   Start by double-checking your expectations.

How have you determined you have a speed problem? Are you using [qperf](#qperf_-_Measure_performance_over_RDMA_or_TCP.2FIP) or [iperf](#iperf_-_Measure_performance_over_TCP.2FIP), which both transmit data to and from memory rather than hard drives. Or, are you benchmarking actual file transfers, which relies on your hard drives? Unless you're running RAID to boost speed, even with the fastest SSD's available in mid 2015, a single hard drive (or sometimes even multiple ones) will be bottlenecking your IB transfer speeds. Are you using RDMA or TCP/IP via IPoIB? If so, [there is a performance hit](#TCP.2FIP_.28IPoIB.29) for using IPoIB instead of RDMA.

*   Check your link speeds. Run [ibstat](#ibstat_-_View_a_computer.27s_IB_GUIDs), [iblinkinfo](#iblinkinfo_-_View_link_information_on_IB_network), or examine `/sys`.

 `$ ibstat`  `(look at the Rate shown on the port you are using)` 

or

 `# iblinkinfo`  `(look at the middle part formatted like "4X     5.0 Gbps")` 

or

 `$ cat /sys/class/infiniband/<kernel module>/ports/<port number>/rate`  `20 Gb/sec (4X DDR)` 

Does this match your expected [bandwidth and number of virtual lanes](#Bandwidth)?

*   Check diagnostic information for entire subnet. Run [#ibdiagnet - Show diagnostic information for entire subnet](#ibdiagnet_-_Show_diagnostic_information_for_entire_subnet). Make sure to use `-ls` with [the proper signaling rate, which is likely the advertised speed of your card divided by 4](#Bandwidth).

```
# ibdiagnet -lw <expected number of virtual lanes -ls <expected signaling rate> -c 1000

```

*   Consider [upgrading firmware](#Upgrade_firmware).