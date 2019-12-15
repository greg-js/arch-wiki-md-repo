相关文章

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

**翻译状态：** 本文是英文页面 [Dm-crypt](/index.php/Dm-crypt "Dm-crypt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-11-22，点击[这里](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=589414)可以查看翻译后英文页面的改动。

dm-crypt is the Linux kernel's [device mapper](https://en.wikipedia.org/wiki/device_mapper "wikipedia:device mapper") crypto target. From [Wikipedia:dm-crypt](https://en.wikipedia.org/wiki/dm-crypt "wikipedia:dm-crypt"), it is:

	a transparent disk encryption subsystem in [the] Linux kernel... [It is] implemented as a device mapper target and may be stacked on top of other device mapper transformations. It can thus encrypt whole disks (including removable media), partitions, software RAID volumes, logical volumes, as well as files. It appears as a block device, which can be used to back file systems, swap or as an LVM physical volume.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 常见场景](#常见场景)
*   [2 Drive preparation](#Drive_preparation)
*   [3 Device encryption](#Device_encryption)
*   [4 System configuration](#System_configuration)
*   [5 Swap device encryption](#Swap_device_encryption)
*   [6 Specialties](#Specialties)
*   [7 See also](#See_also)

## 常见场景

这一部分介绍应用 *dm-crypt* 来加密整个系统或是某个文件系统挂载点的经典场景。这一部分是作为了解不同实际的加密程序的起点。

查看 [dm-crypt/Encrypting a non-root file system (简体中文)](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dm-crypt/Encrypting a non-root file system (简体中文)")，这个页面教你怎么加密一个不是用来启动系统的设备，比如一个 [分区](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#分区 "Dm-crypt/Encrypting a non-root file system (简体中文)") 或者一个 [loop 设备](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#Loop设备 "Dm-crypt/Encrypting a non-root file system (简体中文)").

查看 [/Encrypting an entire system](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Encrypting_an_entire_system&action=edit&redlink=1 "Dm-crypt (简体中文)/Encrypting an entire system (page does not exist)")，这个页面教你怎么加密整个系统，特别是加密根分区（root分区）。这里面又有其他细分场景，包括用 *LUKS* 插件、*plain*加密模式以及配合*LVM*使用。

## Drive preparation

[/Drive preparation](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Drive_preparation&action=edit&redlink=1 "Dm-crypt (简体中文)/Drive preparation (page does not exist)") deals with operations like [securely erasing the drive](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Drive_preparation&action=edit&redlink=1 "Dm-crypt (简体中文)/Drive preparation (page does not exist)") and *dm-crypt* specific points for [partitioning it](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Drive_preparation&action=edit&redlink=1 "Dm-crypt (简体中文)/Drive preparation (page does not exist)").

## Device encryption

[/Device encryption](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Device_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Device encryption (page does not exist)") covers how to manually utilize dm-crypt to encrypt a system through the [cryptsetup](/index.php/Cryptsetup "Cryptsetup") command. It covers examples of the [Encryption options with dm-crypt](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Device_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Device encryption (page does not exist)"), deals with the creation of [keyfiles](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Device_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Device encryption (page does not exist)"), LUKS specific commands for [key management](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Device_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Device encryption (page does not exist)") as well as for [Backup and restore](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Device_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Device encryption (page does not exist)").

## System configuration

[/System configuration](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/System_configuration&action=edit&redlink=1 "Dm-crypt (简体中文)/System configuration (page does not exist)") illustrates how to configure [mkinitcpio](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/System_configuration&action=edit&redlink=1 "Dm-crypt (简体中文)/System configuration (page does not exist)"), the [boot loader](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/System_configuration&action=edit&redlink=1 "Dm-crypt (简体中文)/System configuration (page does not exist)") and the [crypttab](/index.php/Crypttab "Crypttab") file when encrypting a system.

## Swap device encryption

[/Swap encryption](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Swap_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Swap encryption (page does not exist)") covers how to add a swap partition to an encrypted system, if required. The swap partition must be encrypted as well to protect any data swapped out by the system. This part details methods [without](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Swap_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Swap encryption (page does not exist)") and [with](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Swap_encryption&action=edit&redlink=1 "Dm-crypt (简体中文)/Swap encryption (page does not exist)") suspend-to-disk support.

## Specialties

[/Specialties](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Specialties&action=edit&redlink=1 "Dm-crypt (简体中文)/Specialties (page does not exist)") deals with special operations like [securing the unencrypted boot partition](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Specialties&action=edit&redlink=1 "Dm-crypt (简体中文)/Specialties (page does not exist)"), [using GPG or OpenSSL encrypted keyfiles](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Specialties&action=edit&redlink=1 "Dm-crypt (简体中文)/Specialties (page does not exist)"), a method to [boot and unlock via the network](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Specialties&action=edit&redlink=1 "Dm-crypt (简体中文)/Specialties (page does not exist)"), another for [setting up discard/TRIM for a SSD](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Specialties&action=edit&redlink=1 "Dm-crypt (简体中文)/Specialties (page does not exist)"), and sections dealing with [the encrypt hook and multiple disks](/index.php?title=Dm-crypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Specialties&action=edit&redlink=1 "Dm-crypt (简体中文)/Specialties (page does not exist)").

## See also

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - The project homepage
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - The LUKS homepage and [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - the main and foremost help resource.
*   [cryptsetup repository](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) and [release](https://www.kernel.org/pub/linux/utils/cryptsetup/) archive.