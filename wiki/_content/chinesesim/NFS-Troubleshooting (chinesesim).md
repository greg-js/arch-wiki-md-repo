**翻译状态：** 本文是英文页面 [NFS/Troubleshooting](/index.php/NFS/Troubleshooting "NFS/Troubleshooting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-17，点击[这里](https://wiki.archlinux.org/index.php?title=NFS%2FTroubleshooting&diff=0&oldid=449910)可以查看翻译后英文页面的改动。

本篇专述共性问题及其解决方案。

## Contents

*   [1 服务器端问题](#.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AB.AF.E9.97.AE.E9.A2.98)
    *   [1.1 exportfs: /etc/exports:2: syntax error: bad option list](#exportfs:_.2Fetc.2Fexports:2:_syntax_error:_bad_option_list)
    *   [1.2 Group/GID 权限问题](#Group.2FGID_.E6.9D.83.E9.99.90.E9.97.AE.E9.A2.98)
    *   [1.3 尝试以root身份写入文件时报“权限被拒绝("Permission denied")”](#.E5.B0.9D.E8.AF.95.E4.BB.A5root.E8.BA.AB.E4.BB.BD.E5.86.99.E5.85.A5.E6.96.87.E4.BB.B6.E6.97.B6.E6.8A.A5.E2.80.9C.E6.9D.83.E9.99.90.E8.A2.AB.E6.8B.92.E7.BB.9D.28.22Permission_denied.22.29.E2.80.9D)
    *   [1.4 showmount -e 命令报错："RPC: Program not registered"](#showmount_-e_.E5.91.BD.E4.BB.A4.E6.8A.A5.E9.94.99.EF.BC.9A.22RPC:_Program_not_registered.22)
*   [2 客户端问题](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.97.AE.E9.A2.98)
    *   [2.1 mount.nfs4: No such device](#mount.nfs4:_No_such_device)
    *   [2.2 mount.nfs4: access denied by server while mounting](#mount.nfs4:_access_denied_by_server_while_mounting)
    *   [2.3 不能连接到 OS X 客户端](#.E4.B8.8D.E8.83.BD.E8.BF.9E.E6.8E.A5.E5.88.B0_OS_X_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.4 Unreliable connection from OS X clients](#Unreliable_connection_from_OS_X_clients)
    *   [2.5 拷贝大文件时客户端似乎卡住了](#.E6.8B.B7.E8.B4.9D.E5.A4.A7.E6.96.87.E4.BB.B6.E6.97.B6.E5.AE.A2.E6.88.B7.E7.AB.AF.E4.BC.BC.E4.B9.8E.E5.8D.A1.E4.BD.8F.E4.BA.86)
    *   [2.6 mount.nfs: Operation not permitted](#mount.nfs:_Operation_not_permitted)
    *   [2.7 mount.nfs: Protocol not supported](#mount.nfs:_Protocol_not_supported)
    *   [2.8 Problems with Vagrant and synced_folders](#Problems_with_Vagrant_and_synced_folders)
*   [3 性能问题](#.E6.80.A7.E8.83.BD.E9.97.AE.E9.A2.98)
    *   [3.1 诊断问题原因](#.E8.AF.8A.E6.96.AD.E9.97.AE.E9.A2.98.E5.8E.9F.E5.9B.A0)
    *   [3.2 Server threads](#Server_threads)
    *   [3.3 Close-to-open/flush-on-close](#Close-to-open.2Fflush-on-close)
        *   [3.3.1 The nocto mount option](#The_nocto_mount_option)
        *   [3.3.2 The async export option](#The_async_export_option)
    *   [3.4 缓冲区大小与 MTU](#.E7.BC.93.E5.86.B2.E5.8C.BA.E5.A4.A7.E5.B0.8F.E4.B8.8E_MTU)
*   [4 调试](#.E8.B0.83.E8.AF.95)
    *   [4.1 使用rpcdebug](#.E4.BD.BF.E7.94.A8rpcdebug)
    *   [4.2 Using mountstats](#Using_mountstats)
    *   [4.3 内核接口](#.E5.86.85.E6.A0.B8.E6.8E.A5.E5.8F.A3)
    *   [4.4 NFSD debug flags](#NFSD_debug_flags)
    *   [4.5 NFS debug flags](#NFS_debug_flags)
    *   [4.6 NLM debug flags](#NLM_debug_flags)
    *   [4.7 RPC debug flags](#RPC_debug_flags)
    *   [4.8 General Notes](#General_Notes)
    *   [4.9 References](#References)
*   [5 其它问题](#.E5.85.B6.E5.AE.83.E9.97.AE.E9.A2.98)
    *   [5.1 权限问题](#.E6.9D.83.E9.99.90.E9.97.AE.E9.A2.98)

## 服务器端问题

### exportfs: /etc/exports:2: syntax error: bad option list

请将`/etc/exports`文件里选项列表定义中的所有空格都删除

### Group/GID 权限问题

如果挂载NFS共享正常，所有者也可以完全访问，但同组用户无法访问，请检查该所有者用户所属用户组的数量。NFS限制每个用户最多只能归属于16个用户组。如果某用户超出了这个限度，请在NFS服务器上为`rpc.mountd`进程启用`--manage-gids`启动标志。

 `/etc/conf.d/nfs-server.conf` 
```
# Options for rpc.mountd.
# If you have a port-based firewall, you might want to set up
# a fixed port here using the --port option.
# See rpc.mountd(8) for more details.

MOUNTD_OPTS="--manage-gids"
```

### 尝试以root身份写入文件时报“权限被拒绝("Permission denied")”

*   如果需要以root身份挂载共享并在客户端获得全部读写权限，请在`/etc/exports`文件中添加**no_root_squash**选项：

```
/var/cache/pacman/pkg 192.168.1.0/24(rw,no_subtree_check,no_root_squash)

```

*   同时也必须在`/etc/exports`文件的第一行添加**no_root_squash**：

```
/ 192.168.1.0/24(rw,fsid=root,no_root_squash,no_subtree_check)

```

### showmount -e 命令报错："RPC: Program not registered"

请确保服务器端`nfs-server.service`和`rpcbind.service`两个服务已运行。参阅[systemd](/index.php/Systemd "Systemd")。

## 客户端问题

### mount.nfs4: No such device

检查是否加载了`nfs`模块

```
lsmod | grep nfs

```

如果上述命令输出为空或仅有 nfsd-stuff，运行：

```
# modprobe nfs

```

### mount.nfs4: access denied by server while mounting

NFS shares have to reside in /srv - check your `/etc/exports` file and if necessary create the proper folder structure as described in the [NFS#File system](/index.php/NFS#File_system "NFS") page.

Check that the permissions on your client's folder are correct. Try using 755.

or try "exportfs -rav" reload `/etc/exports` file.

### 不能连接到 OS X 客户端

When trying to connect from a OS X client, you will see that everything is ok at logs, but MacOS X refuses to mount your NFS share. You have to add `insecure` option to your share and re-run `exportfs -r`.

### Unreliable connection from OS X clients

OS X's NFS client is optimized for OS X Servers and might present some issues with Linux servers. If you are experiencing slow performance, frequent disconnects and problems with international characters edit the default mount options by adding the line `nfs.client.mount.options = intr,locallocks,nfc` to `/etc/nfs.conf` on your Mac client. More information about the mount options can be found [here](https://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man8/mount_nfs.8.html#//apple_ref/doc/man/8/mount_nfs).

### 拷贝大文件时客户端似乎卡住了

从客户端向 NFS 服务器拷贝大文件时，传输速度极快，但若干秒钟后速度掉下来了，客户端似乎完全被锁住一段时间直至传输结束。

试试在客户端挂载时增加 <tt>sync</tt> 选项（例如在 <tt>/etc/fstab</tt> 中）以修复此问题。

### mount.nfs: Operation not permitted

After updating to *nfs-utils* 1.2.1-2 or higher, mounting NFS shares stopped working. Henceforth, *nfs-utils* uses NFSv4 per default instead of NFSv3\. The problem can be solved by using either mount option `'vers=3'` or `'nfsvers=3'` on the command line:

```
# mount.nfs *remote target* *directory* -o ...,vers=3,...
# mount.nfs *remote target* *directory* -o ...,nfsvers=3,...

```

or in `/etc/fstab`:

```
*remote target* *directory* nfs ...,vers=3,... 0 0
*remote target* *directory* nfs ...,nfsvers=3,... 0 0

```

### mount.nfs: Protocol not supported

Check you are not mounting including the export root. Use:

```
# mount SERVER:/ /mnt

```

instead of, i.e.:

```
# mount SERVER:/srv/nfs4/ /mnt

```

Sometimes it could be the same problem with "Operation not permitted" : *nfs-utils* uses NFSv4 per default instead of NFSv3\. Go and see the previons section

### Problems with Vagrant and synced_folders

If Vagrant scripts are unable to mount folders over NFS, installing the *net-tools* package may solve the issue.

## 性能问题

This [NFS Howto page](http://nfs.sourceforge.net/nfs-howto/ar01s05.html) has some useful information regarding performance. Here are some further tips:

### 诊断问题原因

*   推荐首选 **Htop** 作为诊断工具。大部分明显症状会表现为占满CPU。
*   按 F2 键，在“显示选项(Display options)”下启用“详细CPU时间(Detailed CPU time)”。按 F1 键查看 CPU 图示中各种颜色的含义。特别要查看 CPU 的 IRQs 或 Wait-IO(wio) 响应时间。

### Server threads

**Symptoms:** Nothing seems to be very heavily loaded, but some operations on the client take a long time to complete for no apparent reason.

If your workload involves lots of small reads and writes (or if there are a lot of clients), there may not be enough threads running on the server to handle the quantity of queries. To check if this is the case, run the following command on one or more of the clients:

 `# nfsstat -rc` 
```
Client rpc stats:
calls      retrans    authrefrsh
113482     0          113484

```

If the `retrans` column contains a number larger than 0, the server is failing to respond to some NFS requests, and the number of threads should be increased.

To increase the number of threads on the server, edit the file `/etc/conf.d/nfs-server.conf` and set the value in the `NFSD_OPTS` variable. For example, to set the number of threads to 32:

 `/etc/conf.d/nfs-server.conf` 
```
NFSD_OPTS="32"

```

The default number of threads is 8\. Try doubling this number until `retrans` remains consistently at zero. Don't be afraid of increasing the number quite substantially. 256 threads may be quite reasonable, depending on the workload. You will need to restart the NFS server daemon each time you modify the configuration file. Bear in mind that the client statistics will only be reset to zero when the client is rebooted.

Use **htop** (disable the hiding of kernel threads) to keep an eye on how much work each nfsd thread is doing. If you reach a point where the `retrans` values are non-zero, but you can see `nfsd` threads on the server doing no work, something different is now causing your bottleneck, and you'll need to re-diagnose this new problem.

### Close-to-open/flush-on-close

**Symptoms:** Your clients are writing many small files. The server CPU is not maxed out, but there is very high wait-IO, and the server disk seems to be churning more than you might expect.

In order to ensure data consistency across clients, the NFS protocol requires that the client's cache is flushed (all data is pushed to the server) whenever a file is closed after writing. Because the server is not allowed to buffer disk writes (if it crashes, the client won't realise the data wasn't written properly), the data is written to disk immediately before the client's request is completed. When you're writing lots of small files from the client, this means that the server spends most of its time waiting for small files to be written to its disk, which can cause a significant reduction in throughput.

See [this excellent article](http://docstore.mik.ua/orelly/networking_2ndEd/nfs/ch07_04.htm) or the **nfs** manpage for more details on the close-to-open policy. There are several approaches to solving this problem:

#### The nocto mount option

**Note:** The linux kernel does not seem to honour this option properly. Files are still flushed when they're closed.

Does your situation match these conditions?

*   The export you have mounted on the client is only going to be used by the one client.
*   It doesn't matter too much if a file written on one client doesn't immediately appear on other clients.
*   It doesn't matter if after a client has written a file, and the client thinks the file has been saved, and then the client crashes, the file may be lost.

If you're happy with the above conditions, you can use the **nocto** mount option, which will disable the close-to-open behaviour. See the **nfs** manpage for details.

#### The async export option

Does your situation match these conditions?

*   It's important that when a file is closed after writing on one client, it is:
    *   Immediately visible on all the other clients.
    *   Safely stored on the server, even if the client crashes immediately after closing the file.
*   It's not important to you that if the server crashes:
    *   You may loose the files that were most recently written by clients.
    *   When the server is restarted, the clients will believe their recent files exist, even though they were actually lost.

In this situation, you can use `async` instead of `sync` in the server's `/etc/exports` file for those specific exports. See the **exports** manual page for details. In this case, it does not make sense to use the `nocto` mount option on the client.

### 缓冲区大小与 MTU

**Symptoms:** High kernel or IRQ CPU usage, a very high packet count through the network card.

This is a trickier optimisation. Make sure this is definitely the problem before spending too much time on this. The default values are usually fine for most situations.

See [this excellent article](http://docstore.mik.ua/orelly/networking_2ndEd/nfs/ch07_03.htm) for information about I/O buffering in NFS. Essentially, data is accumulated into buffers before being sent. The size of the buffer will affect the way data is transmitted over the network. The Maximum Transmission Unit (MTU) of the network equipment will also affect throughput, as the buffers need to be split into MTU-sized chunks before they're sent over the network. If your buffer size is too big, the kernel or hardware may spend too much time splitting it into MTU-sized chunks. If the buffer size is too small, there will be overhead involved in sending a very large number of small packets. You can use the **rsize** and **wsize** mount options on the client to alter the buffer cache size. To achieve the best throughput, you need to experiment and discover the best values for your setup.

It is possible to change the MTU of many network cards. If your clients are on a separate subnet (e.g. for a Beowulf cluster), it may be safe to configure all of the network cards to use a high MTU. This should be done in very-high-bandwidth environments.

See also the **nfs** manual page for more about **rsize** and **wsize**.

## 调试

### 使用rpcdebug

Using `rpcdebug` is the easiest way to manipulate the kernel interfaces in place of echoing bitmasks to /proc.

| Option | Description |
| -c | Clear the given debug flags |
| -s | Set the given debug flags |
| -m *module* | Specify which module's flags to set or clear. |
| -v | Increase the verbosity of rpcdebug's output |
| -h | Print a help message and exit. When combined with the -v option, also prints the available debug flags. |

For the **-m** option, the available modules are:

| Module | Description |
| nfsd | The NFS server |
| nfs | The NFS client |
| nlm | The Network Lock Manager, in either an NFS client or server |
| rpc | The Remote Procedure Call module, in either an NFS client or server |

Examples:

```
rpcdebug -m rpc -s all    # sets all debug flags for RPC
rpcdebug -m rpc -c all    # clears all debug flags for RPC

rpcdebug -m nfsd -s all   # sets all debug flags for NFS Server
rpcdebug -m nfsd -c all   # clears all debug flags for NFS Server

```

Once the flags are set you can tail the journal for the debug output, usually `journalctl -fl` or similar.

### Using mountstats

The [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) package contains the `mountstats` tool, which can retrieve a lot of statistics about NFS mounts, including average timings and packet size.

```
$ mountstats 
Stats for example:/tank mounted on /tank:
  NFS mount options: rw,sync,vers=4.2,rsize=524288,wsize=524288,namlen=255,acregmin=3,acregmax=60,acdirmin=30,acdirmax=60,soft,proto=tcp,port=0,timeo=15,retrans=2,sec=sys,clientaddr=xx.yy.zz.tt,local_lock=none
  NFS server capabilities: caps=0xfbffdf,wtmult=512,dtsize=32768,bsize=0,namlen=255
  NFSv4 capability flags: bm0=0xfdffbfff,bm1=0x40f9be3e,bm2=0x803,acl=0x3,sessions,pnfs=notconfigured
  NFS security flavor: 1  pseudoflavor: 0

NFS byte counts:
  applications read 248542089 bytes via read(2)
  applications wrote 0 bytes via write(2)
  applications read 0 bytes via O_DIRECT read(2)
  applications wrote 0 bytes via O_DIRECT write(2)
  client read 171375125 bytes via NFS READ
  client wrote 0 bytes via NFS WRITE

RPC statistics:
  699 RPC requests sent, 699 RPC replies received (0 XIDs not found)
  average backlog queue length: 0

READ:
	338 ops (48%) 
	avg bytes sent per op: 216	avg bytes received per op: 507131
	backlog wait: 0.005917 	RTT: 548.736686 	total execute time: 548.775148 (milliseconds)
GETATTR:
	115 ops (16%) 
	avg bytes sent per op: 199	avg bytes received per op: 240
	backlog wait: 0.008696 	RTT: 15.756522 	total execute time: 15.843478 (milliseconds)
ACCESS:
	93 ops (13%) 
	avg bytes sent per op: 203	avg bytes received per op: 168
	backlog wait: 0.010753 	RTT: 2.967742 	total execute time: 3.032258 (milliseconds)
LOOKUP:
	32 ops (4%) 
	avg bytes sent per op: 220	avg bytes received per op: 274
	backlog wait: 0.000000 	RTT: 3.906250 	total execute time: 3.968750 (milliseconds)
OPEN_NOATTR:
	25 ops (3%) 
	avg bytes sent per op: 268	avg bytes received per op: 350
	backlog wait: 0.000000 	RTT: 2.320000 	total execute time: 2.360000 (milliseconds)
CLOSE:
	24 ops (3%) 
	avg bytes sent per op: 224	avg bytes received per op: 176
	backlog wait: 0.000000 	RTT: 30.250000 	total execute time: 30.291667 (milliseconds)
DELEGRETURN:
	23 ops (3%) 
	avg bytes sent per op: 220	avg bytes received per op: 160
	backlog wait: 0.000000 	RTT: 6.782609 	total execute time: 6.826087 (milliseconds)
READDIR:
	4 ops (0%) 
	avg bytes sent per op: 224	avg bytes received per op: 14372
	backlog wait: 0.000000 	RTT: 198.000000 	total execute time: 198.250000 (milliseconds)
SERVER_CAPS:
	2 ops (0%) 
	avg bytes sent per op: 172	avg bytes received per op: 164
	backlog wait: 0.000000 	RTT: 1.500000 	total execute time: 1.500000 (milliseconds)
FSINFO:
	1 ops (0%) 
	avg bytes sent per op: 172	avg bytes received per op: 164
	backlog wait: 0.000000 	RTT: 2.000000 	total execute time: 2.000000 (milliseconds)
PATHCONF:
	1 ops (0%) 
	avg bytes sent per op: 164	avg bytes received per op: 116
	backlog wait: 0.000000 	RTT: 1.000000 	total execute time: 1.000000 (milliseconds)

```

### 内核接口

A bitmask of the debug flags can be echoed into the interface to enable output to syslog; 0 is the default:

```
/proc/sys/sunrpc/nfsd_debug
/proc/sys/sunrpc/nfs_debug
/proc/sys/sunrpc/nlm_debug
/proc/sys/sunrpc/rpc_debug

```

Sysctl controls are registered for these interfaces, so they can be used instead of echo:

```
sysctl -w sunrpc.rpc_debug=1023
sysctl -w sunrpc.rpc_debug=0

sysctl -w sunrpc.nfsd_debug=1023
sysctl -w sunrpc.nfsd_debug=0
```

At runtime the server holds information that can be examined:

```
grep . /proc/net/rpc/*/content
cat /proc/fs/nfs/exports
cat /proc/net/rpc/nfsd
ls -l /proc/fs/nfsd

```

A rundown of `/proc/net/rpc/nfsd` (the userspace tool `nfsstat` pretty-prints this info):

```
* rc (reply cache): <hits> <misses> <nocache>
- hits: client it's retransmitting
- misses: a operation that requires caching
- nocache: a operation that no requires caching

* fh (filehandle): <stale> <total-lookups> <anonlookups> <dir-not-in-cache> <nodir-not-in-cache>
- stale: file handle errors
- total-lookups, anonlookups, dir-not-in-cache, nodir-not-in-cache
  . always seem to be zeros

* io (input/output): <bytes-read> <bytes-written>
- bytes-read: bytes read directly from disk
- bytes-written: bytes written to disk

* th (threads): <threads> <fullcnt> <10%-20%> <20%-30%> ... <90%-100%> <100%>
- threads: number of nfsd threads
- fullcnt: number of times that the last 10% of threads are busy
- 10%-20%, 20%-30% ... 90%-100%: 10 numbers representing 10-20%, 20-30% to 100%
  . Counts the number of times a given interval are busy

* ra (read-ahead): <cache-size> <10%> <20%> ... <100%> <not-found>
- cache-size: always the double of number threads
- 10%, 20% ... 100%: how deep it found what was looking for
- not-found: not found in the read-ahead cache

* net: <netcnt> <netudpcnt> <nettcpcnt> <nettcpconn>
- netcnt: counts every read
- netudpcnt: counts every UDP packet it receives
- nettcpcnt: counts every time it receives data from a TCP connection
- nettcpconn: count every TCP connection it receives

* rpc: <rpccnt> <rpcbadfmt+rpcbadauth+rpcbadclnt> <rpcbadfmt> <rpcbadauth> <rpcbadclnt>
- rpccnt: counts all rpc operations
- rpcbadfmt: counts if while processing a RPC it encounters the following errors:
  . err_bad_dir, err_bad_rpc, err_bad_prog, err_bad_vers, err_bad_proc, err_bad
- rpcbadauth: bad authentication
  . does not count if you try to mount from a machine that it's not in your exports file
- rpcbadclnt: unused

* procN (N = vers): <vs_nproc> <null> <getattr> <setattr> <lookup> <access> <readlink> <read> <write> <create> <mkdir> <symlink> <mknod> <remove> <rmdir> <rename> <link> <readdir> <readdirplus> <fsstat> <fsinfo> <pathconf> <commit>
- vs_nproc: number of procedures for NFS version
  . v2: nfsproc.c, 18
  . v3: nfs3proc.c, 22
  - v4, nfs4proc.c, 2
- statistics: generated from NFS operations at runtime

* proc4ops: <ops> <x..y>
- ops: the definition of LAST_NFS4_OP, OP_RELEASE_LOCKOWNER = 39, plus 1 (so 40); defined in nfs4.h
- x..y: the array of nfs_opcount up to LAST_NFS4_OP (nfsdstats.nfs4_opcount[i])
```

### NFSD debug flags

 `/usr/include/linux/nfsd/debug.h` 
```
/*
 * knfsd debug flags
 */
#define NFSDDBG_SOCK            0x0001
#define NFSDDBG_FH              0x0002
#define NFSDDBG_EXPORT          0x0004
#define NFSDDBG_SVC             0x0008
#define NFSDDBG_PROC            0x0010
#define NFSDDBG_FILEOP          0x0020
#define NFSDDBG_AUTH            0x0040
#define NFSDDBG_REPCACHE        0x0080
#define NFSDDBG_XDR             0x0100
#define NFSDDBG_LOCKD           0x0200
#define NFSDDBG_ALL             0x7FFF
#define NFSDDBG_NOCHANGE        0xFFFF
```

### NFS debug flags

 `/usr/include/linux/nfs_fs.h` 
```
/*
 * NFS debug flags
 */
#define NFSDBG_VFS              0x0001
#define NFSDBG_DIRCACHE         0x0002
#define NFSDBG_LOOKUPCACHE      0x0004
#define NFSDBG_PAGECACHE        0x0008
#define NFSDBG_PROC             0x0010
#define NFSDBG_XDR              0x0020
#define NFSDBG_FILE             0x0040
#define NFSDBG_ROOT             0x0080
#define NFSDBG_CALLBACK         0x0100
#define NFSDBG_CLIENT           0x0200
#define NFSDBG_MOUNT            0x0400
#define NFSDBG_FSCACHE          0x0800
#define NFSDBG_PNFS             0x1000
#define NFSDBG_PNFS_LD          0x2000
#define NFSDBG_STATE            0x4000
#define NFSDBG_ALL              0xFFFF
```

### NLM debug flags

 `/usr/include/linux/lockd/debug.h` 
```
/*
 * Debug flags
 */
#define NLMDBG_SVC		0x0001
#define NLMDBG_CLIENT		0x0002
#define NLMDBG_CLNTLOCK		0x0004
#define NLMDBG_SVCLOCK		0x0008
#define NLMDBG_MONITOR		0x0010
#define NLMDBG_CLNTSUBS		0x0020
#define NLMDBG_SVCSUBS		0x0040
#define NLMDBG_HOSTCACHE	0x0080
#define NLMDBG_XDR		0x0100
#define NLMDBG_ALL		0x7fff
```

### RPC debug flags

 `/usr/include/linux/sunrpc/debug.h` 
```
/*
 * RPC debug facilities
 */
#define RPCDBG_XPRT             0x0001
#define RPCDBG_CALL             0x0002
#define RPCDBG_DEBUG            0x0004
#define RPCDBG_NFS              0x0008
#define RPCDBG_AUTH             0x0010
#define RPCDBG_BIND             0x0020
#define RPCDBG_SCHED            0x0040
#define RPCDBG_TRANS            0x0080
#define RPCDBG_SVCXPRT          0x0100
#define RPCDBG_SVCDSP           0x0200
#define RPCDBG_MISC             0x0400
#define RPCDBG_CACHE            0x0800
#define RPCDBG_ALL              0x7fff
```

### General Notes

*   While the number of threads can be increased at runtime via an echo to `/proc/fs/nfsd/threads`, the cache size (double the threads, see the **ra** line of /proc/net/rpc/nfsd) is not dynamic. The NFS daemon must be restarted with the new thread size during initialization in order for the thread cache to properly adjust.

### References

*   [https://github.com/torvalds/linux/tree/master/include/linux](https://github.com/torvalds/linux/tree/master/include/linux)
*   [http://linux.die.net/man/8/rpcdebug](http://linux.die.net/man/8/rpcdebug)
*   [http://utcc.utoronto.ca/~cks/space/blog/linux/NFSClientDebuggingBits](http://utcc.utoronto.ca/~cks/space/blog/linux/NFSClientDebuggingBits)
*   [http://www.novell.com/support/kb/doc.php?id=7011571](http://www.novell.com/support/kb/doc.php?id=7011571)
*   [http://stromberg.dnsalias.org/~strombrg/NFS-troubleshooting-2.html](http://stromberg.dnsalias.org/~strombrg/NFS-troubleshooting-2.html)
*   [http://www.opensubscriber.com/message/nfs@lists.sourceforge.net/7833588.html](http://www.opensubscriber.com/message/nfs@lists.sourceforge.net/7833588.html)

## 其它问题

### 权限问题

如果发现文件权限无法按需设置成功，请确认在客户端和服务器端同时修改了用户/组权限。

如果所有文件的属主都是 `nobody` 并且使用了 NFSv4，请在客户端和服务器端同时做到：

*   在使用 systemd 时，确认 `nfs-idmapd` 服务已启动。
*   在使用初始化脚本（initscripts）时，确认`/etc/conf.d/nfs-common.conf` 文件中的 `NEED_IDMAPD` 选项已设置为 `YES`。

某些系统在侦测“FQDN-主机名”这种格式时似乎工作不正常。On some systems detecting the domain from FQDN minus hostname does not seem to work reliably. 如果经过上述更正以后文件仍然显示属主为 `nobody`， 请编辑 /etc/idmapd.conf 文件，确认 `Domain` 选项已设置为 `FQDN-主机名` 形式。例如：

 `/etc/idmapd.conf` 
```
[General]

Verbosity = 7
Pipefs-Directory = /var/lib/nfs/rpc_pipefs
Domain = yourdomain.local

[Mapping]

Nobody-User = nobody
Nobody-Group = nobody

[Translation]

Method = nsswitch
```

如果 nfs-idmapd.service 因无法打开 Pipefs-directory 而拒绝启动，请创建 /etc/idmapd.conf 并添加 '/nfs'，然后重启守护进程。