[ReadyMedia](https://sourceforge.net/projects/minidlna) (previously **MiniDLNA**) is server software with the aim of being fully compliant with [DLNA](https://en.wikipedia.org/wiki/Digital_Living_Network_Alliance "wikipedia:Digital Living Network Alliance")/[UPnP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play "wikipedia:Universal Plug and Play") clients. The MiniDNLA daemon serves media files (music, pictures, and video) to clients on a network. Example clients include applications such as Totem and [Kodi](/index.php/Kodi "Kodi"), and devices such as portable media players, Smartphones, Televisions, and gaming systems (such as PS3 and Xbox 360).

ReadyMedia is a simple, lightweight alternative to [MediaTomb](/index.php/MediaTomb "MediaTomb"), but has fewer features. It does not have a web interface for administration and must be configured by editing a text file.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration and starting](#Configuration_and_starting)
    *   [2.1 Automatic Media_DB Update](#Automatic_Media_DB_Update)
    *   [2.2 Troubleshooting service autostart](#Troubleshooting_service_autostart)
    *   [2.3 Running minidlna as your own user](#Running_minidlna_as_your_own_user)
*   [3 Other aspects](#Other_aspects)
    *   [3.1 Firewall](#Firewall)
    *   [3.2 File System and Localization](#File_System_and_Localization)
    *   [3.3 Media Handling](#Media_Handling)
*   [4 Building a media server](#Building_a_media_server)
    *   [4.1 Automount external drives](#Automount_external_drives)
    *   [4.2 Issues](#Issues)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Server not visible on Wireless behind a router](#Server_not_visible_on_Wireless_behind_a_router)
    *   [5.2 Media directory not accessible](#Media_directory_not_accessible)
    *   [5.3 DLNA server stops being visible after some time when being shared on a bridge device](#DLNA_server_stops_being_visible_after_some_time_when_being_shared_on_a_bridge_device)

## Installation

Install the [minidlna](https://www.archlinux.org/packages/?name=minidlna) package.

If you want to use an unofficial branch which supports transcoding, install the [readymedia-transcode-git](https://aur.archlinux.org/packages/readymedia-transcode-git/) package.

## Configuration and starting

By default, minidlna runs as a system service (alternatively, you can [run it as your own user](#Running_minidlna_as_your_own_user)). It can be configured in `/etc/minidlna.conf`. Set the following necessary settings:

```
#network_interface=eth0                         # Self-discovers if commented (at times necessary to set)
media_dir=A,/home/user/Music                    # Mounted Media_Collection drive directories
media_dir=P,/home/user/Pictures                 # Use A, P, and V to restrict media 'type' in directory
media_dir=V,/home/user/Videos
friendly_name=Media Server                      # Optional
inotify=yes                                     # 'no' for less resources, restart required for new media
presentation_url=[http://www.mylan/index.php](http://www.mylan/index.php)     # or use your device static IP [http://192.168.0.14:8200/](http://192.168.0.14:8200/)
```

By default MiniDLNA runs as the *minidlna* user, which can be changed with the `user` line in `/etc/minidlna.conf`. If you change MiniDLNA user, you should also change the `db_dir` and `log_dir` options to directories that are writeable by that user.

The minidlna service can be managed by `minidlna.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

### Automatic Media_DB Update

Kernel adds one [inotify](https://en.wikipedia.org/wiki/Inotify "wikipedia:Inotify") watch per each folder/subfolder in *Media_Collection* Directories set in `/etc/minidlna.conf` to monitor changes thus allowing MiniDLNA to update *Media_DB* in real time. When MiniDLNA is run as a regular user, it does not have the ability to change the kernel's *inotify* limits. If default number of *inotify* watches is non-sufficient to have MiniDLNA monitor all your media folders, increase *inotify* watches through `sysctl` (100000 should be enough for most uses):

```
# sysctl fs.inotify.max_user_watches=100000

```

To have it permanently changed, add to `/etc/sysctl.d/90-inotify.conf`

```
# Increase inotify max watchs per user for local minidlna
fs.inotify.max_user_watches = 100000

```

*inotify* performance may depend on device type. Some do not rescan media drives on a consistent basis or at all. If files are added/deleted to monitored media directories, they may not be noticed until the device DLNA client is restarted.

Check *inotify* updates via MiniDLNA *presentation_url* by comparing files count. If it does not change, make sure the user running MiniDLNA has *rw* access to the DB folder. If the issue persists, copy or download new files first to a non-watched by *inotify* **Downloads** folder on the same drive, and then move them to appropriate media folders, since lengthy media files copying or downloading may confuse *inotify*.

You can also clean or rebuild MiniDLNA DB manually after stopping MiniDLNA daemon, or analyze its debug output (Ctrl+C to exit):

[Stop](/index.php/Stop "Stop") the MiniDLNA daemon.

To rebuild Media_DB forcibly:

```
# minidlnad -R

```

Stop the daemon after rebuilding Media_DB e.g. `killall minidlnad`.

To run in debug mode:

```
# minidlnad -d

```

`Ctrl+C` to exit it.

### Troubleshooting service autostart

Sometimes the minidlna daemon fails to start while booting. [NetworkManager#Enable NetworkManager Wait Online](/index.php/NetworkManager#Enable_NetworkManager_Wait_Online "NetworkManager") solves this issue. See [FS#35325](https://bugs.archlinux.org/task/35325)

### Running minidlna as your own user

Alternatively to a system service, you can run minidlna as your own user. This can be useful if you want to share media but don't have administrator access to the machine.

Create the necessary files and directories locally and edit the configuration:

```
$ install -Dm644 /etc/minidlna.conf ~/.config/minidlna/minidlna.conf
$ $EDITOR minidlna.conf

```

Configuring should be as above, specifically:

```
media_dir=/home/$USER/dir
db_dir=/home/$USER/.config/minidlna/cache
log_dir=/home/$USER/.config/minidlna

```

You can now start minidlna with the following command:

```
$ minidlnad -f /home/$USER/.config/minidlna/minidlna.conf -P /home/$USER/.config/minidlna/minidlna.pid

```

To autostart it at login, add the previous line to `~/.bash_profile`.

## Other aspects

Other aspects and MiniDLNA limitations may need to be considered beforehand to ensure satisfaction from its performance.

### Firewall

If using a firewall the the ssdp (1900/udp) and trivnet1 (8200/tcp) ports will need to be opened. For example, this can be done with arno's iptables firewall by editing `firewall.conf` and opening the ports by doing:

```
OPEN_TCP="8200"
OPEN_UDP="1900"

```

### File System and Localization

When keeping MiniDLNA *Media_DB* on an external drive accessible in both Linux and Windows, choose proper [file system](/index.php/File_system "File system") for it. **NTFS** preserves in Windows its Linux defaults: *rw* access for *root* user and *UTF8* font *encoding* for file names, so media titles in your language are readable when browsing *Media_DB* in terminal and media players, since most support *UTF8*. If you prefer **Vfat** (FAT32) for better USB drive compatibility with older players when hooked directly, or your *Media_Collection* drive is Vfat and has folder & file names in your local language, MiniDLNA can transcode them to *UTF8* charset while scanning folders to *Media_DB*. Add to *Media_Collection* and *Media_DB* drives' mount options your FS language [codepage](https://en.wikipedia.org/wiki/Code_page "wikipedia:Code page") for transcoding to short DOS file names, and [iocharset](https://en.wikipedia.org/wiki/Character_encoding "wikipedia:Character encoding") for converting long file names to your terminal's locale, i.g. *codepage=cp866,iocharset=utf8 (or ISO-8859-5)*. Set *rw* permissions for all users, since *Vfat* does not preserve Linux access permissions:

 `UUID=6140-75F7 /media/MyDrive/Media_DB vfat user,rw,async,noatime,umask=111,dmask=000,codepage=cp866,iocharset=utf8 0 0` 

While your *iocharset* would be present in the system with a matching [locale](/index.php/Locale "Locale"), if your terminal or player supports only short file names, check if the set *codepage* is also present and enabled (like ru_RU.CP866), i.e. was included in system config when ArchLinux release was compiled, or consider recompiling the release to add it:

```
ls /usr/share/fonts/encodings

```

MiniDLNA lists *Movies* and *Photos* by file name in its DB, and *Music* entries by [ID3 tags](http://id3lib.sourceforge.net/id3/) instead of file names. If Music collection was not tagged in UTF8 but in a local charset, MiniDLNA might not identify and transcode it correctly to UTF8 for display in media players, or the original tags *codepage(s)* may be absent in your system, so the tags will not be readable even when media file names are. In this case consider re-tagging your collection to *UTF-16BE* or *UTF-8* encoding with an **ID3 Tag Converter**.

Picking the "right" *file system* for your *Media_Collection* is a trade-off: XFS and EXT4 show fast read/write for HDs and lower CPU load critical for small [Plug Computers](http://archlinuxarm.org/platforms/armv5/pogoplug-series-4) with attached storage. NTFS is most compatible with Windows when plugging a drive directly for faster copy, while network file systems like Samba, NFS or iSCSI allow import to Windows any Linux FS with slower data copy. As file fragmentation affects playback, store your Movies on a non-system drive formatted in XFS (prevents fragments), NTFS (fragment resistant and easy to defrag), or EXT4 (uses large file *extents*), and [avoid](https://trac.transmissionbt.com/ticket/849) EXT3 or [less](https://en.wikipedia.org/wiki/File_Allocation_Table#Fragmentation "wikipedia:File Allocation Table") resistant FAT32\. For smaller Flash drives with seldom fragmented Music and Photo files, VFAT (FAT32) and EXT4 show faster writes with less CPU load, but EXT4 may affect memory wear due to journaling, and less compatible with media players. Proper drive partitioning, block [alignment](http://lwn.net/Articles/428584/) and *mount options* (i.e. *async,noatime*...- choice depends on file system and memory type) can greatly [accelerate](http://linux-howto-guide.blogspot.ca/2009/10/increase-usb-flash-drive-write-speed.html) flash and HD drive speed among other [advantages](https://en.wikipedia.org/wiki/Logical_Disk_Manager#Advantages_of_using_a_1-MiB_alignment_boundary "wikipedia:Logical Disk Manager").

### Media Handling

MiniDLNA is aimed for small devices, so does not generate movie thumbnails to lower CPU load and DB built time. It uses either thumbs in the same folder with movie if any, or extracts them where present from media containers like MP4 or MKV with embedded Album Art tags, but not AVI. One can add thumbs (JPG 160x160 pxl or less) to media folders with a **Thumbnail Maker**, and miniDLNA will link them to media files after rescan. Larger thumbs will be resized and stored in *Media_DB* that slows scan. At one movie per folder, follow thumb naming rules in *minidlna.conf*. For multiple show episodes per folder, each thumb name should match its episode name without ext. (*<file>.cover.jpg* or *<file>.jpg*). To handle *MS Album Art* thumb names with GUID, add * to the end *"AlbumArt_{*".jpg* . MiniDLNA will list on screen only chosen media type (i.e. Movies), but will not other files in the same folder.

When viewing photos, progressive and/or lossless compression JPG may not be supported by your player via DLNA. Also resize photos to "suggested photo size" by the player's docs for problem free image slideshow. DLNA spec restricts image type to JPG or PNG, and max size to 4096 x 4096 pixels - and that is if the DLNA server implementation supports the LARGE format. The next size limit down (MEDIUM) is 1024 x 768, so resizing may help to show photos correctly.

To decrease system load, MiniDLNA does not transcode on the fly unsupported media files into supported by your player formats. When building *Media_DB*, it might not correctly identify whether certain formats are supported by your player, which may play via UPnP a broader formats choice. DLNA standard is quite limiting UPnP subset in media containers and codec *profiles* allowed. If you do not see on TV screen or cannot play some media files listed in *Media_DB*, check if your HD started spinning or try connecting to your media player via USB for their playback. MiniDLNA might not support choosing audio tracks, subtitles, disk chapters, list sorting, and other advanced playback features for your player model.

## Building a media server

Media served could be based on lightweight and cheap system like development board (Raspberry Pi, CubeBoard, etc.). You do not even need to put X Server on this board.

### Automount external drives

This is very useful if you want to automate the server. See [udev#Automounting udisks wrappers](/index.php/Udev#Automounting_udisks_wrappers "Udev") for more information.

### Issues

Media server based on MiniDLNA could face the drive re-scan issue. Ex.: external HDD you have plugged will be scanned each time again and again. This happens due to MiniDLNA removes DB records for unplugged drive. If your drive plugged all the time it is not a problem, but if you have "pluggable" media library on large external drives this could take a big while till you start watching your video.

One can resolve the rescan issue by using [this minidlna fork](https://code.google.com/p/minidlna-fastscan). It creates a metadata file next to each video file. This can significantly decrease the scan time for large media.

## Troubleshooting

### Server not visible on Wireless behind a router

On some network configurations when the machine hosting MiniDLNA server is connected to the router through Ethernet, there may be problems accessing MiniDLNA server on WiFi (same router). To solve this, make sure that "Multicast Isolation" is turned off on the router. For example, on ADB / Pirelli P.RG EA4202N router, connect to the configuration page, then Settings->Bridge and VLAN->Bridge List->click edit on Bridge Ethernet WiFi->set Multicast Isolation to No->Apply.

### Media directory not accessible

Please note that the default systemd service file enforces the parameter `ProtectHome=on`. If you intend to share files that reside within the `/home/` file system you may want to lessen that restriction. You can achieve this by updating the [systemd](/index.php/Systemd "Systemd") unit override file.

 `/etc/systemd/system/minidlna.service.d/override.conf` 
```
[Service]
ProtectHome=read-only
```

### DLNA server stops being visible after some time when being shared on a bridge device

If you are using ReadyMedia to "broadcast" on a bridged device (such as an OpenVPN device bridged to an Ethernet device), the server may stop being seen by the clients after some time (which may vary from a few seconds to half a day). In order to solve this you need to disable 'multicast snooping'. You can do it instantly with the following command:

```
# echo 0 >> /sys/devices/virtual/net/br0/bridge/multicast_snooping

```

This should make the server visible to the clients *immediately*, but the change will be lost on reboot. If this works, you can make it a permanent change by issuing the following command:

```
# echo 'net.br0.bridge.multicast_snooping=0' > /etc/sysctl.d/35-minidlna_no_snoop.conf

```