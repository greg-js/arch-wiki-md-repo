[Baloo](https://community.kde.org/Baloo) is a file indexing and searching framework for [KDE](/index.php/KDE "KDE") Plasma.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage and configuration](#Usage_and_configuration)
*   [3 Indexing a removable device](#Indexing_a_removable_device)
*   [4 Removing baloo_file](#Removing_baloo_file)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Inotify folder watch limit error](#Inotify_folder_watch_limit_error)

## Installation

[Install](/index.php/Install "Install") the [baloo](https://www.archlinux.org/packages/?name=baloo) package.

## Usage and configuration

In order to search using Baloo on the Plasma desktop, start [KRunner](/index.php/KRunner "KRunner") (default keyboard shortcut `ALT+F2`) and type in your query. Within Dolphin press `CTRL+F`.

By default the Desktop Search KCM exposes only two options: A panel to blacklist folders and a way to disable it with one click.

Alternatively you can edit your `~/.config/baloofilerc` file ([info](https://community.kde.org/Baloo/Configuration)). Additionally the `balooctl` process can also be used. In order to disable Baloo run `balooctl stop` and `balooctl disable`.

Once you added additional folders to the blacklist or disabled Baloo entirely, a process named `baloo_file_cleaner` removes all unneeded index files automatically. They are stored under `~/.local/share/baloo/`.

## Indexing a removable device

By default every removable device is blacklisted. You just have to remove your device from the blacklist in the KCM panel.

## Removing baloo_file

Baloo_file uses a lot of resources and slow down computers. It also increases power consumption on laptops. While it cannot be removed due to dependencies issues, it is however possible to deactivate it until the next update. As root, type

```
killall baloo_file ; mv /usr/bin/baloo_file /usr/bin/baloo_file.bak ; echo '#!/bin/sh' > /usr/bin/baloo_file

```

## Troubleshooting

### Inotify folder watch limit error

If you get the following error:

```
KDE Baloo Filewatch service reached the inotify folder watch limit. File changes may be ignored.

```

Then you will need to increase the inotify folder watch limit:

```
# echo 524288 > /proc/sys/fs/inotify/max_user_watches

```

To make changes permanent, create a `40-max-user-watches.conf` file:

 `/etc/sysctl.d/40-max-user-watches.conf`  `fs.inotify.max_user_watches=524288`