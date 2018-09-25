Related articles

*   [dm-crypt](/index.php/Dm-crypt "Dm-crypt")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [eCryptfs](/index.php/ECryptfs "ECryptfs")
*   [EncFS](/index.php/EncFS "EncFS")
*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [Tomb](/index.php/Tomb "Tomb")
*   [tcplay](/index.php/Tcplay "Tcplay")
*   [GnuPG](/index.php/GnuPG "GnuPG")
*   [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives")

本文讨论[磁盘加密](https://en.wikipedia.org/wiki/Disk_encryption "wikipedia:Disk encryption")软件，它即时加密、解密从[块设备](https://en.wikipedia.org/wiki/Block_device "wikipedia:Block device")（如硬盘驱动器，闪存驱动器和DVD等），[磁盘分区](/index.php/%E7%A3%81%E7%9B%98%E5%88%86%E5%8C%BA "磁盘分区")，目录中写入、读取的数据。 磁盘加密只应被当作操作系统现有安全机制的附属物。磁盘加密从物理访问层面保护，依赖系统的*其他部分*提供网络安全和基于用户的访问控制等功能。

## Contents

*   [1 为什么加密?](#.E4.B8.BA.E4.BB.80.E4.B9.88.E5.8A.A0.E5.AF.86.3F)
*   [2 系统数据加密](#.E7.B3.BB.E7.BB.9F.E6.95.B0.E6.8D.AE.E5.8A.A0.E5.AF.86)
*   [3 可用方法](#.E5.8F.AF.E7.94.A8.E6.96.B9.E6.B3.95)
    *   [3.1 文件系统上加一层保护](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E4.B8.8A.E5.8A.A0.E4.B8.80.E5.B1.82.E4.BF.9D.E6.8A.A4)
        *   [3.1.1 云储存优化](#.E4.BA.91.E5.82.A8.E5.AD.98.E4.BC.98.E5.8C.96)
    *   [3.2 块设备加密](#.E5.9D.97.E8.AE.BE.E5.A4.87.E5.8A.A0.E5.AF.86)
    *   [3.3 各种加密方法的比较](#.E5.90.84.E7.A7.8D.E5.8A.A0.E5.AF.86.E6.96.B9.E6.B3.95.E7.9A.84.E6.AF.94.E8.BE.83)
        *   [3.3.1 Summary](#Summary)
        *   [3.3.2 Basic classification](#Basic_classification)
        *   [3.3.3 Practical implications](#Practical_implications)
        *   [3.3.4 Usability features](#Usability_features)
        *   [3.3.5 Security features](#Security_features)
        *   [3.3.6 Performance features](#Performance_features)
        *   [3.3.7 Block device encryption specific](#Block_device_encryption_specific)
        *   [3.3.8 Stacked filesystem encryption specific](#Stacked_filesystem_encryption_specific)
        *   [3.3.9 Compatibility & prevalence](#Compatibility_.26_prevalence)
*   [4 准备](#.E5.87.86.E5.A4.87)
    *   [4.1 选择一种加密配置](#.E9.80.89.E6.8B.A9.E4.B8.80.E7.A7.8D.E5.8A.A0.E5.AF.86.E9.85.8D.E7.BD.AE)
    *   [4.2 例子](#.E4.BE.8B.E5.AD.90)
    *   [4.3 选择强密码](#.E9.80.89.E6.8B.A9.E5.BC.BA.E5.AF.86.E7.A0.81)
    *   [4.4 磁盘准备](#.E7.A3.81.E7.9B.98.E5.87.86.E5.A4.87)
*   [5 加密如何工作](#.E5.8A.A0.E5.AF.86.E5.A6.82.E4.BD.95.E5.B7.A5.E4.BD.9C)
    *   [5.1 基本原则](#.E5.9F.BA.E6.9C.AC.E5.8E.9F.E5.88.99)
*   [6 =密钥、密钥文件、密码](#.3D.E5.AF.86.E9.92.A5.E3.80.81.E5.AF.86.E9.92.A5.E6.96.87.E4.BB.B6.E3.80.81.E5.AF.86.E7.A0.81)
    *   [6.1 加密元数据](#.E5.8A.A0.E5.AF.86.E5.85.83.E6.95.B0.E6.8D.AE)
    *   [6.2 密码和加密方式](#.E5.AF.86.E7.A0.81.E5.92.8C.E5.8A.A0.E5.AF.86.E6.96.B9.E5.BC.8F)
    *   [6.3 Plausible deniability](#Plausible_deniability)

## 为什么加密?

Disk encryption ensures that files are always stored on disk in an encrypted form. The files only become available to the operating system and applications in readable form while the system is running and unlocked by a trusted user. An unauthorized person looking at the disk contents directly, will only find garbled random-looking data instead of the actual files.

For example, this can prevent unauthorized viewing of the data when the computer or hard-disk is:

*   located in a place to which non-trusted people might gain access while you are away
*   lost or stolen, as with laptops, netbooks or external storage devices
*   in the repair shop
*   discarded after its end-of-life

In addition, disk encryption can also be used to add some security against unauthorized attempts to tamper with your operating system – for example, the installation of keyloggers or Trojan horses by attackers who can gain physical access to the system while you are away.

**Warning:** Disk encryption does **not** protect your data from all threats.

You will still be vulnerable to:

*   Attackers who can break into your system (e.g. over the Internet) while it is running and after you have already unlocked and mounted the encrypted parts of the disk.
*   Attackers who are able to gain physical access to the computer while it is running (even if you use a screenlocker), or very shortly *after* it was running, if they have the resources to perform a [cold boot attack](https://en.wikipedia.org/wiki/Cold_boot_attack "wikipedia:Cold boot attack").
*   A government entity, which not only has the resources to easily pull off the above attacks, but also may simply force you to give up your keys/passphrases using various techniques of [coercion](https://en.wikipedia.org/wiki/Coercion "wikipedia:Coercion"). In most non-democratic countries around the world, as well as in the USA and UK, it may be legal for law enforcement agencies to do so if they have suspicions that you might be hiding something of interest.

A very strong disk encryption setup (e.g. full system encryption with authenticity checking and no plaintext boot partition) is required to stand a chance against professional attackers who are able to tamper with your system *before* you use it. And even then it cannot prevent all types of tampering (e.g. hardware keyloggers). The best remedy might be [hardware-based full disk encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption") and [Trusted Computing](https://en.wikipedia.org/wiki/Trusted_Computing "wikipedia:Trusted Computing").

**Warning:** Disk encryption also will not protect you against someone simply [wiping your disk](/index.php/Securely_wipe_disk "Securely wipe disk"). [Regular backups](/index.php/Backup_programs "Backup programs") are recommended to keep your data safe.

## 系统数据加密

While encrypting only the user data itself (often located within the home directory, or on removable media like a data DVD), is the simplest and least intrusive method, it has some significant drawbacks. In modern computer systems, there are many background processes that may cache and store information about user data or parts of the data itself in non-encrypted areas of the hard drive, like:

*   swap partitions
    *   (potential remedies: disable swapping, or use [encrypted swap](/index.php/Encrypted_swap "Encrypted swap") as well)
*   `/tmp` (temporary files created by user applications)
    *   (potential remedies: avoid such applications; mount `/tmp` inside a [ramdisk](/index.php/Ramdisk "Ramdisk"))
*   `/var` (log files and databases and such; for example, [mlocate](/index.php/Mlocate "Mlocate") stores an index of all file names in `/var/lib/mlocate/mlocate.db`)

The solution is to encrypt both system and user data, preventing unauthorized physical access to private data that may be cached by the system. This however comes with the disadvantage that unlocking of the encrypted parts of the disk has to happen at boot time. Another benefit of system data encryption is that complicates install malware like [keyloggers](https://en.wikipedia.org/wiki/Keystroke_logging "wikipedia:Keystroke logging") or rootkits for someone with physical access.

## 可用方法

All disk encryption methods operate in such a way that even though the disk actually holds encrypted data, the operating system and applications "see" it as the corresponding normal readable data as long as the cryptographic container (i.e. the logical part of the disk that holds the encrypted data) has been "unlocked" and mounted.

For this to happen, some "secret information" (usually in the form of a keyfile and/or passphrase) needs to be supplied by the user, from which the actual encryption key can be derived (and stored in the kernel keyring for the duration of the session).

If you are completely unfamiliar with this sort of operation, please also read the [#How the encryption works](#How_the_encryption_works) section below.

The available disk encryption methods can be separated into two types by their layer of operation:

### 文件系统上加一层保护

Stacked filesystem encryption solutions are implemented as a layer that stacks on top of an existing filesystem, causing all files written to an encryption-enabled folder to be encrypted on-the-fly before the underlying filesystem writes them to disk, and decrypted whenever the filesystem reads them from disk. This way, the files are stored in the host filesystem in encrypted form (meaning that their contents, and usually also their file/folder names, are replaced by random-looking data of roughly the same length), but other than that they still exist in that filesystem as they would without encryption, as normal files / symlinks / hardlinks / etc.

The way it is implemented, is that to unlock the folder storing the raw encrypted files in the host filesystem ("lower directory"), it is mounted (using a special stacked pseudo-filesystem) onto itself or optionally a different location ("upper directory"), where the same files then appear in readable form - until it is unmounted again, or the system is turned off.

Available solutions in this category are [eCryptfs](/index.php/ECryptfs "ECryptfs") and [EncFS](/index.php/EncFS "EncFS").

#### 云储存优化

If you are deploying stacked filesystem encryption to achieve zero-knowledge synchronization with third-party-controlled locations such as cloud-storage services, you may want to consider alternatives to eCryptfs and EncFS, since these are not optimized for transmission of files over the Internet. There are some solutions designed for this purpose instead:

*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [cryptomator](https://aur.archlinux.org/packages/cryptomator/) (multi-platform)
*   [cryfs](https://www.archlinux.org/packages/?name=cryfs)

Note that some cloud-storage services offer zero-knowledge encryption directly through their own [client applications](/index.php/List_of_applications/Internet#Cloud_synchronization_clients "List of applications/Internet").

### 块设备加密

Block device encryption methods, on the other hand, operate *below* the filesystem layer and make sure that everything written to a certain block device (i.e. a whole disk, or a partition, or a file acting as a [loop device](https://en.wikipedia.org/wiki/loop_device "wikipedia:loop device")) is encrypted. This means that while the block device is offline, its whole content looks like a large blob of random data, with no way of determining what kind of filesystem and data it contains. Accessing the data happens, again, by mounting the protected container (in this case the block device) to an arbitrary location in a special way.

The following "block device encryption" solutions are available in Arch Linux:

	loop-AES

	loop-AES is a descendant of cryptoloop and is a secure and fast solution to system encryption. However, loop-AES is considered less user-friendly than other options as it requires non-standard kernel support.

	dm-crypt

	[dm-crypt](/index.php/Dm-crypt "Dm-crypt") is the standard device-mapper encryption functionality provided by the Linux kernel. It can be used directly by those who like to have full control over all aspects of partition and key management. The management of dm-crypt is done with the [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) userspace utility. It can be used for the following types of block-device encryption: *LUKS* (default), *plain*, and has limited features for *loopAES* and *Truecrypt* devices.

*   LUKS, used by default, is an additional convenience layer which stores all of the needed setup information for dm-crypt on the disk itself and abstracts partition and key management in an attempt to improve ease of use and cryptographic security.
*   plain dm-crypt mode, being the original kernel functionality, does not employ the convenience layer. It is more difficult to apply the same cryptographic strength with it. When doing so, longer keys (passphrases or keyfiles) are the result. It has, however, other advantages, described in the following [comparison table](#Practical_implications).

	TrueCrypt/VeraCrypt

	A portable format, supporting encryption of whole disks/partitions or file containers, with compatibility across all major operating systems. [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") was discontinued by its developers in May 2014\. The VeraCrypt fork was audited in 2016.

For practical implications of the chosen layer of operation, see the [comparison table](#Practical_implications) below, as well as the general write up for [eCryptfs](https://www.systutorials.com/docs/linux/packages/ecryptfs-utils-111/ecryptfs-faq.html#compare). See [Category:Encryption](/index.php/Category:Encryption "Category:Encryption") for the available content of the methods compared below, as well as other tools not included in the table.

### 各种加密方法的比较

The column "dm-crypt +/- LUKS" denotes features of dm-crypt for both LUKS ("+") and plain ("-") encryption modes. If a specific feature requires using LUKS, this is indicated by "(with LUKS)". Likewise "(without LUKS)" indicates usage of LUKS is counter-productive to achieve the feature and plain mode should be used.

| 

##### Summary

 | Loop-AES | [dm-crypt](/index.php/Dm-crypt "Dm-crypt") +/- LUKS | [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") | VeraCrypt | [eCryptfs](/index.php/ECryptfs "ECryptfs") | [EncFS](/index.php/EncFS "EncFS") |
| Encryption type | block device | block device | block device | block device | stacked filesystem | stacked filesystem |
| Main selling points | longest-existing one; possibly the fastest; works on legacy systems | de-facto standard for block device encryption on Linux; very flexible | very portable, well-polished, self-contained solution | maintained fork of TrueCrypt | slightly faster than EncFS; individual encrypted files portable between systems | easiest one to use; supports non-root administration |
| Availability in Arch Linux | must manually compile custom kernel | *kernel modules:* already shipped with default kernel; *tools:* [device-mapper](https://www.archlinux.org/packages/?name=device-mapper), [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) | [truecrypt](https://www.archlinux.org/packages/?name=truecrypt) (discontinued) or the backwards-compatible [veracrypt](https://www.archlinux.org/packages/?name=veracrypt) | [veracrypt](https://www.archlinux.org/packages/?name=veracrypt) | *kernel module:* already shipped with default kernel; *tools:* [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) | [encfs](https://www.archlinux.org/packages/?name=encfs) |
| License | GPL | GPL | TrueCrypt License 3.1 | Apache License 2.0, parts subject to TrueCrypt License v3.0 | GPL | GPL |
| 

##### Basic classification

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Encrypts | whole block devices | whole block devices | whole block devices | whole block devices | files | files |
| Container for encrypted data may be... | a disk or disk partition / a file acting as a virtual partition | a disk or disk partition / a file acting as a virtual partition | a disk or disk partition / a file acting as a virtual partition | a disk or disk partition / a file acting as a virtual partition | a directory in an existing file system | a directory in an existing file system |
| Relation to filesystem | operates below filesystem layer: does not care whether the content of the encrypted block device is a filesystem, a partition table, a LVM setup, or anything else | operates below filesystem layer: does not care whether the content of the encrypted block device is a filesystem, a partition table, a LVM setup, or anything else | operates below filesystem layer: does not care whether the content of the encrypted block device is a filesystem, a partition table, a LVM setup, or anything else | operates below filesystem layer: does not care whether the content of the encrypted block device is a filesystem, a partition table, a LVM setup, or anything else | adds an additional layer to an existing filesystem, to automatically encrypt/decrypt files whenever they are written/read | adds an additional layer to an existing filesystem, to automatically encrypt/decrypt files whenever they are written/read |
| Encryption implemented in... | kernelspace | kernelspace | kernelspace | kernelspace | kernelspace | userspace (using FUSE) |
| Cryptographic metadata stored in... | ? | with LUKS: LUKS Header | begin/end of (decrypted) device ([format](http://www.truecrypt.org/docs/volume-format-specification)) | begin/end of (decrypted) device ([format spec](https://www.veracrypt.fr/en/VeraCrypt%20Volume%20Format%20Specification.html)) | header of each encrypted file | control file at the top level of each EncFs container |
| Wrapped encryption key stored in... | ? | with LUKS: LUKS header | begin/end of (decrypted) device ([format spec](http://www.truecrypt.org/docs/volume-format-specification)) | begin/end of (decrypted) device ([format spec](https://www.veracrypt.fr/en/VeraCrypt%20Volume%20Format%20Specification.html)) | key file that can be stored anywhere | key file that can be stored anywhere

[[1]](https://github.com/rfjakob/encfs/blob/next/encfs/encfs.pod#environment-variables)[[2]](https://github.com/vgough/encfs/issues/48#issuecomment-69301831)

 |
| 

##### Practical implications

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| File metadata (number of files, dir structure, file sizes, permissions, mtimes, etc.) is encrypted | ✔ | ✔ | ✔ | ✔ | ✖
(file and dir names can be encrypted though) | ✖
(file and dir names can be encrypted though) |
| Can be used to custom<encrypt whole hard drives (including partition tables) | ✔ | ✔ | ✔ | ✔ | ✖ | ✖ |
| Can be used to encrypt swap space | ✔ | ✔ | ✔ | ✔ | ✖ | ✖ |
| Can be used without pre-allocating a fixed amount of space for the encrypted data container | ✖ | ✖ | ✖ | ✖ | ✔ | ✔ |
| Can be used to protect existing filesystems without block device access, e.g. NFS or Samba shares, cloud storage, etc. | ✖
[](#cite_note-1) | ✖ | ✖ | ✖ | ✔ | ✔ |
| Allows offline file-based backups of encrypted files | ✖ | ✖ | ✖ | ✖ | ✔ | ✔ |
| 

##### Usability features

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Support for automounting on login | ? | ✔ | ✔

with [systemd and /etc/crypttab](/index.php/TrueCrypt#Automounting_using_.2Fetc.2Fcrypttab "TrueCrypt")

 | ✔

with [systemd and /etc/crypttab](/index.php/TrueCrypt#Automounting_using_.2Fetc.2Fcrypttab "TrueCrypt")

 | ✔ | ✔ |
| Support for automatic unmounting in case of inactivity | ? | ? | ? | ? | ? | ✔ |
| Non-root users can create/destroy containers for encrypted data | ✖ | ✖ | ✖ | ✖ | limited | ✔ |
| Provides a GUI | ✖ | ✖ | ✔ | ✔ | ✖ | ✔

[[3]](http://www.libertyzero.com/GEncfsM/)[[4]](https://launchpad.net/gencfsm)

 |
| 

##### Security features

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Supported ciphers | AES | AES, Anubis, CAST5/6, Twofish, Serpent, Camellia, Blowfish,… (every cipher the kernel Crypto API offers) | AES, Twofish, Serpent | AES, Twofish, Serpernt, Camellia, Kuznyechik | AES, Blowfish, Twofish... | AES, Blowfish, Twofish, and any other ciphers available on the system |
| Support for salting | ? | ✔
(with LUKS) | ✔ | ✔ | ✔ | ? |
| Support for cascading multiple ciphers | ? | Not in one device, but blockdevices can be cascaded | ✔

AES-Twofish, AES-Twofish-Serpent, Serpent-AES, Serpent-Twofish-AES, Twofish-Serpent

 | ✔

AES-Twofish, AES-Twofish-Serpent, Serpent-AES, Serpent-Twofish-AES, Twofish-Serpent

 | ? | ✖ |
| Support for key-slot diffusion | ? | ✔
(with LUKS) | ? | ? | ? | ? |
| Protection against key scrubbing | ✔ | ✔
(without LUKS) | ? | ? | ? | ? |
| Support for multiple (independently revocable) keys for the same encrypted data | ? | ✔
(with LUKS) | ? | ? | ? | ✖ |
| 

##### Performance features

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Multithreading support | ? | ✔
[[5]](http://kernelnewbies.org/Linux_2_6_38#head-49f5f735853f8cc7c4d89e5c266fe07316b49f4c) | ✔ | ✔ | ? | ? |
| Hardware-accelerated encryption support | ✔ | ✔ | ✔ | ✔ | ✔ | ✔
[[6]](https://github.com/vgough/encfs/issues/118) |
| 

##### Block device encryption specific

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt |
| Support for (manually) resizing the encrypted block device in-place | ? | ✔ | ✖ | ✖ |
| 

##### Stacked filesystem encryption specific

 | eCryptfs | EncFs |
| Supported file systems | ext3, ext4, xfs (with caveats), jfs, nfs... | ext3, ext4, xfs (with caveats), jfs, nfs, cifs...

[[7]](https://github.com/vgough/encfs)

 |
| Ability to encrypt filenames | ✔ | ✔ |
| Ability to *not* encrypt filenames | ✔ | ✔ |
| Optimized handling of sparse files | ✖ | ✔ |
| 

##### Compatibility & prevalence

 | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs |
| Supported Linux kernel versions | 2.0 or newer | CBC-mode since 2.6.4, ESSIV 2.6.10, LRW 2.6.20, XTS 2.6.24 | ? | ? | ? | 2.4 or newer |
| Encrypted data can also be accessed from Windows | ✔
(with [CrossCrypt](https://en.wikipedia.org/wiki/CrossCrypt "wikipedia:CrossCrypt"), [LibreCrypt](https://github.com/t-d-k/LibreCrypt)) | ?
(with [FreeOTFE](https://en.wikipedia.org/wiki/FreeOTFE "wikipedia:FreeOTFE"), [LibreCrypt](https://github.com/t-d-k/LibreCrypt)) | ✔ | ✔ | ? | ?
[[8]](http://members.ferrara.linux.it/freddy77/encfs.html) |
| Encrypted data can also be accessed from Mac OS X | ? | ? | ✔ | ✔ | ? | ✔
[[9]](https://sites.google.com/a/arg0.net/www/encfs-mac-build) |
| Encrypted data can also be accessed from FreeBSD | ? | ? | ✔

(with VeraCrypt)

 | ✔
 | ? | ✔
[[10]](http://www.freshports.org/sysutils/fusefs-encfs/) |
| Used by | ? | Debian/Ubuntu installer (system encryption)
Fedora installer | ? | ? | Ubuntu installer (home dir encryption)
Chromium OS (encryption of cached user data [[11]](https://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data)) | ? |

1.  [^](#Practical_implications) well, a single file in those filesystems could be used as a container (virtual loop-back device!) but then one would not actually be using the filesystem (and the features it provides) anymore

## 准备

### 选择一种加密配置

Which disk encryption setup is appropriate for you will depend on your goals (please read [#Why use encryption?](#Why_use_encryption.3F) above) and system parameters.

Among other things, you will need to answer the following questions:

	What kind of "attacker" do you want to protect against?

*   Casual computer user snooping around your disk when your system is turned off / stolen / etc.
*   Professional cryptanalyst who can get repeated read/write access to your system before and after you use it
*   Anything in between

	What do you want to encrypt?

*   only user data
*   user data and system data
*   something in between

	How should swap, `/tmp`, etc. be taken care of?

*   Ignore, and hope no data is leaked
*   Disable or mount as ramdisk
*   Encrypt *(as part of full disk encryption, or separately)*

	How should encrypted parts of the disk be unlocked?

*   Passphrase *(same as login password, or separate)*
*   Keyfile *(e.g. on a USB stick, that you keep in a safe place or carry around with yourself)*
*   Both

	*When* should encrypted parts of the disk be unlocked?

*   Before boot
*   During boot
*   At login
*   Manually on demand *(after login)*

	How should multiple users be accommodated?

*   Not at all
*   Using a shared passphrase/key
*   Independently issued and revocable passphrases/keys for the same encrypted part of the disk
*   Separate encrypted parts of the disk for different users

Then you can go on to make the required technical choices (see [#Available methods](#Available_methods) above, and [#How the encryption works](#How_the_encryption_works) below), regarding:

*   stacked filesystem encryption vs. blockdevice encryption
*   key management
*   cipher and mode of operation
*   metadata storage
*   location of the "lower directory" (in case of stacked filesystem encryption)

### 例子

In practice, it could turn out something like:

	Example 1

	Simple user data encryption (internal hard drive) using a virtual folder called `~/Private` in the user's home directory encrypted with [EncFS](/index.php/EncFS "EncFS")

*   encrypted versions of the files stored on-disk in `~/.Private`
*   unlocked on demand with dedicated passphrase

	Example 2

	Partial system encryption with each user's home directory encrypted with [ECryptfs](/index.php/ECryptfs "ECryptfs")

*   unlocked on respective user login, using login passphrase
*   `swap` and `/tmp` partitions encrypted with [Dm-crypt with LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS"), using an automatically generated per-session throwaway key
*   indexing/caching of contents of `/home` by *slocate* (and similar apps) disabled.

	Example 3

	System encryption - whole hard drive except `/boot` partition (however, `/boot` can be encrypted with [GRUB](/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypted_boot_partition_.28GRUB.29 "Dm-crypt/Encrypting an entire system")) encrypted with [Dm-crypt with LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS")

*   unlocked during boot, using passphrases or USB stick with keyfiles
*   Maybe different passphrases/keys per user - independently revocable
*   Maybe encryption spanning multiple drives or partition layout flexibility with [LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system")

	Example 4

	Hidden/plain system encryption - whole hard drive encrypted with [plain dm-crypt](/index.php/Dm-crypt "Dm-crypt")

*   USB-boot, using dedicated passphrase plus USB stick with keyfile
*   data integrity checked before mounting
*   `/boot` partition located on aforementioned USB stick

Many other combinations are of course possible. You should carefully plan what kind of setup will be appropriate for your system.

### 选择强密码

See [Security#Passwords](/index.php/Security#Passwords "Security").

### 磁盘准备

Before setting up disk encryption on a (part of a) disk, consider securely wiping it first. This consists of overwriting the entire drive or partition with a stream of zero bytes or random bytes, and is done for one or both of the following reasons:

	Prevent recovery of previously stored data

Disk encryption does not change the fact that individual sectors are only overwritten on demand, when the file system creates or modifies the data those particular sectors hold (see [#How the encryption works](#How_the_encryption_works) below). Sectors which the filesystem considers "not currently used" are not touched, and may still contain remnants of data from previous filesystems. The only way to make sure that all data which you previously stored on the drive can not be [recovered](https://en.wikipedia.org/wiki/Data_recovery "wikipedia:Data recovery"), is to manually erase it. For this purpose it does not matter whether zero bytes or random bytes are used (although wiping with zero bytes will be much faster).

	Prevent disclosure of usage patterns on the encrypted drive

Ideally, the whole encrypted part of the disk should be indistinguishable from uniformly random data. This way, no unauthorized person can know which and how many sectors actually contain encrypted data - which may be a desirable goal in itself (as part of true confidentiality), and also serves as an additional barrier against attackers trying to break the encryption. In order to satisfy this goal, wiping the disk using high-quality random bytes is crucial.

The second goal only makes sense in combination with block device encryption, because in the case of stacked filesystem encryption the encrypted data can easily be located anyways (in the form of distinct encrypted files in the host filesystem). Also note that even if you only intend to encrypt a particular folder, you will have to erase the whole partition if you want to get rid of files that were previously stored in that folder in unencrypted form (due to [disk fragmentation](https://en.wikipedia.org/wiki/File_system_fragmentation "wikipedia:File system fragmentation")). If there are other folders on the same partition, you will have to back them up and move them back afterwards.

Once you have decided which kind of disk erasure you want to perform, refer to the [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk") article for technical instructions.

**Tip:** In deciding which method to use for secure erasure of a hard disk drive, remember that this will not need to be performed more than once for as long as the drive is used as an encrypted drive.

## 加密如何工作

This section is intended as a high-level introduction to the concepts and processes which are at the heart of usual disk encryption setups.

It does not go into technical or mathematical details (consult the appropriate literature for that), but should provide a system administrator with a rough understanding of how different setup choices (especially regarding key management) can affect usability and security.

### 基本原则

For the purposes of disk encryption, each blockdevice (or individual file in the case of stacked filesystem encryption) is divided into **sectors** of equal length, for example 512 bytes (4,096 bits). The encryption/decryption then happens on a per-sector basis, so the n'th sector of the blockdevice/file on disk will store the encrypted version of the n'th sector of the original data.

Whenever the operating system or an application requests a certain fragment of data from the blockdevice/file, the whole sector (or sectors) that contains the data will be read from disk, decrypted on-the-fly, and temporarily stored in memory:

```
          ╔═══════╗
 sector 1 ║"???.."║
          ╠═══════╣         ╭┈┈┈┈┈╮
 sector 2 ║"???.."║         ┊ key ┊
          ╠═══════╣         ╰┈┈┬┈┈╯
          :       :            │
          ╠═══════╣            ▼             ┣┉┉┉┉┉┉┉┫
 sector n ║"???.."║━━━━━━━(decryption)━━━━━━▶┋"abc.."┋ sector n
          ╠═══════╣                          ┣┉┉┉┉┉┉┉┫
          :       :
          ╚═══════╝

          encrypted                          unencrypted
     blockdevice or                          data in RAM
       file on disk

```

Similarly, on each write operation, all sectors that are affected must be re-encrypted completely (while the rest of the sectors remain untouched).

In order to be able to de/encrypt data, the disk encryption system needs to know the unique secret "key" associated with it. Whenever the encrypted block device or folder in question is to be mounted, its corresponding key (called henceforth its "master key") must be supplied.

The entropy of the key is of utmost importance for the security of the encryption. A randomly generated byte string of a certain length, for example 32 bytes (256 bits), has desired properties but is not feasible to remember and apply manually during the mount.

For that reason two techniques are used as aides. The first is the application of cryptography to increase the entropic property of the master key, usually involving a separate human-friendly passphrase. For the different types of encryption the [#Comparison table](#Comparison_table) lists respective features. The second method is to create a keyfile with high entropy and store it on a medium separate from the data drive to be encrypted.

See also [Wikipedia:Authenticated encryption](https://en.wikipedia.org/wiki/Authenticated_encryption "wikipedia:Authenticated encryption").

## =密钥、密钥文件、密码

The following are examples how to store and cryptographically secure a master key with a keyfile:

	Stored in a plaintext keyfile

Simply storing the master key in a file (in readable form) is the simplest option. The file - called a "keyfile" - can be placed on a USB stick that you keep in a secure location and only connect to the computer when you want to mount the encrypted parts of the disk (e.g. during boot or login).

	Stored in passphrase-protected form in a keyfile or on the disk itself

The master key (and thus the encrypted data) can be protected with a secret passphrase, which you will have to remember and enter each time you want to mount the encrypted block device or folder. See [#Cryptographic metadata](#Cryptographic_metadata) below for details.

	Randomly generated on-the-fly for each session

In some cases, e.g. when encrypting swap space or a `/tmp` partition, it is not necessary to keep a persistent master key at all. A new throwaway key can be randomly generated for each session, without requiring any user interaction. This means that once unmounted, all files written to the partition in question can never be decrypted again by *anyone* - which in those particular use-cases is perfectly fine.

### 加密元数据

Frequently the encryption techniques use cryptographic functions to enhance the security of the master key itself. On mount of the encrypted device the passphrase or keyfile is passed through these and only the result can unlock the master key to decrypt the data.

A common setup is to apply so-called "key stretching" to the passphrase (via a "key derivation function"), and use the resulting enhanced passphrase as the mount key for decrypting the actual master key (which has been previously stored in encrypted form):

```
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮                         ╭┈┈┈┈┈┈┈┈┈┈┈╮
┊ mount passphrase ┊━━━━━⎛key derivation⎞━━━▶┊ mount key ┊
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ,───⎝   function   ⎠    ╰┈┈┈┈┈┬┈┈┈┈┈╯
╭──────╮            ╱                              │
│ salt │───────────´                               │
╰──────╯                                           │
╭─────────────────────╮                            ▼         ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
│ encrypted master key│━━━━━━━━━━━━━━━━━━━━━━(decryption)━━━▶┊ master key ┊
╰─────────────────────╯                                      ╰┈┈┈┈┈┈┈┈┈┈┈┈╯

```

The **key derivation function** (e.g. PBKDF2 or scrypt) is deliberately slow (it applies many iterations of a hash function, e.g. 1000 iterations of HMAC-SHA-512), so that brute-force attacks to find the passphrase are rendered infeasible. For the normal use-case of an authorized user, it will only need to be calculated once per session, so the small slowdown is not a problem. It also takes an additional blob of data, the so-called "**salt**", as an argument - this is randomly generated once during set-up of the disk encryption and stored unprotected as part of the cryptographic metadata. Because it will be a different value for each setup, this makes it infeasible for attackers to speed up brute-force attacks using precomputed tables for the key derivation function.

The **encrypted master key** can be stored on disk together with the encrypted data. This way, the confidentiality of the encrypted data depends completely on the secret passphrase.

Additional security can be attained by instead storing the encrypted master key in a keyfile on e.g. a USB stick. This provides **two-factor authentication**: Accessing the encrypted data now requires something only you *know* (the passphrase), and additionally something only you *have* (the keyfile).

Another way of achieving two-factor authentication is to augment the above key retrieval scheme to mathematically "combine" the passphrase with byte data read from one or more external files (located on a USB stick or similar), before passing it to the key derivation function.The files in question can be anything, e.g. normal JPEG images, which can be beneficial for [#Plausible deniability](#Plausible_deniability). They are still called "keyfiles" in this context, though.

After it has been derived, the master key is securely stored in memory (e.g. in a kernel keyring), for as long as the encrypted block device or folder is mounted.

It is usually not used for de/encrypting the disk data directly, though. For example, in the case of stacked filesystem encryption, each file can be automatically assigned its own encryption key. Whenever the file is to be read/modified, this file key first needs to be decrypted using the main key, before it can itself be used to de/encrypt the file contents:

```
                          ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
                          ┊ master key ┊
  *file on disk:*           ╰┈┈┈┈┈┬┈┈┈┈┈┈╯
 ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐        │
 ╎╭───────────────────╮╎        ▼          ╭┈┈┈┈┈┈┈┈┈┈╮
 ╎│ encrypted file key│━━━━(decryption)━━━▶┊ file key ┊
 ╎╰───────────────────╯╎                   ╰┈┈┈┈┬┈┈┈┈┈╯
 ╎┌───────────────────┐╎                        ▼           ┌┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┐
 ╎│ encrypted file    │◀━━━━━━━━━━━━━━━━━(de/encryption)━━━▶┊ readable file ┊
 ╎│ contents          │╎                                    ┊ contents      ┊
 ╎└───────────────────┘╎                                    └┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┘
 └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘

```

In a similar manner, a separate key (e.g. one per folder) may be used for the encryption of file names in the case of stacked filesystem encryption.

In the case of block device encryption one master key is used per device and, hence, all data. Some methods offer features to assign multiple passphrases/keyfiles for the same device and others not. Some use above mentioned functions to secure the master key and others give the control over the key security fully to the user. Two examples are explained by the cryptographic parameters used by [dm-crypt](/index.php/Dm-crypt "Dm-crypt") in plain or LUKS modes.

When comparing the parameters used by both modes one notes that dm-crypt plain mode has parameters relating to how to locate the keyfile (e.g. `--keyfile-size`, `--keyfile-offset`). The dm-crypt LUKS mode does not need these, because each blockdevice contains a header with the cryptographic metadata at the beginning. The header includes the used cipher, the encrypted master-key itself and parameters required for its derivation for decryption. The latter parameters in turn result from options used during initial encryption of the master-key (e.g. `--iter-time`, `--use-random`).

For the dis-/advantages of the different techniques, please refer back to [#Comparison table](#Comparison_table) or browse the specific pages.

See also:

*   [Wikipedia:Passphrase](https://en.wikipedia.org/wiki/Passphrase "wikipedia:Passphrase")
*   [Wikipedia:Key (cryptography)](https://en.wikipedia.org/wiki/Key_(cryptography) "wikipedia:Key (cryptography)")
*   [Wikipedia:Key management](https://en.wikipedia.org/wiki/Key_management "wikipedia:Key management")
*   [Wikipedia:Key derivation function](https://en.wikipedia.org/wiki/Key_derivation_function "wikipedia:Key derivation function")

### 密码和加密方式

The actual algorithm used for translating between pieces of unencrypted and encrypted data (so-called "plaintext" and "ciphertext") which correspond to each other with respect to a given encryption key, is called a "**cipher**".

Disk encryption employs "block ciphers", which operate on fixed-length blocks of data, e.g. 16 bytes (128 bits). At the time of this writing, the predominantly used ones are:

 block size | key size | comment |
| [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") | 128 bits | 128, 192 or 256 bits | *approved by the NSA for protecting "SECRET" and "TOP SECRET" classified US-government information (when used with a key size of 192 or 256 bits)* |
| [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher) | 64 bits | 32–448 bits | *one of the first patent-free secure ciphers that became publicly available, hence very well established on Linux* |
| [Twofish](https://en.wikipedia.org/wiki/Twofish "wikipedia:Twofish") | 128 bits | 128, 192 or 256 bits | *developed as successor of Blowfish, but has not attained as much widespread usage* |
| [Serpent](https://en.wikipedia.org/wiki/Serpent_(cipher) | 128 bits | 128, 192 or 256 bits | Considered the most secure of the five AES-competition finalists[[12]](http://csrc.nist.gov/archive/aes/round2/r2report.pdf)[[13]](https://www.cl.cam.ac.uk/~rja14/Papers/serpentcase.pdf)[[14]](https://www.cl.cam.ac.uk/~rja14/Papers/serpent.pdf). |

Encrypting/decrypting a sector ([see above](#Basic_principle)) is achieved by dividing it into small blocks matching the cipher's block-size, and following a certain rule-set (a so-called "**mode of operation**") for how to consecutively apply the cipher to the individual blocks.

Simply applying it to each block separately without modification (dubbed the "*electronic codebook (ECB)*" mode) would not be secure, because if the same 16 bytes of plaintext always produce the same 16 bytes of ciphertext, an attacker could easily recognize patterns in the ciphertext that is stored on disk.

The most basic (and common) mode of operation used in practice is "*cipher-block chaining (CBC)*". When encrypting a sector with this mode, each block of plaintext data is combined in a mathematical way with the ciphertext of the previous block, before encrypting it using the cipher. For the first block, since it has no previous ciphertext to use, a special pre-generated data block stored with the sector's cryptographic metadata and called an "**initialization vector (IV)**" is used:

```
                                  ╭──────────────╮
                                  │initialization│
                                  │vector        │
                                  ╰────────┬─────╯
          ╭  ╠══════════╣        ╭─key     │      ┣┉┉┉┉┉┉┉┉┉┉┫        
          │  ║          ║        ▼         ▼      ┋          ┋         . START
          ┴  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"Hello, W"┋ block  ╱╰────┐
    sector n ║          ║                         ┋          ┋ 1      ╲╭────┘
  of file or ║          ║──────────────────╮      ┋          ┋         ' 
 blockdevice ╟──────────╢        ╭─key     │      ┠┈┈┈┈┈┈┈┈┈┈┨
          ┬  ║          ║        ▼         ▼      ┋          ┋
          │  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"orld !!!"┋ block
          │  ║          ║                         ┋          ┋ 2
          │  ║          ║──────────────────╮      ┋          ┋
          │  ╟──────────╢                  │      ┠┈┈┈┈┈┈┈┈┈┈┨
          │  ║          ║                  ▼      ┋          ┋
          :  :   ...    :        ...      ...     :   ...    : ...

               ciphertext                         plaintext
                  on disk                         in RAM

```

When decrypting, the procedure is reversed analogously.

One thing worth noting is the generation of the unique initialization vector for each sector. The simplest choice is to calculate it in a predictable fashion from a readily available value such as the sector number. However, this might allow an attacker with repeated access to the system to perform a so-called [watermarking attack](https://en.wikipedia.org/wiki/Watermarking_attack "wikipedia:Watermarking attack"). To prevent that, a method called "Encrypted salt-sector initialization vector (**ESSIV**)" can be used to generate the initialization vectors in a way that makes them look completely random to a potential attacker.

There are also a number of other, more complicated modes of operation available for disk encryption, which already provide built-in security against such attacks (and hence do not require ESSIV). Some can also additionally guarantee authenticity of the encrypted data (i.e. confirm that it has not been modified/corrupted by someone who does not have access to the key).

See also:

*   [Wikipedia:Disk encryption theory](https://en.wikipedia.org/wiki/Disk_encryption_theory "wikipedia:Disk encryption theory")
*   [Wikipedia:Block cipher](https://en.wikipedia.org/wiki/Block_cipher "wikipedia:Block cipher")
*   [Wikipedia:Block cipher modes of operation](https://en.wikipedia.org/wiki/Block_cipher_modes_of_operation "wikipedia:Block cipher modes of operation")

### Plausible deniability

See [Wikipedia:Plausible deniability](https://en.wikipedia.org/wiki/Plausible_deniability "wikipedia:Plausible deniability").