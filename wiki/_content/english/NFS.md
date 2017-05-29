From [Wikipedia](https://en.wikipedia.org/wiki/Network_File_System "wikipedia:Network File System"):

	*Network File System (NFS) is a distributed file system protocol originally developed by Sun Microsystems in 1984, allowing a user on a client computer to access files over a network in a manner similar to how local storage is accessed.*

**Note:** NFS is not encrypted. Tunnel NFS through an encrypted protocol like [Kerberos](/index.php/Kerberos "Kerberos"), or [tinc](/index.php/Tinc "Tinc") when dealing with sensitive data.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Server](#Server)
        *   [2.1.1 Starting the server](#Starting_the_server)
        *   [2.1.2 Miscellaneous](#Miscellaneous)
            *   [2.1.2.1 Optional configuration](#Optional_configuration)
            *   [2.1.2.2 Restricting NFS to interfaces/IPs](#Restricting_NFS_to_interfaces.2FIPs)
            *   [2.1.2.3 Ensure NFSv4 idmapping is fully enabled](#Ensure_NFSv4_idmapping_is_fully_enabled)
            *   [2.1.2.4 Static ports for NFSv3](#Static_ports_for_NFSv3)
            *   [2.1.2.5 NFSv2 compatibility](#NFSv2_compatibility)
            *   [2.1.2.6 Firewall configuration](#Firewall_configuration)
    *   [2.2 Client](#Client)
        *   [2.2.1 Error from systemd](#Error_from_systemd)
        *   [2.2.2 Manual mounting](#Manual_mounting)
        *   [2.2.3 Mount using /etc/fstab](#Mount_using_.2Fetc.2Ffstab)
        *   [2.2.4 Mount using /etc/fstab with systemd](#Mount_using_.2Fetc.2Ffstab_with_systemd)
        *   [2.2.5 Mount using autofs](#Mount_using_autofs)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Performance tuning](#Performance_tuning)
    *   [3.2 Automounting shares with systemd-networkd](#Automounting_shares_with_systemd-networkd)
    *   [3.3 Automatic mount handling](#Automatic_mount_handling)
        *   [3.3.1 Cron](#Cron)
        *   [3.3.2 systemd/Timers](#systemd.2FTimers)
        *   [3.3.3 Mount at startup via systemd](#Mount_at_startup_via_systemd)
        *   [3.3.4 NetworkManager dispatcher](#NetworkManager_dispatcher)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

Both client and server only require the [installation](/index.php/Install "Install") of the [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) package.

It is **highly** recommended to use a [time sync daemon](/index.php/Time#Time_synchronization "Time") to keep client/server clocks in sync. Without accurate clocks on all nodes, NFS can introduce unwanted delays.

## Configuration

### Server

The NFS server needs a list of exports (shared directories) which are defined in `/etc/exports`. NFS shares defined in `/etc/exports` are relative to the so-called NFS root. A good security practice is to define an NFS root in a discrete directory tree under the server's root file system which will keep users limited to that mount point. Bind mounts are used to link the share mount point to the actual directory elsewhere on the filesystem.

Consider this following example wherein:

1.  The NFS root is `/srv/nfs`.
2.  The export is `/srv/nfs/music` via a bind mount to the actual target `/mnt/music`.

```
# mkdir -p /srv/nfs/music /mnt/music
# mount --bind /mnt/music /srv/nfs/music

```

To make it stick across reboots, add the bind mount to `fstab`:

 `/etc/fstab` 
```
/mnt/music /srv/nfs/music  none   bind   0   0

```

**Note:** The permissions on the server filesystem is what NFS will honor so insure that connecting users have the desired access.

**Note:** [ZFS](/index.php/ZFS "ZFS") filesystems require special handling of bindmounts, see [ZFS#Bind mount](/index.php/ZFS#Bind_mount "ZFS").

Add directories to be shared and limit them to a range of addresses via a CIDR or hostname(s) of client machines that will be allowed to mount them in `/etc/exports`:

 `/etc/exports` 
```
/srv/nfs       192.168.1.0/24(rw,fsid=root,no_subtree_check)
/srv/nfs/music 192.168.1.0/24(rw,no_subtree_check,nohide) # note the nohide option which is applied to mounted directories on the file system.

```

It should be noted that modifying `/etc/exports` while the server is running will require a re-export for changes to take effect:

```
# exportfs -rav

```

For more information about all available options see [exports(5)](http://man7.org/linux/man-pages/man5/exports.5.html).

**Tip:** [ip2cidr](http://ip2cidr.com/) is a tool to convert an IP ranges to correctly structured CDIR specification.

**Note:** If the target export is a tmpfs filesystem, the `fsid=1` option is required.

#### Starting the server

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `nfs-server.service`.

#### Miscellaneous

##### Optional configuration

Advanced configuration options can be set in `/etc/nfs.conf`. Users setting up a simple configuration may not need to edit this file.

##### Restricting NFS to interfaces/IPs

By default, starting `nfs-server.service` will listen for connections on all network interfaces, regardless of `/etc/exports`. This can be changed by defining which IPs and/or hostnames to listen on.

 `/etc/nfs.conf` 
```
[nfsd]
host=192.168.1.123
# Alternatively, you can use your hostname.
# host=myhostname
```

Restarting the service will apply the changes immediately.

```
# systemctl restart nfs-server.service

```

##### Ensure NFSv4 idmapping is fully enabled

Even though idmapd may be running, it may not be fully enabled. Verify by checking `cat /sys/module/nfsd/parameters/nfs4_disable_idmapping` returns `N`. If not:

```
# echo "N" | sudo tee /sys/module/nfsd/parameters/nfs4_disable_idmapping

```

Set this to survive reboots by adding an option to the nfs kernel module:

```
# echo "options nfs nfs4_disable_idmapping=0" | sudo tee -a /etc/modprobe.d/nfs.conf

```

(See [this forum reply](https://bbs.archlinux.org/viewtopic.php?pid=1530693#p1530693) for more information.)

If journalctl reports lines like the following when starting nfs-server.service and nfs-idmapd.service, then this may be the solution.

```
rpc.idmapd[25010]: nfsdcb: authbuf=192.168.0.0/16 authtype=user
rpc.idmapd[25010]: nfsdcb: bad name in upcall

```

##### Static ports for NFSv3

Users needing support for NFSv3 clients, may wish to consider using static ports. By default, for NFSv3 operation `rpc.statd` and `lockd` use random ephemeral ports; in order to allow NFSv3 operations through a firewall static ports need to be defined. Edit `/etc/sysconfig/nfs` to set `STATDARGS`:

 `/etc/sysconfig/nfs`  `STATDARGS="-p 32765 -o 32766 -T 32803"` 

The `rpc.mountd` should consult `/etc/services` and bind to the same static port 20048 under normal operation; however, if it needs to be explicity defined edit `/etc/sysconfig/nfs` to set `RPCMOUNTDARGS`:

 `/etc/sysconfig/nfs`  `RPCMOUNTDARGS="-p 20048"` 

After making these changes, several services need to be restarted; the first writes the configuration options out to `/run/sysconfig/nfs-utils` (see `/usr/lib/systemd/scripts/nfs-utils_env.sh`), the second restarts `rpc.statd` with the new ports, the last reloads `lockd` (kernel module) with the new ports. [Restart](/index.php/Restart "Restart") these services now: `nfs-config`, `rpcbind`, `rpc-statd`, and `nfs-server`.

After the restarts, use `rpcinfo -p` on the server to examine the static ports are as expected. Using `rpcinfo -p <server IP>` from the client should reveal the exact same static ports.

##### NFSv2 compatibility

Users needing to support clients using NFSv2 (for example U-Boot), should set `RPCNFSDARGS="-V 2"` in `/etc/sysconfig/nfs`.

##### Firewall configuration

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

If using V4-only setup, only tcp port 2049 need to be opened. Therefore only one line needed.

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT

```

To apply changes, [Restart](/index.php/Restart "Restart") `iptables.service`.

### Client

Users intending to use NFS4 with [Kerberos](/index.php/Kerberos "Kerberos"), also need to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `nfs-client.target`, which starts `rpc-gssd.service`. However, due to bug [FS#50663](https://bugs.archlinux.org/task/50663) in glibc, `rpc-gssd.service` currently fails to start. Adding the "-f" (foreground) flag in the service is a workaround:

 `# systemctl edit rpc-gssd.service` 
```
[Unit]
Requires=network-online.target
After=network-online.target

[Service]
Type=simple
ExecStart=
ExecStart=/usr/sbin/rpc.gssd -f
```

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
# mount server:/ /mountpoint/on/client

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
servername:/music   /mountpoint/on/client   nfs   rsize=8192,wsize=8192,timeo=14,_netdev	0 0

```

**Note:** Consult [nfs(5)](http://man7.org/linux/man-pages/man5/nfs.5.html) and [mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html) for more mount options.

Some additional mount options to consider are include:

	rsize and wsize

	The `rsize` value is the number of bytes used when reading from the server. The `wsize` value is the number of bytes used when writing to the server. The default for both is 1024, but using higher values such as 8192 can improve throughput. This is not universal. It is recommended to test after making this change, see [#Performance tuning](#Performance_tuning).

	timeo

	The `timeo` value is the amount of time, in tenths of a second, to wait before resending a transmission after an RPC timeout. After the first timeout, the timeout value is doubled for each retry for a maximum of 60 seconds or until a major timeout occurs. If connecting to a slow server or over a busy network, better performance can be achieved by increasing this timeout value.

	_netdev

	The `_netdev` option tells the system to wait until the network is up before trying to mount the share. systemd assumes this for NFS, but anyway it is good practice to use it for all types of networked file systems

**Note:** Setting the sixth field (`fs_passno`) to a nonzero value may lead to unexpected behaviour, e.g. hangs when the systemd automount waits for a check which will never happen.

#### Mount using /etc/fstab with systemd

Another method is using the systemd `automount` service. This is a better option than `_netdev`, because it remounts the network device quickly when the connection is broken and restored. As well, it solves the problem from autofs, see the example below:

 `/etc/fstab`  `servername:/home   */mountpoint/on/client*  nfs  noauto,x-systemd.automount,x-systemd.device-timeout=10,timeo=14,x-systemd.idle-timeout=1min 0 0` 

One might have to reboot the client to make systemd aware of the changes to fstab. Alternatively, try [reloading](/index.php/Systemd#Using_units "Systemd") systemd and restarting `*mountpoint-on-client*.automount` to reload the `/etc/fstab` configuration.

**Tip:**

*   The `noauto` mount option will not mount the NFS share until it is accessed: use `auto` for it to be available immediately.
    If experiencing any issues with the mount failing due to the network not being up/available, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service`. It will ensure that `network.target` has all the links available prior to being active.
*   The `users` mount option would allow user mounts, but be aware it implies further options as `noexec` for example.
*   The `x-systemd.idle-timeout=1min` option will unmount the NFS share automatically after 1 minute of non-use. Good for laptops which might suddenly disconnect from the network.
*   If shutdown/reboot holds too long because of NFS, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service` to ensure that NetworkManager is not exited before the NFS volumes are unmounted. You may also try to add the `x-systemd.requires=network.target` mount option if shutdown takes too long.

**Note:** Users trying to automount a NFS-share via systemd which is mounted the same way on the server may experience a freeze when handling larger amounts of data.

#### Mount using autofs

Using [autofs](/index.php/Autofs "Autofs") is useful when multiple machines want to connect via NFS; they could both be clients as well as servers. The reason this method is preferable over the earlier one is that if the server is switched off, the client will not throw errors about being unable to find NFS shares. See [autofs#NFS network mounts](/index.php/Autofs#NFS_network_mounts "Autofs") for details.

## Tips and tricks

### Performance tuning

In order to get the most out of NFS, it is necessary to tune the `rsize` and `wsize` mount options to meet the requirements of the network configuration.

In recent linux kernels (>2.6.18) the size of I/O operations allowed by the NFS server (default max block size) varies depending on RAM size, with a maximum of 1M (1048576 bytes), the max block size of th server will be used even if nfs clients requires bigger `rsize` and `wsize`. See [https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/5.8_Technical_Notes/Known_Issues-kernel.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/5.8_Technical_Notes/Known_Issues-kernel.html) It is possible to change the default max block size allowed by the server by writing to the /proc/fs/nfsd/max_block_size file before starting nfsd. For example, the following command restores the previous default iosize of 32k:

```
~]# echo 32767 >/proc/fs/nfsd/max_block_size

```

To make the change permanent add

```
ExecStartPre=/usr/bin/bash -c '/usr/bin/echo 32768 > /proc/fs/nfsd/max_block_size'

```

to /etc/systemd/system/multi-user.target.wants/nfs-server.service or create a systemd service as explained here: [https://bbs.archlinux.org/viewtopic.php?id=203893](https://bbs.archlinux.org/viewtopic.php?id=203893)

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

## Troubleshooting

There is a dedicated article [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting").

## See also

*   See also [Avahi](/index.php/Avahi "Avahi"), a Zeroconf implementation which allows automatic discovery of NFS shares.
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [NFS Performance Management](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [NFS on Snow Leopard](https://blogs.oracle.com/jag/entry/nfs_on_snow_leopard)