**翻译状态：** 本文是英文页面 [ISCSI_Initiator](/index.php/ISCSI_Initiator "ISCSI Initiator") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-05-10，点击[这里](https://wiki.archlinux.org/index.php?title=ISCSI_Initiator&diff=0&oldid=332214)可以查看翻译后英文页面的改动。

来自 [维基百科：iSCSI](https://en.wikipedia.org/wiki/iSCSI "wikipedia:iSCSI") 可以通过基于 IP 的网络访问存储设备。

提供受访的实体是 目标(target)，发起访问的实体称为 发起者(initiator)。

本文讲述如何通过 [Open-iSCSI](http://open-iscsi.org/) 的 initiator 访问 iSCSI target。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 概览](#.E6.A6.82.E8.A7.88)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 启动服务](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1)
    *   [3.2 发现目标](#.E5.8F.91.E7.8E.B0.E7.9B.AE.E6.A0.87)
    *   [3.3 删除废旧目标](#.E5.88.A0.E9.99.A4.E5.BA.9F.E6.97.A7.E7.9B.AE.E6.A0.87)
    *   [3.4 登录到有效的目标](#.E7.99.BB.E5.BD.95.E5.88.B0.E6.9C.89.E6.95.88.E7.9A.84.E7.9B.AE.E6.A0.87)
    *   [3.5 信息](#.E4.BF.A1.E6.81.AF)
    *   [3.6 在线修改卷大小](#.E5.9C.A8.E7.BA.BF.E4.BF.AE.E6.94.B9.E5.8D.B7.E5.A4.A7.E5.B0.8F)
*   [4 提示与排错](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8E.92.E9.94.99)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

可以从 [官方源](/index.php/Official_repositories "Official repositories") [安装](/index.php/Pacman "Pacman") 软件包。

**注意:** 旧版的 initiator,[Linux-iSCSI](http://sourceforge.net/projects/linux-iscsi/) 已经于二零零五年四月合并进 Open-iSCSI 。 This should not be confused with [linux-iscsi.org](http://linux-iscsi.org/), the website for the LIO [target](/index.php/ISCSI_Target "ISCSI Target").

## 概览

下图显示各组件是如何协同工作的。更详细的版本参见：[Open-iSCSI 模块](http://www.open-iscsi.org/docs/open-iscsi-0.jpg)

```
 +-------------------------------------------------------+             
 | Targets & Sessions configuration Database (DBM based) |             
 +-------------------------------------------------------+             

 +--------------------------+     +----------------------------------+ 
 | iscsiadm                 |     | iscsid: iSCSI daemon             | 
 |                          |     |                                  | 
 |  * Command line tool     |<--->|  * Implements Session management | 
 |  * Manages database of   |     |  * Communicates with iscsiadm    | 
 |    sessions and targets  |     |    and iscsi kernel modules      | 
 +--------------------------+     +---------------+------------------+ 
                                                  |                    
 User space                                       |                    
- - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - -
 Kernel                                           v                    
         +-----------------------------------------------------------+ 
         | kernel modules: scsi_transport_iscsi, iscsi_tcp, libiscsi | 
         +-----------------------------------------------------------+ 

```

来自 Open-iSCSI [README](http://www.open-iscsi.org/docs/README):

持久化的配置通过一个 DBM 数据库实现，它包括两个表：

*   发现表（Discovery table）(/etc/iscsi/send_targets)
*   节点表（Node table）(/etc/iscsi/nodes)

## 配置

### 启动服务

`iscsid` 由一个 systemd单元 来管理。

[用 systemd](/index.php/Systemd#Using_units "Systemd") 启动 `open-iscsi.service` 。

You only have to include the IP of the [target](/index.php/ISCSI_Target "ISCSI Target") as `SERVER` in `/etc/conf.d/open-iscsi` at the client.

### 发现目标

 `# iscsiadm -m discovery -t sendtargets -p <portalip>` 

### 删除废旧目标

 `# iscsiadm -m discovery -p <portalip> -o delete` 

### 登录到有效的目标

 `# iscsiadm -m node -L all` 

或者，登录到指定目标

 `# iscsiadm -m node --targetname=<targetname> --login` 

登出：

 `# iscsiadm -m node -U all` 

### 信息

对于运行中的会话

 `# iscsiadm -m session -P 3` 

上面命令输出的最后一行会显示连接到的设备名，比如

 `Attached scsi disk **sdd** State: running` 

对于已知节点

 `# iscsiadm -m node` 

### 在线修改卷大小

如果 iscsi 块设备包含一个分区表，则不能在线修改卷大小。这种情况下必须首先卸载文件系统，然后再调整相关分区的大小。

1.  重新扫描当前会话中的活动节点。 `# iscsiadm -m node -R` 
2.  在多路径环境中，也必须重新扫描多路径下的卷信息。 `# multipathd -k"resize map sdx"` 
3.  完成后再调整文件系统大小。 `# resize2fs /dev/sdx` 

## 提示与排错

可以用下列命令检查已连接的 iSCSI 设备在 /dev 设备树中的位置： `ls -lh /dev/disk/by-path/*` 。

在服务器端(target)的 acl 配置中应当包含客户端的 iqn（位于客户端的 `/etc/iscsi/initiatorname.iscsi`）。

`iscsiadm` 的许多操作要求 iSCSI 的守护进程 `iscsid` 处于运行状态。To verify that this is the case, [check the status](/index.php/Systemd#Using_units "Systemd") of the `open-iscsi.service`.

## 参阅

*   [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot") Booting Arch Linux with / on an iSCSI target.