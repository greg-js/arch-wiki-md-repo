## Contents

*   [1 目标](#.E7.9B.AE.E6.A0.87)
*   [2 必须的软件包](#.E5.BF.85.E9.A1.BB.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [3 安装服务器端](#.E5.AE.89.E8.A3.85.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AB.AF)
    *   [3.1 文件](#.E6.96.87.E4.BB.B6)
        *   [3.1.1 /etc/exports](#.2Fetc.2Fexports)
        *   [3.1.2 /etc/conf.d/nfs-common.conf](#.2Fetc.2Fconf.d.2Fnfs-common.conf)
    *   [3.2 守护进程](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
*   [4 设置客户端](#.E8.AE.BE.E7.BD.AE.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [4.1 文件](#.E6.96.87.E4.BB.B6_2)
        *   [4.1.1 /etc/conf.d/nfs-common.conf](#.2Fetc.2Fconf.d.2Fnfs-common.conf_2)
    *   [4.2 守护进程](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B_2)
    *   [4.3 Mounting](#Mounting)
    *   [4.4 使用 cifs 挂载](#.E4.BD.BF.E7.94.A8_cifs_.E6.8C.82.E8.BD.BD)
    *   [4.5 启动时自动挂载](#.E5.90.AF.E5.8A.A8.E6.97.B6.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
*   [5 疑难问题解决](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [5.1 failed to contact local rpcbind server](#failed_to_contact_local_rpcbind_server)
    *   [5.2 Unreliable performance, slow data transfer, and/or high load when using NFS and gigabit](#Unreliable_performance.2C_slow_data_transfer.2C_and.2For_high_load_when_using_NFS_and_gigabit)
    *   [5.3 Portmap daemon fails to start at boot](#Portmap_daemon_fails_to_start_at_boot)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 配置 NFS 固定端口](#.E9.85.8D.E7.BD.AE_NFS_.E5.9B.BA.E5.AE.9A.E7.AB.AF.E5.8F.A3)
*   [7 参考链接](#.E5.8F.82.E8.80.83.E9.93.BE.E6.8E.A5)

## 目标

这篇文档的目的是建立一个通过网络共享文件的nfs服务器。我们将尽可能的使其简单，容易理解。 **备注: 查看更多关于 [NFSv4](/index.php/NFSv4 "NFSv4") 的信息**

## 必须的软件包

服务器端和客户端所需要的软件包都是很少的。
你只需要安装:

*   core/portmap
*   core/nfs-utils

这两个软件包都在 [core] repository 中, 新的Arch会默认包含他们。

## 安装服务器端

现在你可以编辑配置文件（configuration），启动守护进程。需要以root身份运行以下命令。

### 文件

#### /etc/exports

这个文件(/ect/exports)定义了服务器端不同的共享，及其权限。
A few examples:

```
/files *(ro,sync) ; Read-only access to anyone
/files 192.168.0.100(rw,sync) ; Read-write access to a client on 192.168.0.100
/files 192.168.1.1/24(rw,sync) ;  Read-write access to all clients from 192.168.1.1 to 192.168.1.255

```

如果你在启动守护进程后修改了 /etc/exports，可以通过以下命令使其立即生效：

```
exportfs -r

```

如果希望NFS共享是公开(public)和可写(writable),可和 anonuid 选项，anongid 选项一起使用 all_squash 选项。 例如，给 nobody 组中的用户 nobody 设定优先级，可以：

```
; Read-write access to a client on 192.168.0.100, with rw access for the user 99 with gid 99
/files 192.168.0.100(rw,sync,all_squash,anonuid=99,anongid=99))

```

这也意味着，如果想对这个目录拥有写权限，nobody.nobody 必须是共享目录的所有者(owner)。

```
chown -R nobody.nobody /files

```

exports 文件的详细信息请参考 exports 的man page。

#### /etc/conf.d/nfs-common.conf

**注意:** 原来在 `/etc/conf.d/nfs` 的配置文件已经由 `/etc/conf.d/nfs-common.conf` 和 `/etc/conf.d/nfs-server.conf` 代替。

编辑这个文件以传递合适（appropriate）的运行选项给 nfsd, mountd, statd, 和 sm-notify。默认的 Arch NFS 初始化脚本(init scripts)要求 --no-notify 参数的 statd 选项，如下：

```
 STATD_OPTS="--no-notify"

```

其他的选项可采用默认，或者根据需要修改。 详细信息请参考相应的man pages。

### 守护进程

你可以用如下命令开启NFS服务程序:

```
/etc/rc.d/portmap start
/etc/rc.d/nfslock start
/etc/rc.d/nfsd start

```

请注意，必须按照如上顺序启动.
可以将portmap nfslock nfsd 依次加入到/etc/rc.conf的DAEMONS中以使NFS服务程序一开始就启动.

## 设置客户端

### 文件

#### /etc/conf.d/nfs-common.conf

编辑这个文件以传递合适（appropriate）的运行选项给 statd - 剩下的选项都是仅仅供服务器使用的。*不要*在客户端使用 --no-notify 选项，除非你完全意识到这样做的后果。

请参考 statd man page 获取详细信息。

### 守护进程

Start the portmap and nfslock daemons:

```
/etc/rc.d/portmap start
/etc/rc.d/nfslock start

```

Please note that they must be started in that order.
To start the daemons at boot time, add them to the DAEMONS array in /etc/rc.conf.

### Mounting

Then just mount as normal:

```
mount server:/files /files

```

Unlike CIFS shares or [rsync](/index.php/Rsync "Rsync"), NFS exports must be called by the full path on the server; example, if /home/fred/music is defined in /etc/exports on server ELROND, you must call:

```
mount ELROND:/home/fred/music /mnt/point

```

instead of just using:

```
mount ELROND:music /mnt/point

```

or you will get *mount.nfs: access denied by server while mounting*

**Note:** If you see the following message then you probably did not start the daemons from the [previous section](#Daemons) or something went wrong while starting them.
```
mount: wrong fs type, bad option, bad superblock on 192.168.1.99:/media/raid5-4tb,
       missing codepage or helper program, or other error
       (for several filesystems (e.g. nfs, cifs) you might
       need a /sbin/mount.<type> helper program)
       In some cases useful info is found in syslog - try
       dmesg | tail  or so

```

### 使用 cifs 挂载

Mounting the same share using cifs works a bit differently then using NFS. First, you need to have the share defined in Samba. For that look at the [Samba](/index.php/Samba "Samba") article. Lets say you made a share on "ELROND" with the name "music". To mount that share using cifs a command like the following should work

```
mount -t cifs -v ELROND:music /mnt/point -o guest,iocharset=utf8

```

You can try:

```
mount -t cifs -v ELROND:music /mnt/point

```

Or to login with a username and password:

```
mount -t cifs -v ELROND:music /mnt/point -o username=USERNAME,password=PASSWORD,iocharset=utf8

```

More information for this can be found in the [manual mounting](/index.php/Samba#Manual_share_mounting "Samba") section of [samba](/index.php/Samba "Samba"). Now you have effectively made 1 folder accessible for NFS clients (mostly linux) and CIFS clients (mostly windows).

### 启动时自动挂载

欲使网络文件夹在启动时自动挂载，须确保netfs在**/etc/rc.conf**的**DAEMONS**行中，且在**/etc/fstab** 中有相应设置，例如:

```
server:/files /files nfs defaults 0 0

```

如果你要指定读写数据包的大小，可以在fstab中设置。如下所列数据为默认值:

```
server:/files /files nfs rsize=32768,wsize=32768 0 0

```

**man nfs** 以获取更多信息，包括可用的挂载选项等.

## 疑难问题解决

### failed to contact local rpcbind server

表现在挂载到时候，出现“无法链接到本地rpcbind服务器”，错误号是512。具体错误信息如下：

```
rpcbind: server localhost not responding, timed out
RPC: failed to contact local rpcbind server (errno 5) .
rpcbind: server localhost not responding, timed out
RPC: failed to contact local rpcbind server (errno 5).
lockd_up: makesock failed, error=-5
^CRPC: failed to contact local rpcbind server (errno 512).

```

解决方法，在挂载的时候，加上-o nolock 参数即可。

### Unreliable performance, slow data transfer, and/or high load when using NFS and gigabit

This is a result of the default packetsize used by NFS, which causes significant fragmentation on gigabit networks. You can modify this behavior by the rsize and wsize mount parameters. Using rsize=32768,wsize=32768 should suffice. Please note that this problem does not occur on 100Mb networks, due to the lower packet transfer speed.

**注意:** NFSv4 的默认值是32768。最大可以取65536\. Increase from default in increments of 1024 until maximum transfer rate is achieved.

### Portmap daemon fails to start at boot

Make sure you place portmap BEFORE netfs in the daemons array in /etc/rc.conf .

## Tips and tricks

### 配置 NFS 固定端口

如果你有一个基于端口的防火墙，你也许想设置一个固定的端口。对于 rpc.statd 和 rpc.mountd 你应该在 `/etc/conf.d/nfs-common` 中 `/etc/conf.d/nfs-server` 按照如下设置 (端口可以与下面不同)：

 `/etc/conf.d/nfs-common`  `STATD_OPTS="-p 4000 -o 4003"`  `/etc/conf.d/nfs-server`  `MOUNTD_OPTS="--no-nfs-version 2 -p 4002"`  `/etc/modprobe.d/lockd.conf` 
```
# Static ports for NFS lockd
options lockd nlm_udpport=4001 nlm_tcpport=4001
```

之后重启 nfs 守护进程，然后重新载入 lockd 模块：

```
# modprobe -r lockd 
# modprobe lockd 
# rc.d restart nfs-common nfs-server
```

重启 nfs 守护进程和重新载入 lockd 模块之后，你可以使用以下命令检查使用的端口：

 `$ rpcinfo -p` 
```
rpcinfo -p
   program vers proto   port  service
    100000    4   tcp    111  portmapper
    100000    3   tcp    111  portmapper
    100000    2   tcp    111  portmapper
    100000    4   udp    111  portmapper
    100000    3   udp    111  portmapper
    100000    2   udp    111  portmapper
    100024    1   udp   4000  status
    100024    1   tcp   4000  status
    100021    1   udp   4001  nlockmgr
    100021    3   udp   4001  nlockmgr
    100021    4   udp   4001  nlockmgr
    100021    1   tcp   4001  nlockmgr
    100021    3   tcp   4001  nlockmgr
    100021    4   tcp   4001  nlockmgr
    100003    2   tcp   2049  nfs
    100003    3   tcp   2049  nfs
    100003    4   tcp   2049  nfs
    100003    2   udp   2049  nfs
    100003    3   udp   2049  nfs
    100003    4   udp   2049  nfs
    100005    3   udp   4002  mountd
    100005    3   tcp   4002  mountd
```

然后，你需要打开端口 111-2049-4000-4001-4002-4003 的 tcp 和 udp.

## 参考链接

*   参见 [Avahi](/index.php/Avahi "Avahi"), 一个零配置的实现，允许自动发现 NFS 共享。
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [非常有用](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)
*   如果你配置 Archlinux NFS 服务器供 Windows 客户端通过 Microsoft's SFU 使用，你可以查看这里来节约时间和避免细节的配置问题[this forum post](https://bbs.archlinux.org/viewtopic.php?pid=523934#p523934) 。
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [Unix interoperability and Windows Vista](http://blogs.msdn.com/sfu/archive/2007/05/01/unix-interoperability-and-windows-vista.aspx) Prerequisites to connect to NFS with Vista