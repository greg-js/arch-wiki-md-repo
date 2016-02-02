# KMSCON

From the project's [git repository](http://cgit.freedesktop.org/~dvdhrm/kmscon/tree/README):

	_Kmscon is a simple terminal emulator based on linux [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). It is an attempt to replace the in-kernel VT implementation with a userspace console._

## Contents

*   [1 Features](#Features)
*   [2 Install](#Install)
*   [3 CJK support](#CJK_support)
*   [4 Troubleshooting](#Troubleshooting)

## Features

Kmscon can function as a drop-in replacement for the in-kernel linux-console. Features include:

*   Full vt220 to vt510 implementation.
*   Full internationalization support:
    *   Kmscon supports printing full Unicode glyphs, including the CJK ones.
    *   Kmscon provides internationalized keyboard handling through libxkbcommon, thus allowing it to use the full range of keyboard layouts supported in X keyboard.
*   Hardware accelerated rendering.
*   Multi-seat capability.

**Note:** In order to be able to log into a kmscon console as root, you have to disable the `pam_securetty` module by removing or commenting out the corresponding line in `/etc/pam.d/login`.

## Install

Despite its name, kmscon is not a hard requirement for KMS. Kmscon supports the following video backends: fbdev (Linux fbdev video backend), drm2d (Linux DRM software-rendering backend), drm3d (Linux DRM hardware-rendering backend). Make sure one of them is available on your system.

Install the [kmscon](https://www.archlinux.org/packages/?name=kmscon) package from the [official repositories](/index.php/Official_repositories "Official repositories"). Alternatively, you can install the [kmscon-git](https://aur.archlinux.org/packages/kmscon-git/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR").

Normally, there is a special systemd configuration for tty1\. To be conservative, you can continue to run the traditional agetty on tty1 and only run kmscon on all the other virtual terminals. Or you can run kmscon on both tty1 and the other VTs.

To enable kmscon on tty1, run:

```
# systemctl disable getty@tty1.service
# systemctl enable kmsconvt@tty1.service

```

To enable kmscon on all virtual terminals, run:

```
# ln -s /usr/lib/systemd/system/kmsconvt\@.service /etc/systemd/system/autovt\@.service

```

This will make [systemd](https://www.archlinux.org/packages/?name=systemd) start kmscon instead of agetty on each VT. More precisely, this will make _systemd-logind_ use `kmsconvt@.service` instead of `getty@.service` for new VTs. Additionally, all other systemd units that use `getty@.service` will not be affected by this change.

If _kmscon_ cannot start for whatever reason, this unit will cause `getty@.service` to be started instead. Furthermore, if no VTs are available, this unit will not start anything.

**Warning:** If you've replaced agetty on all terminals, take care to ensure _kmscon_ presents you with a prompt before rebooting your machine, otherwise you may have to recover through a live CD.

## CJK support

Kmscon supports rendering CJK characters through the default font engine [pango](https://www.archlinux.org/packages/?name=pango). However, [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) has to be globally configured to map the monospace font alias to proper CJK fonts. For Chinese users, the following template is provided and proved to result in satisfactory Chinese characters rendering:

 `/etc/fonts/conf.d/99-kmscon.conf` 

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
<match>
        <test name="family"><string>monospace</string></test>
        <edit name="family" mode="prepend" binding="strong">
                <string>DejaVu Sans Mono</string>
                <string>WenQuanYi Micro Hei Mono</string>
        </edit>
</match>
</fontconfig>

```

You need to have [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei), both available from the official repositories, installed.

## Troubleshooting

*   You may want to add `hwaccel` to `/etc/kmscon/kmscon.conf` if you have problems with switching between [Xorg](/index.php/Xorg "Xorg") and kmscon.

The file and folder are not part of the package and therefore have to be created manually. Another possibility would be [editing the systemd service file](/index.php/Systemd#Editing_provided_units "Systemd").

*   As version 7, if you cannot control the audio, add your user to **audio** [group](/index.php/Group "Group"). Be aware of the [shortcomings](/index.php/Alsa#Installation "Alsa") of this choice.

Retrieved from "[https://wiki.archlinux.org/index.php?title=KMSCON&oldid=411995](https://wiki.archlinux.org/index.php?title=KMSCON&oldid=411995)"