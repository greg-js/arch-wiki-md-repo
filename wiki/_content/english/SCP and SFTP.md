Related articles

*   [SSHFS](/index.php/SSHFS "SSHFS")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")

The [Secure copy (SCP)](https://en.wikipedia.org/wiki/Secure_copy "wikipedia:Secure copy") is a protocol to transfer files via a [Secure Shell](/index.php/Secure_Shell "Secure Shell") connection. The [SSH file transfer protocol (SFTP)](https://en.wikipedia.org/wiki/SSH_file_transfer_protocol "wikipedia:SSH file transfer protocol") is a related protocol, also relying on a secure shell back-end. Both protocols allow secure file transfers, encrypting passwords and transferred data. The SFTP protocol, however, features additional capabilities like, for example, resuming broken transfers or remote file manipulation like deletion.

## Contents

*   [1 Secure file transfer protocol (SFTP)](#Secure_file_transfer_protocol_.28SFTP.29)
*   [2 Secure file transfer protocol (SFTP) with a chroot jail](#Secure_file_transfer_protocol_.28SFTP.29_with_a_chroot_jail)
    *   [2.1 Setup the filesystem](#Setup_the_filesystem)
    *   [2.2 Create an unprivileged user](#Create_an_unprivileged_user)
    *   [2.3 Setup openssh](#Setup_openssh)
*   [3 Secure copy protocol (SCP)](#Secure_copy_protocol_.28SCP.29)
    *   [3.1 Scponly](#Scponly)
        *   [3.1.1 Adding a chroot jail](#Adding_a_chroot_jail)

## Secure file transfer protocol (SFTP)

Install and configure [OpenSSH](/index.php/OpenSSH "OpenSSH"). Once running, SFTP is available by default.

Access files with the *sftp* program or [SSHFS](/index.php/SSHFS "SSHFS"). Many standard FTP programs should work as well.

## Secure file transfer protocol (SFTP) with a chroot jail

Sysadmins can jail a subset of users to a chroot jail using [openssh](https://www.archlinux.org/packages/?name=openssh) thus restricting their access to a particular directory tree. This can be useful to simply share some files without granting full system access or shell access. Users with this type of setup may use SFTP programs such as [filezilla](https://www.archlinux.org/packages/?name=filezilla) to put/get files in the chroot jail.

### Setup the filesystem

Create a jail directory:

```
# mkdir -p /var/lib/jail

```

**Note:** Readers may select a file access scheme on their own. For example, optionally create a subdirectory for an incoming (writable) space and/or a read-only space. This need not be done directly under /var/lib/jail ... it can be accomplished on the live partition which will be mounted via a bind mount as well.

Bind mount the live filesystem to be shared to this directory. In this example, /mnt/data/share is to be used. It is owned by root and has octal permissions of 755.

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

### Setup openssh

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

Test that in fact, the restrictions are enforced by attempting an ssh connection via the shell. The ssh sever should return a polite notice of the setup:

```
$ ssh foo@someserver.com
foo@someserver.com's password:
This service allows sftp connections only.
Connection to someserver.com closed.

```

## Secure copy protocol (SCP)

[Install](/index.php/Install "Install"), configure and [start](/index.php/Start "Start") [openssh](https://www.archlinux.org/packages/?name=openssh). It contains a *scp* command to transfer files. See [Secure Shell](/index.php/Secure_Shell "Secure Shell") for more information.

More features are available by installing additional packages, for example [rssh](https://aur.archlinux.org/packages/rssh/) or [scponly](https://www.archlinux.org/packages/?name=scponly) described below.

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