Related articles

*   [Xfce](/index.php/Xfce "Xfce")
*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files")
*   [PCManFM](/index.php/PCManFM "PCManFM")
*   [Nemo](/index.php/Nemo "Nemo")

From the project [home page](https://docs.xfce.org/xfce/thunar/start):

	Thunar is a modern file manager for the Xfce Desktop Environment. Thunar has been designed from the ground up to be fast and easy-to-use. Its user interface is clean and intuitive, and does not include any confusing or useless options by default. Thunar is fast and responsive with a good start up time and folder load time.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Plugins and addons](#Plugins_and_addons)
*   [2 Thunar Volume Manager](#Thunar_Volume_Manager)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Automounting of large external drives](#Automounting_of_large_external_drives)
    *   [3.2 Using Thunar to browse remote locations](#Using_Thunar_to_browse_remote_locations)
    *   [3.3 Starting in daemon mode](#Starting_in_daemon_mode)
    *   [3.4 Solving problem with slow cold start](#Solving_problem_with_slow_cold_start)
    *   [3.5 Hide Shortcuts in Side Pane](#Hide_Shortcuts_in_Side_Pane)
    *   [3.6 Assign keyboard shortcuts in Thunar](#Assign_keyboard_shortcuts_in_Thunar)
    *   [3.7 Showing partitions defined in fstab](#Showing_partitions_defined_in_fstab)
*   [4 Custom actions](#Custom_actions)
    *   [4.1 Search for files and folders](#Search_for_files_and_folders)
    *   [4.2 Scan for viruses](#Scan_for_viruses)
    *   [4.3 Link to Dropbox](#Link_to_Dropbox)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Tumblerd hangs up, uses too much CPU](#Tumblerd_hangs_up,_uses_too_much_CPU)
    *   [5.2 Trash/network icons disappear randomly](#Trash/network_icons_disappear_randomly)
    *   [5.3 Not authenticated to mount filesystems](#Not_authenticated_to_mount_filesystems)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [thunar](https://www.archlinux.org/packages/?name=thunar) package. Thunar is part of the [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/) group and the default file manager of the [xfce](/index.php/Xfce "Xfce") desktop environment.

### Plugins and addons

*   **Gnome Virtual File System** — For trash support, mounting removable media, and remote filesystems (`mtp`/`smb`). See [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality") for more details.

	[https://wiki.gnome.org/Projects/gvfs](https://wiki.gnome.org/Projects/gvfs) || [gvfs](https://www.archlinux.org/packages/?name=gvfs)

*   **Thunar Archive Plugin** — Plugin which allows you to create and extract archive files using contextual menu items. It does not create or extract archives directly, but instead acts as a frontend for other programs such as File Roller ([file-roller](https://www.archlinux.org/packages/?name=file-roller)), Ark ([ark](https://www.archlinux.org/packages/?name=ark)) or Xarchiver ([xarchiver](https://www.archlinux.org/packages/?name=xarchiver)). Part of [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) || [thunar-archive-plugin](https://www.archlinux.org/packages/?name=thunar-archive-plugin)

*   **Thunar Media Tags Plugin** — Plugin which allows you to view detailed information about media files. It also has a bulk renamer and allows editing of media tags. It supports ID3 (the MP3 file format's system) and Ogg/Vorbis tags. Part of [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/).

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) || [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin)

*   **Thunar Shares Plugin** — Plugin which allows you to quickly share a folder using Samba from Thunar without requiring root access. See also [how to configure directions](/index.php/Samba#Enable_Usershares "Samba").

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin](https://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin) || [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/)

*   **[Thunar Volume Manager](#Thunar_Volume_Manager)** — Automatic management of removeable devices in Thunar. Part of [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/).

	[https://goodies.xfce.org/projects/thunar-plugins/thunar-volman](https://goodies.xfce.org/projects/thunar-plugins/thunar-volman) || [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman)

*   **Tumbler** — External program to generate thumbnails. Also install [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer) to enable video thumbnailing.

	[https://git.xfce.org/xfce/tumbler/tree/README](https://git.xfce.org/xfce/tumbler/tree/README) || [tumbler](https://www.archlinux.org/packages/?name=tumbler)

*   **RAW Thumbnailer** — A lightweight and fast raw image thumbnailer that is needed to display raw thumbnails.

	[https://code.google.com/p/raw-thumbnailer/](https://code.google.com/p/raw-thumbnailer/) || [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer)

*   **libgsf** — The GNOME Structured File Library is a utility library for reading and writing structured file formats. Install if you need support for odf thumbnails

	[https://directory.fsf.org/wiki/Libgsf](https://directory.fsf.org/wiki/Libgsf) || [libgsf](https://www.archlinux.org/packages/?name=libgsf)

## Thunar Volume Manager

While Thunar supports automatic mounting and unmounting of removable media ([gvfs](https://www.archlinux.org/packages/?name=gvfs) package is required), the Thunar Volume Manager allows extended functionality, such as automatically running commands or automatically opening a Thunar window for mounted media.

### Installation

Thunar Volume Manager can be installed from the package [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman) in the official repositories.

**Tip:** To let Thunar handle automatic mounting, one must launch thunar in [daemon mode](#Starting_in_daemon_mode).

### Configuration

It can also be configured to execute certain actions when cameras and audio players are connected. After installing the plugin:

1.  Launch Thunar and go to *Edit > Preferences*
2.  Under the 'Advanced' tab, check 'Enable Volume Management'
3.  Click configure and check the following items:
    *   Mount removable drives when hot-plugged.
    *   Mount removable media when inserted.
4.  Also make desired changes (see the example below)

Here's an example setting for making Amarok play an audio CD.

```
 Multimedia - Audio CDs: `amarok --cdplay %d`

```

## Tips and tricks

### Automounting of large external drives

If Thunar refuses to mount large removable media (size > 1TB) although thunar-volman and gvfs has been installed, then try installing a different automounter such as [udevil](https://www.archlinux.org/packages/?name=udevil) or [udiskie](https://www.archlinux.org/packages/?name=udiskie). The latter should be preferred as it uses udisks2 and thus is compatible with gvfs. To start udiskie with udisks2 support, add the following line to your autostart file:

```
udiskie -2 &

```

### Using Thunar to browse remote locations

Since Xfce 4.8 (Thunar 1.2) it is possible to browse remote locations (such as FTP servers or Samba shares) directly in Thunar. To enable this functionality ensure that [gvfs](https://www.archlinux.org/packages/?name=gvfs), [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) and [sshfs](https://www.archlinux.org/packages/?name=sshfs) packages are installed. A 'Network' entry is visible in Thunar's side bar and remote locations can be opened by using the following URI schemes in the location dialog (opened with `Ctrl+l`): smb://, ftp://, ssh://, sftp://, davs:// & followed by the server hostname or IP address.

There is no URI scheme for [NFS](/index.php/NFS "NFS") shares, but Thunar can issue a `mount` command if you setup your [fstab](/index.php/Fstab "Fstab") properly.

 `/etc/fstab` 
```
# nas1 server
nas1:/c/home		/media/nas1/home	nfs	noauto,user,_netdev,bg  0 0
```

What's important here is the `noauto` which prevents the share from being mounted until you click on it, `user` which allows any user to mount (and unmount) the share, `_netdev` which makes network connectivity a pre-requisite, and finally `bg` which puts the mounting operation the background so if your server requires some spin-up time you won't have to deal with time out messages and re-clicking until it works.

**Tip:** If you want to permanently store passphrases of remote filesystem locations, you have to install [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

### Starting in daemon mode

Thunar may be run in daemon mode. This has several advantages, including a faster startup for Thunar, Thunar running in the background and only opening a window when necessary (for instance, when a flash drive is inserted), and letting Thunar handle automatic mounting of removable media.

Make sure the command `thunar --daemon` is autostarted on login. See [Xfce](/index.php/Xfce "Xfce") and [Autostarting](/index.php/Autostarting "Autostarting") for more details.

### Solving problem with slow cold start

Some people still have problems with Thunar taking a long time to start for the first time. This is due to gvfs checking the network, preventing Thunar from starting until gvfs finishes its operations. To change this behaviour, edit `/usr/share/gvfs/mounts/network.mount` and change **AutoMount=true** to **AutoMount=false**.

### Hide Shortcuts in Side Pane

There is a hidden menu to hide Shortcuts in the Side Pane.

Right click in the Side Pane where there are no shortcuts, like on the DEVICES section label. Then you will get a pop-up menu where you can uncheck items you do not want displayed.

### Assign keyboard shortcuts in Thunar

See [GTK+#Keyboard shortcuts](/index.php/GTK%2B#Keyboard_shortcuts "GTK+"),

### Showing partitions defined in fstab

By default Thunar will not show in devices any partitions defined in `/etc/fstab` besides the root partition.

We can change that by adding the option **x-gvfs-show** to fstab for the partition we wish to show.

## Custom actions

This section covers useful custom actions which can be accessed through `Edit -> Configure custom actions` and which are stored in `~/.config/Thunar/uca.xml`. More examples are listed in the [thunar wiki](https://docs.xfce.org/xfce/thunar/custom-actions). Furthermore, [this](https://duncanlock.net/blog/2013/06/28/useful-thunar-custom-actions/) blog post provides a comprehensive collection of custom actions.

### Search for files and folders

To use this action you need to have [catfish](https://www.archlinux.org/packages/?name=catfish) installed. The optional dependency [mlocate](https://www.archlinux.org/packages/?name=mlocate) should be installed as well.

| Name | Command | File patterns | Appears if selection contains |
| Search | `catfish --path=%f` | * | Directories |

### Scan for viruses

To use this action you need to have [clamav](https://www.archlinux.org/packages/?name=clamav) and [clamtk](https://www.archlinux.org/packages/?name=clamtk) installed.

| Name | Command | File patterns | Appears if selection contains |
| Scan for virus | `clamtk %F` | * | Select all |

### Link to Dropbox

| Name | Command | File patterns | Appears if selection contains |
| Link to Dropbox | `ln -s %f /path/to/DropboxFolder` | * | Directories, other files |

Please note that when using many custom actions to symlink files and folder to a particular place, it might be useful to put them into the `Send To` folder of the context menu to avoid that the menu itself gets bloated. This is fairly easy to achieve and requires a .desktop file in `~/.local/share/Thunar/sendto` for each action to perform. Say we want to put the above Dropbox symlink action into Send To, we create a `dropbox_folder.desktop` with the following content. The new applied action will be active after restarting Thunar.

```
[Desktop Entry]
Type=Application
Version=1.0
Encoding=UTF-8
Exec=ln -s %f /path/to/DropboxFolder
Icon=/usr/share/icons/dropbox.png
Name=Dropbox

```

## Troubleshooting

### Tumblerd hangs up, uses too much CPU

Tumblerd, the service that watches the file system and notifies the system when a thumbnail needs to be made may get stuck in a loop, using 100% of the system's CPU, see the [bug report](https://bugzilla.xfce.org/show_bug.cgi?id=7384). The following script is a temporary workaround to stop this from happening. Copy, and paste this into a *.sh* file, save it somewhere in your home directory, mark the file as executable then set up the system to autostart it at system startup.

```
#!/bin/bash
period=20
tumblerpath="/usr/lib/*/tumbler-1/tumblerd" # The * here should find the right one, whether 32 and 64-bit
cpu_threshold=50
mem_threshold=20
max_strikes=2                               # max number of above cpu/mem-threshold's in a row
log="/tmp/tumblerd-watcher.log"

if [[ -n "${log}" ]]; then
    cat /dev/null > "${log}"
    exec >"${log}" 2>&1
fi

strikes=0
while sleep "${period}"; do
    while read pid; do
	cpu_usage=$(ps --no-headers -o pcpu -f "${pid}"|cut -f1 -d.)
	mem_usage=$(ps --no-headers -o pmem -f "${pid}"|cut -f1 -d.)

	if [[ $cpu_usage -gt $cpu_threshold ]] || [[ $mem_usage -gt $mem_threshold ]]; then
	    echo "$(date +"%F %T") PID: $pid CPU: $cpu_usage/$cpu_threshold %cpu MEM: $mem_usage/$mem_threshold STRIKES: ${strikes} NPROCS: $(pgrep -c -f ${tumblerpath})"
	    (( strikes++ ))
	    if [[ ${strikes} -ge ${max_strikes} ]]; then
		kill "${pid}"
		echo "$(date +"%F %T") PID: $pid KILLED; NPROCS: $(pgrep -c -f ${tumblerpath})"
		strikes=0
	    fi
	else
	    strikes=0
	fi
    done < <(pgrep -f ${tumblerpath})
done

```

### Trash/network icons disappear randomly

Make sure all Thunar instances start **after** *gvfs*. [[1]](https://bugs.launchpad.net/ubuntu/+source/thunar/+bug/1057610) For `thunar --daemon`, you can create a wrapper that waits until GVFS is active:

**Note:** `/usr/local/bin` should come before `/usr/bin` in `$PATH`.
 `/usr/local/bin/Thunar` 
```
#!/bin/bash
if [[ $1 == --daemon ]]; then
  until pgrep gvfs >/dev/null; do
    sleep 1
  done
  exec /usr/bin/Thunar "$@"
else
  exec /usr/bin/Thunar "$@"
fi

```

### Not authenticated to mount filesystems

See [File manager functionality#Troubleshooting](/index.php/File_manager_functionality#Troubleshooting "File manager functionality").

## See also

*   [Thunar](https://docs.xfce.org/xfce/thunar/start) project page
*   [Thunar Volume Manager](https://goodies.xfce.org/projects/thunar-plugins/thunar-volman) project page
*   This [list](https://goodies.xfce.org/projects/thunar-plugins/start) of plugins
*   Several settings, like showing the full path in the title, are available through `xfconf-query`. See [this list](https://docs.xfce.org/xfce/thunar/hidden-settings) for more details.