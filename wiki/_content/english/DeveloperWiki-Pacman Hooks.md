## Contents

*   [1 Hooks!](#Hooks.21)
    *   [1.1 update-desktop-database](#update-desktop-database)
    *   [1.2 update-mime-database](#update-mime-database)
    *   [1.3 install-info](#install-info)
    *   [1.4 glib-compile-schemas](#glib-compile-schemas)
    *   [1.5 gtk-update-icon-cache, xdg-icon-resource](#gtk-update-icon-cache.2C_xdg-icon-resource)
    *   [1.6 OTHER](#OTHER)

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

Proposed Hook (install/upgrade)

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
Description = Updating icon cache...
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

## OTHER

*   mkfontdir
*   mkfontscale
*   fc-cache
*   gio-querymodules
*   gdk-pixbuf-query-loaders
*   gtk-query-immodules-2.0
*   gtk-query-immodules-3.0