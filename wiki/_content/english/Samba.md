Related articles

*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")
*   [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller")
*   [NFS](/index.php/NFS "NFS")

[Samba](https://www.samba.org/) is a re-implementation of the [SMB](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") networking protocol. It facilitates file and printer sharing among Linux and Windows systems as an alternative to [NFS](/index.php/NFS "NFS"). This article provides instructions for users on how to setup Samba.

## Contents

*   [1 Server](#Server)
    *   [1.1 Installation](#Installation)
        *   [1.1.1 Configure Firewall](#Configure_Firewall)
    *   [1.2 Usage](#Usage)
        *   [1.2.1 User Management](#User_Management)
            *   [1.2.1.1 Adding a user](#Adding_a_user)
            *   [1.2.1.2 Listing users](#Listing_users)
            *   [1.2.1.3 Changing user password](#Changing_user_password)
        *   [1.2.2 Creating a share](#Creating_a_share)
        *   [1.2.3 Starting services](#Starting_services)
    *   [1.3 Advanced Configuration](#Advanced_Configuration)
        *   [1.3.1 Enable usershares](#Enable_usershares)
        *   [1.3.2 Set and forcing permissions](#Set_and_forcing_permissions)
        *   [1.3.3 Restrict protocols for better security](#Restrict_protocols_for_better_security)
        *   [1.3.4 Use native SMB transport encryption](#Use_native_SMB_transport_encryption)
        *   [1.3.5 Disable printer sharing](#Disable_printer_sharing)
        *   [1.3.6 Block certain file extensions on Samba share](#Block_certain_file_extensions_on_Samba_share)
        *   [1.3.7 Improve throughput](#Improve_throughput)
*   [2 Client](#Client)
    *   [2.1 List public shares](#List_public_shares)
    *   [2.2 NetBIOS/WINS host names](#NetBIOS.2FWINS_host_names)
        *   [2.2.1 Disable NetBIOS/WINS support](#Disable_NetBIOS.2FWINS_support)
    *   [2.3 Manual mounting](#Manual_mounting)
        *   [2.3.1 Storing share passwords](#Storing_share_passwords)
    *   [2.4 Automatic mounting](#Automatic_mounting)
        *   [2.4.1 As mount entry](#As_mount_entry)
        *   [2.4.2 As systemd unit](#As_systemd_unit)
        *   [2.4.3 smbnetfs](#smbnetfs)
            *   [2.4.3.1 Daemon](#Daemon)
        *   [2.4.4 autofs](#autofs)
    *   [2.5 File manager configuration](#File_manager_configuration)
        *   [2.5.1 GNOME Files, Nemo, Caja, Thunar and PCManFM](#GNOME_Files.2C_Nemo.2C_Caja.2C_Thunar_and_PCManFM)
        *   [2.5.2 KDE](#KDE)
        *   [2.5.3 Other graphical environments](#Other_graphical_environments)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Discovering network shares](#Discovering_network_shares)
    *   [3.2 Remote control of Windows computer](#Remote_control_of_Windows_computer)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Failed to start Samba SMB/CIFS server](#Failed_to_start_Samba_SMB.2FCIFS_server)
    *   [4.2 Permission issues on AppArmor](#Permission_issues_on_AppArmor)
    *   [4.3 No dialect specified on mount](#No_dialect_specified_on_mount)
    *   [4.4 Unable to overwrite files, permissions errors](#Unable_to_overwrite_files.2C_permissions_errors)
    *   [4.5 Windows clients keep asking for password even if Samba shares are created with guest permissions](#Windows_clients_keep_asking_for_password_even_if_Samba_shares_are_created_with_guest_permissions)
    *   [4.6 Windows 7 connectivity problems - mount error(12): cannot allocate memory](#Windows_7_connectivity_problems_-_mount_error.2812.29:_cannot_allocate_memory)
    *   [4.7 Windows 10 1709 and up connectivity problems - "Windows cannot access" 0x80004005](#Windows_10_1709_and_up_connectivity_problems_-_.22Windows_cannot_access.22_0x80004005)
    *   [4.8 Error: Failed to retrieve printer list: NT_STATUS_UNSUCCESSFUL](#Error:_Failed_to_retrieve_printer_list:_NT_STATUS_UNSUCCESSFUL)
    *   [4.9 Sharing a folder fails](#Sharing_a_folder_fails)
    *   [4.10 "Browsing" network fails with "Failed to retrieve share list from server"](#.22Browsing.22_network_fails_with_.22Failed_to_retrieve_share_list_from_server.22)
    *   [4.11 Protocol negotiation failed: NT_STATUS_INVALID_NETWORK_RESPONSE](#Protocol_negotiation_failed:_NT_STATUS_INVALID_NETWORK_RESPONSE)
    *   [4.12 Connection to SERVER failed: (Error NT_STATUS_UNSUCCESSFUL)](#Connection_to_SERVER_failed:_.28Error_NT_STATUS_UNSUCCESSFUL.29)
    *   [4.13 Connection to SERVER failed: (Error NT_STATUS_CONNECTION_REFUSED)](#Connection_to_SERVER_failed:_.28Error_NT_STATUS_CONNECTION_REFUSED.29)
    *   [4.14 Protocol negotiation failed: NT_STATUS_CONNECTION_RESET](#Protocol_negotiation_failed:_NT_STATUS_CONNECTION_RESET)
    *   [4.15 Password Error when correct credentials are given (error 1326)](#Password_Error_when_correct_credentials_are_given_.28error_1326.29)
    *   [4.16 Mapping reserved Windows characters](#Mapping_reserved_Windows_characters)
    *   [4.17 Folder shared inside graphical environment is not available to guests](#Folder_shared_inside_graphical_environment_is_not_available_to_guests)
        *   [4.17.1 Verify correct samba configuration](#Verify_correct_samba_configuration)
        *   [4.17.2 Verify correct shared folder creation](#Verify_correct_shared_folder_creation)
        *   [4.17.3 Verify folder access by guest](#Verify_folder_access_by_guest)
    *   [4.18 Mount error: Host is down](#Mount_error:_Host_is_down)
*   [5 See also](#See_also)

## Server

### Installation

[Install](/index.php/Install "Install") the [samba](https://www.archlinux.org/packages/?name=samba) package.

Samba is configured in the `/etc/samba/smb.conf` configuration file, which is extensively documented in [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5).

Because the [samba](https://www.archlinux.org/packages/?name=samba) package does not provide this file, one needs to create it **before** starting *smbd*.

A documented example as in `smb.conf.default` from the [Samba git repository](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD) may be used to setup `/etc/samba/smb.conf`.

**Note:**

*   The default configuration sets `log file` to a non-writable location, which will cause errors - apply one of the following workarounds:
    *   Change the log file location to a writable path: `log file = /var/log/samba/%m.log`
    *   Change logging to a non-file backend solution: `logging = syslog` with `syslog only = yes`, or use `logging = systemd`
*   If required; the `workgroup` specified in the `[global]` section has to match the Windows workgroup (default `WORKGROUP`).

**Tip:** Whenever you modify the `smb.conf` file, run the [testparm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/testparm.1) command to check for syntactic errors.

#### Configure Firewall

If you are using a [firewall](/index.php/Firewall "Firewall"), do not forget to open required ports (usually 137-139 + 445). For a complete list, see [Samba port usage](https://www.samba.org/~tpot/articles/firewall.html).

### Usage

#### User Management

##### Adding a user

Samba requires a Linux user account - you may use an existing user account or create a [new one](/index.php/Users_and_groups#User_management "Users and groups").

**Note:** The [user](/index.php/User "User")/[group](/index.php/Group "Group") *nobody* should already exists on the system, is used as default `guest account` and may be used for shares containing `guest ok = yes`, thus preventing the need of user login on that share.

Although the user name is shared with Linux system, Samba uses a password separate from that of the Linux user accounts. Replace `samba_user` with the chosen Samba user account:

```
# smbpasswd -a *samba_user*

```

Depending on the [server role](https://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html#SERVERROLE), existing [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") may need to be altered for the Samba user account.

If you want the new user only to be allowed to remotely access the file server shares through Samba, you can restrict other login options：

*   disabling shell - `usermod --shell /usr/bin/nologin --lock *username*`
*   disabling SSH logons - edit `/etc/ssh/sshd_conf`, change option `AllowUsers`

Also see [Security](/index.php/Security "Security") for hardening your system.

##### Listing users

Samba users can be listed using the [pdbedit(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdbedit.8) command:

```
# pdbedit -L -v

```

##### Changing user password

To change an user password, use `smbpasswd`:

```
# smbpasswd *samba_user*

```

#### Creating a share

**Note:** To allow the usage of *guests* on public shares, one may need to [append](/index.php/Append "Append") `map to guest = Bad User` in the `[global]` section of `/etc/samba/smb.conf`. A different `guest account` may be used instead of the default provided `nobody`.

Make sure shares have been proper defined as can be seen in the *Share Definitions* section of [smb.conf.default](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD).

#### Starting services

To provide basic file sharing through SMB [start/enable](/index.php/Start/enable "Start/enable") `smb.service` and/or `nmb.service` services. See the [smbd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smbd.8) and [nmbd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmbd.8) man pages for details, as the `nmb.service` service may not always be required.

**Note:** In [samba](https://www.archlinux.org/packages/?name=samba) 4.8.0-1, the units were renamed from `smbd.service` and `nmbd.service` to `smb.service` and `nmb.service`.

### Advanced Configuration

#### Enable usershares

**Note:** This is an optional feature. Skip this section if you do not need it.

"Usershares" is a feature that gives non-root users the capability to add, modify, and delete their own share definitions.

This creates the usershares directory in `/var/lib/samba`:

```
# mkdir -p /var/lib/samba/usershares

```

This creates the group sambashare:

```
# groupadd -r sambashare

```

This changes the owner of the directory to root and the group to sambashare:

```
# chown root:sambashare /var/lib/samba/usershares

```

This changes the permissions of the usershares directory so that users in the group sambashare can read, write and execute files:

```
# chmod 1770 /var/lib/samba/usershares

```

Set the following parameters in the `smb.conf` configuration file:

 `/etc/samba/smb.conf` 
```
[global]
  usershare path = /var/lib/samba/usershares
  usershare max shares = 100
  usershare allow guests = yes
  usershare owner only = yes
  ...
```

Add your user to the *sambashare* group. Replace `*your_username*` with the name of your user:

```
# gpasswd sambashare -a *your_username*

```

[Restart](/index.php/Restart "Restart") `smb.service` and `nmb.service` services.

Log out and log back in. You should now be able to configure your samba share using GUI. For example, in [Thunar](/index.php/Thunar "Thunar") you can right click on any directory and share it on the network. If you want to share paths inside your home directory you must make it listable for the group others.

#### Set and forcing permissions

Permissions may be applied to both the server and shares:

 `/etc/samba/smb.conf` 
```
[global]
  ;inherit owner = unix only ; Inherit ownership of the parent directory for new files and directories
  ;inherit permissions = yes ; Inherit permissions of the parent directory for new files and directories
  create mask = 0664
  directory mask = 2755
  force create mode = 0644
  force directory mode = 2755
  ...

[media]
  comment = Media share accessible by *greg* and *pcusers*
  path = */path/to/media*
  valid users = *greg @pcusers*
  force group = *+pcusers*
  public = no
  writable = yes
  create mask = 0664
  directory mask = 2775
  force create mode = 0664
  force directory mode = 2775

[public]
  comment = Public share where *archie* has write access
  path = */path/to/public*
  public = yes
  read only = yes
  write list = *archie*
  printable = no

[guests]
  comment = Allow all users to read/write
  path = */path/to/guests*
  public = yes
  only guest = yes
  writable = yes
  printable = no
```

See [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5) for a full overview of possible permission flags and settings.

#### Restrict protocols for better security

By default Samba allows the usage of (possible) insecure and out-of-dated protocols for compatible reasons.

[Append](/index.php/Append "Append") `server min protocol` and `server max protocol` in `/etc/samba/smb.conf` to force usage of a minimum and maximum protocol:

 `/etc/samba/smb.conf` 
```
[global]
  server min protocol = NT1
  ; server max protocol = SMB3
```

**Note:** See `server max protocol` in [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5) for an overview of supported protocols.

**Tip:** Use `server min protocol = SMB3` when clients should only connect using the latest SMB3 protocol, e.g. on clients running Windows 8 and later.

[Clients](#Manual_mounting) using `mount.cifs` should specify the correct `vers=*`, e.g.:

```
# mount -t cifs //*SERVER*/*sharename* /mnt/*mountpoint* -o username=*username*,password=*password*,iocharset=*utf8*,vers=*3.1.1*

```

See [mount.cifs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.cifs.8) for more information.

#### Use native SMB transport encryption

Native SMB transport encryption is available in SMB version 3.0 or newer. It is only offered by Samba if `server max protocol` is set to `SMB3` or newer. Clients supporting this type of encryption include Windows 8 and newer, Windows server 2012 and newer, and smbclient of Samba 4.1 and newer.

To use native SMB transport encryption by default, set the `smb encrypt` parameter globally and/or by share. Possible values are *off* (or disabled), *enabled* (or *auto* or *if_required*), *desired*, and *required* (or *mandatory*). A special value is *default* which is the implicit default setting of *enabled*:

 `/etc/samba/smb.conf` 
```
[global]
  smb encrypt = required
  ...

[media]
  smb encrypt = desired
  ...
```

See [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5) for more information.

**Tip:** When [mounting](#Manual_mounting) a share, specify the `seal` mount option to force usage of encryption.

#### Disable printer sharing

By default Samba shares printers configured using [CUPS](/index.php/CUPS "CUPS").

If you do not want printers to be shared, use the following settings:

 `/etc/samba/smb.conf` 
```
[global]
  load printers = no
  printing = bsd
  printcap name = /dev/null
  disable spoolss = yes
  show add printer wizard = no
```

#### Block certain file extensions on Samba share

**Note:** Setting this parameter will affect the performance of Samba, as it will be forced to check all files and directories for a match as they are scanned.

Samba offers an option to block files with certain patterns, like file extensions. This option can be used to prevent dissemination of viruses or to dissuade users from wasting space with certain files. More information about this option can be found in [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5).

 `/etc/samba/smb.conf` 
```
...
[myshare]
  comment = Private
  path = /mnt/data
  read only = no
  veto files = /*.exe/*.com/*.dll/*.bat/*.vbs/*.tmp/*.mp3/*.avi/*.mp4/*.wmv/*.wma/
```

#### Improve throughput

**Warning:** Beware this may lead to corruption/connection issues and potentially cripple your TCP/IP stack.

The default settings should be sufficient for most users. However setting the 'socket options' correct can improve performance, but getting them wrong can degrade it by just as much. Test the effect before making any large changes.

Read the [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5) man page before applying any of the options listed below.

The following settings should be [append](/index.php/Append "Append") to the `[global]` section of `/etc/samba/smb.conf`.

SMB3 multi-channel may improve performance, however it may result in data corruption under some race conditions. Future releases may improve this situation:

```
server multi channel support = yes

```

Setting a deadtime is useful to stop a server's resources being exhausted by a large number of inactive connections:

```
deadtime = 30

```

The usage of sendfile may make more efficient use of the system CPU's and cause Samba to be faster:

```
use sendfile = yes

```

The write cache allows Samba to batch client writes into a more efficient write size for [RAID](/index.php/RAID "RAID") disks (i.e. writes may be tuned to be the RAID stripe size) and can improve performance on systems where the disk subsystem is a bottleneck but there is free memory for userspace programs:

```
write cache size = 262144

```

Setting min receivefile size allows zero-copy writes directly from network socket buffers into the filesystem buffer cache (if available). It may improve performance but user testing is recommended:

```
min receivefile size = 16384

```

Reading/writing files asynchronously may improve performance instead of using synchronously writes:

```
aio read size = 1
aio write size = 1

```

Increasing the receive/send buffers size and socket optimize flags might be useful to improve throughput. It is recommended to test each flag separately as it may cause issues on some networks:

```
socket options = IPTOS_LOWDELAY TCP_NODELAY IPTOS_THROUGHPUT SO_RCVBUF=131072 SO_SNDBUF=131072

```

**Note:** Network-interface adjustments may be needed for some options to work, see [Sysctl#Networking](/index.php/Sysctl#Networking "Sysctl").

## Client

Install [smbclient](https://www.archlinux.org/packages/?name=smbclient) for an `ftp`-like command line interface. See [smbclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smbclient.1) for commonly used commands.

For a lightweight alternative (without support for listing public shares, etc.), [install](/index.php/Install "Install") [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) that provides `/usr/bin/mount.cifs`.

Depending on the [desktop environment](/index.php/Desktop_environment "Desktop environment"), GUI methods may be available. See [#File manager configuration](#File_manager_configuration) for use with a file manager.

**Note:**

*   [smbclient](https://www.archlinux.org/packages/?name=smbclient) requires a `/etc/samba/smb.conf` file (see [#Installation](#Installation)), which you can create as an empty file using the `touch` utility.
*   After installing [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) or [smbclient](https://www.archlinux.org/packages/?name=smbclient), load the `cifs` [kernel module](/index.php/Kernel_module "Kernel module") or reboot to prevent mount fails.

### List public shares

The following command lists public shares on a server:

```
$ smbclient -L *hostname* -U%

```

Alternatively, running *smbtree* will show a tree diagram of all the shares. This is not advisable on a network with a lot of computers, but can be helpful for diagnosing if you have the correct sharename.

```
$ smbtree -b -N

```

Where the options are `-b` (`--broadcast`) to use broadcast instead of using the master browser and `-N` (`-no-pass`) to not ask for a password.

### NetBIOS/WINS host names

You may need to [start](/index.php/Start "Start") `winbind.service` in order to resolve host names with e.g., `mount.cifs`

The [smbclient](https://www.archlinux.org/packages/?name=smbclient) package provides a driver to resolve host names using WINS. To enable it, add `wins` to the “hosts” line in `/etc/nsswitch.conf`.

#### Disable NetBIOS/WINS support

When not using NetBIOS/WINS host name resolution, it may be preferred to disable this protocol:

 `/etc/samba/smb.conf` 
```
[global]
  disable netbios = yes
  dns proxy = no
```

Finally [disable](/index.php/Disable "Disable")/[stop](/index.php/Stop "Stop") `winbind.service`.

### Manual mounting

Create a mount point for the share:

```
# mkdir /mnt/*mountpoint*

```

Mount the share using `mount.cifs` as `type`. Not all the options listed below are needed or desirable:

```
# mount -t cifs //*SERVER*/*sharename* /mnt/*mountpoint* -o username=*username*,password=*password*,workgroup=*workgroup*,iocharset=*utf8*,uid=*username*,gid=*group*

```

The options `uid` and `gid` corresponds to the local (e.g. client) [user](/index.php/User "User")/[group](/index.php/Group "Group") to have read/write access on the given path.

**Note:**

*   If the `uid` and `gid` being used does not match the user of the server, the `forceuid` and `forcegid` options may be helpful. However note permissions assigned to a file when `forceuid` or `forcegid` are in effect may not reflect the the real (server) permissions. See the *File And Directory Ownership And Permissions* section in [mount.cifs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.cifs.8#FILE_AND_DIRECTORY_OWNERSHIP_AND_PERMISSIONS) for more information.
*   To allow users to mount it as long as the mount point resides in a directory controllable by the user; i.e. the user's home, append the `users` mount option. The option is user**s** (plural). For other filesystem types handled by mount, this option is usually *user*; sans the "**s**".
*   To mount a Windows share without authentification, use `"username=*"`.

**Warning:** Using `uid` and/or `gid` as mount options may cause I/O errors, it is recommended to set/check correct [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") instead.

*SERVER*

	The server name.

*sharename*

	The shared directory.

*mountpoint*

	The local directory where the share will be mounted.

`-o [options]`

	See [mount.cifs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.cifs.8) for more information.

**Note:**

*   Abstain from using a trailing `/`. `//*SERVER*/*sharename***/**` will not work.
*   If your mount does not work stable, stutters or freezes, try to enable different SMB protocol version with `vers=` option. For example, `vers=2.0` for Windows Vista mount.
*   If having timeouts on a mounted network share with cifs on a shutdown, see [WPA supplicant#Problem with mounted network shares (cifs) and shutdown](/index.php/WPA_supplicant#Problem_with_mounted_network_shares_.28cifs.29_and_shutdown "WPA supplicant").

#### Storing share passwords

Storing passwords in a world readable file is not recommended. A safer method is to use a credentials file instead, e.g. inside `/etc/samba/credentials`:

 `/etc/samba/credentials/share` 
```
username=*myuser*
password=*mypass*
```

Replace `username=myuser,password=mypass` with `credentials=/etc/samba/credentials/share`.

The credential file should explicitly readable/writeable to root:

```
# chown root:root /etc/samba/credentials
# chmod 700 /etc/samba/credentials
# chmod 600 /etc/samba/credentials/share

```

### Automatic mounting

**Note:** You may need to [enable](/index.php/Enable "Enable") `systemd-networkd-wait-online.service` or `NetworkManager-wait-online.service` (depending on your setup) to proper enable booting on start-up.

#### As mount entry

This is an simple example of a `cifs` [mount entry](/index.php/Fstab "Fstab") that requires authentication:

 `/etc/fstab`  `//*SERVER*/*sharename* /mnt/*mountpoint* cifs username=*myuser*,password=*mypass* 0 0` 
**Note:** Space in sharename should be replaced by `\040` (ASCII code for space in octal). For example, `//*SERVER*/share name` on the command line should be `//*SERVER*/share\040name` in `/etc/fstab`.

**Tip:** Use `x-systemd.automount` if you want them to be mounted only upon access. See [Fstab#Remote filesystem](/index.php/Fstab#Remote_filesystem "Fstab") for details.

#### As systemd unit

Create a new `.mount` file inside `/etc/systemd/system`, e.g. `mnt-myshare.mount`.

**Note:** Make sure the filename corresponds to the mountpoint you want to use. E.g. the unit name `mnt-myshare.mount` can only be used if are going to mount the share under `/mnt/myshare`. Otherwise the following error might occur: `systemd[1]: mnt-myshare.mount: Where= setting does not match unit name. Refusing.`.

`Requires=` replace (if needed) with your [Network configuration](/index.php/Category:Network_configuration "Category:Network configuration").

`What=` path to share

`Where=` path to mount the share

`Options=` share mounting options

**Note:** If you want to use a hostname for the server you want to share (instead of an IP address), add `systemd-resolved.service` to `After` and `Wants`. This might avoid mount errors at boot time that do not arise when testing the unit.
 `/etc/systemd/system/mnt-myshare.mount` 
```
[Unit]
Description=Mount Share at boot
Requires=systemd-networkd.service
After=network-online.target
Wants=network-online.target

[Mount]
What=//server/share
Where=/mnt/myshare
Options=credentials=/etc/samba/creds/myshare,iocharset=utf8,rw,x-systemd.automount
Type=cifs
TimeoutSec=30

[Install]
WantedBy=multi-user.target
```

To use `mnt-myshare.mount`, [start](/index.php/Start "Start") the unit and [enable](/index.php/Enable "Enable") it to run on system boot.

#### smbnetfs

**Note:** smbnetfs needs an intact Samba server setup. See above on how to do that.

First, check if you can see all the shares you are interested in mounting:

```
$ smbtree -U *remote_user*

```

If that does not work, find and modify the following line in `/etc/samba/smb.conf` accordingly:

```
domain master = auto

```

Now [restart](/index.php/Restart "Restart") `smb.service` and `nmb.service`.

If everything works as expected, [install](/index.php/Pacman#Installing_specific_packages "Pacman") [smbnetfs](https://www.archlinux.org/packages/?name=smbnetfs) from the official repositories.

Then, add the following line to `/etc/fuse.conf`:

```
user_allow_other

```

Now copy the directory `/etc/smbnetfs/.smb` to your home directory:

```
$ cp -a /etc/smbnetfs/.smb ~

```

Then create a link to `smb.conf`:

```
$ ln -sf /etc/samba/smb.conf ~/.smb/smb.conf

```

If a username and a password are required to access some of the shared folders, edit `~/.smb/smbnetfs.auth` to include one or more entries like this:

 `~/.smb/smbnetfs.auth` 
```
auth			"hostname" "username" "password"

```

It is also possible to add entries for specific hosts to be mounted by smbnetfs, if necessary. More details can be found in `~/.smb/smbnetfs.conf`.

If you are using the [Dolphin](/index.php/Dolphin "Dolphin") or [GNOME Files](/index.php/GNOME_Files "GNOME Files"), you may want to add the following to `~/.smb/smbnetfs.conf` to avoid "Disk full" errors as smbnetfs by default will report 0 bytes of free space:

 `~/.smb/smbnetfs.conf` 
```
free_space_size 1073741824

```

When you are done with the configuration, you need to run

```
$ chmod 600 ~/.smb/smbnetfs.*

```

Otherwise, smbnetfs complains about 'insecure config file permissions'.

Finally, to mount your Samba network neighbourhood to a directory of your choice, call

```
$ smbnetfs *mount_point*

```

##### Daemon

The Arch Linux package also maintains an additional system-wide operation mode for smbnetfs. To enable it, you need to make the said modifications in the directoy `/etc/smbnetfs/.smb`.

Then, you can start and/or enable the `smbnetfs` [daemon](/index.php/Daemon "Daemon") as usual. The system-wide mount point is at `/mnt/smbnet/`.

#### autofs

See [Autofs](/index.php/Autofs "Autofs") for information on the kernel-based automounter for Linux.

### File manager configuration

#### GNOME Files, Nemo, Caja, Thunar and PCManFM

In order to access samba shares through GNOME Files, Nemo, Caja, Thunar or PCManFM, install the [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

Press `Ctrl+l` and enter `smb://*servername*/*share*` in the location bar to access your share.

The mounted share is likely to be present at `/run/user/*your_UID*/gvfs` or `~/.gvfs` in the filesystem.

#### KDE

KDE has the ability to browse Samba shares built in. To use a GUI in the KDE System Settings, you will need to install the [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) package.

If you get a "Time Out" Error when navigating with Dolphin, you should uncomment and edit the following line in smb.conf: `name resolve order = lmhosts bcast host wins` 

as shown in this [page](http://ubuntuforums.org/showthread.php?t=1605499).

#### Other graphical environments

There are a number of useful programs, but they may need to have packages created for them. This can be done with the Arch package build system. The good thing about these others is that they do not require a particular environment to be installed to support them, and so they bring along less baggage.

*   [pyneighborhood](https://www.archlinux.org/packages/?name=pyneighborhood) is available in the official repositories.
*   LinNeighborhood, RUmba, xffm-samba plugin for Xffm are not available in the official repositories or the AUR. As they are not officially (or even unofficially supported), they may be obsolete and may not work at all.

## Tips and tricks

### Discovering network shares

If nothing is known about other systems on the local network, and automated tools such as [smbnetfs](#smbnetfs) are not available, the following methods allow one to manually probe for Samba shares.

1\. First, [install](/index.php/Install "Install") the [nmap](https://www.archlinux.org/packages/?name=nmap) and [smbclient](https://www.archlinux.org/packages/?name=smbclient) packages.

2\. `nmap` checks which ports are open:

```
# nmap -p 139 -sT "192.168.1.*"

```

In this case, a scan on the 192.168.1.* IP address range and port 139 has been performed, resulting in:

 `$ nmap -sT "192.168.1.*"` 
```
Starting nmap 3.78 ( [http://www.insecure.org/nmap/](http://www.insecure.org/nmap/) ) at 2005-02-15 11:45 PHT
Interesting ports on 192.168.1.1:
(The 1661 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
**139/tcp  open  netbios-ssn**
5000/tcp open  UPnP

Interesting ports on 192.168.1.5:
(The 1662 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
6000/tcp open  X11

Nmap run completed -- 256 IP addresses (2 hosts up) scanned in 7.255 seconds

```

The first result is another system; the second happens to be the client from where this scan was performed.

3\. Now that systems with port 139 open are revealed, use [nmblookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmblookup.1) to check for NetBIOS names:

 `$ nmblookup -A 192.168.1.1` 
```
Looking up status of 192.168.1.1
        PUTER           <00> -         B <ACTIVE>
        HOMENET         <00> - <GROUP> B <ACTIVE>
        PUTER           <03> -         B <ACTIVE>
        **PUTER           <20> -         B <ACTIVE>**
        HOMENET         <1e> - <GROUP> B <ACTIVE>
        USERNAME        <03> -         B <ACTIVE>
        HOMENET         <1d> -         B <ACTIVE>
        MSBROWSE        <01> - <GROUP> B <ACTIVE>

```

Regardless of the output, look for **<20>**, which shows the host with open services.

4\. Use `smbclient` to list which services are shared on *PUTER*. If prompted for a password, pressing enter should still display the list:

 `$ smbclient -L \\PUTER` 
```
Sharename       Type      Comment

* * *

       ----      -------
MY_MUSIC        Disk
SHAREDDOCS      Disk
PRINTER$        Disk
PRINTER         Printer
IPC$            IPC       Remote Inter Process Communication

Server               Comment

* * *

            -------
PUTER

Workgroup            Master

* * *

            -------
HOMENET               PUTER
```

### Remote control of Windows computer

Samba offers a set of tools for communication with Windows. These can be handy if access to a Windows computer through remote desktop is not an option, as shown by some examples.

Send shutdown command with a comment:

```
$ net rpc shutdown -C "comment" -I IPADDRESS -U USERNAME%PASSWORD

```

A forced shutdown instead can be invoked by changing -C with comment to a single -f. For a restart, only add -r, followed by a -C or -f.

Stop and start services:

```
$ net rpc service stop SERVICENAME -I IPADDRESS -U USERNAME%PASSWORD

```

To see all possible net rpc command:

```
$ net rpc

```

## Troubleshooting

### Failed to start Samba SMB/CIFS server

Possible solutions:

*   Check `smb.conf` on syntactic errors with [testparm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/testparm.1).
*   Set correct permissions for `/var/cache/samba/` and [restart](/index.php/Restart "Restart") `smb.service`:

```
# chmod 0755 /var/cache/samba/msg

```

### Permission issues on AppArmor

The following adjustments should be applied when using Samba together with [AppArmor](/index.php/AppArmor "AppArmor"):

*   The pid file and log file paths used in the [samba](https://www.archlinux.org/packages/?name=samba) package differ from the ones used in the AppArmor profiles [[1]](https://gitlab.com/apparmor/apparmor/merge_requests/210). Change the `pid directory` to `var/run/samba/` and use a non-file `logging` backend:

 `/etc/samba/smb.conf` 
```
[global]
pid directory = /var/run/samba/
logging = systemd ; or syslog with syslog only
```

*   If using a [share path](#Creating_a_share) located outside of a home-directory whitelist it in `/etc/apparmor.d/local/usr.sbin.smbd`. E.g.:

 `/etc/apparmor.d/local/usr.sbin.smbd` 
```
/data/** rw,

```

### No dialect specified on mount

The client is using an unsupported SMB/CIFS version that is required by the server.

See [#Restrict protocols for better security](#Restrict_protocols_for_better_security) for more information.

### Unable to overwrite files, permissions errors

Possible solutions:

*   Append the mount option `nodfs` to the `/etc/fstab` [entry](#As_mount_entry).
*   Add `msdfs root = no` to the `[global]` section of the server's `/etc/samba/smb.conf`.

### Windows clients keep asking for password even if Samba shares are created with guest permissions

Set `map to guest` inside the `global` section of `/etc/samba/smb.conf`:

```
map to guest = Bad User

```

### Windows 7 connectivity problems - mount error(12): cannot allocate memory

A known Windows 7 bug that causes "mount error(12): cannot allocate memory" on an otherwise perfect cifs share on the Linux end can be fixed by setting a few registry keys on the Windows box as follows:

*   `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\LargeSystemCache` (set to `1`)
*   `HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters\Size` (set to `3`)

Alternatively, start Command Prompt in Admin Mode and execute the following:

```
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" /v "LargeSystemCache" /t REG_DWORD /d 1 /f
reg add "HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" /v "Size" /t REG_DWORD /d 3 /f

```

Do one of the following for the settings to take effect:

*   Restart Windows
*   Restart the Server service via services.msc
*   From the Command Prompt run: 'net stop lanmanserver' and 'net start lanmanserver' - The server may automatically restart after stopping it.

**Note:** Googling will reveal another tweak recommending users to add a key modifying the "IRPStackSize" size. This is incorrect for fixing this issue under Windows 7\. Do not attempt it.

[Original article](http://alan.lamielle.net/2009/09/03/windows-7-nonpaged-pool-srv-error-2017).

### Windows 10 1709 and up connectivity problems - "Windows cannot access" 0x80004005

This error affects some machines running Windows 10 version 1709 and later. It is not related to SMB1 being disabled in this version but to the fact that Microsoft disabled insecure logons for guests on this version for some, but not others.

To fix, open Group Policy Editor (`gpedit.msc`). Navigate to *Computer configuration\administrative templates
etwork\Lanman Workstation > Enable insecure guest logons* and enable it. Alternatively,change the following value in the registry:

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
"AllowInsecureGuestAuth"=dword:1

```

### Error: Failed to retrieve printer list: NT_STATUS_UNSUCCESSFUL

If you are a home user and using samba purely for file sharing from a server or NAS, you are probably not interested in sharing printers through it. If so, you can prevent this error from occurring by adding the following lines to your `/etc/samba/smb.conf`:

 `/etc/samba/smb.conf` 
```
[global]
  load printers = No
  printing = bsd
  printcap name = /dev/null
  disable spoolss = Yes
```

[Restart](/index.php/Restart "Restart") the samba service, `smb.service`, and then check your logs:

```
# cat /var/log/samba/smbd.log

```

and the error should now no longer be appearing.

### Sharing a folder fails

It means that while you are sharing a folder from *Dolphin* (file manager) and everything seems ok at first, after restarting *Dolphin* the share icon is gone from the shared folder, and also some output like this in terminal (*Konsole*) output:

```
‘net usershare’ returned error 255: net usershare: usershares are currently disabled

```

To fix it, enable usershare as described in [#Enable usershares](#Enable_usershares).

### "Browsing" network fails with "Failed to retrieve share list from server"

And you are using a firewall (iptables) because you do not trust your local (school, university, hotel) network. This may be due to the following: When the smbclient is browsing the local network it sends out a broadcast request on udp port 137\. The servers on the network then reply to your client but as the source address of this reply is different from the destination address iptables saw when sending the request for the listing out, iptables will not recognize the reply as being "ESTABLISHED" or "RELATED", and hence the packet is dropped. A possible solution is to add:

```
iptables -t raw -A OUTPUT -p udp -m udp --dport 137 -j CT --helper netbios-ns

```

to your iptables setup.

### Protocol negotiation failed: NT_STATUS_INVALID_NETWORK_RESPONSE

The client probably does not have access to shares. Make sure clients' IP address is in `hosts allow =` line in `/etc/samba/smb.conf`.

Another problem could be, that the client uses an invalid protocol version. To check this try to connect with the `smbclient` where you specify the maximum protocol version manually:

```
$ smbclient -U <user name> -L //<server name> -m <protocol version: e. g. SMB2> -W <domain name>

```

If the command was successful then create a configuration file:

 `~/.smb/smb.conf` 
```
[global]
  workgroup = <domain name>
  client max protocol = SMB2
```

### Connection to SERVER failed: (Error NT_STATUS_UNSUCCESSFUL)

You are probably passing wrong server name to `smbclient`. To find out the server name, run `hostnamectl` on the server and look at "Transient hostname" line

### Connection to SERVER failed: (Error NT_STATUS_CONNECTION_REFUSED)

Make sure that the server has started. The shared directories should exist and be accessible.

### Protocol negotiation failed: NT_STATUS_CONNECTION_RESET

Probably the server is configured not to accept protocol SMB1\. Add option `client max protocol = SMB2` in `/etc/samba/smb.conf`. Or just pass argument `-m SMB2` to `smbclient`.

### Password Error when correct credentials are given (error 1326)

[Samba 4.5](https://www.samba.org/samba/history/samba-4.5.0.html) has NTLMv1 authentication disabled by default. It is recommend to install the latest available upgrades on clients and deny access for unsupported clients.

If you still need support for very old clients without NTLMv2 support (e.g. Windows XP), it is possible force enable NTLMv1, although this is **not recommend** for security reasons:

 `/etc/samba/smb.conf` 
```
[global]
  lanman auth = yes
  ntlm auth = yes
```

If NTLMv2 clients are unable to authenticate when NTLMv1 has been enabled, create the following file on the client:

 `/home/user/.smb/smb.conf` 
```
[global]
  sec = ntlmv2
  client ntlmv2 auth = yes
```

This change also affects samba shares mounted with **mount.cifs**. If after upgrade to Samba 4.5 your mount fails, add the **sec=ntlmssp** option to your mount command, e.g.

```
mount.cifs //server/share /mnt/point -o sec=ntlmssp,...

```

See the [mount.cifs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.cifs.8) man page: **ntlmssp** - Use NTLMv2 password hashing encapsulated in Raw NTLMSSP message. The default in mainline kernel versions prior to v3.8 was **sec=ntlm**. In v3.8, the default was changed to **sec=ntlmssp**.

### Mapping reserved Windows characters

Starting with kernel 3.18, the cifs module uses the ["mapposix" option by default](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=2baa2682531ff02928e2d3904800696d9e7193db). When mounting a share using unix extensions and a default Samba configuration, files and directories containing one of the seven reserved Windows characters `: \ * < > ?` are listed but cannot be accessed.

Possible solutions are:

*   Use the undocumented `nomapposix` mount option for cifs

```
 # mount.cifs //server/share /mnt/point -o nomapposix

```

*   Configure Samba to remap `mapposix` ("SFM", Services for Mac) style characters to the correct native ones using [fruit](https://www.mankier.com/8/vfs_fruit)

 `/etc/samba/smb.conf` 
```
[global]
  vfs objects = catia fruit
  fruit:encoding = native
```

*   Manually remap forbidden characters using [catia](https://www.mankier.com/8/vfs_catia)

 `/etc/samba/smb.conf` 
```
[global]
  vfs objects = catia
  catia:mappings = 0x22:0xf022, 0x2a:0xf02a, 0x2f:0xf02f, 0x3a:0xf03a, 0x3c:0xf03c, 0x3e:0xf03e, 0x3f:0xf03f, 0x5c:0xf05c, 0x7c:0xf07c, 0x20:0xf020
```

The latter approach (using catia or fruit) has the drawback of filtering files with unprintable characters.

### Folder shared inside graphical environment is not available to guests

This section presupposes:

1.  Usershares are configured following [previous section](#Enable_usershares)
2.  A shared folder has been created as a non-root user from GUI
3.  Guests access has been set to shared folder during creation
4.  Samba service has been restarted at least once since last `/etc/samba/smb.conf` file modification

For clarification purpose only, in the following sub-sections is assumed:

*   Shared folder is located inside user home directory path (`/home/yourUser/Shared`)
*   Shared folder name is *MySharedFiles*
*   Guest access is read-only.
*   Windows users will access shared folder content without login prompt

#### Verify correct samba configuration

Run the following command from a terminal to test configuration file correctness:

```
$ testparm

```

#### Verify correct shared folder creation

Run the following commands from a terminal:

```
$ cd /var/lib/samba/usershare
$ ls

```

If everything is fine, you will notice a file named `mysharedfiles`

Read the file contents using the following command:

```
$ cat mysharedfiles

```

The terminal output should display something like this:

 `/var/lib/samba/usershare/mysharedfiles` 
```
path=/home/yourUser/Shared
comment=
usershare_acl=S-1-1-0:r
guest_ok=y
sharename=MySharedFiles
```

#### Verify folder access by guest

Run the following command from a terminal. If prompted for a password, just press Enter:

```
$ smbclient -L localhost

```

If everything is fine, MySharedFiles should be displayed under `Sharename` column

Run the following command in order to access the shared folder as guest (anonymous login)

```
$ smbclient -N //localhost/MySharedFiles

```

If everything is fine samba client prompt will be displayed:

```
smb: \>

```

From samba prompt verify guest can list directory contents:

```
smb: \> ls

```

If `NTFS_STATUS_ACCESS_DENIED` error displayed, probably there is something to be solved at directory permission level.

Run the following commands as root to set correct permissions for folders:

```
# cd /home
# chmod -R 755 /home/yourUser/Shared

```

Access shared folder again as guest to be sure guest read access error has been solved.

### Mount error: Host is down

This error might be seen when mounting shares of Synology NAS servers. Use the mount option `vers=1.0` to solve it.

## See also

*   [Official website](https://www.samba.org/)
*   [Samba: An Introduction](https://www.samba.org/samba/docs/SambaIntro.html)
*   [Samba 3.2.x HOWTO and Reference Guide](https://www.samba.org/samba/docs/Samba-HOWTO-Collection.pdf) (outdated but still most extensive documentation)
*   [Wikipedia](https://en.wikipedia.org/wiki/Samba_(software) "wikipedia:Samba (software)")
*   [Gentoo:Samba/Guide](https://wiki.gentoo.org/wiki/Samba/Guide "gentoo:Samba/Guide")
*   [Debian:SambaServerSimple](https://wiki.debian.org/SambaServerSimple "debian:SambaServerSimple")