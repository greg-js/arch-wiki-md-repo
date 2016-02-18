**Samba** 是 [SMB/CIFS](https://en.wikipedia.org/wiki/Server_Message_Block 的补充使得在 Linux 和 Windows 系统中进行文件共享、打印机共享更容易实现。一些用户说Samba配置简单，操作直观。然而，许多新用户会因为它的复杂性和非直观的机制而遇到问题。强烈建议新用户仔细按照下面的指导。

## Contents

*   [1 服务配置](#.E6.9C.8D.E5.8A.A1.E9.85.8D.E7.BD.AE)
    *   [1.1 建立共享](#.E5.BB.BA.E7.AB.8B.E5.85.B1.E4.BA.AB)
    *   [1.2 启动服务](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1)
    *   [1.3 建立 Usershare 路径](#.E5.BB.BA.E7.AB.8B_Usershare_.E8.B7.AF.E5.BE.84)
    *   [1.4 添加用户](#.E6.B7.BB.E5.8A.A0.E7.94.A8.E6.88.B7)
    *   [1.5 更改 samba 用户的密码](#.E6.9B.B4.E6.94.B9_samba_.E7.94.A8.E6.88.B7.E7.9A.84.E5.AF.86.E7.A0.81)
    *   [1.6 端口设置](#.E7.AB.AF.E5.8F.A3.E8.AE.BE.E7.BD.AE)
*   [2 客户端配置](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.85.8D.E7.BD.AE)
    *   [2.1 Manual mounting](#Manual_mounting)
        *   [2.1.1 Add Share to /etc/fstab](#Add_Share_to_.2Fetc.2Ffstab)
        *   [2.1.2 User mounting](#User_mounting)
    *   [2.2 WINS host names](#WINS_host_names)
    *   [2.3 Automatic mounting](#Automatic_mounting)
        *   [2.3.1 smbnetfs](#smbnetfs)
            *   [2.3.1.1 Daemon](#Daemon)
        *   [2.3.2 autofs](#autofs)
    *   [2.4 文件管理器配置](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E9.85.8D.E7.BD.AE)
        *   [2.4.1 GNOME Files, Nemo, Thunar and PCManFM](#GNOME_Files.2C_Nemo.2C_Thunar_and_PCManFM)
        *   [2.4.2 KDE](#KDE)
        *   [2.4.3 Other graphical environments](#Other_graphical_environments)
*   [3 See also](#See_also)

## 服务配置

如果只是访问文件,而不需要共享文件,仅 [安装](/index.php/Pacman#Installing_specific_packages "Pacman") [smbclient](https://www.archlinux.org/packages/?name=smbclient) 程序就足够了.

```
# pacman -S smbclient

```

如果想要使用 Samba 共享您的文件,还需额外 [安装](/index.php/Pacman#Installing_specific_packages "Pacman") [samba](https://www.archlinux.org/packages/?name=samba) 包( 这将同时安装客户端 ):

```
# pacman -S samba

```

Samba 服务的默认配置文件在 `/etc/samba/smb.conf.default` 中，你可以将初始配置复制到 `/etc/samba/smb.conf` 中：

```
# cp /etc/samba/smb.conf.default /etc/samba/smb.conf

```

**Tip:** 运行 `testparm` 检查 samba 的配置文件是否合法。

### 建立共享

编辑 `/etc/samba/smb.conf` ，滚动到 **Share Definitions** 部分，默认的配置文件会为所有用户在 HOME 目录建立一个共享文件夹和打印机。同时，它也包含一些不错的示例配置。更多的可用选项可以通过 `man smb.conf` 查询，在此处 [Here](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html) 是在线版本。

如果需要共享给 Windows，需要在 `smb.conf` 添加 Windows Workgroup （Windows 系统的工作组默认名称是： WORKGROUP）。

### 启动服务

为了能够用 SMB 使用最基本的文件共享服务，[start/enable](/index.php/Systemd#Using_units "Systemd") `smbd.service` 和 `nmbd.service` 服务。 查看 [smbd](http://www.samba.org/samba/docs/man/manpages-3/smbd.8.html) 和 [nmbd](http://www.samba.org/samba/docs/man/manpages-3/nmbd.8.html) 的 man 手册查看更多信息。

**Tip:** Instead of having the service running since boot, you can enable `smbd.socket` so the daemon is started on the first incoming connection. Don't forget to disable `smbd.service`.

### 建立 Usershare 路径

**Note:** 此为高阶选项，如无需要可以跳过。

"Usershare" 为那些不具有 root 权限的用户提供了可以添加、修改和删除属于他们自己的文件夹的功能。

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

以下操作将会将用户添加到群组 *sambashare* 中。其中，替换 `*your_username*` 为实际的用户名：

```
# usermod -a -G sambashare *your_username*

```

重启 `smbd` 和 `nmbd` 服务。

注销后重新登陆，此时您应该就可以使用 GUI 程序配置您的 samba 共享服务了。例如，在 [Thunar](/index.php/Thunar "Thunar") 中您可以右键点击任何一个文件夹将它在局域网中共享。如果你想共享自己主目录内的路径，需要主目录的内容让其它用户可以列出。

### 添加用户

Create a [Linux user account](/index.php/Users_and_groups#User_management "Users and groups") for *samba* user. Substitute `*samba_user*` with preferred name if desired:

```
# useradd *samba_user*

```

Then create a *Samba* user account with the same name:

```
# pdbedit -a -u *samba_user*

```

### 更改 samba 用户的密码

To change a user's password, use `smbpasswd`:

```
# smbpasswd *samba_user*

```

### 端口设置

If you're using a [firewall](/index.php/Firewall "Firewall"); don't forget to open required ports (usually 137-139 + 445). For a complete list please check [Samba port usage](https://wiki.samba.org/index.php/Samba_port_usage).

## 客户端配置

如果想要从 Samba/SMB/CIFS 服务器中读取文件，仅需要安装 [smbclient](https://www.archlinux.org/packages/?name=smbclient)。此安装包可以直接从官方源取得。

Shared resources from other computers on the LAN may be accessed and mounted locally by GUI or CLI methods. Depending on the [desktop environment](/index.php/Desktop_environment "Desktop environment"), GUI methods may not be available. See also [#File_manager_configuration](#File_manager_configuration) for use with a file manager.

There are two parts in sharing access. The first is the underlying file system mechanism, which some environments have built in. The second is the interface which allows the user to mount shared resources.

**Note:**

*   After installing cifs-utils or smbclient, you must restart or modprobe cifs
*   Otherwise mount fails with "cifs filesystem not supported by the system"

### Manual mounting

For a lighter approach without support for listing public shares, only install [cifs-utils](https://www.archlinux.org/packages/?name=cifs-utils) to provide `/usr/bin/mount.cifs`.

To list public shares on a server:

```
$ smbclient -L *hostname* -U%

```

Create a mount point for the share:

```
# mkdir /mnt/*mountpoint*

```

Mount the share using the `mount.cifs` type. Not all the options listed below are needed or desirable (ie. `password`).

 `# mount -t cifs //*SERVER*/*sharename* /mnt/*mountpoint* -o user=*username*,password=*password*,workgroup=*workgroup*,ip=*serverip*` 
**Note:** If you get the output "mount error(13): Permission denied", this might be due to a bug in mount.cifs. See the following bug report. [https://bugs.archlinux.org/task/43015#comment130771](https://bugs.archlinux.org/task/43015#comment130771) Try specifying the option "sec=ntlmv2" to work around it.

*SERVER*

	The Windows system name.

*sharename*

	The shared directory.

*mountpoint*

	The local directory where the share will be mounted.

`-o [options]`

	See `man mount.cifs` for more information.

**Note:**

*   Abstain from using a trailing `/`. `//*SERVER*/*sharename***/**` will not work.
*   If your mount does not work stable, stutters or freezes, try to enable different SMB protocol version with `vers=` option. For example, `vers=2.0` for Windows Vista mount.

#### Add Share to /etc/fstab

The simplest way to add an fstab entry is something like this:

 `/etc/fstab`  `//*SERVER*/*sharename* /mnt/*mountpoint* cifs username=*username*,password=*password* 0 0` 

However, storing passwords in a world readable file is not recommended! A safer method would be to use a credentials file. As an example, create a file and `chmod 600 *filename*` so only the owning user can read and write to it. It should contain the following information:

 `/path/to/credentials/sambacreds` 
```
username=*username*
password=*password*
```

and the line in your fstab should look something like this:

 `/etc/fstab`  `//SERVER/SHARENAME /mnt/*mountpoint* cifs credentials=*/path/to/credentials/sambacreds* 0 0` 

If using *systemd* (modern installations), one can utilize the `x-systemd.automount` option, which speeds up service boot by a few seconds. Also, one can map current user and group to make life a bit easier, utilizing `uid` and `gid` options.

**Warning:** Using the `uid` and `gid` options may cause input ouput errors in programs that try to fetch data from network drives.
 `/etc/fstab`  `//*SERVER*/*SHARENAME* /mnt/*mountpoint* cifs credentials=*/path/to/smbcredentials*,x-systemd.automount,uid=*username*,gid=*usergroup* 0 0` 
**Note:** Space in sharename should be replaced by `\040` (ASCII code for space in octal). For example, `//*SERVER*/share name` on the command line should be `//*SERVER*/share\040name` in `/etc/fstab`.

#### User mounting

 `/etc/fstab`  `//*SERVER*/*SHARENAME* /mnt/*mountpoint* cifs users,credentials=*/path/to/smbcredentials*,workgroup=*workgroup*,ip=*serverip* 0 0` 
**Note:** The option is user**s** (plural). For other filesystem types handled by mount, this option is usually *user*; sans the "**s**".

This will allow users to mount it as long as the mount point resides in a directory controllable by the user; i.e. the user's home. For users to be allowed to mount and unmount the Samba shares with mount points that they do not own, use [smbnetfs](#smbnetfs), or grant privileges using [sudo](/index.php/Sudo "Sudo").

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

Now [restart](/index.php/Systemd#Using_units "Systemd") `smbd.service` and `nmbd.service`.

If everything works as expected, [install](/index.php/Pacman#Installing_specific_packages "Pacman") [smbnetfs](https://www.archlinux.org/packages/?name=smbnetfs) from the official repositories.

Then, add the following line to `/etc/fuse.conf`:

```
user_allow_other

```

and load the `fuse` [kernel module](/index.php/Kernel_module "Kernel module"):

```
# modprobe fuse

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

If you are using the Dolphin or Nautilus file managers, you may want to the following to `~/.smb/smbnetfs.conf` to avoid "Disk full" errors as smbnetfs by default will report 0 bytes of free space:

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

#### GNOME Files, Nemo, Thunar and PCManFM

In order to access samba shares through GNOME Files, Nemo, Thunar or PCManFM, install the [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

Press `Ctrl+l` and enter `smb://*servername*/*share*` in the location bar to access your share.

The mounted share is likely to be present at `/run/user/*your_UID*/gvfs` in the filesystem.

#### KDE

KDE, has the ability to browse Samba shares built in. Therefore do not need any additional packages. However, for a GUI in the KDE System Settings, install the [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing) package from the official repositories.

If when navigating with Dolphin you get a "Time Out" Error, you should uncomment and edit this line in smb.conf: `name resolve order = lmhosts bcast host wins` 

as shown in this [page](http://ubuntuforums.org/showthread.php?t=1605499).

#### Other graphical environments

There are a number of useful programs, but they may need to have packages created for them. This can be done with the Arch package build system. The good thing about these others is that they do not require a particular environment to be installed to support them, and so they bring along less baggage.

*   [pyneighborhood](https://www.archlinux.org/packages/?name=pyneighborhood) is available in the official repositories.
*   LinNeighborhood, RUmba, xffm-samba plugin for Xffm are not available in the official repositories or the AUR. As they are not officially (or even unofficially supported), they may be obsolete and may not work at all.

## See also

*   [Samba: An Introduction](http://www.samba.org/samba/docs/SambaIntro.html)
*   [Official Samba site](http://www.samba.org/)