[Nemo](https://github.com/linuxmint/nemo) is a fork of [GNOME Files](/index.php/GNOME_Files "GNOME Files"). It is also the default file manager of the [Cinnamon](/index.php/Cinnamon "Cinnamon") desktop. Nemo is based on the Files 3.4 code. It was created as a response to the changes in Files 3.6 which saw features such as type ahead find and split pane view removed.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Extensions](#Extensions)
*   [2 Configuration](#Configuration)
    *   [2.1 Show / hide desktop icons](#Show_.2F_hide_desktop_icons)
    *   [2.2 Change application for "Open in terminal" context menu entry](#Change_application_for_.22Open_in_terminal.22_context_menu_entry)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Nemo Actions](#Nemo_Actions)
        *   [3.1.1 Clam Scan](#Clam_Scan)
        *   [3.1.2 Moving files](#Moving_files)
        *   [3.1.3 Meld compare](#Meld_compare)
        *   [3.1.4 Filenames containing spaces](#Filenames_containing_spaces)

## Installation

[Install](https://wiki.archlinux.org/index.php/Pacman) [nemo](https://www.archlinux.org/packages/?name=nemo) from the [official repositories](/index.php/Official_repositories "Official repositories").

### Extensions

Some programs can add extra functionality to Nemo. Here are a few packages that do just that:

*   **Nemo File Roller** — File archiver extension for Nemo.

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-fileroller](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-fileroller) || [nemo-fileroller](https://www.archlinux.org/packages/?name=nemo-fileroller)

*   **Nemo Compare** — An utility which compares two files using [meld](https://www.archlinux.org/packages/?name=meld).

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-compare](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-compare) || [nemo-compare](https://aur.archlinux.org/packages/nemo-compare/)

*   **Nemo Preview** — GtkClutter and Javascript-based quick previewer for Nemo.

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-preview](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-preview) || [nemo-preview](https://www.archlinux.org/packages/?name=nemo-preview)

*   **Nemo Seahorse** — PGP encryption and signing extension for Nemo.

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-seahorse](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-seahorse) || [nemo-seahorse](https://www.archlinux.org/packages/?name=nemo-seahorse)

*   **Nemo Share** — Samba extension for Nemo.

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-share](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-share) || [nemo-share](https://www.archlinux.org/packages/?name=nemo-share)

*   **RabbitVCS Nemo** — Integrate RabbitVCS into Nemo.

	[http://www.rabbitvcs.org/](http://www.rabbitvcs.org/) || [rabbitvcs-nemo](https://aur.archlinux.org/packages/rabbitvcs-nemo/)

See [nemo-extensions github repo](https://github.com/linuxmint/nemo-extensions) for all extensions.

## Configuration

Nemo is simple to configure graphically but not all options are in the preferences screen in Nemo. More options are available in the *dconf-editor* under `org.nemo`. To set Nemo as the default file browser, see [Xdg-open#Set the default file-browser](/index.php/Xdg-open#Set_the_default_file-browser "Xdg-open").

### Show / hide desktop icons

To enable/disable desktop icons rendering feature in nemo, change the following setting true or false (false to hide, true to show):

```
$ gsettings set org.nemo.desktop show-desktop-icons false

```

This fixes the console warning `WARNING **: Can not determine workarea, guessing at layout` for tiling window managers (such as i3).

### Change application for "Open in terminal" context menu entry

[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) is set as the default, if it is not installed this feature will not work.

Alternatively, change the default setting with *gsettings* to the preferred terminal application.

```
$ gsettings set org.cinnamon.desktop.default-applications.terminal exec <terminal-name>

```

## Tips and tricks

### Nemo Actions

Nemo allows the user to add new entries to the context menu. The file `[/usr/share/nemo/actions/sample.nemo_action](https://github.com/linuxmint/nemo/blob/master/files/usr/share/nemo/actions/sample.nemo_action)` contains an example of a Nemo action. Directories to place custom action files:

*   `/usr/share/nemo/actions/` for system-wide actions
*   `$HOME/.local/share/nemo/actions/` for user actions

Pay attention to the name convention. Your file has to preserve the file ending `.nemo_action`.

#### Clam Scan

 `$HOME/.local/share/nemo/actions/clamscan.nemo_action` 
```
[Nemo Action]
Name=Clam Scan
Comment=Clam Scan

Exec=gnome-terminal -x sh -c "clamscan -r %F | less"

Icon-Name=bug-buddy

Selection=Any

Extensions=dir;exe;dll;zip;gz;7z;rar;
```

#### Moving files

 `$HOME/.local/share/nemo/actions/archive.nemo_action` 
```
[Nemo Action]
Active=true
Name=Archive %N
Comment=Archiving %N will add .archive to the object.
Exec=<archive.py %F>
Selection=S
Extensions=any;
```
 `$HOME/.local/share/nemo/actions/archive.py` 
```
#! /usr/bin/python2 -OOt
import sys
import os
import shutil

filename = sys.argv[0]
print "Running " + filename
print "With the following arguments:"
for arg in sys.argv:
    if filename == arg:
        continue
    else:
        print arg
        #os.rename('%s','%s.archive') % (arg,arg)
        shutil.move(arg, arg+".archive")
```

#### Meld compare

 `$HOME/.local/share/nemo/actions/compare-save-for-later.nemo_action` 
```
[Nemo Action]
Active=true
Name=Compare later
Comment=Save file for comparison later.
Exec=<compare.sh save %F>
Icon-Name=meld
Selection=S
Extensions=any
```
 `$HOME/.local/share/nemo/actions/compare-with-saved.nemo_action` 
```
[Nemo Action]
Active=true
Name=Compare with saved element
Comment=Compare %F saved file or directory.
Exec=<compare.sh compare %F>
Icon-Name=meld
Selection=S
Extensions=any
```
 `$HOME/.local/share/nemo/actions/compare.sh` 
```
#!/bin/bash
savedfile=/var/tmp/compare-save-for-later.$USER
comparator=meld
if [ "$1" == "save" ]; then
	echo "$2" > "$savedfile"
else
	"$comparator" $(cat "$savedfile") "$2"
fi
```

#### Filenames containing spaces

By default, Nemo does not escape filenames. This means that actions for multiple files with some names containing spaces are broken. To fix this, use `Quote=double`.