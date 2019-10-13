Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Ext4](/index.php/Ext4 "Ext4")
*   [F2FS](/index.php/F2FS "F2FS")

The [ext4](/index.php/Ext4 "Ext4"), [F2FS](/index.php/F2FS "F2FS"), and [UBIFS](https://en.wikipedia.org/wiki/UBIFS "wikipedia:UBIFS") [file systems](/index.php/File_systems "File systems") natively support file encryption via a common API called **fscrypt** (originally called "ext4 encryption"). With fscrypt, encryption is applied at the directory level. Different directories can use different encryption keys. In an encrypted directory, all file contents, filenames, and symlinks are encrypted. All subdirectories are encrypted too. Non-filename metadata, such as timestamps, the sizes and number of files, and extended attributes, is not encrypted.

**fscrypt** is also the name of a userspace tool to use the kernel feature of the same name. This article shows how to use the [fscrypt tool](https://github.com/google/fscrypt) to encrypt directories, including how to encrypt a home directory.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Alternatives to consider](#Alternatives_to_consider)
*   [2 Preparations](#Preparations)
    *   [2.1 Kernel](#Kernel)
    *   [2.2 File system](#File_system)
        *   [2.2.1 ext4](#ext4)
        *   [2.2.2 F2FS](#F2FS)
    *   [2.3 Userspace tool](#Userspace_tool)
    *   [2.4 Auto-unlocking directories](#Auto-unlocking_directories)
*   [3 Encrypt a directory](#Encrypt_a_directory)
*   [4 Manually unlock a directory](#Manually_unlock_a_directory)
*   [5 Encrypt a home directory](#Encrypt_a_home_directory)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 See also](#See_also)

## Alternatives to consider

If you want to protect an entire file system with one password, then block device encryption with [dm-crypt](/index.php/Dm-crypt "Dm-crypt") is generally a better option, as it ensures that all file system metadata is encrypted. fscrypt is most useful if you only want to encrypt specific directories, or if you want different encrypted directories to be unlockable independently—for example, per-user encrypted home directories.

Unlike [eCryptfs](/index.php/ECryptfs "ECryptfs"), fscrypt is not a stacked file system, i.e. it is supported by file systems natively. This makes fscrypt more memory-efficient. fscrypt also uses more up-to-date cryptography, and it does not require setuid binaries. Also, eCryptfs is no longer being actively developed, and its largest users have migrated to dm-crypt (Ubuntu) or to fscrypt (Android and Chrome OS).

See [disk encryption](/index.php/Disk_encryption "Disk encryption") for more information about other encryption solutions, and about what encryption does and does not do.

**Note:** The `e4crypt` tool from [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) can be used as an alternative to the `fscrypt` tool. However, this is not recommended since `e4crypt` is missing many basic features and is no longer being actively developed.

## Preparations

### Kernel

All [officially supported kernels](/index.php/Kernel#Officially_supported_kernels "Kernel") support fscrypt on ext4, F2FS, and UBIFS.

If you are using a custom kernel version 5.1 or later, make sure `CONFIG_FS_ENCRYPTION=y` is set. For older kernels, see [the documentation](https://github.com/google/fscrypt#runtime-dependencies).

### File system

#### ext4

For [ext4](/index.php/Ext4 "Ext4"), the file system on which you wish to use encryption must have the `encrypt` feature flag enabled. To do this, first check that your file system uses page-sized blocks:

 `# tune2fs -l */dev/device* | grep 'Block size'` 
```
Block size:               4096

```
 `# getconf PAGE_SIZE` 
```
4096

```

If these values differ, then your file system will not support encryption, so do not proceed further.

To enable the `encrypt` feature on the file system, run:

```
# tune2fs -O encrypt */dev/device*

```

**Warning:** Once the `encrypt` feature is enabled, Linux versions older than 4.1 will be unable to mount the file system.

**Tip:**

*   The operation can be undone with `debugfs -w -R "feature -encrypt" */dev/device*`. Run [fsck](/index.php/Fsck "Fsck") before and after to ensure the integrity of the file system.
*   If you are creating a new file system, you can enable the `encrypt` feature immediately with `mkfs.ext4 -O encrypt -b 4096`.

#### F2FS

For [F2FS](/index.php/F2FS "F2FS"), use `fsck.f2fs -O encrypt` or `mkfs.f2fs -O encrypt`.

### Userspace tool

[Install](/index.php/Install "Install") [fscrypt-git](https://aur.archlinux.org/packages/fscrypt-git/). Then run:

```
# fscrypt setup

```

This creates the file `/etc/fscrypt.conf` and the directory `/.fscrypt`.

Then, if the file system on which you wish to use encryption is not the root file system, also run:

```
# fscrypt setup *mountpoint*

```

where `*mountpoint*` is where the file system is mounted, e.g. `/home`.

This creates the directory `*mountpoint*/.fscrypt` to store fscrypt policies and protectors.

**Warning:** Never delete the `.fscrypt` directory; otherwise you will lose access to your encrypted files.

### Auto-unlocking directories

If you want any encrypted directories to be protected by your login passphrase and be automatically unlocked when you log in, edit your [PAM](/index.php/PAM "PAM") configuration to enable `pam_fscrypt`:

In `/etc/pam.d/system-login`, append the following line to the "auth" section:

```
auth            optional   pam_fscrypt.so

```

Also in `/etc/pam.d/system-login`, append the following line to the "session" section:

```
session         optional   pam_fscrypt.so       drop_caches lock_policies

```

Finally, append the following line to `/etc/pam.d/passwd`:

```
password        optional   pam_fscrypt.so

```

## Encrypt a directory

To encrypt an empty directory, run:

```
$ fscrypt encrypt *dir*

```

Follow the prompts to create or choose a "protector". A protector is the secret or information that protects the directory's encryption key. The types of protectors include:

*   "custom_passphrase". This is exactly what it sounds like—just a passphrase that you specify.
*   "pam_passphrase". This is the login passphrase for a particular user. Directories using this type of protector will be automatically unlocked by `pam_fscrypt` (if enabled) when that user logs in.

In both cases, the passphrase can be changed later, or the directory can be re-protected with another method.

Example for custom passphrase:

 `$ fscrypt encrypt private/` 
```
Should we create a new protector? [y/N] y
Your data can be protected with one of the following sources:
1 - Your login passphrase (pam_passphrase)
2 - A custom passphrase (custom_passphrase)
3 - A raw 256-bit key (raw_key)
Enter the source number for the new protector [2 - custom_passphrase]: 2
Enter a name for the new protector: Super Secret
Enter custom passphrase for protector "Super Secret":
Confirm passphrase:
"private/" is now encrypted, unlocked, and ready for use.

```

Example for PAM passphrase:

 `$ fscrypt encrypt private/` 
```
Should we create a new protector? [y/N] y
Your data can be protected with one of the following sources:
1 - Your login passphrase (pam_passphrase)
2 - A custom passphrase (custom_passphrase)
3 - A raw 256-bit key (raw_key)
Enter the source number for the new protector [2 - custom_passphrase]: 1
Enter login passphrase for testuser:
"private/" is now encrypted, unlocked, and ready for use.

```

**Note:** Encryption can only be enabled on an empty directory. If you want to encrypt an existing directory, you will need to copy and then delete the original files, e.g.:
```
$ mkdir *new_dir*
$ fscrypt encrypt *new_dir*
$ cp -a -T *old_dir* *new_dir*
$ find *old_dir* -type f | xargs shred -u
$ rm -rf *old_dir*

```

Beware that the original unencrypted files may still be forensically recoverable from disk even after being shredded and deleted, especially if you are using an SSD. It is much better to keep your data encrypted from the start.

## Manually unlock a directory

To manually unlock an encrypted directory, run:

```
$ fscrypt unlock *dir*

```

`fscrypt` will prompt you for the passphrase.

## Encrypt a home directory

**Warning:** If a user's home directory is encrypted, ssh'ing to that user will not work until their home directory has been unlocked.

To encrypt a user's home directory, first ensure you have completed all [preparations](#Preparations), including enabling `pam_fscrypt`.

Then, create a new encrypted directory for the user:

```
# mkdir /home/newhome
# chown *user*:*user* /home/newhome 
# fscrypt encrypt /home/newhome --user=*user*

```

Select the option to protect the directory with the user's login passphrase.

Then copy the contents of the user's old home directory into the encrypted directory:

```
# cp -a -T /home/*user* /home/newhome

```

**Tip:** If you do not have enough disk space for a second copy of the home directory, you can use `mv -T /home/*user* /home/newhome` instead. However, this is unsafe. If you do this, making a backup first is strongly recommended.

If you used the `cp` method, you can check whether the directory is being automatically unlocked on login before you actually switch to using it. The simplest way to do this is to reboot and log in as that user. Afterwards, run:

 `$ fscrypt status /home/newhome` 
```
"/home/newhome" is encrypted with fscrypt.

Policy:   d80f252996aae181
Options:  padding:32 contents:AES_256_XTS filenames:AES_256_CTS
Unlocked: Yes

Protected with 1 protector:
PROTECTOR         LINKED  DESCRIPTION
5952c84ebaf0f98d  No      login protector for testuser
```

If it says `Unlocked: No` instead, then something is wrong with your PAM configuration, or you did not choose the correct type of protector.

Otherwise, replace the home directory:

```
# mv /home/*user* /home/oldhome
# mv /home/newhome /home/*user*
# reboot

```

If everything is working as expected, you can delete the old home directory:

```
# find /home/oldhome -type f | xargs shred -u
# rm -rf /home/oldhome

```

**Tip:** Running [shred](/index.php/Shred "Shred") is optional, but strongly recommended.

## Troubleshooting

See [https://github.com/google/fscrypt/blob/master/README.md#troubleshooting](https://github.com/google/fscrypt/blob/master/README.md#troubleshooting) for solutions to some common problems and also the [open issues on Github](https://github.com/google/fscrypt/issues).

## See also

*   [fscrypt tool documentation](https://github.com/google/fscrypt/blob/master/README.md)
*   [fscrypt kernel documentation](https://www.kernel.org/doc/html/latest/filesystems/fscrypt.html)
*   [The design document for the fscrypt tool](https://goo.gl/55cCrI)