相关文章

*   [NFS](/index.php/NFS "NFS")
*   [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller")
*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")

**Samba** 是 [SMB/CIFS](https://en.wikipedia.org/wiki/Server_Message_Block 的补充使得在 Linux 和 Windows 系统中进行文件共享、打印机共享更容易实现。一些用户说Samba配置简单，操作直观。然而，许多新用户会因为它的复杂性和非直观的机制而遇到问题。强烈建议新用户仔细按照下面的指导。

## Contents

*   [1 服务器配置](#服务器配置)
    *   [1.1 建立共享](#建立共享)
    *   [1.2 启动服务](#启动服务)
    *   [1.3 建立 Usershare 路径](#建立_Usershare_路径)
    *   [1.4 添加用户](#添加用户)
    *   [1.5 更改 samba 用户的密码](#更改_samba_用户的密码)
    *   [1.6 端口设置](#端口设置)
    *   [1.7 验证配置](#验证配置)
*   [2 客户端配置](#客户端配置)
    *   [2.1 显示可用共享](#显示可用共享)
    *   [2.2 WINS 主机名](#WINS_主机名)
    *   [2.3 手动挂载](#手动挂载)
        *   [2.3.1 保存共享密码](#保存共享密码)
    *   [2.4 自动挂载](#自动挂载)
        *   [2.4.1 As mount entry](#As_mount_entry)
        *   [2.4.2 As systemd unit](#As_systemd_unit)
        *   [2.4.3 smbnetfs](#smbnetfs)
            *   [2.4.3.1 Daemon](#Daemon)
        *   [2.4.4 autofs](#autofs)
    *   [2.5 文件管理器配置](#文件管理器配置)
        *   [2.5.1 GNOME Files, Nemo, Caja, Thunar and PCManFM](#GNOME_Files,_Nemo,_Caja,_Thunar_and_PCManFM)
        *   [2.5.2 KDE](#KDE)
        *   [2.5.3 Other graphical environments](#Other_graphical_environments)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Block certain file extensions on Samba share](#Block_certain_file_extensions_on_Samba_share)
    *   [3.2 Discovering network shares](#Discovering_network_shares)
    *   [3.3 Remote control of Windows computer](#Remote_control_of_Windows_computer)
    *   [3.4 Share files without a username and password](#Share_files_without_a_username_and_password)
        *   [3.4.1 Sample Passwordless Configuration](#Sample_Passwordless_Configuration)
    *   [3.5 Build Samba without CUPS](#Build_Samba_without_CUPS)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Failed to start Samba SMB/CIFS server](#Failed_to_start_Samba_SMB/CIFS_server)
    *   [4.2 Unable to overwrite files, permissions errors](#Unable_to_overwrite_files,_permissions_errors)
    *   [4.3 Windows clients keep asking for password even if Samba shares are created with guest permissions](#Windows_clients_keep_asking_for_password_even_if_Samba_shares_are_created_with_guest_permissions)
    *   [4.4 Windows 7 connectivity problems - mount error(12): cannot allocate memory](#Windows_7_connectivity_problems_-_mount_error(12):_cannot_allocate_memory)
    *   [4.5 Trouble accessing a password-protected share from Windows](#Trouble_accessing_a_password-protected_share_from_Windows)
    *   [4.6 Getting a dialog box up takes a long time](#Getting_a_dialog_box_up_takes_a_long_time)
    *   [4.7 Error: Failed to retrieve printer list: NT_STATUS_UNSUCCESSFUL](#Error:_Failed_to_retrieve_printer_list:_NT_STATUS_UNSUCCESSFUL)
    *   [4.8 Sharing a folder fails](#Sharing_a_folder_fails)
    *   [4.9 "Browsing" network fails with "Failed to retrieve share list from server"](#"Browsing"_network_fails_with_"Failed_to_retrieve_share_list_from_server")
    *   [4.10 You are not the owner of the folder](#You_are_not_the_owner_of_the_folder)
    *   [4.11 protocol negotiation failed: NT_STATUS_INVALID_NETWORK_RESPONSE](#protocol_negotiation_failed:_NT_STATUS_INVALID_NETWORK_RESPONSE)
    *   [4.12 Connection to SERVER failed: (Error NT_STATUS_UNSUCCESSFUL)](#Connection_to_SERVER_failed:_(Error_NT_STATUS_UNSUCCESSFUL))
    *   [4.13 Connection to SERVER failed: (Error NT_STATUS_CONNECTION_REFUSED)](#Connection_to_SERVER_failed:_(Error_NT_STATUS_CONNECTION_REFUSED))
*   [5 参阅](#参阅)

## 服务器配置

要通过 Samba 共享文件,还需额外 [安装](/index.php/Pacman "Pacman") 软件包 [samba](https://www.archlinux.org/packages/?name=samba)。

Samba 服务的配置文件是 `/etc/samba/smb.conf`，如果没有则 smbd 无法启动。

你可以从 [这里](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD) 获取到默认配置文件：

```
# wget "[https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD)" -O /etc/samba/smb.conf

```

**注意:**

*   从上面载回来的默认配置文件里把日志`log file`设置到了一个不能写的地方, 这会导致出错。 下面的办法可以解决这个问题:
    *   把日志文件放到可写的路径: `log file = /var/log/samba/%m.log`
    *   把日志存到非文件后端的解决方案里: `logging = syslog` 配合 `syslog only = yes`, 或者使用 `logging = systemd`
*   如果需要的话; 在`[global]`部份中指定的 `workgroup` 需要对应windows工作组的名称 (默认是 `WORKGROUP`).

### 建立共享

编辑 `/etc/samba/smb.conf` ，滚动到 **Share Definitions** 部分，默认的配置文件会为所有用户在 HOME 目录建立一个共享。但是需要进行下面配置用户才能登录：

 `/etc/samba/smb.conf` 
```
...
[homes]
   comment = Home Directories
   browseable = no
   writable = yes
   valid users = %S
```

同时，默认配置文件也共享打印机，包含一些不错的示例配置。更多的可用选项可以通过 [smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5) 查询，在此处 [Here](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html) 是在线版本。

**提示：** 如果需要共享给 Windows，需要在 `smb.conf` 中设置当前使用的 Windows 工作组workgroup（默认工作组是 `WORKGROUP`）。

### 启动服务

**注意:** 在 [samba](https://www.archlinux.org/packages/?name=samba) 4.8.0-1里, `smbd.service` 和 `nmbd.service` 单元被改名为 `smb.service` 和 `nmb.service`.

为了能够使用 SMB 进行基本的文件共享，[start/enable](/index.php/Systemd#Using_units "Systemd") `smb.service` 和 `nmb.service` 服务。更多信息参阅 [smbd](http://www.samba.org/samba/docs/man/manpages-3/smbd.8.html) 和 [nmbd](http://www.samba.org/samba/docs/man/manpages-3/nmbd.8.html) 的 man 手册。 `nmbd.service` 并不总是需要启用。

**提示：** 除了在启动时启动服务，可以选择启用 `smbd.socket`，禁用 `smbd.service`。这样的话会在第一次收到连接请求是启动后台进程。

### 建立 Usershare 路径

**Note:** 此为可选功能，如无需要可以跳过。

"Usershare" 让不具有 root 权限的用户可以进行添加、修改和删除自己的文件夹的操作。

以下操作将会在 `/var/lib/samba` 添加 usershares 目录：

```
# mkdir -p /var/lib/samba/usershare

```

以下操作将会建立 sambashare 用户组：

```
# groupadd sambashare

```

以下操作将会将刚刚建立的文件夹的权限：拥有者更改为 root，群组更改为 sambashare：

```
# chown root:sambashare /var/lib/samba/usershare

```

以下的操作将会让 sambashare 群组中的用户拥有读取，写入和执行此文件夹中内容的权限：

```
# chmod 1770 /var/lib/samba/usershare

```

修改 `smb.conf` 配置文件中的以下变量：

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

将用户添加到群组 *sambashare* 中。其中，替换 `*your_username*` 为实际的用户名：

```
# usermod -a -G sambashare *your_username*

```

重启 `smbd.service` 和 `nmbd.service` 服务。

注销后重新登陆，此时您应该就可以使用 GUI 程序配置您的 samba 共享服务了。例如，在 [Thunar](/index.php/Thunar "Thunar") 中您可以右键点击任何一个文件夹将它在局域网中共享。如果你想共享自己主目录内的路径，需要主目录的内容让其它用户可以列出。

### 添加用户

Samba 需要 Linux 账户才能使用 - 可以使用已有账户或 [创建新用户](/index.php/Users_and_groups#User_management "Users and groups").

虽然用户名可以和 Linux 系统共享，Samba 使用单独的密码管理，将下面的 `samba_user` 替换为选择的 Samba 用户:

```
# smbpasswd -a *samba_user*

```

根据 [服务器角色](https://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html#SERVERROLE) 的差异，可能需要修改已有的 [文件权限和属性](/index.php/File_permissions_and_attributes "File permissions and attributes")。

要让新创建的用户仅能访问 Samba 远程文件服务器，可以禁用其它登录选项

*   禁用 shell - `usermod --shell /usr/bin/nologin --lock username`
*   禁用 SSH logons - /etc/ssh/sshd_conf, option `AllowUsers`

参阅[Security](/index.php/Security "Security")。

### 更改 samba 用户的密码

用 `smbpasswd` 修改 samba 用户的密码:

```
# smbpasswd *samba_user*

```

### 端口设置

如果使用 [firewall](/index.php/Firewall "Firewall")，需要将打开 samba 对于的窗口，通常是 137-139 + 445\. 完整列表请参考 [Samba port](https://wiki.samba.org/index.php/Samba_port_usage).

### 验证配置

`testparm` 可以检查 samba.conf 是否有错误:

```
# testparm -s

```

## 客户端配置

如果不需要查询公开的共享，可以安装轻量级的 [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) 软件包，使用 `/usr/bin/mount.cifs` 命令挂载共享.

要使用类似 ftp 的命令行界面，请安装软件包 [smbclient](https://www.archlinux.org/packages/?name=smbclient)。常用命令请参考 [smbclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smbclient.1)。

[桌面环境](/index.php/Desktop_environment "Desktop environment") 可能提供了图形界面，参考[#文件管理器配置](#文件管理器配置).

**Note:** 安装 [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) 或 [smbclient](https://www.archlinux.org/packages/?name=smbclient) 后，请加载 `cifs` [内核模块](/index.php/Kernel_module "Kernel module") 或重启以避免挂载失败。

### 显示可用共享

下面命令会显示服务器上的可用共享:

```
$ smbclient -L *hostname* -U%

```

*smbtree* 可用显示共享目录树，不建议再有大量计算机的网络上使用此功能。可用它检查共享名是否可用。

```
$ smbtree -b -N

```

`-b` (`--broadcast`) 使用广播模式，`-N` (`-no-pass`) 不询问密码.

### WINS 主机名

[smbclient](https://www.archlinux.org/packages/?name=smbclient) 提供了一个用 WINS 解析主机名的驱动，要启用它，将 “wins” 添加到 /etc/nsswitch.conf 的 “hosts” 行。

### 手动挂载

创建共享挂载点：

```
# mkdir /mnt/*mountpoint*

```

使用 `mount.cifs` 作为挂载类型 `type`，下面列出的选项并不是全部都需要：

 `# mount -t cifs //*SERVER*/*sharename* /mnt/*mountpoint* -o user=*username*,password=*password*,uid=*username*,gid=*group*,workgroup=*workgroup*,ip=*serverip*,iocharset=*utf8*` 

要允许用户挂载到自己可以访问的目录，请使用 `users` 挂载选项。

**Note:** 请注意这里有 **s**,其它文件系统一般用的是 *user*。

使用 `uid` 和 `gid` 挂载选项时，请注意 [文件权限](/index.php/File_permissions_and_attributes "File permissions and attributes")，否则会出现 I/O 错误。}}

*SERVER*

	服务器名.

*sharename*

	共享目录.

*mountpoint*

	本地的挂载点.

`-o [options]`

	详情请参考 [mount.cifs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.cifs.8).

**Note:**

*   结尾不要加 `/`. `//*SERVER*/*sharename***/**` 无法工作.
*   如果挂载工作不稳定，出现死机和掉线问题，请尝试用 `vers=` 设置不同的 SMB 协议版本。例如， 挂载 Vista 用 `vers=2.0`.
*   如果挂载了 cifs 机器上出现关机超时，请参考 [WPA supplicant#Problem with mounted network shares (cifs) and shutdown](/index.php/WPA_supplicant#Problem_with_mounted_network_shares_(cifs)_and_shutdown "WPA supplicant").

##### 保存共享密码

不建议将密码保存在所有人都可读的文件中，一个更安全的方式是创建密码文件：

 `/path/to/credentials/share` 
```
username=*myuser*
password=*mypass*
```

将 `username=myuser,password=mypass` 替换为 `credentials=/path/to/credentials/share`.

修改密码文件的权限：

```
# chmod 600 /path/to/credentials/share

```

### 自动挂载

**Note:** You may need to [enable](/index.php/Enable "Enable") `systemd-networkd-wait-online.service` or `NetworkManager-wait-online.service` (depending on your setup) to proper enable booting on start-up.

#### As mount entry

This is an simple example of a `cifs` [mount entry](/index.php/Fstab "Fstab") that requires authentication:

 `/etc/fstab`  `//*SERVER*/*sharename* /mnt/*mountpoint* cifs username=*myuser*,password=*mypass* 0 0` 
**Note:** Space in sharename should be replaced by `\040` (ASCII code for space in octal). For example, `//*SERVER*/share name` on the command line should be `//*SERVER*/share\040name` in `/etc/fstab`.

To speed up the service on boot, add the `x-systemd.automount` option to the entry:

 `/etc/fstab`  `//*SERVER*/*SHARENAME* /mnt/*mountpoint* cifs credentials=*/path/to/smbcredentials/share*,x-systemd.automount 0 0` 

#### As systemd unit

Create a new `.mount` file inside `/etc/systemd/system`, e.g. `mnt-myshare.mount`.

`Requires=` replace (if needed) with your [Network configuration](/index.php/Category:Network_configuration "Category:Network configuration").

`What=` path to share

`Where=` path to mount the share

`Options=` share mounting options

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

查看 [Autofs](/index.php/Autofs "Autofs") 以获得关于基于内核的 Linux 自动挂载器的相关信息。

### 文件管理器配置

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

### Discovering network shares

If nothing is known about other systems on the local network, and automated tools such as [smbnetfs](#smbnetfs) are not available, the following methods allow one to manually probe for Samba shares.

1\. First, install [nmap](https://www.archlinux.org/packages/?name=nmap) and [smbclient](https://www.archlinux.org/packages/?name=smbclient) using [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S nmap smbclient

```

2\. `nmap` checks which ports are open:

```
# nmap -p 139 -sT "192.168.1.*"

```

In this case, a scan on the 192.168.1.* IP address range and port 139 has been performed, resulting in:

```
$ nmap -sT "192.168.1.*"

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

### Share files without a username and password

Edit `/etc/samba/smb.conf` and add the following line:

 `map to guest = Bad User` 

After this line:

 `security = user` 

Restrict the shares data to a specific interface replace:

 `;   interfaces = 192.168.12.2/24 192.168.13.2/24` 

with:

```
interfaces = lo eth0
bind interfaces only = true
```

Optionally edit the account that access the shares, edit the following line:

 `;   guest account = nobody` 

For example:

 `   guest account = pcguest` 

And do something in the likes of:

 `# useradd -c "Guest User" -d /dev/null -s /bin/false pcguest` 

Then setup a "" password for user pcguest.

The last step is to create share directory (for write access make writable = yes):

```
[Public Share]
path = /path/to/public/share
available = yes
browsable = yes
public = yes
writable = no

```

**Note:** Make sure the guest also has permission to visit /path, /path/to and /path/to/public, according to [http://unix.stackexchange.com/questions/13858/do-the-parent-directorys-permissions-matter-when-accessing-a-subdirectory](http://unix.stackexchange.com/questions/13858/do-the-parent-directorys-permissions-matter-when-accessing-a-subdirectory)

#### Sample Passwordless Configuration

This is the configuration I use with samba 4 for easy passwordless filesharing with family on a home network. Change any options needed to suit your network (workgroup and interface). I'm restricting it to the static IP I have on my ethernet interface, just delete that line if you do not care which interface is used.

 `/etc/samba/smb.conf` 
```
[global]

   workgroup = WORKGROUP

   server string = Media Server

   security = user
   map to guest = Bad User

   log file = /var/log/samba/%m.log

   max log size = 50

   interfaces = 192.168.2.194/24

   dns proxy = no 

[media]
   path = /shares
   public = yes
   only guest = yes
   writable = yes

[storage]
   path = /media/storage
   public = yes
   only guest = yes
   writable = yes

```

### Build Samba without CUPS

Just build without cups installed. From the [Samba Wiki](https://wiki.samba.org/index.php/Samba_as_a_print_server):

> Samba has built-in support [for CUPS] and defaults to CUPS if the development package (aka header files and libraries) could be found at compile time.

Of course, modifications to the PKGBUILD will also be necessary: libcups will have to be removed from the depends and makedepends arrays and other references to cups and printing will need to be deleted. In the case of the 4.1.9-1 PKGBUILD, 'other references' includes lines 169, 170 and 236:

```
    mkdir -p ${pkgdir}/usr/lib/cups/backend
    ln -sf /usr/bin/smbspool ${pkgdir}/usr/lib/cups/backend/smb
  install -d -m1777 ${pkgdir}/var/spool/samba

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

## 参阅

*   [Samba: An Introduction](http://www.samba.org/samba/docs/SambaIntro.html)
*   [Official Samba site](http://www.samba.org/)