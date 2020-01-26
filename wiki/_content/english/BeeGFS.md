Related articles

*   [Ceph](/index.php/Ceph "Ceph")
*   [GlusterFS](/index.php/GlusterFS "GlusterFS")
*   [File Systems](/index.php/File_Systems "File Systems")

BeeGFS is a scalable network-storage platform with a focus on being distributed, resilient, highly configurable and having good performance and high reliability. BeeGFS is extremely configurable, with administrators being able to control virtually all aspects of the system. A command line interface is used to monitor and control the cluster.

From [Wikipedia: BeeGFS (software)](https://en.wikipedia.org/wiki/BeeGFS_(software) "wikipedia:BeeGFS (software)"):

	BeeGFS (formerly FhGFS) is a parallel file system, developed and optimized for high-performance computing. BeeGFS includes a distributed metadata architecture for scalability and flexibility reasons. Its most important aspect is data throughput. BeeGFS was originally developed at the [Fraunhofer Center for High Performance Computing](https://www.itwm.fraunhofer.de/en/departments/hpc.html) in Germany by a team around Sven Breuner, who later became the CEO of [ThinkParQ](https://thinkparq.com/), the spin-off company that was founded in 2014 to maintain BeeGFS and offer professional services.

From [BeeGFS.io](https://beegfs.io/):

	BeeGFS is the leading parallel cluster file system, developed with a strong focus on performance and designed for very easy installation and management. If I/O intensive workloads are your problem, BeeGFS is the solution.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Terminology](#Terminology)
*   [2 Installation](#Installation)
    *   [2.1 Example cluster deployment](#Example_cluster_deployment)
    *   [2.2 NTP client](#NTP_client)
    *   [2.3 Management server](#Management_server)
    *   [2.4 Monitoring server](#Monitoring_server)
        *   [2.4.1 Configuration of default Grafana panels](#Configuration_of_default_Grafana_panels)
        *   [2.4.2 Accessing Grafana panels](#Accessing_Grafana_panels)
    *   [2.5 Metadata server](#Metadata_server)
    *   [2.6 Storage server](#Storage_server)
    *   [2.7 Client](#Client)
    *   [2.8 Utilities](#Utilities)
        *   [2.8.1 Check connectivity](#Check_connectivity)
*   [3 Server tuning and advanced features](#Server_tuning_and_advanced_features)
    *   [3.1 InfiniBand Support](#InfiniBand_Support)
    *   [3.2 ACLs](#ACLs)
    *   [3.3 Storage Pools](#Storage_Pools)
    *   [3.4 Quota Enforcement](#Quota_Enforcement)
    *   [3.5 High Availability](#High_Availability)
*   [4 See also](#See_also)

## Terminology

**Tip:** A full glossary is available in the [official documentation](https://www.beegfs.io/wiki/PageIndex).

| Node Type and Description | Packages |
| **Management Server (one node)**

*   Manages configuration and group membership
*   Hostname or IP address must be known by other nodes at service start time

 | [beegfs-mgmtd](https://aur.archlinux.org/packages/beegfs-mgmtd/) |
| **Metadata Server (at least one node)**

*   Stores directory information and allocates file space on storage servers

 | [beegfs-meta](https://aur.archlinux.org/packages/beegfs-meta/) |
| **Storage Server (at least one node)**

*   Stores raw file contents

 | [beegfs-storage](https://aur.archlinux.org/packages/beegfs-storage/) |
| **InfluxDB / Grafana based Monitoring Server (optional)**

*   Continuous monitoring of servers
*   Live statistics
*   beegfs-admon (Java based administration and monitoring GUI), must not be installed on the same server

 | [beegfs-mon](https://aur.archlinux.org/packages/beegfs-mon/) |
| **BeeGFS utilities for administrators**

*   `beegfs-ctl` tool for command-line administration
*   `beegfs-fsck` tool for file system checking
*   Several small helper scripts such logging and [DNS](/index.php/DNS "DNS") lookup functionality

 | [beegfs-utils](https://aur.archlinux.org/packages/beegfs-utils/) |
| **BeeGFS Common**

*   Common files for all packages
*   Enables support for remote direct memory access [rdma-core](https://aur.archlinux.org/packages/rdma-core/) based on the [OpenFabrics IBVerbs API](https://www.openfabrics.org/), through `libbeegfs-ib`.

 | [beegfs-common](https://aur.archlinux.org/packages/beegfs-common/) |
| **Client**

*   Kernel module to mount the file system
*   Requires userspace helper daemon for logging and [hostname](/index.php/Hostname "Hostname") resolution

 | [beegfs-client](https://aur.archlinux.org/packages/beegfs-client/) |

In addition to the free and open-source packages described here, BeeGFS also offers a number of [Enterprise Features and Professional Support](https://www.beegfs.io/content/support/), which include:

*   High Availability
*   Quota Enforcement
*   Access Control Lists (ACLs)
*   Storage Pools
*   Burst buffer function with BeeOND

**Warning:** Whilst the BeeGFS server components are userspace daemons, the client is a native kernel module. The [latest version of BeeGFS v7.1.3 has support for Kernels up to 4.19.x](https://www.beegfs.io/release/beegfs_7_1/Changelog.txt). Hence there are a number of adhoc patches to the client source build files included in the [beegfs-client](https://aur.archlinux.org/packages/beegfs-client/) [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). This in turn may lead to instability with the client kernel module.

## Installation

### Example cluster deployment

The following hardware configuration will be used in this example:

| Hostname | IP Address | Description |
| node01 | `192.168.0.1` | Management Server and Monitoring (optional) Server |
| node02 | `192.168.0.2` | Metadata Server |
| node03 | `192.168.0.3` | Storage Server |
| node04 | `192.168.0.4` | Client |

**Tip:** One if free to choose the option of using dedicated hosts for all BeeGFS services. BeeGFS allows running any combination of services (including client and storage/metadata service) on the same machine. Especially the management and mon daemons are not performance-critical and thus are typically not running on dedicated machines.

### NTP client

[Install](/index.php/Pacman#Installing_packages "Pacman") and run a time synchronization client on all the nodes. See [Time synchronization](/index.php/Time_synchronization "Time synchronization") for details.

**Note:** It is strongly recommended to synchronize the clocks on all cluster nodes to prevent clock drift (see [System time#Time skew](/index.php/System_time#Time_skew "System time") for details), which can degrade the performance of your cluster or stop it from functioning altogether. The [official documentation](https://www.beegfs.io/wiki/ManualInstallWalkThrough#hn_59ca4f8bbb_10:) recommends that nodes run some form of clock synchronization.

### Management server

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") it with the package [beegfs-mgmtd](https://aur.archlinux.org/packages/beegfs-mgmtd/) on the management node `192.168.0.1`.

The management service needs to know where it can store its data. It will only store some node information like connectivity data, so it will not require much storage space and its data access is not performance critical. Thus, this service is typically not running on a dedicated machine.

 `/etc/beegfs/beegfs-mgmtd`  `storeMgmtdDirectory = /mnt/beegfs/beegfs-mgmtd` 

[Start/enable](/index.php/Start/enable "Start/enable") the `beegfs-mgmtd.service` on the management node:

```
 # systemctl start beegfs-mgmtd@node01.service
 # systemctl enable beegfs-mgmtd@node01.service

```

### Monitoring server

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package [beegfs-mon](https://aur.archlinux.org/packages/beegfs-mon/) on the management/monitoring node `192.168.0.1`, which collects statistics from the system and provides them to the user using a time series database [InfluxDB](/index.php/InfluxDB "InfluxDB"). For visualization of the data `beegfs-mon` provides predefined [Grafana](/index.php/Grafana "Grafana") panels that can be used out of the box.

Before running `beegfs-mon`, you need to edit the configuration file `/etc/beegfs/beegfs-mon.conf`. If you have everything installed on the same host, you only need to specify the management host:

 `/etc/beegfs/beegfs-mon.conf`  `sysMgmtHost = localhost` 
**Tip:** If your InfluxDB is installed on another host, say the `client` for example or you need to use a different database port or name, you also need to modify the corresponding entries: `/etc/beegfs/beegfs-mon.conf` 
```
dbHostName = node04
dbHostPort = 9096
dbHostName = beegfs_mon_client
```

[Start/enable](/index.php/Start/enable "Start/enable") the `beegfs-mon.service` on the management/monitoring node:

```
 # systemctl start beegfs-mon@node01.service
 # systemctl enable beegfs-mon@node01.service

```

#### Configuration of default [Grafana](/index.php/Grafana "Grafana") panels

You can use the provided installation script for default [InfluxDB](/index.php/InfluxDB "InfluxDB") and [Grafana](/index.php/Grafana "Grafana") deployments on the same host.

```
 # cd /etc/beegfs/grafana
 # ./import-dashboards default

```

#### Accessing Grafana panels

Access the application on localhost, e.g.: [http://127.0.0.1:3000](http://127.0.0.1:3000) . Refer to [Custom Grafana Panel Configuration](https://www.beegfs.io/wiki/Mon#hn_59ca4f8bbb_5) for non-default installations and for the [Reference to All Metrics monitored](https://www.beegfs.io/wiki/MonDatabaseReference).

**Note:** Different services on the same machine cannot share the same storage directory, so different directories have to be used, i.e. `/mnt/beegfs/beegfs-mgmtd` for management servers and `/mnt/beegfs/beegfs-mon` for monitoring servers.

### Metadata server

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package [beegfs-meta](https://aur.archlinux.org/packages/beegfs-meta/) on the metadata server(s), i.e. `192.168.0.2`.

The metadata service needs to know where it can store its data and where the management service is running. Typically, one will have multiple metadata services running on different machines.

 `/etc/beegfs/beegfs-meta.conf` 
```
sysMgmtdHost = node01
storeMetaDirectory = /mnt/beegfs/beegfs-meta
```

[Start/enable](/index.php/Start/enable "Start/enable") the `beegfs-meta.service` on the metadata node.

```
 # systemctl start beegfs-meta@node02.service
 # systemctl enable beegfs-meta@node02.service

```

### Storage server

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package [beegfs-storage](https://aur.archlinux.org/packages/beegfs-storage/) on the storage server(s), i.e. `192.168.0.3`.

The storage service needs to know where it can store its data and how to reach the management server. Typically, one will have multiple storage services running on different machines and/or multiple storage targets (e.g. multiple [RAID](/index.php/RAID "RAID") volumes) per storage service.

 `/etc/beegfs/beegfs-storage.conf` 
```
sysMgmtdHost = node01
storeStorageDirectory = /mnt/beegfs/beegfs-storage
```

[Start/enable](/index.php/Start/enable "Start/enable") the `beegfs-storage.service` on the storage node.

```
 # systemctl start beegfs-storage@node03.service
 # systemctl enable beegfs-storage@node03.service

```

### Client

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package [beegfs-client](https://aur.archlinux.org/packages/beegfs-client/) on the client node, which will build the client [Kernel module](/index.php/Kernel_module "Kernel module").

The client service needs to know where it can reach the management server.

 `/etc/beegfs/beegfs-client.conf`  `sysMgmtdHost = node01` 

The client service needs to know where it can mount the cluster storage, as well as the location of teh client configuration file.

 `/etc/beegfs/beegfs-mount.conf`  `/mnt/beegfs/beegfs-mount /etc/beegfs/beegfs-client.conf` 

[Load](/index.php/Kernel_module#Manual_module_handling "Kernel module") the Kernel module and its dependencies.

```
 # modprobe beegfs

```

[Start/enable](/index.php/Start/enable "Start/enable") the `beegfs-helperd.service` on the client node:

```
 # systemctl start beegfs-helperd@node04.service
 # systemctl enable beegfs-helperd@node04.service

```

[Start/enable](/index.php/Start/enable "Start/enable") the `beegfs-client.service` on the client node:

```
 # systemctl start beegfs-client.service
 # systemctl enable beegfs-client.service

```

### Utilities

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package [beegfs-utils](https://aur.archlinux.org/packages/beegfs-utils/).

**Tip:** Best to install on either the management server or client node, or both. For the purposes of this example the client node is used.

#### Check connectivity

Check the detected network interfaces and transport protocols from a client node with the following commands:

```
 # beegfs-ctl --listnodes --nodetype=mgmt --nicdetails 
   node01 [ID: 1]
     Ports: UDP: 8008; TCP: 8008
     Interfaces: 
     + enp0s31f6[ip addr: 192.168.0.1; type: TCP]

```

```
 # beegfs-ctl --listnodes --nodetype=meta --nicdetails 
   node02 [ID: 2]
     Ports: UDP: 8005; TCP: 8005
     Interfaces: 
     + eno1[ip addr: 192.168.0.2; type: TCP]

```

```
 # beegfs-ctl --listnodes --nodetype=storage --nicdetails 
   node03 [ID: 3]
     Ports: UDP: 8003; TCP: 8003
     Interfaces: 
     + eno1[ip addr: 192.168.0.3; type: TCP]

```

```
 # beegfs-ctl --listnodes --nodetype=client --nicdetails 
   4E451-5DAEDCBF-node04 [ID: 4]
     Ports: UDP: 8004; TCP: 0
     Interfaces: 
     + wlo1[ip addr: 192.168.0.4; type: TCP]

```

## Server tuning and advanced features

### InfiniBand Support

*   Explicitly [Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") [beegfs-common](https://aur.archlinux.org/packages/beegfs-common/), which will provide `libbeegfs-ib.so` shared object libraries.
*   Enable support for [RDMA-capable network hardware](https://www.beegfs.io/wiki/ManualInstallWalkThrough#hn_59ca4f8bbb_4).
*   Rebuild the [client](#Client) kernel module.

### [ACLs](/index.php/ACL "ACL")

### Storage Pools

### Quota Enforcement

### High Availability

## See also

*   Official site
    *   [Homepage](https://www.beegfs.io/content/)
    *   [Documentation](https://www.beegfs.io/content/documentation/)
*   Official source code
    *   [GitLab BeeGFS](https://git.beegfs.io/pub)
    *   [RPM/DEB Package Build Files](https://www.beegfs.io/content/download/)