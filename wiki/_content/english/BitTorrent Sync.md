[BitTorrent Sync](https://www.getsync.com/) (BTSync) is a file sharing system that relies on the [BitTorrent](http://en.wikipedia.org/wiki/Bittorrent) protocol. Instead of having a central server which archives every file, this syncing method uses peer-to-peer connections between the devices themselves therefore there is no limit on data storage and/or transfer speed. The user's data is exclusively stored on the devices with which the user chose to be in sync with, hence it is required to have at least two user devices, or "nodes" to be online. If many devices are connected simultaneously, files are shared between them in a mesh networking topology.

## Contents

*   [1 Security](#Security)
*   [2 Synchronization](#Synchronization)
*   [3 Installation](#Installation)
*   [4 Usage](#Usage)
*   [5 Configuration](#Configuration)
    *   [5.1 Automatic config file creation](#Automatic_config_file_creation)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Missing storage path](#Missing_storage_path)
    *   [6.2 Ignore some files/folders synchronization](#Ignore_some_files.2Ffolders_synchronization)
    *   [6.3 ARM alignment error](#ARM_alignment_error)
*   [7 See also](#See_also)

## Security

All traffic between devices is encrypted with AES-128 in counter mode, using a unique session key. This key is derived from a 'secret' which itself is a random 21 Byte key Base32-encoded. By handing over the 'secret', files and folders can be shared with other users.

## Synchronization

When a device adds a folder for synchronization, a secret is generated. From now on, every device that wants to synchronize that folder must know the secret key.

The synchronization has no speed or size limits, as long as both devices have enough disk space.

## Installation

[btsync](https://aur.archlinux.org/packages/btsync/) can be installed from the [AUR](/index.php/AUR "AUR"). The package includes [systemd](/index.php/Systemd "Systemd") service definitions for managing the btsync daemon. This package creates a default /etc/btsync.conf for system/root operation. Make the desired changes (e.g. login id and password) to those files prior to enabling the service-file with systemctl.

Alternatively, the bare 'tar.gz' packaged executable can be downloaded from the [official website](http://www.bittorrent.com/sync/download/). The rest of this guide assumes that you are using the btsync AUR package.

## Usage

The Linux client of BTSync does not use a typical GUI, instead it sets up a WebUI server accessible at `localhost:8888`. Shared folders can also be configured statically in a configuration file, but doing so disables the WebGUI.

Once installed, you'll first need to create a configuration file at `~/.config/btsync/btsync.conf`, see [#Configuration](#Configuration). You will also need to create the `storage_path` directory. When that is done, start and (if you want it to start on boot) enable the service:

```
$ systemctl --user start btsync
$ systemctl --user enable btsync

```

The service will run as the user invoking the command. Note that the above command is *not* run as root: doing so may lead to a cryptic error stating that D-Bus has refused the connection.

**Note:** It is important to make sure that when `btsync` is run as the user, the `btsync.conf` file and directory where the `btsync.pid` file will be located have the correct user permissions, i.e. are owned by the user invoking the command. Failure to do so will prevent the service from running. If the user permissions are correct but `btsync` still fails to run after being enabled, restart your system.

**Note:** If running `btsync` on a headless server, enable lingering to start `btsync` and keep it running outside user sessions: [Systemd/User#Automatic start-up of systemd user instances](/index.php/Systemd/User#Automatic_start-up_of_systemd_user_instances "Systemd/User").

You can also run it as the `btsync` system user, just leave the `--user` part out:

```
# systemctl enable btsync
# systemctl start btsync

```

Configuration for this user is located at `/etc/btsync.conf`, and metadata is saved in `/var/lib/btsync/` by default. You should review the configuration settings especially user and password, see below.

## Configuration

A sample configuration file can be created using:

```
# btsync --dump-sample-config > ~/.config/btsync/btsync.conf

```

You'll probably want to change some of the settings, including:

*   device_name
*   storage_path
*   webui/login
*   webui/password

**Note:** The `btsync` executable does not create the `storage_path` directory if it doesn't exist, you will have to do this manually or use [#Automatic config file creation](#Automatic_config_file_creation).

**Note:** The storage_path setting defines where metadata will be saved, **not** the synced files themselves. Where synced files are saved is configured on a per-folder basis in the WebGUI.

**Note:** The configuration option `webui/password_hash` does not seem to be working correctly with recent versions of `btsync`. Use `webui/password` instead for specifying credentials.

### Automatic config file creation

The [btsync-autoconfig](https://aur.archlinux.org/packages/btsync-autoconfig/) package provides a systemd user service (`btsync-autoconfig.service`) which, if enabled, triggers when a user's `btsync.service` starts and creates a config file with default values if it does not already exist.

**Note:** If the config file was generated by [btsync-autoconfig](https://aur.archlinux.org/packages/btsync-autoconfig/) it will be configured with a different port. Rather than 8888, the port for the user's instance of `btsync` will be `7889 + $UID`. If your `$UID` is "1000", the port will be 8889.

The install script enables the service for all users by default. Although disabling it defeats most of its purpose, it can be disabled using

```
# systemctl --global disable btsync-autoconfig.service

```

Individual users can then enable it if they like:

```
$ systemctl --user enable btsync-autoconfig.service

```

`btsync-autoconfig.service` creates `~/.config/btsync/btsync.conf` if it does not exist, and guesses some default values of the settings:

*   device_name: `$USER@$HOSTNAME`
*   storage_path: `~/.btsync`
*   webui/login: `$USER/password`

The script also creates the `storage_path` directory set in the config file if it does not exist. This is done intependently from the creation of the config file.

## Troubleshooting

### Missing storage path

If you start the service but can't reach the WebUI, check the status of the btsync by entering `systemctl --user status btsync` (or `systemctl status btsync` for the system-wide instance).

A common error is `Storage path specified in config file does not exist.`. This is easily fixed by `mkdir ~/.btsync`, or whatever your `storage_path` is set to.

### Ignore some files/folders synchronization

If you don’t want BitTorrent Sync to track some files in your sync folder, please use `IgnoreList`. `IgnoreList` is located in hidden `.sync` folder.

`IgnoreList` is a UTF-8 encoded .txt file that allows you to specify single files, paths or rules for ignoring during the synchronization job. Each line of the `IgnoreList` file represents a separate rule. All the files that fall under the ignore filter are not indexed and not counted in the "Size" column in Sync main view.

It supports '?' and '*' wildcard symbols.

Note that `IgnoreList` is applied only to the folder where it is contained and will not work with the files that have already been synced. If you add indexed files to `IgnoreList`, they will be deleted on other syncing devices. In order to avoid this:

*   Remove the folder from sync on all the devices.
*   Modify `IgnoreList` file on all of them so that it contains same info.
*   Re-add the modified folders.

For further details, please refer to [Ignoring files in Sync (IgnoreList)](http://help.getsync.com/customer/portal/articles/1673122-ignoring-files-in-sync-ignorelist-?b_id=3895)

### ARM alignment error

Add the line `w /proc/cpu/alignment - - - - 2` to `/etc/tmpfiles.d/btsync.conf`. (You need to create the file).
Note that this may lead to performance degradation.

## See also

*   [Official BitTorrent Sync Help](http://help.getsync.com/)
*   [Official BitTorrent Sync FAQ](http://www.bittorrent.com/help/faq/sync)