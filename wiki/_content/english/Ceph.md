Ceph is a storage platform with a focus on being distributed, resilient, and having good performance and high reliability. Ceph can also be used as a block storage solution for [virtual machines](https://en.wikipedia.org/wiki/Virtual_Machine "wikipedia:Virtual Machine") or through the use of [FUSE](/index.php/File_systems#FUSE-based_file_systems "File systems"), a conventional filesystem. Ceph is extremely configurable, with administrators being able to control virtually all aspects of the system. A command line interface is used to monitor and control the cluster. The platform also contains authentication & authorization features, and various gateways to make it compatible with systems such as [OpenStack Swift](https://en.wikipedia.org/wiki/OpenStack#Swift "wikipedia:OpenStack") and [Amazon S3](https://en.wikipedia.org/wiki/Amazon_S3 "wikipedia:Amazon S3").

From [Wikipedia: Ceph (software)](https://en.wikipedia.org/wiki/Ceph_(software) "wikipedia:Ceph (software)"):

	Ceph is a free software storage platform designed to present object, block, and file storage from a single distributed computer cluster. Ceph's main goals are to be completely distributed without a single point of failure, scalable to the exabyte level, and freely-available. The data is replicated, making it fault tolerant.

From [Ceph.com](https://ceph.com/):

	Ceph is a distributed object store and file system designed to provide excellent performance, reliability and scalability.

**Warning:** The recommended installation method for Ceph is via an [upstream tool](https://github.com/ceph/ceph-deploy) which uses [SSH](/index.php/SSH "SSH") to connect to machines with the purpose of automatically installing, configuring, and managing Ceph. The upstream tool (ceph-deploy) does not currently support [Arch Linux](/index.php/Arch_Linux "Arch Linux"). Until ceph-deploy includes support for Arch Linux, it is not possible to use the [quick installation method](http://ceph.com/docs/master/start/) due to the extensive use of the tool. The only other officially documented installation method is the [manual deployment guide](http://ceph.com/docs/master/install/manual-deployment/). This article therefore documents the manual procedure until Arch Linux is supported by the quick method.

The official documentation [states](http://ceph.com/docs/master/install/#deploy-a-cluster-manually) "the manual procedure is primarily for exemplary purposes for those developing deployment scripts with Chef, Juju, Puppet, etc.".

## Contents

*   [1 Terminology](#Terminology)
*   [2 Installation](#Installation)
    *   [2.1 Packages](#Packages)
    *   [2.2 NTP Client](#NTP_Client)
*   [3 Bootstrapping a storage cluster](#Bootstrapping_a_storage_cluster)
    *   [3.1 Starting a monitor](#Starting_a_monitor)
*   [4 See also](#See_also)

## Terminology

**Note:** A full glossary is available in the [official documentation](http://ceph.com/docs/master/glossary/).

*   **Client** : Something which connects to a Ceph cluster to access data but is not part of the Ceph cluster itself.
*   **MONs** : Also known as monitors, these store cluster state and maps containing information about the cluster such as running services and data locations.
*   **MDSs** : Also known as metadata servers, these store metadata for the Ceph filesystem to reduce load on the storage cluster (e.g. information for commands such as `ls`).
*   **Node** : A machine which is running Ceph services, such as OSDs or MONs.
*   **OSDs** : Also known as OSD daemons, these are responsible for the storage of data within the cluster and also conduct various related operations such as replication, recovery, and rebalancing.
*   **Storage cluster** : The core set of software responsible for storing data (OSDs+MONs).

## Installation

### Packages

Install it with the package [ceph](https://www.archlinux.org/packages/?name=ceph), available in the [official repositories](/index.php/Official_repositories "Official repositories"). You may instead install [ceph-git](https://aur.archlinux.org/packages/ceph-git/) if you want a bleeding-edge installation.

The Ceph's official cluster deployment tool is available as [ceph-deploy](https://aur.archlinux.org/packages/ceph-deploy/).

Install [ceph](https://www.archlinux.org/packages/?name=ceph) on all nodes that will be in the cluster.

### NTP Client

**Warning:** You should synchronise the clocks on your monitor nodes to prevent clock drift (see [Time#Time skew](/index.php/Time#Time_skew "Time") for details), which can degrade the performance of your cluster or stop it from functioning entirely. The [official documentation](http://docs.ceph.com/docs/master/rados/configuration/mon-config-ref/#clock:) recommends that nodes run some form of clock synchronisation.

Install and run a time synchronisation client on the node. See [Time#Time synchronization](/index.php/Time#Time_synchronization "Time") for details.

## Bootstrapping a storage cluster

Before a storage cluster can operate, the monitors for that cluster must be bootstrapped with several identifiers and keyrings.

The upstream Ceph documentation is well-written and kept updated with the latest releases.

To boostrap a storage cluster, follow the steps documented in the [official manual deployment guide](http://ceph.com/docs/master/install/manual-deployment/#monitor-bootstrapping).

### Starting a monitor

Since your system most likely uses [systemd](/index.php/Systemd "Systemd"), you can enable a monitor as a systemd unit.

As an example, for a monitor named `node1` start and enable `ceph-mon@node1.service` as detailed in [Systemd#Using units](/index.php/Systemd#Using_units "Systemd").

## See also

*   Official site
    *   [Homepage](https://ceph.com)
    *   [Documentation](http://ceph.com/docs/master/)
*   Official source code
    *   [GitHub organization](https://github.com/ceph)
    *   [Ceph](https://github.com/ceph/ceph)