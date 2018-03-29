[incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en) is a daemon which monitors filesystem events and executes commands defined in system and user tables.

## Contents

*   [1 Installation](#Installation)
*   [2 Activation and Autostart](#Activation_and_Autostart)
*   [3 Configuration](#Configuration)
    *   [3.1 Using incrontab](#Using_incrontab)
*   [4 Incrontab format](#Incrontab_format)

## Installation

[Install](/index.php/Install "Install") the [incron](https://www.archlinux.org/packages/?name=incron) package.

## Activation and Autostart

After installation, the daemmon will not be enabled by default. It can be enabled using [systemctl](/index.php/Systemd#Using_units "Systemd").

## Configuration

Incrontabs should never be edited directly; instead, users should use the `incrontab` program to work with their incrontabs.

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

To edit another users incrontab, isue the following command as root:

```
$ incrontab -u *user*

```

## Incrontab format

Each row in an incrotab file is a table that the dameon runs when an event happens to a certain directory or file.

The basic format for an incrontab is:

```
*path* *mask* *command*

```

*   *path* is the directory or file that *incrond* will monitor for changes.
*   *mask* is the type of filesystem event that incrond will monitor for. This paramter can be seperated by commas.
*   *command* is the commmand to be run after the specified filesystem event(s) occur.