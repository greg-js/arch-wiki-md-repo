# eCryptfs

This article describes basic usage of [eCryptfs](https://launchpad.net/ecryptfs). It guides you through the process of creating a private and secure encrypted directory within your `$HOME` directory to store sensitive files and private data.

In implementation eCryptfs differs from [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), which provides a _block device encryption layer_, while eCryptfs is an actual file-system – a [stacked cryptographic file system](http://en.wikipedia.org/wiki/Cryptographic_filesystems). For comparison of the two you can refer to [this table](http://ksouedu.com/doc/ecryptfs-utils/ecryptfs-faq.html#compare) and the [Disk encryption#Comparison table](/index.php/Disk_encryption#Comparison_table "Disk encryption"). One distinguished feature is that the encryption is stacked on an existing filesystem; eCryptfs can be mounted onto any single existing directory and does not require a separate partition (or size pre-allocation).

**Note:** The article is in the process of being re-structured. If you need to find information that might not be in its place yet again, the revision before the restructuring is [here](https://wiki.archlinux.org/index.php?title=ECryptfs&oldid=291214).

## Contents

*   [1 Basics](#Basics)
    *   [1.1 Deficiencies](#Deficiencies)
*   [2 Setup example overview](#Setup_example_overview)
*   [3 Setup & mounting](#Setup_.26_mounting)
    *   [3.1 Using the Ubuntu tools](#Using_the_Ubuntu_tools)
        *   [3.1.1 Encrypting a data directory](#Encrypting_a_data_directory)
        *   [3.1.2 Encrypting a home directory](#Encrypting_a_home_directory)
        *   [3.1.3 Mounting](#Mounting)
            *   [3.1.3.1 Manually](#Manually)
            *   [3.1.3.2 Auto-mounting](#Auto-mounting)
    *   [3.2 Using ecryptfs-simple](#Using_ecryptfs-simple)
    *   [3.3 Manual setup](#Manual_setup)
        *   [3.3.1 With ecryptfs-utils](#With_ecryptfs-utils)
        *   [3.3.2 Without ecryptfs-utils](#Without_ecryptfs-utils)
            *   [3.3.2.1 Mounting](#Mounting_2)
            *   [3.3.2.2 Auto-mounting](#Auto-mounting_2)
                *   [3.3.2.2.1 Optional step](#Optional_step)
*   [4 Usage](#Usage)
    *   [4.1 Symlinking into the encrypted directory](#Symlinking_into_the_encrypted_directory)
    *   [4.2 Removal of encryption](#Removal_of_encryption)
    *   [4.3 Backup](#Backup)
*   [5 See Also](#See_Also)

## Basics

As mentioned in the summary eCryptfs does not require special on-disk storage allocation effort, such as a separate partition or pre-allocated space. Instead, you can mount eCryptfs on top of any single directory to protect it. That includes, for example, a user's entire `$HOME` directory or single dedicated directories within it. All cryptographic metadata is stored in the headers of files, so encrypted data can be easily moved, stored for backup and recovered. There are other advantages, but there are also drawbacks, for instance eCryptfs is not suitable for encrypting complete partitions which also means you cannot protect swap space with it (but you can, of course, combine it with [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption")). If you are just starting to set up disk encryption, swap encryption and other points to consider are covered in [Disk encryption#Preparation](/index.php/Disk_encryption#Preparation "Disk encryption").

To familiarize with eCryptfs a few points:

*   As a stacked filesystem, a mounting of an eCryptfs directory refers to mounting a (stacked) encrypted directory to another **un**encrypted mount point (directory) at Linux kernel runtime.
*   It is possible to share an encrypted directory between users. However, the encryption is linked to one passphrase so this must be shared as well. It is also possible to share a directory with differently encrypted files (different passphrases).
*   A number of eCryptfs acronyms are used throughout the documentation:
    *   The encrypted directory is referred to as the **lower** and the unencrypted as the **upper** directory throughout the eCryptfs documentation and this article. While not relevant for this article, the "overlay" filesystem introduced with Linux 3.18 uses (and [explains](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/overlayfs.txt)) the same upper/lower nomenclatura for the stacking of filesystems.
    *   the **mount** passphrase (or key) is what gives access to the encrypted files, i.e. unlocks the encryption. eCryptfs uses the term **wrapped** passphrase to refer to the cryptographically secured mount passphrase.
    *   a `FEFEK` refers to a **F**ile's **E**ncryption key **E**ncryption **Key** (see [kernel documentation](https://www.kernel.org/doc/Documentation/security/keys-ecryptfs.txt)).
    *   a `FNEK` refers to a **F**ile **N**ame **E**ncryption **K**ey, a key to (optionally) encrypt the filenames stored in the encrypted directory.

Before using eCryptfs, the following disadvantages should be checked for applicability.

### Deficiencies

*   Hard-coded variables

	The best usability of eCryptfs is achieved by relying on the so-called "Ubuntu tools" of the [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) package. A considerable downside is that a lot of variables (encryption options, lower directory path) are hard-coded into the tools. Changing them infers considerable manual configuration to achieve similar integration.

*   Network storage mounts

	eCryptfs has long-standing [bugs](https://bugs.launchpad.net/ecryptfs/+bug/277578) and/or feature requests relating to networked storage. Replicating a content backup of an encrypted directory to a network backup storage is always possible. However, if you want to employ ecryptfs to store the encrypted directory directly on a network storage and mount it locally, you should search for working solutions of the respective network tools (NFS, Samba, etc.) first. If in doubt, [EncFS](/index.php/EncFS "EncFS") may be a better choice for such application.

*   Sparse files

	eCryptfs does not handle [sparse files](https://en.wikipedia.org/wiki/Sparse_file). This is sometimes referred to as a bug, but likewise is a consequence of the design as a [stacked filesystem encryption](/index.php/Disk_encryption#Stacked_filesystem_encryption "Disk encryption"). For example, in an eCryptfs directory a `truncate -s 1G file.img` creates 1GB encrypted data and passes it to the underlying filesystem to store; with the corresponding resource (disk space, data throughput) requirements. Unencrypted, the same file can be allocated efficiently as sparse file space by the filesystem; with a [block device encryption](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") only the respective filesystem output would be encrypted.

	This should be considered before encrypting large portions of the directory structure. For most intents and purposes this deficiency does not pose a problem. One workaround is to place sparse files in an unencrypted `.Public` directory (as opposed to the standard eCryptfs `.Private` directory, explained below). Another method is to use a _dm-crypt_ [container](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system") in `.Public` for such.

## Setup example overview

The following [#Setup & mounting](#Setup_.26_mounting) section describes alternatives using eCryptfs to encrypt a data directory. The alternatives start with [#Using the Ubuntu tools](#Using_the_Ubuntu_tools), which make eCryptfs usage particularly easy and also safe against user errors. This also applies to [#Encrypting a home directory](#Encrypting_a_home_directory) with the tools. During setup, instructions are given on the console by the scripts. The [#Using ecryptfs-simple](#Using_ecryptfs-simple) section then introduces an alternative package to aide using eCryptfs. The [#Manual setup](#Manual_setup) section then describes the setup using the `ecryptfs` filesystem directly. The first subsection ([#With ecryptfs-utils](#With_ecryptfs-utils)) still uses one more script and is suggested to read to familiarize with the setup of the manual options before using them [#Without ecryptfs-utils](#Without_ecryptfs-utils).

The alternatives include

1.  the setup step for the encrypted directory structures
2.  the setup to mount, unmount the directory at runtime manually and/or automatically at user login

Each of the described alternative examples can be removed after setup very easily, so do not refrain from testing which suits your needs best.

## Setup & mounting

eCryptfs is a part of Linux since version 2.6.19\. But to work with it you will need the userspace tools provided by the package [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) available in the [Official repositories](/index.php/Official_repositories "Official repositories").

Once you have installed that package you can load the `ecryptfs` module and continue with the setup:

```
# modprobe ecryptfs

```

Before starting, check the eCryptfs documentation. It is distributed with a very good and complete set of [manual pages](http://ecryptfs.org/documentation.html).

**Tip:** If you use [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec), auto-loading of cryptographic modules may fail when executing the `ecryptfs-mount-private` wrapper (as of November 2014). As a work-around, load the mentioned module manually; for example `modprobe md5` as root and [configure](/index.php/Modprobe.d#Loading "Modprobe.d") the system to load it at next boot.

### Using the Ubuntu tools

Most of the user-friendly convenience tools installed by the _ecryptfs-utils_ package assume a very specific eCryptfs setup, namely the one that is officially used by Ubuntu (where it can be selected as an option during distro installation). Unfortunately, these choices are not just default options but are actually hard-coded in the tools. If this set-up does not suit your needs, then you can not use the convenience tools and will have to follow the steps at [#Manual setup](#Manual_setup) instead.

The set-up used by these tools is as follows:

*   each user can have **only one encrypted directory** that is managed by these tools:
    *   either full `$HOME` directory encryption, or
    *   a single encrypted data directory (by default `~/Private/`, but this can be customized).
*   the **lower directory** for each user is always `~/.Private/`
    <small>(in the case of full home dir encryption, this will be a symlink to the actual location at `/home/.ecryptfs/$USER/.Private/`)</small>
*   the **encryption options** used are:
    *   _cipher:_ AES
    *   _key length:_ 16 bytes (128 bits)
    *   _key management scheme:_ passphrase
    *   _plaintext passthrough:_ enabled
*   the **configuration / control info** for the encrypted directory is stored in a bunch of files at `~/.ecryptfs/`:
    <small>(in the case of full home dir encryption, this will be a symlink to the actual location at `/home/.ecryptfs/$USER/.ecryptfs/`)</small>
    *   `Private.mnt` _[plain text file]_ - contains the path where the upper directory should be mounted (e.g. `/home/lucy` or `/home/lucy/Private`)
    *   `Private.sig` _[plain text file]_ - contains the signature used to identify the mount passphrase in the kernel keyring
    *   `wrapped-passphrase` _[binary file]_ - the mount passphrase, encrypted with the login passphrase
    *   `auto-mount`, `auto-umount` _[empty files]_ - if they exist, the `pam_ecryptfs.so` module will (assuming it is loaded) automatically mount/unmount this encrypted directory when the user logs in/out

#### Encrypting a data directory

For a full `$HOME` directory encryption see [#Encrypting a home directory](#Encrypting_a_home_directory)

Before the data directory encryption is setup, decide whether it should later be mounted manually or automatically with the user log-in.

To encrypt a single data directory as a user and mount it manually later, run:

```
$ ecryptfs-setup-private --nopwcheck --noautomount 

```

and follow the instructions. The option `--nopwcheck` enables you to choose a passphrase different to the user login passphrase and the option `--noautomount` is self-explanatory. So, if you want to setup the encrypted directory automatically on log-in later, just _leave out_ both options right away.

The script will automatically create the `~/.Private/` and `~/.ecryptfs/` directory structures as described in the box above. It will also ask for two passphrases:

	**login passphrase**

	This is the password you will have to enter each time you want to mount the encrypted directory. If you want auto-mounting on login to work, it has to be the same password you use to login to your user account.

	**mount passphrase**

	This is used to derive the actual file encryption master key. Thus, you should not enter a custom one unless you know what you are doing - instead press Enter to let it auto-generate a secure random one. It will be encrypted using the login passphrase and stored in this encrypted form in `~/.ecryptfs/wrapped-passphrase`. Later it will automatically be decrypted ("unwrapped") again in RAM when needed, so you never have to enter it manually. Make sure this file does not get lost, otherwise you can never access your encrypted folder again! You may want to run `ecryptfs-unwrap-passphrase` to see the mount passphrase in unencrypted form, write it down on a piece of paper, and keep it in a safe (or similar), so you can use it to recover your encrypted data in case the _wrapped-passphrase_ file is accidentally lost/corrupted or in case you forget the login passphrase.

The mount point ("upper directory") for the encrypted folder will be at `~/Private` by default, however you can manually change this right after the setup command has finished running, by doing:

```
$ mv ~/Private /path/to/new/folder
$ echo /path/to/new/folder > ~/.ecryptfs/Private.mnt

```

To actually use your encrypted folder, you will have to mount it - see [#Mounting](#Mounting) below.

#### Encrypting a home directory

The wrapper script `ecryptfs-migrate-home` will set up an encrypted home directory for a user and take care of migrating any existing files they have in their not yet encrypted home directory.

To run it, the user in question must be logged out and own no processes. The best way to achieve this is to log the user out, log into a console as the root user, and check that `ps -U _username_` returns no output. You also need to ensure that you have [rsync](https://www.archlinux.org/packages/?name=rsync) and [lsof](https://www.archlinux.org/packages/?name=lsof) installed. Once the prerequisites have been met, run:

```
# ecryptfs-migrate-home -u _username_

```

and follow the instructions. After the wrapper script is complete, follow the instructions for auto-mounting - see [#Auto-mounting](#Auto-mounting) below. It is imperative that the user logs in _before_ the next reboot, to complete the process.

Once everything is working, the unencrypted backup of the users home directory, which is saved to `/home/_username_._random_characters_`, can and should be deleted.

#### Mounting

##### Manually

Executing the wrapper

```
$ ecryptfs-mount-private 

```

and entering the passphrase is all needed to mount the encrypted directory to the [above](#Using_the_Ubuntu_tools) described _upper directory_ `~/Private`.

Likewise, executing

```
$ ecryptfs-umount-private

```

will unmount it again.

**Tip:** If it is not required to access the private data permanently during a user session, maybe define an [alias](/index.php/Alias "Alias") to speed the manual step up.

The tools include another script that can be very handy to access an encrypted `.Private` data or home directory. Executing `ecryptfs-recover-private` as root will search the system (or an optional specific path) for the directory, interactively query the passphrase for it and mount the directory. It can, for example, be used from a live-CD or different system to access the encrypted data in case of a recovery. Note that if booting from an Arch Linux ISO you must first install the [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) to it. Further, it will only be able to mount `.Private` directories created with the Ubuntu tools.

##### Auto-mounting

The default way to auto-mount an encrypted directory is via [PAM](/index.php/Pam_mount "Pam mount"). See `man pam_ecryptfs` and - for more details - 'PAM MODULE' in:

```
/usr/share/doc/ecryptfs-utils/README

```

For auto-mounting it is required that the passphrase to access the encrypted directory is synchronised with the user log-in.

The following steps set it up:

1\. Check if `~/.ecryptfs/auto-mount`, `~/.ecryptfs/auto-umount` and `~/.ecryptfs/wrapped-passphrase` exist (these are automatically created by _ecryptfs-setup-private_).

2\. Add _ecryptfs_ to the pam-stack exactly as following to allow transparent unwrapping of the passphrase on login:

Open `/etc/pam.d/system-auth` and _after_ the line containing `auth required pam_unix.so` add:

```
auth    required    pam_ecryptfs.so unwrap

```

Next, _above_ the line containing `password required pam_unix.so` insert:

```
password    optional    pam_ecryptfs.so

```

And finally, _after_ the line `session required pam_unix.so` add:

```
session    optional    pam_ecryptfs.so

```

3\. Re-login and check output of _mount_ which should now contain a mountpoint, e.g.:

```
/home/$USER/.Private on /home/$USER/Private type ecryptfs (...)

```

for the user's encrypted directory. It should be perfectly readable at `~$HOME/Private/`.

The latter should be automatically unmounted and made unavailable when the user logs off.

**Warning:** Unfortunately the automatic unmounting is susceptible to [break](https://bbs.archlinux.org/viewtopic.php?id=194509) with systemd and bugs are filed against it.[[1]](https://bugs.freedesktop.org/show_bug.cgi?id=72759) [[2]](https://nwrickert2.wordpress.com/2013/12/16/systemd-user-manager-ecryptfs-and-opensuse-13-1/) [[3]](https://bugs.launchpad.net/ubuntu/+source/ecryptfs-utils/+bug/313812/comments/43) [[4]](http://lists.alioth.debian.org/pipermail/pkg-systemd-maintainers/2014-October/004088.html) If you experience this problem, you can test it by commenting out `-session optional pam_systemd.so` in `/etc/pam.d/system-login`. However, this is no solution because commenting out will break other systemd functionalities.

### Using ecryptfs-simple

Use [ecryptfs-simple](http://xyne.archlinux.ca/projects/ecryptfs-simple/) if you just want to use eCryptfs to mount arbitrary directories the way you can with [EncFS](/index.php/EncFS "EncFS"). ecryptfs-simple does not require root privileges or entries in `/etc/fstab`, nor is it limited to hard-coded directories such as `~/.Private`. The package is available to be [installed](/index.php/Installed "Installed") as [ecryptfs-simple](https://aur.archlinux.org/packages/ecryptfs-simple/) and from [Xyne's repos](http://xyne.archlinux.ca/repos/).

As the name implies, usage is simple:

```
# simple mounting
ecryptfs-simple /path/to/foo /path/to/bar

```

```
# automatic mounting: prompts for options on the first mount of a directory then reloads them next time
ecryptfs-simple -a /path/to/foo /path/to/bar

```

```
# unmounting by source directory
ecryptfs-simple -u /path/to/foo

```

```
# unmounting by mountpoint
ecryptfs-simple -u /path/to/bar

```

### Manual setup

The following details instructions to set up eCryptfs encrypted directories manually. The first section still relies on one extra script from the [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) package. It may be an easier start and can be tried without any root rights. The [second](#Without_ecryptfs-utils) then sets up an encrypted directory with other encryption options than the default tools.

**Tip:** The following examples use an encrypted directory (`.secret`) different to the default, hard-coded `.Private` in the Ubuntu tools. This is on purpose to avoid problems of erroneous [#Auto-mounting](#Auto-mounting) when the system has PAM setup for it, as well as problems with other tools using the hard-coded defaults.

#### With ecryptfs-utils

Alternatively to using the scripts `ecryptfs-setup-private` and `ecryptfs-mount-private` to setup and mount eCryptfs, the same can be done directly with the binaries (which those scripts use) `ecryptfs-add-passphrase` and `mount.ecryptfs_private` from the [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) package. Those binaries require no root privileges to work by default.

First choose an ALIAS as you like. Through this section, ALIAS will be `secret`. Create the required directories/files:

```
$ mkdir ~/.secret ~/secret ~/.ecryptfs
$ touch ~/.ecryptfs/secret.conf ~/.ecryptfs/secret.sig

```

The `~/.secret` directory will hold the encrypted data. The `~/secret` directory is the mount point where `~/.secret` will be mounted as an ecryptfs filesystem.

In the next command, replace USER with the name of the current user's home directory. Note that you should write full paths to `~/.ecryptfs/secret.conf`. Its format looks like the one in `/etc/fstab` without the mount options:

```
$ echo "/home/USER/.secret /home/USER/secret ecryptfs" > ~/.ecryptfs/secret.conf

```

A mount passphrase must be added to the keyring:

```
$ ecryptfs-add-passphrase
Passphrase: 
Inserted auth tok with sig [78c6f0645fe62da0] into the user session keyring

```

Write the output signature (`ecryptfs_sig`) from the previous command to `~/.ecryptfs/secret.sig`:

```
$ echo 78c6f0645fe62da0 > ~/.ecryptfs/secret.sig

```

A second passphrase for filename encryption may be used. If you choose so, add it to the keyring:

```
$ ecryptfs-add-passphrase
Passphrase: 
Inserted auth tok with sig [326a6d3e2a5d444a] into the user session keyring

```

If you run the command above, **append** its output signature (`ecryptfs_fnek_sig`) to `~/.ecryptfs/secret.sig`:

```
 $ echo 326a6d3e2a5d444a >> ~/.ecryptfs/secret.sig

```

Finally, to mount `~/.secret` on `~/secret`:

```
$ mount.ecryptfs_private secret

```

An eCryptfs filesystem will be mounted with the following options:

```
rw,nosuid,nodev,relatime,ecryptfs_fnek_sig=326a6d3e2a5d444a,ecryptfs_sig=78c6f0645fe62da0,ecryptfs_cipher=aes,ecryptfs_key_bytes=16,ecryptfs_unlink_sigs

```

Except for `ecryptfs_sig` and `ecryptfs_fnek_sig`, the options are hard-coded. `ecryptfs_fnek_sig` will exist only if you choose filename encryption.

To unmount `~/.secret`:

```
$ umount.ecryptfs_private secret

```

#### Without ecryptfs-utils

The ecryptfs-utils package is distributed with a few helper scripts which will help you with key management and similar tasks. If one wants, for example, make a choice about the encryption cipher, some of those scripts cannot be used. In this section we setup an encrypted data directory diverting from those defaults.

First create your private directories, in this example we will call them analogous to the previous section: `secret`

```
$ mkdir -m 700 /home/username/{.secret,.ecryptfs}
$ mkdir -m 500 /home/username/secret

```

To summarize:

*   Actual encrypted data will be stored in the lower `~/.secret` directory
*   While mounted, decrypted data will be available in `~/secret` directory
    *   While not mounted nothing can be written to this directory
    *   While mounted it has the same permissions as the lower directory

Second we create the mount-passphrase ("file encryption key, encryption key", or **fekek**) for the directory. It has to be very secure and cannot be changed easily. The _ecryptfs-setup-private_ script offers the option to generate it from `/dev/urandom`. In the following we do a generation similar to the [source](http://bazaar.launchpad.net/~ecryptfs/ecryptfs/trunk/view/head:/src/utils/ecryptfs-setup-private#L96) and then use _ecryptfs-wrap-passphrase_ to wrap it with an extra password ("Arch"):

```
$ printf "%s\n%s" $(od -x -N 100 --width=30 /dev/random | head -n 1 | sed "s/^0000000//" | sed "s/\s*//g") "Arch" | ecryptfs-wrap-passphrase /home/username/.ecryptfs/wrapped-passphrase

```

The advantages of the above step are: the mount passphrase is generated from a random source and secured by extra hashing before it is stored on disk. Further, the wrap-passphrase can be changed later.

Next, we test the passphrase by loading it into the kernel keyring:

```
$ printf "%s" "Arch" | ecryptfs-insert-wrapped-passphrase-into-keyring /home/username/.ecryptfs/wrapped-passphrase -
Inserted auth tok with sig [7c5d3dd8a1b49db0] into the user session keyring

```

and manually copy the signature into the configuration:

```
$ echo "7c5d3dd8a1b49db0" > ~/.ecryptfs/secret.sig

```

Now we continue to setup the encryption options for the directory and prepare an user-mountable entry for `/etc/fstab`. If you already know the eCryptfs options to use in it, you can skip the following _mount_ and create an entry with the above signature already.

The _mount.ecryptfs_ command needs root and does not allow for piping the passphrase unfortunately. The mount helper will ask questions about the options we want to choose ("Key type": passphrase - choose any, we only do this to generate the options to use), but let it mount:

```
# mount -t ecryptfs /home/username/.secret /home/username/secret
Passphrase: yes
Cipher: aes
Key byte: 32
Plaintext passtrough: no
Filename encryption: no
Add signature to cache: yes 

```

To summarize the parameters:

*   The above chosen `32` "key bytes" result in a 256 bit AES encryption (the helper scripts are hard-coded to AES with 128 bit).
*   Plaintext passtrough enables to store and work with **un-encrypted** files stored in the lower directory.
*   In eCryptfs terms the key used to protect filenames is known as "filename encryption key", or **fnek**
*   **fekek** and **fnek** can be the same key or different ones at choice

To create the mount point for the user in [fstab](/index.php/Fstab "Fstab"), find the current mount and copy it. For example (`XY` are placeholders here):

 `# mount`  `/home/username/.secret on /home/username/secret type ecryptfs (... ecryptfs_fnek_sig=XY,ecryptfs_sig=XY,ecryptfs_cipher=aes,ecryptfs_key_bytes=32,ecryptfs_unlink_sigs, user)` 

Or, alternatively, append it into `/etc/fstab` to edit it:

```
# mount | grep secret >> /etc/fstab 

```

Before continuing, we can already un-mount the temporary mount we used to generate the options:

```
# umount /home/username/secret

```

Now the mount line has to be edited into the correct format, the mount options `nosuid,nodev,noexec,relatime` before the first _ecryptfs_ option are default and can be left out. But what we need to add is the correct signatures for the passphrases to replace the ones of the current mount:

```
# cat /home/username/.ecryptfs/secret.sig 
7c5d3dd8a1b49db0 

```

We also need to add the options `user` and `noauto`. After the edit, the entry will look similar to (bold entries added):

 `/etc/fstab`  `/home/username/.secret /home/username/secret ecryptfs **noauto**,**user**,ecryptfs_fnek_sig=**7c5d3dd8a1b49db0**,ecryptfs_sig=**7c5d3dd8a1b49db0**,ecryptfs_cipher=aes,ecryptfs_key_bytes=32,ecryptfs_unlink_sigs **0 0**` 

Some options to note:

*   The `ecryptfs_fnek_sig` option will be only listed if you enabled filename encryption
*   The second last option `ecryptfs_unlink_sigs` ensures that the keyring is cleared every time the directory is un-mounted
*   The bold options have been added:
    *   The `user` option enables to mount the directory as a user
    *   The `noauto` option is important, because otherwise systemd will error trying to mount the entry directly on boot.
*   The user mount will default to option `noexec`. If you want to have at least executable files in your private directory, you can add `exec` to the fstab options.

The setup is now complete and directory should be mountable by the user.

##### Mounting

To mount the encrypted directory as the user, the passphrase must be unwrapped and made available in the user's keyring. Following above section example:

```
$ ecryptfs-insert-wrapped-passphrase-into-keyring /home/username/.ecryptfs/wrapped-passphrase
Passphrase: 
Inserted auth tok with sig [7c5d3dd8a1b49db0] into the user session keyring 

```

Now the directory can be mounted without the mount helper questions:

```
$ mount -i /home/username/secret

```

and files be placed into the `secret` directory. The above two steps are necessary every time to mount the directory manually.

To unmount it again:

```
$ umount /home/username/secret

```

To finalize, the preliminary passphrase to wrap the encryption passphrase may be changed:

```
$ ecryptfs-rewrap-passphrase /home/username/.ecryptfs/wrapped-passphrase
Old wrapping passphrase: 
New wrapping passphrase: 
New wrapping passphrase (again):

```

The un-mounting should also clear the keyring, to check the user's keyring or clear it manually:

```
$ keyctl list @u
$ keyctl clear @u

```

**Note:** One should remember that `/etc/fstab` is for system-wide partitions only and should not generally be used for user-specific mounts

##### Auto-mounting

Different methods can be employed to automount the previously defined user-mount in `/etc/fstab` on login. As a first general step, follow point (1) and (2) of [#Auto-mounting](#Auto-mounting).

Then, if you login via console, a simple way is to specify the [user-interactive](#Mounting_2) _mount_ and _umount_ in the user's shell configuration files, for example [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash").

Another method is to automount the eCryptfs directory on user login using [pam_mount](/index.php/Pam_mount "Pam mount"). To configure this method, add the following lines to `/etc/security/pam_mount.conf.xml`:

```
<luserconf name=".pam_mount.conf.xml" />
<mntoptions require="" /> 
<lclmount>mount -i %(VOLUME) "%(before=\"-o\" OPTIONS)"</lclmount> 

```

Please prefer writing manually these lines instead of simply copy/pasting them (especially the lclmount line), otherwise you might get some corrupted characters. Explanation:

*   the first line indicates where the user-based configuration file is located (here `~/.pam_mount.conf.xml`)
*   the second line overwrites the default required mount options which are unnecessary ("nosuid,nodev")
*   the last line indicates which mount command to run (eCryptfs needs the `-i` switch).

Then set the volume definition, preferably to `~/.pam_mount.conf.xml`:

```
<pam_mount>
    <volume noroot="1" fstype="ecryptfs" path="/home/user/.secret/" mountpoint="/home/user/secret/"/>
</pam_mount>

```

"noroot" is needed because the encryption key will be added to the user's keyring.

Finally, edit `/etc/pam.d/login` as described in [pam_mount](/index.php/Pam_mount "Pam mount")'s article.

###### Optional step

To avoid wasting time needlessly unwrapping the passphrase you can create a script that will check _pmvarrun_ to see the number of open sessions:

```
#!/bin/sh
#
#    /usr/local/bin/doecryptfs

exit $(/usr/sbin/pmvarrun -u$PAM_USER -o0)

```

With the following line added before the eCryptfs unwrap module in your PAM stack:

```
auth    [success=ignore default=1]    pam_exec.so     quiet /usr/local/bin/doecryptfs
auth    required                      pam_ecryptfs.so unwrap

```

The article suggests adding these to `/etc/pam.d/login`, but the changes will need to be added to all other places you login, such as `/etc/pam.d/kde`.

## Usage

### Symlinking into the encrypted directory

Besides using your private directory as storage for sensitive files, and private data, you can also use it to protect application data. [Firefox](/index.php/Firefox "Firefox") for example has an internal password manager, but the browsing history and cache can also be sensitive. Protecting it is easy:

```
 $ mv ~/.mozilla ~/Private/mozilla
 $ ln -s ~/Private/mozilla ~/.mozilla

```

### Removal of encryption

There are no special steps involved, if you want to remove your private directory. Make sure it is un-mounted and delete the respective lower directory (e.g. `~/.Private`), along with all the encrypted files. After also removing the related encryption signatures and configuration in `~/.ecryptfs`, all is gone.

If you were [#Using the Ubuntu tools](#Using_the_Ubuntu_tools) to setup a single directory encryption, you can directly follow the steps detailed by:

```
$ ecryptfs-setup-private --undo

```

and follow the instructions.

### Backup

If you want to move a file out of the private directory just move it to the new destination while `~/Private` is mounted.

With eCryptfs the cryptographic metadata is stored in the header of the files. Setup variants explained in this article separate the directory with encrypted data from the mount point. The unencrypted mount point is fully transparent and available for a backup. Obviously this has to be considered for automated backups, if one has to avoid leaking sensitive unencrypted data into a backup.

You can do backups, or incremental backups, of the encrypted (e.g. `~/.Private`) directory, treating it like any other directory.

Further points to note:

*   If you used the Ubuntu tools for [#Encrypting a home directory](#Encrypting_a_home_directory), be aware the location of the lower directory with the encrypted files is _outside_ the regular user's `$HOME` at `/home/.ecryptfs/$USER/.Private`.

*   It should be ensured to include the eCryptfs setup files (located in `~/.ecryptfs` usually) into the regular or a separate backup.

*   If you use special filesystem mount options, for example `ecryptfs_xattr`, do extra checks on restore integrity.

## See Also

*   [eCryptfs](http://ecryptfs.org/documentation.html) - Manpages and project home
*   [Security audit](https://defuse.ca/audits/ecryptfs.htm) of eCryptfs by Taylor Hornby (January 22, 2014).
*   [eCryptfs and $HOME](http://sysphere.org/~anrxc/j/articles/ecryptfs/index.html) by Adrian C. (anrxc) - Article with installation instructions and discussion of eCryptfs usage
*   [Chromium data protection](http://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data) (November 2009) - Design document detailing encryption options for Chromium OS, including explanation on its eCryptfs usage
*   [eCryptfs design](http://ecryptfs.sourceforge.net/ecryptfs.pdf) by Michael Halcrow (May 2005) - Original design document detailing and discussing eCryptfs

Retrieved from "[https://wiki.archlinux.org/index.php?title=ECryptfs&oldid=418436](https://wiki.archlinux.org/index.php?title=ECryptfs&oldid=418436)"