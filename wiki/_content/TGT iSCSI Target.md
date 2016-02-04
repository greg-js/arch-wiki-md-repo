# TGT iSCSI Target

The [TGT SCSI framework](http://stgt.sourceforge.net) can be used for several storage protocols. This document describes the usage of TGT as iSCSI target.

## Contents

*   [1 About TGT](#About_TGT)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
*   [4 Example configuration](#Example_configuration)
*   [5 Start](#Start)
*   [6 See also](#See_also)

## About TGT

STGT was introduced into the Linux kernel at the end of 2006 by Fujita Tomonori. It has a library in the kernel which assists the in-kernel target drivers. All target processing happens in user space. At the end of 2010, the LIO project was chosen to replace STGT as the in-kernel SCSI target implementation. When LIO was chosen to replace STGT, its implementation has been adapted to allow STGT userspace modules to continue functioning, therefore the STGT community has supported the LIO inclusion in the kernel.

Advantages:

*   active development
*   simplicity
*   support for iSCSI for Ethernet NICs, iSER, virtual SCSI target driver for IBM pSeries
*   supports virtual disks, DVDs, VTLs, RADOS block devices (rbd)
*   supports SCSI UNMAP

As a disadvantage some developers and users have argued that because the target processing happens in user space, in some cases this may lead to performance bottlenecks. However, using 'aio' type LUNs gives a huge performance boost. AIO should only be used in environments that are safe against power loss.

## Installation

Install the [tgt](https://aur.archlinux.org/packages/tgt/) package. If you want to use the direct store, then [sg3_utils](https://www.archlinux.org/packages/?name=sg3_utils) must also be installed.

Using direct-store, the properties of the physical device will be available for the initiator and target.

Please notice, if you're using a [Firewall](/index.php/Firewall "Firewall"), tcp port 3260 should be open.

## Configuration

The configuration can be done:

*   using the `tgtadm` utility, afterwards you can use `tgt-admin --dump` to save the configuration. `tgt-admin` is a Perl script that parses `/etc/tgt/targets.conf` and configures tgt. You can find this method in the [Scsi-target-utils Quickstart Guide](http://fedoraproject.org/wiki/Scsi-target-utils_Quickstart_Guide), as linked from the [TGT website](http://stgt.sourceforge.net).
*   editing the /etc/tgt/targets.conf file. STGT supports multiple configurations. Include other config files in the main configuration file: `include /etc/tgt/*.conf`
*   manual configuration:

Create a target:

```
tgtadm --lld iscsi --op new --mode target --tid <unique target ID> -T <unique iSCSI iqn>

```

Allow only connection from specific initiators:

```
tgtadm --lld iscsi --op bind --mode target --tid <target ID> --initiator-name <initiator IQN>

```

or using the initiator IP:

```
tgtadm --lld iscsi --op bind --mode target --tid <target ID> --initiator-address <initiator IP>

```

Map a LUN to the target:

```
tgtadm --lld iscsi --op new --mode logicalunit --tid <target ID> --lun <unique LUN ID> -b /path_to/lun.img

```

LUN ID must be a non-zero decimal value. LUN 0 is reserved for the target controller.

For ESXi it is very important to map LUNs with persistent LUN IDs. If the LUN on the storage system changes its ID, ESXi will not be able to automatically remount it, and will trigger a PDL condition. Use direct-store instead of backing-store to define LUN IDs which will be persistent across reboots.

View current configuration:

```
tgtadm --op show --mode target --tid <target ID>
MaxRecvDataSegmentLength=8192
HeaderDigest=None
DataDigest=None
InitialR2T=Yes
MaxOutstandingR2T=1
ImmediateData=Yes
FirstBurstLength=65536
MaxBurstLength=262144
DataPDUInOrder=Yes
DataSequenceInOrder=Yes
ErrorRecoveryLevel=0
IFMarker=No
OFMarker=No
DefaultTime2Wait=2
DefaultTime2Retain=20
OFMarkInt=Reject
IFMarkInt=Reject
MaxConnections=1
RDMAExtensions=Yes
TargetRecvDataSegmentLength=262144
InitiatorRecvDataSegmentLength=262144
MaxOutstandingUnexpectedPDUs=0
MaxXmitDataSegmentLength=8192
MaxQueueCmd=128

```

Save configuration:

```
tgt-admin --dump > /etc/tgt/targets.conf

```

Reload configuration:

```
tgt-admin --update ALL

```

This command only updates targets that are not in use. Use '--force' to update targets that are in use.

## Example configuration

```
<target iqn.2004-01.nl.xtg:iscsi-server1>
 direct-store /dev/sdb
 write-cache on
 initiator-address ALL
 incominguser user password
 scsi_id 00010001
 vendor_id XTG
 lun 12
</target>

```

```
MaxRecvDataSegmentLength 131072
MaxXmitDataSegmentLength 131072
MaxBurstLength 262144
FirstBurstLength 262144
TargetRecvDataSegmentLength=262144
InitiatorRecvDataSegmentLength=262144
MaxOutstandingUnexpectedPDUs=0
MaxOutstandingR2T=1
MaxCommands=128

```

In the first part of this example, /dev/sdb will be mapped as LUN 12 and chap authentication is configured. In the second part are some [iSCSI advanced parameters](http://www.ietf.org/rfc/rfc3720.txt)

## Start

STGT can be [started/enabled](/index.php/Started/enabled "Started/enabled") with the `tgtd.service` unit.

You can check if everything works as expected:

```
tgt-admin -s

```

## See also

*   [Quickstart Guide for STGT for Fedora](https://fedoraproject.org/wiki/Scsi-target-utils_Quickstart_Guide)
*   [Configuration File Guide](http://wpkg.org/TGT-admin)

Retrieved from "[https://wiki.archlinux.org/index.php?title=TGT_iSCSI_Target&oldid=403805](https://wiki.archlinux.org/index.php?title=TGT_iSCSI_Target&oldid=403805)"