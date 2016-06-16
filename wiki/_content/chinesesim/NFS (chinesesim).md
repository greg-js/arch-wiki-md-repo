**翻译状态：** 本文是英文页面 [NFS](/index.php/NFS "NFS") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-15，点击[这里](https://wiki.archlinux.org/index.php?title=NFS&diff=0&oldid=435597)可以查看翻译后英文页面的改动。

来自[维基百科](https://en.wikipedia.org/wiki/Network_File_System "wikipedia:Network File System")：NFS 网络文件系统(Network File System) 是由Sun公司1984年发布的分布式文件系统协议。它允许客户端上的用户像访问本地文件一样地访问网络上的文件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
        *   [2.1.1 开始运行服务](#.E5.BC.80.E5.A7.8B.E8.BF.90.E8.A1.8C.E6.9C.8D.E5.8A.A1)
        *   [2.1.2 杂项](#.E6.9D.82.E9.A1.B9)
            *   [2.1.2.1 可选配置](#.E5.8F.AF.E9.80.89.E9.85.8D.E7.BD.AE)
            *   [2.1.2.2 NFSv3 版静态导出](#NFSv3_.E7.89.88.E9.9D.99.E6.80.81.E5.AF.BC.E5.87.BA)
            *   [2.1.2.3 NFSv2 版兼容](#NFSv2_.E7.89.88.E5.85.BC.E5.AE.B9)
            *   [2.1.2.4 配置防火墙](#.E9.85.8D.E7.BD.AE.E9.98.B2.E7.81.AB.E5.A2.99)
    *   [2.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.2.1 Error from systemd](#Error_from_systemd)
        *   [2.2.2 Manual mounting](#Manual_mounting)
        *   [2.2.3 Mount using /etc/fstab](#Mount_using_.2Fetc.2Ffstab)
        *   [2.2.4 Mount using /etc/fstab with systemd](#Mount_using_.2Fetc.2Ffstab_with_systemd)
        *   [2.2.5 Mount using autofs](#Mount_using_autofs)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 性能调优](#.E6.80.A7.E8.83.BD.E8.B0.83.E4.BC.98)
    *   [3.2 Automounting shares with systemd-networkd](#Automounting_shares_with_systemd-networkd)
    *   [3.3 Automatic mount handling](#Automatic_mount_handling)
        *   [3.3.1 Cron](#Cron)
        *   [3.3.2 systemd/Timers](#systemd.2FTimers)
        *   [3.3.3 Mount at startup via systemd](#Mount_at_startup_via_systemd)
        *   [3.3.4 NetworkManager dispatcher](#NetworkManager_dispatcher)
*   [4 排错](#.E6.8E.92.E9.94.99)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

客户端和服务端都只需要[安装](/index.php/Pacman "Pacman") [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) 包。

强烈建议在所有节点机上使用如 [ntp](https://www.archlinux.org/packages/?name=ntp) 之类的时间同步守护进程以保持客户端/服务器之间的时间同步，如果各个节点上没有精确同步的时钟，NFS 可能产生非预期的延迟。建议采用[网络时间协议守护进程](/index.php/%E7%BD%91%E7%BB%9C%E6%97%B6%E9%97%B4%E5%8D%8F%E8%AE%AE%E5%AE%88%E6%8A%A4%E8%BF%9B%E7%A8%8B "网络时间协议守护进程")并使用互联网上的高精度 NTP 服务器同步服务端和客户端的时钟。

**注意:** [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) for Arch Linux ARM starting with update 1.3.2-4 (possibly earlier) has been reported by one user to behave differently from the x86_64 or i686 package. See the discussion page for a recipe for client mounts.

## 配置

### 服务端

NFS 需要查看 `/etc/exports` 文件中定义的共享（“导出”）列表。共享的对象可以是文件系统中的任意目录。出于安全考虑，建议指定一个 NFS 输出的根（目录），来限制用户的可用挂载点。下面的例子践行此原则。

在 `/etc/exports` 中定义的任何 NFS 共享都关联到 NFS 根目录。本例中，NFS 根目录是 `/srv/nfs4` ，将要共享的目录是 `/mnt/music`。

```
# mkdir -p /srv/nfs4/music /mnt/music

```

客户端可能会对 music 目录做写操作，因此必须开放读/写权限。

现在用 mount 命令将实际的 music 目录挂载到 NFS 的共享挂载点 `/mnt/music`。

```
# mount --bind /mnt/music /srv/nfs4/music

```

为了让服务器重启后共享仍旧有效，增加绑定到 `fstab` 文件增加绑定到 `fstab` 文件：

 `/etc/fstab` 
```
/mnt/music /srv/nfs4/music  none   bind   0   0

```

**注意:** [ZFS](/index.php/ZFS "ZFS") 文件系统对于 bindmounts 方式挂载要特殊处理，参阅 [ZFS#Bindmount](/index.php/ZFS#Bindmount "ZFS")。

增加允许被挂载的目录和主机到`exports`：

 `/etc/exports` 
```
/srv/nfs4/ 192.168.1.0/24(rw,fsid=root,no_subtree_check)
/srv/nfs4/music 192.168.1.0/24(rw,no_subtree_check,nohide) # note the nohide option which is applied to mounted directories on the file system.

```

不必要对整个子网都开放共享，也可以仅指定单一 IP 地址或主机名。 更多信息及可用选项请查阅 `man 5 exports`。

如果服务运行时修改了 `/etc/exports` 文件， 你需要重新导出使其生效。

 `# exportfs -ra` 

#### 开始运行服务

[启用](/index.php/Enable "Enable")并[运行](/index.php/Start "Start") `nfs-server.service` 服务。对于较老的 V2 和 V3 版也要开启 `rpcbind.service` 服务。如果仅运行 V4 版，请按[[1]](https://bbs.archlinux.org/viewtopic.php?id=193629)这里的讨论确认完全禁用 V2 和 V3 版：

 `/etc/conf.d/nfs-server.conf`  `NFSD_OPTS="-N 2 -N 3"` 

否则，必须开启 `rpcbind.service` 服务。

#### 杂项

##### 可选配置

`/etc/conf.d/nfs-server.conf` holds optional configurations for options to pass to rpc.nfsd, rpc.mountd, or rpc.svcgssd. Users setting up a simple configuration may not need to edit this file.

##### NFSv3 版静态导出

Users needing support for NFSv3 clients, may wish to consider using static ports. By default, for NFSv3 operation `rpc.statd` and `lockd` use random ephemeral ports; in order to allow NFSv3 operations through a firewall static ports need to be defined. Edit `/etc/conf.d/nfs-common.conf` to set `STATD_OPTS`:

 `/etc/conf.d/nfs-common.conf`  `STATD_OPTS="-p 32765 -o 32766 -T 32803"` 

The `rpc.mountd` should consult `/etc/services` and bind to the same static port 20048 under normal operation; however, if it needs to be explicity defined edit `/etc/conf.d/nfs-server.conf` to set `MOUNTD_OPTS`:

 `/etc/conf.d/nfs-server.conf`  `MOUNTD_OPTS="-p 20048"` 

After making these changes, several services need to be restarted; the first writes the configuration options out to `/run/sysconfig/nfs-utils` (see `/usr/lib/systemd/scripts/nfs-utils_env.sh`), the second restarts `rpc.statd` with the new ports, the last reloads `lockd` (kernel module) with the new ports. [Restart](/index.php/Restart "Restart") these services now: `nfs-config`, `rpcbind`, `rpc-statd`, and `nfs-server`.

After the restarts, use `rpcinfo -p` on the server to examine the static ports are as expected. Using `rpcinfo -p <server IP>` from the client should reveal the exact same static ports.

##### NFSv2 版兼容

Users needing to support clients using NFSv2 (for example U-Boot), should set NFSD_OPTS="-V 2" in /etc/conf.d/nfs-server.conf.

##### 配置防火墙

To enable access through a firewall, tcp and udp ports 111, 2049, and 20048 need to be opened when using the default configuration; use `rpcinfo -p` to examine the exact ports in use on the server. To configure this for [iptables](/index.php/Iptables "Iptables"), execute this commands:

```
# iptables -A INPUT -p tcp -m tcp --dport 111 -j ACCEPT
# iptables -A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT
# iptables -A INPUT -p tcp -m tcp --dport 20048 -j ACCEPT
# iptables -A INPUT -p udp -m udp --dport 111 -j ACCEPT
# iptables -A INPUT -p udp -m udp --dport 2049 -j ACCEPT
# iptables -A INPUT -p udp -m udp --dport 20048 -j ACCEPT

```

To have this configuration load on every system start, edit `/etc/iptables/iptables.rules` to include the following lines:

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 111 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 20048 -j ACCEPT
-A INPUT -p udp -m udp --dport 111 -j ACCEPT
-A INPUT -p udp -m udp --dport 2049 -j ACCEPT
-A INPUT -p udp -m udp --dport 20048 -j ACCEPT

```

The previous commands can be saved by executing:

```
# iptables-save > /etc/iptables/iptables.rules

```

**Note:** This command will **override** the current iptables start configuration with the current iptables configuration!

If using NFSv3 and the above listed static ports for `rpc.statd` and `lockd` these also need to be added to the configuration:

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 32765 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 32803 -j ACCEPT
-A INPUT -p udp -m udp --dport 32765 -j ACCEPT
-A INPUT -p udp -m udp --dport 32803 -j ACCEPT

```

If using V4-only setup, only tcp port 2049 need to be opened. Therefore only one line need.

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT

```

To apply changes, [Restart](/index.php/Restart "Restart") `iptables.service`.

### 客户端

[Start](/index.php/Start "Start") `rpcbind.service`,`nfs-client.target` and `remote-fs.target` and [enable](/index.php/Enable "Enable") them to start at boot.

Users intending to use NFS4 with Kerberos, also need to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `rpc-gssd.service`. Setting up `/etc/krb5.keytab /etc/krb5.conf` are beyond the scope of this article.

#### Error from systemd

Users experiencing the following may consider turning off the service using system's masking feature: "Dependency failed for pNFS block layout mapping daemon."

Example:

```
# systemctl mask nfs-blkmap.service

```

#### Manual mounting

For NFSv3 use this command to show the server's exported file systems:

```
$ showmount -e servername

```

For NFSv4 mount the root NFS directory and look around for available mounts:

```
$ mount server:/ /mountpoint/on/client

```

Then mount omitting the server's NFS export root:

```
# mount -t nfs -o vers=4 servername:/music /mountpoint/on/client

```

If mount fails try including the server's export root (required for Debian/RHEL/SLES, some distributions need `-t nfs4` instead of `-t nfs`):

```
# mount -t nfs -o vers=4 servername:/full/path/to/music /mountpoint/on/client

```

**Note:** Server name needs to be a valid hostname (not just IP address). Otherwise mounting of remote share will hang.

#### Mount using /etc/fstab

Using [fstab](/index.php/Fstab "Fstab") is useful for a server which is always on, and the NFS shares are available whenever the client boots up. Edit `/etc/fstab` file, and add an appropriate line reflecting the setup. Again, the server's NFS export root is omitted.

 `/etc/fstab` 
```
servername:/music   /mountpoint/on/client   nfs4   rsize=8192,wsize=8192,timeo=14,_netdev	0 0

```

**Note:** Consult the *NFS* and *mount* man pages for more mount options.

Some additional mount options to consider are include:

	rsize and wsize

	`rsize` 的值是从服务器读取的字节数。`wsize` 是写入到服务器的字节数。默认都是1024， 如果使用比较高的值，如8192，可以提高传输速度。这并非通用设置，建议测试确定。参阅 [#性能调优](#.E6.80.A7.E8.83.BD.E8.B0.83.E4.BC.98).

	timeo

	The `timeo` value is the amount of time, in tenths of a second, to wait before resending a transmission after an RPC timeout. After the first timeout, the timeout value is doubled for each retry for a maximum of 60 seconds or until a major timeout occurs. If connecting to a slow server or over a busy network, better performance can be achieved by increasing this timeout value.

	_netdev

	The `_netdev` option tells the system to wait until the network is up before trying to mount the share. systemd assumes this for NFS, but anyway it is good practice to use it for all types of networked file systems

**Note:** Setting the sixth field (fs_passno) to a nonzero value may lead to unexpected behaviour, e.g. hangs when the systemd automount waits for a check which will never happen.

#### Mount using /etc/fstab with systemd

Another method is using the systemd `automount` service. This is a better option than `_netdev`, because it remounts the network device quickly when the connection is broken and restored. As well, it solves the problem from autofs, see the example below:

 `/etc/fstab`  `servername:/home   */mountpoint/on/client*  nfs  noauto,x-systemd.automount,x-systemd.device-timeout=10,timeo=14,x-systemd.idle-timeout=1min 0 0` 

One might have to reboot the client to make systemd aware of the changes to fstab. Alternatively, try [reloading](/index.php/Systemd#Using_units "Systemd") systemd and restarting `*mountpoint-on-client*.automount` to reload the `/etc/fstab` configuration.

**Tip:**

*   The `noauto` mount option will not mount the NFS share until it is accessed: use `auto` for it to be available immediately.
    If experiencing any issues with the mount failing due to the network not being up/available, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service`. It will ensure that `network.target` has all the links available prior to being active.
*   The `users` mount option would allow user mounts, but be aware it implies further options as `noexec` for example.
*   The `x-systemd.idle-timeout=1min` option will unmount the NFS share automatically after 1 minute of non-use. Good for laptops which might suddenly disconnect from the network.
*   If shutdown/reboot holds too long because of NFS, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service` to ensure that NetworkManager is not exited before the NFS volumes are unmounted.

**Note:** Users trying to automount a NFS-share via systemd which is mounted the same way on the server may experience a freeze when handling larger amounts of data.

#### Mount using autofs

Using [autofs](/index.php/Autofs "Autofs") is useful when multiple machines want to connect via NFS; they could both be clients as well as servers. The reason this method is preferable over the earlier one is that if the server is switched off, the client will not throw errors about being unable to find NFS shares. See [autofs#NFS network mounts](/index.php/Autofs#NFS_network_mounts "Autofs") for details.

## Tips and tricks

### 性能调优

In order to get the most out of NFS, it is necessary to tune the `rsize` and `wsize` mount options to meet the requirements of the network configuration.

### Automounting shares with systemd-networkd

Users making use of systemd-networkd might notice nfs mounts the fstab are not mounted when booting; errors like the following are common:

```
mount[311]: mount.nfs4: Network is unreachable

```

The solution is simple; force systemd to wait for the network to be completely configured by [enabling](/index.php/Enabling "Enabling") `systemd-networkd-wait-online.service`. In theory this slows down the boot-process because less services run in parallel.

### Automatic mount handling

This trick is useful for laptops that require nfs shares from a local wireless network. If the nfs host becomes unreachable, the nfs share will be unmounted to hopefully prevent system hangs when using the hard mount option. See [https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240](https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240)

Make sure that the NFS mount points are correctly indicated in `/etc/fstab`:

 `$ cat /etc/fstab` 
```
lithium:/mnt/data           /mnt/data	        nfs noauto,noatime,rsize=32768,wsize=32768 0 0
lithium:/var/cache/pacman   /var/cache/pacman	nfs noauto,noatime,rsize=32768,wsize=32768 0 0

```

**Note:** You must use hostnames in `/etc/fstab` for this to work, not IP addresses.

The `noauto` mount option tells systemd not to automatically mount the shares at boot. systemd would otherwise attempt to mount the nfs shares that may or may not exist on the network causing the boot process to appear to stall on a blank screen.

In order to mount NFS shares with non-root users the `user` option has to be added.

Create the `auto_share` script that will be used by *cron* or *systemd/Timers* to use ICMP ping to check if the NFS host is reachable:

 `/usr/local/bin/auto_share` 
```
#!/bin/bash

function net_umount {
  umount -l -f $1 &>/dev/null
}

function net_mount {
  mountpoint -q $1 || mount $1
}

NET_MOUNTS=$(sed -e '/^.*#/d' -e '/^.*:/!d' -e 's/\t/ /g' /etc/fstab | tr -s " ")$'
'b

printf %s "$NET_MOUNTS" | while IFS= read -r line
do
  SERVER=$(echo $line | cut -f1 -d":")
  MOUNT_POINT=$(echo $line | cut -f2 -d" ")

  # Check if server already tested
  if [[ "${server_ok[@]}" =~ "${SERVER}" ]]; then
    # The server is up, make sure the share are mounted
    net_mount $MOUNT_POINT
  elif [[ "${server_notok[@]}" =~ "${SERVER}" ]]; then
    # The server could not be reached, unmount the share
    net_umount $MOUNT_POINT
  else
    # Check if the server is reachable
    ping -c 1 "${SERVER}" &>/dev/null

    if [ $? -ne 0 ]; then
      server_notok[${#Unix[@]}]=$SERVER
      # The server could not be reached, unmount the share
      net_umount $MOUNT_POINT
    else
      server_ok[${#Unix[@]}]=$SERVER
      # The server is up, make sure the share are mounted
      net_mount $MOUNT_POINT
    fi
  fi
done

```

**Note:** If you want to test using a TCP probe instead of ICMP ping (default is tcp port 2049 in NFS4) then replace the line:
```
 # Check if the server is reachable
 ping -c 1 "${SERVER}" &>/dev/null

```

with:

```
 # Check if the server is reachable
 timeout 1 bash -c ": < /dev/tcp/${SERVER}/2049"

```
in the `auto_share` script above.

```
# chmod +x /usr/local/bin/auto_share

```

Create a cron entry or a systemd/Timers timer to check every minute if the server of the shares are reachable.

#### Cron

 `# crontab -e` 
```
* * * * * /usr/local/bin/auto_share

```

#### systemd/Timers

 `# /etc/systemd/system/auto_share.timer` 
```
[Unit]
Description=Check the network mounts

[Timer]
OnCalendar=*-*-* *:*:00

[Install]
WantedBy=timer.target

```
 `# /etc/systemd/system/auto_share.service` 
```
[Unit]
Description=Check the network mounts

[Service]
Type=simple
ExecStart=/usr/local/bin/auto_share

```

```
# systemctl enable auto_share.timer

```

#### Mount at startup via systemd

A systemd unit file can also be used to mount the NFS shares at startup. The unit file is not necessary if NetworkManager is installed and configured on the client system. See [#NetworkManager dispatcher](#NetworkManager_dispatcher).

 `/etc/systemd/system/auto_share.service` 
```
[Unit]
Description=NFS automount
After=syslog.target network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/bin/auto_share

[Install]
WantedBy=multi-user.target

```

Now [enable](/index.php/Enable "Enable") the `auto_share.service`.

#### NetworkManager dispatcher

In addition to the method described previously, [NetworkManager](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") can also be configured to run a script on network status change: [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `NetworkManager-dispatcher.service`.

The easiest method for mount shares on network status change is to just symlink to the `auto_share` script:

```
# ln -s /usr/local/bin/auto_share /etc/NetworkManager/dispatcher.d/30-nfs.sh

```

However, in that particular case unmounting will happen only after the network connection has already been disabled, which is unclean and may result in effects like freezing of KDE Plasma applets.

The following script safely unmounts the NFS shares before the relevant network connection is disabled by listening for the `pre-down` and `vpn-pre-down` events:

**Note:** This script ignores mounts with the noauto option.
 `/etc/NetworkManager/dispatcher.d/30-nfs.sh` 
```
#!/bin/bash

# Find the connection UUID with "nmcli con show" in terminal.
# All NetworkManager connection types are supported: wireless, VPN, wired...
WANTED_CON_UUID="CHANGE-ME-NOW-9c7eff15-010a-4b1c-a786-9b4efa218ba9"

if [[ "$CONNECTION_UUID" == "$WANTED_CON_UUID" ]]; then

    # Script parameter $1: NetworkManager connection name, not used
    # Script parameter $2: dispatched event

    case "$2" in
        "up")
            mount -a -t nfs4,nfs 
            ;;
        "pre-down");&
        "vpn-pre-down")
            umount -l -a -t nfs4,nfs >/dev/null
            ;;
    esac
fi

```

Make the script executable with [chmod](/index.php/Chmod "Chmod") and create a symlink inside `/etc/NetworkManager/dispatcher.d/pre-down` to catch the `pre-down` events:

```
# ln -s /etc/NetworkManager/dispatcher.d/30-nfs.sh /etc/NetworkManager/dispatcher.d/pre-down.d/30-nfs.sh

```

The above script can be modified to mount different shares (even other than NFS) for different connections.

See also: [NetworkManager#Use dispatcher to handle mounting of CIFS shares](/index.php/NetworkManager#Use_dispatcher_to_handle_mounting_of_CIFS_shares "NetworkManager").

## 排错

参阅 [NFS 排错](/index.php?title=NFS_%E6%8E%92%E9%94%99&action=edit&redlink=1 "NFS 排错 (page does not exist)")。

## 参阅

*   参阅 [Avahi](/index.php/Avahi "Avahi")，一个零配置的实现，可以自动发现 NFS 共享。
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [NFS Performance Management](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [NFS on Snow Leopard](https://blogs.oracle.com/jag/entry/nfs_on_snow_leopard)