[pam_mount](http://pam-mount.sourceforge.net/) can be used to automatically mount an encrypted home partition (encrypted with, for example, [LUKS](/index.php/LUKS "LUKS") or [ECryptfs](/index.php/ECryptfs "ECryptfs")) on user log in. It will mount your /home (or whatever mount point you like) when you log in using your login manager or when logging in on console. The encrypted drive's passphrase should be the same as your linux user's password, so you do not have to type in two different passphrases to login.

**Warning:**Pam_mount can also unmount your partitions when you close your last session but this is currently not working due to the use of pam_systemd.so in the pam stack.

## Contents

*   [1 General Setup](#General_Setup)
*   [2 Login Manager Configuration](#Login_Manager_Configuration)
    *   [2.1 SLiM](#SLiM)
    *   [2.2 GDM](#GDM)

## General Setup

1.  Install [pam_mount](https://www.archlinux.org/packages/?name=pam_mount) from the [Official repositories](/index.php/Official_repositories "Official repositories").
2.  Edit /etc/security/pam_mount.conf.xml as follows:

Insert 2 new lines at the end of the file, but **before** the last closing tag, *</pam_mount>*. Notes:

*   USERNAME should be replaced with your linux-username.
*   /dev/sdaX should be replaced with the corresponding device or container file.
*   fstype="auto" can be changed to any <type> that is present in /usr/bin/mount.<type>. "auto" should work fine in most cases. Use fstype="crypt" so that the loop device gets closed at logout for volumes needing it.
*   Add mount options, if needed. Note that mount.cifs does not read smb.conf and so all options must be specified. In the example, uid matches the local smb.conf parameter idmap config ... : range = so that pam_mount is not called for a unix only user. Kerberos is indicated by krb5, SMB3.0 is specified because the other end may not support SMB1 which is the default. Signing is enabled with the i on the end of krb5i. See man mount.cifs for more details.

 `/etc/security/pam_mount.conf.xml` 
```
<volume user="USERNAME" fstype="auto" path="/dev/sdaX" mountpoint="/home" options="fsck,noatime" />
  <volume
      fstype="cifs"
      server="server.example.co.uk"
      path="share_name"
      mountpoint="~/mnt/share_name"
      uid="10000-19999"
      options="sec=krb5i,vers=3.0,cruid=%(USERUID)"
  />
  <mkmountpoint enable="1" remove="true" />

</pam_mount>
```

## Login Manager Configuration

In general, you have to edit configuration files in /etc/pam.d so that pam_mount will be called on login. The correct order of entries in each file is important. It is necessary to edit /etc/pam.d/system-auth as shown below. If you use a display manager (e.g., Slim) edit its file, too. Example configuration files follow, with the added lines in bold. The pam_succeed line before pam_mount in session skips pam_mount (success=n means skip the next n lines) if the systemd-user service is running through the PAM stack. This avoids double mount attempts and errors relating to dropped privileges.

 `/etc/pam.d/system-auth` 
```
#%PAM-1.0

auth      required  pam_env.so
auth      required  pam_unix.so     try_first_pass nullok
**auth      optional  pam_mount.so**
auth      optional  pam_permit.so

account   required  pam_unix.so
account   optional  pam_permit.so
account   required  pam_time.so

**password  optional  pam_mount.so**
password  required  pam_unix.so     try_first_pass nullok sha512 shadow
password  optional  pam_permit.so

**session [success=1 default=ignore]  pam_succeed_if.so  service = systemd-user quiet**
**session   optional  pam_mount.so**
session   required  pam_limits.so
session   required  pam_env.so
session   required  pam_unix.so
session   optional  pam_permit.so
```

### SLiM

For [SLiM](/index.php/SLiM "SLiM"):

 `/etc/pam.d/slim` 
```
auth            requisite       pam_nologin.so
auth            required        pam_env.so
auth            required        pam_unix.so
**auth            optional        pam_mount.so**
account         required        pam_unix.so
password        required        pam_unix.so
**password        optional        pam_mount.so**
session         required        pam_limits.so
session         required        pam_unix.so
**session         optional        pam_mount.so**
session         optional        pam_loginuid.so
session         optional        pam_ck_connector.so

```

### GDM

Manual configuration for GDM is not needed, since it relies on `/etc/pam.d/system-auth`.