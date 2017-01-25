Back to [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system")

**Note:** This tutorial assumes you've already created your encrypted partition, as described in [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system").

**Note:** You need to use the same password for your account and for the partition.

## Contents

*   [1 Unlocking](#Unlocking)
*   [2 Mounting](#Mounting)
    *   [2.1 Explicit dependencies and ordering](#Explicit_dependencies_and_ordering)
*   [3 Unmouting on logout](#Unmouting_on_logout)
*   [4 Locking on unmount](#Locking_on_unmount)
*   [5 Tips](#Tips)
    *   [5.1 SDDM](#SDDM)

**Note:** In all the examples, replace *YOURNAME* with your username, *1000* with your user ID and */dev/PARTITION* with the path of your encrypted partition's device.

## Unlocking

Add `auth       optional   pam_exec.so expose_authtok quiet /usr/bin/cryptsetup open */dev/PARTITION* home-*YOURNAME*` after `auth       include    system-auth` in the **/etc/pam.d/system-login** config file. `/etc/pam.d/system-login **EXAMPLE**` 
```
#%PAM-1.0

auth       required   pam_tally.so         onerr=succeed file=/var/log/faillog
auth       required   pam_shells.so
auth       requisite  pam_nologin.so
auth       include    system-auth
auth       optional   pam_exec.so expose_authtok quiet /usr/bin/cryptsetup open */dev/PARTITION* home-*YOURNAME*

account    required   pam_access.so
account    required   pam_nologin.so
account    include    system-auth

password   include    system-auth

session    optional   pam_loginuid.so
session    include    system-auth
session    optional   pam_motd.so          motd=/etc/motd
session    optional   pam_mail.so          dir=/var/spool/mail standard quiet
-session   optional   pam_systemd.so
session    required   pam_env.so
```

## Mounting

 `/etc/fstab`  `/dev/mapper/home-*YOURNAME*  /home/*YOURNAME*     ext4            rw,noatime,noauto,x-systemd.automount 0 2` 

That's it! Your home directory will be mounted automatically on the first access made by your Desktop Environment or shell.

However, you might want to describe the dependencies and ordering explicitly, as if you want to set up automatic unmounting on logout - you'll end up with a circular dependency loop that cannot by resolved automatically by systemd:

### Explicit dependencies and ordering

 `/etc/systemd/system/user@*1000*.service.d/homedir.conf` 
```
[Unit]
Requires=home-*YOURNAME*.mount
After=home-*YOURNAME*.mount
```

## Unmouting on logout

After you log out of all your sessions, systemd-logind automatically shuts down user@*1000*.service. Therefore, you can specify that your mountpoint requires it - and it'll get unmounted automatically by systemd.

 `/etc/systemd/system/home-*YOURNAME*.mount.d/logout.conf` 
```
[Unit]
Requires=user@*1000*.service
```

**Note:** This will create a circular dependency, resolvable as described in the section above.

**Note:** If your DE or some other application does not kill all its processes on logout, you might need to set KillUserProcesses=yes in **/etc/systemd/logind.conf**.

## Locking on unmount

After unmounting, the device will still be unlocked, and it'll be possible to mount it without re-entering password. Therefore, you can set up a service that starts when the device gets unlocked (BindsTo=dev-mapper-home\x2d*YOURNAME*.device) and dies after the device gets unmounted (Requires,Before=home-*YOURNAME*.mount), locking the device in the process (ExecStop=cryptsetup close).

 `/etc/systemd/cryptsetup-*YOURNAME*.service` 
```
[Unit]
DefaultDependencies=no
BindsTo=*dev-PARTITION*.device
After=*dev-PARTITION*.device
BindsTo=dev-mapper-home\x2d*YOURNAME*.device
Requires=home-*YOURNAME*.mount
Before=home-*YOURNAME*.mount
Conflicts=umount.target
Before=umount.target

[Service]
Type=oneshot
RemainAfterExit=yes
TimeoutSec=0
ExecStop=/usr/bin/cryptsetup close home-*YOURNAME*

[Install]
RequiredBy=dev-mapper-home\x2d*YOURNAME*.device
```

**Note:** *dev-PARTITION* is the result of **systemd-escape -p */dev/PARTITION***
 `systemctl enable cryptsetup-*YOURNAME*.service` 

## Tips

### SDDM

SDDM by default tries to display avatars of users by accessing ~/.face.icon file. As your home directory is an autofs, this will make it wait for 60 seconds - until autofs reports that the directory cannot be mounted.

You can disable avatars by editing /etc/sddm.conf:

 `/etc/sddm.conf` 
```
[Theme]
EnableAvatars=false
```