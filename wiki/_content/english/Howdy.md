[Howdy](https://github.com/boltgolt/howdy) is a program that imitates Windows Hello on Linux. It uses a computer's IR sensors and camera to verify a user's face.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setup Howdy to start when needed](#Setup_Howdy_to_start_when_needed)
        *   [2.1.1 Example](#Example)
    *   [2.2 Add correct IR sensor](#Add_correct_IR_sensor)
    *   [2.3 Add face to Howdy](#Add_face_to_Howdy)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Howdy doesn't seem to work](#Howdy_doesn't_seem_to_work)

## Installation

[Install](/index.php/Install "Install") the [howdy](https://aur.archlinux.org/packages/howdy/) package.

## Configuration

### Setup Howdy to start when needed

In order for Howdy to authenticate a user, a small change must be added to any [PAM](/index.php/PAM "PAM") configuration file where Howdy might want to be used. The following line must be added to any configuration file:

```
auth sufficient pam_python.so /lib/security/howdy/pam.py

```

#### Example

 `/etc/pam.d/sudo` 
```
# PAM-1.0
auth    sufficient pam_python.so /lib/security/howdy/pam.py
auth    include    system-auth
account include    system-auth
session include    system-auth
```

### Add correct IR sensor

Determine the correct `/dev/videoX` file connected to the IR sensor. This can be done through various programs such as [cheese](https://www.archlinux.org/packages/?name=cheese) and [fswebcam](https://aur.archlinux.org/packages/fswebcam/). Once the correct filename is found, edit `/lib/security/howdy/config.ini` using either your preferred editor or with `sudo howdy config`.

**Note:** [gedit](https://www.archlinux.org/packages/?name=gedit) must be installed for `sudo howdy config` to work.

### Add face to Howdy

In order to add a face model to Howdy, run `sudo howdy add`.

## Troubleshooting

### Howdy doesn't seem to work

Verify that Howdy is properly working by running `howdy test` as root. If that seems to work, check any PAM configuration files and verify they are working. Some programs, such as SDDM [[1]](https://github.com/sddm/sddm/issues/284), do not work properly with PAM, which may result in unexpected results.