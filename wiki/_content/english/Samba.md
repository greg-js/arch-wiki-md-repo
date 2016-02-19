**Samba** is a re-implementation of the [SMB/CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") networking protocol, it facilitates file and printer sharing among Linux and Windows systems as an alternative to [NFS](/index.php/NFS "NFS"). Some users say that Samba is easily configured and that operation is very straight-forward. However, many new users run into problems with its complexity and non-intuitive mechanism. This article provides instructions for users on how to setup Samba. It is strongly suggested that the user sticks close to the following directions.

## Contents

*   [1 Server configuration](#Server_configuration)
    *   [1.1 Creating a share](#Creating_a_share)
    *   [1.2 Starting services](#Starting_services)
    *   [1.3 Creating usershare path](#Creating_usershare_path)
    *   [1.4 Adding a user](#Adding_a_user)
    *   [1.5 Changing Samba user's password](#Changing_Samba_user.27s_password)
    *   [1.6 Required ports](#Required_ports)
    *   [1.7 Sample configuration](#Sample_configuration)
    *   [1.8 Validate configuration](#Validate_configuration)
*   [2 Client configuration](#Client_configuration)
    *   [2.1 List Public Shares](#List_Public_Shares)
    *   [2.2 Manual mounting](#Manual_mounting)
        *   [2.2.1 Add Share to /etc/fstab](#Add_Share_to_.2Fetc.2Ffstab)
            *   [2.2.1.1 Storing Share Passwords](#Storing_Share_Passwords)
            *   [2.2.1.2 systemd.automount](#systemd.automount)
    *   [2.3 WINS host names](#WINS_host_names)
    *   [2.4 Automatic mounting](#Automatic_mounting)
        *   [2.4.1 smbnetfs](#smbnetfs)
            *   [2.4.1.1 Daemon](#Daemon)
        *   [2.4.2 autofs](#autofs)
    *   [2.5 File manager configuration](#File_manager_configuration)
        *   [2.5.1 GNOME Files, Nemo, Caja, Thunar and PCManFM](#GNOME_Files.2C_Nemo.2C_Caja.2C_Thunar_and_PCManFM)
        *   [2.5.2 KDE](#KDE)
        *   [2.5.3 Other graphical environments](#Other_graphical_environments)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Block certain file extensions on Samba share](#Block_certain_file_extensions_on_Samba_share)
    *   [3.2 Discovering network shares](#Discovering_network_shares)
    *   [3.3 Remote control of Windows computer](#Remote_control_of_Windows_computer)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Failed to start Samba SMB/CIFS server](#Failed_to_start_Samba_SMB.2FCIFS_server)
    *   [4.2 Unable to overwrite files, permissions errors](#Unable_to_overwrite_files.2C_permissions_errors)
    *   [4.3 Windows clients keep asking for password even if Samba shares are created with guest permissions](#Windows_clients_keep_asking_for_password_even_if_Samba_shares_are_created_with_guest_permissions)
    *   [4.4 Windows 7 connectivity problems - mount error(12): cannot allocate memory](#Windows_7_connectivity_problems_-_mount_error.2812.29:_cannot_allocate_memory)
    *   [4.5 Trouble accessing a password-protected share from Windows](#Trouble_accessing_a_password-protected_share_from_Windows)
    *   [4.6 Getting a dialog box up takes a long time](#Getting_a_dialog_box_up_takes_a_long_time)
    *   [4.7 Error: Failed to retrieve printer list: NT_STATUS_UNSUCCESSFUL](#Error:_Failed_to_retrieve_printer_list:_NT_STATUS_UNSUCCESSFUL)
    *   [4.8 Sharing a folder fails](#Sharing_a_folder_fails)
    *   [4.9 "Browsing" network fails with "Failed to retrieve share list from server"](#.22Browsing.22_network_fails_with_.22Failed_to_retrieve_share_list_from_server.22)
    *   [4.10 You are not the owner of the folder](#You_are_not_the_owner_of_the_folder)
    *   [4.11 protocol negotiation failed: NT_STATUS_INVALID_NETWORK_RESPONSE](#protocol_negotiation_failed:_NT_STATUS_INVALID_NETWORK_RESPONSE)
    *   [4.12 Connection to SERVER failed: (Error NT_STATUS_UNSUCCESSFUL)](#Connection_to_SERVER_failed:_.28Error_NT_STATUS_UNSUCCESSFUL.29)
    *   [4.13 Connection to SERVER failed: (Error NT_STATUS_CONNECTION_REFUSED)](#Connection_to_SERVER_failed:_.28Error_NT_STATUS_CONNECTION_REFUSED.29)
*   [5 See also](#See_also)

## Server configuration

To share files with Samba, [install](/index.php/Install "Install") the [samba](https://www.archlinux.org/packages/?name=samba) package.

The Samba server is configured in `/etc/samba/smb.conf.default`. Copy the default Samba configuration file to `/etc/samba/smb.conf`:

```
# cp /etc/samba/smb.conf.default /etc/samba/smb.conf

```

Otherwise, smbd will fail to start.

### Creating a share

Edit `/etc/samba/smb.conf`, scroll down to the **Share Definitions** section. The default configuration automatically creates a share for each user's home directory. It also creates a share for printers by default. There are a number of commented sample configurations included. More information about available options for shared resources can be found in `man smb.conf`. [There](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html) is also an on-line version available.

On Windows side, be sure to change `smb.conf` to the in-use Windows Workgroup (default: `WORKGROUP`).

### Starting services

To provide basic file sharing through SMB [start/enable](/index.php/Start/enable "Start/enable") `smbd.service` and/or `nmbd.service` services. See [smbd](http://www.samba.org/samba/docs/man/manpages-3/smbd.8.html) and [nmbd](http://www.samba.org/samba/docs/man/manpages-3/nmbd.8.html) manpages for details, as the `nmbd.service` service may not always be required.

**Tip:** Instead of having the service running since boot, you can enable `smbd.socket` so the daemon is started on the first incoming connection. Do not forget to disable `smbd.service`.

### Creating usershare path

**Note:** This is an optional feature. Skip this section if you do not need it.

"Usershare" is a feature that gives non-root users the capability to add, modify, and delete their own share definitions.

This creates the usershare directory in `/var/lib/samba`:

```
# mkdir -p /var/lib/samba/usershare

```

This makes the group sambashare:

```
# groupadd -r sambashare

```

This changes the owner of the directory and group you just created to root:

```
# chown root:sambashare /var/lib/samba/usershare

```

This changes the permissions of the usershare directory so that users in the group sambashare can read, write and execute files:

```
# chmod 1770 /var/lib/samba/usershare

```

Set the following variables in `smb.conf` configuration file:

 `/etc/samba/smb.conf` 
```
...
[global]
  usershare path = /var/lib/samba/usershare
  usershare max shares = 100
  usershare allow guests = yes
  usershare owner only = yes
  ...
```

Add your user to the *sambashare* group. Replace `*your_username*` with the name of your user:

```
# gpasswd sambashare -a *your_username*

```

Restart `smbd.service` and `nmbd.service` services.

Log out and log back in. You should now be able to configure your samba share using GUI. For example, in [Thunar](/index.php/Thunar "Thunar") you can right click on any directory and share it on the network. If you want to share pathes inside your home directory you must make it listable for the group others.

### Adding a user

You may use an existing user account or create a [Linux user account](/index.php/Users_and_groups#User_management "Users and groups") as Samba user.

Samba uses a password separate from that of the Linux user accounts. Replace `samba_user` with the chosen Samba user account:

```
# pdbedit -a -u *samba_user*

```

**Note:** Depending on the [server role](https://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html#SERVERROLE), existing [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") may need to be altered for the Samba user account.

### Changing Samba user's password

To change a user's password, use `smbpasswd`:

```
# smbpasswd *samba_user*

```

### Required ports

If you are using a [firewall](/index.php/Firewall "Firewall"), do not forget to open required ports (usually 137-139 + 445). For a complete list please check [Samba port usage](https://wiki.samba.org/index.php/Samba_port_usage).

### Sample configuration

See `man smb.conf` for details and explanation of configuration options. There is also an [online version](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html) available.

 `/etc/samba/smb.conf` 
```
[global]
  deadtime = 60 ; This is useful to stop a server's resources being exhausted by a large number of inactive connections
  disable netbios = yes ; Disable netbios announcing
  dns proxy = no ; nmbd spawns a second copy of itself to do the DNS name lookup requests on 'yes'
  hosts allow = 192.168.1\. 127\. 10\. ; This parameter is a comma, space, or tab delimited set of hosts which are permitted to access a service
  invalid users = root ; This is a list of users that should not be allowed to login to this service
  security = user ; Use as standalone file server
  map to guest = Bad User ; Means user logins with an invalid password are rejected, or allow guest login and mapped into the guest account
  max connections = 100 ; Number of simultaneous connections to a service to be limited
  workgroup = WORKGROUP ; Workgroup the server will appear to be in when queried by clients

  ; Uncomment the following lines to disable printer support
  ;load printers = no
  ;printing = bsd
  ;printcap name = /dev/null
  ;disable spoolss = yes

  ; Default permissions for all shares  
  inherit owner = yes ; Take the ownership of the parent directory when creating files/folders
  create mask = 0664 ; Create file mask
  directory mask = 0775 ; Create director mask
  force create mode = 0664 ; Force create file mask
  force directory mode = 0775 ; Force create directory mask

; Private Share
[private] ; translate into: \\server\private
  comment = My Private Share ; Seen next to a share when a client queries the server
  path = /path/to/data ; Directory to which the user of the service is to be given access
  read only = no ; An inverted synonym to writeable.
  valid users = user1 user2 @group1 @group2; restrict a service to a particular set of users and/or groups

; Public Share
;[public]
; comment = My Public Share
; path = /path/to/public
; read only = yes
; guest ok = yes; No password required to connect to the service

```

Restart the `smbd` service to apply configuration changes.

**Note:** Connected clients may need to reconnect before configuration changes take effect.

### Validate configuration

The command `testparm` validates the configuration of `smb.conf`:

```
# testparm -s

```

## Client configuration

For a lightweight method (without support for listing public shares, etc.), only install [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) to provide `/usr/bin/mount.cifs`.

Install [smbclient](https://www.archlinux.org/packages/?name=smbclient) for an ftp-like command line interface. See `man smbclient` for commonly used commands.

Depending on the [desktop environment](/index.php/Desktop_environment "Desktop environment"), GUI methods may be available. See [#File manager configuration](#File_manager_configuration) for use with a file manager.

**Note:** After installing [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) or [smbclient](https://www.archlinux.org/packages/?name=smbclient), load the `cifs` [kernel module](/index.php/Kernel_module "Kernel module") or reboot to prevent mount fails.

### List Public Shares

To following command lists public shares on a server:

```
$ smbclient -L *hostname* -U%

```

### Manual mounting

Create a mount point for the share:

```
# mkdir /mnt/*mountpoint*

```

Mount the share using `mount.cifs` as `type`. Not all the options listed below are needed or desirable:

 `# mount -t cifs //*SERVER*/*sharename* /mnt/*mountpoint* -o user=*username*,password=*password*,uid=*username*,gid=*group*,workgroup=*workgroup*,ip=*serverip*,iocharset=*utf8*` 

To allow users to mount it as long as the mount point resides in a directory controllable by the user; i.e. the user's home, append the `users` mount option.

**Note:** The option is user**s** (plural). For other filesystem types handled by mount, this option is usually *user*; sans the "**s**".

**Warning:** Using `uid` and/or `gid` as mount options may cause I/O errors, it's recommended to set/check the [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") instead.

*SERVER*

	The server name.

*sharename*

	The shared directory.

*mountpoint*

	The local directory where the share will be mounted.

`-o [options]`

	See `man mount.cifs` for more information.

**Note:**

*   The output "mount error(13): Permission denied", might be due to a bug in mount.cifs. See the following bug report. [https://bugs.archlinux.org/task/43015#comment130771](https://bugs.archlinux.org/task/43015#comment130771)

Try specifying the option "sec=ntlmv2" as workaround.

*   Abstain from using a trailing `/`. `//*SERVER*/*sharename***/**` will not work.
*   If your mount does not work stable, stutters or freezes, try to enable different SMB protocol version with `vers=` option. For example, `vers=2.0` for Windows Vista mount.
*   If having timeouts on a mounted network share with cifs on a shutdown, see [WPA supplicant#Problem with mounted network shares (cifs) and shutdown (Date: 1st Oct. 2015)](/index.php/WPA_supplicant#Problem_with_mounted_network_shares_.28cifs.29_and_shutdown_.28Date:_1st_Oct._2015.29 "WPA supplicant").

#### Add Share to /etc/fstab

This is an simple example of a `cifs` [mount entry](/index.php/Fstab "Fstab") that requires authentication:

 `/etc/fstab`  `//*SERVER*/*sharename* /mnt/*mountpoint* cifs username=*myuser*,password=*mypass* 0 0` 
**Note:** Space in sharename should be replaced by `\040` (ASCII code for space in octal). For example, `//*SERVER*/share name` on the command line should be `//*SERVER*/share\040name` in `/etc/fstab`.

##### Storing Share Passwords

Storing passwords in a world readable file is not recommended. A safer method is to create a credentials file:

 `/path/to/credentials/share` 
```
username=*myuser*
password=*mypass*
```

Replace `username=myuser,password=mypass` with `credentials=/path/to/credentials/share`.

The credential file should explicitly readable/writeable to root:

```
# chmod 600 /path/to/credentials/share

```

##### systemd.automount

To speed up the service on boot, add the `x-systemd.automount` option to the entry:

 `/etc/fstab`  `//*SERVER*/*SHARENAME* /mnt/*mountpoint* cifs credentials=*/path/to/smbcredentials/share*,x-systemd.automount 0 0` 

### WINS host names

The [smbclient](https://www.archlinux.org/packages/?name=smbclient) package provides a driver to resolve host names using WINS. To enable it, add “wins” to the “hosts” line in /etc/nsswitch.conf.

### Automatic mounting

There are several ways to easily browse shared resources:

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

Now [restart](/index.php/Restart "Restart") `smbd.service` and `nmbd.service`.

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

If you are using the Dolphin or Nautilus file managers, you may want to add the following to `~/.smb/smbnetfs.conf` to avoid "Disk full" errors as smbnetfs by default will report 0 bytes of free space:

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

KDE, has the ability to browse Samba shares built in. Therefore do not need any additional packages. However, for a GUI in the KDE System Settings, install the [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) package from the official repositories.

If when navigating with Dolphin you get a "Time Out" Error, you should uncomment and edit this line in smb.conf: `name resolve order = lmhosts bcast host wins` 

as shown in this [page](http://ubuntuforums.org/showthread.php?t=1605499).

#### Other graphical environments

There are a number of useful programs, but they may need to have packages created for them. This can be done with the Arch package build system. The good thing about these others is that they do not require a particular environment to be installed to support them, and so they bring along less baggage.

*   [pyneighborhood](https://www.archlinux.org/packages/?name=pyneighborhood) is available in the official repositories.
*   LinNeighborhood, RUmba, xffm-samba plugin for Xffm are not available in the official repositories or the AUR. As they are not officially (or even unofficially supported), they may be obsolete and may not work at all.

## Tips and tricks

### Block certain file extensions on Samba share

**Note:** Setting this parameter will affect the performance of Samba, as it will be forced to check all files and directories for a match as they are scanned.

Samba offers an option to block files with certain patterns, like file extensions. This option can be used to prevent dissemination of viruses or to dissuade users from wasting space with certain files. More information about this option can be found in `man smb.conf`.

 `/etc/samba/smb.conf` 
```
...
[myshare]
  comment = Private
  path = /mnt/data
  read only = no
  veto files = /*.exe/*.com/*.dll/*.bat/*.vbs/*.tmp/*.mp3/*.avi/*.mp4/*.wmv/*.wma/
```

### Discovering network shares

If nothing is known about other systems on the local network, and automated tools such as [smbnetfs](#smbnetfs) are not available, the following methods allow one to manually probe for Samba shares.

1\. First, install [nmap](https://www.archlinux.org/packages/?name=nmap) and [smbclient](https://www.archlinux.org/packages/?name=smbclient) using [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S nmap smbclient

```

2\. `nmap` checks which ports are open:

```
# nmap -p 139 -sT 192.168.1.*

```

In this case, a scan on the 192.168.1.* IP address range and port 139 has been performed, resulting in:

```
$ nmap -sT 192.168.1.*

```

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

3\. Now that systems with port 139 open are revealed, use `nmblookup` to check for NetBIOS names:

```
$ nmblookup -A 192.168.1.1

```

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

```
$ smbclient -L \\PUTER

```

```
Sharename       Type      Comment
---------       ----      -------
MY_MUSIC        Disk
SHAREDDOCS      Disk
PRINTER$        Disk
PRINTER         Printer
IPC$            IPC       Remote Inter Process Communication

Server               Comment
---------            -------
PUTER

Workgroup            Master
---------            -------
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

Check if the permissions are set correctly for `/var/cache/samba/` and restart the `smbd.service` or `smbd.socket`:

```
# chmod 0755 /var/cache/samba/msg

```

### Unable to overwrite files, permissions errors

Possible solutions:

*   Append the mount option `nodfs` to the `/etc/fstab` [entry](#Add_Share_to_.2Fetc.2Ffstab).
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

### Trouble accessing a password-protected share from Windows

**Note:** This needs to be added to the **local smb.conf**, not to the server's smb.conf

For trouble accessing a password protected share from Windows, try adding this to `/etc/samba/smb.conf`:[[1]](http://blogs.computerworld.com/networking_nightmare_ii_adding_linux)

```
[global]
# lanman fix
client lanman auth = yes
client ntlmv2 auth = no

```

### Getting a dialog box up takes a long time

I had a problem that it took ~30 seconds to get a password dialog box up when trying to connect from both Windows XP/Windows 7\. Analyzing the error.log on the server I saw:

```
[2009/11/11 06:20:12,  0] printing/print_cups.c:cups_connect(103)
Unable to connect to CUPS server localhost:631 - Interrupted system call

```

This keeps samba from asking cups and also from complaining about /etc/printcap missing:

```
printing = bsd
printcap name = /dev/null

```

### Error: Failed to retrieve printer list: NT_STATUS_UNSUCCESSFUL

If you are a home user and using samba purely for file sharing from a server or NAS, you are probably not interested in sharing printers through it. If so, you can prevent this error from occurring by adding the following lines to your `/etc/samba/smb.conf`:

```
load printers = No
printing = bsd
printcap name = /dev/null
disable spoolss = Yes

```

[Restart](/index.php/Restart "Restart") the samba service, `smbd.service`, and then check your logs:

 `cat /var/log/samba/smbd.log` 

and the error should now no longer be appearing.

### Sharing a folder fails

It means that while you are sharing a folder from *Dolphin* (file manager) and everything seems ok at first, after restarting *Dolphin* the share icon is gone from the shared folder, and also some output like this in terminal (*Konsole*) output:

```
‘net usershare’ returned error 255: net usershare: usershares are currently disabled

```

To fix it, enable usershare as described in [#Creating usershare path](#Creating_usershare_path).

### "Browsing" network fails with "Failed to retrieve share list from server"

And you are using a firewall (iptables) because you do not trust your local (school, university, hotel) local network. This may be due to the following: When the smbclient is browsing the local network it sends out a broadcast request on udp port 137\. The servers on the network then reply to your client but as the source address of this reply is different from the destination address iptables saw when sending the request for the listing out, iptables will not recognize the reply as being "ESTABLISHED" or "RELATED", and hence the packet is dropped. A possible solution is to add:
```
iptables -t raw -A OUTPUT -p udp -m udp --dport 137 -j CT --helper netbios-ns

```

to your iptables setup.

### You are not the owner of the folder

Simply try to reboot the system.

### protocol negotiation failed: NT_STATUS_INVALID_NETWORK_RESPONSE

The client probably does not have access to shares. Make sure clients' IP address is in `hosts allow =` line in `/etc/samba/smb.conf`.

### Connection to SERVER failed: (Error NT_STATUS_UNSUCCESSFUL)

You are probably passing wrong server name to `smbclient`. To find out the server name, run `hostnamectl` on the server and look at "Transient hostname" line

### Connection to SERVER failed: (Error NT_STATUS_CONNECTION_REFUSED)

Make sure that the server has started. The shared directories should exist and be accessible.

## See also

*   [Samba: An Introduction](http://www.samba.org/samba/docs/SambaIntro.html)
*   [Official Samba site](http://www.samba.org/)