**翻译状态：** 本文是英文页面 [ISCSI_Target](/index.php/ISCSI_Target "ISCSI Target") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-06-11，点击[这里](https://wiki.archlinux.org/index.php?title=ISCSI_Target&diff=0&oldid=373078)可以查看翻译后英文页面的改动。

使用 [iSCSI](https://en.wikipedia.org/wiki/iSCSI "wikipedia:iSCSI") 可以通过 IP 网络访问磁盘。

接受来访的实体称为 **目标(target)**，发起访问的实体称为 **[发起者(initiator)](/index.php/ISCSI_Initiator "ISCSI Initiator")**。有多种设置目标的方式：

*   [SCSI Target Framework (STGT/TGT)](http://stgt.berlios.de/) 是 Linux 2.6.38 之前的标准。
*   [LIO target](http://linux-iscsi.org/) 是现在的标准。
*   [iSCSI Enterprise Target (IET)](http://iscsitarget.sourceforge.net/) 是旧版本的实现，[SCSI Target Subsystem (SCST)](http://scst.sourceforge.net/) 是 IET 的升级版本，曾是 LIO 最终入选内核之前的候选方案之一。

## Contents

*   [1 启用 LIO Target](#.E5.90.AF.E7.94.A8_LIO_Target)
    *   [1.1 使用 targetcli](#.E4.BD.BF.E7.94.A8_targetcli)
        *   [1.1.1 认证](#.E8.AE.A4.E8.AF.81)
            *   [1.1.1.1 禁用认证](#.E7.A6.81.E7.94.A8.E8.AE.A4.E8.AF.81)
            *   [1.1.1.2 设置证书](#.E8.AE.BE.E7.BD.AE.E8.AF.81.E4.B9.A6)
    *   [1.2 使用原生 LIO 工具](#.E4.BD.BF.E7.94.A8.E5.8E.9F.E7.94.9F_LIO_.E5.B7.A5.E5.85.B7)
    *   [1.3 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [1.4 上游文档](#.E4.B8.8A.E6.B8.B8.E6.96.87.E6.A1.A3)
*   [2 使用 SCSI Target Framework (STGT/TGT)](#.E4.BD.BF.E7.94.A8_SCSI_Target_Framework_.28STGT.2FTGT.29)
*   [3 使用 iSCSI Enterprise Target (IET)](#.E4.BD.BF.E7.94.A8_iSCSI_Enterprise_Target_.28IET.29)
    *   [3.1 创建 Target](#.E5.88.9B.E5.BB.BA_Target)
        *   [3.1.1 基于硬盘的 Target](#.E5.9F.BA.E4.BA.8E.E7.A1.AC.E7.9B.98.E7.9A.84_Target)
        *   [3.1.2 基于文件的 Target](#.E5.9F.BA.E4.BA.8E.E6.96.87.E4.BB.B6.E7.9A.84_Target)
    *   [3.2 启动服务](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1)
*   [4 参阅](#.E5.8F.82.E9.98.85)

## 启用 LIO Target

LIO target 包含在2.6.38及以后版本的内核中。但从3.1版才开始包含 iSCSI target fabric。

关键的内核模块是 *target_core_mod* 和 *iscsi_target_mod*，它们应该已内置并自动加载。

强烈建议使用 LIO 的免费分支版本：[targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/)，[python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/) 和 [python-configshell-fb](https://aur.archlinux.org/packages/python-configshell-fb/)。原生包 [targetcli](https://aur.archlinux.org/packages/targetcli/) 虽也有效，但其使用另外的方法保存配置，该方法使用不再推荐的 *lio-utils* 及依赖 *epydoc*。

如果使用免费分支版本，则 [python-rtslib-fb](https://aur.archlinux.org/packages/python-rtslib-fb/) 中包含一个 systemd `target.service` 文件。如果直接使用原生的 *targetcli* 或 *lio-utils*，则在 [lio-utils](https://aur.archlinux.org/packages/lio-utils/) 中包含一个 `/etc/rc.d/target`文件。

用下列命令启动 LIO target： `# systemctl start target` 

这样会加载必要的模块，挂载 configfs 并加载之前保存的 iscsi target 配置。

用下列命令可以显示运行中的配置信息（仅免费分支版有效）: `# targetcli status` 若要 lio target 随系统引导时启动，可用下列命令： `# systemctl enable target` 

可以用 **targetcli** 创建全部配置。不推荐直接使用 **lio utils** 中的 tcm_* 和 lio_* 。

### 使用 targetcli

外部使用手册仅对免费分支版有效。[targetd](https://github.com/agrover/targetd) 尚未进入 AUR ，这取决于该免费分支。

用命令行式的配置工具可以自动生成绝大部分的名称和数值，但也支持自定义。 在配置工具中随时可以输入 `help` 命令查看当前状态可用的命令。

**提示:** 配置工具命令行支持 TAB 键命令补全

**提示:** 配置工具命令行支持 `cd` 命令查看和选择路径
target 启动以后，用下列命令进入配置工具： `# targetcli` 

在配置工具中，用下列命令启用一个块设备（此例为：`/dev/disk/by-id/md-name-nas:iscsi`）作为 target：

```
/> cd backstores/block
/backstores/block> create md_block0 /dev/disk/by-id/md-name-nas:iscsi
```

**注意:** 任何块设备都可以用做 target，包括 RAID 和 LVM 设备。如果用 fileio 替换了 block，也可以将文件用作 target。

然后，用下列命令创建一个“iSCSI 合格名称“（iSCSI Qualified Name，即 iqn）和一个 target 入口组（target portal group，tpg)

```
...> cd /iscsi
/iscsi> create
```

**注意:** With appending an iqn of your choice to create you can keep targetcli from automatically creating an iqn

In order to tell LIO that your block device should get used as *backstore* for the target you issue

**注意:** 别忘了可以用 `cd` 命令选择 <iqn>/tpg1 路径

```
.../tpg1> cd luns
.../tpg1/luns> create /backstores/block/md_block0
```

接下来需要创建一个*入口(portal)*，以使守护进程监听传入连接：

```
.../luns/lun0> cd ../../portals
.../portals> create
```

Targetcli 将会告诉你 LIO 监听传入连接的 IP 地址和端口（默认是 0.0.0.0，即全部地址）。 需要为客户端提供至少一个 IP 地址。端口应当是标准的 3260 。

为了让客户端/[发起者](/index.php/ISCSI_Initiator "ISCSI Initiator")能够连接，需要把发起者的 iqn 写入 target 的配置中：

```
...> cd ../../acls
.../acls> create iqn.2005-03.org.open-iscsi:SERIAL
```

将上面命令中的 `iqn.2005-03.org.open-iscsi:SERIAL` 换成所用的发起者的 iqn ，通常位于 `/etc/iscsi/initiatorname.iscsi`。 每个将要接入的发起者都必须如此配置一遍。 Targetcli 将自动把最新创建的 acl 映射到已创建的 lun 。

**注意:** 所映射的 lun 及其访问权限为 rw 或是 ro 都是可修改的。在配置工具中用 `help create` 命令查阅说明。

所有配置工作完成后的最后一步是保存配置：

```
...> cd /
/> saveconfig

```

配置数据将保存在 `/etc/target/saveconfig.json` 文件中。 现在就可以安全地启动或停止 `target.service` 而不会丢失做好的配置数据了。

**提示:** 可以给出一个文件名作为 `saveconfig` 命令的参数，也可以用 `clearconfig` 命令清除配置

#### 认证

Authentication per CHAP is enabled per default for your targets. 也可以设置口令或禁用认证。

##### 禁用认证

在配置工具中进入所创建的 target 路径（例如 /iscsi/iqn.../tpg1），输入下列命令：

```
.../tpg1> set attribute authentication=0

```

**警告:** 这样设置会导致任何获得了任一客户端（发起者）iqn 的人都可以访问 target。因此仅可用于测试或自用。

##### 设置证书

在配置工具中进入某个选定 target 的 acl 路径 (例如 /iscsi/iqn.../tpg1/acls/iqn.../) 。下列命令将显示当前的认证证书：

```
...> get auth

```

下列命令将以 foo:bar 启用认证：

```
...> set auth userid=foo
...> set auth password=bar

```

### 使用原生 LIO 工具

You have to install [lio-utils](https://aur.archlinux.org/packages/lio-utils/) from [AUR](/index.php/AUR "AUR") and the dependencies (python2).

### 提示与技巧

*   使用 `targetcli sessions` 命令可以列出当前已打开的会话。这个命令包含在 [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/) 软件包中，但没有包含在 *lio-utils* 或原生的 *targetcli* 中。

### 上游文档

*   [targetcli](http://www.linux-iscsi.org/wiki/Targetcli)
*   [LIO utils](http://www.linux-iscsi.org/wiki/Lio-utils_HOWTO)
*   You can also use `man targetcli` when you installed the *free branch* version [targetcli-fb](https://aur.archlinux.org/packages/targetcli-fb/).

## 使用 SCSI Target Framework (STGT/TGT)

You will need the Package [tgt](https://aur.archlinux.org/packages/tgt/) from [AUR](/index.php/AUR "AUR").

See: [TGT iSCSI Target](/index.php/TGT_iSCSI_Target "TGT iSCSI Target")

## 使用 iSCSI Enterprise Target (IET)

You will need [iscsitarget-kernel](https://aur.archlinux.org/packages/iscsitarget-kernel/) and [iscsitarget-usr](https://aur.archlinux.org/packages/iscsitarget-usr/) from [AUR](/index.php/AUR "AUR").

### 创建 Target

Modify /etc/iet/ietd.conf accordingly

#### 基于硬盘的 Target

```
Target iqn.2010-06.ServerName:desc
Lun 0 Path=/dev/sdX,Type=blockio

```

#### 基于文件的 Target

Use "dd" to create a file of the required size, this example is 10GB.

```
dd if=/dev/zero of=/root/os.img bs=1G count=10

```

```
Target iqn.2010-06.ServerName:desc
Lun 0 Path=/root/os.img,Type=fileio

```

### 启动服务

```
rc.d start iscsi-target

```

Also you can "iscsi-target" to DAEMONS in /etc/rc.conf so that it starts up during boot.

## 参阅

*   [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot") Booting Arch Linux with / on an iSCSI target.
*   [Persistent block device naming (简体中文)](/index.php/Persistent_block_device_naming_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Persistent block device naming (简体中文)") 给 target 赋予正确的块设备名称