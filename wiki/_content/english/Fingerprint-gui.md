[Fingerprint-gui](http://www.ullrich-online.cc/fingerprint/) is a program that provides an interface and drivers for fingerprint readers. The package includes drivers from the open-source project [fprint](/index.php/Fprint "Fprint") as well as proprietary drivers not included in fprint.

## Contents

*   [1 Installation](#Installation)
*   [2 Registering Fingerprints](#Registering_Fingerprints)
*   [3 Authentication](#Authentication)
*   [4 Verification](#Verification)
*   [5 Exporting](#Exporting)
*   [6 Password](#Password)

## Installation

Install [fingerprint-gui](https://aur.archlinux.org/packages/fingerprint-gui/) from [AUR](/index.php/AUR "AUR"). The package includes an installation guide in html format at `/usr/share/doc/fingerprint-gui/Manual_en.html`.

If you are using [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE") follow the instructions pacman gives and remove the following files:

 `/etc/xdg/autostart/` 

```
polkit-gnome-authentication-agent-1.desktop
polkit-kde-authentication-agent-1.desktop

```

## Registering Fingerprints

After installation, test if your hardware is recognized and correctly working by launching the configuration utility:

```
$ fingerprint-gui -d

```

The '-d' is for debugging, and simply creates a verbose log of events. If you are comfortable without the debug info, you may safely omit the flag.

If your device is not recognized, you might need to reboot in order for udev to set the correct permissions for the device. You may need to add your user to the plugdev and scanner groups.

To start registering your fingerprints with the configuration utility, select the tab **Finger**, select a finger and choose next.

## Authentication

Once your fingerprints have been registered, you may notice that in the setup procedure that the "test" section does not yet work. This is because the necessary authentication has not been approved in the appropriate `pam.d` files.

As an example of how to set up fingerprint authetication for a given service, we will first start with [sudo](/index.php/Sudo "Sudo"). Open `/etc/pam.d/sudo` in your [text editor](/index.php/Common_Applications#Text_Editor "Common Applications") and insert the following **bold text**:

 `/etc/pam.d/sudo` 

```
#%PAM-1.0
**auth		sufficient	pam_fingerprint-gui.so**
auth		required	pam_unix.so
auth		required	pam_nologin.so
```

Keep in mind that your 'sudo' file may contain more entries.

Some users may not have (or want to have) [sudo](/index.php/Sudo "Sudo") installed on their systems. In this case, it is still possible to use your fingerprint to autheticate [su](/index.php/Su "Su"). This can be done just like the sudo example, of course instead adding an entry to `/etc/pam.d/su`. Again, add the following **bold text**.

 `/etc/pam.d/su` 

```
 #%PAM-1.0
 auth		sufficient	pam_rootok.so
 **auth		sufficient	pam_fingerprint-gui.so**
 auth		required	pam_unix.so
 account		required	pam_unix.so
 session		required	pam_unix.so
```

One may also configure such things as GDM, KDM, LightDM and the Gnome-Screensaver. Again, if more information or instruction is needed, please refer to the included manual. The [Package Maintainer's Manual](http://www.ullrich-online.cc/fingerprint/doc/Step-by-step-manual.html) might provide further information that cannot be obtained by the included manual.

## Verification

Now that the necessary authentication has been added to pam, you may wish the confirm the functionality of your setup. The easiest way to do this is to, again, launch the fingerprint-gui. Rather than go through the steps (as your fingerprints should already be established), click directly on the _Settings_ tab. From here you may select the function you wish to test (ie. sudo, su, gdm, etc).

There is also an included utility to simply confirm that your registered fingerprints are recognized. This can be done by simply running:

```
$ fingerprint-identifier

```

and following the onscreen instructions.

## Exporting

If you wish to save your user's fingerprint data to a file, simple use the _Export_ button in the _Settings_ tab. A file Fingerprints.tar.gz" will be created in the desired directory. At this time, I have not yet figured out what exactly to do with this saved file though, as I have not come across an "Import" function.

## Password

In some cases, using your fingerprint to log into the system may inhibit certain other functions of the desktop environment. For example, [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") is dependent on your password, as it is used to encrypt the data in your keyring. To overcome this, fingerprint-gui contains a feature that allows you to store your encrypted password on removable media (USB). You may then use the key to decrypt your keychain by autheticating you rfingerprint while the removable media is plugged in.

The manual indicates that to use this function, mount your USB drive and ensure that you have write access to it. Under the "Password" tab of fingerprint-gui, indicate the appropriate path to your device where it says "Save to directory" (ie. if using gvfs it should be under `/run/media/_your_uid_/_device_`). Enter your password and reenter it and select "save". This will create a hidden directory on your removable media `/.fingerprints` and create a file `_username_@_hostname_.xml`. On the local machine, this will also create the file `/var/lib/fingerprint-gui/_username_/config.xml`.

**Note:** Security warning: Everyone who has access to both, your computer and the external media, can decrypt the password-file! Never leave the computer and the media unattended at the same place! Connect this media only while logon and don't use it if other persons have root-access to your computer.