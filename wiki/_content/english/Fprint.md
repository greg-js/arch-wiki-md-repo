Related articles

*   [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui")
*   [ThinkFinger](/index.php/ThinkFinger "ThinkFinger")

From [the fprint homepage](http://www.freedesktop.org/wiki/Software/fprint/):

	The fprint project aims to plug a gap in the Linux desktop: support for consumer fingerprint reader devices.

The idea is to use the built-in fingerprint reader in some notebooks for login using [PAM](/index.php/PAM "PAM"). This article will also explain how to use regular password for backup login method (solely fingerprint scanner is not recommended due to numerous reasons).

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Login configuration](#Login_configuration)
    *   [3.2 Create fingerprint signature](#Create_fingerprint_signature)
    *   [3.3 Restrict enrolling](#Restrict_enrolling)

## Prerequisites

Make sure you have one of the supported finger scanners. You can check if your device is supported by checking [this](http://www.freedesktop.org/wiki/Software/fprint/libfprint/Supported_devices/) list of supported devices. To check which one you have, type

```
# lsusb

```

**Note:** The above list of supported devices is not updated regularly and is not complete. Its worth testing your device using the instructions on this page even if it does not appear on that list, prior to resorting to [AUR](/index.php/AUR "AUR") packages.

## Installation

[Install](/index.php/Install "Install") the [fprintd](https://www.archlinux.org/packages/?name=fprintd) package. [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) might also be needed.

## Configuration

### Login configuration

**Note:** If you use [GDM](/index.php/GDM "GDM"), the fingerprint-option is already available in the login menu (if not add yourself to the `input` group). You can skip this section!

Add `pam_fprintd.so` as *sufficient* to the top of the auth section of `/etc/pam.d/system-local-login`:

 `/etc/pam.d/system-local-login` 
```
**auth      sufficient pam_fprintd.so**
auth      include   system-login
...

```

This tries to use fingerprint login first, and if it fails or if it finds no fingerprint signatures in the given user's home directory, it proceeds to password login.

You can also modify other files in `/etc/pam.d/` in the same way, for example `/etc/pam.d/polkit-1` for GNOME polkit authentication.

### Create fingerprint signature

To add a signature for a finger, run

```
$ fprintd-enroll

```

or create a new signature for all fingers

```
$ fprintd-delete "$USER"
$ for finger in {left,right}-{thumb,{index,middle,ring,little}-finger}; do fprintd-enroll -f "$finger" "$USER"; done

```

You will be asked to scan the given finger. Swipe your right index finger **five times**. After that, the signature is created in `/var/lib/fprint/`.

For more information, see [fprintd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fprintd.1).

### Restrict enrolling

By default you are allowed to enroll new fingerprints without prompting for the password or the fingerprint. You can change this behavior using Polkit rules.

In the following example only superuser can enroll fingerprints:

 `/etc/polkit-1/rules.d/50-net.reactivated.fprint.device.enroll.rules` 
```
polkit.addRule(function (action, subject) {
  if (action.id == "net.reactivated.fprint.device.enroll") {
    return subject.user == "root" ? polkit.Result.YES : polkit.result.NO
  }
})
```