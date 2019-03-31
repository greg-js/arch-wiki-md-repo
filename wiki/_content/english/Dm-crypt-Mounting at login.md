Related articles

*   [pam_mount](/index.php/Pam_mount "Pam mount")

It is possible to configure [PAM](/index.php/PAM "PAM") and [systemd](/index.php/Systemd "Systemd") to automatically mount a [dm-crypt](/index.php/Dm-crypt "Dm-crypt") encrypted home partition when its owner logs in, and to unmount it when he logs out.

This tutorial assumes you have already created your encrypted partition, as described in [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system").

**Note:**

*   You need to use the same password for your user account and for LUKS.
*   In all the examples, replace `*YOURNAME*` with your username, `*1000*` with your user ID and `*PARTITION*` with the name of your encrypted partition's device.

## Mounting at login

*pam_exec* can be used to unlock the device at login. Edit `/etc/pam.d/system-login` and add the line below emphasized in bold after `auth include system-auth`:

**Note:** GDM, LightDM, and maybe other display managers might require `pam_exec` for `session` as well, see [Talk:Dm-crypt/Mounting at login#pam_exec required for session & using script](/index.php/Talk:Dm-crypt/Mounting_at_login#pam_exec_required_for_session_&_using_script "Talk:Dm-crypt/Mounting at login").
 `/etc/pam.d/system-login` 
```
...

auth       include    system-auth
**auth       optional   pam_exec.so expose_authtok /etc/pam_cryptsetup.sh**

...
```

Then create the mentioned script.

 `/etc/pam_cryptsetup.sh` 
```
#!/bin/sh

CRYPT_USER="*YOURNAME*"
MAPPER="/dev/mapper/home-"$CRYPT_USER

if [ "$PAM_USER" == "$CRYPT_USER" ] && [ ! -e $MAPPER ]
then
  tr '\0' '
' | /usr/bin/cryptsetup open /dev/*PARTITION* home-*YOURNAME*
fi
```

Execute `chmod +x /etc/pam_cryptsetup.sh` to make it executable.

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