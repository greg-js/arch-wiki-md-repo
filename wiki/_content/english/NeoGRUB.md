[NeoGRUB](https://neosmart.net/wiki/easybcd/neogrub/) is an implementation of GRUB4DOS provided by the [EasyBCD](https://neosmart.net/EasyBCD/) bootloader-configurator for Windows. When installed to the Windows bootloader (via Add New Entry - NeoGrub) from EasyBCD, it embeds an implementation of GRUB Legacy *inside the Windows Bootloader*. This implementation can boot Arch Linux and other Linuxes *directly, without chainloading a Linux bootloader installed on the linux's /boot.*

This can be helpful if you find that updates to Arch are breaking your Arch's [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux").

One caveat: NeoGRUB is only known to support the following filesystems: FAT16, FAT32, MINIX fs, ext2, ReiserFS, JFS, XFS that means that your /boot partition must be one of these filesystems if you use NeoGRUB. Your root partition and the others are not restricted to these filesystems.

When you install NeoGRUB to the windows bootloader, click Configure. A configuration file window pops up, prompting you for GRUB configuration syntax for the NeoGrub. Here's an example to boot Arch Linux:

```
title Arch
find --set-root /boot/vmlinuz-linux
kernel /boot/vmlinuz-linux ro root=/dev/sda3

initrd /boot/initramfs-linux.img

```

adjust the /dev/sda3 line accordingly to point to your Linux / partition. Also, if you use a kernel other than default (such as linux-lts or the -ck kernel) adjust the initramfs and vmlinuz files accordingly.

More information of the nature and workings of EasyBCD and NeoGRUB is at the developer's site:

*   [https://neosmart.net/wiki/easybcd/neogrub/](https://neosmart.net/wiki/easybcd/neogrub/)
*   [https://neosmart.net/wiki/easybcd/neogrub/linux/](https://neosmart.net/wiki/easybcd/neogrub/linux/)

note that that last link has an example to boot Ubuntu. Ubuntu adds version numbers to its vmlinuz and initrd files, which would require that you update the NeoGRUB every kernel update. Arch does not have this problem. Also note that Arch uses initramfs, not initrd, but you still use the syntax in the code box above.

## Chainloading GRUB

Since EasyBCD's NeoGRUB currently does not understand the GRUB menu format, chainload to it by replacing the contents of your `C:\NST\menu.lst` file with lines similar to the following:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

Finally, [#Generate the main configuration file](#Generate_the_main_configuration_file).