## Contents

*   [1 Installing](#Installing)
*   [2 Configuration](#Configuration)
    *   [2.1 Do not end files with a new line](#Do_not_end_files_with_a_new_line)
    *   [2.2 Save backup versions of edited files](#Save_backup_versions_of_edited_files)
*   [3 Spell Checking](#Spell_Checking)
*   [4 Plugins](#Plugins)
    *   [4.1 Adding and making custom plugins](#Adding_and_making_custom_plugins)
*   [5 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") the [gedit](https://www.archlinux.org/packages/?name=gedit) package.

## Configuration

### Do not end files with a new line

If you want to ensure that gedit does not end files with a newline, execute the following:

```
$ gsettings set org.gnome.gedit.preferences.editor ensure-trailing-newline false

```

### Save backup versions of edited files

If desired, gedit can create a backup copy of an edited file - the contents of the backup file will be the same as the contents of the original file before the edit was made and then saved. The backup file's name will be the same as original file's name but suffixed with a ~ symbol. Hence, for the file called `file1` the backup copy would have the name `file1~`. Backup files are hidden by default.

To enable this behaviour, access gedit's Preferences panel (for GNOME Shell users, this can be found in gedit's global menu). In the preferences panel, click on the *Editor* tab and tick the option *Create a backup copy of files before saving.*

## Spell Checking

In order to use spell checking in gedit [install](/index.php/Install "Install") the according language, e.g., [aspell-en](https://www.archlinux.org/packages/?name=aspell-en).

## Plugins

Some plugins are available in the [gedit-plugins](https://www.archlinux.org/packages/?name=gedit-plugins) package.

### Adding and making custom plugins

A plugin that shows errors while you type for languages like C, C++, etc, available in the [AUR](/index.php/AUR "AUR"): [gedit-code-assistance-git](https://aur.archlinux.org/packages/gedit-code-assistance-git/).

## See also

*   [Apps/Gedit - GNOME Wiki!](https://wiki.gnome.org/Apps/Gedit)