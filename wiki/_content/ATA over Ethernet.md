# ATA over Ethernet

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

ATA over Ethernet (AoE) is a network protocol developed by the Brantley Coile Company, designed for simple, high-performance access of SATA storage devices over Ethernet networks. It is used to build storage area networks (SANs) with low-cost, standard technologies.

## Contents

*   [1 Prequisites to AOE](#Prequisites_to_AOE)
*   [2 Start Vblade](#Start_Vblade)
    *   [2.1 Testing Local](#Testing_Local)
*   [3 Using AOE](#Using_AOE)

## Prequisites to AOE

To use AOE you need the [AUR](/index.php/AUR "AUR") packages [vblade](https://aur.archlinux.org/packages/vblade/)<sup><small>AUR</small></sup> and [aoetools](https://aur.archlinux.org/packages/aoetools/)<sup><small>AUR</small></sup>.

```
# ip set link eth0 up

```

**Note:** AOE is working without IP Adress

Create a Disk with dd:

```
# dd if=/dev/zero of=vblade0 count=1 bs=1M

```

## Start Vblade

```
# vblade 1 1 eth0 vblade0 

```

**Note:** You can use the vbladed Daemon instead of vblade

Now a Client should be able to see the ATA-Drive

### Testing Local

To test the setup localy you have to assign vblade to lo

```
# modprobe aoe
# vblade 1 1 lo vblade0 &
# aoe-interfaces eth0
# aoe-discover
# aoe-stat
     e1.1         0.001GB   eth0 up

```

## Using AOE

```
# modprobe aoe
# aoe-interfaces eth0
# aoe-discover
# aoe-stat
    e1.1         0.001GB   eth0 up

```

Now the device can be used as a normal device. It will also show up in fdisk! So first make a file system:

```
# mkfs.ext4 /dev/ethered/e1.1
# mkdir /mnt/e1.1
# mount /dev/etherd/e1.1 /mnt/e1.1

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ATA_over_Ethernet&oldid=308260](https://wiki.archlinux.org/index.php?title=ATA_over_Ethernet&oldid=308260)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Storage](/index.php/Category:Storage "Category:Storage")
*   [Networking](/index.php/Category:Networking "Category:Networking")