Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")

[EncFS](https://en.wikipedia.org/wiki/EncFS "wikipedia:EncFS") is a userspace stackable cryptographic file-system similar to [eCryptfs](/index.php/ECryptfs "ECryptfs"), and aims to secure data with the minimum hassle. It uses [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") to mount an encrypted directory onto another directory specified by the user. It does not use a loopback system like some other comparable systems such as [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") and [dm-crypt](/index.php/Dm-crypt "Dm-crypt").

EncFS is definitely the simplest software if you want to try disk encryption on Linux.

This has a number of advantages and disadvantages compared to these systems. Firstly, it does not require any root privileges to implement; any user can create a repository of encrypted files. Secondly, one does not need to create a single file and create a file-system within that; it works on existing file-system without modifications.

This does create a few disadvantages, though; because the encrypted files are not stored in their own file, someone who obtains access to the system can still see the underlying directory structure, the number of files, their sizes and when they were modified. They cannot see the contents, however.

This particular method of securing data is obviously not perfect, but there are situations in which it is useful.

For more details on how EncFS compares to other disk encryption solution, see [Disk encryption#Comparison table](/index.php/Disk_encryption#Comparison_table "Disk encryption").

## Contents

*   [1 Comparison to eCryptFS](#Comparison_to_eCryptFS)
*   [2 Installation](#Installation)
*   [3 Usage](#Usage)
    *   [3.1 Changing the password](#Changing_the_password)
*   [4 User friendly mounting](#User_friendly_mounting)
    *   [4.1 Mount using Gnome Encfs Manager](#Mount_using_Gnome_Encfs_Manager)
    *   [4.2 Mount using gnome-encfs](#Mount_using_gnome-encfs)
    *   [4.3 Mount using CryptKeeper trayicon](#Mount_using_CryptKeeper_trayicon)
    *   [4.4 Mount using encfsui](#Mount_using_encfsui)
    *   [4.5 Mount via fstab](#Mount_via_fstab)
    *   [4.6 Mount at login using pam_encfs](#Mount_at_login_using_pam_encfs)
        *   [4.6.1 Single password](#Single_password)
        *   [4.6.2 /etc/pam.d/](#.2Fetc.2Fpam.d.2F)
            *   [4.6.2.1 setup pam_encfs for all login methods](#setup_pam_encfs_for_all_login_methods)
            *   [4.6.2.2 login](#login)
            *   [4.6.2.3 gdm](#gdm)
            *   [4.6.2.4 Configuration](#Configuration)
    *   [4.7 Mount at login using pam_mount](#Mount_at_login_using_pam_mount)
    *   [4.8 Mount when USB drive with EncFS folders is inserted using fsniper](#Mount_when_USB_drive_with_EncFS_folders_is_inserted_using_fsniper)
        *   [4.8.1 How to](#How_to)
    *   [4.9 Mount using KDE KWallet](#Mount_using_KDE_KWallet)
*   [5 Encrypted backup](#Encrypted_backup)
    *   [5.1 Backup encrypted directory](#Backup_encrypted_directory)
    *   [5.2 Backup plaintext directory](#Backup_plaintext_directory)
*   [6 See also](#See_also)

## Comparison to eCryptFS

[eCryptFS](/index.php/System_Encryption_with_eCryptfs "System Encryption with eCryptfs") is implemented in kernelspace and therefore a little bit harder to configure. You have to remember various encryption options (used cyphers, key type, etc...). With EncFS this is not the case, because it stores the encryption metadata information in a per-directory configuration file (`.encfs6.xml`). So you do not have to remember anything (except the passphrase).

The performance of both depends on the type of disk activity. While eCryptFS can perform faster in some cases because there is less overhead by context switching (between kernel and userspace), EncFS has advantages in other cases because the encryption metadata is centralized and not stored in the individual files' headers. For more information [benchmark examples](https://github.com/vgough/encfs/blob/master/PERFORMANCE.md) are provided by the EncFS project.

## Installation

[Install](/index.php/Install "Install") the [encfs](https://www.archlinux.org/packages/?name=encfs) package.

**Warning:** A security [review](https://defuse.ca/audits/encfs.htm) (February 2014) of *encfs* discovered a number of security issues in the stable release 1.7.4 (June 2014). Please consider the report and the references in it for updated information before using the release.

## Usage

To create a secured repository, type:

```
$ encfs ~/.*name* ~/*name*

```

Note that absolute paths must be used. This will be followed by a prompt about whether you want to go with the default options, expert configuration or a paranoid preset. The first is a fairly secure default setup. The second allows specifying algorithms and other options. After entering a key for the encryption, the encoded file-system will be created and mounted. The encoded files are stored, in this example, at `~/.*name*`, and their unencrypted versions in `~/*name*`.

**Tip:** Using EncFS on exFAT formatted partitions might end up with slow performance as exFAT is also fuse-mounted by default. Use another way to mount the exFAT partition, or change the partition format if possible.

To unmount the file-system, type:

```
$ fusermount -u ~/*name*

```

To remount the file-system, issue the first command, and enter the key used to encode it. Once this has been entered, the file-system will be mounted again.

### Changing the password

To change the password of a directory encrypted by EncFS, the following command can be used:

```
$ encfsctl passwd ~/.*name*

```

In this example, `~/.*name*` is the path to the directory which contains the encoded files. The tool will ask for your current password and afterwards, you will be able to set a new one.

## User friendly mounting

### Mount using Gnome Encfs Manager

The [Gnome Encfs Manager](http://libertyzero.com/GEncfsM/) is an easy to use manager and mounter for encfs stashes featuring per-stash configuration, Gnome Keyring support, a tray menu inspired by Cryptkeeper but using the AppIndicator API and lots of unique features.

Both [gnome-encfs-manager](https://aur.archlinux.org/packages/gnome-encfs-manager/) and a slightly more up to date [gnome-encfs-manager-bzr](https://aur.archlinux.org/packages/gnome-encfs-manager-bzr/) are available.

### Mount using gnome-encfs

gnome-encfs integrates EncFS folders into the GNOME desktop by storing their passwords in the keyring and optionally mounting them at login using GNOME's autostart mechanism. See [https://bitbucket.org/obensonne/gnome-encfs/](https://bitbucket.org/obensonne/gnome-encfs/). This method has the advantage that mounting and can automated and the password does not have to be the same as your user password.

### Mount using CryptKeeper trayicon

Quite simple app, just [install](/index.php/Install "Install") [cryptkeeper](https://aur.archlinux.org/packages/cryptkeeper/) and add it to your X session.

### Mount using encfsui

A bash script [encfsui](http://github.com/bulletmark/encfsui) provides a simple [zenity](https://www.archlinux.org/packages/?name=zenity) gui around the EncFS command line utility to mount and unmount an encrypted directory. It includes a desktop launcher. Install it from [encfsui](https://aur.archlinux.org/packages/encfsui/).

### Mount via fstab

Adding an entry in `/etc/fstab` will allow you to mount the encfs volume with a simple `mount /target/path` and you will be prompted for your password.

 `/etc/fstab` 
```
encfs#/path/to/encfs/data  /mnt/decrypted  fuse  noauto,user  0  0

```

The `noauto` option prevents an attempt to mount the volume at boot, which could delay the boot process while it waits for a password to be entered. `user` can be omitted if only the `root` user should be able to mount the volume.

### Mount at login using pam_encfs

Install [pam_encfs](https://aur.archlinux.org/packages/pam_encfs/). See also:

*   [http://pam-encfs.googlecode.com/svn/trunk/README](http://pam-encfs.googlecode.com/svn/trunk/README)
*   [http://pam-encfs.googlecode.com/svn/trunk/pam_encfs.conf](http://pam-encfs.googlecode.com/svn/trunk/pam_encfs.conf)
*   [https://wiki.edubuntu.org/EncryptedHomeFolder](https://wiki.edubuntu.org/EncryptedHomeFolder)
*   [http://code.google.com/p/pam-encfs/](http://code.google.com/p/pam-encfs/)

#### Single password

**Warning:** Note that if you will use same password (eg.: using try_first_pass or use_first_pass) for login and encfs (so encfs will mount during your login) then you should use [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes") (Preferably SHA512 with some huge number of rounds) and (which is most important) **secure password**, because hash of your password is probably stored in unencrypted form in `/etc/shadow` and it can be cracked in order to get your encfs password (because it is same as your regular unix login password).

#### /etc/pam.d/

Note that when you are using *try_first_pass* parameter to *pam_unix.so* then you will have to set EncFS to use same password as you are using to login (or vice-versa) and you will be entering just single password. Without this parameter you will need to enter two passwords.

##### setup pam_encfs for all login methods

Put encfs line to /etc/pam.d/system-login as follows:

```
...
auth       sufficient pam_encfs.so
...

```

##### login

This section tells how to make encfs automount when you are logging in by virtual terminal.

**Note:** If you only want to use it through GDM, you may pass this and go right to the [GDM section](#gdm) below.

Edit the file `/etc/pam.d/login`:

```
#%PAM-1.0

auth		required	pam_securetty.so
auth		requisite	pam_nologin.so
auth		sufficient	pam_encfs.so
auth		required	pam_unix.so nullok try_first_pass
#auth		required	pam_unix.so nullok
auth		required	pam_tally.so onerr=succeed file=/var/log/faillog
# use this to lockout accounts for 10 minutes after 3 failed attempts
#auth		required	pam_tally.so deny=2 unlock_time=600 onerr=succeed file=/var/log/faillog
account		required	pam_access.so
account		required	pam_time.so
account		required	pam_unix.so
#password	required	pam_cracklib.so difok=2 minlen=8 dcredit=2 ocredit=2 retry=3
#password	required	pam_unix.so md5 shadow use_authtok
session		required	pam_unix.so
session		required	pam_env.so
session		required	pam_motd.so
session		required	pam_limits.so
session		optional	pam_mail.so dir=/var/spool/mail standard
session		optional	pam_lastlog.so
session		optional	pam_loginuid.so
-session	optional	pam_ck_connector.so nox11
#Automatic unmount (optional):
#session	required	pam_encfs.so

```

**Warning:** Note that automatic unmount will process even when there is another session. eg.: logout on VC can unmount encfs mounted by GDM session that is still active.

##### gdm

This section explains how to make encfs automount when you are logging in by GDM.

**Note:** For debug purposes you may try automount on virtual console login first. [This article has a section about automount on virtual console login](#login).

Edit the file `/etc/pam.d/gdm-password`.

Insert (do not overwrite) the following into the bottom of gdm-password:

```
#%PAM-1.0
auth            requisite       pam_nologin.so
auth            required        pam_env.so
auth            sufficient      pam_encfs.so
auth            required        pam_unix.so try_first_pass
auth            optional        pam_gnome_keyring.so
account         required        pam_unix.so
session         required        pam_limits.so
session         required        pam_unix.so
session         optional        pam_gnome_keyring.so auto_start
password        required        pam_unix.so
session         required        pam_encfs.so

```

Save and exit.

##### Configuration

Edit `/etc/security/pam_encfs.conf` :

Recommended: comment out the line

```
encfs_default --idle=1

```

This flag will unmount your encrypted folder after 1 minute of inactivity. If you are automounting this on login, you probably would like to keep this mounted for as long as you are logged in.

At the bottom, comment any existing demo entries and add:

```
#USERNAME       SOURCE                                  TARGET PATH                 ENCFS Options           FUSE Options
foo             /home/foo/EncryptedFolder             /home/foo/DecryptedFolder       -v                    allow_other

```

**Note:** It is not possible to mount multiple EncFS folders at login using `pam_encfs`. If multiple entries are specified in `/etc/security/pam_encfs.conf`, only the first one will be mounted, and the rest will be ignored. To mount multiple EncFS folders at login it is necessary to use [pam_mount](/index.php/Pam_mount "Pam mount"). See [#Mount at login using pam_mount](#Mount_at_login_using_pam_mount) for details.

Also, if you see the following line, remove `allow_root` from the options. Otherwise, it will be in conflict with `allow_other` defined above.

```
fuse_default allow_root,nonempty

```

Next, edit `/etc/fuse.conf`: Uncomment:

```
user_allow_other

```

To test your config, open a new virtual terminal (e.g. `Ctrl+Alt+F4`) and login. You should see pam successfuly mount your EncFS folder.

### Mount at login using pam_mount

Install and configure [pam_mount](/index.php/Pam_mount "Pam mount") as explained on its wiki page. EncFS mounts can be specified in pam_mount's configuration file as follows:

 `/etc/security/pam_mount.conf.xml`  `<volume fstype="fuse" path="encfs#*/path/to/encfs/encrypted/data*" mountpoint="*/path/to/decrypted/data/mountpoint*" options="nonempty" />` 

The EncFS mounts need to have the same password than your user account. The `nonempty` option makes it possible to mount the encrypted file system even when the mount point is non-empty. You may remove this option if this is not the desired behaviour.

It is possible to mount multiple EncFS folders at login specifying multiple consecutive `<volume>` entries in the configuration file.

### Mount when USB drive with EncFS folders is inserted using fsniper

Simple method to automount (asking for password) encfs when USB drive with EncFS one or more folders in root is inserted. We will use [fsniper](https://aur.archlinux.org/packages/fsniper/) (filesystem watching daemon using inotify) and [git](https://www.archlinux.org/packages/?name=git) (for askpass binary).

See more at [https://github.com/Harvie/Programs/tree/master/bash/encfs/automount](https://github.com/Harvie/Programs/tree/master/bash/encfs/automount) (latest version of files used in the [How to](#How_to)).

#### How to

**1.** You need USB automount working for this - like Thunar or Gnome Files does.
**2.** Make encrypted folder on your drive, eg.: `encfs /media/USB/somename /media/USB/somename.plain` (and then unmount everything).
**3.** Create a `~/.config/fsniper/config` file:

```
watch {
	/etc/ {
		mtab {
			# %% is replaced with the filename of the new file
			handler = encfs-automount.sh %%;
		}
	}
}

```

**4.** install helper script:

```
#!/bin/sh
#	~/.config/fsniper/scripts/encfs-automount.sh
# Quick & dirty script for automounting EncFS USB drives
# TODO:
#  - Unmounting!!!
#
ASKPASS="/usr/lib/git-core/git-gui--askpass"

lock=/tmp/fsniper_encfs.lock
lpid=$(cat "$lock" 2>/dev/null) &&
ps "$lpid" | grep "$lpid" >/dev/null && {
	echo "Another instance of fsniper_encfs is running"
	exit;
}
echo $BASHPID > "$lock";
sleep 2;

echo
echo ==== EncFS automount script for fsniper ====

list_mounts() {
	cat /proc/mounts | cut -d ' ' -f 2
}

list_mounts | while read mount; do
	config="$mount"'/*/.encfs*';
	echo Looking for "$config"
	config="$(echo $config)"
	[ -r "$config" ] && {
		cyphertext="$(dirname "$config")";
		plaintext="$cyphertext".plain
		echo Found config: "$config";
		echo Trying to mount: "$cyphertext to $plaintext";
		list_mounts | grep "$plaintext" >/dev/null && {
			echo Already mounted: "$plaintext"
		} || {
			echo Will mount "$cyphertext to $plaintext"
			"$ASKPASS" "EncFS $cyphertext to $plaintext" | encfs --stdinpass "$cyphertext" "$plaintext"
		}
	}
done
echo

rm "$lock" 2>/dev/null

```

**5.** Make sure that /usr/lib/git-core/git-gui--askpass is working for you (that is why you need git package - but you can adjust the helper script).
**6.** Try `fsniper --log-to-stdout` in terminal (askpass should appear when USB drive is inserted).
**7.** Add `fsniper --daemon` to your session.
**8.** Do not forget to unmount encfs before removing drive.

### Mount using KDE KWallet

This can be done in KDE with the [kdeencfs](http://pastebin.com/RR1hguwE) script. You will also have to [install](/index.php/Install "Install") the [kdialog](https://www.archlinux.org/packages/?name=kdialog), [kdebase-runtime](https://www.archlinux.org/packages/?name=kdebase-runtime), [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools) and [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) packages from the [official repositories](/index.php/Official_repositories "Official repositories"). kwallet-pam has to started with the session which it is by default. *(If not: Add /usr/lib/pam_kwallet_init to sessionstart.)* It can be used by calling *kdeencfs encrypted-folder decrypted-folder*.

## Encrypted backup

**Warning:** If you follow below examples to separate the encryption options file from the data, you - of course - need to ensure you have a separate backup of the options file in plaintext as well. If your disk crashes and you have not backed it up in plaintext, the backup alone will help nothing because the file contains cryptographic metadata! The good point is that the file is static, you do not need to back it up repetitively over time unless you change the password.

### Backup encrypted directory

An encrypted directory may be backed up and restored to another location like it is. This is possible, because the configuration file for the encryption options/metadata is actually stored in the directory itself in plaintext in the hidden `.encfs6.xml` file. This poses no direct problem, because the password is not in it.

However, if you - for example - store the backup on a remote location (e.g. in the cloud) or a portable device, you might feel uncomfortable about it. In this case it also is no problem to manually move the file out of the directory before creating the backup. You can even move it permanently and still mount and access the files, if you pass its location to *encfs* via the `ENCFS6_CONFIG` environment variable. For the [#Usage](#Usage) example above:

```
$ mv ~/.name/encfs6.xml ~/.
$ ENCFS6_CONFIG=~/encfs6.xml encfs ~/.name ~/name

```

### Backup plaintext directory

The following example assumes you want to create an encrypted backup of an existing plaintext directory `~/mythesis` which contains the file `thesis.txt`.

First, we create the encrypted backup of the existing plaintext directory:

```
$ encfs --reverse ~/mythesis /tmp/thesisbackup 

```

Note the directory order is reversed to normal usage in this case. Using the `--reverse` option has two effects: Firstly, the configuration file is now stored in the plaintext directory and `/tmp/thesisbackup` only contains it in encrypted form. Secondly, the files in `/tmp/thesisbackup` are not persistent. They will vanish once it is unmounted (no, this is not due to usage of the `/tmp` mountpoint).

For the second reason, now is the time to copy the encrypted files to the desired backup location, *before* unmounting the temporary *encfs* directory again:

```
$ cp -R /tmp/thesisbackup/* /mnt/usbstick/
$ fusermount -u /tmp/thesisbackup 

```

and done.

To restore (or view) the backup, we need access to the encryption options in plaintext, which has to be passed to *encfs* with the environment variable `ENCFS6_CONFIG` (we use a different directory in order not to mess up the existing `~/mythesis`):

```
$ ENCFS6_CONFIG=~/mythesis/.encfs6.xml encfs ~/mnt/usbstick/thesisbackup ~/restoremythesis 

```

If you now list the restore location, it will contain two files:

```
$ ls -la ~/restoremythesis
... 
-rw-r--r--  1 student student    1078  3\. Jan 12:33 .encfs6.xml
-rw-r--r--  1 student student      42  3\. Jan 12:33 thesis.txt
...

```

## See also

*   [EncFS](https://vgough.github.io/encfs/) - project homepage
*   [Security audit](https://defuse.ca/audits/encfs.htm) of EncFS by Taylor Hornby (January 14, 2014).
*   [EncFS micro-how-to](https://www.ict.griffith.edu.au/anthony/info/crypto/encfs.hints) by Anthony Thyssen.