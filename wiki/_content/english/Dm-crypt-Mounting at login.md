It's possible to configure PAM and [systemd](/index.php/Systemd "Systemd") to automatically mount a [dm-crypt](/index.php/Dm-crypt "Dm-crypt") encrypted home partition when its owner logs in, and to unmount it when he logs out.

## Contents

*   [1 General idea](#General_idea)
*   [2 Helper scripts](#Helper_scripts)
    *   [2.1 /usr/local/bin/savepass](#.2Fusr.2Flocal.2Fbin.2Fsavepass)
    *   [2.2 /usr/local/bin/securemount](#.2Fusr.2Flocal.2Fbin.2Fsecuremount)
    *   [2.3 /usr/local/bin/secureumount](#.2Fusr.2Flocal.2Fbin.2Fsecureumount)
*   [3 PAM configuration](#PAM_configuration)
*   [4 systemd service](#systemd_service)

## General idea

We're going to save the user's password during the PAM authentication phase, and put it into the kernel's keyring. Next, we're going to use it in a systemd service, started automatically before systemd's own user@.service, to unlock and mount the partition at the correct place.

When the user logs out, systemd will stop user@.service, and (because of a dependency) our service too - unmounting and locking the partition.

## Helper scripts

You need 3 helper scripts:

### /usr/local/bin/savepass

Script that saves the pam-provided password in the kernel's keyring (for root user).

 `/usr/local/bin/savepass` 
```
#!/bin/sh
exec keyctl padd user user:`id -u $PAM_USER` @u

```

### /usr/local/bin/securemount

Script that unlocks given device with a key obtained from the kernel's keyring, and mounts it at the given place.

 `/usr/local/bin/securemount` 
```
#!/bin/sh
set -e
KEYNAME=$1
DEVICE=$2
TARGET=$3
DEC_DEVICE_NAME=$(/usr/bin/systemd-escape -p `/usr/bin/realpath $DEVICE`)
DEC_DEVICE=/dev/mapper/$DEC_DEVICE_NAME

/usr/bin/keyctl pipe `/usr/bin/keyctl request user $KEYNAME` | /usr/bin/cryptsetup open $DEVICE $DEC_DEVICE_NAME -d -
/usr/bin/mount $DEC_DEVICE $TARGET

```

### /usr/local/bin/secureumount

Script that unmounts and closes the encrypted device.

 `/usr/local/bin/secureumount` 
```
#!/bin/sh
set -e
TARGET=$1
DEC_DEVICE=$(cat /proc/mounts | grep " $TARGET " | cut -d " " -f 1)

/usr/bin/umount $TARGET
/usr/bin/cryptsetup close $DEC_DEVICE

```

## PAM configuration

Add `auth optional pam_exec.so expose_authtok /usr/local/bin/savepass` before `auth optional pam_permit.so`:

 `/etc/pam.d/system-auth` 
```
#%PAM-1.0

auth      required  pam_unix.so     try_first_pass nullok
**auth      optional  pam_exec.so     expose_authtok /usr/local/bin/savepass**
auth      optional  pam_permit.so
auth      required  pam_env.so

account   required  pam_unix.so
account   optional  pam_permit.so
account   required  pam_time.so

password  required  pam_unix.so     try_first_pass nullok sha512 shadow
password  optional  pam_permit.so

session   required  pam_limits.so
session   required  pam_unix.so
session   optional  pam_permit.so

```

## systemd service

Create a new service file in the /etc/systemd/system directory. Replace **123** with the user's ID, **/home/xyz** with the path you want to mount the partition at, and both **c139ae70*\x2d*5861*\x2d*4084*\x2d*84b1*\x2d*7d83f7bb7129** and **c139ae70-5861-4084-84b1-7d83f7bb7129** with the UUID of the encrypted partition. Note, that in the first case you need to use **\x2d** in place of all **-** signs.

 `/etc/systemd/system/homedir@**123**.service` 
```
[Unit]
Description=Home Directory for %I
DefaultDependencies=no
Conflicts=umount.target
IgnoreOnIsolate=true
Before=user@%i.service
Requires=user@%i.service
BindsTo=dev-disk-by\x2duuid-**c139ae70*\x2d*5861*\x2d*4084*\x2d*84b1*\x2d*7d83f7bb7129**.device
After=dev-disk-by\x2duuid-**c139ae70*\x2d*5861*\x2d*4084*\x2d*84b1*\x2d*7d83f7bb7129**.device
Before=umount.target

[Service]
Type=oneshot
RemainAfterExit=yes
TimeoutSec=0
ExecStart=/usr/local/bin/securemount user:%i /dev/disk/by-uuid/**c139ae70-5861-4084-84b1-7d83f7bb7129** **/home/xyz**
ExecStop=/usr/local/bin/secureumount **/home/xyz**

[Install]
RequiredBy=user@%i.service
```

Finally, enable the service.

 `systemctl enable homedir@123.service`