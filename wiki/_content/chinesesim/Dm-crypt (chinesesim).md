相关文章

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

**翻译状态：** 本文是英文页面 [Dm-crypt](/index.php/Dm-crypt "Dm-crypt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-12-30，点击[这里](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=290892)可以查看翻译后英文页面的改动。

This article focuses on how to set up encryption on Arch Linux using *dm-crypt*, which is the standard device-mapper encryption functionality provided by the Linux kernel.

## Contents

*   [1 Common scenarios](#Common_scenarios)
*   [2 Drive preparation](#Drive_preparation)
*   [3 Device encryption](#Device_encryption)
*   [4 System configuration](#System_configuration)
*   [5 Swap device encryption](#Swap_device_encryption)
*   [6 Specialties](#Specialties)
*   [7 See also](#See_also)

## Common scenarios

This section introduces common scenarios to employ *dm-crypt* to encrypt a system or individual filesystem mount points. The scenarios cross-link to the other subpages where needed. It is meant as starting point to familiarize with different practical encryption procedures.

See [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system") if you need to encrypt a device that is not used for booting a system, like a [partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") or a [loop device](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system").

See [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") if you want to encrypt an entire system, in particular a root partition. Several scenarios are covered, including the use of *dm-crypt* with the *LUKS* extension, *plain* mode encryption and encryption and *LVM*.

## Drive preparation

This step will deal with operations like [securely erasing the drive](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") and [partitioning it](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

See [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

## Device encryption

This section covers how to manually utilize dm-crypt to encrypt a system through the [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption") command, also dealing with the usage of [LUKS](/index.php/Dm-crypt/Device_encryption#Cryptsetup_actions_specific_for_LUKS "Dm-crypt/Device encryption") and [keyfiles](/index.php/Dm-crypt/Device_encryption#Cryptsetup_and_keyfiles "Dm-crypt/Device encryption").

See [Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption").

## System configuration

This page illustrates how to configure [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), the [boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and the [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") file when encrypting a system.

See [Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration").

## Swap device encryption

A swap partition may be added to an encrypted system, if required. The swap partition must be encrypted as well to protect any data swapped out by the system. This part details methods [without](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#Without_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") and [with](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#With_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") suspend-to-disk support.

See [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

## Specialties

This part deals with special operations like [securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [using GPG or OpenSSL encrypted keyfiles](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), a method to [boot and unlock via the network](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), or [setting up discard/TRIM for a SSD](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties").

See [Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties").

## See also

*   [cryptsetup FAQ](http://code.google.com/p/cryptsetup/wiki/FrequentlyAskedQuestions) - The main and foremost help resource, directly from the developers.
*   [FreeOTFE](http://www.freeotfe.org/) - Supports unlocking LUKS encrypted volumes in Microsoft Windows.