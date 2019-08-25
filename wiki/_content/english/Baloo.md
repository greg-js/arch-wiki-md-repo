[Baloo](https://community.kde.org/Baloo) is a file indexing and searching framework for [KDE](/index.php/KDE "KDE") Plasma.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage and configuration](#Usage_and_configuration)
*   [3 Indexing a removable or remote device](#Indexing_a_removable_or_remote_device)
*   [4 Disabling the indexer](#Disabling_the_indexer)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Inotify folder watch limit error](#Inotify_folder_watch_limit_error)

## Installation

[Install](/index.php/Install "Install") the [baloo](https://www.archlinux.org/packages/?name=baloo) package.

## Usage and configuration

In order to search using Baloo on the Plasma desktop, start [KRunner](/index.php/KRunner "KRunner") (default keyboard shortcut `ALT+F2`) and type in your query. Within Dolphin press `CTRL+F`. Alternatively, for command-line usage, there is `baloosearch [OPTIONS] query`, which supports complex queries such as `baloosearch //?query=tag:coolpicture AND width:100`, and `balooshow [OPTIONS] filename` to show the data baloo has stored for the file.

By default the Desktop Search KCM exposes only two options: A panel to blacklist folders and a way to disable it with one click. Alternatively you can edit your `~/.config/baloofilerc` file ([info](https://community.kde.org/Baloo/Configuration)).

Additionally the `balooctl` process can also be used to control Baloo, e.g. in order to stop/start Baloo use `balooctl stop` or `balooctl start` to resume.

Once you added additional folders to the blacklist or disabled Baloo entirely, a process named `baloo_file_cleaner` removes all unneeded index files automatically. These are stored under `~/.local/share/baloo/`.

## Indexing a removable or remote device

By default every removable and remote device is blacklisted. It is possible to remove devices from the blacklist in the KCM panel.

## Disabling the indexer

To disable the Baloo file indexer:

```
$ balooctl suspend
$ balooctl disable

```

The indexer will be disabled on next login.

Alternatively, disable *Enable File Search* in *System settings* under *Search > File search*.

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