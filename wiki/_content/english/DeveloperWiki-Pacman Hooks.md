# Hooks!

## udevadm hwdb, systemd-hwdb

Used by 5 packages

This SHOULD be run with --usr, resulting in /usr/lib/udev/hwdb.bin instead of /etc/udev/hwdb.bin.

Although the latter database overrides the former, this would not be a problem since systemd-hwdb-update.service will update /etc/udev/hwdb.bin at boot if /etc/udev/hwdb.bin exists OR /usr/lib/udev/hwdb.bin does not exist OR /etc/udev/hwdb.d is not empty.

However, this service is also gated on ConditionNeedsUpdate=/etc, which passes if /usr has a newer mtime than /etc/.updated. Unfortunately, ConditionNeedsUpdate (used in quite a few services!) is broken for us since pacman will not update the mtime of directories that already exist, such as /usr. This can be worked around with another hook.

If this workaround hook is unacceptable, it and the --usr argument can be dropped.

Proposed hook (systemd)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr

[Action]
Description = Updating /usr...
When = PostTransaction
Exec = /usr/bin/touch -c /usr

```

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
Exec = /usr/bin/systemd-hwdb --usr update

```

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
*   mktexlsr
*   update-ca-trust
*   systemd-tmpfiles
*   systemd-sysusers
*   fontconfig (fc-cache)
*   lib32-fontconfig (fc-cache-32)
*   xorg-mkfontdir (mkfontscale/mkfontdir)