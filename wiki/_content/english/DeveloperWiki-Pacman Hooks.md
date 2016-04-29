## Contents

*   [1 Hooks!](#Hooks.21)
    *   [1.1 update-desktop-database](#update-desktop-database)
    *   [1.2 update-mime-database](#update-mime-database)
    *   [1.3 install-info](#install-info)
    *   [1.4 glib-compile-schemas](#glib-compile-schemas)
    *   [1.5 gtk-update-icon-cache, xdg-icon-resource](#gtk-update-icon-cache.2C_xdg-icon-resource)
    *   [1.6 systemd-tmpfiles](#systemd-tmpfiles)
    *   [1.7 systemd-sysusers](#systemd-sysusers)
    *   [1.8 mktexlsr, texhash](#mktexlsr.2C_texhash)
    *   [1.9 gconf](#gconf)
    *   [1.10 gio-querymodules](#gio-querymodules)
    *   [1.11 fc-cache](#fc-cache)
    *   [1.12 update-ca-trust](#update-ca-trust)
*   [2 TBD](#TBD)

# Hooks!

## update-desktop-database

Used by 490 packages

Proposed Hook (desktop-file-utils)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/share/applications/*.desktop

[Action]
Description = Updating the desktop file MIME type cache...
When = PostTransaction
Exec = /usr/bin/update-desktop-database --quiet

```

## update-mime-database

Used by 142 packages

Proposed Hook (shared-mime-info)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/share/mime/packages/*.xml

[Action]
Description = Updating the MIME type database...
When = PostTransaction
Exec = /usr/bin/update-mime-database /usr/share/mime

```

## install-info

Used by 170 packages

Proposed Hook (texinfo)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = usr/share/info/*

[Action]
Description = Updating the info directory file...
When = PostTransaction
Exec = /bin/sh -c 'while read -r f; do install-info "$f" /usr/share/info/dir 2> /dev/null; done'
NeedsTargets

```

Proposed Hook (remove)

```
[Trigger]
Type = File
Operation = Remove
Target = usr/share/info/*

[Action]
Description = Removing old entries from the info directory file...
When = PostTransaction
Exec = /bin/sh -c 'while read -r f; do install-info --delete "$f" /usr/share/info/dir 2> /dev/null; done'
NeedsTargets

```

## glib-compile-schemas

Used by 222 packages

Proposed Hook (glib2)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/share/glib-2.0/schemas/*.gschema.xml
Target = usr/share/glib-2.0/schemas/*.gschema.override

[Action]
Description = Compiling GSettings XML schema files...
When = PostTransaction
Exec = /usr/bin/glib-compile-schemas /usr/share/glib-2.0/schemas

```

## gtk-update-icon-cache, xdg-icon-resource

Used by 754 packages

Note that `xdg-icon-resource forceupdate` has no effect without gtk-update-icon-cache installed, so removing it doesn't hurt.

Proposed Hook (gtk-update-icon-cache)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/share/icons/*/
Target = !usr/share/icons/*/?*

[Action]
Description = Updating icon theme caches...
When = PostTransaction
Exec = /usr/lib/pacman-hooks/gtk-update-icon-cache
NeedsTargets

```

```
#!/bin/bash

while read -r f; do
  if [[ -e ${f}index.theme ]]; then
    gtk-update-icon-cache -q "$f"
  else
    rm -f "${f}icon-theme.cache"
    rmdir --ignore-fail-on-non-empty "$f"
  fi
done

```

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

## gconf

Used by 55 packages

Proposed hook (gconf)

```
[Trigger]
Type = file
Operation = Install
Operation = Upgrade
Target = usr/share/gconf/schemas/*.schemas

[Action]
Description = Installing GConf schemas...
When = PostTransaction
Exec = /bin/bash -c 'while read -r f; do f=${f##*/}; f=${f%.schemas}; /usr/bin/gconfpkg --install $f; done'
NeedsTargets

```

```
[Trigger]
Type = file
Operation = Remove
Target = usr/share/gconf/schemas/*.schemas

[Action]
Description = Uninstalling GConf schemas...
When = PreTransaction
Exec = /bin/bash -c 'while read -r f; do f=${f##*/}; f=${f%.schemas}; /usr/bin/gconfpkg --uninstall $f; done'
NeedsTargets

```

## gio-querymodules

Used by 6 packages

Proposed hook (glib2)

```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Operation = Remove
Target = usr/lib/gio/modules/*.so

[Action]
Description = Updating GIO module cache...
When = PostTransaction
Exec = /usr/bin/gio-querymodules /usr/lib/gio/modules

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