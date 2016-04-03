From [the fprint homepage](http://www.freedesktop.org/wiki/Software/fprint/):

	*The fprint project aims to plug a gap in the Linux desktop: support for consumer fingerprint reader devices.*

The idea is to use the built-in fingerprint reader in some notebooks for login using [PAM](/index.php/PAM "PAM"). This article will also explain how to use regular password for backup login method (solely fingerprint scanner is not recommended due to numerous reasons).

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Login configuration](#Login_configuration)
    *   [3.2 Create fingeprint signature](#Create_fingeprint_signature)

## Prerequisites

Make sure you have one of the supported finger scanners. You can check if your device is supported by checking [this](http://www.freedesktop.org/wiki/Software/fprint/libfprint/Supported_devices/) list of supported devices. To check which one you have, type

```
# lsusb

```

## Installation

[Install](/index.php/Install "Install") the [fprintd](https://www.archlinux.org/packages/?name=fprintd) package. [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) might also be needed.

## Configuration

### Login configuration

**Note:** If you use [GDM](/index.php/GDM "GDM"), the fingerprint-option is already available in the login menu. You can skip this section!

Add `pam_fprintd.so` as *sufficient* to the top of the auth section of `/etc/pam.d/system-local-login`:

 `/etc/pam.d/system-local-login` 
```
**auth      sufficient pam_fprintd.so**
auth      include   system-login
...

```

This tries to use fingerprint login first, and if it fails or if it finds no fingerprint signatures in the give user's home directory, it proceeds to password login.

You can also modify other files in `/etc/pam.d/` in the same way, for example `/etc/pam.d/polkit-1` for GNOME polkit authentication.

### Create fingeprint signature

To add a signature for a finger, run

```
$ fprintd-enroll

```

You will be asked to scan the given finger. After that, the signature is created in `/var/lib/fprint/`.

For more information, see `man fprintd`.