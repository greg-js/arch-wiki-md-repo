[pam_usb](https://github.com/aluzzardi/pam_usb) provides hardware authentication for Linux using ordinary USB Flash Drives.

It works with any application supporting [PAM](/index.php/PAM "PAM"), such as [su](/index.php/Su "Su") and login managers ([GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM")).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setting up Devices and Users](#Setting_up_Devices_and_Users)
    *   [2.2 Check the configuration](#Check_the_configuration)
    *   [2.3 Setting up the PAM module](#Setting_up_the_PAM_module)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 su fails to use pam_usb](#su_fails_to_use_pam_usb)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pam_usb](https://aur.archlinux.org/packages/pam_usb/) package.

## Configuration

Setting up pam_usb requires the following, once pam_usb is installed:

1.  Set up devices and users
2.  Configuring PAM for system authentication

### Setting up Devices and Users

Once you've connected your USB device to the computer, use pamusb-conf to add it to the configuration file:

 `# pamusb-conf --add-device MyDevice` 
```
Please select the device you wish to add.
* Using "SanDisk Corp. Cruzer Titanium (SNDKXXXXXXXXXXXXXXXX)" (only option)
Which volume would you like to use for storing data ?
* Using "/dev/sda1 (UUID: <6F6B-42FC>)" (only option)
Name            : MyDevice
Vendor          : SanDisk Corp.
Model           : Cruzer Titanium
Serial          : SNDKXXXXXXXXXXXXXXXX
Volume UUID     : 6F6B-42FC (/dev/sda1)
Save to /etc/pamusb.conf ?
[Y/n] y
Done.
```

Note that `MyDevice` can be any arbitrary name you'd like. Also, you can add as many devices as you want.

Next, configure users you want to be able to authenticate with pam_usb:

 `# pamusb-conf --add-user root` 
```

Which device would you like to use for authentication ?
* Using "MyDevice" (only option)
User            : root
Device          : MyDevice
Save to /etc/pamusb.conf ?
[Y/n] y
Done.
```

### Check the configuration

You can run `pamusb-check` anytime to check if everything is correctly worked. This tool will simulate an authentication request (requires your device to be connected, otherwise it will fail).

 `# pamusb-check root` 
```
* Authentication request for user "root" (pamusb-check)
* Device "MyDevice" is connected (good).
* Performing one time pad verification...
* Verification match, updating one time pads...
* Access granted.
```

### Setting up the PAM module

To add pam_usb into the system authentication process, we need to edit `/etc/pam.d/system-auth`

The default PAM configuration file should include the following line:

 `auth    required        pam_unix.so nullok_secure` 

Change it to:

```
auth    sufficient      pam_usb.so
auth    required        pam_unix.so nullok_secure
```

The `sufficient` keyword means that if pam_usb allows the authentication, then no password will be asked. If the authentication fails, then the default password-based authentication will be used as fallback.

If you change it to `required`, it means that both the USB flash drive and the password will be required to grant access to the system.

Now you should be able to authenticate with the relevant USB device plugged-in.

 `$ su` 
```
* pam_usb v.SVN
* Authentication request for user "root" (su)
* Device "MyDevice" is connected (good).
* Performing one time pad verification...
* Verification match, updating one time pads...
* Access granted.
```

## Troubleshooting

### su fails to use pam_usb

If you set:

 `/etc/pam.d/system-auth`  `auth          sufficient   pam_usb.so` 

and `su` prompts for a password, and does not use pam_usb, add the same line at the beginning of `/etc/pam.d/su`. This may be required for other pam-aware applications as well.

## See also

*   [Github repository](https://github.com/aluzzardi/pam_usb)
*   [Github wiki](https://github.com/aluzzardi/pam_usb/wiki)