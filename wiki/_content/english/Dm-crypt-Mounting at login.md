Back to [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system")

It is possible to configure [PAM](/index.php/PAM "PAM") and [systemd](/index.php/Systemd "Systemd") to automatically mount a [dm-crypt](/index.php/Dm-crypt "Dm-crypt") encrypted home partition when its owner logs in, and to unmount it when he logs out.

This tutorial assumes you have already created your encrypted partition, as described in [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system").

**Note:**

*   You need to use the same password for your user account and for LUKS.
*   In all the examples, replace `*YOURNAME*` with your username, `*1000*` with your user ID and `*PARTITION*` with the name of your encrypted partition's device.

## Contents

*   [1 Mounting at login](#Mounting_at_login)
*   [2 Unmouting at logout](#Unmouting_at_logout)
    *   [2.1 Locking](#Locking)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 SDDM](#SDDM)

## Mounting at login

*pam_exec* can be used to unlock the device at login. Edit `/etc/pam.d/system-login` and add the line below emphasized in bold after `auth include system-auth`:

**Note:** GDM, LightDM, and maybe other display managers might require `pam_exec` for `session` as well, see [Discussion](https://wiki.archlinux.org/index.php/Talk:Dm-crypt/Mounting_at_login#pam_exec_required_for_session_.26_using_script).
 `/etc/pam.d/system-login` 
```
...

auth       include    system-auth
**auth       optional   pam_exec.so expose_authtok quiet /usr/bin/cryptsetup open /dev/*PARTITION* home-*YOURNAME***

...
```

Now edit `/etc/fstab` to mount the unlocked device using [systemd.automount](/index.php/Fstab#Automount_with_systemd "Fstab"):

 `/etc/fstab` 
```
...

/dev/mapper/home-*YOURNAME*  /home/*YOURNAME*     ext4            rw,noatime,noauto,x-systemd.automount 0 2

...
```

Your home directory will be mounted automatically on the first access made by your desktop environment or shell.

## Unmouting at logout

After you log out of all your sessions, *systemd-logind* automatically shuts down `user@*1000*.service`. Therefore, you can specify that your mountpoint requires it, and *systemd* will unmount it automatically:

 `/etc/systemd/system/home-*YOURNAME*.mount.d/logout.conf` 
```
[Unit]
Requires=user@*1000*.service
```

This will however create a circular dependency loop that cannot by resolved automatically by *systemd*, so you need to describe the dependencies and ordering explicitly:

 `/etc/systemd/system/user@*1000*.service.d/homedir.conf` 
```
[Unit]
Requires=home-*YOURNAME*.mount
After=home-*YOURNAME*.mount
```

**Note:** If your desktop environment or some other application does not kill all its processes on logout, you might need to set `KillUserProcesses=yes` in `/etc/systemd/logind.conf`.

### Locking

After unmounting, the device will still be unlocked, and it will be possible to mount it without re-entering password. You can set up and [enable](/index.php/Enable "Enable") a service that starts when the device gets unlocked (`BindsTo=dev-mapper-home\x2d*YOURNAME*.device`) and dies after the device gets unmounted (`Requires,Before=home-*YOURNAME*.mount`), locking the device in the process (`ExecStop=cryptsetup close`):

 `/etc/systemd/system/cryptsetup-*YOURNAME*.service` 
```
[Unit]
DefaultDependencies=no
BindsTo=dev-*PARTITION*.device
After=dev-*PARTITION*.device
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

**Note:** `dev-*PARTITION*` is the result of `systemd-escape -p /dev/*PARTITION*`

## Tips and tricks

### SDDM

[SDDM](/index.php/SDDM "SDDM") by default tries to display avatars of users by accessing `~/.face.icon` file. As your home directory is an *autofs*, this will make it wait for 60 seconds, until autofs reports that the directory cannot be mounted.

You can disable avatars by editing `/etc/sddm.conf`:

 `/etc/sddm.conf` 
```
[Theme]
EnableAvatars=false
```