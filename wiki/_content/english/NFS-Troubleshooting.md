Related articles

*   [NFS](/index.php/NFS "NFS")

Dedicated article for common problems and solutions.

## Contents

*   [1 Server-side issues](#Server-side_issues)
    *   [1.1 exportfs: /etc/exports:2: syntax error: bad option list](#exportfs:_.2Fetc.2Fexports:2:_syntax_error:_bad_option_list)
    *   [1.2 Group/GID permissions issues](#Group.2FGID_permissions_issues)
    *   [1.3 "Permission denied" when trying to write files as root](#.22Permission_denied.22_when_trying_to_write_files_as_root)
    *   [1.4 "RPC: Program not registered" when showmount -e command issued](#.22RPC:_Program_not_registered.22_when_showmount_-e_command_issued)
*   [2 Client-side issues](#Client-side_issues)
    *   [2.1 mount.nfs4: No such device](#mount.nfs4:_No_such_device)
    *   [2.2 mount.nfs4: access denied by server while mounting](#mount.nfs4:_access_denied_by_server_while_mounting)
    *   [2.3 mount.nfs4: Invalid argument](#mount.nfs4:_Invalid_argument)
    *   [2.4 Unable to connect from OS X clients](#Unable_to_connect_from_OS_X_clients)
    *   [2.5 Unreliable connection from OS X clients](#Unreliable_connection_from_OS_X_clients)
    *   [2.6 Intermittent client freezes when copying large files](#Intermittent_client_freezes_when_copying_large_files)
    *   [2.7 mount.nfs: Operation not permitted](#mount.nfs:_Operation_not_permitted)
        *   [2.7.1 NFSv4](#NFSv4)
        *   [2.7.2 NFSv3 and earlier](#NFSv3_and_earlier)
    *   [2.8 mount.nfs: Protocol not supported](#mount.nfs:_Protocol_not_supported)
    *   [2.9 Problems with Vagrant and synced_folders](#Problems_with_Vagrant_and_synced_folders)
*   [3 Performance issues](#Performance_issues)
    *   [3.1 Diagnose the problem](#Diagnose_the_problem)
    *   [3.2 Server threads](#Server_threads)
    *   [3.3 Close-to-open/flush-on-close](#Close-to-open.2Fflush-on-close)
        *   [3.3.1 The nocto mount option](#The_nocto_mount_option)
        *   [3.3.2 The async export option](#The_async_export_option)
    *   [3.4 Buffer cache size and MTU](#Buffer_cache_size_and_MTU)
*   [4 Debugging](#Debugging)
    *   [4.1 Using rpcdebug](#Using_rpcdebug)
    *   [4.2 Using mountstats](#Using_mountstats)
    *   [4.3 Kernel Interfaces](#Kernel_Interfaces)
    *   [4.4 NFSD debug flags](#NFSD_debug_flags)
    *   [4.5 NFS debug flags](#NFS_debug_flags)
    *   [4.6 NLM debug flags](#NLM_debug_flags)
    *   [4.7 RPC debug flags](#RPC_debug_flags)
    *   [4.8 General Notes](#General_Notes)
    *   [4.9 References](#References)
*   [5 Other issues](#Other_issues)
    *   [5.1 Permissions issues](#Permissions_issues)

## Server-side issues

### exportfs: /etc/exports:2: syntax error: bad option list

Delete all space from the option list in `/etc/exports`

### Group/GID permissions issues

If NFS shares mount fine, and are fully accessible to the owner, but not to group members; check the number of groups that user belongs to. NFS has a limit of 16 on the number of groups a user can belong to. If you have users with more than this, you need to enable the `--manage-gids` start-up flag for `rpc.mountd` on the NFS server.

 `/etc/conf.d/nfs-server.conf` 
```
# Options for rpc.mountd.
# If you have a port-based firewall, you might want to set up
# a fixed port here using the --port option.
# See rpc.mountd(8) for more details.

MOUNTD_OPTS="--manage-gids"
```

### "Permission denied" when trying to write files as root

*   If you need to mount shares as root, and have full r/w access from the client, add the no_root_squash option to the export in `/etc/exports`:

```
/var/cache/pacman/pkg 192.168.1.0/24(rw,no_subtree_check,no_root_squash)

```

*   You must also add no_root_squash to the first line in `/etc/exports`:

```
/ 192.168.1.0/24(rw,fsid=root,no_root_squash,no_subtree_check)

```

### "RPC: Program not registered" when showmount -e command issued

Make sure that `nfs-server.service` and `rpcbind.service` are running on the server site, see [systemd](/index.php/Systemd "Systemd"). If they are not, start and enable them.

Also make sure NFSv3 is enabled. *showmount* does **not** work with NFSv4-only servers.

## Client-side issues

### mount.nfs4: No such device

Check that you have loaded the `nfs` module

```
lsmod | grep nfs

```

and if previous returns empty or only nfsd-stuff, do

```
# modprobe nfs

```

### mount.nfs4: access denied by server while mounting

NFS shares have to reside in /srv - check your `/etc/exports` file and if necessary create the proper folder structure as described in the [NFS#File system](/index.php/NFS#File_system "NFS") page.

Check that the permissions on your client's folder are correct. Try using 755.

or try "exportfs -rav" reload `/etc/exports` file.

### mount.nfs4: Invalid argument

Enable and start nfs-client.target and make sure the appropriate daemons (nfs-idmapd, rpc-gssd, etc) are running on the server.

### Unable to connect from OS X clients

When trying to connect from an OS X client, you will see that everything is ok in the server logs, but OS X will refuse to mount your NFS share. You can do one of two things to fix this:

*   On the NFS server, add the `insecure` option to the share in `/etc/exports` and re-run `exportfs -r`.

... **OR** ...

*   On the OS X client, add the `resvport` option to the `mount` command line. You can also set `resvport` as a default client mount option in `/etc/nfs.conf`:

 `/etc/nfs.conf` 
```
nfs.client.mount.options = resvport

```

Using the default client mount option should also affect mounting the share from Finder via "Connect to Server...".

### Unreliable connection from OS X clients

OS X's NFS client is optimized for OS X Servers and might present some issues with Linux servers. If you are experiencing slow performance, frequent disconnects and problems with international characters edit the default mount options by adding the line `nfs.client.mount.options = intr,locallocks,nfc` to `/etc/nfs.conf` on your Mac client. More information about the mount options can be found in the OS X [mount_nfs man page](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man8/mount_nfs.8.html).

### Intermittent client freezes when copying large files

If you copy large files from your client machine to the NFS server, the transfer speed is *very* fast, but after some seconds the speed drops and your client machine intermittently locks up completely for some time until the transfer is finished.

Try adding <tt>sync</tt> as a mount option on the client (e.g. in <tt>/etc/fstab</tt>) to fix this problem.

### mount.nfs: Operation not permitted

#### NFSv4

If you use Kerberos (sec=krb5*), make sure the client and server clocks are correct. Using ntpd or systemd-timesyncd is recommended.

#### NFSv3 and earlier

*nfs-utils* versions 1.2.1-2 or higher use NFSv4 by default, resulting in NFSv3 shares failing on upgrade. The problem can be solved by using either mount option `'vers=3'` or `'nfsvers=3'` on the command line:

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

This error occurs when you include the export root in the path of the NFS source. For example:

```
# mount SERVER:/srv/nfs4/media /mnt
mount.nfs4: Protocol not supported

```

Use the relative path instead:

```
# mount SERVER:/media /mnt

```

### Problems with Vagrant and synced_folders

If Vagrant scripts are unable to mount folders over NFS, installing the *net-tools* package may solve the issue.

## Performance issues

This [NFS Howto page](http://nfs.sourceforge.net/nfs-howto/ar01s05.html) has some useful information regarding performance. Here are some further tips:

### Diagnose the problem

*   **Htop** should be your first port of call. The most obvious symptom will be a maxed-out CPU.
*   Press F2, and under "Display options", enable "Detailed CPU time". Press F1 for an explanation of the colours used in the CPU bars. In particular, is the CPU spending most of its time responding to IRQs, or in Wait-IO (wio)?

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

### Buffer cache size and MTU

**Symptoms:** High kernel or IRQ CPU usage, a very high packet count through the network card.

This is a trickier optimisation. Make sure this is definitely the problem before spending too much time on this. The default values are usually fine for most situations.

See [this excellent article](http://docstore.mik.ua/orelly/networking_2ndEd/nfs/ch07_03.htm) for information about I/O buffering in NFS. Essentially, data is accumulated into buffers before being sent. The size of the buffer will affect the way data is transmitted over the network. The Maximum Transmission Unit (MTU) of the network equipment will also affect throughput, as the buffers need to be split into MTU-sized chunks before they're sent over the network. If your buffer size is too big, the kernel or hardware may spend too much time splitting it into MTU-sized chunks. If the buffer size is too small, there will be overhead involved in sending a very large number of small packets. You can use the **rsize** and **wsize** mount options on the client to alter the buffer cache size. To achieve the best throughput, you need to experiment and discover the best values for your setup.

It is possible to change the MTU of many network cards. If your clients are on a separate subnet (e.g. for a Beowulf cluster), it may be safe to configure all of the network cards to use a high MTU. This should be done in very-high-bandwidth environments.

See also the **nfs** manual page for more about **rsize** and **wsize**.

## Debugging

### Using rpcdebug

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

### Kernel Interfaces

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
*   [rpcdebug(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/rpcdebug.8)
*   [http://utcc.utoronto.ca/~cks/space/blog/linux/NFSClientDebuggingBits](http://utcc.utoronto.ca/~cks/space/blog/linux/NFSClientDebuggingBits)
*   [http://www.novell.com/support/kb/doc.php?id=7011571](http://www.novell.com/support/kb/doc.php?id=7011571)
*   [http://stromberg.dnsalias.org/~strombrg/NFS-troubleshooting-2.html](http://stromberg.dnsalias.org/~strombrg/NFS-troubleshooting-2.html)
*   [http://www.opensubscriber.com/message/nfs@lists.sourceforge.net/7833588.html](http://www.opensubscriber.com/message/nfs@lists.sourceforge.net/7833588.html)

## Other issues

### Permissions issues

If you find that you cannot set the permissions on files properly, make sure the user/group you are chowning are on both the client and server.

If all your files are owned by `nobody`, and you are using NFSv4, on both the client and server, you should:

*   For systemd, ensure that the `nfs-idmapd` service has been started.
*   For initscripts, ensure that `NEED_IDMAPD` is set to `YES` in `/etc/conf.d/nfs-common.conf`.

On some systems detecting the domain from FQDN minus hostname does not seem to work reliably. If files are still showing as `nobody` after the above changes, edit /etc/idmapd.conf, ensure that `Domain` is set to `FQDN minus hostname`. For example:

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

If nfs-idmapd.service refuses to start because it cannot open the Pipefs-directory (defined in /etc/idmapd.conf and appended with '/nfs'), issue a mkdir-command and restart the daemon.