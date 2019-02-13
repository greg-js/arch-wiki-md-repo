**Estado de la traducción**
Este artículo es una traducción de [SSHFS](/index.php/SSHFS "SSHFS"), revisada por última vez el **2019-02-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=SSHFS&diff=0&oldid=566372) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [SCP and SFTP](/index.php/SCP_and_SFTP "SCP and SFTP")
*   [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot")
*   [Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")
*   [sftpman](/index.php/Sftpman "Sftpman")

[SSHFS](https://github.com/libfuse/sshfs) es un cliente de sistema de archivos basado en FUSE para montar directorios remotos a través de una conexión [Secure Shell](/index.php/Secure_Shell "Secure Shell").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
    *   [1.1 Montando](#Montando)
    *   [1.2 Desmontando](#Desmontando)
*   [2 Opciones](#Opciones)
*   [3 Chrooting](#Chrooting)
*   [4 Automounting](#Automounting)
    *   [4.1 On demand](#On_demand)
    *   [4.2 On boot](#On_boot)
    *   [4.3 Secure user access](#Secure_user_access)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Checklist](#Checklist)
    *   [5.2 Connection reset by peer](#Connection_reset_by_peer)
    *   [5.3 Remote host has disconnected](#Remote_host_has_disconnected)
    *   [5.4 fstab mounting issues](#fstab_mounting_issues)
*   [6 See also](#See_also)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [sshfs](https://www.archlinux.org/packages/?name=sshfs).

**Sugerencia:**

*   Si a menudo necesita montar sistemas de archivos sshfs, puede estar interesado en utilizar un ayudante sshfs, como [qsshfs](https://aur.archlinux.org/packages/qsshfs/), [sftpman](/index.php/Sftpman "Sftpman"), [sshmnt](https://aur.archlinux.org/packages/sshmnt/) o [fmount.py](https://github.com/lahwaacz/Scripts/blob/master/fmount.py).
*   Es posible que desee utilizar [Google Authenticator](/index.php/Google_Authenticator_(Espa%C3%B1ol) "Google Authenticator (Español)") para proporcionar seguridad adicional como es la autenticación de dos pasos.
*   [SSH keys](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)") puede ser utilizado sobre la autenticación tradicional de contraseña.

### Montando

Para poder montar un directorio, el usuario de SSH necesita poder acceder a él. Invoque *sshfs* para montar un directorio remoto:

```
$ sshfs *[usuario@]host:[dir] puntodemontaje [opciones]*

```

Por ejemplo:

```
$ sshfs miusuario@micomputadora:/ruta/remota /ruta/local -C -p 9876

```

Aquí `-p 9876` especifica el número de puerto y `-C` activa la compresión. Para más opciones véase la sección [#Opciones](#Opciones).

Cuando no se especifica, la ruta remota se establece de manera predeterminada en el directorio de inicio del usuario remoto. Los nombres de usuario y las opciones predeterminadas se pueden predefinir para cada computadora en `~/.ssh/config` para simplificar el uso de *sshfs*. Para obtener más información, véase [OpenSSH#Client use](/index.php/OpenSSH#Client_use "OpenSSH").

SSH le pedirá la contraseña, si es necesario. Si no desea escribir la contraseña varias veces al día, véase [SSH keys](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)").

### Desmontando

Para desmontar el sistema remoto:

```
$ fusermount3 -u *puntodemontaje*

```

Por ejemplo:

```
$ fusermount3 -u /ruta/local

```

## Opciones

*sshfs* can automatically convert between local and remote user IDs. Use the `idmap=user` option to translate the UID of the connecting user to the remote user `myuser` (GID remains unchanged):

```
$ sshfs myuser@mycomputer:/remote/path /local/path -o idmap=user

```

If you need more control over UID and GID translation, look at the options `idmap=file`, `uidfile` and `gidfile`.

A complete list of options can be found in [sshfs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshfs.1).

## Chrooting

You may want to restrict a specific user to a specific directory on the remote system. This can be done by editing `/etc/ssh/sshd_config`:

 `/etc/ssh/sshd_config` 
```
.....
Match User *someuser* 
       ChrootDirectory */chroot/%u*
       ForceCommand internal-sftp
       AllowTcpForwarding no
       X11Forwarding no
.....

```

**Note:** The chroot directory **must** be owned by root, otherwise you will not be able to connect.

See also [SFTP chroot](/index.php/SFTP_chroot "SFTP chroot"). For more information check the [sshd_config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshd_config.5) man page for `Match`, `ChrootDirectory` and `ForceCommand`.

## Automounting

Automounting can happen on boot, or on demand (when accessing the directory). For both, the setup happens in the [fstab](/index.php/Fstab "Fstab").

**Note:** Keep in mind that automounting is done through the root user, therefore you cannot use hosts configured in `.ssh/config` of your normal user.

To let the root user use an SSH key of a normal user, specify its full path in the `IdentityFile` option.

**And most importantly**, use each sshfs mount at least once manually **while root** so the host's signature is added to the `/root/.ssh/known_hosts` file.

### On demand

With systemd on-demand mounting is possible using `/etc/fstab` entries.

Example:

```
user@host:/remote/folder /mount/point  fuse.sshfs noauto,x-systemd.automount,_netdev,users,idmap=user,IdentityFile=/home/user/.ssh/id_rsa,allow_other,reconnect 0 0

```

The important mount options here are *noauto,x-systemd.automount,_netdev*.

*   *noauto* tells it not to mount at boot
*   *x-systemd.automount* does the on-demand magic
*   *_netdev* tells it that it is a network device, not a block device (without it "No such device" errors might happen)

**Note:** After editing `/etc/fstab`, (re)start the required service: `systemctl daemon-reload && systemctl restart <target>` where `<target>` can be found by running `systemctl list-unit-files --type automount`

**Tip:** [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) do not require editing `/etc/fstab` to add a new mountpoint. Instead, regular users can create one by simply attempting to access it (with e. g. something like `ls ~/mnt/ssh/[user@]yourremotehost[:port]`). [autosshfs-git](https://aur.archlinux.org/packages/autosshfs-git/) uses AutoFS. Users need to be enabled to use it with `autosshfs-user`.

### On boot

An example on how to use sshfs to mount a remote filesystem through `/etc/fstab`

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs  defaults,_netdev  0  0

```

Take for example the *fstab* line

```
llib@192.168.1.200:/home/llib/FAH  /media/FAH2  fuse.sshfs  defaults,_netdev  0  0

```

The above will work automatically if you are using an SSH key for the user. See [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

If you want to use sshfs with multiple users:

```
user@domain.org:/home/user  /media/user   fuse.sshfs    defaults,allow_other,_netdev    0  0

```

Again, it is important to set the *_netdev* mount option to make sure the network is available before trying to mount.

### Secure user access

When automounting via [fstab](/index.php/Fstab "Fstab"), the filesystem will generally be mounted by root. By default, this produces undesireable results if you wish access as an ordinary user and limit access to other users.

An example mountpoint configuration:

```
USERNAME@HOSTNAME_OR_IP:/REMOTE/DIRECTORY  /LOCAL/MOUNTPOINT  fuse.sshfs noauto,x-systemd.automount,_netdev,user,idmap=user,follow_symlinks,identityfile=/home/USERNAME/.ssh/id_rsa,allow_other,default_permissions,uid=USER_ID_N,gid=USER_GID_N 0 0

```

Summary of the relevant options:

*   *allow_other* - Allow other users than the mounter (i.e. root) to access the share.
*   *default_permissions* - Allow kernel to check permissions, i.e. use the actual permissions on the remote filesystem. This allows prohibiting access to everybody otherwise granted by *allow_other*.
*   *uid*, *gid* - set reported ownership of files to given values; *uid* is the numeric user ID of your user, *gid* is the numeric group ID of your user.

## Troubleshooting

### Checklist

Read [OpenSSH#Checklist](/index.php/OpenSSH#Checklist "OpenSSH") first. Further issues to check are:

1\. Is your SSH login sending additional information from server's `/etc/issue` file e.g.? This might confuse SSHFS. You should temporarily deactivate server's `/etc/issue` file:

```
$ mv /etc/issue /etc/issue.orig

```

2\. Keep in mind that most SSH related troubleshooting articles you will find on the web are **not** Systemd related. Often `/etc/fstab` definitions wrongly begin with `*sshfs#*user@host:/mnt/server/folder ... fuse ...` instead of using the syntax `user@host:/mnt/server/folder ... fuse.*sshfs* ... *x-systemd*, ...`.

3\. Check that the owner of server's source folder and content is owned by the server's user.

```
$ chown -R USER_S: /mnt/servers/folder

```

4\. The server's user ID can be different from the client's one. Obviously both user names have to be the same. You just have to care for the client's user IDs. SSHFS will translate the UID for you with the following mount options:

```
uid=*USER_C_ID*,gid=*GROUP_C_ID*

```

5\. Check that the client's target mount point (folder) is owned by the client user. This folder should have the same user ID as defined in SSHFS's mount options.

```
$ chown -R USER_C: /mnt/client/folder

```

6\. Check that the client's mount point (folder) is empty. By default you cannot mount SSHFS folders to non-empty folders.

### Connection reset by peer

*   If you are trying to access the remote system with a hostname, try using its IP address, as it can be a domain name solving issue. Make sure you edit `/etc/hosts` with the server details.
*   If you are using non-default key names and are passing it as `-i .ssh/my_key`, this will not work. You have to use `-o IdentityFile=/home/user/.ssh/my_key`, with the full path to the key.
*   If your `/root/.ssh/config` is a symlink, you will be getting this error as well. See [this serverfault topic](http://serverfault.com/questions/507748/bad-owner-or-permissions-on-root-ssh-config)
*   Adding the option '`sshfs_debug`' (as in '`sshfs -o sshfs_debug user@server ...`') can help in resolving the issue.
*   If that doesn't reveal anything useful, you might also try adding the option '`debug`'
*   If you are trying to sshfs into a router running DD-WRT or the like, there is a solution [here](http://www.dd-wrt.com/wiki/index.php/SFTP_with_DD-WRT). (note that the -osftp_server=/opt/libexec/sftp-server option can be used to the sshfs command in stead of patching dropbear)
*   If you see this only on boot, it may be that systemd is attempting to mount prior to a network connection being available. Enabling the 'wait-online' service appropriate to your network connection (eg. systemd-networkd-wait-online.service) fixes this.
*   Old Forum thread: [sshfs: Connection reset by peer](https://bbs.archlinux.org/viewtopic.php?id=27613)
*   Make sure your user can log into the server (especially when using AllowUsers)
*   Make sure `Subsystem sftp /usr/lib/ssh/sftp-server` is enabled in `/etc/ssh/sshd_config`.

**Note:** When providing more than one option for sshfs, they must be comma separated. Like so: '`sshfs -o sshfs_debug,IdentityFile=</path/to/key> user@server ...`')

### Remote host has disconnected

If you receive this message directly after attempting to use *sshfs*:

*   First make sure that the **remote** machine has *sftp* installed! It will not work, if not.
*   Then, check that the path of the `Subsystem sftp` in `/etc/ssh/sshd_config` on the remote machine is valid.

### fstab mounting issues

To get verbose debugging output, add the following to the mount options:

```
ssh_command=ssh\040-vv,sshfs_debug,debug

```

**Note:** Here, `\040` represents a space which fstab uses to separate fields.

To be able to run `mount -av` and see the debug output, remove the following:

```
 noauto,x-systemd.automount

```

## See also

*   [How to mount chrooted SSH filesystem](http://wiki.gilug.org/index.php/How_to_mount_SFTP_accesses), with special care with owners and permissions questions.