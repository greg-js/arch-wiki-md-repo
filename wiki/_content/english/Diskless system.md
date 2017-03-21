From [Wikipedia:Diskless node](https://en.wikipedia.org/wiki/Diskless_node "wikipedia:Diskless node")

	*A diskless node (or diskless workstation) is a workstation or personal computer without disk drives, which employs network booting to load its operating system from a server.*

## Contents

*   [1 Server configuration](#Server_configuration)
    *   [1.1 DHCP](#DHCP)
    *   [1.2 TFTP](#TFTP)
    *   [1.3 Network storage](#Network_storage)
        *   [1.3.1 NFS](#NFS)
        *   [1.3.2 NBD](#NBD)
*   [2 Client installation](#Client_installation)
    *   [2.1 Directory setup](#Directory_setup)
    *   [2.2 Bootstrapping installation](#Bootstrapping_installation)
        *   [2.2.1 NFS](#NFS_2)
        *   [2.2.2 NBD](#NBD_2)
*   [3 Client configuration](#Client_configuration)
    *   [3.1 Bootloader](#Bootloader)
        *   [3.1.1 GRUB](#GRUB)
        *   [3.1.2 Pxelinux](#Pxelinux)
    *   [3.2 Additional mountpoints](#Additional_mountpoints)
        *   [3.2.1 NBD root](#NBD_root)
        *   [3.2.2 Program state directories](#Program_state_directories)
*   [4 Client boot](#Client_boot)
    *   [4.1 NBD](#NBD_3)
*   [5 See also](#See_also)

## Server configuration

First of all, we must install the following components:

*   A [DHCP](/index.php/Dhcpd "Dhcpd") server to assign IP addresses to our diskless nodes.
*   A [TFTP](/index.php/TFTP "TFTP") server to transfer the boot image (a requirement of all PXE option roms).
*   A form of network storage ([NFS](/index.php/NFS "NFS") or NBD) to export the Arch installation to the diskless node.

**Note:** [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) is capable of simultaneously acting as both DHCP and TFTP server. For more information, see the [dnsmasq](/index.php/Dnsmasq "Dnsmasq") article.

### DHCP

Install ISC [dhcp](https://www.archlinux.org/packages/?name=dhcp) and configure it:

 `/etc/dhcpd.conf` 
```
allow booting;
allow bootp;

authoritative;

option domain-name-servers 10.0.0.1;

option architecture code 93 = unsigned integer 16;

group {
    next-server 10.0.0.1;

    if option architecture = 00:07 {
        filename "/grub/x86_64-efi/core.efi";
    } else {
        filename "/grub/i386-pc/core.0";
    }

    subnet 10.0.0.0 netmask 255.255.255.0 {
        option routers 10.0.0.1;
        range 10.0.0.128 10.0.0.254;
    }
}
```

**Note:** `next-server` should be the address of the TFTP server; everything else should be changed to match your network

RFC 4578 defines the "Client System Architecture Type" dhcp option. In the above configuration, if the PXE client requests an x86_64-efi binary (type 0x7), we appropriately give them one, otherwise falling back to the legacy binary. This allows both UEFI and legacy BIOS clients to boot simultaneously on the same network segment.

Start ISC DHCP [systemd](/index.php/Systemd "Systemd") service.

### TFTP

The TFTP server will be used to transfer the bootloader, kernel, and initramfs to the client.

Set the TFTP root to `/srv/arch/boot`. See [Tftpd server](/index.php/Tftpd_server "Tftpd server") for installation and configuration.

### Network storage

The primary difference between using NFS and NBD is while with both you can in fact have multiple clients using the same installation, with NBD (by the nature of manipulating a filesystem directly) you will need to use the `copyonwrite` mode to do so, which ends up discarding all writes on client disconnect. In some situations however, this might be highly desirable.

#### NFS

Install [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) on the server.

You will need to add the root of your Arch installation to your [NFS](/index.php/NFS "NFS") exports:

 `/etc/exports` 
```
/srv       *(rw,fsid=0,no_root_squash,no_subtree_check)
/srv/arch  *(rw,no_root_squash,no_subtree_check)
```

Next, start NFS services: `rpc-idmapd` `rpc-mountd`.

#### NBD

Install [nbd](https://www.archlinux.org/packages/?name=nbd) and configure it.

 `# vim /etc/nbd-server/config` 
```
[generic]
    user = nbd
    group = nbd
[arch]
    exportname = /srv/arch.img
    copyonwrite = false
```

**Note:** Set `copyonwrite` to true if you want to have multiple clients using the same NBD share simultaneously; refer to `man 5 nbd-server` for more details.

Start `nbd` systemd service.

## Client installation

Next we will create a full Arch Linux installation in a subdirectory on the server. During boot, the diskless client will get an IP address from the DHCP server, then boot from the host using PXE and mount this installation as its root.

### Directory setup

Create a [sparse file](https://en.wikipedia.org/wiki/Sparse_file "wikipedia:Sparse file") of at least 1 gigabyte, and create a btrfs filesystem on it (you can of course also use a real block device or [LVM](/index.php/LVM "LVM") if you so desire).

```
# truncate -s 1G /srv/arch.img
# mkfs.btrfs /srv/arch.img
# export root=/srv/arch
# mkdir -p "$root"
# mount -o loop,discard,compress=lzo /srv/arch.img "$root"

```

**Note:** Creating a separate filesystem is required for NBD but optional for NFS and can be skipped/ignored.

### Bootstrapping installation

Install [devtools](https://www.archlinux.org/packages/?name=devtools) and [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), and run `mkarchroot`.

```
# pacstrap -d "$root" base mkinitcpio-nfs-utils nfs-utils

```

**Note:** In all cases [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) is still required. `ipconfig` used in early-boot is provided only by the latter.

Now the initramfs needs to be constructed.

#### NFS

Trivial modifications to the `net` hook are required in order for NFSv4 mounting to work (not supported by `nfsmount`--the default for the `net` hook).

```
# sed s/nfsmount/mount.nfs4/ "$root/usr/lib/initcpio/hooks/net" > "$root/usr/lib/initcpio/hooks/net_nfs4"
# cp $root/usr/lib/initcpio/install/net{,_nfs4}

```

The copy of `net` is unfortunately needed so it does not get overwritten when [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) is updated on the client installation.

Edit `$root/etc/mkinitcpio.conf` and add `nfsv4` to `MODULES`, `net_nfs4` to `HOOKS`, and `/usr/bin/mount.nfs4` to `BINARIES`.

Next, we [chroot](/index.php/Chroot "Chroot") our installation and run *mkinitcpio*:

```
# arch-chroot "$root" mkinitcpio -p linux

```

#### NBD

The [mkinitcpio-nbd](https://aur.archlinux.org/packages/mkinitcpio-nbd/) package needs to be installed on the client. Build it with *makepkg* and install it:

```
# pacman --root "$root" --dbpath "$root/var/lib/pacman" -U mkinitcpio-nbd-0.4-1-any.pkg.tar.xz

```

You will then need to append `nbd` to your `HOOKS` array after `net`; `net` will configure your networking for you, but not attempt a NFS mount if `nfsroot` is not specified in the kernel line.

## Client configuration

In addition to the setup mentioned here, you should also set up your [hostname](/index.php/HOSTNAME#Set_the_host_name "HOSTNAME"), [timezone](/index.php/Timezone#Time_Zone "Timezone"), [locale](/index.php/Locale#Setting_the_system_locale "Locale"), and [keymap](/index.php/Keymap "Keymap"), and follow any other relevant parts of the [Installation guide](/index.php/Installation_guide "Installation guide").

### Bootloader

#### GRUB

Though poorly documented, GRUB supports being loaded via PXE.

```
# pacman --root "$root" --dbpath "$root/var/lib/pacman" -S grub

```

Create a grub prefix on the target installation for both architectures using `grub-mknetdir`.

```
# arch-chroot "$root" grub-mknetdir --net-directory=/boot --subdir=grub

```

Luckily for us, grub-mknetdir creates prefixes for all currently compiled/installed targets, and the [grub](https://www.archlinux.org/packages/?name=grub) maintainers were nice enough to give us both in the same package, thus grub-mknetdir only needs to be run once.

Now we create a trivial GRUB configuration:

 `# vim "$root/boot/grub/grub.cfg"` 
```
menuentry "Arch Linux" {
    linux /vmlinuz-linux quiet add_efi_memmap ip=:::::eth0:dhcp nfsroot=10.0.0.1:/arch
    initrd /initramfs-linux.img
}
```

[GRUB](/index.php/GRUB "GRUB") dark-magic will `set root=(tftp,10.0.0.1)` automatically, so that the kernel and initramfs are transferred via TFTP without any additional configuration, though you might want to set it explicitly if you have any other non-tftp menuentries.

**Note:** Modify your kernel line as-necessary, refer to [Pxelinux](/index.php/Syslinux#Pxelinux "Syslinux") for NBD-related options

#### Pxelinux

[Pxelinux](/index.php/Syslinux "Syslinux") is provided by [syslinux](https://www.archlinux.org/packages/?name=syslinux), see [here](/index.php/Syslinux#Pxelinux "Syslinux") for detail.

### Additional mountpoints

#### NBD root

In late boot, you will want to switch your root filesystem mount to both `rw`, and enable `compress=lzo`, for much improved disk performance in comparison to [NFS](/index.php/NFS "NFS").

 `# vim "$root/etc/fstab"`  `/dev/nbd0  /  btrfs  rw,noatime,discard,compress=lzo  0 0` 

#### Program state directories

You could mount `/var/log`, for example, as tmpfs so that logs from multiple hosts do not mix unpredictably, and do the same with `/var/spool/cups`, so the 20 instances of cups using the same spool do not fight with each other and make 1,498 print jobs and eat an entire ream of paper (or worse: toner cartridge) overnight.

 `# vim "$root/etc/fstab"` 
```
tmpfs   /var/log        tmpfs     nodev,nosuid    0 0
tmpfs   /var/spool/cups tmpfs     nodev,nosuid    0 0
```

It would be best to configure software that has some sort of state/database to use unique state/database storage directories for each host. If you wanted to run [puppet](http://puppetlabs.com/), for example, you could simply use the `%H` specifier in the puppet unit file:

 `# vim "$root/etc/systemd/system/puppetagent.service"` 
```
[Unit]
Description=Puppet agent
Wants=basic.target
After=basic.target network.target

[Service]
Type=forking
PIDFile=/run/puppet/agent.pid
ExecStartPre=/usr/bin/install -d -o puppet -m 755 /run/puppet
ExecStart=/usr/bin/puppet agent --vardir=/var/lib/puppet-%H --ssldir=/etc/puppet/ssl-%H

[Install]
WantedBy=multi-user.target
```

Puppet-agent creates vardir and ssldir if they do not exist.

If neither of these approaches are appropriate, the last sane option would be to create a [systemd generator](http://www.freedesktop.org/wiki/Software/systemd/Generators) that creates a mount unit specific to the current host (specifiers are not allowed in mount units, unfortunately).

## Client boot

### NBD

If you are using NBD, you will need to umount the `arch.img` before/while you boot your client.

This makes things particularly interesting when it comes to kernel updates. You cannot have your client filesystem mounted while you are booting a client, but that also means you need to use a kernel separate from your client filesystem in order to build it.

You will need to first copy `$root/boot` from the client installation to your tftp root (i.e. `/srv/boot`).

```
# cp -r "$root/boot" /srv/boot

```

You will then need to umount `$root` before you start the client.

```
# umount "$root"

```

**Note:** To update the kernel in this setup, you either need to mount `/srv/boot` using [NFS](/index.php/NFS "NFS") in [fstab](/index.php/Fstab "Fstab") on the client (prior to doing the kernel update) or mount your client filesystem after the client has disconnected from NBD

## See also

*   [kernel.org: Mounting the root filesystem via NFS (nfsroot)](https://www.kernel.org/doc/Documentation/filesystems/nfs/nfsroot.txt)
*   [syslinux.org: pxelinux FAQ](http://www.syslinux.org/wiki/index.php/PXELINUX)