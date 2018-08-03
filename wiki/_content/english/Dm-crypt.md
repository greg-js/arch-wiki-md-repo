Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

dm-crypt is the Linux kernel's [device mapper](https://en.wikipedia.org/wiki/device_mapper "wikipedia:device mapper") crypto target. From [Wikipedia:dm-crypt](https://en.wikipedia.org/wiki/dm-crypt "wikipedia:dm-crypt"), it is a:

	a transparent disk encryption subsystem in [the] Linux kernel.... [It is] implemented as a device mapper target and may be stacked on top of other device mapper transformations. It can thus encrypt whole disks (including removable media), partitions, software RAID volumes, logical volumes, as well as files. It appears as a block device, which can be used to back file systems, swap or as an LVM physical volume.

## Contents

*   [1 Common scenarios](#Common_scenarios)
*   [2 Drive preparation](#Drive_preparation)
*   [3 Device encryption](#Device_encryption)
*   [4 System configuration](#System_configuration)
*   [5 Swap device encryption](#Swap_device_encryption)
*   [6 Specialties](#Specialties)
*   [7 See also](#See_also)

## Common scenarios

This part introduces common scenarios to employ *dm-crypt* to encrypt a system or individual filesystem mount points. It is meant as a starting point to get familiarized with different practical encryption procedures. The scenarios cross-link to the other subpages where needed.

See [dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system") if you need to encrypt a device that is not used for booting a system, like a [partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") or a [loop device](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system").

See [dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") if you want to encrypt an entire system, in particular a root partition. Several scenarios are covered, including the use of *dm-crypt* with the *LUKS* extension, *plain* mode encryption and encryption and *LVM*.

## Drive preparation

[dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") deals with operations like [securely erasing the drive](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") and *dm-crypt* specific points for [partitioning it](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

## Device encryption

[dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") covers how to manually utilize dm-crypt to encrypt a system through the [cryptsetup](/index.php/Cryptsetup "Cryptsetup") command. It covers examples of the [Encryption options with dm-crypt](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption"), deals with the creation of [keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"), LUKS specific commands for [key management](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption") as well as for [Backup and restore](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## System configuration

[dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") illustrates how to configure [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), the [boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and the [crypttab](/index.php/Crypttab "Crypttab") file when encrypting a system.

## Swap device encryption

[dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") covers how to add a swap partition to an encrypted system, if required. The swap partition must be encrypted as well to protect any data swapped out by the system. This part details methods [without](/index.php/Dm-crypt/Swap_encryption#Without_suspend-to-disk_support "Dm-crypt/Swap encryption") and [with](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption") suspend-to-disk support.

## Specialties

[dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") deals with special operations like [securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [using GPG or OpenSSL encrypted keyfiles](/index.php/Dm-crypt/Specialties#Using_GPG.2C_LUKS.2C_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), a method to [boot and unlock via the network](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties"), another for [setting up discard/TRIM for a SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties"), and sections dealing with [the encrypt hook and multiple disks](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").

## See also

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - The project homepage
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - The LUKS homepage and [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - the main and foremost help resource.
*   [cryptsetup repository](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) and [release](https://www.kernel.org/pub/linux/utils/cryptsetup/) archive.
*   [DOXBOX](https://github.com/t-d-k/doxbox) - Supports unlocking LUKS encrypted volumes in Microsoft Windows.