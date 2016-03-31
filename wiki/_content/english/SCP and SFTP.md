The [Secure copy (SCP)](https://en.wikipedia.org/wiki/Secure_copy "wikipedia:Secure copy") is a protocol to transfer files via a [Secure Shell](/index.php/Secure_Shell "Secure Shell") connection. The [SSH file transfer protocol (SFTP)](https://en.wikipedia.org/wiki/SSH_file_transfer_protocol "wikipedia:SSH file transfer protocol") is a related protocol, also relying on a secure shell back-end. Both protocols allow secure file transfers, encrypting passwords and transferred data. The SFTP protocol, however, features additional capabilities like, for example, resuming broken transfers or remote file manipulation like deletion.

## Contents

*   [1 Secure file transfer protocol (SFTP)](#Secure_file_transfer_protocol_.28SFTP.29)
*   [2 Secure copy protocol (SCP)](#Secure_copy_protocol_.28SCP.29)
    *   [2.1 Scponly](#Scponly)
        *   [2.1.1 Adding a chroot jail](#Adding_a_chroot_jail)

## Secure file transfer protocol (SFTP)

To set up SFTP you only need to install and configure [OpenSSH](/index.php/OpenSSH "OpenSSH"). Once you have this running, SFTP is running too because the default configuration file enables it. Follow the instructions below for older configs.

Open `/etc/ssh/sshd_config` with your favorite editor and add this line if it does not already exist:

```
Subsystem sftp /usr/lib/ssh/sftp-server

```

[Restart](/index.php/Restart "Restart") the `sshd.service` daemon and it should work.

You can access your files with the *sftp* program or [SSHFS](/index.php/SSHFS "SSHFS"). Many standard FTP programs should work as well.

## Secure copy protocol (SCP)

[Install](/index.php/Install "Install"), configure and [start](/index.php/Start "Start") [openssh](https://www.archlinux.org/packages/?name=openssh). It contains a *scp* command to transfer files. See [Secure Shell](/index.php/Secure_Shell "Secure Shell") for more information.

More features are available by installing additional packages, for example [rssh](https://aur.archlinux.org/packages/rssh/) or [scponly](https://www.archlinux.org/packages/?name=scponly) described below.

### Scponly

[Scponly](https://github.com/scponly/scponly/wiki) is a limited shell for allowing users scp/sftp access and only scp/sftp access to your box. Additionally, you can setup *scponly* to chroot the user into a particular directory increasing the level of security.

[install](/index.php/Install "Install") [scponly](https://www.archlinux.org/packages/?name=scponly).

If you have a user already created, simply set the user's shell to scponly:

```
# usermod -s /usr/bin/scponly *username*

```

That is it. Go ahead and test it using your favorite sftp client.

#### Adding a chroot jail

The package comes with a script to create a chroot. To use it:

 `# cd /usr/share/doc/scponly/`  `# ./setup_chroot.sh` 

*   Provide answers
*   Check that `/path/to/chroot` has `root:root` owner and `r-x` for others
*   Change the shell for selected user to `/usr/bin/scponlyc`
*   sftp-server may require some libnss modules such as libnss_files. Copy them to chroot's `/lib` path.