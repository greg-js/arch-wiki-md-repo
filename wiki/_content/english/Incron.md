[incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en) is a daemon which monitors [filesystem events](/index.php/Autostarting#On_filesystem_events "Autostarting") and executes commands defined in system and user tables.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Activation and autostart](#Activation_and_autostart)
*   [3 Configuration](#Configuration)
    *   [3.1 Using incrontab](#Using_incrontab)
    *   [3.2 Incrontab format](#Incrontab_format)
        *   [3.2.1 Mask types](#Mask_types)

## Installation

[Install](/index.php/Install "Install") the [incron](https://www.archlinux.org/packages/?name=incron) package.

## Activation and autostart

After installation, the daemon will not be enabled by default. It can be enabled using [systemctl](/index.php/Systemd#Using_units "Systemd").

## Configuration

Incrontabs should never be edited directly; instead, users should use the *incrontab* program to work with their incrontabs.

### Using incrontab

To view their incrontabs, users should issue the command:

```
$ incrontab -l

```

To edit their incrontabs, they should use:

```
$ incrontab -e

```

To remove their incrontabs, they may use:

```
$ incrontab -r

```

To reload *incrond*, use:

```
$ incrontab -d

```

To edit another user's incrontab, isue the following command as root:

```
$ incrontab -u *user*

```

### Incrontab format

Each row in an incrontab file is a table that the dameon runs when an event happens to a certain directory or file.

The basic format for an incrontab is:

```
*path* *mask* *command*

```

*   *path* is the directory or file that *incrond* will monitor for changes.
*   *mask* is the type of filesystem event that incrond will monitor for. This paramter can be seperated by commas.
*   *command* is the commmand to be run after the specified filesystem event(s) occur.

#### Mask types

*incrontab* uses mask types to specify which file system event to monitor for. For more options see [inotify(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotify.7)

To trigger an command if a file is accessed or read:

```
**IN_ACCESS**

```

To trigger an command if metadata of a file change (e.g. *timestamps*, *permissons*):

```
**IN_ATTRIB**

```

To trigger a command if a file opened for writing is closed:

```
**IN_CLOSE_WRITE**

```

To trigger a command if a file or directory not opened for writing is closed:

```
**IN_CLOSE_NOWRITE**

```

To trigger a command if a file or directory is created in a watched directory:

```
**IN_CREATE**

```

To trigger a command if a file or directory is deleted from a watched directory:

```
**IN_DELETE**

```

To trigger a command if a watched file or directory is deleted (or moved to a different filesystem):

```
**IN_DELETE_SELF**

```

To trigger a command if a file was modified:

```
**IN_MODIFY**

```

To trigger a command if a watched file or directory is moved within the filesystem:

```
**IN_MOVE_SELF**

```

To trigger a command if a file or directory is moved out of the watched directory:

```
**IN_MOVED_FROM**

```

To trigger a command if a file or directory is moved to the watched directory:

```
**IN_MOVED_TO**

```

To trigger a command if a watched file or directory is opened:

```
**IN_OPEN**

```