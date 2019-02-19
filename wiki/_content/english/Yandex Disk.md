[Yandex Disk](https://disk.yandex.ru) is a free cloud storage service created by Yandex.ru that gives you access to your photos, videos and documents from any internet-enabled device. The Yandex.Disk client console lets you:

*   synchronize files and folders with your Disk
*   get public links to files and folders
*   customize folder syncing

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Commands](#Commands)
*   [3 Unofficial clients](#Unofficial_clients)
*   [4 See also](#See_also)

## Installation

[yandex-disk](https://aur.archlinux.org/packages/yandex-disk/) client for Linux can be installed in from the [AUR](/index.php/AUR "AUR"). Note that it's a CLI client - there is no official GUI for it at the moment.(see [#Unofficial clients](#Unofficial_clients))

To setup your proxy, user and local folder, enter

```
$ yandex-disk setup

```

Syncing will start after completing this step, now you're ready to use Yandex Disk.

## Commands

You can manage your folder using any filemanager or console.

Full list of commands is available in `man yandex-disk` or using

```
$ yandex-disk --help

```

Here're some examples of use:

*   `setup` - Launch the setup wizard.

*   `start` - Launch as daemon and start syncing folders. The current sync status is recorded in the file ".sync/status".

*   `stop` - stop daemon.

*   `status` - show daemon status: sync status, errors, recently synced files, disk space status. If FILE is shown, the status for this file will be returned.

*   `token` - receive OAuth token, encode and save it in a special file (by default - /.config/yandex-disk/passwd). If the options -p PASSWORD or --password PASSWORD are not shown, then the password must be entered from STDIN.

*   `sync` - sync the folder and log out (if the daemon is running, wait for syncing to finish).

*   `publish` - make the file/folder public and remove the link to STDOUT. The item will be copied to the sync folder. Use the option --overwrite to rewrite existing items.

*   `unpublish` - removes public access to the file/folder.

## Unofficial clients

*   [ydcmd](https://aur.archlinux.org/packages/ydcmd/) - console client in [python](/index.php/Python "Python").
*   [ekstertera](https://aur.archlinux.org/packages/ekstertera/) - gui client based on [qt5](/index.php/Qt "Qt").

## See also

[http://help.yandex.com/disk/cli-clients.xml](http://help.yandex.com/disk/cli-clients.xml)