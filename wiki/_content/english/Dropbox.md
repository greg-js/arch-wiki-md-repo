Related articles

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [Syncthing](/index.php/Syncthing "Syncthing")

[Dropbox](https://www.dropbox.com) is a file sharing system with a GNU/Linux client. Use it to transparently sync files across computers and architectures. Simply drop files into your `~/Dropbox` folder, and they will automatically sync to your centralized repository.

**Note:** In July, 2019, Dropbox Client build 77.3.127 added support for [ZFS](/index.php/ZFS "ZFS"), [eCryptfs](/index.php/ECryptfs "ECryptfs"), [XFS](/index.php/XFS "XFS") and [Btrfs](/index.php/Btrfs "Btrfs").[[1]](https://www.dropboxforum.com/t5/Desktop-client-builds/Beta-Build-77-3-127/td-p/354660) It once dropped support for all file systems except plain [Ext4](/index.php/Ext4 "Ext4") in November, 2018.[[2]](https://www.dropboxforum.com/t5/Syncing-and-uploads/Dropbox-client-warns-me-that-it-ll-stop-syncing-in-Nov-why/m-p/290065/highlight/true#M42255)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 AUR](#AUR)
    *   [1.2 Optional packages](#Optional_packages)
    *   [1.3 Prevent automatic updates](#Prevent_automatic_updates)
*   [2 Autostart](#Autostart)
    *   [2.1 Autostart with your WM/DE](#Autostart_with_your_WM/DE)
    *   [2.2 Autostart on boot with systemd](#Autostart_on_boot_with_systemd)
    *   [2.3 Autostart on login with systemd](#Autostart_on_login_with_systemd)
*   [3 Accessing the files without installing a sync client](#Accessing_the_files_without_installing_a_sync_client)
*   [4 Encrypting your Dropbox files](#Encrypting_your_Dropbox_files)
    *   [4.1 Setup EncFS with Dropbox](#Setup_EncFS_with_Dropbox)
*   [5 Multiple Dropbox instances](#Multiple_Dropbox_instances)
*   [6 Dropbox on laptops](#Dropbox_on_laptops)
    *   [6.1 Using netctl](#Using_netctl)
    *   [6.2 Using NetworkManager](#Using_NetworkManager)
    *   [6.3 Using wicd](#Using_wicd)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Using Dropbox with non-ext4 filesystems](#Using_Dropbox_with_non-ext4_filesystems)
    *   [7.2 Dropbox keeps saying Downloading files](#Dropbox_keeps_saying_Downloading_files)
    *   [7.3 Change the Dropbox location from the installation wizard](#Change_the_Dropbox_location_from_the_installation_wizard)
    *   [7.4 Context menu entries in file manager do not work](#Context_menu_entries_in_file_manager_do_not_work)
    *   [7.5 Connecting...](#Connecting...)
    *   [7.6 Dropbox does not start - "This is usually because of a permission error"](#Dropbox_does_not_start_-_"This_is_usually_because_of_a_permission_error")
        *   [7.6.1 Check permissions](#Check_permissions)
        *   [7.6.2 Re-linking your account](#Re-linking_your_account)
        *   [7.6.3 Errors caused by running out of space](#Errors_caused_by_running_out_of_space)
        *   [7.6.4 Locale caused errors](#Locale_caused_errors)
        *   [7.6.5 Filesystem monitoring problem](#Filesystem_monitoring_problem)
    *   [7.7 Proxy settings](#Proxy_settings)
    *   [7.8 Missing tray icon in GNOME](#Missing_tray_icon_in_GNOME)

## Installation

### AUR

[dropbox](https://aur.archlinux.org/packages/dropbox/) can be [installed](/index.php/Install "Install"). Alternatively, [dropbox-experimental](https://aur.archlinux.org/packages/dropbox-experimental/) is also available. As a last resort, the Dropbox website has instructions for a [headless install via command line](https://www.dropbox.com/install?os=lnx).

1.  After installing the package, you can start Dropbox from your application menu or run `dropbox` from the command-line. The client icon will appear in the system tray.
2.  A pop-up will notify you that Dropbox is running from an unsupported location. Click on *Don't ask again* since you know that you have installed it from AUR rather than from the official homepage.
3.  Eventually a pop-up will ask you to log in to your Dropbox account or create a new account. Enter your credentials.
4.  After some time you will see a "Welcome to Dropbox" pop-up, which will give you the opportunity to view a short tour of Dropbox.
5.  Press the "Finish and go to My Dropbox".

### Optional packages

| command-line interface | [dropbox-cli](https://aur.archlinux.org/packages/dropbox-cli/) |
| [GNOME/Files](/index.php/GNOME/Files "GNOME/Files") integration | [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/) |
| [Nemo](/index.php/Nemo "Nemo") integration | [nemo-dropbox](https://aur.archlinux.org/packages/nemo-dropbox/) |
| [Thunar](/index.php/Thunar "Thunar") integration | [thunar-dropbox](https://aur.archlinux.org/packages/thunar-dropbox/) |
| [Dolphin](/index.php/Dolphin "Dolphin") integration | [dolphin-plugins](https://www.archlinux.org/packages/?name=dolphin-plugins) |
| Caja integration | [caja-dropbox](https://aur.archlinux.org/packages/caja-dropbox/) |
| [KDE](/index.php/KDE "KDE") client | [kfilebox](https://aur.archlinux.org/packages/kfilebox/) |

Note that in order to access the GUI and the settings, the only way is via a tray icon. You need an X panel with a system tray or a standalone [system tray application](/index.php/List_of_applications#System_tray "List of applications") for that.

### Prevent automatic updates

Since at least version 2.4.6 (see comments around 2013-11-06 on [AUR](https://aur.archlinux.org/packages/dropbox/?comments=all)), Dropbox has had an auto-update capability which downloads a new binary to the `~/.dropbox-dist/` folder. The service then attempts to hand over control to this binary and dies, causing systemd to re-start the service, generating a conflict and an endless loop of log-filling, CPU-eating misery.

A workaround is to prevent Dropbox from downloading the automatic update by creating the `~/.dropbox-dist/` folder and making it read-only:

```
$ rm -rf ~/.dropbox-dist
$ install -dm0 ~/.dropbox-dist

```

This appears to be necessary for modern Dropbox clients to operate successfully from systemd on arch.

Also see the [relevant Dropbox forum post](https://www.dropboxforum.com/hc/en-us/community/posts/202917115-dropbox-will-not-start-under-systemd-on-linux).

## Autostart

In the Dropbox preferences, under the "General" tab there should be a "Start Dropbox on system startup" checkbox. Try checking this box and seeing if Dropbox starts automatically.

If that does not work, uncheck the box and use one of the following methods instead:

### Autostart with your WM/DE

For [KDE](/index.php/KDE "KDE") users, no further steps are required, as KDE saves running applications when logging out and restarts them automatically. Similarly for [Xfce](/index.php/Xfce "Xfce") users, Dropbox will be restarted automatically next time you login since the `dropbox.desktop` file has been placed in `~/.config/autostart`.

For [Cinnamon](/index.php/Cinnamon "Cinnamon") users, it's recommended to start Dropbox client by configuring Startup Applications with a little delay (Cinnamon issue [#4396](https://github.com/linuxmint/Cinnamon/issues/4396)). Starting Dropbox with systemd works, running in background, but there's is no icon on systray due to some Cinnamon bugs ([#481](https://github.com/linuxmint/Cinnamon/issues/481), [#2846](https://github.com/linuxmint/Cinnamon/issues/2846)).

If that does not work, you can start the Dropbox sync client along with your window manager by adding `/usr/bin/dropbox &` to your [xinitrc](/index.php/Xinitrc "Xinitrc") (or `~/.config/openbox/autostart`, depending on your setup).

### Autostart on boot with systemd

**Note:** If *systemd* keeps restarting Dropbox, see [#Prevent automatic updates](#Prevent_automatic_updates).

To have Dropbox automatically start when your system boots, simply [enable](/index.php/Enable "Enable") the systemd service, passing your username as the instance identifier. The service unit to be enabled takes the format `dropbox@*username*`.

By default, running the service does not give you an icon in the system tray because it does not know which X display to use. If you want to have tray support, you must [edit](/index.php/Edit "Edit") the provided service:

 `# systemctl edit dropbox@*username*` 
```
[Service]
Environment=DISPLAY=:0

```

### Autostart on login with systemd

To have Dropbox automatically start when you log in, simply [enable](/index.php/Enable "Enable") the [user service](/index.php/Systemd/User "Systemd/User").

If you want Dropbox to appear in your system tray, you will need to [edit](/index.php/Edit "Edit") the service unit so that it knows which X display the system tray is in:

 `$ systemctl --user edit dropbox` 
```
[Service]
Environment=DISPLAY=:0

```

## Accessing the files without installing a sync client

If all you need is basic access to the files in your Dropbox, you can use the web interface at [https://www.dropbox.com/](https://www.dropbox.com/) to upload and download files to your Dropbox. This can be a viable alternative to running a Dropbox daemon and mirroring all the files on your own machine.

Alternatively, the [AUR](/index.php/AUR "AUR") package [droxi](https://aur.archlinux.org/packages/droxi/) provides a command-line interface to Dropbox similar to the GNU `ftp` client.

## Encrypting your Dropbox files

If you want to store sensitive data in your Dropbox, you should encrypt it before doing so. Syncing to Dropbox is encrypted, but all files are (for the time being) stored on the server unencrypted just as you put them in your Dropbox.

*   Dropbox works with [TrueCrypt](/index.php/TrueCrypt "TrueCrypt"), and after you initially uploaded the TrueCrypt volume to Dropbox, performance is quite okay, because Dropbox has a working binary diff.

*   Another possibility is to use [EncFS](/index.php/EncFS "EncFS"), which has the advantage that all files are encrypted separately, i.e. you do not have to determine in advance the size of the content you want to encrypt and your encrypted directory grows and shrinks while you add/delete/modify files in it. You can also mount an encrypted volume at startup using the `-S` option of `encfs` to avoid having to input the passphrase, but note that your encrypted files are not secure from someone who has direct access to your computer.

*   A third option is to use [gocryptfs](/index.php/Gocryptfs "Gocryptfs"). It is similar to EncFS, except that gocryptfs uses authenticated encryption, for protecting both confidentiality and integrity (tamper-resistance) of the data.

### Setup EncFS with Dropbox

Follow the Wiki instructions to install [EncFS](/index.php/EncFS "EncFS").

Assuming you have set your Dropbox directory as `~/Dropbox`:

Create a folder. Files you want synced to Dropbox will go in here.

```
$ mkdir ~/Private

```

Run the following and enter a password when asked:

```
$ encfs ~/Dropbox/Encrypted ~/Private

```

Your secure folder is ready for use; creating any file inside `~/Private` will automatically encrypt it into `~/Dropbox/Encrypted`, which will then be synced to your cloud storage.

To mount your EncFS folder on every boot, follow the instructions in the [EncFS](/index.php/EncFS#User_friendly_mounting "EncFS") wiki page.

**Tip:** Consider using the `ENCFS6_CONFIG` variable and moving the `.encfs6.xml` file to another location (like a USB stick), to help ensure that your encrypted data and the means to realistically decrypt it do not exist together online.

## Multiple Dropbox instances

If you need to separate or distinguish your data, personal and work usage for example, you can subscribe to Dropbox with different email addresses and have their directories synced by different Dropbox instances running on a single machine.

The basic principle and general how-to are described in the [Dropbox Wiki](http://www.dropboxwiki.com/Multiple_Instances_On_Unix).

To summarize, you can setup new or additional instances with:

```
mkdir /path/to/.dropbox-alt-1
HOME=/path/to/.dropbox-alt-1 /usr/bin/dropbox start -i

```

Once that is done, stop any Dropbox instance still running and start them like this:

```
HOME=/path/to/.dropbox-alt-1 /path/to/.dropbox-alt-1/.dropbox-dist/dropboxd
HOME=/path/to/.dropbox-alt-2 /path/to/.dropbox-alt-2/.dropbox-dist/dropboxd

```

Pay attention to use different `.../.dropbox-dist/dropboxd` binaries. Even when setting a custom HOME value, the `/opt/dropbox/dropbox` or `/opt/dropbox/dropboxd` wrappers allow only one instance and when started they will kill the one already running.

## Dropbox on laptops

Dropbox itself is pretty good at dealing with connectivity problems. If you have a laptop and roam between different network environments, Dropbox will have problems reconnecting if you do not restart it. **Try one of the methods described below first,** if for some reason the problem remains, you may try one of these hackish solutions: [[3]](https://bbs.archlinux.org/viewtopic.php?pid=790905), [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1012343#p1012343).

**Note:** When using any of these methods, you need to prevent Dropbox from doing a standard autostart by unchecking *Dropbox - Preferences - General - Start Dropbox on system startup*. This prevents Dropbox from creating the `~/.config/autostart/dropbox.desktop` file and thus from starting twice.

### Using netctl

For [netctl](/index.php/Netctl "Netctl"), use `ExecUpPost` and `ExecDownPre` respectively in every network profile you use, or for example in `/etc/netctl/interfaces/wlan0` to start Dropbox automatically whenever profile on `wlan0` is active. Add '|| true' to your command to make sure [netctl](/index.php/Netctl "Netctl") will bring up your profile, although Dropbox fails to start.

```
ExecUpPost="*any other code*; su -c 'DISPLAY=:0 /usr/bin/dropbox &' *your_user* || true"
ExecDownPre="*any other code*; killall dropbox"

```

Obviously, `*your_user*` has to be edited and `*any other code*;` can be omitted if you do not have any. The above will make sure that Dropbox is running only if there is a network profile active.

### Using NetworkManager

For [NetworkManager](/index.php/NetworkManager "NetworkManager"), use its [dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") feature.

Create the following file:

 `/etc/NetworkManager/dispatcher.d/10-dropbox.sh` 
```
#!/bin/sh
USER=''your_user''
status=$2
case $status in
       up)
		su -c 'DISPLAY=:0 /usr/bin/dropbox & ' $USER
       ;;
       down)
       		killall dropbox
       ;;
esac

```

or, for the systemd alternative:

 `/etc/NetworkManager/dispatcher.d/10-dropbox.sh` 
```
#!/bin/sh
USER=''your_user''
status=$2

case $status in
       up)
		systemctl start dropbox@$USER.service
       ;;
       down)
       		systemctl stop dropbox@USER.service
       ;;
esac

```

Do not forget to change scripts to be owned by root and to make them executable.

### Using wicd

Create `/etc/wicd/scripts/postconnect/dropbox`:

```
#!/usr/bin/env bash
su -c 'DISPLAY=:0 /usr/bin/dbus-launch dropbox &' your_username

```

or, if you use Dropbox with systemd:

```
#!/usr/bin/env bash
systemctl restart dropbox@<user>

```

Create `/etc/wicd/scripts/postdisconnect/dropbox`:

```
#!/usr/bin/env bash
killall dropbox

```

or, if you use Dropbox with systemd:

```
#!/usr/bin/env bash
systemctl stop dropbox@<user>

```

Do not forget to make the above scripts executable.

## Troubleshooting

### Using Dropbox with non-ext4 filesystems

Workarounds have been created, see for example [dropbox-fix2](https://aur.archlinux.org/packages/dropbox-fix2/). These workarounds are based on substituting the filesystem detection functions by the use of LD_PRELOAD.

It is also possible to create an ext4 formatted [sparse file](/index.php/Sparse_file "Sparse file") within a non-ext4 filesystem. It can then be mounted to the desired location for the Dropbox folder. On btrfs systems, it's recommended to [disable copy-on-write](/index.php/Btrfs#Disabling_CoW "Btrfs").

### Dropbox keeps saying Downloading files

But in fact now files are synced with your box. This problem is likely to appear when your Dropbox folder is located on a NTFS partition whose mount path contains spaces, or permissions are not set for that partition. See more in the [forums](https://bbs.archlinux.org/viewtopic.php?id=153368). To resolve the problem pay attention to your entry in `/etc/fstab`. Avoid spaces in the mount path and set write permissions with the "default_permissions" option:

```
UUID=01CD2ABB65E17DE0 /run/media/username/Windows ntfs-3g uid=username,gid=users,default_permissions 0 0

```

### Change the Dropbox location from the installation wizard

Some users experience the problem during setting-up Dropbox that they cannot select a Dropbox folder other than `/home/username/Dropbox`. In this case when the window for changing the path is shown , hit `Ctrl+l`, enter the location (e.g. /mnt/data/Dropbox) and click on the *Choose* or *Open* button.

### Context menu entries in file manager do not work

Several file managers such as Thunar, GNOME Files or its fork Nemo come with extensions that provide context menu entries for files and folders inside your Dropbox. Most of them will result in a browser action such as opening the file or folder in dropbox.com or sharing the link. If you experience these entries not working, then it is likely you have not set the `$BROWSER` variable which Dropbox requires. See [Environment variables](/index.php/Environment_variables "Environment variables") for details.

### Connecting...

It may happen that Dropbox cannot connect successfully because it was loaded before an internet connection was established. This can happen on wireless connections, or fast loading machines on wired networks. The best solution to this problem, for wired and wireless connections, is [#Dropbox on laptops](#Dropbox_on_laptops) which will ensure that Dropbox is started only after the connection is established.

An alternative solution, for those not using netctl or NetworkManager, is to delay the startup of Dropbox:

*   `cp ~/.config/autostart/dropbox.desktop ~/.config/autostart/dropbox-delayed.desktop`
*   Prevent Dropbox from doing a standard autostart by unchecking Dropbox - Preferences - General - Start Dropbox on system startup. This removes `~/.config/autostart/dropbox.desktop`.
*   Edit `~/.config/autostart/dropbox-delayed.desktop` and replace `Exec=dropbox` with `Exec=bash -c "sleep *timeout* && dropbox"`. Tweak the *timeout* parameter, the value of `3` is a good start.

### Dropbox does not start - "This is usually because of a permission error"

#### Check permissions

Make sure that you own Dropbox's directories before running the application. This includes

*   `~/.dropbox` - Dropbox's configuration directory
*   `~/Dropbox` - Dropbox's download directory (default)

You can ensure this by changing their owner with `chown -R`.

This error could also be caused by `/var` being full.

#### Re-linking your account

[Dropbox's FAQ](https://www.dropbox.com/help/72) suggests that this error may be caused by misconfiguration and is fixed by (re)moving the current configuration folder

```
# mv ~/.dropbox ~/.dropbox.old

```

and restarting Dropbox.

#### Errors caused by running out of space

A common error that might happen is that there is no more available space on your `/tmp` and `/var` partitions. If this happens, Dropbox will crash on startup with the following error in its log:

```
Exception: Not a valid FileCache file

```

A detailed story of such an occurrence can be found in the [forums](https://bbs.archlinux.org/viewtopic.php?pid=973458). Make sure there is enough space available before launching Dropbox.

Another case is when the root partition is full:

```
OperationalError: database or disk is full

```

Check to see the available space on partitions with `df`.

#### Locale caused errors

Try starting `dropbox` with this code:

```
LANG=$LOCALE
dropbox

```

(You can also use a different value for LANG; it must be in the format "en_US.UTF-8") This helps when running from a Bash script or Bash shell where `/etc/rc.d/functions` has been loaded

#### Filesystem monitoring problem

If you have a lot of files to sync in your Dropbox folder, you might get the following error:

```
Unable to monitor filesystem
Please run: echo 100000 | sudo tee /proc/sys/fs/inotify/max_user_watches and restart Dropbox to correct the problem.

```

This can be fixed easily by adding

```
fs.inotify.max_user_watches = 100000

```

to `/etc/sysctl.d/99-sysctl.conf` and then reload the kernel parameters

```
# sysctl --system

```

### Proxy settings

The easiest way to set Dropbox's proxy settings is by defining them manually in the Proxies tab of the Preferences window. Alternatively, you can also set it to 'Auto-detect' and then export your proxy server to the http_proxy env variable prior to starting Dropbox (HTTP_PROXY is also usable)

 `env http_proxy=http://your.proxy.here:port /usr/bin/dropbox` 

or

```
export http_proxy=http://your.proxy.here:port
/usr/bin/dropbox

```

**Note:** Dropbox will only use proxy settings of the form `http://your.proxy.here:port`, not `your.proxy.here:port` as some other applications do.

### Missing tray icon in GNOME

GNOME 3.26 removed support for tray icons in [bug 785956](https://bugzilla.gnome.org/show_bug.cgi?id=785956) which will prevent the Dropbox icon from showing. To restore tray icons an appropriate extension such as [App Indicator](https://extensions.gnome.org/extension/615/appindicator-support/) needs to be installed.