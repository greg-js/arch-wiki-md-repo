## Contents

*   [1 Hooks!](#Hooks.21)
    *   [1.1 systemd-tmpfiles](#systemd-tmpfiles)
    *   [1.2 systemd-sysusers](#systemd-sysusers)
    *   [1.3 udevadm hwdb, systemd-hwdb](#udevadm_hwdb.2C_systemd-hwdb)
    *   [1.4 mktexlsr, texhash](#mktexlsr.2C_texhash)
    *   [1.5 fc-cache](#fc-cache)
    *   [1.6 update-ca-trust](#update-ca-trust)
*   [2 TBD](#TBD)
*   [3 Implemented](#Implemented)

# Hooks!

## systemd-tmpfiles

Used by 52 packages

Proposed hook (systemd)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = usr/lib/tmpfiles.d/*.conf

[Action]
Description = Creating temporary files...
When = PostTransaction
Exec = /bin/sh -c 'while read -r f; do /usr/bin/systemd-tmpfiles --create "/$f"; done'
NeedsTargets

```

## systemd-sysusers

Used by 29 packages

Proposed hook (systemd)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = usr/lib/sysusers.d/*.conf

[Action]
Description = Updating system user accounts...
When = PostTransaction
Exec = /bin/sh -c 'while read -r f; do /usr/bin/systemd-sysusers "/$f" ; done'
NeedsTargets

```

## udevadm hwdb, systemd-hwdb

Used by 5 packages

This SHOULD be run with --usr, resulting in /usr/lib/udev/hwdb.bin instead of /etc/udev/hwdb.bin.

Although the latter database overrides the former, this would not be a problem since systemd-hwdb-update.service will update /etc/udev/hwdb.bin at boot if /etc/udev/hwdb.bin exists OR /usr/lib/udev/hwdb.bin does not exist OR /etc/udev/hwdb.d is not empty.

However, this service is also gated on ConditionNeedsUpdate=/etc, which passes if /usr has a newer mtime than /etc/.updated. Unfortunately, ConditionNeedsUpdate (used in quite a few services!) is broken for us since pacman will not update the mtime of directories that already exist, such as /usr.

Proposed hook (systemd)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/lib/udev/hwdb.d/*.hwdb

[Action]
Description = Updating udev hardware database...
When = PostTransaction
Exec = /usr/bin/systemd-hwdb update

```

## mktexlsr, texhash

Used in 27 packages

Proposed hook (texlive-texmf)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/share/texmf/*
Target = usr/share/texmf-dist/*

[Action]
Description = Updating TeX Live ls-R databases...
When = PostTransaction
Exec = /usr/bin/mktexlsr

```

## fc-cache

Used by 53 packages

Proposed hook (fontconfig)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/share/fonts/*

[Action]
Description = Updating fontconfig cache...
When = PostTransaction
Exec = /usr/bin/fc-cache -s

```

## update-ca-trust

Used by 5 packages

Proposed hook (ca-certificates-utils)

```
[Trigger]
Operation = Install
Operation = Upgrade
Operation = Remove
Type = File
Target = usr/share/ca-certificates/trust-source/*

[Action]
Description = Rebuilding certificate stores...
When = PostTransaction
Exec = /usr/bin/update-ca-trust

```

# TBD

*   mkfontscale, mkfontdir (58 packages)
*   gdk-pixbuf-query-loaders (6 packages)
*   gtk-query-immodules-2.0 (7 packages)
*   gtk-query-immodules-3.0 (7 packages)

# Implemented

*   update-desktop-database
*   update-mime-database
*   update-appstream-index
*   install-info
*   glib-compile-schemas
*   gtk-update-icon-cache, xdg-icon-resource
*   gconfpkg
*   gio-querymodules
*   gdk-pixbuf-query-loaders
*   gtk-query-immodules-2.0
*   gtk-query-immodules-3.0