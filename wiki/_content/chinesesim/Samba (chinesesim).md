相关文章

*   [NFS](/index.php/NFS "NFS")
*   [Samba/Active Directory domain controller](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller")
*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")

**翻译状态：** 本文是英文页面 [Samba](/index.php/Samba "Samba") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-13，点击[这里](https://wiki.archlinux.org/index.php?title=Samba&diff=0&oldid=568014)可以查看翻译后英文页面的改动。

**Samba** 是 [SMB/CIFS](https://en.wikipedia.org/wiki/Server_Message_Block 的功能类似。本文介绍如何配置和使用 Samba.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 服务器](#服务器)
    *   [1.1 安装](#安装)
        *   [1.1.1 配置防火墙](#配置防火墙)
    *   [1.2 用户管理](#用户管理)
        *   [1.2.1 添加用户](#添加用户)
        *   [1.2.2 查询用户](#查询用户)
        *   [1.2.3 更改 samba 用户的密码](#更改_samba_用户的密码)
        *   [1.2.4 创建共享](#创建共享)
        *   [1.2.5 启动服务](#启动服务)
    *   [1.3 高级配置](#高级配置)
        *   [1.3.1 建立 Usershare 路径](#建立_Usershare_路径)
*   [2 客户端配置](#客户端配置)
    *   [2.1 显示可用共享](#显示可用共享)
    *   [2.2 WINS 主机名](#WINS_主机名)
    *   [2.3 手动挂载](#手动挂载)
        *   [2.3.1 保存共享密码](#保存共享密码)
    *   [2.4 Automatic mounting](#Automatic_mounting)
        *   [2.4.1 As mount entry](#As_mount_entry)
        *   [2.4.2 As systemd unit](#As_systemd_unit)
        *   [2.4.3 smbnetfs](#smbnetfs)
            *   [2.4.3.1 Daemon](#Daemon)
        *   [2.4.4 autofs](#autofs)
    *   [2.5 File manager configuration](#File_manager_configuration)
        *   [2.5.1 GNOME Files, Nemo, Caja, Thunar and PCManFM](#GNOME_Files,_Nemo,_Caja,_Thunar_and_PCManFM)
        *   [2.5.2 KDE](#KDE)
        *   [2.5.3 Other graphical environments](#Other_graphical_environments)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Discovering network shares](#Discovering_network_shares)
    *   [3.2 Remote control of Windows computer](#Remote_control_of_Windows_computer)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Failed to start Samba SMB/CIFS server](#Failed_to_start_Samba_SMB/CIFS_server)
    *   [4.2 Permission issues on AppArmor](#Permission_issues_on_AppArmor)
    *   [4.3 No dialect specified on mount](#No_dialect_specified_on_mount)
    *   [4.4 Unable to overwrite files, permissions errors](#Unable_to_overwrite_files,_permissions_errors)
    *   [4.5 Windows clients keep asking for password even if Samba shares are created with guest permissions](#Windows_clients_keep_asking_for_password_even_if_Samba_shares_are_created_with_guest_permissions)
    *   [4.6 Windows 7 connectivity problems - mount error(12): cannot allocate memory](#Windows_7_connectivity_problems_-_mount_error(12):_cannot_allocate_memory)
    *   [4.7 Windows 10 1709 and up connectivity problems - "Windows cannot access" 0x80004005](#Windows_10_1709_and_up_connectivity_problems_-_"Windows_cannot_access"_0x80004005)
    *   [4.8 Error: Failed to retrieve printer list: NT_STATUS_UNSUCCESSFUL](#Error:_Failed_to_retrieve_printer_list:_NT_STATUS_UNSUCCESSFUL)
    *   [4.9 Sharing a folder fails](#Sharing_a_folder_fails)
    *   [4.10 "Browsing" network fails with "Failed to retrieve share list from server"](#"Browsing"_network_fails_with_"Failed_to_retrieve_share_list_from_server")
    *   [4.11 Protocol negotiation failed: NT_STATUS_INVALID_NETWORK_RESPONSE](#Protocol_negotiation_failed:_NT_STATUS_INVALID_NETWORK_RESPONSE)
    *   [4.12 Connection to SERVER failed: (Error NT_STATUS_UNSUCCESSFUL)](#Connection_to_SERVER_failed:_(Error_NT_STATUS_UNSUCCESSFUL))
    *   [4.13 Connection to SERVER failed: (Error NT_STATUS_CONNECTION_REFUSED)](#Connection_to_SERVER_failed:_(Error_NT_STATUS_CONNECTION_REFUSED))
    *   [4.14 Protocol negotiation failed: NT_STATUS_CONNECTION_RESET](#Protocol_negotiation_failed:_NT_STATUS_CONNECTION_RESET)
    *   [4.15 Password Error when correct credentials are given (error 1326)](#Password_Error_when_correct_credentials_are_given_(error_1326))
    *   [4.16 Mapping reserved Windows characters](#Mapping_reserved_Windows_characters)
    *   [4.17 Folder shared inside graphical environment is not available to guests](#Folder_shared_inside_graphical_environment_is_not_available_to_guests)
        *   [4.17.1 Verify correct samba configuration](#Verify_correct_samba_configuration)
        *   [4.17.2 Verify correct shared folder creation](#Verify_correct_shared_folder_creation)
        *   [4.17.3 Verify folder access by guest](#Verify_folder_access_by_guest)
    *   [4.18 Mount error: Host is down](#Mount_error:_Host_is_down)
*   [5 See also](#See_also)

## 服务器

### 安装

[安装](/index.php/Pacman "Pacman") 软件包 [samba](https://www.archlinux.org/packages/?name=samba)。

Samba 服务的配置文件是 `/etc/samba/smb.conf`，[smb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smb.conf.5)提供了详细的文档。

[samba](https://www.archlinux.org/packages/?name=samba) 软件包没有提供此文件，启动 *smb*.service 前需要先创建这个文件。从 [这里](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD) 可以获取到示例文件。

从上面获取的默认配置文件里把日志`log file`设置到一个不能写的地方, 这会引起错误。下面的办法可以解决这个问题:

*   把日志文件放到可写的路径: `log file = /var/log/samba/%m.log`
    *   把日志存到非文件后端的解决方案里: `logging = syslog` 配合 `syslog only = yes`, 或者使用 `logging = systemd`

如果需要的话; 在`[global]`部份中指定的 `workgroup` 需要对应windows工作组的名称 (默认是 `WORKGROUP`).

**Tip:** 修改 `smb.conf` 文件后，运行 [testparm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/testparm.1) 命令看看有没有语法错误。

#### 配置防火墙

如果使用了 [防火墙](/index.php/Firewall "Firewall")，请记得打开需要的端口(通常是 137-139 + 445). 完整列表请查看 [Samba 端口使用](https://www.samba.org/~tpot/articles/firewall.html)。

### 用户管理

#### 添加用户

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

#### 查询用户

用 [pdbedit(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pdbedit.8) 命令查询现有用户:

```
# pdbedit -L -v

```

#### 更改 samba 用户的密码

用 `smbpasswd` 修改 samba 用户的密码:

```
# smbpasswd *samba_user*

```

#### 创建共享

**Note:** To allow the usage of *guests* on public shares, one may need to [append](/index.php/Append "Append") `map to guest = Bad User` in the `[global]` section of `/etc/samba/smb.conf`. A different `guest account` may be used instead of the default provided `nobody`.

请确保 [smb.conf.default](https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD) 的 *Share Definitions* 部分正确设置了共享。

#### 启动服务

**注意:** 在 [samba](https://www.archlinux.org/packages/?name=samba) 4.8.0-1里, `smbd.service` 和 `nmbd.service` 单元被改名为 `smb.service` 和 `nmb.service`.

为了能够使用 SMB 进行基本的文件共享，[start/enable](/index.php/Systemd#Using_units "Systemd") `smb.service` 和 `nmb.service` 服务。更多信息参阅 [smbd](http://www.samba.org/samba/docs/man/manpages-3/smbd.8.html) 和 [nmbd](http://www.samba.org/samba/docs/man/manpages-3/nmbd.8.html) 的 man 手册。 `nmbd.service` 并不总是需要启用。

**提示：** 除了在启动时启动服务，可以选择启用 `smbd.socket`，禁用 `smbd.service`。这样的话会在第一次收到连接请求是启动后台进程。

### 高级配置

#### 建立 Usershare 路径

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

## 客户端配置

如果不需要查询公开的共享，可以安装轻量级的 [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) 软件包，使用 `/usr/bin/mount.cifs` 命令挂载共享.

要使用类似 ftp 的命令行界面，请安装软件包 [smbclient](https://www.archlinux.org/packages/?name=smbclient)。常用命令请参考 [smbclient(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smbclient.1)。

[桌面环境](/index.php/Desktop_environment "Desktop environment") 可能提供了图形界面，参考[#文件管理器配置](#文件管理器配置).

**Note:** 安装 [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) 或 [smbclient](https://www.archlinux.org/packages/?name=smbclient) 后，请加载 `cifs` [内核模块](/index.php/Kernel_module "Kernel module") 或重启以避免挂载失败。

#### 显示可用共享

下面命令会显示服务器上的可用共享:

```
$ smbclient -L *hostname* -U%

```

*smbtree* 可用显示共享目录树，不建议再有大量计算机的网络上使用此功能。可用它检查共享名是否可用。

```
$ smbtree -b -N

```

`-b` (`--broadcast`) 使用广播模式，`-N` (`-no-pass`) 不询问密码.

#### WINS 主机名

[smbclient](https://www.archlinux.org/packages/?name=smbclient) 提供了一个用 WINS 解析主机名的驱动，要启用它，将 “wins” 添加到 /etc/nsswitch.conf 的 “hosts” 行。

#### 手动挂载

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

### Automatic mounting

**Note:** You may need to [enable](/index.php/Enable "Enable") `systemd-networkd-wait-online.service` or `NetworkManager-wait-online.service` (depending on your setup) to proper enable booting on start-up.

#### As mount entry

This is a simple example of a `cifs` [mount entry](/index.php/Fstab "Fstab") that requires authentication:

 `/etc/fstab`  `//*SERVER*/*sharename* /mnt/*mountpoint* cifs username=*myuser*,password=*mypass* 0 0` 
**Note:** Spaces in sharename should be replaced by `\040` (ASCII code for space in octal). For example, `//*SERVER*/share name` on the command line should be `//*SERVER*/share\040name` in `/etc/fstab`.

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

If using a [share path](#Creating_a_share) located outside of a home-directory, whitelist it in `/etc/apparmor.d/local/usr.sbin.smbd`. E.g.:

 `/etc/apparmor.d/local/usr.sbin.smbd` 
```
/data/** lrwk,

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

You are probably passing a wrong server name to `smbclient`. To find out the server name, run `hostnamectl` on the server and look at "Transient hostname" line

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