来源 [Wikipedia](https://en.wikipedia.org/wiki/Network_File_System "wikipedia:Network File System"): NFS 网络文件系统(Network File System) 是由Sun公司1984年发布的分散式文件系统协议。允许用户像访问本地文件一样，去访问网络上共享的文件。NFS 是一個成功的文件共享方法，但它最大的问题是它不太适合大型的分散式系統。

本文介绍 NFSv4 的安装.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
        *   [2.1.1 ID mapping](#ID_mapping)
        *   [2.1.2 文件系统](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
        *   [2.1.3 Exports](#Exports)
        *   [2.1.4 开始运行服务](#.E5.BC.80.E5.A7.8B.E8.BF.90.E8.A1.8C.E6.9C.8D.E5.8A.A1)
    *   [2.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.2.1 Linux 上挂载](#Linux_.E4.B8.8A.E6.8C.82.E8.BD.BD)
            *   [2.2.1.1 /etc/fstab 设置](#.2Fetc.2Ffstab_.E8.AE.BE.E7.BD.AE)
            *   [2.2.1.2 Using autofs](#Using_autofs)
        *   [2.2.2 挂载源位于Windows系统](#.E6.8C.82.E8.BD.BD.E6.BA.90.E4.BD.8D.E4.BA.8EWindows.E7.B3.BB.E7.BB.9F)
        *   [2.2.3 Mounting from OS X](#Mounting_from_OS_X)
*   [3 Troubleshooting](#Troubleshooting)

## 安装

客户端和服务端都需要 [installation](/index.php/Pacman "Pacman") [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) 包。

**Note:** 建议在所有客户机和服务器上使用时间同步的守护进程（daemon），如果各个节点上没有精确的时钟，NFS 可能产生延时。

建议通过互联网同步服务端和客户端的时钟。

## 配置

### 服务端

#### ID mapping

编辑 `/etc/idmapd.conf` 设置 `Domain` 字段为你的域名。

 `/etc/idmapd.conf` 

```
[General]

Verbosity = 1
Pipefs-Directory = /var/lib/nfs/rpc_pipefs
Domain = atomic

[Mapping]

Nobody-User = nobody
Nobody-Group = nobody

```

#### 文件系统

**Note:** 基于安全原因，建议指定一个 NFS 输出的根（目录），来限制用户的可用挂载点。下面的例子践行此原则。

在 `/etc/exports` 里定义相对于 NFS 根目录的任意 NFS 共享。 在这个例子中，NFS 根目录为 `/srv/nfs4` 并且共享 `/mnt/music` 目录。

 `# mkdir -p /srv/nfs4/music` 

要想让客户端可以写入这个目录，确保 music 目录有读写权限。

挂载 `/mnt/music` 到 NFS 共享。 使用 mount 命令：

 `# mount --bind /mnt/music /srv/nfs4/music` 

为使服务器重启后仍然有效， 增加绑定到 `fstab` 文件:

 `/etc/fstab` 

```
/mnt/music /srv/nfs4/music  none   bind   0   0

```

#### Exports

增加允许被挂载的目录和主机到`exports`:

 `/etc/exports` 

```
/srv/nfs4/ 192.168.0.1/24(rw,fsid=0,no_subtree_check)
/srv/nfs4/music 192.168.0.1/24(rw,no_subtree_check,nohide) # note the nohide option which is applied to mounted directories on the file system.

```

不必共享给整个子网； 设置一个指定的IP地址也不错。

具体设置查看 `man exports` 。

**Note:** The `fsid=0` is required for the root file system being exported. `/srv/nfs4` is the NFS root here (due to the `fsid=0` entry). Everything else that you want to be shared over NFS must be accessible under `/srv/nfs4`. Setting an NFS root is required. For exporting directories outside the NFS root, see below.

更多可用选项 `man 5 exports`.

如果服务运行时修改了 `/etc/exports` 文件， 你需要重新导出使其生效。

 `# exportfs -ra` 

#### 开始运行服务

NFS 服务包括 `rpc-idmapd.service` 和 `rpc-mountd.service`

注意这些 units 会请求其它服务， 这些服务会被 [systemd](/index.php/Systemd "Systemd") 自动开启。

### 客户端

客户端需要 [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils)，但在连接 NFS4 服务器时无需其它步骤；

#### Linux 上挂载

显示指定服务器的共享：

 `$ showmount -e 服务器名或IP` 

然后按照普通方式挂载：

 `# mount -t nfs4 servername:/music /mountpoint/on/client` 

##### /etc/fstab 设置

在启动时自动挂载。编辑 `/etc/fstab` 文件，增加一行。

 `/etc/fstab` 

```
servername:/music   /mountpoint/on/client   nfs4   rsize=8192,wsize=8192,timeo=14,intr	0 0

```

一些实用的附加挂载选项：

*   `rsize=8192` 和 `wsize=8192`
*   `timeo=14`
*   `intr`

`rsize` 的值是从服务器读取的字节数。`wsize` 是写入到服务器的字节数。默认都是1024， 如果使用比较高的值，如8192,可以提高传输速度。 到底设到多少合适，还是自己测试吧。

The `timeo` value is the amount of time, in tenths of a second, to wait before resending a transmission after an RPC timeout. After the first timeout, the timeout value is doubled for each retry for a maximum of 60 seconds or until a major timeout occurs. If connecting to a slow server or over a busy network, better performance can be achieved by increasing this timeout value.

The `intr` option allows signals to interrupt the file operation if a major timeout occurs for a hard-mounted share.

##### Using autofs

Using [autofs](/index.php/Autofs "Autofs") is useful when multiple machines want to connect via NFS; they could both be clients as well as servers. The reason this method is preferable over the earlier one is that if the server is switched off, the client will not throw errors about being unable to find NFS shares. See [autofs#NFS network mounts](/index.php/Autofs#NFS_network_mounts "Autofs") for details.

#### 挂载源位于Windows系统

**Warning:** Serious performance issues may occur (it randomly takes 30-60 seconds to display a folder, 2 MB/s file copy speed on gigabit LAN, ...) to which Microsoft does not have a solution yet.[[1]](https://social.technet.microsoft.com/Forums/en-CA/w7itpronetworking/thread/40cc01e3-65e4-4bb6-855e-cef1364a60ac)

**Note:** Only the Ultimate and Enterprise editions of Windows 7 and the Enterprise edition of Windows 8 include "Client for NFS"

NFS shares can be mounted from windows if the "Client for NFS" service is actived (which it is not by default). To install the service go to "Programs and features" either through the control panel or by typing it in the search box from the start menu and click on "Turn Windows features on or off". Locate the "Services for NFS" and activate it as well as both subservices ("Administrative tools" and "Client for NFS").

Some global options can be set by opening the "Services for Network File System" (locate it with the search box) and right clicking on the client->properties.

**Warning:** Under Windows the share is addressed by its full path on the server, not just the path relative to the nfsroot! If in doubt run `showmount -e servername` from **cmd.exe**

#### Mounting from OS X

**Note:** OS X by default uses an insecure (>1024) port to mount a share.

Either export the share with the `insecure` flag, and mount using Finder:

`Go` > `Connect to Server` > `nfs://servername/`

Or, mount the share using a secure port using the terminal:

 `# sudo mount -t nfs -o resvport servername:/ /Volumes/servername/` 
**Warning:** Under OS X the share is addressed by its full path on the server, not just the path relative to the nfsroot! If in doubt run `showmount -e servername` from the terminal

## Troubleshooting

_There is a dedicated article [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting")._