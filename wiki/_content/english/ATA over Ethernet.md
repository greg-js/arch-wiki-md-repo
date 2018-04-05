From [w:ATA over Ethernet](https://en.wikipedia.org/wiki/ATA_over_Ethernet "w:ATA over Ethernet"):

	*ATA over Ethernet (AoE) is a network protocol developed by the Brantley Coile Company, designed for simple, high-performance access of SATA storage devices over Ethernet networks. It is used to build storage area networks (SANs) with low-cost, standard technologies.*

## Prequisites to AE

To use AOE you need the [AUR](/index.php/AUR "AUR") packages [vblade](https://aur.archlinux.org/packages/vblade/) and [aoetools](https://aur.archlinux.org/packages/aoetools/).

AoE does not use IPv4/IPv6; it works directly on top of Ethernet and is limited to the local subnet. It is enough to make sure that the interface is up. (For best performance, the subnet should use jumbo frames.)

```
# ip link set eth0 up

```

## Target: Export a disk

You can export block devices or image files using `vblade` or the `vbladed` daemon.

Create an empty disk image:

```
# dd if=/dev/zero of=vblade0 bs=1M count=256

```

Start `vblade` to export the disk over eth0:

```
# vblade 1 1 eth0 vblade0

```

Exported disks are identified by their "shelf ID" and "slot ID" (within that shelf), in this case `1.1`; the combination must be unique across the SAN.

## Initiator: Attach to a disk

Ensure the kernel module is loaded:

```
# modprobe aoe

```

By default all interfaces are used, but you can specify a whitelist either as `aoe` module parameter, or using the `aoe-interfaces` command:

```
# aoe-interfaces eth0

```

The kernel module performs periodic discovery; to do it immediately (e.g. after changing interfaces) use `aoe-discover`. Afterwards use `aoe-stat` to list "visible" disks.

```
# aoe-discover
# aoe-stat
     e1.1         0.001GB   eth0 up

```

The first column shows a device name which also can be found under `/dev/etherd` as a regular block device. You can partition it with fdisk, or just create a file system:

```
# mkfs.ext4 /dev/etherd/e1.1
# mkdir /mnt/e1.1
# mount /dev/etherd/e1.1 /mnt/e1.1

```