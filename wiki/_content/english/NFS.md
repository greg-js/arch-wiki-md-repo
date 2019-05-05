Related articles

*   [NFS/Troubleshooting](/index.php/NFS/Troubleshooting "NFS/Troubleshooting")

From [Wikipedia](https://en.wikipedia.org/wiki/Network_File_System "wikipedia:Network File System"):

	Network File System (NFS) is a distributed file system protocol originally developed by Sun Microsystems in 1984, allowing a user on a client computer to access files over a network in a manner similar to how local storage is accessed.

**Note:**

*   NFS is not encrypted. Tunnel NFS through an encrypted protocol like [Kerberos](/index.php/Kerberos "Kerberos"), or [tinc](/index.php/Tinc "Tinc") when dealing with sensitive data.
*   Unlike [Samba](/index.php/Samba "Samba"), NFS does not have any user authentication by default, client access is restricted by their IP-address/[hostname](/index.php/Hostname "Hostname").
*   NFS expects the [user](/index.php/User "User") and/or [user group](/index.php/User_group "User group") ID's are the same on both the client and server. [Enable NFSv4 idmapping](#Enabling_NFSv4_idmapping) or overrule the UID/GID manually by using `anonuid`/`anongid` together with `all_squash` in `/etc/exports`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Server](#Server)
        *   [2.1.1 Starting the server](#Starting_the_server)
        *   [2.1.2 Restricting NFS to interfaces/IPs](#Restricting_NFS_to_interfaces/IPs)
        *   [2.1.3 Firewall configuration](#Firewall_configuration)
        *   [2.1.4 Enabling NFSv4 idmapping](#Enabling_NFSv4_idmapping)
        *   [2.1.5 Static ports for NFSv3](#Static_ports_for_NFSv3)
        *   [2.1.6 NFSv2 compatibility](#NFSv2_compatibility)
    *   [2.2 Client](#Client)
        *   [2.2.1 Manual mounting](#Manual_mounting)
        *   [2.2.2 Mount using /etc/fstab](#Mount_using_/etc/fstab)
        *   [2.2.3 Mount using /etc/fstab with systemd](#Mount_using_/etc/fstab_with_systemd)
        *   [2.2.4 As systemd unit](#As_systemd_unit)
        *   [2.2.5 Mount using autofs](#Mount_using_autofs)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Performance tuning](#Performance_tuning)
    *   [3.2 Automatic mount handling](#Automatic_mount_handling)
        *   [3.2.1 Cron](#Cron)
        *   [3.2.2 systemd/Timers](#systemd/Timers)
        *   [3.2.3 Using a NetworkManager dispatcher](#Using_a_NetworkManager_dispatcher)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Installation

Both client and server only require the [installation](/index.php/Install "Install") of the [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) package.

It is **highly** recommended to use a [time synchronization](/index.php/Time_synchronization "Time synchronization") daemon to keep client/server clocks in sync. Without accurate clocks on all nodes, NFS can introduce unwanted delays.

## Configuration

### Server

Global configuration options are set in `/etc/nfs.conf`. Users of simple configurations should not need to edit this file.

The NFS server needs a list of exports (see [exports(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/exports.5) for details) which are defined in `/etc/exports` or `/etc/exports.d/*.exports`. These shares are relative to the so-called NFS root. A good security practice is to define a NFS root in a discrete directory tree which will keep users limited to that mount point. Bind mounts are used to link the share mount point to the actual directory elsewhere on the [filesystem](/index.php/Filesystem "Filesystem").

Consider this following example wherein:

1.  The NFS root is `/srv/nfs`.
2.  The export is `/srv/nfs/music` via a bind mount to the actual target `/mnt/music`.

```
# mkdir -p /srv/nfs/music /mnt/music
# mount --bind /mnt/music /srv/nfs/music

```

**Note:** [ZFS](/index.php/ZFS "ZFS") filesystems require special handling of bindmounts, see [ZFS#Bind mount](/index.php/ZFS#Bind_mount "ZFS").

To make the bind mount persistent across reboots, add it to [fstab](/index.php/Fstab "Fstab"):

 `/etc/fstab` 
```
/mnt/music /srv/nfs/music  none   bind   0   0

```

Add directories to be shared and limit them to a range of addresses via a CIDR or hostname(s) of client machines that will be allowed to mount them in `/etc/exports`, e.g.:

 `/etc/exports` 
```
/srv/nfs        192.168.1.0/24(rw,sync,crossmnt,fsid=0)
/srv/nfs/music  192.168.1.0/24(rw,sync)
/srv/nfs/home   192.168.1.0/24(rw,sync,nohide)
/srv/nfs/public 192.168.1.0/24(ro,all_squash,insecure) desktop(rw,sync,all_squash,anonuid=99,anongid=99) # map to user/group - in this case *nobody*
```

**Tip:**

*   The `crossmnt` option is necessary to share exported directories inside an exported directory.
*   Use an asterisk (*) to allow access from any interface.

It should be noted that modifying `/etc/exports` while the server is running will require a re-export for changes to take effect:

```
# exportfs -arv

```

To view the current loaded exports state in more detail, use:

```
# exportfs -v

```

For more information about all available options see [exports(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/exports.5).

**Tip:** [ip2cidr](http://ip2cidr.com/) is a tool to convert an IP ranges to correctly structured CIDR specification.

**Note:** If the target export is a [tmpfs](/index.php/Tmpfs "Tmpfs") filesystem, the `fsid=1` option is required.

#### Starting the server

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `nfs-server.service`.

**Warning:** A hard dependency of serving NFS (`rpc-gssd.service`) will wait until the [random number generator](/index.php/Random_number_generator "Random number generator") pool is sufficiently initialized possibly delaying the boot process. This is particularly prevalent on headless servers. It is *highly* recommended to populate the entropy pool using a utility such as [Rng-tools](/index.php/Rng-tools "Rng-tools") (if [TPM](/index.php/TPM "TPM") is supported) or [Haveged](/index.php/Haveged "Haveged") in these scenarios.

**Note:** If exporting ZFS shares, also [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `zfs-share.service`. Without this, ZFS shares will no longer be exported after a reboot. See [ZFS#NFS](/index.php/ZFS#NFS "ZFS").

#### Restricting NFS to interfaces/IPs

By default, starting `nfs-server.service` will listen for connections on all network interfaces, regardless of `/etc/exports`. This can be changed by defining which IPs and/or hostnames to listen on.

 `/etc/nfs.conf` 
```
[nfsd]
host=192.168.1.123
# Alternatively, use the hostname.
# host=myhostname
```

[Restart](/index.php/Restart "Restart") `nfs-server.service` to apply the changes immediately.

#### Firewall configuration

To enable access through a [firewall](/index.php/Firewall "Firewall"), TCP and UDP ports `111`, `2049`, and `20048` may need to be opened when using the default configuration; use `rpcinfo -p` to examine the exact ports in use on the server:

 `$ rpcinfo -p | grep nfs` 
```
100003    3   tcp   2049  nfs
100003    4   tcp   2049  nfs
100227    3   tcp   2049  nfs_acl

```

When using NFSv4, make sure TCP port `2049` is open. No other port opening should be required:

 `/etc/iptables/iptables.rules`  `-A INPUT -p tcp -m tcp --dport 2049 -j ACCEPT` 

When using an older NFS version, make sure other ports are open:

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

**Warning:** This command will **override** the current iptables start configuration with the current iptables configuration!

If using NFSv3 and the above listed static ports for `rpc.statd` and `lockd` the following ports may also need to be added to the configuration:

 `/etc/iptables/iptables.rules` 
```
-A INPUT -p tcp -m tcp --dport 32765 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 32803 -j ACCEPT
-A INPUT -p udp -m udp --dport 32765 -j ACCEPT
-A INPUT -p udp -m udp --dport 32803 -j ACCEPT
```

To apply changes, [Restart](/index.php/Restart "Restart") `iptables.service`.

#### Enabling NFSv4 idmapping

**Note:**

*   NFSv4 idmapping needs to be enabled on **both** the client and server.
*   Another option is to make sure the user and group IDs (UID and GID) match on both the client and server.

The NFSv4 protocol represents the local system's UID and GID values on the wire as strings of the form `user@domain`. The process of translating from UID to string and string to UID is referred to as *ID mapping* [[1]](http://man7.org/linux/man-pages/man5/nfsidmap.5.html).

Even though idmapd may be running, it may not be fully enabled. If `/sys/module/nfsd/parameters/nfs4_disable_idmapping` returns `Y` on a client/server, enable it by:

```
# echo "N" | tee /sys/module/nfsd/parameters/nfs4_disable_idmapping

```

Set as [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules") to make this change permanent, i.e.:

 `/etc/modprobe.d/nfsd.conf` 
```
options nfs nfs4_disable_idmapping=0
options nfsd nfs4_disable_idmapping=0
```

To fully use *idmapping*, make sure the domain is configured in `/etc/idmapd.conf` on **both** the server and the client:

 `/etc/idmapd.conf` 
```
# The following should be set to the local NFSv4 domain name
# The default is the host's DNS domain name.
Domain = *domain.tld*
```

#### Static ports for NFSv3

Users needing support for NFSv3 clients, may wish to consider using static ports. By default, for NFSv3 operation `rpc.statd` and `lockd` use random ephemeral ports; in order to allow NFSv3 operations through a firewall static ports need to be defined. Edit `/etc/sysconfig/nfs` to set `STATDARGS`:

 `/etc/sysconfig/nfs`  `STATDARGS="-p 32765 -o 32766 -T 32803"` 

The `rpc.mountd` should consult `/etc/services` and bind to the same static port 20048 under normal operation; however, if it needs to be explicity defined edit `/etc/sysconfig/nfs` to set `RPCMOUNTDARGS`:

 `/etc/sysconfig/nfs`  `RPCMOUNTDARGS="-p 20048"` 

After making these changes, several services need to be restarted; the first writes the configuration options out to `/run/sysconfig/nfs-utils` (see `/usr/lib/systemd/scripts/nfs-utils_env.sh`), the second restarts `rpc.statd` with the new ports, the last reloads `lockd` (kernel module) with the new ports. [Restart](/index.php/Restart "Restart") these services now: `nfs-config`, `rpcbind`, `rpc-statd`, and `nfs-server`.

After the restarts, use `rpcinfo -p` on the server to examine the static ports are as expected. Using `rpcinfo -p <server IP>` from the client should reveal the exact same static ports.

#### NFSv2 compatibility

Users needing to support clients using NFSv2 (for example U-Boot), should set `RPCNFSDARGS="-V 2"` in `/etc/sysconfig/nfs`.

### Client

Users intending to use NFS4 with [Kerberos](/index.php/Kerberos "Kerberos") need to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `nfs-client.target`.

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
# mount -t nfs -o vers=4 servername:/srv/nfs/music /mountpoint/on/client

```

**Note:** Server name needs to be a valid hostname (not just IP address). Otherwise mounting of remote share will hang.

#### Mount using /etc/fstab

Using [fstab](/index.php/Fstab "Fstab") is useful for a server which is always on, and the NFS shares are available whenever the client boots up. Edit `/etc/fstab` file, and add an appropriate line reflecting the setup. Again, the server's NFS export root is omitted.

 `/etc/fstab`  `servername:/music   /mountpoint/on/client   nfs   defaults,timeo=900,retrans=5,_netdev	0 0` 
**Note:** Consult [nfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nfs.5) and [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) for more mount options.

Some additional mount options to consider:

	rsize and wsize

	The `rsize` value is the number of bytes used when reading from the server. The `wsize` value is the number of bytes used when writing to the server. By default, if these options are not specified, the client and server negotiate the largest values they can both support (see [nfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nfs.5) for details). After changing these values, it is recommended to test the performance (see [#Performance tuning](#Performance_tuning)).

	soft or hard

	Determines the recovery behaviour of the NFS client after an NFS request times out. If neither option is specified (or if the `hard` option is specified), NFS requests are retried indefinitely. If the `soft` option is specified, then the NFS client fails a NFS request after *retrans* retransmissions have been sent, causing the NFS client to return an error to the calling application.

**Warning:** A so-called `soft` timeout can cause silent data corruption in certain cases. As such, use the `soft` option only when client responsiveness is more important than data integrity. Using NFS over TCP or increasing the value of the `retrans` option may mitigate some of the risks of using the `soft` option.

	timeo

	The `timeo` value is the amount of time, in tenths of a second, to wait before resending a transmission after an RPC timeout. The default value for NFS over TCP is 600 (60 seconds). After the first timeout, the timeout value is doubled for each retry for a maximum of 60 seconds or until a major timeout occurs. If connecting to a slow server or over a busy network, better stability can be achieved by increasing this timeout value.

	retrans

	The number of times the NFS client retries a request before it attempts further recovery action. If the `retrans` option is not specified, the NFS client tries each request three times. The NFS client generates a "server not responding" message after *retrans* retries, then attempts further recovery (depending on whether the hard mount option is in effect).

	_netdev

	The `_netdev` option tells the system to wait until the network is up before trying to mount the share - [systemd](/index.php/Systemd "Systemd") assumes this for NFS, although [automount](#Mount_using_/etc/fstab_with_systemd) may be a more preferred solution.

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
*   If shutdown/reboot holds too long because of NFS, [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service` to ensure that NetworkManager is not exited before the NFS volumes are unmounted. Also try to add the `x-systemd.requires=network-online.target` mount option if shutdown takes too long.
*   Using mount options as `noatime`, `nodiratime`, `noac`, `nocto` may be used to increase NFS performance.

#### As systemd unit

Create a new `.mount` file inside `/etc/systemd/system`, e.g. `mnt-myshare.mount`. See [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5) for details.

**Note:** Make sure the filename corresponds to the mountpoint you want to use. E.g. the unit name `mnt-myshare.mount` can only be used if are going to mount the share under `/mnt/myshare`. Otherwise the following error might occur: `systemd[1]: mnt-myshare.mount: Where= setting does not match unit name. Refusing.`.

`What=` path to share

`Where=` path to mount the share

`Options=` share mounting options

**Note:**

*   Network mount units automatically acquire `After` dependencies on *remote-fs-pre.target*, *network.target* and *network-online.target*, and gain a `Before` dependency on *remote-fs.target* unless `nofail` mount option is set. Towards the latter a `Wants` unit is added as well.
*   [Append](/index.php/Append "Append") `noauto` to `Options` preventing automatically mount during boot (unless it is pulled in by some other unit).
*   If you want to use a hostname for the server you want to share (instead of an IP address), add `nss-lookup.target` to `After` and `Wants`. This might avoid mount errors at boot time that do not arise when testing the unit.

 `/etc/systemd/system/mnt-myshare.mount` 
```
[Unit]
Description=Mount Share at boot

[Mount]
What=172.16.24.192:/mnt/myshare
Where=/mnt/myshare
Options=x-systemd.automount,noatime
Type=nfs
TimeoutSec=30

[Install]
WantedBy=multi-user.target
```

**Tip:** In case of an unreachable system, [append](/index.php/Append "Append") `ForceUnmount=true` to `[Mount]`, allowing the share to be (force-)unmounted.

To use `mnt-myshare.mount`, [start](/index.php/Start "Start") the unit and [enable](/index.php/Enable "Enable") it to run on system boot.

#### Mount using autofs

Using [autofs](/index.php/Autofs "Autofs") is useful when multiple machines want to connect via NFS; they could both be clients as well as servers. The reason this method is preferable over the earlier one is that if the server is switched off, the client will not throw errors about being unable to find NFS shares. See [autofs#NFS network mounts](/index.php/Autofs#NFS_network_mounts "Autofs") for details.

## Tips and tricks

### Performance tuning

When using NFS on a network with a significant number of clients one may increase the default NFS threads from *8* to *16* or even a higher, depending on the server/network requirements:

 `/etc/nfs.conf` 
```
[nfsd]
threads=16
```

It may be necessary to tune the `rsize` and `wsize` mount options to meet the requirements of the network configuration.

In recent linux kernels (>2.6.18) the size of I/O operations allowed by the NFS server (default max block size) varies depending on RAM size, with a maximum of 1M (1048576 bytes), the max block size of the server will be used even if nfs clients requires bigger `rsize` and `wsize`. See [https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/5.8_Technical_Notes/Known_Issues-kernel.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/5.8_Technical_Notes/Known_Issues-kernel.html) It is possible to change the default max block size allowed by the server by writing to the `/proc/fs/nfsd/max_block_size` before starting *nfsd*. For example, the following command restores the previous default iosize of 32k:

```
# echo 32768 > /proc/fs/nfsd/max_block_size

```

To make the change permanent, create a [systemd-tmpfile](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/nfsd-block-size.conf` 
```
w /proc/fs/nfsd/max_block_size - - - - 32768

```

To mount with the increased `rsize` and `wsize` mount options:

```
# mount -t nfs -o rsize=32768,wsize=32768,vers=4 servername:/srv/nfs/music /mountpoint/on/client

```

### Automatic mount handling

This trick is useful for NFS-shares on a [wireless](/index.php/Wireless "Wireless") network and/or on a network that may be unreliable. If the NFS host becomes unreachable, the NFS share will be unmounted to hopefully prevent system hangs when using the `hard` mount option [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1260240#p1260240).

Make sure that the NFS mount points are correctly indicated in [fstab](/index.php/Fstab "Fstab"):

 `/etc/fstab` 
```
lithium:/mnt/data           /mnt/data	        nfs noauto,noatime 0 0
lithium:/var/cache/pacman   /var/cache/pacman	nfs noauto,noatime 0 0
```

**Note:**

*   Use hostnames in [fstab](/index.php/Fstab "Fstab") for this to work, not IP addresses.
*   In order to mount NFS shares with non-root users the `users` option has to be added.
*   The `noauto` mount option tells [systemd](/index.php/Systemd "Systemd") to not automatically [mount](/index.php/Mount "Mount") the shares at boot, otherwise this may causing the boot process to stall.

Create the `auto_share` script that will be used by [cron](/index.php/Cron "Cron") or [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") to use ICMP ping to check if the NFS host is reachable:

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

**Note:** Test using a TCP probe instead of ICMP ping (default is tcp port 2049 in NFS4) then replace the line:
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

Make sure the script is [executable](/index.php/Executable "Executable"):

```
# chmod +x /usr/local/bin/auto_share

```

Next check configure the script to run every X, in the examples below this is every minute.

#### Cron

 `# crontab -e` 
```
* * * * * /usr/local/bin/auto_share

```

#### systemd/Timers

 `/etc/systemd/system/auto_share.timer` 
```
[Unit]
Description=Automount NFS shares every minute

[Timer]
OnCalendar=*-*-* *:*:00

[Install]
WantedBy=timers.target
```
 `/etc/systemd/system/auto_share.service` 
```
[Unit]
Description=Automount NFS shares
After=syslog.target network.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/auto_share

[Install]
WantedBy=multi-user.target
```

Finally, [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `auto_share.timer`.

#### Using a NetworkManager dispatcher

[NetworkManager](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") can also be configured to run a script on network status change.

The easiest method for mount shares on network status change is to symlink the `auto_share` script:

```
# ln -s /usr/local/bin/auto_share /etc/NetworkManager/dispatcher.d/30-nfs.sh

```

However, in that particular case unmounting will happen only after the network connection has already been disabled, which is unclean and may result in effects like freezing of KDE Plasma applets.

The following script safely unmounts the NFS shares before the relevant network connection is disabled by listening for the `pre-down` and `vpn-pre-down` events, make the script is [executable](/index.php/Executable "Executable"):

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

**Note:** This script ignores mounts with the `noauto` option, remove this mount option or use `auto` to allow the dispatcher to manage these mounts.

Create a symlink inside `/etc/NetworkManager/dispatcher.d/pre-down` to catch the `pre-down` events:

```
# ln -s /etc/NetworkManager/dispatcher.d/30-nfs.sh /etc/NetworkManager/dispatcher.d/pre-down.d/30-nfs.sh

```

## Troubleshooting

There is a dedicated article [NFS/Troubleshooting](/index.php/NFS/Troubleshooting "NFS/Troubleshooting").

## See also

*   See also [Avahi](/index.php/Avahi "Avahi"), a Zeroconf implementation which allows automatic discovery of NFS shares.
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [NFS on Snow Leopard](https://blogs.oracle.com/jag/entry/nfs_on_snow_leopard) (Dead Link => [Archive.org Mirror](https://web.archive.org/web/20151212160906/https://blogs.oracle.com/jag/entry/nfs_on_snow_leopard))
*   [http://chschneider.eu/linux/server/nfs.shtml](http://chschneider.eu/linux/server/nfs.shtml)
*   [How to do Linux NFS Performance Tuning and Optimization](https://www.slashroot.in/how-do-linux-nfs-performance-tuning-and-optimization)
*   [Linux: Tune NFS Performance](https://www.cyberciti.biz/faq/linux-unix-tuning-nfs-server-client-performance/)