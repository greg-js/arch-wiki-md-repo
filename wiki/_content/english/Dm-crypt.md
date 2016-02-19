From the cryptsetup project's [wiki](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt):

	Device-mapper is infrastructure in the Linux 2.6 and 3.x kernel that provides a generic way to create virtual layers of block devices. Device-mapper crypt target provides transparent encryption of block devices using the kernel crypto API. The user can basically specify one of the symmetric ciphers, an encryption mode, a key (of any allowed size), an iv generation mode and then the user can create a new block device in /dev. Writes to this device will be encrypted and reads decrypted. You can mount your filesystem on it as usual or stack dm-crypt device with another device like RAID or LVM volume. Basic documentation of dm-crypt mapping table comes with kernel source and the latest version is available in git repository.

## Contents

*   [1 Common scenarios](#Common_scenarios)
*   [2 Drive preparation](#Drive_preparation)
*   [3 Device encryption](#Device_encryption)
*   [4 System configuration](#System_configuration)
*   [5 Swap device encryption](#Swap_device_encryption)
*   [6 Specialties](#Specialties)
*   [7 See also](#See_also)

## Common scenarios

This part introduces common scenarios to employ *dm-crypt* to encrypt a system or individual filesystem mount points. It is meant as starting point to familiarize with different practical encryption procedures. The scenarios cross-link to the other subpages where needed.

See [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system") if you need to encrypt a device that is not used for booting a system, like a [partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") or a [loop device](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system").

See [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") if you want to encrypt an entire system, in particular a root partition. Several scenarios are covered, including the use of *dm-crypt* with the *LUKS* extension, *plain* mode encryption and encryption and *LVM*.

## Drive preparation

[Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") deals with operations like [securely erasing the drive](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") and *dm-crypt* specific points for [partitioning it](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

## Device encryption

[Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") covers how to manually utilize dm-crypt to encrypt a system through the [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption") command. It covers examples of the [Encryption options with dm-crypt](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption"), deals with the creation of [keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"), LUKS specific commands for [key management](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption") as well as for [Backup and restore](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## System configuration

[Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") illustrates how to configure [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), the [boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and the [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") file when encrypting a system.

## Swap device encryption

[Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") covers how to add a swap partition to an encrypted system, if required. The swap partition must be encrypted as well to protect any data swapped out by the system. This part details methods [without](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#Without_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") and [with](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#With_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") suspend-to-disk support.

## Specialties

[Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") deals with special operations like [securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [using GPG or OpenSSL encrypted keyfiles](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), a method to [boot and unlock via the network](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties"), another for [setting up discard/TRIM for a SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties"), and sections dealing with [the encrypt hook and multiple disks](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").

## See also

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - The project homepage
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - The LUKS homepage and [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - the main and foremost help resource.
*   [cryptsetup repository](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) and [release](https://www.kernel.org/pub/linux/utils/cryptsetup/) archive.
*   [DOXBOX](https://github.com/t-d-k/doxbox) - Supports unlocking LUKS encrypted volumes in Microsoft Windows.