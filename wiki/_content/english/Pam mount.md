[pam_mount](http://pam-mount.sourceforge.net/) can be used to automatically mount an encrypted home partition (encrypted with, for example, [LUKS](/index.php/LUKS "LUKS") or [ECryptfs](/index.php/ECryptfs "ECryptfs")) on user log in. It will mount your /home (or whatever mount point you like) when you log in using your login manager or when logging in on console. The encrypted drive's passphrase should be the same as your linux user's password, so you do not have to type in two different passphrases to login.

**Warning:** Pam_mount can also unmount your partitions when you close your last session but this is currently not working due to the use of pam_systemd.so in the pam stack.

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
*   Add mount options, if needed.

 `/etc/security/pam_mount.conf.xml` 
```
**<volume user="USERNAME" fstype="auto" path="/dev/sdaX" mountpoint="/home" options="fsck,noatime" />**
**<mkmountpoint enable="1" remove="true" />**

</pam_mount>
```

## Login Manager Configuration

In general, you have to edit configuration files in /etc/pam.d so that pam_mount will be called on login. The correct order of entries in each file is important. It is necessary to edit /etc/pam.d/system-auth as shown below. If you use a display manager (e.g., Slim or GDM) edit its file, too. Example configuration files follow, with the added lines in bold.

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

For [GDM](/index.php/GDM "GDM"):

**Note:** The configuration file has changed to be /etc/pam.d/gdm-password (instead of /etc/pam.d/gdm) as of GDM version 3.2.
 `/etc/pam.d/gdm-password` 
```
#%PAM-1.0
auth            requisite       pam_nologin.so
auth            required        pam_env.so

auth            requisite       pam_unix.so nullok
**auth	        optional        pam_mount.so**
auth            optional        pam_gnome_keyring.so

auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so

account         required        pam_unix.so

password        required        pam_unix.so
**password        optional        pam_mount.so**

session         required        pam_loginuid.so
-session        optional        pam_systemd.so
session         optional        pam_keyinit.so force revoke
session         required        pam_limits.so
session         required        pam_unix.so
**session         optional        pam_mount.so**
session         optional        pam_gnome_keyring.so auto_start
```