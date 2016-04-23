## Contents

*   [1 Hooks!](#Hooks.21)
    *   [1.1 update-desktop-database](#update-desktop-database)
    *   [1.2 update-mime-database](#update-mime-database)
    *   [1.3 install-info](#install-info)
    *   [1.4 OTHER](#OTHER)

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
Description = Updating desktop file MIME types cache database...
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
Description = Updating the Shared MIME-Info database cache...
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
Description = Remove old entries from the info directory file...
When = PostTransaction
Exec = /bin/sh -c 'while read -r f; do install-info --delete "$f" /usr/share/info/dir 2> /dev/null; done'
NeedsTargets

```

## OTHER

*   mkfontdir
*   fc-cache
*   gtk-update-icon-cache
*   xdg-icon-resource