**翻译状态：** 本文是英文页面 [Ceph](/index.php/Ceph "Ceph") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-13，点击[这里](https://wiki.archlinux.org/index.php?title=Ceph&diff=0&oldid=419278)可以查看翻译后英文页面的改动。

Ceph 是一个专注于分布式的、弹性可扩展的、高可靠的、性能优异的存储系统平台，可用于为[虚拟机](https://en.wikipedia.org/wiki/Virtual_Machine "wikipedia:Virtual Machine")提供块存储方案或通过 [FUSE](/index.php/File_systems#FUSE-based_file_systems "File systems") 提供常规的文件系统。Ceph 是个高度可配置的系统，管理者可以控制系统的各个方面。它提供了一个命令行界面用于监视和控制其存储集群。Ceph 也包含鉴证和授权功能，可兼容多种存储网关接口如 [OpenStack Swift](https://en.wikipedia.org/wiki/OpenStack#Swift "wikipedia:OpenStack") 和 [Amazon S3](https://en.wikipedia.org/wiki/Amazon_S3 "wikipedia:Amazon S3").

引自 [Wikipedia: Ceph (software)](https://en.wikipedia.org/wiki/Ceph_(software) "wikipedia:Ceph (software)"):

	Ceph is a free software storage platform designed to present object, block, and file storage from a single distributed computer cluster. Ceph's main goals are to be completely distributed without a single point of failure, scalable to the exabyte level, and freely-available. The data is replicated, making it fault tolerant.

引自 [Ceph.com](https://ceph.com/):

	Ceph is a distributed object store and file system designed to provide excellent performance, reliability and scalability.

**警告:** 推荐使用[官方部署工具](https://github.com/ceph/ceph-deploy)安装 Ceph 。该工具通过 [SSH](/index.php/SSH "SSH") 连接到目标机器并自动完成安装、配置和系统管理。官方部署工具(ceph-deploy)目前尚不支持 [Arch Linux](/index.php/Arch_Linux "Arch Linux") ，不能使用 [快速安装方式](http://ceph.com/docs/master/start/) 部署，只能按官方文档[手工部署](http://ceph.com/docs/master/install/manual-deployment/)。因此本文目前仅介绍手工部署方法。

The official documentation [states](http://ceph.com/docs/master/install/#deploy-a-cluster-manually) "the manual procedure is primarily for exemplary purposes for those developing deployment scripts with Chef, Juju, Puppet, etc.".

## Contents

*   [1 术语](#.E6.9C.AF.E8.AF.AD)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 软件包](#.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.2 NTP 客户端](#NTP_.E5.AE.A2.E6.88.B7.E7.AB.AF)
*   [3 启动一个存储集群](#.E5.90.AF.E5.8A.A8.E4.B8.80.E4.B8.AA.E5.AD.98.E5.82.A8.E9.9B.86.E7.BE.A4)
    *   [3.1 启动一个监视器](#.E5.90.AF.E5.8A.A8.E4.B8.80.E4.B8.AA.E7.9B.91.E8.A7.86.E5.99.A8)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 术语

**提示:** [官方文档](http://ceph.com/docs/master/glossary/)提供了完整的术语表

*   **Client** : Something which connects to a Ceph cluster to access data but is not part of the Ceph cluster itself.
*   **MONs** : Also known as monitors, these store cluster state and maps containing information about the cluster such as running services and data locations.
*   **MDSs** : Also known as metadata servers, these store metadata for the Ceph filesystem to reduce load on the storage cluster (e.g. information for commands such as `ls`).
*   **Node** : A machine which is running Ceph services, such as OSDs or MONs.
*   **OSDs** : Also known as OSD daemons, these are responsible for the storage of data within the cluster and also conduct various related operations such as replication, recovery, and rebalancing.
*   **Storage cluster** : The core set of software responsible for storing data (OSDs+MONs).

## 安装

### 软件包

可以从 [官方源](/index.php/Official_repositories "Official repositories") 安装[ceph](https://www.archlinux.org/packages/?name=ceph)。如果愿意冒险，也可以安装开发版的 [ceph-git](https://aur.archlinux.org/packages/ceph-git/)。

[ceph-deploy](https://aur.archlinux.org/packages/ceph-deploy/)提供了 Ceph 的官方部署工具。

存储集群的所有节点都要安装 [ceph](https://www.archlinux.org/packages/?name=ceph)。

### NTP 客户端

**警告:** 应当同步监视器节点的时钟以避免时钟偏移(详见 [Time (简体中文)#时间偏移](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.97.B6.E9.97.B4.E5.81.8F.E7.A7.BB "Time (简体中文)"))，否则将导致集群性能下降甚至停止工作。[官方文档](http://docs.ceph.com/docs/master/rados/configuration/mon-config-ref/#clock:) 建议所有节点都应采取某种方式同步时钟。

在节点上安装并运行时钟同步客户端，可参阅 [Time (简体中文)#时间同步](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.97.B6.E9.97.B4.E5.90.8C.E6.AD.A5 "Time (简体中文)")。

## 启动一个存储集群

Before a storage cluster can operate, the monitors for that cluster must be bootstrapped with several identifiers and keyrings.

The upstream Ceph documentation is well-written and kept updated with the latest releases.

To boostrap a storage cluster, follow the steps documented in the [official manual deployment guide](http://ceph.com/docs/master/install/manual-deployment/#monitor-bootstrapping).

### 启动一个监视器

Since your system most likely uses [systemd](/index.php/Systemd "Systemd"), you can enable a monitor as a systemd unit.

As an example, for a monitor named `node1` start and enable `ceph-mon@node1.service` as detailed in [Systemd#Using units](/index.php/Systemd#Using_units "Systemd").

## 参阅

*   官方网站
    *   [主页](https://ceph.com)
    *   [文档](http://ceph.com/docs/master/)
*   官方源码下载
    *   [GitHub organization](https://github.com/ceph)
    *   [Ceph](https://github.com/ceph/ceph)