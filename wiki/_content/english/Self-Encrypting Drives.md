Hardware-based full-disk encryption (FDE) is now available from many hard disk drive (HDD) vendors, becoming increasingly common especially for solid-state drives (SSD). The term "Self-Encrypting Drive" (SED) is now common when referring to HDDs / SSDs with built-in full-disk encryption (FDE).

## Contents

*   [1 Overview](#Overview)
    *   [1.1 Key management technical implementation](#Key_management_technical_implementation)
    *   [1.2 Advantages](#Advantages)
    *   [1.3 Disadvantages](#Disadvantages)
*   [2 Linux support](#Linux_support)
*   [3 Encrypting the root (boot) drive](#Encrypting_the_root_.28boot.29_drive)
    *   [3.1 Check if your disk supports OPAL](#Check_if_your_disk_supports_OPAL)
    *   [3.2 Download (or create) the pre-boot authorization (PBA) image](#Download_.28or_create.29_the_pre-boot_authorization_.28PBA.29_image)
    *   [3.3 Test the PBA on your machine (optional)](#Test_the_PBA_on_your_machine_.28optional.29)
    *   [3.4 Prepare and test the rescue image (optional)](#Prepare_and_test_the_rescue_image_.28optional.29)
    *   [3.5 Set up the drive](#Set_up_the_drive)
    *   [3.6 Enable locking](#Enable_locking)
    *   [3.7 Accessing the drive from a live distro](#Accessing_the_drive_from_a_live_distro)
    *   [3.8 Disable locking](#Disable_locking)
    *   [3.9 Re-enable locking and the PBA](#Re-enable_locking_and_the_PBA)
*   [4 Encrypting a non-root drive](#Encrypting_a_non-root_drive)
*   [5 Changing the passphrase](#Changing_the_passphrase)
*   [6 Secure disk erasure](#Secure_disk_erasure)
*   [7 BIOS based ATA-password](#BIOS_based_ATA-password)
*   [8 See also](#See_also)

## Overview

Many modern SED FDE are made by HDD/SSD vendors which adher to the [OPAL 2.0](http://www.trustedcomputinggroup.org/files/resource_files/FF80CE7D-1A4B-B294-D060AD8807BF9453/TCG_Storage-Opal_SSC_v2.01_rev1.00.pdf) and [Enterprise](http://www.trustedcomputinggroup.org/files/resource_files/FFAE13C6-1A4B-B294-D0D8D885F9F4FB67/TCG_Storage-SSC_Enterprise-v1.01_r1.00.pdf) standards developed by the Trusted Computing Group (TCG). Enterprise SAS versions of the TCG standard are called "TCG Enterprise" drives. The hardware manufactured according to the standards is [labelled](http://www.wavesys.com/self-encrypting-drive-compatibility-list) accordingly.

Unlocking (for runtime decryption) of the drive takes place via either a software, pre-boot authentication environment or with a [#BIOS based ATA-password](#BIOS_based_ATA-password) on power up.

**Tip:** "Encryption" in the context of this page refers to hardware-based encryption. See [Disk encryption#Block device encryption](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") and [Disk encryption#Stacked filesystem encryption](/index.php/Disk_encryption#Stacked_filesystem_encryption "Disk encryption") for software-based encryption.

Refer to the [#Advantages](#Advantages) and [#Disadvantages](#Disadvantages) sections to better understand and decide if hardware-based FDE is what you want.

### Key management technical implementation

**Tip:** This section is important to understand the core concepts behind effective key management, and secure erasure of the disk.

Key management takes place within the disk controller and encryption keys are usually 128 or 256 bit Advanced Encryption Standard (AES).

SEDs adhering to the TCG OPAL 2.0 standard specification (almost all modern SEDs) implement key management via an Authentication Key (AK), and a 2nd-level Data Encryption Key (DEK). The DEK is the key against which the data is actually encrypted/decrypeted. The AK is the user-facing 1st-level password/passphrase which decrypts the DEK (which in-turn decrypts the data). This approach has specific advantages:

*   Allows the user to change the passphrase *without* losing the existing encrypted data on the disk
    *   This improves security, as it is fast and easy to respond to security threats and revoke a compromised passphrase
*   Facilitates near-instant and cryptographically secure full disk erasure.

For those who are familiar; this concept is similar to the LUKS key management layer often used in a [dm-crypt](/index.php/Dm-crypt "Dm-crypt") deployment. Using LUKS, the user can effectively have up to 8 different key-files / passphrases to decrypt the *encryption key*, which in turn decrypts the underlying data. This approach allows the user to revoke / change these key-files / passphrases as required *without* needing to re-encrypt the data, as the 2nd-level encryption key *is unchanged* (itself being re-encrypted by the new passphrase).

In fact, in drives featuring FDE, data is *always* encrypted with the DEK when stored to disk, even if there is no password set (e.g. a new drive). Manufacturers do this to make it easier for users who are not able to, or do not wish to enable the SEDs' security features. This can be thought of as all drives by default having a zero-length password that transparently encrypts/decrypts the data *always* (similar to how passwordless ssh keys provide (somewhat) secure access without user intervention).

*The key point to note* is that if at a later stage a user wishes to *"enable"* encryption, they can configure the passphrase (AK), which will then be used to encrypt the *existing* DEK (thus prompting for passphrase beforing decrypting the DEK in future). However, as the existing DEK *will not* be changed / regenerated; this in effect locks the drive, while preserving the existing encrypted data on the disk.

### Advantages

*   Easier to setup (compared to software-based encryption)
*   Notably transparent to the user, except for initial bootup authentication
*   Data-at-Rest protection
*   Increased performance (cpu is freed up from encryption/decryption calculations)
*   Increased security due to reduced attack vectors (the main cpu & memory are eliminated as possible attack targets)
*   Optimally fast and [#Secure disk erasure](#Secure_disk_erasure) (sanitation) (regardless of disk size)
*   Protection from alternative boot methods due to the possibility to encrypt the MBR, rendering the drive inaccessible before pre-boot authentication

### Disadvantages

*   Constant-power exploits

	Typical self-encrypting drives, once unlocked, will remain unlocked as long as power is provided. This vulnerability can be exploited by means of altering the environment external to the drive, without cutting power, in effect keeping the drive in an unlocked state. For example, it has been shown (by researchers at Universiy of Erlangen-Nuremberg) that it is possible to reboot the computer into an attacker-controlled operating system without cutting power to the drive. The researchers have also demonstrated moving the drive to another computer without cutting power.[[1]](https://www1.cs.fau.de/sed)

*   Key-in-memory exploits

	When the system is powered down into S3 ("sleep") mode, the drive is powered down, but the drive keeps access to the encryption key in its internal memory (NVRAM) to allow for a resume ("wake"). This is necessary because for system booted with an arbitrary operating system there is no standard mechanism to prompt the user to re-enter the pre-boot decryption passphrase again. An attacker (with physical access to the drive) can leverage this to access the drive. Taking together known exploits the researchers summarize "we were able to break hardware-based FDE on eleven [of twelve] of those systems provided they were running or in standby mode".[[2]](https://www1.cs.fau.de/sed) Note, however, S3 ("sleep") is **not** currently supported by sedutil (the current available toolset for managing a TCG OPAL 2.0 SED via Linux)

*   Compromised firmware

	The firmware of the drive may be compromised (backdoor) and data sent to it thus potentially compromised (decryptable by the malicious third party in question, provided access to physical drive is achievable). However, if data is encrypted by the operating system (e.g. dm-crypt), the encryption key is unknown to the compromised drive, thus circumventing this attack vector entirely.

## Linux support

*msed* and *OpalTool*, the two known Open Source code bases available for SED support on Linux, have both been retired, and their development efforts officially merged to form *[sedutil](https://github.com/Drive-Trust-Alliance/sedutil)*, under the umbrella of The [Drive Trust Alliance (DTA)](https://www.drivetrust.com). [sedutil](https://github.com/Drive-Trust-Alliance/sedutil) is "*an Open Source (GPLv3) effort to make Self Encrypting Drive technology freely available to everyone.*"

[Install](/index.php/Install "Install") the [sedutil](https://aur.archlinux.org/packages/sedutil/) package, which contains the *sedutil-cli* tool, and helper scripts to create a custom pre-boot authorization (PBA) image based off the *current* OS in use (e.g. for setting a custom console keymap). Alternatively, you can install *sedutil* solely for acquiring the *sedutil-cli* toolset, but download and use the [precompiled PBA image (for BIOS)](https://github.com/Drive-Trust-Alliance/exec/blob/master/LINUXPBARelease.img.gz?raw=true) provided by the Drive Trust Alliance. If you are using a UEFI machine, you must download [this 64-bit UEFI PBA instead](https://github.com/Drive-Trust-Alliance/exec/blob/master/UEFI64_Release.img.gz?raw=true).

**Note:** UEFI support currently requires that Secure Boot be turned off.

`libata.allow_tpm` **must** be set to `1` (true) in order to use sedutil. Either add `libata.allow_tpm=1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), or by setting `/sys/module/libata/parameters/allow_tpm` to `1` on a running system.

## Encrypting the root (boot) drive

These instructions assume you have the *sedutil-cli* tool installed (via the [AUR](https://aur.archlinux.org/packages/sedutil), or by other means)

### Check if your disk supports OPAL

```
# sedutil-cli --scan

```

If you get something like

```
Scanning for Opal compliant disks
/dev/sda No  LITEONIT LMT-256L9M-11 MSATA 256GB       HM8110B

```

then your disk doesn't support OPAL. On the contrary, the following output means OPAL is supported:

```
/dev/sda 12  Samsung SSD 850 EVO 500GB                EMT02B6Q

```

Windows version of sedutils output:

```
\\.\PhysicalDrive0 12  Samsung SSD 850 PRO 512GB                EXM02B6Q

```

**Note:** [NVMe disks](/index.php/Solid_State_Drives/NVMe "Solid State Drives/NVMe") are only partially supported: The *sedutil-cli --scan* command and the Linux PBA (pre-boot-authorisation) image currently only see SATA disks. It is possible to enable self-encryption on an NVMe device by passing the name to sedutil-cli, but not possible to boot from a locked NVMe disk (the PBA image does not see it). [More details here](https://github.com/Drive-Trust-Alliance/sedutil/issues/120).

### Download (or create) the pre-boot authorization (PBA) image

Download the pre-boot authorization (PBA) image for a [BIOS](https://github.com/Drive-Trust-Alliance/exec/blob/master/LINUXPBARelease.img.gz?raw=true) or [64bit UEFI](https://github.com/Drive-Trust-Alliance/exec/blob/master/UEFI64_Release.img.gz?raw=true) machine.

**Note:** UEFI support currently requires that Secure Boot be turned off.

Alternatively, you can create your own PBA image using the supplied helpers:

```
# mklinuxpba-efi

```

to create an EFI image (/boot/linuxpba-efi.diskimg) and

```
# mklinuxpba-bios

```

to create a BIOS image (/boot/linuxpba.diskimg).

### Test the PBA on your machine (optional)

Refer to the [official docs](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Test-the-PBA).

Don't expect to get a list of your OPAL disks. If you try the PBA from a USB stick and your SSD disk is still not activated for OPAL locking (as it is recommended before the PBA has been successfully tested) you will get an error message including "INVALID PARAMETER" (see [this issue](https://github.com/Drive-Trust-Alliance/sedutil/issues/73)). But this shows that the PBA is actually working and finding your disk. The Wiki is outdated in this regard.

### Prepare and test the rescue image (optional)

Refer to the [official docs](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Test-the-Rescue-system).

### Set up the drive

Decompress the PBA (if required):

```
$ gunzip pba.img.gz

```

Use the output of `lsblk --fs` to help identify the correct drive.

```
# sedutil-cli --initialsetup <password> <drive>
# sedutil-cli --loadPBAimage <password> <pba_file> <drive>
# sedutil-cli --setMBREnable on <password> <drive>

```

### Enable locking

```
# sedutil-cli --enableLockingRange 0 <password> <drive>

```

Power off the computer to lock the drive.

When the computer is next powered on, the PBA should ask for your password; then unlock the drive and chain-load the decrypted OS.

### Accessing the drive from a live distro

The easiest way is to boot the encrypted SSD first, in order to run the shadow MBR. Then press the key that prompts the boot menu and boot whatever device you prefer. Such a way the SED will be completely transparent.

Another way is to directly boot into the live distro and use sedutil to unlock the SSD:

```
# sedutil-cli --setlockingrange 0 rw <password> <drive>
# sedutil-cli --setmbrdone on <password> <drive>

```

`libata.allow_tpm` **must** be set to `1` (true) in order to use sedutil. Either add `libata.allow_tpm=1` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), or by setting `/sys/module/libata/parameters/allow_tpm` to `1` on a running system.

### Disable locking

If you want to turn off Locking and the PBA:

```
# sedutil-cli --disableLockingRange 0 <password> <drive>
# sedutil-cli --setMBREnable off <password> <drive>

```

### Re-enable locking and the PBA

You can later re-enable locking and the PBA using this command sequence

```
# sedutil-cli --enableLockingRange 0 <password> <drive>
# sedutil-cli --setMBRDone on <password> <drive>
# sedutil-cli --setMBREnable on <password> <drive>

```

## Encrypting a non-root drive

A non-root drive does not require loading a PBA. So, activating the encryption is as simple as running:

```
# sedutil-cli --initialsetup <password> <drive>

```

## Changing the passphrase

Changing the passphrase does *not* lose existing data on the drive, and does not require re-encryption of data.

```
# sedutil-cli --setSIDPwd <password> <newpassword> <device>
# sedutil-cli --setAdmin1Pwd <password> <newpassword> <device>

```

Read the [#Key management technical implementation](#Key_management_technical_implementation) section above to learn about how this is implemented securely within the drive, and why it is possible to change the passphrase *without* losing the existing encrypted data on the drive.

## Secure disk erasure

Whole disk erasure is very fast, and remarkably simple for a SED. Simply passing a cryptographic disk erasure (or crypto erase) command (after providing the correct authentication credentials) will have the drive self-generate a new random encryption key (DEK) internally. This will permanently discard the old key, thus rendering the encrypted data irrevocably un-decryptable. The drive will now be in a 'new drive' state.

Read the [#Key management technical implementation](#Key_management_technical_implementation) section above to learn more about how this is implemented securely within the drive.

## BIOS based ATA-password

Previous to the industry's TCG OPAL 2.0 standard initiative, the relevant [ATA](https://en.wikipedia.org/wiki/Parallel_ATA#ATA_standards_versions.2C_transfer_rates.2C_and_features "w:Parallel ATA") standard defined an "ATA Security feature Set" for SED FDE. This relies on the PC (not SSD/HDD) BIOS to feature an unlocking mechanism utilizing the BIOS to setup the user's encryption password/passphrase. This legacy BIOS-based (ATA) method was considered more unreliable to setup and prone to error with regard to interoperability between PC vendors.[[3]](http://www.t13.org/documents/UploadedDocuments/docs2006/e05179r4-ACS-SecurityClarifications.pdf) Typical errors include, for example, inabilities to unlock a device once it is plugged into a system from a different hardware vendor. Hence, the availability of BIOS support for the legacy password mechanism decreases in availability, particularly for consumer hardware.

See [Solid State Drives#Tips for SSD security](/index.php/Solid_State_Drives#Tips_for_SSD_security "Solid State Drives") for more information.

## See also

*   [sedutil (github)](https://github.com/Drive-Trust-Alliance/sedutil)
*   [sedutil official docs](https://github.com/Drive-Trust-Alliance/sedutil/wiki)
*   [sedutil-cli commands usage](https://github.com/Drive-Trust-Alliance/sedutil/wiki/Command-Syntax)
*   [Wikipedia article on hardware-based FDE](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption#Hard_disk_drive_FDE "wikipedia:Hardware-based full disk encryption")