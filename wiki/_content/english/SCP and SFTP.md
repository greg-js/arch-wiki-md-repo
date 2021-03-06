Related articles

*   [SSHFS](/index.php/SSHFS "SSHFS")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")

The [Secure copy (SCP)](https://en.wikipedia.org/wiki/Secure_copy "wikipedia:Secure copy") is a protocol to transfer files via a [Secure Shell](/index.php/Secure_Shell "Secure Shell") connection. The [SSH file transfer protocol (SFTP)](https://en.wikipedia.org/wiki/SSH_file_transfer_protocol "wikipedia:SSH file transfer protocol") is a related protocol, also relying on a secure shell back-end. Both protocols allow secure file transfers, encrypting passwords and transferred data. The SFTP protocol, however, features additional capabilities like, for example, resuming broken transfers or remote file manipulation like deletion.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Secure file transfer protocol (SFTP)](#Secure_file_transfer_protocol_(SFTP))
*   [2 Secure file transfer protocol (SFTP) with a chroot jail](#Secure_file_transfer_protocol_(SFTP)_with_a_chroot_jail)
    *   [2.1 Setup the filesystem](#Setup_the_filesystem)
    *   [2.2 Create an unprivileged user](#Create_an_unprivileged_user)
    *   [2.3 Setup OpenSSH](#Setup_OpenSSH)
    *   [2.4 Uploads to Chroot jail root dir](#Uploads_to_Chroot_jail_root_dir)
*   [3 Secure copy protocol (SCP)](#Secure_copy_protocol_(SCP))
    *   [3.1 General Usage](#General_Usage)
        *   [3.1.1 Linux to Linux](#Linux_to_Linux)
        *   [3.1.2 Linux to Windows](#Linux_to_Windows)
    *   [3.2 Scponly](#Scponly)
        *   [3.2.1 Adding a chroot jail](#Adding_a_chroot_jail)

## Secure file transfer protocol (SFTP)

Install and configure [OpenSSH](/index.php/OpenSSH "OpenSSH"). Once running, SFTP is available by default.

Access files with the *sftp* program or [SSHFS](/index.php/SSHFS "SSHFS"). Many standard FTP programs should work as well.

## Secure file transfer protocol (SFTP) with a chroot jail

Sysadmins can jail a subset of users to a chroot jail using [openssh](https://www.archlinux.org/packages/?name=openssh) thus restricting their access to a particular directory tree. This can be useful to simply share some files without granting full system access or shell access. Users with this type of setup may use SFTP clients such as [filezilla](https://www.archlinux.org/packages/?name=filezilla) to put/get files in the chroot jail.

### Setup the filesystem

Create a jail directory:

```
# mkdir -p /var/lib/jail

```

Optionally, bind mount the filesystem to be shared to this directory. In this example, `/mnt/data/share` is to be used. It is owned by root and has octal permissions of 755.

```
# mount -o bind /mnt/data/share /var/lib/jail

```

**Tip:** Consider adding an entry to `/etc/fstab` to make the bind mount survive a reboot.

### Create an unprivileged user

Create the share user and setup a good password:

```
# useradd -g sshusers -d /var/lib/jail foo
# passwd foo

```

### Setup OpenSSH

Add the following to the end of `/etc/ssh/sshd_config` to enable the share and to enforce the restrictions:

 `/etc/ssh/sshd_config` 
```
...
 Match group sshusers
  ChrootDirectory %h
  X11Forwarding no
  AllowTcpForwarding no
  PasswordAuthentication yes
  ForceCommand internal-sftp

```

[Restart](/index.php/Restart "Restart") `sshd.service` to re-read the config file.

Test that in fact, the restrictions are enforced by attempting an ssh connection via the shell. The ssh server should return a polite notice of the setup:

 `$ ssh foo@someserver.com` 
```
foo@someserver.com's password:
This service allows sftp connections only.
Connection to someserver.com closed.

```

### Uploads to Chroot jail root dir

For security reasons the directory set as the chroot directory must be owned by root with only root having write access to it otherwise sftp/ssh connections will be denied. This of course means regular users cannot upload files to the root directory. In order to get around this while not compromising security you can create a folder inside the chroot directory which the regular user or group has write access to, e.g:

```
# cd /var/lib/jail
# mkdir uploads
# chown :sshusers uploads
# chmod 730 uploads

```

**Note:** This will only allow users of group "sshusers" to upload to (but not list the contents of) the "uploads" directory. Use `chmod 770` to allow sshusers to view contents.

Some applications utilizing SFTP do not allow input of sub-directories when performing operations (e.g. uploading files), and will attempt to upload files to the chroot base directory (which will be denied). In order to force these applications to use a specific sub-directory you can append the following to the "ForceCommand" option:

 `/etc/ssh/sshd_config` 
```
...
 Match group sshusers
  ...
  ForceCommand internal-sftp -d /uploads

```

Users on connect will then have their start directory change to the specified sub-directory (remember to restart the sshd server).

## Secure copy protocol (SCP)

[Install](/index.php/Install "Install"), configure and [start](/index.php/Start "Start") [OpenSSH](/index.php/OpenSSH "OpenSSH"). It contains the *scp* utility to transfer files.

More features are available by installing additional packages, for example [rssh](https://aur.archlinux.org/packages/rssh/) or [scponly](https://www.archlinux.org/packages/?name=scponly) described below.

**Note:** The scp protocol is outdated, inflexible and not readily fixed. Its authors recommend the use of more modern protocols like sftp and rsync for file transfer instead.[[1]](https://lists.mindrot.org/pipermail/openssh-unix-dev/2019-March/037672.html)

### General Usage

#### Linux to Linux

Copy file from a remote host to local host SCP example:

```
$ scp username@from_host:file.txt /local/directory/

```

Copy file from local host to a remote host SCP example:

```
$ scp file.txt username@to_host:/remote/directory/

```

Copy directory from a remote host to local host SCP example:

```
$ scp -r username@from_host:/remote/directory/  /local/directory/

```

Copy directory from local host to a remote hos SCP example:

```
$ scp -r /local/directory/ username@to_host:/remote/directory/

```

Copy file from remote host to remote host SCP example:

```
$ scp username@from_host:/remote/directory/file.txt username@to_host:/remote/directory/

```

#### Linux to Windows

Use a Windows program such as [WinSCP](https://winscp.net/eng/download.php)

### Scponly

[Scponly](https://github.com/scponly/scponly/wiki) is a limited shell for allowing users scp/sftp access and only scp/sftp access. Additionally, one can setup *scponly* to chroot the user into a particular directory increasing the level of security.

[install](/index.php/Install "Install") [scponly](https://www.archlinux.org/packages/?name=scponly).

For existing users, simply set the user's shell to scponly:

```
# usermod -s /usr/bin/scponly *username*

```

#### Adding a chroot jail

The package comes with a script to create a chroot. To use it, run:

```
# /usr/share/doc/scponly/setup_chroot.sh

```

*   Provide answers
*   Check that `/path/to/chroot` has `root:root` owner and `r-x` for others
*   Change the shell for selected user to `/usr/bin/scponlyc`
*   sftp-server may require some libnss modules such as libnss_files. Copy them to chroot's `/lib` path.